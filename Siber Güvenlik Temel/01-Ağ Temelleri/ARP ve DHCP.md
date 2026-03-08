# Ağın Gizli Kahramanları: ARP ve DHCP

## ARP (Address Resolution Protocol)
IP adresini bildiği bir cihazın, **MAC adresini** öğrenmek için kullandığı protokoldür. 
* *Siber Güvenlik Notu:* "ARP Spoofing/Poisoning" saldırısı ile hackerlar ağdaki trafiği kendi üzerlerine çekebilir (Ortadaki Adam - MiTM saldırısı).

## DHCP (Dynamic Host Configuration Protocol)
Ağa yeni bağlanan cihazlara otomatik olarak IP adresi, Alt Ağ Maskesi (Subnet Mask) ve Gateway dağıtan sunucudur. Elle IP girme zahmetinden kurtarır.

### DHCP Çalışma Mantığı (DORA Süreci)
Bir cihaz ağa bağlandığında şu 4 adımı izler:
1. **D (Discover - Keşif):** Cihaz ağa bağırır: *"Buralarda bir DHCP sunucusu var mı?"*
2. **O (Offer - Teklif):** DHCP sunucusu cevap verir: *"Buradayım, sana `192.168.1.10` IP'sini verebilirim."*
3. **R (Request - İstek):** Cihaz kabul eder: *"Tamam, o IP'yi almak istiyorum, bana tahsis et."*
4. **A (Acknowledgment - Onay):** DHCP sunucusu onaylar: *"Kayıtlara geçtim, o IP artık senin."*