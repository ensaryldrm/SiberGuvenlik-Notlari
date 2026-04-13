# DNS Enumeration (DNS Keşfi) ve Sorgulama


DNS (Domain Name System), karmaşık IP adreslerini (`172.217.17.110`) insanların anlayabileceği alan adlarına (`youtube.com`) çeviren internetin telefon rehberidir. 

**DNS Enumeration (DNS Keşfi)** ise bir sızma testi uzmanının, hedefin e-posta sunucularını, alt alan adlarını (subdomain), doğrulama mekanizmalarını ve ağ haritasını çıkarmak için bu telefon rehberini detaylıca sorgulaması işlemidir.

## 1. Temel DNS Kayıt Türleri
Bir hedefin altyapısını anlamak için hangi kaydın ne işe yaradığını bilmek kritik öneme sahiptir:

| Kayıt Türü | Açıklama ve Siber Güvenlikteki Önemi |
| :--- | :--- |
| **A** | Alan adını **IPv4** adresine çevirir. Hedefin ana sunucusunun yerini söyler. |
| **AAAA** | Alan adını **IPv6** adresine çevirir. |
| **CNAME** | (Canonical Name) Bir alan adını başka bir alan adına yönlendirir. (Subdomain keşiflerinde sıkça karşılaşılır). |
| **MX** | (Mail Exchange) E-postaların hangi sunucuya gideceğini belirtir. Hedefin mail altyapısını (Örn: Google Workspace, Microsoft 365) ele verir. |
| **NS** | (Name Server) Alan adının DNS kayıtlarını tutan yetkili sunucudur. Hedefin hangi hosting/CDN firmasını kullandığını gösterir. |
| **TXT** | Metin tabanlı bilgilerdir. Genellikle SPF, DMARC gibi e-posta doğrulama politikalarını barındırır. (Eksikliği, e-posta sahteciliği / Spoofing zafiyetine yol açar). |
| **SOA** | (Start of Authority) DNS bölgesinin yönetimsel bilgilerini (Örn: Yönetici e-posta adresi) içerir. |
| **PTR** | (Pointer) **Ters DNS** kaydıdır. Bir IP adresinden alan adını bulmaya yarar (A kaydının tam tersi). |

---

## 2. DNS Bilgi Toplama Araçları
Hedefin DNS haritasını çıkarmak için hem web tabanlı hem de komut satırı araçları kullanılır.

* **DNSdumpster:** Web tabanlı, çok güçlü bir OSINT aracıdır. Hedefin DNS yapısını görsel bir harita (grafik) olarak sunar ve gizli kalmış alt alan adlarını bulmada çok etkilidir.
* **host:** Hızlı ve basit sorgular için kullanılan temel komut satırı aracıdır. (`host youtube.com`)
* **nslookup:** Hem interaktif hem de tek satırlık sorgular yapabilen klasik DNS aracıdır. (`nslookup google.com`)

---

## 3. `dig` Komutu Hızlı Referans (Cheat Sheet)
`dig` (Domain Information Groper), siber güvenlik uzmanlarının en çok kullandığı, en detaylı çıktıyı veren DNS aracıdır. 

*Not: Çıktılarda asıl aradığımız bilgi her zaman **`;; ANSWER SECTION:`** başlığı altındadır.*

**A ve AAAA (IP Adresi) Sorgulama:**
```bash
dig A youtube.com      # IPv4 adresini getirir
dig AAAA youtube.com   # IPv6 adresini getirir
````

**MX (Mail Sunucusu) Sorgulama:**

```Bash
dig MX youtube.com
# Çıktı Örneği: youtube.com. 300 IN MX 0 smtp.google.com.
```

**NS (İsim Sunucusu) Sorgulama:**

```Bash
dig NS youtube.com
# Çıktı Örneği: youtube.com. 21600 IN NS ns1.google.com.
```

**TXT (Metin ve Güvenlik Politikaları) Sorgulama:**

```Bash
dig TXT youtube.com
# Çıktı Örneği: youtube.com. 3600 IN TXT "v=spf1 include:google.com mx -all"
```

**PTR (Ters DNS - Reverse Lookup) Sorgulama:** Elbette IP adresini yazarken `dig -x` parametresi kullanılır.

```Bash
dig -x 172.217.17.110
# Çıktı Örneği: 110.17.217.172.in-addr.arpa. 8008 IN PTR sof02s47-in-f14.1e100.net.
```