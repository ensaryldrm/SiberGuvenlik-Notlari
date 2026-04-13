## 1. SSH (Secure Shell) Nedir?

- **Tanım:** Ağ üzerinden başka bir bilgisayara güvenli (şifreli) bir şekilde komut satırı erişimi sağlamak için kullanılan protokoldür. İstemci (Client) ve Sunucu (Server) mantığıyla çalışır.
    
- **Varsayılan Port:** TCP **22**
    
- **Güvenlik:** Telnet veya FTP'nin aksine, SSH üzerindeki tüm trafik şifrelenir (Man-in-the-Middle saldırılarını engeller).
    
- **Dosya Transferi:** Sadece komut çalıştırmakla kalmaz; SCP (Secure Copy) ve SFTP (SSH File Transfer Protocol) gibi araçlarla güvenli dosya aktarımı da sağlar.
    

## 2. Kimlik Doğrulama Yöntemleri

SSH sunucularına bağlanırken iki temel yöntem kullanılır:

1. **Kullanıcı Adı ve Parola:** Geleneksel yöntemdir. Kaba kuvvet (Brute-force) saldırılarına açıktır.
    
2. **Anahtar Tabanlı Doğrulama (Key-Based Authentication):** Çok daha güvenlidir. Kullanıcıda gizli kalması gereken bir **Private Key (Özel Anahtar)**, sunucuda ise **Public Key (Açık Anahtar)** bulunur. Sunucu, bağlantı isteği geldiğinde bu iki anahtarın eşleşip eşleşmediğini kriptografik olarak doğrular.
    

## 3. SSH Bağlantısı Kurma

Linux (veya modern Windows) terminalinden bir SSH sunucusuna bağlanmak için temel söz dizimi şu şekildedir:

Bash

```
ssh kullanici_adi@hedef_ip
```

_(Not: Eğer hedef sistem varsayılan 22 portu yerine farklı bir port kullanıyorsa `-p` parametresi ile belirtilmelidir: `ssh kullanici_adi@hedef_ip -p 2222`)_

## 4. Sistem İçi Keşif ve Yetki Yükseltme (Linux Temelleri)

Hedef makineye düşük yetkili bir kullanıcıyla sızdıktan sonra (Post-Exploitation) içeride ilerlemek için şu temel Linux komutları kullanılır:

### A. Kullanıcı Değiştirme (Switch User)

- **`su` komutu:** Linux ortamında mevcut kullanıcıdan başka bir kullanıcıya (genellikle en yetkili olan `root` kullanıcısına) geçiş yapmak için kullanılır.
    
- _Sızma Testi İpucu:_ CTF'lerde düşük yetkili bir hesaba girildiğinde, `su root` yazılarak root kullanıcısına geçilmeye çalışılır ve parola olarak `root`, `toor`, `admin`, `password` gibi çok zayıf/varsayılan parolalar mutlaka denenmelidir.
    

### B. Gizli Dosyaları Görüntüleme

- Linux dosya sisteminde adının başında nokta (`.`) bulunan dosya ve klasörler **gizli (hidden)** kabul edilir (Örn: `.bash_history`, `.ssh`).
    
- Standart `ls` komutu bu dosyaları göstermez. Gizli dosyaları görmek için `-a` (all) parametresi kullanılmalıdır:
    
    Bash
    
    ```
    ls -a
    ```
    
    _(Daha detaylı bir görünüm için genellikle `ls -la` tercih edilir)._
    

### C. Dosya İçeriğini Okuma

- **`cat` komutu:** Metin tabanlı dosyaların içeriğini doğrudan terminal ekranına basmak (okumak) için kullanılır.
    
    Bash
    
    ```
    cat .gizli_dosya_adi.txt
    ```
