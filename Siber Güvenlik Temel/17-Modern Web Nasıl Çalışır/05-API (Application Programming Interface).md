# API (Application Programming Interface) Temelleri


## 1. API Nedir?
API (Uygulama Geliştirme Arayüzü), farklı yazılımların ve sistemlerin birbirleriyle iletişim kurmasını sağlayan bir köprüdür. Genellikle Frontend (kullanıcı arayüzü) ile Backend (sunucu/veritabanı) arasındaki veri alışverişini standart protokollerle sağlar.

## 2. Temel API Çeşitleri ve Mimarileri

### A. REST (Representational State Transfer)
* **Mantığı:** Web üzerindeki sistemler arası iletişimde en yaygın kullanılan esnek mimari modeldir. Kaynak tabanlıdır ve HTTP protokolü üzerinden çalışır.
* **İşlev:** CRUD (Oluştur, Oku, Güncelle, Sil) işlemlerini destekler. Veri alışverişini genellikle **JSON** (veya XML) formatında yapar.
* **Örnek Uç Nokta (Endpoint):** `GET https://api.example.com/users/123`

### B. SOAP (Simple Object Access Protocol)
* **Mantığı:** HTTP ve **XML** tabanlı, daha katı kuralları olan eski ama sağlam bir protokoldür.
* **Kullanım Alanı:** Yüksek güvenlik, işlem bütünlüğü ve karmaşık mantık gerektiren kurumsal ve bankacılık uygulamalarında tercih edilir. 

### C. GraphQL
* **Mantığı:** Facebook tarafından geliştirilen modern bir sorgulama dilidir.
* **Avantajı:** REST'teki gibi sunucunun belirlediği veri paketini almak (aşırı veri yükü) yerine, tek bir istekle **sadece sizin belirttiğiniz spesifik verileri** almanızı sağlar. Performansı artırır.
* **Örnek Sorgu:**
```GraphQL
query {
    user(id: "123") { name, email }
}
```
 

### D. WebSocket

- **Mantığı:** HTTP'nin klasik "istek at - cevap al - bağlantıyı kapat" modelinin aksine, istemci ile sunucu arasında **iki yönlü ve sürekli (kesintisiz)** bir tünel kurar.
    
- **Kullanım Alanı:** Canlı destek mesajlaşmaları, borsa ekranları, online oyunlar gibi **gerçek zamanlı (real-time)** ve düşük gecikmeli veri akışı gereken yerlerde kullanılır (`ws://` veya güvenli hali `wss://`).
    

---

## 3. Popüler API Kullanım Alanları ve Örnekler

|Kategori|Popüler Servisler|İşlevi|
|---|---|---|
|**Sosyal Medya**|Facebook Graph, Twitter API, Instagram Graph|Dış uygulamalardan gönderi paylaşma, yorum okuma ve hesap analitiği çekme.|
|**Harita & Konum**|Google Maps API, OpenStreetMap, Mapbox|Uygulamalara etkileşimli harita gömme, yol tarifi ve GPS konum bazlı işlemler.|
|**Ödeme Sistemleri**|Stripe, PayPal, Square|Uygulama içinden çıkmadan kredi kartı ile güvenli ödeme alma ve faturalandırma.|
|**Hava Durumu**|OpenWeather, AccuWeather, Weatherstack|Lokasyona göre anlık hava durumu ve geçmiş meteorolojik verileri çekme.|

E-Tablolar'a aktar

---

## 4. API Güvenliği (Siber Güvenlik Odaklı)

API'ler doğrudan veritabanı veya iç sistemlerle konuştuğu için sızma testlerinde kritik hedeflerdir. Korunmak için şu temel yöntemler uygulanır:

- **Yetkilendirme (Auth):** İsteklerin anonim olmasını engellemek için **OAuth**, JWT (JSON Web Tokens) veya **API Anahtarları (API Keys)** kullanılır.
    
- **Veri Şifreleme:** İletişimin araya girenler (MitM) tarafından okunmaması için trafiğin mutlaka HTTPS üzerinden akması zorunlu kılınır.
    
- **Hız Sınırlandırma (Rate Limiting):** Bir IP adresinin veya kullanıcının saniyede yapabileceği API istek sayısını kısıtlayarak sunucuyu DoS (Servis Dışı Bırakma) ve Kaba Kuvvet (Brute-Force) saldırılarından korur.