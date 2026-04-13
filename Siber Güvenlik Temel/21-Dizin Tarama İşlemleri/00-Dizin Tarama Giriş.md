# İçerik Keşfi, Dizin Tarama ve Fuzzing

Güvenlik testlerinde (Sızma Testleri / Pentest) bir sisteme erişim sağlamanın en önemli adımlarından biri, hedefin sahip olduğu ancak dışarıdan görünmeyen (gizli, unutulmuş, yapılandırma hatası olan) dosyaları ve dizinleri keşfetmektir. Web uygulamalarının kapsamlı ve derinlemesine analiz edilmesini sağlayarak uzmanlara değerli içgörüler sunar.

---

## Temel Kavramlar

### Dizin Tarama (Directory Scanning)
Bir web sitesinin dizin yapısını keşfetmeye yönelik bir tekniktir. Bu süreç, güvenlik açıklarını tespit etmek amacıyla gerçekleştirilir ve web uygulamalarındaki gizli dosya ve dizinleri ortaya çıkarır.

### İçerik Keşfi (Content Discovery)
Bilgi toplama sürecinin bir parçasıdır. Bu yöntem, belirli bir hedefe yönelik olarak, gizli veya unutulmuş sayfaları, dosyaları ve diğer kaynakları keşfetmeye yöneliktir.

### Fuzzing
Yazılımdaki zafiyetleri bulmak için sisteme **beklenmedik, hatalı veya rastgele veriler** gönderme tekniğidir. Fuzzing sayesinde uygulamanın nasıl davranacağı ve potansiyel zafiyetlerin nerede olabileceği tespit edilir.
* **Örnek 1:** Rastgele dosya isimleri listesi oluşturup bunların sunucuda olup olmadığını kontrol etmek.
* **Örnek 2:** Bir giriş formuna rastgele girdiler (payload) göndererek web uygulamasının verdiği tepkiyi gözlemlemek.

### Wordlist (Kelime Listesi)
Dizin ve sayfa taraması yapmak için yaygın olarak kullanılan kelimelerden oluşan metin dosyalarıdır. Bu yöntem, parola sözlük saldırılarına (dictionary attack) benzer. Rastgele karakter denemek yerine, internette en çok kullanılan klasör ve dosya isimleri denenerek web sitesinin dizin yapısının büyük bir çoğunluğu ortaya çıkarılabilir.
* **SecLists:** Her türlü fuzzing işlemi için en sık kullanılan kelimelerin belirlendiği ve arşivlendiği popüler GitHub deposudur.
* *HackerBox'ta SecLists Yolu:* `/root/Desktop/misc/SecLists`
* *Örnek Liste:* `/root/Desktop/misc/SecLists/Discovery/Web-Content/directory-list-2.3-big.txt`

---

## Sık Kullanılan Tarama Araçları

Dizin ve sayfa taraması için komut satırı üzerinden çalışan birçok etkili araç bulunmaktadır.

### 1. Gobuster
Go dili ile yazılmış, oldukça hızlı bir dizin tarama aracıdır. Birden fazla iş parçacığından (thread) yararlanarak eşzamanlı işlemler gerçekleştirebilir. Tek dezavantajı rekürsif (iç içe) dizin taramasını desteklememesidir.
* **Çalışma Modları:**
    * `dir` - Klasik dizin ve dosya tarama (kaba kuvvet) modu.
    * `dns` - DNS alt alan adları (subdomain) tarama modu.
    * `vhost` - Sanal sunucu (Virtual Host) tarama modu.
    * `s3` / `gcs` - Açık Amazon S3 ve Google Cloud bucket tarama modları.
    * `fuzz` - Temel fuzzing işlemleri.
* **Kullanımı:** `gobuster [mode] [options]`

### 2. FFUF (Fuzz Faster U Fool)
Web uygulamalarındaki zafiyetleri bulmak için tasarlanmış, Go diliyle geliştirilen ücretsiz ve çok hızlı bir araçtır. Çeşitli payloadlar içeren büyük miktarda istek gönderir ve gelen yanıtları analiz eder.
* **Uygulama Alanları:** Dizin keşfi, sanal bilgisayar keşfi, GET/POST parametrelerine fuzzing uygulanması.
* **Kullanımı:** `ffuf -u http://target.com/FUZZ -w <wordlist>`

### 3. Dirb
Tipik web sunucu klasörleri ve dosyalarını (yönetici sayfaları, yedek dosyalar vb.) tespit etmek için kullanılan eski ama popüler bir araçtır. İçerisinde yaklaşık 4000 kelimelik dahili bir wordlist bulunur ve rekürsif tarama yapabilir.
* **Kullanımı:** `dirb <url_base> [<wordlist_file(s)>] [options]`

### 4. Feroxbuster
Rust programlama dilinde yazılmış, hem hızlı hem de verimli yeni nesil bir tarama aracıdır. Brute-force, rekürsif tarama ve wordlistlere dayalı keşif tekniklerini bir arada kullanır. İş parçacığı sayısı, user-agent ve çerez gibi seçenekleri kolayca yapılandırmaya olanak tanır.
* **Kullanımı:** `feroxbuster -u <url> -w <wordlist>`