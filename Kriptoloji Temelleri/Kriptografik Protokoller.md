# Kriptografik Protokoller
Kriptografik algoritmaların (AES, RSA, SHA) gerçek dünyada iki veya daha fazla taraf arasında **nasıl, hangi sırayla ve hangi kurallarla** uygulanacağını belirleyen sistemlerdir. Algoritmalar işin matematiği, protokoller ise ağ üzerindeki mühendisliğidir.

## 1. Ağ ve İletişim Güvenliği Protokolleri


* **SSL/TLS (Secure Sockets Layer / Transport Layer Security):** İnternet (HTTPS) trafiğinin güvenliğini sağlar.
  * *Çalışma Mantığı (Handshake):* İletişim başlarken asimetrik şifreleme ile kimlik doğrulanır ve güvenli bir "oturum anahtarı" oluşturulur. İletişimin geri kalanı, hız kazanmak amacıyla bu anahtarla **simetrik olarak** şifrelenir.
* **IPsec (Internet Protocol Security):** IP paketlerini ağ katmanında korur. Genellikle kurumlar arası VPN kurulumlarında kullanılır.
  * *Bileşenler:* **ESP** (Veriyi şifreler ve gizler), **AH** (Bütünlük ve kimlik doğrulama sağlar, şifreleme yapmaz), **IKE** (Anahtar değişimini yönetir).
* **SSH (Secure Shell):** Uzak sunuculara güvenli terminal erişimi sağlar (CTF laboratuvarlarında hedef makinelere sızarken veya sunucu yönetirken kullandığımız temel yapı). El sıkışma, anahtar değişimi ve şifreli tünel adımlarından oluşur.

---

## 2. Kimlik Doğrulama ve Yetkilendirme Protokolleri


Bu kısım özellikle Active Directory ağlarına sızma testleri yaparken ve modern uygulama mimarileri kurarken doğrudan karşına çıkacak:

* **Kerberos:** Kurumsal ağlarda (Örn: Windows Active Directory) parolaları ağda düz metin olarak dolaştırmadan, zaman damgalı **"Biletler (Tickets)"** üzerinden kimlik doğrulayan protokoldür. Bilet Veren Sunucu (TGS) aracılığıyla çalışır. *(Siber güvenlikte ağa tamamen sızmayı sağlayan "Golden Ticket" saldırılarının merkezidir).*
* **OAuth:** Bir şifreleme protokolünden ziyade yetkilendirme (authorization) çerçevesidir. Geliştirdiğin bir Node.js backend veya Flutter uygulamasında "Google ile Giriş Yap" seçeneği sunduğunda bu yapıyı kullanırsın. Parola paylaşmadan, **Erişim Belirteçleri (Access Token)** ile üçüncü taraf uygulamalara güvenli yetki verilmesini sağlar.

---

## 3. Veri ve E-Posta Güvenliği Protokolleri

* **PGP (Pretty Good Privacy):** E-posta mesajlarının şifrelenmesi ve dijital olarak imzalanması için kullanılır. Asimetrik şifreleme (açık anahtar dağıtımı), simetrik şifreleme (mesajı şifreleme) ve hash algoritmalarının (dijital imza) üçünü birden harmanlayarak çalışır.

---

## 4. Protokol Güvenliği ve Zafiyetler

Güçlü kriptografik algoritmalar kullanılsa bile protokoller zayıf konfigüre edilirse sistemler hacklenebilir:
* **Güncel Algoritma Kullanımı:** Zayıf/kırılmış algoritmaların (MD5, DES, RC4) protokolde desteklenmemesi (Downgrade saldırılarına karşı).
* **Anahtar Yönetimi:** Güçlü anahtarların güvenli saklanması ve düzenli olarak değiştirilmesi.
* **Doğru Uygulama (Implementation):** Protokol yazılımlarının standartlara uygun kodlanması, düzenli yama (patch) yapılması ve Heartbleed tarzı kodlama hatalarının giderilmesi.