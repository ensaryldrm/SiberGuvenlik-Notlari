# Burp Suite Intruder: Otomatize Saldırılar ve Fuzzing
## 1. Intruder Nedir?
Intruder, Burp Suite içerisinde yakalanan bir HTTP isteğini (Request) baz alarak, o istek içindeki belirli parametrelere binlerce farklı veriyi (Payload) çok yüksek bir hızda denemek (fuzzing veya brute-force) için tasarlanmış bir otomasyon aracıdır.
* **Kullanım Alanları:** Giriş (Login) formlarında brute-force saldırıları, dizin ve dosya taramaları (Directory Bruteforcing), XSS veya SQL Injection parametre denemeleri.
* **Nasıl Gönderilir?** `Site Map`, `HTTP History` veya `Proxy` (Intercept) ekranında bir isteğe sağ tıklayıp **"Send to Intruder"** denilerek ilgili istek bu araca aktarılır.
* *(Not: Community versiyonunda Intruder'ın hızı kasıtlı olarak kısıtlanmıştır, saniyede çok az istek atar. Gerçek bir pentest için Professional sürümü şarttır).*

---

## 2. Positions (Saldırı Noktaları ve Tipleri)
Intruder sekmesine geçildiğinde, ilk ayarlanması gereken yer saldırının nereye yapılacağı ve nasıl bir metodoloji izleneceğidir. 

**Değişkenlerin İşaretlenmesi:**
Sistem otomatik olarak olası tüm değişkenleri seçer (Yeşil renkli ve `§` işaretleri arasında). İstemediğiniz alanları **"Clear §"** butonu ile temizleyebilir, kendi saldırmak istediğiniz bir parametreyi (Örn: `password=1234`) seçip **"Add §"** diyerek işaretleyebilirsiniz. Seçilen alan `password=§1234§` şekline dönüşür.

### Attack Types (Saldırı Tipleri)
Hedefin yapısına ve eldeki listelere (Wordlist) göre 4 farklı saldırı tipi seçilebilir:

* **Sniper (Keskin Nişancı):** Genellikle tek bir parametreyi (Örn: sadece parolanın bilinemediği bir alan) hedef alırken kullanılır. Eğer birden fazla parametre işaretlendiyse, eldeki wordlist'i sırayla önce birinci parametreye dener (diğerlerini sabit bırakır), sonra ikinciye geçer.
* **Battering Ram (Koçbaşı):** Elimizde tek bir wordlist vardır ve işaretli tüm parametrelere **aynı anda aynı değeri** basar. (Örn: Hem username hem password alanına `admin` yazar, sonra ikisine de `test` yazar).
* **Pitchfork (Yaba):** Elimizde her parametre için ayrı bir liste vardır. Birinci listeden 1. satırı alıp ilk parametreye koyarken, **aynı anda** ikinci listeden de 1. satırı alıp ikinci parametreye koyar. Listeler aynı anda aşağı doğru paralel ilerler.
* **Cluster Bomb (Misket Bombası):** En tehlikeli ve en uzun süren yöntemdir. Çaprazlama kombinasyon yapar. (Örn: Kullanıcı adı listesindeki ilk ismi alır, parola listesindeki *tüm* parolaları o isme dener. Sonra ikinci isme geçer, tüm parolaları ona da dener). Tam bir brute-force işlemidir.

---

## 3. Payloads (Saldırı Veri Setleri)
Saldırı pozisyonları ayarlandıktan sonra bu kısımda saldırıda kullanılacak silahlar (listeler) yüklenir.
* **Payload Sets:** Seçilen saldırı tipine göre kaç liste kullanılacağı buradan seçilir (Örn: Cluster Bomb seçtiyseniz 2 liste girmeniz gerekir).
* **Payload Settings:** Bilgisayarınızdaki bir metin dosyasını (`.txt`) **"Load"** butonu ile yükleyebileceğiniz kısımdır.
* **Payload Processing & Encoding:** Listeden alınan her bir kelimenin hedefe gitmeden önce örneğin URL-encode işlemine tabi tutulması veya Base64'e çevrilmesi gibi kuralların tanımlandığı harika bir özelliktir.

### Sık Tercih Edilen Parola ve Wordlist Kaynakları
* **SecLists:** Siber güvenliğin en büyük kelime listesi arşividir. Burp Suite'te en sık kullanılan listeler `Passwords/Common-Credentials` dizininde yer alır. (Örn: `10k-most-common.txt`). [GitHub Linki](https://github.com/danielmiessler/SecLists)
* **PayloadsAllTheThings:** XSS, SQLi vb. açıklar için özel script kodlarını içeren listedir.
* **FuzzDB:** Uygulama hatalarını tetiklemek için kullanılan garip karakter ve saldırı kalıpları listesidir.

---

## 4. Sonuçların Analizi (Saldırıyı Başlatma)
Tüm ayarlar bittikten sonra sağ üstteki **"Start Attack"** butonuna basılır ve yeni bir pencere açılır.
Intruder binlerce isteği saniyeler içinde atarken, asıl yetenek doğru sonucu bulmaktır. Çünkü binlerce istek atıldığı için tek tek incelenemezler.

**Nasıl Analiz Edilir?**
Açılan tabloda Status (HTTP Durum Kodu) ve Length (Yanıt Boyutu) sütunlarına tıklayarak sıralama yapılır. Çoğu zaman başarısız girişler "200 OK" dönse bile yanıt boyutu (Length) 3050 bayt iken, parolayı bulduğunuz doğru istek **boyut olarak diğerlerinden bariz şekilde farklı olacaktır** (Örn: 3200 bayt veya 500 bayt). Farklı olanı bulduğunuzda, parola o satırdadır!