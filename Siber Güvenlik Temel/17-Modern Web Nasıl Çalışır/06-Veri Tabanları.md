# Veri Tabanı Sunucuları (Database Servers)

Veri tabanı sunucusu, verilerin depolanması, sorgulanması, güncellenmesi ve yönetilmesi süreçlerini üstlenen, Veri Tabanı Yönetim Sistemlerini (DBMS) barındıran temel altyapıdır. 1960'lardaki basit dosya sistemlerinden günümüzün karmaşık ilişkisel (RDBMS) ve ilişkisel olmayan (NoSQL) sistemlerine kadar büyük bir evrim geçirmiştir.

**Temel İşlevleri:**

- **Veri Depolama ve İyileştirme:** Verileri yapılandırarak hızlı sorgulama ve erişim sağlar.
    
- **Güvenlik:** Kimlik doğrulama, yetkilendirme ve şifreleme ile verileri korur.
    
- **Yedekleme ve Kurtarma:** Olası felaket senaryolarına karşı veri bütünlüğünü ve sürekliliğini garanti altına alır.
    

---

## 1. SQL (İlişkisel) Veri Tabanları

Verileri satırlar ve sütunlar halinde **tablolar** şeklinde düzenler. Veri bütünlüğünü sağlamak için tablolar arası ilişkiler kurulur.

- **ACID Uyumluluğu:** İşlemlerin güvenilirliğini garanti eden Atomiklik (Atomicity), Tutarlılık (Consistency), İzolasyon (Isolation) ve Dayanıklılık (Durability) ilkelerine sıkı sıkıya bağlıdır.
    
- **Sıkı Şema:** Veri yapısının önceden tanımlanması zorunludur.
    
- **Ölçeklenebilirlik:** Genellikle _dikey_ (sunucu donanımını artırarak) ölçeklenir.
    

|Veri Tabanı|Port|Öne Çıkan Özellikler ve Kullanım Alanları|Örnek Sorgu|
|---|---|---|---|
|**MySQL**|`3306`|LAMP yığınının popüler parçasıdır. Web siteleri, forumlar, CMS sistemleri ve KOBİ uygulamaları için idealdir.|`SELECT * FROM users WHERE age > 18;`|
|**PostgreSQL**|`5432`|Nesne-ilişkisel yapı, karmaşık sorgular ve yüksek uyumluluk sunar. Finansal işlemler, devasa CRM/ERP sistemleri ve coğrafi bilgi sistemlerinde (CBS) kullanılır.|`INSERT INTO books (name, author) VALUES ('Animal Farm', 'George Orwell');`|
|**Oracle**|`1521`|Kurumsal düzeyde yüksek güvenilirlik ve performans sunar. Bankacılık, e-ticaret, veri ambarları ve kritik iş uygulamaları için tasarlanmıştır.|`UPDATE employees SET salary = salary * 1.05 WHERE department_id = 10;`|
|**MS SQL Server**|`1433`|.NET ekosistemiyle kusursuz entegrasyon, güçlü iş zekası ve analiz araçları sunar. Kurumsal düzeyde büyük veri depolama için tercih edilir.|`UPDATE orders SET status = 'delivered' WHERE order_no = 100;`|

E-Tablolar'a aktar

---

## 2. NoSQL (İlişkisel Olmayan) Veri Tabanları

Büyük veri setleri ve yapılandırılmamış/yarı-yapılandırılmış veriler için tasarlanmış, esnek şemalı veri modelleridir.

- **Şema Esnekliği:** Veri yapısı önceden tanımlanmak zorunda değildir, hızlı geliştirme imkanı sunar.
    
- **Ölçeklenebilirlik:** Yüksek trafikli sistemlerde _yatay_ ölçeklenmeye (yeni sunucular eklemeye) çok uygundur.
    
- **Veri Modelleri:** Belge (Document), Sütun (Column), Anahtar-Değer (Key-Value) veya Grafik (Graph) tabanlı olabilir.
    

|Veri Tabanı|Port|Model & Öne Çıkan Özellikler|Örnek Sorgu / Komut|
|---|---|---|---|
|**MongoDB**|`27017`|**Belge Tabanlı:** Verileri JSON benzeri formatta saklar. Gerçek zamanlı analitik ve büyük ölçekli, esnek veri depolama gerektiren uygulamalar içindir.|`db.users.find({name: "John"});`|
|**Cassandra**|`9042`|**Sütun Tabanlı:** Yüksek hata toleransı ve lineer ölçeklenebilirlik sunar. Yoğun okuma/yazma gerektiren zaman serisi verilerinde kullanılır.|`SELECT * FROM user_status WHERE status = 'active';`|
|**Redis**|`6379`|**Anahtar-Değer:** Veriyi doğrudan RAM'de tutarak muazzam hız sunar. Önbellekleme (caching), oturum yönetimi ve gerçek zamanlı mesaj kuyrukları için kullanılır.|`SET session_123 { "name": "John" }`|

E-Tablolar'a aktar

---

## Özet Karşılaştırma: SQL mi, NoSQL mi?

| Karşılaştırma Kriteri   | SQL (İlişkisel)                                                   | NoSQL (İlişkisel Olmayan)                                   |
| ----------------------- | ----------------------------------------------------------------- | ----------------------------------------------------------- |
| **Veri Yapısı**         | Tablo tabanlı, katı ve önceden tanımlanmış şema.                  | Esnek şema (JSON, Anahtar-Değer, Grafik vb.).               |
| **Ölçeklenme Tipi**     | Dikey (Vertical - Sunucu gücünü artırma).                         | Yatay (Horizontal - Sunucu sayısını artırma).               |
| **İşlem Güvenilirliği** | ACID prensiplerine sıkı bağlılık.                                 | Eventual Consistency (Nihai Tutarlılık) modeline yatkınlık. |
| **İdeal Kullanım**      | Karmaşık sorgular ve çoklu tablo ilişkileri gerektiren sistemler. | Büyük hacimli, hızlı değişen veya yapısal olmayan veriler.  |