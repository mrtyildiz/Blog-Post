## Docker Konteynerlarını Optimize Etme Yolları

Docker konteynerlarının boyutlarını optimize etmek ve büyük boyutlara ulaşan konteynerların boyutlarını daha küçük hale getirme yolları aşağıdaki gibidir;

* MultiStage Builds (Çok Aşamalı Yapılar)
* Katman Optimizasyonu (Layer Optimization)
* "Scratch" Görüntüleri ("Scratch" Images)

![image](/IMG/Docker.png)

### MultiStage Builds (Çok Aşamalı Yapılar)

MultiStage Builds, Dockerfile içerisinde birden fazla FROM komutu kullanarak birden fazla image kullanıldığı bir tekniktir. Bu yöntem, tek bir Dockerfile içinde birden fazla bağımsız yapı aşamasını tanımlamamıza imkan tanır. Bu yapı da amaç yalnızca gerekli olan dosyaları son aşamaya taşıyarak daha küçük boyutta ve optimize bir Docker image oluşturmakdır.

Bu yöntem derleme işleminin sorunsuz ve gerekli olan bağımlılıklarla gerçekleştirilmesini sağlar. Bu durum fazlasıyla geçici dosya bulunan projelerde işimize yarayacaktır. MultiStage Builds yöntemi ile geçici dosyalar nihai docker image dahil edilmez.

Bu konu özelindeki örnek aşağıdaki gibidir;

Go dilinde yazılmış basit bir uygulama kullanacağız. İlk öncelikle kodu çalıştırmak için normal bir dockerfile yazağım ve build ederek oluşan docker image boyutunu görüntüleyeceğim bu amaçla kullanacağım Go script aşağıdaki gibidir;

```go
// main.go
package main

import (
    "fmt"
    "net/http"
)

func handler(w http.ResponseWriter, r *http.Request) {
    fmt.Fprintf(w, "Merhaba, Docker!")
}

func main() {
    http.HandleFunc("/", handler)
    http.ListenAndServe(":8080", nil)
}

```
İlk olarak kullanacağımız Dockerfile aşağıdaki gibidir;

```dockerfile
# Base image olarak Go'nun resmi imajını kullanıyoruz
FROM golang:1.18-alpine

# Çalışma dizinini oluştur ve ayarla
WORKDIR /app

# Go mod dosyalarını oluştur
RUN go mod init my-go-app
RUN go mod tidy

# Proje dosyalarını çalışma dizinine kopyala
COPY . .

# Go uygulamasını derle
RUN go build -o main .

# Uygulamayı başlat
CMD ["./main"]

# HTTP portunu aç
EXPOSE 8080

```
"docker build . -t golangapp:latest" komutu ile docker image oluşturulmuştur.

![image](/IMG/1_size.png)

Oluşturulmuş olan docker image boyutunun görüntülenmesi amacıyla docker desktop kullanıyorum.

![image](/IMG/2_size.png)

Şimdi MultiStage Builds methodunu kullanarak daha küçük boyutta bir docker image elde edelim. Örnek dockerfile aşağıdaki gibidir;
Bu dosyada MultiStage Builds kullanarak iki aşama tanımlayacağız:

* İlk aşama: Go uygulamasını derlemek için gerekli tüm bağımlılıkları indirip, uygulamayı derleyeceğiz.
* İkinci aşama: Derlenen uygulamayı minimal bir görüntüye kopyalayıp çalıştıracağız.

```dockerfile
# İlk aşama: Yapı aşaması
FROM golang:1.16 as builder

# Çalışma dizinini ayarla
WORKDIR /app

# Modülleri indir
RUN go mod init my-go-app
RUN go mod tidy
RUN go mod download

# Kaynak kodu kopyala
COPY . .

# Uygulamayı derle
RUN go build -o myapp

# İkinci aşama: Çalıştırma aşaması
FROM scratch

# Çalıştırılabilir dosyayı kopyala
COPY --from=builder /app/myapp /myapp

# Çalıştırma komutunu belirle
ENTRYPOINT ["/myapp"]

# Uygulama portunu belirle
EXPOSE 8080
```

Belirtilen dockerfile build edilir ve yeniden docker image boyutuna bakılır.

![image](/IMG/3_size.png)

Görselde görüldüğü gibi yaklaşık 53 katlıkn bir küçülme ile çalışabilir bir docker image 'a sahip olduk.

### Katman Optimizasyonu (Layer Optimization)

Docker yapısı gereği her komut için ayrı bir komut oluşturmaktadır. Bu durum docker image boyutunu doğrudan eklemektedir. Bu nedenle daha küçük ve verimli bir docker image oluşturulması için aşağıdaki işlemler gerçekleştirilebilir;

* **RUN komutlarını birleştirme:** Birden fazla olan RUN komutunu birleştirme işlemi gereksiz katmanların oluşmasını önler

* **Gereksiz Dosyaları Temizleme:** Geçici dosyaların ve bağımlılıkların temizlenmesi.

