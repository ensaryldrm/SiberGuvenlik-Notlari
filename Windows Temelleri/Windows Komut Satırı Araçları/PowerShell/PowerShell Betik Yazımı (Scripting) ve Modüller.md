# PowerShell Betik Yazımı (Scripting) ve Modüller
PowerShell betikleri (scripts), bir dizi komutu ve fonksiyonu tek bir dosyada toplayarak tekrarlayan görevleri (sistem yönetimi, ağ yapılandırması, veri işleme) otomatize etmeyi sağlar. Betik dosyaları **`.ps1`** uzantısıyla kaydedilir.

Betikleri yazmak, test etmek ve hata ayıklamak (debug) için grafiksel bir arayüz sunan **Windows PowerShell ISE (Integrated Scripting Environment)** kullanılır.

## 1. Temel Kontrol Yapıları

PowerShell'de değişkenler her zaman **`$`** işareti ile başlar.

### Değişkenler
```powershell
# Değişken tanımlama ve değer atama
$name = "John Doe"
$age = 30

# Birden fazla değişkeni tek satırda tanımlama
$firstName, $lastName = "John", "Doe"
````

### Koşullar (If-Else ve Switch)

Karşılaştırma operatörleri klasik programlama dillerindeki gibi işaretlerle değil, harflerle (`-gt`, `-lt`, `-eq`) ifade edilir.

**If-Else Yapısı:**

```PowerShell
if ($age -gt 18) {
  Write-Host "Yetişkin"
} else {
  Write-Host "Çocuk"
}
```

**Switch-Case Yapısı:**

```PowerShell
$dayOfWeek = Get-Date -Format dddd

switch ($dayOfWeek) {
    "Monday" { Write-Host "Pazartesi" }
    "Friday" { Write-Host "Cuma! Hafta sonu yaklaşıyor." }
    Default { Write-Host "Geçersiz gün." }
}
```

### Döngüler (Loops)

Bir kod bloğunu belirli bir koşul sağlanana kadar tekrarlamak için kullanılır.

**For Döngüsü:**

```PowerShell
for ($i = 1; $i -le 10; $i++) {
  Write-Host $i
}
```

**While ve Do-While Döngüsü:**

```PowerShell
$i = 1
while ($i -le 10) {
  Write-Host $i
  $i++
}
```

**Foreach Döngüsü:** (Diziler veya koleksiyonlar içinde gezinmek için en ideal yöntemdir)

```PowerShell
$names = "John", "Jane", "Doe"
foreach ($name in $names) {
  Write-Host $name
}
```

---
## 2. PowerShell Gallery ve Modül Yönetimi

PowerShell Gallery, Microsoft ve topluluk tarafından oluşturulan PowerShell kodlarını, betiklerini ve modüllerini barındıran merkezi bir havuzdur (Node.js'teki npm paket yöneticisine benzer bir yapıdadır).

_Not: Topluluk modüllerini indirirken güvenlik açısından kaynakların güvenilirliğine dikkat edilmelidir. İlk arama işleminde sistem "NuGet" sağlayıcısını kurmak isteyebilir, onaylanarak devam edilir._

**Modül Arama (Find-Module):** Örneğin SysInternals araçlarının PowerShell modülünü aramak için:

```PowerShell
Find-Module -Name "sysinternals"
```

**Modül Yükleme (Install-Module):** Bulunan modülü sisteme kurmak için:

```PowerShell
Install-Module -Name SysInternals
```
