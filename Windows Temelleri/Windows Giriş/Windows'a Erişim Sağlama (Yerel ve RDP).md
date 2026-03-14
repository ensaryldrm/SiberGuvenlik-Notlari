
Bilgisayar açıldığında, Windows'un masaüstüne veya oturum açma ekranına yönlendirilirsiniz. Bu ekran, geçerli hesap bilgilerini girmeniz gereken yerdir. İki temel erişim yöntemi bulunur:

## Yerel Erişim
Fiziksel erişiminizin olduğu bir bilgisayarın doğrudan başında oturarak giriş yaptığınız yöntemdir.

## Uzaktan Erişim
Fiziksel erişiminizin olmadığı bir makineye (sunucu, sanal makine vb.) ağ üzerinden sağlanan bağlantıdır.

### RDP (Uzak Masaüstü Protokolü)
* Microsoft tarafından geliştirilmiş bir uzak masaüstü teknolojisidir.
* Bir ağ üzerinden başka bir bilgisayara, sanki o bilgisayarın direkt önünde oturuyormuş gibi erişim sağlamanızı ve çalışmanızı sağlar.
* Bağlantı için hedef makinede RDP'nin aktif olması ve geçerli bir kullanıcı adı/şifre ile kimlik doğrulaması gerekir.
* **Araç Örneği:** RDP protokolünü kullanan popüler programlara bir örnek Linux sistemlerde de sıkça kullanılan **Remmina**'dır.

```Bash
xfreerdp /v:HEDEF_IP_ADRESI /u:KULLANICI_ADI /p:SIFRE
```


### SSH (Secure Shell)

```Bash
ssh kullanici_adi@hedef_ip_adresi
```


```Bash
ssh -p PORT_NUMARASI kullanici_adi@hedef_ip_adresi
```
