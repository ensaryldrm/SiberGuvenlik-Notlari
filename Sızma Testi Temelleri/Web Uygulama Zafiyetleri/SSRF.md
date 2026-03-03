# SSRF (Server-Side Request Forgery)

## SSRF Nedir?
**SSRF (Server-Side Request Forgery)**, kötü niyetli bir kullanıcının, web sunucusunu kendi seçtiği bir hedefe veya kaynağa ek/düzenlenmiş bir HTTP isteği (HTTP request) yapmaya zorlamasına olanak tanıyan bir güvenlik zafiyetidir.

## SSRF Türleri
İki temel SSRF zafiyeti türü vardır:
- **Regular (Normal) SSRF:** Zafiyet tetiklendiğinde, hedeften dönen veriler doğrudan saldırganın ekranına (yanıt olarak) yansır.
- **Blind (Kör) SSRF:** SSRF zafiyeti arka planda başarılı bir şekilde gerçekleşir, ancak saldırganın ekranına hiçbir bilgi veya yanıt dönmez.

## Etkileri (Impact)
Başarılı bir SSRF saldırısı aşağıdaki kritik sonuçlara yol açabilir:
- Yetkisiz alanlara (unauthorised areas) erişim sağlanması.
- Müşteri veya kurum verilerine erişim (Access to customer/organisational data).
- İç ağlara (Internal networks) sızma ve yayılma (Scale) yeteneği.
- Kimlik doğrulama token'larının (Authentication tokens) veya kimlik bilgilerinin/parolaların açığa çıkması.

## SSRF Saldırı Vektörleri ve Taktikleri

### 1. Tam Kontrol (Complete URL Control)
Saldırgan, web sunucusunun arka planda veri çekmek için istek attığı URL'nin tamamını kendi seçtiği bir adresle değiştirebilir.

### 2. Dizin Atlatma (Directory Traversal) ile SSRF
Eğer URL'nin tamamı değil, sadece dosya yolu (path) kontrol edilebiliyorsa `../` (üst dizine çık) taktiği kullanılır.
* **Mantık:** Sisteme gönderilen `../` ifadesi, orijinal isteğin bir kısmını (örn: `/stock`) silerek nihai isteği saldırganın hedeflediği başka bir endpointe (örn: `/api/user`) yönlendirir.

### 3. Subdomain Kontrolü ve Parametre İptali (`&x=`)
İsteğin gittiği alt alan adı (subdomain) kontrol edilebildiğinde, sistemin URL'nin sonuna otomatik eklediği orijinal dosya yolları payload'u bozabilir.
* **Taktik:** Payload'un sonuna `&x=` (veya `?x=`) eklenir. Bu sayede, sunucunun URL'nin sonuna zorla yapıştırdığı kısımlar etkisiz bir sorgu parametresine (query string) dönüşür ve saldırganın URL'si çalışmaya devam eder.

### 4. İstek Başlıklarını (Headers) ve API Key'leri Çalma
Web sunucusu, doğrudan saldırganın kontrol ettiği harici bir sunucuya istek atmaya zorlanır.
* **Amaç:** Hedef web sunucusu, normalde kendi iç sistemlerine (örn: `api.website.thm`) gönderdiği yetkilendirme bilgileri (credentials) veya API anahtarlarını (API keys) yanlışlıkla saldırganın sunucusuna gönderir ve bu hassas veriler ele geçirilir.

### SSRF Nerelerde Aranmalıdır? (Giriş Noktaları)
Bir web uygulamasında SSRF zafiyeti ararken özellikle şu 4 yaygın noktaya dikkat edilmelidir:

1. **Adres Çubuğu Parametreleri:** Parametre olarak tam bir URL'nin (Full URL) kullanıldığı yerler (Örn: `?url=https://...`).
2. **Gizli Form Alanları (Hidden Fields):** Kullanıcının sayfada görmediği ama arka planda sunucuya giden HTML form verileri (Örn: `<input type="hidden" name="server" value="http://server.website.thm/store">`).
3. **Kısmi URL'ler:** Parametrenin sadece sunucu adını (hostname) aldığı durumlar.
4. **Sadece Dosya Yolu (Path):** Sadece dizin veya yol bilgisinin girildiği alanlar.

*Not: Bu noktalardaki sömürü (exploit) zorluğu değişiklik gösterir. Çalışan payload'u bulmak için bolca deneme yanılma (trial and error) yapmak gerekir.*

