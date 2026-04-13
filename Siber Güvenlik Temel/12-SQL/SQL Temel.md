## 1. Veritabanı ve SQL Nedir?

- **Veritabanı (Database):** Verileri düzenli ve güvenli bir şekilde saklamak, yönetmek ve gerektiğinde hızlıca erişmek için kullanılan sistemlerdir.
    
- **SQL (Structured Query Language):** İlişkisel veritabanlarındaki verileri yönetmek, sorgulamak, eklemek veya silmek için kullanılan standart programlama dilidir.
    

## 2. Veritabanı Türleri

Sızma testlerinde hedefte hangi tür veritabanı olduğunu bilmek, kullanılacak saldırı vektörünü (SQLi vs NoSQLi) belirler:

1. **İlişkisel Veritabanları (SQL):** Verileri satırlar ve sütunlar halinde tablolarda saklar. (Örn: MySQL, PostgreSQL, MSSQL).
    
2. **Belge Tabanlı Veritabanları (NoSQL):** JSON, XML gibi yapıları kullanarak veriyi belge formunda esnek şekilde saklar. (Örn: MongoDB, CouchDB).
    
3. **Anahtar-Değer (Key-Value):** Basit anahtar-değer çiftleriyle RAM üzerinde çok hızlı çalışır. (Örn: Redis, DynamoDB).
    

## 3. Temel SQL Sorguları (CRUD İşlemleri)

Bir tablo içerisindeki veriyi manipüle etmek için şu dört temel komut kullanılır:

- **SELECT (Veri Çekme):** Tablodaki verileri okumak için kullanılır. `SELECT name, surname, age FROM users;` (Tüm veriyi çekmek için `SELECT * FROM users;` kullanılır).
    
- **INSERT (Veri Ekleme):** Tabloya yeni satır ekler. `INSERT INTO users (name, surname, age) VALUES ('Lynn', 'Spence', 37);`
    
- **UPDATE (Veri Güncelleme):** Mevcut veriyi değiştirir. `UPDATE users SET age = 34 WHERE name = 'Lynn';`
    
- **DELETE (Veri Silme):** Şarta uyan verileri siler. `DELETE FROM users WHERE age > 60;`
    

## 4. Veritabanı Yönetim Komutları

Sunucuya bağlandıktan sonra sistemde gezinmek (Enumeration) için kullanılan komutlardır (Sızma testlerinde en çok bunlar kullanılır):

- `SHOW DATABASES;` : Sunucudaki tüm veritabanlarını listeler.
    
- `USE <veritabanı_adı>;` : İşlem yapılacak veritabanını seçer (İçine girer).
    
- `SHOW TABLES;` : Seçili veritabanının içindeki tüm tabloları listeler.
    
- `DESCRIBE <tablo_adı>;` : Bir tablonun hangi sütunlardan ve veri türlerinden oluştuğunu gösterir.
    
- `DROP DATABASE <veritabanı_adı>;` : Veritabanını tamamen siler.
    
- `DROP TABLE <tablo_adı>;` : Tabloyu siler.
    

## 5. MySQL Sızma Testi Metodolojisi (CTF Adımları)

Bir CTF makinesinde MySQL portu (Varsayılan: **3306**) açık bulunduğunda izlenmesi gereken adımlar şunlardır:

### A. Bağlantı Denemesi (Yapılandırma Hatası Arama)

Sistem yöneticileri bazen `root` (en yetkili kullanıcı) hesabına parola koymayı unutabilirler. Parolasız giriş denemesi her zaman yapılmalıdır:

Bash

```
mysql -u root -h <hedef_ip>
```

_(Eğer varsayılan 3306 dışında bir porttaysa `-P <port>` parametresi eklenir)._

### B. Bilgi Toplama (Enumeration)

Sisteme erişim sağlandıktan (ve `mysql>` komut satırına düşüldükten) sonra içerideki hassas verileri bulmak için sırasıyla şu adımlar izlenir:

1. **Veritabanlarını Listele:** `SHOW DATABASES;`
    
2. **Şüpheli Veritabanına Gir:** `USE detective_inspector;` (Örnek isim)
    
3. **İçindeki Tablolara Bak:** `SHOW TABLES;`
    
4. **Hedef Tablodaki Verileri Çek:** Hedef tabloda (Örn: `hacker_list`) ne olduğunu görmek için tüm veriler ekrana basılır: `SELECT * FROM hacker_list;`
    

---