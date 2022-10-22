## FastAPI Swagger, Docs ve Redoc Kavramları

Merhabalar önceki bloğumda Doc ve Redoc kavramlarından kısa olarak bahsetmiştim. Önceki bloğuma [buradan](https://medium.com/@muratasnb/fastapi-giri%C5%9F-798edbda01ec)  ulaşabilirsiniz.
![](https://github.com/mrtyildiz/Blog-Post/blob/main/Python/img/1.png?raw=true)
Bu kavramların daha iyi anlaşılması adına önceki bloğumda oluşturmuş olduğumuz fastapi:2.0 adlı imajı yeniden çalıştırılması germektedir. Bu nedenle "docker run -it -d -p 80:8000 fastapi:2.0" komutu kullanılarak istemiş olduğumız docker konteynerı çalıştırılır.
![](https://github.com/mrtyildiz/Blog-Post/blob/main/Python/img/14.png?raw=true)

Konteyner çalıştırıldıktan sonra host makinenin IP adresi kullanılarak 80 portuna browser docs path'e istek gönderilir. 
![](https://github.com/mrtyildiz/Blog-Post/blob/main/Python/img/15.png?raw=true)
Burada görselde  görüldüğü gibi bir "Internal Server Error /openapi.json" hatası alınmaktadır. Bu hatanın giderilmesi amacıyla uygulamamızı çalıştırmakta oluduğumuz model.py dosyasını düzenleyeceğiz. Burada kullanmış olduğumuz id adresinin değişkeni pasif hale getirilir.
![](https://github.com/mrtyildiz/Blog-Post/blob/main/Python/img/16.png?raw=true)
Dosya kayıt edildikten sonra konteyner yeniden başlatılır. Sonrasında bowser üzerinden yeniden gönderilir. 
![](https://github.com/mrtyildiz/Blog-Post/blob/main/Python/img/17.png?raw=true)

Görselde görülen ekran üzerinden GET ve POST isteklerimizi gerçekleştirebilmekteyiz. İlk öncelikle açılan swagger üzerinden GET methodu açılır ve "Try it out" butonuna tıklanılır. Sonrasında isteğin gerçekleştirilmesi amacıyla "Execute" butonuna tıklanılır. "server response" kısmında API üzerinden gelen cevapları aşağıdaki görselde görüldüğü gibidir.
![](https://github.com/mrtyildiz/Blog-Post/blob/main/Python/img/18.png?raw=true)
Görselde görüldüğü gibi kullanılabilecek Curl komutu ve Request URL görülmektedir.

Swagger üzerinden POST isteğinin gönderilmesi amacıyla "Try it out" butonuna tıklanılır. Request body kısmı düzenlenilir ve "Execute" butonu kullanılarak istek gönderilir.
![](https://github.com/mrtyildiz/Blog-Post/blob/main/Python/img/19.png?raw=true)
Gönderilen request 'e ait response 'nın incelenmesi amacıyla Responses kısmı incelenir.
![](https://github.com/mrtyildiz/Blog-Post/blob/main/Python/img/20.png?raw=true)

Görselde görüldüğü gibi kullanılabilecek örnek curl komutu ve isteğin atılmış olduğu Request URL bulunmaktadır. "Server response" olarak HTTP kodu ve response body kısmı bulunmaktdır.

### Fastapi redoc kavramı

FastAPI 'de bulunan /redoc path'i oluşturmuş olduğumuz pathler hakkında bilgi vermektedir. Bu bilgiler;
* Pathlerin methodları
* Request Body Schema
* Response HTTP kod bilgileri

![](https://github.com/mrtyildiz/Blog-Post/blob/main/Python/img/21.png?raw=true)
