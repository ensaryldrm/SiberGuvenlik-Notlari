# PowerShell ile Sistem ve Bilgi Toplama

Hedef sisteme sızdıktan sonra (veya sistem yönetimi sırasında) makinenin donanımını, işletim sistemi sürümünü, güncellemelerini ve dosya izinlerini analiz etmek için kullanılan keşif (recon) komutlarıdır.

## 1. Sistem Hakkında Bilgi Edinme

* **Get-ComputerInfo:** İşletim sistemi detayları (sürüm, build numarası), donanım bilgileri ve BIOS dahil olmak üzere sistem hakkında çok kapsamlı bir özet sunar.
```powershell
Get-ComputerInfo
````

- **win32_OperatingSystem Sınıfı:** Hedef sistemi kendi laboratuvar ortamında birebir kopyalamak (replike etmek) veya exploit aramak için tam sürüm/build numaralarını çekmek için idealdir.
    


```PowerShell
Get-WmiObject -Class win32_OperatingSystem
```

- **Get-Hotfix:** Windows Update üzerinden veya manuel olarak sisteme yüklenen tüm yamaları (hotfix) ve yüklenme tarihlerini listeler. Sistemdeki zafiyetleri (kapatılmamış açıkları) tespit etmek için çok kritiktir.
    

```PowerShell
Get-Hotfix
```

- **Defender Servislerini Kontrol Etme:** Sistemdeki antivirüs ve güvenlik duvarı (Windows Defender) servislerinin çalışıp çalışmadığını filtreleyerek listeler.
    

```PowerShell
Get-Service | Where-Object DisplayName -like '*Defender*'
```

## 2. Dosyalar Hakkında Bilgi Edinme

- **Dosya İçeriklerinde Metin Arama:** Belirtilen bir dizindeki tüm dosyaların içine tek tek girerek (özyineli - recurse) istenilen bir metni/şifreyi arar. _(Zafiyet ararken yapılandırma dosyalarındaki şifreleri bulmak için harikadır)._
    

```PowerShell
Get-ChildItem -Recurse *.* | Select-String -Pattern "ARANACAK_KELIME"
```

- **Get-Acl (Access Control List):** Bir dosya veya klasörün Erişim Kontrol Listesi'ni görüntüler. Hangi kullanıcının veya grubun o dosya üzerinde okuma, yazma veya çalıştırma (RX) yetkisi olduğunu gösterir.
    

```PowerShell
Get-Acl hedef_dosya.txt
```

- **Get-FileHash:** Belirtilen bir dosyanın şifreleme özetini (hash değerini) hesaplar. Zararlı yazılım analizi yaparken dosyanın virüs veritabanlarındaki (VirusTotal vb.) kaydını aratmak veya dosyanın değiştirilip değiştirilmediğini (bütünlüğünü) doğrulamak için kullanılır. Varsayılan olarak SHA256 algoritmasını kullanır.
    

```PowerShell
Get-FileHash hedef_dosya.exe
```
