# Docker – Birinci Bölüm

## Docker Nedir?

Son beş yıl içerisinde BT endüstürisinin herhangi bir yerindeyseniz , büyük olasılıkla konteyner ve konteyner platformu olan Docker’ı duymuşsunuzdur. Docker ve konteynerlar, yazılım geliştirme ve teslimatında çığır açan bir yazılım çalıştırmanın yeni bir yoludur.
 
Docker, geliştirme ekiplerinin her yerde uygulamalar oluşturup yönetmesine ve güvenli hale getirmesine olanak tanıyan yeni bir teknolojidir.
 
Konteyner kavramını açıklamadan Docker’ı açıklamak mümkün değil , bu yüzden konteynerların nasıl çalıştığına bir göz atalım.
Konteyner ve konteynerleştirme neden önemlidir?
Gördüğümüz bu standartları tanımlanmış metal kutucuk olmadan önce lojistik endüstrisi aklında bir sürü problem ve soru vardı;
*Taşımak istediğim ürünüm diğer ürünlerden etkilenecek mi? Daha hafif taşınan ürünler ağırların altında ezilecek mi?
*Birçok farklı ürün var her ürün için farklı farklı taşıma yöntemleri var her ürünüm için ayrı bir araç mı gerekli?
*Ya çuvallarım başka birinin çuvalları ile karışırsa üretim oranım ile teslimat oranım aynı çıkmazsa?
İşte konteynerlar sayesinde bunların hepsi çözüme ulaşmış oldu. Boyutları ve standartları herkes tarafından bilinen bu metal yığınlarının içine istediğiniz gibi kendi ürünlerinizi yerleştirebilirsiniz. İşte Docker da aynı yolu izler.
Docker ve Konteynerlar, yazılım endüstirisinde devrim yarattı ve beş yıl içerisinde bir araç ve platform olarak popülaritesi hızla arttı.

VM (Virtual Machine)
*OS : Tam işletim sistemi
*İzolasyon : Yüksek
*Çalışır hale gelmesi : Dakikalar
*Versiyonlama : Yok
*Kolay paylaşılabilirlik : Düşük
Docker
*OS : Küçültülmüş işletim sistemi imajı
*İzolasyon : Daha düşük
*Çalışır hale gelmesi : Saniyeler
*Versiyonlama : Yüksek
*Kolay paylaşılabilirlik : Yüksek
İki sanallaştırma yaklaşımı açısından bakarsak ikisinin birbirlerine göre avantaj ve dezavantajları mevcut . Ancak , Docker yönünden bakıldığında bazı avantajların kritik olduğunu söyleyebiliriz. 
Bu tabloyu inceledikten sonra artık şu soruyu sorabiliriz “Neden Docker?"

## Neden Docker?
Docker, yazılım teslim ve dağıtımı için sunduğu olanaklar sebebiyle çok fazla popülerdir. Birçok sorun ve verimsizlik durumları konteynerlerla çözülür.
Bu popülaritenin 5 nedeni;
1.Kullanım Kolaylığı
Docker’ın popülaritesinin büyük bir kısmı, kullanımının ne kadar kolay olmasındadır. Docker’ın temelini konteynerların nasıl oluşturulacağını ve yönetileceğini hızlı bir şekilde öğrenebilirsiniz. Docker açık kaynak kodludur , bu nedenle başlamak için tek yapmanız gereken Mac/Windows veya Linux gibi işetim sistemlerine sahip Hyper-V desteğine sahip olan bir bilgisayarınızın olması.
2. Sistemlerin daha hızlı ölçeklendirilmesi
Konteynerlar, veri merkezi operatörlerinin çok daha fazla iş yükünü daha az donanıma sığdırmasına izin verir. Paylaşılan donanım, daha düşük maliyet anlamına gelir. Operatörler bu sayede tasarruf edebilir maliyeti düşürebilirler.
3. Daha iyi yazılım teslimatı
Konteynerları kullanmak , yazılım dağıtımını da verimli hale getirebilir. Konteynerlar portatiftir. Ayrıca tamamen bağımsızdır. Konteynerlar izole edilmiş bir disk birimi içerir. Bu birim, çeşitli ortamlara geliştirilip dağıtıldıkça konteynerla birlikte gider. Yazılım bağımlılıkları(kütüphaneler , çalışma zamanları, vb.) kapla birlikte
gönderilir.
4. Yazılım tanımlı ağ
Docker , yazılım tanımlı ağları destekler. CLI ve Engine , operatörlerin tek bir yönlendiriciye dokunmadan konteynerlar için yalıtılmış ağlar tanımlamasına olanak tanır. Geliştiriciler ve operatörler gelişmişkarmaşık ağlara sahip sistemler tasarlayabilir ve yapılandırma dosyalarında ağları tanımlayabilir. Bu bir güvenlik avantajıdır.
5. Mikro hizmet mimarisinin yükselişi
Mikro hizmetler , genellikle HTTP ve HTTPS üzerinden erişilen basit işlevlerdir. Mikro hizmet mimarisinin yükselişi Docker’ın popülaritesini olumlu yönde etkiledi. Mikro hizmetler bir sistemi bağımsız olarak konuşlandırılabilecek işlevlere böler. Konteynerlar, mikro hizmetler için müthiş makinelerdir.
 
Bir konteyner, diğer işlemlerden izole edilen özel bir işlem türüdür. Konteynerlara başka hiçbir işlemin erişemediği kaynaklar atanır ve bunlara açıkça atanmamış kaynaklara erişemezler.