* **ADD Yerine COPY Kullanma:** COPY ile sadece belirli dosyaları kopyalar ve daha az bağımsızdır. ADD ise dosyaları açabilir veya internet üzerinden dosya indirebilir. Bu durumlar gereksiz katmanlar oluşturabilir.

Katman Optimizasyonu (Layer Optimization) ile ilgili örnek aşağıdaki gibidir;

**Optimize Edilmemiş Dockerfile**

```dockerfile
FROM node:14

WORKDIR /app

COPY package.json .
RUN npm install

COPY . .

RUN apt-get update
RUN apt-get install -y python3
RUN apt-get clean && rm -rf /var/lib/apt/lists/*

CMD ["node", "index.js"]
```

Belirtilen dockerfile "docker build . -t nodeapp:latest" komutu ile çalıştırılır. Oluşturulan docker image boyutu 937 MB boyutundadır.  
![image](/IMG/4_size.png)

**Optimize Edilmiş Dockerfile**
```dockerfile
FROM node:14

WORKDIR /app

# Bağımlılıkları kur
COPY package.json .
RUN npm install && npm cache clean --force

# Uygulama kaynaklarını kopyala
COPY . .

# Gereksiz dosyaları temizleyin ve RUN komutlarını birleştirin
RUN apt-get update && \
    apt-get install -y python3 && \
    apt-get clean && rm -rf /var/lib/apt/lists/*

CMD ["node", "index.js"]
```

Bu optimize işleminde;

* **npm install** ve **npm cache clean --force** komutları birleştirilmiştir. Bu durum hem  bağımılıkların kurulmasını hemde npm cache temizlenmesini sağlar

* **apt-get update**, **apt-get install** ve **apt-get clean** komutları tek bir RUN komutunda birleşririlmiştir. Bu durum gereksiz katmanların oluşturulmasını engeller.

Belirtilen dockerfile "docker build . -t nodeapp:latest" komutu ile çalıştırılır. Oluşturulan docker image boyutu 914 MB boyutundadır.

![image](/IMG/5_size.png)

#### Katman Optimizasyonunun Avantajları

* **Daha Küçük Görüntü Boyutu:** Gereksiz katmanların azaltılması, Docker görüntüsünün boyutunu küçültür.
* **Daha Hızlı Dağıtım:** Daha küçük görüntüler, daha hızlı indirilebilir ve dağıtılabilir.
* **Daha Az Depolama Maliyeti:** Daha küçük görüntüler, daha az depolama alanı gerektirir, bu da maliyetleri düşürür.
* **Daha Az Güvenlik Açığı:** Gereksiz dosyaların ve bağımlılıkların temizlenmesi, potansiyel güvenlik açıklarını azaltır.

### "Scratch" Images

Bu yapıyı şu şekilde düşünebiliriz python, go ve C/C++ gibi bir cok dilde yazmış olduğumuz kodu delerek kullanabiliriz. Bu durum için basit bir yapıya sahip olan "Scratch" image kullanılmaktadır.

örneğin 
```dockerfile
FROM scratch

# Çalıştırılabilir dosyayı kopyala
COPY myapp /myapp

# Çalıştırma komutunu belirle
ENTRYPOINT ["/myapp"]

# Uygulama portunu belirle
EXPOSE 8080

```

myapp adlı derlenmiş uygulama docker image içerisine atılır ve çalıştırılması sağlanır. Bu Durum bizim derlenmiş uygulamamız hızlı bir şekilde çalıştırılmasına imkan sunmaktadır.

### Docker Image 'larının Boyunlarının Küçültülmesinin Faydaları

Docker image boyutunun küçülmesi çeşitli avantajlar sağlar. İşte bunlardan bazıları:

* **Daha Hızlı Dağıtım:** CI/CD süreçlerindeki dağıtım sürelerinin azaltılmasına önemli ölçü de katkı sağlar.

* **Depolama ve Bant Genişliği Tasarrufu:** Docker gerek yerel (Local)'de gerekse Cloud sistemlerde önemli yer kaplamaktadır. Docker image boyutlarının küçültülmesi kullanılan disk'te tasarrufu sağlar.

* **Güvenlik:** Genellikle daha az bileşene sahip olan uygulamalarda güvenlik açığı çıkma potansiyeli daha azdır. 
* **Yönetim Kolaylığı:** Daha az bağımlılık ve bileşene sahip olunması daha az güncelleme gerektirir, bu da yönetimi basitleştirir.

* **Daha Hızlı Geliştirme ve Test Döngüleri:** Küçük Docker imageları, daha hızlı oluşturulabilir ve test edilebilir. B durum geliştiricilerin daha hızlı geri bildirim almasını sağlar ve geliştirme döngülerini hızlandırır.

* **Kaynak Kullanımının Azaltılması:** Daha küçük image, daha az kaynak kullanır, bu da özellikle sınırlı kaynaklara sahip ortamlarda (örneğin, geliştirme ve test sunucuları) önemlidir.