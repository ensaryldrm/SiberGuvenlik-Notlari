# Nmap Temel Komutları ve Parametreleri

Nmap komutlarının temel dizilimi şu şekildedir:
`nmap [Tarama Türü] [Seçenekler] [Hedef IP/Domain]`

## 1. Hedef Belirleme (Target Specification)
* `nmap 192.168.1.1` : Tek bir IP'yi tarar.
* `nmap 192.168.1.1-50` : 1 ile 50 arasındaki IP'leri tarar.
* `nmap 192.168.1.0/24` : Tüm bir alt ağı (Subnet) tarar.
* `nmap -iL hedef_listesi.txt` : İçinde IP'lerin olduğu bir metin dosyasındaki herkesi tarar.

## 2. Tarama Türleri (Scan Techniques)
* `-sS` **(SYN Scan - Stealth Scan):** En yaygın taramadır. Tam bağlantı kurmadan (TCP el sıkışmasını tamamlamadan) sadece SYN bayrağı göndererek hızlı ve gizli tarama yapar. Root yetkisi gerektirir.
* `-sT` **(TCP Connect Scan):** TCP bağlantısını (3-way handshake) tamamen bitirir. Çok ses çıkarır, loglarda iz bırakır ama root yetkisi gerektirmez.
* `-sU` **(UDP Scan):** UDP portlarını tarar (DNS, DHCP gibi). Çok yavaştır.

## 3. Host Keşfi (Host Discovery)
* `-sn` **(Ping Scan):** Portları taramaz, sadece "Ağdaki hangi cihazlar açık?" sorusunun cevabını verir. Hızlı ağ haritalaması için kullanılır.
* `-Pn` **(No Ping):** Hedef ping isteklerini (ICMP) engelliyorsa, "Hedefi kesin açık kabul et ve port taramasına geç" demek için kullanılır. (Güvenlik duvarı olan sistemlerde hayat kurtarır).

## 4. Port Belirleme (Port Specification)
Nmap varsayılan olarak en çok bilinen ilk 1000 portu tarar.
* `-p 80` : Sadece 80. portu tarar.
* `-p 22,80,443` : Belirtilen portları tarar.
* `-p 1-10000` : 1 ile 10.000 arasındaki portları tarar.
* `-p-` : Tüm 65.535 portu eksiksiz tarar. (CTF'lerde gizli portları bulmak için **şarttır**).
* `-F` **(Fast Scan):** En yaygın ilk 100 portu çok hızlıca tarar.

## 5. Keşif ve Bilgi Toplama (Service & OS Detection)
En çok puan getiren parametreler bunlardır:
* `-sV` **(Version Detection):** Açık portların arkasında çalışan servisin adını ve **tam sürümünü (versiyonunu)** bulur. (Örn: Sadece SSH açık demez, "OpenSSH 7.2p2" der). Zafiyet aramak için zorunludur.
* `-O` **(OS Detection):** Hedefin işletim sistemini tahmin eder.
* `-sC` **(Default Scripts):** Nmap'in varsayılan güvenlik test betiklerini (NSE) açık portlar üzerinde çalıştırır (Örn: Anonim FTP girişlerini dener).
* `-A` **(Aggressive Scan):** Tek bir harfle `-sV`, `-O`, `-sC` ve `--traceroute` parametrelerinin hepsini birden çalıştırır. Agresiftir ve gürültülüdür.

## 6. Çıktı Alma ve Performans
* `-T<0-5>` **(Timing Template):** Tarama hızını belirler. T0 en yavaş (paranoyak), T5 en hızlıdır. CTF'lerde standart olarak **`-T4`** kullanılır.
* `-v` / `-vv` **(Verbosity):** Ekrana basılan detay seviyesini artırır. Tarama bitmeden açık portları anında görmek için kullanılır.
* `-oN dosya.txt` : Çıktıyı standart metin dosyası olarak kaydeder.
* `-oA dosya_adi` : Çıktıyı hem txt, hem xml hem de greplenebilir formatta aynı anda kaydeder.

---
** En Yaygın CTF Tarama Komutu:**
```bash
nmap -sS -sV -sC -p- -T4 -v HEDEF_IP
```
