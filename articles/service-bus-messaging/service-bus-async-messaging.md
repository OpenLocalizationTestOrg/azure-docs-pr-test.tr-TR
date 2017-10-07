---
title: "aaaService Bus zaman uyumsuz Mesajlaşma | Microsoft Docs"
description: "Azure Service Bus zaman uyumsuz Mesajlaşma açıklaması."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: f1435549-e1f2-40cb-a280-64ea07b39fc7
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/19/2017
ms.author: sethm
ms.openlocfilehash: 5ab6ddf052155a9dd975b413cfaf393119c1999d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="asynchronous-messaging-patterns-and-high-availability"></a>Zaman uyumsuz mesajlaşma modelleri ve yüksek kullanılabilirlik

Zaman uyumsuz Mesajlaşma çeşitli farklı şekillerde uygulanabilir. Kuyruklar, konular ve abonelikler ile Azure Service Bus deposu ve iletme mekanizması aracılığıyla asynchronism destekler. Normal (zaman uyumlu) işleminde, iletileri tooqueues ve konuları gönderebilir ve kuyrukları ve aboneliklerinden iletiler alabilirsiniz. Yazdığınız uygulamalar her zaman kullanılabilir olan varlıkları bağlıdır. Merhaba varlık durumu değiştiğinde tooa çeşitli koşullar, yolu tooprovide çoğu gereksinimlerini karşılayabilen bir azaltılmış yetenek varlık gerekir.

Uygulamalar genellikle zaman uyumsuz Mesajlaşma desenleri tooenable çeşitli iletişim senaryoları kullanın. Hatta hello hizmeti çalışmadığı zaman, istemciler iletileri tooservices gönderebilir uygulamalar oluşturabilir. WINS'e iletişimin deneyimi uygulamalar için bir sıra yer toobuffer iletişim sağlayarak yük düzeyi hello yardımcı olabilir. Son olarak, birden fazla makine arasında basit ancak etkili bir yük dengeleyici toodistribute iletileri alabilirsiniz.

Sipariş toomaintain kullanılabilirliğini bu varlıkları içinde birkaç farklı yolla bu varlıklar için sağlam bir ileti sistemi kullanılamaz görünebilir göz önünde bulundurun. Genel olarak bakıldığında, biz farklı şekillerde aşağıdaki hello yazma kullanılamaz tooapplications hale hello varlık bakın:

* %S toosend iletileri.
* %S tooreceive iletileri.
* %S toomanage varlıkları (oluşturma, alma, güncelleştirme veya varlıklarını silme).
* %S toocontact hello hizmeti.

Bu başarısızlıkların her biri için farklı bir hata modları azaltılmış yeteneğinin düzeyinde bir uygulama toocontinue tooperform iş sağlayan mevcut. Örneğin, ileti gönderme ancak bunları almamayı bir sistem siparişleri müşterilerden hala alabilir ancak bu siparişleri işleyemiyor. Bu konu, oluşabilecek olası sorunları ele alır ve bu sorunların nasıl azalır. Service Bus içine opt Azaltıcı Etkenler sayısı sunulan ve bu konuda Ayrıca bu katılımı Azaltıcı hello yöneten kuralları kullan hello anlatılmaktadır.

## <a name="reliability-in-service-bus"></a>Service Bus içinde güvenilirliği
Toohandle iletisi ve varlık sorunları birkaç yolu vardır ve bu Azaltıcı Etkenler hello uygun kullanımını yöneten yönergeler vardır. toounderstand hello yönergeleri, hizmet veri yolundaki yük devredebilir önce anlamanız gerekir. Azure sistemlerinin toohello tasarım nedeniyle bu sorunların tümü toobe kısa süreli eğilimindedir. Yüksek bir düzeyde kullanılamazlık farklı nedenleri hello şu şekilde görünür:

* Hizmet veri yolu bağımlı olduğu bir dış sistemden azaltma. Depolama ve işlem kaynakları ile etkileşim gelen azaltma oluşur.
* Hizmet veri yolu bağımlı olduğu bir sistem sorunu. Örneğin, belirli bir depolama parçası sorunlarla.
* Tek alt sisteminde hata hizmet veri yolu. Bu durumda, bir işlem düğümünde tutarsız bir duruma alabilir ve kendisini yeniden başlatmanız gerekir; tüm varlıklar neden tooload Bakiye tooother düğümleri görev yapar. Bu sırayla yavaş ileti işleme kısa bir süre neden olabilir.
* Azure veri merkezi içinde hatası hizmet veri yolu. "Hello sistem birçok dakika ya da birkaç saat için ulaşılamaz olduğu yıkıcı bir hatadan" budur.

