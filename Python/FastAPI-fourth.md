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
Görselde görüldüğü gibi seçilmiş olan obje silinmiştir ve yazmış olduğumuz fonksiyon düzgün bir şekilde çalışmaktadır.
