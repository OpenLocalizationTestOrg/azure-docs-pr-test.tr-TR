---
title: "Azure Event Hubs için programlama kılavuzu | Microsoft Belgeleri"
description: "Azure .NET SDK kullanarak Azure Event Hubs için kod yazma."
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
ms.date: 11/16/2017
ms.author: sethm
ms.openlocfilehash: 7d5f14d5a65253cf0aad1811ace419bf2f39f7db
ms.sourcegitcommit: 29bac59f1d62f38740b60274cb4912816ee775ea
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/29/2017
---
# <a name="event-hubs-programming-guide"></a>Event Hubs programlama kılavuzu

Bu makalede Azure Event Hubs'a ve Azure .NET SDK'sını kullanarak kod yazarken bazı genel senaryolar açıklanmaktadır. Burada Event Hubs’ın önceden bilindiği varsayılır. Event Hubs’a kavramsal genel bakış için bkz. [Event Hubs’a genel bakış](event-hubs-what-is-event-hubs.md).

## <a name="event-publishers"></a>Olay yayımcıları

Olayları ya da HTTP POST kullanılarak bir olay hub'ına veya bir AMQP 1.0 bağlantısı üzerinden gönderir. Kullanılacak seçimi ve ne zaman ele alınan belirli senaryoya bağlıdır. AMQP 1.0 bağlantıları Service Bus içinde aracılı bağlantılar olarak ölçülür ve sıklıkla daha yüksek ileti hacimlerine ve düşük gecikme gereksinimlerine sahip senaryolar kalıcı bir mesajlaşma kanalı sağladığından bu senaryolarda daha uygundur.

Oluşturma ve olay hub'ları kullanarak yönetme [NamespaceManager][] sınıfı. .NET ile yönetilen API’ler kullanılırken Event Hubs’a veri yayımlamaya yönelik birincil yapılar [EventHubClient](/dotnet/api/microsoft.servicebus.messaging.eventhubclient) ve [EventData][] sınıflarıdır. [EventHubClient][] üzerinde olayları event hub'ına gönderildiği AMQP iletişim kanalını sağlar. [EventData][] sınıfı bir olayı temsil eder ve bir event hub'ına iletileri yayımlamak için kullanılır. Bu sınıf, olayla ilgili gövde bilgileri, bazı meta verileri ve üst bilgileri içerir. Diğer özellikler eklenir [EventData][] bir olay hub'ından geçtikçe nesne.

## <a name="get-started"></a>başlarken

Event Hubs’ı destekleyen .NET sınıfları Microsoft.ServiceBus.dll bütünleştirilmiş kodunda sağlanır. Service Bus API'sini almanın ve uygulamanızı tüm Service Bus bağımlılıklarıyla yapılandırmanın en kolay yolu [Service Bus NuGet paketi](https://www.nuget.org/packages/WindowsAzure.ServiceBus)’nin indirilmesidir. Alternatif olarak, Visual Studio’daki [Paket Yöneticisi Konsolu](http://docs.nuget.org/docs/start-here/using-the-package-manager-console)'nu kullanabilirsiniz. Bunu yapmak için [Paket Yöneticisi Konsolu](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) penceresinde aşağıdaki komutu yürütün:

```
Install-Package WindowsAzure.ServiceBus
```

## <a name="create-an-event-hub"></a>Olay hub’ı oluşturma
Event Hubs oluşturmak için [NamespaceManager][] sınıfını kullanabilirsiniz. Örneğin:

```csharp
var manager = new Microsoft.ServiceBus.NamespaceManager("mynamespace.servicebus.windows.net");
var description = manager.CreateEventHub("MyEventHub");
```

Çoğu durumda hizmetin yeniden başlatılması halinde özel durumların oluşmasını engellemek için [CreateEventHubIfNotExists][] yöntemlerini kullanmanız önerilir. Örneğin:

```csharp
var description = manager.CreateEventHubIfNotExists("MyEventHub");
```

[CreateEventHubIfNotExists][] dahil tüm Event Hubs’ı oluşturma işlemleri söz konusu ad alanında **Manage** izinlerini gerektirir. Yayımcı veya tüketici uygulamanızın izinlerini kısıtlamak istiyorsanız, sınırlı izinlere sahip kimlik bilgileri kullanırken üretim kodunda bu oluşturma işlemi çağrılarından kaçınabilirsiniz.