Docker Engine
Docker Engine, uygulamalarınızı oluşturmak ve kaplamak için açık kaynaklı bir konteyner teknolojisidir. Dockerfile veya “docker-compose.yml” ‘den bilgileri alarak imajları oluşturur ve çalıştırır . Docker CLI üzerinden bir “docker” komutunu kullandığında yapılması gereken işlemleri yapması için Docker Engine ile iletişime geçer.
Docker Compose
Docker Compose, çok kaplamalı Docker uygulamalarını tanımlamak ve çalıştırmak için bir araçtır . Compose ile uygulamanızın hizmetlerini yapılandırmak için bir YAML dosyası kullanırsınız. Ardından, tek bir komutla, tüm hizmetleri yapılandırmanızdan oluşturur ve başlatırsınız. Docker Compose, çoklu mikro servisler , veritabanları ve benzeri bağımlılıklardan oluşan ve yapıların çalıştırılması için kullanılır . “docker-compose.yml”, gerekli olan tüm servisleri tek bir yerden konfigüre etmemize ve hepsini tek bir komut ile oluşturup, çalıştırmamızı sağlar.
Docker Machine
Docker Machİne, sanal ana bilgisayarlara Docker Engine’i yüklemenizi ve ana bilgisayarları “docker-machine” komutlarıyla yönetmenizi sağlayan bir araçtır. Docker, içerisinde birden fazla Docker Engine motoru yönetilebilir. Docker Machine, Docker Engine’i uzaktaki yer alan makinelerine yüklemenize ve kendi bilgisayarınızdan, uzaktaki yer alan Docker Engine motorunu yönetilmesini sağlar.
Docker Swarm
Docker Swarm, Docker platformu için konteyner orkestrason aracıdır. Veritabanı, uygulama sunucuları, web sunucuları gibi bileşenlerden oluşan büyük kapsama sahip uygulamalarınızı Docker Swarm ile yönetebilir, yük altında kolaylıkla ölçekleme yapılabilmektedir.

## Docker Nasıl Çalışır?
## Docker Nerede Kullanılır?

| 	 Komut       | Açıklama     |
| :------------- | :----------: |
|  docker images | Lokal registry’de mevcut bulunan Image’ları listeler  |
| docker ps	     | Halihazırda çalışmakta olan Container’ları listeler |
|docker ps -a|Docker Daemon üzerindeki bütün Container’ları listeler|
|docker ps -aq|Docker Daemon üzerindeki bütün Container’ların ID’lerini listeler|
|docker pull <repository_name>/<image_name>:<image_tag>|Belirtilen Image’ı lokal registry’ye indirir. Örnek: docker pull gsengun/jmeter3.0:1.7|
|docker top <container_id>|İlgili Container’da top komutunu çalıştırarak çıktısını gösterir|
|docker run -it <image_id/image_name> CMD|Verilen Image’dan terminal’i attach ederek bir Container oluşturur|
|docker pause <container_id>|İlgili Container’ı duraklatır|
|docker unpause <container_id>|İlgili Container pause ile duraklatılmış ise çalışmasına devam ettirilir|
|docker stop <container_id>|İlgili Container’ı durdurur|
|docker start <container_id>|İlgili Container’ı durdurulmuşsa tekrar başlatır|
|docker rm <container_id>|İlgili Container’ı kaldırır fakat ilişkili Volume’lara dokunmaz|
|docker rm -v <container_id>|İlgili Container’ı ilişkili Volume’lar ile birlikte kaldırır|
|docker rm -f <container_id>|İlgili Container’ı zorlayarak kaldırır. Çalışan bir Container ancak -f ile kaldırılabilir|
|docker rmi <image_id/image_name>|İlgili Image’ı siler|
|docker rmi -f <image_id/image_name>|İlgili Image’ı zorlayarak kaldırır, başka isimlerle Tag’lenmiş Image’lar -f ile kaldırılabilir|
|docker info|Docker Daemon’la ilgili özet bilgiler verir|
|docker inspect <container_id>|İlgili Container’la ilgili detaylı bilgiler verir|
|docker inspect <image_id/image_name>|İlgili Image’la ilgili detaylı bilgiler verir|
|docker rm $(docker ps -aq)|Bütün Container’ları kaldırır|
|docker stop $(docker ps -aq)|	Çalışan bütün Container’ları durdurur|
|docker rmi $(docker images -aq)|	Bütün Image’ları kaldırır|
|docker images -q -f dangling=true|Dangling (taglenmemiş ve bir Container ile ilişkilendirilmemiş) Image’ları listeler|
|docker rmi $(docker images -q -f dangling=true)|Dangling Image’ları kaldırır|
|docker volume ls -f dangling=true|Dangling Volume’ları listeler|
|docker volume rm $(docker volume ls -f dangling=true -q)|Danling Volume’ları kaldırır|
|docker logs <container_id>|İlgili Container’ın terminalinde o ana kadar oluşan çıktıyı gösterir|
|docker logs -f <container_id>|	İlgili Container’ın terminalinde o ana kadar oluşan çıktıyı gösterir ve -f follow parametresi ile o andan sonra oluşan logları da göstermeye devam eder|
|docker exec <container_id> <command>|Çalışan bir Container içinde bir komut koşturmak için kullanılır|
|docker exec -it <container_id> /bin/bash|Çalışan bir Container içinde terminal açmak için kullanılır. İlgili Image’da /bin/bash bulunduğu varsayımı ile|
|docker attach <container_id>|Önceden detached modda -d başlatılan bir Container’a attach olmak için kullanılır|

https://www.argenova.com.tr/docker-nedir-ve-nasil-kullanilir
