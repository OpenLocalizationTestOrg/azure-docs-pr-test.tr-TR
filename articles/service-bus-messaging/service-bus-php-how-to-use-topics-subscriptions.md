---
title: "PHP ile Service Bus konu başlıklarını kullanma | Microsoft Docs"
description: "Azure'da PHP ile Service Bus konu başlıklarını kullanmayı öğrenin."
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
ms.openlocfilehash: afa9efcb6335786198021ec81dd087287c39bda9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-use-service-bus-topics-and-subscriptions-with-php"></a><span data-ttu-id="510f7-103">Service Bus konuları ve abonelikleri PHP ile kullanma</span><span class="sxs-lookup"><span data-stu-id="510f7-103">How to use Service Bus topics and subscriptions with PHP</span></span>

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

<span data-ttu-id="510f7-104">Bu makalede, Service Bus konuları ve abonelikleri nasıl kullanılacağı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="510f7-104">This article shows you how to use Service Bus topics and subscriptions.</span></span> <span data-ttu-id="510f7-105">PHP ve kullanım örnekleri yazılır [PHP için Azure SDK](../php-download-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="510f7-105">The samples are written in PHP and use the [Azure SDK for PHP](../php-download-sdk.md).</span></span> <span data-ttu-id="510f7-106">Kapsamdaki senaryolar dahil **konuları ve abonelikleri oluşturma**, **abonelik filtreleri oluşturma**, **konu başlığına ileti gönderme**, **abonelikten ileti alma**, ve **konuları ve abonelikleri silmeyi**.</span><span class="sxs-lookup"><span data-stu-id="510f7-106">The scenarios covered include **creating topics and subscriptions**, **creating subscription filters**, **sending messages to a topic**, **receiving messages from a subscription**, and **deleting topics and subscriptions**.</span></span>

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

## <a name="create-a-php-application"></a><span data-ttu-id="510f7-107">PHP uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="510f7-107">Create a PHP application</span></span>
<span data-ttu-id="510f7-108">Azure Blob hizmete erişen bir PHP uygulaması oluşturmak için yalnızca sınıflarda başvurmak için gereksinimdir [PHP için Azure SDK](../php-download-sdk.md) gelen kodunuzu içinde.</span><span class="sxs-lookup"><span data-stu-id="510f7-108">The only requirement for creating a PHP application that accesses the Azure Blob service is to reference classes in the [Azure SDK for PHP](../php-download-sdk.md) from within your code.</span></span> <span data-ttu-id="510f7-109">Herhangi bir geliştirme aracı, uygulama veya Notepad oluşturmak için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="510f7-109">You can use any development tools to create your application, or Notepad.</span></span>

> [!NOTE]
> <span data-ttu-id="510f7-110">PHP yüklemenizi de olmalıdır [OpenSSL uzantısı](http://php.net/openssl) yüklenir ve etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="510f7-110">Your PHP installation must also have the [OpenSSL extension](http://php.net/openssl) installed and enabled.</span></span>
> 
> 

<span data-ttu-id="510f7-111">Bu makalede, bir PHP uygulamanızda yerel olarak veya bir Azure web rolü, çalışan rolü veya Web sitesi içinde çalışan kodu çağrılabilir hizmet özelliklerini kullanmayı açıklar.</span><span class="sxs-lookup"><span data-stu-id="510f7-111">This article describes how to use service features that can be called within a PHP application locally, or in code running within an Azure web role, worker role, or website.</span></span>

## <a name="get-the-azure-client-libraries"></a><span data-ttu-id="510f7-112">Azure istemci kitaplıkları Al</span><span class="sxs-lookup"><span data-stu-id="510f7-112">Get the Azure client libraries</span></span>
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-to-use-service-bus"></a><span data-ttu-id="510f7-113">Service Bus hizmetini kullanmak için uygulamanızı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="510f7-113">Configure your application to use Service Bus</span></span>
<span data-ttu-id="510f7-114">Service Bus API'lerine kullanmak için:</span><span class="sxs-lookup"><span data-stu-id="510f7-114">To use the Service Bus APIs:</span></span>

1. <span data-ttu-id="510f7-115">Otomatik Yükleyiciden kullanarak dosya başvuru [require_once] [ require-once] deyimi.</span><span class="sxs-lookup"><span data-stu-id="510f7-115">Reference the autoloader file using the [require_once][require-once] statement.</span></span>
2. <span data-ttu-id="510f7-116">Kullanabileceğinize sınıfları başvuru.</span><span class="sxs-lookup"><span data-stu-id="510f7-116">Reference any classes you might use.</span></span>

<span data-ttu-id="510f7-117">Aşağıdaki örnek otomatik Yükleyiciden dosya ve başvuru dahil gösterilmektedir **ServiceBusService** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="510f7-117">The following example shows how to include the autoloader file and reference the **ServiceBusService** class.</span></span>

> [!NOTE]
> <span data-ttu-id="510f7-118">Bu örnek (ve diğer örnekleri bu makalede) oluşturucu aracılığıyla Azure için PHP istemci kitaplıkları yüklü olduğunu varsayar.</span><span class="sxs-lookup"><span data-stu-id="510f7-118">This example (and other examples in this article) assumes you have installed the PHP Client Libraries for Azure via Composer.</span></span> <span data-ttu-id="510f7-119">El ile veya bir ARMUTLU paketi olarak kitaplıkları yüklediyseniz, başvurmalıdır **WindowsAzure.php** otomatik yükleyici dosyası.</span><span class="sxs-lookup"><span data-stu-id="510f7-119">If you installed the libraries manually or as a PEAR package, you must reference the **WindowsAzure.php** autoloader file.</span></span>
> 
> 

```php
require_once 'vendor\autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

<span data-ttu-id="510f7-120">Aşağıdaki örneklerde, `require_once` deyimi her zaman gösterilecek, ancak yalnızca örnek yürütmek gerekli sınıfları başvurulur.</span><span class="sxs-lookup"><span data-stu-id="510f7-120">In the following examples, the `require_once` statement will always be shown, but only the classes necessary for the example to execute are referenced.</span></span>

## <a name="set-up-a-service-bus-connection"></a><span data-ttu-id="510f7-121">Hizmet veri yolu bağlantı kurma</span><span class="sxs-lookup"><span data-stu-id="510f7-121">Set up a Service Bus connection</span></span>
<span data-ttu-id="510f7-122">Service Bus istemci örneği oluşturmak için önce geçerli bir bağlantı dizesi şu biçimde olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="510f7-122">To instantiate a Service Bus client you must first have a valid connection string in this format:</span></span>

```
Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]
```

<span data-ttu-id="510f7-123">Burada `Endpoint` genellikle biçimidir `https://[yourNamespace].servicebus.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="510f7-123">Where `Endpoint` is typically of the format `https://[yourNamespace].servicebus.windows.net`.</span></span>

<span data-ttu-id="510f7-124">Kullanmalısınız herhangi bir Azure hizmeti istemcisi oluşturmak için `ServicesBuilder` sınıfı.</span><span class="sxs-lookup"><span data-stu-id="510f7-124">To create any Azure service client you must use the `ServicesBuilder` class.</span></span> <span data-ttu-id="510f7-125">Şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="510f7-125">You can:</span></span>

* <span data-ttu-id="510f7-126">Bağlantı dizesi doğrudan geçirin.</span><span class="sxs-lookup"><span data-stu-id="510f7-126">Pass the connection string directly to it.</span></span>
* <span data-ttu-id="510f7-127">kullanmak **CloudConfigurationManager (CCM)** bağlantı dizesi için dış kaynaklardan denetlemek için:</span><span class="sxs-lookup"><span data-stu-id="510f7-127">Use the **CloudConfigurationManager (CCM)** to check multiple external sources for the connection string:</span></span>
  * <span data-ttu-id="510f7-128">Varsayılan olarak, bir dış kaynak - ortam değişkenleri desteği ile birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="510f7-128">By default it comes with support for one external source - environmental variables.</span></span>
  * <span data-ttu-id="510f7-129">Genişleterek yeni kaynakları ekleyebilirsiniz `ConnectionStringSource` sınıfı.</span><span class="sxs-lookup"><span data-stu-id="510f7-129">You can add new sources by extending the `ConnectionStringSource` class.</span></span>

<span data-ttu-id="510f7-130">Burada özetlenen örnekler için bağlantı dizesi doğrudan geçirilir.</span><span class="sxs-lookup"><span data-stu-id="510f7-130">For the examples outlined here, the connection string is passed directly.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$connectionString = "Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]";

$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);
```

## <a name="create-a-topic"></a><span data-ttu-id="510f7-131">Konu başlığı oluşturma</span><span class="sxs-lookup"><span data-stu-id="510f7-131">Create a topic</span></span>
<span data-ttu-id="510f7-132">Service Bus konu başlıklarına yönelik yönetim işlemlerini gerçekleştirebilirsiniz `ServiceBusRestProxy` sınıfı.</span><span class="sxs-lookup"><span data-stu-id="510f7-132">You can perform management operations for Service Bus topics via the `ServiceBusRestProxy` class.</span></span> <span data-ttu-id="510f7-133">A `ServiceBusRestProxy` nesnesi aracılığıyla yapılandırılmıştır `ServicesBuilder::createServiceBusService` yönetmek için belirteç izinleri yalıtan bir uygun bir bağlantı dizesi ile Üreteç yöntemi.</span><span class="sxs-lookup"><span data-stu-id="510f7-133">A `ServiceBusRestProxy` object is constructed via the `ServicesBuilder::createServiceBusService` factory method with an appropriate connection string that encapsulates the token permissions to manage it.</span></span>

<span data-ttu-id="510f7-134">Aşağıdaki örnek örneği gösterilmektedir bir `ServiceBusRestProxy` ve arama `ServiceBusRestProxy->createTopic` adlandırılan bir konu oluşturmak için `mytopic` içinde bir `MySBNamespace` ad alanı:</span><span class="sxs-lookup"><span data-stu-id="510f7-134">The following example shows how to instantiate a `ServiceBusRestProxy` and call `ServiceBusRestProxy->createTopic` to create a topic named `mytopic` within a `MySBNamespace` namespace:</span></span>

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
> <span data-ttu-id="510f7-135">Kullanabileceğiniz `listTopics` yöntemi `ServiceBusRestProxy` nesneleri zaten bir hizmet ad alanında belirtilen ada sahip bir konu var olup olmadığını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="510f7-135">You can use the `listTopics` method on `ServiceBusRestProxy` objects to check if a topic with a specified name already exists within a service namespace.</span></span>
> 
> 

## <a name="create-a-subscription"></a><span data-ttu-id="510f7-136">Abonelik oluşturma</span><span class="sxs-lookup"><span data-stu-id="510f7-136">Create a subscription</span></span>
<span data-ttu-id="510f7-137">Konu aboneliklerini içeren de oluşturulur `ServiceBusRestProxy->createSubscription` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="510f7-137">Topic subscriptions are also created with the `ServiceBusRestProxy->createSubscription` method.</span></span> <span data-ttu-id="510f7-138">Abonelikler adlandırılır ve aboneliğin sanal kuyruğuna gönderilen ileti kümesini sınırlayan isteğe bağlı bir filtre içerebilir.</span><span class="sxs-lookup"><span data-stu-id="510f7-138">Subscriptions are named and can have an optional filter that restricts the set of messages passed to the subscription's virtual queue.</span></span>

### <a name="create-a-subscription-with-the-default-matchall-filter"></a><span data-ttu-id="510f7-139">Varsayılan (MatchAll) filtreyle abonelik oluşturma</span><span class="sxs-lookup"><span data-stu-id="510f7-139">Create a subscription with the default (MatchAll) filter</span></span>
<span data-ttu-id="510f7-140">**MatchAll** filtresi, yeni bir abonelik oluşturulurken filtre belirtilmeyen durumlarda kullanılan varsayılan filtredir.</span><span class="sxs-lookup"><span data-stu-id="510f7-140">The **MatchAll** filter is the default filter that is used if no filter is specified when a new subscription is created.</span></span> <span data-ttu-id="510f7-141">Zaman **MatchAll** filtre kullanıldığında, konu başlığında yayımlanan tüm iletiler aboneliğin sanal kuyruğuna yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="510f7-141">When the **MatchAll** filter is used, all messages published to the topic are placed in the subscription's virtual queue.</span></span> <span data-ttu-id="510f7-142">Aşağıdaki örnekte 'mysubscription' adlı bir abonelik oluşturulur ve varsayılan **MatchAll** Filtresi.</span><span class="sxs-lookup"><span data-stu-id="510f7-142">The following example creates a subscription named 'mysubscription' and uses the default **MatchAll** filter.</span></span>

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

### <a name="create-subscriptions-with-filters"></a><span data-ttu-id="510f7-143">Filtre içeren abonelik oluşturma</span><span class="sxs-lookup"><span data-stu-id="510f7-143">Create subscriptions with filters</span></span>
<span data-ttu-id="510f7-144">Bir konu başlığına gönderilen iletilerden hangilerinin belirli bir konu başlığı aboneliğinde görüneceğini belirlemenize olanak sağlayan filtreler de ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="510f7-144">You can also set up filters that enable you to specify which messages sent to a topic should appear within a specific topic subscription.</span></span> <span data-ttu-id="510f7-145">Filtre abonelikler tarafından desteklenen en esnek türü [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter), SQL92 alt kümesi uygular.</span><span class="sxs-lookup"><span data-stu-id="510f7-145">The most flexible type of filter supported by subscriptions is the [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter), which implements a subset of SQL92.</span></span> <span data-ttu-id="510f7-146">SQL filtreleri, konu başlığında yayımlanan iletilerin özelliklerinde çalışır.</span><span class="sxs-lookup"><span data-stu-id="510f7-146">SQL filters operate on the properties of the messages that are published to the topic.</span></span> <span data-ttu-id="510f7-147">SqlFilters hakkında daha fazla bilgi için bkz: [SqlFilter.SqlExpression özelliği][sqlfilter].</span><span class="sxs-lookup"><span data-stu-id="510f7-147">For more information about SqlFilters, see [SqlFilter.SqlExpression Property][sqlfilter].</span></span>

> [!NOTE]
> <span data-ttu-id="510f7-148">Bir abonelikte her bir kural kendi sonuç iletileri için abonelik ekleme gelen iletileri bağımsız olarak işler.</span><span class="sxs-lookup"><span data-stu-id="510f7-148">Each rule on a subscription processes incoming messages independently, adding their result messages to the subscription.</span></span> <span data-ttu-id="510f7-149">Ayrıca, her yeni abonelik varsayılan sahip **kural** tüm iletileri konusundan aboneliğine ekler bir filtre ile nesne.</span><span class="sxs-lookup"><span data-stu-id="510f7-149">In addition, each new subscription has a default **Rule** object with a filter that adds all messages from the topic to the subscription.</span></span> <span data-ttu-id="510f7-150">Filtrenizle eşleşen iletileri almak için varsayılan kuralı kaldırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="510f7-150">To receive only messages matching your filter, you must remove the default rule.</span></span> <span data-ttu-id="510f7-151">Varsayılan kural kullanarak kaldırabilirsiniz `ServiceBusRestProxy->deleteRule` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="510f7-151">You can remove the default rule by using the `ServiceBusRestProxy->deleteRule` method.</span></span>
> 
> 

<span data-ttu-id="510f7-152">Aşağıdaki örnek adlı bir abonelik oluşturur `HighMessages` ile bir **SqlFilter** özel iletileri yalnızca seçer `MessageNumber` özelliği 3'ten büyük.</span><span class="sxs-lookup"><span data-stu-id="510f7-152">The following example creates a subscription named `HighMessages` with a **SqlFilter** that only selects messages that have a custom `MessageNumber` property greater than 3.</span></span> <span data-ttu-id="510f7-153">Bkz: [konu başlığına ileti gönderme](#send-messages-to-a-topic) iletileri özel özellikler ekleme hakkında bilgi.</span><span class="sxs-lookup"><span data-stu-id="510f7-153">See [Send messages to a topic](#send-messages-to-a-topic) for information about adding custom properties to messages.</span></span>

```php
$subscriptionInfo = new SubscriptionInfo("HighMessages");
$serviceBusRestProxy->createSubscription("mytopic", $subscriptionInfo);

