# Web Geliştirme Temelleri: Frontend ve Backend


Web geliştirme süreci, sitelerin nasıl göründüğü (Frontend) ve arka planda nasıl çalıştığı (Backend) olmak üzere iki temel bileşene ayrılır.

## 1. Frontend (İstemci Tarafı - Client Side)
Kullanıcıların web sitesinde doğrudan gördüğü, dokunduğu ve etkileşime girdiği her şeyin (arayüz, butonlar, renkler, animasyonlar) inşa edildiği alandır.

### Temel Teknolojiler (Büyük Üçlü)
* **HTML (HyperText Markup Language):** Sayfanın iskeletini ve yapısını oluşturur (Metinler, resimler, başlıklar).
* **CSS (Cascading Style Sheets):** HTML iskeletine stil (renk, font, düzen) vererek görsel tasarımı oluşturur.
* **JavaScript (JS):** Sayfayı dinamik ve interaktif hale getirir (Tıklama olayları, veri güncellemeleri, animasyonlar).

### Frontend Framework ve Kütüphaneleri
Geliştirme sürecini hızlandırmak ve karmaşık Tek Sayfa Uygulamaları (SPA) yapmak için kullanılırlar:
* **React:** Facebook tarafından geliştirilen, bileşen (component) tabanlı popüler kütüphane.
* **Angular:** Google tarafından geliştirilen, geniş çaplı uygulamalar için MVC mimarisi sunan framework.
* **Vue.js:** Öğrenmesi daha kolay, hafif ve esnek framework.

---

## 2. Backend (Sunucu Tarafı - Server Side)
Kullanıcının görmediği "arka plan" işlemlerinin yapıldığı yerdir. Kullanıcı isteklerini alır, veritabanını sorgular, hesaplamaları yapar ve sonucu Frontend'e gönderir.

### Temel Bileşenler
1. **Sunucu (Server):** İstemciden (tarayıcıdan) gelen isteklere (HTTP) yanıt veren altyapıdır (Örn: Apache, Nginx).
2. **Veritabanı (Database):** Verilerin güvenli ve düzenli saklandığı yerdir (Örn: MySQL, PostgreSQL, MongoDB).
3. **Sunucu Dilleri ve Frameworkler:**
   * **Go (Golang):** Google'ın geliştirdiği; çok hızlı, yüksek performanslı ve eşzamanlı (concurrency) çalışan derlemeli dildir. (Frameworkleri: *Fiber*, *Echo*).
   * **Node.js:** JavaScript'in sadece tarayıcıda değil, sunucuda da çalışmasını sağlayan asenkron yapılı çalışma zamanı (runtime).
   * **Python:** Okunabilirliği yüksek dildir. Büyük projeler için *Django*, hafif projeler için *Flask* frameworkleri kullanılır.
   * **PHP:** Web'in en eski ve yaygın sunucu dillerinden biridir (Örn: WordPress altyapısı). Modern framework'ü *Laravel*'dir.
   * **Ruby:** Geliştirme hızına odaklanan dildir, *Ruby on Rails* framework'ü ile ünlüdür.

### Örnek: Go (Fiber) ile Basit Bir Backend Sunucusu
Aşağıdaki kod, gelen bir HTTP GET isteğine sadece "Hello World!" cevabı veren minimal bir sunucudur:
```go
package main
import "[github.com/gofiber/fiber/v2](https://github.com/gofiber/fiber/v2)"

func main() {
    app := fiber.New()
    // Kök dizine (/) gelen istekleri karşıla
    app.Get("/", func(c *fiber.Ctx) error {
        return c.SendString("Hello World!")
    })
    // Sunucuyu 3000 portunda dinlemeye başla
    app.Listen(":3000")
}
````

---

## 3. Web Geliştirme Süreci (Nasıl Çalışırlar?)

1. **Tasarım (UI/UX):** Kullanıcı deneyimi ve arayüzü planlanır.
    
2. **Geliştirme:** Frontend geliştirici arayüzü kodlarken, Backend geliştirici veritabanını ve sunucu mantığını yazar. İki taraf birbiriyle **API'ler (Application Programming Interfaces)** ve HTTP istekleri aracılığıyla konuşur.
    
3. **Test ve Dağıtım:** Hatalar ve güvenlik açıkları test edildikten sonra proje canlı sunuculara (veya buluta) yüklenerek kullanıma açılır.