## 1. RDP (Remote Desktop Protocol) Nedir?

- **Tanım:** Microsoft tarafından geliştirilen, bir ağ üzerinden başka bir Windows bilgisayara grafik arayüz (GUI) ile uzaktan erişim sağlamaya olanak tanıyan protokoldür.
    
- **Varsayılan Port:** TCP **3389**
    
- **Zafiyet Mantığı:** Sistem yöneticileri bazen test amacıyla veya dikkatsizlik sonucu RDP servisini dışarıya açık unutabilir veya varsayılan yetkili kullanıcıların (Örn: `Administrator`) parolasız girişine izin verecek şekilde hatalı yapılandırabilir.
    

## 2. NetBIOS Keşfi ve Bilgi Toplama

Ağdaki Windows makinelerin isimlerini (Hostname) veya IP adreslerini çözümlemek için NetBIOS protokolü kullanılır. Bunun için Linux ortamında `nmblookup` aracı tercih edilir.

**Temel `nmblookup` Parametreleri:**

- `-A` : Bir bilgisayarın IP adresinden NetBIOS adını (Hostname) öğrenmek için kullanılır. _(Örn: `nmblookup -A hedef_ip`)_
    
- `-B` : Bir bilgisayarın NetBIOS adından IP adresini öğrenmek için kullanılır.
    

## 3. RDP Bağlantısı Kurma

Linux (Örn: Kali, HackerBox) üzerinden bir Windows makineye RDP ile bağlanmak için çeşitli açık kaynaklı araçlar bulunur. En popülerleri şunlardır:

- **Remmina:** Grafik arayüzü (GUI) olan, kullanımı çok kolay bir uzak masaüstü istemcisidir.
    
- **rdesktop:** Komut satırı üzerinden çalışan klasik RDP aracıdır.
    
- **FreeRDP (xfreerdp):** Modern ve komut satırı destekli güçlü bir alternatiftir.
    

_Sızma Testi İpucu:_ Hedefte RDP açıksa, her zaman `Administrator` (Windows'un varsayılan en yetkili kullanıcısı) adı ve boş parola ile giriş yapılıp yapılamayacağı test edilmelidir.

## 4. Windows İçi Keşif (Post-Exploitation Temelleri)

Sisteme (RDP üzerinden veya başka bir yolla) erişim sağlandıktan sonra içeride bilgi toplamak için şu yöntemler kullanılır:

- **İşletim Sistemi Versiyonunu Öğrenme:** PowerShell üzerinden sistemin tam versiyonunu çekmek için şu komut kullanılır:
    
    PowerShell
    
    ```
    Get-ComputerInfo | Select-Object WindowsVersion
    ```
    
- **Dosya/Klasör Sahipliğini İnceleme (GUI Yöntemi):** RDP ile bağlandığınız bir sistemde şüpheli bir klasör veya dosya bulduğunuzda, bu klasörün hangi kullanıcıya ait olduğunu (sahibini) öğrenmek için Windows arayüzünde şu yol izlenir:
    
    1. Klasöre sağ tıklayıp **Properties (Özellikler)** seçilir.
        
    2. **Security (Güvenlik)** sekmesine geçilir.
        
    3. **Advanced (Gelişmiş)** butonuna tıklanarak "Owner" (Sahip) bilgisi kontrol edilir.
        

---