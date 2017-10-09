---
title: "PHP ile aaaHow toouse Service Bus konuları | Microsoft Docs"
description: "Bilgi nasıl toouse Service Bus konuları azure'da PHP ile."
services: service-bus-messaging
documentationcenter: php
author: sethmanheim
manager: timlt
editor: 
ms.assetid: faaa4bbd-f6ef-42ff-aca7-fc4353976449
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/27/2017
ms.author: sethm
ms.openlocfilehash: 0ca8625fa3edc5854c0d6c1c2f6adab6a2d42f91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-topics-and-subscriptions-with-php"></a><span data-ttu-id="a9fc0-103">Nasıl toouse Service Bus konuları ve abonelikleri PHP ile</span><span class="sxs-lookup"><span data-stu-id="a9fc0-103">How toouse Service Bus topics and subscriptions with PHP</span></span>

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

<span data-ttu-id="a9fc0-104">Bu makale size nasıl gösterir toouse Service Bus konuları ve abonelikleri.</span><span class="sxs-lookup"><span data-stu-id="a9fc0-104">This article shows you how toouse Service Bus topics and subscriptions.</span></span> <span data-ttu-id="a9fc0-105">Merhaba örnekler PHP ile yazılmıştır ve hello kullan [PHP için Azure SDK](../php-download-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="a9fc0-105">hello samples are written in PHP and use hello [Azure SDK for PHP](../php-download-sdk.md).</span></span> <span data-ttu-id="a9fc0-106">Merhaba kapsanan senaryolar dahil **konuları ve abonelikleri oluşturma**, **abonelik filtreleri oluşturma**, **iletileri tooa konu gönderme**, **alma bir abonelik iletilerden**, ve **konuları ve abonelikleri silmeyi**.</span><span class="sxs-lookup"><span data-stu-id="a9fc0-106">hello scenarios covered include **creating topics and subscriptions**, **creating subscription filters**, **sending messages tooa topic**, **receiving messages from a subscription**, and **deleting topics and subscriptions**.</span></span>

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

## <a name="create-a-php-application"></a><span data-ttu-id="a9fc0-107">PHP uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="a9fc0-107">Create a PHP application</span></span>
<span data-ttu-id="a9fc0-108">Merhaba tooreference sınıflarda hello Azure Blob hizmete erişen bir PHP uygulaması oluşturmaya yönelik gereksinim, yalnızca hello [PHP için Azure SDK](../php-download-sdk.md) gelen kodunuzu içinde.</span><span class="sxs-lookup"><span data-stu-id="a9fc0-108">hello only requirement for creating a PHP application that accesses hello Azure Blob service is tooreference classes in hello [Azure SDK for PHP](../php-download-sdk.md) from within your code.</span></span> <span data-ttu-id="a9fc0-109">Uygulama veya Notepad tüm geliştirme araçları toocreate kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a9fc0-109">You can use any development tools toocreate your application, or Notepad.</span></span>

> [!NOTE]
> <span data-ttu-id="a9fc0-110">PHP yüklemenizi de hello olmalıdır [OpenSSL uzantısı](http://php.net/openssl) yüklenir ve etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="a9fc0-110">Your PHP installation must also have hello [OpenSSL extension](http://php.net/openssl) installed and enabled.</span></span>
> 
> 

<span data-ttu-id="a9fc0-111">Bu makalede nasıl toouse hizmet PHP uygulamanızda yerel olarak veya bir Azure web rolü, çalışan rolü veya Web sitesi içinde çalışan kodu çağrılabilir özellikleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="a9fc0-111">This article describes how toouse service features that can be called within a PHP application locally, or in code running within an Azure web role, worker role, or website.</span></span>

## <a name="get-hello-azure-client-libraries"></a><span data-ttu-id="a9fc0-112">Hello Azure istemci kitaplıkları Al</span><span class="sxs-lookup"><span data-stu-id="a9fc0-112">Get hello Azure client libraries</span></span>
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-toouse-service-bus"></a><span data-ttu-id="a9fc0-113">Uygulama toouse Service Bus yapılandırın</span><span class="sxs-lookup"><span data-stu-id="a9fc0-113">Configure your application toouse Service Bus</span></span>
<span data-ttu-id="a9fc0-114">toouse hello Service Bus API'lerine:</span><span class="sxs-lookup"><span data-stu-id="a9fc0-114">toouse hello Service Bus APIs:</span></span>

1. <span data-ttu-id="a9fc0-115">Hello kullanarak başvuru hello otomatik yükleyici dosyasını [require_once] [ require-once] deyimi.</span><span class="sxs-lookup"><span data-stu-id="a9fc0-115">Reference hello autoloader file using hello [require_once][require-once] statement.</span></span>
2. <span data-ttu-id="a9fc0-116">Kullanabileceğinize sınıfları başvuru.</span><span class="sxs-lookup"><span data-stu-id="a9fc0-116">Reference any classes you might use.</span></span>

<span data-ttu-id="a9fc0-117">Merhaba aşağıdaki örnekte nasıl tooinclude hello otomatik Yükleyiciden dosya ve başvuru hello gösterir **ServiceBusService** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="a9fc0-117">hello following example shows how tooinclude hello autoloader file and reference hello **ServiceBusService** class.</span></span>

> [!NOTE]
> <span data-ttu-id="a9fc0-118">Bu örnek (ve diğer örnekleri bu makalede) hello PHP istemci kitaplıkları oluşturucu aracılığıyla Azure yüklü olduğunu varsayar.</span><span class="sxs-lookup"><span data-stu-id="a9fc0-118">This example (and other examples in this article) assumes you have installed hello PHP Client Libraries for Azure via Composer.</span></span> <span data-ttu-id="a9fc0-119">El ile veya bir ARMUTLU paketi olarak hello kitaplıkları yüklediyseniz, hello başvurmalıdır **WindowsAzure.php** otomatik yükleyici dosyası.</span><span class="sxs-lookup"><span data-stu-id="a9fc0-119">If you installed hello libraries manually or as a PEAR package, you must reference hello **WindowsAzure.php** autoloader file.</span></span>
> 
> 

```php
require_once 'vendor\autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

<span data-ttu-id="a9fc0-120">Örnek hello hello `require_once` deyimi her zaman gösterilecek, ancak yalnızca hello sınıfları hello örnek tooexecute için gereken başvuru.</span><span class="sxs-lookup"><span data-stu-id="a9fc0-120">In hello following examples, hello `require_once` statement will always be shown, but only hello classes necessary for hello example tooexecute are referenced.</span></span>

## <a name="set-up-a-service-bus-connection"></a><span data-ttu-id="a9fc0-121">Hizmet veri yolu bağlantı kurma</span><span class="sxs-lookup"><span data-stu-id="a9fc0-121">Set up a Service Bus connection</span></span>
<span data-ttu-id="a9fc0-122">tooinstantiate önce yapmalısınız Service Bus istemci geçerli bir bağlantı dizesi şu biçimde vardır:</span><span class="sxs-lookup"><span data-stu-id="a9fc0-122">tooinstantiate a Service Bus client you must first have a valid connection string in this format:</span></span>

```
Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]
```

<span data-ttu-id="a9fc0-123">Burada `Endpoint` genellikle hello biçimidir `https://[yourNamespace].servicebus.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="a9fc0-123">Where `Endpoint` is typically of hello format `https://[yourNamespace].servicebus.windows.net`.</span></span>

<span data-ttu-id="a9fc0-124">toocreate hello kullanmalıdır herhangi bir Azure hizmeti istemci `ServicesBuilder` sınıfı.</span><span class="sxs-lookup"><span data-stu-id="a9fc0-124">toocreate any Azure service client you must use hello `ServicesBuilder` class.</span></span> <span data-ttu-id="a9fc0-125">Şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="a9fc0-125">You can:</span></span>

* <span data-ttu-id="a9fc0-126">Merhaba bağlantı geçirmek doğrudan tooit dize.</span><span class="sxs-lookup"><span data-stu-id="a9fc0-126">Pass hello connection string directly tooit.</span></span>
* <span data-ttu-id="a9fc0-127">Kullanım hello **CloudConfigurationManager (CCM)** toocheck birden çok dış kaynaklardan hello bağlantı dizesi:</span><span class="sxs-lookup"><span data-stu-id="a9fc0-127">Use hello **CloudConfigurationManager (CCM)** toocheck multiple external sources for hello connection string:</span></span>
  * <span data-ttu-id="a9fc0-128">Varsayılan olarak, bir dış kaynak - ortam değişkenleri desteği ile birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="a9fc0-128">By default it comes with support for one external source - environmental variables.</span></span>
  * <span data-ttu-id="a9fc0-129">Merhaba genişleterek yeni kaynakları ekleyebilirsiniz `ConnectionStringSource` sınıfı.</span><span class="sxs-lookup"><span data-stu-id="a9fc0-129">You can add new sources by extending hello `ConnectionStringSource` class.</span></span>

<span data-ttu-id="a9fc0-130">Burada özetlenen hello örnekler için başlangıç bağlantı dizesi doğrudan geçirilir.</span><span class="sxs-lookup"><span data-stu-id="a9fc0-130">For hello examples outlined here, hello connection string is passed directly.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$connectionString = "Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]";

$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);
```

## <a name="create-a-topic"></a><span data-ttu-id="a9fc0-131">Konu başlığı oluşturma</span><span class="sxs-lookup"><span data-stu-id="a9fc0-131">Create a topic</span></span>
<span data-ttu-id="a9fc0-132">Merhaba üzerinden Service Bus konu başlıklarına yönelik yönetim işlemlerini gerçekleştirebilirsiniz `ServiceBusRestProxy` sınıfı.</span><span class="sxs-lookup"><span data-stu-id="a9fc0-132">You can perform management operations for Service Bus topics via hello `ServiceBusRestProxy` class.</span></span> <span data-ttu-id="a9fc0-133">A `ServiceBusRestProxy` nesne hello oluşturulan `ServicesBuilder::createServiceBusService` Üreteç yöntemi hello belirteci izinleri toomanage yalıtan bir uygun bir bağlantı dizesi ile.</span><span class="sxs-lookup"><span data-stu-id="a9fc0-133">A `ServiceBusRestProxy` object is constructed via hello `ServicesBuilder::createServiceBusService` factory method with an appropriate connection string that encapsulates hello token permissions toomanage it.</span></span>

<span data-ttu-id="a9fc0-134">örnekte gösterildiği nasıl aşağıdaki hello tooinstantiate bir `ServiceBusRestProxy` ve arama `ServiceBusRestProxy->createTopic` toocreate adlandırılan bir konu `mytopic` içinde bir `MySBNamespace` ad alanı:</span><span class="sxs-lookup"><span data-stu-id="a9fc0-134">hello following example shows how tooinstantiate a `ServiceBusRestProxy` and call `ServiceBusRestProxy->createTopic` toocreate a topic named `mytopic` within a `MySBNamespace` namespace:</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use WindowsAzure\Common\ServiceException;
use WindowsAzure\ServiceBus\Models\TopicInfo;

// Create Service Bus REST proxy.
$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);

try    {        
    // Create topic.
    $topicInfo = new TopicInfo("mytopic");
    $serviceBusRestProxy->createTopic($topicInfo);
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
> <span data-ttu-id="a9fc0-135">Merhaba kullanabilirsiniz `listTopics` yöntemi `ServiceBusRestProxy` bir hizmet ad alanında belirtilen ada sahip bir konu zaten varsa toocheck nesneleri.</span><span class="sxs-lookup"><span data-stu-id="a9fc0-135">You can use hello `listTopics` method on `ServiceBusRestProxy` objects toocheck if a topic with a specified name already exists within a service namespace.</span></span>
> 
> 

## <a name="create-a-subscription"></a><span data-ttu-id="a9fc0-136">Abonelik oluşturma</span><span class="sxs-lookup"><span data-stu-id="a9fc0-136">Create a subscription</span></span>
<span data-ttu-id="a9fc0-137">Konu aboneliklerini ayrıca hello ile oluşturulan `ServiceBusRestProxy->createSubscription` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="a9fc0-137">Topic subscriptions are also created with hello `ServiceBusRestProxy->createSubscription` method.</span></span> <span data-ttu-id="a9fc0-138">Abonelikler adlandırılır ve hello toohello aboneliğin sanal kuyruğuna gönderilen ileti kümesini sınırlayan isteğe bağlı bir filtre içerebilir.</span><span class="sxs-lookup"><span data-stu-id="a9fc0-138">Subscriptions are named and can have an optional filter that restricts hello set of messages passed toohello subscription's virtual queue.</span></span>

### <a name="create-a-subscription-with-hello-default-matchall-filter"></a><span data-ttu-id="a9fc0-139">Merhaba varsayılan (MatchAll) filtreyle abonelik oluşturma</span><span class="sxs-lookup"><span data-stu-id="a9fc0-139">Create a subscription with hello default (MatchAll) filter</span></span>
<span data-ttu-id="a9fc0-140">Merhaba **MatchAll** yeni bir abonelik oluşturulurken filtre belirtilmeyen varsa, kullanılan hello varsayılan filtre filtredir.</span><span class="sxs-lookup"><span data-stu-id="a9fc0-140">hello **MatchAll** filter is hello default filter that is used if no filter is specified when a new subscription is created.</span></span> <span data-ttu-id="a9fc0-141">Ne zaman hello **MatchAll** filtre kullanıldığında, tüm iletileri yayımlanan toohello konu hello aboneliğin sanal kuyruğuna yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="a9fc0-141">When hello **MatchAll** filter is used, all messages published toohello topic are placed in hello subscription's virtual queue.</span></span> <span data-ttu-id="a9fc0-142">Merhaba aşağıdaki örnekte 'mysubscription' adlı bir abonelik oluşturur ve kullanır hello varsayılan **MatchAll** Filtresi.</span><span class="sxs-lookup"><span data-stu-id="a9fc0-142">hello following example creates a subscription named 'mysubscription' and uses hello default **MatchAll** filter.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use WindowsAzure\Common\ServiceException;
use WindowsAzure\ServiceBus\Models\SubscriptionInfo;

// Create Service Bus REST proxy.
$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);

try    {
    // Create subscription.
    $subscriptionInfo = new SubscriptionInfo("mysubscription");
    $serviceBusRestProxy->createSubscription("mytopic", $subscriptionInfo);
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

### <a name="create-subscriptions-with-filters"></a><span data-ttu-id="a9fc0-143">Filtre içeren abonelik oluşturma</span><span class="sxs-lookup"><span data-stu-id="a9fc0-143">Create subscriptions with filters</span></span>
<span data-ttu-id="a9fc0-144">Hangi iletilerin tooa konu içinde belirli konu aboneliği görünmelidir gönderilen toospecify etkinleştirmek filtreler de ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a9fc0-144">You can also set up filters that enable you toospecify which messages sent tooa topic should appear within a specific topic subscription.</span></span> <span data-ttu-id="a9fc0-145">Merhaba en esnek filtre abonelikler tarafından desteklenen hello türünde [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter), SQL92 alt kümesi uygular.</span><span class="sxs-lookup"><span data-stu-id="a9fc0-145">hello most flexible type of filter supported by subscriptions is hello [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter), which implements a subset of SQL92.</span></span> <span data-ttu-id="a9fc0-146">SQL filtreleri yayımlanan toohello konu hello iletilerinin hello özelliklerini çalışır.</span><span class="sxs-lookup"><span data-stu-id="a9fc0-146">SQL filters operate on hello properties of hello messages that are published toohello topic.</span></span> <span data-ttu-id="a9fc0-147">SqlFilters hakkında daha fazla bilgi için bkz: [SqlFilter.SqlExpression özelliği][sqlfilter].</span><span class="sxs-lookup"><span data-stu-id="a9fc0-147">For more information about SqlFilters, see [SqlFilter.SqlExpression Property][sqlfilter].</span></span>

> [!NOTE]
> <span data-ttu-id="a9fc0-148">Bir abonelikte her bir kural sonuç iletileri toohello aboneliğini ekleme gelen iletileri bağımsız olarak işler.</span><span class="sxs-lookup"><span data-stu-id="a9fc0-148">Each rule on a subscription processes incoming messages independently, adding their result messages toohello subscription.</span></span> <span data-ttu-id="a9fc0-149">Ayrıca, her yeni abonelik varsayılan sahip **kural** tüm iletileri hello konu toohello abonelikten ekler bir filtre ile nesne.</span><span class="sxs-lookup"><span data-stu-id="a9fc0-149">In addition, each new subscription has a default **Rule** object with a filter that adds all messages from hello topic toohello subscription.</span></span> <span data-ttu-id="a9fc0-150">filtrenizle eşleşen tooreceive yalnızca iletiler hello varsayılan kural kaldırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="a9fc0-150">tooreceive only messages matching your filter, you must remove hello default rule.</span></span> <span data-ttu-id="a9fc0-151">Hello kullanarak hello varsayılan kural kaldırabilirsiniz `ServiceBusRestProxy->deleteRule` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="a9fc0-151">You can remove hello default rule by using hello `ServiceBusRestProxy->deleteRule` method.</span></span>
> 
> 

<span data-ttu-id="a9fc0-152">Merhaba aşağıdaki örnek adlı bir abonelik oluşturulur `HighMessages` ile bir **SqlFilter** özel iletileri yalnızca seçer `MessageNumber` özelliği 3'ten büyük.</span><span class="sxs-lookup"><span data-stu-id="a9fc0-152">hello following example creates a subscription named `HighMessages` with a **SqlFilter** that only selects messages that have a custom `MessageNumber` property greater than 3.</span></span> <span data-ttu-id="a9fc0-153">Bkz: [gönderme iletileri tooa konu](#send-messages-to-a-topic) özel özellikler toomessages ekleme hakkında bilgi.</span><span class="sxs-lookup"><span data-stu-id="a9fc0-153">See [Send messages tooa topic](#send-messages-to-a-topic) for information about adding custom properties toomessages.</span></span>

```php
$subscriptionInfo = new SubscriptionInfo("HighMessages");
$serviceBusRestProxy->createSubscription("mytopic", $subscriptionInfo);

