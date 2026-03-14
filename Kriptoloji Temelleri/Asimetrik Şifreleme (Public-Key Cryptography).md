# Asimetrik Şifreleme (Public-Key Cryptography)
Veriyi şifrelemek ve çözmek için matematiksel olarak birbirine bağlı **iki farklı anahtarın** kullanıldığı şifreleme yöntemidir.
* **Açık Anahtar (Public Key):** Herkesle paylaşılabilir. Veriyi şifrelemek veya dijital imzayı doğrulamak için kullanılır.
* **Gizli Anahtar (Private Key):** Sadece sahibinde bulunur ve asla paylaşılmaz. Şifrelenmiş veriyi çözmek veya dijital imza oluşturmak için kullanılır.

**Özellikleri:** Simetrik şifrelemedeki "anahtar dağıtımı" (Key Distribution) sorununu kökten çözer. Ancak karmaşık matematiksel işlemler gerektirdiği için simetrik şifrelemeye göre **çok daha yavaştır**.

---

## 1. Asimetrik Şifreleme Algoritmaları

CTF laboratuvarlarında bu algoritmaların matematiksel zayıflıklarına yönelik saldırılar sıkça sorulur:

* **RSA (Rivest-Shamir-Adleman):** En yaygın olanıdır. Güvenliğini, devasa boyutlardaki **asal sayıların çarpanlarına ayrılmasının zorluğundan** (Prime Factorization) alır. 1024, 2048, 4096 bit anahtar uzunlukları kullanır.
* **ECC (Elliptic Curve Cryptography):** Eliptik eğri matematiğine dayanır. RSA ile aynı güvenliği **çok daha kısa anahtarlarla** sağlar (Örn: 256-bit ECC = 2048-bit RSA). Daha az işlem gücü gerektirdiği için mobil cihazlarda yaygın kullanılır.
* **ElGamal:** Güvenliğini **ayrık logaritma (discrete logarithm)** probleminin zorluğuna dayandırır. Hem şifreleme hem imzalama yapar.
* **DSA (Digital Signature Algorithm):** Sadece dijital imza oluşturma ve doğrulama için tasarlanmıştır (şifreleme yapmaz). O da ayrık logaritma problemini kullanır.

---

## 2. Açık Anahtar Altyapısı (PKI - Public Key Infrastructure)

Ağ üzerindeki (özellikle Node.js backend sunucuları ile React/Flutter istemcileri arasındaki) iletişimde, "Bu açık anahtar gerçekten o kişiye/sunucuya mı ait?" sorusunu çözen güven mimarisidir.

* **Sertifika Otoriteleri (CA - Certificate Authority):** Açık anahtarların gerçek sahiplerine ait olduğunu dijital olarak imzalayan ve onaylayan güvenilir üst kurumlardır.
* **Kayıt Otoriteleri (RA - Registration Authority):** CA adına kimlik doğrulama süreçlerini yürüten aracı kurumlardır.
* **Dijital Sertifikalar:** Bir kişi veya sunucunun kimlik bilgilerini ve açık anahtarını barındıran, CA tarafından onaylanmış dijital kimlik kartlarıdır.

---

## 3. Dijital İmzalar (Digital Signatures)


Bir belgenin/verinin yetkisiz değiştirilmediğini (Bütünlük) ve gerçekten iddia edilen kişiden geldiğini (Kimlik Doğrulama ve İnkâr Edilemezlik) kanıtlayan sistemdir.

1. **Oluşturma (İmzalama):** Gönderici, verinin bir özetini (Hash) alır. Bu hash değerini kendi **Gizli Anahtarı (Private Key)** ile şifreler. Bu şifreli paket "dijital imza"dır.
2. **Doğrulama:** Alıcı, gelen verinin hash değerini kendisi tekrar hesaplar. Ardından göndericinin **Açık Anahtarını (Public Key)** kullanarak dijital imzayı çözer. Çıkan hash ile kendi hesapladığı hash aynıysa belge orijinaldir.

---

## 4. Uygulama Alanları
Asimetrik şifreleme genellikle simetrik şifreleme için gereken "ortak gizli anahtarı" güvenlice iletmek için bir köprü olarak kullanılır.
* **SSL/TLS:** Web trafiğinin güvenliğini sağlayan HTTPS mimarisi.
* **E-posta Güvenliği:** PGP ve S/MIME protokolleri ile maillerin şifrelenmesi.
* **VPN (Virtual Private Network):** Uzak ağlara güvenli tünelleme.