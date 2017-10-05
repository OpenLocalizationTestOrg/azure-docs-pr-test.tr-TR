---
title: "Node.js içinde Service Bus kuyruklarını kullanma | Microsoft Docs"
description: "Bir Node.js uygulamasını Azure'da Service Bus kuyruklarını kullanmayı öğrenin."
services: service-bus-messaging
documentationcenter: nodejs
author: sethmanheim
manager: timlt
editor: 
ms.assetid: a87a00f9-9aba-4c49-a0df-f900a8b67b3f
ms.service: service-bus-messaging
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: fe2c02534996d99c190593a419a4823888f03d31
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-service-bus-queues-with-nodejs"></a><span data-ttu-id="f4f06-103">Node.js ile Service Bus kuyruklarını kullanma</span><span class="sxs-lookup"><span data-stu-id="f4f06-103">How to use Service Bus queues with Node.js</span></span>

[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

<span data-ttu-id="f4f06-104">Bu makalede, Node.js ile Service Bus kuyruklarını kullanmayı açıklar.</span><span class="sxs-lookup"><span data-stu-id="f4f06-104">This article describes how to use Service Bus queues with Node.js.</span></span> <span data-ttu-id="f4f06-105">Örnekler JavaScript'te yazılmış ve Node.js Azure modülü kullanın.</span><span class="sxs-lookup"><span data-stu-id="f4f06-105">The samples are written in JavaScript and use the Node.js Azure module.</span></span> <span data-ttu-id="f4f06-106">Kapsamdaki senaryolar dahil **sıra oluşturma**, **ileti gönderme ve alma**, ve **sıraları silme**.</span><span class="sxs-lookup"><span data-stu-id="f4f06-106">The scenarios covered include **creating queues**, **sending and receiving messages**, and **deleting queues**.</span></span> <span data-ttu-id="f4f06-107">Kuyruklar hakkında daha fazla bilgi için bkz: [sonraki adımlar](#next-steps) bölümü.</span><span class="sxs-lookup"><span data-stu-id="f4f06-107">For more information on queues, see the [Next steps](#next-steps) section.</span></span>

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="create-a-nodejs-application"></a><span data-ttu-id="f4f06-108">Node.js uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="f4f06-108">Create a Node.js application</span></span>
<span data-ttu-id="f4f06-109">Boş bir Node.js uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f4f06-109">Create a blank Node.js application.</span></span> <span data-ttu-id="f4f06-110">Bir Node.js uygulaması oluşturma hakkında daha fazla yönerge için bkz: [oluşturma ve bir Azure Web sitesine bir Node.js uygulaması dağıtma][Create and deploy a Node.js application to an Azure Website], veya [Node.js bulut hizmeti] [ Node.js Cloud Service] Windows PowerShell kullanarak.</span><span class="sxs-lookup"><span data-stu-id="f4f06-110">For instructions on how to create a Node.js application, see [Create and deploy a Node.js application to an Azure Website][Create and deploy a Node.js application to an Azure Website], or [Node.js Cloud Service][Node.js Cloud Service] using Windows PowerShell.</span></span>

## <a name="configure-your-application-to-use-service-bus"></a><span data-ttu-id="f4f06-111">Service Bus hizmetini kullanmak için uygulamanızı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="f4f06-111">Configure your application to use Service Bus</span></span>
<span data-ttu-id="f4f06-112">Azure Service Bus hizmetini kullanmak için karşıdan yükle ve Node.js Azure paketini kullanın.</span><span class="sxs-lookup"><span data-stu-id="f4f06-112">To use Azure Service Bus, download and use the Node.js Azure package.</span></span> <span data-ttu-id="f4f06-113">Bu paket Service Bus REST Hizmetleri ile iletişim kitaplıkları kümesi içerir.</span><span class="sxs-lookup"><span data-stu-id="f4f06-113">This package includes a set of libraries that communicate with the Service Bus REST services.</span></span>

### <a name="use-node-package-manager-npm-to-obtain-the-package"></a><span data-ttu-id="f4f06-114">Paket elde etmek için düğüm paketi Yöneticisi (NPM) kullanın</span><span class="sxs-lookup"><span data-stu-id="f4f06-114">Use Node Package Manager (NPM) to obtain the package</span></span>
1. <span data-ttu-id="f4f06-115">Kullanım **Node.js için Windows PowerShell** gitmek için komut penceresi **c:\\düğümü\\sbqueues\\WebRole1** örneğinizi oluşturduğunuz klasörü uygulama.</span><span class="sxs-lookup"><span data-stu-id="f4f06-115">Use the **Windows PowerShell for Node.js** command window to navigate to the **c:\\node\\sbqueues\\WebRole1** folder in which you created your sample application.</span></span>
2. <span data-ttu-id="f4f06-116">Tür **npm yükleme azure** komut penceresinde hangi neden aşağıdakine benzer bir çıktı:</span><span class="sxs-lookup"><span data-stu-id="f4f06-116">Type **npm install azure** in the command window, which should result in output similar to the following:</span></span>

    ```
    azure@0.7.5 node_modules\azure
        ├── dateformat@1.0.2-1.2.3
        ├── xmlbuilder@0.4.2
        ├── node-uuid@1.2.0
        ├── mime@1.2.9
        ├── underscore@1.4.4
        ├── validator@1.1.1
        ├── tunnel@0.0.2
        ├── wns@0.5.3
        ├── xml2js@0.2.7 (sax@0.5.2)
        └── request@2.21.0 (json-stringify-safe@4.0.0, forever-agent@0.5.0, aws-sign@0.3.0, tunnel-agent@0.3.0, oauth-sign@0.3.0, qs@0.6.5, cookie-jar@0.3.0, node-uuid@1.4.0, http-signature@0.9.11, form-data@0.0.8, hawk@0.13.1)
    ```
3. <span data-ttu-id="f4f06-117">El ile çalıştırabilirsiniz **ls** doğrulamak için komutu bir **node_modules** klasörü oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="f4f06-117">You can manually run the **ls** command to verify that a **node_modules** folder was created.</span></span> <span data-ttu-id="f4f06-118">Bu klasöre Bul **azure** Service Bus kuyruklarını erişmek için gereken kitaplıklar içeren paket.</span><span class="sxs-lookup"><span data-stu-id="f4f06-118">Inside that folder find the **azure** package, which contains the libraries you need to access Service Bus queues.</span></span>

### <a name="import-the-module"></a><span data-ttu-id="f4f06-119">Modülünü içeri aktarın</span><span class="sxs-lookup"><span data-stu-id="f4f06-119">Import the module</span></span>
<span data-ttu-id="f4f06-120">Not Defteri'nde veya başka bir metin düzenleyicisi kullanarak, aşağıdaki üst kısmına ekleyin **server.js** uygulamanın dosya:</span><span class="sxs-lookup"><span data-stu-id="f4f06-120">Using Notepad or another text editor, add the following to the top of the **server.js** file of the application:</span></span>

```javascript
var azure = require('azure');
```

### <a name="set-up-an-azure-service-bus-connection"></a><span data-ttu-id="f4f06-121">Bir Azure hizmet veri yolu bağlantı kurma</span><span class="sxs-lookup"><span data-stu-id="f4f06-121">Set up an Azure Service Bus connection</span></span>
<span data-ttu-id="f4f06-122">Ortam değişkeni Azure modül okur `AZURE_SERVICEBUS_CONNECTION_STRING` Service Bus hizmetine bağlanmak için gerekli bilgileri elde edilir.</span><span class="sxs-lookup"><span data-stu-id="f4f06-122">The Azure module reads the environment variable `AZURE_SERVICEBUS_CONNECTION_STRING` to obtain information required to connect to Service Bus.</span></span> <span data-ttu-id="f4f06-123">Bu ortam değişkenini ayarlanmamışsa çağrılırken hesap bilgileri belirtmelisiniz `createServiceBusService`.</span><span class="sxs-lookup"><span data-stu-id="f4f06-123">If this environment variable is not set, you must specify the account information when calling `createServiceBusService`.</span></span>

<span data-ttu-id="f4f06-124">Azure bulut hizmeti için bir yapılandırma dosyasında ortam değişkenlerini ayarlama örneği için bkz: [depolama Node.js bulut hizmetiyle][Node.js Cloud Service with Storage].</span><span class="sxs-lookup"><span data-stu-id="f4f06-124">For an example of setting the environment variables in a configuration file for an Azure Cloud Service, see [Node.js Cloud Service with Storage][Node.js Cloud Service with Storage].</span></span>

<span data-ttu-id="f4f06-125">Ortam değişkenlerini ayarlama örnek için [Azure portal] [ Azure portal] bir Azure Web sitesi için bkz: [Node.js Web uygulaması depolama ile] [ Node.js Web Application with Storage].</span><span class="sxs-lookup"><span data-stu-id="f4f06-125">For an example of setting the environment variables in the [Azure portal][Azure portal] for an Azure Website, see [Node.js Web Application with Storage][Node.js Web Application with Storage].</span></span>

## <a name="create-a-queue"></a><span data-ttu-id="f4f06-126">Bir kuyruk oluşturma</span><span class="sxs-lookup"><span data-stu-id="f4f06-126">Create a queue</span></span>
<span data-ttu-id="f4f06-127">**ServiceBusService** nesnesi ile Service Bus kuyruklarını çalışmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="f4f06-127">The **ServiceBusService** object enables you to work with Service Bus queues.</span></span> <span data-ttu-id="f4f06-128">Aşağıdaki kod oluşturur bir **ServiceBusService** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="f4f06-128">The following code creates a **ServiceBusService** object.</span></span> <span data-ttu-id="f4f06-129">Üst kısmına ekleyin **server.js** Azure modülü içeri aktarmak için deyimi sonra dosyayı:</span><span class="sxs-lookup"><span data-stu-id="f4f06-129">Add it near the top of the **server.js** file, after the statement to import the Azure module:</span></span>

```javascript
var serviceBusService = azure.createServiceBusService();
```

<span data-ttu-id="f4f06-130">Çağırarak `createQueueIfNotExists` üzerinde **ServiceBusService** nesnesi, (varsa) belirtilen sırada döndürülür veya belirtilen ada sahip yeni bir sıra oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="f4f06-130">By calling `createQueueIfNotExists` on the **ServiceBusService** object, the specified queue is returned (if it exists), or a new queue with the specified name is created.</span></span> <span data-ttu-id="f4f06-131">Aşağıdaki kod `createQueueIfNotExists` oluşturmak veya adlı kuyruğuna bağlanmak için `myqueue`:</span><span class="sxs-lookup"><span data-stu-id="f4f06-131">The following code uses `createQueueIfNotExists` to create or connect to the queue named `myqueue`:</span></span>

```javascript
serviceBusService.createQueueIfNotExists('myqueue', function(error){
    if(!error){
        // Queue exists
    }
});
```

<span data-ttu-id="f4f06-132">`createServiceBusService` Yöntemi de ileti zamanı dinamik veya en büyük sıra boyutu gibi varsayılan sırası ayarlarını geçersiz kılmanıza olanak sağlayan ek seçenekleri destekler.</span><span class="sxs-lookup"><span data-stu-id="f4f06-132">The `createServiceBusService` method also supports additional options, which enable you to override default queue settings such as message time to live or maximum queue size.</span></span> <span data-ttu-id="f4f06-133">Aşağıdaki örnek en büyük sıra boyutu 5 GB ve bir süre için 1 dakika (TTL) değerini Canlı ayarlar:</span><span class="sxs-lookup"><span data-stu-id="f4f06-133">The following example sets the maximum queue size to 5 GB, and a time to live (TTL) value of 1 minute:</span></span>

```javascript
var queueOptions = {
      MaxSizeInMegabytes: '5120',
      DefaultMessageTimeToLive: 'PT1M'
    };

serviceBusService.createQueueIfNotExists('myqueue', queueOptions, function(error){
    if(!error){
        // Queue exists
    }
});
```

### <a name="filters"></a><span data-ttu-id="f4f06-134">Filtreler</span><span class="sxs-lookup"><span data-stu-id="f4f06-134">Filters</span></span>
<span data-ttu-id="f4f06-135">İsteğe bağlı filtreleme işlemleri kullanarak gerçekleştirilen işlemler için uygulanabilir **ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="f4f06-135">Optional filtering operations can be applied to operations performed using **ServiceBusService**.</span></span> <span data-ttu-id="f4f06-136">İşlemleri filtreleme içerebilir günlüğe kaydetme, otomatik olarak yeniden deneniyor, vs. İmzalı bir yöntem uygulayan nesneler filtreleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="f4f06-136">Filtering operations can include logging, automatically retrying, etc. Filters are objects that implement a method with the signature:</span></span>

```javascript
function handle (requestOptions, next)
```

<span data-ttu-id="f4f06-137">Ön işleme isteği seçenekleri yaptıktan sonra yöntemini çağırmalı `next`, bir geri çağırma aşağıdaki imzayla geçirme:</span><span class="sxs-lookup"><span data-stu-id="f4f06-137">After doing its pre-processing on the request options, the method must call `next`, passing a callback with the following signature:</span></span>

```javascript
function (returnObject, finalCallback, next)
```

<span data-ttu-id="f4f06-138">İşleme sonra bu geri çağırma `returnObject` (yanıt istek sunucuya), geri çağırma ya da çağırmanız gerekir `next` diğer filtreleri işlemeye devam et veya yalnızca çağrılacak varsa `finalCallback`, hizmet sona erer çağırma.</span><span class="sxs-lookup"><span data-stu-id="f4f06-138">In this callback, and after processing the `returnObject` (the response from the request to the server), the callback must either invoke `next` if it exists to continue processing other filters, or simply invoke `finalCallback`, which ends the service invocation.</span></span>

<span data-ttu-id="f4f06-139">Yeniden deneme mantığını uygulaması iki filtre Node.js için Azure SDK'sı ile birlikte `ExponentialRetryPolicyFilter` ve `LinearRetryPolicyFilter`.</span><span class="sxs-lookup"><span data-stu-id="f4f06-139">Two filters that implement retry logic are included with the Azure SDK for Node.js, `ExponentialRetryPolicyFilter` and `LinearRetryPolicyFilter`.</span></span> <span data-ttu-id="f4f06-140">Aşağıdaki kod oluşturur bir `ServiceBusService` kullanan nesneyi `ExponentialRetryPolicyFilter`:</span><span class="sxs-lookup"><span data-stu-id="f4f06-140">The following code creates a `ServiceBusService` object that uses the `ExponentialRetryPolicyFilter`:</span></span>

```javascript
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var serviceBusService = azure.createServiceBusService().withFilter(retryOperations);
```

## <a name="send-messages-to-a-queue"></a><span data-ttu-id="f4f06-141">Kuyruğa ileti gönderme</span><span class="sxs-lookup"><span data-stu-id="f4f06-141">Send messages to a queue</span></span>
<span data-ttu-id="f4f06-142">Uygulama çağrılarınızı bir Service Bus kuyruğuna bir ileti göndermek için `sendQueueMessage` yöntemi **ServiceBusService** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="f4f06-142">To send a message to a Service Bus queue, your application calls the `sendQueueMessage` method on the **ServiceBusService** object.</span></span> <span data-ttu-id="f4f06-143">İletileri gönderilen (ve öğesinden alınan) hizmet kuyruklar veri yolu **BrokeredMessage** nesneleri ve bir standart özellikler kümesi sahip (gibi **etiket** ve **TimeToLive**), Özel uygulamaya özgü özellikler ve rastgele uygulama verileri gövdesi tutmak için kullanılan sözlüğü.</span><span class="sxs-lookup"><span data-stu-id="f4f06-143">Messages sent to (and received from) Service Bus queues are **BrokeredMessage** objects, and have a set of standard properties (such as **Label** and **TimeToLive**), a dictionary that is used to hold custom application-specific properties, and a body of arbitrary application data.</span></span> <span data-ttu-id="f4f06-144">Bir uygulama, iletisi olarak bir dize geçirerek ileti gövdesini ayarlayabilir.</span><span class="sxs-lookup"><span data-stu-id="f4f06-144">An application can set the body of the message by passing a string as the message.</span></span> <span data-ttu-id="f4f06-145">Gerekli tüm standart özellikleri varsayılan değerlerle doldurulur.</span><span class="sxs-lookup"><span data-stu-id="f4f06-145">Any required standard properties are populated with default values.</span></span>

<span data-ttu-id="f4f06-146">Aşağıdaki örnek adlı sırasına sınama iletisi göndermek nasıl gösterir `myqueue` kullanarak `sendQueueMessage`:</span><span class="sxs-lookup"><span data-stu-id="f4f06-146">The following example demonstrates how to send a test message to the queue named `myqueue` using `sendQueueMessage`:</span></span>

```javascript
var message = {
    body: 'Test message',
    customProperties: {
        testproperty: 'TestValue'
    }};
serviceBusService.sendQueueMessage('myqueue', message, function(error){
    if(!error){
        // message sent
    }
});
```

<span data-ttu-id="f4f06-147">Service Bus kuyrukları, [Standart katmanda](service-bus-premium-messaging.md) maksimum 256 KB ve [Premium katmanda](service-bus-premium-messaging.md) maksimum 1 MB ileti boyutunu destekler.</span><span class="sxs-lookup"><span data-stu-id="f4f06-147">Service Bus queues support a maximum message size of 256 KB in the [Standard tier](service-bus-premium-messaging.md) and 1 MB in the [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="f4f06-148">Standart ve özel uygulama özelliklerini içeren üst bilginin maksimum dosya boyutu 64 KB olabilir.</span><span class="sxs-lookup"><span data-stu-id="f4f06-148">The header, which includes the standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="f4f06-149">Kuyrukta tutulan ileti sayısına ilişkin bir sınır yoktur ancak kuyruk tarafından tutulan iletilerin toplam boyutu için uç sınır vardır.</span><span class="sxs-lookup"><span data-stu-id="f4f06-149">There is no limit on the number of messages held in a queue but there is a cap on the total size of the messages held by a queue.</span></span> <span data-ttu-id="f4f06-150">Bu kuyruk boyutu, üst sınır 5 GB olacak şekilde oluşturulma zamanında belirlenir.</span><span class="sxs-lookup"><span data-stu-id="f4f06-150">This queue size is defined at creation time, with an upper limit of 5 GB.</span></span> <span data-ttu-id="f4f06-151">Kotalar hakkında daha fazla bilgi için bkz: [Service Bus kotaları][Service Bus quotas].</span><span class="sxs-lookup"><span data-stu-id="f4f06-151">For more information about quotas, see [Service Bus quotas][Service Bus quotas].</span></span>

## <a name="receive-messages-from-a-queue"></a><span data-ttu-id="f4f06-152">Kuyruktan ileti alma</span><span class="sxs-lookup"><span data-stu-id="f4f06-152">Receive messages from a queue</span></span>
<span data-ttu-id="f4f06-153">İletileri kullanarak bir Sıraya alınan `receiveQueueMessage` yöntemi **ServiceBusService** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="f4f06-153">Messages are received from a queue using the `receiveQueueMessage` method on the **ServiceBusService** object.</span></span> <span data-ttu-id="f4f06-154">Varsayılan olarak, bunlar okurken iletiler sıradan silinir; Ancak, (Özet) okuma ve iletiyi sıradan isteğe bağlı parametresi ayarlanarak silmeden kilitlemek `isPeekLock` için **doğru**.</span><span class="sxs-lookup"><span data-stu-id="f4f06-154">By default, messages are deleted from the queue as they are read; however, you can read (peek) and lock the message without deleting it from the queue by setting the optional parameter `isPeekLock` to **true**.</span></span>

<span data-ttu-id="f4f06-155">Okuma ve ileti alma işleminin bir parçası olarak silme varsayılan davranışı en basit modeldir ve uygulamanın hata oluştuğunda bir iletiyi işlemeyi değil dayanabileceği senaryoları için en iyi şekilde çalışır.</span><span class="sxs-lookup"><span data-stu-id="f4f06-155">The default behavior of reading and deleting the message as part of the receive operation is the simplest model, and works best for scenarios in which an application can tolerate not processing a message in the event of a failure.</span></span> <span data-ttu-id="f4f06-156">Bu durumu daha iyi anlamak için müşterinin bir alma isteği bildirdiğini ve bu isteğin işlenmeden çöktüğünü varsayın.</span><span class="sxs-lookup"><span data-stu-id="f4f06-156">To understand this, consider a scenario in which the consumer issues the receive request and then crashes before processing it.</span></span> <span data-ttu-id="f4f06-157">Service Bus iletiyi kullanılıyor olarak işaretlenmiş nedeniyle uygulama yeniden başlatılıp iletileri tekrar kullanmaya başladığında, sonra da çökmenin öncesinde kullanılan iletiyi atlamış olur.</span><span class="sxs-lookup"><span data-stu-id="f4f06-157">Because Service Bus will have marked the message as being consumed, then when the application restarts and begins consuming messages again, it will have missed the message that was consumed prior to the crash.</span></span>

<span data-ttu-id="f4f06-158">Varsa `isPeekLock` parametrenin ayarlanmış **doğru**, alma, iletilere veremeyen uygulamaları desteklemenin mümkün kılar bir iki aşamalı işlemi haline gelir.</span><span class="sxs-lookup"><span data-stu-id="f4f06-158">If the `isPeekLock` parameter is set to **true**, the receive becomes a two stage operation, which makes it possible to support applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="f4f06-159">Service Bus bir istek aldığında bir sonraki kullanılacak iletiyi bulur, diğer tüketicilerin bu iletiyi almasını engellemek için kilitler ve ardından uygulamaya döndürür.</span><span class="sxs-lookup"><span data-stu-id="f4f06-159">When Service Bus receives a request, it finds the next message to be consumed, locks it to prevent other consumers receiving it, and then returns it to the application.</span></span> <span data-ttu-id="f4f06-160">Uygulama iletiyi işlemeyi tamamladıktan sonra (veya sonra işlemek için depoladıktan sonra), çağırarak alma işleminin ikinci aşamasını tamamlar `deleteMessage` yöntemi ve parametre olarak silinecek ileti sağlama.</span><span class="sxs-lookup"><span data-stu-id="f4f06-160">After the application finishes processing the message (or stores it reliably for future processing), it completes the second stage of the receive process by calling `deleteMessage` method and providing the message to be deleted as a parameter.</span></span> <span data-ttu-id="f4f06-161">`deleteMessage` Yöntemi iletiyi kullanılıyor olarak işaretler ve kuyruktan kaldırır.</span><span class="sxs-lookup"><span data-stu-id="f4f06-161">The `deleteMessage` method marks the message as being consumed and removes it from the queue.</span></span>

<span data-ttu-id="f4f06-162">Aşağıdaki örnek, kullanarak iletileri almak ve işlemek gösterilmiştir `receiveQueueMessage`.</span><span class="sxs-lookup"><span data-stu-id="f4f06-162">The following example demonstrates how to receive and process messages using `receiveQueueMessage`.</span></span> <span data-ttu-id="f4f06-163">Örnek ilk alır ve bir iletiyi siler ve kullanarak bir ileti alır `isPeekLock` kümesine **true**, iletiyi kullanarak siler `deleteMessage`:</span><span class="sxs-lookup"><span data-stu-id="f4f06-163">The example first receives and deletes a message, and then receives a message using `isPeekLock` set to **true**, then deletes the message using `deleteMessage`:</span></span>

```javascript
serviceBusService.receiveQueueMessage('myqueue', function(error, receivedMessage){
    if(!error){
        // Message received and deleted
    }
});
serviceBusService.receiveQueueMessage('myqueue', { isPeekLock: true }, function(error, lockedMessage){
    if(!error){
        // Message received and locked
        serviceBusService.deleteMessage(lockedMessage, function (deleteError){
            if(!deleteError){
                // Message deleted
            }
        });
    }
});
```

## <a name="how-to-handle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="f4f06-164">Uygulama çökmelerini ve okunmayan iletileri giderme</span><span class="sxs-lookup"><span data-stu-id="f4f06-164">How to handle application crashes and unreadable messages</span></span>
<span data-ttu-id="f4f06-165">Service Bus, uygulamanızda gerçekleşen hataları veya ileti işlenirken oluşan zorlukları rahat bir şekilde ortadan kaldırmanıza yardımcı olmak için işlevsellik sağlar.</span><span class="sxs-lookup"><span data-stu-id="f4f06-165">Service Bus provides functionality to help you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="f4f06-166">Alıcı uygulamanın iletiyi herhangi bir nedenden dolayı işleyemedi sonra işleyememesi `unlockMessage` yöntemi **ServiceBusService** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="f4f06-166">If a receiver application is unable to process the message for some reason, then it can call the `unlockMessage` method on the **ServiceBusService** object.</span></span> <span data-ttu-id="f4f06-167">Bu, Service Bus hizmetinin Kuyruktaki iletinin kilidini açmasına ve iletiyi aynı veya başka bir kullanıcı uygulama tarafından tekrar alınabilir hale getirmesine neden olur.</span><span class="sxs-lookup"><span data-stu-id="f4f06-167">This will cause Service Bus to unlock the message within the queue and make it available to be received again, either by the same consuming application or by another consuming application.</span></span>

<span data-ttu-id="f4f06-168">Ayrıca kuyrukta kilitlenen iletiye ilişkin bir zaman aşımı vardır ve uygulama önce iletiyi işleyemezse (örneğin, uygulama çökerse) Service Bus otomatik olarak iletinin kilidini açmak ve onu kilit zaman aşımı dolmadan yeniden alınabilmesi kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="f4f06-168">There is also a timeout associated with a message locked within the queue, and if the application fails to process the message before the lock timeout expires (e.g., if the application crashes), then Service Bus will unlock the message automatically and make it available to be received again.</span></span>

<span data-ttu-id="f4f06-169">Uygulama iletiyi ancak önce çökmesi durumunda, `deleteMessage` yöntemi çağrıldıktan sonra yeniden başlatıldığında ileti uygulamaya tekrar teslim edilir.</span><span class="sxs-lookup"><span data-stu-id="f4f06-169">In the event that the application crashes after processing the message but before the `deleteMessage` method is called, then the message will be redelivered to the application when it restarts.</span></span> <span data-ttu-id="f4f06-170">Bu genellikle adlandırılır *en az bir kez işleme*, diğer bir deyişle, her ileti en az bir kez işlenir ancak belirli durumlarda aynı ileti yeniden teslim.</span><span class="sxs-lookup"><span data-stu-id="f4f06-170">This is often called *At Least Once Processing*, that is, each message will be processed at least once but in certain situations the same message may be redelivered.</span></span> <span data-ttu-id="f4f06-171">Senaryo yinelenen işlemeyi kabul etmiyorsa yinelenen ileti teslimine izin vermek için uygulama geliştiricilerin uygulamaya ilave bir mantık eklemesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="f4f06-171">If the scenario cannot tolerate duplicate processing, then application developers should add additional logic to their application to handle duplicate message delivery.</span></span> <span data-ttu-id="f4f06-172">Bu genellikle kullanılarak elde edilen **MessageID** özelliğini iletinin teslimat denemelerinde.</span><span class="sxs-lookup"><span data-stu-id="f4f06-172">This is often achieved using the **MessageId** property of the message, which will remain constant across delivery attempts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f4f06-173">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f4f06-173">Next steps</span></span>
<span data-ttu-id="f4f06-174">Kuyruklar hakkında daha fazla bilgi edinmek için aşağıdaki kaynaklara bakın.</span><span class="sxs-lookup"><span data-stu-id="f4f06-174">To learn more about queues, see the following resources.</span></span>

* <span data-ttu-id="f4f06-175">[Kuyruklar, konu başlıkları ve abonelikler][Queues, topics, and subscriptions]</span><span class="sxs-lookup"><span data-stu-id="f4f06-175">[Queues, topics, and subscriptions][Queues, topics, and subscriptions]</span></span>
* <span data-ttu-id="f4f06-176">[Düğümü için Azure SDK] [ Azure SDK for Node] github'daki</span><span class="sxs-lookup"><span data-stu-id="f4f06-176">[Azure SDK for Node][Azure SDK for Node] repository on GitHub</span></span>
* [<span data-ttu-id="f4f06-177">Node.js Geliştirici Merkezi</span><span class="sxs-lookup"><span data-stu-id="f4f06-177">Node.js Developer Center</span></span>](https://azure.microsoft.com/develop/nodejs/)

[Azure SDK for Node]: https://github.com/Azure/azure-sdk-for-node
[Azure portal]: https://portal.azure.com

[Node.js Cloud Service]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[Create and deploy a Node.js application to an Azure Website]: ../app-service-web/app-service-web-get-started-nodejs.md
[Node.js Cloud Service with Storage]:../cosmos-db/table-storage-cloud-service-nodejs.md
[Node.js Web Application with Storage]:../cosmos-db/table-storage-how-to-use-nodejs.md
[Service Bus quotas]: service-bus-quotas.md
