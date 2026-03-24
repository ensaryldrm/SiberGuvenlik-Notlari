# Meterpreter ve Gelişmiş Komutlar


Meterpreter, sızılan hedef makinede standart bir terminalden (cmd.exe veya /bin/bash) çok daha fazlasını sunan, gelişmiş ve dinamik bir payload'dır. 

## Neden Bu Kadar Güçlüdür? (Tasarım Hedefleri)
1. **Kusursuz Gizlilik (Sadece RAM'de Çalışır):** Meterpreter hedef sistemin sabit diskine hiçbir dosya yazmaz. Tamamen sistem belleği (RAM) üzerinde çalışır. Bu sayede dosya taraması yapan klasik Antivirüsleri kolayca atlatır.
2. **Şifreli İletişim:** Saldırgan (siz) ile kurban arasındaki tüm trafik TLS üzerinden şifrelenir. Ağ trafiğini dinleyen bir güvenlik cihazı (IDS/IPS) içeride ne komutlar çalıştırdığınızı göremez.
3. **Süreçler Arası Geçiş (Migration):** Yeni ve şüpheli bir program (process) başlatmak yerine, hedefin o an çalışan meşru bir programının (Örn: `explorer.exe` veya `svchost.exe`) içine kendini enjekte edip onun kılığında çalışır.

---

## Meterpreter Cheat Sheet (En Çok Kullanılan Komutlar)


Meterpreter oturumu (`meterpreter >`) açıldığında hedef sisteme göre otomatik olarak yüzlerce komut yüklenir. CTF'lerde ve sızma testlerinde hayat kurtaran komutlar şunlardır:

### 1. Temel ve Yönetim Komutları
* `help` (veya `?`): Kullanabileceğiniz tüm komutların detaylı listesini ekrana basar.
* `background` (veya `bg`): Meterpreter oturumunu kapatmadan arka plana alır ve sizi ana MSFConsole ekranına döndürür.
* `sessions`: Arka plandaki oturumları listeler ve geçiş yapmanızı sağlar.
* `exit`: Oturumu tamamen sonlandırır ve bağlantıyı koparır.

### 2. Sistem Komutları (Bilgi Toplama ve Sömürü)
* `sysinfo`: Hedef sistemin işletim sistemi, mimarisi (x86/x64) ve bilgisayar adını getirir. Yetki yükseltme (Privilege Escalation) öncesi ilk bakılan yerdir.
* `getuid`: Hedef sistemde şu an "hangi kullanıcı" haklarıyla çalıştığınızı gösterir. (Hedefimiz her zaman NT AUTHORITY\SYSTEM veya root olmaktır).
* `ps`: Hedef makinede o an çalışan tüm işlemleri (process) listeler.
* `shell`: Meterpreter ortamından çıkıp, hedefin kendi yerel işletim sistemi komut satırına (cmd veya bash) düşmenizi sağlar.

### 3. Dosya Sistemi Komutları (İndirme/Yükleme)
* `ls` / `cd` / `pwd`: Tıpkı Linux'taki gibi dizinleri listeler, dizin değiştirir ve bulunduğunuz dizini gösterir.
* `upload [kendi_dosyanız] [hedef_dizin]`: Kendi makinenizdeki bir dosyayı kurbanın makinesine gizlice yükler. (Örn: Bir yetki yükseltme scripti yüklemek için).
* `download [hedef_dosya]`: Kurbanın makinesindeki bir dosyayı kendi makinenize çeker. (Örn: `/etc/shadow` veya `SAM` dosyasını çalmak).
* `edit [dosya_adi]`: Hedefteki bir metin dosyasını Vim benzeri bir editörle doğrudan terminal üzerinden düzenlemenizi sağlar.

### 4. Ağ Komutları (Keşif ve Sıçrama)
* `ifconfig` / `ipconfig`: Hedefin tüm ağ arayüzlerini listeler. (İç ağda sizin göremediğiniz başka IP blokları olup olmadığını bulmak için kritiktir).
* `netstat`: Hedefin hangi portlardan kimlerle iletişim kurduğunu gösterir.
* `portfwd`: Hedefin sadece iç ağa (localhost) açık olan bir servisini, tünelleme yaparak kendi makinenize yönlendirmenizi sağlar.

### 5. Casusluk ve Gözetleme Komutları (Fiziksel Donanım)
* `webcam_snap`: Hedefin web kamerasından çaktırmadan tek bir fotoğraf çeker ve size kaydeder.
* `webcam_stream`: Hedefin web kamerasından canlı video yayını başlatır.
* `mic_start` / `mic_stop`: Hedefin mikrofonunu açarak ortam sesini kaydetmeye başlar/durdurur.