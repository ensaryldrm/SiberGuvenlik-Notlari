# Sızma Testi (Penetration Testing) Temelleri

Sızma testi, bir sistemin güvenliğini değerlendirmek için yetkili ve planlı bir şekilde gerçekleştirilen siber saldırı simülasyonudur.

## Hacker Şapkaları (Hacker Hats) & Etik
* **White Hat (Beyaz Şapka):** Kurallara uyar, izinli test yapar, defansiftir.
* **Black Hat (Siyah Şapka):** Kötü niyetli saldırgandır, izinsiz girer, zarar verir veya çalar.
* **Grey Hat (Gri Şapka):** İzinsiz sistemlere girer ama zarar vermez, genelde açığı bulup firmaya bildirir (bazen ödül bekler).
* **Rules of Engagement (RoE - Angajman Kuralları):** Testin sınırlarını, saatlerini ve nelerin yasak olduğunu belirleyen resmi sözleşmedir. Her şeyin başıdır.

## Pentest Kapsamları (Scopes)
* **White Box (Beyaz Kutu):** Test eden kişiye sistemin tüm kaynak kodları, mimarisi ve şifreleri verilir. En kapsamlısıdır.
* **Black Box (Siyah Kutu):** Test eden kişiye hiçbir bilgi verilmez (Sadece şirket adı veya IP verilir). Gerçek bir hacker gibi dışarıdan saldırılır.
* **Grey Box (Gri Kutu):** Sınırlı bilgi verilir (Örn: Sadece standart bir kullanıcı hesabı verilir).

## Metodolojiler ve Frameworkler
**Pentest Yaşam Döngüsü (Life Cycle):**
1. Bilgi Toplama (Reconnaissance)
2. Tarama & Zafiyet Tespiti (Scanning)
3. Sisteme Sızma (Gaining Access / Exploitation)
4. Erişimi Koruma (Maintaining Access / Backdoors)
5. İzleri Silme (Covering Tracks)

**Bilinen Frameworkler:** OWASP (Web için altın standart), NIST, PTES.

## Güvenlik Prensipleri ve Modeller
* **[[CIA Triad]] (CIA Üçlüsü):** * *Confidentiality (Gizlilik):* Veriyi sadece yetkililer görmeli.
  * *Integrity (Bütünlük):* Veri yolda değiştirilmemeli.
  * *Availability (Erişilebilirlik):* Sistem 7/24 hizmet verebilmeli (DoS saldırıları bunu hedefler).
* **Erişim ve Ayrıcalıklar (Privileges):**
  * *Principle of Least Privilege (PoLP):* En az ayrıcalık prensibi. Bir kullanıcıya sadece işini yapmasına yetecek kadar yetki verilmesidir.
  * *PIM vs PAM:* **PIM** (Privileged Identity Management) yetkili kimliklerin yönetilmesidir. **PAM** (Privileged Access Management) ise bu kimliklerin sisteme nasıl ve ne zaman eriştiğini denetleyen teknolojilerdir.
* **Güvenlik Modelleri:**
  * *Bell-LaPadula:* Gizliliğe odaklanır. "Yukarı okuma, aşağı yazma" (No read up, no write down).
  * *Biba:* Bütünlüğe odaklanır. "Aşağı okuma, yukarı yazma" (No read down, no write up).

## Tehdit Modelleme (Threat Modelling) & STRIDE
Sistemi tasarlarken zafiyetleri öngörme sanatıdır. **STRIDE** Framework'ü kullanılır:
* **S**poofing (Kimlik Sahtekarlığı)
* **T**ampering (Veriyi Değiştirme)
* **R**epudiation (İnkar Edilebilirlik)
* **I**nformation Disclosure (Bilgi İfşası)
* **D**enial of Service (Hizmet Aksatma - DoS)
* **E**levation of Privilege (Yetki Yükseltme)
*(Olası bir sızıntıda [[Incident Response]] yani Olay Müdahalesi süreçleri devreye girer).*