### Kör (Blind) SSRF Nasıl Tespit Edilir?
Eğer zafiyet tetiklendiğinde hedef sistemden ekrana hiçbir sonuç veya hata mesajı yansımıyorsa (Blind SSRF), sunucunun bizim istediğimiz adrese arka planda gidip gitmediğini doğrulamak zorundayız. 

Bunun için hedefin bizim sistemimize istek atmasını sağlayacak **harici HTTP loglama araçları (dinleyiciler)** kullanılır:
* **Burp Suite Collaborator Client** (Sektör standardı)
* **requestbin.com** (veya webhook.site gibi online servisler)
* Kendi kontrolünüzdeki bir HTTP sunucusu (Örn: terminalde açılan basit bir Python HTTP Server veya Netcat dinleyicisi)

## SSRF Savunmalarını Atlatma (Bypass Techniques)

Geliştiriciler SSRF zafiyetlerini engellemek için genellikle girdileri (input) belirli kurallara göre denetlerler. Bu denetimler iki ana yaklaşımla yapılır: **Deny List** (Kara Liste) ve **Allow List** (Beyaz Liste). Ancak bu savunmaların da atlatılma yöntemleri vardır.

### 1. Deny List (Kara Liste) Atlatma
**Deny List**, belirtilen zararlı girdiler dışındaki her şeyi kabul eden bir yaklaşımdır.
* **Hedef:** Genellikle sunucu performans verilerini veya hassas bilgileri barındıran `localhost` veya `127.0.0.1` adresleri ile bulut ortamlarındaki metadata IP'si olan `169.254.169.254` yasaklanır.
* **Atlatma Taktikleri (Localhost Bypass):** Filtreleri şaşırtmak için alternatif localhost yazımları (formatları) kullanılır:
  * `0`
  * `0.0.0.0`
  * `0000`
  * `127.1`
  * `127.*.*.*`
  * `2130706433` *(Ondalık/Decimal format)*
  * `017700000001` *(Sekizlik/Octal format)*
  * **DNS Çözümlemesi:** Doğrudan `127.0.0.1` adresine çözümlenen özel alt alan adları kullanmak (Örn: `127.0.0.1.nip.io`).
* **Bulut (Cloud) Metadata Bypass:** `169.254.169.254` engelliyse, saldırgan kendi alan adında bu IP'ye işaret eden (A kaydı) özel bir subdomain oluşturarak bu engeli aşabilir.

### 2. Allow List (Beyaz Liste) Atlatma
**Allow List**, sadece belirtilen güvenilir formattaki girdileri kabul edip, geri kalan her şeyi reddeden daha katı bir yaklaşımdır.
* **Kural Örneği:** Girilen URL kesinlikle `https://website.thm` ile başlamak zorundadır.
* **Atlatma Taktiği:** Saldırgan, kendi kontrolündeki bir alan adında hedefin kuralına uyan bir alt alan adı (subdomain) açar.
  * **Payload:** `https://website.thm.saldirgan-adresi.thm`
  * **Mantık:** Sistem baştaki `https://website.thm` kısmını okuyup isteğe izin verir, ancak ağ isteği aslında saldırganın sunucusuna gider.

### 3. Open Redirect (Açık Yönlendirme) ile SSRF Atlatma
Eğer yukarıdaki filtre atlatma yöntemleri işe yaramazsa ve çok katı kurallar varsa, hedefin kendi içindeki başka bir zafiyet olan "Open Redirect" zincirleme bir saldırı için kullanılabilir.
* **Nasıl Çalışır?:** Uygulamanın içinde, tıklanma sayılarını ölçmek vb. amaçlarla ziyaretçileri başka sitelere yönlendiren meşru bir endpoint (Örn: `https://website.thm/link?url=...`) varsa bu harika bir fırsattır.
* **Atlatma Taktiği:** Allow List sadece `https://website.thm/` ile başlayan linklere izin veriyorsa, payload olarak hedefin kendi Open Redirect linki verilir:
  * **Payload:** `https://website.thm/link?url=http://127.0.0.1/admin`
  * **Mantık:** Sunucu, URL kendi güvenilir adresiyle başladığı için güvenlik kontrolünü geçirir. İsteği attığında kendi Open Redirect endpoint'ine gider, o endpoint de HTTP arka planında sunucuyu otomatik olarak asıl hedeflediğimiz adrese yönlendirir. Böylece kural kırılmadan SSRF tetiklenmiş olur.