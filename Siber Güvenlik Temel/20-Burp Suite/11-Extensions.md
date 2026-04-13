# Burp Suite Extensions: Eklenti Yönetimi ve BApp Store
## 1. Extensions (Eklentiler) Nedir?
Extensions, Burp Suite'in varsayılan yeteneklerini aşarak işlevselliğini artıran, güvenlik test süreçlerini özelleştiren ve manuel yapılan zorlu görevleri otomatikleştiren eklentilerdir. 

Bu eklentiler sayesinde Burp Suite, sadece bir Proxy aracı olmaktan çıkıp her türlü güvenlik açığına özel olarak modifiye edilebilen devasa bir platforma dönüşür.

---

## 2. Eklenti Yükleme Yöntemleri
Burp Suite'e eklenti yüklemenin iki temel yolu vardır:

### A. BApp Store'dan Yükleme (Önerilen)
Burp Suite'in kendi resmi ve güvenilir uygulama mağazasıdır.
1. Üst menüden **Extensions** sekmesine gidilir.
2. Alt sekmelerden **BApp Store** seçilir.
3. Çıkan listeden ihtiyaç duyulan eklenti bulunur ve sağ taraftaki **"Install" (Yükle)** butonuna basılır. (Not: Bazı eklentiler sistemde Python [Jython] veya Ruby ortamlarının kurulu olmasını gerektirebilir).

### B. Manuel Yükleme
İnternetten (Örn: GitHub) indirilen veya kendi yazdığınız özel bir eklentiyi yüklemek için kullanılır.
1. **Extensions > Installed** sekmesine gidilir.
2. **"Add" (Ekle)** butonuna tıklanır.
3. Eklentinin yazıldığı dil (Java, Python veya Ruby) seçilir.
4. **"Select file"** ile bilgisayardaki `.jar` veya `.py` dosyası seçilip yüklenir.

---

## 3. Sızma Testlerinde En Sık Kullanılan Eklentiler

| Eklenti Adı | Siber Güvenlikteki İşlevi ve Amacı |
| :--- | :--- |
| **Turbo Intruder** | Standart Intruder'dan çok daha hızlı ve güçlü bir HTTP saldırı aracıdır. Race Condition (Yarış Durumu) zafiyetlerini test etmek ve devasa Fuzzing işlemleri için saniyede binlerce istek atar. |
| **Autorize** | Farklı yetkilere sahip kullanıcılar arasındaki erişim kontrolü (IDOR / Privilege Escalation) zafiyetlerini otomatik olarak test eder. Sizi sürekli hesap değiştirme zahmetinden kurtarır. |
| **SQLMap for Burp** | Dünyanın en popüler SQL Enjeksiyon aracı olan SQLMap'i doğrudan Burp Suite içerisinden tek tıkla çalıştırmanızı sağlar. |
| **Active Scan++** | Burp Suite'in mevcut zafiyet tarayıcısını (Scanner) genişleterek, tespit edilmesi zor olan daha modern ve kompleks güvenlik açıklarını da taramasına olanak tanır. |
| **403 Bypasser** | Sunucu tarafından erişimi engellenmiş (HTTP 403 Forbidden) gizli dizinlere erişmek için çeşitli header manipülasyonlarını otomatik olarak dener. |

---

## 4. Eklenti Yönetimi (Kullanım, Güncelleme ve Kaldırma)
* **Kullanım:** Yüklenen eklentiler genellikle Burp Suite'in üst menüsüne tamamen **yeni bir sekme** olarak eklenir veya Site Map / HTTP History'de sağ tık (Context) menüsüne yeni seçenekler olarak yerleşir.
* **Güncelleme:** BApp Store üzerinden yüklenen eklentiler için mağaza sekmesinde güncellemeler kontrol edilir ve çıkan talimatlar izlenir.
* **Kaldırma:** `Extensions > Installed` sekmesindeki listeden istenen eklenti seçilir ve sağ taraftaki **"Remove" (Kaldır)** butonuna tıklanarak sistemden silinir.

---

## 5. API Desteği (Kendi Eklentini Yazma)
Burp Suite (PortSwigger), geliştiricilere platformun kalbine erişebilmeleri için kapsamlı API'ler sunar. Bu API'ler kullanılarak (Java veya Python ile) şirketinizin kendi iç mimarisine veya özel bir zafiyet türüne yönelik tamamen size ait eklentiler kodlayabilir ve iş akışınızı otomatikleştirebilirsiniz.