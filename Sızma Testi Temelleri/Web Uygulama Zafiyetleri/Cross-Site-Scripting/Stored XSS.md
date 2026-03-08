İsminden de anlaşılacağı üzere, Stored XSS (Kalıcı XSS), gönderdiğiniz zararlı JavaScript payload'unun web uygulamasında (örneğin uygulamanın veritabanında) kalıcı olarak depolandığı saldırı türüdür. Bu zararlı kod, diğer kullanıcılar ilgili siteyi veya sayfayı ziyaret ettiğinde otomatik olarak çalışır.

## Nasıl Çalışır? (Örnek Senaryo)

Kullanıcıların yorum yapmasına izin veren bir blog sitesi düşünün. Ne yazık ki, bu yorumlar JavaScript veya diğer zararlı kodları filtrelemek için herhangi bir güvenlik kontrolünden geçirilmiyor. Eğer saldırgan JavaScript içeren bir yorum gönderirse, bu kod doğrudan veritabanına kaydedilir. Artık o makaleyi okumak için sayfayı ziyaret eden her kullanıcının tarayıcısında bu zararlı JavaScript kodu çalışacaktır.

## Potansiyel Etki (Impact)

Zararlı kod kalıcı olduğu için, hedef kitle çok daha geniştir. Sayfayı ziyaret eden herkes potansiyel kurbandır. Bu kod ile:

- Kullanıcılar başka bir web sitesine yönlendirilebilir.
    
- Ziyaretçilerin oturum çerezleri (session cookies) çalınabilir.
    
- Kod, sanki ziyaret eden kullanıcıymış gibi web sitesi üzerinde çeşitli işlemler gerçekleştirebilir.
    

---

## Önemli Notlar: Stored XSS Nasıl Test Edilir?

Stored XSS'i tespit etmek için, sisteme veri girilebilen, bu verinin depolandığı ve sonrasında diğer kullanıcıların erişimine açık olan alanlarda gösterildiği tüm giriş noktalarını (entry points) test etmeniz gerekir.

**En Sık Karşılaşılan Test Noktaları:**

- Blog veya forumlardaki yorum kısımları
    
- Kullanıcı profil bilgileri (Biyografi, kullanıcı adı, vb.)
    
- Web sitesi listelemeleri (İlanlar, ürün incelemeleri)
    

**İstemci Tarafı (Client-Side) Kontrollerini Atlatmak (ÖNEMLİ):** Bazen geliştiriciler, güvenlik önlemi olarak sadece kullanıcı arayüzünde (istemci tarafında) kısıtlamalar yapmanın yeterli olduğunu düşünürler. Örneğin, yaş sorulan bir alanda sadece tam sayı (integer) seçilebilen bir açılır menü (dropdown) koyarlar. Ancak siz, formu tarayıcı üzerinden normal yollarla kullanmak yerine, HTTP isteğini manuel olarak (örneğin Burp Suite gibi araçlarla) yakalayıp değiştirirseniz, sistemin beklemediği bir değeri (tam sayı yerine zararlı bir JavaScript payload'u) sunucuya gönderebilirsiniz. Bu yöntem, Stored XSS zafiyetlerini keşfetmek için harika bir kaynaktır.

Web uygulamasında depolanan bir veri bulduğunuzda, tıpkı Reflected XSS'te olduğu gibi payload'unuzun başarıyla çalışıp çalışmadığını onaylamanız gerekir. Kodun çalışması, uygulamanın kodu sayfanın neresine yansıttığına bağlı olacaktır.