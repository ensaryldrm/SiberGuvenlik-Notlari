## 1. FTP (File Transfer Protocol) Nedir?

- İnternet üzerinden dosya aktarımı (yükleme/indirme) yapmak için kullanılan, 1971 yılında geliştirilmiş bir ağ protokolüdür.
    
- **Mimari:** İstemci (Client) ve Sunucu (Server) modeliyle çalışır.
    
- **Port:** Varsayılan olarak TCP **21** portunu kullanır.
    
- **Güvenlik Uyarısı:** FTP şifrelenmemiş (clear-text) bir protokoldür. Trafik dinlenirse parolalar açıkça okunabilir. Güvenli veri aktarımı için her zaman **SFTP** (SSH üzerinden) veya **FTPS** (SSL/TLS ile) tercih edilmelidir.
    

## 2. CTF Keşif Aşaması (Bilgi Toplama)

Sisteme saldırmadan önce portlarda çalışan servislerin tam sürümlerini öğrenmek gerekir.

- **Nmap Versiyon Taraması:**

```Bash
nmap -sV hedef_ip
```

## 3. Sisteme Erişim ve Anonim Bağlantı (Anonymous Login)

FTP sunucularında parola gerektirmeden herkese açık dosya paylaşımı yapmak için "Anonim" giriş aktif bırakılmış olabilir. CTF'lerde kontrol edilecek ilk yapılandırma hatası budur.

- **Bağlantı Komutu:**

```Bash
ftp hedef_ip
```

_(Not: Varsayılan 21 portu dışında bir port kullanılıyorsa `ftp hedef_ip -P port_numarasi` şeklinde girilir)._

- **Giriş Bilgileri:**
    
    - Kullanıcı Adı: `anonymous`
        
    - Parola: _(Boş bırakıp Enter'a basılır)_
        

## 4. Temel FTP İstemci Komutları

Bağlantı sağlandıktan sonra terminal `ftp>` satırına düşer. İçeride veri toplamak ve dosya çekmek için şu komutlar kullanılır:

- `help` : Sunucuda çalıştırabileceğin geçerli komutların listesini ve açıklamalarını getirir.
    
- `ls` (veya `dir`) : İçinde bulunduğun dizindeki (klasördeki) dosyaları listeler.
    
- `get [dosya_adi]` : Hedef sunucudaki bir dosyayı kendi yerel makinenize indirir. (Örn: `get userlist`)
    
- `bye` : FTP oturumunu güvenli bir şekilde kapatır ve çıkar.