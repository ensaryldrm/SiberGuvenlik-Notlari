# Servis ve Versiyon Tespiti (-sV)
Nmap'in standart taramaları sadece portun açık olup olmadığını söyler. **`-sV` (Service Version)** parametresi ise açık olan portlara özel problar (istek paketleri) göndererek, arkada çalışan servisin kendisiyle konuşur ve tam adını/sürümünü (Banner Grabbing) öğrenmeye çalışır.

## 1. Neden Bu Kadar Önemlidir? (CTF Mantığı)

* **Zafiyet (Exploit) Bulma:** Sızma testlerinin %90'ı, sistemde çalışan eski ve zafiyetli bir yazılım sürümünü bulmaya dayanır. `Apache 2.4.7` sürümünde bir açık varsa, hedefe özel olarak o açığı (exploit) kullanarak sızarsınız.
* **Gizli Servisleri Keşfetme:** Sistem yöneticileri bazen güvenlik önlemi (Security through obscurity) olarak servislerin varsayılan portlarını değiştirirler. Örneğin; SSH servisini 22 yerine 8080 portuna taşıyabilirler. Standart bir tarama 8080'i "HTTP-Proxy" olarak etiketlerken, `-sV` parametresi o portla iletişime geçip arkadakinin aslında "SSH" olduğunu ortaya çıkarır.

## 2. Kullanımı ve Çıktı Analizi

En temel kullanımı şu şekildedir:
```bash
nmap -sV hedef_ip
````

**Örnek Çıktı Okuma:**

Plaintext

```
PORT      STATE SERVICE    VERSION
22/tcp    open  ssh        OpenSSH 6.6.1p1 Ubuntu 2ubuntu2.13 (Ubuntu Linux; protocol 2.0)
80/tcp    open  http       Apache httpd 2.4.7 ((Ubuntu))
```

Bu çıktı siber güvenlik uzmanına şunu söyler:

- _Sadece portlar açık değil; 22. portta Ubuntu işletim sistemine ait OpenSSH'ın 6.6.1 sürümü koşuyor. 80. portta ise Apache Web Sunucusunun 2.4.7 sürümü var._ * Saldırgan bu noktadan sonra doğrudan Google veya Exploit-DB üzerinde `"Apache 2.4.7 exploit"` veya `"OpenSSH 6.6.1p1 vulnerability"` araması yaparak içeri girmenin yolunu arar.
    

## 3. Versiyon Tespiti Yoğunluğu (Intensity)

Bazen Nmap, servisin versiyonunu anlamakta zorlanabilir. Böyle durumlarda Nmap'i daha agresif sorular sormaya zorlayabilirsiniz. Yoğunluk seviyesi 0 (en hafif) ile 9 (en agresif/tüm ihtimalleri dener) arasındadır. Varsayılan seviye 7'dir.

Eğer kesin sonuç istiyorsanız ve hız/gizlilik sorununuz yoksa:

Bash

```
nmap -sV --version-intensity 9 hedef_ip
# Veya kısaltması:
nmap -sV --version-all hedef_ip
```

_(Not: Bu işlem tarama süresini ciddi şekilde uzatır.)_