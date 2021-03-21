# Bash Script Giriş

## Bash Nedir?

Bash, Brian Fox tarafından GNU Projesi için Bourne kabuğuna özgür yazılım alternatifi olarak yazılmış, Unix ve benzeri işletim sistemlerinde kullanılan komut satırı kabuğu ve bu kabuğun betik dilidir. 
Linux tabanlı işlemtim sistemlerinin temel komutlarını bilmek Bash script yazarken oldukça işimizi kolaylaştıracaktır.
Bash öğrenirken uygulamalı gitmesi açısından Sana makine üzerinde bunun Ubuntu Server Windows ortamından SSH ile bağlandım.

Bash script kodlamaya başlamadan önce bir **".sh"** uzantıılı dosya oluşturmak için **"touch"** komutu kullanılması gerekmektedir.
Dosya oluşturulduktan sonra bir text editör kullanılarak basit bir script yazalım. Bash script yazılmaya başlandığından **"#!/bin/bash"** header ekliyoruz.
echo komutu ekrana yazı yazdırma için kullanılan komuttur. Bash script yazıldıktan sonra erişim izinlerini değiştirmek için **"chmod"** komutu kullanılır.
Dosya izinleri belirlendikten sonra bash script dosyası **"./bashscript_Adı"** veya **"bash bashscript_Adı"** yazılarak çalışıtırılır.

![image](https://github.com/mrtyildiz/Blog-Post/blob/main/Linux%20101/img/1.PNG)

Bash script 'de değişken kullanımı aşağıdaki görselde görülmektedir.

![image](https://github.com/mrtyildiz/Blog-Post/blob/main/Linux%20101/img/2.PNG)

**"read"** komutu kullanılarak dışarından veri alınması için kullanılır. Alınan bu veri **NAME** adlı değişkene atanır. Bu değişkenin kullanılması için **"$"** işareti kullanılır.

![image](https://github.com/mrtyildiz/Blog-Post/blob/main/Linux%20101/img/3.PNG)

Terminal üzerinden text editör kullanmadan **"cat > bash-Script.sh"** komutu kullanılarak dosya üzerine yazılabilir. Dosyayı kapatmak ve kaydetmek için **"ctrl + D"** kullanılır.

if kullanımı aşağıdaki gibidir;

if [condition]

then

//if block code

else
 
 // else block code

fi

![image](https://github.com/mrtyildiz/Blog-Post/blob/main/Linux%20101/img/4.PNG)
![image](https://github.com/mrtyildiz/Blog-Post/blob/main/Linux%20101/img/5.PNG)
![image](https://github.com/mrtyildiz/Blog-Post/blob/main/Linux%20101/img/6.PNG)
![image](https://github.com/mrtyildiz/Blog-Post/blob/main/Linux%20101/img/7.PNG)
![image](https://github.com/mrtyildiz/Blog-Post/blob/main/Linux%20101/img/8.PNG)
