# API Güvenliği - 3

Selamlar API güvenliği konusundaki son blog yazım bir önceki blog yazıma [buradan](https://medium.com/@muratasnb/api-g%C3%BCvenli%C4%9Fi-2-b33361adfebf) ulaşabilirsiniz.

![Golang API](./img/3.png)

## API Güvenliği - Insecure Cookies, Path Traversal ve Rate Limiting

Golang programlama dili ile API geliştiriken saldırganlar önem alınması oldukça önemlidir. Güvenlik önlemleri alınmaması durumunda ciddi güvenlik açıkları ortaya çıkabilir. Bu yazıda API 'lerde karşımıza çıkan üç güvenlik açığı anlatılmaktadır;

1. **Insecure Cookies (Güvensiz Çerezler)**
2. **Path Traversal (Yol Geçişi Saldırıları)**
3. **Rate Limiting (İstek Sınırlama)**

Her güvenlik açığının açıklaması ve olası senaryoları aşağıdaki gibidir.

---

## 1. Insecure Cookies (Güvensiz Çerezler)

Çerezler, kullanıcı oturumlarını yönetmek için kullanılmaktadır. Cerezler güvenli olmayan kullanımlarından saldırganlar tarafından ele geçirilebilir ve session hijacking (Oturum çalma) gibi tehditlere yol açabilmektedir. 

### Örnek Insecure Cookies Senaryosu

Örnek kod aşağıdaki gibidir;

```go
package main

import (
    "net/http"
)

func main() {
    http.HandleFunc("/set-cookie", func(w http.ResponseWriter, r *http.Request) {
        http.SetCookie(w, &http.Cookie{
            Name:  "session_id",
            Value: "123456",
            Path:  "/",
        })
        w.Write([]byte("Cookie set"))
    })
    
    http.ListenAndServe(":8080", nil)
}
```
Örnekte verilen kod tarafından oluşturulan cerezleri **Secure** ve **HttpOnly** bayrakları olmadan oluşturmaktadır.
Bu durum aşağıdaki güvenlik hatalarına neden olabilir;

- **XSS saldırıları**: Çerez JavaScript ile okunabilir ve çalınabilir.
- **Güvensiz bağlantılar**: Çerezler HTTP üzerinden iletilebilir.

Kodun güvenli hale getirilmesi amacıyla 

### **Güvenli Kullanım Senaryosu**
Aşağıdaki kod, çerezi daha güvenli hale getiririlmesi amacıyla aşağıdaki öneriler gerçekleştirilebilir.

**Öneriler:**
- Çerezleri **HttpOnly** ve **Secure** olarak ayarlanır.
- **SameSite** politikasını kullanarak CSRF saldırılarının engellenmesi sağlanabilir.
- Cerez'in sadece site içerisinde kullanılması sağlanabilir.
- **HTTP** yerine **HTTPS** kullanılabilir.

Kodun güncellenmiş hali aşağıdaki gibidir;

```go
package main

import (
    "net/http"
)

func main() {
    http.HandleFunc("/set-secure-cookie", func(w http.ResponseWriter, r *http.Request) {
        http.SetCookie(w, &http.Cookie{
            Name:     "session_id",
            Value:    "123456",
            Path:     "/",
            Secure:   true,  // Sadece HTTPS üzerinden iletilir
            HttpOnly: true,  // JavaScript ile erişilemez
            SameSite: http.SameSiteStrictMode, // Çerez, yalnızca aynı site içinde çalışır
        })
        w.Write([]byte("Secure cookie set"))
    })
    
    http.ListenAndServeTLS(":8080", "server.crt", "server.key", nil)
}
```

## 2. Path Traversal (Yol Geçişi Saldırıları)

Path Traversal hatası, saldırganların API 'nin çalıştığı sunucu içerisindeki dosyalara erişmesine neden olabilmektedir.
Örnek bir Path Traversal hatasının bulunduğu kod;

```go
package main

import (
    "net/http"
    "os"
)

func main() {
    http.HandleFunc("/files", func(w http.ResponseWriter, r *http.Request) {
        filePath := r.URL.Query().Get("file")
        data, err := os.ReadFile("./uploads/" + filePath)
        if err != nil {
            http.Error(w, "File not found", http.StatusNotFound)
            return
        }
        w.Write(data)
    })
    
    http.ListenAndServe(":8080", nil)
}
```

Görülen bu kodda saldırgan `file=../../etc/passwd` gibi bir parametre ile sistem dosyalarına erişmesine neden olabilir.
Kodda görülen hatanın düzeltilmesi amacıyla aşağıdaki öneriler ugulanabilir;

- `filepath.Clean()` ile gelen yolu normalize edin.
- `filepath.Abs()` ile yetkisiz dizinlere erişimin önüne geçirilebilir.
- Kullanıcılardan gelen girdileri kontrol edilebilir.

Önerilen güvenlik önlemleri uygulandığın da golang kodu aşağıdaki gibi görülür;

```go
package main

import (
    "net/http"
    "os"
    "path/filepath"
    "strings"
)

func main() {
    http.HandleFunc("/secure-files", func(w http.ResponseWriter, r *http.Request) {
        filePath := r.URL.Query().Get("file")
        cleanPath := filepath.Clean(filePath)
        absPath, _ := filepath.Abs("./uploads/" + cleanPath)
        basePath, _ := filepath.Abs("./uploads/")
        
        if !strings.HasPrefix(absPath, basePath) {
            http.Error(w, "Unauthorized access", http.StatusForbidden)
            return
        }
        
        data, err := os.ReadFile(absPath)
        if err != nil {
            http.Error(w, "File not found", http.StatusNotFound)
            return
        }
        w.Write(data)
    })
    
    http.ListenAndServe(":8080", nil)
}

```

## 3. Rate Limiting (İstek Sınırlama)

API'lere uygulanabilecek brute-force saldırısının önüne geçilmesi amacıyla atılan isteklere kısıtlama getirilmelidir.
Rate Limiting, belirli bir zaman diliminde belirli sayıda isteğe izin verecektir.
Örnek Rate Limiting kodu aşağıdaki gibidir;

```go
package main

import (
    "net/http"
    "time"
    "github.com/didip/tollbooth"
    "github.com/didip/tollbooth/limiter"
)

func main() {
    lmt := tollbooth.NewLimiter(5, &limiter.ExpirableOptions{DefaultExpirationTTL: time.Minute})
    
    http.Handle("/secure-endpoint", tollbooth.LimitFuncHandler(lmt, func(w http.ResponseWriter, r *http.Request) {
        w.Write([]byte("Request allowed"))
    }))
    
    http.ListenAndServe(":8080", nil)
}
```
Örnekte verilen kodda her dakika başına maksimum **5 isteğe** izin vermektedir. Eğer daha fazla istek gönderilmesi durumunda **HTTP 429 Too Many Requests** hatasını alacaktır.
Bu hatanın önüne geçilmesi amacıyla aşağıdaki öneriler uygulanabilir;

- IP başına rate limiting uygulanması
- Redis, **Tollbooth** gibi araçlar ile isteklerin sınırlandırılması
- Rate limiting 'i API key bazlı uygulanması
