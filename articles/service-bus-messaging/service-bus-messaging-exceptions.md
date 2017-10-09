---
title: "aaaAzure Service Bus Mesajlaşma özel durumlar | Microsoft Docs"
description: "Service Bus Mesajlaşma özel durumlar ve önerilen eylemler listesi."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 3d8526fe-6e47-4119-9f3e-c56d916a98f9
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/06/2017
ms.author: sethm
ms.openlocfilehash: 0a206b7bbc808c1190044c1dfd6ffd47b9d454fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-messaging-exceptions"></a>Hizmet Veri Yolu mesajlaşma özel durumları
Bu makalede Microsoft Azure Service Bus hello tarafından oluşturulan bazı özel durumlar listelenir API'leri Mesajlaşma. Bu başvuru konusu toochange, bu nedenle geri Güncelleştirmeleri denetle.

## <a name="exception-categories"></a>Özel durum kategorileri
Merhaba ilişkili eylemi birlikte tootry toofix alabilir, Hello Mesajlaşma API'lerini oluşturur kategorileri aşağıdaki hello dönebilir özel durumlar bunları. Merhaba anlamı ve bir özel durum nedenlerini Mesajlaşma varlığı (kuyruklar/konular veya olay hub'ları) hello türüne bağlı olarak değişebilir dikkat edin:

