# Bilgi Toplama Temelleri
Siber güvenlikte ve sızma testlerinde ilk ve en kritik aşama hedef hakkında bilgi toplamaktır. Amacı; hedefin saldırı yüzeyini anlamak, potansiyel zayıflıkları haritalandırmak ve doğru saldırı/savunma stratejisini geliştirmektir. 

Bilgi toplama süreci metodolojik olarak iki ana kategoriye ayrılır:

## 1. Aktif Bilgi Toplama (Active Reconnaissance)
Hedef sistemin kendisiyle **doğrudan temas ve etkileşim** kurularak yapılan bilgi toplama sürecidir. 
* **Özellikleri:** Hedef sistemin loglarına (kayıtlarına) düşer, iz bırakır ve güvenlik duvarları/IDS sistemleri tarafından algılanabilir. Bu nedenle daha agresiftir ve dikkatli, gizlilik önlemleri alınarak yapılmalıdır.
* **Kullanılan Yöntemler/Araçlar:**
  * Port taramaları (Örn: Nmap)
  * Servis ve versiyon tespiti
  * Zafiyet tarayıcıları (Nessus vb.) ile hedefe paket gönderme

## 2. Pasif Bilgi Toplama (Passive Reconnaissance)
Hedef sistemle **hiçbir doğrudan etkileşime girmeden**, tamamen dış kaynaklar üzerinden hedef hakkında bilgi toplama sürecidir.
* **Özellikleri:** Hedef sistemde hiçbir iz bırakmaz, tamamen gizli ve sessiz bir şekilde yürütülür. Hedefin haberi olmaz.
* **Kullanılan Yöntemler/Araçlar:**
  * WHOIS sorgulamaları (Alan adı kayıt bilgileri)
  * Arama motoru operatörleri (Google Dorks)
  * Üçüncü parti veri tabanları ve pasif tarayıcılar (Shodan, Censys)
  * Sosyal medya analizi ve Açık Kaynak İstihbaratı (OSINT)
  * Web sitesi teknolojilerinin (Tech Stack) tespiti (Wappalyzer vb.)

---

## 3. Eğitim Yol Haritası ve Araçlar
Bu sürecin devamında öğrenilecek ve siber güvenlik uzmanının el kitabında yer alması gereken temel yetenekler şunlardır:
* Hedefin WHOIS verilerinin analizi.
* Web uygulamasının arkasında yatan teknolojilerin (Backend, Frontend, Veritabanı) pasif olarak tespiti.
* Arama motorlarının gücünü kullanarak (Google Dorks) hedefin dışarıya sızmış veya indekslenmiş hassas dosyalarını bulma.