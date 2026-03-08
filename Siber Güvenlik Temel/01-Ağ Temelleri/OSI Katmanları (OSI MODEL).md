# OSI Referans Modeli
Ağ üzerindeki iletişimi standartlaştırmak için oluşturulmuş 7 katmanlı teorik bir modeldir. Siber güvenlikte bir sorunun (veya zafiyetin) hangi katmanda olduğunu bilmek hayati önem taşır.

## 7 Katman (Yukarıdan Aşağıya)
7. **Application (Uygulama):** Kullanıcının etkileşime girdiği katmandır (HTTP, FTP, DNS).
8. **Presentation (Sunum):** Verinin formatlandığı, şifrelendiği (SSL/TLS) ve sıkıştırıldığı katmandır.
9. **Session (Oturum):** Cihazlar arasındaki bağlantıyı (oturumu) kurar, yönetir ve sonlandırır.
10. **Transport (Taşıma):** Verinin güvenli veya hızlı iletiminden sorumludur (TCP ve UDP burada çalışır). Portlar bu katmandadır.
11. **Network (Ağ):** IP adreslemesinin ve yönlendirmenin (Router) yapıldığı katmandır. Veriye "Paket" denir.
12. **Data Link (Veri Bağlantısı):** MAC adreslemesinin yapıldığı, Switch'lerin çalıştığı katmandır. Veriye "Frame (Çerçeve)" denir.
13. **Physical (Fiziksel):** Kablolar, fiber optikler, Wi-Fi sinyalleri. Veri burada sadece `1` ve `0` (Bit) halindedir.

** Akılda Tutma Şifresi (Aşağıdan Yukarıya):** **P**lease **D**o **N**ot **T**hrow **S**ausage **P**izza **A**way *(Physical, Data Link, Network, Transport, Session, Presentation, Application)*