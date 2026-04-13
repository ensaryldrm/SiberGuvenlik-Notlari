# Gobuster: Hızlı Dizin ve İçerik Keşfi
## 1. Gobuster Nedir?
Gobuster, web sunucularında gizli dizinleri, dosyaları ve alt alan adlarını (subdomain) keşfetmek için kaba kuvvet (brute-force) ve sözlük saldırıları (dictionary attack) yöntemlerini kullanan popüler bir komut satırı aracıdır. 

* **Hızlı Performans:** Go (Golang) programlama diliyle yazıldığı için rakiplerine göre (örn: dirb) çok daha hızlı çalışır ve eşzamanlı (multi-thread) işlemleri mükemmel yönetir.
* **Çoklu Mod:** Sadece dizin değil; DNS, VHost (Sanal Sunucu) ve Amazon S3 / Google Cloud bucket'larını taramak için de farklı çalışma modlarına sahiptir.
* **Esneklik:** İş parçacığı sayısı (thread), zaman aşımı, özel HTTP başlıkları ve user-agent gibi birçok parametre kullanıcının isteğine göre özelleştirilebilir.

---

## 2. dir Modu ve Önemli Parametreler
Gobuster'ın en sık kullanılan modu, web dizinlerini ve dosyalarını tarayan `dir` modudur. Yardım menüsüne (`gobuster dir --help`) bakıldığında onlarca parametre görülür, ancak sızma testlerinde en çok kullanılan temel parametreler şunlardır:

| Parametre | Uzun Yazılışı | Açıklama |
| :--- | :--- | :--- |
| `-u` | `--url` | **(Zorunlu)** Taranacak hedef URL'i belirtir. (Örn: `http://hedef.com`) |
| `-w` | `--wordlist` | **(Zorunlu)** Tarama sırasında kullanılacak kelime listesinin dosya yolunu belirtir. |
| `-x` | `--extensions` | Aranacak dosya uzantılarını belirler. Virgülle ayrılarak birden fazla yazılabilir (Örn: `php,txt,html`). |
| `-t` | `--threads` | Eşzamanlı atılacak istek sayısını belirler (Varsayılan: 10). Hızı artırır ama sunucuyu yorabilir. |
| `-s` | `--status-codes` | Sadece belirli HTTP durum kodlarına sahip sonuçları ekrana basar (Örn: `200,301,302`). |
| `-v` | `--verbose` | Detaylı çıktı verir. Normalde gizlenen bazı bilgileri (yönlendirme adresleri vb.) gösterir. |

---

## 3. Kullanım Örnekleri

### A. Klasik Dizin Tarama
Sadece klasörleri ve uzantısız dizinleri bulmak için `-u` (hedef) ve `-w` (wordlist) parametreleri yeterlidir.
```bash
# SecLists içindeki directory-list-1.0.txt kullanılarak yapılan standart bir tarama
gobuster dir -u [http://172.20.8.56](http://172.20.8.56) -w /root/Desktop/misc/SecLists/Discovery/Web-Content/directory-list-1.0.txt
````

### B. Belirli Dosya Uzantılarını Tarama (Dosya/Sayfa Keşfi)

Web sunucusunun dilini biliyorsanız (Örn: PHP), dizinlerin yanı sıra doğrudan zafiyet barındırabilecek `.php` dosyalarını da aramak için `-x` parametresi kullanılır. `-v` (verbose) ile detaylı loglama açılır.

```Bash
# Hedefte .php uzantılı dosyaları arayan tarama komutu
gobuster dir -u [http://172.20.8.56](http://172.20.8.56) -w /root/Desktop/misc/SecLists/Discovery/Web-Content/common.txt -x php -v
```

_(Bu komut, wordlist'teki her kelimeyi hem normal dener (Örn: `/admin`) hem de sonuna uzantıyı ekleyerek dener (Örn: `/admin.php`).)_