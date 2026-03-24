# MSFConsole ve Temel Komutlar


MSFConsole, Metasploit Framework'ün tüm yeteneklerine (exploit, payload, auxiliary vb.) erişmemizi sağlayan komut satırı arayüzüdür (CLI). Tüm sızma testi süreci bu ekrandan yönetilir.

## 1. MSFConsole'u Başlatma
Terminalde arayüzü başlatmak için kullanılan temel komutlar:
* `msfconsole` : Standart başlatma komutudur (Ekrana rastgele, havalı bir ASCII banner çizer).
* `msfconsole -q` : **(Quiet - Sessiz Mod):** Banner çizmeden, doğrudan ve çok daha hızlı bir şekilde komut satırına düşmek için kullanılır.

## 2. Sızma Testi İş Akışı (Temel Komutlar)

Gerçek bir sızma testinde komutlar genellikle aşağıdaki sırayla kullanılır:

### A. Bulma ve Seçme (Search & Use)
Hedefteki zafiyete uygun modülü bulup içine girdiğimiz aşamadır.
* **`search [kelime]` :** Metasploit veritabanında modül (exploit/auxiliary) arar. (Örn: `search vsftpd` veya `search type:exploit smb`).
  * *-S : Sonuçları filtreler.*
  * *-s : Belirtilen sütuna göre sıralar.*
* **`use [modül_yolu veya numarası]` :** Arama sonucunda bulduğumuz modülü seçmek ve aktif hale getirmek için kullanılır. (Örn: `use exploit/unix/ftp/vsftpd_234_backdoor` veya listedeki sırasına göre `use 0`).
* **`back` :** Seçili olan modülün içinden çıkıp ana MSF menüsüne dönmeyi sağlar.

### B. Bilgi Alma ve Yapılandırma (Info, Options, Set)
Seçtiğimiz modülün (silahın) hedefe doğru ateşlenebilmesi için ayarlarının yapıldığı kritik aşamadır.
* **`info` :** Seçili modülün ne işe yaradığını, kimin yazdığını ve hangi zafiyeti sömürdüğünü anlatan detaylı bilgi sayfasını açar.
* **`options` (veya `show options`) :** Modülü çalıştırmak için hangi ayarların girilmesi gerektiğini listeler. **"Required" (Gerekli)** sütununda `yes` yazan her parametre (Örn: RHOSTS - Hedef IP) mutlaka doldurulmalıdır.
* **`set [Değişken] [Değer]` :** Ayarları (parametreleri) tanımlamak için kullanılır. (Örn: `set RHOSTS 192.168.1.10` veya `set RPORT 21`).
* **`get [Değişken]` :** Atadığınız bir ayarın o anki değerini görmek için kullanılır.
* **`unset [Değişken]` :** Yanlış girdiğiniz veya temizlemek istediğiniz bir ayarı sıfırlar.
* **`advanced` :** Modülün standart ayarları dışında kalan, ileri düzey ince ayarlarını (timeout süreleri, evasion teknikleri vb.) listeler.

### C. Görüntüleme ve Yönetim (Show, Sessions)
* **`show [kategori]` :** MSFConsole içindeki bileşenleri listelemek için kullanılır. (Örn: `show payloads` seçili exploite uygun zararlı kodları listeler, `show targets` ise hedef işletim sistemi seçeneklerini gösterir).
* **`sessions` :** Başarıyla hacklenmiş ve arka plana alınmış (background) aktif hedef bağlantılarını (Meterpreter veya Shell) listeler. Bir oturuma geri dönmek için `sessions -i [ID_Numarası]` kullanılır.
* **`history` :** O ana kadar terminalde yazdığınız komut geçmişini listeler.