# API Güvenliği - 2

Önceki blog yazımda API güvenliği konusuna giriş yapmıştım. Bu konu özelinde devam etmek üzere yazıyorum.
Önceki yazıma [Buradan](https://www.google.com) ulaşabilirsiniz.

### API Güvenliği - Information Leak

#### Information Leak (Bilgi Sızdırma) Nedir?


API tarafının client tarafına gereksiz sistem bilgileri sunması durumuna Information Leak denmektedir. Bu durum şu şekiller de olabilir;

* **Yanıt Mesajları:** API'nin hata veya işlem yanıtlarında hassas bilgilerin göstermesi.
* **HTTP Headers:** Server, X-Powered-By, StackTrace gibi başlıkların istemciye açık olması.
* **Gereksiz JSON Alanları:** Kullanıcı bilgileri veya sistem detayları gibi ek veri döndürme.
* **StackTrace Gösterimi:** Hata mesajlarında sistem iç yapısının istemciye görünmesi.

Bilgi sızıntılar, API'nin çalıştığı sistem hakkında bilgi vermekte ve siber saldırıların kolayşmasına imkan sunmaktadır.

#### Information Leak Örnekleri ve Önlem yöntemleri

Aşağıdaki örnek senaryolarda Information Leak örnekleri verilmekte ve bu durumlara karşın nasıl önlem alınacağı belirtirlmektedir.

#### Senaryo - 1

Aşağıdaki kod örneğinde bir hata olduğunu ve doğrudan kullanıcıya döndürüldüğü görülmektedir;

```golang
package main

import (
	"errors"
	"github.com/gin-gonic/gin"
	"net/http"
)

func main() {
	r := gin.Default()

	r.GET("/user/:id", func(c *gin.Context) {
		id := c.Param("id")

		if id == "0" {
			err := errors.New("database connection failed: timeout")
			c.JSON(http.StatusInternalServerError, gin.H{"error": err.Error()}) // ❌ Hata mesajı saldırganlara açık
			return
		}

		c.JSON(http.StatusOK, gin.H{"message": "User found"})
	})

	r.Run(":8080")
}
```
**🚨 Hataya Neden Olan Noktalr**

* __"database connection failed: timeout"__ hatasının doğrundan client tarafına gitmektedir.
* Bu hata nedeniyle veritabanı türü ve bağlantı yapısının öğrenilmesine neden olabilmektedir.

#### ✅ Çözüm: Genel Hata Geri Dönüş Mesajlarının Kullanılması

Bu kullanım ile sadece Client tarafına genel hata mesajı döndürülmektedir.

```golang
package main

import (
	"errors"
	"log"
	"net/http"

	"github.com/gin-gonic/gin"
)

func main() {
	r := gin.Default()

	r.GET("/user/:id", func(c *gin.Context) {
		id := c.Param("id")

		if id == "0" {
			err := errors.New("database connection failed: timeout")
			log.Println("Internal Server Error:", err) // ✅ Sadece log’a yaz

			c.JSON(http.StatusInternalServerError, gin.H{"error": "Beklenmeyen bir hata oluştu."}) // ✅ Genel mesaj
			return
		}

		c.JSON(http.StatusOK, gin.H{"message": "User found"})
	})

	r.Run(":8080")
}
```

Bu kullanım ile;
* Salgırgan sistem iç yapısını öğrenemez
* Geliştiriciler kaydedilen hata logları ile çözüm konusunda fikir sahibi olması sağlanrır.


#### Senaryo - 2: API Yanıtlarında Gereksiz Bilgilerin Kullanılması

HTTP Headers bazen clientlara gereksiz bilgileri iletebilmektedir. Örneğin X-Powered-By veya hata durumlarından dönen StackTrace bilgileri, Saldırgan için kritik bilgiler içerebilmektedir.

Aşağıdaki örnekte, GIN varsayılan ayarlarıyla çalıştırıldığında sunucu hakkında hangi bilgilerin sızdığına dair bir örnek gösterilmektedir.

```golang
package main

import (
	"github.com/gin-gonic/gin"
	"net/http"
)

func main() {
	r := gin.Default()

	r.GET("/", func(c *gin.Context) {
		c.String(http.StatusOK, "Hello, World!")
	})

	r.Run(":8080")
}
```

Bu uygulama çalıştırıldığında, client tarafında aşağıdaki gibi bir HTTP response elde edilebilir;

```http
HTTP/1.1 200 OK
Server: gin
Date: Mon, 01 Jan 2025 12:00:00 GMT
Content-Length: 13
Content-Type: text/plain; charset=utf-8
```

Burada saldırgan kullanılan framework bilgisini **Server: gin** kısmında alınabilmektedir.

✅ **Çözüm: Gereksiz HTTP Başlıklarını Kaldırma**

Aşağıdaki örnekteki gibi gereksiz http headers 'ların kaldırılması güvenliğin arttırılmasında büyük bir rol oynayabilir.

```golang
package main

import (
	"github.com/gin-gonic/gin"
	"net/http"
)

func main() {
	r := gin.Default()

	// Middleware: Gereksiz header'ları kaldır
	r.Use(func(c *gin.Context) {
		c.Writer.Header().Del("Server")        // Server başlığını kaldır
		c.Writer.Header().Del("X-Powered-By")  // X-Powered-By başlığını kaldır
	})

	r.GET("/", func(c *gin.Context) {
		c.String(http.StatusOK, "Hello, World!")
	})

	r.Run(":8080")
}
```
Kodda görüldüğü gibi gereksiz olan **Server** ve **X-Powered-By** http headersların gösterilmesinin önüne geçilmiştir.

#### Senaryo - 3: Gereksiz JSON Alanları Üzerinden Bilgi Sızdırma

Uygulamaların döndürdüğü JSON responslarında, Clientların ihtiyaç duymadıkları ekstra alanların/verilerin bulunması, sistem hakkında gereksiz bilgilerin verilmesi salgırganların sistem hakkında bilgi sahibi olmalarına neden olabilmektedir.

Aşağıdaki örnekte, client tarafına iletilen response json nesnesinde kullanıcı parola bilgisi hash'i 'de yer almakta;

```golang
package main

import (
	"github.com/gin-gonic/gin"
	"net/http"
)

type User struct {
	ID       int    `json:"id"`
	Username string `json:"username"`
	Email    string `json:"email"`
	Password string `json:"password"` // ❌ Kullanıcı şifresi istemciye gidiyor!
}

func main() {
	r := gin.Default()

	r.GET("/profile", func(c *gin.Context) {
		user := User{
			ID:       1,
			Username: "johndoe",
			Email:    "johndoe@example.com",
			Password: "hashedpassword123", // ❌ Şifre istemciye gönderiliyor
		}

		c.JSON(http.StatusOK, user)
	})

	r.Run(":8080")
}

```

Bu kod çalıştırıldığında dönen örnek json verisi aşağıdaki gibidir;

```json
{
	"id": 1,
	"username": "johndoe",
	"email": "johndoe@example.com",
	"password": "hashedpassword123"
}
```

Buradaki **password** alanı client tarafına gönderilmesi gereksiz bir bilgidir.

✅ ***Çözüm: Hassas Verileri JSON Yanıtından Çıkarmak***

Bu hatanın çözülmesi amacıyla, yalnızca gerekli verilerin iletilmesi amacıyla **DTO (Data Transfer Object)** veya farklı bir struct tanımlayarak client tarafına hassas bilgilerin gönderilmesinin önüne geçilebilmektedir.

Örneğin;

```golang
package main

import (
	"github.com/gin-gonic/gin"
	"net/http"
)

type User struct {
	ID       int    `json:"id"`
	Username string `json:"username"`
	Email    string `json:"email"`
}

func main() {
	r := gin.Default()

	r.GET("/profile", func(c *gin.Context) {
		user := User{
			ID:       1,
			Username: "johndoe",
			Email:    "johndoe@example.com",
		}

		c.JSON(http.StatusOK, user) // ✅ Sadece gerekli alanlar döndürülüyor
	})

	r.Run(":8080")
}

```
Bu yöntem ile client tarafına aşağıdaki gibi bir geri dönüş olmaktadır.
```json
{
	"id": 1,
	"username": "johndoe",
	"email": "johndoe@example.com"
}
```

Bu sayede gereksiz ve hasas bilgilerin önüne geçilmesi sağlanmaktadır.
