# Payloadlar ve Shellcode Üretimi


Payload, bir exploit başarılı olduktan sonra hedef sistemde çalıştırılan zararlı koddur. Sisteme yeni bir kullanıcı eklemekten, gelişmiş bir Meterpreter oturumu açmaya kadar geniş bir yelpazede görev alabilirler.

Metasploit içinde payloadlar mimarisine göre 3 ana kategoriye ayrılır:

## 1. Payload Mimarisi (Çok Önemli)

### A. Tekiller (Singles)
Kendi kendine yeten, bağımsız ve genellikle çok basit görevleri yerine getiren payloadlardır. Örneğin sadece `calc.exe` (hesap makinesi) çalıştırmak veya yeni bir "admin" kullanıcısı eklemek için kullanılırlar. Boyutları küçüktür.
* İsimlendirme formatı: `platform/arch/single` (Örn: `windows/x64/shell_bind_tcp`)

### B. Stagers (Taşıyıcılar/Köprüler)
Bazen hedef sistemdeki zafiyetin izin verdiği bellek alanı çok küçüktür ve büyük bir payload'ı (örneğin 1 MB'lık Meterpreter) oraya doğrudan sığdıramayız. İşte bu noktada Stager devreye girer. Stager, hedefe ilk enjekte edilen **çok küçük** bir koddur. Tek görevi saldırgan makineye bağlanıp asıl büyük kodu (Stage) hedefe indirmektir.

### C. Stages (Aşamalar)
Stager tarafından hedefe sonradan indirilen asıl büyük ve karmaşık koddur (Meterpreter, VNC Injection vb.).
* İsimlendirme formatı: `platform/arch/stage/stager` (Örn: `windows/x64/meterpreter/reverse_tcp`)

---

## 2. Bind Shell vs. Reverse Shell Payloadları

Payload seçerken en çok karşılaşacağınız iki tür şudur:
* **`bind_tcp`:** Hedef makinede bir port açar ve bizim o porta bağlanmamızı bekler (Güvenlik duvarlarına takılma ihtimali yüksektir).
* **`reverse_tcp`:** Hedef makine, bizim (saldırganın) açtığımız dinleme portuna içeriden dışarıya doğru bağlanır (Güvenlik duvarlarını aşmak için en çok kullanılan yöntemdir).

---

## 3. MSFConsole İçinden Payload (Shellcode) Üretme

Kendi yazacağınız bir exploit veya zararlı yazılım (malware) içine gömmek için çıplak bir **Shellcode** (makine kodu) üretmeniz gerekebilir.

### Adım 1: Payload'ı Seçme
```bash
use payload/linux/x64/shell_bind_tcp
````

### Adım 2: Format Belirleyerek Üretme (`generate`)

`generate` komutu ile payload'u istediğimiz programlama dili formatında (Python, C, Ruby, raw, exe, elf vb.) dışarı çıkarabiliriz.

_Örnek: Python dilinde kullanmak üzere ( `\x` formatında) shellcode üretmek:_

Bash

```
generate -f python LHOST=192.168.1.10 LPORT=4444
```

**Sık Kullanılan `generate` Parametreleri:**

- `-f [format]`: Çıktı formatını belirler (Örn: `c`, `python`, `exe`, `elf`).
    
- `-b [bad_chars]`: Sömürü sırasında sorun yaratacak "kötü karakterleri" (örneğin `\x00` null byte) shellcode içinden çıkarmak için kullanılır. (Exploit geliştirmede hayati öneme sahiptir).
    
- `-o [dosya_adi]`: Çıktıyı ekrana basmak yerine doğrudan bir dosyaya kaydeder.