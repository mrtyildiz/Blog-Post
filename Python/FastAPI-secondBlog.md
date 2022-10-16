# FastAPI 

## HTTP request methods

HTTP, belirli bir kaynak için gerçekleştirilecek istenen eylemi belirlemek amacıyla bir dizi istek yöntemi kullanılır.  Kullanılan istek türlerinin her birinin farklı göre ve yapıları bulunmaktadır. HTTP methodları aşağıdaki gibidir;
![](https://github.com/mrtyildiz/Blog-Post/blob/main/Python/img/1.png?raw=true)
* GET: GET yöntemi, belirtilen kaynağın bir temsilini ister. GET kullanan istekler yalnızca veriler alınmaktadır.

```
from fastapi import FastAPI
app = FastAPI()

@app.get("/")
def root():
    return {"Hello": "Murat"}
```
* HEAD: HEAD yöntemi, bir GET isteğine benzer, ancak yanıt body olmadan bir yanıt ister.

* POST: POST yöntemi, belirtilen kaynağa bir obje ekleme veya güncellem işlemi gönderilmektedir.

* DELETE: DELETE yöntemi belirtilen kaynaktaki objeyi silmektedir.
* CONNECT: CONNECT yöntemi, hedef kaynak tarafından tanımlanan sunucuya bir tunnel kurar.
* OPTIONS: OPTIONS yöntemi, hedef kaynak için iletişim seçeneklerini açıklar.

## FastAPI - UserModel

Temel anlamda FastAPI üzerinden hızlı bir şekilde belli bir model üzerinden RESTAPI oluşturulabilmektedir. Bu kapsamda aşağıdaki görselde görüldüğü gibi bir yapı kullanılır.

![](https://github.com/mrtyildiz/Blog-Post/blob/main/Python/img/7.png?raw=true)

Görselde görüldüğü gibi client üzerinden gönderilen istekler FastAPI üzerinden database 'e iletilir. Bu bağlamda bir model oluşturulması amacıyla FastAPI uygulamamıza "models.py" python script eklenir. models.py;
```
from typing import Optional, List
from uuid import UUID, uuid4
from pydantic import BaseModel
from enum import Enum

class Gender(str, Enum):
    male = "male"
    female = "female"

class Role(str, Enum):
    admin = "admin"
    user = "user"
    student = "student"

class User(BaseModel):
    id: Optional[UUID] = uuid4
    first_name: str
    last_name: str
    middle_name: Optional[str]
    gender: Gender
    roles: List[Role]
```
Oluşturulmuş olan bu models.py dosyasının kullanılası ve yeni objelerin eklenmesi amacıyla aşağıdaki main.py dosyası kullanılır;

```
from typing import List
from uuid import uuid4
from fastapi import FastAPI
from models import User, Gender, Role

app = FastAPI()

db: List[User] = [
    User(
        id=uuid4(),
        first_name="Murat",
        last_name="yildiz",
        gender=Gender.male,
        roles=[Role.student]
    ),
    User(
        id=uuid4(),
        first_name="Ülkü",
        last_name="yildiz",
        gender=Gender.female,
        roles=[Role.admin, Role.user]
    )
]

@app.get("/api/v1/users")
async def fetch_users():
    return db;

@app.post("/api/v1/users")
async def register_user(user: User):
    db.append(user)
    return {"id": user.id}
```
Yukarıdaki örnekte görüldüğü gibi bir GET ve POST örneği bulunmaktadır. Buradaki örneğin çalıştırılması amacıyla aşağıdaki Dockerfile dosyası kullanılır;
```
FROM python:latest

RUN apt-get install -y && apt-get update -y && apt-get upgrade -y
RUN pip3 install fastapi
RUN pip install "uvicorn[standard]"
RUN mkdir app
COPY main.py /app/
COPY models.py /app/
WORKDIR /app/
ENTRYPOINT ["uvicorn","main:app","--host","0.0.0.0","--reload"]
```
Dockerfile ile yeni bir imajın oluşturulması amacıyla "docker build . -t fastapi:2.0" komutu kullanılmaktadır.

![](https://github.com/mrtyildiz/Blog-Post/blob/main/Python/img/8.png?raw=true)

Oluşturulmuş olan fastapi:2.0 imajının çalıştırılması amacıyla "docker run -it -d -p 80:8000 fastapi:2.0" komutu kullanılır. Buradaki komutta default olarak 8000 portunda çalışan fastapi'ye 80 portundan ulaşılabilmesi amacıyla 80:8000 ibaresi kullanılmıştır. Çalışan konteynerların görüntülenebilmesi amacıyla "docker ps" komutu kullanılmıştır.
![](https://github.com/mrtyildiz/Blog-Post/blob/main/Python/img/9.png?raw=true)

Oluşturulmuş olan API 'nin kontrol edilmesi amacıyla http komutu üzerinden istek atılır.

![](https://github.com/mrtyildiz/Blog-Post/blob/main/Python/img/10.png?raw=true)

"http" komutu ile GET isteği FastAPI 'ye gönderilmektedir. FastAPI 'ye POST isteğinin gönderilmesi amacıyla rest client aracına ihtiyaç duyulmaktadır. Bu nedenle Thunder Client aracı kurulur ve çalıştırılır.

![](https://github.com/mrtyildiz/Blog-Post/blob/main/Python/img/11.png?raw=true)

Thunder Client aracı çalıştırılır ilk öncelikle POST method 'u kullanılarak /api/v1/users path 'e yeni obje oluşturulması amacıyla json ifade gönderilir.
![](https://github.com/mrtyildiz/Blog-Post/blob/main/Python/img/12.png?raw=true)

Göderilen isteğin başarılı olmasının ardından eklenen yeni verinin kontrol edilmesi amacıyla Thunder Client aracı kullanılarak /api/v1/users path'e GET isteği gönderilmektedir.
![](https://github.com/mrtyildiz/Blog-Post/blob/main/Python/img/13.png?raw=true)
