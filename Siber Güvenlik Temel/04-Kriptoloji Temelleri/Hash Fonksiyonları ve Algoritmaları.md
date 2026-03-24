# Hash Fonksiyonları ve Algoritmaları
**Hash (Özet) Fonksiyonu**, herhangi bir uzunluktaki veriyi (girdiyi) alıp, matematiksel bir işlemden geçirerek **sabit uzunlukta**, benzersiz bir özet değeri (hash değeri/digest) üreten tek yönlü bir fonksiyondur.

## 1. Hash Fonksiyonlarının Temel Özellikleri (Çok Önemli)

Bir hash fonksiyonunun güvenli sayılabilmesi için şu kurallara uyması şarttır:
* **Tek Yönlülük (One-Way):** Üretilen hash değerine bakılarak orijinal girdi **asla** geri döndürülememelidir (Şifreleme ile Hash arasındaki en büyük fark budur; şifre çözülür, hash çözülmez, sadece karşılaştırılır).
* **Deterministik:** Aynı girdi (harfi harfine aynı olduğu sürece) her zaman birebir aynı hash değerini üretmelidir.
* **Çığ Etkisi (Avalanche Effect):** Girdideki tek bir bitlik/harflik değişiklik bile, ortaya çıkan hash değerini tamamen ve baştan aşağı değiştirmelidir.
* **Çarpışma Direnci (Collision Resistance):** İki farklı verinin/dosyanın aynı hash değerini üretme olasılığı imkansıza yakın olmalıdır.

---

## 2. Yaygın Hash Algoritmaları



* **MD5 (Message Digest 5):** 128-bit hash üretir. Hızlıdır ancak **çarpışma direnci kırılmıştır**. Günümüzde güvenlik amacıyla (parola saklama vb.) kullanılması kesinlikle önerilmez. CTF'lerde en sık karşılaşılan ve kırılması istenen formattır.
* **SHA-1 (Secure Hash Algorithm 1):** 160-bit hash üretir. 2017'de Google tarafından bir çarpışma (SHAttered) bulunarak kırıldığı kanıtlanmıştır. Artık güvenli kabul edilmez.
* **SHA-2 Ailesi (SHA-256, SHA-512 vs.):** Günümüzün endüstri standardıdır. Blok zinciri (Bitcoin vb.) ve güvenli web sertifikalarında yaygın olarak kullanılır. Kırılması şu anki teknolojiyle pratik olarak imkansızdır.
* **SHA-3 (Keccak):** SHA-2'nin alternatifidir. Aynı uzunluklarda hash üretir ancak tamamen farklı bir matematiksel iç yapıya sahiptir.
* **RIPEMD-160:** 160-bit hash üreten alternatif bir Avrupa standardıdır.

---

## 3. Hash Fonksiyonlarına Yönelik Saldırılar

CTF senaryolarında bir parola hash'ini ele geçirdiğinde uygulayacağın temel saldırı türleri:

1. **Çarpışma Saldırıları (Collision Attacks):** Aynı hash değerini üretecek iki farklı girdi (örneğin iki farklı PDF dosyası) bulmaya çalışarak sistemi kandırma işlemidir.
2. **Doğrudan Metin Saldırıları (Preimage Attacks):** Elindeki hash değerini üretebilecek orijinal girdiyi matematiksel olarak tersine mühendislikle bulmaya çalışma işlemidir.
3. **Rainbow Table (Gökkuşağı Tablosu) Saldırıları:** Milyarlarca olası parolanın önceden hesaplanmış hash değerlerini içeren devasa veritabanları (tablolar) kullanarak, elindeki hash'i bu tabloda aratma ve eşleştirme yöntemidir. (MD5 ve SHA-1 bu yöntemle saniyeler içinde kırılır).

---

## 4. Kullanım Alanları
* **Parola Güvenliği:** Kullanıcı parolalarını veritabanında güvende tutmak (Genellikle salt (tuzlama) işlemi ile birlikte kullanılır).
* **Veri Bütünlüğü Kontrolü:** İndirilen bir dosyanın veya ağdan gelen bir paketin yolda bozulup bozulmadığını kontrol etmek (Checksum).
* **Dijital İmzalar:** Asimetrik şifreleme sırasında tüm belgeyi şifrelemek yavaş olacağı için, belgenin sadece hash değeri alınır ve bu hash imzalanır.