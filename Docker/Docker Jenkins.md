# Jenkins Kullanımı


Jenkins Continuous Integration (Sürekli Entegrasyon) yöntemi için kullanılan açık kaynak kodlu bir otomasyon sunucusudur.
Yazılım geliştirme ve test süreçlerini otomatize etmemize imkan sağlamaktadır. Jenkins belirlenen kaynaktan projeye ulaşır ve istenen işlemleri otomatize etmemize imkan sağlamaktadır.
Test süreçleri sonucunda oluşan çıktıları belirli kişilere iletmektedir. Bu sayede proje sürekli olarak test edilir ve hataların tespit edilmesi sağlanmakdır.

Jenkins kavramları aşağıdaki gibidir;

* Job: Otomatize edilmesi istenilen işler burada belirtilir. Örneğin, job config üzerinden repository 'i çek, şartları build et, 
testleri gerçekleştirilir ve mail atma işlemleri burada belirlenir.

* Node: Job 'un çalıştığı sunucuyu ifade etmektedir.  Testleri başka bir bilgisayarda koşmak istediğimizde node oluşturur ve bağlantı için gerekli şartları gerçekleştirdikten sonra node’da testlerimizi koşabiliriz.

* Plugin (eklenti): Jenkins default haliyle yüklenir, ihtiyacımıza göre plugin yükler ve bunları kullanılırız. Örneğin, Job çalıştıktan sonra mail atması için “Email Extension” eklentisini yüklemelidir.
* Pipeline: Belirli işlem çıktısının başka bir işleme girilmesini/gönderilmesini sağlamaktadır.
