# Burp Suite Dashboard ve Görev Yönetimi
## 1. Dashboard (Ana Ekran) Nedir?
Dashboard, Burp Suite açıldığında karşımıza çıkan ilk ekrandır. Uygulamanın kontrol merkezi (komuta merkezi) olarak görev yapar ve yürütülen güncel çalışmalar hakkında anlık ve özet bir görünüm sunar.

**Temel Özellikleri:**
* **Güvenlik Açığı Tarama (Vulnerability Scanning):** Tarama işlemlerini başlatma, duraklatma veya iptal etme seçenekleri sunar. Dashboard üzerinde bulunan **"New scan"** butonu ile hedefe yönelik yeni bir otomatik güvenlik taraması başlatılabilir. *(Not: Otomatik tarama özelliği sadece Professional ve Enterprise sürümlerinde mevcuttur).*
* **Görev Listesi (Tasks):** Arka planda çalışan aktif görevlerin veya tamamlanmış işlemlerin listelendiği alandır.
* **Güvenlik Uyarıları (Issue Activity):** Otomatik taramalar veya pasif analizler sırasında tespit edilen güvenlik zafiyetlerinin gerçek zamanlı olarak düştüğü kısımdır.

---

## 2. Görev Yönetimi (Task Management)
Burp Suite, arka planda yapılan tüm işlemleri "Görevler (Tasks)" olarak adlandırır ve Dashboard üzerinden bu görevlerin yönetilmesini sağlar.

* **Yeni Görev Ekleme:** Dashboard'da bulunan **"New live task"** butonu kullanılarak, tarayıcıdan gelen trafiği pasif olarak izleyen veya aktif olarak tarayan yeni görevler eklenebilir.
* **Görev Durumunu Kontrol Etme:** Her görevin kendi panelinde mevcut durumunu (aktif, duraklatılmış, tamamlanmış veya hata vermiş) ve ilerleme yüzdesini gösteren simgeler ve ilerleme çubukları (progress bar) bulunur.

---

## 3. Güvenlik Uyarıları ve Analiz (Issue Activity)
Hedef web uygulamasında bulunan potansiyel zafiyetler, ciddiyet derecelerine göre (High, Medium, Low, Information) renk kodlarıyla bu bölümde listelenir. Listeden bir zafiyete tıklandığında detaylı analiz penceresi açılır:

* **Zafiyet Türü (Issue Detail):** Tespit edilen açığın teknik adıdır (Örn: Cross-site scripting (Reflected)).
* **Etkilenen Alan (Path):** Zafiyetin bulunduğu tam URL adresi ve etkilenen parametreler.
* **Açıklama (Background):** Zafiyetin ne olduğu ve nasıl çalıştığına dair teorik açıklama.
* **Öneriler (Remediation):** Zafiyetin yazılım tarafında nasıl yamalanabileceği ve giderilebileceği hakkında çözüm önerileri (Örn: Girdilerin filtrelenmesi, Output encoding kullanılması vb.).

---

## 4. Ayarlar ve Kişiselleştirme (Settings)
Eski sürümlerde sekmeler arasında dağınık olan ayarlar, yeni sürümlerde Dashboard'un sağ üst köşesinde bulunan **Settings (Ayarlar)** simgesi (dişli çark) altında toplanmıştır.

Bu bölümden yapılabilecek başlıca konfigürasyonlar:
* **Network / Proxy Ayarları:** Burp'ün dinlediği portu ve arayüzü değiştirme.
* **Tarama Hızı ve Performans:** Otomatik tarayıcının sunucuya saniyede kaç istek atacağı (Thread sayısı).
* **Görünüm (Display):** Karanlık tema (Dark Mode) seçimi ve font büyüklükleri.
* **Otomatik Güncellemeler:** Uygulamanın güncelleme davranışlarını kontrol etme.