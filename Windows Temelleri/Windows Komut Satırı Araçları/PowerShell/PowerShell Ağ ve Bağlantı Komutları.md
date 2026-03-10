# PowerShell Ağ ve Bağlantı Komutları
PowerShell, ağ kartlarını listelemek, bağlantı durumlarını kontrol etmek ve IP adreslerini yapılandırmak için hem modern cmdlet'leri hem de eski CMD (MS-DOS) araçlarını bir arada kullanmaya olanak tanır.

## 1. Ağ Yapılandırması ve Bilgi Edinme

* **Get-NetIPAddress:** Bilgisayarın ağ arabirimlerine (network interfaces) atanmış IP adreslerini ve güncel yapılandırma bilgilerini detaylı olarak listeler.
```powershell
Get-NetIPAddress
````

- **ipconfig:** (Klasik CMD aracı) Bilgisayarın mevcut ağ bağlantılarına atanan IPv4/IPv6 adreslerini, alt ağ maskelerini (subnet mask) ve varsayılan ağ geçitlerini (default gateway) özet halinde gösterir.
    


```DOS
ipconfig
```

- **netstat:** Bilgisayarın anlık ağ bağlantılarını, dinlenen (listening) veya kurulan (established) bağlantı noktalarını (portları) görüntüler.
    

```DOS
netstat
```

- **nslookup:** Bir alan adının (domain) DNS sunucularında çözülmesini sağlar. Alan adına karşılık gelen hedef IP adresini bulmak için kullanılır.
    

```DOS
nslookup example.com
```

- **arp:** IP adreslerini fiziksel MAC adreslerine eşleyen ARP (Address Resolution Protocol) önbelleğini listeler ve yönetir.
    

```DOS
arp -a
```

## 2. Ağ Bağlantısını Test Etme

- **Test-NetConnection:** Hedef makineye ping atarak veya belirli bir porta istek göndererek ağ bağlantısının durumunu test eder.
    

```PowerShell
Test-NetConnection
```

## 3. Web Üzerinden Dosya İndirme

- **Invoke-WebRequest:** Web sayfaları ve HTTP/HTTPS servisleriyle etkileşim kurmak için kullanılan çok güçlü bir cmdlet'tir. Genellikle terminal üzerinden doğrudan dosya indirmek için kullanılır.
    
    - `-Uri`: İndirilecek dosyanın veya sayfanın tam web adresi.
        
    - `-OutFile`: Dosyanın bilgisayara hangi isimle kaydedileceği.
        

```PowerShell
Invoke-WebRequest -Uri "[https://example.com/file.png](https://example.com/file.png)" -OutFile "kaydedilen_dosya.png"
```