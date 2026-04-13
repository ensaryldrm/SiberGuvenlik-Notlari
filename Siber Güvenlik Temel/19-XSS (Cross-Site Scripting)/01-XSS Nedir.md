# Cross-site Scripting (XSS) Zafiyeti ve Temelleri
## 1. Cross-site Scripting (XSS) Nedir?
Cross-site Scripting (XSS), web tabanlı uygulamalarda sıkça karşılaşılan, temelde **istemci tarafında (client-side) kod enjeksiyonuna** dayanan bir güvenlik zafiyetidir. 
* **Çalışma Mantığı:** Saldırganlar, web sayfalarına kötü niyetli JavaScript kodları dahil eder. Web sayfası bir aracı olarak kullanılır ve zafiyet, kurban bu sayfayı ziyaret ettiğinde zararlı kodun kendi tarayıcısında çalışmasıyla tetiklenir.
* **Sık Görüldüğü Yerler:** Kullanıcı girdilerinin alındığı forumlar, arama kutuları, mesaj arayüzleri ve yorum alanları.

---

## 2. XSS Saldırılarının Etkileri ve Tehlikeleri
XSS, basit bir uyarı mesajı (alert) göstermekten çok daha öte, kritik sonuçlar doğurabilen bir zafiyettir:

* **Oturum Çerezlerinin (Cookies) Ele Geçirilmesi:** Otomatik giriş yapmak için kullanılan oturum bilgileri (Session ID) çalınarak yetkisiz hesap erişimi (Account Takeover) sağlanabilir.
* **Hassas Verilerin Sızdırılması:** Form verileri, kredi kartı veya kişisel bilgiler zararlı scriptler aracılığıyla saldırganın sunucusuna gönderilebilir.
* **Web Sayfası İçeriğinin Değiştirilmesi (Defacement):** Sitenin görünümü değiştirilerek kullanıcılara sahte veya zararlı içerik sunulabilir. Kurumsal itibar zedelenir.
* **Yetkisiz İşlemler:** Saldırgan, kurbanın yetkilerini kullanarak kurban adına (yönetici ekleme, veri silme, para transferi) işlemler yapabilir.
* **Sosyal Mühendislik ve Diğer Zafiyetler:** Oltalama (Phishing) kampanyalarına zemin hazırlayabilir veya CSRF gibi farklı zafiyetleri tetiklemek için köprü olarak kullanılabilir.

---

## 3. XSS Saldırı Türleri



XSS saldırıları genel olarak 3 ana kategoriye ayrılır:

1. **Reflected XSS (Kalıcı Olmayan XSS):** Kullanıcıdan alınan girdinin filtrelenmeden doğrudan anlık olarak sayfaya yansıtılmasıdır. Zararlı script genellikle bir URL parametresi ile (örn: `?search=<script>...`) kurbana gönderilir. Kurban linke tıkladığında kod çalışır.
2. **Stored XSS (Kalıcı XSS):** En tehlikeli türdür. Zararlı payload sitenin veri tabanına (örneğin bir blog yorumu olarak) kaydedilir. O sayfayı ziyaret eden *her kullanıcının* tarayıcısında bu script otomatik olarak çalışır.
3. **DOM-based XSS (DOM Tabanlı XSS):** Zararlı script, sunucuya hiç gitmeden, doğrudan kullanıcının tarayıcısında çalışan Document Object Model (DOM) yapısının manipüle edilmesiyle tetiklenir.

---

## 4. XSS Analizinde Bilinmesi Gereken Temel Kavramlar

* **HTML:** Web sayfalarının iskeletini oluşturan işaretleme dilidir.
* **JavaScript (JS):** XSS'in kalbidir. Etkileşimli web sayfaları yaratır ve zararlı kodların çalıştırılmasını sağlar. (Örn: `alert('XSS');`)
* **DOM (Document Object Model):** Tarayıcının HTML'i ağaç yapısında modellediği ve JS ile etkileşime girdiği programlama arayüzüdür.
* **Payload:** Hedefte çalıştırılması amaçlanan, zararlı içeriği taşıyan kod parçasıdır. (Örn: `<script>alert(1)</script>`)
* **CSP (Content Security Policy):** XSS'i önlemek için en güçlü savunma mekanizmalarından biridir. Sitenin dışarıdan hangi kaynaklardan script yükleyebileceğini kısıtlar.
  * *Örnek CSP:* `Content-Security-Policy: script-src 'self' https://apis.example.com`

---

## 5. XSS Saldırılarında Sık Kullanılanlar

### JavaScript Fonksiyonları ve Nesneleri

| JS Metodu | Siber Güvenlikteki Önemi / İşlevi |
| :--- | :--- |
| `alert()`, `prompt()`, `confirm()` | XSS zafiyetinin varlığını kanıtlamak (Proof of Concept - PoC) için sıkça ekrana kutu çıkarmada kullanılır. |
| `document.cookie` | Kullanıcının tarayıcısındaki çerezleri (oturum bilgisi) okumak için kullanılır. Çoğu XSS saldırısının ana hedefidir. |
| `eval()` | Bir metin dizgesini (string) doğrudan JS kodu olarak çalıştırır. Son derece tehlikelidir. |
| `fetch()`, `XMLHttpRequest` | Arka planda kurbanın haberi olmadan saldırganın sunucusuna HTTP isteği (veri hırsızlığı) göndermek için kullanılır. |
| `innerHTML` | DOM üzerinde HTML öğelerinin içeriğini değiştirir, DOM tabanlı XSS'in en büyük sebeplerinden biridir. |
| `localStorage`, `sessionStorage` | Tarayıcıda kalıcı/geçici olarak depolanan hassas token'lara (örn: JWT) erişmek için kullanılır. |
| `setTimeout()`, `setInterval()` | Kötü niyetli kodun belirli bir süre sonra veya sürekli olarak çalışmasını sağlar. |

### XSS İçin Kullanılan HTML Etiketleri (Vectors)

| HTML Etiketi | XSS Kullanım Senaryosu |
| :--- | :--- |
| `<script>` | Doğrudan JS kodunu sayfaya gömmek için temel etikettir. |
| `<img>` | Resim yüklenemediğinde hata verdirtip kod çalıştırmak için kullanılır. (Örn: `<img src=x onerror=alert(1)>`) |
| `<iframe>` | Sayfa içine sahte bir giriş ekranı (phishing) veya zararlı bir site gömmek için kullanılır. |
| `<a>` | Kullanıcı tıkladığında kod çalıştıran linkler oluşturulur. (Örn: `<a href="javascript:alert(1)">Tıkla</a>`) |
| `<input>`, `<textarea>` | Fareyle üzerine gelindiğinde, tıklandığında veya odaktan çıkıldığında kod tetikleyecek (Event Handler) yapılandırmalar için kullanılır. (Örn: `onmouseover`, `onfocus`) |
| `<svg>` | Resim formatı gibi görünse de içinde gömülü JS barındırabildiği için XSS filtrelerini atlatmak (Bypass) için harikadır. |