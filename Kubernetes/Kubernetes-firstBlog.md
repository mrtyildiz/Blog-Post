## Kubernetes 'e Giriş

Kubernetes, Docker Containerlerı için orkestra hizmeti sağlayan açık haynaklı sistemdir. Google tarafından desteklenen ve kullanılan bir sistemdir. Kubernetes manuel olarak gerçekleştirilen süreçleri ortadan kaldırarak süreçlerin otomatize hale getirilmesi hale getirilmektedir. Containerlarının durumunu yönetmek için;
* Belirli Nodes 'ların başlatılması
* Herhangi bir neden duran Container 'ların yeniden başlatılması
* Container 'ların başka bir node taşınması

Kubernetes sisteminin özellikleri aşağıdaki gibidir;
## Features of Kubernetes
* __Automated Scheduling(Otomatik Zamanlama)__: Kubernetes, kaynak gereksinimlerine ve kısıtlamalarına göre Node veya Cluster Node düzeyinde zamanlayıcı sağlamaktadır.
* __Healing Capabilities(İyileştirme Yetenekleri)__:  Kubernetes, herhangi bir nedenden dolayı Nodes durduğunda containerın yeniden planlamasına olanak tanımaktadır.
* __Auto Upgrade and RollBack(Otomatik Yükseltme ve Geri Alma)__: Kubernetes üzerinde güncelleme ve geri alma işlemlerin olası yanlışlıklar veya ihtiyaçlardan dolayı yapılabilmektedir.
* __Horizontal Scaling(Yatay Ölçeklendirme)__: Kubernetes mimarisi gereği yatay ölçekte küçültülebilir veya büyütülebilir.
* __Storage Orchestration(Depolama Orkestrasyon)__: Kubernetes mimarisine isteğimiz zaman sisteme yeni bir disk eklenebilir. Bu disk yerelde bulunabileceği gibi cloud üzerinden sağlanabilir.
* __Secret & Configuration Management(Gizli Anahtar ve Yapılandırma Yönetimi)__: Kubernetes, imajın deploy edilmesi ve stack yapılandırılması secret keylerin dağıtılmasına ve güncellemenize yardımcı olmaktadır.

Kubernetes 'in çalışabileceği yerler;
* On-Premise(Own DataCenter- Kendi veri merkezimiz)
* Public Cloud(Google, AWS, Azure, DigitalOcean)

