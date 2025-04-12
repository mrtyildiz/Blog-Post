# Terrafrom - Infrastructure as Code (IaC) Kavramı

Selamlar bu yazım **Terrafrom** aracından bu aracın kullanım amacından bahsetmek istiyorum. Yazılım geliştirme süreçleri hızla kendisini güncellerken, altyapı yönetiminin de bu duruma ayarak uydurması gerekmektedir. Büyük ölçekli projelerde sunucu ve ağ konfigürasyonlarını manuel olarak yönetmek sürdürülebilir bir yöntem değildir. İşte tam olarak burada **Infrastructure as Code (IaC)** kavramı karşımıza çıkmaktadır. Infrastructure as Code (IaC), altyapılarımızı manuel yönetmek yerine kod yazarak otomatik olarak yönetmemize imkan sağlayan bir yaklaşımdır. **Terrafrom**, bu yaklaşımı destekleyen en popüler araçlardan biridir.

![Terrafrom](./img/1.png)

Burada şu soru karşımıza çıkmakta Cloud hizmet sağlayıcıları (AWS, Azure veya Google Cloud vb.) manuel olarak yapılandırmak ve oluşturmak ne gibi problemlere neden olabilmektedir.

* **Zaman Kaybı:** Manuel olarak bir uygulama için alltyapıyı kurmak saatler alabilir.
* **Ölçeklenebilirlik Sorunu:** Küçük projeler için uygun olsa da, büyük ölçekli şirketlerde yüzlerce sunucu oluşturmak büyük bir iş güçü gerektirmektedir.
* **Maliyet kontrolü:** Kullanılmayan altyapıların kaldırılması otomatize edilmezse gereksiz maliyet oluşturabilmektedir.
* **Tutarsız ortamlar:** Yazılım geliştirildiği ortam ile çalışacağı ortamın birbirine uyumlu olması manuel yöntemlerle zor olmaktadır.
* **Güvenlik ve yönetim:** Manuel yapılandırmalar güvenlik açıklarına ve hatalara yol açabilir.

Yukarıda bahsedilen dezavantajların önüne geçilmesi amacıyla oluşturlan sistem de **Infrastructure as Code (IaC)** bakış açısına uygun bir yaklaşım geliştirilmelidir. Bu yaklaşımın avantajları aşağıdaki gibidir;

* **Tutarlılık:** Aynı yapılandırmayı her seferinde aynı şekilde uygulanır. Aynı kod farklı ortamlarda da çalıştırılabilmektedir.
* **Maliyet Kontrolü:** Kaynak kullanımı takip edilebilir ve gereksiz kullanımın önüne gecilebilemektedir.
* **Zaman Tasarrufu:** Altyapı dakikalr içinde tamamlanır ve çalışır duruma getirilebilir.
* **İnsan kaynaklı hataların önüne geçilmesi:** Manuel işlemlerde olabilecek olası insan hatalarının önüne geçilebilir.
* **Versiyon Kontrolü:** Altyapı değişiklikleri git gibi sistemlerle takip edilebilmektedir.
* **Geliştiriclere Odaklanma Fırsatı:** Altyapı yönetimine harcanan süre önemli ölçüde azalırken, uygulama geliştirmeye daha fazla zaman ayrılabilir.

## Terraform Nedir?

Terraform, HashiCorp tarafından geliştirilen ve altyapıyı kod olarak yönetmeyi sağlayan açık kaynaklı bir **Infrastructure as Code (IaC)** aracıdır. Terraform’un sunduğu avantajlar şunlardır:

- Farklı cloud sağlayıcılarını destekler (AWS, Azure, Google Cloud vb.).
- İstenilen altyapıyı tanımlamak için **Terraform Configuration Language (HCL)** kullanır.
- Altyapıyı oluşturmak, yönetmek ve silmek için kolay komutlar sunar.
- İzin verilen değişiklikleri planlayarak yönetim kolaylığı sağlar.

## Terraform Nasıl Çalışır?

Terraform kullanarak altyapı yönetimini şu adımlarla gerçekleştirilebilir:

1. **Terraform dosyalarını yazın** → Altyapı HCL kullanarak tanımlanır.
2. **Terraform komutlarını çalıştırın** → Kodları doğrulanır ve plan oluşturulur.
3. **Cloud sağlayıcınızın API’sine çağrı yaparak kaynakları oluşturun** → Terraform, ilgili sağlayıcıya istek göndererek altyapıyı oluşturur.

### Terraform İş Akışı:

1. **`terraform init`** → Terraform modüllerini ve sağlayıcıları hazırlar.
2. **`terraform validate`** → Kodlarınızı doğrular.
3. **`terraform plan`** → Uygulanacak değişiklikleri görüntüler.
4. **`terraform apply`** → Altyapıyı oluşturur veya günceller.
5. **`terraform destroy`** → Altyapıyı kaldırır.


## Terrafrom kurulum işlemleri 

### **Windows Üzerine Terraform Kurulumu**

#### **Adım 1: Terraform'u İndirin**

Terraform’un en son sürümünü HashiCorp’un resmi web sitesinden indirin:

