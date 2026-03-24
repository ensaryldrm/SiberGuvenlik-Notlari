
## Ön Koşullar (Prerequisites)
XSS temelde JavaScript'e dayandığı için aşağıdaki konularda temel bilgi sahibi olmak süreci kolaylaştırır:
- **JavaScript:** Temel seviyede kod okuma ve yazma.
- **İstemci-Sunucu (Client-Server) Mimarisi:** İstek (request) ve yanıt (response) döngüsünün işleyiş mantığı.
## XSS (Cross-Site Scripting) Nedir?
- **Kategori:** Siber güvenlikte bir **enjeksiyon (injection) saldırısı** olarak sınıflandırılır.
- **Nasıl Çalışır:** Kötü niyetli JavaScript kodları, web uygulamasına enjekte edilir. Asıl hedef sunucu değil, **kodu çalıştıracak olan diğer kullanıcılardır**.
- **Yaygınlık:** Web uygulamalarında en sık rastlanan güvenlik zafiyetlerinden biridir.

## Oda Kapsamı ve Hedefler
Bu odada öğrenilecek temel yetenekler:
1. Farklı XSS türlerini tanıma.
2. XSS payload'ları (zararlı kod blokları) oluşturma.
3. Güvenlik filtrelerini atlatmak (evade) için payload'ları modifiye etme.
4. Yeni öğrenilen yetenekleri pratik bir laboratuvar ortamında test etme.

## Bug Bounty (Ödül Avcılığı) Motivasyonu
XSS zafiyetleri çok yaygındır ve büyük platformlarda tespit edildiğinde ciddi ödüller (bounty) kazandırabilir. Bilinen bazı örnekler:
- Shopify'da tespit edilen XSS zafiyetleri.
- Steam sohbetinde bulunan XSS (Ödenen Ödül: **$7,500**).
- HackerOne'da bulunan XSS (Ödenen Ödül: **$2,500**).
- Infogram'da tespit edilen XSS zafiyetleri.

