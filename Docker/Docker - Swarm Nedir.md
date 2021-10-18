## Docker Swarm Nedir?


![](https://github.com/mrtyildiz/Blog-Post/blob/main/Docker/img/Docker_logo.svg.png)

Docker Swarm Temelde container notları oluşturma ve yönetmek amacıyla kullanılmaktadır.
Docker nodelarının loglarının yönetilmesi kolaylık sağlamaktadır. Docker Swarm özelliği 
Docker Engine ile birlikte default olarak yüklenmektedir.

Docker Swarm 'ın öne çıkan özellikleri aşağıdaki gibidir;

* __Cluster management integrated with Docker Engine:__ Docker Engine ile oluşturulan node 'lar yönetilebilir. Yönetimsel işlemler için harici hiçbir yazılıma ihtiyaç bulunmamaktadır.
* __Decentralized Design:__ Oluşuturulan imaj üzerinden birden fazla node 'lar oluşturulmuştur. 
* __Declarative Service Model:__ Bildirimlerin alınması ve sıraya konulması amacıyla kullanışlı bir teknolojidir. Örneğin mesaj kuyruğa alma hizmeti.
* __Scaling:__ Her hizmet için istenilen sayıda node oluşturulabilir. Node sayısı duruma göre büyütülebilir veya küçültülebilir.
* __Desired state reconciliation:__ oluşturulan nodelardan herhangi birinin çökmesi durumunda yerine yeni bir node 'u otomatik olarak oluşturulur.
* __Multi-host networking:__ Nodelara yeni bir ağ tanımlandığında otomatik olarak yeni ağ sistemine uyum göstermeye başlar.
* __Service discovery:__ DNS benzeri hizmetlerin otomatik olarak tanımasına olanak sağlar.
* __Load Balancing:__ Nodelar arasındaki sağlayacağı hizmetin ve dengenin belirlenmesine olanak tanınır.
* __Secure by default:__ Self-signed root sertifikası ve CA kök sertifikasının kullanılmasına imkan sunmaktadır.
* __Rolling updates:__ Herhangi bir sebeten dolayı hata yaşanması durumunda önceki sürüme geri dönülmesine imkan sunmaktadır.



Docker Swarm teknolojisi kullanılır iken temel komutlar aşağıdaki gibidir;

* swarm init
* swarm join

![](https://github.com/mrtyildiz/Blog-Post/blob/main/Docker/img/swarm_scale.PNG?raw=true)

* service create
* service inspect
* service ls
* service rm
* service scale
* service ps
* service update
