# Active Directory ve RSAT Temelleri (PowerShell)
**Active Directory (AD):** Microsoft'un Windows Server ortamları için geliştirdiği merkezi dizin hizmetidir. Ağdaki tüm domain'e katılmış bilgisayarları, kullanıcıları, grupları ve güvenlik politikalarını (GPO) tek bir merkezden yönetmeyi sağlar.

**RSAT (Remote Server Administration Tools):** Standart bir Windows işletim sisteminden, uzaktaki Windows Server'ları (ve AD yapılarını) yönetmeyi sağlayan araç setidir. AD cmdlet'lerinin PowerShell'de çalışması için RSAT modüllerinin yüklü olması gerekir.

## Active Directory Kullanıcı Yönetimi (ADUser)

* **Get-ADUser:** AD'deki kullanıcı hesaplarını sorgular.
  * Belirli bir kullanıcıyı aramak: `Get-ADUser "j.doe"`
  * Tüm kullanıcıları listelemek: `Get-ADUser -Filter *`

* **New-ADUser:** AD'de yeni bir domain kullanıcı hesabı oluşturur.
```powershell
New-ADUser -Name "j.doe" -SamAccountName j.doe -AccountPassword (ConvertTo-SecureString "sifre123!" -AsPlainText -Force)
````

- **Set-ADUser:** AD'deki mevcut bir kullanıcının özelliklerini değiştirir.
    

```PowerShell
Set-ADUser -Identity "j.doe" -Surname "doe"
```

- **Remove-ADUser:** Kullanıcıyı AD'den siler.
    

```PowerShell
Remove-ADUser "j.doe"
```

## Active Directory Grup Yönetimi (ADGroup)

- **Get-ADGroup:** AD'deki güvenlik gruplarını sorgular.
    
    - Belirli bir grubu aramak: `Get-ADGroup "Students"`
        
    - Tüm grupları listelemek: `Get-ADGroup -Filter *`
        
- **New-ADGroup:** AD'de yeni bir grup oluşturur (GroupScope ile kapsam belirlenir; Universal, Global, DomainLocal).
    

```PowerShell
New-ADGroup -Name "Students" -GroupScope Universal
```

- **Set-ADGroup:** AD grubunun özelliklerini değiştirir.
    

```PowerShell
Set-ADGroup -Identity "Students" -Description "Öğrenci Domain Grubu"
```

- **Get-ADGroupMember:** Belirli bir AD grubunun içindeki üyeleri listeler.
    

```PowerShell
Get-ADGroupMember -Identity "Students"
```

- **Add-ADGroupMember:** Kullanıcıyı bir AD güvenlik grubuna ekler.
    

```PowerShell
Add-ADGroupMember -Identity "Students" -Members j.doe
```

- **Remove-ADGroupMember:** Kullanıcıyı gruptan çıkarır.
    

```PowerShell
Remove-ADGroupMember -Identity "Students" -Member "j.doe"
```

- **Remove-ADGroup:** AD güvenlik grubunu siler.
    

```PowerShell
Remove-ADGroup "Students"
```