[EventHubDescription](/dotnet/api/microsoft.servicebus.messaging.eventhubdescription) sınıfı yetkilendirme kuralları, ileti elde tutma aralığı, bölüm kimlikleri, durum ve yol dahil olmak üzere bir event hub ile ilgili ayrıntılar içerir. Bu sınıf, bir olay hub'ındaki meta verilerini güncelleştirmek için kullanabilirsiniz.

## <a name="create-an-event-hubs-client"></a>Event Hubs istemcisi oluşturma
Event Hubs ile etkileşim kurmaya yönelik birincil sınıf [Microsoft.ServiceBus.Messaging.EventHubClient][EventHubClient]. Bu sınıf hem gönderen hem de alıcı özellikleri sağlar. Kullanarak bu sınıfın örneği [oluşturma](/dotnet/api/microsoft.servicebus.messaging.eventhubclient.create) yöntemi, aşağıdaki örnekte gösterildiği gibi:

```csharp
var client = EventHubClient.Create(description.Path);
```

Bu yöntem `appSettings` bölümündeki App.config dosyasında bulunan Service Bus bağlantı bilgilerini kullanır. Service Bus bağlantı bilgilerini depolamak için kullanılan `appSettings` XML örneği için [Microsoft.ServiceBus.Messaging.EventHubClient.Create(System.String)](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_Create_System_String_) yönteminin belgelerine bakın.

Başka bir seçenek ise istemcinin bir bağlantı dizesinden oluşturulmasıdır. Dizeyi çalışanın yapılandırma özelliklerine depolayabileceğiniz için, bu seçenek Azure çalışan rolleri kullanılarak iyi çalışır. Örneğin:

```csharp
EventHubClient.CreateFromConnectionString("your_connection_string");
```

Bağlantı dizesi önceki yöntemler için App.config dosyasında göründüğü biçimde olacaktır:

```
Endpoint=sb://[namespace].servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[key]
```

Son olarak, bu da oluşturmak mümkündür bir [EventHubClient][] nesnesinin bir [Eventhubclient](/dotnet/api/microsoft.servicebus.messaging.messagingfactory) , aşağıdaki örnekte gösterildiği gibi örneği:

```csharp
var factory = MessagingFactory.CreateFromConnectionString("your_connection_string");
var client = factory.CreateEventHubClient("MyEventHub");
```

Ek önemlidir [EventHubClient][] bir Mesajlaşma fabrikası örneğinden oluşturulan nesneler temel alınan aynı TCP bağlantısını yeniden kullanabilirsiniz. Bu nedenle, bu nesneler işlemede istemci tarafı sınırlamasına sahiptir. [Create](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_Create_System_String_) yöntemi tek bir mesajlaşma altyapısını yeniden kullanır. Tek bir gönderenden çok yüksek işleme gerekiyorsa birden fazla ileti altyapısı ve her mesajlaşma altyapısından bir [EventHubClient][] nesnesi oluşturabilirsiniz.

## <a name="send-events-to-an-event-hub"></a>Olayları bir event hub'ına Gönder
Oluşturarak olay hub'ına olayları göndermek bir [EventData][] örneği ve ile göndererek [Gönder](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_Send_Microsoft_ServiceBus_Messaging_EventData_) yöntemi. Bu yöntem tek bir alır [EventData][] örnek parametresini ve zaman uyumlu olarak olay hub'ına gönderir.

