# pkcs11 kullanımı, pkcs11 hata mesajları
 Kriptoloji projelerimizin ana domaini olduğu için, algoritmalar hakkında yeterli bilgiye sahip olmamız gerekiyor. Hangi algoritmada, hangi algoritma ve mekanizmalar kullanılmaktadır vs.
Diğer bir konu ise pkcs'ye aşina olmak. Örneğin cryptaway'de bize hsm'den bir hata döndüğü zaman PKCS hata formatında dönebiliyor. Bu durumda hatayı anlamlandırmak için, hangi hata ne anlama geliyor bilmemiz gerekiyor.

*Cryptaway'de çalışan servislerin, configlerinin incelenmesi. Hangi config ne için kullanılıyor bunun anlaşılması ve öğrenilmesi gerekiyor.

Bu sayede kurulumda bir hata oldugu zaman, servislerin configlerine bakıldıgı zaman hata kolayca anlamlandırılabilir. Bu konuda müsait vakitlerde projenin kodlarını da inceleyebilir, dilerseniz yazılımcı arkadaslara da hangi config ne için kullanılıyor detaylı öğrenmek için sorabilirsiniz. Configlerin her birinde yapılan bir harf hatası kurulum hatalı olmasına sebep vereceğinden, her birinin anlamını bilmek büyük önem arz ediyor.


https://developers.yubico.com/YubiHSM2/Usage_Guides/OpenSSL_with_pkcs11_engine.html
