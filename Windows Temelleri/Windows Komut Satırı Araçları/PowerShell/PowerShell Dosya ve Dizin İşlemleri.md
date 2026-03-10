# PowerShell Dosya ve Dizin İşlemleri


PowerShell'de dosya ve dizin (klasör) manipülasyonu için kullanılan temel cmdlet'ler şunlardır:
*(Not: Tek nokta `.` bulunulan dizini, çift nokta `..` bir üst dizini ifade eder.)*

## 1. Get-ChildItem (Alias: ls, dir)
Belirtilen dizinin içeriğini (dosyaları ve klasörleri) listeler.
```powershell
Get-ChildItem
````

## 2. Set-Location (Alias: cd)

Çalışma dizinini (bulunulan klasörü) değiştirir.

```PowerShell
Set-Location .\Documents\
```

## 3. New-Item

Yeni bir dosya veya dizin oluşturur. Parametre verilmezse varsayılan olarak boş bir dosya oluşturur.

- **Boş dosya oluşturmak için:**
    

```PowerShell
New-Item file.txt
```

- **Yeni klasör oluşturmak için:** (`-ItemType Directory` parametresi kullanılır)
    

```PowerShell
New-Item -ItemType Directory logs
```

## 4. Remove-Item (Alias: rm, del)

Belirtilen dosyaları veya dizinleri siler.

```PowerShell
Remove-Item .\logs\
```

## 5. Copy-Item (Alias: cp, copy)

Dosya veya dizinleri başka bir konuma kopyalar.

```PowerShell
Copy-Item file.txt file1.txt
```

## 6. Move-Item (Alias: mv, move)

Dosyaları/dizinleri taşır veya yeniden adlandırır.

- **Sadece taşımak için:**
    

```PowerShell
Move-Item .\file1.txt ..\Desktop\
```

- **Taşırken yeniden adlandırmak için:**
    

```PowerShell
Move-Item ..\Desktop\file1.txt .\file01.txt
```

## 7. Get-Content (Alias: cat)

Metin dosyalarının içeriğini doğrudan terminal ekranında görüntülemek için kullanılır.

```PowerShell
Get-Content .\file.txt
```