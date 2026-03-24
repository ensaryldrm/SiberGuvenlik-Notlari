## Blind XSS Nedir?
- **Tanım:** Stored XSS'e (Depolanmış XSS) benzer. Gönderilen zararlı payload web sitesinde depolanır ve hedeflenen başka bir kullanıcı tarafından görüntülenmek üzere bekler.
- **Temel Farkı:** Saldırgan, payload'un çalıştığını doğrudan göremez veya kodun çalışıp çalışmadığını öncelikle kendi üzerinde test edemez. (Saldırgan için sonuçlar "kör"dür).

## Örnek Senaryo
1. Bir web sitesinde yetkililere mesaj gönderebileceğiniz bir iletişim formu bulunur.
2. Formdaki mesaj içeriği herhangi bir zararlı kod kontrolünden (sanitization) geçmez.
3. Saldırgan bu forma istediği zararlı JavaScript kodunu girer ve gönderir.
4. Bu mesajlar destek biletlerine (support ticket) dönüşür.
5. Yetkili personel bu biletleri dışarıya kapalı, gizli bir web portalında görüntülediğinde zararlı kod çalışır.

## Potansiyel Etki (Impact)
Doğru payload kullanıldığında, saldırganın JavaScript kodu kendi sunucusuna gizlice veri gönderebilir (call back). Bu durum şunlara yol açabilir:
- Gizli personel portalının URL'sinin sızdırılması.
- Personelin oturum çerezlerinin (cookies) çalınması.
- Görüntülenen gizli portal sayfasının tüm içeriğinin ele geçirilmesi.
- **Sonuç:** Saldırgan, personelin oturumunu ele geçirebilir (session hijacking) ve gizli iç portala yetkisiz erişim sağlayabilir.

## Blind XSS Nasıl Test Edilir?
- **Call Back (Geri Bildirim) Mekanizması:** Blind XSS zafiyetlerini test ederken, yazdığınız payload'un mutlaka dışarıya bir istek (genellikle bir HTTP isteği) yapmasını sağlamalısınız. Ancak bu sayede kodunuzun bir yerlerde çalışıp çalışmadığını ve ne zaman tetiklendiğini bilebilirsiniz.

### Kullanılan Araçlar
- **XSS Hunter Express:** Blind XSS saldırılarını tespit etmek için en popüler araçlardan biridir. Çerezleri, URL'leri, sayfa içeriklerini ve daha fazlasını otomatik olarak yakalar ve size raporlar.
- **Özel Araçlar:** Gerekirse JavaScript kullanarak kendi "call back" dinleyicinizi de oluşturabilirsiniz.