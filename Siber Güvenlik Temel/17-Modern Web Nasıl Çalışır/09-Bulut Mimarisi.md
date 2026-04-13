# Bulut Mimarisi ve Modern Web Teknolojileri
## 1. Bulut Bilişim (Cloud Computing) Nedir?
İnternet üzerinden erişilebilen veri depolama, işleme ve yönetim hizmetlerini kapsayan dağıtık bilgi işlem altyapısıdır. İşletmeleri fiziksel sunucu maliyetlerinden kurtararak esneklik, yüksek erişilebilirlik ve otomatik ölçeklenebilirlik sağlar.

### Bulut Dağıtım Modelleri
* **Kamu Bulutu (Public Cloud):** İnternet üzerinden herkese açık kaynaklardır (AWS, Google Cloud). Donanım birden fazla müşteri (kiracı) tarafından paylaşılır.
* **Özel Bulut (Private Cloud):** Sadece tek bir kuruma ayrılmış, genellikle yüksek güvenlik ve yasal uyumluluk gerektiren durumlarda kullanılan altyapıdır.
* **Hibrit Bulut (Hybrid Cloud):** Kamu ve özel bulutun birleşimidir. Hassas veriler özel bulutta tutulurken, genel işlemler kamu bulutuna aktarılabilir.

---

## 2. Bulut Hizmet Modelleri

| Model | Açılımı ve Anlamı | Kullanıcı Kontrolü | Örnekler |
| :--- | :--- | :--- | :--- |
| **IaaS** | **Infrastructure as a Service (Altyapı):** Sanal sunucu, ağ ve depolama gibi temel donanım kaynaklarının internetten sunulmasıdır. | İşletim sistemi ve uygulamalar kullanıcının kontrolündedir. | AWS EC2, Azure VM |
| **PaaS** | **Platform as a Service (Platform):** Geliştiriciler için kod yazıp test edebilecekleri hazır ortamlar sunar. Altyapı yönetimi (işletim sistemi, güncellemeler) bulut sağlayıcısına aittir. | Sadece uygulama ve veriler kullanıcının kontrolündedir. | Heroku, Google App Engine |
| **SaaS** | **Software as a Service (Yazılım):** Son kullanıcıya internet üzerinden doğrudan hizmet veren, kurulum gerektirmeyen tam işlevsel uygulamalardır. | Kullanıcı sadece yazılımı kullanır, altyapı veya kodla ilgilenmez. | Google Workspace, Microsoft 365, Salesforce |

---

## 3. Modern Altyapı Teknolojileri
Bulut mimarisinin gücünü tam olarak kullanabilmek için geleneksel (monolitik) yazılım geliştirme yöntemleri yerini modern teknolojilere bırakmıştır.



### Docker (Konteynerizasyon)
Uygulamaları ve çalışması için gereken tüm kütüphaneleri (bağımlılıkları) hafif ve taşınabilir **konteynerler** içine paketleyen platformdur.
* İşletim sistemi çekirdeğini paylaşırlar ancak birbirlerinden izoledirler.
* *"Benim bilgisayarımda çalışıyordu, sunucuda çalışmıyor"* problemini ortadan kaldırır.

### Kubernetes (K8s - Orkestrasyon)
Yüzlerce veya binlerce Docker konteynerinin otomatik olarak dağıtılmasını, ölçeklendirilmesini ve yönetilmesini sağlayan sistemdir.
* Uygulama trafiği arttığında otomatik olarak yeni konteynerler açar (Ölçeklendirme).
* Çöken bir konteyneri tespit edip yerine yenisini başlatır (Kendi kendine iyileşme).

### Mikroservisler (Microservices)
Devasa ve tek parça (monolitik) bir uygulamayı, her biri tek bir işi yapan küçük ve bağımsız hizmetlere bölme mimarisidir.
* Servisler birbirleriyle API'ler üzerinden haberleşir.
* Bir servisteki arıza tüm uygulamayı çökertmez.

---

## 4. DevOps ve CI/CD Süreçleri


**DevOps (Development & Operations):** Yazılım geliştiriciler (Dev) ile sistem yöneticileri (Ops) arasındaki duvarları yıkarak, yazılımın daha hızlı ve güvenilir bir şekilde üretilmesini sağlayan kültürdür.

### CI/CD (Sürekli Entegrasyon ve Sürekli Dağıtım)
Yazılımın kodlanmasından sunucuya yüklenmesine kadar geçen sürecin **otomatize** edilmesidir.

* **CI (Continuous Integration - Sürekli Entegrasyon):** Geliştiricilerin yazdığı kodların günde birkaç kez merkezi depoya aktarılması ve sistem tarafından **otomatik olarak test edilmesidir.** Hatayı anında bulmayı sağlar.
* **CD (Continuous Deployment - Sürekli Dağıtım):** Testlerden başarıyla geçen kodun, insan müdahalesi olmadan otomatik olarak canlı sunucuya (üretim ortamına) aktarılmasıdır. 