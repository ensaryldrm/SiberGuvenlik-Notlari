```bash
# Henüz commit yapmadık ama dosyadaki değişiklikleri iptal etmek istiyorsak:
git restore dosya_adi.py

# git add . yaptık ama commit atmaktan vazgeçtiysek (Staging'den çıkarmak):
git restore --staged dosya_adi.py

# Son atılan commit mesajını yanlış yazdıysak ve düzeltmek istiyorsak:
git commit --amend -m "Yeni doğru mesaj"

# Son commit'i tamamen iptal etmek ama yazılan kodları silmemek için:
git reset HEAD~1
```
