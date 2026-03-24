# Kriptografik Protokoller ve Ağ Güvenliği


Kriptografik algoritmaların (AES, RSA, SHA vb.) iki veya daha fazla taraf arasında iletişim kurarken **hangi sırayla ve nasıl** kullanılacağını belirleyen kurallar bütünüdür. Algoritmalar matematiği, protokoller ise mühendisliği ve ağ iletişimini temsil eder.

## 1. Temel Ağ ve İletişim Protokolleri

* **SSL/TLS (Secure Sockets Layer / Transport Layer Security):** Web trafiğinin (HTTPS) belkemiğidir. 
  * *Çalışma Mantığı:* İletişim başlarken "El Sıkışma (Handshake)" evresinde **Asimetrik Şifreleme (RSA/ECC)** ile güvenli bir ortak oturum anahtarı oluşturulur. Ardından yüksek hız için iletişimin geri kalanı bu anahtarla **Simetrik Şifreleme (AES)** üzerinden devam eder.
* **IPsec (Internet Protocol Security):** IP paketlerini ağ katmanında korur. Genellikle VPN kurulumlarında ve kurumlar arası güvenli ağ tünellemelerinde (Site-to-Site) kullanılır. İki ana bileşeni vardır:
  * *ESP (Encapsulating Security Payload):* Veriyi şifreler (Gizlilik).
  * *AH (Authentication Header):* Verinin kaynağını doğrular ve bütünlüğünü korur (Şifreleme yapmaz).
* **SSH (Secure Shell):** Uzaktaki sunuculara veya ağ cihazlarına güvenli terminal erişimi sağlar (Attackbox üzerinden hedef makinelere bağlanırken kullandığımız yapı). SSL/TLS'e benzer bir el sıkışma mantığıyla çalışır.

---

## 2. Kimlik Doğrulama ve Yetkilendirme Protokolleri


Sızma testlerinde (özellikle Active Directory ortamlarında) ve modern web mimarilerinde en çok karşılaşacağın iki protokol:

* **Kerberos:** Büyük kurumsal ağlarda (Windows Active Directory vb.) güvenli kimlik doğrulama sağlar. Parolaları ağ üzerinden göndermek yerine, zaman damgalı **"Biletler (Tickets)"** kullanır. 
  * *Bilet Veren Sunucu (TGT - Ticket Granting Ticket):* Kullanıcı doğrulanınca ona bir ana bilet verir. Kullanıcı bu biletle ağdaki diğer hizmetlere (dosya sunucusu, yazıcı) erişim sağlar. CTF'lerde bu biletleri çalmak veya sahtesini üretmek (Golden Ticket saldırıları) en kritik adımlardan biridir.
* **OAuth (Open Authorization):** Bir şifreleme protokolü olmaktan ziyade bir yetkilendirme (authorization) çerçevesidir. Geliştirdiğin bir Node.js backend veya mobil uygulamada kullanıcılarına "Google ile Giriş Yap" seçeneği sunduğunda doğrudan bu yapıyı kurarsın. Parola paylaşmadan, HTTPS üzerinden **Erişim Belirteçleri (Access Tokens)** ile üçüncü taraf uygulamalara güvenli yetki verilmesini sağlar.

---

## 3. Veri ve Dosya Güvenliği Protokolleri

* **PGP (Pretty Good Privacy):** E-posta iletişimini şifrelemek ve dijital olarak imzalamak için kullanılır. Asimetrik şifreleme ile göndericinin açık anahtarı alınır, mesaj simetrik olarak şifrelenir ve asimetrik olarak imzalanır.

---

## 4. Kriptografik Protokollerin Zayıf Noktaları

Güvenlik uzmanlarının protokolleri incelerken aradığı temel zafiyetler şunlardır:
1. **Eski Algoritmaların Kullanımı:** Sunucunun hala MD5, RC4 veya DES gibi kırılmış algoritmaları desteklemesi (Downgrade saldırılarına zemin hazırlar).
2. **Yanlış Uygulama (Implementation Flaws):** Protokolün standartlarına uyulmadan, eksik kodlanması (Heartbleed gibi SSL/TLS zafiyetleri buradan çıkar).
3. **Zayıf Anahtar Yönetimi:** Güçlü algoritmalar kullanılsa bile, gizli anahtarların sunucuda düz metin olarak unutulması veya zayıf parolalarla korunması.