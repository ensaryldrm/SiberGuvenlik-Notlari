# Metasploit Framework: Giriş ve Temel Kavramlar

Metasploit, güvenlik açıklarını bulmak, bu açıkları sömürmek ve hedef sistemde yetki elde etmek için kullanılan dünyanın en popüler sızma testi platformudur. 

İki ana sürümü vardır:
1. **Metasploit Pro:** Ücretli, web arayüzü (GUI) olan, raporlama ve sosyal mühendislik süreçlerini otomatikleştiren kurumsal sürümdür.
2. **Metasploit Framework (MSF):** Ücretsiz, açık kaynaklı ve komut satırı (CLI) üzerinden çalışan sürümdür. CTF'lerde, sızma testlerinde ve OSCP gibi sınavlarda ana silahımız bu sürümdür.

---

## 1. Temel Terminoloji (CTF Sözlüğü)

Metasploit konsoluna (`msfconsole`) girdiğinizde her şey bu modüller etrafında döner. Bu kavramların farkını bilmek hayati önem taşır:

* **Modül (Module):** Metasploit içindeki her bir araca verilen genel isimdir. Exploitler, payloadlar ve tarayıcıların hepsi birer modüldür.
* **Exploit:** Hedef sistemdeki bir yazılım zafiyetini (bug, zayıflık) kullanarak sistemi kırıp içeri girmemizi sağlayan "koçbaşı" kodudur. Exploit sadece kapıyı kırar, içeri girdikten sonra ne yapılacağını Payload belirler.
* **Payload:** Exploit başarılı olup sistem kırıldıktan sonra, hedef makinede çalıştırılacak olan asıl "zararlı" koddur (Örn: Bize terminal bağlantısı açan kod).
* **Auxiliary (Yardımcı Modüller):** Sömürü (exploit) yapmayan, doğrudan sisteme sızmayan tarama modülleridir. Nmap gibi port tarayabilir, brute-force (kaba kuvvet) yapabilir veya zafiyetin var olup olmadığını uzaktan kontrol edebilirler.
* **Shellcode:** Sistemin belleğine doğrudan enjekte edilerek çalıştırılan ve genellikle bize bir komut satırı (shell) sağlayan küçük yapıdaki payload türüdür.

---

## 2. Shell (Kabuk) ve Bağlantı Türleri (Çok Önemli)


Hedef sistemi exploit ettikten sonra komut çalıştırabilmek için bir "Shell" elde etmeliyiz. İki temel mantık vardır:

* **Bind Shell (Bağlanan Kabuk):** Saldırgan hedefi hackler ve hedefin makinesinde gizli bir port (örn: 4444) açarak dinlemeye başlar. Ardından saldırgan, kendi makinesinden hedefin bu açılan portuna bağlanır. *Dezavantajı: Hedefte bir Güvenlik Duvarı (Firewall) varsa, dışarıdan içeriye yapılan bu bağlantı isteğini engelleyecektir.*
* **Reverse Shell (Tersine Kabuk):** Siber güvenlikte en çok kullanılan yöntemdir. Saldırgan kendi makinesinde bir port açıp dinlemeye geçer. Hedef makinedeki zararlı kod (payload) çalışınca, hedef makine "içeriden dışarıya" doğru saldırganın makinesine bağlanır. *Avantajı: Güvenlik duvarları genellikle dışarıdan gelen bağlantıları engellerken, içeriden dışarı (internete) çıkan bağlantılara izin verdiği için güvenlik duvarını kolayca atlatır.*

---

## 3. Meterpreter: Gelişmiş Payload
Standart bir shell size sadece siyah bir komut ekranı (cmd/bash) verir. **Meterpreter** ise Metasploit'e özel, çok yetenekli ve gelişmiş bir payload türüdür.
* Hedefin sabit diskine dokunmadan **sadece RAM (Bellek) üzerinde** çalışır. Bu sayede Antivirüs (AV) sistemleri tarafından yakalanması çok zordur.
* Kendine ait özel komutları vardır: Tek komutla hedefin kamerasını açabilir, mikrofonunu dinleyebilir, ekran görüntüsü alabilir veya kullanıcı parolalarının hash değerlerini (`hashdump`) çekebilirsiniz.