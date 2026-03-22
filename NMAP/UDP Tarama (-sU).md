# UDP Tarama (-sU)


İnternetin büyük bir kısmı TCP üzerinden çalışsa da DNS (53), DHCP (67/68), SNMP (161) ve NTP (123) gibi çok kritik servisler UDP kullanır. UDP bağlantısız bir protokol olduğu için Nmap hedefe paket gönderdiğinde, hedefin paketi alıp almadığını doğrulaması çok zordur.

## 1. UDP Tarama Nasıl Çalışır?
Nmap, hedef porta boş bir UDP paketi (veya bilinen portlar için o protokole ait özel bir veri yükü) gönderir ve gelecek olan yanıtı veya **hata mesajını** bekler.

**Hedefin Vereceği Tepkilere Göre Port Durumları:**
* **Açık (Open):** Hedef porttan herhangi bir UDP yanıtı (veri) gelirse.
* **Kapalı (Closed):** Hedef sistemden **"ICMP Port Unreachable (Tip 3, Kod 3)"** hata mesajı dönerse. (En kesin sonuçlardan biridir).
* **Filtrelenmiş (Filtered):** Hedef sistemden diğer ICMP erişilemez hataları (Tip 3; Kod 1, 2, 9, 10 veya 13) dönerse. Arada bir güvenlik duvarı paketleri engelliyor demektir.
* **Açık|Filtrelenmiş (Open|Filtered):** Nmap paketi gönderdikten sonra **hiçbir yanıt alamazsa**. UDP'de bir paketin yolda kaybolması veya uygulamanın boş pakete cevap vermemesi çok normaldir. Bu yüzden portun gerçekten açık mı yoksa bir güvenlik duvarı tarafından mı engellendiği (Drop) bilinemez. 

## 2. Kullanım Komutları

Sadece UDP taraması yapmak için (Genellikle root yetkisi gerektirir):
```bash
sudo nmap -sU hedef_ip
````

**🔥 CTF İpucu (Kombinasyon Taraması):** Gerçek bir sızma testinde zaman kazanmak için en sık kullanılan TCP (SYN) taraması ile UDP taraması genellikle aynı komutta birleştirilir:

Bash

```
sudo nmap -sS -sU -p U:53,161,T:22,80 hedef_ip
```

_(Açıklaması: UDP port 53 ve 161'i, TCP port 22 ve 80'i aynı anda tara)._

## 3. UDP Taramanın Zorlukları ve Çözümleri

- **Dehşet Verici Yavaşlık:** Nmap, kaybolan UDP paketlerini telafi etmek için sürekli paketi tekrar gönderir (Retransmission) ve sistemlerin hız sınırlarına (rate limiting) takılır. Tüm 65.535 UDP portunu taramak günlerce sürebilir.
    
    - _Çözüm:_ Sadece en popüler UDP portlarını taramak. (`nmap -sU --top-ports 20 hedef_ip`)
        
- **Open|Filtered Belirsizliği:** Nmap cevap alamadığı portlara bu etiketi basar. Eğer bir portun gerçekten açık olup olmadığını doğrulamak istiyorsanız, o servise özgü scriptler (NSE) veya `-sV` (Versiyon Tespiti) parametresini kullanmanız gerekir.