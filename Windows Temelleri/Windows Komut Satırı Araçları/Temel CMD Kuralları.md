# Temel CMD Komutları (Dosya ve Dizin Yönetimi)

Windows Komut İstemi'nde (CMD) dosya ve klasörler üzerinde gezinmek, oluşturmak veya silmek için kullanılan temel komutlar şunlardır:

## 1. dir (Directory List)
Belirtilen veya o an içinde bulunulan dizindeki (klasördeki) tüm dosyaları ve alt klasörleri listeler.
```cmd
C:\Users\user> dir
````

## 2. cd (Change Directory)

Mevcut çalışma dizinini değiştirmek için kullanılır.

- **`.` (Tek nokta):** O an bulunulan klasörü temsil eder.
    
- **`..` (Çift nokta):** Bir üst klasörü temsil eder.
    


```DOS
C:\Users\user> cd Documents
C:\Users\user\Documents>
```

## 3. mkdir (Make Directory)

Bulunulan konumda yeni bir klasör oluşturur.

```DOS
C:\Users\user\Documents> mkdir newdir
```

## 4. rmdir (Remove Directory)

İçi tamamen boş olan bir klasörü silmek için kullanılır (İçi doluysa silmez, hata verir).

```DOS
C:\Users\user\Documents> rmdir newdir
```

## 5. copy

Bir dosyayı bulunduğu yerden alıp, adını veya konumunu belirterek başka bir yere (veya aynı yere farklı bir isimle) kopyalar.

```DOS
C:\Users\user\Documents> copy test.txt test1.txt
```

## 6. move

Bir dosyayı veya klasörü bir dizinden alıp başka bir dizine taşır (Kes-Yapıştır mantığı). Aynı zamanda dosyanın adını değiştirmek için de kullanılabilir.

```DOS
C:\Users\user\Documents> move test.txt ..\Desktop
```

## 7. del (Delete)

Belirtilen bir dosyayı kalıcı olarak siler (Geri Dönüşüm Kutusu'na göndermez).

```DOS
C:\Users\user\Documents> del test1.txt
```
