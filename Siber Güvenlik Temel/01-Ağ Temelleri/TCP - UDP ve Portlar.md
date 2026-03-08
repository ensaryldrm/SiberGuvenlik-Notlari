## Port Nedir? 
IP adresi bir apartmanın dış kapı numarasıysa, **Port** o apartmanın içindeki daire numaralarıdır. Bir bilgisayara gelen verinin hangi uygulamaya (Web, E-posta, Oyun) gideceğini belirler. Toplam 65.535 port vardır. 
### En Kritik Portlar (Siber Güvenlik İçin) 
* **21:** FTP (Dosya Transferi) 
* **22:** SSH (Güvenli Uzaktan Bağlantı - Kritik!) 
* **53:** DNS (İsim Çözümleme) 
* **80:** HTTP (Şifresiz Web Trafiği) 
* **443:** HTTPS (Şifreli Web Trafiği) 

## TCP vs UDP Karşılaştırması (Taşıma Katmanı) 
| Özellik | TCP (Transmission Control Protocol) | UDP (User Datagram Protocol) |
| --- | --- | --- |
| **Bağlantı Tipi** | Bağlantı Yönelimli (Connection-oriented) | Bağlantısız (Connectionless) | 
| **Güvenilirlik** | %100 Güvenilir. Giden verinin ulaştığını teyit eder (3-Way Handshake) | Güvenilir değil. Veriyi yollar ve ulaştı mı diye bakmaz | 
| **Hız** | Yavaştır (Kontrol mekanizmaları yüzünden) | Çok Hızlıdır | 
| **Kullanım Alanı** | Web Siteleri (HTTP), Dosya İndirme, E-posta | Canlı Yayınlar, Online Oyunlar, DNS Sorguları |