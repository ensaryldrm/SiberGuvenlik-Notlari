**UAC (User Account Control)**, Microsoft Windows işletim sistemlerinde yerleşik bir güvenlik özelliğidir. Bilgisayarınızda yönetici yetkisi gerektiren işlemleri gerçekleştirmeden önce size onay isteyerek çalışır. Bu, yetkisiz değişikliklerden veya zararlı yazılımların yüklenmesinden kaynaklanan hataları önlemeye yardımcı olur.

Bir program yönetici ayrıcalıkları gerektiren bir işlem gerçekleştirmeye çalıştığında, UAC penceresi ekranda görüntülenir ve onay/red kararı vermeniz gerekir.

**UAC Dereceleri (Yüksekten Alçağa):**

- **Her zaman uyar:** En güvenli seçenektir. Sistem ayarlarında yaptığınız değişiklikler dahil her şey için uyarı alırsınız.
    
- **Yalnızca programlar bilgisayarımda değişiklik yapmaya çalıştığında uyar (Varsayılan):** Programların yaptığı değişiklikler için uyarı alırsınız ancak kendi yaptığınız değişiklikler için uyarı almazsınız.
    
- **Yalnızca programlar bilgisayarımda değişiklik yapmaya çalıştığında uyar (Masaüstü kararmaz):** Üç bildirim seçeneğinin en az güvenli olanıdır. Uyarı varsayılan ile aynıdır ancak UAC penceresi açıldığında masaüstü kullanılabilir kalır.
    
- **Asla uyarı gösterme (UAC devre dışı):** Önerilmez. Tüm UAC uyarılarını devre dışı bırakarak sisteminizi savunmasız hale getirir.
    

**Avantajları:**

- **Güvenlik:** Yetkisiz değişikliklerden kaynaklanan hataları ve zararlı yazılımların yüklenmesini önler.
    
- **Kontrol:** Yönetici ayrıcalıkları gerektiren işlemler üzerinde daha fazla kontrol sağlar.
    
- **Kullanıcı Dostu:** Ne olup bittiğini anlamanıza ve işlem öncesi durdurmanıza olanak tanır.
    

**Dezavantajları:**

- **Rahatsızlık:** Sık onay istemesi bazı kullanıcılar için rahatsız edici olabilir.
    
- **Uyumsuzluk:** Bazı programlar UAC ile uyumsuz olabilir ve düzgün çalışmayabilir.