$serviceBusRestProxy->deleteRule("mytopic", "HighMessages", '$Default');

$ruleInfo = new RuleInfo("HighMessagesRule");
$ruleInfo->withSqlFilter("MessageNumber > 3");
$ruleResult = $serviceBusRestProxy->createRule("mytopic", "HighMessages", $ruleInfo);
```

<span data-ttu-id="510f7-154">Bu kod ek bir ad alanı kullanılmasını gerektiren Not: `WindowsAzure\ServiceBus\Models\SubscriptionInfo`.</span><span class="sxs-lookup"><span data-stu-id="510f7-154">Note that this code requires the use of an additional namespace: `WindowsAzure\ServiceBus\Models\SubscriptionInfo`.</span></span>

<span data-ttu-id="510f7-155">Benzer şekilde, aşağıdaki örnekte adlı bir abonelik oluşturulur `LowMessages` ile bir `SqlFilter` olan iletiler yalnızca seçer bir `MessageNumber` özelliğine daha az veya bu değere eşit 3.</span><span class="sxs-lookup"><span data-stu-id="510f7-155">Similarly, the following example creates a subscription named `LowMessages` with a `SqlFilter` that only selects messages that have a `MessageNumber` property less than or equal to 3.</span></span>

```php
$subscriptionInfo = new SubscriptionInfo("LowMessages");
$serviceBusRestProxy->createSubscription("mytopic", $subscriptionInfo);

