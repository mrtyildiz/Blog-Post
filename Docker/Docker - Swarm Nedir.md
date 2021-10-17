## Docker Swarm Nedir?


![](https://github.com/mrtyildiz/Blog-Post/blob/main/Docker/img/Docker_logo.svg.png)

Docker Swarm Temelde container notları oluşturma ve yönetmek amacıyla kullanılmaktadır.
Docker nodelarının loglarının yönetilmesi kolaylık sağlamaktadır. Docker Swarm özelliği 
Docker Engine ile birlikte default olarak yüklenmektedir.

Docker Swarm 'ın öne çıkan özellikleri aşağıdaki gibidir;

* Cluster management integrated with Docker Engine: Docker Engine ile oluşturulan node 'lar yönetilebilir. Yönetimsel işlemler için harici hiçbir yazılıma ihtiyaç bulunmamaktadır.
* Decentralized Design: Oluşuturulan imaj üzerinden birden fazla node 'lar oluşturulmuştur. 
* Declarative Service Model: Bildirimlerin alınması ve sıraya konulması amacıyla kullanışlı bir teknolojidir. Örneğin mesaj kuyruğa alma hizmeti.
* Scaling: Her hizmet için istenilen sayıda node oluşturulabilir. Node sayısı duruma göre büyütülebilir veya küçültülebilir.
* Desired state reconciliation: oluşturulan nodelardan herhangi birinin çökmesi durumunda yerine yeni bir node 'u otomatik olarak oluşturulur.
* Multi-host networking: Nodelara yeni bir ağ tanımlandığında otomatik olarak yeni ağ sistemine uyum göstermeye başlar.
* Service discovery: DNS benzeri hizmetlerin otomatik olarak tanımasına olanak sağlar.
* Load Balancing: Nodelar arasındaki sağlayacağı hizmetin ve dengenin belirlenmesine olanak tanınır.
* Secure by default: Self-signed root sertifikası ve CA kök sertifikasının kullanılmasına imkan sunmaktadır.
* Rolling updates: Herhangi bir sebeten dolayı hata yaşanması durumunda önceki sürüme geri dönülmesine imkan sunmaktadır.



Docker Swarm teknolojisi kullanılır iken temel komutlar aşağıdaki gibidir;

* swarm init
* swarm join
* service create
* service inspect
* service ls
* service rm
* service scale
* service ps
* service update
