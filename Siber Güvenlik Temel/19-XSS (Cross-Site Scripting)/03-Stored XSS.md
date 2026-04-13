# Stored XSS (Kalıcı XSS) Zafiyeti

## 1. Stored XSS Nedir?
Stored XSS (Kalıcı XSS), zararlı bir scriptin uygulamanın veri tabanına kalıcı olarak kaydedildiği ve o sayfayı görüntüleyen tüm kullanıcıların tarayıcısında otomatik olarak çalıştırıldığı saldırı türüdür.
* **Karakteristiği:** Çok tehlikelidir çünkü kurbanın özel bir linke tıklamasına gerek yoktur. Sadece zararlı kodun bulunduğu sayfayı (örneğin bir forum başlığını veya yorumlar kısmını) ziyaret etmesi yeterlidir.
* **Sık Görüldüğü Yerler:** Mesajlaşma uygulamaları, forum gönderileri, blog yorumları, kullanıcı profili düzenleme ekranları.
* **Reflected XSS'ten Farkı:** Reflected XSS anlık bir yansımadır ve kurbanın linke tıklamasını gerektirir. Stored XSS ise veri tabanında saklanır ve kendi kendine yayılır (Örn: XSS solucanları).

---

## 2. Zafiyetin Sömürülmesi (Örnek Senaryo)

Bir mesajlaşma uygulamasında, kullanıcıların gönderdiği mesajlar veri tabanına kaydedilip sayfayı ziyaret eden herkese gösterilmektedir.

### A. Normal HTTP İsteği
Bir kullanıcı "Hello World" yazdığında arka planda giden POST isteği:
```http
POST /index.php HTTP/1.1
Host: example.com
Cookie: PHPSESSID=jl5kamgcplionfan0kkjhcujh3
Content-Type: application/x-www-form-urlencoded

message=Hello+World
````

### B. XSS Payload Enjeksiyonu

Saldırgan, girdi alanına "Hello World" yerine oturum çerezlerini (cookie) çalan bir JavaScript kodu yazar ve sunucuya gönderir.

```HTTP
POST /index.php HTTP/1.1
Host: example.com
Cookie: PHPSESSID=jl5kamgcplionfan0kkjhcujh3
Content-Type: application/x-www-form-urlencoded

message=<script>alert(document.cookie)</script>
```

- **Sonuç:** Bu andan itibaren o mesajlaşma sayfasını ziyaret eden **istisnasız her kullanıcının** tarayıcısında bu kod çalışır ve `PHPSESSID` (oturum bilgisi) ekranda uyarı kutusu olarak belirir (Gerçek bir saldırıda bu bilgi sessizce saldırganın sunucusuna gönderilir).
    

---

## 3. Kaynak Kod Analizi (Neden Olur ve Nasıl Önlenir?)

Zafiyetin temel sebebi, veri tabanından çekilen verilerin doğrudan tarayıcıya (HTML içine) render edilmesidir.

### Zafiyetli Kod Örneği (PHP)

Aşağıdaki kod, veri tabanından (`messages` tablosu) verileri çeker ve hiçbir filtreleme yapmadan `div` etiketleri arasında ekrana basar.

```PHP
<?php 
    $messages = $db->query("SELECT * FROM messages");
    if ($messages) {
        while ($row = $messages->fetch(PDO::FETCH_ASSOC)) {
            // Veri olduğu gibi HTML'e yansıtılıyor!
            echo "<div>" . $row['message'] . "</div>";
        }
    }
?>
```

### Güvenli Kod Örneği (PHP - Mitigation)

Saldırıyı önlemek için, veri tabanından gelen kullanıcı girdileri ekrana basılmadan hemen önce `htmlspecialchars` (veya benzeri bir output encoding) işleminden geçirilmelidir.

```PHP
<?php 
    $messages = $db->query("SELECT * FROM messages");
    if ($messages) {
        while ($row = $messages->fetch(PDO::FETCH_ASSOC)) {
            // htmlspecialchars ile zararlı karakterler (&lt;, &gt;) temizleniyor
            echo "<div>" . htmlspecialchars($row['message']) . "</div>";
        }
    }
?>
```

- **Koruma Mantığı:** Veri tabanında `<script>` yazsa bile, PHP bunu tarayıcıya gönderirken `&lt;script&gt;` olarak çevirir. Tarayıcı bunu zararsız bir düz metin olarak yorumlar ve XSS saldırısı engellenmiş olur.