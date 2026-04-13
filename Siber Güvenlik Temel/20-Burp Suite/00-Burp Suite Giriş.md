# Burp Suite Temelleri ve Araçları
## 1. Burp Suite Nedir?
PortSwigger tarafından Java diliyle geliştirilen ve ilk olarak 2003 yılında piyasaya sürülen Burp Suite, web uygulamalarının güvenlik açıklarını tespit etmek, sömürmek ve analiz etmek için kullanılan endüstri standardı bir siber güvenlik platformudur.
* **Temel İşlevi:** Bir web tarayıcısı (istemci) ile web sunucusu arasına girerek (Proxy) aradaki HTTP/HTTPS trafiğini **yakalama, durdurma, inceleme ve manipüle etme** imkanı sağlar. 
* **Önemi:** Güvenlik açıklarının tespit edilmesinden (Scanning) sömürülmesine (Exploitation) kadar tüm süreci tek bir platform üzerinden yönetmeyi sağlar.

---

## 2. Burp Suite Versiyonları
PortSwigger, kullanıcı profillerine göre 3 farklı sürüm sunmaktadır:

| Sürüm | Hedef Kitle | Özellikler |
| :--- | :--- | :--- |
| **Community** | Öğrenciler, Başlangıç Seviyesi, CTF Oyuncuları | **Ücretsizdir.** Temel araçları (Proxy, Repeater, Intruder vb.) barındırır. Otomatik zafiyet tarayıcısı (Scanner) yoktur. Intruder (Fuzzing) hızı kasıtlı olarak yavaşlatılmıştır. |
| **Professional** | Penetrasyon Testi Uzmanları, Güvenlik Araştırmacıları | **Ücretlidir.** Gelişmiş otomatik zafiyet tarama (Scanner), hız sınırı olmayan Intruder, gelişmiş raporlama ve profesyonel eklenti (BApp) desteği sunar. |
| **Enterprise** | Büyük Kurumlar, DevSecOps Ekipleri | **Ücretlidir.** Sürekli (otomatize) tarama, CI/CD entegrasyonu, birden fazla kullanıcı ile eşzamanlı çalışma ve merkezi yönetim arayüzü sunar. |

---

## 3. Temel Araçlar (Modüller) ve İşlevleri
Burp Suite, sekme (tab) tabanlı bir arayüze sahiptir. Her bir sekme belirli bir saldırı veya analiz vektörüne odaklanır:

| Araç Adı | Siber Güvenlikteki İşlevi |
| :--- | :--- |
| **Target** | Hedeflenen web uygulamasının site haritasını (Site Map) çıkarır, klasör/dosya dizinlerini gösterir ve hedefin kapsamını (Scope) belirlemeye yarar. |
| **Proxy** | **Burp'ün Kalbidir.** Tarayıcı ile sunucu arasındaki trafiği durdurur (Intercept). İstekleri (Request) sunucuya gitmeden önce veya sunucudan gelen yanıtları (Response) tarayıcıya ulaşmadan önce değiştirmeyi sağlar. |
| **Intruder** | Otomatize saldırı aracıdır. Brute-force (Kaba Kuvvet) ve Fuzzing saldırıları için kullanılır. Yakalanan bir isteğin içindeki belirli parametrelere wordlist (kelime listesi) atayarak binlerce deneme yapar. |
| **Repeater** | Yakalanan tek bir isteği tekrar tekrar sunucuya göndermeyi sağlar. İstek üzerinde manuel değişiklikler yaparak sunucunun tepkisi (zafiyet olup olmadığı) test edilir. |
| **Collaborator** | *(Sadece Pro)* Hedef sistemin dışarıya DNS veya HTTP isteği yapıp yapmadığını test eder. Blind SSRF ve Blind XSS gibi kör zafiyetleri tespit etmek için harikadır. |
| **Sequencer** | Sunucunun ürettiği Oturum Kimliklerinin (Session Token) veya CSRF tokenlarının rastgeleliğini ve tahmin edilebilirliğini analiz eder. |
| **Decoder** | Base64, URL, HTML, Hex gibi farklı formatlarda kodlanmış (encoded) verileri çözer veya veriyi bu formatlara dönüştürür (encode). |
| **Comparer** | İki farklı HTTP isteği veya yanıtı arasındaki farkları (kelime veya byte bazında) yan yana karşılaştırarak (diff) analiz eder. |
| **Logger** | Burp Suite üzerinden geçen istisnasız tüm HTTP/HTTPS trafiğini ve eklenti olaylarını saniye saniye kaydeder. |
| **Organizer** | Kapsamlı testlerde bulunan ilginç istekleri, verileri veya notları proje içerisinde düzenli tutmaya yarayan bir not defteri sistemidir. |
| **Extensions** | *(BApp Store)* Burp Suite'in yeteneklerini artırmak için yazılmış özel eklentilerin yüklenip yönetildiği bölümdür. |