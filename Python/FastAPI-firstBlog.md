# Fast API Giriş 

Merhabalar bu blog serilerisinde temel anlamda Fast API 'nin çalışma mantığı ve kullanılması ilgili anlatımlar olacaktır.
Şimdiden keyifli okumalar ve iyi çalışmalar dilerim :)
![](https://github.com/mrtyildiz/Blog-Post/blob/main/Python/img/1.png?raw=true)
## Fast API 'nin Kurulumu

Genel anlamda kullanacağımız ortamın hazırlanması amacıyla docker teknolojisinde faydalanacağız. Docker içerisinde hali hazırda var olan bir python imajını kullanacağız. Bu imajın indirilmesi amacıyla "docker pull python" komutu kullanılır. Indirmiş olduğumuz bu image ister bash ile çalıştırıp içerisine manuel kurulumları gerçekleştirebilir. İstersek de bir dockerfile oluşturup build edebilir. Bu işlem için kullanabileceğimiz dokerfile aşağıdaki gibidir;

```
FROM python:latest
RUN apt-get install -y && apt-get update -y && apt-get upgrade -y
RUN pip3 install fastapi
RUN pip install "uvicorn[standard]"
RUN mkdir app
COPY main.py /app/
WORKDIR /app/
ENTRYPOINT ["uvicorn","main:app","--host","0.0.0.0","--reload"]
```
Yukarıdaki dockerfile görüldüğü gibi konteynerın içerisine main.py adlı bir python script eklenmesi gerekmektedir. Python script 'in içeriği aşağıdaki gibidir;
```
from typing import Union
from fastapi import FastAPI
app = FastAPI()
@app.get("/")
def read_root():
    return {"Hello": "World"}
```
Oluşturulmuş olan dockerfile ve main.py adlı python script'ti ile konteyner oluşturulması amacıyla aşağıdaki işlem adımları sırasıyla izlenir.
1-Adım; İmajın oluşuturulması amacıyla "docker build . -t fastapi:1.0" komutu kullanılır.
![](https://github.com/mrtyildiz/Blog-Post/blob/main/Python/img/2.png?raw=true)

2-Adım; Oluşturulmuş olan fastapi:1.0 imajının çalıştırılması amacıyla "docker run -it -d -p 80:8000 fastapi:1.0" komutu kullanılır. Buradaki komutta default olarak 8000 portunda çalışan fastapi'ye 80 portundan ulaşılabilmesi amacıyla 80:8000 ibaresi kullanılmıştır. Çalışan konteynerların görüntülenebilmesi amacıyla "docker ps" komutu kullanılmıştır.
![](https://github.com/mrtyildiz/Blog-Post/blob/main/Python/img/3.png?raw=true)

3-Adım; Oluşturulmul olan API 'nin kontrol edilmesi amacıyla curl komutu üzerinden istek atılır.

![](https://github.com/mrtyildiz/Blog-Post/blob/main/Python/img/4.png?raw=true)


FastAPI 'nin güzel özelliklerinden biri olan /docs path ile yazmakta olduğunuz API 'ye gönderilecek olan istekler kontrol edilebilmektedir. Bu sayede otomatik oluşan dokümanı inceleyebilirsiniz.

![](https://github.com/mrtyildiz/Blog-Post/blob/main/Python/img/5.png?raw=true)

/docs path benzer bir şekilde alternatif pathlerin görüntülenmesine imkan sunmaktadır.

![](https://github.com/mrtyildiz/Blog-Post/blob/main/Python/img/5.png?raw=true)
