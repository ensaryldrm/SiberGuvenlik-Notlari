## Linux İzin Mantığı (Permissions)
Linux'ta her dosyanın 3 tür izni vardır: **R (Read/Okuma - 4)**, **W (Write/Yazma - 2)**, **X (Execute/Çalıştırma - 1)**.
* Yetki yükseltmek için genelde `chmod` komutu kullanılır.

```bash
# Sadece sahibine tam yetki, diğerlerine sıfır yetki verir.
chmod 700 gizli_dosya.txt 

# HERKESE okuma, yazma ve çalıştırma yetkisi verir (Çok tehlikeli!)
chmod 777 zararli_yazilim.sh```
```
## Süreç Yönetimi (Process Management)
Arka planda çalışan uygulamaları yönetme:
* `ps aux`: Sistemde çalışan tüm süreçleri ve kimin çalıştırdığını listeler.
* `top`: Çalışan süreçleri canlı (Windows Görev Yöneticisi gibi) gösterir.
* `kill -9 <PID>`: Zorluk çıkaran veya donan bir uygulamayı ID numarası (PID) ile zorla kapatır.