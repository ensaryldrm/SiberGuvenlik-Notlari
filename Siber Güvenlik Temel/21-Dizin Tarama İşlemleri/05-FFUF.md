# FFUF (Fuzz Faster U Fool): Hızlı Fuzzing ve Keşif

FFUF, web uygulamalarında sızma testi yaparken kullanılan, Go dili ile geliştirilmiş inanılmaz hızlı ve esnek bir fuzzing aracıdır. Sadece dizinleri değil; parametreleri, HTTP başlıklarını (Header), POST verilerini ve hatta alt alan adlarını (Subdomain) taramak için de mükemmel bir seçenektir.

## 1. Neden FFUF? (Temel Özellikler)
* **Hız:** Go dilinin gücünü kullanarak saniyede binlerce istek atabilir.
* **FUZZ Anahtar Kelimesi:** Diğer araçlardan en büyük farkı, wordlist'teki kelimelerin **nereye** yerleştirileceğini `FUZZ` kelimesiyle sizin belirlemenizdir. Bu sayede URL'in ortasını, sonunu veya bir parametreyi kolayca manipüle edebilirsiniz.
* **Filtreleme ve Eşleştirme (Matcher/Filter):** Sadece `200 OK` dönenleri göster (`-mc 200`), boyutu 42 byte olanları gizle (`-fs 42`) gibi çok gelişmiş çıktı filtreleme seçeneklerine sahiptir.

---

## 2. En Sık Kullanılan Parametreler

| Parametre | Açıklama |
| :--- | :--- |
| `-u` | **(Zorunlu)** Hedef URL. İçerisinde mutlaka `FUZZ` kelimesi geçmelidir. |
| `-w` | **(Zorunlu)** Kullanılacak kelime listesinin (wordlist) yolunu belirtir. |
| `-v` | Verbose modu. Çıktıda yönlendirme (redirect) adreslerini ve tam URL'leri gösterir. |
| `-mc` | (Match Code) Sadece belirtilen HTTP durum kodlarını gösterir (Örn: `-mc 200,301`). |
| `-fc` | (Filter Code) Belirtilen HTTP durum kodlarını gizler (Örn: `-fc 404`). |
| `-fs` | (Filter Size) Sitenin varsayılan hata sayfasının boyutu biliniyorsa, o boyuttaki yanıtları gizler. (Örn: `-fs 1542`). |
| `-H` | İsteğe özel HTTP başlığı (Header) ekler. (Örn: `-H "Cookie: session=123"`) |

---

## 3. Kullanım Senaryoları ve Örnekler

### A. Klasik Dizin Tarama
Hedefteki klasörleri bulmak için `FUZZ` kelimesi URL'in sonuna eklenir.
```bash
ffuf -u [http://172.20.3.144/FUZZ](http://172.20.3.144/FUZZ) -w /root/Desktop/misc/SecLists/Discovery/Web-Content/directory-list-1.0.txt
````

_(Wordlist'teki "admin" kelimesi, `http://172.20.3.144/admin` olarak denenir)._

### B. Dosya Uzantısı Tahmin Etme (Extension Fuzzing)

Sitenin hangi teknolojiyi (PHP, ASPX, HTML) kullandığını bilmiyorsak, bilinen bir dosya adı üzerinden (Örn: `index`) uzantı listesi ile tarama yapabiliriz.

```Bash
# SecLists içindeki web-extensions.txt kullanılarak uzantı taraması
ffuf -u [http://172.20.3.144/indexFUZZ](http://172.20.3.144/indexFUZZ) -w /root/Desktop/misc/SecLists/Discovery/Web-Content/web-extensions.txt
```

_(Wordlist'teki ".php" uzantısı, `http://172.20.3.144/index.php` olarak denenir)._

### C. Belirli Uzantıya Sahip Dosyaları Tarama

Eğer sistemin `.html` sayfalarından oluştuğunu anladıysak, sayfaları bulmak için `FUZZ` kelimesinin sonuna statik olarak `.html` ekleriz.

```Bash
ffuf -u [http://172.20.3.144/FUZZ.html](http://172.20.3.144/FUZZ.html) -w /root/Desktop/misc/SecLists/Discovery/Web-Content/common.txt -v
```

_(Wordlist'teki "contact" kelimesi, `http://172.20.3.144/contact.html` olarak denenir)._