BitLocker, Windows işletim sistemlerinde bulunan tam disk şifreleme (Full Disk Encryption) özelliğidir. Sabit sürücüdeki (HDD/SSD) veya çıkarılabilir sürücülerdeki (USB bellek, hafıza kartı) tüm verileri şifreler.

## Çalışma Mantığı
* Verileri yetkisiz **fiziksel erişime** karşı korur (Örneğin, bilgisayarın çalınması veya diskin sökülüp başka bilgisayara takılması durumunda).

* Etkinleştirildiğinde bir şifreleme anahtarı (ve genellikle bir kurtarma anahtarı) oluşturulur.

* Şifreleme işleminden sonra, diskteki veriler yalnızca doğru şifreleme anahtarı (veya TPM ile entegre çalışarak doğrulanan PIN/Parola) kullanılarak okunabilir formata dönüştürülür.