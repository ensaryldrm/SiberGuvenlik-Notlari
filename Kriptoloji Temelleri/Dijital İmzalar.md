# Dijital İmzalar
Dijital imza, elektronik bir belgenin veya mesajın kaynağını doğrulamak ve içeriğinin değiştirilmediğini kanıtlamak için asimetrik şifreleme ve hash algoritmalarının birlikte kullanıldığı kriptografik bir tekniktir.

**Üç Temel Amacı Vardır:**
1. **Kimlik Doğrulama (Authentication):** Belgenin gerçekten iddia edilen kişiden/sunucudan geldiğini doğrular.
2. **Bütünlük (Integrity):** Belgenin imzalandıktan sonra yolda (ağ üzerinde) tek bir bitinin bile değiştirilmediğini garanti eder.
3. **İnkâr Edilemezlik (Non-repudiation):** Göndericinin, ileride bu belgeyi kendisinin gönderdiğini (veya imzaladığını) inkar etmesini hukuki ve teknik olarak engeller.

---

## 1. Dijital İmzanın Çalışma Prensibi

Dijital imza, belgenin kendisini şifrelemez; belgenin "özetini" şifreler.

**A. İmza Oluşturma (Gönderici Tarafı):**
1. İmzalanacak belgenin güvenli bir hash algoritması (örn. SHA-256) ile **Özet Değeri (Hash)** hesaplanır.
2. Çıkan bu hash değeri, göndericinin **Gizli Anahtarı (Private Key)** ile şifrelenir. *İşte bu şifrelenmiş hash paketi dijital imzanın ta kendisidir.*
3. Belge ve dijital imza birlikte alıcıya gönderilir.

**B. İmza Doğrulama (Alıcı Tarafı):**
1. Alıcı, gelen belgenin hash değerini aynı algoritma ile **kendisi yeniden hesaplar**.
2. Alıcı, göndericiye ait **Açık Anahtarı (Public Key)** kullanarak, gelen dijital imzayı (şifreli hash'i) çözer.
3. Çözülen hash ile kendi hesapladığı hash **birebir eşleşiyorsa**, belge orijinaldir ve gönderen kişi doğrulanmıştır.

---

## 2. Kullanılan Asimetrik Algoritmalar

* **RSA:** Hem şifreleme hem imzalama yapabilir. İmzalamada ve doğrulamada çok güvenilir bir standarttır.
* **DSA (Digital Signature Algorithm):** Sadece imza oluşturma ve doğrulama için tasarlanmıştır. RSA'ya göre imza atarken daha hızlıdır, ancak doğrularken daha yavaştır.
* **ECDSA (Elliptic Curve DSA):** Eliptik eğri matematiğini kullanan DSA versiyonudur. Çok daha kısa anahtarlarla aynı yüksek güvenliği sağlar (IoT ve mobil cihazlar için vazgeçilmezdir).

---

## 3. Açık Anahtar Altyapısı (PKI) Entegrasyonu


Dijital imzaların güvenebileceği bir altyapı kurmak için PKI (Public Key Infrastructure) kullanılır. Çünkü alıcının kullandığı "Açık Anahtar"ın gerçekten o kişiye ait olduğu kanıtlanmalıdır.

* **Dijital Sertifikalar (X.509 Standardı):** Bir kişi veya cihazın açık anahtarını kimlik bilgileriyle birleştiren ve yetkili bir kurum tarafından dijital olarak imzalanan elektronik kimliktir.
* **Sertifika Otoritesi (CA):** Dijital sertifikaları üreten, doğrulayan ve imzalayan güvenilir tepe kurumdur.
* **CRL (Certificate Revocation List - Sertifika İptal Listesi):** Süresi dolmadan önce güvenliği ihlal edilmiş (örneğin private key'i çalınmış) ve iptal edilmiş sertifikaların kara listesidir. Sistemler bir imzayı doğrulamadan önce bu listeyi kontrol etmelidir.

---

## 4. Gerçek Dünya Uygulamaları
* **E-Posta Güvenliği:** PGP (Pretty Good Privacy) ve S/MIME ile maillerin imzalanması.
* **Web Güvenliği (SSL/TLS):** Web sitelerinin (HTTPS) sahte olmadığını kanıtlamak için sunucu sertifikalarının imzalanması.
* **Yazılım Doğrulama:** İndirilen yazılım güncellemelerinin veya çalıştırılabilir dosyaların (exe, apk) içine zararlı yazılım enjekte edilmediğini kanıtlamak.