# WHOIS Sorgulaması ve Bilgi Toplama

Siber güvenlikte pasif bilgi toplama aşamasının en temel adımlarından biri WHOIS sorgusudur. Hedef sistemle hiçbir doğrudan temas kurmadan, sadece alan adının (domain) kayıtlı olduğu açık veri tabanları üzerinden kritik istihbarat elde etmeyi sağlar.

## 1. WHOIS Nedir?
WHOIS, bir alan adının veya IP adresinin arkasındaki yasal sahibini, iletişim bilgilerini ve teknik altyapısını öğrenmek için kullanılan bir sorgulama/yanıt protokolüdür. Hedefin kimliğini ve altyapı sağlayıcılarını haritalandırmak için kullanılır.

## 2. Sorgulama Yöntemleri
WHOIS sorguları iki farklı şekilde yapılabilir:

* **Web Tabanlı Araçlar:** Terminal erişimi olmayan durumlarda veya görsel arayüz istenildiğinde kullanılır. (Örn: *ICANN Whois, whois.com, DomainTools*)
* **Komut Satırı (CLI) Araçları:** Linux/Unix sistemlerde doğrudan terminal üzerinden en hızlı ve en ham veriyi almak için kullanılır.

```bash
  whois hedefsite.com
```

## 3. Örnek Bir WHOIS Çıktısının Analizi

Terminal üzerinden `whois google.com` komutu çalıştırıldığında gelen uzun çıktıdaki en kritik veriler ve anlamları aşağıda özetlenmiştir:

### A. Domain Sahibi ve İletişim Bilgileri

Sitenin yasal olarak kime veya hangi şirkete ait olduğunu gösterir.

- `Registrant Organization: Google LLC`
    
- `Registrant Country: US`
    
- _Siber Güvenlik Açısından:_ Hedefin fiziksel lokasyonunu ve yasal şirket adını doğrulamak, gerektiğinde sosyal mühendislik (OSINT) senaryoları üretmek için kullanılır.
    

### B. Kayıt ve Bitiş Tarihleri (Creation / Expiry Dates)

Alan adının ne zaman alındığını ve süresinin ne zaman dolacağını gösterir.

- `Creation Date: 1997-09-15` (Kayıt Tarihi)
    
- `Registry Expiry Date: 2028-09-14` (Bitiş Tarihi)
    
- `Updated Date: 2019-09-09` (Son Güncelleme)
    
- _Siber Güvenlik Açısından:_ Yeni açılmış (1-2 günlük) domainler genellikle oltalama (phishing) veya geçici C2 (Komuta Kontrol) sunucuları olabilir. Eski ve köklü domainler ise genellikle daha güvenilirdir.
    

### C. Kayıt Edici Firma (Registrar)

Alan adının hangi firma üzerinden satın alındığını gösterir.

- `Registrar: MarkMonitor, Inc.`
    
- _Siber Güvenlik Açısından:_ Alan adının barındırıldığı firmayı bilmek, hedefin kullandığı altyapı servisleri hakkında fikir verir.
    

### D. İsim Sunucuları (Name Servers - NS)

Alan adının trafiğini yönlendiren DNS sunucularıdır.

- `Name Server: ns1.google.com`
    
- `Name Server: ns2.google.com`
    
- _Siber Güvenlik Açısından:_ İsim sunucuları genellikle sitenin gerçekte nerede barındırıldığını (Hosting/CDN) ele verir. Örneğin, isim sunucularında `cloudflare.com` görülüyorsa, hedefin gerçek IP adresinin bir WAF (Web Application Firewall) arkasında gizlendiği anlaşılır.