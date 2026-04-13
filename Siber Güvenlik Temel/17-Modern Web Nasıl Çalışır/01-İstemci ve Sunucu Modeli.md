## İstemci Nedir?
- Web sitelerini görüntüleyebilen ve sunucularla etkileşimde bulunabilen cihazlardır. Genellikle kişisel bilgisayarlar, akıllı telefonlar, tabletler gibi internete bağlanabilen her türlü cihazı kapsar. İstemciler, web tarayıcıları aracılığıyla kullanıcıların web sayfalarıyla etkileşime girmesini sağlar. Kullanıcı, web tarayıcısında bir URL girerek veya bir bağlantıya tıklayarak bir web sayfası talep eder. Bu eylem, sunucuya bir HTTP/HTTPS isteği olarak iletilir.

## Sunucu Nedir?
- istemcilerden gelen istekleri kabul eden, işleyen ve gerekli yanıtları geri gönderen bir bilgisayar veya yazılım uygulamasıdır. Web siteleri, internet üzerinde bulunan sunucularda barındırılır.

## İstemci ve Sunucu İletişimi
- İstemci ve sunucu arasındaki iletişim genellikle HTTP veya HTTPS protokolleri üzerinden gerçekleşir. İstemci, bir web sayfasına erişmek istediğinde, URL'yi içeren bir HTTP GET isteği gönderir. Sunucu, bu isteği alır, gerekli kaynağı bulur ve HTTP yanıtı ile birlikte istemciye geri gönderir.

	Örneğin: 
	1) Kullanıcı, tarayıcıda www.example.com adresine girer.
	2) Tarayıcı, www.example.com adresine bir HTTP GET isteği gönderir.
	3)  www.example.com adresinde çalışan web sunucusu, isteği alır ve istenen ana sayfayı bulur.
	4) Sunucu, ana sayfanın HTML içeriğini içeren bir HTTP yanıtı hazırlar ve istemciye geri gönderir.
	5) Tarayıcı, gelen HTML içeriğini işler ve kullanıcıya görsel bir web sayfası olarak sunar.