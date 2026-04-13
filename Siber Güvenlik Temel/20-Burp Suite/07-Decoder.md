# Burp Suite Decoder: Veri Çözümleme ve Dönüştürme
## 1. Decoder Nedir?
Decoder, ağ trafiği üzerinden geçen veya uygulamalarda saklanan şifrelenmiş, kodlanmış (encoded) veya karmaşıklaştırılmış (obfuscated) verileri okunabilir hale getiren (veya okunabilir veriyi bu formatlara çeviren) temel bir kriptografi ve veri dönüşüm modülüdür.

* **Neden İhtiyaç Duyulur?** Web uygulamaları özel karakterlerin ağda bozulmaması için (Örn: URL Encoding) veya veriyi gizlemek için (Örn: Base64) farklı formatlar kullanır. Güvenlik testlerinde, bir parametreye (Örneğin `id=MTA=`) saldırmadan önce onun aslında ne anlama geldiğini (`10`) çözmek gerekir.

---

## 2. Veri Girişi ve İş Akışı
Veriler Decoder arayüzüne iki şekilde alınır:
* **Manuel Giriş:** Üst paneldeki kutuya veri doğrudan klavyeden yazılır veya yapıştırılır.
* **Akıllı Aktarım:** Proxy (Intercept) veya Repeater ekranında şüpheli bir veri (Örn: bir çerez değeri) seçilip sağ tıklanarak **"Send to Decoder"** denilir. Veri anında bu ekrana düşer.

---

## 3. Kodlama ve Çözme (Encode / Decode) Yöntemleri
Decoder ekranı, art arda işlem (zincirleme çözümleme) yapmak için tasarlanmıştır. Çözülen veri alt panele düşer ve o veri üzerinde yeni bir işlem daha yapılabilir.

* **Smart Decode (Akıllı Çözümleme):** Burp Suite'in verinin formatını (URL mi, Base64 mü?) tahmin edip otomatik olarak çözdüğü işlevdir. Hayat kurtarır.

### En Sık Kullanılan Formatlar (Encode / Decode As...)
* **URL:** Boşlukları `%20`, özel karakterleri `%3C` (`<`) gibi web dostu formatlara çevirir. XSS testlerinde çok sık kullanılır.
* **HTML:** Karakterleri HTML Entity'lerine (Örn: `>` yerine `&gt;`) çevirir.
* **Base64:** Binary veriyi veya metni sadece ASCII karakterlere (A-Z, 0-9) dönüştüren **en yaygın** kodlama türüdür. Sonunda genellikle `=` veya `==` bulunur (Örn: `YWRtaW4=`).
* **ASCII Hex / Hex / Octal / Binary:** Bilgisayar sistemlerinin anladığı düşük seviyeli formatlardır.
* **GZIP:** Sıkıştırılmış verileri okunabilir düz metne çevirir.

---

## 4. Hash (Özet) Algoritmaları
Şifreleme (Encryption) çift yönlüdür, çözülebilir. Hash işlemi (Özetleme) ise **tek yönlüdür**, orijinal veriye geri döndürülemez. Veri bütünlüğünü doğrulamak veya parolaları güvenli saklamak için kullanılır.

Decoder, girdiğiniz bir metnin saniyeler içinde şu formatlardaki Hash değerini üretebilir:
* **MD5:** Eski ve zayıftır. 32 karakterlik bir çıktı üretir. Çarpışma (Collision) saldırılarına açıktır.
* **SHA-1:** 40 karakterlik çıktı üretir. Artık güvenli kabul edilmemektedir.
* **SHA-256 / SHA-512:** Günümüzün modern ve en güvenli Hash standartlarıdır. (Örn: SHA-256, 64 karakterlik bir değer üretir).