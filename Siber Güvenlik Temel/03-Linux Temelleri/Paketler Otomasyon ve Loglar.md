# Sistem Yönetimi ve İz Bırakma

## Paket Yönetimi (Package Management)
Yeni araçlar kurmak veya sistemi güncellemek için kullanılır (Debian/Ubuntu/Kali tabanlı sistemlerde).

```bash
sudo apt update       # Paket listelerini günceller
sudo apt install nmap # Nmap aracını kurar
```

## Otomasyon (Automation - Cronjobs)
Linux'ta "Şu saatte şu komutu çalıştır" demek için **Cron** kullanılır.
* `crontab -e` komutuyla zamanlanmış görevler düzenlenir. 
* *Siber Güvenlik Notu:* Hackerlar sisteme sızdıklarında, sistemden atılsalar bile geri girebilmek (Persistence/Kalıcılık) için arka planda çalışan gizli Cron görevleri yazarlar.

## Loglar (İzlerimiz)
Sistemdeki her hareket `/var/log` klasörüne kaydedilir.
* `/var/log/auth.log`: Sisteme kimlerin giriş (SSH vb.) yaptığını veya yapmaya çalıştığını kaydeder (Brute-force saldırıları burada görünür).
* `/var/log/syslog` veya `/var/log/messages`: Sistemin genel mesajları.