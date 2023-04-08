## ChatGPT Kullanılarak Kubernetes CKA Sertifikasına hazırlık

Yaygın ve popüler olan yapay zeka uygulaması olan ChatGPT ile kubernetes üzerine çalışmalar gerçekleştirmek mümkündür. Bu çalışmaların gerçekleştirilmesi amacıyla bir kuberntes ortamı olarak minikube kurulmuştur. Kurulan bu ortamda yapılacak olan çalışmanın belirlenmesi amacıyla ChatGPT uygulamasının dan 15 adet CKA için uygun soru istenmiştir.
![](https://raw.githubusercontent.com/mrtyildiz/Blog-Post/main/Kubernetes/img/Kubernetes-ChatCPT/1.png)

Oluşturulmuş olan soruların çözülmesi ve alıştırma yapmak amacıyla "minikube start --driver=docker" komutu kullanılır. 
![](https://raw.githubusercontent.com/mrtyildiz/Blog-Post/main/Kubernetes/img/Kubernetes-ChatCPT/2.png)

Kurulmuş olan ortam üzerinde ChatGPT 'den almış aldığımız uygulamaları sıralı bir şekilde gerçekleştirebiliriz.
Sorular ve cevapları aşağıdaki gibidir;

1. Bir Kubernetes pod'u nasıl oluşturursunuz? Pod'u nasıl silersiniz?

Cevap: Kubernetes içerisinde var olan pod en küçük birim olarak bilinir ve uygulamanın çalıştırılması için gerekli olanlar pod içerisinde bulunmaktadır. Basit bir pod oluşturmak amacıyla "kubectl run nginx-pod --image=nginx" komutu kullanılır.
![](https://raw.githubusercontent.com/mrtyildiz/Blog-Post/main/Kubernetes/img/Kubernetes-ChatCPT/3.png)

Oluşturulmuş olan pod 'un görüntülenmesi amacıyla "kubectl get pod" komutu silinmesi amacıyla "kubectl delete pod <pod_name>" komutu kullanılır.

![](https://raw.githubusercontent.com/mrtyildiz/Blog-Post/main/Kubernetes/img/Kubernetes-ChatCPT/4.png)

2. Bir Kubernetes deployment'ı nasıl oluşturursunuz? Deployment'ı nasıl güncellersiniz?

Cevap: Kubernetes deployment, Kubernetes üzerinde uygulama dağıtımını yönetmek için kullanılan bir kaynaktır. Deployment, belirli bir uygulamanın birden fazla kopyasını (replica) oluşturmak ve bu kopyaların aynı anda çalışmasını sağlamak için tasarlanmıştır. Replica'lar, belirli bir deployment için belirtilen bir şablon (template) kullanarak oluşturulur. 

Kubernetes üzerinde bir deployment oluşturulması amacıyla "kubectl create deployment nginx-deployment --image=nginx:1.21.0 --replicas=3" komutu kullanılır.

![](https://raw.githubusercontent.com/mrtyildiz/Blog-Post/main/Kubernetes/img/Kubernetes-ChatCPT/5.png)

Oluşturulmuş olan deployment dosyasının güncellenmesi amacıyla "kubectl edit deployments <deployment_name>"
![](https://raw.githubusercontent.com/mrtyildiz/Blog-Post/main/Kubernetes/img/Kubernetes-ChatCPT/6.png)
Açılan notepad üzerinden isteğiniz değişikliği gerçekleştirebilirsiniz. Burada kendi deployments'da replica sayısını değiştirdim.
![](https://raw.githubusercontent.com/mrtyildiz/Blog-Post/main/Kubernetes/img/Kubernetes-ChatCPT/7.png)

3. Bir Kubernetes servisi nasıl oluşturulur? Servisi nasıl silersiniz?

Cevap: Kubernetes servisi, uygulamanın dış dünyadan erişilebilir olmasını sağlar. Servisler, uygulama replica'larına yönlendirilen ağ trafiğini yönetir ve yük dengelemesi yaparak uygulamanın yükünü paylaştırır. Ayrıca servisler, replica'ların değişen IP adreslerine karşı esnek bir şekilde yönetim yapmanızı sağlar. Servisin oluşturulması amacıyla kulanılabilecek service.yml dosyası;

```
apiVersion: v1
kind: Service
metadata:
  name: my-service
spec:
  selector:
    app: my-app
  ports:
    - name: http
      protocol: TCP
      port: 80
      targetPort: 8080
  type: ClusterIP
```

Oluşturulan .yaml dosyasından servisin oluşturulması amacıyla "kubectl apply -f my-service.yaml" komutu kullanılır. 
![](https://raw.githubusercontent.com/mrtyildiz/Blog-Post/main/Kubernetes/img/Kubernetes-ChatCPT/8.png)

oluşturulmuş olan servisin silinmesi amacıyla "kubectl delete -f my-service.yaml" veya "kubectl delete svc <service-name>" komutu kullanılır.

![](https://raw.githubusercontent.com/mrtyildiz/Blog-Post/main/Kubernetes/img/Kubernetes-ChatCPT/9.png)

4. Bir Kubernetes volume nasıl oluşturulur? Volume nasıl silinir?

Kubernetes volume, bir pod içindeki verilerin depolanmasını sağlar. Bir volume, pod ömrü boyunca verileri saklar ve pod yeniden oluşturulduğunda bile verilerin kaybolmasını önler. Volume oluşturulması amacıyla my-volume.yaml adlı dosyas oluşturulur;

```
apiVersion: v1
kind: PersistentVolume
metadata:
  name: my-volume
spec:
  capacity:
    storage: 1Gi
  accessModes:
    - ReadWriteOnce
  persistentVolumeReclaimPolicy: Retain
  storageClassName: my-storage-class
  hostPath:
    path: /data/my-volume

```

Oluşturulmuş olan my-volume.yaml dosyasın kullanılarak volume oluşturma işlemi için "kubectl apply -f my-volume.yaml" komutu kullanılır. 
![](https://raw.githubusercontent.com/mrtyildiz/Blog-Post/main/Kubernetes/img/Kubernetes-ChatCPT/10.png)

Oluşturulmuş olan volume silinmesi amacıyla "kubectl delete -f my-volume.yaml" veya "kubectl delete PersistentVolume my-volume" komutu kullanılmaktadır.
![](https://raw.githubusercontent.com/mrtyildiz/Blog-Post/main/Kubernetes/img/Kubernetes-ChatCPT/11.png)

5. Bir Kubernetes konfigürasyon haritası (configMap) nasıl oluşturulur? Konfigürasyon haritası nasıl silinir?

Kubernetes configMap, bir pod'un çalışma zamanında ihtiyaç duyabileceği yapılandırma bilgilerini depolamak için kullanılır. Bu yapılandırma bilgileri, pod'a doğrudan yerleştirilmeden önce configMap üzerinde tanımlanır ve pod çalıştırıldığında bu bilgiler kullanılır. Bir configMap 'in oluşturulması amacıyla "my-configmap.yaml" adlı dosya oluşturulur.

```
apiVersion: v1
kind: ConfigMap
metadata:
  name: my-configmap
data:
  DB_HOST: db.example.com
  DB_PORT: "5432"
  DB_NAME: mydatabase
```
Oluşturulmuş olan "my-configmap.yaml" adlı dosyanın çalıştırılması amacıyla "kubect apply -f my-configmap.yaml" komutu kullanılmaktadır.

![](https://raw.githubusercontent.com/mrtyildiz/Blog-Post/main/Kubernetes/img/Kubernetes-ChatCPT/12.png)

Oluşturulmuş olan Configmap'in silinmesi amacıyla "kubectl delete -f my-configmap.yaml" veya "kubectl delete configmap <configmap-name>" komutu kullanılır.

![](https://raw.githubusercontent.com/mrtyildiz/Blog-Post/main/Kubernetes/img/Kubernetes-ChatCPT/13.png)

6. Bir Kubernetes secret nasıl oluşturulur? Secret nasıl silinir?

Kubernetes secret, pod'ların çalışma zamanında ihtiyaç duyabileceği hassas bilgileri (örneğin, şifreler, kimlik bilgileri vb.) depolamak için kullanılır. Bu hassas bilgiler, pod'a doğrudan yerleştirilmeden önce secret üzerinde tanımlanır ve pod çalıştırıldığında bu bilgiler kullanılır.

Secret uygulamasının gerçekleştirilmesi amacıyla "my-secret.yaml" adlı dosya oluşturulur.
```
apiVersion: v1
kind: Secret
metadata:
  name: my-secret
type: Opaque
data:
  username: dXNlcm5hbWU=
  password: cGFzc3dvcmQ=
```
Oluşturulmuş olan "my-secret.yaml" dosyasının çalıştırılması amacıyla "kubectl -f apply my-secret.yaml" komutu kullanılır.

![](https://raw.githubusercontent.com/mrtyildiz/Blog-Post/main/Kubernetes/img/Kubernetes-ChatCPT/14.png)

Oluşturulmuş olan secret 'ın silinmesi amacıyla "kubectl delete secret my-secret" ve "kubectl delete -f my-secret.yaml" komutlarından herhangi bir kullanılır.

![](https://raw.githubusercontent.com/mrtyildiz/Blog-Post/main/Kubernetes/img/Kubernetes-ChatCPT/15.png)

7. Bir Kubernetes ingress nasıl oluşturulur? Ingress nasıl silinir? /// soruyu tekrar yap

Kubernetes'te ingress, HTTP veya HTTPS üzerinden bir Kubernetes servisine yönlendirmeleri yapılandırmak için kullanılan bir kaynaktır. Ingress, belirli bir host ve yol için bir veya daha fazla hedef servis belirtebilir.

Ingress için kullanılacak olan bir servis 'e ihtiyaç duymaktayız bu nedenle ilk öncelikle servisin oluşuturulması amacıyla "servis.yaml" dosyası oluşturulur. 

```
apiVersion: v1
kind: Service
metadata:
  name: my-service
spec:
  selector:
    app: my-app
  ports:
    - name: http
      port: 80
      targetPort: 8080

```

![](https://raw.githubusercontent.com/mrtyildiz/Blog-Post/main/Kubernetes/img/Kubernetes-ChatCPT/16.png)

Servisin oluşturulması amacıyla "kubectl apply -f servis.yaml" komutu kullanılır. Ingress oluşturulması amacıyla my-ingress.yaml dosyası oluşturulur ve "kubectl apply -f my-ingress.yaml" komutu kullanılır.

```
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: my-ingress
spec:
  rules:
    - host: mydomain.com
      http:
        paths:
          - path: /myapp
            pathType: Prefix
            backend:
              service:
                name: my-service
                port:
                  name: http


```
![](https://raw.githubusercontent.com/mrtyildiz/Blog-Post/main/Kubernetes/img/Kubernetes-ChatCPT/17.png)

Oluşturulmuş olan ingresslerin silinmesi için "kubectl delete -f my-ingress.yaml" dosyası kullanılır. 

![](https://raw.githubusercontent.com/mrtyildiz/Blog-Post/main/Kubernetes/img/Kubernetes-ChatCPT/18.png)

8. Bir Kubernetes job nasıl oluşturulur? Job nasıl silinir?

Bir Kubernetes job, bir görevin yalnızca bir kez veya belirli bir zaman aralığında yürütülmesi için kullanılır. İşleri oluşturmak ve silmek için kubectl komutlarını kullanabilirsiniz. Kubernetes ortamında Job oluşturulması amacıyla "kubectl create job my-job --image=my-image" komutu kullanılabilir.

Oluşturulan Job 'un silinmesi amacıyla "kubectl delete job my-job" komutu kullanılabilir. "kubectl delete" komutunun başarısız olaması durumunda;

* kubectl delete jobs --field-selector=status.successful=1
* kubectl delete jobs --field-selector=status.failed=1

komutları sırasıyla kullanılabilir.

9. Bir Kubernetes cron job nasıl oluşturulur? Cron job nasıl silinir?

Bir Kubernetes cron job, belirli aralıklarla tekrarlanan görevler için kullanılır. Bu tür görevler genellikle sistem bakımı, veritabanı yedekleme veya diğer rutin görevlerdir. Bir cron job oluşturmak ve silmek için kubectl komutlarını kullanabilirsiniz.
Crontab oluşturma işlemi için "kubectl create cronjob my-cronjob --image=my-image --schedule="0 * * * *"" komutu kullanılabilir. Bu sayede belirli aralıklarla işlemler otomatik olarak tekrar edebilmektedir.

Oluşturulmuş olan Crontab 'ın silinmesi amacıyla "kubectl delete cronjob my-cronjob" komutu kullanılmaktadır. Silinme işleminin başarısız olması durumunda aşağıdaki komutlar sırasıyla çalıştırılır;

* kubectl delete jobs --field-selector=status.successful=1
* kubectl delete jobs --field-selector=status.failed=1

10. Bir Kubernetes namespace nasıl oluşturulur? Namespace nasıl silinir?

Kubernetes'te namespace'ler, kaynakların kapsamını belirlemek için kullanılır. Aynı Kubernetes kümesi içinde birden fazla kullanıcının veya takımın ayrı ayrı kaynaklarını yönetmesine izin verir. Bir namespace oluşturmak ve silmek için kubectl komutlarını kullanabilirsiniz. Kubernetes üzerinde namespace oluşturulması amacıyla "kubectl create namespace my-namespace" komutu kullanılır.

Oluşturulmuş olan namespace silinmesi amacıyla "kubectl delete namespace my-namespace" komutu kulanılır.

11. Bir Kubernetes etiketi (label) nasıl eklenir? Etiket nasıl silinir?

Kubernetes'te namespace'ler, kaynakların kapsamını belirlemek için kullanılır. Aynı Kubernetes kümesi içinde birden fazla kullanıcının veya takımın ayrı ayrı kaynaklarını yönetmesine izin verir. Bir namespace oluşturmak ve silmek için kubectl komutlarını kullanabilirsiniz. Kubernetes içerisinde label tanımlamasının yapılabilemesi amacıyla bir pod oluşturulur. Pod üzerinde label tanımlamasının yapılabilmesi adına "kubectl label pod my-pod env=prod" komutu kullanılır

![](https://raw.githubusercontent.com/mrtyildiz/Blog-Post/main/Kubernetes/img/Kubernetes-ChatCPT/19.png)

Tanımlamış olduğumuz bu label 'ın görüntülenebilmesi amacıyla pod "kubectl describe pod my-pod" komutuyla incelenir.

![](https://raw.githubusercontent.com/mrtyildiz/Blog-Post/main/Kubernetes/img/Kubernetes-ChatCPT/20.png)

Tanımlanmış olan label silinmesi amacıyla "kubectl label pod my-pod env-" komutu kullanılır.

![](https://raw.githubusercontent.com/mrtyildiz/Blog-Post/main/Kubernetes/img/Kubernetes-ChatCPT/21.png)

12. Bir Kubernetes hizmet hesabı (service account) nasıl oluşturulur? Hizmet hesabı nasıl silinir?

Kubernetes'te hizmet hesapları, bir Pod veya başka bir kaynak için kimlik doğrulama bilgilerini sağlayan nesnelerdir. Hizmet hesapları, bir Pod'un diğer kaynaklarla (örneğin, ConfigMaps, Secrets) iletişim kurmasına veya bir Pod'un Kubernetes API'siyle etkileşim kurmasına izin verir. Kubernetes içerisinde service account oluşturulması amacıyla "my-serviceaccount.yaml"dosyası oluşturulur ve "kubectl apply -f my-serviceaccount.yaml"

```
apiVersion: v1
kind: ServiceAccount
metadata:
  name: my-serviceaccount
```

![](https://raw.githubusercontent.com/mrtyildiz/Blog-Post/main/Kubernetes/img/Kubernetes-ChatCPT/22.png)

Oluşturulmuş olan bu service-account silinmesi amacıyla "kubectl delete -f my-serviceaccount.yaml" komutu kullanılır.

![](https://raw.githubusercontent.com/mrtyildiz/Blog-Post/main/Kubernetes/img/Kubernetes-ChatCPT/23.png)


13. Bir Kubernetes node'unda çalışan pod'ları nasıl listelersiniz?

Node, Kubernetes kavramında bir worker machine (işçi makine) olarak tanımlanır ve Kubernetes cluster'ında, pod'ların çalıştığı fiziksel veya sanal bir sunucudur. Node, Kubernetes cluster'ında kaynakların kullanımını ve dağıtımını yönetmek için kullanılır. 

Varolan nodeların görüntülenmesi amacıyla "kubectl get node" komutu kullanılır. 

![](https://raw.githubusercontent.com/mrtyildiz/Blog-Post/main/Kubernetes/img/Kubernetes-ChatCPT/24.png)

Şuan bir minikube ortamında olduğum için tek node üzerinden çalılmaktayım. minikube node üzerinde çalışan podların görüntülemek amacıyla "kubectl get pods -n default --field-selector spec.nodeName=minikube" komutu kullanılır.

![](https://raw.githubusercontent.com/mrtyildiz/Blog-Post/main/Kubernetes/img/Kubernetes-ChatCPT/25.png)


14. Bir Kubernetes pod'unun günlüklerini (logs) nasıl görüntülersiniz?

Kubernetes sistemimiz üzerinde çalışan pod'un logların görüntülenmesi mümkündür. Bu işlem için "kubectl logs <pod-name>" komutu kullanılabilir.

![](https://raw.githubusercontent.com/mrtyildiz/Blog-Post/main/Kubernetes/img/Kubernetes-ChatCPT/26.png)


15. Bir Kubernetes deployment'ının hemen silinmesini sağlamak için hangi komutu kullanırsınız?

Hali hazırda var olan bir deployment hemen silinmesi amacıyla "kubectl delete deployment nginx-deployment --cascade=false" komutu kullanılmaktadır.

![](https://raw.githubusercontent.com/mrtyildiz/Blog-Post/main/Kubernetes/img/Kubernetes-ChatCPT/27.png)

--cascade=false argümanı, deployment'a bağlı tüm kaynakların da silinmemesini sağlar, yani sadece deployment silinir, pod'lar, replica set'ler, hizmetler vb. silinmez. Bu, deployment'ı hızlıca silmeniz gerektiğinde kullanışlıdır. Ancak, bu, diğer kaynakların elle silinmesi gerektiği anlamına gelir.
