---
title: "Azure Event Hubs için aaaProgramming Kılavuzu | Microsoft Docs"
description: "Hello Azure .NET SDK kullanarak Azure Event Hubs için kod yazma."
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 64cbfd3d-4a0e-4455-a90a-7f3d4f080323
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 08/17/2017
ms.author: sethm
ms.openlocfilehash: 43bebd126c2311af9e3daeb52324132b66cf0884
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-programming-guide"></a>Event Hubs programlama kılavuzu

Bu makalede Azure olay hub'ları ve hello Azure .NET SDK'sını kullanarak kod yazarken bazı genel senaryolar açıklanmaktadır. Burada Event Hubs’ın önceden bilindiği varsayılır. Olay hub'ları kavramsal bir genel bakış için bkz: Merhaba [Event Hubs'a genel bakış](event-hubs-what-is-event-hubs.md).

## <a name="event-publishers"></a>Olay yayımcıları

Olayları tooan olay hub'ı ya da HTTP POST veya bir AMQP 1.0 bağlantısı üzerinden kullanarak gönderin. Merhaba hangi toouse seçimine ve ne zaman ele alınan hello belirli senaryoya bağlıdır. AMQP 1.0 bağlantıları Service Bus içinde aracılı bağlantılar olarak ölçülür ve sıklıkla daha yüksek ileti hacimlerine ve düşük gecikme gereksinimlerine sahip senaryolar kalıcı bir mesajlaşma kanalı sağladığından bu senaryolarda daha uygundur.

Oluşturma ve olay hub'ın hello kullanarak yönetme [NamespaceManager][] sınıfı. Veri tooEvent yayımlama hello birincil Hello .NET ile yönetilen API'ler kullanılırken oluşturur hub olan hello [EventHubClient](/dotnet/api/microsoft.servicebus.messaging.eventhubclient) ve [EventData][] sınıfları. [EventHubClient][] üzerinde olayları toohello olay hub'ı gönderilir hello AMQP iletişim kanalını sağlar. Merhaba [EventData][] sınıfı bir olayı temsil eder ve kullanılan toopublish iletileri tooan olay hub'ı. Bu sınıf hello gövdesi, bazı meta verileri ve üstbilgisine hello olay hakkında bilgi içerir. Diğer özellikler toohello eklenir [EventData][] bir olay hub'ından geçtikçe nesne.

## <a name="get-started"></a>başlarken

