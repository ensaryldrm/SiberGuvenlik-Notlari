# TCP Connect Tarama (-sT)


İşletim sisteminin standart ağ bağlantı altyapısını (Berkeley Sockets API) kullanarak hedef portlarla **tam bir TCP bağlantısı (3'lü el sıkışma)** kuran tarama türüdür. Nmap, özel (raw) paketler üretmek yerine işletim sistemine "Şu adrese bağlan" komutu verir.

## 1. Ne Zaman Kullanılır?
* Makinede **Root / Administrator yetkiniz yoksa** (Örneğin standart bir kullanıcı hesabı ele geçirdiyseniz ve içeriden ağı taramak istiyorsanız).
* **IPv6** ağlarında tarama yapmanız gerektiğinde.

## 2. Nasıl Çalışır? (Trafiğin Arka Planı)
SYN (Yarı-Açık) taramasının aksine, bağlantı işlemi yarım bırakılmaz, işletim sistemi seviyesinde tamamlanır.

1. **Bağlantı İsteği:** Nmap hedef porta bir **SYN** paketi gönderir.
2. **Hedefin Yanıtı:** Port açıksa, hedef sistem **SYN/ACK** paketi ile döner.
3. **Bağlantının Tamamlanması:** Nmap, hedefe bir **ACK** paketi gönderir. *(İşte bu noktada TCP bağlantısı tam olarak kurulmuş olur).*
4. **Bağlantının Kesilmesi:** Nmap portun açık olduğunu işletim sisteminden öğrenir öğrenmez, veri alışverişine girmeden bağlantıyı bir **RST** paketi ile aniden koparır.

## 3. Kullanımı
```bash
nmap -sT hedef_ip
````

_(Not: Bu tarama root yetkisi gerektirmez. Standart kullanıcılar da çalıştırabilir.)_

## 4. Avantajları ve Dezavantajları

**Avantajları:**

- Özel yetkilere (raw socket) ihtiyaç duymaz, herhangi bir kullanıcı hesabı ile her ortamda çalıştırılabilir.
    
- IPv6 desteği sorunsuzdur.
    

**Dezavantajları (Neden İlk Tercih Değildir?):**

- **Çok Gürültülüdür (Log Bırakır):** TCP bağlantısı tam olarak kurulduğu için, hedefin üzerindeki Apache, Nginx, SSH gibi uygulamalar bu bağlantıyı **log dosyalarına (kayıtlarına) yazar**. Hedef sistem yöneticisi veya güvenlik cihazları (IDS/IPS) tarama yapıldığını çok kolay ve net bir şekilde tespit eder.
    
- **Daha Yavaştır:** SYN taramasına kıyasla ağda daha fazla paket trafiği yaratır ve bağlantıların tamamlanmasını beklediği için daha uzun sürer.