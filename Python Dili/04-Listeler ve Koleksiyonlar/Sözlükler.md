Listeler verileri alt alta sıralamak için harikadır ama veriler arasında bir ilişki kuramazlar. Sözlükler ise verileri **"Anahtar ve Değer" (Key - Value)** eşleşmesiyle tutmamızı sağlar.

Gerçek hayattaki bir sözlük gibi düşünebiliriz: "Kelime" (Anahtar) ve "Anlamı" (Değer). Python'da sözlükler süslü parantez `{}` ile oluşturulur.

**Sözlük Oluşturma ve Veri Çekme**

```python
# 'anahtar': 'değer' formatında yazılır.
kullanici = {
    "isim": "Ensar",
    "meslek": "Yazılım",
    "yas": 21
}

# Sözlükten bir veri çekmek için sırasını değil, anahtarın adını kullanırız.
print(kullanici["meslek"])  # Çıktı: Yazılım
```

**Sözlüğe Yeni Veri Ekleme veya Güncelleme**

```python
# Boş bir sözlük oluşturma
sistem = {}

# Sözlüğe yeni bir kayıt ekleme
sistem["kullanici_adi"] = "admin123"

# Var olan bir kaydı güncelleme
sistem["kullanici_adi"] = "superadmin"
```
## Sözlüklerde For Döngüsü Kullanımı (.items) 
Sözlükler üzerinde sadece `for x in sozluk:` dersek sadece anahtarları (keys) elde ederiz. Hem anahtarı hem de karşılığındaki değeri aynı anda almak için `.items()` metodu kullanılır ve `for` döngüsüne iki değişken verilir. 

```python 
kullanici = {"isim": "Ali", "yas": 25} 

for anahtar, deger in kullanici.items(): 
	print(f"{anahtar}: {deger}")
```
