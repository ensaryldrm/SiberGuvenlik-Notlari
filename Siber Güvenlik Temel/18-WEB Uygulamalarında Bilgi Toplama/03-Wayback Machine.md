# İnternet Arşivi (Wayback Machine) ile Pasif Bilgi Toplama


Siber güvenlikte pasif bilgi toplama (OSINT) sürecinin en değerli araçlarından biri İnternet Arşivi'dir (Wayback Machine). 1996 yılından bu yana web sayfalarının anlık görüntülerini (snapshot) alarak dijital bir zaman kapsülü görevi görür.

* **Bağlantı:** [https://web.archive.org/](https://web.archive.org/)

## 1. Wayback Machine Nedir ve Nasıl Çalışır?
Web sitelerinin zaman içindeki değişimlerini, eski arayüzlerini ve silinmiş içeriklerini kayıt altına alan bir servistir. Hedef alan adını arama çubuğuna yazdığınızda, karşınıza yıllara ve aylara bölünmüş bir takvim çıkar. Takvimdeki işaretli tarihlere tıklayarak sitenin o günkü birebir kopyasına erişebilirsiniz.

## 2. Siber Güvenlik (OSINT) Açısından Kullanım Alanları
Sıradan bir kullanıcı için eski günleri yad etme aracı olan bu platform, siber güvenlik uzmanları için bir istihbarat madenidir:

* **Unutulan/Silinen Zafiyetlerin Keşfi (Kayıp İçerik):** Hedef kurum, geçmişte web sitesine yanlışlıkla hassas bir belge (örneğin içi şifre dolu bir PDF) veya test amaçlı bir geliştirici dizini (Örn: `/test`, `/dev`) yükleyip sonra silmiş olabilir. Wayback Machine bu silinmiş sayfaların kopyalarını saklamaya devam eder.
* **Güvenlik Analizi:** Zararlı yazılım (malware) barındıran veya oltalama (phishing) amacıyla kullanılmış sitelerin geçmişteki hallerini, o dönemde hangi IP'lerde veya temalarda çalıştığını analiz etmek için kullanılır.
* **Hedefin Teknolojik Evrimi:** Sitenin eski HTML kaynak kodlarına bakılarak, kurumun geçmişte hangi teknolojileri kullandığı ve altyapısını ne yönde güncellediği haritalandırılabilir.
* **Araştırma ve Doğrulama:** Geçmişte yayınlanmış ancak sonradan değiştirilmiş makaleler, çalışan listeleri (sosyal mühendislik için hedefler) veya duyurular hakkında değişmez kanıtlar sunar.

---

### İpucu: Otomatize Araçlar
Gerçek bir sızma testinde Wayback Machine üzerinde manuel olarak takvimde gezinmek yerine, hedef sitenin arşivlenmiş tüm URL'lerini otomatik olarak çeken komut satırı araçları (Örneğin: `waybackurls`) kullanılır. Bu sayede hedefin yıllar boyunca sahip olduğu tüm gizli yollar (endpoints) saniyeler içinde listelenebilir.