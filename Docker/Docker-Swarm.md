# Docker Swarm Kullanımı

## Giriş ve Temel Kavramlar

### Docker Swarm nedir?

Docker Swarm, Docker'ın entegre bir kümelenme ve yönetim aracıdır. Swarm, birden fazla Docker konteynerini tek bir sanal yapıda birleştiren ve yöneten bir araçtır. Bu sayede yüksek kullanılabilirlik, ölçeklendirme ve hata toleransı gibi avantajlar elde edilir. Docker Swarm, konteyner tabanlı uygulamaları büyük ölçekte dağıtmak, yönetmek ve izlemek için kullanılır.

Docker Swarm'ın bazı temel özellikleri şunlardır:

1. **Küme Yönetimi:** Docker Swarm, birden fazla fiziksel veya sanal makineden oluşan bir konteyner kümesi oluşturmanıza olanak tanır. Bu küme içindeki makinelere "Node" denir.

2. **Servis Yönetimi:** Docker Swarm, bir servisi birden fazla konteyner örneği ile çalıştırmak için kullanılır. Bu, uygulamanın yüksek kullanılabilirlik sağlamasına ve ölçeklemesine olanak tanır.

3. **Replica ve Global Modlar:** Swarm, "replica" ve "global" olmak üzere iki farklı modda servislerin çalıştırılmasına izin verir. "Replica" modunda belirli bir sayıda konteyner örneği çalıştırabilirken, "global" modunda her bir Swarm Node üzerinde bir örnek çalıştırabilirsiniz.

4. **Ölçeklendirme ve Yüksek Kullanılabilirlik:** Docker Swarm, servislerinizi ölçeklendirebilir ve daha fazla konteyner örneği başlatabilirsiniz. Eğer bir Node veya konteyner başarısız olursa, Swarm otomatik olarak iş yükünü başka bir sağlıklı Node'a taşıyarak yüksek kullanılabilirlik sağlar.

5. **Servis Güncellemeleri:** Swarm, servislerde güncellemeleri kolayca yönetmenize olanak tanır. Yeni bir konteyner sürümü kullanmak veya yapılandırmaları güncellemek için Swarm'ın güncelleme stratejilerini kullanabilirsiniz.

6. **Overlay Ağları:** Docker Swarm, servisler arasında iletişim sağlamak ve aynı ağı paylaşan konteynerleri izole etmek için "overlay" ağlarını destekler.

7. **Veri Paylaşımı:** Swarm, farklı servisler veya konteynerler arasında veri paylaşımını destekler ve bu sayede uygulama bileşenleri arasında iletişim kurmanızı sağlar.

8. **Güvenlik ve Sertifikalar:** Swarm, iletişimi güvenli hale getirmek için TLS sertifikalarını kullanır ve kümelenmiş ortamlarda güvenlik önlemleri sağlar.

Docker Swarm, konteyner tabanlı uygulamaların kolayca dağıtılmasını, ölçeklendirilmesini ve yönetilmesini sağlayan güçlü bir araçtır.Bu teknolojinin pek çok avantajı ve farklı kullanım senaryosu bulunmaktadır:

**Avantajları:**

1. **Kolay Kullanım:** Docker Swarm, Docker'ın temel yapı taşlarına dayandığı için Docker'ı zaten bilen kullanıcılar için hızlı bir şekilde öğrenilebilir. Mevcut Docker komutlarını ve imajlarını kullanarak Swarm kümesi oluşturmak ve yönetmek kolaydır.

2. **Entegrasyon:** Docker Swarm, Docker Compose gibi diğer Docker araçlarıyla iyi bir şekilde entegre olur. Bu, uygulamanın geliştirme aşamasından dağıtımına kadar olan sürecin daha kolay ve tutarlı olmasını sağlar.

3. **Yüksek Kullanılabilirlik:** Swarm, yüksek kullanılabilirlik gerektiren uygulamalar için ideal bir çözümdür. Birden fazla konteyner örneği çalıştırarak, bir Node veya konteynerin başarısız olması durumunda servisin kesintisiz olarak devam etmesini sağlar.

4. **Ölçeklenebilirlik:** Swarm, uygulamanızın trafik yükü arttığında kolayca ölçeklendirilmesini sağlar. Servis örneklerini artırarak daha fazla talebi karşılayabilirsiniz.

5. **Hızlı Dağıtım:** Swarm, konteyner tabanlı uygulamaların hızlı bir şekilde dağıtılmasını sağlar. Servislerinizi birkaç komutla oluşturabilir ve Swarm, otomatik olarak servislerinizi uygun Swarm Node'larına yerleştirir.