> [!NOTE]
> Merhaba terim **depolama** Azure Storage ve SQL Azure anlamına gelebilir.
> 
> 

Service Bus bu sorunlar için Azaltıcı Etkenler sayısını içerir. Aşağıdaki bölümlerde hello her sorun ve bunların ilgili Azaltıcı Etkenler tartışın.

### <a name="throttling"></a>Azaltma
Service Bus ile azaltma işbirlikçi ileti oranı yönetimi sağlar. Tek tek her Service Bus düğüm birçok varlık barındırır. Bu varlıkların her CPU, bellek, depolama ve diğer yönleri açısından hello sistemde taleplerini yapar. Bu modellerle hiçbirini algıladığında, kullanım tanımlı eşiklerini aşan, hizmet veri yolu, belirtilen bir isteğin reddedebilirsiniz. Merhaba arayan alan bir [ServerBusyException] [ ServerBusyException] ve 10 saniye sonra yeniden deneme sayısı.

Azaltma, hello kodu okuma hello hatası ve en az 10 saniye boyunca tüm yeniden denemeler hello iletisinin durdurmak gerekir. Merhaba müşteri uygulaması parça Hello hata oluşabilir olduğundan, her parça hello yeniden deneme mantığını bağımsız olarak yürüten beklenir. Merhaba kod bir kuyruk veya konu bölümleme etkinleştirerek karşılaşıldığı hello olasılığını azaltır.

### <a name="issue-for-an-azure-dependency"></a>Bir Azure bağımlılığı sorunu
Azure'daki diğer bileşenleri bazen hizmet sorunları olabilir. Örneğin, Service Bus kullanan bir sistemi yükseltme, sistemin geçici olarak azaltılmış yetenekleri yaşayabilirsiniz. Bu tür sorunlar, düzenli olarak Service Bus geçici toowork araştırır ve bunları azaltmanın yollarını uygular. Bu Azaltıcı Etkenler yan etkileri görünür. Örneğin, depolama ile toohandle geçici sorunlar, hizmet veri yolu ileti gönderme işlemleri toowork tutarlı bir şekilde sağlayan bir sistemi uygular. Gönderilen iletiyi hello azaltma toohello yapısı, etkilenen hello sıra veya abonelik too15 dakika tooappear kaplayan ve alma işlemi için hazır. Genel olarak bakıldığında, bu sorun çoğu varlık karşılaşmazsınız. Ancak, Azure içinde Service Bus içinde hello varlıkların sayısı verildiğinde, bu azaltma bazen Service Bus müşteriler küçük bir kısmı için gereklidir.

### <a name="service-bus-failure-on-a-single-subsystem"></a>Tek bir alt sistemi bağlı hizmet veri yolu hatası
Herhangi bir uygulama ile durumlarda Service Bus toobecome tutarsız iç bir bileşeninin neden olabilir. Service Bus bu algıladığında ne tanılama içinde hello uygulama tooaid veri toplar. Merhaba veri toplandığında, hello uygulamasıdır bir girişim tooreturn tooa tutarlı bir duruma yeniden. Bu işlem oldukça hızlı bir şekilde gerçekleşir ve normal olsa kapalı kaldıkları birkaç dakika toobe tooa kullanılamaz görünen bir varlık sonuçlarında çok kısa.

Bu gibi durumlarda Merhaba istemci uygulaması oluşturan bir [System.TimeoutException] [ System.TimeoutException] veya [MessagingException] [ MessagingException] özel durum. Hizmet veri yolu azaltma bu sorunun otomatik istemci yeniden deneme mantığı hello biçiminde içerir. Merhaba yeniden deneme süresi tükendi ve hello ileti teslim edilmedi sonra gibi diğer özellikleri kullanılarak keşfedebilirsiniz [eşleştirilmiş ad alanları][paired namespaces]. Eşleştirilmiş ad alanları bu makalede ele alınan diğer uyarılar var.

### <a name="failure-of-service-bus-within-an-azure-datacenter"></a>Hizmet veri yolu hatası Azure veri merkezi içinde
Azure veri merkezi içinde bir hata Hello en olası nedeni hizmet veri yolu veya bağımlı sistemi başarısız yükseltme dağıtımı olmasıdır. Merhaba platform olgunlaştığından gibi bu hata türü hello olasılığını yayınladıklarını. Bir veri merkezi hatası de hello şunlar nedenlerle oluşabilir:

* Elektrik kesintisi (güç kaynağı ve kayboluyor oluşturma güç).
* Bağlantı (internet kesme istemcileri ve Azure arasında).

