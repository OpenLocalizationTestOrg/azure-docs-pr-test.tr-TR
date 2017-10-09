## <a name="what-are-service-bus-queues"></a>Service Bus kuyrukları nelerdir?
Service Bus kuyrukları **aracılı mesajlaşma** iletişim modelini destekler. Kuyruklar kullanıldığında, dağıtılmış uygulamanın bileşenleri birbirleriyle doğrudan iletişim kurmazlar; bunun yerine bir aracı gibi davranan bir kuyruk aracılığıyla iletileri değiş tokuş eder (aracı). İleti üreticisi (gönderen) devre dışı bir ileti toohello sırası aktarır ve işleme devam eder. Zaman uyumsuz olarak bir ileti tüketicisi (alıcı) selamlama iletisine hello sırasından çeker ve işler. Merhaba üretici değil toowait hello tüketici yanıt sırası toocontinue tooprocess sahip ve daha fazla ileti göndermesi yapar. Kuyruklar teklif **ilk, ilk çıkar (FIFO)** teslim tooone veya birden çok rakip tüketiciye ileti. Diğer bir deyişle, iletiler genellikle alınan ve hangi toohello sıraya eklendi ve her ileti alındı ve tek bir ileti tüketicisi tarafından alınıp hello düzende hello alıcılar tarafından işlenir.

![QueueConcepts](./media/howto-service-bus-queues/sb-queues-08.png)

Service Bus kuyrukları çok sayıda çeşitli senaryolar için kullanılabilen genel amaçlı bir teknolojidir:

* Çok katmanlı bir Azure uygulamasında web ve çalışan rolleri arasındaki iletişim.
* Karma bir çözümde şirket içi uygulamalar ve Azure barındırmalı uygulamalar arasındaki iletişim.
* Farklı kuruluşlarda veya bir kuruluşun farklı departmanlarında şirket içi çalışan dağıtılmış bir uygulamanın bileşenleri arasındaki iletişim.

Kuyrukları kullanma, tooscale uygulamalarınızı daha kolay sağlar ve daha fazla esneklik tooyour mimarisi etkinleştirin.


