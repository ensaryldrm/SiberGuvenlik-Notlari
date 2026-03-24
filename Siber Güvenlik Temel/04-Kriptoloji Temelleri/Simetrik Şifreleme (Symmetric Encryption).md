# Simetrik Şifreleme (Symmetric Encryption)
Şifreleme (encryption) ve şifre çözme (decryption) işlemleri için **aynı (ortak) gizli anahtarın** kullanıldığı yöntemdir. Gönderici ve alıcı bu anahtarı önceden güvenli bir şekilde paylaşmış olmalıdır.

* **Avantajları:** Çok hızlıdır, daha az işlem gücü ve kaynak gerektirir, büyük veri yığınlarını şifrelemek için idealdir (Dosya/Disk şifreleme, VPN).
* **Dezavantajları:** Anahtar dağıtımı (Key Distribution) en büyük zayıflığıdır. Anahtar ağ üzerinden gönderilirken ele geçirilirse tüm veriler açığa çıkar. Büyük ağlarda anahtar yönetimi karmaşıktır.

---

## 1. Simetrik Şifreleme Algoritmaları


Simetrik algoritmalar veriyi işleme biçimlerine göre ikiye ayrılır:

### A. Blok Şifreler (Block Ciphers)
Veriyi sabit boyutlu bloklara (örn: 64-bit, 128-bit) bölerek şifreler.
* **DES (Data Encryption Standard):** 1970'lerde IBM geliştirdi. 56-bit anahtar kullanır. Günümüzde kaba kuvvet (brute-force) ile kırılabildiği için **güvenli değildir** ve kullanılmaz.
* **3DES (Triple DES):** DES'in zayıflığını kapatmak için veriyi 3 kez DES işleminden geçirir (şifrele-çöz-şifrele). 168-bit anahtarı vardır. Daha güvenli ama yavaştır.
* **AES (Advanced Encryption Standard):** Günümüzün endüstri standardıdır (NIST, 2001). 128, 192 ve 256-bit anahtar seçenekleri sunar. Çok güvenli ve oldukça hızlıdır.

### B. Akış Şifreleri (Stream Ciphers)
Veriyi bloklar halinde değil, sürekli bir bit veya bayt akışı (stream) olarak tek tek şifreler. Canlı veri akışları için idealdir.
* **RC4 (Rivest Cipher 4):** 1987 çıkışlıdır, çok hızlıdır ancak günümüzde ciddi güvenlik zayıflıkları (WEP zafiyetleri gibi) barındırdığı için terk edilmektedir.
* **Salsa20 ve ChaCha20:** RC4'ün modern alternatifleridir. Çok güvenli ve hızlıdır. Özellikle mobil cihazlar ve IoT gibi düşük işlem gücü olan ortamlarda tercih edilir.

---

## 2. Blok Şifreleme Modları (Modes of Operation)


Bir blok şifreleyicinin (örneğin AES) veriyi nasıl zincirleyeceğini veya yöneteceğini belirleyen modlardır. CTF'lerde şifreleme zafiyetleri genellikle bu modların yanlış kullanımından doğar.

* **ECB (Electronic Codebook):** En basit ve **en güvensiz** moddur. Her blok birbirinden bağımsız şifrelenir. Aynı düz metin, her zaman aynı şifreli metni üretir. Bu da şifrelenmiş veride görsel veya istatistiksel **desenlerin (pattern) ortaya çıkmasına** neden olur.
* **CBC (Cipher Block Chaining):** Güvenlidir. Her blok, şifrelenmeden önce bir önceki şifreli blok ile XOR işlemine sokulur. İlk blok için rastgele bir **Başlangıç Vektörü (IV - Initialization Vector)** kullanılır. Desenleri gizler.
* **CFB (Cipher Feedback) & OFB (Output Feedback):** Bir blok şifreleyiciyi, akış şifreleyicisine (stream cipher) dönüştürmek için XOR işlemini farklı sıralarla uygulayan modlardır.
* **CTR (Counter):** Her blok için artan bir sayaç (counter) değeri kullanır. Blokların birbirini beklemeden **paralel** olarak şifrelenmesine olanak tanıdığı için **en hızlı** ve en modern modlardan biridir.