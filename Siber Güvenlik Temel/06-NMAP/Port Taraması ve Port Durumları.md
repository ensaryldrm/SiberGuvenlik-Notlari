# Port Taraması ve Port Durumları

Hedef cihaz ayakta (up) ise, bir sonraki adım sızabileceğimiz bir "kapı" yani açık bir **Port** bulmaktır. Toplamda 65.535 adet port vardır ve her servis standart olarak belirli bir portu dinler.

## 1. Siber Güvenlikte En Kritik Portlar
Sızma testlerinde (CTF'lerde) ilk olarak bu portların açık olup olmadığına bakılır ve zafiyetler genellikle buralardan çıkar:

| Port | Servis | Neden Önemli? (Saldırı Yüzeyi) |
| :--- | :--- | :--- |
| **21** | FTP | Dosya transferi. Anonim (şifresiz) giriş izni olup olmadığı kontrol edilir. |
| **22** | SSH | Güvenli terminal erişimi. Brute-force denenebilir veya eski versiyonlarda zafiyet aranır. |
| **23** | Telnet | Şifresiz terminal. Trafik dinlenerek (MitM) parolalar çok kolay çalınır. |
| **25** | SMTP | E-posta gönderimi. Sahte mail atmak veya kullanıcı adlarını tespit etmek için kullanılır. |
| **53** | DNS | Alan adı çözümü. Zone Transfer (Bölge Transferi) zafiyeti aranır. |
| **80/443** | HTTP/HTTPS | Web sunucusu. SQL Injection, XSS, dizin taraması gibi tüm web saldırıları buradan yapılır. |
| **139/445** | SMB/NetBIOS | Windows dosya/yazıcı paylaşımı. Meşhur EternalBlue (MS17-010) zafiyetinin sömürüldüğü porttur. |
| **3306** | MySQL | Veritabanı portu. Dışarıya açık olması başlı başına bir risktir. |
| **3389** | RDP | Windows Uzak Masaüstü. Kaba kuvvet veya BlueKeep zafiyeti denenir. |

---

## 2. Nmap Port Durumları (State)


Nmap tarama sonucunda portun karşısına şu durumlardan birini yazar. Bunu doğru yorumlamak hayati önem taşır:

* **Open (Açık):** En sevdiğimiz durumdur. Portta bir servis aktif olarak dinliyor ve bağlantı kabul ediyor. Saldırıya açıktır.
* **Closed (Kapalı):** Cihaz açık, porta ulaşılabiliyor ama o portu dinleyen (çalışan) hiçbir servis yok.
* **Filtered (Filtrelenmiş):** Nmap gönderdiği paketlere hiçbir yanıt (veya hata) alamadı. Önünde bir **Güvenlik Duvarı (Firewall)** var demektir. Portun gerçekten açık mı yoksa kapalı mı olduğunu bilemeyiz. *(CTF'lerde atlatma (evasion) teknikleri kullanmak gerekir).*
* **Unfiltered (Filtrelenmemiş):** Sadece ACK taramalarında görülür. Porta ulaşılabiliyor (Firewall yok) ama açık mı kapalı mı olduğu bilinemiyor.

---

## 3. Port Tarama Komutları ve Stratejileri

### A. Varsayılan Tarama
Belirtilmezse Nmap en yaygın ilk 1000 portu tarar.
```bash
nmap 192.168.1.10
````

### B. Hızlı Tarama (Fast Scan)

Büyük bir ağı tararken zaman kazanmak için sadece en popüler ilk **100** portu tarar.

```Bash
nmap -F 192.168.1.10

nmap --top-ports <sayı> ip_adresi
```


### C. Spesifik Portları Tarama

Sadece ilgilendiğin servise odaklanmak (ve gürültü yapmamak) için kullanılır.

- **Tek port:** `nmap -p 80 192.168.1.10`
    
- **Birden çok port:** `nmap -p 22,80,445 192.168.1.10`
    
- **Port Aralığı:** `nmap -p 1000-2000 192.168.1.10`
    

### D. Tüm Portları Tarama (Zorunlu CTF Komutu)

Gizlenmiş veya yüksek numaralı (Örn: 31337 veya 8080) portları kaçırmamak için 1'den 65.535'e kadar her yeri tarar. Uzun sürer.

```Bash
nmap -p- 192.168.1.10
```

### E. Agresif Tarama (-A)

Nmap'in İsviçre Çakısıdır. Tek bir komutla işletim sistemini (-O), versiyonları (-sV), scriptleri (-sC) ve hedef rotasını (--traceroute) birlikte çalıştırır. Güvenlik duvarları tarafından **anında fark edilir.**

```Bash
nmap -A 192.168.1.10
```