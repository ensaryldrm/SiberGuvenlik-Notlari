## 1. NFS Nedir?

- **Tanım:** UNIX ve Linux tabanlı sistemler arasında, ağ üzerinden dosya ve dizin paylaşımını sağlayan bir protokoldür. Bir NFS istemcisi, uzaktaki sunucuda bulunan dosyaları sanki kendi yerel sabit diskindeymiş gibi kullanabilir.
    
- **Varsayılan Portlar:** NFS'nin düzgün çalışabilmesi için iki temel porta ihtiyacı vardır:
    
    - **TCP/UDP 111 (RPCBind / Portmapper):** İstemcilere NFS servisinin hangi portta çalıştığını söyler.
        
    - **TCP/UDP 2049 (NFS):** Asıl dosya aktarımının yapıldığı porttur.
        

## 2. Bilgi Toplama ve Paylaşımları Listeleme (Enumeration)

Bir hedefte 111 ve 2049 portları açıksa, dışarıya paylaşılan (export edilen) klasörleri görmek için Linux sistemlerde bulunan `showmount` komutu kullanılır:


```Bash
showmount -e <hedef_ip_adresi>
```

-a : Hem client bilgisayar adını veya IP adresini hem de bağlanan dizini
bilgisayar:dizin biçiminde listeleyin.
-d : Sadece bağlanan dizinleri listeleyin.
-e : NFS sunucusunun dışa aktarma listesini gösterir.
-h : Yardım menüsü

_(Not: `-e` parametresi "exports" anlamına gelir. Çıktı olarak size hedefin hangi klasörleri, hangi IP bloklarına paylaştığını gösterir. Örneğin: `/var/nfs_share *` satırındaki `*` işareti, o klasöre herkesin bağlanabileceği anlamına gelir)._

## 3. Sisteme Erişim: Paylaşımı Bağlama (Mount)

NFS paylaşımlarına FTP veya SMB gibi doğrudan bir istemci arayüzü ile girilmez. Hedefteki klasörü, kendi Linux makinemizdeki boş bir klasöre "monte etmemiz" (Mount) gerekir.

**Adım Adım Bağlama İşlemi:**

1. Kendi makinemizde geçici ve boş bir klasör oluşturulur:
    
    
    
    ```Bash
    mkdir /tmp/nfs_hedef
    ```
    
2. Hedefteki paylaşım (`/var/nfs_share`), kendi oluşturduğumuz klasöre bağlanır:
    
    
    
    ```Bash
    sudo mount -t nfs <hedef_ip>:/var/nfs_share /tmp/nfs_hedef
    ```
    
3. Artık hedef sisteme bağlandık. Kendi yerel klasörümüze giderek hedefteki dosyaları görebiliriz:
    
    
    ```Bash
    cd /tmp/nfs_hedef
    ls -la
    ```
    

_(İşlem bittikten ve dosyaları çektikten sonra bağlantıyı güvenle koparmak için `sudo umount /tmp/nfs_hedef` komutu kullanılır)._

## 4. İleri Düzey: `no_root_squash` Zafiyeti

Sızma testlerinde ve CTF'lerde NFS ile ilgili en çok aranan yapılandırma hatasıdır.

- NFS sunucusunun ayarları `/etc/exports` dosyası içinde tutulur.
    
- **Varsayılan Güvenlik (root_squash):** Siz kendi makinenizde "root" yetkisinde olsanız bile, NFS klasörüne bağlandığınızda sunucu sizin yetkilerinizi sıradan, yetkisiz bir kullanıcıya (`nfsnobody`) düşürür.
    
- **Yapılandırma Hatası (no_root_squash):** Sistem yöneticisi bu özelliği ayarlarına eklediyse, kendi makinenizde `root` iseniz, hedef makinenin NFS paylaşımında da **tam yetkili `root` olarak** işlem yaparsınız.