🔗 [Terraform İndirme Sayfası](https://developer.hashicorp.com/terraform/install)

İşletim sisteminize uygun **Windows (64-bit)** paketini indirin.

#### **Adım 2: Dosyaları Çıkartın ve Yol Tanımlayın**

1. İndirilen **.zip** dosyasını uygun bir klasöre çıkartın (Örneğin: `C:\terraform`)
2. `terraform.exe` dosyasının yolunu sisteme tanıtın:
   
   **Komut İstemcisine (CMD) veya PowerShell'e girin ve aşağıdaki komutu çalıştırın:**

   ```powershell
   [System.Environment]::SetEnvironmentVariable("Path", $Env:Path + ";C:\terraform", [System.EnvironmentVariableTarget]::Machine)
   ```

3. Terminali kapatıp yeniden açın ve kurulumu doğrulamak için aşağıdaki komutu çalıştırın:

   ```powershell
   terraform -version
   ```

   **Başarıyla kurulduysa, Terraform’un sürümü görüntülenecektir.** 🎉

---

### **macOS Üzerine Terraform Kurulumu**

#### **Adım 1: Homebrew ile Terraform’u Kurun**

Mac kullanıyorsanız, en kolay yöntem **Homebrew** ile kurulum yapmaktır:

```bash
brew tap hashicorp/tap
brew install hashicorp/tap/terraform
```

#### **Adım 2: Kurulumu Doğrulayın**

Kurulumu doğrulamak için aşağıdaki komutu çalıştırın:

```bash
terraform -version
```

#### **Hata: "No developer tools installed"**

Eğer aşağıdaki hatayı alırsanız:

```bash
Error: No developer tools installed.
```

Çözüm olarak Xcode geliştirici araçlarını yükleyin:

```bash
xcode-select --install
```

Kurulum tamamlandıktan sonra terminali yeniden başlatın ve Terraform’u tekrar doğrulayın.

---

### **Linux Üzerine Terraform Kurulumu**

#### **Adım 1: Terraform’u İndirin ve Çalıştırılabilir Yapın**

Linux için Terraform’u indirip yüklemek için şu adımları takip edin:

```bash
wget https://releases.hashicorp.com/terraform/1.5.5/terraform_1.5.5_linux_amd64.zip
unzip terraform_1.5.5_linux_amd64.zip
sudo mv terraform /usr/local/bin/
```

#### **Adım 2: Kurulumu Doğrulayın**

```bash
terraform -version
```

Eğer Terraform’un sürümü görüntüleniyorsa kurulum tamamlanmıştır. 🎉

---

## 3. Terraform Autocomplete ve Alias Ayarları

Terraform komutlarını daha hızlı yazmak için şu ek ayarları yapabilirsiniz:

**macOS/Linux İçin:**

```bash
echo 'complete -C /usr/local/bin/terraform terraform' >> ~/.bashrc
source ~/.bashrc
```

Alias tanımlamak için:

```bash
echo 'alias tf=terraform' >> ~/.bashrc
source ~/.bashrc
```

**Windows İçin:** (PowerShell Kullanarak)

```powershell
Set-Alias -Name tf -Value terraform
```

Bu ayarlarla **`tf plan`** gibi kısa komutlarla Terraform’u kullanabilirsiniz.

---

## 4. Terraform’un Çalıştığını Test Etme

Başarılı bir kurulumdan sonra, Terraform’u test etmek için aşağıdaki komutları kullanabilirsiniz:

```bash
terraform init
terraform validate
terraform plan
```

Bu komutlar herhangi bir hata vermiyorsa, Terraform başarılı bir şekilde kuruldu demektir. 🎉

Artık Terraform'u kullanmaya hazırdır! 🚀

## Terrafrom Provider Kavramı

Terrafrom provider ile belirli cloud sistmelerlerinin yönetilmesi ve kurulması mümkündür. Biz bu yazı dizisinde AWS cloud servisler de bu işlemlerin nasıl gerçekleştirlebileceği anlatılacaktır.

### 1.AWS Provider 'ın Kurulumu 

Terraform 'un AWS Provider'ını kullanabilmek için öncelikle "aws" bloğunu konfigürasyon dosyamıza eklememiz gerekmektedir. Örnek Provider tanımı;

```hcl
terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 5.0"
    }
  }
}

provider "aws" {
  region = "us-east-1" # AWS Bölgesi
}
```
Verilen örnekteki parametrelerin açıklaması aşağıdaki gibidir;

* ```source = "hashicorp/aws"``` ile HashCorp tarafından sağlanan version kullanılır.
* ```version = "~> 5.0"``` 5.x sürümlerinden en güncel olanı kullanılır.
* ```region = "us-east-1"``` AWS kaynaklarının oluşturulacağı bölgeyi belirler.

### 2.AWS Kimlik Doğrulama (Authentication)

Terraform’un AWS ile çalışabilmesi için kimlik bilgilerine ihtiyacı vardır. Kimlik bilgilerini aşağıdaki yöntemler ile yapılabilmektedir.

### a. AWS CLI Profili Kullanımı

AWS kimlik bilgilerini AWS CLI profilleri ile yönetilebilmektedir. Örneğin;

```hcl
provider "aws" {
  region  = "us-east-1"
  profile = "default"
}
```
Eğer henüz bir AWS profili oluşturulması için aşağıdaki komut ile oluşturulabilmektedir:

```sh
aws configure
```
Kimlik bilgilerini girdikten sonra ```~/.aws/credentials``` dosyasında saklanmaktadır.

### b. Değişken Kullanımı

AWS Erişim bilgilerini değişken kullanarak saklanması mümkündür. Aşağıdaki değişkenleri kullanarak erişim işlemini sağlayabilirsiniz.

```sh
export AWS_ACCESS_KEY_ID="your-access-key-id"
export AWS_SECRET_ACCESS_KEY="your-secret-access-key"
export AWS_REGION="us-east-1"
```
Bu yöntem genellikle CI/CD süreçlerinde kullanılır.

### C. IAM Rolü Kullanımı

IAM Rolü (Identity and Access Management Role), AWS'de bir varlığın (kullanıcı, hizmet, uygulama vb.) belirli izinlerle kaynaklara erişmesini sağlamak için kullanılan bir kimlik yönetimidir. IAM rolleri, doğrudan kullanıcı adı veya parola gerektirmez; bunun yerine, geçici kimlik bilgileri sağlayarak AWS hizmetleri arasında güvenli bir şekilde yetkilendirme yapılmasını mümkün kılar.

Bu yöntem eğer Terrafrom AWS EC2 veya AWS Lambda çalışıyorsa kullanılabilmektedir. Bunun için;

```hcl
provider "aws" {
  region = "us-east-1"
}
```
Terraform, IAM rolünü otomatik olarak keşfedecektir.


## 3. AWS Kaynaklarını Yönetme

AWS üzerinde bulunan ve kullanılabilecek kaynaklar aşağıdaki gibidir;

### a. EC2 Instance Oluşturma

AWS EC2 (Elastic Compute Cloud), Amazon Web Services'in sunduğu ölçeklenebilir, isteğe bağlı sanal sunucu hizmetidir. EC2, kullanıcıların fiziksel bir sunucu satın almadan AWS bulut ortamında sanal makineler (VM'ler) çalıştırmasını sağlar.