Her iki durumda da doğal ya da man-made olağanüstü durum hello sorunu neden oldu. Bu geçici toowork ve iletileri göndermeye devam edebilir, kullanabileceğiniz emin olun [eşleştirilmiş ad alanları] [ paired namespaces] hello birincil konumu yeniden sağlıklı yapılan sırada tooenable iletileri gönderilen toobe tooa ikinci konumu. Daha fazla bilgi için bkz: [en iyi uygulamalar için Service Bus kesintileri ve olağanüstü karşı uygulamalar insulating][Best practices for insulating applications against Service Bus outages and disasters].

## <a name="paired-namespaces"></a>Eşleştirilen ad alanları
Merhaba [eşleştirilmiş ad alanları] [ paired namespaces] özelliğini destekleyen senaryoları, Service Bus varlık veya dağıtım bir veri merkezi içinde kullanılamaz. Bu olay sık gerçekleşirken dağıtılmış sistemlerin hala toohandle kötü örneği senaryolarının hazırlanması gerekir. Genellikle, Service Bus bağımlı olduğu bazı öğesi kısa süreli bir sorunla karşılaştığı için bu olay gerçekleşir. toomaintain uygulama kullanılabilirliği kesinti sırasında hizmet veri yolu kullanıcılar kendi Mesajlaşma varlıkları iki ayrı ad alanları, tercihen ayrı veri merkezleri, toohost kullanabilir. Bu bölümde Hello kalanı terminolojisi aşağıdaki hello kullanır:

* Birincil ad: ad alanı ile uygulamanızı etkileşim, gönderme için hello ve alma işlemleri.
* İkincil ad alanı: yedekleme toohello birincil ad alanı olarak davranan ad alanı hello. Uygulama mantığını bu ad alanı ile etkileşime girmez.
* Yük devretme aralığı: Merhaba uygulaması önce zaman tooaccept normal hataları hello miktarını hello birincil ad alanı toohello ikincil ad alanından geçer.

Ad alanları destek eşleştirilmiş *kullanılabilirlik Gönder*. Merhaba özelliği toosend iletileri kullanılabilirlik korur gönderin. toouse gönderme kullanılabilirlik, uygulamanızın gereksinimlerine hello karşılaması gerekir:

1. İletileri yalnızca hello birincil ad alanından alınır.
2. Verilen kuyruk veya konu gönderilen iletileri tooa bozuk ulaşır.
3. Bir oturumu içinde iletiler bozuk geldiğinde. Oturumları normal işlevselliğini aradan budur. Bu, uygulamanızın oturumları toologically Grup iletileri kullandığı anlamına gelir.
4. Oturum durumu yalnızca hello birincil ad korunur.
5. Merhaba birincil kuyruk çevrimiçine ve hello ikincil sıra tüm iletileri hello birincil sıraya teslim önce iletileri kabul etmeye başlatın.

Aşağıdaki bölümlerde hello hello API'leri, hello API'leri nasıl uygulanır ve hello özelliğini kullanan gösterir örnek kod tartışın. Bu özellik ile ilişkili fatura etkileri olduğunu unutmayın.

### <a name="hello-messagingfactorypairnamespaceasync-api"></a>Merhaba MessagingFactory.PairNamespaceAsync API
Merhaba eşleştirilmiş ad alanları özelliği içerir hello [PairNamespaceAsync] [ PairNamespaceAsync] hello yöntemi [Microsoft.ServiceBus.Messaging.MessagingFactory] [ Microsoft.ServiceBus.Messaging.MessagingFactory] sınıfı:

```csharp
public Task PairNamespaceAsync(PairedNamespaceOptions options);
```

Merhaba görevi tamamlandığında hello ad alanı eşleştirme de üzerine tam ve hazır tooact herhangi olan [MessageReceiver][MessageReceiver], [QueueClient] [ QueueClient], veya [TopicClient] [ TopicClient] hello ile oluşturulan [Eventhubclient] [ MessagingFactory] örneği. [Microsoft.ServiceBus.Messaging.PairedNamespaceOptions] [ Microsoft.ServiceBus.Messaging.PairedNamespaceOptions] hello hello temel sınıfı ile kullanılabilen çifti farklı olan bir [Eventhubclient] [ MessagingFactory] nesnesi. Şu anda hello türetilmiş sınıf yalnızca adlı biridir [SendAvailabilityPairedNamespaceOptions][SendAvailabilityPairedNamespaceOptions], hello gönderme kullanılabilirlik gereksinimlerini uygular. [SendAvailabilityPairedNamespaceOptions] [ SendAvailabilityPairedNamespaceOptions] birbirine yapı oluşturucuları kümesi vardır. Hello Oluşturucusu ile Merhaba çoğu parametreleri baktığınızda, diğer oluşturucular hello hello davranışını anlayabilirsiniz.

