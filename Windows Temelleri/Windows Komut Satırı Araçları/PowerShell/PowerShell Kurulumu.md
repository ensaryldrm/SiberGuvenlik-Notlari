# PowerShell Kurulumu

Güncel Windows sistemlerinde PowerShell varsayılan olarak yüklü gelse de, güncel sürümleri çekmek veya farklı işletim sistemlerine (Linux/macOS) kurulum yapmak için aşağıdaki yöntemler kullanılır.

## 1. Windows (WinGet ile Kurulum)


Microsoft, Windows ortamında kurulum için kendi paket yöneticisi olan **WinGet**'i önermektedir.
* **WinGet Nedir?** Windows 10 ve 11 için geliştirilmiş, komut satırı veya arayüz üzerinden yazılım kurmayı/güncellemeyi sağlayan açık kaynaklı bir paket yöneticisidir.
* Modern Windows sürümlerinde "Uygulama Yükleyicisi (App Installer)" paketinin bir parçası olarak varsayılan olarak gelir.

**Kurulum Adımları (CMD üzerinden):**

1. Sistemdeki PowerShell paketlerini aramak için:
```cmd
winget search Microsoft.PowerShell
````

_(Bu komut `Microsoft.PowerShell` ve `Microsoft.PowerShell.Preview` gibi paketlerin ID'lerini listeler.)_

2. Belirlenen ID ile tam kurulumu başlatmak için:
    

```DOS
winget install --id Microsoft.Powershell --source winget
```

---

## 2. Linux (Ubuntu)

Ubuntu ortamında PowerShell'in paketlenmiş sürümünü kurmak için **Snapstore** kullanılır:

```Bash
sudo snap install powershell --classic
```

---

## 3. macOS

macOS ortamında kurulum için en popüler ve pratik yöntem **Homebrew** paket yöneticisini kullanmaktır:

```Bash
brew install powershell/tap/powershell
```