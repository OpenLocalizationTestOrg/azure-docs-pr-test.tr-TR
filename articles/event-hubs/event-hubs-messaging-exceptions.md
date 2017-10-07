---
title: "özel durumlar Mesajlaşma aaaAzure Event Hubs | Microsoft Docs"
description: "Azure Event Hubs özel durumlar ve önerilen eylemler ileti listesi."
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 2c6273de-0106-47e5-b45d-59040e51f2c5
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: 9c164e76612c26607219f08407f689aaab4050a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-messaging-exceptions"></a>Event Hubs mesajlaşma özel durumları
Bu makalede Azure hizmet veri yolu hello tarafından oluşturulan hello özel durumlar bazıları listelenmiştir iletileşme API'ları, ama olay hub'ları içerir. Bu başvuru konusu toochange, bu nedenle geri Güncelleştirmeleri denetle.

## <a name="exception-categories"></a>Özel durum kategorileri
Merhaba ilişkili eylemi birlikte tootry toofix alabilir, Hello olay hub'ları API'ler oluşturur kategorileri aşağıdaki hello dönebilir özel durumlar bunları.

1. Kullanıcı kodlama hatası: [System.ArgumentException](https://msdn.microsoft.com/library/system.argumentexception.aspx), [System.InvalidOperationException](https://msdn.microsoft.com/library/system.invalidoperationexception.aspx), [System.OperationCanceledException](https://msdn.microsoft.com/library/system.operationcanceledexception.aspx), [System.Runtime.Serialization.SerializationException](https://msdn.microsoft.com/library/system.runtime.serialization.serializationexception.aspx). Genel eylem: toofix hello kod devam etmeden önce deneyin.
2. Kurulum/yapılandırma hatası: [Microsoft.ServiceBus.Messaging.MessagingEntityNotFoundException](/dotnet/api/microsoft.servicebus.messaging.messagingentitynotfoundexception), [Microsoft.Azure.EventHubs.MessagingEntityNotFoundException](/dotnet/api/microsoft.azure.eventhubs.messagingentitynotfoundexception), [System.UnauthorizedAccessException](https://msdn.microsoft.com/library/system.unauthorizedaccessexception.aspx). Genel eylem: yapılandırmanızı inceleyin ve gerekirse değiştirin.
3. Geçici özel durumlar: [Microsoft.ServiceBus.Messaging.MessagingException](/dotnet/api/microsoft.servicebus.messaging.messagingexception), [Microsoft.ServiceBus.Messaging.ServerBusyException](#serverbusyexception), [Microsoft.Azure.EventHubs.ServerBusyException](#serverbusyexception), [Microsoft.ServiceBus.Messaging.MessagingCommunicationException](/dotnet/api/microsoft.servicebus.messaging.messagingcommunicationexception). Genel eylem: hello işlemi yeniden deneyin veya kullanıcılara bildirin.
4. Diğer özel durumlar: [System.Transactions.TransactionException](https://msdn.microsoft.com/library/system.transactions.transactionexception.aspx), [System.TimeoutException](#timeoutexception), [Microsoft.ServiceBus.Messaging.MessageLockLostException](/dotnet/api/microsoft.servicebus.messaging.messagelocklostexception), [Microsoft.ServiceBus.Messaging.SessionLockLostException](/dotnet/api/microsoft.servicebus.messaging.sessionlocklostexception). Genel eylem: belirli toohello özel durum türü; Lütfen bölümden hello toohello tablosuna bakın. 

## <a name="exception-types"></a>Özel durum türleri
Merhaba aşağıdaki tabloda Mesajlaşma özel durum türleri ve neden olur ve notlar önerilen eylem yapabileceğiniz listeler.

| **Özel durum türü** | **Neden/açıklama/örnekleri** | **Önerilen eylem** | **Otomatik/hemen yeniden deneme sırasında unutmayın** |
| --- | --- | --- | --- |
| [TimeoutException](https://msdn.microsoft.com/library/system.timeoutexception.aspx) |Merhaba sunucu istenen toohello yanıt vermedi işlem hello içinde belirtilen tarafından denetlenen zaman [OperationTimeout](/dotnet/api/microsoft.servicebus.messaging.messagingfactorysettings#Microsoft_ServiceBus_Messaging_MessagingFactorySettings_OperationTimeout). Merhaba sunucu tamamlanmış hello işlemi istendi. Bu toonetwork veya diğer altyapı gecikmeler gerçekleşebilir. |Tutarlılık Hello sistem durumunu denetleyin ve gerekiyorsa yeniden deneyin.<br /> Bkz: [TimeoutException](#timeoutexception). |Yeniden deneme bazı durumlarda yardımcı olabilir; yeniden deneme mantığı toocode ekleyin. |
| [InvalidOperationException](https://msdn.microsoft.com/library/system.invalidoperationexception.aspx) |Merhaba, kullanıcı işlemi hello sunucu veya hizmet içinde izin verilmiyor istedi. Merhaba özel durum iletisi Ayrıntılar için bkz. Örneğin, [tam](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete) hello iletisi alındı bu özel durum oluşturur [ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode) modu. |Hello kodu ve hello belgelerine bakın. İşlemi geçerli Hello istenen emin olun. |Yeniden deneme yardımcı olmayacaktır. |
| [OperationCanceledException](https://msdn.microsoft.com/library/system.operationcanceledexception.aspx) |Bir deneme tooinvoke zaten kapatılmış, durduruldu veya atılmış bir nesne üzerinde bir işlemi yapılan. Nadir durumlarda hello ortam işlem zaten atıldı. |Merhaba kodu kontrol edip bırakılmış bir nesne üzerinde işlem çağrılmaz emin olun. |Yeniden deneme yardımcı olmayacaktır. |
| [UnauthorizedAccessException](https://msdn.microsoft.com/library/system.unauthorizedaccessexception.aspx) |Merhaba [TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider) nesne bir belirteç alınamadı, hello belirteç geçersiz veya hello belirteci hello talep gerekli tooperform hello işlemi içermiyor. |Merhaba belirteç sağlayıcısı hello doğru değerlerle oluşturulduğundan emin olun. Merhaba erişim denetimi hizmeti Hello yapılandırmasını denetleyin. |Yeniden deneme bazı durumlarda yardımcı olabilir; yeniden deneme mantığı toocode ekleyin. |
| [ArgumentException](https://msdn.microsoft.com/library/system.argumentexception.aspx)<br /> [ArgumentNullException](https://msdn.microsoft.com/library/system.argumentnullexception.aspx)<br />[ArgumentOutOfRangeException](https://msdn.microsoft.com/library/system.argumentoutofrangeexception.aspx) |Bir veya daha fazla sağlanan bağımsız değişkenler toohello yöntemi geçersiz. Merhaba URI çok sağlanan[NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) veya [oluşturma](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_Create_System_Collections_Generic_IEnumerable_System_Uri__) yolu segment(s) içerir. Merhaba URI şeması sağlanan çok[NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) veya [oluşturma](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_Create_System_Collections_Generic_IEnumerable_System_Uri__) geçersiz. Başlangıç özellik değeri, 32 KB'den büyük. |Merhaba çağıran kodu kontrol edip hello bağımsız değişken doğru olduğundan emin olun. |Yeniden deneme yardımcı olmayacaktır. |
| [Microsoft.ServiceBus.Messaging.MessagingEntityNotFoundException](/dotnet/api/microsoft.servicebus.messaging.messagingentitynotfoundexception) <br /> [Microsoft.Azure.EventHubs.MessagingEntityNotFoundException](/dotnet/api/microsoft.azure.eventhubs.messagingentitynotfoundexception) |Merhaba işlemle ilişkili varlık yok veya silinmiş olabilir. |Merhaba varlık var olduğundan emin olun. |Yeniden deneme yardımcı olmayacaktır. |
| [MessageNotFoundException](/dotnet/api/microsoft.servicebus.messaging.messagenotfoundexception) |Tooreceive bir ileti belirli sıra numarası ile çalışır. Bu ileti bulunamadı. |Merhaba ileti zaten alınmadı emin olun. Selamlama iletisine deadlettered yüklediyse hello sahipsiz sıra toosee denetleyin. |Yeniden deneme yardımcı olmayacaktır. |
| [MessagingCommunicationException](/dotnet/api/microsoft.servicebus.messaging.messagingcommunicationexception) |İstemci mümkün tooestablish bağlantı tooEvent Hub değil. |Sağlanan hello ana bilgisayar adının doğru olduğundan ve hello konağa erişilebildiğinden emin olun. |Aralıklı bağlantısı sorunları varsa, yeniden deneme yardımcı olabilir. |
| [Microsoft.ServiceBus.Messaging.ServerBusyException](/dotnet/api/microsoft.servicebus.messaging.serverbusyexception) <br /> [Microsoft.Azure.EventHubs.ServerBusyException](/dotnet/api/microsoft.azure.eventhubs.serverbusyexception) |Hizmet mümkün tooprocess hello isteği şu anda değil. |İstemci bir süre bekleyin sonra hello işlemi yeniden deneyin. <br /> Bkz: [ServerBusyException](#serverbusyexception). |İstemci, belirli bir zaman aralığından sonra yeniden deneyebilir. Farklı bir özel durumla bir yeniden deneme sonuçlanırsa, bu özel durum yeniden deneme davranışını denetleyin. |
| [MessageLockLostException](/dotnet/api/microsoft.servicebus.messaging.messagelocklostexception) |Merhaba ileti ile ilişkili kilit belirtecinin süresi doldu veya hello kilit belirteci bulunamadı. |Selamlama iletisine siler. |Yeniden deneme yardımcı olmayacaktır. |
| [SessionLockLostException](/dotnet/api/microsoft.servicebus.messaging.sessionlocklostexception) |Bu oturumla ilişkili kilit kaybolur. | Merhaba abort [MessageSession](/dotnet/api/microsoft.servicebus.messaging.messagesession) nesnesi. |Yeniden deneme yardımcı olmayacaktır. |
| [MessagingException](/dotnet/api/microsoft.servicebus.messaging.messagingexception) |Aşağıdaki durumlarda hello oluşturulan özel durum ileti genel: girişimde toocreate bir [QueueClient](/dotnet/api/microsoft.servicebus.messaging.queueclient) bir ad veya tooa farklı varlık türü (örneğin, bir konu) ait yolu kullanarak. Bir deneme toosend bir ileti 256 KB'den büyük yapılan. Merhaba sunucusu veya hizmeti hello isteğin işlenmesi sırasında bir hatayla karşılaştı. Merhaba özel durum iletisi ayrıntıları için lütfen bkz. Bu genellikle geçici bir istisnadır. |Merhaba kodunu kontrol edin ve yalnızca serileştirilebilir nesneler hello ileti gövdesi için kullanıldığından emin olun (veya özel bir seri hale getirici kullanın). Merhaba özelliklerinin desteklenen hello değer türleri ve yalnızca desteklenen kullanım türleri için Hello belgelerine bakın. Merhaba denetleyin [IsTransient](/dotnet/api/microsoft.servicebus.messaging.messagingexception#Microsoft_ServiceBus_Messaging_MessagingException_IsTransient) özelliği. Eğer öyleyse **doğru**, hello işlemi yeniden deneyin. |Yeniden deneme davranışı tanımlanmamış ve yardımcı. |
| [MessagingEntityAlreadyExistsException](/dotnet/api/microsoft.servicebus.messaging.messagingentityalreadyexistsexception) |Bu hizmet ad alanı içinde başka bir varlık tarafından kullanılan bir ada sahip bir varlık toocreate deneyin. |Merhaba varolan varlık silin veya oluşturulan hello varlık toobe için farklı bir ad seçin. |Yeniden deneme yardımcı olmayacaktır. |
| [QuotaExceededException](/dotnet/api/microsoft.servicebus.messaging.quotaexceededexception) |Varlık Mesajlaşma hello izin verilen boyut üst sınırına ulaştı. (5'tir) hello maksimum sayısı alıcılar bir tüketici başına grubu düzeyinde açılan bu durum meydana gelebilir. |Alanı hello varlık hello varlıktan alıcı iletileri veya onun alt sıraları oluşturun. <br /> Bkz: [QuotaExceededException](#quotaexceededexception) |İletileri hello sırada kaldırılmışsa yeniden deneme yardımcı olabilir. |
|  | | | |
| [SessionCannotBeLockedException](/dotnet/api/microsoft.servicebus.messaging.sessioncannotbelockedexception) |Belirli bir oturum kimliği ile bir oturumu ancak hello oturum başka bir istemci tarafından şu anda kilitli tooaccept deneyin. |Diğer istemciler tarafından Hello oturum kilidi emin olun. |Merhaba oturum hello geçici serbest yeniden deneme yardımcı olabilir. |
| [TransactionSizeExceededException](/dotnet/api/microsoft.servicebus.messaging.transactionsizeexceededexception) |Çok fazla operations hello işlem bir parçasıdır. |Bu işlemin bir parçası olan işlemleri Hello sayısını azaltın. |Yeniden deneme yardımcı olmayacaktır. |
| [MessagingEntityDisabledException](/dotnet/api/microsoft.servicebus.messaging.messagingentitydisabledexception) |Devre dışı bırakılmış bir varlığı üzerinde bir çalışma zamanı işlemi isteği. |Merhaba varlık etkinleştirin. |Merhaba varlık hello geçici etkinleştirdiyseniz yeniden deneme yardımcı olabilir. |
| [Microsoft.ServiceBus.Messaging.MessageSizeExceededException](/dotnet/api/microsoft.servicebus.messaging.messagesizeexceededexception) <br /> [Microsoft.Azure.EventHubs.MessageSizeExceededException](/dotnet/api/microsoft.azure.eventhubs.messagesizeexceededexception) | İleti yükünü hello 256 K sınırını aşıyor. Sistem özellikleri ve tüm .NET ek yükü içerebilir hello toplam ileti boyutu, bu hello 256 k sınırı olduğuna dikkat edin. |Merhaba ileti yükü Hello boyutunu hello işlemi yeniden deneyin. |Yeniden deneme yardımcı olmayacaktır. |
| [TransactionException](https://msdn.microsoft.com/library/system.transactions.transactionexception.aspx) |Merhaba ortam işlem (*Transaction.Current*) geçersiz. Tamamlanan veya iptal. İç özel duruma ek bilgi sağlayabilir. | |Yeniden deneme yardımcı olmayacaktır. |
| [Transactionındoubtexception](https://msdn.microsoft.com/library/system.transactions.transactionindoubtexception.aspx) |Bir işlem, şüpheli bir işlem denendi veya girişimde toocommit hello işlem ve şüpheli hello işlem olur. |Merhaba işlem zaten önem silinmiş gibi uygulamanız (bir özel durum olarak), bu özel durumun işlemelidir. |- |

## <a name="quotaexceededexception"></a>QuotaExceededException
[QuotaExceededException](/dotnet/api/microsoft.servicebus.messaging.quotaexceededexception) belirli bir varlık için bir kota aşıldı gösterir.

Alıcıları (5) Hello sayısının bir tüketici başına grubu düzeyinde açılan bu durum meydana gelebilir.

### <a name="event-hubs"></a>Event Hubs
Event Hubs olay hub'ı başına 20 tüketici grupları sınırı vardır. Daha fazla toocreate çalıştığınızda aldığınız bir [QuotaExceededException](/dotnet/api/microsoft.servicebus.messaging.quotaexceededexception). 

## <a name="timeoutexception"></a>TimeoutException
A [TimeoutException](https://msdn.microsoft.com/library/system.timeoutexception.aspx) bir kullanıcı tarafından başlatılan işlem hello işlemi zaman aşımından daha uzun sürüyor gösterir. 

Olay hub'larına hello zaman aşımı parçası olarak hello bağlantı dizesi veya aracılığıyla belirtilen [ServiceBusConnectionStringBuilder](/dotnet/api/microsoft.servicebus.servicebusconnectionstringbuilder). Merhaba hata iletisi kendisini değişebilir ancak her zaman hello geçerli işlem için belirtilen hello zaman aşımı değeri içeriyor. 

### <a name="common-causes"></a>Olası nedenler
Bu hatanın ortak nedenleri vardır: yanlış yapılandırma ya da geçici hizmet hatası.

1. **Yanlış yapılandırma** hello işlem zaman aşımı hello işletimsel koşul için çok küçük olabilir. Merhaba hello hello istemci SDK işlemi zaman aşımı için varsayılan değer 60 saniyedir. Kodunuzu başlangıç değeri varsa toosee toosomething çok küçük ayarlayıp denetleyin. Bu hello koşulu hello ağın unutmayın ve CPU kullanımı hello işlem zaman aşımı tooa çok düşük bir değere ayarlanmamalıdır şekilde belirli işlemi toocomplete için hello süresini etkileyebilir.
2. **Geçici hizmet hatası** bazen hello Event Hubs hizmeti gecikmeler istekleri işlemeyi; Örneğin, yüksek trafiği dönemlerinde deneyimi. Merhaba işlemi başarılı olana kadar bu gibi durumlarda bir gecikmeden sonra işlemi yeniden deneyebilir. Merhaba aynı işlemi hala birden çok denemeden sonra başarısız olursa, Lütfen başlangıç adresini ziyaret edin [Azure hizmet durumu site](https://azure.microsoft.com/status/) bilinen bir hizmet kesintileri varsa toosee.

## <a name="serverbusyexception"></a>ServerBusyException

A [Microsoft.ServiceBus.Messaging.ServerBusyException](/dotnet/api/microsoft.servicebus.messaging.serverbusyexception) veya [Microsoft.Azure.EventHubs.ServerBusyException](/dotnet/api/microsoft.azure.eventhubs.serverbusyexception) bir sunucusu aşırı yüklendi gösterir. Bu özel durumun iki ilgili hata kodları vardır.

### <a name="error-code-50002"></a>Hata kodu 50002

Bu hata iki nedenlerden biriyle oluşabilir:

1. Merhaba yük, hello olay hub'ı ve bir bölüm isabet hello yerel işleme birimi sınırlaması tüm bölümleri arasında eşit olarak dağıtılmış değil.
    
    Çözüm: hello bölüm Dağıtım stratejisi düzeltilmesi veya çalışırken [EventHubClient.Send(eventDataWithOutPartitionKey)](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_Send_Microsoft_ServiceBus_Messaging_EventData_) yardımcı olabilir.

2. Merhaba olay hub'ları ad yeterli üretilen iş birimleri yok (Merhaba denetleyebilirsiniz **ölçümleri** olay hub'ları ad alanı dikey penceresinde hello dikey penceresinde [Azure portal](https://portal.azure.com) tooconfirm). Merhaba portal toplanmış (1 dakika) bilgileri gösterir, ancak yalnızca bir tahmin olacak şekilde size gerçek zamanlı – hello verimlilik ölçmek unutmayın.

    Çözüm: hello ad alanı birimlerde yardımcı olabilecek hello verim artar. Bunu bu hello portalında hello yapabilirsiniz **ölçek** dikey penceresinde hello olay hub'ları ad alanı dikey.

### <a name="error-code-50001"></a>Hata kodu 50001

Bu hata nadiren olmalıdır. Bu ad alanınız için bir kod çalıştırmasını hello kapsayıcı CPU üzerinde düşük – olay hub'ları fazla birkaç saniye hello önce yük dengeleyici başlar olur.


## <a name="next-steps"></a>Sonraki adımlar
Bağlantılar aşağıdaki hello ziyaret ederek Event Hubs hakkında daha fazla bilgi edinebilirsiniz:

* [Event Hubs’a genel bakış](event-hubs-what-is-event-hubs.md)
* [Olay Hub’ı oluşturma](event-hubs-create.md)
* [Event Hubs ile ilgili SSS](event-hubs-faq.md)
