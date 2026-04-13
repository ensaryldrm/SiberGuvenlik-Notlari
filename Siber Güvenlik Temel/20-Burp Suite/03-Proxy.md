# Burp Suite Proxy Modülü ve Trafik Analizi
## 1. Proxy Nedir?
Proxy (Vekil Sunucu), ağdaki istemci (tarayıcı) ile hedef sunucu arasındaki iletişime aracılık eden bir sistemdir.
Siber güvenlikte Proxy, kullanıcının internete çıkarken gerçek IP adresini gizlemesinin yanı sıra, cihazdan çıkan ve cihaza gelen tüm ağ trafiğini **izlemek, analiz etmek ve manipüle etmek** için kullanılır. Burp Suite'in en temel ve en çok kullanılan aracıdır.

---

## 2. Intercept (Durdurma) Modülü
Bu sekme, ağ trafiğini gerçek zamanlı olarak yakalayıp müdahale etmenizi sağlar.

* **Intercept is ON / OFF:** "ON" modundayken tarayıcıdan çıkan her HTTP/HTTPS isteği sunucuya gitmeden önce Burp Suite'te bekletilir (dondurulur). "OFF" modunda ise trafik kesintisiz akmaya devam eder.
* **Forward (İlet):** Bekletilen ve üzerinde istenen değişiklikler (Örn: XSS payload'u ekleme) yapılan isteği hedef sunucuya yollar.
* **Drop (Düşür):** Bekletilen isteği sunucuya hiç göndermeden iptal eder (yok sayar). Bağlantı koparılır.
* **Open Browser:** Sertifika yükleme veya proxy ayarı yapma zahmetine girmeden, Burp Suite'in kendi içine entegre edilmiş ve tüm ayarları hazır olan güvenli Chromium tarayıcısını tek tıkla açar. (Pratik testler için hayat kurtarıcıdır).

---

## 3. History (Geçmiş) Sekmeleri
Trafik akarken her isteği durdurmak (Intercept ON) çok yorucudur. Çoğu zaman trafik "OFF" modunda akarken arka planda kaydedilen loglar incelenir.

* **HTTP History:** Proxy üzerinden geçen istisnasız tüm HTTP/HTTPS isteklerini ve sunucudan dönen yanıtları zaman damgası, URL, metod (GET/POST) ve durum kodu (200, 404, 500) ile tablo halinde listeler. Listeden bir isteğe tıklandığında alt panelde detaylı Request/Response kodları görünür.
* **Websockets History:** Web soketleri (WebSockets), anlık mesajlaşma veya canlı borsa ekranları gibi sunucu ile istemci arasında sürekli açık kalan, çift yönlü ve gerçek zamanlı iletişimi sağlayan protokollerdir. Bu sekme, bu özel bağlantı türü üzerinden akan veriyi kaydeder.

---

## 4. Proxy Settings (Gelişmiş Ayarlar ve Filtreler)
Bu bölüm, trafiğin nereden dinleneceğini ve hangi kurallara göre yakalanacağını belirler.

* **Proxy Listeners (Dinleyiciler):** Burp Suite'in bilgisayarda hangi IP ve Port üzerinden trafiği dinleyeceğini ayarlar. Varsayılan olarak `127.0.0.1` (Localhost) ve `8080` portunu dinler. Birden fazla port için yeni dinleyiciler eklenebilir.
* **Request Interception Rules:** Hangi isteklerin "Intercept" ekranına düşeceğini filtreler. Örneğin; `.jpg`, `.png`, `.css` gibi resim ve stil dosyaları güvenlik testlerinde genellikle gereksizdir. Bu kurala "Uzantısı .jpg ise yakalama" derseniz, ekranınız gereksiz fotoğraflarla dolmaz.
* **Response Interception Rules:** Sunucudan dönen yanıtlar için filtre kuralları oluşturur. Sadece "200 OK" dönen başarılı sayfaları yakala veya "404 Not Found" hatalarını gizle gibi filtreler tanımlanabilir.

---

## 5. Harici Tarayıcı ve Sertifika (CA) Yönetimi
Burp'ün kendi tarayıcısı yerine kendi Chrome veya Firefox tarayıcınızı kullanmak isterseniz, HTTPS (Şifreli) trafiği okuyabilmek için bilgisayarınıza **Burp Suite Sertifikası** kurmanız şarttır. Aksi takdirde tarayıcı "Bağlantınız Gizli Değil" hatası verir.

**Adım Adım Kurulum:**
1. **Proxy Yönlendirmesi (FoxyProxy):** Tarayıcıya FoxyProxy eklentisi kurulur. Yeni bir profil açılarak IP adresi `127.0.0.1`, Port ise `8080` olarak ayarlanır ve aktif edilir. Artık tarayıcınız Burp üzerinden internete çıkmaktadır.
2. **Sertifikanın İndirilmesi:** FoxyProxy açıkken tarayıcının adres çubuğuna `http://burp` yazılır. Açılan sayfadan sağ üstteki **CA Certificate** butonuna basılarak `.der` uzantılı sertifika dosyası indirilir.
3. **Sertifikanın Yüklenmesi:** Tarayıcı ayarlarından "Güvenlik > Sertifikaları Yönet" kısmına girilir. "Güvenilir Kök Sertifika Yetkilileri (Trusted Root Certification Authorities)" sekmesine gelinir ve indirilen dosya "İçe Aktar (Import)" edilerek tüm izinler verilir.