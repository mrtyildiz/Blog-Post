# Kubernetes

## Kubernetes Pod kavramı 

Kubernetes temel taşlarından biri olarak kabul edilen Podlara konteynerların çalışma alanları diyebiliriz. Pod bir veya birden fazla uygulama aynı anda pod içerisinde çalışabilmektedir. Pod yapısı kullanılarak kullanılacak olan kaynaklar kapsamı kolaylaylıklar Pod oluşturacak olan .yaml dosyası içerisinde belirtilebilmektedir. Bunlar;
* Depolama alanı
* IP adresi veya bağlı bulunacağı subnet adresi
* Port Adresi
* Kullanılacak olan Imaj adı

Pod yapısının mantığı kullanılarak yatay mimaride sistem istenile ölçekte büyüyebilir olmaktadır. Yapı özelinde sistemin kolaylıkla güncellenmesine imkan sunmaktadır.

## Kubernetes üzerinde Pod Oluşturma işlemi 

Kuberntes üzerinde pod oluşturma işlemi için ilk öncelikle .yaml dosyasının oluşturulması gerekmektedir. Bu nedenle nginx imajı kullanılarak 2 replika olacak biçimde pod oluşturulması amacıyla aşağıdaki yaml dosyası kullanılmaktadır.
```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  selector:
    matchLabels:
      app: nginx
  replicas: 2 
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.14.2
        ports:
        - containerPort: 80
```
Örnekte görülen nginx-deployment isimli pod 80 nolu port adresini kullanabilecek şekilde tasarlanmıştır. [Buraya](https://kubernetes.io/docs/tasks/run-application/run-stateless-application-deployment/) tıklayarak örneğin web adresine ulaşabilirsiniz. Örnekte olan pod.yaml dosyasının çalıştırılması amacıyla "kubectl apply  -f pod.yaml" komutu kullanılmaktadır.

![](https://github.com/mrtyildiz/Blog-Post/blob/main/Kubernetes/img/20.png?raw=true)

Oluşturulmuş olan pod'a ait bütün bilgilerin görüntülenmesi amacıyla "kubectl describe pod <pod_adı>" komutu kullanılarak bilgiler elde edilmektedir.

![](https://github.com/mrtyildiz/Blog-Post/blob/main/Kubernetes/img/21.png?raw=true)

Çalışmakta olan podların içerisinde 80 portunda çalışmakta index.html görüntülenmesi amacıyla "kubectl -it <pod_adı> bash" komutu ile bir shell elde edilir. Elde edilen shell ile "curl http://localhost" komutu kullanılan servisin çalışma durumu belirlenir ve index.html içerisinde var olan bilgiler görüntülenmektedir.

![](https://github.com/mrtyildiz/Blog-Post/blob/main/Kubernetes/img/22.png?raw=true)

Görüldüğü gibi sadece pod içerisinde bulunan servise sadece local üzerinde bağlanabilmekteyiz. Servisi uzaktan erişelebilir hale getirilmesi amacıyla kubernetes üzerinde  port forwading işlemine tabi tutulması gerekmektedir.

## Kubernetes Üzerinden Port Forwading İşlemi

Pod üzerinden çalışan servise host makinenin localinden ulaşılabilmesi amacıyla Port Forwading işlemine tabi tutulabilir. Bu işlem için ilk öncelikle kubernetes üzerinde çalışan pod adresleri kontrol edilir. Bu işlem için "kubectl get pods" komutu kullanılar. Bu komut ile çalışan podların adları status bilgileri gibi temel bilgiler elde edilir. Elde edilen Pod adı bilgisi kullanılarak Port Forwading işlemi için "kubectl port-forward <Pod_Name> 30080:80"

![](https://github.com/mrtyildiz/Blog-Post/blob/main/Kubernetes/img/23.png?raw=true)

Görselde görüldüğü gibi localhost(127.0.0.1)'dan 30080 'e yapılan her istek çalışmakta olan pod 'un 80 portuna yönlendirilmektedir. Bu isteğin kontrol edilmesi amacıyla browser üzerinden istekte bulunulur.

![](https://github.com/mrtyildiz/Blog-Post/blob/main/Kubernetes/img/24.png?raw=true)

Görselde görüldüğü gibi istek başarılı bir şekilde servise iletilmiştir.

## Kubernetes Services Kavramı 

Bir önceki başlıkta gördüğümüz gibi birden fazla replica pod oluşturduğumuzda port yönlendirmeyi sadece belirli pod üzerinde gerçekleştirmekteyiz. Bu durum uygulamalarımızın sağlıklı bir şekilde çalışmasına engel olmaktadır. Kubernetes yapısı içerisinde replica podlara tek bir port adresi üzerinden uzaktan ulaşılabilmesi adına services kavramı ortaya çıkmaktadır. Bu kavramın daha iyi anlaşılması adına aşağıdaki görselde görüldüğü gibi;

![](https://github.com/mrtyildiz/Blog-Post/blob/main/Kubernetes/img/25.png?raw=true)

Browser üzerinden belirli port adresinde gönderilen istek ilk öncelikle services 'e gelmektedir. Services 'e gelen istek kubernetes mimarisinde en uygun olan replica pod 'a yönlendirilimektedir. Önceki örneğimizde iki adet replica'dan olan bir nginx pod 'u oluşturulmuştur. Servisin oluşturulması adına nginx-service.yaml dosyası oluşturulur.
```
apiVersion: v1
kind: Service
metadata:
  name: service-nginx
spec:
  type: NodePort
  selector:
    app: nginx
  ports:
    - port: 80
      targetPort: 80
      nodePort: 31111
```

Bu yaml dosyasında bulunan kavramlar ve anlamları aşağıdaki gibidir;

* metadata:name - Oluşturulmuş olan servisin DNS adı olarak kullanılacak olann addır.
* spec:selector - Dahil olacağı pod 'un adının tanımlanması amacıyla addır.
* spec:ports - Port adreslerinin belirlenmesi amacıyla kullanılan bölümdür.

Servisin oluşturulması amacıyla "kubectl apply -f service-nginx.yaml" komutu kullanılmaktadır. Kubernetes üzerinde oluşturulmuş olan servislerin görüntülenmesi amacıyla "kubectl get all" veya "kubectl get services" komutu kullanılmaktadır. Servislerin görüntülenmesiyle pod 'a bağlantı için kullanılacak olan port adresi belirlenir. Kubernetes içerisinde var olan node 'ların ayrıntılı bir biçinde görüntülebilmesi amacıyla "kubectl get nodes -o wide" komutu kullanılır. Kullanılan komut ile kubernetes içerisinde bulunan External ve Internal IP adreslerininin görüntülenmesi sağlanmıştır. Local bir networkte bulunduğumuz için 192.168.49.2 IP adresinin 31111 nolu Portuna bir curl isteği gönderilir. Bu şekilde yapılmasının ana sebebi minikube üzerinden çalışmasıdır.

![](https://github.com/mrtyildiz/Blog-Post/blob/main/Kubernetes/img/26.png?raw=true)