$serviceBusRestProxy->deleteRule("mytopic", "HighMessages", '$Default');

$ruleInfo = new RuleInfo("HighMessagesRule");
$ruleInfo->withSqlFilter("MessageNumber > 3");
$ruleResult = $serviceBusRestProxy->createRule("mytopic", "HighMessages", $ruleInfo);
```

<span data-ttu-id="a9fc0-154">Bu kod ek bir ad alanı hello kullanılmasını gerektiren Not: `WindowsAzure\ServiceBus\Models\SubscriptionInfo`.</span><span class="sxs-lookup"><span data-stu-id="a9fc0-154">Note that this code requires hello use of an additional namespace: `WindowsAzure\ServiceBus\Models\SubscriptionInfo`.</span></span>

<span data-ttu-id="a9fc0-155">Benzer şekilde, hello aşağıdaki örnek adlı bir abonelik oluşturur `LowMessages` ile bir `SqlFilter` olan iletiler yalnızca seçer bir `MessageNumber` özelliği daha az veya bu değere eşit too3.</span><span class="sxs-lookup"><span data-stu-id="a9fc0-155">Similarly, hello following example creates a subscription named `LowMessages` with a `SqlFilter` that only selects messages that have a `MessageNumber` property less than or equal too3.</span></span>

```php
$subscriptionInfo = new SubscriptionInfo("LowMessages");
$serviceBusRestProxy->createSubscription("mytopic", $subscriptionInfo);

