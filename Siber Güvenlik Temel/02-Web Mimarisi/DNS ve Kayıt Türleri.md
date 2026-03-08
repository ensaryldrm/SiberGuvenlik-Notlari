DNS, internetin telefon rehberidir. İnsanların okuyabildiği alan adlarını (`google.com`), makinelerin okuyabildiği IP adreslerine (`142.250.190.46`) çevirir.

## DNS Hiyerarşisi (URL'nin Parçaları)
Örnek URL: `blog.tryhackme.com`
* **Root (Kök):** En sondaki gizli noktadır `.`.
* **TLD (Top Level Domain):** `.com`, `.org`, `.net` (En üst düzey alan adı).
* **SLD (Second Level Domain):** `tryhackme` (Satın alınan asıl marka/isim).
* **Subdomain (Alt Alan Adı):** `blog` (Ana siteye bağlı alt siteler). Subdomain keşfi (Enumeration) bilgi toplama aşamasının kalbidir!

## Önemli DNS Kayıt Türleri (Record Types)
| Kayıt Tipi | Ne İşe Yarar? | Siber Güvenlik Önemi |
| :--- | :--- | :--- |
| **A Kaydı** | Alan adını bir **IPv4** adresine yönlendirir. | Hedefin asıl sunucu IP'sini bulmamızı sağlar. |
| **AAAA Kaydı**| Alan adını bir **IPv6** adresine yönlendirir. | Modern ağ taramalarında kullanılır. |
| **CNAME** | Bir alan adını başka bir alan adına yönlendirir (Alias). | Subdomain Takeover (Alt alan adı gaspı) zafiyeti aranır. |
| **MX Kaydı** | E-posta trafiğini yönetecek sunucuyu (Mail Exchange) belirler. | Oltalama (Phishing) ve mail güvenliği testlerinde incelenir. |
| **TXT Kaydı** | Domain sahibinin kimliğini doğrulamak için metin tutar. | SPF, DKIM gibi mail güvenlik ayarlarının yanlış yapılandırılması aranır. |