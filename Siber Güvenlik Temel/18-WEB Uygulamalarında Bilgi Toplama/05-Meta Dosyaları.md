# Web Meta Dosyaları ve Dizin Keşfi
Siber güvenlikte, bir web uygulamasının kök dizininde (root) bulunan ve genellikle botlar veya arama motorları için yerleştirilen meta dosyalarını incelemek, uygulamanın haritasını çıkarmak (mapping) için çok değerlidir. Geliştiriciler bu dosyalarda sık sık gizli dizinleri veya hassas iletişim bilgilerini ifşa ederler.

## 1. robots.txt (Arama Motoru Yönergeleri)
Arama motoru botlarına (Googlebot vb.) sitenin hangi bölümlerini tarayabileceklerini, hangi bölümlerden uzak durmaları gerektiğini söyleyen bir kurallar dosyasıdır. Ancak botlar için bir "kural" olsa da, siber güvenlik uzmanları için bir **"hazine haritasıdır"**.

* **Konum:** `https://hedefsite.com/robots.txt`
* **Yapısı:**
  * `User-agent:` Hangi botun hedeflendiğini gösterir (`*` hepsi demektir).
  * `Allow:` Bota izin verilen dizinleri belirtir.
  * `Disallow:` Bota yasaklanan dizinleri belirtir.
* **Siber Güvenlik Açısından:** Sistem yöneticileri bazen dışarıdan bulunmasını istemedikleri yönetici panellerini (`Disallow: /admin-panel`) veya veritabanı yedek klasörlerini (`Disallow: /db-backups`) botlardan gizlemek için buraya yazarlar. Bu dosyayı okumak, doğrudan bu gizli yolları bulmanızı sağlar.

## 2. sitemap.xml (Site Haritası)
Uygulamanın genel yapısını, tüm alt sayfalarını, API noktalarını ve dosyalarını XML formatında listeleyen bir "fihrist"tir.

* **Konum:** `https://hedefsite.com/sitemap.xml`
* **Siber Güvenlik Açısından:** Site çok karmaşık ve büyükse, arayüzden tıklayarak bulamayacağınız derin sayfalara, eski kampanya linklerine veya API dökümantasyon dizinlerine (`/api/v1/users`) bu dosya üzerinden hızlıca erişilebilir.

## 3. security.txt (Güvenlik Politikası)
Kurumların siber güvenlik uzmanlarına, buldukları açıkları nasıl (hangi mail veya platform üzerinden) ve hangi kurallarla bildireceklerini anlattıkları standart (RFC 9116) bir dosyadır.

* **Konum:** `https://hedefsite.com/security.txt` veya `https://hedefsite.com/.well-known/security.txt`
* **Siber Güvenlik Açısından:** Eğer hedefte bir Bug Bounty (Ödül Avcılığı) programı varsa bu dosya doğrudan o platformun linkini (Örn: HackerOne profili) verir. Ayrıca OSINT (Açık Kaynak İstihbaratı) için güvenlik ekibinin iletişim adreslerini içerir.

## 4. humans.txt (Geliştirici İmzası)
Sitenin arkasındaki kodlayıcılar, tasarımcılar ve yöneticiler hakkında bilgi veren eğlenceli/bilgilendirici bir dosyadır.

* **Konum:** `https://hedefsite.com/humans.txt`
* **Siber Güvenlik Açısından:** İçerisinde "Backend by John Doe, Server setup by Jane" gibi bilgiler bulunabilir. Bu isimler, LinkedIn üzerinden araştırılarak şirket hiyerarşisi haritalandırılabilir ve Sosyal Mühendislik (Oltalama/Phishing) senaryolarında hedef (target) olarak kullanılabilir.

---

## 5. Ekstra: HTML Meta Etiketleri
Bu dosyaların dışında, uygulamanın kaynak kodunda (`<head>` tagları arasında) bulunan ve sosyal medya platformları (Facebook, Twitter) için veriler taşıyan etiketler de vardır:
* `<meta name="robots" content="NOINDEX, NOFOLLOW">` (Bu sayfa Google'da çıkmasın emri, genellikle gizli sayfalarda olur).
* `og:title`, `twitter:card` (Sosyal ağlarda paylaşım önizlemelerini ayarlar).