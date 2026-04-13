# Web Güvenliği ve Performans Temelleri


Modern web uygulamalarının başarısı ve kullanıcı deneyimi, sistemin ne kadar güvenli ve performanslı (hızlı) çalıştığına doğrudan bağlıdır. Bu iki hedefi sağlamak için çeşitli altyapı servisleri kullanılır.

## 1. Güvenlik ve Yük Dağıtımı

### WAF (Web Application Firewall - Web Uygulama Güvenlik Duvarı)
Web uygulamalarını HTTP/HTTPS seviyesinde koruyan özel bir güvenlik duvarıdır. SQL Enjeksiyonu (SQLi), XSS, CSRF ve DDoS gibi saldırıları engeller.
* **DDoS Koruma Stratejileri:**
  * *Trafik Analizi:* Anormal istekleri tespit eder.
  * *Oran Limiti (Rate Limiting):* Belirli bir sürede yapılabilecek maksimum istek sayısını sınırlar.
  * *Coğrafi (Geo) Bloklama:* Saldırı gelen belirli ülkeleri/bölgeleri engeller.
  * *Davranışsal Bloklama:* Bot trafiğini (insan gibi davranmayan istekleri) engeller.
* *Örnek:* Cloudflare.

### Load Balancer (Yük Dengeleyici)

Gelen kullanıcı isteklerini, arkada çalışan birden fazla sunucu arasında (Round-robin vb. algoritmalarla) paylaştıran sistemdir. 
* Tek bir sunucunun çökmesini engeller, yüksek trafikli siteleri ayakta tutar. 
* Aynı zamanda **Reverse Proxy (Ters Proxy)** olarak çalışarak ana sunucuların IP adreslerini gizler.

---

## 2. Performans ve Optimizasyon

### CDN (Content Delivery Network - İçerik Dağıtım Ağı)

Görsel, video, CSS, JS gibi statik dosyaları dünyanın farklı yerlerindeki sunucularda (Edge Servers) kopyalayarak barındıran ağdır. Kullanıcı siteye girdiğinde, veriler ana sunucudan değil, **kullanıcıya coğrafi olarak en yakın** sunucudan gelir. Sayfa yüklenme süresini (Latency) muazzam ölçüde düşürür.

### Caching (Önbellekleme)
Sık erişilen verilerin, tekrar tekrar veritabanından sorgulanmak yerine RAM gibi çok hızlı belleklere (Geçici Hafıza) kaydedilmesidir. (Örn: Bir haber sitesindeki anasayfa haberlerinin önbelleğe alınarak binlerce kişiye anında gösterilmesi).

### Connection Pooling (Bağlantı Havuzu)
Veritabanına bağlanmak (TCP el sıkışması, kimlik doğrulama) zaman alan, maliyetli bir işlemdir. Connection pooling, veritabanı bağlantılarını bir havuzda açık olarak bekletir. Uygulama veritabanına işi düştüğünde sıfırdan bağlanmak yerine havuzdaki **hazır açık bağlantıyı** kullanır.

---

## 3. Sistem Yönetimi ve Arka Plan Servisleri

| Servis Adı | İşlevi | Örnek Teknolojiler |
| :--- | :--- | :--- |
| **Log Sunucusu** | Sistem ve uygulamaların ürettiği olay kayıtlarını (log) tek bir merkezde toplar. Siber olay analizi ve hata ayıklama için hayatidir. | ELK Stack (Elasticsearch, Logstash, Kibana), Splunk |
| **Mail Sunucusu** | E-posta iletişimini sağlar. Gönderim için **SMTP**, alım için **IMAP** (sunucuda tutar) veya **POP3** (cihaza indirir) protokolleri kullanılır. | Microsoft Exchange, Postfix |
| **Session Servisi** | Kullanıcının oturum bilgilerini (Giriş yaptı mı? Sepetinde ne var?) takip eder. Session ID (Oturum Kimliği) ile çalışır. | Redis (Anahtar-Değer deposu), JWT (Token bazlı) |
| **Felaket Kurtarma (DR)** | Sistem çökmesi, fidye yazılımı (Ransomware) veya donanım arızasına karşı verilerin düzenli yedeklenmesi ve sistemin hızla geri ayağa kaldırılmasıdır. | - |
