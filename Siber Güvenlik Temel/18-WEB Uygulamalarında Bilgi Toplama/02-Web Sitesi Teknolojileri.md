# Web Sitesi Teknolojilerinin Tespiti 
Siber güvenlikte bir web sitesinin arkasında çalışan teknolojileri (Sunucu yazılımı, Framework, Veritabanı, CMS) tespit etmek, o sisteme ait bilinen güvenlik açıklarını (CVE) arayabilmek için atılması gereken ilk adımdır.

## 1. Kullanılan Temel Araçlar ve Yöntemler
Teknoloji tespiti genellikle üç farklı yaklaşımla yapılır:

* **Çevrimiçi Araçlar (Web Tabanlı):** Hedef siteyi tarayarak teknoloji profilini çıkaran platformlardır. (Örn: *BuiltWith*)
* **Tarayıcı Eklentileri:** Ziyaret edilen web sitesinin teknolojilerini anında tarayıcı çubuğunda gösteren, en pratik bilgi toplama araçlarıdır. (Örn: *Wappalyzer, WhatRuns*)
* **Komut Satırı Araçları (CLI):** HTTP başlıklarını (Headers) manuel olarak çekip incelemek için kullanılan araçlardır. (Örn: *curl, wget*)

---

## 2. HTTP Başlıkları (Headers) ile Bilgi Edinme
Hedef sunucuya sadece başlıkları getirmesi için bir `HEAD` isteği gönderilerek sunucu yazılımı ve versiyonları tespit edilebilir.

**Örnek Komut ve Çıktı:**
```bash
curl --head [https://wordpress.org](https://wordpress.org)
````

```Plaintext
HTTP/2 200 
server: nginx
date: Thu, 28 Mar 2024 10:44:38 GMT
content-type: text/html; charset=UTF-8
...
```

- **Analiz:** Çıktıdaki `server: nginx` satırı, sitenin arka planda **Nginx** web sunucusu üzerinde koştuğunu net bir şekilde ele verir. Bazen bu satırda `Apache/2.4.41 (Ubuntu)` gibi işletim sistemini ve tam versiyonu açığa çıkaran kritik bilgiler de bulunabilir.
    

---

## 3. İleri Düzey Tespit (Manuel Fingerprinting)

Otomatik araçların çalışmadığı veya WAF arkasında gizlenen sistemlerde, manuel olarak bırakılan "İşaretçiler" (Indicators) aranır.

### A. Çerezler (Cookies) Üzerinden Tespit

Geliştiriciler, framework'lerin varsayılan oturum (session) çerez isimlerini değiştirmeyi genellikle unuturlar. Tarayıcıda oluşan çerez isimleri teknolojiyi ele verir:

|Kullanılan Teknoloji / Framework|Çerez Adı (Cookie Name)|
|---|---|
|**Laravel (PHP)**|`laravel_session`|
|**WordPress**|`wp-settings-1`|
|**phpBB**|`phpbb3_`|
|**CakePHP**|`cakephp`|
|**Django CMS**|`django`|

E-Tablolar'a aktar

### B. HTML Kaynak Kodu Üzerinden Tespit (Meta Etiketleri)

Sayfanın kaynak kodunda (`CTRL+U`) yer alan `<meta>` etiketleri veya özel yorum satırları, kullanılan İçerik Yönetim Sistemini (CMS) doğrudan söyler.

|CMS / Teknoloji|HTML Kaynak Kodundaki İşaretçi|
|---|---|
|**WordPress**|`<meta name="generator" content="WordPress 3.9.2" />`|
|**Joomla**|`<meta name="generator" content="Joomla! - Open Source Content Management" />`|
|**Drupal**|`<meta name="Generator" content="Drupal 7 (http://drupal.org)" />`|
|**phpBB**|`<body id="phpbb"`|
