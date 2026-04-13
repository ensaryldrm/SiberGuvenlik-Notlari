# XSS Zafiyeti Tarama ve İstismar Araçları

XSS zafiyetlerini manuel olarak tespit etmek, özellikle büyük web uygulamalarında ve Web Uygulama Güvenlik Duvarlarının (WAF) arkasında oldukça zaman alıcıdır. Bu süreci otomatize etmek, hızlıca tarama yapmak ve bulunan zafiyeti sömürmek (exploit) için özel araçlar kullanılır.

## 1. XSStrike (Gelişmiş Tarama ve Bypass)
XSStrike, Python ile geliştirilmiş piyasadaki en yetenekli ve akıllı XSS tarama araçlarından biridir. Basitçe payload denemek yerine, hedefin filtreleme mekanizmasını analiz eder ve engelleri aşmak (Bypass) için **kendi payload'larını özel olarak üretir.** Ayrıca DOM tabanlı XSS tespiti konusunda çok başarılıdır.

* **GitHub:** [https://github.com/s0md3v/XSStrike](https://github.com/s0md3v/XSStrike)
* **Kurulum:**
```bash
  git clone [https://github.com/s0md3v/XSStrike.git](https://github.com/s0md3v/XSStrike.git)
  cd XSStrike
  pip3 install -r requirements.txt
```

- **Temel Kullanım:** Belirtilen URL'deki parametreleri analiz edip zafiyet taraması başlatır.

```bash
python3 xsstrike.py -u "[http://example.com/page?param=test](http://example.com/page?param=test)"
```

---

## 2. XSSCon (Basit ve Hızlı Tarayıcı)

XSSCon, daha hafif ve doğrudan sonuca odaklanan bir komut satırı aracıdır. Derinlemesine analiz yerine, elindeki listelerle belirli bir URL'deki girdi alanlarını (input) hızlıca tarayarak potansiyel riskleri raporlar.

- **GitHub:** [https://github.com/menkrep1337/XSSCon](https://github.com/menkrep1337/XSSCon)
    
- **Kurulum:**

```bash
git clone [https://github.com/menkrep1337/XSSCon.git](https://github.com/menkrep1337/XSSCon.git)
cd XSSCon
chmod 755 -R XSSCon
pip install bs4 requests
```

- **Temel Kullanım:**

```bash
python3 xsscon.py -u "[http://example.com](http://example.com)"
```

---

## 3. BeEF (Browser Exploitation Framework) - İstismar Aracı

BeEF bir zafiyet _tarama_ aracı değildir; zafiyet bulunduktan sonra kullanılan bir **İstismar ve Komuta Kontrol (C2)** platformudur. Eğer hedefte bir XSS zafiyeti (özellikle Stored XSS) bulursanız, BeEF'in ürettiği özel JavaScript kodunu (`hook.js`) o sayfaya enjekte edersiniz.

Bu zararlı kodu çalıştıran her kurbanın tarayıcısı bir **"Zombi (Hooked Browser)"** haline gelir. Artık BeEF kontrol paneli üzerinden kurbanın tarayıcısında işlemler yapabilir, kamerasını açmayı deneyebilir, sahte giriş ekranları gösterebilir veya ağındaki diğer cihazlara saldırabilirsiniz.

- **GitHub:** [https://github.com/beefproject/beef](https://github.com/beefproject/beef)
    
- **Kurulum (Kali Linux gibi sistemlerde):**
- 
```bash
git clone [https://github.com/beefproject/beef.git](https://github.com/beefproject/beef.git)
cd beef
./install
```
- **Kullanım ve Erişim:** BeEF servisi başlatıldıktan sonra tarayıcıdan yönetim arayüzüne gidilir.
    
    - **Yönetim Paneli:** `http://localhost:3000/ui/panel`
        
    - **Varsayılan Kimlik Bilgileri:** Kullanıcı Adı: `beef` / Parola: `beef` (Kurulumda değiştirilmesi istenir).