Olay hub'ları destekleyen hello .NET sınıfları Microsoft.ServiceBus.dll bütünleştirilmiş hello sağlanır. en kolay yolu tooreference hello hizmet veri yolu API'sini ve tooconfigure hello tüm hello Service Bus bağımlılıklarıyla uygulamanızla toodownload hello olan [Service Bus NuGet paketini](https://www.nuget.org/packages/WindowsAzure.ServiceBus). Alternatif olarak, hello kullanabilirsiniz [Paket Yöneticisi Konsolu](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) Visual Studio. toodo bu nedenle, sorunu hello komutunda aşağıdaki hello [Paket Yöneticisi Konsolu](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) penceresi:

```
Install-Package WindowsAzure.ServiceBus
```

## <a name="create-an-event-hub"></a>Olay hub’ı oluşturma
Merhaba kullanabilirsiniz [NamespaceManager][] toocreate olay hub'ları sınıfı. Örneğin:

```csharp
var manager = new Microsoft.ServiceBus.NamespaceManager("mynamespace.servicebus.windows.net");
var description = manager.CreateEventHub("MyEventHub");
```

Çoğu durumda, hello kullanmanız önerilir [Createeventhubıfnotexists][] hello hizmetin yeniden başlatılması halinde özel durumlar oluşturma yöntemleri tooavoid. Örneğin:

```csharp
var description = manager.CreateEventHubIfNotExists("MyEventHub");
```

Tüm olay hub'ları oluşturma işlemleri dahil olmak üzere, [Createeventhubıfnotexists][], gerektiren **Yönet** hello ad alanı söz konusu izinleri. Yayımcı veya tüketici uygulamanızın toolimit hello izinlerinin istiyorsanız, bu önleyebilirsiniz sınırlı izinlere sahip kimlik bilgileri kullanırken üretim kodunda işlemi çağrılarından oluşturun.

Merhaba [EventHubDescription](/dotnet/api/microsoft.servicebus.messaging.eventhubdescription) sınıfı hello yetkilendirme kuralları, hello ileti elde tutma aralığı, bölüm kimlikleri, durum ve yol dahil olmak üzere bir event hub ile ilgili ayrıntılar içerir. Bu sınıf tooupdate hello meta veriler bir olay hub'ına kullanabilirsiniz.

## <a name="create-an-event-hubs-client"></a>Event Hubs istemcisi oluşturma
Event Hubs ile etkileşim için birincil sınıf hello [Microsoft.ServiceBus.Messaging.EventHubClient][EventHubClient]. Bu sınıf hem gönderen hem de alıcı özellikleri sağlar. Hello kullanarak bu sınıfın örneği [oluşturma](/dotnet/api/microsoft.servicebus.messaging.eventhubclient.create) hello aşağıdaki örnekte gösterildiği gibi yöntemi.

```csharp
var client = EventHubClient.Create(description.Path);
```

Bu yöntem hello App.config dosyasında hello hello Service Bus bağlantı bilgilerini kullanır, `appSettings` bölümü. Merhaba ilişkin bir örnek `appSettings` XML kullanılan toostore hello Service Bus bağlantı bilgilerini, hello hello belgelerine bakın [Microsoft.ServiceBus.Messaging.EventHubClient.Create(System.String)](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_Create_System_String_) yöntemi.

Bir bağlantı dizesi toocreate hello istemciden başka bir seçenektir. Hello yapılandırma özelliklerinde hello çalışan hello dize depolayabileceğiniz bu seçenek Azure çalışan rolleri kullanırken iyi çalışır. Örneğin:

```csharp
EventHubClient.CreateFromConnectionString("your_connection_string");
```

Merhaba bağlantı dizesi hello önceki yöntemler için hello App.config dosyasında göründüğü gibi aynı biçimi hello olacaktır:

```
Endpoint=sb://[namespace].servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[key]
```

Son olarak, olası toocreate de olan bir [EventHubClient][] nesnesinin bir [Eventhubclient](/dotnet/api/microsoft.servicebus.messaging.messagingfactory) hello aşağıdaki örnekte gösterildiği gibi örneği.

```csharp
var factory = MessagingFactory.CreateFromConnectionString("your_connection_string");
var client = factory.CreateEventHubClient("MyEventHub");
```

Önemli toonote ek olan [EventHubClient][] bir Mesajlaşma fabrikası örneğinden oluşturulan nesneler hello yeniden kullanacaktır aynı temel alınan TCP bağlantı. Bu nedenle, bu nesneler işlemede istemci tarafı sınırlamasına sahiptir. Merhaba [oluşturma](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_Create_System_String_) yöntemi tek bir Mesajlaşma altyapısını yeniden kullanır. Tek bir gönderenden çok yüksek işleme gerekiyorsa birden fazla ileti altyapısı ve her mesajlaşma altyapısından bir [EventHubClient][] nesnesi oluşturabilirsiniz.

## <a name="send-events-tooan-event-hub"></a>Olayları tooan olay hub'ı Gönder
Oluşturarak tooan event hub'ı olayları göndermek bir [EventData][] örneği ve hello gönderme [Gönder](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_Send_Microsoft_ServiceBus_Messaging_EventData_) yöntemi. Bu yöntem tek bir alır [EventData][] örnek parametresini ve zaman uyumlu olarak tooan olay hub'ı gönderir.

## <a name="event-serialization"></a>Olayı seri hale getirme
Merhaba [EventData][] sınıfına sahip [dört aşırı yüklü Oluşturucu](/dotnet/api/microsoft.servicebus.messaging.eventdata#constructors_) parametreleri, bir nesne ve seri hale getirici, bayt dizisi veya akış gibi çeşitli alın. Aynı zamanda olası tooinstantiate hello olan [EventData][] sınıfı ve daha sonra hello gövdesi akışına ayarlayın. JSON ile kullanırken [EventData][], kullanabileceğiniz **Encoding.UTF8.GetBytes()** tooretrieve hello bayt dizisi JSON olarak kodlanmış bir dize.

## <a name="partition-key"></a>Bölüm anahtarı
Merhaba [EventData][] sınıfına sahip bir [PartitionKey][] hello gönderen toospecify olan bir değer sağlayan özelliği karma tooproduce bir bölüm ataması. Bir bölüm anahtarının kullanılması sağlar tüm olayları ile aynı anahtarı gönderilir hello hello aynı bölüm hello event hub'ında toohello. Yaygın bölüm anahtarları kullanıcı oturum kimlikleri ve benzersiz gönderen kimlikleridir. Merhaba [PartitionKey][] özellik isteğe bağlıdır ve hello kullanılırken sağlanabilir [Microsoft.ServiceBus.Messaging.EventHubClient.Send(Microsoft.ServiceBus.Messaging.EventData)](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_Send_Microsoft_ServiceBus_Messaging_EventData_) veya [Microsoft.ServiceBus.Messaging.EventHubClient.SendAsync(Microsoft.ServiceBus.Messaging.EventData)](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_SendAsync_Microsoft_ServiceBus_Messaging_EventData_) yöntemleri. İçin bir değer belirtmezseniz, [PartitionKey][], olayları hepsini modelini kullanarak dağıtılmış toopartitions gönderilir.

### <a name="availability-considerations"></a>Kullanılabilirlik konusunda dikkat edilmesi gerekenler

Bir bölüm anahtarının kullanılması isteğe bağlıdır ve dikkatle düşünmelisiniz desteklemediğini toouse biri. Olay sıralama önemliyse, çoğu durumda, bir bölüm anahtarının kullanılması iyi bir seçimdir. Bölüm anahtarı kullandığınızda, bu bölümler kullanılabilirlik tek bir düğümde gerektirir ve zaman içinde kesintiler; Örneğin, düğümlerin yeniden başlatma ve düzeltme zaman işlem. Bu nedenle, bölüm kimliği ayarlamak ve bu bölümü için herhangi bir nedenle kullanılamaz duruma gelir, bu bölüm bir girişim tooaccess hello verilerde başarısız olur. Bölüm anahtarı yüksek oranda kullanılabilirlik en önemli ise belirtmeyin; Bu durumda olayları daha önce açıklanan hello hepsini modelini kullanarak toopartitions gönderilir. Bu senaryoda, kullanılabilirlik (bölüm kimliği) ve tutarlılık (olayları tooa bölüm kimliği sabitleme) arasında açık bir seçim getirirsiniz.

Başka bir göz önünde bulundurarak olayları işleme gecikme işliyor. Bazı durumlarda daha iyi toodrop veriler tootry yeniden deneyin ve daha aşağı akış işleme gecikmelere neden olabilir işlemeyle takip edin. Örneğin, onu tam olmasa bile borsa ile daha iyi toowait tam güncel verileri, ancak bir canlı sohbet ya da hello verileri hızlı bir şekilde, bunun yerine olurdu VoIP senaryo olur.

Bu kullanılabilirlik noktalar bu senaryolarda hata işleme stratejileri aşağıdaki hello birini seçebilirsiniz:

- Durdur (stop şeyler çözülene kadar olay hub'larından okuma)
- Bırakma (iletileri önemli olmayan sürükleyip bırakın)
- (Yeniden deneme hello iletileri gördüğünüz gibi uygun) yeniden deneyin
- [Sahipsiz](../service-bus-messaging/service-bus-dead-letter-queues.md) (bir sıraya veya başka bir olay hub'ı toodead hello iletileri yalnızca harf kullanımı işleyemedi)

Daha fazla bilgi ve hello dengelemeler kullanılabilirlik ve tutarlılık arasında hakkında tartışma için bkz: [kullanılabilirlik ve Event Hubs tutarlılığını](event-hubs-availability-and-consistency.md). 

## <a name="batch-event-send-operations"></a>Toplu olay gönderme işlemleri
Olayların toplu olarak gönderilmesi üretilen işi çarpıcı biçimde artırabilir. Merhaba [SendBatch](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_SendBatch_System_Collections_Generic_IEnumerable_Microsoft_ServiceBus_Messaging_EventData__) metodu bir **IEnumerable** türünde parametresi [EventData][] ve hello toplu işin tamamını atomik işlemi toohello olay hub'ı olarak gönderir.

```csharp
public void SendBatch(IEnumerable<EventData> eventDataList);
```

Tek bir toplu bir olay hello 256 KB'lik sınırını aşmamalıdır unutmayın. Ayrıca, her ileti hello toplu hello kullanır aynı yayımcı kimliği. Bu toplu hello hello gönderen tooensure hello sorumluluğunda hello en fazla olay boyutu aşmayan olur. Aşması durumunda bir istemci **Gönderme** hatası oluşturulur.

## <a name="send-asynchronously-and-send-at-scale"></a>Zaman uyumsuz olarak gönderme ve ölçekli gönderme
Olayları tooan olay hub'ı zaman uyumsuz olarak da gönderebilirsiniz. Zaman uyumsuz gönderme bir istemcinin mümkün toosend olayları olduğu hello hızı artırabilir. Her iki hello [Gönder](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_Send_Microsoft_ServiceBus_Messaging_EventData_) ve [SendBatch](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_SendBatch_System_Collections_Generic_IEnumerable_Microsoft_ServiceBus_Messaging_EventData__) yöntemleri döndüren zaman uyumsuz sürümlerde kullanılabilir bir [görev](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) nesnesi. Bu teknik üretilen işi artırabilse, hatta hello Event Hubs hizmeti tarafından kısıtlanan ve hello istemcinin hata veya kayıp iletilerle karşılaşmasına yol açabilir ancak hello istemci toocontinue toosend olayları da neden olabilir düzgün uygulanmaması durumunda. Ayrıca, hello kullanabilirsiniz [RetryPolicy](/dotnet/api/microsoft.servicebus.messaging.cliententity#Microsoft_ServiceBus_Messaging_ClientEntity_RetryPolicy) hello istemci toocontrol istemci yeniden deneme seçeneklerini özelliği.

## <a name="create-a-partition-sender"></a>Bölüm göndereni oluşturma
Bazı durumlarda en yaygın toosend olayları tooan olay hub'ı bölüm anahtarı olmayan olmasına karşın, toosend olayları isteyebilirsiniz doğrudan bölüm verilen tooa. Örneğin:

```csharp
var partitionedSender = client.CreatePartitionedSender(description.PartitionIds[0]);
```

[CreatePartitionedSender](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_CreatePartitionedSender_System_String_) döndüren bir [EventHubSender](/dotnet/api/microsoft.servicebus.messaging.eventhubsender) toopublish olayları tooa belirli olay hub'ı bölüm kullanabileceğiniz nesne.

## <a name="event-consumers"></a>Olay tüketicileri
Event Hubs olay tüketimi için iki adet birincil modele sahiptir: doğrudan alıcılar ve [EventProcessorHost][] gibi üst düzey soyutlamalar. Doğrudan alıcılar bir tüketici grubundaki erişim toopartitions kendi eşgüdümünü sorumludur.

### <a name="direct-consumer"></a>Doğrudan tüketici
Merhaba en doğrudan yolu tooread bir tüketici grubundaki bölümden olduğu toouse hello [EventHubReceiver](/dotnet/apie/microsoft.servicebus.messaging.eventhubreceiver) sınıfı. toocreate bu sınıfın örneği bir hello örneği kullanmalıdır [EventHubConsumerGroup](/dotnet/api/microsoft.servicebus.messaging.eventhubconsumergroup) sınıfı. Aşağıdaki örneğine hello hello tüketici grubu için hello alıcı oluştururken hello bölüm kimliği belirtilmelidir.

```csharp
EventHubConsumerGroup group = client.GetDefaultConsumerGroup();
var receiver = group.CreateReceiver(client.GetRuntimeInformation().PartitionIds[0]);
```

Merhaba [CreateReceiver](/dotnet/api/microsoft.servicebus.messaging.eventhubconsumergroup#methods_summary) yöntemi oluşturulmakta hello okuyucu üzerinde denetimi kolaylaştıran birkaç aşırı sahiptir. Bu yöntemler bir uzaklığı dize veya zaman damgası olarak belirtmeyi içerir ve olup tooinclude hello belirtilen bu uzaklığın döndürülen akışla aktarmak veya bundan sonra Başlat özelliği toospecify hello. Merhaba alıcıyı oluşturduktan sonra nesne döndürdü hello olayları almaya başlayabilirsiniz. Merhaba [alma](/dotnet/api/microsoft.servicebus.messaging.eventhubreceiver#methods_summary) yöntemi, bu denetim hello dört aşırı sahip toplu iş boyutu gibi işlem parametrelerini alır ve bir süre bekleyin. Bir tüketicinin bu yöntemleri tooincrease hello verimliliğini hello zaman uyumsuz sürümlerini kullanabilirsiniz. Örneğin:

```csharp
bool receive = true;
string myOffset;
while(receive)
{
    var message = receiver.Receive();
    myOffset = message.Offset;
    string body = Encoding.UTF8.GetString(message.GetBytes());
    Console.WriteLine(String.Format("Received message offset: {0} \nbody: {1}", myOffset, body));
}
```

Saygı tooa belirli bölümü ile Merhaba iletileri toohello olay hub'ı gönderildikleri hello sırayla alınır. Merhaba, bir dize belirteci kullanılan tooidentify bir bölümdeki bir iletiyi uzaklığı.

Bir tüketici grubundaki tek bir bölüm aynı anda 5'ten fazla eşzamanlı okuyucunun bağlanmasına izin vermez. Okuyucular bağlandığında veya bağlantıları kesildiğinde gibi oturumlarını hello hizmet bağlantı kesilmesini algılamasından önce birkaç dakika boyunca etkin kalabilir. Bu süre boyunca tooa bölüm bağlanılması başarısız olabilir. Event Hubs için doğrudan alıcı yazmaya tam örnek için bkz: Merhaba [Event Hubs doğrudan alıcıları](https://code.msdn.microsoft.com/Event-Hub-Direct-Receivers-13fa95c6) örnek.

### <a name="event-processor-host"></a>Olay işlemcisi konağı
Merhaba [EventProcessorHost][] sınıfı Event Hubs verilerini işler. Merhaba .NET platformu üzerinde olay okuyucuları oluştururken bu uygulamayı kullanmanız gerekir. [EventProcessorHost][] aynı zamanda denetim noktası oluşturma ve bölüm kiralama yönetimi sağlayan olay işlemcisi uygulamaları için iş parçacığı güvenli, çok işlemli, güvenli bir çalışma zamanı ortamı sağlar.

toouse hello [EventProcessorHost][] sınıfı, uygulayabilirsiniz [Ieventprocessor](/dotnet/api/microsoft.servicebus.messaging.ieventprocessor). Bu arabirim üç yöntem içerir:

* [OpenAsync](/dotnet/api/microsoft.servicebus.messaging.ieventprocessor#Microsoft_ServiceBus_Messaging_IEventProcessor_OpenAsync_Microsoft_ServiceBus_Messaging_PartitionContext_)
* [CloseAsync](/dotnet/api/microsoft.servicebus.messaging.ieventprocessor#Microsoft_ServiceBus_Messaging_IEventProcessor_CloseAsync_Microsoft_ServiceBus_Messaging_PartitionContext_Microsoft_ServiceBus_Messaging_CloseReason_)
* [ProcessEventsAsync](/dotnet/api/microsoft.servicebus.messaging.ieventprocessor#Microsoft_ServiceBus_Messaging_IEventProcessor_ProcessEventsAsync_Microsoft_ServiceBus_Messaging_PartitionContext_System_Collections_Generic_IEnumerable_Microsoft_ServiceBus_Messaging_EventData__)

toostart olay işleme, örneği [EventProcessorHost][], event hub'ınıza uygun parametreleri hello sağlama. Ardından, çağıran [Ieventprocessor](/dotnet/api/microsoft.servicebus.messaging.eventprocessorhost#Microsoft_ServiceBus_Messaging_EventProcessorHost_RegisterEventProcessorAsync__1) tooregister, [Ieventprocessor](/dotnet/api/microsoft.servicebus.messaging.ieventprocessor) uygulama hello çalışma zamanı ile. Bu noktada, hello konak tooacquire "Hızlı" algoritma kullanarak hello event hub'ındaki her bölüm üzerinde bir kira deneyecek. Bu kiralar belirli bir zaman çerçevesi boyunca sürer ve sonrasında yenilenmelidir. Yeni düğüm olarak çalışan örnekleri bu durumda, çevrimiçi olması, kiralama ayırmaları yapar ve her tooacquire daha fazla kira girişimleri olarak zaman içinde hello yük düğümler arasında kayar..

![Olay İşlemcisi Konağı](./media/event-hubs-programming-guide/IC759863.png)

Zaman içerisinde bir denge sağlanır. Bu dinamik özellik hem ölçek büyütme ve ölçek azaltma için CPU tabanlı otomatik ölçeklendirmenin uygulanan toobe tooconsumers sağlar. Olay hub'ları ileti sayısı doğrudan kavramına sahip olmadığından ortalama CPU kullanımı hello en iyi mekanizması toomeasure arka uç veya tüketici ölçeğini görülür. Yayımcılar tüketicilerin'den daha fazla olay işleyebilir toopublish başlarsa, tüketiciler üzerindeki CPU artışı hello çalışan örnek sayısı üzerinde otomatik ölçeklendirmeye kullanılan toocause olabilir.

Merhaba [EventProcessorHost][] sınıfı ayrıca bir Azure depolama tabanlı denetim noktası oluşturma mekanizması uygular. Her bir tüketici hangi hello son denetim noktasından hello önceki tüketicinin belirleyebilmesi bölüm başına temelinde uzaklığı Bu mekanizma depolarını hello oluştu. Geçiş bölümler kiralamalar aracılığıyla düğümler arasında yaptığında yük kaymasını kolaylaştıran hello eşitleme mekanizması budur.

## <a name="publisher-revocation"></a>Yayımcı iptali
Toohello çalışma zamanı özelliklerine ek olarak Gelişmiş [EventProcessorHost][], olay hub'ları yayımcı iptalini sipariş tooblock belirli yayımcıları tooan event hub'ı olay göndermesini sağlar. Bu özellikleri özellikle bir yayımcı belirteci tehlike ya da bir yazılım güncelleştirme onları toobehave açamayacağı neden yararlıdır. Bu durumlarda SAS belirtecinin bir parçası olan hello yayımcı kimliğinin olayları yayımlaması engellenebilir.

Yayımcı iptali ve toosend tooEvent hub'ları bir yayımcı olarak nasıl görürüm hakkında daha fazla bilgi için hello [olay hub'ları büyük ölçekli güvenli yayımlama](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-99ce67ab) örnek.

## <a name="next-steps"></a>Sonraki adımlar
Event Hubs senaryoları hakkında daha fazla toolearn bu bağlantıları ziyaret edin:

* [Event Hubs API’sine genel bakış](event-hubs-api-overview.md)
* [Event Hubs nedir](event-hubs-what-is-event-hubs.md)
* [Event Hubs’da kullanılabilirlik ve tutarlılık](event-hubs-availability-and-consistency.md)
* [Olay işlemcisi konağı API başvurusu](/dotnet/api/microsoft.servicebus.messaging.eventprocessorhost)

[NamespaceManager]: /dotnet/api/microsoft.servicebus.namespacemanager
[EventHubClient]: /dotnet/api/microsoft.servicebus.messaging.eventhubclient
[EventData]: /dotnet/api/microsoft.servicebus.messaging.eventdata
[Createeventhubıfnotexists]: /dotnet/api/microsoft.servicebus.namespacemanager.createeventhubifnotexists
[PartitionKey]: /dotnet/api/microsoft.servicebus.messaging.eventdata#Microsoft_ServiceBus_Messaging_EventData_PartitionKey
[EventProcessorHost]: /dotnet/api/microsoft.servicebus.messaging.eventprocessorhost
