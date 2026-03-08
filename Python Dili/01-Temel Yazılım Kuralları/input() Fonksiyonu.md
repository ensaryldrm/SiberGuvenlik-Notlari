### Kullanıcıdan Veri Alma ve Metin Biçimlendirme
Python'da programın dışarıdan veri almasını sağlamak için `input()` fonksiyonu kullanılır. Çalıştığında, sistem kullanıcının klavyeden bir şeyler yazıp `Enter` tuşuna basmasını bekler.

*  **Kritik Bilgi:** `input()` ile dışarıdan alınan her değer, kullanıcı sayı bile girse, Python tarafından her zaman **metin (string)** formatında kaydedilir.

```python
isim = input("Adınızı giriniz: ")
yas = input("Yaşınızı giriniz: ") # Kullanıcı 20 yazsa bile, Python bunu matematiksel bir sayı olarak değil, "20" kelimesi olarak görür.