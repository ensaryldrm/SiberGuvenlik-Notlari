# PowerShell Pipeline ve Filtreleme
PowerShell'i diğer CLI araçlarından ayıran en güçlü özelliği, çıktıları "nesne (object)" olarak işlemesi ve komutları birbirine zincirleyebilmesidir.

## Pipe İşlemi ( | )
Pipe (`|`) sembolü, soldaki komutun çıktısını alıp, sağındaki komuta "girdi" olarak aktarır. Komutları zincirleyerek karmaşık görevleri otomatikleştirmeyi sağlar.

## 1. Select-Object (Alias: select)
Çok fazla veri dönen bir komutun çıktısından, sadece ihtiyacımız olan belirli "sütunları/özellikleri" seçmek için kullanılır.
* *Örnek:* Sadece işlemlerin adını ve ID'sini listelemek:
```powershell
Get-Process | Select-Object ProcessName, Id
````

## 2. Where-Object (Alias: where)

Nesneleri belirli mantıksal kriterlere göre filtreler. Yalnızca şarta uyan verileri ekrana veya bir sonraki komuta geçirir.

- _Örnek:_ Sadece "Çalışan (Running)" servisleri listelemek:
    

```PowerShell
Get-Service | Where-Object Status -eq "Running"
```

**Sık Kullanılan Karşılaştırma Operatörleri:**

- `-eq` : Eşittir (Equal)
    
- `-ne` : Eşit değil (Not Equal)
    
- `-gt` : Büyüktür (Greater Than)
    
- `-ge` : Büyük veya eşittir (Greater or Equal)
    
- `-lt` : Küçüktür (Less Than)
    
- `-le` : Küçük veya eşittir (Less or Equal)
    

## 3. Select-String

Linux'taki `grep` komutunun karşılığıdır. Metin dosyalarında veya dizelerdeki belirli kelimeleri, ifadeleri veya Regex desenlerini aramak için kullanılır.

- _Örnek:_ `file.txt` içinde "today" geçen satırları bulmak:
    

```PowerShell
Select-String -Pattern "today" .\file.txt
```