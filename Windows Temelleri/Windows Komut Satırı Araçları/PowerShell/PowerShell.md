
# PowerShell

PowerShell, Microsoft tarafından geliştirilen, Windows işletim sistemi için gelişmiş bir komut satırı arayüzü ve betikleme (scripting) dilidir. Klasik Komut İstemi'nden (CMD) çok daha yeteneklidir ve Microsoft tarafından CMD yerine kullanılması önerilir (CMD komutlarıyla geriye dönük uyumlu çalışır).

## Temel Özellikleri
* **.NET Framework Tabanlı:** PowerShell .NET nesnelerini manipüle edebilir, bu da onu klasik metin tabanlı (string) işleyicilerden farklı olarak "nesneye yönelik" (object-oriented) yapar.

* **Cmdlet (Command-let):** Çeşitli sistem yönetimi görevlerini gerçekleştirmek için kullanılan küçük, tek amaçlı komutlara verilen isimdir.

* **Betikleme:** Kullanıcılar `.ps1` uzantılı PowerShell betik dosyaları (script) oluşturarak karmaşık işlemleri otomatikleştirebilir.

## Ağ Sorun Giderme Komutları

Bilgisayarın ağ adresi ayarlarını (IP) öğrenmek için:

```powershell
ipconfig
```

Bir komutla (örneğin ipconfig) birlikte kullanılabilecek ekstra parametreleri ve yardım dokümanını görmek için:

```PowerShell
ipconfig -?
```