# Reddict Makinesi Notları (NoSQL ve Redis Temelleri)

## 1. NoSQL Nedir?

- **Açılımı:** Not Only SQL (Sadece SQL Değil).
    
- **Mantığı:** Geleneksel ilişkisel veritabanlarının (MySQL, PostgreSQL vb.) katı tablo yapıları yerine, daha esnek veri modelleri (döküman, anahtar-değer, grafik vb.) sunan veritabanı yönetim sistemleridir.
    
- **Kullanım Amacı:** Büyük ölçekli, yapılandırılmamış verilerle yüksek performansta çalışmak ve yatayda kolayca ölçeklenebilmek için tasarlanmıştır.
    

## 2. Redis (REmote DIctionary Service) Nedir?

- Açık kaynak kodlu, **hafıza içi (in-memory)** çalışan, muazzam hızlı bir NoSQL veritabanıdır.
    
- Verileri RAM üzerinde tuttuğu için okuma/yazma performansı çok yüksektir. Gerekli durumlarda veriyi diske de yazabilir.
    
- **Veri Yapısı:** Temel olarak **Anahtar-Değer (Key-Value)** yapısıyla çalışır. Diziler, listeler, setler gibi veri tiplerini destekler.
    
- **Kullanım Alanları:** Web uygulamalarında oturum yönetimi (session management), önbellekleme (caching) ve gerçek zamanlı işlemler için sıkça tercih edilir.
    
- **Varsayılan Port:** TCP **6379**
    

---

## 3. redis-cli ve Temel Bağlantı Parametreleri

`redis-cli`, Redis sunucularına bağlanmak ve onları komut satırından yönetmek için kullanılan varsayılan araçtır.

- **Bağlantı Komutu:**
    
    Bash
    
    ```
    redis-cli -h <hostname_veya_ip> -p <port> --user <kullanici_adi> -a <parola>
    ```
    
    _(Not: Aynı makine üzerinde (localhost) çalışıyorsanız ve varsayılan 6379 portu kullanılıyorsa sadece `redis-cli` yazmak yeterlidir)._
    

## 4. Kritik Redis Komutları (Sızma Testi İçin)

Bağlantı sağlandıktan sonra (komut satırı `IP:6379>` şekline döndüğünde) bilgi toplamak ve veri çekmek için şu komutlar kullanılır:

- `PING` : Sunucunun ayakta olup olmadığını kontrol eder (Cevap genellikle "PONG" döner).
    
- `HELP` : Kullanılabilir komutlar hakkında bilgi verir.
    
- `INFO` : Redis sunucusunun sürümü, yapılandırması, bellek kullanımı ve istatistikleri hakkında çok detaylı bilgi verir. (Zafiyet aramak için sürüm kontrolü burada yapılır).
    
- `MONITOR` : Sunucuya gelen tüm istekleri (sorguları) gerçek zamanlı olarak dinler ve ekrana basar. (Hassas verileri yakalamak için sızma testlerinde çok değerlidir).
    
- `KEYS *` : Veritabanındaki **tüm anahtarları (keys)** listeler. Hedefteki verilerin haritasını çıkarmak için ilk çalıştırılan komutlardandır.
    
- `GET <anahtar_adi>` : Belirtilen anahtarın içindeki değeri (value) okur. (Örneğin: `GET session:admin-001`).
    
- `SET <anahtar_adi> <deger>` : Veritabanına yeni bir anahtar ve değer ekler/değiştirir.
    
- `QUIT` : Sunucu bağlantısını kapatır.
    

---

## 5. Sızma Testi Metodolojisi (Redis Özeti)

1. **Keşif:** Nmap taraması yapılarak (`nmap -sV hedef_ip`) 6379 portunda Redis servisinin çalıştığı doğrulanır.
    
2. **Erişim Testi:** `redis-cli -h hedef_ip` komutuyla şifresiz (anonim) bağlantı kabul edilip edilmediği test edilir.
    
3. **Bilgi Toplama:** Başarılı bağlantı sonrası `INFO` komutuyla sunucu detayları incelenir.
    
4. **Veri Çekme:** `KEYS *` komutu ile sistemdeki tüm anahtarlar listelenir. Aralarında "admin", "session", "token", "password" gibi kritik kelimeler barındıran anahtarlar aranır.
    
5. **Sömürü:** Bulunan kritik anahtarların içerikleri `GET` komutu ile okunarak yetki yükseltme veya sisteme sızma amacıyla kullanılır.