# Nops (No Operations) Modülleri


"Nop", işlemciye (CPU) hiçbir işlem yapmamasını ve doğrudan bir sonraki komuta geçmesini söyleyen makine dili komutudur. (Örneğin x86 mimarisinde bu komut `\x90` baytı ile ifade edilir).

Metasploit'te Nops modülleri, zararlı kodun (payload) sistem belleğinde (RAM) sorunsuz çalışmasını garanti altına almak için tasarlanmış özel destekleyicilerdir.

## 1. Neden Kullanılır? (NOP Sled / Kaydırak Mantığı)

Sistemlerdeki bellek taşması (Buffer Overflow) zafiyetlerini sömürürken, enjekte ettiğimiz payload'ın bellekte tam olarak hangi adrese (hangi adrese ait hex değerine) yerleşeceğini her zaman milimetrik olarak bilemeyiz. Eğer işlemciyi (EIP kaydedicisini) yanlış bir bellek adresine yönlendirirsek sistem çöker ve exploit başarısız olur.

Bu belirsizliği ortadan kaldırmak için **NOP Sled (NOP Kaydırağı)** tekniği kullanılır:
* Saldırgan, asıl zararlı kodunun (Payload) hemen önüne yüzlerce veya binlerce NOP komutu (`\x90\x90\x90...`) ekler.
* İşlemci, bellekte hedeflenen alanın tam isabetli noktasına düşemese bile, bu geniş "NOP Kaydırağının" herhangi bir noktasına düşer.
* İşlemci NOP komutlarını gördükçe "bir şey yapma, aşağı in" emrini uygular ve adeta kaydıraktan kayar gibi hızla aşağı inerek eninde sonunda asıl Payload ile çarpışır ve onu çalıştırır.

## 2. Metasploit'te Kullanımı

Metasploit, exploitleri hedefe gönderirken genellikle hedef mimariye en uygun NOP dizilimini (güvenlik sistemlerini atlatmak için sadece `\x90` kullanmak yerine farklı anlamsız komutları harmanlayarak) **otomatik olarak** ekler.

Yine de manuel olarak yönetmek veya listelemek isterseniz:

Tüm NOP üreteçlerini görmek için:
```bash
show nops
````

Bir payload üretirken (`generate` komutu ile) özel bir NOP modülü atamak isterseniz:

```Bash
set NOP [nop_modul_adi]
```

_(Ayrıca `generate` komutunun `-n` parametresi ile NOP kaydırağının kaç bayt uzunluğunda olacağını belirleyebilirsiniz: Örn: `generate -n 100` kodu 100 baytlık bir kaydırak ekler)._