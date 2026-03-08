Programların belirli bir şarta kadar veya sonsuza kadar tekrar etmesini sağlamak için döngüler (loops) kullanılır. Python'daki en temel döngülerden biri `while` döngüsüdür.

## while True Yapısı
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
