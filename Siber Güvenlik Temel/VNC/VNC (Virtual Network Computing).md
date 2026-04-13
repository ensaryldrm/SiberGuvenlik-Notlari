# VNC (Virtual Network Computing) Nedir ve Nasıl Kullanılır?


## 1. VNC Nedir?
* **Tanım:** VNC (Sanal Ağ Hesaplama), bir bilgisayarın masaüstü ortamını ağ üzerinden başka bir bilgisayardan görüntülemek ve kontrol etmek için kullanılan grafiksel bir masaüstü paylaşım sistemidir.
* **Protokol:** Temelinde **RFB (Remote Frame Buffer)** protokolünü kullanır.
* **Varsayılan Port:** Genellikle TCP **5900** (veya ekran numarasına göre 5901, 5902...) portlarını kullanır.
* **Platform Bağımsızlığı:** VNC'nin en büyük avantajı işletim sisteminden bağımsız olmasıdır. Bir Windows makinesinden bir Linux sunucusuna veya Mac'ten bir Raspberry Pi'ye kolayca grafiksel bağlantı kurabilirsin.

## 2. RDP ile VNC Arasındaki Fark Nedir?
* **RDP (Uzak Masaüstü):** Microsoft'a özgüdür. Genellikle arka planda sanal bir oturum açar, Windows sistemlerde çok hızlıdır ve bant genişliğini verimli kullanır.
* **VNC:** Ekrandaki pikselleri (görüntüyü) karşı tarafa aktarma mantığıyla çalışır. Bu nedenle RDP'ye göre biraz daha yavaş olabilir ancak her işletim sisteminde (Linux, macOS, Windows) çalışır. O an bilgisayarın başında oturan kişi ekranda ne görüyorsa, VNC ile bağlanan kişi de birebir aynı ekranı görür.

## 3. VNC Mimarisinin Temel Bileşenleri
VNC, klasik İstemci-Sunucu (Client-Server) mimarisiyle çalışır:
* **VNC Server (Sunucu):** Uzaktan kontrol edilecek (hedef) makineye kurulur. Ekran görüntüsünü yakalar ve istemciye gönderir. (Örn: *TightVNC, RealVNC, TigerVNC, x11vnc*)
* **VNC Viewer/Client (İstemci):** Kontrolü sağlayacak olan (sizin) bilgisayarınıza kurulur. Klavyeden ve fareden gelen hareketleri sunucuya iletir.

---

## 4. Adım Adım VNC Kullanımı (Linux Örneği)

Diyelim ki uzaktaki bir Ubuntu sunucusunun masaüstüne bağlanmak istiyorsunuz:

### Adım 1: Hedef Makineye VNC Sunucusu Kurma
Hedef (uzak) makinede bir VNC sunucusu yazılımı kurulur.
```bash
sudo apt update
sudo apt install tightvncserver
````

### Adım 2: VNC Sunucusunu Başlatma ve Parola Belirleme

Sunucuyu ilk kez başlattığınızda sizden bir erişim parolası belirlemenizi ister:

```Bash
vncserver
```

_(Bu komut çalıştırıldığında VNC genellikle `:1` numaralı ekranı oluşturur. Bu, port numarasının `5901` olduğu anlamına gelir)._

### Adım 3: Kendi Makinenizden Bağlantı Kurma

Kendi bilgisayarınıza bir VNC Viewer (Örn: RealVNC Viewer veya Remmina) kurun. Bağlantı adresine hedef IP'yi ve portu yazın:


```Plaintext
Hedef Adres: 192.168.1.50:5901
```

Bağlan (Connect) butonuna tıkladıktan sonra 2. adımda belirlediğiniz parolayı girerek uzak masaüstüne erişebilirsiniz.

---

## 5. VNC ve Siber Güvenlik (Kritik Uyarı)

VNC, varsayılan halinde **şifrelenmemiş (clear-text)** bir protokoldür. Eğer VNC trafiğini internete doğrudan açarsanız, klavye vuruşlarınız ve ekrandaki görüntüler aradaki saldırganlar (Man-in-the-Middle) tarafından ele geçirilebilir.

**Güvenli Kullanım (SSH Tünelleme):** Sızma testlerinde ve profesyonel sistem yönetiminde VNC portu asla dışarıya (internete) açılmaz. Bunun yerine VNC trafiği, güvenli bir SSH tünelinin içinden geçirilir:

_Güvenli bağlantı için kendi makinenizde çalıştıracağınız SSH Tünel komutu:_



```Bash
ssh -L 5901:127.0.0.1:5901 kullanici_adi@hedef_ip
```

_Bu komut çalıştıktan sonra VNC Viewer programınıza hedef olarak `127.0.0.1:5901` yazarsınız ve görüntü SSH şifrelemesinin içinden güvenle gelir.



## 6. Remmina bağlantısı

Konsola remmina yazıp uygulamayı çalıştırıp ip ve portu yazıp bilgisayara bağlanabiliriz vnc ile.

whoami ile kim olduğumuzu öğreniriz.
uname -r ile linuxun bilgisini öğreniriz.