# Distributed-Systems-App
Proje Özeti: Dağıtık Sistemler ile Yük Dengeleme ve Failover
Bu projede, Docker teknolojisini kullanarak bir dağıtık sistem mimarisi oluşturduk. Proje, yük dengeleme, yüksek erişilebilirlik ve failover işlevlerini gerçekleştiren bir yapı kurmaya odaklandı. Aşağıda, projemizin genel yapısını ve her bir bileşenin ne işe yaradığını açıklıyorum.

1. Mimari Tasarımı
Nginx: Yük dengelemesi yapmak için kullanıldı. Nginx, gelen HTTP isteklerini iki farklı Spring Boot uygulama sunucusuna (app1 ve app2) yönlendirir.
Spring Boot Uygulamaları: İki adet Spring Boot uygulaması (app1 ve app2) kuruldu ve her biri aynı işlevi yerine getiren RESTful API’leri sağlıyor. Bu uygulamalar replikasyon mantığıyla çalışarak yüksek erişilebilirlik sağladı.
PostgreSQL Veritabanı: Uygulamalar, verilerini bu veritabanında saklar.
Redis Cache: Spring Boot uygulamaları, veri işleme hızlarını artırmak amacıyla Redis ile önbellekleme yaptı.
2. Docker ve Docker Compose Kullanımı
Dockerfile: Spring Boot uygulamasının doğru şekilde çalışabilmesi için bir Dockerfile yazıldı. Maven, Docker imajı içerisinde çalışarak uygulamanın derlenmesini sağladı.
Docker Compose: Tüm servisleri bir arada çalıştırmak ve birbirleriyle iletişim kurmalarını sağlamak için Docker Compose kullanıldı. Bu sayede, Nginx, Spring Boot uygulamaları, PostgreSQL ve Redis konteyner'ları birbirleriyle düzgün şekilde iletişim kurabiliyor.
3. Yük Dengeleme ve Failover Yapısı
Yük Dengeleme: Nginx, gelen istekleri round-robin şeklinde Spring Boot uygulamaları arasında yönlendiriyor. Yani, her yeni istek farklı bir uygulama sunucusuna gider. Böylece uygulamalar arasında yük dengelemesi sağlanır.
Failover: Eğer bir uygulama sunucusu (örneğin, app1) devre dışı kalırsa, Nginx otomatik olarak diğer sunucuya (app2) yönlendirir. Bu şekilde yüksek erişilebilirlik sağlanmış olur.
4. Test ve Sonuçlar
Proje çalıştırıldığında, Nginx başarılı bir şekilde istekleri Spring Boot uygulamalarına yönlendiriyor.
Failover Testi: Bir uygulama sunucusu (app1) kapatıldığında, Nginx diğer sunucuya (app2) yönlendirme yaparak sistemin kesintisiz çalışmasını sağladı.
Uygulama, Spring Boot üzerinden /api/hello endpoint'ini sağladı ve her iki Spring Boot uygulamasından gelen yanıtlar farklı host isimleri ile kullanıcıya iletildi.
5. Kullanılan Teknolojiler
Docker: Konteyner teknolojisi ile her servisi izole şekilde çalıştırdık.
Nginx: Yük dengelemesi ve yönlendirme işlemleri için kullanıldı.
Spring Boot: Backend API geliştirmek için kullanıldı.
PostgreSQL: Veritabanı işlemleri için kullanıldı.
Redis: Performans artırma amacıyla veri önbellekleme sağlandı.
Bu proje ile dağıtık sistemlerin temel bileşenleri olan yük dengeleme, yüksek erişilebilirlik ve failover gibi önemli konuları pratik bir şekilde uygulamış olduk. Docker kullanarak tüm servisleri tek bir komutla çalıştırıp yönetebilmek büyük bir kolaylık sağladı. Ayrıca, Spring Boot ve Nginx arasındaki etkileşimi daha verimli hale getirerek gerçek dünyada karşılaşılabilecek sorunlara karşı sağlam bir altyapı oluşturduk.
