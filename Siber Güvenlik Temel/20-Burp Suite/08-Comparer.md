# Burp Suite Comparer: Veri Karşılaştırma ve Fark Analizi
## 1. Comparer Nedir?
Comparer, iki farklı veri parçasını (genellikle iki HTTP İsteğini veya Yanıtını) yan yana koyarak aralarındaki **farklılıkları (diff) kelime veya byte düzeyinde vurgulayan** bir analiz aracıdır.

* **Neden İhtiyaç Duyulur?** Siber güvenlik testlerinde bazen sunucunun verdiği tepkiler birbirine çok benzerdir. Örneğin; bir Blind SQL Injection testinde, "Doğru" dönen bir sorgu ile "Yanlış" dönen bir sorgu arasındaki tek fark, sayfanın derinliklerinde fazladan yazılmış bir "Hoşgeldiniz" kelimesi veya birkaç byte'lık bir boyut farkı olabilir. Comparer, gözle görülmesi imkansız olan bu detayları anında ortaya çıkarır.

---

## 2. Veri Girişi ve İş Akışı
Comparer arayüzüne veriler iki farklı şekilde aktarılabilir:
* **Manuel Giriş:** Karşılaştırılacak metinler kopyalanıp Comparer ekranındaki "Item 1" ve "Item 2" panellerine doğrudan yapıştırılabilir (Paste).
* **Akıllı Aktarım (Send to Comparer):** Proxy, HTTP History veya Repeater ekranlarında incelenen iki farklı istek sırayla sağ tıklanıp **"Send to Comparer"** denilir. İstekler Comparer hafızasına alınır.

---

## 3. Karşılaştırma Modları
Comparer modülünde veriler listelendikten sonra, sağ alt köşeden iki farklı analiz metodundan biri seçilir:

### A. Words (Kelime Modu)
En sık kullanılan moddur. Verileri **metin tabanlı** olarak karşılaştırır. 
* **Kullanım Alanı:** HTML kaynak kodları, JSON API yanıtları veya düz HTTP başlıkları (Headers) arasındaki farkları ararken kullanılır.
* **Görünüm:** Silinen, eklenen veya değiştirilen kelimeler farklı arka plan renkleriyle (genellikle turuncu, mavi, sarı) vurgulanır.

### B. Bytes (Byte Modu)
Verileri karakter olarak değil, **hexadecimal (onaltılık) byte** düzeyinde karşılaştırır.
* **Kullanım Alanı:** Derlenmiş binary (ikili) dosyalar, resim dosyalarındaki manipülasyonlar veya şifrelenmiş (encrypted) karmaşık veriler arasındaki yapısal farkları incelerken kullanılır. Metin tabanlı analizlerde başarısız olan görünmez (non-printable) karakter farklarını yakalamada etkilidir.

---

## 4. Siber Güvenlikte Sık Kullanıldığı Senaryolar
1. **Yetki Aşımı (Privilege Escalation):** Standart bir kullanıcının paneli (Item 1) ile Admin kullanıcısının paneli (Item 2) karşılaştırılarak, Admin'e özel fazladan gelen gizli menüler veya buton kodları tespit edilir.
2. **Kör Zafiyetler (Blind SQLi / Command Injection):** Gönderilen zararlı payload'un sistemde bir değişikliğe yol açıp açmadığı (True/False durumu), dönen sayfaların byte boyutları ve içerik farkları karşılaştırılarak onaylanır.
3. **Oturum Kimliği Analizi:** Üst üste alınan iki farklı oturum kimliğinin (Session ID) birbirine ne kadar benzediği veya hangi kısımlarının sabit kaldığı incelenir.