## <a name="event-serialization"></a>Olayı seri hale getirme
[EventData][] sınıfında nesne ve seri hale getirici, bayt dizisi veya akış gibi çeşitli parametreler kullanan [dört aşırı yüklü oluşturucu](/dotnet/api/microsoft.servicebus.messaging.eventdata#constructors_) bulunur. [EventData][] sınıfının bir örneğini oluşturup gövde akışını daha sonra ayarlamak da mümkündür. JSON’u [EventData][] ile kullanırken JSON ile kodlanmış bir dize için bayt dizisini almak üzere **Encoding.UTF8.GetBytes()** kullanabilirsiniz.

## <a name="partition-key"></a>Bölüm anahtarı
[EventData][] sınıfında gönderenin bir bölüm ataması oluşturmak üzere karma hale getirilmiş değer belirtmesini sağlayan bir [PartitionKey][] özelliği bulunur. Bir bölüm anahtarının kullanılması aynı anahtara sahip tüm olayların aynı bölüm için olay hub'ı gönderilmesini sağlar. Yaygın bölüm anahtarları kullanıcı oturum kimlikleri ve benzersiz gönderen kimlikleridir. [PartitionKey][] özelliği isteğe bağlıdır ve [Microsoft.ServiceBus.Messaging.EventHubClient.Send(Microsoft.ServiceBus.Messaging.EventData)](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_Send_Microsoft_ServiceBus_Messaging_EventData_) veya [Microsoft.ServiceBus.Messaging.EventHubClient.SendAsync(Microsoft.ServiceBus.Messaging.EventData)](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_SendAsync_Microsoft_ServiceBus_Messaging_EventData_) yöntemleri kullanılırken sağlanabilir. [PartitionKey][] için bir değer belirtmezseniz gönderilen olaylar genel bir model kullanılarak bölümlere dağıtılır.

### <a name="availability-considerations"></a>Kullanılabilirlik konusunda dikkat edilmesi gerekenler

Bir bölüm anahtarının kullanılması isteğe bağlıdır ve bir kullanılıp kullanılmayacağını dikkatle düşünmelisiniz. Olay sıralama önemliyse, çoğu durumda, bir bölüm anahtarının kullanılması iyi bir seçimdir. Bölüm anahtarı kullandığınızda, bu bölümler kullanılabilirlik tek bir düğümde gerektirir ve zaman içinde kesintiler; Örneğin, düğümlerin yeniden başlatma ve düzeltme zaman işlem. Bu nedenle, bölüm kimliği ayarlamak ve bu bölümü için herhangi bir nedenle kullanılamaz duruma gelir, bu bölümü verilere erişim denemesi başarısız olur. Bölüm anahtarı yüksek oranda kullanılabilirlik en önemli ise belirtmeyin; Bu durumda olayları daha önce açıklanan hepsini model kullanılarak bölümlere gönderilir. Bu senaryoda, kullanılabilirlik (bölüm kimliği) ve tutarlılık (bölüm kimliği için olaylar sabitleme) arasında açık bir seçim getirirsiniz.

Başka bir göz önünde bulundurarak olayları işleme gecikme işliyor. Bazı durumlarda, veri ve potansiyel olarak daha aşağı akış işleme gecikmelere neden olabilir işlemeyle tutmaya çalışın fazla yeniden deneme bırakma daha iyi olabilir. Örneğin, bir bandı, eksiksiz olmasa bile tam güncel verileri, ancak bir canlı sohbet ya da verileri hızlı bir şekilde, bunun yerine olurdu VoIP senaryo bekleyin en iyisidir.

Bu kullanılabilirlik noktalar bu senaryolarda verilen aşağıdaki hata işleme stratejiler birini:

- Durdur (stop şeyler çözülene kadar olay hub'larından okuma)
- Bırakma (iletileri önemli olmayan sürükleyip bırakın)
- (İletileri gördüğünüz gibi uygun yeniden deneme) yeniden deneyin
- [Sahipsiz](../service-bus-messaging/service-bus-dead-letter-queues.md) (veya başka bir olay hub'ına atılacak harf yalnızca uygulanamadı işlem iletileri bir sıra kullanın)

Daha fazla bilgi ve dengelemeler kullanılabilirlik ve tutarlılık arasında hakkında tartışma için bkz: [kullanılabilirlik ve Event Hubs tutarlılığını](event-hubs-availability-and-consistency.md). 

## <a name="batch-event-send-operations"></a>Toplu olay gönderme işlemleri
Olayların toplu olarak gönderilmesi yardımcı verimliliğini artırmak. [SendBatch](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_SendBatch_System_Collections_Generic_IEnumerable_Microsoft_ServiceBus_Messaging_EventData__) metodu bir **IEnumerable** türünde parametresi [EventData][] ve toplu işin tamamını atomik bir işlem olay hub'ına gönderir.

```csharp
public void SendBatch(IEnumerable<EventData> eventDataList);
```

Tek bir toplu iş olayın 256 KB’lik sınırını aşmamalıdır. Ayrıca, toplu işteki her bir ileti aynı yayımcı kimliğini kullanır. Toplu işin en büyük olay boyutu aşmamasını sağlamak gönderenin sorumluluğundadır. Aşması durumunda bir istemci **Gönderme** hatası oluşturulur. Yardımcı yöntemi kullanabileceğiniz [EventHubClient.CreateBatch](/dotnet/api/microsoft.servicebus.messaging.eventhubclient.createbatch) toplu 256 KB aşmadığından emin olmak için. Boş bir get [EventDataBatch](/dotnet/api/microsoft.servicebus.messaging.eventdatabatch) gelen [CreateBatch](/dotnet/api/microsoft.servicebus.messaging.eventhubclient.createbatch) API ve ardından [TryAdd](/dotnet/api/microsoft.servicebus.messaging.eventdatabatch.tryadd#Microsoft_ServiceBus_Messaging_EventDataBatch_TryAdd_Microsoft_ServiceBus_Messaging_EventData_) toplu oluşturmak için olay eklemek için. Son olarak, [EventDataBatch.ToEnumerable](/dotnet/api/microsoft.servicebus.messaging.eventdatabatch.toenumerable) geçirilecek temelindeki olayları almak için [EventHubClient.Send](/dotnet/api/microsoft.servicebus.messaging.eventhubclient.send) API.

## <a name="send-asynchronously-and-send-at-scale"></a>Zaman uyumsuz olarak gönderme ve ölçekli gönderme
Ayrıca olayları bir event hub'ına zaman uyumsuz olarak gönderebilirsiniz. Zaman uyumsuz gönderme bir istemcinin olayları gönderebildiği hızı artırabilir. Bir [Task](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) nesnesi döndüren zaman uyumsuz sürümlerde hem [Send](/dotnet/api/microsoft.servicebus.messaging.eventhubclient.send) hem de [SendBatch](/dotnet/api/microsoft.servicebus.messaging.eventhubclient.sendbatch) yöntemleri kullanılabilir. Bu teknik üretilen işi artırabilse de, istemcinin Event Hubs hizmeti tarafından kısıtlandığında bile olay göndermeye devam etmesine neden olabilir ve düzgün uygulanmaması durumunda istemcinin hata veya kayıp iletilerle karşılaşmasına yol açabilir. Ayrıca, istemci yeniden deneme seçeneklerini denetlemek için istemci üzerindeki [RetryPolicy](/dotnet/api/microsoft.servicebus.messaging.cliententity.retrypolicy) özelliğini kullanabilirsiniz.

## <a name="create-a-partition-sender"></a>Bölüm göndereni oluşturma
Bölüm anahtarı olmayan bir olay hub'ına olayları göndermek için en yaygın olsa da, bazı durumlarda olayları doğrudan belirli bir bölüme göndermek isteyebilirsiniz. Örneğin:

```csharp
var partitionedSender = client.CreatePartitionedSender(description.PartitionIds[0]);
```

[CreatePartitionedSender](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_CreatePartitionedSender_System_String_) döndüren bir [EventHubSender](/dotnet/api/microsoft.servicebus.messaging.eventhubsender) nesne olayları belirli olay hub'ı bölümünde yayımlamak için kullanabilirsiniz.

## <a name="event-consumers"></a>Olay tüketicileri
Event Hubs olay tüketimi için iki adet birincil modele sahiptir: doğrudan alıcılar ve [EventProcessorHost][] gibi üst düzey soyutlamalar. Alıcıları bölümleri sorumlu kendi erişim koordinasyonu için doğrudan bir *tüketici grubu*. Bir görünüme (durumu, konum veya offset) bölümlenmiş olay hub'ı bir tüketici grubudur.

### <a name="direct-consumer"></a>Doğrudan tüketici
Bir bölümün dışında okumak için en doğrudan yolu kullanmaktır [EventHubReceiver](/dotnet/apie/microsoft.servicebus.messaging.eventhubreceiver) sınıfı. Bu sınıfın bir örneğini oluşturmak için [EventHubConsumerGroup](/dotnet/api/microsoft.servicebus.messaging.eventhubconsumergroup) sınıfının bir örneğini kullanmanız gerekir. Aşağıdaki örnekte tüketici grubu için alıcı oluşturulurken bölüm kimliği belirtilmelidir:

```csharp
EventHubConsumerGroup group = client.GetDefaultConsumerGroup();
var receiver = group.CreateReceiver(client.GetRuntimeInformation().PartitionIds[0]);
```

[CreateReceiver](/dotnet/api/microsoft.servicebus.messaging.eventhubconsumergroup#methods_summary) yöntemi oluşturulmakta olan okuyucu üzerinde denetimi kolaylaştıran birkaç aşırı yüke sahiptir. Bu yöntemler bir uzaklığı dize veya zaman damgası olarak belirtmeyi ve belirtilen bu uzaklığın döndürülen akışa dahil edileceğini ya da ondan sonra başlayacağını belirtebilmeyi içerir. Alıcıyı oluşturduktan sonra döndürülen nesne üzerinde olayları almaya başlayabilirsiniz. [Receive](/dotnet/api/microsoft.servicebus.messaging.eventhubreceiver#methods_summary) yönteminde toplu işlem boyutu ve bekleme süresi gibi alma işlemi parametrelerini denetleyen dört aşırı yük bulunur. Bir tüketicinin verimliliğini artırmak için bu yöntemlerin zaman uyumsuz sürümlerini kullanabilirsiniz. Örneğin:

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

Belirli bir bölüme göre iletiler event hub'ına gönderildikleri sırayla alınır. Uzaklık bir bölümdeki bir iletiyi tanımlamak için kullanılan bir dize belirtecidir.

Tek bir bölüm 5'ten fazla eşzamanlı okuyucu herhangi bir zamanda bağlı olamaz unutmayın. Okuyucular bağlandığında veya bağlantıları kesildiğinde hizmetin bağlantı kesilmesini algılamasından önce oturumları birkaç dakika boyunca etkin kalabilir. Bu süre boyunca bir bölüme yeniden bağlanılması başarısız olabilir. Event Hubs için doğrudan alıcı yazmaya tam örnek için bkz [Event Hubs doğrudan alıcıları](https://code.msdn.microsoft.com/Event-Hub-Direct-Receivers-13fa95c6) örnek.

### <a name="event-processor-host"></a>Olay işlemcisi konağı
[EventProcessorHost][] sınıfı Event Hubs verilerini işler. .NET platformu üzerinde olay okuyucuları oluştururken bu uygulamayı kullanmanız gerekir. [EventProcessorHost][] aynı zamanda denetim noktası oluşturma ve bölüm kiralama yönetimi sağlayan olay işlemcisi uygulamaları için iş parçacığı güvenli, çok işlemli, güvenli bir çalışma zamanı ortamı sağlar.

[EventProcessorHost][] sınıfını kullanmak için [IEventProcessor](/dotnet/api/microsoft.servicebus.messaging.ieventprocessor) uygulayabilirsiniz. Bu arabirim üç yöntem içerir:

* [OpenAsync](/dotnet/api/microsoft.servicebus.messaging.ieventprocessor#Microsoft_ServiceBus_Messaging_IEventProcessor_OpenAsync_Microsoft_ServiceBus_Messaging_PartitionContext_)
* [CloseAsync](/dotnet/api/microsoft.servicebus.messaging.ieventprocessor#Microsoft_ServiceBus_Messaging_IEventProcessor_CloseAsync_Microsoft_ServiceBus_Messaging_PartitionContext_Microsoft_ServiceBus_Messaging_CloseReason_)
* [ProcessEventsAsync](/dotnet/api/microsoft.servicebus.messaging.ieventprocessor#Microsoft_ServiceBus_Messaging_IEventProcessor_ProcessEventsAsync_Microsoft_ServiceBus_Messaging_PartitionContext_System_Collections_Generic_IEnumerable_Microsoft_ServiceBus_Messaging_EventData__)

Olay işlemeyi başlatmak için örneği [EventProcessorHost][], event hub'ınıza uygun parametreleri sağlayarak. Ardından [IEventProcessor](/dotnet/api/microsoft.servicebus.messaging.ieventprocessor) uygulamanızı çalışma zamanına kaydetmek için [RegisterEventProcessorAsync](/dotnet/api/microsoft.servicebus.messaging.eventprocessorhost#Microsoft_ServiceBus_Messaging_EventProcessorHost_RegisterEventProcessorAsync__1) çağrısı yapın. Bu noktada konak bir "Hızlı" algoritma kullanarak event hub'ındaki her bölüm üzerinde bir kira almaya çalışır. Bu kiralar belirli bir zaman çerçevesi için en son ve sonrasında yenilenmelidir. Bu örnekte çalışan örnekleri olan yeni düğümler çevrimiçi oldukça kiralama ayırmaları yapar ve zaman içerisinde yük daha fazla kira elde etmeye çalıştığından düğümler arasında kayar.

![Olay İşlemcisi Konağı](./media/event-hubs-programming-guide/IC759863.png)

Zaman içerisinde bir denge sağlanır. Bu dinamik özellik hem ölçek artırma hem de ölçek azaltma için tüketicilere CPU tabanlı otomatik ölçeklendirmenin uygulanmasını sağlar. Olay hub'ları ileti sayısı doğrudan kavramına sahip olmadığından ortalama CPU kullanımı genellikle arka uç veya tüketici ölçeğini ölçmeye yönelik en iyi mekanizmadır. Yayımcılar tüketicilerin işleyebileceğinden daha fazla olay yayımlamaya başlarsa, tüketiciler üzerindeki CPU artışı çalışan örnek sayısı üzerinde otomatik ölçeklendirmeye neden olmak için kullanılabilir.

[EventProcessorHost][] sınıfı ayrıca bir Azure depolama tabanlı denetim noktası oluşturma mekanizması kullanır. Bu mekanizma uzaklığı bölüm başına temelinde depolar, böylece her tüketici önceki tüketicinin son denetim noktasının ne olduğunu belirleyebilir. Bölümler kiralamalar aracılığıyla düğümler arasında geçiş yaptığında yük kaymasını kolaylaştıran eşitleme mekanizması budur.

## <a name="publisher-revocation"></a>Yayımcı iptali
Gelişmiş çalışma zamanı özelliklerine ek olarak [EventProcessorHost][], Event Hubs, belirli yayımcıların bir event hub'ına olay göndermesini engellemek üzere yayımcı iptalini sağlar. Bu özellikler bir yayımcı belirteci tehlike veya bir yazılım güncelleştirmesi yayımcının uygunsuz şekilde davranmasına neden yararlıdır. Bu durumlarda SAS belirtecinin bir parçası olan yayımcı kimliğinin olayları yayımlaması engellenebilir.

Yayımcı iptali ve yayımcı olarak Event Hubs’a gönderme hakkında daha fazla bilgi için [Event Hubs Büyük Ölçekli Güvenli Yayımlama](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-99ce67ab) örneğine bakın.

## <a name="next-steps"></a>Sonraki adımlar
Event Hubs senaryoları hakkında daha fazla bilgi almak için aşağıdaki bağlantıları ziyaret edin:

* [Event Hubs API’sine genel bakış](event-hubs-api-overview.md)
* [Event Hubs nedir](event-hubs-what-is-event-hubs.md)
* [Event Hubs’da kullanılabilirlik ve tutarlılık](event-hubs-availability-and-consistency.md)
* [Olay işlemcisi konağı API başvurusu](/dotnet/api/microsoft.servicebus.messaging.eventprocessorhost)

[NamespaceManager]: /dotnet/api/microsoft.servicebus.namespacemanager
[EventHubClient]: /dotnet/api/microsoft.servicebus.messaging.eventhubclient
[EventData]: /dotnet/api/microsoft.servicebus.messaging.eventdata
[CreateEventHubIfNotExists]: /dotnet/api/microsoft.servicebus.namespacemanager.createeventhubifnotexists
[PartitionKey]: /dotnet/api/microsoft.servicebus.messaging.eventdata#Microsoft_ServiceBus_Messaging_EventData_PartitionKey
[EventProcessorHost]: /dotnet/api/microsoft.servicebus.messaging.eventprocessorhost
