`while` döngüsü "belirli bir şart sağlanana kadar çalış" derken; `for` döngüsü "elimdeki bir listenin veya veri grubunun içindeki her bir elemanı sırayla tek tek gez" demek için kullanılır.

## Temel Mantık
For döngüsü çalışırken, listenin içindeki her bir eleman sırasıyla geçici bir değişkene atanır ve içerideki kodlar o eleman için çalıştırılır. Liste bittiğinde döngü kendiliğinden durur, `break` kullanmaya gerek yoktur.

```python
isimler = ["Ali", "Ayşe", "Mehmet"]

# "isimler listesinin içindeki her bir elemanı sırayla 'kisi' değişkenine ata ve işlemleri yap"
for kisi in isimler:
    print(f"Hoş geldin {kisi}")
    
# Çıktı:
# Hoş geldin Ali
# Hoş geldin Ayşe
# Hoş geldin Mehmet
```
## while ve for Arasındaki Fark

- **`while`**: Ne zaman biteceği belli olmayan, bir şarta veya kullanıcı girdisine bağlı durumlar için idealdir (Sonsuz menüler, çıkış yapılana kadar bekleyen sistemler).
    
- **`for`**: Ne kadar süreceği belli olan, elimizdeki hazır verilerin (örneğin 100 kişilik bir müşteri listesi, sepetteki 5 ürün vb.) üzerinde işlem yapmak için idealdir.