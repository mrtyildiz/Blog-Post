## Django Web Server Üzerinde API Kullanımı

İlk öncelikle Django projesinin oluşturulması amacıyla “django-admin startproject api” ve “python3 app/manage.py startapp app” komutları kullanılır.

![](https://github.com/mrtyildiz/Blog-Post/blob/main/Django/img/1.png?raw=true)

Django üzerinde REST API özelliğinin kullanılabilmesi amacıyla “djangorestframework” adlı kütüphane yüklenir. Bu amaç doğrultusunda “pip3 install djangorestframework” komutu kullanılır.

![](https://github.com/mrtyildiz/Blog-Post/blob/main/Django/img/2.png?raw=true)

Oluşturulmuş app klasörünün ve yüklenmiş olan REST Framework kütüphanesinin projeye tanıtılması amacıyla settings.py dosyasında düzenleme yapılır.

![](https://github.com/mrtyildiz/Blog-Post/blob/main/Django/img/3.png?raw=true)

İlk öncelikle app klasörünün içerisine urls.py adlı python script oluşturulur. Oluşturulan urls.py dosyasının içerisine aşağıdaki gibi kullanılacak olan views fonksiyonu import edilir. 

![](https://github.com/mrtyildiz/Blog-Post/blob/main/Django/img/4.png?raw=true)

Oluşturulmuş olan urls.py dosyası api klasörünün altında bulunan urls.py ‘ye import edilir. Bu sayede oluşturulan urls.py ‘de yapılan her navigasyon ayarlamaları proje tarafından kullanılabilir. 

![](https://github.com/mrtyildiz/Blog-Post/blob/main/Django/img/5.png?raw=true)

Yukarıdaki görselde görüldüğü gibi /api/ üzerinde gelen her istek /app/urls.py python script yönlendirilmektedir. 
Kullanılan /app/views.py dosyası içerisinde bulunan “getAPI” fonksiyonu aşağıdaki gibidir. Bu fonksiyondaki temel amaçlı routes değişkeni içerisine yazılan json verisini GET method kullanılarak işlenmesine imkan sunmaktadır.

![](https://github.com/mrtyildiz/Blog-Post/blob/main/Django/img/6.png?raw=true)

Tarayıcı üzerinden Django web server çalıştığı sunucuya GET isteği yapıldığında aşağıdaki görseldeki gibi bir geri dönüş olmaktadır.

![](https://github.com/mrtyildiz/Blog-Post/blob/main/Django/img/7.png?raw=true)
