---
title: "aaaAzure depolama kuyrukları ve Service Bus kuyruklarını - karşılaştırılan ve contrasted | Microsoft Docs"
description: "İki tür Azure tarafından sunulan kuyruk arasındaki benzerlikler ve farkları analiz eder."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: tysonn
ms.assetid: f07301dc-ca9b-465c-bd5b-a0f99bab606b
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 08/07/2017
ms.author: sethm
ms.openlocfilehash: f8b915e73ea3c82d823a96bf23c8c9e24c96aa42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="storage-queues-and-service-bus-queues---compared-and-contrasted"></a>Depolama kuyrukları ve Service Bus kuyruklarını - karşılaştırılan ve contrasted
Bu makalede hello farklar ve hello iki tür bugün Microsoft Azure tarafından sunulan kuyruk arasındaki benzerlikler Çözümler: depolama kuyrukları ve Service Bus kuyruklarını. Bu bilgileri kullanarak, karşılaştırın ve hello ilgili teknolojileri karşıtlık ve kullanabilirsiniz mümkün toomake uygun çözümü hakkında daha fazla bilinçli bir karar ihtiyaçlarınıza uygun olabilir.

## <a name="introduction"></a>Giriş
Azure kuyruk mekanizmasıyla iki türlerini destekler: **depolama kuyrukları** ve **Service Bus kuyruklarını**.

