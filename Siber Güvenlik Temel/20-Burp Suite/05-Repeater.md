# Burp Suite Repeater: Manuel İstek Manipülasyonu
## 1. Repeater Nedir?
Repeater (Tekrarlayıcı), yakalanan bir HTTP isteğini (Request) defalarca kez sunucuya gönderip, her seferinde parametreler üzerinde **manuel değişiklikler yaparak** sunucunun nasıl tepki verdiğini (Response) analiz etmenizi sağlayan en temel test aracıdır.

* **Kullanım Amacı:** Otomatik araçların (Intruder, Scanner) bulduğu zafiyetleri doğrulamak, iş mantığı hatalarını (Business Logic Flaws) aramak, IDOR (Insecure Direct Object Reference) veya SQL Injection gibi açıkları adım adım manuel olarak test etmek için kullanılır.

---

## 2. Repeater İş Akışı (Nasıl Kullanılır?)
Siber güvenlik uzmanları, bir web sitesini test ederken şüpheli gördükleri her isteği hemen Repeater'a atarlar. İşlem adımları şu şekildedir:

1. **İstek Yakalama:** Proxy (Intercept) sekmesi veya HTTP History listesi üzerinden incelenecek istek bulunur.
2. **Repeater'a Gönderme:** İsteğin üzerinde sağ tıklanır ve **"Send to Repeater"** (veya `CTRL+R` kısayolu) seçilerek istek bu modüle aktarılır.
3. **Düzenleme (Edit):** Repeater sekmesine geçilir. Sol taraftaki "Request" panelinde metin tabanlı olarak isteğin içi kurcalanır.
4. **Gönderme:** Değişiklikler bittikten sonra sol üstteki **"Send"** butonuna basılarak istek hedef sunucuya iletilir.

---

## 5. Değiştirilebilecek Temel Bileşenler
Repeater ekranında, sunucuyu kandırmak veya sınırlarını zorlamak için isteğin şu bölümleri değiştirilir:

* **HTTP Metodu (Method):** `GET` olan bir isteği `POST`, `PUT` veya `DELETE` yaparak sunucunun tepkisi ölçülür. *(Örn: Sadece GET kabul eden bir sayfaya POST atıp hata verdirmek).*
* **URL ve Dizinler:** Gidilen adres `/api/user` iken bunu `/api/admin` yaparak yetki aşımı test edilir.
* **Başlıklar (Headers):**