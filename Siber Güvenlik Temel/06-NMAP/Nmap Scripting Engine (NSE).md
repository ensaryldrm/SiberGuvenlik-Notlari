# Nmap Scripting Engine (NSE)


Nmap'in yeteneklerini ağ taramasının ötesine taşıyarak; otomasyon, zafiyet tespiti ve ileri düzey bilgi toplama yapmasını sağlayan eklenti motorudur. Scriptler **Lua** programlama dili ile yazılır. 

## 1. Temel NSE Kullanımı

* **Varsayılan Scriptler (-sC):** Nmap'in en popüler ve "güvenli" (sistemi çökertmeyecek) varsayılan script setini çalıştırır. (Versiyon tespiti `-sV` ile birlikte kullanılması altın kuraldır).

```bash
  nmap -sC hedef_ip
```

- **Özel Script veya Kategori Belirleme (--script):** Belirli bir amaca yönelik (örneğin sadece zafiyet aramak) scriptleri çalıştırmak için kullanılır.
    
    

```Bash
   nmap --script=kategori_adi hedef_ip
```

## 2. CTF ve Sızma Testlerinde En Çok Kullanılan Kategoriler

Yüzlerce script 14 ana kategoriye ayrılmıştır. Laboratuvar ortamlarında en çok işinize yarayacak olanlar şunlardır:

- **vuln:** Sistemde bilinen bir güvenlik açığı (CVE, zafiyet) olup olmadığını kontrol eder. Bir makineyi hacklemeye çalışırken ilk çalıştırılan kategorilerden biridir. _(Örn: `nmap --script=vuln hedef_ip`)_
    
- **exploit:** Sadece zafiyetin varlığını kontrol etmekle kalmaz, doğrudan sömürmeye (hacklemeye) çalışır.
    
- **brute:** FTP, SSH, HTTP, veritabanı gibi servislere kaba kuvvet (brute-force) saldırısı yaparak parolaları kırmaya çalışır.
    
- **auth:** Kimlik doğrulama mekanizmalarını test eder (Örneğin FTP servisinde şifresiz "Anonymous" girişinin açık olup olmadığını `ftp-anon` scripti ile bulur).
    
- **discovery:** Standart taramaların ötesine geçer. SMB (Windows dosya paylaşımı) üzerindeki klasörleri listelemek veya web sunucusunun dizinlerini/başlıklarını (HTML Title) çekmek için kullanılır.
    
- **safe:** Sistemi çökertme (DoS) riski olmayan, sadece pasif bilgi toplayan güvenli scriptlerdir.
    
- **intrusive:** Sistemi yoran, çökertme riski taşıyan ve IDS/IPS sistemleri tarafından anında fark edilen son derece gürültülü saldırgan betiklerdir.
    

## 3. Pratik Senaryolar (Cheat Sheet)

Sadece belirli bir scripti çalıştırmak isterseniz adını doğrudan yazabilirsiniz:

- **Sadece SMB Zafiyetlerini (Örn: EternalBlue) Aramak:**
    
    Bash
    
    ```
    nmap --script smb-vuln* -p 139,445 hedef_ip
    ```
    
- **Web Sunucusundaki Dizinleri Taramak:**
    
    Bash
    
```    
  nmap --script http-enum -p 80 hedef_ip
```
    
- **Scriptlere Dışarıdan Argüman (Parametre) Vermek:** (Örneğin brute-force yaparken kendi Wordlist'imizi vermek)
    
    
```Bash
nmap --script http-brute --script-args userdb=users.txt,passdb=passwords.txt hedef_ip
```
 
 