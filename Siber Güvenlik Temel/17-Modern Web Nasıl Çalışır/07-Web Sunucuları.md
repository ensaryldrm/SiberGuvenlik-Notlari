# Web Sunucusu (Web Server) Temelleri
## 1. Web Sunucusu Nedir?
Web sunucusu, internet üzerinden kullanıcıların (tarayıcıların) HTTP/HTTPS protokolü ile gönderdiği istekleri karşılayan ve onlara web sayfalarını (HTML, CSS, JavaScript, Medya) sunan sistemdir. 
* *Tarihçe:* İlk web sunucusu 1990 yılında Tim Berners-Lee tarafından CERN'de World Wide Web projesi için geliştirilmiştir.

---

## 2. Popüler Web Sunucusu Yazılımları
Modern web sunucuları statik içeriklerin yanında dinamik içerikleri de işler. Genellikle yapılandırma (config) dosyaları ile yönetilirler.

### A. Apache HTTP Server
Açık kaynaklı, esnek ve modüler bir web sunucusudur. Dizin bazında yetkilendirme için `.htaccess` dosyalarını kullanır.
* **Yapılandırma Örneği (Sanal Sunucu - Virtual Host):**

```apache
<VirtualHost *:80>
    ServerName [www.example.com](https://www.example.com)
    DocumentRoot "/www/example"
    <Directory "/www/example">
        AllowOverride All
        Require all granted
    </Directory>
</VirtualHost>
````

### B. Nginx (Engine-X)

Yüksek eşzamanlılık (asenkron yapı) ve düşük bellek kullanımı ile öne çıkar. Genellikle yüksek trafikli sitelerde **Ters Proxy (Reverse Proxy)** ve yük dengeleyici olarak kullanılır.

- **Yapılandırma Örneği (Ters Proxy):**

```Nginx
server {
    listen 80;
    server_name example.com;

    location / {
        proxy_pass http://localhost:3000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }
}
```

### C. Microsoft IIS (Internet Information Services)

Windows sunucular için özel olarak geliştirilmiştir. ASP.NET ekosistemiyle derin entegrasyona sahiptir ve genellikle grafik arayüz (GUI) üzerinden yönetilir.

- **Yapılandırma Örneği (Komut Satırı / appcmd):**

```DOS
appcmd add site /name:example /bindings:http/*:80:example.com /physicalPath:C:\inetpub\example
```

### D. Tomcat

Apache Software Foundation tarafından geliştirilen, özellikle **Java** servletlerini ve JSP (JavaServer Pages) sayfalarını çalıştırmak için kullanılan bir web konteyneridir.

- **Yapılandırma Örneği (server.xml - Connector Ayarı):**

```XML
<Connector port="8080" protocol="HTTP/1.1"
           connectionTimeout="20000"
           redirectPort="8443" />
```

---

## 3. İstek-Yanıt Döngüsü (Request-Response Cycle)

1. **İstek (Request):** Kullanıcı tarayıcıya URL'yi girer. Tarayıcı, hedef IP'deki web sunucusuna bir HTTP isteği (Genellikle GET) gönderir.
    
2. **İşleme (Processing):** Web sunucusu gelen isteği analiz eder, hangi dizine veya uygulamaya gitmesi gerektiğini yapılandırma dosyalarına göre belirler.
    
3. **Yanıt (Response):** İstenen dosya (HTML, Görsel vb.) bulunursa HTTP 200 (OK) koduyla tarayıcıya gönderilir. Bulunamazsa HTTP 404 (Not Found) gibi bir hata kodu döndürülür.
    

---

## 4. Güvenlik ve Performans

Web sunucuları doğrudan internete açık oldukları için kritik hedeflerdir.

- **Güvenlik Önlemleri:** İletişimi şifrelemek için SSL/TLS sertifikaları, DDoS, XSS ve SQL Enjeksiyonu gibi saldırılara karşı WAF (Web Application Firewall) kullanılır.
    
- **Performans İyileştirmeleri:** Yüksek trafiği kaldırmak için Önbellekleme (Caching), Yük Dengeleme (Load Balancing) ve global olarak hızlı erişim için İçerik Dağıtım Ağları (CDN) entegre edilir.