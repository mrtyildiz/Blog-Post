## PostgresSQL Veritabanlarında Barman Kullanımı

Bu yazımızda popüler veritabanlarından biri olan postgresql üzerinden backup alma işleminin nasıl olması gerektiğini ve bu işlemin nasıl yönetileceğini anlatmaya çalışacağım. Backup alma işlemi için Barman uygulaması kullanılmaktadır. Barman uygulaması açık kaynak kodlu ve olağanüstü durumlarda sistemin yeniden çalışır hale getirilmesi amacıyla kullanılmaktadır. Barman 'in temel yetenekleri aşağıdaki gibidir;

* Aynı sunucu üzerinde yedek oluşturabilirsiniz.
* Farklı bir yedekleme sunucusuna yedek oluşturabilirsiniz.
* Birden çok PostgreSQL küme yedeği oluşturabilirsiniz.
* PostgreSQL'in farklı ana sürümlerinde çalışan birden fazla PostgreSQL Kümesini yedekleyebilirsiniz. Böylece yedeklerinizi merkezi bir yedekleme sunucusunda toplayabilirsiniz.
* Barman ile 2 farklı şekilde yedek oluşturabilirsiniz:
  -  rsync / ssh
  - streaming

Barman uygulaması üzerinde çalışabilmek adına aşağıdaki adımları izlerek Barman kurulumunu gerçekleştirelim;

### Barman Kurulumu

Barman kurulumu için ubuntu bionic veya daha üst bir versiyona sahip olan bir sunucu tercih edilmelidir. Bu amaç doğrultusunda bu uygulama biz ubuntu 20.04 sürümünü kullanacağız. Barman kurulması amacıyla gerekli paketlerin yüklenmesi amacıyla ubuntu paketleri yüklenir;

* sudo apt-get update && sudo apt-get upgrade -y

Barman uygulamasının yüklenmesi amacıyla;
* sudo apt-get barman 

### Barman Yapılandırma İşlemi

Barman uygulaması için iki farklı sunucu kullanılması önerilmektedir. Bir sunucu üzerinde Barman uyguması kullanılırken diğer sunucu üzerinde postgresql veritabanı kullanılmaktadır. Veritabanı sunucusu üzerinde aşağıdaki işlem adımları yapılmalıdır.

Terminal üzerinde postgres kullanıcısına geçiş yapılır;

* sudo -i -u postgres

postgres kullanıcısının yetkileri kullanılarak barman kullanıcısı aktif edilir.

* createuser --interactive -P barman
  
![](https://github.com/mrtyildiz/Blog-Post/blob/main/Database/img/1.png?raw=true)

Postgresql 'in dışarından ulaşılabilir olması adına "/etc/postgresql/14/main/" dizini altında bulunan postgresql.conf dosyası uzaktan erişime açılması amacıyla 'listen_addresses="*"' olacak şekilde düzenlenir. Postgresql yeniden başlatılır.

* sudo service postgresql restart

Test amacıyla barman kullanıcıyla aşağıdaki komut kullanılır;

* psql -c 'SELECT version()' -U barman -h 127.0.0.1 postgres

![](https://github.com/mrtyildiz/Blog-Post/blob/main/Database/img/2.png?raw=true)

Postgresql sunucusu üzerindeki işlemlerden sonra barman uygulamasını kurmuş olduğumuz sunucu üzerinde "barman" kullanıcısı ve .pgpass dosyası oluşturulur. Bu amaç doğrultusunda aşağıdaki komutlar sırasıyla kullanılır.

* sudo passwd barman
* sudo -i -u barman
* echo "pgsql:5432:*:barman:password" >> ~/.pgpass

### Anahtar Tanımlama işlemi

SSH keylerinin paylaşılması ve tanıtılması amacıyla ilk öncelikle RSA key üretme işlemi yapılmaktadır;
* su barman
* ssh-keygen -t rsa

Oluşturulmuş olan anahtarın postgresql sunucusuyla paylaşılması amacıyla;
* ssh-copy-id -i /var/lib/barman/.ssh/id_rsa.pub postgres@barmanpostsql

İşlemin test edilmesi amacıyla; 
* ssh 'postgres@barmanpostsql'

![](https://github.com/mrtyildiz/Blog-Post/blob/main/Database/img/9.png?raw=true)


SSH keylerinin paylaşılması ve tanıtılması amacıyla ilk öncelikle RSA key üretme işlemi yapılmaktadır;
* su postgres
* ssh-keygen -t rsa

Oluşturulmuş olan anahtarın postgresql sunucusuyla paylaşılması amacıyla;
* ssh-copy-id -i /var/lib/postgresql/.ssh/id_rsa.pub barman@barman 
  
İşlemin test edilmesi amacıyla; 
* ssh ‘barman@barman'

![](https://github.com/mrtyildiz/Blog-Post/blob/main/Database/img/10.png?raw=true)


### Barman Yapılandırma işlemi

Barman'ın konfigürasyonu sunucu üzerinde yapılır.

/etc/barman.d dizini oluşturulur.
* mkdir -p /etc/barman.d

/etc/barman.conf dosyası içerisindeki ";configuration_files_directory = /etc/barman.d" satırındaki ";" silinir.
/etc/barman.d/ klasörü altına "pgsql.conf" dosyası oluşturulur ve içerisine aşağıdaki komutlar yazılır.
```
[pgsql]
description =  "Old PostgreSQL server"
conninfo = host=192.168.121.130 user=barman dbname=Our_Database
ssh_command = ssh postgres@192.168.121.130
retention_policy = RECOVERY WINDOW OF 2 WEEKS
```
![](https://github.com/mrtyildiz/Blog-Post/blob/main/Database/img/3.png?raw=true)

Barman uygulamasının Potgresql bağlanılabilmesi amacıyla Barman IP adresi trusted olarak eklenir.
```
host    all             all             172.17.0.2/32         trust
```
/etc/postgresql/14/main/pg_hba.conf dosyasına aşağıdaki komutlar eklenir.

```
wal_level = archive
archive_mode = on
archive_command = 'rsync -a %p barman@172.17.0.2:/var/lib/barman/pgsql/incoming/%f'
```
![](https://github.com/mrtyildiz/Blog-Post/blob/main/Database/img/4.png?raw=true)
Potgresql yeniden başlatılır;
```
sudo systemctl restart postgresql
```
Postgresql üzerindeki işlemler gerçekleştirildikten sonra barman üzerin test işlemi gerçekleştirilir.

![](https://github.com/mrtyildiz/Blog-Post/blob/main/Database/img/7.png?raw=true)
