# Auxiliary (Yardımcı) Modüller

Auxiliary modülleri, hedefe doğrudan sızmayan (exploit etmeyen) ve sisteme zararlı kod (payload) enjekte etmeyen modüllerdir. Sistemin kapısını kırmazlar, ancak kapının kilidini inceler, kapının arkasını dinler veya kapıyı sürekli çalarak sistemi yorarlar.

## 1. Auxiliary Modül Kategorileri
Sızma testlerinde kullanım amaçlarına göre altı ana kategoriye ayrılırlar:

* **Scanner (Tarayıcılar):** Nmap'e benzer şekilde ağdaki cihazları, açık sportları ve bilinen zafiyetleri tarar (En çok kullanılan kategoridir).
* **Gather (Veri Toplama):** Hedef sistemden pasif veya aktif olarak bilgi (kullanıcı adları, e-posta adresleri, versiyon bilgileri) çeker.
* **Analyze (Analiz):** Parola kırma (brute-force) veya zafiyet analizi gibi işlemleri gerçekleştirir.
* **Admin (Yönetim):** Hedefte veya kendi sisteminizde idari değişiklikler yapar.
* **DoS (Hizmet Reddi):** Hedef servisi veya makineyi trafiğe boğarak çökertmeyi veya yavaşlatmayı hedefler (Sisteme sızmaz, sadece erişilemez hale getirir).
* **Server (Sunucu Desteği):** Kendi makinenizde sahte bir FTP, SMB veya HTTP sunucusu ayağa kaldırarak hedefin size bağlanmasını veya dosya çekmesini sağlar.

---

## 2. Web Scraping Uygulaması (HTTP ve HTTPS)


Bir web sunucusunda çalışan sayfanın `<title>` (Başlık) etiketini veya dizin yapısını çekmek, hedefin ne işe yaradığını anlamak için harika bir keşif yöntemidir.

**A. Standart HTTP (Port 80) İçin Uygulama:**
```bash
msfconsole
use auxiliary/scanner/http/scraper
set RHOSTS hedef_ip_veya_domain
set RPORT 80
run
````

**B. HTTPS (Port 443) İçin Uygulama (Güvenli Bağlantı):** Eğer hedef SSL/TLS sertifikası kullanıyorsa (HTTPS), standart portu değiştirip SSL modunu aktif etmeniz gerekir:

```Bash
use auxiliary/scanner/http/scraper
set RHOSTS hedef_ip_veya_domain
set RPORT 443
set SSL true
run
```