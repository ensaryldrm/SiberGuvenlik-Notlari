# Reflected XSS (Kalıcı Olmayan XSS) ve HTML Enjeksiyonu

## 1. Reflected XSS Nedir?
Reflected XSS, zararlı bir scriptin (genellikle URL üzerinden) web uygulamasına gönderildiği ve sunucunun bu isteği HTTP yanıtı olarak kullanıcının tarayıcısında anında geri yansıttığı (reflected) bir saldırı türüdür.
* **Karakteristiği:** Tek bir HTTP istek/yanıt döngüsüyle tamamlanır. Veritabanına kaydedilmez.
* **Tetiklenme:** Genellikle Oltalama (Phishing) veya sosyal mühendislik yöntemleriyle kurbanın zararlı payload içeren bir linke tıklaması sağlanarak gerçekleştirilir.

---

## 2. Zafiyetin Sömürülmesi ve Örnekler

### A. Temel XSS Payload (JavaScript Enjeksiyonu)
Saldırgan, sayfanın arama kutusuna (`q` parametresi) uyarı kutusu çıkartan basit bir JavaScript kodu ekler.
* **Örnek URL:** `https://example.com/home?q=<script>alert(1)</script>`
* **Sonuç:** Kurban bu linke tıkladığında, sunucu aranan kelimeyi sayfaya basarken `<script>` etiketlerini de basar ve kurbanın tarayıcısında kod çalışarak `1` uyarısı çıkar.

### B. HTML Injection (HTML Enjeksiyonu)
Zafiyetli alanlara sadece JavaScript değil, HTML kodları da enjekte edilebilir. Bu sayede sayfanın tasarımı manipüle edilerek yanıltıcı giriş formları (Sahte Login ekranı vb.) oluşturulabilir.
* **Örnek URL:** `https://example.com/home?q=<h1 style="color:green;">TEST</h1>`
* **Sonuç:** Ekranda yeşil renkte, büyük "TEST" yazısı belirir.

---

## 3. Kaynak Kod Analizi (Neden Olur ve Nasıl Önlenir?)
Zafiyetin temel sebebi, kullanıcıdan alınan verinin (Input) hiçbir filtreden geçirilmeden doğrudan ekrana (Output) basılmasıdır.

### Zafiyetli Kod Örneği (PHP)
Aşağıdaki kodda `$q` değişkeni, URL'den alındığı gibi doğrudan HTML etiketlerinin arasına yazdırılmaktadır.
```php
<?php 
    if (isset($_GET['q'])) {
        $q = $_GET['q']; // Veri filtrelenmeden alınıyor
        echo '<div class="alert alert-danger" role="alert">
            No Result Found for <b>' . $q . '</b> 
        </div>';
    } 
?>
````

- **Tehlike:** `$q` yerine `<script>alert(1)</script>` gelirse, tarayıcı bunu düz metin değil, çalıştırılabilir kod olarak algılar.
    

### Güvenli Kod Örneği (PHP - Mitigation)

Saldırıyı önlemek için kullanıcıdan alınan verilerdeki özel HTML karakterleri (`<`, `>`, `&`, `"`, `'`), HTML varlıklarına (`&lt;`, `&gt;` vb.) dönüştürülmelidir.

```php
<?php 
    if (isset($_GET['q'])) {
        $q = $_GET['q'];
        // htmlspecialchars fonksiyonu ile zararlı karakterler temizleniyor
        echo '<div class="alert alert-danger" role="alert">
            No Result Found for <b>' . htmlspecialchars($q) . '</b> 
        </div>';
    } 
?>
```

- **Koruma Mantığı:** Eğer kullanıcı `<script>` gönderirse, `htmlspecialchars` bunu `&lt;script&gt;` formatına çevirir. Tarayıcı bunu bir kod olarak değil, sadece ekranda gösterilecek güvenli bir metin (düz yazı) olarak işler.