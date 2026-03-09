Windows, kullanıcıları farklı erişim haklarına sahip kategorilere ayıran bir kullanıcı yapısı kullanır. En yaygın iki kategori şunlardır:

### Yöneticiler (Administrators)

- Bilgisayarda tam kontrol sahibidirler.
    
- Sistem ayarlarını değiştirebilir, programları yükleyebilir ve kaldırabilir, diğer kullanıcı hesaplarını yönetebilirler.
    
- Hassas sistem dosyalarını ve verileri değiştirme yeteneğine sahip olduklarından, bu rol yalnızca güvenilir kişilere atanmalıdır.
    

### Standart Kullanıcılar

- Bilgisayarı kullanmak için temel izinlere sahiptirler.
    
- Programları çalıştırabilir, dosyaları açabilir ve düzenleyebilir, internete erişebilirler.
    
- Sistem ayarlarını değiştiremez, programları yükleyemez veya kaldıramaz ve diğer kullanıcı hesaplarını yönetemezler. Bilgisayarın güvenliğini ve istikrarını korumaya yardımcı olurlar.
    

### Diğer Kullanıcı Türleri

- **Konuk (Guest):** Bilgisayarı geçici olarak kullanmak için sınırlı izinlere sahip olan kullanıcı türüdür.
    
- **Belirtilmiş Erişim:** Belirli programları veya dosyaları kullanmak için özel izinlere sahip olan kullanıcı türüdür.
    

### Kullanıcı Hesaplarını Yönetme

Hesapları yönetmenin en hızlı yolu "Yerel Kullanıcı ve Gruplar" üzerinden düzenleme yapmaktır:

1. Başlat menüsüne PowerShell yazıp açın.
    
2. Gelen ekrana aşağıdaki komutu yazın:
    

```PowerShell
lusrmgr
```

3. Gelen pencereden yerel kullanıcıları ve grupları yönetebilir, hesap türlerini değiştirebilir, hesapları aktifleştirip devre dışı bırakabilirsiniz.