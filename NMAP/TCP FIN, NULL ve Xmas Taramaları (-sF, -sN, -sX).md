# TCP FIN, NULL ve Xmas Taramaları (-sF, -sN, -sX)
Bu üç tarama türü, standart TCP el sıkışmasını kullanmak yerine TCP protokolünün kurallar kitabındaki (RFC 793) şu boşluğu sömürür: 
*Kurallara göre; bir porta SYN, RST veya ACK bayrağı taşımayan "anlamsız" bir paket gelirse ve port **AÇIKSA**, port bu paketi görmezden gelmeli (cevap vermemeli) ve düşürmelidir. Ancak port **KAPALIYSA**, anlamsız da olsa bu pakete bir **RST (Reset)** paketi ile cevap vermelidir.*

## 1. Tarama Türleri Nelerdir?
Nmap, hedefe bayrakları manipüle edilmiş (kural dışı) paketler gönderir:

* **FIN Taraması (-sF):** Sadece "Bağlantıyı bitir" anlamına gelen **FIN** bayrağı gönderilir. Ortada kurulmuş bir bağlantı olmadığı için bu paket hedefe çok anlamsız gelir.
* **NULL Taraması (-sN):** Hiçbir bayrak işaretlenmez. TCP başlığı tamamen boştur (NULL). 
* **Xmas Taraması (-sX):** **FIN, PSH ve URG** bayraklarının üçü birden işaretlenir. (Paket bir yılbaşı ağacı gibi ışıl ışıl yandığı için bu ismi almıştır).

## 2. Hedefin Vereceği Tepkilere Göre Port Durumları

Bu üç taramanın da hedeften beklediği tepki ve yorumlama mantığı birebir aynıdır:

* **Açık|Filtrelenmiş (Open|Filtered):** Nmap hedef porta bu tuhaf paketleri gönderir ve **hiçbir cevap alamazsa**. (Port kurallara uyup paketi çöpe atmış olabilir veya aradaki bir Firewall paketi yutmuş olabilir. Bu yüzden Nmap kesin karar veremez).
* **Kapalı (Closed):** Hedef port kurala uyar ve **TCP RST** paketi ile "Kapalıyım" derse.
* **Filtrelenmiş (Filtered):** Hedef sistemden ICMP Unreachable (Ulaşılamaz) hata mesajları dönerse (Güvenlik duvarı engelliyor demektir).

## 3. Avantajları ve En Büyük Dezavantajı (CTF Tuzağı)

**Avantajları:**
* SYN taramasından bile daha gizlidirler.
* Durum bilgisi tutmayan (Stateless) eski nesil güvenlik duvarlarını ve yönlendiricileri (Router) çok rahat atlatarak içerideki portların kapalı mı yoksa açık/filtrelenmiş mi olduğunu tespit etmemizi sağlarlar.

**En Büyük Dezavantajı (Windows Tuzağı):**
* RFC 793 kurallarına %100 uyan sistemler genellikle **Linux/Unix** tabanlı sistemlerdir. 
* **Microsoft Windows** işletim sistemleri bu kurala uymaz! Windows, bir port açık olsa bile bu tuhaf paketlere doğrudan **RST** ile cevap verir. Bu nedenle Windows bir makineye Xmas, FIN veya NULL taraması yaparsan Nmap sana *tüm portların kapalı olduğunu* söyleyecektir. (Laboratuvarlarda hedefin Windows mu Linux mu olduğunu anlamak için bile bu hile kullanılır).
