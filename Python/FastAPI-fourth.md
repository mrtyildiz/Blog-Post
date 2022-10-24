## FastAPI HTTP Delete Requests

HTTP istekleri kullnılarak database üzerinde bulunan objenin silinmesi için kullanılabilmektedir. Bu isteğin gerçekleştirilmesi amaçıyla DELETE methodu kullanılmaktadır.
![](https://github.com/mrtyildiz/Blog-Post/blob/main/Python/img/1.png?raw=true)
İlk öncelikle DELETE method uygulayacağımız ve daha önceden oluşturmuş olduğumuz fastapi:2.0 imajı çalıştırılır.
![](https://github.com/mrtyildiz/Blog-Post/blob/main/Python/img/22.png?raw=true)
Bu amaç doğrultusunda "docker run -it -d -p 80:8000 fastapi:2.0" komutu kullanılır.
DELETE method 'un main.py adlı python script eklenmesi amacıyla aşağıdaki delete_users fonksiyonu main.py eklenir ve konteynerın içerisinde eklenmesi amacıyla host makinede bulunan koda eklenir.
```
@app.delete("/api/v1/users/{user_id}")
async def delete_users(user_id: UUID):
    for user in db:
        if user.id == user_id:
            db.remove(user)
            return {"Silinen kullanıcı": user.id}
```
Eklenmiş olan komutun docker konteynerına taşınması amacıyla "docker cp main.py 01610bd15730:/app/" komutu kullanılır. konteynerın yeniden başlatılması amacıyla "docker restart 01610bd15730" komutu kullanılır. Kodda oluşabilecek hataların önceden görülmesi amacıyla "docker logs 01610bd15730" komutu kullanılır.
![](https://github.com/mrtyildiz/Blog-Post/blob/main/Python/img/23.png?raw=true)
Thunter client eklentisi kullanılarak ilk öncelikle GET method kullanılarak var olan objeler görüntülenir.
![](https://github.com/mrtyildiz/Blog-Post/blob/main/Python/img/24.png?raw=true)
Var olan objelerden herhangi birinin id adresi seçilir ve silinmesi amacıyla DELETE method kullanılır.
![](https://github.com/mrtyildiz/Blog-Post/blob/main/Python/img/25.png?raw=true)
Objenin silinip silinmediğinin kontrol edilmesi amacıyla API 'ye yeniden GET isteği gönderilir.
![](https://github.com/mrtyildiz/Blog-Post/blob/main/Python/img/26.png?raw=true)
Görselde görüldüğü gibi seçilmiş olan obje silinmiştir ve yazmış olduğumuz fonksiyon düzgün bir şekilde çalışmaktadır. Ancak olmayan bir ID adresi ile işlem yapılmak istendiğinde response olarak null geri dönüşü olmaktadır ve HTTP kodu olarak 200 dönmektedir. 
![](https://github.com/mrtyildiz/Blog-Post/blob/main/Python/img/27.png?raw=true)

Bu durumu engellemek amacıyla aşağıdaki gibi kodu yeniden düzenlememiz gerekmektedir. Burada her id bulunamadığında 404 olarak dönmekte ve bir uyarı dönmekteyiz. Bu duruma HTTPException neden olmaktadır.
```
@app.delete("/api/v1/users/{user_id}")
async def delete_users(user_id: UUID):
    for user in db:
        if user.id == user_id:
            db.remove(user)
            return {"Remove Users": user.id}
        else:
            raise HTTPException(status_code = 404, detail=  "user with id: {user_id} does not exists")
```
Kodu ekledikten sonra konteynerın yeniden çalışması amacıyla konteyner restart edilir.
![](https://github.com/mrtyildiz/Blog-Post/blob/main/Python/img/28.png?raw=true)

Konteyner restart edildikten sonra Thunter Client uygulaması üzerinden DELETE method isteği tekrar gönderilir.
![](https://github.com/mrtyildiz/Blog-Post/blob/main/Python/img/29.png?raw=true)

Görselde de görüldüğü gibi ID 'i bulunmayan kullanıcıya ait bizim öngördüğümüz şekilde 404 olarak geri dönüş yapmaktadır.
