# Docker – Birinci Bölüm

## Docker Nedir?

![image](https://github.com/mrtyildiz/Blog-Post/blob/main/Docker/img/Docker_logo.svg.png)
Docker Konteyner teknolojisini kullanarak yazılım geliştirme teknolojisinde kullanılmaya başlayan yeni bir teknolojidir.
Docker, yazılım geliştirme ekiplerinin her yerde uygulamaların oluşturulmasına ve yönetilmesini daha güvenli hale gelmesine olanak sağlamaktadır.

Docker teknolojisindeki temel mantık konteyner teknolojisinden gelmektedir. Bu mantığa uygun olarak oluşturulan konteynerlar tek bir işin yapılması için oluşturulur.
örneğin bir apache konteyner oluşturulduğunda sadece o konteyner apache server olarak kullanılmaktadır.
Sanallaştırma mantığını uygun oluşturulan konteynerlar arasında iç bir network oluşturmak münkündür.
Bu durum konteylar oluşuturularak kodun çalıştırılacağı oluşturulması ve istendiği zaman farklı ortamlarda yeniden kullanılmasına hazır hale getirmektedir.

Docker 'ın temelde konteyner mantığına dayandığını söyledik peki bu durum diğer sanallaştırma teknolojisine göre bize sağladığı ayrıcalıklar nelerdir?
Docker 'ın bize sağlamış olduğu faydalar aşağıdaki gibidir;
 * Klasik sanallaştırma teknolojilerinde tam bir işletim sistemi kullanılmaktadır. Docker 'da ise küçültülmüş bir imaj kullanılmaktadır.
 * Kurulum maliyeti klasik sanallaştırma teknolojilerinde dakikalardadır. Docker bu durum saniyelere kadar düşürülmüştür.
 * Paylaşılabilirlik/Taşınabilirlik konusunda ise Docker konteyner yapısına sahip olduğu için öne çıkmaktadır.


## Neden Docker?
Docker teknolojisinin popülerleşmesinin nedenleri arasında birçok sorun ve verimsizlik durumlarına konteyner teknolojisi çözüm sunmasıdır.
Docker 'ın popülaritesinin nedenlerini aşağıdaki gibi sıralayabiliriz;

* Docker öğrenilmesi kolay bir yapıya sahiptir. Bunun yanı sıra açık kaynak olması ile Docker kullanmak için tek ihtiyaçınız olan Hyper-V desteğine sahip olan bir bilgisayardır.

* Docker Konteyner teknolojisine sahip olması sayesinde daha düşük donanımlar üzerinde çalışabilmektedir. Bu sayede ciddi bir tasarruf sağlanabilmekte ve maliyet düşürülebilmektedir.

* Yazlımlar için uygun bir test ortamlarını oluşturulmasına ve bu ortamların istenildiğinde taşına bilmesine olanak tanır.

* Docker Yazılım tabanlı ağlarını (SDN) desteklemektedir. CLI ve Engine, yönlendiricilere dokunmadan konteynerlar için yalıtılmış ağlar tanımlamasına olanak sağlamaktadır. Bu ağ yapısı yapılandırma dosyaları ile tanımlanabilmektedir. Bu güvenlik için önemli bir avantajdır.

* Mikro hizmet mimarisine uygun olarak çalışması docker popülerliğini olumlu yönde etkilemiştir.

Docker kullanımında bilinmesi gereken kavramlar aşağıdaki gibidir;

* Docker Engine, açık kaynaklı bir konteyner teknolojisidir. Dockerfile veya docker-compose.yml 'den alınan bilgiler doğrultusunda imajlar oluşturulur ve çalıştırılır. Docker CLI üzerinden bir "docker" komutu kullanıldığında yapılması gereken işlemlerin yapılması için Docker engine ile iletişime geçer.

* Docker Compose, çoklu mikromimariye sahip olan yapıların kurulmasına olanak sağlayan docker teknolojisidir. "docker-compose.yml" dosyası ile tüm servislerin conteynerların tek yerden konfigüre etmemize olanak sağlar.
* Docker Machine, sanal ana bilgisayarlara Docker Engine’i yüklemenizi ve ana bilgisayarları “docker-machine” komutlarıyla yönetmenizi sağlayan bir araçtır. Docker, içerisinde birden fazla Docker Engine motoru yönetilebilir.
* Docker Swarm, konteyner orkestrasyon aracıdır. Büyük kapsama sahip olan olan uygulamaları Docker Swarm ile yönetilir kolaylıkla ölçeklenebilir.

Docker kullanımın da işinize yarayabilecek docker komutları aşağıdaki gibidir.

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
