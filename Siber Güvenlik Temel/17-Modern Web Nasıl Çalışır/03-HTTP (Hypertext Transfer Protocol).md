# HTTP ve HTTPS Protokolleri Temelleri


## 1. HTTP ve HTTPS Nedir?
* **HTTP (Hypertext Transfer Protocol):** Web tarayıcısı (istemci) ile web sunucusu arasındaki bilgi alışverişinin temelini oluşturan, istemci-sunucu modeline dayalı protokoldür. Veriler açık metin (clear-text) olarak iletilir.
* **HTTPS (HTTP Secure):** HTTP'nin SSL (Secure Sockets Layer) veya güncel adıyla TLS (Transport Layer Security) protokolleri ile şifrelenmiş halidir.
* **HTTPS İşleyişi (Handshake):** Tarayıcı ve sunucu iletişim kurmadan önce sunucu kimliğini sertifika ile doğrular, güvenli bir oturum anahtarı oluşturulur ve tüm veri aktarımı bu anahtar ile şifrelenir.

---

## 2. HTTP İstekleri (Requests)
Bir istemcinin sunucudan işlem talep etmesidir. Dört temel bileşenden oluşur:

### A. İstek Metotları (Request Methods)
| Metot | İşlev |
| :--- | :--- |
| **GET** | Sunucudan veri/kaynak almak için kullanılır. |
| **POST** | Sunucuya yeni veri göndermek için kullanılır (Örn: Form doldurma). |
| **PUT** | Kaynağı oluşturmak veya tamamen güncellemek için kullanılır. |
| **PATCH** | Kaynağı kısmen güncellemek için kullanılır. |
| **DELETE** | Belirtilen kaynağı silmek için kullanılır. |
| **HEAD** | GET gibidir ancak sadece başlık (header) döner, içerik dönmez. |
| **OPTIONS** | Kaynağın hangi metotları desteklediğini sorgular. |

### B. İstek Başlıkları (Request Headers)
İsteğin nasıl işleneceği hakkında ekstra veriler (metadata) taşır. `İsim: Değer` formatındadır.
* `Host`: Hedef sunucu adresi (Örn: `example.com`).
* `User-Agent`: İsteği yapan tarayıcı/işletim sistemi bilgisi.
* `Cookie`: Oturum yönetimi için istemcide saklanan çerezleri gönderir (Örn: `SESSIONID=12345`).
* `Authorization`: Kimlik doğrulama belirteçlerini (Token) taşır.
* `Accept`: İstemcinin kabul edeceği veri türlerini belirtir.

### C. İstek Gövdesi (Request Body)
Sadece veri gönderirken (POST, PUT, PATCH) kullanılır. Gönderilen verinin formatı (JSON, Form-Data) başlıktaki `Content-Type` ile belirtilir.

---

## 3. HTTP Yanıtları ve Durum Kodları (Responses)
Sunucunun isteğe verdiği cevaptır. En önemli bileşeni durum kodlarıdır (Status Codes).

### 1xx: Bilgilendirici (İşlem devam ediyor)
| Kod | Adı | Açıklama |
| :--- | :--- | :--- |
| **100** | Continue | İstemci isteği göndermeye devam edebilir. |
| **101** | Switching Protocols | Sunucu protokol değiştirme talebini kabul etti. |

### 2xx: Başarılı (İşlem tamamlandı)
| Kod | Adı | Açıklama |
| :--- | :--- | :--- |
| **200** | OK | İstek başarıyla gerçekleşti. |
| **201** | Created | Yeni kaynak başarıyla oluşturuldu. |
| **204** | No Content | İstek başarılı ancak dönecek bir içerik/gövde yok. |

### 3xx: Yönlendirme (Başka adrese git)
| Kod | Adı | Açıklama |
| :--- | :--- | :--- |
| **301** | Moved Permanently | Kaynak kalıcı olarak başka bir URL'ye taşındı. |
| **302** | Found | Kaynak geçici olarak başka bir URL'ye taşındı. |
| **304** | Not Modified | Kaynak değişmedi, tarayıcı önbelleğindeki (cache) veri kullanılabilir. |

### 4xx: İstemci Hatası (Kullanıcı kaynaklı sorun)
| Kod | Adı | Açıklama |
| :--- | :--- | :--- |
| **400** | Bad Request | Sözdizimi hatalı veya geçersiz istek. |
| **401** | Unauthorized | İşlem için kimlik doğrulama/giriş yapılması gerekiyor. |
| **403** | Forbidden | Kimlik doğrulansa bile bu kaynağa erişim yetkisi yok. |
| **404** | Not Found | İstenen kaynak sunucuda bulunamadı. |
| **405** | Method Not Allowed | İstenen HTTP metodu bu kaynak için kullanılamaz. |

### 5xx: Sunucu Hatası (Sistem kaynaklı sorun)
| Kod | Adı | Açıklama |
| :--- | :--- | :--- |
| **500** | Internal Server Error | Sunucu tarafında beklenmeyen genel bir hata oluştu. |
| **502** | Bad Gateway | Ara sunucu (Proxy/Gateway) üst sunucudan geçersiz yanıt aldı. |
| **503** | Service Unavailable | Sunucu aşırı yüklü veya bakımda olduğu için hizmet veremiyor. |
| **504** | Gateway Timeout | Ara sunucu, hedef sunucudan zamanında yanıt alamadı. |

---

## 4. Web'in Çalışma Prensibi (Adım Adım)
1. **URL Girme:** Tarayıcıya adres yazılır.
2. **DNS Sorgusu:** Alan adı (URL), DNS aracılığıyla hedefin IP adresine dönüştürülür.
3. **İstek Gönderme (Request):** Tarayıcı hedefe bir HTTP isteği yollar.
4. **Yanıt Alma (Response):** Sunucu isteği işler ve veriyi (HTML, JSON vb.) HTTP yanıtı olarak döndürür.
5. **Görüntüleme:** Tarayıcı gelen kodları derler ve görsel sayfayı oluşturur.
6. **Bağlantı Sonlandırma:** İstek döngüsü bitince bağlantı kapatılır (veya `keep-alive` ile bir süre daha açık tutulur).
```