```csharp
public SendAvailabilityPairedNamespaceOptions(
    NamespaceManager secondaryNamespaceManager,
    MessagingFactory messagingFactory,
    int backlogQueueCount,
    TimeSpan failoverInterval,
    bool enableSyphon)
```

Bu parametreler anlamları aşağıdaki hello vardır:

* *secondaryNamespaceManager*: başlatılan bir [NamespaceManager] [ NamespaceManager] bu hello hello ikincil ad alanı için örnek [PairNamespaceAsync] [ PairNamespaceAsync] yöntemi hello ikincil ad alanı yukarı tooset kullanabilirsiniz. Hello ad alanı yöneticisi kullanılan tooobtain hello hello ad alanı ve gerekli hello biriktirme listesi sıraları var olduğundan emin toomake kuyruklarda listesidir. Sıraların yoksa, oluşturulur. [NamespaceManager] [ NamespaceManager] hello özelliği toocreate hello belirteciyle gerektirir **Yönet** talep.
* *Eventhubclient*: Merhaba [Eventhubclient] [ MessagingFactory] hello ikincil ad alanı için örneği. Merhaba [Eventhubclient] [ MessagingFactory] nesnesidir kullanılan toosend ve hello [EnableSyphon] [ EnableSyphon] özelliği çok ayarlanmış**true** , hello biriktirme listesi sıralarından iletileri alacak.
* *backlogQueueCount*: biriktirme listesi hello sayısı toocreate sıralar. Bu değer, en az 1 olmalıdır. İletileri toohello biriktirme listesi gönderirken bu sıraların birini rastgele seçilir. Merhaba değeri too1 ayarlarsanız, yalnızca bir sıra herhangi bir zamanda kullanılabilir. Bu gerçekleşir ve hataları hello bir biriktirme listesi kuyruk oluşturur, hello istemci mümkün tootry farklı biriktirme listesi sırası değil ve iletinizi toosend başarısız olabilir. Bu değer toosome büyük değer ve varsayılan hello değeri too10 ayarı öneririz. Bu tooa daha yüksek değiştirebilir veya daha düşük değer ne kadar veri bağlı olarak, uygulamanızın günde gönderir. Her bir biriktirme listesi sırası iletilerinin too5 GB basılı tutabilirsiniz.
* *failoverInterval*: hello sırasında kabul edeceğiniz hataları hello birincil ad alanı üzerinde tek bir varlık toohello ikincil ad geçmeden önce süre miktarı. Yük devretme, bir varlık tarafından varlık temelinde oluşur. Tek bir ad alanındaki varlıklara sık Service Bus içinde farklı düğümleri dinamik. Bir varlık içinde bir hata başka bir hata göstermez. Bu değeri çok ayarlayabilirsiniz[System.TimeSpan.Zero] [ System.TimeSpan.Zero] toofailover toohello, ilk, geçici olmayan hatasından hemen sonra ikincil. Merhaba yük devretme Zamanlayıcı tetikleyen hatalarıdır herhangi [MessagingException] [ MessagingException] hangi hello içinde [IsTransient] [ IsTransient] özelliği false veya [System.TimeoutException][System.TimeoutException]. Diğer özel durumlar gibi [UnauthorizedAccessException] [ UnauthorizedAccessException] hello istemci yanlış yapılandırılmış belirttiğinden yük devretme, neden olmaz. A [ServerBusyException] [ ServerBusyException] hello doğru deseni 10 saniye toowait olduğundan değil neden yük devretme ardından Selamlama iletisine yeniden göndermez.
* *enableSyphon*: Bu belirli eşlemeyi hello ikincil ad alanı geri toohello birincil ad alanından iletileri de syphon olduğunu gösterir. Genel olarak, ileti gönderme uygulamalar bu değeri çok ayarlamalısınız**false**; iletileri alacak uygulamaları ayarlamalıdır bu değeri çok**doğru**. Bunun nedeni Hello sık var. ileti gönderenler daha az ileti alıcıları olmasıdır. Alıcıları Hello sayısına bağlı olarak, bir tek bir uygulama örneği tanıtıcı hello Sifon görevlerini toohave seçebilirsiniz. Birçok alıcıları kullanarak her biriktirme listesi sırası için fatura etkilere sahiptir.

