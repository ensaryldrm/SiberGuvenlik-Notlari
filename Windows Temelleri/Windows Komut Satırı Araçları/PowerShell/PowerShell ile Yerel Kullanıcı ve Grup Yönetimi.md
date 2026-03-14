# PowerShell ile Yerel Kullanıcı ve Grup Yönetimi


Bu cmdlet'ler tek bir makine üzerindeki yerel (Local) kullanıcı hesaplarını ve grupları yönetmek için kullanılır.

> **Önemli Not:** Bu komutların çoğu sistemde değişiklik yaptığı için PowerShell'in **Yönetici Olarak (Run as Administrator)** açılmasını gerektirir.

## Yerel Kullanıcı (Local User) Yönetimi

* **Get-LocalUser:** Sistemdeki kullanıcıları listeler. Parametre verilmezse tüm kullanıcıları getirir.
```powershell
Get-LocalUser
```

* **Get-LocalUser:**  Sistemdeki filterenlemiş kullanıcıları listeler.
```powershell
Get-LocalGroup | Where-Object Description -match "certificate"
````

- **New-LocalUser:** Bilgisayarda yeni bir yerel kullanıcı hesabı oluşturur. Parolayı güvenli metne (secure string) çevirmek zorunludur.
    

```PowerShell
New-LocalUser -Name "j.doe" -Password (ConvertTo-SecureString -String 'password123' -AsPlainText -Force)
```

- **Set-LocalUser:** Mevcut bir kullanıcı hesabının özelliklerini (örneğin açıklamasını) değiştirir.
    

```PowerShell
Set-LocalUser -Name "j.doe" -Description "Bu bir test kullanıcısıdır."
```

- **Disable-LocalUser:** Bir kullanıcı hesabını devre dışı bırakır (hesap silinmez ama giriş yapılamaz).
    

```PowerShell
Disable-LocalUser -Name "j.doe"
```

- **Enable-LocalUser:** Devre dışı bırakılmış hesabı yeniden etkinleştirir.
    

```PowerShell
Enable-LocalUser -Name "j.doe"
```

- **Remove-LocalUser:** Bir kullanıcı hesabını sistemden tamamen siler.
    

```PowerShell
Remove-LocalUser -Name "j.doe"
```

## Yerel Grup (Local Group) Yönetimi

- **Get-LocalGroup:** Bilgisayardaki tüm yerel grupları (Administrators, Users vb.) listeler.
    

```PowerShell
Get-LocalGroup
```

- **New-LocalGroup:** Yeni bir yerel grup oluşturur.
    

```PowerShell
New-LocalGroup -Name "Students"
```

- **Set-LocalGroup:** Mevcut bir yerel grubun özelliklerini değiştirir.
    

```PowerShell
Set-LocalGroup -Name "Students" -Description "Öğrenci Grubu"
```

- **Add-LocalGroupMember:** Bir kullanıcıyı oluşturulan veya mevcut olan bir gruba üye olarak ekler.
    

```PowerShell
Add-LocalGroupMember -Group "Students" -Member "j.doe"
```

- **Remove-LocalGroupMember:** Kullanıcıyı gruptan çıkarır.
    

```PowerShell
Remove-LocalGroupMember -Group "Students" -Member "j.doe"
```

- **Remove-LocalGroup:** Sistemi yerel grubunu tamamen siler.
    
```PowerShell
Remove-LocalGroup -Name "Students"
```

