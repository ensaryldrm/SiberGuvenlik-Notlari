# Burp Suite Target Modülü: Site Haritası ve Kapsam Yönetimi
## 1. Target Modülü Nedir?
Target sekmesi, Burp Suite'in üst araç çubuğunda yer alan ve hedeflenen web uygulamasının mimarisini, dizinlerini ve dosyalarını organize bir şekilde gösteren ana keşif (Reconnaissance) merkezidir. 

Güvenlik testlerinde hedefin sınırlarını belirlemek ve trafiği yönetmek için iki ana alt sekmeye ayrılır: **Site Map (Site Haritası)** ve **Scope (Kapsam)**.

---

## 2. Site Map (Site Haritası)
Uygulamada gezinirken (Proxy açıkken) veya otomatik tarama yaparken keşfedilen tüm URL'ler, klasörler ve dosyalar burada hiyerarşik bir **ağaç yapısı (tree view)** şeklinde listelenir.

**Site Map'in Sağladığı Temel İşlevler:**
* **Keşif ve Görünürlük:** Sitenin hangi dizinlere (`/admin`, `/api`, `/images`) sahip olduğunu görselleştirir. Gri renkteki klasörler sayfa içinde linki bulunan ama henüz ziyaret edilmemiş yerleri, siyah/koyu renkliler ise ziyaret edilmiş ve isteği yakalanmış yerleri gösterir.
* **Filtreleme:** Ekrandaki karmaşayı önlemek için sadece belirli uzantıları (örn: sadece `.php` veya `.js`) gösterebilir veya `.jpg`, `.css` gibi güvenlik testi açısından önemsiz dosyaları gizleyebilirsiniz.
* **Sağ Tık Menüsü (Context Menu):** Listeden herhangi bir hedefe sağ tıklandığında; o isteği *Intruder* veya *Repeater*'a gönderme, tarayıcıda açma veya URL'yi kopyalama gibi kritik eylemler gerçekleştirilir.

### İstek (Request) ve Yanıt (Response) Analizi
Site Map üzerinden bir adrese tıklandığında, alt veya yan panelde o adresle yapılan iletişimin ham hali görünür:
* **Request (İstek):** İstemcinin (Tarayıcının) sunucuya gönderdiği veridir (Örn: `GET /login HTTP/1.1`). İçerisinde çerezler, User-Agent ve gönderilen parametreler bulunur.
* **Response (Yanıt):** Sunucunun istemciye verdiği cevaptır (Örn: `HTTP/1.1 200 OK`). İçerisinde HTML kaynak kodu, set-cookie bilgileri ve sunucu başlıkları yer alır.

---

## 3. Scope (Kapsam) Ayarları
Siber güvenlik testlerinde "Scope" yani kapsam, **yasal olarak test etme izniniz olan hedeflerin sınırıdır.**

* **Neden Önemlidir?** İnternette gezinirken tarayıcınız arka planda yüzlerce farklı siteye (Google Analytics, reklam ağları, eklenti sunucuları) istek atar. Scope ayarlanmazsa Burp Suite hepsini kaydeder ve devasa bir karmaşa oluşur. Daha kötüsü, izniniz olmayan bir sisteme yanlışlıkla saldırı (Örn: otomatik tarama) yapabilirsiniz.
* **Nasıl Ayarlanır?** Site Map üzerinden hedef alan adına (`example.com`) sağ tıklayıp **"Add to scope"** denir. 
* **Gelişmiş Filtreleme:** Kapsam eklendikten sonra Site Map filtresinden *“Show only in-scope items” (Sadece kapsam içindekileri göster)* seçilerek, heves kaçıran tüm gereksiz trafik (Google, YouTube, eklenti trafikleri vb.) ekrandan gizlenir.

---

## 4. Issue Definitions (Sorun Tanımları)
Burp Suite'in içinde gömülü olarak gelen bir "Zafiyet Ansiklopedisi"dir.
Burada SQL Injection'dan XSS'e, SSRF'den CSRF'e kadar yüzlerce güvenlik zafiyetinin ne anlama geldiği, nasıl çalıştığı, ne gibi riskler barındırdığı ve nasıl çözülmesi gerektiğine dair referans niteliğinde detaylı teknik belgeler bulunur.