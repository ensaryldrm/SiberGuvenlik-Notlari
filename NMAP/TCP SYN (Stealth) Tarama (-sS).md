# TCP SYN (Stealth) Tarama (-sS)
Nmap'i "Administrator" veya "Root" yetkileriyle (örneğin `sudo nmap`) çalıştırdığında varsayılan olarak kullanılan, en hızlı ve en popüler port tarama yöntemidir. 

Diğer adı **Half-Open (Yarı Açık)** taramadır. Sebebi ise TCP'nin meşhur 3'lü el sıkışmasını (3-way handshake) bilerek tamamlamamasıdır.

## 1. Nasıl Çalışır? (Trafiğin Arka Planı)
Normal bir TCP bağlantısında (SYN -> SYN/ACK -> ACK) adımları izlenir. Ancak SYN taraması hedefe çaktırmadan şu adımları uygular:

1. **Nmap (Saldırgan):** Hedef porta bir **SYN** (Merhaba) paketi gönderir.
2. **Hedef Sistem:** Eğer port açıksa **SYN/ACK** (Merhaba, buyur gel) paketiyle yanıt verir.
3. **Nmap (Saldırgan):** Portun açık olduğunu anladığı an bağlantıyı kurmak yerine aniden **RST** (Reset - İptal) paketi göndererek iletişimi koparır. 

*Eğer port kapalıysa hedef doğrudan RST/ACK paketi döner. Eğer arada bir Firewall (Güvenlik Duvarı) varsa hedef hiçbir şey dönmez (Drop) ve Nmap portu "Filtrelenmiş (Filtered)" olarak işaretler.*

## 2. Kullanımı ve Çıktı Analizi

```bash
sudo nmap -sS -p 22,113,139 hedef_ip
````

_(Not: Bu tarama alt seviye ağ paketleri ürettiği için kesinlikle **Root yetkisi** gerektirir.)_

**Örnek Çıktı Yorumlama:**

- `22/tcp open ssh` : Hedef SYN paketimize SYN/ACK ile döndü. Port kesinlikle açık.
    
- `139/tcp filtered netbios-ssn` : Hedef SYN paketimize hiçbir cevap vermedi (veya ICMP hata mesajı döndü). Önünde bir güvenlik duvarı (Firewall) var, içeri sızamıyoruz.
    

## 3. Neden En Çok Bu Tarama Kullanılır? (Avantajları)

- **Gizlilik (Düşük Profil):** Bağlantı (3-way handshake) hiçbir zaman tamamlanmadığı için, hedef sunucunun üzerindeki Apache, Nginx veya SSH gibi uygulamalar bu bağlantıyı **log dosyalarına (kayıtlarına) yazmaz**. (Uygulama seviyesinde gizlilik sağlar).
    
- **Muazzam Hız:** Binlerce portu, tam bağlantı kurmayı beklemeden saniyeler içinde tarayabilir.
    
- **Net ve Güvenilir:** Açık, kapalı ve filtrelenmiş portları en kesin ayırt eden yöntemdir.
    

## 4. Dikkat Edilmesi Gerekenler

Adı "Stealth (Gizli)" olsa da, modern ağlardaki IDS/IPS (Saldırı Tespit ve Engelleme Sistemleri) ve gelişmiş güvenlik duvarları saniyede yüzlerce yarım kalan SYN paketi gördüğünde bunun bir Nmap taraması olduğunu anında anlar ve IP adresini bloklar. Gerçek bir sızma testinde tarama hızını (`-T` parametresiyle) düşürmek gerekebilir.