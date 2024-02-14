# 6 Must Know Software Architectural Patterns

## Event-Driven Architecture
Event-Driven Architecture (EDA), bir yazılım mimarisi modelidir ve sistemlerin, uygulamaların veya hizmetlerin, bir olayın gerçekleşmesine yanıt olarak birbirleriyle iletişim kurmasını sağlar. Bu mimari model, özellikle gerçek zamanlı veri işleme ve asenkron iletişim gereksinimlerinin olduğu durumlar için uygundur. EDA, olayları temel alır ve bu olayların sistem içerisinde veya sistemler arasında iletilmesi, algılanması ve işlenmesine dayanır.

#### Temel Kavramlar
* **Olay (Event):** Bir durum değişikliğini temsil eden ve bir hizmetin, uygulamanın veya sistem bileşeninin ürettiği veri parçasıdır. Örneğin, bir ürünün stoktan düşmesi veya bir kullanıcının sisteme giriş yapması bir olay olabilir.
* **Olay Üreticisi (Event Producer):** Olayları yaratan ve bunları bir olay kanalı üzerinden ileten bileşen.
* **Olay Kanalı (Event Channel):** Üreticilerin olayları yayınladığı ve tüketicilerin bu olayları dinlediği ara katmandır.
* **Olay Tüketicisi (Event Consumer):** Olayları dinleyen ve bunlara yanıt olarak belirli işlemleri gerçekleştiren bileşen.

#### Avantajları

* **Esneklik ve Ölçeklenebilirlik:** Sistem bileşenleri arasındaki gevşek bağlantı, bileşenlerin bağımsız olarak geliştirilmesine, dağıtılmasına ve ölçeklendirilmesine olanak tanır.
* **Reaktif Sistemler:** Olaylara hızlı bir şekilde yanıt vermek, sistemlerin daha reaktif olmasını sağlar. Bu, kullanıcı deneyimini iyileştirebilir ve gerçek zamanlı veri işleme ihtiyaçlarını karşılar.
* **Asenkron İletişim:** Bileşenler arasındaki asenkron iletişim, sistem kaynaklarının daha etkin kullanılmasını sağlar ve bloklama işlemlerinin azaltılmasına yardımcı olur.

#### Uygulama Senaryoları

* **Mikroservis Mimarileri:** Mikroservisler arasındaki iletişimde olay tabanlı mesajlaşma kullanılabilir. Bu, servislerin bağımsız olarak geliştirilmesini ve yönetilmesini kolaylaştırır.

* **Gerçek Zamanlı Veri İşleme:** Finans, oyun, sosyal medya gibi alanlarda kullanıcı etkileşimleri veya piyasa hareketleri gibi olayların gerçek zamanlı olarak işlenmesi gerekebilir.

* **IoT Sistemleri:** İnternet üzerinden bağlı cihazlar arasındaki etkileşimler, olay tabanlı mimariler kullanılarak etkin bir şekilde yönetilebilir.

#### Zorluklar

* **Olay İzleme ve Yönetimi:** Sistem genelinde olayların izlenmesi ve yönetilmesi karmaşık olabilir. Bu, etkin bir izleme ve hata yönetimi altyapısı gerektirir.
* **Tutarlılık ve Güvenilirlik:** Olayların sırası ve teslimat garantileri gibi konular, özellikle dağıtık sistemlerde dikkat edilmesi gereken önemli noktalardır.

