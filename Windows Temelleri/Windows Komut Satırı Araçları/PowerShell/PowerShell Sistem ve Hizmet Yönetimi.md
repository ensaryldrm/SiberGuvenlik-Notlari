# PowerShell Sistem ve Hizmet Yönetimi

İşletim sistemindeki çalışan süreçleri (process) ve arka plan hizmetlerini (service) yönetmek için kullanılan cmdlet'lerdir.

## İşlem (Process) Yönetimi

* **Get-Process:** Sistemde çalışan tüm işlemleri listeler. Belirli bir işlemi filtrelemek için `-Name` parametresi veya joker karakter (`*`) kullanılabilir.
```powershell
Get-Process
Get-Process -Name win*
````

- **Stop-Process:** Çalışan bir işlemi anında sonlandırır (kill). İşlem adı veya benzersiz ID'si (`-Id`) ile çağrılabilir.
    

```PowerShell
Stop-Process -Id 5432
```

## Hizmet (Service) Yönetimi

- **Get-Service:** Sistemdeki tüm hizmetleri ve güncel durumlarını (Running/Stopped) listeler.
    

```PowerShell
Get-Service
```

- **Start-Service:** Durdurulmuş bir hizmeti başlatır.
    

```PowerShell
Start-Service -Name Appinfo
```

- **Stop-Service:** Çalışan bir hizmeti durdurur.
    

```PowerShell
Stop-Service -Name Appinfo
```