6. **Tek Yönetim Arayüzü:** Swarm, tüm küme yönetimini tek bir arayüz üzerinden gerçekleştirmenizi sağlar. Bu, birden fazla Node'un yönetimini basit ve merkezi bir şekilde yapmanıza yardımcı olur.

**Kullanım Senaryoları:**

1. **Web Uygulamaları:** Swarm, web uygulamalarınızı yüksek kullanılabilirlik ve ölçeklenebilirlik ile dağıtmak için kullanışlıdır. Örneğin, bir e-ticaret platformunu iş yükü arttığında ölçeklendirmek veya hata durumunda kesintisiz hizmet sağlamak için kullanabilirsiniz.

2. **Mikroservis Mimarisi:** Mikroservis tabanlı uygulamaların dağıtımı Swarm ile kolayca yönetilebilir. Farklı mikroservislerinizi farklı konteyner örnekleri olarak çalıştırarak, uygulamanızın farklı bileşenlerini izole edebilirsiniz.

3. **CI/CD Entegrasyonu:** Swarm, sürekli entegrasyon ve sürekli dağıtım (CI/CD) süreçlerini destekler. Kodunuzu güncellediğinizde, Swarm'ın güncelleme stratejilerini kullanarak servislerinizi güncelleyebilirsiniz.

4.** Veri Analitiği ve Big Data:** Swarm, büyük veri analitiği ve işleme için kullanılabilecek konteyner tabanlı platformların oluşturulmasında yardımcı olabilir. Birden fazla veri işleme konteynerını kolayca çalıştırabilir ve yönetebilirsiniz.

5. **Veritabanları ve Veri Depolama:** Swarm, veritabanları gibi stateful (durum taşıyan) uygulamaların dağıtımını da destekler. Overlay ağları ve volume'lar aracılığıyla veritabanı konteynerlarını izole edebilir ve veri depolamanızı yönetebilirsiniz.

6. **Uygulama Geliştirme ve Testi:** Swarm, uygulama geliştirme ve testi sırasında farklı ortamlarda hızlıca konteynerları başlatmanızı sağlar. Bu, geliştirme döngüsünü hızlandırabilir ve uygulamanın farklı senaryolarda nasıl davrandığını test etmenizi kolaylaştırabilir.

Docker Swarm, bu avantajları ve kullanım senaryolarını kullanarak konteyner tabanlı uygulamalarınızı daha etkili bir şekilde yönetmenizi sağlayan güçlü bir araçtır.


### Temel Docker Swarm kavramları
Docker Swarm kullanırken karşılaşacağınız temel kavramlar şunlardır: Node, Service, Task ve Overlay Network.

* **Node:** Bir Docker Swarm kümesinin üyelerine "Node" denir. Bu, fiziksel veya sanal makineler olabilir. Swarm kümesine katılan her bir makine bir Node olarak kabul edilir. Node'lar, Swarm kümesi içinde konteynerlerin çalıştırıldığı ve yönetildiği fiziksel veya sanal işlemcisidir.

* **Service:** Bir "Service" (Servis), benzer özelliklere ve amaca sahip konteynerleri gruplayan mantıksal bir yapıdır. Servis, bir uygulamanın belirli bir parçasını veya hizmetini temsil eder. Örneğin, bir web uygulamasının ön yüzünü veya veritabanını bir servis olarak tanımlayabilirsiniz.

* **Task:** Bir "Task" (Görev), bir servisin belirli bir zamanda çalışan bir konteyner örneğini ifade eder. Servisin belirttiği örnekleme sayısına (replica sayısı veya global mod) bağlı olarak, Docker Swarm otomatik olarak her bir görevi farklı Node'larda çalıştırır. Görevler, servislerin yönetilen durumunun temel yapı taşlarıdır.

* **Overlay Network:** Bir "Overlay Network" (Örtü Ağı), Swarm kümesinin farklı Node'ları arasında konteynerlerin iletişim kurmasını sağlayan mantıksal bir ağdır. Bu ağ, farklı fiziksel veya sanal makinelerde çalışan konteynerlerin sanki aynı fiziksel ağda gibi iletişim kurmalarını sağlar. Overlay ağları, servislerin iletişimini ve veri paylaşımını kolaylaştırır.

Bu temel kavramlar, Docker Swarm kullanırken anlamanız gereken önemli terimlerdir. Bu kavramları kavradığınızda, Docker Swarm'ın nasıl çalıştığını daha iyi anlayabilir ve konteyner tabanlı uygulamalarınızı daha etkili bir şekilde yönetebilirsiniz.

## Swarm Küme Kurulumu

Docker Swarm Kümesi Oluşturma işlemi için aşağıdaki komut kullanılır.

