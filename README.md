
# Dağıtık Sistemler Uygulaması

Bu proje, Docker teknolojisi kullanılarak oluşturulmuş dağıtık bir sistem mimarisidir. Projede, Nginx yük dengeleyici, iki adet replikasyonlu Spring Boot uygulama sunucusu, PostgreSQL veritabanı sunucusu ve Redis cache sunucusu yer almaktadır.


## Tanıtım videosu
Link: https://drive.google.com/file/d/1E3az6li3DxFd8jdXUb0gBtC0vCSltikz/view?usp=sharing


## Uygulamanın amacı

Bu proje, temel dağıtık sistem prensiplerini göstermek ve yük dengeleme ile yüksek erişilebilirliği sağlamak amacıyla geliştirilmiştir.

 Amaç:

- Gelen isteklerin Nginx üzerinden iki farklı Spring Boot uygulamasına paylaştırılması.

- Bir uygulama kapanırsa diğerinin devreye girerek sistemi çalışır halde tutması (failover).
- Redis ile cache yönetimi ve PostgreSQL ile veri kalıcılığı sağlamak
  
## Proje Mimarisi

```bash
  Kullanıcı İsteği
      │
      ▼
   [ Nginx ]
      │
 ┌────┴────┐
 │         │
▼          ▼
App1     App2
  │         │
 PostgreSQL │
     Redis  │

```

  
## Gereksinimler

Bu projeyi çalıştırmak için aşağıdakiler kurulu olmalıdır

`Docker Engine`

`Java`

`Docker Compose`


  
## Özellikler

- Nginx:

    Yük dengeleyici olarak çalışır ve gelen istekleri Spring Boot uygulamalarına yönlendirir.
    Failover yapılandırması sayesinde, bir uygulama sunucusu devre dışı kaldığında diğeri devreye girer.
- Spring Boot Uygulamaları:

    İki adet replikasyonlu uygulama sunucusu bulunur (app1, app2).
    PostgreSQL veritabanı ve Redis cache ile entegre çalışır.
    Hangi uygulamanın cevap verdiğini test etmek için basit bir /api/hello endpoint'i vardır.
- PostgreSQL:

    Veritabanı olarak kullanılır.
    pg_data adlı Docker volume ile verilerin kalıcılığı sağlanır.

- Redis:

    Cache mekanizması sağlayarak uygulamanın performansını artırır.    

  
## Proje Dosya Dizini


```bash
  DOCKER PROJE/
├── app/
│   └── src/
│       └── main/
│           ├── java/
│           │   └── com/
│           │       └── example/
│           │           └── demo/
│           │               └── DemoApplication.java
│           └── resources/
│               └── application.properties
├── Dockerfile
├── pom.xml
├── nginx/
│   └── nginx.conf
└── docker-compose.yml

```

## Bilgisayarınızda Çalıştırın

Projeyi klonlayın

```bash
  git clone <repository_url>  
  cd <repository_klasörü>  

```

Docker container'larını oluşturun ve başlatın:

```bash
  docker-compose up --build -d  

```

Uygulamayı kontrol edin:

```bash
  http://localhost/api/hello 
```

Container’ları durdurmak için:

```bash
  docker-compose down  

```

  
## Lisans

[MIT](https://choosealicense.com/licenses/mit/)

  
## Geliştirici

- [@alperenataner](https://www.github.com/alperenataner)

  
## Feedback

Herhangi bir geri bildiriminiz varsa, lütfen alperenataner10@hotmail.com adresinden bana ulaşabilirsiniz.

  
