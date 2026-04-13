# Gizli Dosya ve Dizin Keşfi 
Web uygulamalarında hedef sistemin haritasını çıkarmak sadece ana sayfadan ibaret değildir. Sistem yöneticileri genellikle yönetim panellerini (`/admin`), geliştirici klasörlerini (`/dev`), eski sürüm dosyalarını (`/old`) veya veri tabanı yedeklerini (`backup.zip`) URL'de gizleyerek güvende olduklarını sanırlar. 

Bu gizli dizinleri ve dosyaları bulmak (fuzzing/brute-force) için en sık kullanılan araçlardan biri **Gobuster**'dır.

## 1. Gobuster - `dir` Modu (Dizin Tarama)
Belirli bir URL üzerinde, elinizdeki bir kelime listesini (wordlist) sırayla deneyerek hangi klasörlerin sunucuda mevcut (HTTP 200/301 vb.) olduğunu tespit eder.

* **Temel Sözdizimi (Syntax):**
```bash
  gobuster dir -u [http://hedefsite.com](http://hedefsite.com) -w /path/to/wordlist.txt
```

- **Örnek Kullanım (Klasör Arama):** Aşağıdaki komut, `172.20.8.56` IP adresindeki sunucuda yaygın kullanılan klasör isimlerini arar:

```Bash
gobuster dir -u [http://172.20.8.56](http://172.20.8.56) -w /root/Desktop/misc/SecLists/Discovery/Web-Content/directory-list-1.0.txt
```
    Siber Güvenlik İpucu:_ Bulunan bir `/api` veya `/uploads` dizini, saldırı yüzeyini bir anda inanılmaz ölçüde genişletebilir.
    

---

## 2. Belirli Dosya Uzantılarını Tarama (File/Page Scanning)

Klasörlerin yanı sıra, sunucuda unutulmuş spesifik dosyaları (Örneğin: PHP dosyaları, log metinleri, konfigürasyon dosyaları) bulmak için `--extensions` (veya kısaca `-x`) parametresi kullanılır.

- **Sözdizimi (Syntax):**
    
    Bash
    
    ```
    gobuster dir -u [http://hedefsite.com](http://hedefsite.com) -w /path/to/wordlist.txt -x php,txt,bak
    ```
    
- **Örnek Kullanım (.php Dosyalarını Arama):** Aşağıdaki komut, sunucudaki sadece `.php` uzantılı sayfaları arar ve `-v` (Verbose) parametresi sayesinde detaylı log çıktısı verir:

```Bash
    gobuster dir -u [http://172.20.8.56](http://172.20.8.56) -w /root/Desktop/misc/SecLists/Discovery/Web-Content/common.txt --extensions php -v
```
    
    _Siber Güvenlik İpucu:_ `.bak`, `.old`, `.zip`, `.sql` uzantılı aramalar yapmak, unutulmuş yedek dosyalarını bulmak için altın değerindedir.
    

---

## Kritik Gobuster Parametreleri Özeti

- `dir`: Dizin ve dosya tarama modunu başlatır.
    
- `-u` (url): Hedef web sitesini veya IP adresini belirtir.
    
- `-w` (wordlist): Kullanılacak kelime listesinin dosya yolunu belirtir (SecLists klasörü bu iş için biçilmiş kaftandır).
    
- `--extensions` veya `-x`: Aranacak dosya uzantılarını virgülle ayırarak eklemenizi sağlar (Örn: `php,html,txt`).
    
- `-v` (verbose): İşlem sırasında ne olup bittiğini detaylıca ekrana basar.