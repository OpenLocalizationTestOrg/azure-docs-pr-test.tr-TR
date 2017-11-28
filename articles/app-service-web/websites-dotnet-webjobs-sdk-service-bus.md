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
# <a name="how-toouse-azure-service-bus-with-hello-webjobs-sdk"></a><span data-ttu-id="c6dae-103">Web işleri SDK'si toouse Azure Service Bus ile nasıl hello</span><span class="sxs-lookup"><span data-stu-id="c6dae-103">How toouse Azure Service Bus with hello WebJobs SDK</span></span>
## <a name="overview"></a><span data-ttu-id="c6dae-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="c6dae-104">Overview</span></span>
<span data-ttu-id="c6dae-105">Bu kılavuz C# sağlar kod örnekleri gösteren nasıl tootrigger bir Azure hizmet veri yolu ileti alındığında bir işlem.</span><span class="sxs-lookup"><span data-stu-id="c6dae-105">This guide provides C# code samples that show how tootrigger a process when an Azure Service Bus message is received.</span></span> <span data-ttu-id="c6dae-106">Merhaba kod örnekleri kullan [WebJobs SDK](websites-dotnet-webjobs-sdk.md) sürüm 1.x.</span><span class="sxs-lookup"><span data-stu-id="c6dae-106">hello code samples use [WebJobs SDK](websites-dotnet-webjobs-sdk.md) version 1.x.</span></span>

