# Manuel Keşif: robots.txt ve sitemap.xml
Sızma testi (pentest) süreçlerinde dizin taramasına (directory bruteforcing) otomatik araçlarla başlamadan önce, web sitelerinin doğası gereği barındırdığı ve herkese açık olan bazı yapılandırma dosyalarını **manuel olarak** kontrol etmek hayati önem taşır. Çoğu zaman en kritik zafiyetler veya gizli paneller bu dosyalarda açıkça listelenmiştir.

---

## 1. robots.txt

`robots.txt`, web sitelerinin kök dizininde bulunan ve arama motoru botlarına (Googlebot, Bingbot vb.) site içerisinde hangi sayfaları indeksleyebileceğini, hangilerinden uzak durması gerektiğini söyleyen standart bir metin dosyasıdır.

* **Siber Güvenlikteki Önemi:** Birçok acemi veya dikkatsiz sistem yöneticisi, Google'da görünmesini istemediği hassas panelleri, yedekleme dosyalarını veya test dizinlerini bu dosyaya yazarak "yasaklar" (`Disallow`). Ancak arama motorları bu kurallara uyarken, kötü niyetli kişiler ve siber güvenlik uzmanları için bu dosya tam anlamıyla bir **"Hazine Haritası"**na dönüşür. Ziyaret edilmemesi istenen yerler, aslında ilk saldırılması gereken yerlerdir!
* **Kullanımı:** Tarayıcının adres çubuğuna `https://hedefsite.com/robots.txt` yazılarak doğrudan görüntülenir.

**Örnek bir robots.txt dosyası:**
```text
User-agent: *
Disallow: /admin_paneli
Disallow: /db_yedekleri
Disallow: /gizli_test_sayfasi.php
````

_(Yukarıdaki örnekte bir hacker, otomatik araca ihtiyaç duymadan doğrudan `/db_yedekleri` dizinine gidip veritabanını indirebilir)._

---

## 2. sitemap.xml (Site Haritası)

`sitemap.xml`, bir web sitesindeki tüm önemli sayfaların hiyerarşik bir listesini içeren XML formatında bir haritadır. Temel amacı SEO'dur (Arama Motoru Optimizasyonu); arama motorlarına sitenin yapısını bildirerek sayfaların daha hızlı keşfedilmesini sağlar.

- **Siber Güvenlikteki Önemi:** Site haritaları bazen otomatik araçlar (pluginler) tarafından oluşturulur ve site sahibinin bile unuttuğu, site içi linklemesi yapılmamış (orphan pages), eski versiyonlu sayfaları veya API uç noktalarını açığa çıkarabilir. Sızma testi uzmanları bu dosyayı analiz ederek, normal kullanıcıların sitede gezinerek asla bulamayacağı sayfalara erişim sağlar.
    
- **Kullanımı:** Tarayıcının adres çubuğuna `https://hedefsite.com/sitemap.xml` yazılarak görüntülenir.
    

**Örnek bir sitemap.xml dosyası:**

```xml
<urlset xmlns="[http://www.sitemaps.org/schemas/sitemap/0.9](http://www.sitemaps.org/schemas/sitemap/0.9)">
   <url>
      <loc>[http://www.example.com/](http://www.example.com/)</loc>
   </url>
   <url>
      <loc>[http://www.example.com/eski_versiyon_yedek](http://www.example.com/eski_versiyon_yedek)</loc>
   </url>
   <url>
      <loc>[http://www.example.com/api/v1/test_kullanicilari](http://www.example.com/api/v1/test_kullanicilari)</loc>
   </url>
</urlset>
```