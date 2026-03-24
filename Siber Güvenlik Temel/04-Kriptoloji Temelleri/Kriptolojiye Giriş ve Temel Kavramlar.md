# Kriptolojiye Giriş ve Temel Kavramlar
**Kriptoloji**, bilginin gizliliğini, bütünlüğünü ve doğruluğunu korumak için matematiksel tekniklerin kullanıldığı bilim dalıdır. İki ana alt dala ayrılır:
1. **Kriptografi:** Bilgiyi şifreleme ve şifre çözme tekniklerini geliştirir.
2. **Kriptoanaliz:** Şifrelenmiş bilgiyi çözme (kırma) yöntemlerini ve sistem zafiyetlerini araştırır.

## Tarihsel Gelişim (Özet)
* Eski Mısır (hiyeroglifler) ve Romalılar (Sezar şifreleme) ile başlamıştır.
* Modern kriptolojinin temelleri 20. yüzyılda, özellikle 2. Dünya Savaşı'ndaki **Enigma makinesi** ve **Alan Turing**'in çalışmalarıyla atılmıştır.

## Kullanım Alanları
* **İletişim & Veri Depolama Güvenliği:** Ağ üzerindeki trafiğin ve diskteki hassas verilerin korunması.
* **Kimlik Doğrulama:** Dijital imzalar ve sertifikalar ile kaynağın doğrulanması.
* **Kritik İşlemler:** Finansal altyapılar (e-ticaret, bankacılık) ve askeri/devlet haberleşmesi.

## Temel Kriptografik Terimler

* **Şifreleme (Encryption):** Düz metin halindeki bilgiyi, bir algoritma ve anahtar kullanarak okunamaz (şifreli) hale getirme işlemidir.
* **Şifre Çözme (Decryption):** Şifrelenmiş bilgiyi (ciphertext), uygun algoritma ve anahtar ile orijinal haline (düz metin - plaintext) geri getirme işlemidir.
* **Anahtar (Key):** Şifreleme ve çözme algoritmalarının çalışması için gereken, matematiksel bir değer veya gizli bilgidir.
* **Anahtar Yönetimi (Key Management):** Kriptografik güvenliğin en hassas noktasıdır. Anahtarların güvenli bir şekilde oluşturulması, dağıtılması, saklanması ve süresi dolduğunda yok edilmesi süreçlerinin tamamıdır.

## Anahtar Türleri

* **Açık Anahtar (Public Key):** Asimetrik şifreleme sistemlerinde kullanılan ve herkesin erişimine açık olan anahtardır. Veriyi şifrelemek için kullanılır.
* **Gizli Anahtar (Private Key):** Sadece sahibi tarafından bilinen, asla paylaşılmayan anahtardır. Açık anahtar ile şifrelenen veriyi çözmek veya dijital imza oluşturmak için kullanılır.

## Algoritma ve Protokol Farkı

* **Kriptografik Algoritmalar:** Şifreleme işlemini gerçekleştiren saf matematiksel fonksiyonlar ve yöntemlerdir. 
  * *Örnekler:* AES, RSA, DES.
* **Kriptografik Protokoller:** Bu algoritmaların iletişim kanallarında (örneğin internette) nasıl ve hangi sırayla güvenli bir şekilde kullanılacağını belirleyen kurallar dizisidir. 
  * *Örnekler:* SSL/TLS (Web güvenliği), SSH (Güvenli terminal), IPsec (Ağ katmanı güvenliği).