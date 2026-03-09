FIDO2 (Fast Identity Online 2) güvenlik anahtarları, parolalar yerine kullanılabilen fiziksel donanım cihazlarıdır. 

* İki faktörlü kimlik doğrulama (2FA) veya tamamen parolasız (passwordless) kimlik doğrulama için kullanılırlar.
* USB cihazı veya NFC etiketi formunda olabilirler.

## Çalışma Mantığı
1. Cihaza takıldığında veya dokundurulduğunda (NFC), kimlik doğrulamayı onaylamak için benzersiz bir kriptografik **anahtar çifti** (public/private key) oluşturur.
2. Bu anahtar çifti sadece ilgili kullanıcı cihazı ve fiziksel FIDO2 donanımı arasında geçerlidir. Kimlik avı (phishing) saldırılarına karşı en üst düzey korumalardan birini sağlar.