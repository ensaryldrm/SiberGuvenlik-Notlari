## DOM Nedir?

DOM (Document Object Model - Belge Nesnesi Modeli), HTML ve XML belgeleri için bir programlama arayüzüdür. Sayfayı mantıksal bir ağaç yapısı olarak temsil eder. Bu sayede programlar (özellikle JavaScript), belgenin yapısını, stilini ve içeriğini dinamik olarak değiştirebilir.

## DOM Based XSS Nedir?

DOM Based XSS, zararlı JavaScript kodunun yürütülmesinin (execution) sunucuya (backend) herhangi bir veri gönderilmeden veya yeni bir sayfa yüklenmeden **doğrudan tarayıcıda (istemci tarafında)** gerçekleştiği XSS türüdür. Zafiyet, web sitesinin kendi JavaScript kodunun, kullanıcının girdisini veya etkileşimini güvenli olmayan bir şekilde işlemesi sonucu ortaya çıkar.

## Örnek Senaryo

1. Web sitesinde çalışan meşru bir JavaScript kodu, URL'deki `window.location.hash` parametresinin (URL'deki `#` işaretinden sonraki kısım) içeriğini alır.
    
2. Kod, bu içeriği hiçbir zararlı kod filtresinden geçirmeden sayfanın görüntülenen kısmına doğrudan yazar.
    
3. Bunu fark eden saldırgan, URL'nin hash kısmına kendi JavaScript kodunu ekler ve zararlı kodun tarayıcı üzerinde çalışmasını sağlar.
    

## Potansiyel Etki (Impact)

Tıpkı Reflected XSS'te olduğu gibi, saldırganın hazırladığı özel bağlantılar (linkler) kurbanlara gönderilir. Kurban bu bağlantıya tıkladığında zararlı kod tarayıcısında çalışır ve şu sonuçlara yol açabilir:

- Kullanıcıyı sahte/zararlı başka bir web sitesine yönlendirme.
    
- Sayfadaki içerikleri veya kullanıcının oturum bilgilerini (session) çalma.
    

---

## Önemli Notlar: DOM Based XSS Nasıl Test Edilir?

DOM Based XSS'i tespit etmek diğer türlere göre daha zorlayıcıdır ve kaynak kodunu okuyup anlayabilmek için belirli bir **JavaScript bilgisi** gerektirir.

**Adım Adım Test Mantığı:**

1. **Kaynakları (Sources) Bulmak:** Kaynak kodunda, saldırganın manipüle edip kontrol edebileceği değişkenlere erişen bölümleri aramalısınız. En bilinen örnekler `window.location.x` (örn: `window.location.hash`, `window.location.search`) parametreleridir.
    
2. **Kuyuya (Sinks) Takip Etmek:** Bu değişkenleri bulduktan sonra, kodun bu verileri nasıl işlediğini takip etmeniz gerekir. Eğitimsiz/filtrelenmemiş bu değerler:
    
    - Doğrudan web sayfasının DOM yapısına (örneğin `document.write`, `innerHTML` ile) yazılıyor mu?
        
    - `eval()`, `setTimeout()`, `setInterval()` gibi güvenli olmayan, tehlikeli JavaScript metotlarına parametre olarak aktarılıyor mu?
        

Eğer girdi manipüle edilebiliyor ve güvenli olmayan bir fonksiyona doğrudan ulaşıyorsa, orada DOM Based XSS zafiyeti vardır.