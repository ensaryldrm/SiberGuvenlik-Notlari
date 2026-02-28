## HTTP vs HTTPS
* **HTTP (HyperText Transfer Protocol - Port 80):** İstemci (Tarayıcı) ile Sunucu (Web Server) arasındaki iletişimi sağlar. **Şifresizdir!** Araya giren biri (Wireshark vb. ile) şifreleri düz metin (clear-text) okuyabilir.
* **HTTPS (HTTP Secure - Port 443):** HTTP'nin SSL/TLS protokolleri ile **şifrelenmiş** halidir. Veriler karmaşık paketler halinde gider, araya giren kişi okuyamaz.

## URL (Uniform Resource Locator) Yapısı
Bir web adresinin anatomisi:
`https://www.hedef.com:443/login.php?id=1`
1. **Scheme (Protokol):** `https://`
2. **Subdomain:** `www.`
3. **Domain (SLD + TLD):** `hedef.com`
4. **Port:** `:443` (Genelde gizlidir)
5. **Path (Dizin/Dosya):** `/login.php` (Zafiyetlerin genelde yattığı yer)
6. **Query String (Parametre):** `?id=1` (IDOR ve SQL Injection zafiyetlerinin en çok arandığı, Burp Suite ile kurcalanan kısımdır!)