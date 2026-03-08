# Veri Koleksiyonları: Listeler (Lists)

Python'da tek bir değişkenin içine birden fazla değer saklamak istediğimizde listeleri kullanırız. Listeler köşeli parantez `[]` ile oluşturulur ve içindeki elemanlar virgül `,` ile ayrılır.

## Liste Oluşturma
```python
# Metinlerden oluşan bir liste
ogrenciler = ["Ali", "Ayşe", "Mehmet"]

# Sayılardan oluşan bir liste
notlar = [85, 90, 100]

# Boş bir liste (İçini program çalışırken doldurmak için)
sepet = []
```

## Listeye Eleman Ekleme (.append)

Mevcut veya boş bir listeye yeni bir eleman eklemek için `.append()` metodu kullanılır. Bu metot, eklenen veriyi her zaman listenin **en sonuna** yerleştirir.

Python

```python
meyveler = ["Elma", "Armut"]
meyveler.append("Muz")

print(meyveler) 
# Çıktı: ['Elma', 'Armut', 'Muz']
```