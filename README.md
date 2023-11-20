# Blog-Post
Burada Çeşitli konularda yazıları yayınlamak için oluşturulmuştur.

## Olması Gereken konular;

* Data Structures & Algorithms
* Desingn Patterns (+ Abstractions, Decoupling)
* Software Architecture (DDD, Clean/Hexagonal, Microsevice)
* Parallel & concurrent execution
* Linux Kernel capabilities, syscalls
* TCP/IP


Eğitim konuları şunlar :

1)İnternet nedir, nasıl çalışır? (https://www.youtube.com/watch?v=jVsUOiBzu7o&list=PLh9ECzBB8tJMKXMd8ovXR8TmQeaVtz5-l)
Geliştirdiğimiz uygulamalar web üzerinde çalıştığı için, internetin çalışma mantığını anlamamız gerekiyor.

2)Http protokolü, rest api, Json, xml konuları
  Bunun sonrasında, rest api best practice'leri konusunda okumalar yapılabilir. Http status kodlarını kesinlikle bilmemiz gerekiyor.
  cryptaway'de bir hata kodu döndüğü zaman onu anlamlandırabilmek için http status kodlarını bilmeye ihtiyacımız var

3)Net Core ile web geliştirme (https://code-maze.com/back-end-stack/)

4)Docker & Docker Compose
 Linux sistemlerde container mimaride çalıştıgımız için, docker nedir, nasıl çalışır, image'lar nasıl oluşturulur, servisler compose'a nasıl eklenir, docker cli nasıl kullanılır, docker network vb konuları bilmemiz gerekiyor.

5)Windows Service Kullanımı
Windows sistemlerde kuruluma aşina olabilmek için, windows servisler nasıl çalışır. ne tarz configler vardır vs bilmemiz gerekiyor.

6)Linux 101 & Bash Komutları
 Linux olmazsa olmaz noktamız. Bunun için de bash komutlarına hakim olmak, linuxta neyi nasıl yaparız bilmemiz gerekiyor. Deamon servis nedir, nasıl eklenir, firewall ayarları nasıl yapılır, disk biçimlendirme nasıl yapılır, paket yöneticileri nasıl kullanılır vb konuları bilmemiz gerekiyor.

7)Database(SQL) 101
 Özellikle kurulumlarda yaşanan sıkıntılarda, database'den dönen hataları anlamlandırmak ve çözüm üretebilmek için database konusuna hakim olmamız gerekiyor.

8)Simetrik, asimetrik şifreleme algoritmaları

9)pkcs11 kullanımı, pkcs11 hata mesajları
 Kriptoloji projelerimizin ana domaini olduğu için, algoritmalar hakkında yeterli bilgiye sahip olmamız gerekiyor. Hangi algoritmada, hangi algoritma ve mekanizmalar kullanılmaktadır vs.
Diğer bir konu ise pkcs'ye aşina olmak. Örneğin cryptaway'de bize hsm'den bir hata döndüğü zaman PKCS hata formatında dönebiliyor. Bu durumda hatayı anlamlandırmak için, hangi hata ne anlama geliyor bilmemiz gerekiyor.

*Cryptaway'de çalışan servislerin, configlerinin incelenmesi. Hangi config ne için kullanılıyor bunun anlaşılması ve öğrenilmesi gerekiyor.

Bu sayede kurulumda bir hata oldugu zaman, servislerin configlerine bakıldıgı zaman hata kolayca anlamlandırılabilir. Bu konuda müsait vakitlerde projenin kodlarını da inceleyebilir, dilerseniz yazılımcı arkadaslara da hangi config ne için kullanılıyor detaylı öğrenmek için sorabilirsiniz. Configlerin her birinde yapılan bir harf hatası kurulum hatalı olmasına sebep vereceğinden, her birinin anlamını bilmek büyük önem arz ediyor.



+--------------------------------------------+---------------------------------------------+
| OID Değeri                                 | Amaç                                        |
+--------------------------------------------+---------------------------------------------+
| NameOID.COUNTRY_NAME                       | Ülke adı                                    |
| NameOID.STATE_OR_PROVINCE_NAME             | Eyalet veya bölge adı                       |
| NameOID.LOCALITY_NAME                      | Yerel alan veya şehir adı                   |
| NameOID.ORGANIZATION_NAME                  | Organizasyon adı                            |
| NameOID.ORGANIZATIONAL_UNIT_NAME           | Organizasyon birimi adı                     |
| NameOID.COMMON_NAME                        | Ortak ad (genellikle kişi veya cihaz adı)  |
| NameOID.GIVEN_NAME                         | Verilen ad                                  |
| NameOID.SURNAME                            | Soyad                                       |
| NameOID.PSEUDONYM                          | Takma ad                                    |
| NameOID.TITLE                              | Unvan veya başlık                           |
| NameOID.ORGANIZATION_IDENTIFIER            | Organizasyon kimliği                       |
| NameOID.DN_QUALIFIER                       | DN belirleyici                              |
| NameOID.COUNTRY_OF_CITIZENSHIP             | Vatandaşlık ülkesi                         |
| NameOID.COUNTRY_OF_RESIDENCE               | İkamet ülkesi                              |
| NameOID.DATE_OF_BIRTH                      | Doğum tarihi                               |
| NameOID.PLACE_OF_BIRTH                     | Doğum yeri                                |
| NameOID.GENDER                             | Cinsiyet                                   |
| NameOID.SERIAL_NUMBER                      | Seri numarası                              |
| NameOID.USER_ID                            | Kullanıcı kimliği                          |
| NameOID.EMAIL_ADDRESS                      | E-posta adresi                             |
| NameOID.STREET_ADDRESS                     | Sokak adresi                              |
| NameOID.UNSTRUCTURED_NAME                  | Yapısız ad                                 |
| NameOID.UNSTRUCTURED_ADDRESS               | Yapısız adres                              |
| NameOID.NAME                               | İsim                                      |
| NameOID.SURNAME_GIVEN_NAME                 | Soyad ve verilen ad                        |
| NameOID.PHONE_NUMBER                       | Telefon numarası                           |
| NameOID.PROFESSION_NAME                    | Meslek adı                                |
| NameOID.IDENTIFIER_REGISTRY                | Tanımlayıcı kayıt                          |
| NameOID.DISTINGUISHED_NAME                 | Ayırt edici ad                            |
| NameOID.PSEUDONYM                          | Takma ad                                  |
| NameOID.ROLE                               | Rol                                       |
| NameOID.MOBILE_PHONE_NUMBER                | Cep telefonu numarası                     |
| NameOID.POSTAL_CODE                        | Posta kodu                                |
| NameOID.BUSINESS_CATEGORY                  | İş kategorisi                             |
| NameOID.TELEPHONE_NUMBER                   | Telefon numarası                           |
| NameOID.FAX_NUMBER                         | Faks numarası                             |
| NameOID.NAME_CONSTRAINTS                   | İsim kısıtlamaları                         |
| NameOID.ADDRESS_POLICY                     | Adres politikası                          |
| NameOID.TARGET_INFORMATION                 | Hedef bilgisi                             |
+--------------------------------------------+---------------------------------------------+
