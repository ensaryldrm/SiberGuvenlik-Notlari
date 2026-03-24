# Host Keşfi ve Hedef Belirleme (Host Discovery)


Nmap, varsayılan olarak bir hedefin portlarını taramaya başlamadan önce o hedefin gerçekten açık (up) olup olmadığını kontrol etmek için bir **Ping Taraması (ICMP Echo)** yapar. Eğer hedef pinge cevap vermezse, Nmap o IP'yi "ölü" (down) kabul eder ve port taramasına hiç geçmez. Bu durum zaman kazandırır ancak güvenlik duvarları (Firewall) genellikle ping isteklerini engellediği için bizi yanıltabilir.

İşte bu süreci kontrol etmek için kullandığımız temel Host Keşfi parametreleri:

## 1. Liste Taraması (-sL)
Hedef ağa **hiçbir paket göndermez**. Sadece tarayacağı IP adreslerinin bir listesini çıkarır ve bu IP'lerin isimlerini (Reverse-DNS ile) bulmaya çalışır. 
* **Ne işe yarar?:** Yanlışlıkla başka bir şirketin/kurumun ağına saldırmamak için "doğru hedefleri mi tarıyorum?" diye bir gerçeklik kontrolü (sanity check) yapmak için kullanılır.
```bash
nmap -sL 192.168.1.0/24
````

## 2. Port Taramasını Kapatma / Sadece Ping Taraması (-sn)

Eski adıyla `-sP` olarak bilinir. Nmap'e "Sadece cihazın ayakta olup olmadığını kontrol et, eğer açıksa bile kesinlikle portlarını (80, 22 vb.) taramaya kalkma" deriz.

- **Ne işe yarar?:** Ağda (Subnet) o an kaç cihazın aktif olduğunu çok hızlı bir şekilde saymak veya ağ haritası çıkarmak için kullanılır. Çok az ses çıkarır.
    

Bash

```
nmap -sn 10.0.0.0/24
```

## 3. Ping Taramasını Kapatma / Hedefi Kesin Açık Kabul Etme (-Pn)

Nmap'e "Hedefe ping atma, cevap vermese bile onu açık (up) kabul et ve doğrudan portlarını taramaya başla" deriz.

- **Ne işe yarar?:** Sistemde bir Firewall (Güvenlik Duvarı) varsa ve ping (ICMP) isteklerini blokluyorsa, cihaz aslında açık olsa bile Nmap onu "ölü" sanıp es geçer. `-Pn` parametresi bu engeli aşmamızı ve hedefin açık portlarını zorla taramamızı sağlar. **(CTF'lerde hedefe ulaşamadığında ilk denemen gereken parametredir).**
    

Bash

```
nmap -Pn 192.168.1.10
```

## 4. Subnet (Alt Ağ) Taraması

Bir şirketin veya evin iç ağındaki tüm olası cihazları taramak için CIDR notasyonu (`/24`, `/16` vb.) kullanılır.

- `/24` notasyonu, o bloğun son hanesindeki (oktet) 256 ihtimali (0-255) tarayacağı anlamına gelir. (Örn: 192.168.1.0'dan 192.168.1.255'e kadar).
    

Bash

```
nmap 192.168.1.0/24
```

---