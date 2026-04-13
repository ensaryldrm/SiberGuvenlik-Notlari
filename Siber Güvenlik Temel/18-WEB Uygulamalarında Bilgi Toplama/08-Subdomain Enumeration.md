# Alt Alan Adı Keşfi 
Siber güvenlikte bir kurumun ana web sitesi (örn: `example.com`) genellikle çok sıkı korunur. Ancak aynı kurumun unutulmuş, test aşamasında bırakılmış veya zayıf yapılandırılmış alt alan adları (örn: `dev.example.com` veya `old-api.example.com`) saldırganlar için içeri sızmak adına harika kapılardır. 

Alt alan adı haritasını çıkarmak (Enumeration) saldırı yüzeyini genişletmek için kritik bir adımdır. Bu işlem için en güçlü ve popüler araçlardan biri **Gobuster**'dır.

## 1. Gobuster - `dns` Modu (Klasik Subdomain Taraması)
Bu mod, kaba kuvvet (Brute-force) mantığıyla çalışır. Elinizdeki bir kelime listesini (Wordlist) hedef domainin başına ekleyerek DNS sorguları yapar ve hangi adreslerin gerçekte var olduğunu (çözümlendiğini) bulur.

* **Sözdizimi (Syntax):**
```bash
  gobuster dns -d hedefsite.com -w /path/to/wordlist.txt
```

- **Örnek Kullanım ve Çıktı Analizi:**
```Bash
gobuster dns -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt -d facebook.com
```
    
    _Çıktı:_ Gobuster listeyi dener ve DNS'te var olanları ekrana basar: `Found: m.facebook.com` `Found: m.dev.facebook.com` (Siber güvenlik uzmanı için potansiyel bir hedef)
    

---

## 2. Gobuster - `vhost` Modu (Sanal Sunucu Fuzzing)

Bazen şirketler masraftan kısmak için tek bir sunucuda (aynı IP adresinde) birden fazla web sitesi barındırırlar (Virtual Hosting). DNS kayıtlarında görünmeseler bile, doğru HTTP Host başlığı (Header) ile istek yapıldığında bu gizli siteler açılır.

- `vhost` modu, DNS'e değil, doğrudan hedefin IP adresine (veya URL'sine) gider ve HTTP isteklerinin `Host:` başlığını wordlistteki kelimelerle değiştirerek tepkiyi ölçer.
    
- **Sözdizimi (Syntax):**
```Bash
gobuster vhost -u [https://hedefsite.com](https://hedefsite.com) -w /path/to/wordlist.txt
```


### Kritik Detay: Boyut Filtreleme (Exclude Length)

`vhost` taraması yaparken, sunucu genellikle var olmayan tüm alt alan adları için aynı varsayılan "Hata" sayfasını (veya ana sayfayı) döndürür. Bu durum, ekranda yüzlerce `Status: 400 [Size: 1542]` veya `Status: 200` sonucu görmenize neden olur (False Positive).

Gerçek bir gizli vhost bulduğumuzu, sayfanın **boyutunun (Size) farklı olmasından** anlarız. Ekranda sürekli tekrar eden boyutu (Örn: 1542 bayt) filtrelemek için `--exclude-length` parametresi kullanılır:

- **Filtreli Kullanım:**
```Bash
# 1542 bayt boyutunda dönen (sahte) sonuçları gizle!
gobuster vhost -u [https://hedefsite.com](https://hedefsite.com) -w /path/to/wordlist.txt --exclude-length 1542
```