**Depolama kuyrukları**, hello parçası olan [Azure depolama](https://azure.microsoft.com/services/storage/) altyapı, özellik içinde ve hizmetleri arasında güvenilir ve kalıcı Mesajlaşma sağlayan basit bir GET/PUT/GÖZLEM REST tabanlı arabirim.

**Service Bus kuyruklarını** daha geniş bir parçası olan [Azure Mesajlaşma](https://azure.microsoft.com/services/service-bus/) altyapısını destekleyen Yayınla/Abone ol yanı sıra queuing ve daha gelişmiş tümleştirme desenleri. Service Bus kuyrukları/konuları/abonelikler hakkında daha fazla bilgi için bkz: Merhaba [Service Bus genel bakış](service-bus-messaging-overview.md).

Depolama kuyrukları queuing iki teknolojiyi aynı anda mevcut olsa da, ilk Azure Storage hizmetleri üzerine inşa ayrılmış kuyruk depolama mekanizması olarak eklenmiştir. Service Bus kuyruklarını hello "tasarlanmış altyapı toointegrate uygulamaları veya birden çok iletişim protokolü, veri sözleşmeleri, güven etki alanları ve/veya ağ ortamları yayılabilir uygulama bileşenleri Mesajlaşma" daha geniş üzerinde oluşturulmuştur.

## <a name="technology-selection-considerations"></a>Teknoloji seçimi konuları
Depolama kuyrukları ve Service Bus kuyruklarını hello message queuing hizmeti şu anda Microsoft Azure üzerinde sunulan uygulamalarıdır. Her birini seçin veya diğer hello veya her ikisi de belirli çözüm ya da iş/teknik sorun çözme hello gereksinimlerine bağlı olarak kullanmak anlamına gelir biraz farklı özellik kümesi vardır.

Hangi queuing teknolojisi hello amacı belirli bir çözümü için uygun belirlerken, çözüm mimarları ve geliştiricileri hello önerileri aşağıda dikkate almalısınız. Daha fazla ayrıntı için hello sonraki bölüme bakın.

Bir çözümü Mimarı/geliştirici, olarak **depolama kuyruklarını kullanmayı düşünmelisiniz** zaman:

* Uygulamanızın üzerinde 80 GB iletileri Merhaba iletileri 7 günden daha kısa bir ömre sahip olduğu bir kuyrukta depolamanız gerekir.
* Uygulamanızı hello sıra içinde bir ileti işlenmek üzere tootrack ilerleme istemektedir. Bu ileti işlenirken hello çalışan çökmesi durumunda faydalı olur. Bir sonraki alt daha sonra bu bilgileri toocontinue burada hello önceki çalışan bıraktığınız gelen kullanabilirsiniz.
* Sunucu tarafı günlükleri tüm, kuyruklar karşı yürütülen hello işlemleri gerektirir.

Bir çözümü Mimarı/geliştirici, olarak **Service Bus kuyruklarını kullanmayı düşünmelisiniz** zaman:

* Çözümünüzü toopoll hello sıra kalmadan mümkün tooreceive iletileri olması gerekir. Service Bus ile bu hello elde edilebilir hello uzun yoklama kullanımını Service Bus destekleyen hello TCP dayanan protokoller kullanarak işlemini alırsınız.
* Çözümünüzü hello sıra tooprovide bir garantili ilk-giren ilk çıkar gerektirir (FIFO) sıralı teslim.
* Simetrik bir deneyim Azure ve Windows Server (özel bulut) üzerinde istediğiniz. Daha fazla bilgi için bkz: [Windows Server için hizmet veri yolu](https://msdn.microsoft.com/library/dn282144.aspx).
* Çözümünüzü mümkün toosupport otomatik yinelenen algılama olması gerekir.
* Uygulama tooprocess iletilerinizi paralel uzun süre çalışan akış olarak istediğiniz (iletileri hello kullanarak bir akış ile ilişkili [SessionID](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.sessionid?view=azureservicebus-4.0.0#Microsoft_ServiceBus_Messaging_BrokeredMessage_SessionId) selamlama iletisine özellikte). Bu modelde, her bir düğümünde uygulama hello karşılıklı toomessages akışlar için rekabet. Bir akış düğümü tüketen tooa verildiğinde hello düğümü işlemleri kullanarak hello uygulama akışı durumunu hello durumunu inceleyebilirsiniz.
* Çözümünüzü işlem davranışı ve gönderme ya da birden fazla ileti kuyruktan alırken kararlılık gerektirir.
* Merhaba yaşam süresi (TTL) karakteristiğini hello uygulamaya özgü iş yükü, hello 7 günlük sürede aşabilir.
* Uygulamanız 64 KB aşabilir iletilerini işleme ancak olası değil yaklaşım 256 KB sınırını hello.
* Kuyruklar, bir rol tabanlı erişim modeli toohello gereksinim tooprovide ile ilgilidir ve göndericiler ile alıcılar için farklı hakları/izinler.
* Sıra boyutu 80 GB'den büyük büyüyecektir değil.
* Toouse hello AMQP 1.0 standartlara dayalı Mesajlaşma Protokolü istiyor. AMQP hakkında daha fazla bilgi için bkz: [hizmet veri yolu AMQP genel bakış](service-bus-amqp-overview.md).
* Bir son ek alıcılar (aboneleri için), kesintisiz tümleştirilmesi, her biri bazı veya tüm bağımsız bir kopyasını alır sağlayan sıra tabanlı noktadan noktaya iletişim tooa ileti değişim deseni geçişini planladığınız toohello sıraya gönderilen iletileri. Merhaba ikinci yerel olarak Service Bus tarafından sağlanan toohello Yayınla/Abone ol yeteneği anlamına gelir.
* Mesajlaşma çözümü mümkün toosupport hello "en-çoğu-kez" teslim garantisi, toobuild hello ek altyapı bileşenleri için hello gerek kalmadan olması gerekir.
* Toobe mümkün toopublish ister ve iletileri toplu kullanmak.

## <a name="comparing-storage-queues-and-service-bus-queues"></a>Depolama kuyrukları ve Service Bus kuyruklarını karşılaştırma
Aşağıdaki bölümlerde hello Hello tablolarda sıra özelliklerinin mantıksal bir gruplandırma sağlayın ve hello yetenekler depolama kuyrukları ve Service Bus kuyruklarını bir bakışta karşılaştırmanıza olanak tanır.

## <a name="foundational-capabilities"></a>Temel özellikler
Bu bölümde bazı özelliklerini depolama kuyrukları ve hizmet veri yolu sıraları sağladığı hello temel queuing karşılaştırır.

| Karşılaştırma ölçütü | Depolama kuyrukları | Service Bus Kuyrukları |
| --- | --- | --- |
| Garanti sıralama |**Hayır** <br/><br>Daha fazla bilgi için hello ilk Not hello "Ek bilgiler" bölümüne bakın.</br> |**Evet - ilk-giren ilk çıkar (FIFO)**<br/><br>(oturumları Mesajlaşma hello aracılığıyla kullanım) |
| Teslim garantisi |**En az bir kere** |**En az bir kere**<br/><br/>**En çok-bir kez** |
| Atomik işlem desteği |**Hayır** |**Evet**<br/><br/> |
| Davranış alma |**Olmayan engelleme**<br/><br/>(hemen yeni bir ileti bulunursa tamamlandıktan) |**Zaman aşımı olan ve olmayan engelleme**<br/><br/>(uzun yoklama veya hello sunan ["Comet teknik"](http://go.microsoft.com/fwlink/?LinkId=613759))<br/><br/>**Olmayan engelleme**<br/><br/>(Merhaba .NET kullanımını API yalnızca yönetilen) |
| Anında iletme stili API |**Hayır** |**Evet**<br/><br/>[Onmessageoptions](/dotnet/api/microsoft.servicebus.messaging.queueclient.onmessage#Microsoft_ServiceBus_Messaging_QueueClient_OnMessage_System_Action_Microsoft_ServiceBus_Messaging_BrokeredMessage__) ve **Onmessageoptions** oturumları .NET API. |
| Mod alma |**Peek & kira** |**Peek & Kilitle**<br/><br/>**Alma & Sil** |
| Özel erişim modu |**Kira tabanlı** |**Kilit tabanlı** |
| Kira/süre kilidi |**30 saniye (varsayılan)**<br/><br/>**7 gün (en)** (yenileme veya hello kullanarak bir ileti kira serbest [UpdateMessage](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.updatemessage.aspx) API.) |**60 saniye (varsayılan)**<br/><br/>Hello kullanarak bir ileti kilidi yenileyebilirsiniz [RenewLock](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.renewlock#Microsoft_ServiceBus_Messaging_BrokeredMessage_RenewLock) API. |
| Kira/duyarlık kilidi |**İleti düzeyi**<br/><br/>(her ileti sonra gereken şekilde hello kullanarak hello ileti işlenirken güncelleştirebilirsiniz bir başka zaman aşımı değerine sahip [UpdateMessage](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.updatemessage.aspx) API) |**Sıranın düzeyi**<br/><br/>(her sıranın kilit uygulanan duyarlık tooall kendi iletilerinin vardır, ancak hello kullanarak hello kilit yenileyebilirsiniz [RenewLock](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.renewlock#Microsoft_ServiceBus_Messaging_BrokeredMessage_RenewLock) API.) |
| Toplu alma |**Evet**<br/><br/>(açıkça ileti sayısı mesajlarını tooa en fazla 32 iletileri alınırken belirtme) |**Evet**<br/><br/>(örtük olarak getirme öncesi özellik etkinleştirme veya açıkça hello hareketlerinin kullanın) |
| Toplu iş gönderme |**Hayır** |**Evet**<br/><br/>(Merhaba kullanımı hareketleri veya istemci tarafı toplu işleme) |

### <a name="additional-information"></a>Ek bilgiler
* Depolama sıralarındaki iletileri genellikle ilk-giren ilk çıkar ancak bazen bozuk olabilirler; Örneğin, bir iletinin görünürlük zaman aşımı süresi (örneğin, bir istemci uygulaması işleme sırasında kilitlenen) sonucunda süresi dolduğunda. Merhaba görünürlük zaman aşımı süresi dolduğunda, selamlama iletisine yeniden hello sıra başka bir çalışan toodequeue için görünür hale gelir. Bu noktada, hello yeni görünür ileti hello sırasına yerleştirilecek (toobe kuyruktan çıkarıldı yeniden) ilk olarak sıraya alınan sonra olan bir ileti sonra.
* Merhaba, Service Bus kuyruklarını FIFO desende Mesajlaşma oturumları hello kullanılmasını gerektiren garanti. Hello alınan ileti işlenirken bir uygulama hello olay Hello çöküyor **Peek & Kilitle** sıra alıcı modu, hello sonraki bir Mesajlaşma oturumu kabul, sonra hello başarısız iletisiyle başlar, yaşam süresi (TTL) süresi sona eriyor.
* Depolama sorguları gibi uygulama bileşenleri tooincrease ölçeklenebilirlik ve dayanıklılık hataları için kesilmesi tasarlanmış toosupport standart queuing senaryolar, Yük Dengeleme ve süreç iş akışlarının oluşturulmasını.
* Service Bus kuyruklarını destek hello *en az bir kere* teslim garanti edilemez. Ayrıca, hello *adresindeki çoğu-kez* anlamsal oturum durumu toostore hello uygulama durumu kullanarak desteklenen ve işlemleri tooatomically kullanarak ileti alma ve güncelleştirme hello oturum durumu.
* Geliştiriciler hem işletim ekipleri, kuyruklar, tablolar ve BLOB'lar – arasında Tekdüzen ve tutarlı bir programlama modeli depolama kuyrukları sağlar.
* Service Bus kuyruklarını yerel hareketlerinin tek bir sıraya için hello bağlamda destek sağlar.
* Merhaba **alma ve silme** Service Bus tarafından desteklenen modu işlem sayısını (ve ilişkili maliyet) Mesajlaşma hello özelliği tooreduce hello karşılığında alçaltılmış teslim güvence sağlar.
* Depolama kuyrukları iletileri için hello özelliği tooextend hello kiraları ile kiraları sağlar. Bu hello çalışanları toomaintain kısa kira iletileri sağlar. Bir çalışan kilitlenirse bu durum, bu nedenle, selamlama iletisine hızlı bir şekilde yeniden başka bir çalışan tarafından işlenebilir. Ayrıca, bu hello geçerli daha uzun kira süresi tooprocess gerekiyorsa bir çalışan bir ileti hello kira genişletebilirsiniz.
* Depolama kuyrukları hello içine alınırken ayarlayın veya bir ileti kuyruktan alma yapabileceğiniz bir görünürlük zaman aşımını sunar. Ayrıca, çalışma zamanında farklı kira değerleri içeren bir ileti güncelleştirebilir ve güncelleştirme farklı değerleri hello iletilerinde arasında aynı sıra. Hizmet veri yolu kilit zaman aşımı hello sıra meta verilerde tanımlanan; Ancak, arama hello tarafından hello kilit yenileyebilirsiniz [RenewLock](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.renewlock#Microsoft_ServiceBus_Messaging_BrokeredMessage_RenewLock) yöntemi.
* Service Bus kuyruklarını işlemi bir engelleme almak üzere hello en uzun zaman aşımı 24 gündür. Ancak, REST tabanlı zaman aşımları 55 saniyelik en fazla bir değere sahip.
* İstemci-tarafı toplu işlem tarafından hizmet veri yolu etkinleştirir sıra istemci toobatch birden fazla ileti tek gönderme işlemi sağlanan. Toplu işleme yalnızca zaman uyumsuz gönderme işlemleri için kullanılabilir.
* Merhaba 200 TB'ye tavan depolama sıralarının (daha fazla hesapları sanallaştırmak olduğunda) ve sınırsız sıraları gibi özellikler SaaS sağlayıcıları için ideal bir platform kolaylaştırır.
* Kullanıcı erişim denetimi mekanizması temsilci ve depolama sorguları bir esnek sağlar.

## <a name="advanced-capabilities"></a>Gelişmiş Özellikler
Bu bölüm, depolama kuyrukları ve Service Bus kuyruklarını tarafından sağlanan gelişmiş özellikleri karşılaştırır.

| Karşılaştırma ölçütü | Depolama kuyrukları | Service Bus Kuyrukları |
| --- | --- | --- |
| Zamanlanan teslim |**Evet** |**Evet** |
| Otomatik ölü harflerinin |**Hayır** |**Evet** |
| Artan sıra yaşam süresi değeri |**Evet**<br/><br/>(yerinde görünürlük zaman aşımını güncelleştirilmesini) |**Evet**<br/><br/>(ayrılmış bir API işlevi sağlanır) |
| Zehirli ileti desteği |**Evet** |**Evet** |
| Yerinde güncelleştirme |**Evet** |**Evet** |
| Sunucu tarafında işlem günlüğü |**Evet** |**Hayır** |
| Depolama ölçümleri |**Evet**<br/><br/>**Ölçümleri dakika**: kullanılabilirlik, TP'leri, API için gerçek zamanlı ölçümleri çağrı sayısı, hata sayısı ve tüm gerçek (dakika başına toplanır ve yalnızca üretimde ne gelen birkaç dakika içinde bildirilen. zaman içinde daha sağlar Daha fazla bilgi için bkz: [Storage Analytics ölçümleri hakkında](/rest/api/storageservices/fileservices/About-Storage-Analytics-Metrics). |**Evet**<br/><br/>(Toplu sorguları çağırarak [GetQueues](/dotnet/api/microsoft.servicebus.namespacemanager.getqueues#Microsoft_ServiceBus_NamespaceManager_GetQueues)) |
| Durum Yönetimi |**Hayır** |**Evet**<br/><br/>[Microsoft.ServiceBus.Messaging.EntityStatus.Active](/dotnet/api/microsoft.servicebus.messaging.entitystatus.active), [Microsoft.ServiceBus.Messaging.EntityStatus.Disabled](/dotnet/api/microsoft.servicebus.messaging.entitystatus.disabled), [Microsoft.ServiceBus.Messaging.EntityStatus.SendDisabled](/dotnet/api/microsoft.servicebus.messaging.entitystatus.senddisabled), [Microsoft.ServiceBus.Messaging.EntityStatus.ReceiveDisabled](/dotnet/api/microsoft.servicebus.messaging.entitystatus.receivedisabled) |
| Otomatik iletme iletisi |**Hayır** |**Evet** |
| Sıra işlevi Temizle |**Evet** |**Hayır** |
| İleti grupları |**Hayır** |**Evet**<br/><br/>(oturumları Mesajlaşma hello aracılığıyla kullanım) |
| İleti grubu başına uygulama durumu |**Hayır** |**Evet** |
| Yinelenen algılama |**Hayır** |**Evet**<br/><br/>(Merhaba Gönderen tarafında yapılandırılabilir) |
| Gözatma ileti grupları |**Hayır** |**Evet** |
| İleti oturumları Kimliğine göre getirme |**Hayır** |**Evet** |

### <a name="additional-information"></a>Ek bilgiler
* Her iki queuing teknolojileri daha sonraki bir zamanda teslim edilmek üzere zamanlanmış bir ileti toobe etkinleştirin.
* Sıra otomatik iletme sıraları tooauto kendi iletileri tooa tek sıra, hangi hello alıcı uygulamasından selamlama iletisine tüketir iletme binlerce sağlar. Bu mekanizma tooachieve güvenlik, akış denetimi ve her ileti yayımcı arasında yalıtmaya depolama kullanabilirsiniz.
* Depolama kuyrukları, ileti içeriği güncelleştirmek için destek sağlar. Böylece sıfırdan yerine hello en son bilinen kontrol noktasından, işlenebilir, bu işlev kalıcı durum bilgilerini ve artımlı ilerleme durumu güncelleştirmeleri için hello iletisine kullanabilirsiniz. Service Bus kuyrukları ile Merhaba etkinleştirebilirsiniz ileti oturumları hello kullanımı aracılığıyla aynı senaryo. Oturumları toosave etkinleştirin ve hello uygulama işlem durumunu al (kullanarak [SetState](/dotnet/api/microsoft.servicebus.messaging.messagesession.setstate#Microsoft_ServiceBus_Messaging_MessageSession_SetState_System_IO_Stream_) ve [GetState](/dotnet/api/microsoft.servicebus.messaging.messagesession.getstate#Microsoft_ServiceBus_Messaging_MessageSession_GetState)).
* [Kullanılmayan lettering](service-bus-dead-letter-queues.md), olduğu Service Bus kuyruklarını tarafından desteklenen yalnızca hello alıcı uygulama tarafından başarıyla işlenemiyor iletileri yalıtmak için kullanışlı olabilir veya iletileri hedeflerine son ulaştığında tooan süresi yaşam süresi (TTL) özelliği. ne kadar bir ileti hello kuyruğunda kalır Hello TTL değeri belirtir. Service Bus ile selamlama iletisine taşınan tooa özel sıra hello TTL süresi sona erdiğinde $DeadLetterQueue adlı olacaktır.
* Depolama sıralarda, ileti Merhaba uygulaması kuyruktan alma hello incelerken toofind "zarar" iletileri  **[DequeueCount](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueuemessage.dequeuecount.aspx)**  hello iletinin özelliği. Varsa **DequeueCount** belirli bir eşik değerinden yüksek Merhaba uygulaması hello ileti tooan uygulama tanımlı "sahipsiz" sırası taşır.
* Depolama kuyrukları tüm hello hareketlerinin ayrıntılı günlüğü hello sıra karşı yürütülen yanı sıra ölçümleri toplanan tooobtain etkinleştirin. Bu seçeneklerin ikisi de hata ayıklama ve depolama sorguları uygulamanızı nasıl kullandığını anlamak için kullanışlıdır. Ayrıca, uygulamanızın performans ayarlama ve kuyrukları kullanmanın hello maliyetlerini azaltmak için yararlıdır.
* "Service Bus tarafından desteklenen ileti oturumları" Merhaba kavramı tooa ait iletileri sırayla iletileri ve bunların ilgili alıcılar arasında oturum benzeri benzeşim oluşturur belirli bir alıcı ile ilgili belirli bir mantıksal Grup toobe sağlar. Bu ayarı hello tarafından Service Bus işlevindeki Gelişmiş etkinleştirebilirsiniz [SessionID](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.sessionid#Microsoft_ServiceBus_Messaging_BrokeredMessage_SessionId) bir ileti özelliği. Alıcılar, ardından belirli bir oturum kimliği üzerinde dinleme ve belirtilen hello paylaşmak iletilerini oturum tanımlayıcısı.
* Merhaba Service Bus kuyruklarını tarafından otomatik olarak desteklenen yineleme algılama işlevi gönderilen yinelenen iletileri tooa kuyruk veya konu başlığı, hello değerine göre hello kaldırır [MessageID](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.messageid#Microsoft_ServiceBus_Messaging_BrokeredMessage_MessageId) özelliği.

## <a name="capacity-and-quotas"></a>Kapasite ve kotaları
Bu bölümde depolama kuyrukları ve Service Bus kuyrukları hello açısından karşılaştırır [kapasiteyi ve kotayı](service-bus-quotas.md) geçerli olabilir.

| Karşılaştırma ölçütü | Depolama kuyrukları | Service Bus Kuyrukları |
| --- | --- | --- |
| En büyük sıra boyutu |**500 TB**<br/><br/>(sınırlı tooa [tek bir depolama hesabı kapasitesi](../storage/common/storage-introduction.md#queue-storage)) |**1 GB too80 GB**<br/><br/>(kuyruk oluşturma sırasında tanımlanan ve [bölümleme etkinleştirme](service-bus-partitioning.md) – bkz hello "Ek bilgiler" bölümüne) |
| İleti boyutu üst sınırı |**64 KB**<br/><br/>(48 kullanırken KB **Base64** kodlama)<br/><br/>Azure, kuyruklar ve BLOB'lar – enqueue too200GB tek bir öğe için yukarı olabilir, bu noktada birleştirerek büyük iletileri destekler. |**256 KB** veya **1 MB**<br/><br/>(başlık ve gövde, en fazla üstbilgi boyutu dahil: 64 KB).<br/><br/>Merhaba üzerinde bağlıdır [hizmet katmanı](service-bus-premium-messaging.md). |
| En fazla ileti TTL |**7 gün** |**`TimeSpan.Max`** |
| Kuyruğu en yüksek sayısı |**Sınırsız** |**10,000**<br/><br/>(hizmet ad alanı artırılabilir) |
| Maksimum eşzamanlı istemci sayısı |**Sınırsız** |**Sınırsız**<br/><br/>(yalnızca 100 eş zamanlı bağlantı sınırı tooTCP Protokolü tabanlı iletişim için geçerlidir) |

### <a name="additional-information"></a>Ek bilgiler
* Hizmet veri yolu kuyruğu boyutu sınırları zorlar. Merhaba en büyük sıra boyutu hello kuyruk oluşturma sırasında belirtilir ve 1 ile 80 GB arasında bir değer olabilir. Merhaba kuyruk boyutu değeri hello sırasının oluşturulması ayarlanmış ulaştıysanız, ek gelen iletileri reddedilir ve bir özel durum kodu çağırma hello tarafından alınır. Service Bus kotaları hakkında daha fazla bilgi için bkz: [Service Bus kotaları](service-bus-quotas.md).
* Merhaba, [standart katmanı](service-bus-premium-messaging.md), Service Bus kuyruklarını boyutlarında, 1, 2, 3, 4 veya 5 GB (Merhaba varsayılan olarak 1 GB) oluşturabilirsiniz. Merhaba Premium katmanındaki too80 GB boyutunda sıralarını oluşturabilirsiniz. Standart bölümlendirme ile katmanı, etkin (Merhaba varsayılan olmayan), hizmet veri yolu için belirttiğiniz her GB 16 bölümler oluşturur. 5 GB cinsinden boyutu olan bir kuyruk oluşturun, bu nedenle, 16 bölümlerle hello en büyük sıra boyutu (5 * 16) haline gelir = 80 GB. Merhaba üzerinde kendi girdisi bakarak bölümlenmiş kuyruk veya konu en büyük boyutunu hello görebilirsiniz [Azure portal][Azure portal]. Merhaba Premium katmanındaki yalnızca 2 bölüm sıra oluşturulur.
* Depolama kuyruklarla hello hello iletinin içeriği XML uyumlu değil, sonra bu olmalıdır **Base64** kodlanmış. Varsa, **Base64**-selamlama iletisine kodlamak, hello kullanıcı yükü 64 KB yerine too48 KB yukarı olabilir.
* Service Bus kuyrukları ile bir sırada depolanan her ileti iki bölümden oluşur: bir başlık ve gövde. Merhaba toplam boyutu selamlama iletisine hello maksimum ileti boyutu hello hizmet katmanı tarafından desteklenen aşamaz.
* İstemciler ile Service Bus kuyruklarını hello TCP protokolü iletişim kurduğunda, hello en fazla eşzamanlı bağlantı tooa tek Service Bus kuyruğuna sınırlı too100 sayısıdır. Bu numara göndericiler ile alıcılar arasında paylaşılır. Bu kotasına ulaşıldığında, sonraki istekleri için ek bağlantıları reddedilir ve bir özel durum kodu çağırma hello tarafından alınır. Bu sınır REST tabanlı API kullanarak toohello sıraları bağlanan istemciler üzerinde uygulanan değil.
* Tek bir hizmet veri yolu ad alanı 10. 000'den fazla kuyruklarda gerektiriyorsa, hello Azure Destek ekibine başvurun ve artışı isteyebilir. tooscale Service Bus 10.000 kuyruklarla ötesinde ek ad alanlarını hello kullanarak da oluşturabilir [Azure portal][Azure portal].

## <a name="management-and-operations"></a>Yönetim ve işlemler
Bu bölüm, depolama kuyrukları ve hizmet veri yolu sıraları sağladığı hello yönetim özellikleri karşılaştırılır.

| Karşılaştırma ölçütü | Depolama kuyrukları | Hizmet Veri Yolu kuyrukları |
| --- | --- | --- |
| Yönetim Protokolü |**HTTP/HTTPS üzerinden getirin** |**HTTPS üzerinden getirin** |
| Çalışma zamanı Protokolü |**HTTP/HTTPS üzerinden getirin** |**HTTPS üzerinden getirin**<br/><br/>**AMQP 1.0 Standart (TCP TLS ile)** |
| .NET API’si |**Evet**<br/><br/>(.NET depolama İstemcisi API) |**Evet**<br/><br/>(.NET Service Bus API) |
| Yerel C++ |**Evet** |**Evet** |
| Java API’si |**Evet** |**Evet** |
| PHP API |**Evet** |**Evet** |
| Node.js API |**Evet** |**Evet** |
| İsteğe bağlı meta veri desteği |**Evet** |**Hayır** |
| Sıra adlandırma kuralları |**Too63 karakter uzunluğunda**<br/><br/>(Bir sıra adı harfler küçük olmalıdır.) |**Too260 karakter uzunluğunda**<br/><br/>(Kuyruk yollar ve adları büyük küçük harfe duyarsızdır.) |
| Get kuyruk uzunluğu işlevi |**Evet**<br/><br/>(Silinmiş olmadan iletileri TTL hello zaman aşımına uğrarsa yaklaşık değeri.) |**Evet**<br/><br/>(Değer. tam, zaman içinde nokta) |
| Peek işlevi |**Evet** |**Evet** |

### <a name="additional-information"></a>Ek bilgiler
* Depolama kuyrukları, ad/değer çiftleri hello formunda uygulanan toohello sıra açıklaması olabilir rasgele öznitelikleri için destek sağlar.
* Her iki sıra teknolojileri hello özelliği toopeek toolock gerek kalmadan bir ileti sunar queue explorer/tarayıcı aracı uygularken yararlı olabilecek BT.
* Merhaba Service Bus .NET aracılı Mesajlaşma API'lerini Dengeleme tam çift yönlü TCP bağlantılarını Gelişmiş performans için HTTP üzerinden tooREST karşılaştırılan ve hello AMQP 1.0 standart protokol desteği.
* Depolama sıraların adları 3-63 karakter uzunluğunda olabilir, küçük harf, sayı ve tire içerebilir. Daha fazla bilgi için bkz: [adlandırma kuyrukları ve meta verileri](/rest/api/storageservices/fileservices/Naming-Queues-and-Metadata).
* Hizmet veri yolu sıra adları too260 karakter uzunluğunda olmalıdır ve daha az kısıtlayıcı adlandırma kurallarına sahiptir. Hizmet veri yolu kuyruğu adlar harf, rakam, nokta, kısa çizgi ve alt çizgi içerebilir.

## <a name="authentication-and-authorization"></a>Kimlik doğrulama ve yetkilendirme
Bu bölümde depolama kuyrukları ve Service Bus kuyruklarını tarafından desteklenen hello kimlik doğrulama ve yetkilendirme özellikleri açıklanmaktadır.

| Karşılaştırma ölçütü | Depolama kuyrukları | Service Bus Kuyrukları |
| --- | --- | --- |
| Kimlik Doğrulaması |**Simetrik anahtar** |**Simetrik anahtar** |
| Güvenlik modeli |SAS belirteci üzerinden yetkilendirilmiş erişim. |SAS |
| Kimlik sağlayıcısı Federasyon |**Hayır** |**Evet** |

### <a name="additional-information"></a>Ek bilgiler
* Her istek tooeither teknolojileri queuing Merhaba, kimliğinizin doğrulanması gerekiyor. Anonim erişimi olan genel sıralar desteklenmiyor. Kullanarak [SAS](service-bus-sas.md), bu senaryo yalnızca yazma SAS, salt okunur SAS veya tam erişim SAS yayımlayarak karşılayabilir.
* Merhaba kimlik doğrulama şeması tarafından depolama sıraları içerir sağlanan bir karma tabanlı ileti kimlik doğrulama kodu (HMAC) bir simetrik anahtar hello kullanımını hello SHA-256 algoritması ile hesaplanır ve olarak kodlanmış bir **Base64** dize. Merhaba ilgili protokolü hakkında daha fazla bilgi için bkz: [hello Azure Storage Hizmetleri için kimlik doğrulaması](/rest/api/storageservices/fileservices/Authentication-for-the-Azure-Storage-Services). Service Bus kuyruklarını simetrik anahtarlar kullanılarak benzer bir modelini destekler. Daha fazla bilgi için bkz: [paylaşılan erişim imzası kimlik doğrulaması Service Bus ile](service-bus-sas.md).

## <a name="conclusion"></a>Sonuç
Merhaba iki teknolojileri daha derin bir anlayış sağlamasını tarafından üretileceği daha bilinçli bir karar sıraya teknolojisi toouse mümkün toomake olması ve ne zaman olur. Merhaba toouse depolama sorguları ya da hizmet veri yolu zaman açıkça kuyruklar hakkında karar bir dizi etkene bağlıdır. Bu etkenler yoğun hello tek tek ihtiyaçlara göre uygulamanız ve mimarisinin bağlı olabilir. Uygulama zaten Microsoft Azure hello çekirdek özellikleri kullanıyorsa, özellikle temel iletişimi ve Hizmetleri veya 80 GB boyutunda daha büyük olabilir gerek sıraları arasında Mesajlaşma gerekiyorsa toochoose depolama kuyruklarında tercih edebilirsiniz.

Service Bus kuyruklarını birkaç oturumları, işlemleri gibi gelişmiş özellikler sağlamak için yinelenen saptama, otomatik ulaşmayan posta ve sürekli yayımlama/abonelik özellikleri, bunlar olabilir bir tercih edilen seçenek karma oluşturuluyorsa uygulama veya aksi durumda, uygulamanızın bu özelliklerden gerektirip gerektirmediğini.

## <a name="next-steps"></a>Sonraki adımlar
aşağıdaki makaleleri hello daha fazla yönerge ve depolama sorguları ya da Service Bus kuyruklarını kullanma hakkında bilgi sağlar.

* [Service Bus kuyrukları ile çalışmaya başlama](service-bus-dotnet-get-started-with-queues.md)
* [Nasıl tooUse hello kuyruk depolama birimi hizmeti](../storage/queues/storage-dotnet-how-to-use-queues.md)
* [Aracılı Mesajlaşma kullanan Service Bus performans iyileştirmeleri için en iyi yöntemler](service-bus-performance-improvements.md)
* [Kuyruklar ve konu başlıkları Azure Service Bus (blog yayını) içinde Tanıtımı](http://www.code-magazine.com/article.aspx?quickid=1112041)
* [Geliştirici Kılavuzu tooService Bus hello](http://www.cloudcasts.net/devguide/Default.aspx?id=11030)
* [Azure'da Hello Message Queuing hizmeti kullanma](http://www.developerfusion.com/article/120197/using-the-queuing-service-in-windows-azure/)

[Azure portal]: https://portal.azure.com

