# Nmap ve Ağ Temellerine Giriş

Ağ taraması (Network Scanning), bir ağdaki aktif cihazların, bu cihazlarda çalışan servislerin, açık portların ve olası zafiyetlerin tespit edilerek ağın anlık haritasının çıkarılması işlemidir. Bu işlemlerin endüstri standardı aracı **Nmap**'tir.

## 1. Ağ Tarama Çeşitleri
* **Host Tarama (Ping Sweep):** Ağda hangi IP adreslerinin (cihazların) aktif ve ayakta olduğunu bulur.
* **Port Tarama:** Hedef cihazda hangi kapıların (portların) açık olduğunu ve dinlediğini tespit eder.
* **Servis ve Versiyon Tespiti:** Açık portların arkasında hangi yazılımın ve hangi sürümün çalıştığını bulur (Zafiyet aramak için en kritik adımdır).
* **İşletim Sistemi Belirleme (OS Detection):** Hedef cihazın Windows mu, Linux mu yoksa bir ağ cihazı mı olduğunu tahmin eder.

---

## 2. Temel Ağ Kavramları


[Image of TCP/IP model layers compared to OSI model]


Nmap'in nasıl çalıştığını anlamak için bu üçlüyü çok iyi bilmek gerekir:
* **IP (Internet Protocol):** Cihazın ağ üzerindeki fiziksel/mantıksal adresidir (Örn: 192.168.1.10).
* **Port:** Cihaz üzerindeki belirli bir servise açılan mantıksal kapıdır. Bir IP adresinde 65535 adet port bulunabilir (Örn: 80 HTTP, 443 HTTPS, 22 SSH).
* **TCP (Transmission Control Protocol):** İnternet üzerindeki veri iletiminin **güvenilir, sıralı ve kayıpsız** olmasını sağlayan protokoldür. Nmap, taramalarını yaparken hedefin TCP kurallarına vereceği tepkileri ölçerek sonuca ulaşır.

### TCP/IP Katmanları (Dörtlü Mimari)
1. **Uygulama (Application):** Kullanıcının etkileşime girdiği servisler (HTTP, FTP, SSH).
2. **Taşıma (Transport):** Veri aktarımının ve güvenilirliğin yönetildiği katman (TCP, UDP). *Nmap en çok bu katmanda işlem yapar.*
3. **İnternet (Internet):** Paketlerin yönlendirilmesi (IP).
4. **Ağ Erişim (Network Access):** Fiziksel donanım (MAC adresleri, Ethernet) üzerinden iletim.

---

## 3. TCP İletişim Bayrakları (Flags)


Nmap'in kalbi bu bayraklardır. Nmap, hedefe bu bayrakları manipüle ederek gönderir ve gelen cevaba göre portun "Açık", "Kapalı" veya "Filtreli" (Firewall var) olduğuna karar verir.

* **SYN (Synchronize):** Bağlantı başlatmak, tanışmak için gönderilir ("Merhaba, görüşebilir miyiz?").
* **ACK (Acknowledgment):** Gelen paketin alındığını onaylamak için gönderilir ("Mesajını aldım").
* **FIN (Finish):** İletişimi normal yollarla, nazikçe bitirmek için gönderilir ("İşim bitti, görüşmek üzere").
* **RST (Reset):** Bağlantıyı aniden koparmak veya reddetmek için kullanılır ("Bağlantıyı kes!" veya "Burada kimse yok!").
* **PSH (Push):** Verinin tampon belleğe (buffer) alınmadan derhal uygulamaya iletilmesini ister.
* **URG (Urgent):** Verinin acil olduğunu ve öncelikli işlenmesi gerektiğini belirtir.