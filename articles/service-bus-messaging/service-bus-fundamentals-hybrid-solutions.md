---
title: Azure Service Bus temelleri aaaOverview | Microsoft Docs
description: "Bir giriş toousing Service Bus tooconnect Azure uygulamalarını tooother yazılım."
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 12654cdd-82ab-4b95-b56f-08a5a8bbc6f9
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/15/2017
ms.author: sethm
ms.openlocfilehash: 1abd5cf310ef06ba35e1e2489a7c0a07e1797736
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-bus"></a>Azure Service Bus

Bir uygulama veya hizmet hello bulutta veya şirket içi çalışır olup olmadığını genellikle diğer uygulamalar veya hizmetler ile toointeract gerekir. tooprovide kapsamlı ve kullanışlı şekilde toodo Bu, Microsoft Azure teklifleri hizmet veri yolu. Bu makalede nedir ve neden toouse isteyebileceğinizi verilerek bu teknoloji görünüyor.

## <a name="service-bus-fundamentals"></a>Service Bus ile ilgili temel bilgiler

Farklı çözümler, farklı iletişim stilleri gerektirir. Bazı durumlarda, basit bir kuyruk aracılığıyla ileti gönderme ve alma uygulamaları izin vererek hello en iyi çözümdür. Diğer durumlarda ise sıradan bir kuyruk yeterli değildir; yayımla ve abone ol mekanizmasını içeren bir kuyruk daha faydalıdır. Bazı durumlarda uygulamalar arasında bağlantı olması yeterlidir ve kuyruklara gerek yoktur. Hizmet veri yolu uygulamaları toointeract birkaç farklı şekilde etkinleştirilmesi her üç seçenek sağlar.

Hizmet veri yolu birden çok kullanıcı tarafından paylaşılan hello hizmeti anlamına gelir çok kiracılı bulut hizmetidir. Bir uygulama geliştiricisi gibi her bir kullanıcı oluşturur bir *ad alanı*, ad alanında gerekli hello iletişim mekanizmasını tanımlar. Şekil 1'de bu mimarinin nasıl göründüğü gösterilmiştir.

![][1]

**Şekil 1: Service Bus hello bulut üzerinden uygulamaları bağlamak için çok kiracılı bir hizmet sunar.**

Ad alanı içinde, üç farklı iletişim mekanizmasının bir veya birden fazla örneğini kullanabilirsiniz. Bu mekanizmaların her biri, uygulamaları farklı yöntemlerle bağlar. Merhaba Seçenekler şunlardır:

* Tek yönlü iletişime izin veren *kuyruklar*. Her kuyruk, alınana kadar gönderilen iletileri depolayan bir ara hizmet olarak görev yapar (bazen *aracı* olarak adlandırılır). Her ileti tek bir alıcı tarafından alınır.
* *Abonelikler* olmak üzere tek konu başlığı kullanan, tek yönlü iletişim sağlayan *Konu Başlıkları*, birden çok aboneliği barındırabilir. Kuyrukta olduğu gibi konu başlığı aracı gibi davranır ancak her abonelik isteğe bağlı olarak belirli bir ölçüte uyan bir filtre tooreceive yalnızca iletileri kullanabilirsiniz.
* Çift yönlü iletişim sunan *geçişler*. Kuyruk ve konu başlıklarının aksine, bir geçiş yürütülen iletileri depolamaz; yani bir aracı değildir. Bunun yerine, bunu yalnızca bunları toohello hedef uygulamaya geçirir.

Bir kuyruk, konu veya geçiş oluşturduğunuzda bunları adlandırırsınız. Ne olursa olsun, ad alanınız birlikte, bu ad hello nesne için benzersiz bir tanımlayıcı oluşturur. Uygulamalar bu adı tooService veri yolu sağlayan sonra bu kuyruk, konu veya geçiş toocommunicate birbiriyle kullanın. 

Bu nesnelerin hello geçiş senaryosunda toouse, Windows uygulamaları Windows Communication Foundation (WCF) kullanabilir. Bu hizmet [WCF Geçişi](../service-bus-relay/relay-what-is-it.md) olarak bilinir. Windows uygulamaları kuyruklar ve konular için Service Bus tanımlı mesajlaşma API'lerini kullanabilir. toomake Windows dışı uygulamalar bu nesneleri daha kolay toouse, Microsoft Java, Node.js ve diğer dillere yönelik SDK sunar. Kuyruklara ve konu başlıklarına HTTP(s) üzerinden [REST API'lerini](/rest/api/servicebus/) kullanarak da erişebilirsiniz. 

