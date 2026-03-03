# (Insecure Direct Object Reference)
Kullanıcıların erişmemesi gereken başka kullanıcılara ait nesnelere (fatura, profil, dosya) sadece URL'deki ID değerini değiştirerek erişebilmesidir.
* **Lokasyonlar (Nerelerde Aranır?):** URL parametreleri (`?user_id=12`), gizli form alanları, API istekleri (AJAX), Çerezler (Cookies).
* **Veri Manipülasyonu & Bypass Yöntemleri:**
  * Bazen ID değeri açıkça `12` yazmaz. `Base64` ile şifrelenmiş olabilir (`MTI=`). Bunu Decoder ile çözüp, 13 yapıp tekrar şifreleyerek istek atılır.
  * *Hashed ID:* ID'ler MD5 gibi hash'lerle tutulabilir. Kendi hash'ini analiz edip başkasınınkini tahmin etmeye çalışırsın.
* **Savunma (Unpredictable IDs):** IDOR'u çözmenin yolu ardışık sayılar (`1, 2, 3`) yerine tahmin edilemez **UUID/GUID** (`550e8400-e29b...`) kullanmaktır.