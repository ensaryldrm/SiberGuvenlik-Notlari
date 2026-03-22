# Zamanlama Şablonları (Timing Templates) (-T)


Nmap, ağın durumuna ve saldırganın niyetine göre tarama hızını ayarlamak için 0'dan 5'e kadar numaralandırılmış altı farklı zamanlama (hız) şablonu sunar. 

Bu şablonlar, paketlerin ne kadar hızlı gönderileceğini ve bir paketin yanıtı için ne kadar bekleneceğini (Timeout) otomatik olarak ayarlar.

## 1. Zamanlama Modları (T0 - T5)

* **-T0 (Paranoid - Paranoyak):** En yavaş moddur. Ağda sıfır iz bırakmak ve IDS (Saldırı Tespit Sistemleri) alarmlarını tetiklememek için her paket arasına tam 5 dakika gecikme koyar. Devasa ağlarda kullanılması imkansızdır (yıllar sürebilir).
* **-T1 (Sneaky - Sinsi):** Gizliliğin ön planda olduğu yavaş bir moddur. Paketler arasına 15 saniye koyar. T0 gibi sadece IDS atlatmak için kullanılır.
* **-T2 (Polite - Kibar):** Hedef sistemi ve ağın bant genişliğini yormamak için tarama hızını düşürür (paket arası 0.4 saniye). Hedefi çökertmekten korkulan (örneğin eski endüstriyel SCADA sistemleri) durumlarda tercih edilir.
* **-T3 (Normal):** Nmap'in **varsayılan** çalışma modudur. `-T` parametresi girilmezse Nmap doğrudan T3 hızında çalışır. Hız ve doğruluk açısından en dengeli moddur.
* **-T4 (Aggressive - Agresif):** Modern, hızlı ve geniş bantlı bir ağda olduğunuzu varsayar. Taramaları oldukça hızlandırır.
* **-T5 (Insane - Çılgın):** Ağın kusursuz derecede hızlı olduğunu ve hız uğruna doğruluktan ödün verilebileceğini varsayar. Aşırı hızlıdır ancak paket kayıpları yaşanacağı için **bazı açık portları kaçırma ihtimali çok yüksektir.**

---

## 2. Kullanım Senaryoları ve CTF Tavsiyeleri

Kullanımı sadece parametrenin yanına rakamı yazmaktan ibarettir:
```bash
nmap -sS -T4 hedef_ip
````

**🔥 Sızma Testi ve CTF İpuçları:**

1. **Altın Standart (-T4):** CTF laboratuvarlarında ve modern ağlarda yapılan sızma testlerinde endüstri standardı **`-T4`**'tür. T3 bazen çok vakit kaybettirirken, T4 kabul edilebilir bir doğrulukla çok ciddi zaman kazandırır.
    
2. **T5 Tehlikesi:** Eğer çok hızlı bir ağda değilsen `-T5` kullanmak, tıpkı okumadan bir sözleşmeyi imzalamak gibidir. Hedefteki açık olan SSH (22) veya FTP (21) gibi kritik portlar, ağdaki milisaniyelik bir gecikme yüzünden taramada çıkmayabilir.
    
3. **IDS Atlatma:** Eğer hedefte çok katı bir güvenlik cihazı (IPS/IDS) varsa ve anında IP'nizi banlıyorsa, `-T2` veya `-T1` kullanarak cihazın eşik değerlerinin (rate limit) altında kalmaya çalışabilirsiniz.