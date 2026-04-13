# Burp Suite Logger: Kapsamlı Trafik Günlüğü (Kara Kutu)
## 1. Logger Nedir?
Logger, Burp Suite açık kaldığı süre boyunca programın içinden geçen **istisnasız tüm HTTP/HTTPS istek ve yanıtlarını** saniye saniye kaydeden merkezi bir log (günlük) tutma aracıdır.
Adeta bir uçağın "Kara Kutusu" gibi çalışır. Burp Suite içindeki hangi aracın (Intruder, Repeater, Scanner veya Eklentiler) hedef sunucuya ne gönderdiğini ve ne cevap aldığını detaylıca gösterir.

---

## 2. Logger ve HTTP History Arasındaki Temel Farklar
Güvenlik testlerine yeni başlayanlar genellikle "Zaten Proxy sekmesinde HTTP History (Geçmiş) var, Logger'a ne gerek var?" diye sorarlar. İkisi arasındaki fark kritik derecede önemlidir:

| Özellik | Proxy > HTTP History | Logger |
| :--- | :--- | :--- |
| **Odak Noktası** | Manuel Testler ve Tarayıcı Trafiği | Burp Suite'in Genel Trafiği (Her Şey) |
| **Neyi Kaydeder?** | Sadece tarayıcınızdan çıkıp Proxy üzerinden geçen istekleri gösterir. | Proxy, Repeater, Intruder, Otomatik Tarayıcı (Scanner) ve hatta kurulu Eklentilerin (Extensions) arka planda attığı tüm istekleri gösterir. |
| **Gürültü Oranı** | Düşüktür. Sadece sizin tıkladığınız sayfalar görünür. | Çok yüksektir. Siz arkaya yaslanıp kahvenizi içerken, Intruder'ın saniyede attığı yüzlerce istek buraya sel gibi akar. |

---

## 3. Siber Güvenlikte Ne Zaman Kullanılır?
Logger, genellikle aktif bir saldırı yapmaktan ziyade **"Hata Ayıklama (Troubleshooting)"** ve **"Gözlem"** amacıyla kullanılır:

1. **Görünmez Trafiği İnceleme:** Bazen indirdiğiniz bir Burp eklentisi (BApp) veya Scanner arka planda hedefe sizin haberiniz olmadan binlerce istek atar. Hedef sistemin çöküp çökmediğini veya WAF (Web Application Firewall) tarafından engellenip engellenmediğinizi Logger'dan takip edersiniz.
2. **Kayıp İstekleri Bulma:** Repeater'da veya Intruder'da yanlışlıkla sildiğiniz veya unuttuğunuz çok güzel bir payload'u/isteği bulmak için Logger geçmişine bakarak o isteği kurtarabilirsiniz.
3. **Macro ve Oturum Hataları:** Eğer otomatik oturum yenileme (Macro) kurduysanız, Burp Suite'in arka planda giriş yapıp yapamadığını (şifrenin patlayıp patlamadığını) sadece Logger üzerinden teyit edebilirsiniz.