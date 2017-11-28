---
title: "aaaHow toouse Service Bus kuyrukları Node.js içinde | Microsoft Docs"
description: "Hizmet veri yolu toouse Azure'da bir Node.js uygulamasını nasıl kuyruklar öğrenin."
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
ms.openlocfilehash: c55354b2061c41aba1093cc3f12ce2a1bc37a3cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-queues-with-nodejs"></a><span data-ttu-id="3a03f-103">Node.js ile nasıl toouse Service Bus kuyrukları</span><span class="sxs-lookup"><span data-stu-id="3a03f-103">How toouse Service Bus queues with Node.js</span></span>

[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

<span data-ttu-id="3a03f-104">Bu makalede, Node.js ile nasıl toouse Service Bus kuyrukları açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="3a03f-104">This article describes how toouse Service Bus queues with Node.js.</span></span> <span data-ttu-id="3a03f-105">Merhaba örnekler JavaScript'te yazılmış ve hello Node.js Azure modülü kullanın.</span><span class="sxs-lookup"><span data-stu-id="3a03f-105">hello samples are written in JavaScript and use hello Node.js Azure module.</span></span> <span data-ttu-id="3a03f-106">Merhaba kapsanan senaryolar dahil **sıra oluşturma**, **ileti gönderme ve alma**, ve **sıraları silme**.</span><span class="sxs-lookup"><span data-stu-id="3a03f-106">hello scenarios covered include **creating queues**, **sending and receiving messages**, and **deleting queues**.</span></span> <span data-ttu-id="3a03f-107">Merhaba kuyruklar hakkında daha fazla bilgi için bkz: [sonraki adımlar](#next-steps) bölümü.</span><span class="sxs-lookup"><span data-stu-id="3a03f-107">For more information on queues, see hello [Next steps](#next-steps) section.</span></span>

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="create-a-nodejs-application"></a><span data-ttu-id="3a03f-108">Node.js uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="3a03f-108">Create a Node.js application</span></span>
<span data-ttu-id="3a03f-109">Boş bir Node.js uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="3a03f-109">Create a blank Node.js application.</span></span> <span data-ttu-id="3a03f-110">Yönergeler için toocreate bir Node.js uygulaması bkz [oluşturma ve bir Node.js uygulaması tooan Azure Web sitesi dağıtma][Create and deploy a Node.js application tooan Azure Website], veya [Node.js bulut hizmeti] [ Node.js Cloud Service] Windows PowerShell kullanarak.</span><span class="sxs-lookup"><span data-stu-id="3a03f-110">For instructions on how toocreate a Node.js application, see [Create and deploy a Node.js application tooan Azure Website][Create and deploy a Node.js application tooan Azure Website], or [Node.js Cloud Service][Node.js Cloud Service] using Windows PowerShell.</span></span>

## <a name="configure-your-application-toouse-service-bus"></a><span data-ttu-id="3a03f-111">Uygulama toouse Service Bus yapılandırın</span><span class="sxs-lookup"><span data-stu-id="3a03f-111">Configure your application toouse Service Bus</span></span>
<span data-ttu-id="3a03f-112">toouse Azure Service Bus, indirin ve hello Node.js Azure paketini kullanın.</span><span class="sxs-lookup"><span data-stu-id="3a03f-112">toouse Azure Service Bus, download and use hello Node.js Azure package.</span></span> <span data-ttu-id="3a03f-113">Bu paket hello Service Bus REST Hizmetleri ile iletişim kitaplıkları kümesi içerir.</span><span class="sxs-lookup"><span data-stu-id="3a03f-113">This package includes a set of libraries that communicate with hello Service Bus REST services.</span></span>

### <a name="use-node-package-manager-npm-tooobtain-hello-package"></a><span data-ttu-id="3a03f-114">Düğüm paketi Yöneticisi (NPM) tooobtain hello paketini kullanın</span><span class="sxs-lookup"><span data-stu-id="3a03f-114">Use Node Package Manager (NPM) tooobtain hello package</span></span>
1. <span data-ttu-id="3a03f-115">Kullanım hello **Node.js için Windows PowerShell** komut penceresinde toonavigate toohello **c:\\düğümü\\sbqueues\\WebRole1** içinde oluşturduğunuz klasörü, örnek uygulama.</span><span class="sxs-lookup"><span data-stu-id="3a03f-115">Use hello **Windows PowerShell for Node.js** command window toonavigate toohello **c:\\node\\sbqueues\\WebRole1** folder in which you created your sample application.</span></span>
2. <span data-ttu-id="3a03f-116">Tür **npm yükleme azure** hello komut penceresinde, neden çıktı benzer toohello aşağıdakileri:</span><span class="sxs-lookup"><span data-stu-id="3a03f-116">Type **npm install azure** in hello command window, which should result in output similar toohello following:</span></span>

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
3. <span data-ttu-id="3a03f-117">Merhaba el ile çalıştırabilirsiniz **ls** komutu tooverify, bir **node_modules** klasörü oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="3a03f-117">You can manually run hello **ls** command tooverify that a **node_modules** folder was created.</span></span> <span data-ttu-id="3a03f-118">Bu klasör Bul hello içinde **azure** tooaccess Service Bus kuyruklarını ihtiyacınız hello kitaplıklarını içeren paket.</span><span class="sxs-lookup"><span data-stu-id="3a03f-118">Inside that folder find hello **azure** package, which contains hello libraries you need tooaccess Service Bus queues.</span></span>

### <a name="import-hello-module"></a><span data-ttu-id="3a03f-119">İçeri aktarma hello Modülü</span><span class="sxs-lookup"><span data-stu-id="3a03f-119">Import hello module</span></span>
<span data-ttu-id="3a03f-120">Not Defteri'nde veya başka bir metin düzenleyicisi kullanarak eklemek hello toohello üstündeki aşağıdaki hello **server.js** hello uygulama dosyası:</span><span class="sxs-lookup"><span data-stu-id="3a03f-120">Using Notepad or another text editor, add hello following toohello top of hello **server.js** file of hello application:</span></span>

```javascript
var azure = require('azure');
```

### <a name="set-up-an-azure-service-bus-connection"></a><span data-ttu-id="3a03f-121">Bir Azure hizmet veri yolu bağlantı kurma</span><span class="sxs-lookup"><span data-stu-id="3a03f-121">Set up an Azure Service Bus connection</span></span>
<span data-ttu-id="3a03f-122">Hello Azure modül okur hello ortam değişkeni `AZURE_SERVICEBUS_CONNECTION_STRING` tooobtain bilgi tooconnect tooService veri yolu gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="3a03f-122">hello Azure module reads hello environment variable `AZURE_SERVICEBUS_CONNECTION_STRING` tooobtain information required tooconnect tooService Bus.</span></span> <span data-ttu-id="3a03f-123">Bu ortam değişkenini ayarlanmamışsa çağrılırken hello hesap bilgileri belirtmelisiniz `createServiceBusService`.</span><span class="sxs-lookup"><span data-stu-id="3a03f-123">If this environment variable is not set, you must specify hello account information when calling `createServiceBusService`.</span></span>

<span data-ttu-id="3a03f-124">Azure bulut hizmeti için yapılandırma dosyasında hello ortam değişkenlerini ayarlama örneği için bkz: [depolama Node.js bulut hizmetiyle][Node.js Cloud Service with Storage].</span><span class="sxs-lookup"><span data-stu-id="3a03f-124">For an example of setting hello environment variables in a configuration file for an Azure Cloud Service, see [Node.js Cloud Service with Storage][Node.js Cloud Service with Storage].</span></span>

<span data-ttu-id="3a03f-125">Hello hello ortam değişkenlerini ayarlama örneği için [Azure portal] [ Azure portal] bir Azure Web sitesi için bkz: [Node.js Web uygulaması depolama ile] [ Node.js Web Application with Storage].</span><span class="sxs-lookup"><span data-stu-id="3a03f-125">For an example of setting hello environment variables in hello [Azure portal][Azure portal] for an Azure Website, see [Node.js Web Application with Storage][Node.js Web Application with Storage].</span></span>

## <a name="create-a-queue"></a><span data-ttu-id="3a03f-126">Bir kuyruk oluşturma</span><span class="sxs-lookup"><span data-stu-id="3a03f-126">Create a queue</span></span>
<span data-ttu-id="3a03f-127">Merhaba **ServiceBusService** nesnesi, Service Bus kuyrukları ile toowork sağlar.</span><span class="sxs-lookup"><span data-stu-id="3a03f-127">hello **ServiceBusService** object enables you toowork with Service Bus queues.</span></span> <span data-ttu-id="3a03f-128">Merhaba aşağıdaki kod oluşturur bir **ServiceBusService** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="3a03f-128">hello following code creates a **ServiceBusService** object.</span></span> <span data-ttu-id="3a03f-129">Merhaba hello yukarıya yakın eklemek **server.js** hello deyimi tooimport hello Azure modülü sonra dosyayı:</span><span class="sxs-lookup"><span data-stu-id="3a03f-129">Add it near hello top of hello **server.js** file, after hello statement tooimport hello Azure module:</span></span>

```javascript
var serviceBusService = azure.createServiceBusService();
```

<span data-ttu-id="3a03f-130">Çağırarak `createQueueIfNotExists` hello üzerinde **ServiceBusService** nesnesi, hello belirtilen sıra döndürülür (varsa) veya hello belirtilen ada sahip yeni bir sıra oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="3a03f-130">By calling `createQueueIfNotExists` on hello **ServiceBusService** object, hello specified queue is returned (if it exists), or a new queue with hello specified name is created.</span></span> <span data-ttu-id="3a03f-131">Merhaba aşağıdaki kod kullanır `createQueueIfNotExists` toocreate veya adlı toohello sıra bağlanmak `myqueue`:</span><span class="sxs-lookup"><span data-stu-id="3a03f-131">hello following code uses `createQueueIfNotExists` toocreate or connect toohello queue named `myqueue`:</span></span>

```javascript
serviceBusService.createQueueIfNotExists('myqueue', function(error){
    if(!error){
        // Queue exists
    }
});
```

<span data-ttu-id="3a03f-132">Merhaba `createServiceBusService` yöntemi de ileti zaman toolive veya en büyük sıra boyutu gibi toooverride varsayılan sıra ayarları etkinleştirmek ek seçenekleri destekler.</span><span class="sxs-lookup"><span data-stu-id="3a03f-132">hello `createServiceBusService` method also supports additional options, which enable you toooverride default queue settings such as message time toolive or maximum queue size.</span></span> <span data-ttu-id="3a03f-133">Merhaba aşağıdaki örnek hello en büyük sıra boyutu too5 GB ve bir süre toolive (TTL) değerini 1 dakika ayarlar:</span><span class="sxs-lookup"><span data-stu-id="3a03f-133">hello following example sets hello maximum queue size too5 GB, and a time toolive (TTL) value of 1 minute:</span></span>

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

### <a name="filters"></a><span data-ttu-id="3a03f-134">Filtreler</span><span class="sxs-lookup"><span data-stu-id="3a03f-134">Filters</span></span>
<span data-ttu-id="3a03f-135">İsteğe bağlı filtreleme operations kullanılarak gerçekleştirilen uygulanan toooperations olabilir **ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="3a03f-135">Optional filtering operations can be applied toooperations performed using **ServiceBusService**.</span></span> <span data-ttu-id="3a03f-136">İşlemleri filtreleme içerebilir günlüğe kaydetme, otomatik olarak yeniden deneniyor, vs. Filtreleri hello imza yöntemiyle uygulayan nesneler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="3a03f-136">Filtering operations can include logging, automatically retrying, etc. Filters are objects that implement a method with hello signature:</span></span>

```javascript
function handle (requestOptions, next)
```

<span data-ttu-id="3a03f-137">Ön işleme hello isteği seçenekleri yaptıktan sonra hello yöntemini çağırmalı `next`, bir geri çağırma imza aşağıdaki hello ile geçirme:</span><span class="sxs-lookup"><span data-stu-id="3a03f-137">After doing its pre-processing on hello request options, hello method must call `next`, passing a callback with hello following signature:</span></span>

```javascript
function (returnObject, finalCallback, next)
```

<span data-ttu-id="3a03f-138">İşleme hello sonra bu geri çağırma `returnObject` (Merhaba isteği toohello sunucudan yanıt hello) hello geri çağırma gerekir ya da çağırma `next` , diğer filtrelerle işleme toocontinue var veya yalnızca çağırma `finalCallback`, hangi sona erer Merhaba hizmet başlatma.</span><span class="sxs-lookup"><span data-stu-id="3a03f-138">In this callback, and after processing hello `returnObject` (hello response from hello request toohello server), hello callback must either invoke `next` if it exists toocontinue processing other filters, or simply invoke `finalCallback`, which ends hello service invocation.</span></span>

<span data-ttu-id="3a03f-139">Yeniden deneme mantığını uygulaması iki filtre hello Node.js için Azure SDK ile birlikte `ExponentialRetryPolicyFilter` ve `LinearRetryPolicyFilter`.</span><span class="sxs-lookup"><span data-stu-id="3a03f-139">Two filters that implement retry logic are included with hello Azure SDK for Node.js, `ExponentialRetryPolicyFilter` and `LinearRetryPolicyFilter`.</span></span> <span data-ttu-id="3a03f-140">Merhaba aşağıdaki kod oluşturur bir `ServiceBusService` hello kullanan nesneyi `ExponentialRetryPolicyFilter`:</span><span class="sxs-lookup"><span data-stu-id="3a03f-140">hello following code creates a `ServiceBusService` object that uses hello `ExponentialRetryPolicyFilter`:</span></span>

```javascript
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var serviceBusService = azure.createServiceBusService().withFilter(retryOperations);
```

## <a name="send-messages-tooa-queue"></a><span data-ttu-id="3a03f-141">İletileri tooa sırası Gönder</span><span class="sxs-lookup"><span data-stu-id="3a03f-141">Send messages tooa queue</span></span>
<span data-ttu-id="3a03f-142">ileti tooa Service Bus kuyruğuna toosend, uygulamanızın çağırır hello `sendQueueMessage` hello yöntemi **ServiceBusService** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="3a03f-142">toosend a message tooa Service Bus queue, your application calls hello `sendQueueMessage` method on hello **ServiceBusService** object.</span></span> <span data-ttu-id="3a03f-143">İletileri çok gönderilen (ve öğesinden alınan) hizmet kuyruklar veri yolu **BrokeredMessage** nesneleri ve bir standart özellikler kümesi sahip (gibi **etiket** ve **TimeToLive**), kullanılan toohold özel uygulamaya özgü özellikler ve rastgele uygulama verileri gövdesi sözlüğü.</span><span class="sxs-lookup"><span data-stu-id="3a03f-143">Messages sent too(and received from) Service Bus queues are **BrokeredMessage** objects, and have a set of standard properties (such as **Label** and **TimeToLive**), a dictionary that is used toohold custom application-specific properties, and a body of arbitrary application data.</span></span> <span data-ttu-id="3a03f-144">Bir uygulama, bir dize selamlama iletisine geçirerek hello hello ileti gövdesi ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3a03f-144">An application can set hello body of hello message by passing a string as hello message.</span></span> <span data-ttu-id="3a03f-145">Gerekli tüm standart özellikleri varsayılan değerlerle doldurulur.</span><span class="sxs-lookup"><span data-stu-id="3a03f-145">Any required standard properties are populated with default values.</span></span>

<span data-ttu-id="3a03f-146">Merhaba aşağıdaki örnekte nasıl toosend adlı bir sınama iletisi toohello sırası gösteren `myqueue` kullanarak `sendQueueMessage`:</span><span class="sxs-lookup"><span data-stu-id="3a03f-146">hello following example demonstrates how toosend a test message toohello queue named `myqueue` using `sendQueueMessage`:</span></span>

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

<span data-ttu-id="3a03f-147">Service Bus kuyruklarını destek maksimum ileti boyutu 256 KB hello [standart katmanı](service-bus-premium-messaging.md) hello 1 MB [Premium katmanı](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="3a03f-147">Service Bus queues support a maximum message size of 256 KB in hello [Standard tier](service-bus-premium-messaging.md) and 1 MB in hello [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="3a03f-148">Merhaba standart ve özel uygulama özelliklerini içeren hello üstbilgi en büyük boyutu 64 KB olabilir.</span><span class="sxs-lookup"><span data-stu-id="3a03f-148">hello header, which includes hello standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="3a03f-149">Merhaba bir kuyrukta tutulan ileti sayısına bir sınır yoktur ancak kuyruk tarafından tutulan hello iletilerin toplam boyutu hello bir sınır yoktur.</span><span class="sxs-lookup"><span data-stu-id="3a03f-149">There is no limit on hello number of messages held in a queue but there is a cap on hello total size of hello messages held by a queue.</span></span> <span data-ttu-id="3a03f-150">Bu kuyruk boyutu, üst sınır 5 GB olacak şekilde oluşturulma zamanında belirlenir.</span><span class="sxs-lookup"><span data-stu-id="3a03f-150">This queue size is defined at creation time, with an upper limit of 5 GB.</span></span> <span data-ttu-id="3a03f-151">Kotalar hakkında daha fazla bilgi için bkz: [Service Bus kotaları][Service Bus quotas].</span><span class="sxs-lookup"><span data-stu-id="3a03f-151">For more information about quotas, see [Service Bus quotas][Service Bus quotas].</span></span>

## <a name="receive-messages-from-a-queue"></a><span data-ttu-id="3a03f-152">Kuyruktan ileti alma</span><span class="sxs-lookup"><span data-stu-id="3a03f-152">Receive messages from a queue</span></span>
<span data-ttu-id="3a03f-153">İletileri hello kullanarak bir kuyruktan alınan `receiveQueueMessage` hello yöntemi **ServiceBusService** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="3a03f-153">Messages are received from a queue using hello `receiveQueueMessage` method on hello **ServiceBusService** object.</span></span> <span data-ttu-id="3a03f-154">Varsayılan olarak, bunlar okurken iletiler hello sıradan silinir; Ancak, (Özet) okuma ve kilitleme selamlama iletisine hello isteğe bağlı parametre ayarı tarafından hello sıradan silmeden `isPeekLock` çok**doğru**.</span><span class="sxs-lookup"><span data-stu-id="3a03f-154">By default, messages are deleted from hello queue as they are read; however, you can read (peek) and lock hello message without deleting it from hello queue by setting hello optional parameter `isPeekLock` too**true**.</span></span>

<span data-ttu-id="3a03f-155">Okuma varsayılan davranışını hello ve hello parçası işlemi aldıklarında hello iletisi siliniyor hello en basit modeldir ve uygulamanın bir hatanın hello Olay iletisinde işlenmiyor dayanabileceği senaryolarda en iyi şekilde çalışır.</span><span class="sxs-lookup"><span data-stu-id="3a03f-155">hello default behavior of reading and deleting hello message as part of hello receive operation is hello simplest model, and works best for scenarios in which an application can tolerate not processing a message in hello event of a failure.</span></span> <span data-ttu-id="3a03f-156">toounderstand Bu, hangi hello tüketici sorunları hello alma isteği bir senaryo düşünün ve işlemeden önce çöküyor.</span><span class="sxs-lookup"><span data-stu-id="3a03f-156">toounderstand this, consider a scenario in which hello consumer issues hello receive request and then crashes before processing it.</span></span> <span data-ttu-id="3a03f-157">Hizmet veri yolu selamlama iletisine hello uygulama yeniden başlatılıp iletileri tekrar kullanmaya başladığında olduğunda, ardından kullanılıyor olarak işaretlenmiş için onu olan hello iletiyi atlamış olur önceki toohello kilitlenme tüketilen.</span><span class="sxs-lookup"><span data-stu-id="3a03f-157">Because Service Bus will have marked hello message as being consumed, then when hello application restarts and begins consuming messages again, it will have missed hello message that was consumed prior toohello crash.</span></span>

<span data-ttu-id="3a03f-158">Merhaba, `isPeekLock` parametresi çok ayarlanırsa**true**, hello alma iletilere olası toosupport uygulamaları iki aşamalı işlemi olur.</span><span class="sxs-lookup"><span data-stu-id="3a03f-158">If hello `isPeekLock` parameter is set too**true**, hello receive becomes a two stage operation, which makes it possible toosupport applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="3a03f-159">Service Bus bir istek aldığında hello sonraki ileti toobe tüketilen, diğer tüketicilerin alırken tooprevent kilitler ve toohello uygulama döndürür bulur.</span><span class="sxs-lookup"><span data-stu-id="3a03f-159">When Service Bus receives a request, it finds hello next message toobe consumed, locks it tooprevent other consumers receiving it, and then returns it toohello application.</span></span> <span data-ttu-id="3a03f-160">Merhaba uygulaması hello iletiyi işlemeyi tamamladıktan sonra (veya sonra işlemek için depoladıktan sonra), hello hello ikinci aşamasını tamamlar çağırarak alma işleminin `deleteMessage` yöntemi ve parametre olarak silinmiş hello ileti toobe sağlama.</span><span class="sxs-lookup"><span data-stu-id="3a03f-160">After hello application finishes processing hello message (or stores it reliably for future processing), it completes hello second stage of hello receive process by calling `deleteMessage` method and providing hello message toobe deleted as a parameter.</span></span> <span data-ttu-id="3a03f-161">Merhaba `deleteMessage` yöntemi hello iletiyi kullanılıyor olarak işaretler ve hello kuyruktan kaldırır.</span><span class="sxs-lookup"><span data-stu-id="3a03f-161">hello `deleteMessage` method marks hello message as being consumed and removes it from hello queue.</span></span>

<span data-ttu-id="3a03f-162">Merhaba aşağıdaki örnekte nasıl tooreceive ve işlem iletileri kullanarak gösteren `receiveQueueMessage`.</span><span class="sxs-lookup"><span data-stu-id="3a03f-162">hello following example demonstrates how tooreceive and process messages using `receiveQueueMessage`.</span></span> <span data-ttu-id="3a03f-163">Merhaba örnek ilk alır ve bir iletiyi siler ve kullanarak bir ileti alır `isPeekLock` çok ayarlamak**true**, iletiyi kullanarak siler hello sonra `deleteMessage`:</span><span class="sxs-lookup"><span data-stu-id="3a03f-163">hello example first receives and deletes a message, and then receives a message using `isPeekLock` set too**true**, then deletes hello message using `deleteMessage`:</span></span>

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

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="3a03f-164">Nasıl toohandle uygulaması kilitlenir ve Okunmayan iletileri</span><span class="sxs-lookup"><span data-stu-id="3a03f-164">How toohandle application crashes and unreadable messages</span></span>
<span data-ttu-id="3a03f-165">Hizmet veri yolu, gerçekleşen hataları uygulama ya da ileti işlenirken zorlukları rahat işlevselliği toohelp sağlar.</span><span class="sxs-lookup"><span data-stu-id="3a03f-165">Service Bus provides functionality toohelp you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="3a03f-166">Alıcı uygulamanın kaydedemediği tooprocess Merhaba ileti herhangi bir nedenden dolayı ardından hello çağırabilirsiniz `unlockMessage` hello yöntemi **ServiceBusService** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="3a03f-166">If a receiver application is unable tooprocess hello message for some reason, then it can call hello `unlockMessage` method on hello **ServiceBusService** object.</span></span> <span data-ttu-id="3a03f-167">Bu hizmet veri yolu toounlock hello sıra içinde ileti neden ve yeniden alınan kullanılabilir toobe olun, ya da göre aynı uygulama veya başka bir kullanıcı uygulama tarafından tüketen hello.</span><span class="sxs-lookup"><span data-stu-id="3a03f-167">This will cause Service Bus toounlock the message within hello queue and make it available toobe received again, either by hello same consuming application or by another consuming application.</span></span>

<span data-ttu-id="3a03f-168">Ayrıca hello kuyrukta kilitlenen iletiye ilişkin bir zaman aşımı vardır ve hello tooprocess önce iletiyi hello hello uygulama başarısız olursa (örneğin, hello uygulama çökerse) Service Bus selamlama iletisine otomatik olarak kilitlenmeden kilit zaman aşımı dolmadan ve yeniden alınan kullanılabilir toobe yapın.</span><span class="sxs-lookup"><span data-stu-id="3a03f-168">There is also a timeout associated with a message locked within hello queue, and if hello application fails tooprocess hello message before hello lock timeout expires (e.g., if hello application crashes), then Service Bus will unlock hello message automatically and make it available toobe received again.</span></span>

<span data-ttu-id="3a03f-169">Merhaba ileti işlenirken sonra ancak hello önce uygulama hello olay Hello çöküyor `deleteMessage` yöntemi çağrıldıktan sonra başlatıldığında hello ileti yeniden teslim toohello uygulama olacaktır.</span><span class="sxs-lookup"><span data-stu-id="3a03f-169">In hello event that hello application crashes after processing hello message but before hello `deleteMessage` method is called, then hello message will be redelivered toohello application when it restarts.</span></span> <span data-ttu-id="3a03f-170">Bu genellikle adlandırılır *en az bir kez işleme*, diğer bir deyişle, her ileti en az bir kez işlenir ancak belirli durumlarda hello aynı ileti yeniden teslim.</span><span class="sxs-lookup"><span data-stu-id="3a03f-170">This is often called *At Least Once Processing*, that is, each message will be processed at least once but in certain situations hello same message may be redelivered.</span></span> <span data-ttu-id="3a03f-171">Merhaba senaryo yinelenen işlemeyi kabul etmiyorsa, uygulama geliştiricilerinin ek mantık tootheir uygulama toohandle yinelenen ileti teslimi eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="3a03f-171">If hello scenario cannot tolerate duplicate processing, then application developers should add additional logic tootheir application toohandle duplicate message delivery.</span></span> <span data-ttu-id="3a03f-172">Bu genellikle hello kullanılarak elde edilen **MessageID** teslimat denemelerinde hello iletinin özelliği.</span><span class="sxs-lookup"><span data-stu-id="3a03f-172">This is often achieved using hello **MessageId** property of hello message, which will remain constant across delivery attempts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3a03f-173">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3a03f-173">Next steps</span></span>
<span data-ttu-id="3a03f-174">Kuyruklar hakkında daha fazla toolearn kaynakları aşağıdaki hello bakın.</span><span class="sxs-lookup"><span data-stu-id="3a03f-174">toolearn more about queues, see hello following resources.</span></span>

* <span data-ttu-id="3a03f-175">[Kuyruklar, konu başlıkları ve abonelikler][Queues, topics, and subscriptions]</span><span class="sxs-lookup"><span data-stu-id="3a03f-175">[Queues, topics, and subscriptions][Queues, topics, and subscriptions]</span></span>
* <span data-ttu-id="3a03f-176">[Düğümü için Azure SDK] [ Azure SDK for Node] github'daki</span><span class="sxs-lookup"><span data-stu-id="3a03f-176">[Azure SDK for Node][Azure SDK for Node] repository on GitHub</span></span>
* [<span data-ttu-id="3a03f-177">Node.js Geliştirici Merkezi</span><span class="sxs-lookup"><span data-stu-id="3a03f-177">Node.js Developer Center</span></span>](https://azure.microsoft.com/develop/nodejs/)

[Azure SDK for Node]: https://github.com/Azure/azure-sdk-for-node
[Azure portal]: https://portal.azure.com

[Node.js Cloud Service]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[Create and deploy a Node.js application tooan Azure Website]: ../app-service-web/app-service-web-get-started-nodejs.md
[Node.js Cloud Service with Storage]:../cosmos-db/table-storage-cloud-service-nodejs.md
[Node.js Web Application with Storage]:../cosmos-db/table-storage-how-to-use-nodejs.md
[Service Bus quotas]: service-bus-quotas.md
