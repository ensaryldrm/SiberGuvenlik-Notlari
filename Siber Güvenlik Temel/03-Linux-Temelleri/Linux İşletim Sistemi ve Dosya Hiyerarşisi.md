Linux, açık kaynaklı ve siber güvenlik/sunucu altyapılarında en çok kullanılan işletim sistemidir. Her şey kök dizinden (`/`) başlar.

## En Önemli Linux Dizinleri (Common Directories)
Sızdığımız bir sistemde ilk bakacağımız yerler buralardır:
* **`/` (Root Directory):** Tüm sistemin başlangıç noktasıdır.
* **`/root`:** Sistemin tanrısı olan "root" kullanıcısının ev dizinidir. (Normal kullanıcılar giremez).
* **`/home`:** Normal kullanıcıların (Ahmet, Ayşe) kişisel dosyalarının bulunduğu yerdir. (Örn: `/home/ahmet`).
* **`/etc`:** Sistemin ve uygulamaların **yapılandırma (ayar)** dosyalarının bulunduğu en kritik dizindir. (Şifrelerin tutulduğu `/etc/shadow` buradadır!).
* **`/var`:** Sürekli değişen dosyaların tutulduğu yerdir. Veritabanları, web siteleri (`/var/www/html`) ve **Log dosyaları** buradadır.
* **`/bin` ve `/sbin`:** Sistem komutlarının (ls, cd, ping) çalıştırılabilir dosyalarının bulunduğu yerdir.
* **`/tmp`:** Geçici dosyalar içindir. Sistem yeniden başlayınca silinir. *Hackerlar sisteme zararlı dosya yüklemek için genelde bu klasörü kullanır çünkü buraya herkesin yazma izni vardır!*