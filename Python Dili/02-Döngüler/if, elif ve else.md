# Karar Mekanizmaları: if, elif ve else

Programların belirli şartlara göre farklı kararlar almasını ve farklı kod bloklarını çalıştırmasını sağlamak için kullanılır.

## Temel Kurallar
* **İki Nokta:** Şart belirten satırların (`if`, `elif`, `else`) sonuna her zaman iki nokta üst üste `:` konulmalıdır.
* **Girinti (Indentation):** Şart sağlandığında çalışmasını istediğimiz kodlar bir miktar içeriden (genellikle bir Tab boşluğu) yazılmalıdır. Python, hangi kodun şarta bağlı olduğunu bu boşluklardan anlar.

## Karşılaştırma Operatörleri
* `>` : Büyüktür
* `<` : Küçüktür
* `>=` : Büyük eşittir
* `<=` : Küçük eşittir
* `==` : Eşittir (Dikkat: Tek `=` değişken atar, iki `==` eşitlik kontrolü yapar)
* `!=` : Eşit değildir

## Örnek Kullanım: Sinema Bileti Sistemi
```python
yas = int(input("Yaşınızı giriniz: "))

# Kodlar yukarıdan aşağıya doğru okunur. İlk sağlanan şart çalışır, diğerleri atlanır.
if yas >= 18:
    print(f"Yaşınız {yas}, tam bilet parası veriniz.")
elif yas >= 7:
    print(f"Yaşınız {yas}, öğrenci bileti alabilirsiniz.")
else:
    print(f"Yaşınız {yas}, çocuklar için bilet ücretsizdir.")
```
