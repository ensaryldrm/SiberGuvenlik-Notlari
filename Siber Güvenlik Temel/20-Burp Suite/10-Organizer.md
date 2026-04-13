# Burp Suite Organizer: Bilgi ve Bulgu Yönetimi
## 1. Organizer Nedir?
Organizer, Burp Suite içerisinde gerçekleştirilen sızma testleri (pentest) boyunca elde edilen bulguları, şüpheli trafikleri, alınan notları ve gözlemleri tek bir merkezde düzenli bir şekilde saklamaya yarayan dijital bir not defteridir.

* **Neden Önemlidir?** Kapsamlı bir güvenlik testi günlerce, hatta haftalarca sürebilir. Testin sonunda rapor yazarken "O bulduğum SQL Injection parametresi hangi sayfadaydı?" diye düşünmemek ve binlerce satır log arasında kaybolmamak için şüpheli görülen her şey anında Organizer'a kaydedilir.

---

## 2. Organizer Kullanımı ve Veri Aktarımı
Organizer modülüne iki farklı şekilde veri eklenebilir:

* **Manuel Not Ekleme:** Doğrudan Organizer sekmesine gidip **"Add note" (Not ekle)** butonuna tıklayarak bağımsız bir not (Örn: "Admin panelinin IP adresi: 10.0.0.5") oluşturulabilir.
* **Trafik Aktarımı (En Sık Kullanılan):** Proxy, HTTP History, Repeater veya Target ekranlarında incelenen şüpheli bir isteğin üzerine sağ tıklanıp **"Send to Organizer"** seçeneği tıklanır. Bu işlem, o anki HTTP isteğini ve yanıtını (Request/Response) kopyalayarak Organizer'a atar ve üzerine özel notlar yazmanıza olanak tanır.

---

## 3. Sınıflandırma ve Yönetim
Organizer'ın en güçlü tarafı, eklenen bulguları kolayca filtreleyebilmek için sunduğu görsel ve metinsel sınıflandırma etiketleridir. Listede bir öğenin üzerine sağ tıklandığında şu işlemler yapılabilir:

* **Status (Durum Atama):** Bulgunun o anki aşamasını belirler.
  * `New (Yeni)`: Yeni eklendi, henüz incelenmedi.
  * `In Progress (İşlemde)`: Şu an bu zafiyet üzerinde çalışılıyor (Örn: Repeater'da test ediliyor).
  * `Done (Tamamlandı)`: Zafiyet doğrulandı (veya yanlış pozitif olduğu anlaşıldı), raporlanmaya hazır.
* **Highlight (Renklendirme):** Satırları görsel olarak kategorize etmek için renk atanır (Kırmızı, Mavi, Sarı vb.). Örneğin; kesinleşmiş kritik zafiyetleri Kırmızı, sadece şüphelendiğiniz ve sonra bakacağınız yerleri Sarı renkle işaretleyerek görsel bir hiyerarşi oluşturabilirsiniz.
* **Filtreleme:** Tablonun üst kısmındaki filtreler kullanılarak "Sadece Durumu 'Yeni' olanları ve Rengi 'Kırmızı' olanları göster" gibi hızlı aramalar yapılabilir. Bu da rapor yazım sürecini inanılmaz derecede hızlandırır.