```hcl
resource "aws_instance" "example" {
  ami           = "ami-0c55b159cbfafe1f0" # Amazon Linux 2 AMI
  instance_type = "t2.micro"

  tags = {
    Name = "Terraform-Instance"
  }
}
```
* ```ami```: Kullanılacak olan Amazon Machine Image (AMI) ID'si.
* ```instance_type```: Makinenin tipi (CPU, RAM gibi özellikleri belirler).
* ```tag```: Kaynağa etiket eklemek için kullanılır.

### b. S3 Bucket Oluşturma

AWS S3 (Simple Storage Service), Amazon’un ölçeklenebilir, dayanıklı ve güvenli bir bulut depolama hizmetidir. S3 Bucket, bu hizmetin içinde dosyaların saklandığı mantıksal bir kapsayıcıdır.

```hcl
resource "aws_s3_bucket" "example" {
  bucket = "my-terraform-bucket"
  acl    = "private"
}
```
* ````bucket```: S3 bucket adı.
* ```acl```: Erişim kontrol listesi (private, public-read gibi)

### c. VPC (Virtual Private Cloud) Oluşturma

AWS VPC (Virtual Private Cloud), AWS bulutunda kendi izole edilmiş sanal ağı oluşturmanıza olanak tanıyan bir hizmettir. VPC sayesinde, AWS kaynaklarınızı (EC2, RDS, Lambda vb.) özelleştirilmiş bir ağ ortamında güvenli bir şekilde çalıştırabilirsiniz.

```hcl
resource "aws_vpc" "example" {
  cidr_block = "10.0.0.0/16"

  tags = {
    Name = "MyVPC"
  }
}
```
* ```cidr_block```: VPC’nin IP aralığını belirler.

## 4. Terraform State Yönetimi

Terrafrom, AWS 'de oluşturulan kaynakları bir state dosyasında (```terrafrom.tfstate```) saklar. Eğer ekibinizle çalışıyorsanız ve ortak bir yönetim yapmak istiyorsanız, Terraform Remote State özelliğini kullanabilirsiniz.

**AWS S3 ile Remote State Yönetimi**

```hcl
terraform {
  backend "s3" {
    bucket         = "my-terraform-state-bucket"
    key            = "terraform.tfstate"
    region         = "us-east-1"
    encrypt        = true
    dynamodb_table = "terraform-lock"
  }
}
```
Bu yapılandırmada;

* ```bucket```: State dosyasını saklamak için kullanılan S3 bucket
* ```dynamodb_table```: Aynı anda birden fazla kişinin terrafrom apply çalıştırmasını önlemek için DynamoDB kilitleme mekanizmasını kullanır.


Şimdilik bu kadar gelecek blog yazılarımda Terrafrom 'u anlatmaya devam edeceğim. 
Esenlikler.