$serviceBusRestProxy->deleteRule("mytopic", "LowMessages", '$Default');

$ruleInfo = new RuleInfo("LowMessagesRule");
$ruleInfo->withSqlFilter("MessageNumber <= 3");
$ruleResult = $serviceBusRestProxy->createRule("mytopic", "LowMessages", $ruleInfo);
```

<span data-ttu-id="a9fc0-156">Şimdi, ne zaman bir ileti gönderilir toohello `mytopic` konuya abone tooreceivers toohello her zaman teslim `mysubscription` abonelik ve abone olunan seçmeli olarak teslim tooreceivers toohello `HighMessages` ve `LowMessages` abonelikleri ( Merhaba ileti içeriği bağlı olarak).</span><span class="sxs-lookup"><span data-stu-id="a9fc0-156">Now, when a message is sent toohello `mytopic` topic, it is always delivered tooreceivers subscribed toohello `mysubscription` subscription, and selectively delivered tooreceivers subscribed toohello `HighMessages` and `LowMessages` subscriptions (depending upon hello message content).</span></span>

## <a name="send-messages-tooa-topic"></a><span data-ttu-id="a9fc0-157">İletileri tooa konu gönderin</span><span class="sxs-lookup"><span data-stu-id="a9fc0-157">Send messages tooa topic</span></span>
<span data-ttu-id="a9fc0-158">toosend ileti tooa Service Bus konu, uygulamanızı çağırır hello `ServiceBusRestProxy->sendTopicMessage` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="a9fc0-158">toosend a message tooa Service Bus topic, your application calls hello `ServiceBusRestProxy->sendTopicMessage` method.</span></span> <span data-ttu-id="a9fc0-159">kodun gösterdiği nasıl aşağıdaki hello toosend ileti toohello `mytopic` konu içinde daha önce oluşturduğunuz `MySBNamespace` hizmet ad alanı.</span><span class="sxs-lookup"><span data-stu-id="a9fc0-159">hello following code shows how toosend a message toohello `mytopic` topic previously created within the `MySBNamespace` service namespace.</span></span>

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
    $serviceBusRestProxy->sendTopicMessage("mytopic", $message);
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

<span data-ttu-id="a9fc0-160">İletileri gönderilir tooService veri yolu konuları hello örneklerini [BrokeredMessage] [ BrokeredMessage] sınıfı.</span><span class="sxs-lookup"><span data-stu-id="a9fc0-160">Messages sent tooService Bus topics are instances of hello [BrokeredMessage][BrokeredMessage] class.</span></span> <span data-ttu-id="a9fc0-161">[BrokeredMessage] [ BrokeredMessage] nesnelerinin standart özellikleri ve yöntemleri yanı sıra, kullanılan toohold özel uygulamaya özgü özellikleri olabilir özellikler kümesi vardır.</span><span class="sxs-lookup"><span data-stu-id="a9fc0-161">[BrokeredMessage][BrokeredMessage] objects have a set of standard properties and methods, as well as properties that can be used toohold custom application-specific properties.</span></span> <span data-ttu-id="a9fc0-162">Merhaba aşağıdaki örnekte nasıl toosend 5 test toohello iletileri gösterir `mytopic` daha önce oluşturulan konu.</span><span class="sxs-lookup"><span data-stu-id="a9fc0-162">hello following example shows how toosend 5 test messages toohello `mytopic` topic previously created.</span></span> <span data-ttu-id="a9fc0-163">Merhaba `setProperty` yöntemdir kullanılan tooadd özel özelliğin (`MessageNumber`) tooeach ileti.</span><span class="sxs-lookup"><span data-stu-id="a9fc0-163">hello `setProperty` method is used tooadd a custom property (`MessageNumber`) tooeach message.</span></span> <span data-ttu-id="a9fc0-164">Bu hello Not `MessageNumber` özellik değeri değişir her ileti için (hangi abonelik almak, bu değer toodetermine hello gösterildiği gibi kullanabilirsiniz [abonelik oluşturma](#create-a-subscription) bölümü):</span><span class="sxs-lookup"><span data-stu-id="a9fc0-164">Note that hello `MessageNumber` property value varies on each message (you can use this value toodetermine which subscriptions receive it, as shown in hello [Create a subscription](#create-a-subscription) section):</span></span>

```php
for($i = 0; $i < 5; $i++){
    // Create message.
    $message = new BrokeredMessage();
    $message->setBody("my message ".$i);

    // Set custom property.
    $message->setProperty("MessageNumber", $i);

    // Send message.
    $serviceBusRestProxy->sendTopicMessage("mytopic", $message);
}
```

<span data-ttu-id="a9fc0-165">Service Bus konu başlıklarını destek maksimum ileti boyutu 256 KB hello [standart katmanı](service-bus-premium-messaging.md) hello 1 MB [Premium katmanı](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="a9fc0-165">Service Bus topics support a maximum message size of 256 KB in hello [Standard tier](service-bus-premium-messaging.md) and 1 MB in hello [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="a9fc0-166">Merhaba standart ve özel uygulama özelliklerini içeren hello üstbilgi en büyük boyutu 64 KB olabilir.</span><span class="sxs-lookup"><span data-stu-id="a9fc0-166">hello header, which includes hello standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="a9fc0-167">Merhaba konu başlığında tutulan ileti sayısına bir sınır yoktur ancak konu başlığı tarafından tutulan hello iletilerin toplam boyutu hello bir sınır yoktur.</span><span class="sxs-lookup"><span data-stu-id="a9fc0-167">There is no limit on hello number of messages held in a topic but there is a cap on hello total size of hello messages held by a topic.</span></span> <span data-ttu-id="a9fc0-168">Bu konu başlığı boyutu üst sınır 5 GB'tır.</span><span class="sxs-lookup"><span data-stu-id="a9fc0-168">This upper limit on topic size is 5 GB.</span></span> <span data-ttu-id="a9fc0-169">Kotalar hakkında daha fazla bilgi için bkz: [Service Bus kotaları][Service Bus quotas].</span><span class="sxs-lookup"><span data-stu-id="a9fc0-169">For more information about quotas, see [Service Bus quotas][Service Bus quotas].</span></span>

## <a name="receive-messages-from-a-subscription"></a><span data-ttu-id="a9fc0-170">Abonelikten ileti alma</span><span class="sxs-lookup"><span data-stu-id="a9fc0-170">Receive messages from a subscription</span></span>
<span data-ttu-id="a9fc0-171">Merhaba en iyi şekilde tooreceive iletileri bir aboneliğe ilişkin toouse olan bir `ServiceBusRestProxy->receiveSubscriptionMessage` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="a9fc0-171">hello best way tooreceive messages from a subscription is toouse a `ServiceBusRestProxy->receiveSubscriptionMessage` method.</span></span> <span data-ttu-id="a9fc0-172">İletileri iki farklı modda alınan: [ *ReceiveAndDelete* ve *PeekLock*](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode).</span><span class="sxs-lookup"><span data-stu-id="a9fc0-172">Messages can be received in two different modes: [*ReceiveAndDelete* and *PeekLock*](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode).</span></span> <span data-ttu-id="a9fc0-173">**PeekLock** hello varsayılandır.</span><span class="sxs-lookup"><span data-stu-id="a9fc0-173">**PeekLock** is hello default.</span></span>

<span data-ttu-id="a9fc0-174">Merhaba kullanırken [ReceiveAndDelete](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) modu, alma bir tek işlemi; diğer bir deyişle, hizmet veri yolu bir abonelikte bir iletiye yönelik Okuma isteği aldığında, hello iletiyi kullanılıyor olarak işaretler ve toohello döndürür uygulama.</span><span class="sxs-lookup"><span data-stu-id="a9fc0-174">When using hello [ReceiveAndDelete](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) mode, receive is a single-shot operation; that is, when Service Bus receives a read request for a message in a subscription, it marks hello message as being consumed and returns it toohello application.</span></span> <span data-ttu-id="a9fc0-175">[ReceiveAndDelete](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) * modu hello en basit modeldir ve senaryoları bir uygulama içinde tolerans bir hatanın hello Olay iletisinde işlenmiyor en iyi şekilde çalışır.</span><span class="sxs-lookup"><span data-stu-id="a9fc0-175">[ReceiveAndDelete](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) * mode is hello simplest model and works best for scenarios in which an application can tolerate not processing a message in hello event of a failure.</span></span> <span data-ttu-id="a9fc0-176">toounderstand Bu, hangi hello tüketici sorunları hello alma isteği bir senaryo düşünün ve işlemeden önce çöküyor.</span><span class="sxs-lookup"><span data-stu-id="a9fc0-176">toounderstand this, consider a scenario in which hello consumer issues hello receive request and then crashes before processing it.</span></span> <span data-ttu-id="a9fc0-177">Hizmet veri yolu selamlama iletisine hello uygulama yeniden başlatılıp iletileri tekrar kullanmaya başladığında olduğunda, ardından kullanılıyor olarak işaretlenmiş için onu olan hello iletiyi atlamış olur önceki toohello kilitlenme tüketilen.</span><span class="sxs-lookup"><span data-stu-id="a9fc0-177">Because Service Bus will have marked hello message as being consumed, then when hello application restarts and begins consuming messages again, it will have missed hello message that was consumed prior toohello crash.</span></span>

<span data-ttu-id="a9fc0-178">Merhaba varsayılan [PeekLock](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) bir ileti alma modu, iletilere olası toosupport uygulamaları iki aşamalı işlemi haline gelir.</span><span class="sxs-lookup"><span data-stu-id="a9fc0-178">In hello default [PeekLock](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) mode, receiving a message becomes a two stage operation, which makes it possible toosupport applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="a9fc0-179">Service Bus bir istek aldığında hello sonraki ileti toobe tüketilen, diğer tüketicilerin alırken tooprevent kilitler ve toohello uygulama döndürür bulur.</span><span class="sxs-lookup"><span data-stu-id="a9fc0-179">When Service Bus receives a request, it finds hello next message toobe consumed, locks it tooprevent other consumers receiving it, and then returns it toohello application.</span></span> <span data-ttu-id="a9fc0-180">Merhaba uygulaması hello iletiyi işlemeyi tamamladıktan sonra (veya sonra işlemek için depoladıktan sonra), hello hello ikinci aşamasını tamamlar alınan selamlama iletisine çok geçirerek alma işleminin`ServiceBusRestProxy->deleteMessage`.</span><span class="sxs-lookup"><span data-stu-id="a9fc0-180">After hello application finishes processing hello message (or stores it reliably for future processing), it completes hello second stage of hello receive process by passing hello received message too`ServiceBusRestProxy->deleteMessage`.</span></span> <span data-ttu-id="a9fc0-181">Hizmet veri yolu hello gördüğünde `deleteMessage` çağrısı hello iletiyi kullanılıyor olarak işaretler ve hello sıradan kaldırın.</span><span class="sxs-lookup"><span data-stu-id="a9fc0-181">When Service Bus sees hello `deleteMessage` call, it will mark hello message as being consumed and remove it from hello queue.</span></span>

<span data-ttu-id="a9fc0-182">örnekte gösterildiği nasıl aşağıdaki hello tooreceive ve bir iletiyi kullanarak işlem [PeekLock](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) (Merhaba varsayılan modu).</span><span class="sxs-lookup"><span data-stu-id="a9fc0-182">hello following example shows how tooreceive and process a message using [PeekLock](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) mode (hello default mode).</span></span> 

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use WindowsAzure\Common\ServiceException;
use WindowsAzure\ServiceBus\Models\ReceiveMessageOptions;

// Create Service Bus REST proxy.
$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);

try    {
    // Set receive mode tooPeekLock (default is ReceiveAndDelete)
    $options = new ReceiveMessageOptions();
    $options->setPeekLock();

    // Get message.
    $message = $serviceBusRestProxy->receiveSubscriptionMessage("mytopic", "mysubscription", $options);

    echo "Body: ".$message->getBody()."<br />";
    echo "MessageID: ".$message->getMessageId()."<br />";

    /*---------------------------
        Process message here.
    ----------------------------*/

    // Delete message. Not necessary if peek lock is not set.
    echo "Deleting message...<br />";
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

## <a name="how-to-handle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="a9fc0-183">Nasıl yapılır: uygulama çökmelerini ve Okunmayan iletileri işleme</span><span class="sxs-lookup"><span data-stu-id="a9fc0-183">How to: handle application crashes and unreadable messages</span></span>
<span data-ttu-id="a9fc0-184">Hizmet veri yolu, gerçekleşen hataları uygulama ya da ileti işlenirken zorlukları rahat işlevselliği toohelp sağlar.</span><span class="sxs-lookup"><span data-stu-id="a9fc0-184">Service Bus provides functionality toohelp you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="a9fc0-185">Alıcı uygulamanın kaydedemediği tooprocess Merhaba ileti herhangi bir nedenden dolayı ardından hello çağırabilirsiniz `unlockMessage` hello alınan ileti üzerinde yöntemi (hello yerine `deleteMessage` yöntemi).</span><span class="sxs-lookup"><span data-stu-id="a9fc0-185">If a receiver application is unable tooprocess hello message for some reason, then it can call hello `unlockMessage` method on hello received message (instead of hello `deleteMessage` method).</span></span> <span data-ttu-id="a9fc0-186">Bu hizmet veri yolu toounlock selamlama iletisine hello sıra içinde neden ve yeniden alınan kullanılabilir toobe olun, ya da göre aynı uygulama veya başka bir kullanıcı uygulama tarafından tüketen hello.</span><span class="sxs-lookup"><span data-stu-id="a9fc0-186">This will cause Service Bus toounlock hello message within hello queue and make it available toobe received again, either by hello same consuming application or by another consuming application.</span></span>

<span data-ttu-id="a9fc0-187">Ayrıca hello kuyrukta kilitlenen iletiye ilişkin bir zaman aşımı vardır ve tooprocess selamlama iletisine önce hello uygulama başarısız olursa (örneğin, hello uygulama çökerse) Service Bus selamlama iletisine kilidini hello kilit zaman aşımı dolmadan otomatik olarak yeniden alınan kullanılabilir toobe olun.</span><span class="sxs-lookup"><span data-stu-id="a9fc0-187">There is also a timeout associated with a message locked within hello queue, and if hello application fails tooprocess hello message before hello lock timeout expires (for example, if hello application crashes), then Service Bus will unlock hello message automatically and make it available toobe received again.</span></span>

<span data-ttu-id="a9fc0-188">Merhaba ileti işlenirken sonra ancak hello önce uygulama hello olay Hello çöküyor `deleteMessage` isteği bildirilmeden sonra başlatıldığında hello ileti yeniden teslim toohello uygulama olacaktır.</span><span class="sxs-lookup"><span data-stu-id="a9fc0-188">In hello event that hello application crashes after processing hello message but before hello `deleteMessage` request is issued, then hello message will be redelivered toohello application when it restarts.</span></span> <span data-ttu-id="a9fc0-189">Bu genellikle adlandırılır *en az bir kez* işleme; diğer bir deyişle, her ileti en az bir kez işlenir ancak belirli durumlarda hello aynı ileti yeniden teslim.</span><span class="sxs-lookup"><span data-stu-id="a9fc0-189">This is often called *At Least Once* processing; that is, each message is processed at least once but in certain situations hello same message may be redelivered.</span></span> <span data-ttu-id="a9fc0-190">Merhaba senaryo yinelenen işlemeyi kabul etmiyorsa, uygulama geliştiricilerinin ek mantık tooapplications toohandle yinelenen ileti teslimi eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="a9fc0-190">If hello scenario cannot tolerate duplicate processing, then application developers should add additional logic tooapplications toohandle duplicate message delivery.</span></span> <span data-ttu-id="a9fc0-191">Bu genellikle hello kullanılarak elde edilen `getMessageId` teslimat denemelerinde hello iletisinin yöntemi.</span><span class="sxs-lookup"><span data-stu-id="a9fc0-191">This is often achieved using hello `getMessageId` method of hello message, which remains constant across delivery attempts.</span></span>

## <a name="delete-topics-and-subscriptions"></a><span data-ttu-id="a9fc0-192">Konu başlıklarını ve abonelikleri silme</span><span class="sxs-lookup"><span data-stu-id="a9fc0-192">Delete topics and subscriptions</span></span>
<span data-ttu-id="a9fc0-193">bir konu veya abonelik, kullanım hello toodelete `ServiceBusRestProxy->deleteTopic` veya hello `ServiceBusRestProxy->deleteSubscripton` yöntemleri, sırasıyla.</span><span class="sxs-lookup"><span data-stu-id="a9fc0-193">toodelete a topic or a subscription, use hello `ServiceBusRestProxy->deleteTopic` or hello `ServiceBusRestProxy->deleteSubscripton` methods, respectively.</span></span> <span data-ttu-id="a9fc0-194">Konu başlığı silindiğinde, hello konu başlığıyla kaydedilen tüm abonelikler de silinir olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="a9fc0-194">Note that deleting a topic also deletes any subscriptions that are registered with hello topic.</span></span>

<span data-ttu-id="a9fc0-195">Merhaba aşağıdaki örnekte nasıl toodelete bir konu adlı gösterir `mytopic` ve kayıtlı abonelikler.</span><span class="sxs-lookup"><span data-stu-id="a9fc0-195">hello following example shows how toodelete a topic named `mytopic` and its registered subscriptions.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\ServiceBus\ServiceBusService;
use WindowsAzure\ServiceBus\ServiceBusSettings;
use WindowsAzure\Common\ServiceException;

// Create Service Bus REST proxy.
$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);

try    {        
    // Delete topic.
    $serviceBusRestProxy->deleteTopic("mytopic");
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

<span data-ttu-id="a9fc0-196">Hello kullanarak `deleteSubscription` yöntemi, bir abonelik bağımsız olarak silebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="a9fc0-196">By using hello `deleteSubscription` method, you can delete a subscription independently:</span></span>

```php
$serviceBusRestProxy->deleteSubscription("mytopic", "mysubscription");
```

## <a name="next-steps"></a><span data-ttu-id="a9fc0-197">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a9fc0-197">Next steps</span></span>
<span data-ttu-id="a9fc0-198">Artık Service Bus kuyruklarını hello temellerini öğrendiğinize göre bkz: [kuyruklar, konu başlıkları ve abonelikler] [ Queues, topics, and subscriptions] daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="a9fc0-198">Now that you've learned hello basics of Service Bus queues, see [Queues, topics, and subscriptions][Queues, topics, and subscriptions] for more information.</span></span>

[BrokeredMessage]: https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.brokeredmessage
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[sqlfilter]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter
[require-once]: http://php.net/require_once
[Service Bus quotas]: service-bus-quotas.md
