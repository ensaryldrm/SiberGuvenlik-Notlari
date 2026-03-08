```bash
# 1. Klasörde Git'i başlat (Sadece projenin başında 1 kez yapılır)
git init
 
# 2. Değişen dosyaları hazırlık aşamasına (staging area) al 
git add . # Tüm değişen dosyaları ekler 
git add dosya_adi.py  # Sadece belirli bir dosyayı ekler 

# 3. Değişiklikleri paketle ve etiketle 
git commit -m "feat: ilk python scripti eklendi" 

# 4. GitHub'daki repoyu bilgisayarına bağla (Sadece ilk seferde) 
git remote add origin [https://github.com/ensaryldrm/repo-adi.git]

# 5. Kodları GitHub'a gönder (push) # (İlk gönderimde -u parametresi gerekir, sonrakilerde sadece git push yeterlidir) 
git push -u origin main
```
