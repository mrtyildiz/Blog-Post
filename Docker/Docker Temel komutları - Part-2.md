## Docker Temel komutları - Part-2

## Docker Image Commands
Docker üzerinde çalışan imajların taginin değiştirilmesi amacıyla kullanılan komuttur.
* docker tag

![](https://github.com/mrtyildiz/Blog-Post/blob/main/Docker/img/docker-tag.PNG?raw=true)

Docker üzerinde docker pull komutu ile indirilen imagesların görüntülenmesi amacıyla kullanılan komuttur.

* docker images


![](https://github.com/mrtyildiz/Blog-Post/blob/main/Docker/img/docker-images.PNG?raw=true)

Docker üzerinde özel olarak hazırladığımız olan imageların web sitesine upload edilmesine imkan sunmaktadır.

* docker push

![](https://github.com/mrtyildiz/Blog-Post/blob/main/Docker/img/docker-push.PNG?raw=true)

Docker üzerinde önceden çalıştırılmış komutların görüntülenmesi amacıyla kullanılan komuttur;

* docker history

![](https://github.com/mrtyildiz/Blog-Post/blob/main/Docker/img/docker-history.PNG?raw=true)

Çalıştırılan container .tar uzantısında image dosyasının oluşturulmasına imkan sunmaktadır.

* docker save

![](https://github.com/mrtyildiz/Blog-Post/blob/main/Docker/img/docker-save.PNG?raw=true)

Docker üzerinde çalışan çalışan containerın export/import işlemleri aşağıdaki komutlar kullanılır.

* docker import
* docker export

![](https://github.com/mrtyildiz/Blog-Post/blob/main/Docker/img/docker-import-export.PNG?raw=true)

Docker save komutu ile oluşturulmuş image 'ın docker içerisine aktarılmasına imkan sunmaktadır.

* docker load

docker üzerinde var olan imagelardan her hangi birinin silinmesi amacıyla kullanılan docker komutudur.

* docker rmi

![](https://github.com/mrtyildiz/Blog-Post/blob/main/Docker/img/docker-rmi.PNG?raw=true)


## Docker Networking Commands

Docker üzerinde yeni bir sana NIC (Network) oluşturulması amacıyla kullanılır
* docker network create

![](https://github.com/mrtyildiz/Blog-Post/blob/main/Docker/img/docker-network-inspect.PNG?raw=true)

Docker üzerinde kurulum sonrasında yüklenen ve daha sonrasında oluşturulan bütün docker networklerinin görüntülenmesine olanak sunmaktadır.
* docker network ls

![](https://github.com/mrtyildiz/Blog-Post/blob/main/Docker/img/docker-network-inspect.PNG?raw=true)

Docker üzerinde var olan networklerin özelliklerinin görüntülenmesi amacıyla docker inspect komutu kullanılır.
* docker network inspect

![](https://github.com/mrtyildiz/Blog-Post/blob/main/Docker/img/docker-network-inspect.PNG?raw=true)