<span data-ttu-id="c6dae-107">Merhaba Kılavuzu varsayar bildiğiniz [nasıl toocreate bağlantısı ile Visual Studio'da bir Web işi projesi bu noktası tooyour depolama hesabı dizeleri](websites-dotnet-webjobs-sdk-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="c6dae-107">hello guide assumes you know [how toocreate a WebJob project in Visual Studio with connection strings that point tooyour storage account](websites-dotnet-webjobs-sdk-get-started.md).</span></span>

<span data-ttu-id="c6dae-108">İşlevler, yalnızca Hello kod parçacıkları Göster hello oluşturan kodunu hello değil `JobHost` nesne bu örnekte olduğu gibi:</span><span class="sxs-lookup"><span data-stu-id="c6dae-108">hello code snippets only show functions, not hello code that creates hello `JobHost` object as in this example:</span></span>

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

<span data-ttu-id="c6dae-109">A [tam Service Bus kod örneğinde](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/ServiceBus/Program.cs) Github.com'u hello azure webjobs sdk örnekleri havuzda bulunmaktadır.</span><span class="sxs-lookup"><span data-stu-id="c6dae-109">A [complete Service Bus code example](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/ServiceBus/Program.cs) is in hello azure-webjobs-sdk-samples repository on GitHub.com.</span></span>

## <span data-ttu-id="c6dae-110"><a id="prerequisites"></a>Önkoşulları</span><span class="sxs-lookup"><span data-stu-id="c6dae-110"><a id="prerequisites"></a> Prerequisites</span></span>
<span data-ttu-id="c6dae-111">toowork tooinstall hello sahip Service Bus ile [Microsoft.Azure.WebJobs.ServiceBus](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus/) NuGet paketini ayrıca diğer Web işleri SDK'si paketleri toohello.</span><span class="sxs-lookup"><span data-stu-id="c6dae-111">toowork with Service Bus you have tooinstall hello [Microsoft.Azure.WebJobs.ServiceBus](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus/) NuGet package in addition toohello other WebJobs SDK packages.</span></span> 

<span data-ttu-id="c6dae-112">Ayrıca ek toohello depolama bağlantı dizeleri tooset hello AzureWebJobsServiceBus bağlantı dizesini de vardır.</span><span class="sxs-lookup"><span data-stu-id="c6dae-112">You also have tooset hello AzureWebJobsServiceBus connection string in addition toohello storage connection strings.</span></span>  <span data-ttu-id="c6dae-113">Hello bunu yapabilirsiniz `connectionStrings` hello App.config dosyasının hello aşağıdaki örnekte gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="c6dae-113">You can do this in hello `connectionStrings` section of hello App.config file, as shown in hello following example:</span></span>

        <connectionStrings>
            <add name="AzureWebJobsDashboard" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="AzureWebJobsStorage" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="AzureWebJobsServiceBus" connectionString="Endpoint=sb://[yourServiceNamespace].servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[yourKey]"/>
        </connectionStrings>

<span data-ttu-id="c6dae-114">Merhaba App.config dosyasında hello hizmet veri yolu bağlantı dizesi ayarı içeren bir örnek proje için bkz: [hizmet veri yolu örnek](https://github.com/Azure/azure-webjobs-sdk-samples/tree/master/BasicSamples/ServiceBus).</span><span class="sxs-lookup"><span data-stu-id="c6dae-114">For a sample project that includes hello Service Bus connection string setting in hello App.config file, see [Service Bus example](https://github.com/Azure/azure-webjobs-sdk-samples/tree/master/BasicSamples/ServiceBus).</span></span> 

<span data-ttu-id="c6dae-115">Merhaba bağlantı dizeleri de hello WebJob Azure içinde çalıştığında, hello App.config ayarları geçersiz kılan hello Azure çalışma zamanı ortamı ayarlanabilir; Daha fazla bilgi için bkz: [hello WebJobs SDK ile çalışmaya başlama](websites-dotnet-webjobs-sdk-get-started.md#configure-the-web-app-to-use-your-azure-sql-database-and-storage-account).</span><span class="sxs-lookup"><span data-stu-id="c6dae-115">hello connection strings can also be set in hello Azure runtime environment, which then overrides hello App.config settings when hello WebJob runs in Azure; for more information, see [Get Started with hello WebJobs SDK](websites-dotnet-webjobs-sdk-get-started.md#configure-the-web-app-to-use-your-azure-sql-database-and-storage-account).</span></span>

## <span data-ttu-id="c6dae-116"><a id="trigger"></a>Tootrigger Service Bus sıraya olduğunda ileti işlevi nasıl alındı</span><span class="sxs-lookup"><span data-stu-id="c6dae-116"><a id="trigger"></a> How tootrigger a function when a Service Bus queue message is received</span></span>
<span data-ttu-id="c6dae-117">toowrite Web işleri SDK'si hello işlevi çağıran bir kuyruk iletisi alındığında, hello kullan `ServiceBusTrigger` özniteliği.</span><span class="sxs-lookup"><span data-stu-id="c6dae-117">toowrite a function that hello WebJobs SDK calls when a queue message is received, use hello `ServiceBusTrigger` attribute.</span></span> <span data-ttu-id="c6dae-118">Merhaba öznitelik oluşturucunun hello sıra toopoll hello adını belirtir bir parametre alır.</span><span class="sxs-lookup"><span data-stu-id="c6dae-118">hello attribute constructor takes a parameter that specifies hello name of hello queue toopoll.</span></span>

### <a name="how-servicebustrigger-works"></a><span data-ttu-id="c6dae-119">ServiceBusTrigger nasıl çalışır?</span><span class="sxs-lookup"><span data-stu-id="c6dae-119">How ServiceBusTrigger works</span></span>
<span data-ttu-id="c6dae-120">Merhaba SDK bir iletisinde aldığı `PeekLock` modu ve çağrıları `Complete` hello işlevi başarıyla tamamlanırsa selamlama iletisine veya çağrıları `Abandon` hello işlevi başarısız olursa.</span><span class="sxs-lookup"><span data-stu-id="c6dae-120">hello SDK receives a message in `PeekLock` mode and calls `Complete` on hello message if hello function finishes successfully, or calls `Abandon` if hello function fails.</span></span> <span data-ttu-id="c6dae-121">Merhaba işlevi hello uzun çalışırsa `PeekLock` zaman aşımı, hello kilidi otomatik olarak yenilenir.</span><span class="sxs-lookup"><span data-stu-id="c6dae-121">If hello function runs longer than hello `PeekLock` timeout, hello lock is automatically renewed.</span></span>

<span data-ttu-id="c6dae-122">Hizmet veri yolu, denetlenmesi veya Web işleri SDK'si hello tarafından yapılandırılan kendi zararlı sıra işleme yapar.</span><span class="sxs-lookup"><span data-stu-id="c6dae-122">Service Bus does its own poison queue handling which cannot be controlled or configured by hello WebJobs SDK.</span></span> 

### <a name="string-queue-message"></a><span data-ttu-id="c6dae-123">Dize kuyruk iletisi</span><span class="sxs-lookup"><span data-stu-id="c6dae-123">String queue message</span></span>
<span data-ttu-id="c6dae-124">Merhaba aşağıdaki kod örneği bir dize içeriyor ve hello dize toohello WebJobs SDK Pano yazan bir kuyruk iletisi okur.</span><span class="sxs-lookup"><span data-stu-id="c6dae-124">hello following code sample reads a queue message that contains a string and writes hello string toohello WebJobs SDK dashboard.</span></span>

        public static void ProcessQueueMessage([ServiceBusTrigger("inputqueue")] string message, 
            TextWriter logger)
        {
            logger.WriteLine(message);
        }

<span data-ttu-id="c6dae-125">**Not:** hello iletileri kuyruğa hello Web işleri SDK'si kullanmayan bir uygulamada oluşturuyorsanız emin tooset olun [BrokeredMessage.ContentType](http://msdn.microsoft.com/library/microsoft.servicebus.messaging.brokeredmessage.contenttype.aspx) çok "metin/düz".</span><span class="sxs-lookup"><span data-stu-id="c6dae-125">**Note:** If you are creating hello queue messages in an application that doesn't use hello WebJobs SDK, make sure tooset [BrokeredMessage.ContentType](http://msdn.microsoft.com/library/microsoft.servicebus.messaging.brokeredmessage.contenttype.aspx) too"text/plain".</span></span>

### <a name="poco-queue-message"></a><span data-ttu-id="c6dae-126">POCO kuyruk iletisi</span><span class="sxs-lookup"><span data-stu-id="c6dae-126">POCO queue message</span></span>
<span data-ttu-id="c6dae-127">Merhaba SDK otomatik olarak JSON için bir POCO içeren bir kuyruk iletisi serisini [(düz eski CLR nesnesi](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) yazın.</span><span class="sxs-lookup"><span data-stu-id="c6dae-127">hello SDK will automatically deserialize a queue message that contains JSON for a POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) type.</span></span> <span data-ttu-id="c6dae-128">Merhaba aşağıdaki kod örneği okur içeren bir kuyruk iletisi bir `BlobInformation` olan nesne bir `BlobName` özelliği:</span><span class="sxs-lookup"><span data-stu-id="c6dae-128">hello following code sample reads a queue message that contains a `BlobInformation` object which has a `BlobName` property:</span></span>

        public static void WriteLogPOCO([ServiceBusTrigger("inputqueue")] BlobInformation blobInfo,
            TextWriter logger)
        {
            logger.WriteLine("Queue message refers tooblob: " + blobInfo.BlobName);
        }

<span data-ttu-id="c6dae-129">Nasıl BLOB'ları ve tablolar ile Merhaba POCO toowork toouse özelliklerini aynı hello gösteren kod örnekleri için işlev, hello bkz [bu makalenin depolama kuyrukları sürümü](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#pocoblobs).</span><span class="sxs-lookup"><span data-stu-id="c6dae-129">For code samples showing how toouse properties of hello POCO toowork with blobs and tables in hello same function, see hello [storage queues version of this article](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#pocoblobs).</span></span>

<span data-ttu-id="c6dae-130">Merhaba kuyruk iletisi oluşturur, kodunuzu hello Web işleri SDK'si kullanmıyorsa, aşağıdaki örnek kod benzer toohello kullanın:</span><span class="sxs-lookup"><span data-stu-id="c6dae-130">If your code that creates hello queue message doesn't use hello WebJobs SDK, use code similar toohello following example:</span></span>

        var client = QueueClient.CreateFromConnectionString(ConfigurationManager.ConnectionStrings["AzureWebJobsServiceBus"].ConnectionString, "blobadded");
        BlobInformation blobInformation = new BlobInformation () ;
        var message = new BrokeredMessage(blobInformation);
        client.Send(message);

### <a name="types-servicebustrigger-works-with"></a><span data-ttu-id="c6dae-131">Türleri ServiceBusTrigger birlikte çalışır.</span><span class="sxs-lookup"><span data-stu-id="c6dae-131">Types ServiceBusTrigger works with</span></span>
<span data-ttu-id="c6dae-132">Yanında `string` ve POCO türleri hello kullanabilirsiniz `ServiceBusTrigger` bir bayt dizisi özniteliğiyle veya `BrokeredMessage` nesnesi.</span><span class="sxs-lookup"><span data-stu-id="c6dae-132">Besides `string` and POCO  types, you can use hello `ServiceBusTrigger` attribute with a byte array or a `BrokeredMessage` object.</span></span>

## <span data-ttu-id="c6dae-133"><a id="create"></a>Nasıl toocreate Service Bus kuyruk iletileri</span><span class="sxs-lookup"><span data-stu-id="c6dae-133"><a id="create"></a> How toocreate Service Bus queue messages</span></span>
<span data-ttu-id="c6dae-134">toowrite yeni bir kuyruk iletisi oluşturan bir işlev kullanmak hello `ServiceBus` özniteliği ve hello kuyruk adı toohello öznitelik oluşturucuda geçirin.</span><span class="sxs-lookup"><span data-stu-id="c6dae-134">toowrite a function that creates a new queue message use hello `ServiceBus` attribute and pass in hello queue name toohello attribute constructor.</span></span> 

### <a name="create-a-single-queue-message-in-a-non-async-function"></a><span data-ttu-id="c6dae-135">Zaman uyumsuz olmayan işlevinde tek bir kuyruk iletisinin oluşturma</span><span class="sxs-lookup"><span data-stu-id="c6dae-135">Create a single queue message in a non-async function</span></span>
<span data-ttu-id="c6dae-136">Aşağıdaki kod örneği hello hello sırasındaki yeni bir ileti ile aynı içerik olarak "inputqueue" adlı hello sıraya alınan ileti hello hello "outputqueue" adlı bir çıktı parametresi toocreate kullanır.</span><span class="sxs-lookup"><span data-stu-id="c6dae-136">hello following code sample uses an output parameter toocreate a new message in hello queue named "outputqueue" with hello same content as hello message received in hello queue named "inputqueue".</span></span>

        public static void CreateQueueMessage(
            [ServiceBusTrigger("inputqueue")] string queueMessage,
            [ServiceBus("outputqueue")] out string outputQueueMessage)
        {
            outputQueueMessage = queueMessage;
        }

<span data-ttu-id="c6dae-137">tek bir kuyruk iletisinin oluşturmak için hello çıktı parametresi şu türlerini hello biri olabilir:</span><span class="sxs-lookup"><span data-stu-id="c6dae-137">hello output parameter for creating a single queue message can be any of hello following types:</span></span>

* `string`
* `byte[]`
* `BrokeredMessage`
* <span data-ttu-id="c6dae-138">Tanımladığınız POCO serileştirilebilir bir türde.</span><span class="sxs-lookup"><span data-stu-id="c6dae-138">A serializable POCO type that you define.</span></span> <span data-ttu-id="c6dae-139">Otomatik olarak JSON olarak serileştirilen.</span><span class="sxs-lookup"><span data-stu-id="c6dae-139">Automatically serialized as JSON.</span></span>

<span data-ttu-id="c6dae-140">Merhaba işlevi sona erdiğinde POCO tür parametreleri için her zaman bir kuyruk iletisi oluşturulur; Merhaba parametre null ise, hello SDK hello ileti alındı ve seri durumdan yükleyen null döner bir kuyruk iletisi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c6dae-140">For POCO type parameters, a queue message is always created when hello function ends; if hello parameter is null, hello SDK creates a queue message that will return null when hello message is received and deserialized.</span></span> <span data-ttu-id="c6dae-141">İçin diğer türleri Merhaba, herhangi bir kuyruk iletisi hello parametre null ise oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="c6dae-141">For hello other types, if hello parameter is null no queue message is created.</span></span>

### <a name="create-multiple-queue-messages-or-in-async-functions"></a><span data-ttu-id="c6dae-142">Birden çok sıra iletileri oluşturmak veya zaman uyumsuz işlevleri</span><span class="sxs-lookup"><span data-stu-id="c6dae-142">Create multiple queue messages or in async functions</span></span>
<span data-ttu-id="c6dae-143">toocreate birden fazla ileti kullanmak hello `ServiceBus` ile öznitelik `ICollector<T>` veya `IAsyncCollector<T>`hello kodu örneği aşağıdaki gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="c6dae-143">toocreate multiple messages, use  hello `ServiceBus` attribute with `ICollector<T>` or `IAsyncCollector<T>`, as shown in hello following code sample:</span></span>

        public static void CreateQueueMessages(
            [ServiceBusTrigger("inputqueue")] string queueMessage,
            [ServiceBus("outputqueue")] ICollector<string> outputQueueMessage,
            TextWriter logger)
        {
            logger.WriteLine("Creating 2 messages in outputqueue");
            outputQueueMessage.Add(queueMessage + "1");
            outputQueueMessage.Add(queueMessage + "2");
        }

<span data-ttu-id="c6dae-144">Her kuyruk iletisi hemen hello oluşturulduğunda `Add` yöntemi çağrılır.</span><span class="sxs-lookup"><span data-stu-id="c6dae-144">Each queue message is created immediately when hello `Add` method is called.</span></span>

## <span data-ttu-id="c6dae-145"><a id="topics"></a>Nasıl toowork ile Service Bus konuları</span><span class="sxs-lookup"><span data-stu-id="c6dae-145"><a id="topics"></a>How toowork with Service Bus topics</span></span>
<span data-ttu-id="c6dae-146">toowrite SDK hello işlevi çağıran bir Service Bus konu hakkında bir ileti alındığında, hello kullan `ServiceBusTrigger` konu adı ve abonelik adı hello kodu örneği aşağıdaki gösterildiği gibi alan hello Oluşturucu özniteliğiyle:</span><span class="sxs-lookup"><span data-stu-id="c6dae-146">toowrite a function that hello SDK calls when a message is received on a Service Bus topic, use hello `ServiceBusTrigger` attribute with hello constructor that takes topic name and subscription name, as shown in hello following code sample:</span></span>

        public static void WriteLog([ServiceBusTrigger("outputtopic","subscription1")] string message,
            TextWriter logger)
        {
            logger.WriteLine("Topic message: " + message);
        }

<span data-ttu-id="c6dae-147">toocreate kullanım hello bir konu ileti `ServiceBus` bir konu adı hello ile aynı özniteliği kullanmanız kuyruk adı ile yolu.</span><span class="sxs-lookup"><span data-stu-id="c6dae-147">toocreate a message on a topic, use hello `ServiceBus` attribute with a topic name hello same way you use it with a queue name.</span></span>

## <a name="features-added-in-release-11"></a><span data-ttu-id="c6dae-148">Sürüm 1.1 eklenen özellikler</span><span class="sxs-lookup"><span data-stu-id="c6dae-148">Features added in release 1.1</span></span>
<span data-ttu-id="c6dae-149">özellikler aşağıdaki hello sürüm 1.1 eklendi:</span><span class="sxs-lookup"><span data-stu-id="c6dae-149">hello following features were added in release 1.1:</span></span>

* <span data-ttu-id="c6dae-150">İleti aracılığıyla işleme derin özelleştirilmesine imkan tanımak `ServiceBusConfiguration.MessagingProvider`.</span><span class="sxs-lookup"><span data-stu-id="c6dae-150">Allow deep customization of message processing via `ServiceBusConfiguration.MessagingProvider`.</span></span>
* <span data-ttu-id="c6dae-151">`MessagingProvider`Merhaba Service Bus özelleştirmesini destekleyen `MessagingFactory` ve `NamespaceManager`.</span><span class="sxs-lookup"><span data-stu-id="c6dae-151">`MessagingProvider` supports customization of hello Service Bus `MessagingFactory` and `NamespaceManager`.</span></span>
* <span data-ttu-id="c6dae-152">A `MessageProcessor` stratejisi düzeni toospecify işlemci sırası/konu başına sağlar.</span><span class="sxs-lookup"><span data-stu-id="c6dae-152">A `MessageProcessor` strategy pattern allows you toospecify a processor per queue/topic.</span></span>
* <span data-ttu-id="c6dae-153">İleti işleme eşzamanlılık varsayılan olarak desteklenir.</span><span class="sxs-lookup"><span data-stu-id="c6dae-153">Message processing concurrency is supported by default.</span></span> 
* <span data-ttu-id="c6dae-154">Kolay özelleştirmesini `OnMessageOptions` aracılığıyla `ServiceBusConfiguration.MessageOptions`.</span><span class="sxs-lookup"><span data-stu-id="c6dae-154">Easy customization of `OnMessageOptions` via `ServiceBusConfiguration.MessageOptions`.</span></span>
* <span data-ttu-id="c6dae-155">İzin [erişimHakları](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/ServiceBus/Functions.cs#L71) belirtilen toobe `ServiceBusTriggerAttribute` / `ServiceBusAttribute` (burada, sahip olmayabilir senaryolarını haklarını yönetmek için).</span><span class="sxs-lookup"><span data-stu-id="c6dae-155">Allow [AccessRights](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/ServiceBus/Functions.cs#L71) toobe specified on `ServiceBusTriggerAttribute`/`ServiceBusAttribute` (for scenarios where you might not have Manage rights).</span></span> <span data-ttu-id="c6dae-156">Azure Web işleri oluşturulamıyor tooautomatically sağlama mevcut olmayan sıraları ve konuları yönetme erişimHakları olmadan olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="c6dae-156">Note that Azure WebJobs is unable tooautomatically provision non-existent queues and topics without Manage AccessRights.</span></span>

## <span data-ttu-id="c6dae-157"><a id="queues"></a>Merhaba depolama kuyrukları nasıl-tooarticle tarafından kapsanan ilgili konular</span><span class="sxs-lookup"><span data-stu-id="c6dae-157"><a id="queues"></a>Related topics covered by hello storage queues how-tooarticle</span></span>
<span data-ttu-id="c6dae-158">Özel olmayan tooService veri yolu, Web işleri SDK'si senaryoları hakkında bilgi için bkz: [nasıl toouse Azure kuyruk depolama hello WebJobs SDK ile](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="c6dae-158">For information about WebJobs SDK scenarios not specific tooService Bus, see [How toouse Azure queue storage with hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span></span> 

<span data-ttu-id="c6dae-159">Bu makalede ele alınan konular hello şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="c6dae-159">Topics covered in that article include hello following:</span></span>

* <span data-ttu-id="c6dae-160">Zaman uyumsuz işlevleri</span><span class="sxs-lookup"><span data-stu-id="c6dae-160">Async functions</span></span>
* <span data-ttu-id="c6dae-161">Birden çok örneği</span><span class="sxs-lookup"><span data-stu-id="c6dae-161">Multiple instances</span></span>
* <span data-ttu-id="c6dae-162">Kapama</span><span class="sxs-lookup"><span data-stu-id="c6dae-162">Graceful shutdown</span></span>
* <span data-ttu-id="c6dae-163">Web işleri SDK'si özniteliklerini işlevinin hello gövdesindeki kullanın</span><span class="sxs-lookup"><span data-stu-id="c6dae-163">Use WebJobs SDK attributes in hello body of a function</span></span>
* <span data-ttu-id="c6dae-164">Kod içinde Hello SDK bağlantı dizelerini ayarlayın</span><span class="sxs-lookup"><span data-stu-id="c6dae-164">Set hello SDK connection strings in code</span></span>
* <span data-ttu-id="c6dae-165">Değerleri için Web işleri SDK'si Oluşturucu parametreleri kodda ayarlama</span><span class="sxs-lookup"><span data-stu-id="c6dae-165">Set values for WebJobs SDK constructor parameters in code</span></span>
* <span data-ttu-id="c6dae-166">Tetik el ile bir işlevi</span><span class="sxs-lookup"><span data-stu-id="c6dae-166">Trigger a function manually</span></span>
* <span data-ttu-id="c6dae-167">Günlüklerini yazma</span><span class="sxs-lookup"><span data-stu-id="c6dae-167">Write logs</span></span>

## <span data-ttu-id="c6dae-168"><a id="nextsteps"></a> Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c6dae-168"><a id="nextsteps"></a> Next steps</span></span>
<span data-ttu-id="c6dae-169">Bu kılavuz kodu sağlamıştır gösteren nasıl örnekleri Azure Service Bus ile çalışmak için genel senaryolar toohandle.</span><span class="sxs-lookup"><span data-stu-id="c6dae-169">This guide has provided code samples that show how toohandle common scenarios for working with Azure Service Bus.</span></span> <span data-ttu-id="c6dae-170">Toouse Azure Web işleri ve hello Web işleri SDK'si nasıl görürüm hakkında daha fazla bilgi için [Azure Web işleri önerilen kaynakları](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="c6dae-170">For more information about how toouse Azure WebJobs and hello WebJobs SDK, see [Azure WebJobs Recommended Resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

