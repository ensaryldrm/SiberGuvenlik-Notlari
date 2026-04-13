# Google Dorks (Gelişmiş Arama Operatörleri) ile Bilgi Toplama


Siber güvenlikte "Google Hacking" olarak da bilinen Google Dorks, arama motorunun gelişmiş filtreleme operatörlerini kullanarak normalde gizli kalması gereken hassas bilgilere, yapılandırma dosyalarına ve güvenlik açıklarına ulaşma pratiğidir.

## 1. Google Dorks Nedir?
Google botları interneti sürekli tarar (crawl) ve indeksler. Bazen sistem yöneticileri yanlış yapılandırmalar sonucu şifre dosyalarını, veritabanı yedeklerini veya gizli panelleri dışarıya açık unutur. Google Dorks, milyarlarca sayfa arasından tam olarak bu unutulmuş hassas verileri cımbızla çekmemizi sağlayan özel sorgulardır.

## 2. Temel Dork Operatörleri
Bu operatörler tek başlarına kullanılabileceği gibi, birleştirilerek (kombinasyon yapılarak) çok daha ölümcül sorgular elde edilebilir.

| Operatör | İşlevi | Örnek Kullanım |
| :--- | :--- | :--- |
| **site:** | Sadece belirtilen alan adı (domain) veya alt alan adları içerisinde arama yapar. | `site:example.com` |
| **filetype:** | Sadece belirtilen dosya uzantısına sahip (PDF, DOCX, SQL, ENV) dosyaları arar. | `filetype:pdf` |
| **inurl:** | Web adresinin (URL) içerisinde belirtilen kelimenin geçtiği sayfaları listeler. | `inurl:admin` |
| **intext:** | Web sayfasının görünür metin içeriğinde belirtilen kelimeyi arar. | `intext:"password"` |
| **intitle:** | Tarayıcı sekmesinde yazan sayfa başlığında arama yapar. Açık dizinleri bulmak için çok sık kullanılır. | `intitle:"index of"` |

---

## 3. Kullanım Mantığı ve Siber Güvenlik Örnekleri
Gerçek bir sızma testinde amaç belirleyip operatörleri birleştirerek (zincirleyerek) nokta atışı aramalar yapılır.

* **Örnek 1 (Sıradan Arama):** `site:youtube.com filetype:pdf`
  * *Sonuç:* Sadece YouTube alan adına yüklenmiş PDF dosyalarını getirir.
* **Örnek 2 (Hassas Veri Avı):** `site:hedef.com filetype:env intext:DB_PASSWORD`
  * *Sonuç:* Hedef sitede yanlışlıkla dışarıya açılmış ve içinde veritabanı parolası yazan `.env` yapılandırma dosyalarını arar.
* **Örnek 3 (Açık Dizin Zafiyeti):** `intitle:"index of" "id_rsa"`
  * *Sonuç:* Dizin listeleme (Directory Listing) zafiyeti olan sunucularda, sistem yöneticilerine ait gizli SSH özel anahtarlarını (`id_rsa`) arar.

---

## 4. Google Hacking Database (GHDB)
Siber güvenlik uzmanlarının ve araştırmacıların bulduğu, hazır ve test edilmiş binlerce özel arama sorgusunun (Dork) toplandığı resmi veritabanıdır. Exploit-DB platformu altında barındırılır.

* **Bağlantı:** [https://www.exploit-db.com/google-hacking-database](https://www.exploit-db.com/google-hacking-database)
* **Kullanım Alanı:** Kendi sorgularınızı yazmak yerine, başkalarının "Kamera sistemleri", "Şifre dosyaları", "Savunmasız sunucular" için yazdığı hazır dorkları buradan kopyalayıp kullanabilirsiniz.