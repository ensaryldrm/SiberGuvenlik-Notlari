# TCP ACK Taraması (-sA)
Şimdiye kadar öğrendiğimiz tüm taramalar (SYN, Connect, Xmas vb.) hedefin portlarının "Açık" olup olmadığını bulmaya çalışıyordu. **TCP ACK Taraması ise portların açık olup olmadığıyla hiç ilgilenmez.** Tek bir amacı vardır: Hedefin önündeki Güvenlik Duvarının (Firewall) kurallarını haritalamak ve bu duvarın durum bilgisi tutup tutmadığını (Stateful vs Stateless) test etmektir.

## 1. Nasıl Çalışır?
Nmap, hedef porta sadece **ACK (Onay)** bayrağı işaretlenmiş bir paket gönderir. Normal TCP iletişiminde ACK paketi, önceden kurulmuş bir bağlantının devamıdır ("Mesajını aldım" demek için gönderilir). Nmap ortada hiçbir iletişim (SYN el sıkışması) yokken durduk yere bu paketi göndererek sistemi şaşırtmaya çalışır.

## 2. Hedefin Vereceği Tepkilere Göre Port Durumları

Hedefin (veya aradaki güvenlik duvarının) bu garip pakete vereceği tepki, bize ağın mimarisi hakkında net bir harita sunar:

* **Filtrelenmemiş (Unfiltered):** Eğer hedef port (açık veya kapalı olması fark etmeksizin) bu anlamsız ACK paketine bir **TCP RST (Reset)** paketi ile dönerek "Sen kimsin, aramızda bir bağlantı yok" derse. Bu, arada bir güvenlik duvarı olmadığını veya sadece basit/eski nesil (Stateless) bir koruma olduğunu gösterir. Paketimiz engellenmemiştir.
* **Filtrelenmiş (Filtered):** Nmap hiçbir yanıt alamazsa (no-response) veya ICMP Ulaşılamaz (Unreachable) hatası dönerse. Bu, arada akıllı, bağlantı durumlarını takip eden (Stateful) bir Güvenlik Duvarı olduğunu ve sahte ACK paketini fark edip anında çöpe attığını (Drop) kanıtlar.

## 3. Kullanımı ve CTF Senaryosu

```bash
nmap -sA hedef_ip
````

**Ne Zaman Kullanılır?** Sızma testinde bir hedefe SYN taraması (`-sS`) yaptığınızda Nmap size tüm portların "Filtered" olduğunu söylüyorsa, içeriye körlemesine girmek yerine `-sA` parametresini kullanırsınız. Bu sayede güvenlik duvarının hangi spesifik portları sıkı denetlediğini veya hangi portların denetim dışı bırakıldığını (ACL kurallarını) tespit edip, saldırı stratejinizi ona göre belirlersiniz.