toouse Merhaba kod, birincil [Eventhubclient] [ MessagingFactory] örnek, bir ikincil [Eventhubclient] [ MessagingFactory] örnek, bir ikincil [NamespaceManager] [ NamespaceManager] örneği ve [SendAvailabilityPairedNamespaceOptions] [ SendAvailabilityPairedNamespaceOptions] örneği. Merhaba çağrısı hello aşağıdaki gibi basit olabilir:

```csharp
SendAvailabilityPairedNamespaceOptions sendAvailabilityOptions = new SendAvailabilityPairedNamespaceOptions(secondaryNamespaceManager, secondary);
primary.PairNamespaceAsync(sendAvailabilityOptions).Wait();
```

Görev hello tarafından döndürülen'ne zaman hello [PairNamespaceAsync] [ PairNamespaceAsync] yöntemi tamamlayan, her şeyi ayarlanır ve toouse hazır. Merhaba görev döndürülmeden önce tüm hello arka plan iş toowork sağ eşleştirme hello için gerekli tamamlanmamış olabilir. Sonuç olarak, hello görev dönene kadar ileti gönderme başlamamalıdır. Hatalı kimlik bilgileri veya hata toocreate hello biriktirme listesi sıraları, gibi hatalar oluşursa hello görev tamamlandıktan sonra bu özel durum oluşturulur. Hello görev döndüğünde hello sıraları bulundu hello inceleyerek oluşturulmuş olduğunu doğrulayın veya [BacklogQueueCount] [ BacklogQueueCount] özelliği, [SendAvailabilityPairedNamespaceOptions] [ SendAvailabilityPairedNamespaceOptions] örneği. Kod önceki hello için bu işlem aşağıdaki gibidir:

```csharp
if (sendAvailabilityOptions.BacklogQueueCount < 1)
{
    // Handle case where no queues were created.
}
```

## <a name="next-steps"></a>Sonraki adımlar
Zaman uyumsuz Service Bus Mesajlaşma hello temellerini öğrendiğinize göre hakkında daha fazla ayrıntı okuyun [eşleştirilmiş ad alanları][paired namespaces].

[ServerBusyException]: /dotnet/api/microsoft.servicebus.messaging.serverbusyexception
[System.TimeoutException]: https://msdn.microsoft.com/library/system.timeoutexception.aspx
[MessagingException]: /dotnet/api/microsoft.servicebus.messaging.messagingexception
[Best practices for insulating applications against Service Bus outages and disasters]: service-bus-outages-disasters.md
[Microsoft.ServiceBus.Messaging.MessagingFactory]: /dotnet/api/microsoft.servicebus.messaging.messagingfactory
[MessageReceiver]: /dotnet/api/microsoft.servicebus.messaging.messagereceiver
[QueueClient]: /dotnet/api/microsoft.servicebus.messaging.queueclient
[TopicClient]: /dotnet/api/microsoft.servicebus.messaging.topicclient
[Microsoft.ServiceBus.Messaging.PairedNamespaceOptions]: /dotnet/api/microsoft.servicebus.messaging.pairednamespaceoptions
[MessagingFactory]: /dotnet/api/microsoft.servicebus.messaging.messagingfactory
[SendAvailabilityPairedNamespaceOptions]: /dotnet/api/microsoft.servicebus.messaging.sendavailabilitypairednamespaceoptions
[NamespaceManager]: /dotnet/api/microsoft.servicebus.namespacemanager
[PairNamespaceAsync]: /dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_PairNamespaceAsync_Microsoft_ServiceBus_Messaging_PairedNamespaceOptions_
[EnableSyphon]: /dotnet/api/microsoft.servicebus.messaging.sendavailabilitypairednamespaceoptions#Microsoft_ServiceBus_Messaging_SendAvailabilityPairedNamespaceOptions_EnableSyphon
[System.TimeSpan.Zero]: https://msdn.microsoft.com/library/system.timespan.zero.aspx
[IsTransient]: /dotnet/api/microsoft.servicebus.messaging.messagingexception#Microsoft_ServiceBus_Messaging_MessagingException_IsTransient
[UnauthorizedAccessException]: https://msdn.microsoft.com/library/system.unauthorizedaccessexception.aspx
[BacklogQueueCount]: /dotnet/api/microsoft.servicebus.messaging.sendavailabilitypairednamespaceoptions?redirectedfrom=MSDN#Microsoft_ServiceBus_Messaging_SendAvailabilityPairedNamespaceOptions_BacklogQueueCount
[paired namespaces]: service-bus-paired-namespaces.md
