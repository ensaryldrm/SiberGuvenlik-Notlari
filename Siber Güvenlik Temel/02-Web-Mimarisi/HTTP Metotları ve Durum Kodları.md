## HTTP İstekleri (Requests) ve Cevapları (Responses)
## En Sık Kullanılan HTTP Metotları
Tarayıcımızın sunucudan ne istediğini belirten fiillerdir.
* **GET:** Sunucudan sadece veri/sayfa **okumak** için kullanılır. (Örn: Bir habere tıklamak). Veriler URL çubuğunda görünür, şifre gönderirken kullanılmamalıdır.
* **POST:** Sunucuya yeni veri **göndermek/yazmak** için kullanılır. (Örn: Login olmak, form doldurmak). Veriler URL'de değil, HTTP gövdesinde (Body) gizli gider.
* **PUT:** Sunucudaki var olan bir veriyi **güncellemek** için kullanılır.
* **DELETE:** Sunucudaki bir veriyi **silmek** için kullanılır.

## HTTP Durum Kodları (Status Codes)
Sunucunun bize verdiği "İşlem başarılı mı, başarısız mı?" cevaplarıdır. Sızma testlerinde (Dirb, Gobuster) bu kodlara göre gizli klasörler bulunur.

| Kod Serisi | Anlamı | En Sık Karşılaşılan Örnekler |
| :--- | :--- | :--- |
| **1xx (Bilgi)** | İşlem başladı, devam ediyor. | `100 Continue` |
| **2xx (Başarılı)** | İstek ulaştı ve kabul edildi. | `200 OK` (Sayfa sorunsuz yüklendi) |
| **3xx (Yönlendirme)**| Aradığın sayfa başka yere taşındı. | `301 Moved Permanently`, `302 Found` |
| **4xx (İstemci Hatası)**| **Bizim** (Kullanıcının) hatası. | `400 Bad Request`, `401 Unauthorized` (Giriş yapmadın), `403 Forbidden` (Erişim yasağı), `404 Not Found` (Sayfa yok) |
| **5xx (Sunucu Hatası)**| **Sunucunun** (Karşı tarafın) hatası. | `500 Internal Server Error` (Hackerların sistemi çökerttiğinde veya SQL hatası verdirdiğinde gördüğü kod) |