![](https://raw.githubusercontent.com/mrtyildiz/Blog-Post/main/Software/IMG/Event-Driven%20Architecture.webp)


## Layered Architecture

Katmanlı Mimarisi (Layered Architecture), yazılım mühendisliğinde sıkça kullanılan bir tasarım modelidir. Bu model, bir uygulamanın farklı işlevlerini ayrı katmanlara ayırarak, her katmanın belirli bir sorumluluğu olmasını sağlar. Bu yaklaşım, uygulama geliştirmeyi daha yönetilebilir ve modüler hale getirir, böylece farklı katmanlar arasında net bir ayrım sağlanır ve her katmanın bağımsız olarak geliştirilmesine ve test edilmesine olanak tanır.


Katmanlı Mimarisi (Layered Architecture), yazılım mühendisliğinde sıkça kullanılan bir tasarım modelidir. Bu model, bir uygulamanın farklı işlevlerini ayrı katmanlara ayırarak, her katmanın belirli bir sorumluluğu olmasını sağlar. Bu yaklaşım, uygulama geliştirmeyi daha yönetilebilir ve modüler hale getirir, böylece farklı katmanlar arasında net bir ayrım sağlanır ve her katmanın bağımsız olarak geliştirilmesine ve test edilmesine olanak tanır.

#### Temel Katmanlar
Katmanlı mimari genellikle aşağıdaki katmanlardan oluşur:

* **Sunum Katmanı (Presentation Layer):** Kullanıcı arayüzü (UI) ve kullanıcı deneyimi (UX) ile ilgilenir. Kullanıcıdan gelen istekleri alır ve kullanıcıya görsel geri bildirim sağlar.
* **İş Mantığı Katmanı (Business Logic Layer - BLL):** Uygulamanın temel işlevlerini ve kurallarını içerir. Veri erişim katmanından gelen verileri işler ve sunum katmanına sonuçları iletir.
* **Veri Erişim Katmanı (Data Access Layer - DAL): **Veritabanı ile etkileşimde bulunur. Veritabanından veri okuma, veri yazma, güncelleme ve silme işlemlerini gerçekleştirir.
* **Veri Modeli Katmanı (Data Model Layer):** Uygulamanın veri modellerini ve veri transfer objelerini (DTO) tanımlar. Bu katman, verinin nasıl saklandığını ve iş mantığı katmanına nasıl aktarıldığını tanımlar.

#### Avantajları
* **Modülerlik:** Katmanlar arasında net bir ayrım, geliştiricilerin yalnızca ilgilendikleri katman üzerinde çalışmalarını sağlar. Bu, kodun daha okunabilir ve yönetilebilir olmasına yardımcı olur.
* **Bakım Kolaylığı:** Bir katmandaki değişiklikler genellikle diğer katmanları etkilemez, bu da bakım ve güncellemeleri kolaylaştırır.
* **Yeniden Kullanılabilirlik:** İş mantığı ve veri erişim katmanları genellikle uygulamalarda benzerdir, bu nedenle kodun yeniden kullanılması mümkündür.
* **Test Edilebilirlik:** Katmanlar bağımsız olarak test edilebilir, bu da hata bulma ve düzeltme işlemini kolaylaştırır.

#### Zorluklar

* **Performans Overhead:** Katmanlar arası iletişim, ek işlem yükü getirebilir ve performansı düşürebilir.
* **Katmanlar Arası Bağımlılıklar:** Yanlış tasarım kararları, katmanlar arasında gereksiz bağımlılıklara yol açabilir ve sistem karmaşıklığını artırabilir.

Katmanlı mimari, özellikle büyük ve karmaşık uygulamalar için uygun bir tasarım yaklaşımıdır. Ancak, performans ve katmanlar arası bağımlılıklar gibi potansiyel zorluklar göz önünde bulundurulmalıdır.

![](./IMG/Layered%20Architecture.webp)

## Monolithic Architecture


Monolitik mimari, yazılım uygulamalarını tasarlama konusunda geleneksel bir modeldir. Bu mimaride, uygulamanın tüm bileşenleri—kullanıcı arayüzü, iş mantığı, veritabanı işlemleri ve uygulama servisleri gibi—tek bir büyük ve bütünleşik sistem içinde birleştirilir. Bu yaklaşım, uygulamanın tüm parçalarının birlikte geliştirilmesini ve dağıtılmasını gerektirir.

Monolitik mimarinin bazı özellikleri şunlardır:

* **Tekil Kod Tabanı:** Uygulamanın tüm fonksiyonları tek bir kod tabanında bulunur, bu da geliştirme ve yönetimi basitleştirebilir.
* **Basit Dağıtım:** Uygulama, genellikle tek bir dosya veya paket olarak dağıtılır, bu da başlangıçta dağıtımı kolaylaştırır.
* **Entegre Geliştirme Ortamı:** Geliştiriciler, uygulamanın farklı bölümleri üzerinde çalışırken, tüm uygulama üzerinde genel bir bakışa ve kontrol sahibi olabilirler

* **Karşılıklı Bağımlılıklar:** Uygulamanın bileşenleri arasında yüksek derecede bağlılık olabilir, bu da bir bölümde yapılan değişikliklerin diğer bölümleri etkileyebileceği anlamına gelir.

Monolitik mimari, küçük veya orta ölçekli projelerde ve basit uygulamalarda iyi çalışabilir, çünkü bu tür projelerde sistem karmaşıklığı ve ölçeklenme ihtiyaçları sınırlıdır. Ancak, uygulama büyüdükçe ve daha karmaşık hale geldikçe, monolitik mimarinin sınırlamaları ortaya çıkabilir. Örneğin, uygulamanın bir bölümünde yapılacak küçük bir değişiklik, tüm sistemin yeniden derlenmesini ve dağıtılmasını gerektirebilir. Ayrıca, büyük monolitik sistemlerin ölçeklenmesi zor olabilir, çünkü genellikle tüm uygulamanın tek bir sunucu örneğinde çalıştırılması gerekir.

![](/IMG/Monolithic%20Architecture.webp)

Bu nedenle, büyük ve karmaşık sistemler için mikro hizmetler gibi daha modüler mimari yaklaşımlar tercih edilmeye başlanmıştır. Mikro hizmet mimarisi, uygulamanın bağımsız olarak geliştirilebilen, dağıtılabilen ve ölçeklendirilebilen küçük servislerden oluşmasını sağlar. Bu, büyük uygulamaların yönetimini, ölçeklenmesini ve güncellenmesini kolaylaştırır.

## Microservices Architecture

Mikro hizmetler mimarisi, bir yazılım uygulamasını daha küçük, bağımsız servislerin bir koleksiyonu olarak tasarlama yaklaşımıdır. Bu servisler belirli işlevleri yerine getirir ve birbirleriyle hafif ağırlıklı mekanizmalar, genellikle HTTP tabanlı API'ler aracılığıyla iletişim kurarlar. Her bir mikro hizmet, kendi veritabanı ve depolama mekanizmaları da dahil olmak üzere, bir iş sürecini veya işlevi kapsayacak şekilde tasarlanır ve geliştirilir.

Mikro hizmetler mimarisinin temel özellikleri şunlardır:

* **Modülerlik:** Uygulama, belirli işlevleri gerçekleştiren bir dizi bağımsız modülden oluşur. Bu yaklaşım, sistem üzerinde çalışmayı ve yeni özellikler eklemeyi kolaylaştırır.

* **Esnek Dağıtım:** Mikro hizmetler, bağımsız olarak dağıtılabilir ve ölçeklenebilir. Bu, bir servisin güncellenmesinin diğer servisleri etkilememesi anlamına gelir, böylece daha hızlı ve sık sık güncellemeler mümkün olur.

* **Dil ve Teknoloji Çeşitliliği:** Her mikro hizmet, en uygun olduğu düşünülen programlama dili ve teknoloji yığını kullanılarak geliştirilebilir. Bu, teknoloji seçiminde esneklik sağlar.

* **Dayanıklılık:** Bir mikro hizmetin başarısız olması durumunda, diğer mikro hizmetler etkilenmez ve çalışmaya devam eder. Bu, sistemin genel dayanıklılığını artırır.

* **Ölçeklenebilirlik:** Her mikro hizmet, ihtiyaca göre bağımsız olarak ölçeklendirilebilir. Bu, sistem kaynaklarının daha verimli kullanımını sağlar ve yüksek talep gören servislerin performansını artırabilir.

![](/IMG/Microservices%20Architecture.webp)

Mikro hizmetler mimarisi, büyük ve karmaşık sistemlerin yönetilmesini kolaylaştırır, ancak aynı zamanda sistemler arası iletişim, veri tutarlılığı ve hizmetlerin keşfi gibi zorlukları da beraberinde getirir. Bu mimariyi benimseyen ekipler, bu zorlukların üstesinden gelmek için ek araçlar ve yöntemler kullanır, örneğin servis ağları, API ağ geçitleri ve merkezi yapılandırma hizmetleri.

## Model-View-Controller (MVC)

Model-View-Controller (MVC), yazılım geliştirmede kullanılan bir mimari desendir. Uygulamaları üç ana bileşene ayırarak geliştirme sürecini düzenler: Model, View ve Controller. Bu ayrım, uygulamanın farklı yönlerinin birbirinden bağımsız olarak geliştirilmesine, test edilmesine ve bakımının yapılmasına olanak tanır, böylece kodun daha temiz, daha organize ve daha kolay yönetilebilir olmasını sağlar.

![](/IMG/Model-View-Controller.webp)
#### Model

Model, uygulamanın veri yapısını temsil eder ve doğrudan veri işleme ile ilgilenir (örneğin, veritabanı işlemleri). Verilerin nasıl saklanacağı, yönetileceği ve manipüle edileceği ile ilgili kuralları içerir. Model, uygulamanın "beyni" olarak düşünülebilir ve iş mantığı ile veri erişim katmanlarını içerir.

#### View

View, kullanıcıya gösterilen verileri ve kullanıcı arayüzünü (UI) temsil eder. Kullanıcının gördüğü her şey View kapsamına girer; örneğin, web uygulamalarında HTML sayfaları, mobil uygulamalarda kullanıcı arayüzü elemanları. View, Model'den aldığı verileri görsel bir formatla sunar ve kullanıcı girişini alır, ancak doğrudan veri işleme yapmaz.

#### Controller

Controller, Model ve View arasındaki etkileşimi yönetir. Kullanıcıdan gelen girişleri alır (örneğin, klavye girişleri, fare tıklamaları), bu girişleri işler ve Model'i günceller veya değiştirir. Ardından, gerekli görünümü seçer ve kullanıcıya sunar. Controller, kullanıcı eylemlerine yanıt olarak neyin görüntüleneceğini ve uygulamanın nasıl tepki vereceğini belirler.

MVC mimarisi, uygulama geliştirmede sorumlulukların ayrılmasını sağlayarak, geliştirme sürecini daha verimli hale getirir. Bu yapı, birçok modern web çerçevesinde ve uygulama geliştirme kitinde kullanılır ve büyük ölçüde kabul görmüş bir tasarım desenidir. Bu mimari sayesinde, kod tekrarını azaltmak, uygulama bakımını kolaylaştırmak ve geliştirme sürecini hızlandırmak mümkündür.

## Master-Slave Architecture

Master-Slave (Ana-Köle) mimarisi, bilgisayar bilimi ve yazılım mühendisliğinde kullanılan bir sistem tasarım modelidir. Bu mimari modelde, iki tür bileşen vardır: bir veya birden fazla "master" (ana) bileşeni ve bir veya birden fazla "slave" (köle) bileşeni. Master bileşeni, işlemleri kontrol eder ve yönetirken, slave bileşenleri verilen komutları yerine getirir ve genellikle veri işleme, hesaplama veya depolama görevleri gibi spesifik işleri yapar.

Temel Özellikleri:
* **Merkezi Kontrol:** Master bileşeni, sistem üzerindeki tüm önemli kararları alır, işlemleri koordine eder ve slave bileşenlerine talimatlar gönderir.

* **Dağıtık İşlem:** İş yükü, birden çok slave bileşeni arasında dağıtılabilir, böylece paralel işlem ve yüksek işlem kapasitesi sağlanır.
* **Esneklik ve Ölçeklenebilirlik:** Yeni slave bileşenlerinin eklenmesiyle sistem kolayca ölçeklendirilebilir, bu da büyük veri setleri üzerinde işlem yapma veya yüksek kullanıcı talebini karşılama kapasitesini artırır.
* **Dayanıklılık:** Bir slave bileşeni arızalandığında, master bileşeni işi başka bir slave bileşenine yönlendirebilir, bu sayede sistem kesintisiz çalışmaya devam edebilir.

#### Kullanım Alanları:
Master-Slave mimarisi, veritabanı replikasyonu, yüksek kullanılabilirlik sistemleri, dağıtık hesaplama ve veri işleme gibi birçok alanda kullan
