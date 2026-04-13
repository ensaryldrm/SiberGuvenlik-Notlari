# Burp Suite Sequencer: Token ve Rastgelelik Analizi
## 1. Sequencer Nedir?
Sequencer, web uygulamaları tarafından üretilen **Oturum Kimliklerinin (Session Tokens), CSRF token'larının, Parola Sıfırlama bağlantılarının** ve diğer kritik rastgele verilerin ne kadar güvenli olduğunu istatistiksel olarak test eden bir analiz aracıdır.

* **Neden Önemlidir?** Eğer bir sunucunun ürettiği oturum kimlikleri gerçekten "rastgele" değilse ve bir algoritmaya dayanıyorsa (Örneğin: o anki saniyenin Base64 ile şifrelenmesi), bir saldırgan kendi aldığı token'a bakarak **başka bir kullanıcının token'ını tahmin edebilir**. Bu da doğrudan **Session Hijacking (Oturum Ele Geçirme)** saldırısına yol açar.
* **Ne Yapar?** Milyonlarca bit seviyesinde veriyi toplayarak "Rastgelelik (Entropy)" ve "Tahmin Edilemezlik" analizi yapar. 

---

## 2. Sequencer İş Akışı ve Veri Toplama
Sequencer'ın başarılı bir analiz yapabilmesi için tek bir token yeterli değildir; algoritmanın desenini (pattern) çözebilmek için yüzlerce veya binlerce token örneğine ihtiyacı vardır.

### Adım 1: İstek Yakalama ve Gönderme
1. Proxy (Intercept) veya HTTP History sekmesinden uygulamanın token ürettiği bir işlem (Örn: Giriş yapma veya anasayfayı ilk ziyaret) bulunur.
2. Bu isteğe sağ tıklanıp **"Send to Sequencer"** denilerek analiz modülüne gönderilir.

### Adım 2: Token Seçimi ve Veri Toplama (Live Capture)
1. Sequencer arayüzünde, uygulamanın döndürdüğü yanıt (Response) içerisinden analiz edilecek veri (Örn: `PHPSESSID=...` veya `X-CSRF-Token: ...`) işaretlenir.
2. **"Start live capture" (Canlı yakalamayı başlat)** butonuna basılır. 
3. Burp Suite, hedef sunucuya binlerce kez otomatik istek atarak dönen tüm yeni token'ları bir havuza toplamaya başlar. (Sağlıklı bir analiz için genellikle en az 1000 - 5000 arası token toplanması önerilir).

---

## 3. Analiz Süreci ve Sonuçlar
Yeterli veri toplandıktan sonra "Analyze now" butonuna basılarak istatistiksel testler başlatılır. 

Sequencer, toplanan token'ları bit seviyesinde inceler ve şu sorulara cevap arar:
* Karakterlerin dağılımı eşit mi?
* Peş peşe gelen token'lar arasında matematiksel bir bağ var mı?
* Token'ın bir kısmı sabit kalıp sadece sonu mu değişiyor?

**Analiz Raporu:**
Analiz sonucunda araç size genel bir kalite puanı verir. Eğer sonuç **"Excellent (Mükemmel)"** ise tokenlar kriptografik olarak güvenlidir. Ancak sonuç **"Poor (Zayıf)"** ise, bu sistemin tahmin edilebilir bir algoritma kullandığını gösterir ve kritik bir güvenlik zafiyeti (Kötü Kriptografi / Predictable Session Token) olarak raporlanır.