```
docker swarm init
```
![](https://raw.githubusercontent.com/mrtyildiz/Blog-Post/main/Docker/img/Docker-Swarm-1.png)

Oluşturulmuş olan bu kümeye yeni bir node eklemek amacıyla aşağıdaki komut kullanılır.
```
docker swarm join --token <TOKEN> <MANAGER-IP>:<MANAGER-PORT> 
```
![](https://raw.githubusercontent.com/mrtyildiz/Blog-Post/main/Docker/img/Docker-Swarm-2.png)

## Servisleri Yönetmek ve Dağıtmak

Oluşturulmuş olan bu ortam üzerinden yeni bir servis oluşturulması amacıyla aşağıdaki komut kullanılır.
```
docker service create --name myweb --replicas 3 -p 80:80 httpd
```
![](https://raw.githubusercontent.com/mrtyildiz/Blog-Post/main/Docker/img/Docker-Swarm-3.png)

Servis durumunun görüntülenmesi amacıyla aşağıdaki komut kullanılır;
```
docker service ls
```
![](https://raw.githubusercontent.com/mrtyildiz/Blog-Post/main/Docker/img/Docker-Swarm-4.png)

Servisler hakkında detaylı bilgi alınması amacıyla aşağıdaki komut kullanılır;

```
docker service inspect myweb
```
![](https://raw.githubusercontent.com/mrtyildiz/Blog-Post/main/Docker/img/Docker-Swarm-5.png)

Oluşturulmuş servisin ihtiyaç doğrultusunda servis sayısı arttırılabilir veya azaltılabilir;

```
docker service scale myweb=5
```
![](https://raw.githubusercontent.com/mrtyildiz/Blog-Post/main/Docker/img/Docker-Swarm-6.png)

"Global Service" (Küresel Hizmet) terimi, Docker Swarm'da kullanılan bir hizmet modunu ifade eder. Bir "global service" olarak tanımlanan bir hizmet, her Swarm düğümünde otomatik olarak çalıştırılmak üzere ayarlanır. Yani, Swarm kümesinde bulunan her bir düğümde bu hizmetin bir örneği çalışır.

Bu yaklaşım, hizmetin her düğümde otomatik olarak dağıtılması ve ölçeklendirilmesi anlamına gelir. Örneğin, bir veritabanı hizmetini "global service" olarak tanımlarsanız, her Swarm düğümünde bu hizmetin bir kopyası çalışır ve veritabanı hizmeti yüksek kullanılabilirlik ve dağıtım esnekliği sağlar.

Global servis oluşturulması amacıyla aşağıdaki komut kullanılır.
```
docker service create --name logs --mode global linuxserver/syslog-ng
```
![](https://raw.githubusercontent.com/mrtyildiz/Blog-Post/main/Docker/img/Docker-Swarm-7.png)

## Docker Swarm Güncelleme Stratejileri 


### Rolling Update (Yavaşça Güncelleme):

Bu strateji, hizmetinizi yavaşça güncellemenizi sağlar. Mevcut konteynerleri yeni sürümle değiştirirken, belirli bir zaman diliminde azami hizmet kesintisi yaşanmasını engellemek için kullanışlıdır. Bu strateji, belirli bir zaman aralığında adım adım güncelleme yapmanızı sağlar.

Örnek: Bir web uygulaması hizmetinizin yeni bir sürümünü dağıtacaksınız. Şu anda 10 tane çalışan konteyneriniz var ve güncellemeyi %20'lik adımlarla gerçekleştirmeye karar verdiniz. Her adımda 2 konteyneri yeni sürümle değiştirirsiniz. Bu, kullanıcılara kesintisiz hizmet sunmaya yardımcı olur.

Örnek güncelleme komutu;
```
# Hizmeti yavaşça güncelleme komutu
docker service update --update-parallelism 1 --update-delay 10s <servis_adı>
```

### Recreate (Yeniden Oluşturma):
Bu strateji, hizmetin tüm örneklerini aynı anda kapatıp yeni sürümle değiştirmeyi sağlar. Bu nedenle, hizmet kesintisi yaşanabilir ancak işlem hızlıdır. Bu strateji özellikle hızlı güncellemeler gerektiğinde veya yeni sürümle uyumlu olmayan büyük değişiklikler yapılacağında kullanışlı olabilir.

Örnek: Bir mikro servis hizmeti, API'sinde önemli bir değişiklik yapmanız gerekiyor ve bu değişiklik geriye dönük uyumsuzluğa neden olacak. Bu durumda, mevcut tüm konteynerleri kapatıp yeni sürümü hızla devreye alabilirsiniz.

Örnek güncelleme komutu;
```
# Hizmeti yeniden oluşturma komutu
docker service update --force <servis_adı>
```

### Global Service (Küresel Hizmet):
Bu strateji, belirli bir hizmetin her Swarm düğümünde çalışmasını sağlar. Yeni sürümü otomatik olarak tüm düğümlerde devreye alır. Bu strateji, yüksek kullanılabilirlik ve hızlı güncellemeler gerektiğinde kullanışlıdır.

Örnek: Veritabanı hizmetiniz, güncellemeler nedeniyle her düğümde eşzamanlı olarak çalışmalıdır. Bu durumda, "global service" stratejisini kullanarak tüm düğümlerde yeni sürümü otomatik olarak çalıştırabilirsiniz.

Örnek güncelleme komutu;
```
# Küresel hizmeti güncelleme komutu
docker service update --image <yeni_görüntü> <servis_adı>
```

Hali hazırda çalışmakta olan servisin güncellenmesi amacıyla aşağıdaki komut kullanılır

```
docker service update --image new-image:tag webapp
```
![](https://raw.githubusercontent.com/mrtyildiz/Blog-Post/main/Docker/img/Docker-Swarm-8.png)

##  Overlay Ağı Oluşturma İşlemi

Docker Swarm Overlay Ağı, Docker Swarm adı verilen bir dağıtılmış sistemdeki konteynerler arasında iletişim kurmak için kullanılan bir ağ türüdür. Bu ağ, farklı bilgisayarlar üzerindeki konteynerler arasında veri iletişimi ve paylaşımını sağlar. Overlay ağları, otomatik IP yönetimi ve güvenli iletişim gibi özellikler sunarak konteyner tabanlı uygulamaların daha kolay yönetilmesini ve ölçeklendirilmesini sağlar.

```
docker network create -d overlay my-overlay-network
```
![](https://raw.githubusercontent.com/mrtyildiz/Blog-Post/main/Docker/img/Docker-Swarm-9.png)

Oluşturulan servisin yeni oluşturulmuş olan overlay ağına ekleme işlemi aşağıdaki gibidir;
```
docker service create --name app --network my-overlay-network httpd
```
![](https://raw.githubusercontent.com/mrtyildiz/Blog-Post/main/Docker/img/Docker-Swarm-10.png)

## Güvenlik ve Sertifikalar

### Swarm'da güvenlik önlemleri

Docker Swarm, dağıtılmış uygulamaları yönetmek ve çalıştırmak için kullanılan bir platformdur. Bu tür bir ortamda güvenlik büyük önem taşır. İşte Docker Swarm'da alabileceğiniz güvenlik önlemlerinden bazıları:

1. **Güçlü Kimlik Doğrulama ve Yetkilendirme:** Docker Swarm'a erişim sağlayan kullanıcıların güçlü kimlik doğrulama süreçleri ve minimum ayrıcalıklarla sınırlı olması gerekmektedir. İhtiyaca uygun roller ve izinler oluşturarak sadece gerekli erişimleri sağlayın.

2. **TLS Şifrelemesi:** Docker Swarm düğümleri arasındaki iletişimi korumak için TLS (Transport Layer Security) şifrelemesi kullanın. Bu, verilerin güvenli bir şekilde iletilmesini sağlar.

3. **Overlay Ağları ve Güvenli İletişim:** Docker Swarm overlay ağları, konteynerler arasındaki trafiği izole edebilir ve şifreleyebilir. Bu, konteynerler arasındaki güvenli iletişimi sağlar.

4. **Docker İmaj Güvenliği:** Kullanılan Docker imajlarının güvenilir ve güvenli olduğundan emin olun. Resmi Docker deposundan veya güvenilir kaynaklardan imajlar kullanmaya özen gösterin.

5. **Güncellemeleri İzleme ve Yükleme:** Docker Swarm düğümlerinde ve kullanılan imajlarda güvenlik güncellemelerini düzenli olarak takip edin ve yükleyin. Güncel yazılımlar güvenlik açıklarını en aza indirmenize yardımcı olur.

6. **Firewall Ayarları:** Gereksiz ağ trafiğini engellemek ve saldırılara karşı koruma sağlamak için güvenlik duvarları (firewall) kullanın. Sadece gereksinim duyulan portları açık bırakın.

7. **Güvenli Ağ Konfigürasyonu:** Ağ yapılandırmanızı doğru bir şekilde yaparak, iç ve dış ağlardan gelen istenmeyen trafiği engelleyebilirsiniz. İhtiyaca göre ağ segmentasyonu yapmak da önemlidir.

8. **Günlük Kayıtları İzleme:** Docker Swarm düğümlerinin ve hizmetlerinin günlük kayıtlarını izlemek, olası güvenlik ihlallerini ve anormallikleri tespit etmek için önemlidir.

9. **Güvenli Dağıtım:** Uygulama ve hizmet dağıtımı yaparken, imza doğrulaması gibi güvenlik kontrollerini uygulayarak kötü niyetli veya değiştirilmiş imajların kullanımını engelleyin.

10. **Penetrasyon Testleri ve İzleme:** Düzenli olarak penetrasyon testleri yaptırarak sisteminizin güvenliğini değerlendirin. Ayrıca, sürekli izleme araçları kullanarak anormal faaliyetleri ve güvenlik açıklarını tespit edin.

Bu öneriler, Docker Swarm ortamında güvenliği artırmak için başlangıç ​​noktası olabilir. Güvenlik, sürekli bir çaba gerektiren bir konudur, bu yüzden en son güvenlik uygulamalarını takip etmeyi ve sistem güvenliğini sürekli değerlendirmeyi unutmayın.

### TLS sertifikaları ve yönetimi

Docker Swarm'da güvenliği artırmak ve düğümler arasındaki iletişimi korumak için TLS (Transport Layer Security) sertifikaları kullanılır. Bu sertifikalar, düğümler arasındaki güvenli iletişimi sağlar ve yetkisiz erişimlerden korunmanıza yardımcı olur. İşte Docker Swarm TLS sertifikalarını oluşturma ve yönetme süreci hakkında temel adımlar:

1. Root CA (Kök Yetkilendirme Belgesi) Oluşturma:

İlk adım olarak, bir Root CA oluşturmanız gerekiyor. Bu, tüm sertifikaların güvendiği bir kök sertifikadır.
```
openssl genpkey -algorithm RSA -out rootca.key
openssl req -new -key rootca.key -x509 -days 365 -out rootca.crt
```
2. Düğüm Sertifikaları Oluşturma:

Docker Swarm düğümleri için sertifikalar oluşturmanız gerekiyor. Her düğüm için bir çift anahtar ve sertifika oluşturun.

```
openssl genpkey -algorithm RSA -out node-key.pem
openssl req -new -key node-key.pem -out node.csr
openssl x509 -req -in node.csr -CA rootca.crt -CAkey rootca.key -CAcreateserial -out node-cert.pem -days 365
```
3. Swarm Hizmeti İçin Sertifikaları Yükleme:

Düğümler ve hizmetler arasındaki güvenli iletişimi sağlamak için düğümlere ait sertifikaları yüklemeniz gerekecek.

4. Swarm Modunu Güvenceye Alma:

Docker Swarm modunu güvenceye almak için aşağıdaki adımları izleyin:

* Düğümlere ait sertifikaları ilgili dizinlere yükleyin.
* Düğümlerin Docker Swarm'a katılması için "--tlsverify", "--tlscacert", "--tlscert" ve "--tlskey" gibi parametreleri kullanın.
Örnek komut:

```
docker swarm join --token <TOKEN> <MANAGER-IP>:<MANAGER-PORT> \
--tlsverify --tlscacert=/path/to/ca.pem --tlscert=/path/to/cert.pem --tlskey=/path/to/key.pem
```
5. Swarm Hizmetlerini Yönetme:

Yeni hizmetler oluştururken "--endpoint-mode dnsrr" ve "--publish" gibi parametreleri kullanarak güvenli iletişimi sağlayabilirsiniz.

Örnek komut:

```
docker service create --name myservice --endpoint-mode dnsrr --publish mode=host,target=80,published=8080 \
--constraint 'node.labels.type == web' nginx
```
Docker Swarm'da TLS sertifikalarını yönetmek karmaşık olabilir. Bu nedenle, resmi Docker Swarm belgelerini incelemek ve güvenlik en iyi uygulamalarına uymak önemlidir. Bu belgeler, daha ayrıntılı talimatlar ve güvenliği artırmak için daha fazla bilgi sunacaktır.


### Swarm Kümesini Sonlandırma İşlemi

Docker swarm üzerinde servislerin silinmesi amacıyla aşağıdaki komut kulllanılır;

```
docker service rm <Service_Name>
```
![](https://raw.githubusercontent.com/mrtyildiz/Blog-Post/main/Docker/img/Docker-Swarm-11.png)

Docker swarm 'ın tamamının durdurulması amacıyla aşağıdaki komut kullanılır;

```
docker swarm leave --force
```
![](https://raw.githubusercontent.com/mrtyildiz/Blog-Post/main/Docker/img/Docker-Swarm-12.png)
