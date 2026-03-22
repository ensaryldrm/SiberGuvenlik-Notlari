# TCP Idle (Zombi) Taraması (-sI)


Kendi IP adresinizi tamamen gizleyerek, ağdaki başka bir makineyi (Zombi) aracı olarak kullandığınız, %100 kör (blind) ve en üst düzey gizlilik sağlayan port tarama yöntemidir. 

Hedefin güvenlik duvarı veya saldırı tespit sistemi (IDS), taramayı sizin değil, "Zombi" makinenin yaptığını zanneder. Ayrıca Zombi ile Hedef arasındaki "Güven İlişkilerini" (IP tabanlı beyaz listeleri) sömürmek için de kullanılır.

## 1. Zombi Makinede Aranan Şartlar
Bu saldırının çalışması için rastgele bir makineyi zombi yapamazsınız. Makinede şu iki şart olmalıdır:
1. **Gerçekten Boşta (Idle) Olmalı:** Zombi makine o an ağda aktif bir trafik üretmiyor olmalıdır. Aksi takdirde IP ID numaraları sürekli değişeceği için sonuçlar karışır.
2. **Tahmin Edilebilir IP ID:** Zombi makinenin işletim sistemi, ürettiği her ağ paketine sırayla artan (ardışık) bir IP Kimlik Numarası (IP ID) vermelidir (Örn: Eski Windows sürümleri veya bazı yazıcılar).

## 2. Idle Tarama Nasıl Çalışır? (3 Adımlı Büyü)

Saldırgan (Nmap), Zombi ve Hedef arasındaki kusursuz üçgen şu şekilde işler:

1. **Zombinin Nabzını Ölçme:** Nmap, Zombi makineye bir paket gönderir ve Zombinin o anki **IP ID numarasını** öğrenip kaydeder (Örneğin IP ID: 100 olsun).
2. **Hedefe Sahte (Spoofed) Paket Gönderme:** Nmap, hedef makinenin portuna bir SYN paketi gönderir. Ancak bu paketin "Kaynak IP" kısmına kendi IP'sini değil, **Zombinin IP'sini** yazar!
3. **Hedefin Zombiye Tepkisi (Kritik Aşama):**
   * **Eğer port AÇIKSA:** Hedef, SYN paketini Zombiden geldi sandığı için Zombiye bir SYN/ACK paketi gönderir. Zombi bu paketi beklemediği için hedefe "Sen hayırdır?" dercesine bir **RST** paketi fırlatır. Zombi bir paket ürettiği için **IP ID numarası 1 artar** (101 olur).
   * **Eğer port KAPALIYSA:** Hedef, Zombiye RST paketi gönderir. Zombi gelen RST paketini umursamaz ve hiçbir şey yapmaz. **IP ID numarası artmaz** (100 kalır).
4. **Sonuç (Zombiyi Tekrar Ölçme):** Nmap, Zombiye tekrar bir paket gönderir. 
   * Zombinin yeni IP ID'si **102** olmuşsa (Nmap'in ilk sorgusu + Zombinin hedefe attığı RST + Nmap'in son sorgusu = 2 artış), **Port AÇIKTIR**.
   * Zombinin yeni IP ID'si **101** olmuşsa (Sadece Nmap'in iki sorgusu = 1 artış), **Port KAPALI veya FİLTRELİDİR**.

## 3. Kullanımı

Kullanımı çok basittir, ancak uygun zombiyi bulmak zordur:
```bash
nmap -sI [Zombi_IP] [Hedef_IP]
````

Örnek:

Bash

```
nmap -sI 10.10.10.10 10.10.10.192
```

## 4. Avantajları ve Dezavantajları

**Avantajları:**

- **Mutlak Gizlilik:** Kendi IP adresiniz hedef sistemin loglarına kesinlikle düşmez.
    
- **Firewall Atlatma:** Hedef sistem, sadece Zombi makinenin (örneğin ağdaki güvenilir bir yazıcının) IP'sine izin veriyorsa, bu güven ilişkisini sömürerek güvenlik duvarını aşabilirsiniz.
    

**Dezavantajları:**

- Uygun (gerçekten boşta duran ve ardışık IP ID üreten) bir zombi bulmak modern ağlarda çok zordur.
    
- Diğer tarama türlerine göre oldukça yavaş çalışır.