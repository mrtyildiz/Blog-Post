# Terrafrom ie AWS Storage İşlemi

Selamlar! Terraform üzerine yazmaya başladığım bu yazı dizisinde, Storage işleminin nasıl gerçekleşebileceğini ele alan bir blog yazısıdır. Bir önceki [Buradan](https://medium.com/@muratasnb/terrafrom-infrastructure-as-code-iac-kavram%C4%B1-a9e60b0bd7f8) yazıma buradan ulaşabilirsiniz.


![Terrafrom](./img/1.png)

İlk öncelikle AWS cloud üzerinden verilen Storage hizmetinin mantığı aşağıdaki gibidir;

## AWS Storage Hizmetleri: Amazon S3, EBS ve EFS

AWS Cloud 'da Storage hizmetleri için kullanım senaryolarına göre üç ana hizmete ayrılır;

* **Amazon S3 (Simple Storage Service)**
* **EBS (Elastic Block Store)**
* **EFS (Elastic File System)**

Bu storage hizmetlerinin Terrafrom ile nasıl oluşturulacağı ele alınmıştır.

### **1. Amazon S3 (Simple Storage Service)**

AWS S3, **objektif depolama** hizmetidir. Yani verilerinizi **Bucket** olarak adlandırılan depolama alanlarına yüklenmektedir.
AWS S3, HA (yüksek erişilebilirlik), esneklik ve düşük maliyet sunmaktadır. Genelikle;
* Yedekleme
* Statik web sitenin barındırılması
* Big Date analizi
* Log depolama 

gibi amaçlarla kullanılır. Örnek olarak, Terraform ile bir S3 Bucket oluşturmak için aşağıdaki konfigürasyon kullanılabilir.

```hcl
provider "aws" {
  region = "us-east-1"
}

resource "aws_s3_bucket" "example" {
  bucket = "my-unique-bucket-name"
  acl    = "private"

  tags = {
    Name        = "MyBucket"
    Environment = "Dev"
  }
}
```
Bu Terraform kodu, **AWS üzerinde özel erişimli bir S3 Bucket oluşturur.**

* **Provider Tanımı:** AWS'yi Terraform için yapılandırır (```us-east-1``` bölgesinde).
* **S3 Bucket Kaynağı:** ```my-unique-bucket-name``` adıyla bir S3 Bucket oluşturur.
* **ACL (Access Control List):** ```private``` olarak ayarlanarak, yalnızca sahibi erişebilir.
* **Tags:** Bucket’a ```"Name" = "MyBucket"``` ve ```"Environment" = "Dev"``` etiketleri eklenir.

**Özet: Terraform ile AWS üzerinde özel (```private```) erişimli bir S3 Bucket oluşturur ve etiketler ekler.**

---

### **2. Amazon EBS (Elastic Block Store)**

AWS EBS, **block tabanlı** bir depolama çözümüdür ve genellikle **EC2 sanal makinelerine disk (HDD veya SSD) olarak eklenebilmektedir.** Yani, bir sunucuya takılmış bir fiziksel disk gibi çalışır. AWS EBS, işletim sistemi ve veritabanları gibi **yüksek performans gerektiren** işlemler için kullanılmaktadır. Örnek Terraform konfigürasyon kodu aşağıdaki gibidir;

```hcl
provider "aws" {
  region = "us-east-1"
}

resource "aws_ebs_volume" "ebs_example" {
  availability_zone = "us-east-1a"
  size             = 10  # 10 GB disk
  type             = "gp3"  # SSD disk

  tags = {
    Name = "MyEBSVolume"
  }
}

resource "aws_instance" "ec2_example" {
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = "t2.micro"

  tags = {
    Name = "MyEC2Instance"
  }
}

resource "aws_volume_attachment" "ebs_attachment" {
  device_name = "/dev/sdh"
  volume_id   = aws_ebs_volume.ebs_example.id
  instance_id = aws_instance.ec2_example.id
}
```
Bu Terraform kodu, **AWS'de bir EC2 instance oluşturup, ona 10 GB'lık bir EBS diski bağlar.**

* **EBS Volume:** ```gp3``` tipi 10 GB disk oluşturur.
* **EC2 Instance:** ```t2.micro``` tipi bir sanal sunucu oluşturur.
* **Disk Bağlantısı:** EBS diskini EC2'ye ```/dev/sdh``` olarak bağlar.

---

## **3. Amazon EFS (Elastic File System)**

AWS EFS, **paylaşımlı dosya sistemi** olarak tanımlanmaktadır. Bu yöntemle birden fazla EC' sunucusunun aynı anda okuma/yazma yapmasına imkan sunmaktadır. Bu yöntem **NFS (Network File System) protokolüyle çalışır** ve HA (High Availability- yüksek erişilebilirlik) gerektiren senaryolar için uygulanmaktadır. Konu özelinde kod örneği aşağıdaki gibidir;

```hcl
provider "aws" {
  region = "us-east-1"
}

resource "aws_efs_file_system" "efs_example" {
  creation_token = "my-efs"
  performance_mode = "generalPurpose"
  
  tags = {
    Name = "MyEFS"
  }
}

resource "aws_efs_mount_target" "efs_mount" {
  file_system_id  = aws_efs_file_system.efs_example.id
  subnet_id       = "subnet-0c4a7f6a"
}
```


Bu Terraform kodu, **AWS'de bir EFS (Elastic File System) oluşturup bir alt ağa bağlar.**

* **EFS Dosya Sistemi:** ```"my-efs"``` adıyla oluşturulur.
* **Performans Modu:** ```generalPurpose``` olarak ayarlanır.
* **Mount Target:** EFS, ```"subnet-0c4a7f6a"``` alt ağına bağlanır.

* **Özet:** AWS'de **paylaşımlı bir dosya sistemi (EFS) oluşturur ve bir subnet'e bağlar.**

---

## **Terraform StateFile Management With AWS S3**

State File, Terraform ile yönetilen altyapıların mevcut durumlarının takip edildiği dosyadır. Bu dosyanın özellikleri;

* **Kaynakları Takip Eder:** Terraform, oluşturulan kaynakların ID'lerini ve yapılandırmalarını bu dosyada saklanır.
* **Durum Senkronizasyonu Sağlar:** Altyapının güncel durumunu bilir ve gereksiz değişiklikleri önler
* **Uzaktan Saklanabilir:** AWS S3, Terraform Cloud, Consul, Azure Storage gibi servislerde bulundurulabilir. Bu durum ekiplerin ortak çalışmasına imkan sağlar.
* **Locking Desteği:** DynamoDB gibi mekanizmalar ile aynı anda birden fazla Terraform çalışmasının önüne geçer.

Aşağıdaki kod örneğinde AWS S3 üzerinde State File(`terraform.tfstate`) saklanama işlemi anlatılmaktadır.
Örnek Kod;

```hcl
terraform {
  backend "s3" {
    bucket         = "my-terraform-state-bucket"
    key            = "terraform/state.tfstate"
    region         = "us-east-1"
    encrypt        = true
  }
}
``` 
Aynı anda birden fazla Terraform 'un kullanılmasını önmlemek amacıyla ***DynamoDB** kullanılır
Örneğin

```hcl
resource "aws_dynamodb_table" "terraform_locks" {
  name         = "terraform-locks"
  billing_mode = "PAY_PER_REQUEST"
  hash_key     = "LockID"

  attribute {
    name = "LockID"
    type = "S"
  }
}
```

S3 Backend yapılandırmasında `dynamodb_table` eklenerek aktif hale getirilir:

```hcl
terraform {
  backend "s3" {
    bucket         = "my-terraform-state-bucket"
    key            = "terraform/state.tfstate"
    region         = "us-east-1"
    encrypt        = true
    dynamodb_table = "terraform-locks"
  }
}
```
---

## **Hangi Depolama Çözümünü Seçmelisiniz?**

| **Özellik**   | **Amazon S3** | **Amazon EBS** | **Amazon EFS** |
|--------------|--------------|---------------|---------------|
| **Depolama Tipi** | Objeler | Blok Depolama | Paylaşımlı Dosya Sistemi |
| **EC2 ile Kullanım** | Doğrudan kullanılamaz | Bir EC2’ye bağlı çalışır | Birden fazla EC2 ile paylaşılabilir |
| **Performans** | Düşük-Orta | Yüksek | Orta |
| **Maliyet** | Düşük | Orta | Yüksek |
| **Örnek Kullanım** | Log Depolama, Yedekleme, Statik Dosyalar | Veritabanları, Uygulamalar | Web sunucularında paylaşımlı dosyalar |

---
