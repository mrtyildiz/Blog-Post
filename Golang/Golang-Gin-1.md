## Docker üzerinde Golang uygulmasının geliştirilmesi

### Golang Nedir?

Go, genellikle "Golang" olarak da bilinen, Google tarafından geliştirilen açık kaynaklı bir programlama dilidir. Go'nun tasarım amacı, hızlı, basit, güvenli ve verimli bir şekilde yazılım geliştirmeyi sağlamaktır. Aynı zamanda paralel ve dağıtık sistemler için de uygun bir dil olarak tasarlanmıştır.

![Golang](https://raw.githubusercontent.com/mrtyildiz/Blog-Post/main/Golang/img/Golang-Gin-1.jpg)


Go, aşağıdaki özellikleriyle öne çıkar:

1. **Hızlı ve Verimli:** Go, derlenmiş bir dil olduğu için yüksek performans sağlar. Çalışma zamanında yorumlanma gereksinimi olmadan doğrudan makine koduna çevrilebilir.

2. **Basit ve Sade:** Go'nun sentaksı oldukça basittir. Dil tasarımı, gereksiz karmaşıklığı önlemek ve kodun anlaşılabilirliğini artırmak amacıyla yapılmıştır.

3. **Paralellik ve Eşzamanlılık:** Go, paralel ve eşzamanlı programlamayı kolaylaştıran birçok özellik sunar. Goroutine adı verilen hafif iş parçacıkları ile eşzamanlı programlamayı destekler.

4. **Bellek Yönetimi:** Go, otomatik bellek yönetimi (garbage collection) ile geliştiricilere bellekle ilgili sorunlarla uğraşma gerekliliğini azaltır.

5. **Derlenmiş Dil:** Go, C ve C++ gibi derlenmiş dillerin avantajlarını sunar. Bu sayede yüksek performans elde edilirken, kodun daha güvenli ve hata yapmaya karşı daha dayanıklı olması sağlanır.

6. **Kapsamlı Standart Kütüphane:** Go'nun geniş bir standart kütüphanesi bulunur. Bu kütüphaneler, çeşitli görevleri yerine getirmek için kullanılabilir ve geliştirme sürecini hızlandırabilir.

7. **Taşınabilirlik:** Go, birçok işletim sistemi ve platformda çalışabilen taşınabilir bir dildir. Bu özellik, uygulamaların farklı ortamlarda kolayca çalıştırılabilmesini sağlar.

Go, genellikle sistem programlaması, ağ programlaması, veritabanı yönetimi ve büyük ölçekli yazılım projeleri gibi alanlarda tercih edilir. Hem öğrenmesi kolay hem de etkili bir dil olarak kabul edilir.

### Docker Nedir?

Docker, yazılım uygulamalarını geliştirmek, dağıtmak ve çalıştırmak için kullanılan bir konteynerleştirme platformudur. Konteynerleştirme, bir uygulamanın tüm gereksinimlerini, kodunu, çalışma zamanını ve bağımlılıklarını bir araya getirerek izole bir çevre içinde çalışmasını sağlayan bir teknolojidir. Docker, bu konteynerleştirme sürecini basit ve tekrarlanabilir bir şekilde gerçekleştirmeyi amaçlar.

![Golang](https://raw.githubusercontent.com/mrtyildiz/Blog-Post/main/Golang/img/Golang-Gin-2.png)


Docker'ın temel bileşenleri şunlardır:

1. **Docker Konteynerleri:** Docker, uygulamaların çalıştırılabileceği hafif ve taşınabilir konteynerler oluşturmanızı sağlar. Her konteyner, uygulamanın kodunu, bağımlılıklarını ve çalışma zamanını içerir. Konteynerler, işletim sistemine bağımsız olarak çalışabilir ve aynı şekilde davranır, böylece bir ortamdan diğerine kolayca taşınabilirler.

2. **Docker Görüntüleri:** Docker konteynerlerinin temel yapı taşı olan görüntüler, bir uygulamanın tüm gereksinimlerini içeren bir örnek olarak düşünülebilir. Görüntüler, uygulamanın çalışması için gerekli olan dosyaları, kodu ve konfigürasyonları içerir. Görüntüler temel alınarak konteynerler oluşturulur.

3. **Docker Hub:** Docker Hub, kullanıcıların ve geliştiricilerin Docker görüntülerini paylaşabileceği ve bulabileceği bir depodur. Bu, hazır görüntülerin paylaşılmasını, topluluk tarafından oluşturulan görüntülerin kullanılmasını ve işbirliğini kolaylaştırır.

Docker'ın sağladığı avantajlar:

* **Taşınabilirlik:** Docker konteynerleri, herhangi bir ortamda çalışabilirler, bu da geliştirme ve dağıtım süreçlerini kolaylaştırır.
* **Hız ve Verimlilik:** Docker, hızlı başlatma ve sonlandırma süreçleriyle uygulamaların daha verimli çalışmasını sağlar.
* **İzolasyon:** Her bir konteyner, izole bir çevrede çalıştığı için bir konteynerde oluşan sorunlar diğerlerini etkilemez.
* **Çeviklik:** Docker, hızlı bir şekilde uygulama geliştirmeyi, test etmeyi ve dağıtmayı mümkün kılar.
* **Ölçeklenebilirlik:** Docker, uygulamaları ihtiyaca göre hızlıca ölçeklendirebilmenizi sağlar.

Docker, yazılım geliştirme ve dağıtım süreçlerini daha kolay, tekrarlanabilir ve etkili bir hale getiren önemli bir teknolojidir.

### Docker çalışma ortamının oluşturulması

````dockerfile
FROM golang

RUN apt-get install -y && apt-get update -y && apt-get upgrade -y && apt-get dist-upgrade -y
RUN apt install -y nano
RUN mkdir -p /app
VOLUME [ "/app" ]
````
Belirtilen Dockerfile 'ın açıklaması aşağıdaki gibidir;

1. **FROM golang:** Bu satır, Docker görüntüsünün temel alınacağı temel görüntüyü belirtir. Bu örnekte, temel görüntü olarak "golang" adlı bir Golang görüntüsü kullanılıyor. Bu, Golang dilini içeren bir temel görüntü anlamına gelir. Yani, uygulamanın Golang kodunu bu görüntü üzerine inşa edeceğiz.

2. **RUN apt-get install -y && apt-get update -y && apt-get upgrade -y && apt-get dist-upgrade -y:** Bu satırda, işletim sistemindeki paket yöneticisi olan apt-get kullanılarak sistemdeki paketler güncelleniyor ve yükseltiliyor. Önce update komutu ile paket listesi güncellenir, ardından upgrade ve dist-upgrade komutlarıyla sistemdeki paketler yükseltilir. -y parametresi, tüm işlemlerin onay almadan otomatik olarak gerçekleştirilmesini sağlar.

3. **RUN apt install -y nano:** Bu satırda, nano adlı metin düzenleyici paketini kuruyoruz. Metin düzenleme işlerinde kullanılabilecek bir araçtır.

4. **RUN mkdir -p /app:** Bu satırda, Docker konteyneri içinde "/app" adlı bir dizin oluşturuyoruz. Bu dizin, uygulamanın çalıştığı dizini temsil edebilir.

5. **VOLUME [ "/app" ]:** Bu satırda, "/app" dizini Docker konteynerinin bir hacim noktası olarak belirleniyor. Hacimler, konteyner içi ve dışı arasında veri paylaşımını sağlayan mekanizmalardır. Bu satır, "/app" dizinini dışarıya açarak, konteyner içindeki verilerin dışarıya kaydedilmesini ve paylaşılmasını mümkün kılar.

Bu Dockerfile, temel Golang görüntüsü üzerine ihtiyaca göre birçok ekstra işlemi eklemekte ve "/app" dizinini dışarıya açarak veri paylaşımını sağlamaktadır. Bu tür bir Dockerfile, Golang uygulamalarını hazırlamak ve çalıştırmak için kullanılabilir.

Uygulama geliştirileceği ortamın kurulması amacıyla "docker build . -t golangtutorial:latest" komutu kullanılır.

![Building](https://raw.githubusercontent.com/mrtyildiz/Blog-Post/main/Golang/img/Golang-Gin-3.png)

Oluşturulmuş olan image 'ın kullanılarak bir docker konteyner oluşturmak için **"docker run -it -d -p 8000:8000 -v D:\Projects\Golang\Tutorials-Golang\app:/app golangtutorial:latest"** komutu kullanılır.

![Container Running](https://raw.githubusercontent.com/mrtyildiz/Blog-Post/main/Golang/img/Golang-Gin-4.png)

Konteyner oluşturulduktan sonra oluşturulan konteynırın kullanılması için docker ara yüzünden konteynerın terminaline bağlanılır.

![Docker Interface](https://raw.githubusercontent.com/mrtyildiz/Blog-Post/main/Golang/img/Golang-Gin-5.png)

Oluşturulmuş bu ortam üzerinde örnek olması amacıyla Gin kütüphanesi kullanılarak bir API oluşturulmuş ve CRUD işlemlerine ait fonksiyonlar yazılmıştır.

### Golang ile API Geliştrilmesi

Golang Gin, Go programlama dilinde web uygulamaları ve API'ler oluşturmayı kolaylaştıran hızlı ve hafif bir web framework'üdür. "Gin" adı, hızlı ve hafif olduğunu vurgulamak için "engine" kelimesinin bir kısaltmasıdır. Gin, özellikle performansı önemseyen projeler için tercih edilen bir web framework'üdür.

İşte Gin'in temel özelliklerinden bazıları:

1. **Hızlı ve Hafif:** Gin, performans odaklı bir tasarıma sahiptir. Minimalist bir yapıya sahip olması, hızlı çalışmasına olanak tanır.

2. **Router:** İstekleri yönlendirmek ve işlemek için güçlü bir yönlendirme sistemi sunar. Farklı HTTP metodlarını (GET, POST, PUT, DELETE vb.) ve URL örüntülerini destekler.

3. **Middleware Desteği:** Middleware'ler, istek ve yanıt işlemlerinin arasına girerek farklı işlevleri uygulamanızı sağlar. Örneğin, oturum yönetimi, kimlik doğrulama gibi işlemleri middleware'lerle kolayca entegre edebilirsiniz.

4. **JSON Desteği:** JSON verileriyle çalışmayı kolaylaştıran fonksiyonlar ve yapılar sunar. Bu sayede API'ler oluştururken verileri dönüştürmek ve almak basit hale gelir.

5. **Validasyon:** İstek verilerini doğrulamak için kullanışlı bir validasyon mekanizması sunar. Bu, gelen verileri kontrol ederek güvenlik ve tutarlılık sağlamanıza yardımcı olur.

6. **Swagger Desteği:** API belgelerini otomatik olarak oluşturmanıza yardımcı olacak Swagger desteği sunar. Bu, API'nizi belgelemeyi ve anlaşılabilir hale getirmeyi kolaylaştırır.

7. **Gruplama:** İlgili rotaları gruplamak ve yönetmek için gruplama özelliği sunar. Bu, büyük ölçekli projelerde rotaların düzenlenmesini kolaylaştırır.

Gin, Go programcıları için hızlı, etkili ve basit bir çözüm sunar. Performansı önemli olan web uygulamaları ve mikro hizmetler oluşturmak isteyen geliştiriciler için tercih edilen bir seçenektir.

### Golang Gin ile CRUD işlemleri

CRUD, genellikle veritabanı işlemlerini ifade eden bir kısaltmadır ve aşağıdaki dört temel işlemi temsil eder:

1. **Create (Oluşturma):** Veritabanına yeni veri eklemek için kullanılan işlemdir. Yeni bir kayıt oluştururken, veritabanında bir tabloya veya koleksiyona yeni bir satır veya belge eklenir.

2. **Read (Okuma):** Varolan verileri veritabanından çekmek veya almak için kullanılan işlemdir. Bir veya daha fazla kaydı sorgulayarak veritabanından bilgi almayı sağlar.

3. **Update (Güncelleme):** Varolan verileri güncellemek veya değiştirmek için kullanılan işlemdir. Mevcut bir kaydı alıp belirli alanlarını veya değerlerini güncellemek amacıyla kullanılır.

4. **Delete (Silme):** Veritabanından varolan verileri silmek için kullanılan işlemdir. Bir kaydı veritabanından tamamen kaldırmayı sağlar.

CRUD işlemleri, tipik olarak bir veritabanı veya veri deposu ile etkileşimde bulunurken kullanılır. Bu işlemler, birçok uygulama ve sistemde temel veri yönetimi işlevlerini gerçekleştirmek için kullanılır. Örneğin, bir kullanıcı kaydı oluşturmak, kullanıcı bilgilerini okumak, kullanıcı bilgilerini güncellemek veya kullanıcıyı silmek gibi işlemler CRUD işlemlerine örnek olarak verilebilir. 

Bu blog yazısında örnek olarak kullanacağımız golang kodu ve açıklaması aşağıdaki gibidir;

```go
package main

import (
	"net/http"
	"strconv"

	"github.com/gin-gonic/gin"
)

```
İlk öncelikle uygulama özelinde kullanılacak olan kütüphaneler tanımlanmıştır. kütüphanelerin işlevleri aşağıdaki gibidir;


1. **github.com/gin-gonic/gin:** Bu kütüphane, web uygulamaları ve API'ler oluşturmayı kolaylaştıran bir Go (Golang) framework'ü olan Gin'in temel parçasıdır. HTTP isteklerini işlemek, yönlendirmek ve middleware'leri kullanmak gibi bir dizi web geliştirme işlevi sunar.

2. **net/http:** Bu, Go'nun standart kitaplığından bir pakettir ve HTTP sunucu ve istemci işlemleri için gerekli olan temel araçları sağlar. Gin'in altında da net/http paketi kullanılırken, Gin daha yüksek seviyeli bir abstraksiyon sunar.

3. **strconv:** Bu, Go'nun standart kitaplığından bir pakettir ve dize dönüşüm işlemleri için kullanılır. Bu örnekte, URL parametresinden gelen metin tabanlı ID'leri tam sayılara dönüştürmek için kullanılır.


```go
type User struct {
	ID       int    `json:"id"`
	Username string `json:"username"`
	Email    string `json:"email"`
}

var users []User

```
struct yapısına uygun olarak bir user tanımlaması gerçekleştirilmiştir.

```go 
// Yeni bir kullanıcı oluşturur
func CreateUser(c *gin.Context) {
	var user User
	if err := c.ShouldBindJSON(&user); err != nil {
		c.JSON(http.StatusBadRequest, gin.H{"error": err.Error()})
		return
	}

	user.ID = len(users) + 1
	users = append(users, user)

	c.JSON(http.StatusCreated, user)
}
```
Yeni kullanıcının oluşturulması için gerekli olan kod bloğu.

```go
// Verilen ID'ye sahip kullanıcıyı bulur ve döndürür
func GetUserByID(c *gin.Context) {
	id, err := strconv.Atoi(c.Param("id"))
	if err != nil {
		c.JSON(http.StatusBadRequest, gin.H{"error": "Invalid ID"})
		return
	}

	for _, user := range users {
		if user.ID == id {
			c.JSON(http.StatusOK, user)
			return
		}
	}

	c.JSON(http.StatusNotFound, gin.H{"error": "User not found"})
}

```
Kullanıcı bilgilerinin Id bazlı çekilmesi amacıyla kullanılan kod bloğu.

```go
// Verilen ID'ye sahip kullanıcıyı günceller
func UpdateUser(c *gin.Context) {
	id, err := strconv.Atoi(c.Param("id"))
	if err != nil {
		c.JSON(http.StatusBadRequest, gin.H{"error": "Invalid ID"})
		return
	}

	var updatedUser User
	if err := c.ShouldBindJSON(&updatedUser); err != nil {
		c.JSON(http.StatusBadRequest, gin.H{"error": err.Error()})
		return
	}

	for i, user := range users {
		if user.ID == id {
			updatedUser.ID = id
			users[i] = updatedUser
			c.JSON(http.StatusOK, updatedUser)
			return
		}
	}

	c.JSON(http.StatusNotFound, gin.H{"error": "User not found"})
}
```

Kullanıcı bilgilerini ID bazlı olarak Update edilmesine imkan sunan kod bloğu

```go
// Verilen ID'ye sahip kullanıcıyı siler
func DeleteUser(c *gin.Context) {
	id, err := strconv.Atoi(c.Param("id"))
	if err != nil {
		c.JSON(http.StatusBadRequest, gin.H{"error": "Invalid ID"})
		return
	}

	for i, user := range users {
		if user.ID == id {
			users = append(users[:i], users[i+1:]...)
			c.JSON(http.StatusOK, gin.H{"message": "User deleted"})
			return
		}
	}

	c.JSON(http.StatusNotFound, gin.H{"error": "User not found"})
}

```
Belirtilen ID adresli kullanıcının silinmesine imkan sunan kod bloğu.

```go
func main() {
	r := gin.Default()

	// Kullanıcı oluşturma endpoint'i
	r.POST("/users", CreateUser)

	// Kullanıcı okuma endpoint'i
	r.GET("/users/:id", GetUserByID)

	// Kullanıcı güncelleme endpoint'i
	r.PUT("/users/:id", UpdateUser)

	// Kullanıcı silme endpoint'i
	r.DELETE("/users/:id", DeleteUser)

	// Sunucuyu başlat
	r.Run(":8000")
}

```

Main fonksiyonu tanımlanmış olan fonksiyonlara hangi path üzerinden gideceğini belirleme ve golang gin uygulamasının çalıştırılması amacıyla kullanılmaktadır. Belirtilen uygulamanın  çalıştırılması amacıyla sırasıyla aşağıdaki komutlar kullanılır;

* go mod init app
* go mod tidy
* go run main.go

![Docker Interface](https://raw.githubusercontent.com/mrtyildiz/Blog-Post/main/Golang/img/Golang-Gin-6.png)

Yeni bir kullanıcı eklemek amacıyla Postman uygulaması üzerinden aşağıdaki json datasını POST methoduyla gönderebilirsiniz;

```json
{
  "username": "Murat",
  "email": "murat@mail.com"
}
```

![POST Json](https://raw.githubusercontent.com/mrtyildiz/Blog-Post/main/Golang/img/Golang-Gin-7.png)

Oluşturulmuş ve ID değeri bilinen users bilgilerinin elde edilmesi amacıyla GET methodu kullanılarak istek gönderilir.

![GET Request](https://raw.githubusercontent.com/mrtyildiz/Blog-Post/main/Golang/img/Golang-Gin-8.png)

Oluşturulmuş ve ID değeri bilinen users 'ın bilgilerinin update edilmesi amacıyla aşağıdaki örnek json verisi PUT methodu ile iletilir.

```json
{
  "username": "Murat",
  "email": "murat123@mail.com"
}
```

![PUT Request](https://raw.githubusercontent.com/mrtyildiz/Blog-Post/main/Golang/img/Golang-Gin-9.png)

ID'si bilenen users 'ın silinmesi amacıyla DELETE methodu kullanılarak istek gönderilir.

![DELETE Request](https://raw.githubusercontent.com/mrtyildiz/Blog-Post/main/Golang/img/Golang-Gin-10.png)
