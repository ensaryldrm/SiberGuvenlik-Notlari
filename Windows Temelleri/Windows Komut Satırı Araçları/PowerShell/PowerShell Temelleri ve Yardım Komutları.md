# PowerShell Temelleri ve Yardım Komutları

PowerShell (PS), komut satırı üzerinden sistem yönetimi ve otomasyon sağlayan güçlü bir araçtır. 

## 1. PowerShell ve ISE Farkı
* **Windows PowerShell:** Standart, metin tabanlı komut satırı arayüzüdür.
* **Windows PowerShell ISE (Integrated Scripting Environment):** PowerShell için geliştirilmiş grafiksel bir arayüzdür (GUI). Komut yazmak, betik (script) çalıştırmak, test etmek ve hata ayıklamak (debugging) için kullanılır.

## 2. PowerShell Sürümünü Öğrenme
Sistemde yüklü olan PowerShell versiyonunu ve yapı numaralarını görmek için şu değişken çağrılır:
```powershell
$PSVersionTable
````

## 3. Cmdlet Yapısı ve Yardım Sistemi

PowerShell'de komutlar **"Cmdlet"** (Command-let) olarak adlandırılır ve standart olarak **`Fiil-İsim`** (Verb-Noun) formatında yazılır (Örn: `Get-Process`, `Get-Service`). Binlerce komutu ezberlemek yerine yerleşik yardım sistemi kullanılır.

### Get-Help (Yardım Alma)

Bir komutun ne işe yaradığını, parametrelerini ve nasıl kullanıldığını gösterir.

```PowerShell
Get-Help Get-Process
```

_Alternatif kısayol:_ Herhangi bir komutun sonuna `-?` ekleyerek de yardım sayfasına ulaşılabilir (Örn: `Get-Process -?`).

### Get-Command (Komut Arama)

İsmi tam hatırlanamayan komutları, işlevleri ve betikleri listelemek veya aramak için kullanılır.

```PowerShell
Get-Command
```

_Not:_ `Get-Command`'ın kendi detaylı kullanımını öğrenmek için: `Get-Help -Name Get-Command -Detailed`

### Update-Help (Yardım Dosyalarını Güncelleme)

Sistemdeki yardım sayfaları eksik veya güncel değilse, internet üzerinden en yeni yardım dosyalarını indirir.

```PowerShell
Update-Help
```

_(Bu komutun çalışması için PowerShell'in "Yönetici Olarak" - Elevated privileges ile başlatılması gerekir.)_

## 4. Alias (Kısaltmalar) ve Hızlı Kullanım

Aliaslar, uzun cmdlet'ler yerine kullanılabilecek kısa adlardır. Özellikle Linux (bash) veya eski CMD komutlarına alışkın olanların işini kolaylaştırır (Örn: `Set-Location` cmdlet'i yerine kısaca `cd` yazılabilir).

Sistemdeki tüm kısaltmaları görmek için:

```PowerShell
alias
```

Belirli bir komutun veya kısaltmanın neye karşılık geldiğini bulmak için:

```PowerShell
alias cd
```

## 5. Tab Tamamlaması (Tab Completion)

Komutları veya dosya yollarını hızlı yazmak için kullanılan özelliktir.

- Komutun veya dizinin ilk birkaç harfini yazıp **Tab** tuşuna basıldığında PowerShell geri kalanı otomatik tamamlar.
    
- Eğer o harflerle başlayan birden fazla seçenek varsa, **Tab tuşuna art arda basılarak** mevcut seçenekler arasında geçiş yapılabilir (Örn: `Set-Location do<TAB>` yapıldığında önce `.\Documents\`, tekrar basıldığında `.\Downloads\` gelir).