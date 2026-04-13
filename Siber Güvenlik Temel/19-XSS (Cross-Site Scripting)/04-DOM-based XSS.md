# DOM-based XSS (DOM Tabanlı XSS)
## 1. DOM-based XSS Nedir?
DOM (Document Object Model) tabanlı XSS, zararlı kodun sunucu tarafından HTTP yanıtında döndürülmediği, bunun yerine **sayfadaki mevcut client-side (istemci tarafı) JavaScript kodlarının DOM'u manipüle etmesiyle** tarayıcı üzerinde tetiklendiği saldırı türüdür.

* **Farkı:** Reflected ve Stored XSS'te zararlı payload sunucuya gider ve sunucudan HTML içinde geri gelir. DOM XSS'te ise payload sunucuya hiç gitmeyebilir (örneğin URL'deki `#` hash kısmından alınarak çalıştırılır). Tüm olay kurbanın tarayıcısında olup biter.

## 2. Tehlikeli Fonksiyonlar (Sinks)
DOM XSS genellikle, kullanıcı girdisini alıp (Source) dinamik kod yürüten güvensiz JavaScript fonksiyonlarına (Sink) aktaran geliştirici hatalarından kaynaklanır:

* **`eval()`:** Kendisine verilen metin dizesini (string) doğrudan JavaScript kodu olarak okur ve çalıştırır. (Örn: `eval("console.log(1)");`)
* **`innerHTML`:** Bir HTML elementinin içeriğini dinamik olarak değiştirmek için kullanılır. İçine aktarılan metin tarayıcı tarafından HTML kodu olarak render edilir.

---

## 3. Yaygın DOM XSS Vektörleri ve Analizleri

### A. URL Fragment (Hash) Üzerinden Enjeksiyon
URL'in sonuna eklenen `#` (hash) kısmı sunucuya gönderilmez, sadece tarayıcı tarafından okunur.
* **Zafiyetli Kod:** `document.getElementById('output').innerHTML = window.location.hash.substring(1);`
* **Payload:** `https://example.com#<img src=x onerror="alert(1)">`
* **Sonuç:** Tarayıcı adresteki hash'i alır ve `innerHTML` ile sayfaya gömer. Resim hatalı olduğu için `onerror` tetiklenir ve JavaScript çalışır.

### B. `eval()` Fonksiyonunun Manipüle Edilmesi
Parametrelerin güvensizce doğrudan çalıştırılabilir koda dahil edilmesidir.
* **Zafiyetli Kod:** 

```javascript
  const productId = new URLSearchParams(window.location.search).get('id');
  eval('getProduct(' + productId + ')');
```

- **Payload:** `https://example.com/products?id=');alert(1)//`
    
- **Sonuç:** Oluşan kod `eval('getProduct('');alert(1)//')` haline gelir. Kod akışı kırılarak (`);`) araya zararlı `alert(1)` sıkıştırılır.
    

---

## 4. Gerçek Dünya Senaryosu: Üçgen Alanı Hesaplayıcı

Dışarıdan girilen yükseklik (`height`) ve taban (`base`) değerlerini alıp hesaplama yapan bir sistemde DOM XSS incelemesi:

### Zafiyetli PHP Kodu

```PHP
<?php
    if (isset($_GET['base']) && isset($_GET['height'])) {
        echo '<script>';
        echo 'var height = ' . $_GET['height'] . ';';
        echo 'var base = ' . $_GET['base'] . ';';
        echo 'var ans = base * height / 2;';
        echo 'document.getElementById("answer").innerHTML = "<b>Area:</b> " + ans;';
        echo '</script>';
    }
?>
```

- **Payload:** `?height=5; alert('XSS')&base=12`
    
- **Neden Çalışır?** Tarayıcıya giden JS kodu şu hale gelir: `var height = 5; alert('XSS');` Değişken ataması noktalı virgül ile sonlandırılır ve hemen ardından zararlı script devreye girer.
    

### Güvenli PHP Kodu (Mitigation)

Korunmanın temel yolu, JavaScript bağlamına (context) veri aktarırken özel karakterleri zararsız hale getirmektir.

```php
<?php
    if (isset($_GET['base']) && isset($_GET['height'])) {
        // htmlspecialchars ile girdiler temizlenir (Output Encoding)
        $base = htmlspecialchars($_GET['base'], ENT_QUOTES, 'UTF-8');
        $height = htmlspecialchars($_GET['height'], ENT_QUOTES, 'UTF-8');
        
        echo '<script>';
        echo 'var height = ' . $height . ';';
        echo 'var base = ' . $base . ';';
        // ... (devamı)
    }
?>
```

- **Ekstra Client-Side Koruma:** İstemci tarafında veriyi DOM'a basarken `innerHTML` yerine **`textContent`** veya **`innerText`** kullanmak, tarayıcının veriyi kod olarak okumasını tamamen engeller.