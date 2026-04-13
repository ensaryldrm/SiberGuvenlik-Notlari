# Feroxbuster: Hızlı ve Yinelemeli İçerik Keşfi

Feroxbuster, web uygulamalarında gizli kalan veya unutulmuş dizinleri ve dosyaları keşfetmek için tasarlanmış, komut satırı tabanlı yeni nesil bir araçtır. Güvenlik profesyonelleri ve sızma testçileri tarafından kaba kuvvet (brute-force) ve sözlük saldırıları (wordlist attacks) yöntemleriyle web sunucularını taramak için kullanılır.

## 1. Neden Feroxbuster? (Temel Özellikler)
* **Yüksek Performans:** Rust programlama dilinde yazılmış olması, onu rakiplerine göre (örn: Dirb veya Gobuster) çok daha hızlı, bellek dostu ve verimli kılar.
* **Yinelemeli (Recursive) Tarama:** Bulduğu bir gizli dizinin (Örn: `/admin`) içine girerek, o dizinin içinde de otomatik olarak yeni bir tarama başlatabilir. Bu, manuel iş yükünü inanılmaz derecede azaltır.
* **Esneklik ve Çok Yönlülük:** İstek başına iş parçacığı (thread) sayısı, tarama derinliği (depth), zaman aşımı süreleri ve filtreleme ayarları son derece detaylı bir şekilde özelleştirilebilir.

---

## 2. En Sık Kullanılan Parametreler
Feroxbuster çok geniş bir yardım menüsüne (`feroxbuster --help`) sahiptir. Sızma testlerinde en çok ihtiyaç duyulan temel parametreler şunlardır:

| Parametre | Uzun Yazılışı | Açıklama |
| :--- | :--- | :--- |
| `-u` | `--url` | **(Zorunlu)** Taranacak hedef URL'i belirtir. (Örn: `http://hedef.com`) |
| `-w` | `--wordlist` | **(Zorunlu)** Kullanılacak kelime listesinin (wordlist) yolunu belirtir. |
| `-x` | `--extensions` | Aranacak dosya uzantılarını belirler (Örn: `-x pdf -x php,txt`). |
| `-t` | `--threads` | Eşzamanlı atılacak istek sayısını belirler (Varsayılan: 50). |
| `-d` | `--depth` | Yinelemeli (recursive) taramanın maksimum derinliğini belirler (Varsayılan: 4). `0` sonsuz döngü anlamına gelir. |
| `-n` | `--no-recursion`| Yinelemeli taramayı kapatır (Bulduğu klasörlerin içine girmez). |
| `--burp` | - | Tüm trafiği anında Burp Suite üzerinden geçirir (`http://127.0.0.1:8080`). Hata ayıklama için mükemmeldir. |

---

## 3. Kullanım Senaryoları ve Örnekler

### A. Temel Dizin Tarama
Hedef sistem üzerinde, standart bir wordlist (`directory-list-1.0.txt`) kullanarak sadece dizinleri (klasörleri) tarayan en temel komuttur.
```bash
feroxbuster -u [http://172.20.8.56](http://172.20.8.56) -w /root/Desktop/misc/SecLists/Discovery/Web-Content/directory-list-1.0.txt
````

### B. Belirli Dosya Uzantılarını Tarama (Dosya Keşfi)

Eğer hedefte PDF raporları, yedek dosyaları veya PHP betikleri aranıyorsa `-x` parametresi ile uzantılar belirtilir. Aşağıdaki örnek, `common.txt` listesindeki kelimelerin sonuna `.pdf` ekleyerek tarama yapar.

```Bash
feroxbuster -u [http://172.20.8.56](http://172.20.8.56) -w /root/Desktop/misc/SecLists/Discovery/Web-Content/common.txt -x pdf
```

_Feroxbuster'ın örnek terminal çıktısı (Banner ve Bulunanlar):_

```Plaintext
 ___  ___  __   __     __      __         __   ___
|__  |__  |__) |__) | /  `    /  \ \_/ | |  \ |__
|    |___ |  \ |  \ | \__,    \__/ / \ | |__/ |___
by Ben "epi" Risher 🤓                 ver: 2.10.2
───────────────────────────┬──────────────────────
 🎯  Target Url            │ [https://172.20.8.56/](https://172.20.8.56/)
 🚀  Threads               │ 50
 📖  Wordlist              │ /root/Desktop/misc/SecLists/Discovery/Web-Content/common.txt
 💲  Extensions            │ [pdf]
 🔃  Recursion Depth       │ 4
───────────────────────────┴──────────────────────
308      GET        1l        1w       15c [https://172.20.8.56/.git/index](https://172.20.8.56/.git/index) => [https://172.20.8.56/.git](https://172.20.8.56/.git)
200      GET        1l        1w       24c [https://172.20.8.56/.well-known/http-opportunistic](https://172.20.8.56/.well-known/http-opportunistic)
```