Kendisini olsa bile Service Bus toounderstand hello bulutta çalışan önemlidir (diğer bir deyişle, Microsoft'un Azure veri merkezlerinde), bunu kullanan uygulamalar her yerden çalıştırabilirsiniz. Azure, örneğin, veya kendi veri merkezinizde çalışan uygulamalar üzerinde çalışan Service Bus tooconnect uygulamaları kullanabilir. Ayrıca bunu tooconnect Azure veya başka bir çalışan bir uygulama kullanabilirsiniz tabletler ve telefonlardan veya bir şirket içi uygulama ile bulut platformu. Bile olası tooconnect ev aletlerini, sensörleri ve diğer aygıtlar tooa Merkezi uygulama veya tooone diğer olabilir. Service Bus, neredeyse her yerden erişilebilen hello bulutta bir iletişim mekanizmasıdır. Kullandığınız nasıl toodo hangi uygulamalarınızı gereksinimlerine göre değişir.

## <a name="queues"></a>Kuyruklar

Service Bus kuyruğu kullanarak iki uygulama tooconnect karar verdiğinizi varsayalım. Şekil 2'de bu durum gösterilir.

![][2]

**Şekil 2: Service Bus kuyrukları tek yönlü, zaman uyumsuz kuyruğa alma işlemi sunar.**

Merhaba işlem basittir: bir gönderici tooa Service Bus kuyruğuna ileti gönderir ve bir alıcı bu iletiyi daha sonraki bir zamanda seçer. Kuyruk Şekil 2'de gösterildiği gibi yalnızca tek bir alıcıya sahip olabilir. Ya da birden çok uygulama hello okuyabilir aynı sırası. Merhaba ikinci durumda, her ileti tek bir alıcı tarafından okunur. Çok noktaya yayın hizmetinde bunun yerine bir konu kullanmanız gerekir.

Her ileti iki bölümden oluşur: özellikler kümesi (her biri anahtar/değer çifti olmak üzere) ve ileti yükü. Merhaba yükü ikili, metin veya hatta XML olabilir. Bunların nasıl kullanıldığı hangi uygulamanın toodo çalışırken bağlıdır. Örneğin, yakın zamandaki bir satış hakkında bir ileti gönderen uygulama hello özellikleri içerebilir **Seller = "Ava"** ve **tutar = 10000**. Merhaba ileti gövdesi hello satışın imzalı sözleşmesinin taranmış bir görüntüsünü içerir veya hiç yoksa, boş kalır.

Bir alıcı iki farklı şekilde Service Bus kuyruğundaki iletileri okuyabilir. Merhaba olarak adlandırılan ilk seçenek  *[ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode)*hello kuyruktan iletiyi kaldırır ve anında siler. Bu basit bir seçenektir ancak hello iletiyi işlemeyi tamamlamadan hello alıcı çökerse hello ileti kaybolur. Merhaba kuyruktan kaldırılmış olduğundan başka bir alıcı, erişebilir. 

Merhaba ikinci seçeneği  *[PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode)*, bu sorunla toohelp anlamına gelir. Gibi **ReceiveAndDelete**, **PeekLock** okuma hello kuyruktan iletiyi kaldırır. Selamlama iletisine ancak silmez. Bunun yerine, onu görünmez tooother alıcıları kolaylaştırarak hello iletiyi kilitleyerek olaylardan birinin bekler:

* Merhaba alıcısı işlemler ileti başarıyla Merhaba, çağıran [Complete()](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete), ve hello sıra selamlama iletisine siler. 
* Merhaba alıcı, selamlama iletisine başarıyla işleyemediği verirse, çağıran [Abandon()](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Abandon). Merhaba sıra hello kilidi hello iletiden kaldırır ve kullanılabilir tooother alıcıları kolaylaştırır.
* Merhaba alıcı bu yöntemlerin hiçbiri yapılandırılabilir bir süre içinde (varsayılan olarak 60 saniye) çağırırsa, hello sıra hello alıcının başarısız olduğunu varsayar. Bu durumda, Hello çağrısı yaptığını sanki gibi davranır **Abandon**, ileti kullanılabilir tooother alıcıları hello yapma.

Burada gerçekleşebilecek dikkat edin: hello aynı ileti iki kez, belki de tootwo farklı alıcıya teslim edilebilir. Service Bus kuyruklarını kullanan uygulamalar bu durum için hazırlıklı olmalıdır. toomake yinelenen algılama daha kolay, her iletinin benzersiz olan [MessageID](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_MessageId) hello kalır, varsayılan olarak özelliği aynı selamlama iletisine kaç kez olsun okunur kuyruktan. 

Kuyruklar birçok durumda oldukça faydalıdır. Her ikisi de başlangıç bile çalıştırmıyor bunlar etkinleştirmek uygulamaları toocommunicate aynı zaman, bir toplu işlem ve mobil uygulamaları ile özellikle kullanışlıdır. Ayrıca, birden çok alıcısı bulunan bir kuyruk otomatik olarak yük dengelemesi sunar. Bu durum, gönderilen iletilerin tüm alıcılara dağıtılmasından kaynaklanır.

## <a name="topics"></a>Konu başlıkları

Yararlı oldukları gibi kuyruklar, her zaman hello doğru çözüm değildir. Bazı durumlarda Service Bus konu başlıkları daha faydalıdır. Şekil 3'te bu durum gösterilir.

![][3]

**Şekil 3: abone uygulamanın belirtir hello filtreye göre bazı alabilir veya tooa Service Bus konu tüm Merhaba iletileri gönderilir.**

A *konu* birçok yolu tooa sırada benzer. Göndericiler gönderme iletileri tooa hello konudaki iletileri tooa sırası göndermek ve bu iletiler görünümünü hello aynı kuyruklarla gibi aynı şekilde. Merhaba konuları her alıcı uygulama toocreate etkinleştirmenizi farktır kendi *abonelik* tanımlayarak bir *filtre*. Bir abonenin sonra bu filtreyle eşleşen Merhaba iletileri görür. Örneğin, Şekil 3'te, bir gönderici ile üç abonesi bulunan bir konu başlığı ve abonelerin her birinin kendi filtrelerine sahip olduğu bir durum gösterilir:

* Abone 1 yalnızca hello özelliğini içeren iletileri alır *Seller = "Ava"*.
* Abone 2 hello özelliğini içeren iletileri alır *Seller = "Ruby"* ve/veya içeren bir *tutar* değeri 100. 000 ' fazla olan özelliği. Belki de toosee kendi satış ve kimlerin yapar bağımsız olarak tüm büyük satışları istediği şekilde Ruby hello satış yöneticisi, ' dir.
* Abone 3 ayarladı, filtre çok*doğru*, yani tüm iletileri alır. Örneğin, bu uygulama bir denetim kaydı tutmakla olabilir ve bu nedenle tüm Merhaba iletileri toosee gerekiyor.

Kuyruklar, aboneler tooa konu kullanarak iletileri okuyabilir gibi [ReceiveAndDelete veya PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode). Kuyrukların aksine, ancak tooa konu birden fazla abonelik tarafından alınabilir tek bir ileti gönderdi. Yaygın olarak adlandırılan bu yaklaşım *Yayımla ve abone ol* (veya *pub/alt*), birden çok uygulama hello ilginizi çekiyor mu durumunda faydalıdır aynı iletileri. Merhaba doğru filtreyi tanımlayarak, her abone toosee ihtiyaç duyduğu hello ileti akışının yalnızca hello kısmını dokunun.

## <a name="relays"></a>Geçişler

Hem kuyruklar hem de konu başlıkları, bir aracı yoluyla tek yönlü zaman uyumsuz iletişim sağlar. Trafik akışları sadece tek yöndedir ve göndericiler ile alıcılar arasında doğrudan bağlantı yoktur. Peki bu bağlantıyı istemiyorsanız ne yapmanız gerekir? Uygulamalarınızı varsayalım tooboth iletileri almasına ve göndermesine, veya belki de bunları arasında doğrudan bağlantı istediğinizi ve Aracısı toostore iletileri olması gerekmez. Bu gibi tooaddress senaryoları, hizmet veri yolu sağlayan *geçişleri*, Şekil 4'te gösterildiği gibi.

![][4]

**Şekil 4: Service Bus geçişi, uygulamalar arasında zaman uyumlu, çift yönlü iletişim sağlar.**

Merhaba ilk soru tooask geçişler hakkında budur: neden kullanmalıyım? Kuyruklara ihtiyacım olsa bile, uygulamaları bir bulut hizmeti aracılığıyla değil, yalnızca etkileşim doğrudan iletişim neden hale? Merhaba yanıt Konuşmayı doğrudan düşündüğünüzden daha zor olması açısından önemlidir.

Tooconnect iki içi uygulamaları istediğinizi düşünelim her ikisi de kurumsal veri merkezlerinde çalışıyor. Bu uygulamaların her biri güvenlik duvarının arkasında bulunur ve her veri merkezi de ağ adresi çevirisi (NAT) kullanır. birkaç bağlantı noktaları ve NAT dışındaki tüm gelen verileri her bir uygulama çalıştıran bu hello makine gelir hello güvenlik duvarı blokları doğrudan dış hello veri merkezinden ulaşabilir sabit bir IP adresi yok. Bazı ek Yardım olmadan genel internet hello bu uygulamaları bağlamak sorunlu oluşturur.

Bir Service Bus geçişi yararlı olabilir. çift yönlü bir geçiş, her bir uygulama aracılığıyla toocommunicate Service Bus içeren bir giden TCP bağlantısı kurar ve ardından bağlantıyı açık tutar. Merhaba iki uygulama arasındaki tüm iletişim bu bağlantılar üzerinden geçen. Her bağlantı kurulduğundan hello Merkezinizde hello güvenlik duvarı gelen trafiği tooeach uygulama yeni bağlantı noktaları açmadan izin verir. Her uygulama hello bulut hello iletişimi genelinde tutarlı bir uç nokta içerdiğinden bu yaklaşım hello NAT sorunu da alır. Merhaba geçiş aracılığıyla veri değişimi tarafından hello uygulamaları aksi iletişimi zorlaştıracak hello sorunlarını önleyebilirsiniz. 

Hizmet veri yolu toouse geçirir, uygulamaları hello üzerinde Windows Communication Foundation (WCF) güvenir. Hizmet veri yolu için geçişler aracılığıyla Windows uygulamaları toointeract basit hale WCF bağlamalarını sunar. WCF zaten kullanan uygulamalar genellikle bu bağlamaların bir tanesini belirtin, sonra tooeach bir geçiş aracılığıyla diğer konuşun. Öte yandan kuyrukların ve konu başlıklarının aksine, olası durumlarda Windows uygulaması olmayan uygulamalarda geçişlerin kullanılması standart kitaplıklar sağlanmadığından programlama açısından biraz daha fazla çaba sarf edilmesini gerektirir.

Kuyruk ve konu başlıklarının aksine uygulamalar, geçişleri açık bir şekilde oluşturmaz. Bunun yerine, bir geçiş tooreceive iletileri isteyen bir uygulama Service Bus ile TCP bağlantısı kurduğunda otomatik olarak oluşturulur. Merhaba bağlantı kesildiğinde hello geçiş de silinir. Service Bus belirli bir dinleyici tarafından oluşturulan uygulama toofind hello geçişe tooenable uygulamaları toolocate sağlayan bir kayıt defteri ada göre belirli bir geçiş sağlar.

Uygulamalar arasında doğrudan iletişim gerektiğinde geçişler hello doğru çözümdür. Örneğin; check-in kiosk cihazları, mobil cihazlar ve diğer bilgisayarlardan erişilebilmesi gereken ve bir şirket içi veri merkezinde çalışan hava yolu rezervasyon sistemini ele alalım. Çalışıyor olurlarsa olsunlar bu tüm sistemlerde çalışan uygulamalar hello bulut toocommunicate, Service Bus geçişlerine güvenebilirler.

## <a name="summary"></a>Özet

Uygulamaları bağlamak her zaman eksiksiz çözüm oluşturmanın bir parçası, süredir ve uygulamaları ve Hizmetleri toocommunicate birbirleriyle gerektiren senaryolar hello aralığı tooincrease ayarlanmış olarak daha fazla uygulama ve cihazlar bağlı toohello Internet. Kuyruklar, konu başlıkları ve geçişler aracılığıyla iletişimi ulaşmak için bulut tabanlı teknolojiler sağlayarak, hizmet veri yolu toomake bu temel işlevin daha kolay tooimplement amaçlar ve daha geniş çapta kullanılabilir.

## <a name="next-steps"></a>Sonraki adımlar

Artık Azure Service Bus, hello temellerini öğrendiğinize göre daha fazla bu bağlantılar toolearn izleyin.

* Nasıl toouse [Service Bus kuyrukları](service-bus-dotnet-get-started-with-queues.md)
* Nasıl toouse [Service Bus konuları](service-bus-dotnet-how-to-use-topics-subscriptions.md)
* Nasıl toouse [Service Bus geçişi](../service-bus-relay/service-bus-dotnet-how-to-use-relay.md)
* [Service Bus örnekleri](service-bus-samples.md)

[1]: ./media/service-bus-fundamentals-hybrid-solutions/SvcBus_01_architecture.png
[2]: ./media/service-bus-fundamentals-hybrid-solutions/SvcBus_02_queues.png
[3]: ./media/service-bus-fundamentals-hybrid-solutions/SvcBus_03_topicsandsubscriptions.png
[4]: ./media/service-bus-fundamentals-hybrid-solutions/SvcBus_04_relay.png
