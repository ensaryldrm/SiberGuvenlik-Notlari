Bir XSS payload'unun başarılı olması, girdinizin hedef web sitesinin kodları arasında **nereye ve nasıl yansıdığına (reflected)** bağlıdır. Girdiniz düz bir HTML sayfasında mı duruyor, bir HTML etiketinin içinde mi, yoksa bir JavaScript değişkeninin içinde mi? Bu durumu analiz edip payload'unuzu buna göre şekillendirmeniz (kaçış/escape yapmanız) gerekir.

Aşağıda, alert('THM') fonksiyonunu çalıştırmak için farklı senaryolarda nasıl payload geliştirileceği 6 seviye üzerinden anlatılmıştır.

## Seviye 1: Temel Yansıma (Basic Reflection)

- **Durum:** Girdiğiniz metin, hiçbir kısıtlama veya HTML etiketi olmadan doğrudan sayfanın kaynak koduna yansır.
    
- **Çözüm:** En temel XSS payload'u doğrudan kullanılabilir.
    
- **Payload:** ```html <script>alert('THM');</script>
    

## Seviye 2: Input Etiketinden Kaçış (Escaping Input Tags)

- **Durum:** Girdiniz, bir HTML `<input>` etiketinin `value` niteliği (attribute) içine yansıtılır. (Örnek: `<input value="isim">`)
    
- **Çözüm:** Önce içinde bulunduğunuz niteliği (`"` ile) kapatmalı, sonra HTML etiketini (`>` ile) kapatmalısınız. Ardından kendi script'inizi başlatabilirsiniz.
    
- **Payload:** ```html "><script>alert('THM');</script>
    
- **Açıklama:** `">` kısmı `value` parametresini ve `input` etiketini güvenli bir şekilde kapatır, script'in serbest kalmasını sağlar.
    

## Seviye 3: Textarea Etiketinden Kaçış (Escaping Textarea Tags)

- **Durum:** Girdiniz bir `<textarea>` etiketinin arasına yansıtılır. Textarea içindeki her şey metin olarak algılanır, script çalışmaz.
    
- **Çözüm:** Textarea etiketini manuel olarak sonlandırmanız gerekir.
    
- **Payload:** ```html </textarea><script>alert('THM');</script>
    

## Seviye 4: JavaScript İçinden Kaçış (Escaping JavaScript Strings)

- **Durum:** Girdiniz bir HTML etiketine değil, doğrudan sayfadaki mevcut bir JavaScript kodunun içine (örneğin bir değişkene) yansıtılır. (Örnek: `var isim = 'girdi';`)
    
- **Çözüm:** JavaScript dizesini (string) sonlandırmalı, kendi komutunuzu girmeli ve geri kalan mevcut kodun hata vermemesi için yorum satırına almalısınız.
    
- **Payload:** ```javascript ';alert('THM');//
    
- **Açıklama:** - `'` kısmı değişken dizesini kapatır.
    
    - `;` komutun bittiğini belirtir.
        
    - `alert('THM')` kendi kodumuzdur.
        
    - `//` kısmı orijinal kodun geri kalanını yorum satırı yaparak bozulmasını (syntax error) engeller.
        

## Seviye 5: Filtre Atlatma (Filter Evasion - Nested Payload)

- **Durum:** Güvenlik filtresi, tehlikeli gördüğü kelimeleri (örneğin "script") girdinizden tamamen silmektedir.
    
- **Çözüm:** Silinen kelimenin içine aynı kelimeyi gömerek filtreyi kandırmak. Filtre içteki kelimeyi sildiğinde, geriye kalan harfler dışarıda tekrar birleşerek orijinal kelimeyi oluşturur.
    
- **Payload:** ```html <sscriptcript>alert('THM');</sscriptcript>
    
- **Açıklama:** Filtre ortadaki "script" kelimesini sildiğinde, kalan `<s` ve `cript>` birleşerek `<script>` etiketini oluşturur.
    

## Seviye 6: Karakter Filtresi ve DOM Olayları (Event Handlers)

- **Durum:** Filtre, HTML etiketi oluşturmanızı engellemek için `<` ve `>` gibi kritik karakterleri siliyor veya engelliyordur. Ancak girdiniz halihazırda bir etiket (örneğin `<img src="...">`) içindedir.
    
- **Çözüm:** Etiketten kaçmak yerine, içinde bulunduğunuz etikete yeni bir özellik (attribute) ekleyerek DOM olaylarını (örneğin `onload`, `onerror`) kullanabilirsiniz.
    
- **Payload:** ```html /images/cat.jpg" onload="alert('THM');
    
- **Açıklama:** Görsel yüklendiğinde (`onload`), sizin belirlediğiniz JavaScript kodu çalışır. `<` veya `>` karakterlerine ihtiyaç duyulmaz.
    

---

## XSS Polyglot Nedir?

XSS Polyglot, aynı anda birçok farklı kaçış (escape) senaryosunu, etiketi ve filtreyi aşmak üzere tasarlanmış **evrensel ve karmaşık bir metin dizisidir**. Yukarıdaki 6 farklı seviyenin tamamında bu tek polyglot kodunu kullansaydınız, hepsinde başarılı olurdu. Çünkü içinde hem HTML kapatıcılar, hem JS dize sonlandırıcılar hem de DOM olayı tetikleyiciler barındırır.