## Kubernetes Mimarisi
## Kubernetes Architecture
* Kubernetes mimarisi gereği Master ve Slave(worker) Nodeları bulunmaktadır.
* Master Node: Kubernetes mimarisinde bütün yönetim işlemlerine sahip node'tur. Tüm işlevsel için başlangıç noktasıdır.
* Burada kubernetes mimarisinde önemli bir not olarak kubernetes çoklu master yapısına sahip olabilmektedir.
![](https://github.com/mrtyildiz/Blog-Post/blob/main/Kubernetes/img/2.png?raw=true)

* API Server: Kubernetes içerisinde yönetim için kullanılan bir REST API 'dir
* Kubernetes giriş noktasıdır.

![](https://github.com/mrtyildiz/Blog-Post/blob/main/Kubernetes/img/3.png?raw=true)

* ETCD: Cluster mimarisinde keyvalue store işlemi için kullanılmaktadır. Kubernetes'de Back-End kullanılmaktadır.
* Cluster State(Durumu) ilgili verilerin HA olarak kullanılabilirlğini sağlamaktadır.

![](https://github.com/mrtyildiz/Blog-Post/blob/main/Kubernetes/img/4.png?raw=true)

* Scheduler: Slave node 'un görevlerini düzenler. Her bağımlı olan her slave node 'un kaynak kullanım bilgilerini depolamaktadır.

![](https://github.com/mrtyildiz/Blog-Post/blob/main/Kubernetes/img/5.png?raw=true)

* Controller: Tek işlemde birden çok Controller çalıştırır
* Kubernetes ile otomatik hale getirilen tasklar(görevler) oluşturulabilmektedir.

![](https://github.com/mrtyildiz/Blog-Post/blob/main/Kubernetes/img/6.png?raw=true)

### Kubernetes İçerisinde Var Olan Kavramlar

* __Worker Node__: Yönetici node olarak görülebilir. Sanal veya fiziksel bir sunucu olabilir. Worker node 'un ana görevleri arasında ağı yönetmek, nodelar arasında iletişim kurmak vb hizmetleri içermektedir.
* __Kubelet__: Worker nodes 'ların çalışmasını sağlayan kubernetes aracıdır.Kubelet, API sunucusundan bir Pod yapılandırmasını alır ve açıklanan kapsayıcıların çalışır durumda olmasını sağlar.
* __Pods__: Kubernetes üzerinde belirli kurallara uygun olarak çalıştırılan containers 'lara verilen addır. Tek bir Container olarak çalışabileceği gibi çoklu container olarak da çalışabilmektedir.
* __Kube-Proxy__: worker-nodelar arasındaki load balancer hizmeti sağlamaktadır. Bu sayede ana network ile kubernetes ağaı arasında bağlantı sağlamaktadır.

### Kubernetes Kurulumu

Kubernetes kuruumu birkaç farklı kurulum adımlarından oluşmaktadır. Bu adımlar aşağıdaki gibidir;
1. Docker CE Edition Kurulumu
2. KubeCtl komutunun kurulumu
3. MiniKube kurulumu

#### Docker CE Edition Kurulumu
Docker CE kurulumu için aşağıdaki adımların izlenmesi gerekmektedir.
1. Var ise eski versionların kaldırılması/silinmesi için aşağıdaki komut kullanılmaktadır;
   * sudo apt-get remove docker docker-engine docker.io containerd runc
2. Sistemin güncellenmesi amaçıyla aşağıdaki komut kullanılmaktadır;
   * sudo apt-get update
![](https://github.com/mrtyildiz/Blog-Post/blob/main/Kubernetes/img/7.png?raw=true)

Gerekli olan thrid parth programların yüklenmesi amacıyla aşağıdaki komut kullanılır.
* sudo apt-get install apt-transport-https ca-certificates curl gnupg lsb-release
![](https://github.com/mrtyildiz/Blog-Post/blob/main/Kubernetes/img/8.png?raw=true)

3. Docker için GPG key eklenir.
* curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
4. deb paketinin eklenmesi amaçıyla aşağıdaki komut kullanılmaktadır.

* echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \ $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
5. Eklenen paketlerin yüklenmesi amacıyla sisten update edilir ve docker indirilir.
* sudo apt-get update
* sudo apt-get install docker-ce docker-ce-cli containerd.io
![](https://github.com/mrtyildiz/Blog-Post/blob/main/Kubernetes/img/9.png?raw=true)
6. Yüklenmiş olan docker 'ın versionun görülmesi amaçıyla aşağıdaki komut kullanılır.
* docker --version
![](https://github.com/mrtyildiz/Blog-Post/blob/main/Kubernetes/img/10.png?raw=true)
#### KubeCtl Kurulumu

Kullanılmakta olan işletim sistemine uygun kubectl 'ib indirilmesi amacıyla aşağıdaki komutlar sırasıyla kullanılmaktadır. 
* curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
* sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
* kubectl version --client
![](https://github.com/mrtyildiz/Blog-Post/blob/main/Kubernetes/img/11.png?raw=true)

### Minikube Kurulumu 
Kullanılmakta olan işletim sistemine uygun minikube 'ün indirilmesi amacıyla aşağıdaki komutlar sırasıyla kullanılmaktadır. 
* curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
* chmod +x minikube-linux-amd64
* sudo install minikube-linux-amd64 /usr/local/bin/minikube
* minikube version
![](https://github.com/mrtyildiz/Blog-Post/blob/main/Kubernetes/img/12.png?raw=true)

Yüklenmiş olan minikube çalıştırılması amacıyla aşağıdaki komutlar kullanılır.
* sudo apt install conntrack
* sudo minikube start --vm-driver=none
![](https://github.com/mrtyildiz/Blog-Post/blob/main/Kubernetes/img/13.png?raw=true)

Minikube çalıştırıldığında sistemde bulunan Cluster bilgilerinin görüntülenmesi amacıyla;
* kubectl config view
![](https://github.com/mrtyildiz/Blog-Post/blob/main/Kubernetes/img/14.png?raw=true)

#### Kubectl Komutları

Kubectl kullanımın anlaşılması ve öğrenilmesi amacıyla aşağıdaki komutları kullanılabilmektedir. kubectl create komutu kullanılarak yeni pod 'u yöneten Deployment oluşturmak için kullanılmaktadır.
* kubectl create deployment hello-node --image=k8s.gcr.io/echoserver:1.4
Oluşturulmuş olan deployments görüntülenmesi amacıyla kullanılan komut;
* kubectl get deployments
Oluşturulmuş olan pods 'un görüntülenmesi amacıyla kullanılan komut;
* kubectl get pods
![](https://github.com/mrtyildiz/Blog-Post/blob/main/Kubernetes/img/15.png?raw=true)

Kubectl expose komutu kullanılarak uzaktan podları ulaşılabilir hale gelmektedir. --type parametresi kullanılarak kullanmak isteğimiz türü belirtebilmekteyiz. Aşağıdaki örnek loadbalancer olarak seçilmiştir.
* kubectl expose deployment hello-node --type=LoadBalancer --port=8080
Oluşturmuş olduğumuz servis'in görüntülenmesi amacıyla;
* minikube service hello-node
![](https://github.com/mrtyildiz/Blog-Post/blob/main/Kubernetes/img/16.png?raw=true)

Oluşturmuş olduğumuz uygulamanın silinmesi/kaldırılması amacıyla;
Servisin silinmesi amacıyla;
* kubectl delete service hello-node
Oluşturulmuş olan deployment 'ın silinmesi amacıyla;
* kubectl delete deployment hello-node
![](https://github.com/mrtyildiz/Blog-Post/blob/main/Kubernetes/img/17.png?raw=true)

#### Kubernetes 'te NameSpace kavramı

NameSpaces kubernetes ortamında sanal cluster oluşturmamızı sağlanayan yapılardır. Bu sayede podlar ve containerların organize edilmesi konusunda yardımcı olmaktadır. Örnek NameSpaces komutları aşağıdaki gibidir;
NameSpaces 'lerin listelenmesi amacıyla;
* kubectl get namespaces
Belirtilen NameSpace 'deki podların listelenmesi amacıyla;
* kubectl get pods - -namespace <namespace>
Yeni bir NameSpace oluşturulması amacıyla;
* kubectl create namespace <namespace>
![](https://github.com/mrtyildiz/Blog-Post/blob/main/Kubernetes/img/18.png?raw=true)
