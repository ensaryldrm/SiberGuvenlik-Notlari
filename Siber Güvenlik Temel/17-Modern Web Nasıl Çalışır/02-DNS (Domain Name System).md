# DNS (Domain Name System) Temelleri

## 1. DNS Nedir?
DNS, internetin **telefon rehberidir**. İnsanların hatırlaması kolay olan alan adlarını (örn: `www.example.com`), bilgisayarların iletişim kurmak için kullandığı IP adreslerine (örn: `192.168.1.10`) çevirir.

## 2. Alan Adı (Domain) Yapısı
Alan adları hiyerarşik bir yapıya sahiptir ve noktalarla ayrılır:
* **www** : Alt alan adı (Subdomain)
* **example** : İkinci düzey alan adı (İsmin kendisi)
* **com** : Üst Düzey Alan Adı (TLD - Top Level Domain). Sitenin türünü veya ülkesini belirtir (Örn: `.org`, `.gov`, `.tr`).

## 3. DNS Sunucu Türleri
DNS çözümleme sürecinde 3 ana aktör görev yapar:
1. **Özyineli Çözücü (Recursive Resolver):** İnternet Servis Sağlayıcısı (ISP) tarafından sunulur. Kullanıcı adına tüm araştırmayı yapan, diğer sunuculara sorular soran ve sonuçları önbelleğe (cache) alan işçi sunucudur.
2. **Kök Ad Sunucuları (Root Name Servers):** Hiyerarşinin en üstüdür. TLD'lerin (.com, .net vb.) adreslerini bilir ve çözücüyü doğru TLD sunucusuna yönlendirir.
3. **Yetkili Ad Sunucusu (Authoritative Name Server):** Belirli bir alan adının "resmi" sahibidir. Asıl IP adresini ve DNS kayıtlarını barındıran son duraktır.

## 4. DNS Çözümleme Süreci (Adım Adım)
Bir web sitesine girmek istediğinizde arka planda milisaniyeler içinde şu döngü gerçekleşir:
1. **Sorgu:** Kullanıcı tarayıcıya adresi girer, bilgisayar bu adresi **Özyineli Çözücüye** (Resolver) sorar.
2. **Kök Sunucuya Gidiş:** Çözücünün önbelleğinde adres yoksa, **Kök Sunucuya** gider. Kök sunucu onu ilgili **TLD Sunucusuna** (Örn: .com sunucusu) yönlendirir.
3. **TLD ve Yetkili Sunucu:** TLD sunucusu, alan adının **Yetkili Sunucusunun** yerini söyler. Çözücü son olarak yetkili sunucuya gidip asıl IP adresini alır.
4. **Bağlantı:** Çözücü bu IP adresini kullanıcının bilgisayarına iletir ve tarayıcı hedef sunucuya bağlanır.

## 5. Önemli DNS Kayıt Türleri
| Kayıt | İşlevi |
| :--- | :--- |
| **A** | Alan adını **IPv4** adresine çevirir. |
| **AAAA** | Alan adını **IPv6** adresine çevirir. |
| **CNAME** | Bir alan adını başka bir alan adına yönlendirir (Alias/Takma ad). |
| **MX** | O alan adına ait e-posta (Mail) sunucusunun adresini belirtir. |
| **NS** | Alan adının Yetkili Ad Sunucularının (Name Servers) adreslerini gösterir. |
| **TXT** | Alan adıyla ilişkili metinleri saklar. Genellikle e-posta güvenliği (SPF vb.) ve doğrulama için kullanılır. |
