Programların belirli bir şarta kadar veya sonsuza kadar tekrar etmesini sağlamak için döngüler (loops) kullanılır. Python'daki en temel döngülerden biri `while` döngüsüdür.

# While True Yapısı
Eğer bir işlemin biz aksini söyleyene kadar (örneğin kullanıcı çıkış yapana kadar) sürekli tekrar etmesini istiyorsak `while True:` yapısını kullanırız. Döngüyü durdurmak istediğimiz noktada ise `break` komutu devreye girer.

```python
# Bu kod, kullanıcı "q" yazana kadar sürekli çalışır.
while True:
    mesaj = input("Bir mesaj yazın (Çıkmak için 'q'): ")
    
    # Döngüyü kırma şartımız
    if mesaj == "q":
        print("Sistemden çıkılıyor...")
        break # break komutu çalıştığı an döngü tamamen durur.
        
    print(f"Yazdığınız mesaj: {mesaj}")
```
# Ek Bilgi: Döngü Kırma Yöntemleri (break vs exit)

Döngüleri veya programı sonlandırırken duruma göre iki farklı yöntem seçilebilir:

- **`break`:** Sadece içinde bulunduğu döngüyü (örneğin `while`) kırar ve durdurur. Eğer döngü bloğunun dışında, alt satırlarda başka kodlar varsa program onları okumaya ve çalışmaya devam eder.
    
- **`exit()`:** Döngüye veya altındaki kodlara bakmaksızın, o an çalışan tüm Python dosyasını (programı) anında ve tamamen kapatır.