## Sistem Dosyaları

### Program Dosyaları

- `\Program Files`: 64-bit Windows'ta 64-bit programlar için.
    
- `\Program Files (x86)`: 64-bit Windows'ta 32-bit programlar için.
    
- `\ProgramData`: Kullanıcıdan bağımsız program verileri için.
    

### Kullanıcı Verileri

- `\Users`: Her kullanıcı için bir profil klasörü içerir.
    
- `\Public`: Kullanıcılar arasında paylaşılan dosyalar için.
    
- `[kullanıcı_adı]\AppData`: Kullanıcı başına uygulama verileri ve ayarları için.
    

### Windows Sistemi

- `\Windows`: Windows'un kendisini içerir.
    
- `\System`, `\System32`, `\SysWOW64`: Windows çekirdek bileşenlerini ve dinamik bağlantı kitaplıklarını (DLL'lerini) içerir.
    
- `\WinSxS`: Windows bileşen deposu (güncellemeler ve hizmet paketleri dahil).
    

### Diğer

- `\PerfLogs`: Windows performans kayıtları (varsayılan olarak boş).
    

---

## Dosya Sistemi

Windows ilk çıktığında, **FAT (File Allocation Table)** dosya sistemini kullanıyordu. FAT, basit ve uyumlu bir dosya sistemiydi, ancak büyük dosyaları (4 GB'tan büyük) desteklemiyordu ve gelişmiş güvenlik özellikleri sunmuyordu.

1993 yılında Windows NT 3.1 ile birlikte **NTFS (New Technology File System)** dosya sistemi tanıtıldı. NTFS, FAT'ın eksikliklerini gidermek için tasarlanmıştı. Büyük dosyaları destekler, dosya ve klasör izinleri gibi gelişmiş güvenlik özellikleri sunar ve disk alanını daha verimli kullanır. NTFS günümüzde Windows'un varsayılan dosya sistemidir.

2000'li yılların başında USB flash sürücüler gibi taşınabilir depolama aygıtları popüler hale geldi. **FAT32** dosya sistemi, taşınabilir depolama aygıtları için ideal bir çözüm olarak ortaya çıktı. FAT32, FAT'tan daha gelişmiş bir dosya sistemidir ve 4 GB'tan büyük dosyaları destekler.

2006 yılında Windows Vista ile birlikte **exFAT (Extended File Allocation Table)** dosya sistemi tanıtıldı. exFAT, FAT32'nin yerini alması için tasarlanmıştır ve 4 GB'tan büyük dosyaları destekler. NTFS kadar gelişmiş olmasa da, daha basittir ve taşınabilir depolama aygıtları için daha uygundur.