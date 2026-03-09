Windows Defender Güvenlik Duvarı (Firewall), cihazın ağ üzerindeki iletişimini denetler ve yetkisiz erişimleri engeller. Cihazın bağlı olduğu ağ türüne göre farklı güvenlik profilleri uygular:

* **Etki Alanı (İş Yeri) Ağı:** Active Directory gibi bir domain ortamına bağlıyken kullanılır.

* **Özel (Güvenilen) Ağ:** Ev veya iş yeri gibi güvenilir yerel ağlar içindir (Dosya ve yazıcı paylaşımına izin verilebilir).

* **Ortak (Güvenilmeyen) Ağ:** Kafe veya havalimanı gibi ortak Wi-Fi ağları içindir. En sıkı güvenlik kuralları burada uygulanır.

## Yapılandırma Seçenekleri
* **Uygulamaya İzin Verme:** Güvenlik duvarı meşru bir uygulamanın iletişimini engelliyorsa, manuel olarak "Özel Durum (Exception)" eklenebilir.

* **Ağ ve İnternet Sorun Giderici:** Genel bağlantı sorunlarını otomatik teşhis edip düzeltir.

* **Bildirim Ayarları:** Güvenlik duvarı bir eylemi engellediğinde kullanıcıya verilecek uyarıların seviyesini belirler.

* **Gelişmiş Ayarlar:** Gelen/giden kuralları (Inbound/Outbound rules), port izinleri, bağlantı güvenlik kuralları oluşturmak ve logları incelemek için kullanılır.

* **Varsayılana Geri Yükle:** Yapılan kural değişiklikleri sistemi bozduysa güvenlik duvarını ilk kurulduğu anki sıfır ayarlarına döndürür.