1. Kodlama hatası kullanıcı ([System.ArgumentException](https://msdn.microsoft.com/library/system.argumentexception.aspx), [System.InvalidOperationException](https://msdn.microsoft.com/library/system.invalidoperationexception.aspx), [System.OperationCanceledException](https://msdn.microsoft.com/library/system.operationcanceledexception.aspx), [ System.Runtime.Serialization.SerializationException](https://msdn.microsoft.com/library/system.runtime.serialization.serializationexception.aspx)). Genel eylem: toofix hello kod devam etmeden önce deneyin.
2. Kurulum/yapılandırma hatası ([Microsoft.ServiceBus.Messaging.MessagingEntityNotFoundException](/dotnet/api/microsoft.servicebus.messaging.messagingentitynotfoundexception), [System.UnauthorizedAccessException](https://msdn.microsoft.com/library/system.unauthorizedaccessexception.aspx). Genel eylem: yapılandırmanızı inceleyin ve gerekirse değiştirin.
3. Geçici özel durumları ([Microsoft.ServiceBus.Messaging.MessagingException](/dotnet/api/microsoft.servicebus.messaging.messagingexception), [Microsoft.ServiceBus.Messaging.ServerBusyException](/dotnet/api/microsoft.servicebus.messaging.serverbusyexception), [ Microsoft.ServiceBus.Messaging.MessagingCommunicationException](/dotnet/api/microsoft.servicebus.messaging.messagingcommunicationexception)). Genel eylem: hello işlemi yeniden deneyin veya kullanıcılara bildirin.
4. Diğer özel durumlar ([System.Transactions.TransactionException](https://msdn.microsoft.com/library/system.transactions.transactionexception.aspx), [System.TimeoutException](https://msdn.microsoft.com/library/system.timeoutexception.aspx), [Microsoft.ServiceBus.Messaging.MessageLockLostException](/dotnet/api/microsoft.servicebus.messaging.messagelocklostexception), [Microsoft.ServiceBus.Messaging.SessionLockLostException](/dotnet/api/microsoft.servicebus.messaging.sessionlocklostexception)). Genel eylem: belirli toohello özel durum türü; Lütfen bölümden hello toohello tablosuna bakın. 

## <a name="exception-types"></a>Özel durum türleri
Merhaba aşağıdaki tabloda Mesajlaşma özel durum türleri ve neden olur ve notlar önerilen eylem yapabileceğiniz listeler.

| **Özel durum türü** | **Neden/açıklama/örnekleri** | **Önerilen eylem** | **Otomatik/hemen yeniden deneme sırasında unutmayın** |
| --- | --- | --- | --- |
| [TimeoutException](https://msdn.microsoft.com/library/system.timeoutexception.aspx) |Merhaba sunucu istenen toohello yanıt vermedi işlem hello içinde belirtilen denetlenen zaman [OperationTimeout](/dotnet/api/microsoft.servicebus.messaging.messagingfactorysettings#Microsoft_ServiceBus_Messaging_MessagingFactorySettings_OperationTimeout). Merhaba sunucu tamamlanmış hello işlemi istendi. Bu toonetwork veya diğer altyapı gecikmeler gerçekleşebilir. |Tutarlılık Hello sistem durumunu denetleyin ve gerekiyorsa yeniden deneyin. Bkz: [zaman aşımı özel durumları](#timeoutexception). |Yeniden deneme bazı durumlarda yardımcı olabilir; yeniden deneme mantığı toocode ekleyin. |
| [InvalidOperationException](https://msdn.microsoft.com/library/system.invalidoperationexception.aspx) |Merhaba, kullanıcı işlemi hello sunucu veya hizmet içinde izin verilmiyor istedi. Merhaba özel durum iletisi Ayrıntılar için bkz. Örneğin, [tam](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete) hello iletisi alındı bu özel durum oluşturur [ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode) modu. |Hello kodu ve hello belgelerine bakın. İşlemi geçerli Hello istenen emin olun. |Yeniden deneme yardımcı olmayacaktır. |
| [OperationCanceledException](https://msdn.microsoft.com/library/system.operationcanceledexception.aspx) |Bir deneme tooinvoke zaten kapatılmış, durduruldu veya atılmış bir nesne üzerinde bir işlemi yapılan. Nadir durumlarda hello ortam işlem zaten atıldı. |Merhaba kodu kontrol edip bırakılmış bir nesne üzerinde işlem çağrılmaz emin olun. |Yeniden deneme yardımcı olmayacaktır. |
| [UnauthorizedAccessException](https://msdn.microsoft.com/library/system.unauthorizedaccessexception.aspx) |Merhaba [TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider) nesne bir belirteç alınamadı, hello belirteç geçersiz veya hello belirteci hello talep gerekli tooperform hello işlemi içermiyor. |Merhaba belirteç sağlayıcısı hello doğru değerlerle oluşturulduğundan emin olun. Merhaba erişim denetimi hizmeti Hello yapılandırmasını denetleyin. |Yeniden deneme bazı durumlarda yardımcı olabilir; yeniden deneme mantığı toocode ekleyin. |
| [ArgumentException](https://msdn.microsoft.com/library/system.argumentexception.aspx)<br /> [ArgumentNullException](https://msdn.microsoft.com/library/system.argumentnullexception.aspx)<br />[ArgumentOutOfRangeException](https://msdn.microsoft.com/library/system.argumentoutofrangeexception.aspx) |Bir veya daha fazla sağlanan bağımsız değişkenler toohello yöntemi geçersiz.<br /> Merhaba URI çok sağlanan[NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) veya [oluşturma](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_Create_System_Collections_Generic_IEnumerable_System_Uri__) yolu segment(s) içerir.<br /> Merhaba URI şeması sağlanan çok[NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) veya [oluşturma](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_Create_System_Collections_Generic_IEnumerable_System_Uri__) geçersiz. <br />Başlangıç özellik değeri, 32 KB'den büyük. |Merhaba çağıran kodu kontrol edip hello bağımsız değişken doğru olduğundan emin olun. |Yeniden deneme yardımcı olmayacaktır. |
| [MessagingEntityNotFoundException](/dotnet/api/microsoft.servicebus.messaging.messagingentitynotfoundexception) |Merhaba işlemle ilişkili varlık yok veya silinmiş olabilir. |Merhaba varlık var olduğundan emin olun. |Yeniden deneme yardımcı olmayacaktır. |
| [MessageNotFoundException](/dotnet/api/microsoft.servicebus.messaging.messagenotfoundexception) |Tooreceive bir ileti belirli sıra numarası ile çalışır. Bu ileti bulunamadı. |Merhaba ileti zaten alınmadı emin olun. Selamlama iletisine deadlettered yüklediyse hello sahipsiz sıra toosee denetleyin. |Yeniden deneme yardımcı olmayacaktır. |
| [MessagingCommunicationException](/dotnet/api/microsoft.servicebus.messaging.messagingcommunicationexception) |İstemci mümkün tooestablish bağlantı tooService veri yolu değil. |Sağlanan hello ana bilgisayar adının doğru olduğundan ve hello konağa erişilebildiğinden emin olun. |Aralıklı bağlantısı sorunları varsa, yeniden deneme yardımcı olabilir. |
| [ServerBusyException](/dotnet/api/microsoft.servicebus.messaging.serverbusyexception) |Hizmet mümkün tooprocess hello isteği şu anda değil. |İstemci bir süre bekleyin sonra hello işlemi yeniden deneyin. |İstemci, belirli bir zaman aralığından sonra yeniden deneyebilir. Farklı bir özel durumla bir yeniden deneme sonuçlanırsa, bu özel durum yeniden deneme davranışını denetleyin. |
| [MessageLockLostException](/dotnet/api/microsoft.servicebus.messaging.messagelocklostexception) |Merhaba ileti ile ilişkili kilit belirtecinin süresi doldu veya hello kilit belirteci bulunamadı. |Selamlama iletisine siler. |Yeniden deneme yardımcı olmayacaktır. |
| [SessionLockLostException](/dotnet/api/microsoft.servicebus.messaging.sessionlocklostexception) |Bu oturumla ilişkili kilit kaybolur. |Merhaba abort [MessageSession](/dotnet/api/microsoft.servicebus.messaging.messagesession) nesnesi. |Yeniden deneme yardımcı olmayacaktır. |
| [MessagingException](/dotnet/api/microsoft.servicebus.messaging.messagingexception) |Genel durumlarda aşağıdaki hello oluşturulan özel durum iletileri:<br /> Girişimde toocreate bir [QueueClient](/dotnet/api/microsoft.servicebus.messaging.queueclient) bir ad veya tooa farklı varlık türü (örneğin, bir konu) ait yolu kullanarak.<br />  Bir deneme toosend bir ileti 256 KB'den büyük yapılan. Merhaba sunucusu veya hizmeti hello isteğin işlenmesi sırasında bir hatayla karşılaştı. Merhaba özel durum iletisi ayrıntıları için lütfen bkz. Bu genellikle geçici bir istisnadır. |Merhaba kodunu kontrol edin ve yalnızca serileştirilebilir nesneler hello ileti gövdesi için kullanıldığından emin olun (veya özel bir seri hale getirici kullanın). Merhaba özelliklerinin desteklenen hello değer türleri ve yalnızca desteklenen kullanım türleri için Hello belgelerine bakın. Merhaba denetleyin [IsTransient](/dotnet/api/microsoft.servicebus.messaging.messagingexception#Microsoft_ServiceBus_Messaging_MessagingException_IsTransient) özelliği. Eğer öyleyse **doğru**, hello işlemi yeniden deneyin. |Yeniden deneme davranışı tanımlanmamış ve yardımcı. |
| [MessagingEntityAlreadyExistsException](/dotnet/api/microsoft.servicebus.messaging.messagingentityalreadyexistsexception) |Bu hizmet ad alanı içinde başka bir varlık tarafından kullanılan bir ada sahip bir varlık toocreate deneyin. |Merhaba varolan varlık silin veya oluşturulan hello varlık toobe için farklı bir ad seçin. |Yeniden deneme yardımcı olmayacaktır. |
| [QuotaExceededException](/dotnet/api/microsoft.servicebus.messaging.quotaexceededexception) |Varlık Mesajlaşma hello izin verilen boyut üst sınırına ulaştı veya bağlantıları tooa ad alanı hello sayısı aşıldı. |Alanı hello varlık hello varlıktan alıcı iletileri veya onun alt sıraları oluşturun. Bkz: [QuotaExceededException](#quotaexceededexception). |İletileri hello sırada kaldırılmışsa yeniden deneme yardımcı olabilir. |
| [RuleActionException](/dotnet/api/microsoft.servicebus.messaging.ruleactionexception) |Hizmet veri yolu toocreate geçersiz kural eylemi çalışırsanız, bu özel durum döndürür. Merhaba kural eylemi, iletinin işlenirken bir hata oluşursa, Service Bus bu özel durum tooa deadlettered iletisi ekler. |Merhaba kural eylemi doğruluğunu denetleyin. |Yeniden deneme yardımcı olmayacaktır. |
| [FilterException](/dotnet/api/microsoft.servicebus.messaging.filterexception) |Hizmet veri yolu toocreate geçersiz bir filtre çalışırsanız, bu özel durumun döndürür. Bu ileti için hello filtre işlenirken bir hata oluştu, Service Bus bu özel durum tooa deadlettered iletisi ekler. |Merhaba filtre doğruluğunu denetleyin. |Yeniden deneme yardımcı olmayacaktır. |
| [SessionCannotBeLockedException](/dotnet/api/microsoft.servicebus.messaging.sessioncannotbelockedexception) |Belirli bir oturum kimliği ile bir oturumu ancak hello oturum başka bir istemci tarafından şu anda kilitli tooaccept deneyin. |Diğer istemciler tarafından Hello oturum kilidi emin olun. |Merhaba oturum hello geçici serbest yeniden deneme yardımcı olabilir. |
| [TransactionSizeExceededException](/dotnet/api/microsoft.servicebus.messaging.transactionsizeexceededexception) |Çok fazla operations hello işlem bir parçasıdır. |Bu işlemin bir parçası olan işlemleri Hello sayısını azaltın. |Yeniden deneme yardımcı olmayacaktır. |
| [MessagingEntityDisabledException](/dotnet/api/microsoft.servicebus.messaging.messagingentitydisabledexception) |Devre dışı bırakılmış bir varlığı üzerinde bir çalışma zamanı işlemi isteği. |Merhaba varlık etkinleştirin. |Merhaba varlık hello geçici etkinleştirdiyseniz yeniden deneme yardımcı olabilir. |
| [NoMatchingSubscriptionException](/dotnet/api/microsoft.servicebus.messaging.nomatchingsubscriptionexception) |Önceden filtreleme etkin olduğundan ve hello filtreleri hiçbiri eşleşen bir ileti tooa konu gönderirseniz, Service Bus bu özel durumun döndürür. |En az bir filtre eşleştiğinden emin olun. |Yeniden deneme yardımcı olmayacaktır. |
| [MessageSizeExceededException](/dotnet/api/microsoft.servicebus.messaging.messagesizeexceededexception) |İleti yükünü hello 256 KB sınırını aşıyor. Sistem özellikleri ve tüm .NET ek yükü içerebilir hello toplam ileti boyutu, bu hello 256 KB sınıra olduğuna dikkat edin. |Merhaba ileti yükü Hello boyutunu hello işlemi yeniden deneyin. |Yeniden deneme yardımcı olmayacaktır. |
| [TransactionException](https://msdn.microsoft.com/library/system.transactions.transactionexception.aspx) |Merhaba ortam işlem (*Transaction.Current*) geçersiz. Tamamlanan veya iptal. İç özel duruma ek bilgi sağlayabilir. | |Yeniden deneme yardımcı olmayacaktır. |
| [Transactionındoubtexception](https://msdn.microsoft.com/library/system.transactions.transactionindoubtexception.aspx) |Bir işlem, şüpheli bir işlem denendi veya girişimde toocommit hello işlem ve şüpheli hello işlem olur. |Merhaba işlem zaten önem silinmiş gibi uygulamanız (bir özel durum olarak), bu özel durumun işlemelidir. |- |

## <a name="quotaexceededexception"></a>QuotaExceededException
[QuotaExceededException](/dotnet/api/microsoft.servicebus.messaging.quotaexceededexception) belirli bir varlık için bir kota aşıldı gösterir.

### <a name="queues-and-topics"></a>Kuyruklar ve konu başlıkları
Kuyruklar ve konular için bu genellikle hello hello sırasının boyutudur. Merhaba hata iletisi özelliği aşağıdaki örneğine hello olduğu gibi daha ayrıntılı bilgi içerir:

```
Microsoft.ServiceBus.Messaging.QuotaExceededException
Message: hello maximum entity size has been reached or exceeded for Topic: ‘xxx-xxx-xxx’. 
    Size of entity in bytes:1073742326, Max entity size in bytes:
1073741824..TrackingId:xxxxxxxxxxxxxxxxxxxxxxxxxx, TimeStamp:3/15/2013 7:50:18 AM
```

Selamlama iletisine durumları, bu hello konu, bu örnek 1 GB (Merhaba varsayılan boyut sınırı) boyut sınırını aştı. 

### <a name="namespaces"></a>ad alanları

Ad alanları için [QuotaExceededException](/dotnet/api/microsoft.servicebus.messaging.quotaexceededexception) bir uygulama bağlantıları tooa ad alanı hello sayısını aştı belirtebilirsiniz. Örneğin:

```
Microsoft.ServiceBus.Messaging.QuotaExceededException: ConnectionsQuotaExceeded for namespace xxx.
<tracking-id-guid>_G12 ---> 
System.ServiceModel.FaultException`1[System.ServiceModel.ExceptionDetail]: 
ConnectionsQuotaExceeded for namespace xxx.
```

#### <a name="common-causes"></a>Olası nedenler
Bu hatanın ortak nedenleri vardır: sahipsiz sırayı ve ileti alıcıları çalışmayan hello.

1. **Sahipsiz sıra** bir okuyucu toocomplete iletileri başarısız oluyor ve hello kilitleme sona erdiğinde Merhaba iletileri toohello sıra/konu döndürülür. Merhaba okuyucu gelen arama engelleyen bir özel durum karşılaşırsa gerçekleşebilir [BrokeredMessage.Complete](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.brokeredmessage.complete.aspx). Bir ileti 10 kez okuduktan sonra varsayılan olarak toohello sahipsiz sırayı taşır. Bu davranış hello tarafından denetlenen [QueueDescription.MaxDeliveryCount](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.queuedescription.maxdeliverycount.aspx) özelliği ve varsayılan değer 10 sahiptir. Merhaba sahipsiz sıraya ileti üst üste yığmak gibi bunlar yer kaplar.
   
    tooresolve hello sorun, siz hello sahipsiz sırasından okuma ve tam hello ileti başka bir sıradan olacaktır. Merhaba [QueueClient](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.queueclient.aspx) sınıfı bile içeren bir [FormatDeadLetterPath](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.queueclient.formatdeadletterpath.aspx) yöntemi toohelp biçiminde hello sahipsiz sırayı yolu.
2. **Alıcı durduruldu** bir alıcı bir kuyruk veya abonelik iletileri alma durduruldu. yol tooidentify hello hello adresindeki toolook budur [QueueDescription.MessageCountDetails](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.queuedescription.messagecountdetails.aspx) hello tam Merhaba iletileri dökümünü gösterir özelliği. Merhaba, [ActiveMessageCount](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.messagecountdetails.activemessagecount.aspx) özelliği yüksek veya artan sonra Merhaba iletileri yazılmakta kadar hızlı okunamıyor.

### <a name="event-hubs"></a>Event Hubs
Event Hubs olay hub'ı başına 20 tüketici grupları sınırı vardır. Daha fazla toocreate çalıştığınızda aldığınız bir [QuotaExceededException](/dotnet/api/microsoft.servicebus.messaging.quotaexceededexception). 

## <a name="timeoutexception"></a>TimeoutException
A [TimeoutException](https://msdn.microsoft.com/library/system.timeoutexception.aspx) bir kullanıcı tarafından başlatılan işlem hello işlemi zaman aşımından daha uzun sürüyor gösterir. 

Merhaba hello değerini denetlemelisiniz [ServicePointManager.DefaultConnectionLimit](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit) bu sınırı basarsa olarak özelliği, ayrıca neden olabilecek bir [TimeoutException](https://msdn.microsoft.com/library/system.timeoutexception.aspx).

### <a name="queues-and-topics"></a>Kuyruklar ve konu başlıkları
Kuyruklar ve konu başlıkları için hello zaman aşımı belirtilen ya da hello [MessagingFactorySettings.OperationTimeout](/dotnet/api/microsoft.servicebus.messaging.messagingfactorysettings#Microsoft_ServiceBus_Messaging_MessagingFactorySettings_OperationTimeout) parçası olarak hello bağlantı dizesi veya aracılığıyla özelliği [ServiceBusConnectionStringBuilder](/dotnet/api/microsoft.servicebus.servicebusconnectionstringbuilder). Merhaba hata iletisi kendisini değişebilir ancak her zaman hello geçerli işlem için belirtilen hello zaman aşımı değeri içeriyor. 

### <a name="event-hubs"></a>Event Hubs
Olay hub'larına hello zaman aşımı parçası olarak hello bağlantı dizesi veya aracılığıyla belirtilen [ServiceBusConnectionStringBuilder](/dotnet/api/microsoft.servicebus.servicebusconnectionstringbuilder). Merhaba hata iletisi kendisini değişebilir ancak her zaman hello geçerli işlem için belirtilen hello zaman aşımı değeri içeriyor. 

### <a name="common-causes"></a>Olası nedenler
Bu hatanın ortak nedenleri vardır: yanlış yapılandırma ya da geçici hizmet hatası.

1. **Yanlış yapılandırma** hello işlem zaman aşımı hello işletimsel koşul için çok küçük olabilir. Merhaba hello hello istemci SDK işlemi zaman aşımı için varsayılan değer 60 saniyedir. Kodunuzu başlangıç değeri varsa toosee toosomething çok küçük ayarlayıp denetleyin. Bu hello koşulu hello ağın unutmayın ve CPU kullanımı hello işlem zaman aşımı tooa çok düşük bir değere ayarlanmamalıdır şekilde belirli işlemi toocomplete için hello süresini etkileyebilir.
2. **Geçici hizmet hatası** bazen hello Service Bus hizmetini gecikmeler istekleri işlemeyi; Örneğin, yüksek trafiği dönemlerinde deneyimi. Merhaba işlemi başarılı olana kadar bu gibi durumlarda bir gecikmeden sonra işlemi yeniden deneyebilir. Merhaba aynı işlemi hala birden çok denemeden sonra başarısız olursa, Lütfen başlangıç adresini ziyaret edin [Azure hizmet durumu site](https://azure.microsoft.com/status/) bilinen bir hizmet kesintileri varsa toosee.

## <a name="next-steps"></a>Sonraki adımlar

Merhaba Hello tam Service Bus .NET API başvuru için bkz: [Azure .NET API Başvurusu](/dotnet/api/overview/azure/servicebus).

toolearn hakkında daha fazla [Service Bus](https://azure.microsoft.com/services/service-bus/), aşağıdaki konularda hello bakın.

* [Service Bus mesajlaşma hizmetine genel bakış](service-bus-messaging-overview.md)
* [Service Bus ile ilgili temel bilgiler](service-bus-fundamentals-hybrid-solutions.md)
* [Service Bus mimarisi](service-bus-architecture.md)

