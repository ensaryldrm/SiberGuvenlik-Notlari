# Gelişmiş OSINT ve Çok Amaçlı Keşif Araçları
Pasif bilgi toplama sürecinde tek bir araca güvenmek yerine, farklı veri kaynaklarını (arama motorları, DNS veritabanları, sosyal ağlar) tarayan hibrit araçlar kullanmak çok daha geniş bir saldırı yüzeyi haritası çıkarmanızı sağlar.

## 1. theHarvester
theHarvester, tamamen açık kaynak istihbaratına (OSINT) dayalı, hedef hakkında e-posta adresleri, alt alan adları (subdomain), IP adresleri ve çalışan isimlerini toplayan çok güçlü bir Python aracıdır.

* **Nasıl Çalışır?** Google, Bing, LinkedIn, Shodan gibi onlarca farklı kaynaktan gelen verileri birleştirir.
* **Siber Güvenlikteki Önemi:** Topladığı e-posta adresleri üzerinden **Sosyal Mühendislik / Oltalama** (Phishing) saldırıları planlanabilir; bulduğu gizli host isimleri ise sisteme giriş noktası olabilir.
* **Temel Komut:**

```bash
  theharvester -d hedefsite.com -b all
```

_(Burada `-d` domaini, `-b all` ise tüm kaynakların (Google, Bing vb.) kullanılacağını belirtir.)_

---

## 2. Çevrimiçi Analiz Platformları

Terminal kullanmadan tarayıcı üzerinden derinlemesine teknik analiz sunan "Hepsi Bir Arada" servislerdir.

### A. Netcraft (Sitereport)

Bir web sitesinin teknolojik özgeçmişini sunar. Sitenin ilk ne zaman görüldüğü, hangi hosting firmasında barındığı, SSL sertifika geçmişi ve işletim sistemi gibi detayları raporlar.

- **Bağlantı:** [sitereport.netcraft.com](https://sitereport.netcraft.com/)
    
- **Kritik Bilgi:** Hedefin eskiden hangi IP'lerde barındığını (IP History) görmek, WAF arkasına gizlenmiş ana sunucuyu bulmaya yardımcı olabilir.
    

### B. ViewDNS.info

DNS dünyasının "İsviçre Çakısı"dır. Ters DNS (Reverse IP), WHOIS, IP Lokasyonu ve bir sunucuda barınan diğer web sitelerini (Reverse IP Lookup) bulmak için kullanılır.

- **Bağlantı:** [viewdns.info](https://viewdns.info/)
    

### C. MXToolbox

Öncelikle e-posta (MX) kayıtlarını analiz etmek için tasarlanmış olsa da; DNS sorguları, SSL/TLS sertifika hataları ve hedefin herhangi bir kara listede (Blacklist) olup olmadığını kontrol etmek için eşsizdir.

- **Bağlantı:** [mxtoolbox.com](https://mxtoolbox.com/)

---

## Özet Tablo: Hangi Aracı Ne Zaman Kullanmalı?

|İhtiyaç Duyulan Bilgi|Tercih Edilecek Araç|
|---|---|
|Çalışan e-postaları ve Subdomainler|**theHarvester**|
|Geçmiş IP kayıtları ve Hosting geçmişi|**Netcraft**|
|Aynı sunucudaki diğer web sitelerini bulma|**ViewDNS (Reverse IP)**|
|Mail sunucusu ve Güvenlik sertifikası analizi|**MXToolbox**|
