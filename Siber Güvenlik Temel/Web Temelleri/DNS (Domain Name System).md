## DNS (Domain Name System)
* Kullanıcıları WWW 'deki web sitelerine, hizmetlere ve kaynaklara bağlamada temel bir rol oynayan İnternet altyapısının kritik bir bileşenidir. Kısaca İnternetin telefon rehberi diyebiliriz.
* Kullanıcı dostu olan alan adlarını bilgisayarın ve ağ cihazlarının internette birbirlerini bulmak için kullandıkları sayısal IP adreslerine çevirir.

### Alan Adı (Domain)
- İnternet üzerindeki belirli bir konumu veya kaynağı temsil eden, insan tarafından okunabilir bir etikettir. Alan adları, noktalarla ayrılmış seviyelerle bir hiyerarşi olarak yapılandırılmıştır.
-  Örneğin, www.example.com alan adı üç bölümden oluşur:
	 1) www - alt alan adı(subdomain)
	 2) example - ikinci düzey alan adı (second-level domain)
	 3) com - üst düzey alan adı (top-level domain)
#### Üst Düzey Alan Adı (Top-Level Domain, TLD)
- İnternet alan adları hiyerarşisinin en üstünde yer alır.
- Genellikle alan adı uzantısı da denir. 
- TLD'ler, web sitelerinin türünü, amacını veya coğrafi konumunu belirtmek için kullanılır.

### DNS Sunucu Türleri
1) Yetkili Ad Sunucusu (Authoritative Name Server)
	- Belirli bir alan adı için "resmi" bilgi kaynağıdır. Her alan adının en az bir yetkili ad sunucusu vardır ve bu sunucu o alan adına ait bir DNS kayıtlarını tutar.

2) Özyineli Çözücü (Recursive Resolver)
	-  Kullanıcı bir web sitesine erişmek istediğinde, bu talep ilk olarak özyineli çözücüye gider. Özyineli çözücü, kullanıcı adına sorguyu çözmek için gerekli araştırmayı yapar. Bu süreç, önce genel bir yönlendirme ile başlar ve sonunda istenen bilgiyi bulana kadar çeşitli DNS sunucuları arasında adım adım ilerler. Bu süreç sırasında özyineli çözücü, gerekli DNS kayıtlarını önbelleğine alır, bu da gelecekteki sorguların daha hızlı çözümlenmesini sağlar.

3) Kök Ad Sunucuları (Root Name Servers)
	- Internetin DNS hiyerarşisinin en üstündeki sunuculardır ve tüm TLD'lerin adres bilgilerini barındırır. Bir özyineli çözücü, alan adının hangi TLD sunucusuna sorması gerektiğini bilmiyorsa, sorguyu çözmeye başlamak için önce kök ad sunucularına başvurur. Kök ad sunucuları, sorgunun doğru TLD sunucusuna yönlendirilmesi için gerekli ilk yönlendirme bilgisini sağlar.