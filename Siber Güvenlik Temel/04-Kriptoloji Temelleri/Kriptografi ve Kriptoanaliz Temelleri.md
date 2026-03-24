# Kriptografi ve Kriptoanaliz Temelleri

Kriptoloji, birbirini sürekli geliştiren iki temel alt daldan oluşur: Bilgiyi koruyan **Kriptografi** ve bu korumayı aşmaya çalışan **Kriptoanaliz**.

## 1. Kriptografi (Şifreleme Bilimi)
Bilgiyi güvenli bir şekilde iletmek ve saklamak için matematiksel algoritmalar kullanır. 

**Temel Amaçları:**
* **Gizlilik (Confidentiality):** Bilgiyi sadece yetkili kişilerin okuyabilmesi.
* **Bütünlük (Integrity):** Bilginin aktarım sırasında yetkisizce değiştirilmemesi.
* **Kimlik Doğrulama (Authentication):** Bilgiyi gönderenin gerçekten iddia ettiği kişi olduğunun doğrulanması.
* **İnkâr Edilemezlik (Non-repudiation):** Göndericinin, bilgiyi gönderdiğini sonradan inkar edememesi.

**Kriptografi Türleri:**
1. **Simetrik Kriptografi:** Şifreleme ve şifre çözme işlemleri için **aynı** anahtar kullanılır (Hızlıdır, ancak anahtar dağıtımı zordur).
2. **Asimetrik Kriptografi:** Biri şifrelemek, diğeri çözmek için kullanılan, matematiksel olarak birbiriyle ilişkili **farklı** anahtarlar (Açık ve Gizli Anahtar) kullanılır.

---

## 2. Kriptoanaliz (Şifre Kırma Bilimi)
Kriptografik sistemlerin zayıflıklarını bulmak, şifrelenmiş bilgiyi veya gizli anahtarı yetkisiz olarak elde etmek için kullanılan yöntemlerdir. Sistemlerin güvenliğini test etmek (veya hacklemek) için kullanılır.

**Saldırı Yaklaşımları:**
* **Kırma Saldırıları (Breaking Attacks):** Doğrudan şifreli metni çözmeyi veya anahtarı ele geçirmeyi hedefler.
* **Analiz Saldırıları (Analysis Attacks):** Şifreleme algoritmasının veya kullanılan protokolün (SSL, SSH vb.) mimari zayıflıklarını hedefler.

---

## 3. Kriptografinin Temel Prensipleri

Kriptosistemlerin tasarımı şu iki sarsılmaz kurala dayanır:

1. **Kerckhoffs'un Prensibi:** Bir şifreleme sisteminin güvenliği, algoritmanın gizli tutulmasına **bağlı olmamalıdır**. Sistemin güvenliği yalnızca **anahtarın gizliliğine** dayanmalıdır. (Algoritmayı herkes bilse bile, anahtar olmadan şifre çözülememelidir).
2. **Shannon'ın Belirsizlik Teorisi:** Şifrelenmiş metin, orijinal metne dair hiçbir istatistiksel veya anlamlı desen içermemeli, tamamen rastgele (random) görünmelidir.

---

## 4. Kriptoanaliz (Saldırı) Teknikleri


Saldırganların veya güvenlik uzmanlarının şifreleri kırmak için kullandığı başlıca yöntemler:

1. **Kaba Kuvvet Saldırıları (Brute Force):** Doğru olanı bulana kadar, olası tüm anahtar veya parola kombinasyonlarını tek tek deneme yöntemidir.
2. **Sözlük Saldırıları (Dictionary Attacks):** Tüm harf kombinasyonları yerine, insanların sık kullandığı kelimeleri, şifreleri ve özel kelime listelerini (wordlist) deneyerek hedefi kırmayı amaçlar.
3. **İstatistiksel Saldırılar (Statistical Attacks):** Şifreli metindeki harf frekanslarını veya tekrarlayan desenleri analiz ederek şifreyi çözmeyi hedefler (Shannon prensibinin ihlal edildiği durumlarda işe yarar).
4. **Yan Kanal Saldırıları (Side-Channel Attacks):** Doğrudan algoritmayı kırmak yerine, sistemi çalıştıran donanımın fiziksel sızıntılarını kullanır. Cihazın şifreleme yaparken harcadığı **süre**, tükettiği **enerji/güç** veya yaydığı **elektromanyetik dalgalar** ölçülerek anahtar tahmin edilir.