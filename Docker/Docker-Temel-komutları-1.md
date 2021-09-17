# Docker Temel komutları - Part-1

Docker işletim sistemlerinin imahını kullanarak sadece tek bir servisin üzerinde çalışmasına izin veren sanallaştırma teknolojisidir. Docker mimarisindeki temel amaç yazılım geliştiricilerinin çalışabilecekleri alanın sağlanması ve daha sağlıklı bir şekilde kod geliştirilmesine olanak sunmaktadır.  Docker Windows ve Linux sistemlerde çalışabilmaktadır. Bunun yanı sıra Linux sistemlerde kullanılması tavsiye edilmektedir. 
Windows ortamında Docker kullanmak isteyenlerin wsl yüklenmesi önerilmektedir.


## DockerBasic Commands
* docker

docker --help komutuyla birebir olarak aynı işlevde kullanılabilir. "docker" komutu ile kullanılabilecek parametrelerin görülmesine olanak vermektedir.

![](https://github.com/mrtyildiz/Blog-Post/blob/main/Docker/img/docker.PNG?raw=true)

* docker version

İşletim sistemi üzerine yüklü olan Docker'ın versiyonunun öğrenilmesi amacıyla kullanılır.
![](https://github.com/mrtyildiz/Blog-Post/blob/main/Docker/img/docker.PNG?raw=true)


* docker info

Docker o andaki durumunun öğrenilmesi yani üzerinde kaç tane Container bulunmakta bunların durumları hakkında sayısal olarak bilgi edinmesini sağlamaktadır.
![](https://github.com/mrtyildiz/Blog-Post/blob/main/Docker/img/docker-info.PNG?raw=true)


* docker pull

https://hub.docker.com/ adresinde bulunan imajların kendi makinemize indirmemiz sağlayan komuttur. Görselde görüldüğü gibi nginx imajının kendi makinemize indirilmesini sağlamaktadır.
![](https://github.com/mrtyildiz/Blog-Post/blob/main/Docker/img/docker-pull.PNG?raw=true)

* docker build

docker build komutu dockerfile içerisinde oluşturduğumuz özel imajın oluşturulmasına imkan sunan docker docker komutudur.

* docker run

docker run komutu imaj biçiminde olan docker makinesinin çalıştırılmasını imkan sunmaktadır. aşağıdaki görselde nginx makine çalıştırılmış ve -p parametesi kullanılarak 80 portu üzerinde dışarı ulaşılmasına imkan sunulmuştur.
Çalıştırılan docker containerın arka planda çalışması amacıyla -d parametresi kullanılmıştır.

![](https://github.com/mrtyildiz/Blog-Post/blob/main/Docker/img/docker-run.PNG?raw=true)

* docker commit 
* docker ps

Docker ps komutu kullanılarak çalışır durumda olan docker containerları listelenmesi sağlanır.
![](https://github.com/mrtyildiz/Blog-Post/blob/main/Docker/img/docker-ps.PNG?raw=true)

* docker start


docker start komutu ile durdurulmuş olan docker containerın yeniden çalıştırılmasına imkan sunmaktadır.
* docker stop


Çalışır durumda olan docker containerın durdurulmasına imkan sunmaktadır.
![](https://github.com/mrtyildiz/Blog-Post/blob/main/Docker/img/docker-start.PNG?raw=true)

* docker logs

Belirtilen Container-ID 'sindeki makinanın loglarının görülmesine imkan sunmaktadır.

![](https://github.com/mrtyildiz/Blog-Post/blob/main/Docker/img/docker-logs.PNG?raw=true)

* docker rename

Docker üzerinde bulunan containerın adının değiştirilmesi amacıyla kullanılan komuttur.

![](https://github.com/mrtyildiz/Blog-Post/blob/main/Docker/img/docker-rename.PNG?raw=true)

* docker rm

Docker üzerinde çalışır durumda olmayan containerların silinmesine olanak sağlayan komuttur.

![](https://github.com/mrtyildiz/Blog-Post/blob/main/Docker/img/docker-rm.PNG?raw=true)


## Docker Logs And Monitoring Commands
* docker ps -a
Docker üzerinde çalışan ve çalışmayan bütün containerların görüntülenmesini sağlamaktadır.

![](https://github.com/mrtyildiz/Blog-Post/blob/main/Docker/img/docker-ps-a.PNG?raw=true)

* docker events

Sunucu üzerinde gerçekleşen işlemleri gerçek zamanlı olarak görülmesine imkan sunan komuttur.

![](https://github.com/mrtyildiz/Blog-Post/blob/main/Docker/img/docker-events.PNG?raw=true)

* docker top

Belirtilen docker container içerisinde çalışan processlerin görülmesine olanak sağlayan docker komutudur.

![](https://github.com/mrtyildiz/Blog-Post/blob/main/Docker/img/docker-top.PNG?raw=true)

* docker stats

Çalışan containerların ne düzelde ram ve CPU kullandığını öğrenmek amacıyla kullanılan komuttur.

![](https://github.com/mrtyildiz/Blog-Post/blob/main/Docker/img/docker-stats.PNG?raw=true)

* docker port

Docker Container üzerinde kullanılan port adresinin görüntülenmesi amacıyla kullanılan komuttur.

![](https://github.com/mrtyildiz/Blog-Post/blob/main/Docker/img/docker-port.PNG?raw=true)

## Docker Volume Commands

Birimler, Docker kapsayıcıları tarafından oluşturulan ve kullanılan kalıcı veriler için tercih edilen mekanizmadır. Bağlama bağlamaları, ana makinenin dizin yapısına ve işletim sistemine bağlı olsa da, birimler tamamen Docker tarafından yönetilir. Birimlerin bağlama bağlamalarına göre çeşitli avantajları vardır:

    ** Birimlerin yedeklenmesi veya taşınması, bağlama bağlamalarına göre daha kolaydır.
    * Docker CLI komutlarını veya Docker API'sini kullanarak birimleri yönetebilirsiniz.
    * Birimler hem Linux hem de Windows kapsayıcılarında çalışır.
    * Hacimler, birden çok kapsayıcı arasında daha güvenli bir şekilde paylaşılabilir.
    * Birim sürücüleri, birimlerin içeriğini şifrelemek veya başka işlevler eklemek için birimleri uzak ana bilgisayarlarda veya bulut sağlayıcılarında depolamanıza olanak tanır.
    * Yeni ciltlerin içeriği bir kapsayıcı tarafından önceden doldurulabilir.
    * Docker Desktop'taki birimler, Mac ve Windows ana bilgisayarlarından bind mount'lardan çok daha yüksek performansa sahiptir.
docker volume kullanımı için kullanılabilecek komutlar aşağıdaki gibidir;
* docker volume create
* docker volume inspect
* docker volume rm

![](https://github.com/mrtyildiz/Blog-Post/blob/main/Docker/img/docker-volume.PNG?raw=true)

## Docker Container Commands

* docker exec

docker container üzerinde istenilen komutun çalıştırılmasına imkan sağlayan docker komutudur.

![](https://github.com/mrtyildiz/Blog-Post/blob/main/Docker/img/docker-exec.PNG?raw=true)

* docker inspect

Docker Containerlarının birçok temel bilgisinin görülmesine imkan sununan dokcer komutudur.

![](https://github.com/mrtyildiz/Blog-Post/blob/main/Docker/img/docker-inspect.PNG?raw=true)


* docker kill

Docker containerın durdurulmasını sağlamaktadır.

![](https://github.com/mrtyildiz/Blog-Post/blob/main/Docker/img/docker-kill.PNG?raw=true)

* docker cp

Gerek container içerisinde ana makinaya gerek ise ana makinadan container makinaya dosya kopyalama işlemi için kullanılmaktadır.

![](https://github.com/mrtyildiz/Blog-Post/blob/main/Docker/img/docker-cp.PNG?raw=true)

## DockerLifecycle Commands

Docker üzerinde containerı durdurulabilir ve yeniden çalıştırılabilir. Bu şekilde container çalışması kapatılmasına gerek kalmadan durdurulabilmektedir.

![](https://github.com/mrtyildiz/Blog-Post/blob/main/Docker/img/docker-pause.PNG?raw=true)

* docker pause
* docker unpause
* docker restart
* docker wait
