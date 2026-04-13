# HTTP (Hypertext Transfer Protocol)
- İnternet üzerinde bilgi alışverişi yapılmasını sağlayan temel bir protokoldür. Web sayfalarının ve diğer verilerin, bir ağ üzerindeki sunuculardan istemcilere aktarılmasını mümkün kılar.

- HTTP, istemci-sunucu modelini kullanır. Bu modelde, bir istemci bir sunucuya bir istek (request) gönderir ve sunucu bu isteğe bir yanıt (response) ile karşılık verir. Bu istek ve yanıt mekanizması, web sayfalarının, resimlerin, videoların ve diğer içeriklerin internet üzerinden alınıp gönderilmesini sağlar.

### HTTP İstekleri (Request)
Http istekleri, aşağıdaki dört temel bileşenden oluşur.
1) URL
2) Method
3) Başlıklar
4) İstek Gövdesi (Opsiyonel)

```bash
GET /index.html HTTP/1.1
Host: www.example.com
Cookie: SESSIONID=badb655ebd99ed6c8e58c0a1aab44eb9
```
- İlk satırda HTTP Methodu, isteğin gönderildiği yol (path) ve HTTP protokolünün versiyonu bulunmaktadır. Örneğimizde, isteğin GET methodu ile index.html yoluna gönderildiği görülmektedir. HTTP versiyonu ise HTTP/1.1 olarak belirtilmiş.

- İkinci satırda, isteğimizin gideceği hedef sunucunun adresi yer almaktadır. Hedef sunucu adresine alan adı veya IP adresi yazılabilir. Örneğimizde www.example.com alan adına istek gönderildiği görülmektedir

- Üçüncü satır, istemci tarafında veri saklamak için kullanılan bir çerez (cookie) başlığı içeriyor. Web sitelerindeki oturum açma süreçleri genellikle çerezler ile yürütülür. Bu örnekte, hedef sunucuya istemciyi tanıyabilmesi için SESSIONID isminde bir çerezi badb655ebd99ed6c8e58c0a1aab44eb9 değeri ile gönderildiği anlaşılmaktadır.

# HTTP Temelleri ve Çalışma Prensibi


## 1. HTTP İstek Metotları (Request Methods)
İstemcinin (tarayıcının vb.) sunucudan ne tür bir işlem yapmasını istediğini belirtir.

| Metot | Tanım |
| :--- | :--- |
| **GET** | Kaynağı almak/okumak için kullanılır. Sunucudan veri çeker. |
| **POST** | Sunucuya yeni veri göndermek için kullanılır (Örn: Form veya dosya gönderimi). |
| **PUT** | Belirli bir kaynağı oluşturmak veya mevcut kaynağı tamamen güncellemek için kullanılır. |
| **PATCH** | Bir kaynağın sadece belirli bir kısmını/parçasını güncellemek için kullanılır. |
| **DELETE** | Belirtilen kaynağı silmek için kullanılır. |
| **HEAD** | GET gibidir ancak sadece başlıkları (headers) döndürür, veri gövdesini döndürmez. |
| **OPTIONS** | Hedef kaynağın hangi HTTP metotlarını desteklediğini sorgular. |

---

## 2. HTTP İstek Başlıkları (Request Headers)
İsteğin nasıl işleneceği, istemci bilgileri ve veri türü gibi ek detayları (metadata) taşır. `İsim: Değer` formatında yazılır.

* **Önemli Başlıklar:**
  * `Host`: Bağlanılacak sunucunun alan adını belirtir (Örn: example.com).
  * `User-Agent`: İsteği yapan tarayıcı ve işletim sistemi hakkında bilgi verir.
  * `Accept`: İstemcinin yanıt olarak kabul edebileceği veri türlerini (MIME) belirtir.
  * `Authorization`: Kimlik doğrulama amaçlı erişim belirteçlerini (Token) taşır.
  * `Content-Type`: İstek gövdesinde (body) gönderilen verinin türünü belirtir (Örn: `application/json`).

---

## 3. HTTP İstek Gövdesi (Request Body)
İstemciden sunucuya gönderilen asıl veriyi (payload) içerir. Genellikle GET isteklerinde bulunmaz; POST, PUT, PATCH gibi metotlarda kullanılır.
* **Format:** Gönderilen verinin yapısı, başlıklarda yer alan `Content-Type` ile sunucuya bildirilir (JSON, XML, Form-Data vb.).

---

## 4. HTTP Yanıtları (Responses)
Sunucunun istemciye verdiği cevaptır. HTTP sürümünü, durum kodunu, yanıt başlıklarını ve istenen asıl veriyi içerir.

| Durum Kodu | Kategori / Anlamı |
| :--- | :--- |
| **200** | Başarılı (OK) |
| **201** | Oluşturuldu (Created) |
| **301** | Kalıcı Olarak Taşındı (İstenen kaynak yeni bir URL'ye taşındı) |
| **404** | Bulunamadı (İstenen kaynak sunucuda yok) |
| **500** | İç Sunucu Hatası (Sunucu isteği işlerken bir hata ile karşılaştı) |

---

## 5. Adım Adım Web Çalışma Prensibi
Bir web sitesine girmek istediğinizde arka planda sırasıyla şu işlemler gerçekleşir:

1. **URL Girme:** Tarayıcıya adres yazılır (Örn: `https://google.com`).
2. **DNS Sorgusu:** İnsanların okuyabildiği alan adı (URL), DNS sunucuları aracılığıyla bilgisayarların anladığı sayısal IP adresine dönüştürülür.
3. **İstek Gönderme (Request):** Elde edilen IP adresindeki sunucuya hedeflenen içerik için bir HTTP isteği gönderilir.
4. **Yanıt Alma (Response):** Web sunucusu isteği işler ve istenilen içeriği (genelde HTML kodları) bir HTTP yanıtı ile geri döndürür.
5. **Görüntüleme:** Tarayıcı, sunucudan gelen HTML, CSS ve JavaScript kaynaklarını derleyerek görsel sayfayı oluşturur.
6. **Bağlantıyı Sonlandırma:** İstek-yanıt döngüsü tamamlandığında (ve bağlantıyı açık tutacak `keep-alive` gibi özel bir komut yoksa) istemci ile sunucu arasındaki bağlantı kapatılır.