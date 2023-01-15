## Kubernetes Üzerinde Python App 

Bu makalede, Kubernetes temellerinden ve basit bir python servisinin kubernetes 'le nasıl konuşturulacağını öğretmeyi amaçlamaktadır.

### Kubernetes Nedir?

Kuberntes, kapsayıcılı uygulmaları dağıtmanıza, ölçeklendirmenize ve yönetmenize olanak tanıyan açık kaynaklı bir kapsayıcı düzenleme sistemidir.

### Kuberntes Termolojisi

- Image: Bir uygulamanın çalıştırılması için gerekli olan Image, uygulama dosyalarının barındıran değiştirilemez dosyadır.
- Container: Çalışan bir Image örneğidir.
- Cluster: Container uygulamaları çalıştıran nodedur
- Node: Kubernetes uygulamalarında çalışan bir nodedur
- Pod: Kubernetes 'in en küçük yapı birimidir.
- Service: Kubernetes içerisinde bir ağ erişimi sağlar
- Docker: Containerların oluşturulması, paylasılması ve çalıştırılması amacıyla kullanılan araçtır.

![](https://raw.githubusercontent.com/mrtyildiz/Blog-Post/main/Kubernetes/img/27.webp)

### Kubectl

Kubernetes cluster yönetilmesinde kullanılan kubectl komutudur. Kubectl komutunun genel kullanımı aşağıdaki gibidir.

````
kubectl <command><type><name><flag>
````

- command: gerçekleştirilmek istenen eylemin belirtildiği yerdir(create, delete, run) 
- type: Kubernetes nesnesidir(pod, service, deployment)
- name: kubernetes nesnesine verilen isimdir.
- flags: ekstra verilmek istenen parametreler buraya gelmektedir.

En sık kullanılan kubectl komutlaro şunlardır;

| Komut    | Açıklama |
|:---------|:--------|
| kubectl get pod/deployment/service    | Seçilen objeyi listelemek için kullanılmaktadır   |
| kubectl apply -f <filename>.yml   | Belirtilen yml dosyasının çalıştırılmasını sağlar   |
| kubectl describe pod <podname>    | Adı belirtilen pod hakkında bilgi verir   |
| kubectl delete pod <podname>    | Adı belirtilen pod'u siler   |
| kubectl logs <podname>    | Adı belirtilen pod 'un loglarını görüntüler   |
| kubectl exec -it <podname> --bash    | Adı belirtilen pod üzerinde komut çalıştırılması izin verir   |

### Kubernetes FastAPI Uygulaması

FastAPI üzerinde geliştirilen uygulamanın kubernetes üzerinden çalıştırılması amacıyla aşağıdaki işlem adımları uygulanır.

İlk öncelikle uygulamanın gerçekleştirilmesi amacıyla  [killercode](https://killercoda.com/killer-shell-cka/scenario/playground) üzerinden işlemin gerçekleştirilmesi amacıyla yeni sunucu start edilir.

![](https://github.com/mrtyildiz/Blog-Post/blob/main/Kubernetes/img/28.png?raw=true)

Oluşturulmuş olan sunucuya git clone komutu kullanılarak ihtiyaç duyacağımız kodlar indirilir.

```
git clone https://github.com/mrtyildiz/KubernetesTutorials.git
```
![](https://github.com/mrtyildiz/Blog-Post/blob/main/Kubernetes/img/29.png?raw=true)

İndirilen kodlar aşağıdaki gibi;

- app.py
```
from fastapi import FastAPI
from uvicorn import run

app = FastAPI()

items = []

@app.post("/items/")
async def create_item(item: dict):
    items.append(item)
    return {"item": item}

@app.get("/items/")
async def read_items():
    return {"items": items}

if __name__ == "__main__":
    run(app, host="0.0.0.0", port=8000)
```

- Dockerfile

```
FROM python:3.11-slim-buster
WORKDIR /app
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt
COPY . .
EXPOSE 8000
CMD ["python3", "app.py"]
```

- requirements.txt

```
anyio==3.6.2
certifi==2022.12.7
charset-normalizer==3.0.1
click==8.1.3
fastapi==0.89.1
Flask==2.2.2
h11==0.14.0
idna==3.4
itsdangerous==2.1.2
Jinja2==3.1.2
mailjet-rest==1.3.4
MarkupSafe==2.1.1
pydantic==1.10.4
requests==2.28.2
sniffio==1.3.0
starlette==0.22.0
typing_extensions==4.4.0
urllib3==1.26.14
uvicorn==0.20.0
Werkzeug==2.2.2
```
- deployment.yml

```
apiVersion: apps/v1 
kind: Deployment 
metadata: 
  name: fastapi-service 
spec: 
  replicas: 2 
  selector: 
    matchLabels: 
      app: fastapi-service 
  template: 
    metadata: 
      labels: 
        app: fastapi-service   
    spec: 
      containers: 
        - name: fastapi-service 
          image: muratyildiz66/fastapi:latest
          ports: 
            - containerPort: 8000 
              protocol: TCP
```

İlk öncelikle kullanacağımız image oluşturmamız gerekmektedir. Bu amaçla ilk öncelikle aşğıdaki komut kullanabilir.
- docker build -t fastapi-service .

![](https://github.com/mrtyildiz/Blog-Post/blob/main/Kubernetes/img/30.png?raw=true)

Oluşturulmuş olan image 'ın dockerhub yüklenmesi amacıyla aşağıdaki iyi komut sırasyla kullanılır.
```
docker tag fastapi-service:latest muratyildiz66/fastapi:latest
docker push muratyildiz66/fastapi:latest
```
Image oluşturma ve yükleme işlemi tamamlandıktan sonra "kubectl apply -f deployment.yml" komut kullanılarak kubernetes uygulaması çalıştırılır. Oluşturulmuş olan deployment'ın görüntülenmesi amacıyla "kubectl get deployment", oluşturulan podların görüntülenmesi amacıyla "kubectl get pods" komutu kullanılır.

![](https://github.com/mrtyildiz/Blog-Post/blob/main/Kubernetes/img/31.png?raw=true)

Oluşturulmuş olan podların loglarının görüntülenmesi amacıyla "kubectl log <pod-name>" komutu kullanılır.

![](https://github.com/mrtyildiz/Blog-Post/blob/main/Kubernetes/img/32.png?raw=true)

Oluşturulan podlara ana makineden ulaşılabilmesi amacıyla port yönlendirme işlemi yapılmıştır. Bu amaçla "kubectl port-forward deployment/fastapi-service 80:8000" komutu kullanılmıştır. 
![](https://github.com/mrtyildiz/Blog-Post/blob/main/Kubernetes/img/33.png?raw=true)

Yönlendirme işleminin ardından 80 portuna POST ve GET isteklerinde bulunulmuştur. Bu amaçla kullanılan komutlar;
```
http POST localhost:80/items/ name=test
http GET localhost:80/items/
```
![](https://github.com/mrtyildiz/Blog-Post/blob/main/Kubernetes/img/34.png?raw=true)

Bu amaçla kullanmış olduğum kodlara [buradan](https://github.com/mrtyildiz/KubernetesTutorials) ulaşabilirsiniz.
