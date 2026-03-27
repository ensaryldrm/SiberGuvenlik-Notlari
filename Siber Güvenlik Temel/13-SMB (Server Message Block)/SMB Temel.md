## 1. SMB (Server Message Block) Nedir?

- **Tanım:** Ağ üzerindeki cihazlar (özellikle Windows işletim sistemleri) arasında dosya, yazıcı ve diğer kaynakların paylaşılmasını sağlayan ağ iletişim protokolüdür.
    
- **Varsayılan Port:** TCP **445** (Eski sistemlerde NetBIOS üzerinden 139 da kullanılır).
    
- **Zafiyet Mantığı:** SMB'nin eski sürümleri (SMBv1) çok ciddi zafiyetler barındırır. Ayrıca sistem yöneticilerinin yanlış yapılandırmaları sonucu, hassas klasörler kimlik doğrulaması olmadan (Anonim / Null Session) dışarıdan erişime açık bırakılabilir.
    

## 2. Windows'taki Gizli ve Varsayılan Paylaşımlar (Shares)

Windows sistemler, ağ üzerinde bazı dizinleri yönetimsel amaçlarla varsayılan olarak paylaşıma açar. Sonunda `$` işareti olan paylaşımlar **gizlidir** ve normal ağ taramalarında gözükmezler.

- **C$ / D$ :** Sistem yöneticilerine ayrılmış, doğrudan C: veya D: sürücülerinin kök dizinine tam erişim sağlayan gizli paylaşımlardır.
    
- **ADMIN$ :** Yönetimsel amaçlıdır, genellikle Windows'un kurulu olduğu dizine (`C:\Windows`) erişim sağlar.
    
- **IPC$ (Inter-Process Communication Share) :** İşlemler arası iletişim için kullanılır. Doğrudan dosya/dizin erişimi sağlamaz ancak sistemdeki kullanıcıları ve diğer paylaşımları listelemek (Enumeration) için anonim oturumlarda sıklıkla istismar edilir.
    
- **PRINT$ :** Ağ üzerinden yazıcılara erişimi ve sürücü yapılandırmalarını kolaylaştırmak için kullanılan paylaşımdır.
    

## 3. smbclient Nedir ve Nasıl Kullanılır?

`smbclient`, Linux terminali üzerinden FTP'ye benzer bir mantıkla Windows (SMB) paylaşımlarına bağlanmamızı sağlayan araçtır.

**En Sık Kullanılan Parametreleri:**

- `-L` (List): Hedef sunucudaki mevcut paylaşımları (klasörleri) listeler.
    
- `--no-pass` (veya kısaca `-N`): Parola sormayı devre dışı bırakır. (Anonim giriş denemeleri için şarttır).
    

## 4. SMB Sızma Testi Metodolojisi (CTF Adımları)

Bir CTF makinesinde veya sızma testinde 445 portunun açık olduğu görüldüğünde şu adımlar izlenir:

### Adım 1: Paylaşımları Listeleme (Keşif)

Öncelikle hedef sistemde dışarıya açık hangi klasörlerin olduğu, parola girmeden (anonim olarak) listelenmeye çalışılır:

Bash

```
smbclient -L <hedef_ip_adresi> --no-pass
```

_Bu komutun çıktısında isimleri (`Sharename`) ve yanlarında açıklamaları (`Comment`) olan bir tablo listelenir. İlginç görünen bir paylaşım adı (Örn: `Projects`, `Backups`, `Public`) not alınır._

### Adım 2: Belirli Bir Paylaşıma Bağlanma

Keşfedilen ve parolaya ihtiyaç duymadığı tahmin edilen hedefe bağlanılır. (Not: Linux terminalinde ters bölü `\` karakteri kaçış karakteri olduğu için komut satırında çift yazılarak `\\\\` şeklinde kullanılır).

Bash

```
smbclient --no-pass \\\\<hedef_ip_adresi>\\<Paylasim_Adi>
```

_(Alternatif ve daha kolay kullanım: `smbclient //hedef_ip_adresi/Paylasim_Adi -N`)_

### Adım 3: İçeride Gezinme (Dosya Okuma)

Bağlantı başarılı olursa `smb: \>` şeklinde bir komut satırına düşülür. Bu aşamadan sonrası tıpkı FTP komutlarına benzer:

- `help` : Kullanılabilecek komutları gösterir.
    
- `ls` (veya `l`) : Bulunduğunuz klasördeki dosyaları listeler.
    
- `get <dosya_adi>` : Hedefteki şüpheli dosyayı kendi makinenize indirmenizi sağlar.