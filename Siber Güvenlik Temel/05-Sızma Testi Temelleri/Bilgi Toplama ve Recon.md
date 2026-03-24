# Bilgi Toplama (Content Discovery & OSINT)

Saldırının %80'i bilgi toplamaktır. Sistemin haritasını çıkarmadan körü körüne saldırılmaz.

## Web Geliştirici Araçları (DevTools - F12)
* **View Source:** Sayfanın HTML kaynak kodu (Gizli yorum satırları, eski linkler aranır).
* **Inspector:** DOM yapısını ve anlık CSS/HTML kodlarını manipüle etmek için.
* **Debugger:** JavaScript kodlarını adım adım çalıştırmak ve mantık hatalarını (Client-side) bulmak için.
* **Network Tab:** Sitenin arka planda API ile nasıl konuştuğunu (AJAX istekleri) görmek için.

## Keşif (Content Discovery)
**Manuel Keşif:**
* `robots.txt`: Arama motorlarına "şuralara girme" denen dosya (Hackerların ilk baktığı yerdir, genelde admin panelleri burada saklanır).
* `sitemap.xml`: Sitenin tüm sayfalarının haritası.
* `Favicon`: İkon dosyasının hash değerinden sitenin hangi altyapıyı kullandığı bulunur.
* `HTML Headers`: Sunucunun verdiği yanıt başlıkları (Server: Apache 2.4, X-Powered-By: PHP gibi versiyon ifşaları).

**[[OSINT]] (Açık Kaynak İstihbaratı):**
* *Google Dorking:* Google'ı hack aracı gibi kullanmak (Örn: `site:hedef.com ext:pdf` veya `intitle:"index of"`).
* *Wappalyzer:* Sitenin kullandığı teknolojileri (Framework Stack) saniyeler içinde gösteren eklenti.
* *Wayback Machine:* Sitenin yıllar önceki hallerine bakıp unutulmuş/kaldırılmış sayfaları bulmak.
* *GitHub & S3 Buckets:* Yanlışlıkla sızdırılmış `.env` şifreleri, API keyler ve açık bulut depolama alanları.

**Otomatik Keşif (Automated Discovery):**
* Araçlar: `ffuf`, `dirb`, `gobuster`.
* Mantık: Hazır kelime listeleri (Wordlists) kullanılarak saniyede binlerce istek atılır ve gizli dizinler (örn: `/admin`, `/backup.zip`) bulunur.

## Subdomain (Alt Alan Adı) Keşfi
* **SSL/TLS Sertifikaları:** `crt.sh` gibi sitelerden şeffaflık logları aranarak gizli subdomainler bulunur.
* **Arama Motorları (OSINT):** `site:*.hedef.com -www`
* **DNS Bruteforce:** `gobuster vhost` veya `dnsenum` ile tahmin yürütme.
* **Araçlar:** `Sublist3r` (Otomatize OSINT aracı).
* **Virtual Hosts (VHosts):** Aynı IP'de barınan ama DNS'e kaydedilmemiş gizli geliştirici siteleri.