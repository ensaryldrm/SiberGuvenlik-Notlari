# Kriptoanaliz Teknikleri ve Saldırı Türleri
Kriptoanaliz, şifrelenmiş bilgiyi (ciphertext) veya şifreleme algoritmalarının kendisini kırmak, sistemlerin zayıflıklarını bulmak ve güvenliğini test etmek için kullanılan teknikler bütünüdür.

## Temel Kriptoanaliz Saldırıları

Kriptografik sistemleri aşmak için kullanılan başlıca 8 teknik şunlardır:

### 1. Kaba Kuvvet (Brute Force) Saldırıları
* **Mantık:** Doğru olanı bulana kadar **tüm olası** anahtar veya parola kombinasyonlarını tek tek dener.
* **Özellik:** Başarı oranı %100'dür ancak anahtar uzunluğuna bağlı olarak yıllar (hatta yüzyıllar) sürebilir.
* **Savunma:** Yeterince uzun ve karmaşık anahtarlar (Örn: 256-bit AES) kullanmak.

### 2. Sözlük (Dictionary) Saldırıları
* **Mantık:** Rastgele karakterler denemek yerine, insanların sık kullandığı parolalardan oluşan hazır kelime listeleri (Wordlist) kullanır.
* **Özellik:** Brute Force'a göre çok daha hızlıdır. Parola kırma işlemlerinde ilk tercih edilen yöntemdir.
* **Savunma:** Tahmin edilmesi zor, anlamsız ve karmaşık parolalar seçmek.

### 3. Yan Kanal (Side-Channel) Saldırıları

* **Mantık:** Şifreleme algoritmasının matematiğine saldırmak yerine, sistemi çalıştıran donanımın fiziksel açıklarına odaklanır.
* **Özellik:** Cihazın şifreleme yaparken harcadığı **elektrik enerjisi**, işlem **süresi** veya yaydığı **elektromanyetik sızıntılar** analiz edilerek gizli anahtar elde edilir.
* **Savunma:** Donanım seviyesinde yalıtım ve işlemlerin sabit sürede/enerjide gerçekleşmesini sağlayan yazılımsal önlemler almak.

### 4. Doğrudan Metin (Known Plaintext) Saldırıları
* **Mantık:** Saldırganın elinde hem şifrelenmiş metin (ciphertext) hem de bu metnin şifrelenmeden önceki orijinal hali (plaintext) vardır.
* **Özellik:** Bu iki veri karşılaştırılarak şifreleme algoritmasının iç yapısı veya gizli anahtar çözülmeye çalışılır.

### 5. Frekans Analizi (Frequency Analysis)
* **Mantık:** Şifreli metindeki harflerin veya sembollerin kullanım sıklığını (frekansını) analiz ederek orijinal metni tahmin eder.
* **Özellik:** Klasik kriptografide (Sezar, Vigenère şifreleri) çok etkilidir. Örneğin Türkçe bir metinde en çok geçen harfin 'a' veya 'e' olması kuralına dayanır.
* **Savunma:** Modern ve karmaşık algoritmalar (AES, RSA) kullanarak harf desenlerini tamamen yok etmek.

### 6. Diferansiyel ve Lineer Kriptoanaliz
* **Mantık:** Özellikle **blok şifrelere** (Block Ciphers) yönelik ileri düzey matematiksel saldırılardır. 
* **Özellik:** Diferansiyel analiz, "girdilerdeki küçük farkların, çıktılarda nasıl farklar yarattığını" inceler. Lineer analiz ise algoritmanın iç yapısını doğrusal (lineer) denklemlerle modellemeye çalışır.

### 7. MitM (Man-in-the-Middle - Ortadaki Adam) Saldırıları

* **Mantık:** İletişim kuran iki taraf (örneğin kullanıcı ve sunucu) arasına gizlice girip, trafiği dinlemek veya değiştirmektir.
* **Özellik:** Saldırgan, her iki tarafa da kendini diğer tarafmış gibi tanıtır. Ağ (Network) güvenliğinin en büyük tehditlerindendir.
* **Savunma:** Güçlü SSL/TLS sertifikaları, güvenli anahtar değişim protokolleri (Diffie-Hellman) ve uçtan uca şifreleme kullanmak.

---

## Kriptoanalizin Kullanım Alanları
* **Güvenlik Değerlendirmesi (Sızma Testleri):** Sistemleri kendi ellerimizle kırarak açıkları kapatmak.
* **Adli Bilişim (Forensics):** Siber suçlulara ait ele geçirilen cihazlardaki şifreli dosyaları çözmek.
* **İstihbarat:** Düşman veya rakip devletlerin şifreli iletişim ağlarını (tarihteki Enigma örneği gibi) kırmak.