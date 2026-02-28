# Burp Suite Detaylı Kullanımı

[[Burp Suite]], siber güvenlikçilerin İsviçre Çakısıdır. Tarayıcı ile sunucu arasına giren bir **Web Proxy** aracıdır. Zafiyetleri bulmak ve sömürmek için HTTP isteklerini havada yakalar ve değiştirir.

## Temel Ayarlar ve Dashboard
* **Dashboard:** Otomatik taramaların (Tasks), uyarıların (Advisory), bulunan zafiyetlerin (Issue Activity) ve hata kayıtlarının (Event Log) izlendiği ana panel.
* **Settings:** * *Project Settings:* Sadece o anki projeye (hedefe) özel ayarlar.
  * *User Settings:* Burp'ün tüm projelerinde geçerli genel UI/Kısayol ayarları.
* **Target & Scoping (Kapsam):** Hedef dışı sitelere (Google, YouTube) yanlışlıkla saldırmamak için sadece test edilecek URL'ler "Scope" içine alınır. 

## Burp Suite Modülleri (Tools)
* **Proxy (Intercept):** Tarayıcıdan giden HTTP paketini havada tutar (Intercept). Sen onaylamadan (Forward) paket sunucuya gitmez. Paket üzerinde manipülasyon yapmanı sağlar.
* **[[Repeater]]:** Havada yakalanan bir paketin tekrar tekrar sunucuya gönderilmesini sağlayan manuel test alanıdır.
* **Intruder:** Zafiyetleri otomatize etmek, Brute-Force (kaba kuvvet) yapmak veya Fuzzing yapmak için kullanılır (Çok hızlı istek atar).
* **Decoder:** URL, Base64, HTML gibi şifreleme ve kodlama türlerini çözer veya kodlar.
* **Comparer:** İki farklı paketi veya cevabı yan yana koyup aralarındaki ufak farkları bulur (Örn: Başarılı vs Başarısız giriş denemeleri).
* **Sequencer:** Uygulamanın ürettiği rastgele değerlerin (Oturum tokenleri, CSRF tokenleri) gerçekten "rastgele" olup olmadığını matematiksel olarak analiz eder.

## Repeater Detaylı Kullanım
Repeater, [[Web Zafiyetleri]]ni (IDOR, SQLi vb.) test ettiğimiz ana laboratuvardır.
* **Response Views (Yanıt Görünümleri):** Sunucudan gelen cevabı okuma yollarıdır. *Pretty* (Renkli HTML), *Raw* (Saf veri), *Hex* (Bayt seviyesi), *Render* (Tarayıcıda görünür hali).
* **Inspector Paneli:** Karmaşık paketlerin içindeki spesifik parametreleri (Çerezler, URL değerleri, Body parametreleri) hızlıca bulup değiştirmeyi sağlayan akıllı yan paneldir.