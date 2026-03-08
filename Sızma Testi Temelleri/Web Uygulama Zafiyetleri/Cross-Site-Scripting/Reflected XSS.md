Reflected XSS, bir kullanıcının HTTP isteği aracılığıyla web sitesine gönderdiği verinin, hiçbir güvenlik kontrolünden (validation/sanitization) geçirilmeden doğrudan web sayfasının kaynak koduna eklenmesiyle (yansımasıyla) ortaya çıkar.

Blind XSS veya Stored XSS'ten en büyük farkı, zararlı kodun sunucunun veritabanında **saklanmamasıdır**. Kod, sadece o anki istekte çalışır.

## Nasıl Çalışır? (Örnek Senaryo)

Diyelim ki bir web sitesinde hatalı giriş yaptığınızda URL şu şekilde değişiyor: `site.com/login?error=HataliSifre`. Sitedeki kod, URL'deki `error` parametresini alıp doğrudan ekrana "Hata: HataliSifre" olarak basıyor. Saldırgan bu durumu fark ederse, URL'yi şu şekilde değiştirebilir: `site.com/login?error=<script>alert('Hacklendin')</script>`. Site bu girdiyi kontrol etmezse, zararlı script doğrudan sayfanın içine yerleşir ve çalışır.

## Potansiyel Etki (Impact)

Zararlı kod sunucuda kalıcı olmadığı için, saldırganın kurbanı **bu özel olarak hazırlanmış linke tıklamaya ikna etmesi** gerekir. Saldırgan, zararlı payload içeren bu linki e-posta ile kurbanlara gönderebilir veya başka bir web sitesindeki bir `iframe` içine gizleyebilir. Kurban linke tıkladığında kod kendi tarayıcısında çalışır ve oturum bilgileri (session) veya kişisel müşteri verileri saldırganın eline geçebilir.

---

## Önemli Notlar: Reflected XSS Nasıl Test Edilir?

Reflected XSS zafiyetini bulmak için uygulamaya veri girişi yapılan tüm noktaları (entry points) test etmeniz gerekir. En kritik test noktaları şunlardır:

1. **URL Sorgu Parametreleri (Query Strings):** URL'de `?` işaretinden sonra gelen değişkenler (örn: `?id=1`, `?search=test`, `?error=...`). En yaygın Reflected XSS noktasıdır.
    
2. **URL Dosya Yolu (File Path):** URL'nin dizin yapısındaki kısımlar. Bazen web uygulamaları dosya yolunu doğrudan ekrana yansıtabilir.
    
3. **HTTP Başlıkları (Headers):** İstek başlıklarındaki veriler (örn: User-Agent, Referer). Pratikte istismar edilmesi (exploit) çok daha zor olsa da, güvenlik testlerinde kontrol edilmelidir.
    

**Test Sürecinde Dikkat Edilmesi Gerekenler:** Web uygulamasında yansıyan (reflected) bir veri bulduğunuzda, payload'unuzun başarıyla çalışıp çalışmadığını doğrulamanız gerekir. Kullanacağınız payload'un yapısı, verinin sayfanın neresinde (bir HTML etiketinin içinde mi, bir JavaScript değişkeninin içinde mi, yoksa düz metin olarak mı) yansıdığına bağlı olarak değişiklik gösterecektir.