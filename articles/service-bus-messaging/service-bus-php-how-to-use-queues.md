---
title: "aaaHow toouse Service Bus kuyrukları ile PHP | Microsoft Docs"
description: "Azure'da nasıl toouse Service Bus kuyrukları öğrenin. PHP ile yazılan kod örnekleri."
services: service-bus-messaging
documentationcenter: php
author: sethmanheim
manager: timlt
editor: 
ms.assetid: e29c829b-44c5-4350-8f2e-39e0c380a9f2
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: 8cf233176029b679d172eaf713632087beca5e4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-queues-with-php"></a><span data-ttu-id="5e806-104">PHP ile nasıl toouse Service Bus kuyrukları</span><span class="sxs-lookup"><span data-stu-id="5e806-104">How toouse Service Bus queues with PHP</span></span>
[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

<span data-ttu-id="5e806-105">Bu kılavuz size nasıl gösterir toouse Service Bus kuyruklarını.</span><span class="sxs-lookup"><span data-stu-id="5e806-105">This guide shows you how toouse Service Bus queues.</span></span> <span data-ttu-id="5e806-106">Merhaba örnekler PHP ile yazılmıştır ve hello kullan [PHP için Azure SDK](../php-download-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="5e806-106">hello samples are written in PHP and use hello [Azure SDK for PHP](../php-download-sdk.md).</span></span> <span data-ttu-id="5e806-107">Merhaba kapsanan senaryolar dahil **sıra oluşturma**, **ileti gönderme ve alma**, ve **sıraları silme**.</span><span class="sxs-lookup"><span data-stu-id="5e806-107">hello scenarios covered include **creating queues**, **sending and receiving messages**, and **deleting queues**.</span></span>

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

## <a name="create-a-php-application"></a><span data-ttu-id="5e806-108">PHP uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="5e806-108">Create a PHP application</span></span>
<span data-ttu-id="5e806-109">Merhaba hello Azure Blob hizmete erişen bir PHP uygulaması oluşturmaya yönelik gereksinim, yalnızca hello hello sınıfların başvuran [PHP için Azure SDK](../php-download-sdk.md) gelen kodunuzu içinde.</span><span class="sxs-lookup"><span data-stu-id="5e806-109">hello only requirement for creating a PHP application that accesses hello Azure Blob service is hello referencing of classes in hello [Azure SDK for PHP](../php-download-sdk.md) from within your code.</span></span> <span data-ttu-id="5e806-110">Uygulama veya Notepad tüm geliştirme araçları toocreate kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5e806-110">You can use any development tools toocreate your application, or Notepad.</span></span>

> [!NOTE]
> <span data-ttu-id="5e806-111">PHP yüklemenizi de hello olmalıdır [OpenSSL uzantısı](http://php.net/openssl) yüklenir ve etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="5e806-111">Your PHP installation must also have hello [OpenSSL extension](http://php.net/openssl) installed and enabled.</span></span>
> 
> 

<span data-ttu-id="5e806-112">Bu kılavuzda, bir PHP uygulamanızda yerel olarak veya bir Azure web rolü, çalışan rolü veya Web sitesi içinde çalışan kodu çağrılabilir hizmet özelliklerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="5e806-112">In this guide, you will use service features which can be called from within a PHP application locally, or in code running within an Azure web role, worker role, or website.</span></span>

## <a name="get-hello-azure-client-libraries"></a><span data-ttu-id="5e806-113">Hello Azure istemci kitaplıkları Al</span><span class="sxs-lookup"><span data-stu-id="5e806-113">Get hello Azure client libraries</span></span>
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-toouse-service-bus"></a><span data-ttu-id="5e806-114">Uygulama toouse Service Bus yapılandırın</span><span class="sxs-lookup"><span data-stu-id="5e806-114">Configure your application toouse Service Bus</span></span>
<span data-ttu-id="5e806-115">toouse hello Service Bus kuyruğuna API'leri, hello aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="5e806-115">toouse hello Service Bus queue APIs, do hello following:</span></span>

1. <span data-ttu-id="5e806-116">Hello kullanarak başvuru hello otomatik yükleyici dosyasını [require_once] [ require_once] deyimi.</span><span class="sxs-lookup"><span data-stu-id="5e806-116">Reference hello autoloader file using hello [require_once][require_once] statement.</span></span>
2. <span data-ttu-id="5e806-117">Kullanabileceğinize sınıfları başvuru.</span><span class="sxs-lookup"><span data-stu-id="5e806-117">Reference any classes you might use.</span></span>

<span data-ttu-id="5e806-118">Merhaba aşağıdaki örnekte nasıl tooinclude hello otomatik Yükleyiciden dosya ve başvuru hello gösterir `ServicesBuilder` sınıfı.</span><span class="sxs-lookup"><span data-stu-id="5e806-118">hello following example shows how tooinclude hello autoloader file and reference hello `ServicesBuilder` class.</span></span>

> [!NOTE]
> <span data-ttu-id="5e806-119">Bu örnek (ve diğer örnekleri bu makalede) hello PHP istemci kitaplıkları oluşturucu aracılığıyla Azure yüklü olduğunu varsayar.</span><span class="sxs-lookup"><span data-stu-id="5e806-119">This example (and other examples in this article) assumes you have installed hello PHP Client Libraries for Azure via Composer.</span></span> <span data-ttu-id="5e806-120">El ile veya bir ARMUTLU paketi olarak hello kitaplıkları yüklediyseniz, hello başvurmalıdır **WindowsAzure.php** otomatik yükleyici dosyası.</span><span class="sxs-lookup"><span data-stu-id="5e806-120">If you installed hello libraries manually or as a PEAR package, you must reference hello **WindowsAzure.php** autoloader file.</span></span>
> 
> 

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

<span data-ttu-id="5e806-121">Merhaba aşağıdaki örnekte, hello `require_once` deyimi her zaman gösterilecek, ancak yalnızca hello sınıfları hello örnek tooexecute için gereken başvuru.</span><span class="sxs-lookup"><span data-stu-id="5e806-121">In hello examples below, hello `require_once` statement will always be shown, but only hello classes necessary for hello example tooexecute are referenced.</span></span>

## <a name="set-up-a-service-bus-connection"></a><span data-ttu-id="5e806-122">Hizmet veri yolu bağlantı kurma</span><span class="sxs-lookup"><span data-stu-id="5e806-122">Set up a Service Bus connection</span></span>
<span data-ttu-id="5e806-123">Service Bus istemci tooinstantiate, şu biçimde geçerli bir bağlantı dizesi ilk olması gerekir:</span><span class="sxs-lookup"><span data-stu-id="5e806-123">tooinstantiate a Service Bus client, you must first have a valid connection string in this format:</span></span>

```
Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]
```

<span data-ttu-id="5e806-124">Burada `Endpoint` genellikle hello biçimidir `[yourNamespace].servicebus.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="5e806-124">Where `Endpoint` is typically of hello format `[yourNamespace].servicebus.windows.net`.</span></span>

<span data-ttu-id="5e806-125">toocreate hello kullanmalıdır herhangi bir Azure hizmeti istemci `ServicesBuilder` sınıfı.</span><span class="sxs-lookup"><span data-stu-id="5e806-125">toocreate any Azure service client you must use hello `ServicesBuilder` class.</span></span> <span data-ttu-id="5e806-126">Şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="5e806-126">You can:</span></span>

* <span data-ttu-id="5e806-127">Merhaba bağlantı geçirmek doğrudan tooit dize.</span><span class="sxs-lookup"><span data-stu-id="5e806-127">Pass hello connection string directly tooit.</span></span>
* <span data-ttu-id="5e806-128">Kullanım hello **CloudConfigurationManager (CCM)** toocheck birden çok dış kaynaklardan hello bağlantı dizesi:</span><span class="sxs-lookup"><span data-stu-id="5e806-128">Use hello **CloudConfigurationManager (CCM)** toocheck multiple external sources for hello connection string:</span></span>
  * <span data-ttu-id="5e806-129">Bir dış kaynak - ortam değişkenleri için destek ile birlikte varsayılan olarak</span><span class="sxs-lookup"><span data-stu-id="5e806-129">By default it comes with support for one external source - environmental variables</span></span>
  * <span data-ttu-id="5e806-130">Merhaba genişleterek yeni kaynakları ekleyebilirsiniz `ConnectionStringSource` sınıfı</span><span class="sxs-lookup"><span data-stu-id="5e806-130">You can add new sources by extending hello `ConnectionStringSource` class</span></span>

<span data-ttu-id="5e806-131">Burada özetlenen hello örnekler için başlangıç bağlantı dizesi doğrudan geçirilir.</span><span class="sxs-lookup"><span data-stu-id="5e806-131">For hello examples outlined here, hello connection string is passed directly.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$connectionString = "Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]";

$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);
```

## <a name="create-a-queue"></a><span data-ttu-id="5e806-132">Bir kuyruk oluşturma</span><span class="sxs-lookup"><span data-stu-id="5e806-132">Create a queue</span></span>
<span data-ttu-id="5e806-133">Service Bus kuyruklarını hello aracılığıyla yönelik yönetim işlemlerini gerçekleştirebilirsiniz `ServiceBusRestProxy` sınıfı.</span><span class="sxs-lookup"><span data-stu-id="5e806-133">You can perform management operations for Service Bus queues via hello `ServiceBusRestProxy` class.</span></span> <span data-ttu-id="5e806-134">A `ServiceBusRestProxy` nesne hello oluşturulan `ServicesBuilder::createServiceBusService` Üreteç yöntemi hello belirteci izinleri toomanage yalıtan bir uygun bir bağlantı dizesi ile.</span><span class="sxs-lookup"><span data-stu-id="5e806-134">A `ServiceBusRestProxy` object is constructed via hello `ServicesBuilder::createServiceBusService` factory method with an appropriate connection string that encapsulates hello token permissions toomanage it.</span></span>

<span data-ttu-id="5e806-135">örnekte gösterildiği nasıl aşağıdaki hello tooinstantiate bir `ServiceBusRestProxy` ve arama `ServiceBusRestProxy->createQueue` toocreate adlandırılan bir kuyruğun `myqueue` içinde bir `MySBNamespace` hizmet ad alanı:</span><span class="sxs-lookup"><span data-stu-id="5e806-135">hello following example shows how tooinstantiate a `ServiceBusRestProxy` and call `ServiceBusRestProxy->createQueue` toocreate a queue named `myqueue` within a `MySBNamespace` service namespace:</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use WindowsAzure\Common\ServiceException;
use WindowsAzure\ServiceBus\Models\QueueInfo;

// Create Service Bus REST proxy.
$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);

try    {
    $queueInfo = new QueueInfo("myqueue");

    // Create queue.
    $serviceBusRestProxy->createQueue($queueInfo);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here: 
    // https://docs.microsoft.com/rest/api/storageservices/Common-REST-API-Error-Codes
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

> [!NOTE]
> <span data-ttu-id="5e806-136">Merhaba kullanabilirsiniz `listQueues` yöntemi `ServiceBusRestProxy` belirtilen ada sahip bir sıra içinde bir ad alanı zaten varsa toocheck nesneleri.</span><span class="sxs-lookup"><span data-stu-id="5e806-136">You can use hello `listQueues` method on `ServiceBusRestProxy` objects toocheck if a queue with a specified name already exists within a namespace.</span></span>
> 
> 

## <a name="send-messages-tooa-queue"></a><span data-ttu-id="5e806-137">İletileri tooa sırası Gönder</span><span class="sxs-lookup"><span data-stu-id="5e806-137">Send messages tooa queue</span></span>
<span data-ttu-id="5e806-138">ileti tooa Service Bus kuyruğuna toosend, uygulamanızın çağırır hello `ServiceBusRestProxy->sendQueueMessage` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="5e806-138">toosend a message tooa Service Bus queue, your application calls hello `ServiceBusRestProxy->sendQueueMessage` method.</span></span> <span data-ttu-id="5e806-139">kodun gösterdiği nasıl aşağıdaki hello toosend ileti toohello `myqueue` içinde daha önce oluşturduğunuz sıra `MySBNamespace` hizmet ad alanı.</span><span class="sxs-lookup"><span data-stu-id="5e806-139">hello following code shows how toosend a message toohello `myqueue` queue previously created within the `MySBNamespace` service namespace.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use WindowsAzure\Common\ServiceException;
use WindowsAzure\ServiceBus\Models\BrokeredMessage;

// Create Service Bus REST proxy.
$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);

try    {
    // Create message.
    $message = new BrokeredMessage();
    $message->setBody("my message");

    // Send message.
    $serviceBusRestProxy->sendQueueMessage("myqueue", $message);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here: 
    // https://docs.microsoft.com/rest/api/storageservices/Common-REST-API-Error-Codes
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

<span data-ttu-id="5e806-140">Service Bus kuyrukları çok gönderilen (ve öğesinden alınan) hello örneklerini iletileri [BrokeredMessage] [ BrokeredMessage] sınıfı.</span><span class="sxs-lookup"><span data-stu-id="5e806-140">Messages sent too(and received from ) Service Bus queues are instances of hello [BrokeredMessage][BrokeredMessage] class.</span></span> <span data-ttu-id="5e806-141">[BrokeredMessage] [ BrokeredMessage] nesnelerinin bir dizi standart yöntemleri ve kullanılan toohold özel uygulamaya özgü özellikler ve rastgele uygulama verileri gövdesi özellikleri vardır.</span><span class="sxs-lookup"><span data-stu-id="5e806-141">[BrokeredMessage][BrokeredMessage] objects have a set of standard methods and properties that are used toohold custom application-specific properties, and a body of arbitrary application data.</span></span>

<span data-ttu-id="5e806-142">Service Bus kuyruklarını destek maksimum ileti boyutu 256 KB hello [standart katmanı](service-bus-premium-messaging.md) hello 1 MB [Premium katmanı](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="5e806-142">Service Bus queues support a maximum message size of 256 KB in hello [Standard tier](service-bus-premium-messaging.md) and 1 MB in hello [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="5e806-143">Merhaba standart ve özel uygulama özelliklerini içeren hello üstbilgi en büyük boyutu 64 KB olabilir.</span><span class="sxs-lookup"><span data-stu-id="5e806-143">hello header, which includes hello standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="5e806-144">Merhaba bir kuyrukta tutulan ileti sayısına bir sınır yoktur ancak kuyruk tarafından tutulan hello iletilerin toplam boyutu hello bir sınır yoktur.</span><span class="sxs-lookup"><span data-stu-id="5e806-144">There is no limit on hello number of messages held in a queue but there is a cap on hello total size of hello messages held by a queue.</span></span> <span data-ttu-id="5e806-145">Bu sıra boyutu üst sınır 5 GB'tır.</span><span class="sxs-lookup"><span data-stu-id="5e806-145">This upper limit on queue size is 5 GB.</span></span>

## <a name="receive-messages-from-a-queue"></a><span data-ttu-id="5e806-146">Kuyruktan ileti alma</span><span class="sxs-lookup"><span data-stu-id="5e806-146">Receive messages from a queue</span></span>

<span data-ttu-id="5e806-147">Merhaba en iyi şekilde tooreceive iletilerin bir kuyruktan toouse olan bir `ServiceBusRestProxy->receiveQueueMessage` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="5e806-147">hello best way tooreceive messages from a queue is toouse a `ServiceBusRestProxy->receiveQueueMessage` method.</span></span> <span data-ttu-id="5e806-148">İletileri iki farklı modda alınan: [ *ReceiveAndDelete* ](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) ve [ *PeekLock*](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock).</span><span class="sxs-lookup"><span data-stu-id="5e806-148">Messages can be received in two different modes: [*ReceiveAndDelete*](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) and [*PeekLock*](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock).</span></span> <span data-ttu-id="5e806-149">**PeekLock** hello varsayılandır.</span><span class="sxs-lookup"><span data-stu-id="5e806-149">**PeekLock** is hello default.</span></span>

<span data-ttu-id="5e806-150">Kullanırken [ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) modu, alma bir tek işlemi; diğer bir deyişle, hizmet veri yolu bir kuyrukta İletiye yönelik Okuma isteği aldığında, hello iletiyi kullanılıyor olarak işaretler ve toohello uygulama döndürür.</span><span class="sxs-lookup"><span data-stu-id="5e806-150">When using [ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) mode, receive is a single-shot operation; that is, when Service Bus receives a read request for a message in a queue, it marks hello message as being consumed and returns it toohello application.</span></span> <span data-ttu-id="5e806-151">[ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) modu hello en basit modeldir ve senaryoları bir uygulama içinde tolerans bir hatanın hello Olay iletisinde işlenmiyor en iyi şekilde çalışır.</span><span class="sxs-lookup"><span data-stu-id="5e806-151">[ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) mode is hello simplest model and works best for scenarios in which an application can tolerate not processing a message in hello event of a failure.</span></span> <span data-ttu-id="5e806-152">toounderstand Bu, hangi hello tüketici sorunları hello alma isteği bir senaryo düşünün ve işlemeden önce çöküyor.</span><span class="sxs-lookup"><span data-stu-id="5e806-152">toounderstand this, consider a scenario in which hello consumer issues hello receive request and then crashes before processing it.</span></span> <span data-ttu-id="5e806-153">Hizmet veri yolu selamlama iletisine hello uygulama yeniden başlatılıp iletileri tekrar kullanmaya başladığında olduğunda, ardından kullanılıyor olarak işaretlenmiş için onu olan hello iletiyi atlamış olur önceki toohello kilitlenme tüketilen.</span><span class="sxs-lookup"><span data-stu-id="5e806-153">Because Service Bus will have marked hello message as being consumed, then when hello application restarts and begins consuming messages again, it will have missed hello message that was consumed prior toohello crash.</span></span>

<span data-ttu-id="5e806-154">Merhaba varsayılan [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock) bir ileti alma modu, iletilere olası toosupport uygulamaları iki aşamalı işlemi haline gelir.</span><span class="sxs-lookup"><span data-stu-id="5e806-154">In hello default [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock) mode, receiving a message becomes a two stage operation, which makes it possible toosupport applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="5e806-155">Service Bus bir istek aldığında, tüketilen hello sonraki ileti toobe bulur, tooprevent kilitler, almasını diğer tüketicilerin ve toohello uygulama döndürür.</span><span class="sxs-lookup"><span data-stu-id="5e806-155">When Service Bus receives a request, it finds hello next message toobe consumed, locks it tooprevent other consumers from receiving it, and then returns it toohello application.</span></span> <span data-ttu-id="5e806-156">Merhaba uygulaması hello iletiyi işlemeyi tamamladıktan sonra (veya sonra işlemek için depoladıktan sonra), hello hello ikinci aşamasını tamamlar alınan selamlama iletisine çok geçirerek alma işleminin`ServiceBusRestProxy->deleteMessage`.</span><span class="sxs-lookup"><span data-stu-id="5e806-156">After hello application finishes processing hello message (or stores it reliably for future processing), it completes hello second stage of hello receive process by passing hello received message too`ServiceBusRestProxy->deleteMessage`.</span></span> <span data-ttu-id="5e806-157">Hizmet veri yolu hello gördüğünde `deleteMessage` çağrısı hello iletiyi kullanılıyor olarak işaretler ve hello sıradan kaldırın.</span><span class="sxs-lookup"><span data-stu-id="5e806-157">When Service Bus sees hello `deleteMessage` call, it will mark hello message as being consumed and remove it from hello queue.</span></span>

<span data-ttu-id="5e806-158">örnekte gösterildiği nasıl aşağıdaki hello tooreceive ve bir iletiyi kullanarak işlem [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock) (Merhaba varsayılan modu).</span><span class="sxs-lookup"><span data-stu-id="5e806-158">hello following example shows how tooreceive and process a message using [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock) mode (hello default mode).</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use WindowsAzure\Common\ServiceException;
use WindowsAzure\ServiceBus\Models\ReceiveMessageOptions;

// Create Service Bus REST proxy.
$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);

try    {
    // Set hello receive mode tooPeekLock (default is ReceiveAndDelete).
    $options = new ReceiveMessageOptions();
    $options->setPeekLock();

    // Receive message.
    $message = $serviceBusRestProxy->receiveQueueMessage("myqueue", $options);
    echo "Body: ".$message->getBody()."<br />";
    echo "MessageID: ".$message->getMessageId()."<br />";

    /*---------------------------
        Process message here.
    ----------------------------*/

    // Delete message. Not necessary if peek lock is not set.
    echo "Message deleted.<br />";
    $serviceBusRestProxy->deleteMessage($message);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // https://docs.microsoft.com/rest/api/storageservices/Common-REST-API-Error-Codes
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="5e806-159">Nasıl toohandle uygulaması kilitlenir ve Okunmayan iletileri</span><span class="sxs-lookup"><span data-stu-id="5e806-159">How toohandle application crashes and unreadable messages</span></span>

<span data-ttu-id="5e806-160">Hizmet veri yolu, gerçekleşen hataları uygulama ya da ileti işlenirken zorlukları rahat işlevselliği toohelp sağlar.</span><span class="sxs-lookup"><span data-stu-id="5e806-160">Service Bus provides functionality toohelp you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="5e806-161">Alıcı uygulamanın kaydedemediği tooprocess Merhaba ileti herhangi bir nedenden dolayı ardından hello çağırabilirsiniz `unlockMessage` hello alınan ileti üzerinde yöntemi (hello yerine `deleteMessage` yöntemi).</span><span class="sxs-lookup"><span data-stu-id="5e806-161">If a receiver application is unable tooprocess hello message for some reason, then it can call hello `unlockMessage` method on hello received message (instead of hello `deleteMessage` method).</span></span> <span data-ttu-id="5e806-162">Bu hizmet veri yolu toounlock selamlama iletisine hello sıra içinde neden ve yeniden alınan kullanılabilir toobe olun, ya da göre aynı uygulama veya başka bir kullanıcı uygulama tarafından tüketen hello.</span><span class="sxs-lookup"><span data-stu-id="5e806-162">This will cause Service Bus toounlock hello message within hello queue and make it available toobe received again, either by hello same consuming application or by another consuming application.</span></span>

<span data-ttu-id="5e806-163">Ayrıca hello kuyrukta kilitlenen iletiye ilişkin bir zaman aşımı vardır ve tooprocess selamlama iletisine önce hello uygulama başarısız olursa (örneğin, hello uygulama çökerse) Service Bus selamlama iletisine kilidini hello kilit zaman aşımı dolmadan otomatik olarak yeniden alınan kullanılabilir toobe olun.</span><span class="sxs-lookup"><span data-stu-id="5e806-163">There is also a timeout associated with a message locked within hello queue, and if hello application fails tooprocess hello message before hello lock timeout expires (for example, if hello application crashes), then Service Bus will unlock hello message automatically and make it available toobe received again.</span></span>

<span data-ttu-id="5e806-164">Merhaba ileti işlenirken sonra ancak hello önce uygulama hello olay Hello çöküyor `deleteMessage` isteği bildirilmeden sonra başlatıldığında hello ileti yeniden teslim toohello uygulama olacaktır.</span><span class="sxs-lookup"><span data-stu-id="5e806-164">In hello event that hello application crashes after processing hello message but before hello `deleteMessage` request is issued, then hello message will be redelivered toohello application when it restarts.</span></span> <span data-ttu-id="5e806-165">Bu genellikle adlandırılır *en az bir kez* işleme; diğer bir deyişle, her ileti en az bir kez işlenir ancak belirli durumlarda hello aynı ileti yeniden teslim.</span><span class="sxs-lookup"><span data-stu-id="5e806-165">This is often called *At Least Once* processing; that is, each message is processed at least once but in certain situations hello same message may be redelivered.</span></span> <span data-ttu-id="5e806-166">Merhaba senaryo yinelenen işlemeyi sonra ek ekleme etmiyorsa mantığı tooapplications toohandle yinelenen ileti teslimi önerilir.</span><span class="sxs-lookup"><span data-stu-id="5e806-166">If hello scenario cannot tolerate duplicate processing, then adding additional logic tooapplications toohandle duplicate message delivery is recommended.</span></span> <span data-ttu-id="5e806-167">Bu genellikle hello kullanılarak elde edilen `getMessageId` teslimat denemelerinde hello iletisinin yöntemi.</span><span class="sxs-lookup"><span data-stu-id="5e806-167">This is often achieved using hello `getMessageId` method of hello message, which remains constant across delivery attempts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5e806-168">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5e806-168">Next steps</span></span>
<span data-ttu-id="5e806-169">Artık Service Bus kuyruklarını hello temellerini öğrendiğinize göre bkz: [kuyruklar, konu başlıkları ve abonelikler] [ Queues, topics, and subscriptions] daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="5e806-169">Now that you've learned hello basics of Service Bus queues, see [Queues, topics, and subscriptions][Queues, topics, and subscriptions] for more information.</span></span>

<span data-ttu-id="5e806-170">Daha fazla bilgi için ayrıca hello ziyaret [PHP Geliştirici Merkezi](https://azure.microsoft.com/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="5e806-170">For more information, also visit hello [PHP Developer Center](https://azure.microsoft.com/develop/php/).</span></span>

[BrokeredMessage]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[require_once]: http://php.net/require_once


