---
title: Merhaba WebJobs SDK ile aaaHow toouse Azure hizmet veri yolu
description: "Web işleri SDK'si toouse Azure Service Bus kuyrukları ve konularından ile nasıl hello öğrenin."
services: app-service\web, service-bus
documentationcenter: .net
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: 2114a934-135b-42b8-871c-6cc040214e76
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/01/2016
ms.author: glenga
ms.openlocfilehash: cb801a9320a20c276da4f48c8941c09d3f09bb1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-service-bus-with-hello-webjobs-sdk"></a>Web işleri SDK'si toouse Azure Service Bus ile nasıl hello
## <a name="overview"></a>Genel Bakış
Bu kılavuz C# sağlar kod örnekleri gösteren nasıl tootrigger bir Azure hizmet veri yolu ileti alındığında bir işlem. Merhaba kod örnekleri kullan [WebJobs SDK](websites-dotnet-webjobs-sdk.md) sürüm 1.x.

Merhaba Kılavuzu varsayar bildiğiniz [nasıl toocreate bağlantısı ile Visual Studio'da bir Web işi projesi bu noktası tooyour depolama hesabı dizeleri](websites-dotnet-webjobs-sdk-get-started.md).

İşlevler, yalnızca Hello kod parçacıkları Göster hello oluşturan kodunu hello değil `JobHost` nesne bu örnekte olduğu gibi:

```
public class Program
{
   public static void Main()
   {
      JobHostConfiguration config = new JobHostConfiguration();
      config.UseServiceBus();
      JobHost host = new JobHost(config);
      host.RunAndBlock();
   }
}
```

A [tam Service Bus kod örneğinde](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/ServiceBus/Program.cs) Github.com'u hello azure webjobs sdk örnekleri havuzda bulunmaktadır.

## <a id="prerequisites"></a>Önkoşulları
toowork tooinstall hello sahip Service Bus ile [Microsoft.Azure.WebJobs.ServiceBus](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus/) NuGet paketini ayrıca diğer Web işleri SDK'si paketleri toohello. 

Ayrıca ek toohello depolama bağlantı dizeleri tooset hello AzureWebJobsServiceBus bağlantı dizesini de vardır.  Hello bunu yapabilirsiniz `connectionStrings` hello App.config dosyasının hello aşağıdaki örnekte gösterildiği gibi:

        <connectionStrings>
            <add name="AzureWebJobsDashboard" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="AzureWebJobsStorage" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="AzureWebJobsServiceBus" connectionString="Endpoint=sb://[yourServiceNamespace].servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[yourKey]"/>
        </connectionStrings>

Merhaba App.config dosyasında hello hizmet veri yolu bağlantı dizesi ayarı içeren bir örnek proje için bkz: [hizmet veri yolu örnek](https://github.com/Azure/azure-webjobs-sdk-samples/tree/master/BasicSamples/ServiceBus). 

Merhaba bağlantı dizeleri de hello WebJob Azure içinde çalıştığında, hello App.config ayarları geçersiz kılan hello Azure çalışma zamanı ortamı ayarlanabilir; Daha fazla bilgi için bkz: [hello WebJobs SDK ile çalışmaya başlama](websites-dotnet-webjobs-sdk-get-started.md#configure-the-web-app-to-use-your-azure-sql-database-and-storage-account).

## <a id="trigger"></a>Tootrigger Service Bus sıraya olduğunda ileti işlevi nasıl alındı
toowrite Web işleri SDK'si hello işlevi çağıran bir kuyruk iletisi alındığında, hello kullan `ServiceBusTrigger` özniteliği. Merhaba öznitelik oluşturucunun hello sıra toopoll hello adını belirtir bir parametre alır.

### <a name="how-servicebustrigger-works"></a>ServiceBusTrigger nasıl çalışır?
Merhaba SDK bir iletisinde aldığı `PeekLock` modu ve çağrıları `Complete` hello işlevi başarıyla tamamlanırsa selamlama iletisine veya çağrıları `Abandon` hello işlevi başarısız olursa. Merhaba işlevi hello uzun çalışırsa `PeekLock` zaman aşımı, hello kilidi otomatik olarak yenilenir.

Hizmet veri yolu, denetlenmesi veya Web işleri SDK'si hello tarafından yapılandırılan kendi zararlı sıra işleme yapar. 

### <a name="string-queue-message"></a>Dize kuyruk iletisi
Merhaba aşağıdaki kod örneği bir dize içeriyor ve hello dize toohello WebJobs SDK Pano yazan bir kuyruk iletisi okur.

        public static void ProcessQueueMessage([ServiceBusTrigger("inputqueue")] string message, 
            TextWriter logger)
        {
            logger.WriteLine(message);
        }

**Not:** hello iletileri kuyruğa hello Web işleri SDK'si kullanmayan bir uygulamada oluşturuyorsanız emin tooset olun [BrokeredMessage.ContentType](http://msdn.microsoft.com/library/microsoft.servicebus.messaging.brokeredmessage.contenttype.aspx) çok "metin/düz".

### <a name="poco-queue-message"></a>POCO kuyruk iletisi
Merhaba SDK otomatik olarak JSON için bir POCO içeren bir kuyruk iletisi serisini [(düz eski CLR nesnesi](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) yazın. Merhaba aşağıdaki kod örneği okur içeren bir kuyruk iletisi bir `BlobInformation` olan nesne bir `BlobName` özelliği:

        public static void WriteLogPOCO([ServiceBusTrigger("inputqueue")] BlobInformation blobInfo,
            TextWriter logger)
        {
            logger.WriteLine("Queue message refers tooblob: " + blobInfo.BlobName);
        }

Nasıl BLOB'ları ve tablolar ile Merhaba POCO toowork toouse özelliklerini aynı hello gösteren kod örnekleri için işlev, hello bkz [bu makalenin depolama kuyrukları sürümü](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#pocoblobs).

Merhaba kuyruk iletisi oluşturur, kodunuzu hello Web işleri SDK'si kullanmıyorsa, aşağıdaki örnek kod benzer toohello kullanın:

        var client = QueueClient.CreateFromConnectionString(ConfigurationManager.ConnectionStrings["AzureWebJobsServiceBus"].ConnectionString, "blobadded");
        BlobInformation blobInformation = new BlobInformation () ;
        var message = new BrokeredMessage(blobInformation);
        client.Send(message);

### <a name="types-servicebustrigger-works-with"></a>Türleri ServiceBusTrigger birlikte çalışır.
Yanında `string` ve POCO türleri hello kullanabilirsiniz `ServiceBusTrigger` bir bayt dizisi özniteliğiyle veya `BrokeredMessage` nesnesi.

## <a id="create"></a>Nasıl toocreate Service Bus kuyruk iletileri
toowrite yeni bir kuyruk iletisi oluşturan bir işlev kullanmak hello `ServiceBus` özniteliği ve hello kuyruk adı toohello öznitelik oluşturucuda geçirin. 

### <a name="create-a-single-queue-message-in-a-non-async-function"></a>Zaman uyumsuz olmayan işlevinde tek bir kuyruk iletisinin oluşturma
Aşağıdaki kod örneği hello hello sırasındaki yeni bir ileti ile aynı içerik olarak "inputqueue" adlı hello sıraya alınan ileti hello hello "outputqueue" adlı bir çıktı parametresi toocreate kullanır.

        public static void CreateQueueMessage(
            [ServiceBusTrigger("inputqueue")] string queueMessage,
            [ServiceBus("outputqueue")] out string outputQueueMessage)
        {
            outputQueueMessage = queueMessage;
        }

tek bir kuyruk iletisinin oluşturmak için hello çıktı parametresi şu türlerini hello biri olabilir:

* `string`
* `byte[]`
* `BrokeredMessage`
* Tanımladığınız POCO serileştirilebilir bir türde. Otomatik olarak JSON olarak serileştirilen.

Merhaba işlevi sona erdiğinde POCO tür parametreleri için her zaman bir kuyruk iletisi oluşturulur; Merhaba parametre null ise, hello SDK hello ileti alındı ve seri durumdan yükleyen null döner bir kuyruk iletisi oluşturur. İçin diğer türleri Merhaba, herhangi bir kuyruk iletisi hello parametre null ise oluşturulur.

### <a name="create-multiple-queue-messages-or-in-async-functions"></a>Birden çok sıra iletileri oluşturmak veya zaman uyumsuz işlevleri
toocreate birden fazla ileti kullanmak hello `ServiceBus` ile öznitelik `ICollector<T>` veya `IAsyncCollector<T>`hello kodu örneği aşağıdaki gösterildiği gibi:

        public static void CreateQueueMessages(
            [ServiceBusTrigger("inputqueue")] string queueMessage,
            [ServiceBus("outputqueue")] ICollector<string> outputQueueMessage,
            TextWriter logger)
        {
            logger.WriteLine("Creating 2 messages in outputqueue");
            outputQueueMessage.Add(queueMessage + "1");
            outputQueueMessage.Add(queueMessage + "2");
        }

Her kuyruk iletisi hemen hello oluşturulduğunda `Add` yöntemi çağrılır.

## <a id="topics"></a>Nasıl toowork ile Service Bus konuları
toowrite SDK hello işlevi çağıran bir Service Bus konu hakkında bir ileti alındığında, hello kullan `ServiceBusTrigger` konu adı ve abonelik adı hello kodu örneği aşağıdaki gösterildiği gibi alan hello Oluşturucu özniteliğiyle:

        public static void WriteLog([ServiceBusTrigger("outputtopic","subscription1")] string message,
            TextWriter logger)
        {
            logger.WriteLine("Topic message: " + message);
        }

toocreate kullanım hello bir konu ileti `ServiceBus` bir konu adı hello ile aynı özniteliği kullanmanız kuyruk adı ile yolu.

## <a name="features-added-in-release-11"></a>Sürüm 1.1 eklenen özellikler
özellikler aşağıdaki hello sürüm 1.1 eklendi:

* İleti aracılığıyla işleme derin özelleştirilmesine imkan tanımak `ServiceBusConfiguration.MessagingProvider`.
* `MessagingProvider`Merhaba Service Bus özelleştirmesini destekleyen `MessagingFactory` ve `NamespaceManager`.
* A `MessageProcessor` stratejisi düzeni toospecify işlemci sırası/konu başına sağlar.
* İleti işleme eşzamanlılık varsayılan olarak desteklenir. 
* Kolay özelleştirmesini `OnMessageOptions` aracılığıyla `ServiceBusConfiguration.MessageOptions`.
* İzin [erişimHakları](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/ServiceBus/Functions.cs#L71) belirtilen toobe `ServiceBusTriggerAttribute` / `ServiceBusAttribute` (burada, sahip olmayabilir senaryolarını haklarını yönetmek için). Azure Web işleri oluşturulamıyor tooautomatically sağlama mevcut olmayan sıraları ve konuları yönetme erişimHakları olmadan olduğuna dikkat edin.

## <a id="queues"></a>Merhaba depolama kuyrukları nasıl-tooarticle tarafından kapsanan ilgili konular
Özel olmayan tooService veri yolu, Web işleri SDK'si senaryoları hakkında bilgi için bkz: [nasıl toouse Azure kuyruk depolama hello WebJobs SDK ile](websites-dotnet-webjobs-sdk-storage-queues-how-to.md). 

Bu makalede ele alınan konular hello şunları içerir:

* Zaman uyumsuz işlevleri
* Birden çok örneği
* Kapama
* Web işleri SDK'si özniteliklerini işlevinin hello gövdesindeki kullanın
* Kod içinde Hello SDK bağlantı dizelerini ayarlayın
* Değerleri için Web işleri SDK'si Oluşturucu parametreleri kodda ayarlama
* Tetik el ile bir işlevi
* Günlüklerini yazma

## <a id="nextsteps"></a> Sonraki adımlar
Bu kılavuz kodu sağlamıştır gösteren nasıl örnekleri Azure Service Bus ile çalışmak için genel senaryolar toohandle. Toouse Azure Web işleri ve hello Web işleri SDK'si nasıl görürüm hakkında daha fazla bilgi için [Azure Web işleri önerilen kaynakları](http://go.microsoft.com/fwlink/?linkid=390226).