$serviceBusRestProxy->deleteRule("mytopic", "LowMessages", '$Default');

$ruleInfo = new RuleInfo("LowMessagesRule");
$ruleInfo->withSqlFilter("MessageNumber <= 3");
$ruleResult = $serviceBusRestProxy->createRule("mytopic", "LowMessages", $ruleInfo);
```

<span data-ttu-id="510f7-156">Şimdi, ne zaman bir ileti gönderilir `mytopic` konu her zaman teslim alıcılara `mysubscription` aboneliği ve alıcılara teslim seçmeli olarak `HighMessages` ve `LowMessages` (bağlı olarak abonelikleri ileti içeriği).</span><span class="sxs-lookup"><span data-stu-id="510f7-156">Now, when a message is sent to the `mytopic` topic, it is always delivered to receivers subscribed to the `mysubscription` subscription, and selectively delivered to receivers subscribed to the `HighMessages` and `LowMessages` subscriptions (depending upon the message content).</span></span>

## <a name="send-messages-to-a-topic"></a><span data-ttu-id="510f7-157">Konu başlığına ileti gönderme</span><span class="sxs-lookup"><span data-stu-id="510f7-157">Send messages to a topic</span></span>
<span data-ttu-id="510f7-158">Uygulama çağrılarınızı bir Service Bus konu başlığına bir ileti göndermek için `ServiceBusRestProxy->sendTopicMessage` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="510f7-158">To send a message to a Service Bus topic, your application calls the `ServiceBusRestProxy->sendTopicMessage` method.</span></span> <span data-ttu-id="510f7-159">Aşağıdaki kod bir ileti göndermek nasıl gösterir `mytopic` konu içinde daha önce oluşturduğunuz `MySBNamespace` hizmet ad alanı.</span><span class="sxs-lookup"><span data-stu-id="510f7-159">The following code shows how to send a message to the `mytopic` topic previously created within the `MySBNamespace` service namespace.</span></span>

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

<span data-ttu-id="510f7-160">Service Bus konu başlıklarına gönderilen iletiler örnekleridir [BrokeredMessage] [ BrokeredMessage] sınıfı.</span><span class="sxs-lookup"><span data-stu-id="510f7-160">Messages sent to Service Bus topics are instances of the [BrokeredMessage][BrokeredMessage] class.</span></span> <span data-ttu-id="510f7-161">[BrokeredMessage] [ BrokeredMessage] nesnelerinin standart özellikleri ve yöntemleri yanı sıra, uygulamaya özgü özel özellikleri tutmak için kullanılan özellikler kümesi vardır.</span><span class="sxs-lookup"><span data-stu-id="510f7-161">[BrokeredMessage][BrokeredMessage] objects have a set of standard properties and methods, as well as properties that can be used to hold custom application-specific properties.</span></span> <span data-ttu-id="510f7-162">Aşağıdaki örnek 5 sınama iletileri göndermek nasıl gösterir `mytopic` daha önce oluşturulan konu.</span><span class="sxs-lookup"><span data-stu-id="510f7-162">The following example shows how to send 5 test messages to the `mytopic` topic previously created.</span></span> <span data-ttu-id="510f7-163">`setProperty` Yöntemi bir özel özellik eklemek için kullanılır (`MessageNumber`) her ileti için.</span><span class="sxs-lookup"><span data-stu-id="510f7-163">The `setProperty` method is used to add a custom property (`MessageNumber`) to each message.</span></span> <span data-ttu-id="510f7-164">Unutmayın `MessageNumber` özellik değeri değişir her ileti için (gösterildiği gibi alacak abonelikleri belirlemek için bu değeri kullanın [abonelik oluşturma](#create-a-subscription) bölümü):</span><span class="sxs-lookup"><span data-stu-id="510f7-164">Note that the `MessageNumber` property value varies on each message (you can use this value to determine which subscriptions receive it, as shown in the [Create a subscription](#create-a-subscription) section):</span></span>

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

<span data-ttu-id="510f7-165">Service Bus konu başlıkları, [Standart katmanda](service-bus-premium-messaging.md) maksimum 256 KB ve [Premium katmanda](service-bus-premium-messaging.md) maksimum 1 MB ileti boyutunu destekler.</span><span class="sxs-lookup"><span data-stu-id="510f7-165">Service Bus topics support a maximum message size of 256 KB in the [Standard tier](service-bus-premium-messaging.md) and 1 MB in the [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="510f7-166">Standart ve özel uygulama özelliklerini içeren üst bilginin maksimum dosya boyutu 64 KB olabilir.</span><span class="sxs-lookup"><span data-stu-id="510f7-166">The header, which includes the standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="510f7-167">Konu başlığında tutulan ileti sayısına ilişkin bir sınır yoktur ancak konu başlığı tarafından tutulan iletilerin toplam boyutu için uç sınır vardır.</span><span class="sxs-lookup"><span data-stu-id="510f7-167">There is no limit on the number of messages held in a topic but there is a cap on the total size of the messages held by a topic.</span></span> <span data-ttu-id="510f7-168">Bu konu başlığı boyutu üst sınır 5 GB'tır.</span><span class="sxs-lookup"><span data-stu-id="510f7-168">This upper limit on topic size is 5 GB.</span></span> <span data-ttu-id="510f7-169">Kotalar hakkında daha fazla bilgi için bkz: [Service Bus kotaları][Service Bus quotas].</span><span class="sxs-lookup"><span data-stu-id="510f7-169">For more information about quotas, see [Service Bus quotas][Service Bus quotas].</span></span>

## <a name="receive-messages-from-a-subscription"></a><span data-ttu-id="510f7-170">Abonelikten ileti alma</span><span class="sxs-lookup"><span data-stu-id="510f7-170">Receive messages from a subscription</span></span>
<span data-ttu-id="510f7-171">Abonelikten ileti almak için en iyi yolu bir `ServiceBusRestProxy->receiveSubscriptionMessage` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="510f7-171">The best way to receive messages from a subscription is to use a `ServiceBusRestProxy->receiveSubscriptionMessage` method.</span></span> <span data-ttu-id="510f7-172">İletileri iki farklı modda alınan: [ *ReceiveAndDelete* ve *PeekLock*](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode).</span><span class="sxs-lookup"><span data-stu-id="510f7-172">Messages can be received in two different modes: [*ReceiveAndDelete* and *PeekLock*](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode).</span></span> <span data-ttu-id="510f7-173">**PeekLock** varsayılan değerdir.</span><span class="sxs-lookup"><span data-stu-id="510f7-173">**PeekLock** is the default.</span></span>

<span data-ttu-id="510f7-174">[ReceiveAndDelete](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) modunu kullanırken alma işlemi tek aşamalıdır. Service Bus abonelikte bir iletiye yönelik okuma isteği aldığında, iletiyi kullanılıyor olarak işaretler ve uygulamaya döndürür.</span><span class="sxs-lookup"><span data-stu-id="510f7-174">When using the [ReceiveAndDelete](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) mode, receive is a single-shot operation; that is, when Service Bus receives a read request for a message in a subscription, it marks the message as being consumed and returns it to the application.</span></span> <span data-ttu-id="510f7-175">[ReceiveAndDelete](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) * modu en basit modeldir ve senaryoları bir uygulama içinde tolerans bir arıza olması durumunda bir ileti işlenirken değil en iyi şekilde çalışır.</span><span class="sxs-lookup"><span data-stu-id="510f7-175">[ReceiveAndDelete](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) * mode is the simplest model and works best for scenarios in which an application can tolerate not processing a message in the event of a failure.</span></span> <span data-ttu-id="510f7-176">Bu durumu daha iyi anlamak için müşterinin bir alma isteği bildirdiğini ve bu isteğin işlenmeden çöktüğünü varsayın.</span><span class="sxs-lookup"><span data-stu-id="510f7-176">To understand this, consider a scenario in which the consumer issues the receive request and then crashes before processing it.</span></span> <span data-ttu-id="510f7-177">Service Bus iletiyi kullanılıyor olarak işaretlenmiş nedeniyle uygulama yeniden başlatılıp iletileri tekrar kullanmaya başladığında, sonra da çökmenin öncesinde kullanılan iletiyi atlamış olur.</span><span class="sxs-lookup"><span data-stu-id="510f7-177">Because Service Bus will have marked the message as being consumed, then when the application restarts and begins consuming messages again, it will have missed the message that was consumed prior to the crash.</span></span>

<span data-ttu-id="510f7-178">Varsayılan [PeekLock](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) bir ileti alma modu, iletilere veremeyen uygulamaları desteklemenin mümkün kılar bir iki aşamalı işlemi haline gelir.</span><span class="sxs-lookup"><span data-stu-id="510f7-178">In the default [PeekLock](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) mode, receiving a message becomes a two stage operation, which makes it possible to support applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="510f7-179">Service Bus bir istek aldığında bir sonraki kullanılacak iletiyi bulur, diğer tüketicilerin bu iletiyi almasını engellemek için kilitler ve ardından uygulamaya döndürür.</span><span class="sxs-lookup"><span data-stu-id="510f7-179">When Service Bus receives a request, it finds the next message to be consumed, locks it to prevent other consumers receiving it, and then returns it to the application.</span></span> <span data-ttu-id="510f7-180">Uygulama iletiyi işlemeyi tamamladıktan sonra (veya sonra işlemek için depoladıktan sonra), alınan ileti geçirerek alma işleminin ikinci aşamasını tamamlar `ServiceBusRestProxy->deleteMessage`.</span><span class="sxs-lookup"><span data-stu-id="510f7-180">After the application finishes processing the message (or stores it reliably for future processing), it completes the second stage of the receive process by passing the received message to `ServiceBusRestProxy->deleteMessage`.</span></span> <span data-ttu-id="510f7-181">Hizmet veri yolu gördüğünde `deleteMessage` çağrısı iletiyi kullanılıyor olarak işaretler ve kuyruktan kaldırın.</span><span class="sxs-lookup"><span data-stu-id="510f7-181">When Service Bus sees the `deleteMessage` call, it will mark the message as being consumed and remove it from the queue.</span></span>

<span data-ttu-id="510f7-182">Aşağıdaki örnek, almak ve bir iletiyi kullanarak işlemek gösterilmiştir [PeekLock](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) modu (varsayılan).</span><span class="sxs-lookup"><span data-stu-id="510f7-182">The following example shows how to receive and process a message using [PeekLock](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) mode (the default mode).</span></span> 

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use WindowsAzure\Common\ServiceException;
use WindowsAzure\ServiceBus\Models\ReceiveMessageOptions;

// Create Service Bus REST proxy.
$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);

try    {
    // Set receive mode to PeekLock (default is ReceiveAndDelete)
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

## <a name="how-to-handle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="510f7-183">Nasıl yapılır: uygulama çökmelerini ve Okunmayan iletileri işleme</span><span class="sxs-lookup"><span data-stu-id="510f7-183">How to: handle application crashes and unreadable messages</span></span>
<span data-ttu-id="510f7-184">Service Bus, uygulamanızda gerçekleşen hataları veya ileti işlenirken oluşan zorlukları rahat bir şekilde ortadan kaldırmanıza yardımcı olmak için işlevsellik sağlar.</span><span class="sxs-lookup"><span data-stu-id="510f7-184">Service Bus provides functionality to help you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="510f7-185">Alıcı uygulamanın iletiyi herhangi bir nedenden dolayı işleyemedi sonra işleyememesi `unlockMessage` alınan iletide yöntemi (yerine `deleteMessage` yöntemi).</span><span class="sxs-lookup"><span data-stu-id="510f7-185">If a receiver application is unable to process the message for some reason, then it can call the `unlockMessage` method on the received message (instead of the `deleteMessage` method).</span></span> <span data-ttu-id="510f7-186">Bu, Service Bus hizmetinin Kuyruktaki iletinin kilidini açmasına ve iletiyi aynı veya başka bir kullanıcı uygulama tarafından tekrar alınabilir hale getirmesine neden olur.</span><span class="sxs-lookup"><span data-stu-id="510f7-186">This will cause Service Bus to unlock the message within the queue and make it available to be received again, either by the same consuming application or by another consuming application.</span></span>

<span data-ttu-id="510f7-187">Ayrıca kuyrukta kilitlenen iletiye ilişkin bir zaman aşımı vardır ve uygulama önce iletiyi işleyemezse (örneğin, uygulama çökerse) hizmet veri yolu ileti otomatik olarak kilidini açmasına ve tekrar alınabilir hale kilit zaman aşımı dolmadan.</span><span class="sxs-lookup"><span data-stu-id="510f7-187">There is also a timeout associated with a message locked within the queue, and if the application fails to process the message before the lock timeout expires (for example, if the application crashes), then Service Bus will unlock the message automatically and make it available to be received again.</span></span>

<span data-ttu-id="510f7-188">Uygulama iletiyi ancak önce çökmesi durumunda, `deleteMessage` isteği bildirilmeden, sonra yeniden başlatıldığında ileti uygulamaya tekrar teslim edilir.</span><span class="sxs-lookup"><span data-stu-id="510f7-188">In the event that the application crashes after processing the message but before the `deleteMessage` request is issued, then the message will be redelivered to the application when it restarts.</span></span> <span data-ttu-id="510f7-189">Bu genellikle adlandırılır *en az bir kez* diğer bir deyişle, her ileti en az bir kez işlenir işleme; ancak belirli durumlarda aynı ileti yeniden teslim.</span><span class="sxs-lookup"><span data-stu-id="510f7-189">This is often called *At Least Once* processing; that is, each message is processed at least once but in certain situations the same message may be redelivered.</span></span> <span data-ttu-id="510f7-190">Senaryo yinelenen işlemeyi kabul etmiyorsa, uygulama geliştiricilerinin yinelenen ileti teslimine uygulamalar için ek mantık eklemelisiniz.</span><span class="sxs-lookup"><span data-stu-id="510f7-190">If the scenario cannot tolerate duplicate processing, then application developers should add additional logic to applications to handle duplicate message delivery.</span></span> <span data-ttu-id="510f7-191">Bu genellikle kullanılarak elde edilen `getMessageId` iletinin teslimat denemelerinde yöntemi.</span><span class="sxs-lookup"><span data-stu-id="510f7-191">This is often achieved using the `getMessageId` method of the message, which remains constant across delivery attempts.</span></span>

## <a name="delete-topics-and-subscriptions"></a><span data-ttu-id="510f7-192">Konu başlıklarını ve abonelikleri silme</span><span class="sxs-lookup"><span data-stu-id="510f7-192">Delete topics and subscriptions</span></span>
<span data-ttu-id="510f7-193">Bir konu veya abonelik silmek için kullanın `ServiceBusRestProxy->deleteTopic` veya `ServiceBusRestProxy->deleteSubscripton` yöntemleri, sırasıyla.</span><span class="sxs-lookup"><span data-stu-id="510f7-193">To delete a topic or a subscription, use the `ServiceBusRestProxy->deleteTopic` or the `ServiceBusRestProxy->deleteSubscripton` methods, respectively.</span></span> <span data-ttu-id="510f7-194">Konu başlığı silindiğinde, konu başlığıyla kaydedilen tüm abonelikler de silinir olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="510f7-194">Note that deleting a topic also deletes any subscriptions that are registered with the topic.</span></span>

<span data-ttu-id="510f7-195">Aşağıdaki örnek, adlandırılan bir konu silmek gösterilmiştir `mytopic` ve kayıtlı abonelikler.</span><span class="sxs-lookup"><span data-stu-id="510f7-195">The following example shows how to delete a topic named `mytopic` and its registered subscriptions.</span></span>

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

<span data-ttu-id="510f7-196">Kullanarak `deleteSubscription` yöntemi, bir abonelik bağımsız olarak silebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="510f7-196">By using the `deleteSubscription` method, you can delete a subscription independently:</span></span>

```php
$serviceBusRestProxy->deleteSubscription("mytopic", "mysubscription");
```

## <a name="next-steps"></a><span data-ttu-id="510f7-197">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="510f7-197">Next steps</span></span>
<span data-ttu-id="510f7-198">Service Bus kuyruklarına öğrendiğinize göre bkz: [kuyruklar, konu başlıkları ve abonelikler] [ Queues, topics, and subscriptions] daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="510f7-198">Now that you've learned the basics of Service Bus queues, see [Queues, topics, and subscriptions][Queues, topics, and subscriptions] for more information.</span></span>

[BrokeredMessage]: https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.brokeredmessage
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[sqlfilter]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter
[require-once]: http://php.net/require_once
[Service Bus quotas]: service-bus-quotas.md
