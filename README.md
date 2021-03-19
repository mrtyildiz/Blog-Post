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
