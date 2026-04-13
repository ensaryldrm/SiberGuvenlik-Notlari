# Dirb: Klasik ve Etkili Dizin Keşfi

Dirb, web sunucularında gizli veya unutulmuş dosya ve dizinleri keşfetmek için tasarlanmış, siber güvenlik dünyasının en köklü ve popüler araçlarından biridir. C diliyle yazılmış olan Dirb, Kali Linux ve HackerBox gibi sızma testi dağıtımlarında yüklü olarak gelir.

## 1. Neden Dirb? (Temel Özellikler)
* **Kendi Wordlist'ine Sahiptir:** Dirb'ün en büyük avantajı, dışarıdan bir kelime listesi (wordlist) belirtmeseniz bile kendi içindeki varsayılan listeyle (`/usr/share/dirb/wordlists/common.txt`) hemen taramaya başlayabilmesidir.
* **Otomatik Rekürsif (İç İçe) Tarama:** Dirb, tarama sırasında yeni bir dizin (Örn: `/filemanager/`) bulduğunda, ana taramayı duraklatıp otomatik olarak o dizinin içine girer ve orada da tarama yapar.
* **Çok Amaçlı Kullanım:** Hem statik dosyaları (HTML, PDF) hem de dinamik içerikleri (PHP, CGI betikleri) tespit etmek için özel olarak yapılandırılabilir.

---

## 2. En Sık Kullanılan Parametreler
Dirb'ün yardım menüsüne (`dirb`) bakıldığında birçok ayar görülür. Ancak günlük sızma testlerinde en çok şu parametreler kullanılır:

| Parametre | Açıklama |
| :--- | :--- |
| `url_base` | **(Zorunlu)** Taranacak temel URL'i belirtir. (Örn: `http://hedef.com/`) |
| `wordlist_file` | İsteğe bağlıdır. Belirtilmezse varsayılan olarak `common.txt` kullanılır. |
| `-X` | Sadece belirli bir dosya uzantısını aramak için kullanılır (Örn: `-X .html`). |
| `-r` | Dirb'ün o meşhur rekürsif (iç içe) tarama özelliğini kapatır. Sadece ana dizini tarar. |
| `-a` | HTTP isteklerinde kullanılacak User-Agent (Tarayıcı Kimliği) bilgisini değiştirir. |

---

## 3. Kullanım Senaryoları ve Örnekler

### A. Temel Dizin Tarama (Varsayılan Wordlist ile)
Hiçbir liste belirtilmediğinde Dirb, 4612 kelimelik kendi listesiyle hızlı bir tarama başlatır ve bulduğu klasörlerin içine otomatik olarak girer (`---- Entering directory... ----`).
```bash
dirb [http://172.20.8.56/](http://172.20.8.56/)
````

_Örnek Çıktı:_

```Plaintext
---- Scanning URL: [http://172.20.8.56/](http://172.20.8.56/) ----
==> DIRECTORY: [http://172.20.8.56/filemanager/](http://172.20.8.56/filemanager/)                                                              
+ [http://172.20.8.56/index.html](http://172.20.8.56/index.html) (CODE:200|SIZE:10701)                                                       
                                                                                                            
---- Entering directory: [http://172.20.8.56/filemanager/](http://172.20.8.56/filemanager/) ----
+ [http://172.20.8.56/filemanager/index.php](http://172.20.8.56/filemanager/index.php) (CODE:200|SIZE:11558) 
```

### B. Belirli Dosya Uzantılarını Tarama

Web sunucusunda sadece belirli bir formattaki dosyaları (Örneğin `.html` sayfaları) aramak istiyorsak `-X` parametresi kullanılır. (Dikkat: Gobuster'da `-x html` yazılırken, Dirb'de noktasıyla beraber `-X .html` yazılır).

```Bash
dirb [http://172.20.8.56/](http://172.20.8.56/) -X .html
```

_Örnek Çıktı:_

```plaintext
START_TIME: Fri Mar 22 14:58:28 2024
EXTENSIONS_LIST: (.html) | (.html) [NUM = 1]
---- Scanning URL: [http://172.20.8.56/](http://172.20.8.56/) ----
+ [http://172.20.8.56/index.html](http://172.20.8.56/index.html) (CODE:200|SIZE:10701)  
```