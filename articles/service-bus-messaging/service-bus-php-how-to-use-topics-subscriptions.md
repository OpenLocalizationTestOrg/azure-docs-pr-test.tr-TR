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
# <a name="how-toouse-service-bus-topics-and-subscriptions-with-php"></a>Nasıl toouse Service Bus konuları ve abonelikleri PHP ile

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

Bu makale size nasıl gösterir toouse Service Bus konuları ve abonelikleri. Merhaba örnekler PHP ile yazılmıştır ve hello kullan [PHP için Azure SDK](../php-download-sdk.md). Merhaba kapsanan senaryolar dahil **konuları ve abonelikleri oluşturma**, **abonelik filtreleri oluşturma**, **iletileri tooa konu gönderme**, **alma bir abonelik iletilerden**, ve **konuları ve abonelikleri silmeyi**.

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

## <a name="create-a-php-application"></a>PHP uygulaması oluşturma
Merhaba tooreference sınıflarda hello Azure Blob hizmete erişen bir PHP uygulaması oluşturmaya yönelik gereksinim, yalnızca hello [PHP için Azure SDK](../php-download-sdk.md) gelen kodunuzu içinde. Uygulama veya Notepad tüm geliştirme araçları toocreate kullanabilirsiniz.

> [!NOTE]
> PHP yüklemenizi de hello olmalıdır [OpenSSL uzantısı](http://php.net/openssl) yüklenir ve etkinleştirilir.
> 
> 

Bu makalede nasıl toouse hizmet PHP uygulamanızda yerel olarak veya bir Azure web rolü, çalışan rolü veya Web sitesi içinde çalışan kodu çağrılabilir özellikleri açıklanmaktadır.

## <a name="get-hello-azure-client-libraries"></a>Hello Azure istemci kitaplıkları Al
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-toouse-service-bus"></a>Uygulama toouse Service Bus yapılandırın
toouse hello Service Bus API'lerine:

1. Hello kullanarak başvuru hello otomatik yükleyici dosyasını [require_once] [ require-once] deyimi.
2. Kullanabileceğinize sınıfları başvuru.

Merhaba aşağıdaki örnekte nasıl tooinclude hello otomatik Yükleyiciden dosya ve başvuru hello gösterir **ServiceBusService** sınıfı.

> [!NOTE]
> Bu örnek (ve diğer örnekleri bu makalede) hello PHP istemci kitaplıkları oluşturucu aracılığıyla Azure yüklü olduğunu varsayar. El ile veya bir ARMUTLU paketi olarak hello kitaplıkları yüklediyseniz, hello başvurmalıdır **WindowsAzure.php** otomatik yükleyici dosyası.
> 
> 

```php
require_once 'vendor\autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

Örnek hello hello `require_once` deyimi her zaman gösterilecek, ancak yalnızca hello sınıfları hello örnek tooexecute için gereken başvuru.

## <a name="set-up-a-service-bus-connection"></a>Hizmet veri yolu bağlantı kurma
tooinstantiate önce yapmalısınız Service Bus istemci geçerli bir bağlantı dizesi şu biçimde vardır:

```
Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]
```

Burada `Endpoint` genellikle hello biçimidir `https://[yourNamespace].servicebus.windows.net`.

toocreate hello kullanmalıdır herhangi bir Azure hizmeti istemci `ServicesBuilder` sınıfı. Şunları yapabilirsiniz:

* Merhaba bağlantı geçirmek doğrudan tooit dize.
* Kullanım hello **CloudConfigurationManager (CCM)** toocheck birden çok dış kaynaklardan hello bağlantı dizesi:
  * Varsayılan olarak, bir dış kaynak - ortam değişkenleri desteği ile birlikte gelir.
  * Merhaba genişleterek yeni kaynakları ekleyebilirsiniz `ConnectionStringSource` sınıfı.

Burada özetlenen hello örnekler için başlangıç bağlantı dizesi doğrudan geçirilir.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$connectionString = "Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]";

$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);
```

## <a name="create-a-topic"></a>Konu başlığı oluşturma
Merhaba üzerinden Service Bus konu başlıklarına yönelik yönetim işlemlerini gerçekleştirebilirsiniz `ServiceBusRestProxy` sınıfı. A `ServiceBusRestProxy` nesne hello oluşturulan `ServicesBuilder::createServiceBusService` Üreteç yöntemi hello belirteci izinleri toomanage yalıtan bir uygun bir bağlantı dizesi ile.

örnekte gösterildiği nasıl aşağıdaki hello tooinstantiate bir `ServiceBusRestProxy` ve arama `ServiceBusRestProxy->createTopic` toocreate adlandırılan bir konu `mytopic` içinde bir `MySBNamespace` ad alanı:

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
> Merhaba kullanabilirsiniz `listTopics` yöntemi `ServiceBusRestProxy` bir hizmet ad alanında belirtilen ada sahip bir konu zaten varsa toocheck nesneleri.
> 
> 

## <a name="create-a-subscription"></a>Abonelik oluşturma
Konu aboneliklerini ayrıca hello ile oluşturulan `ServiceBusRestProxy->createSubscription` yöntemi. Abonelikler adlandırılır ve hello toohello aboneliğin sanal kuyruğuna gönderilen ileti kümesini sınırlayan isteğe bağlı bir filtre içerebilir.

### <a name="create-a-subscription-with-hello-default-matchall-filter"></a>Merhaba varsayılan (MatchAll) filtreyle abonelik oluşturma
Merhaba **MatchAll** yeni bir abonelik oluşturulurken filtre belirtilmeyen varsa, kullanılan hello varsayılan filtre filtredir. Ne zaman hello **MatchAll** filtre kullanıldığında, tüm iletileri yayımlanan toohello konu hello aboneliğin sanal kuyruğuna yerleştirilir. Merhaba aşağıdaki örnekte 'mysubscription' adlı bir abonelik oluşturur ve kullanır hello varsayılan **MatchAll** Filtresi.

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

### <a name="create-subscriptions-with-filters"></a>Filtre içeren abonelik oluşturma
Hangi iletilerin tooa konu içinde belirli konu aboneliği görünmelidir gönderilen toospecify etkinleştirmek filtreler de ayarlayabilirsiniz. Merhaba en esnek filtre abonelikler tarafından desteklenen hello türünde [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter), SQL92 alt kümesi uygular. SQL filtreleri yayımlanan toohello konu hello iletilerinin hello özelliklerini çalışır. SqlFilters hakkında daha fazla bilgi için bkz: [SqlFilter.SqlExpression özelliği][sqlfilter].

> [!NOTE]
> Bir abonelikte her bir kural sonuç iletileri toohello aboneliğini ekleme gelen iletileri bağımsız olarak işler. Ayrıca, her yeni abonelik varsayılan sahip **kural** tüm iletileri hello konu toohello abonelikten ekler bir filtre ile nesne. filtrenizle eşleşen tooreceive yalnızca iletiler hello varsayılan kural kaldırmanız gerekir. Hello kullanarak hello varsayılan kural kaldırabilirsiniz `ServiceBusRestProxy->deleteRule` yöntemi.
> 
> 

Merhaba aşağıdaki örnek adlı bir abonelik oluşturulur `HighMessages` ile bir **SqlFilter** özel iletileri yalnızca seçer `MessageNumber` özelliği 3'ten büyük. Bkz: [gönderme iletileri tooa konu](#send-messages-to-a-topic) özel özellikler toomessages ekleme hakkında bilgi.

```php
$subscriptionInfo = new SubscriptionInfo("HighMessages");
$serviceBusRestProxy->createSubscription("mytopic", $subscriptionInfo);

$serviceBusRestProxy->deleteRule("mytopic", "HighMessages", '$Default');

$ruleInfo = new RuleInfo("HighMessagesRule");
$ruleInfo->withSqlFilter("MessageNumber > 3");
$ruleResult = $serviceBusRestProxy->createRule("mytopic", "HighMessages", $ruleInfo);
```

Bu kod ek bir ad alanı hello kullanılmasını gerektiren Not: `WindowsAzure\ServiceBus\Models\SubscriptionInfo`.

Benzer şekilde, hello aşağıdaki örnek adlı bir abonelik oluşturur `LowMessages` ile bir `SqlFilter` olan iletiler yalnızca seçer bir `MessageNumber` özelliği daha az veya bu değere eşit too3.

```php
$subscriptionInfo = new SubscriptionInfo("LowMessages");
$serviceBusRestProxy->createSubscription("mytopic", $subscriptionInfo);

$serviceBusRestProxy->deleteRule("mytopic", "LowMessages", '$Default');

$ruleInfo = new RuleInfo("LowMessagesRule");
$ruleInfo->withSqlFilter("MessageNumber <= 3");
$ruleResult = $serviceBusRestProxy->createRule("mytopic", "LowMessages", $ruleInfo);
```

Şimdi, ne zaman bir ileti gönderilir toohello `mytopic` konuya abone tooreceivers toohello her zaman teslim `mysubscription` abonelik ve abone olunan seçmeli olarak teslim tooreceivers toohello `HighMessages` ve `LowMessages` abonelikleri ( Merhaba ileti içeriği bağlı olarak).

## <a name="send-messages-tooa-topic"></a>İletileri tooa konu gönderin
toosend ileti tooa Service Bus konu, uygulamanızı çağırır hello `ServiceBusRestProxy->sendTopicMessage` yöntemi. kodun gösterdiği nasıl aşağıdaki hello toosend ileti toohello `mytopic` konu içinde daha önce oluşturduğunuz `MySBNamespace` hizmet ad alanı.

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

İletileri gönderilir tooService veri yolu konuları hello örneklerini [BrokeredMessage] [ BrokeredMessage] sınıfı. [BrokeredMessage] [ BrokeredMessage] nesnelerinin standart özellikleri ve yöntemleri yanı sıra, kullanılan toohold özel uygulamaya özgü özellikleri olabilir özellikler kümesi vardır. Merhaba aşağıdaki örnekte nasıl toosend 5 test toohello iletileri gösterir `mytopic` daha önce oluşturulan konu. Merhaba `setProperty` yöntemdir kullanılan tooadd özel özelliğin (`MessageNumber`) tooeach ileti. Bu hello Not `MessageNumber` özellik değeri değişir her ileti için (hangi abonelik almak, bu değer toodetermine hello gösterildiği gibi kullanabilirsiniz [abonelik oluşturma](#create-a-subscription) bölümü):

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

Service Bus konu başlıklarını destek maksimum ileti boyutu 256 KB hello [standart katmanı](service-bus-premium-messaging.md) hello 1 MB [Premium katmanı](service-bus-premium-messaging.md). Merhaba standart ve özel uygulama özelliklerini içeren hello üstbilgi en büyük boyutu 64 KB olabilir. Merhaba konu başlığında tutulan ileti sayısına bir sınır yoktur ancak konu başlığı tarafından tutulan hello iletilerin toplam boyutu hello bir sınır yoktur. Bu konu başlığı boyutu üst sınır 5 GB'tır. Kotalar hakkında daha fazla bilgi için bkz: [Service Bus kotaları][Service Bus quotas].

## <a name="receive-messages-from-a-subscription"></a>Abonelikten ileti alma
Merhaba en iyi şekilde tooreceive iletileri bir aboneliğe ilişkin toouse olan bir `ServiceBusRestProxy->receiveSubscriptionMessage` yöntemi. İletileri iki farklı modda alınan: [ *ReceiveAndDelete* ve *PeekLock*](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode). **PeekLock** hello varsayılandır.

Merhaba kullanırken [ReceiveAndDelete](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) modu, alma bir tek işlemi; diğer bir deyişle, hizmet veri yolu bir abonelikte bir iletiye yönelik Okuma isteği aldığında, hello iletiyi kullanılıyor olarak işaretler ve toohello döndürür uygulama. [ReceiveAndDelete](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) * modu hello en basit modeldir ve senaryoları bir uygulama içinde tolerans bir hatanın hello Olay iletisinde işlenmiyor en iyi şekilde çalışır. toounderstand Bu, hangi hello tüketici sorunları hello alma isteği bir senaryo düşünün ve işlemeden önce çöküyor. Hizmet veri yolu selamlama iletisine hello uygulama yeniden başlatılıp iletileri tekrar kullanmaya başladığında olduğunda, ardından kullanılıyor olarak işaretlenmiş için onu olan hello iletiyi atlamış olur önceki toohello kilitlenme tüketilen.

Merhaba varsayılan [PeekLock](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) bir ileti alma modu, iletilere olası toosupport uygulamaları iki aşamalı işlemi haline gelir. Service Bus bir istek aldığında hello sonraki ileti toobe tüketilen, diğer tüketicilerin alırken tooprevent kilitler ve toohello uygulama döndürür bulur. Merhaba uygulaması hello iletiyi işlemeyi tamamladıktan sonra (veya sonra işlemek için depoladıktan sonra), hello hello ikinci aşamasını tamamlar alınan selamlama iletisine çok geçirerek alma işleminin`ServiceBusRestProxy->deleteMessage`. Hizmet veri yolu hello gördüğünde `deleteMessage` çağrısı hello iletiyi kullanılıyor olarak işaretler ve hello sıradan kaldırın.

örnekte gösterildiği nasıl aşağıdaki hello tooreceive ve bir iletiyi kullanarak işlem [PeekLock](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) (Merhaba varsayılan modu). 

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

## <a name="how-to-handle-application-crashes-and-unreadable-messages"></a>Nasıl yapılır: uygulama çökmelerini ve Okunmayan iletileri işleme
Hizmet veri yolu, gerçekleşen hataları uygulama ya da ileti işlenirken zorlukları rahat işlevselliği toohelp sağlar. Alıcı uygulamanın kaydedemediği tooprocess Merhaba ileti herhangi bir nedenden dolayı ardından hello çağırabilirsiniz `unlockMessage` hello alınan ileti üzerinde yöntemi (hello yerine `deleteMessage` yöntemi). Bu hizmet veri yolu toounlock selamlama iletisine hello sıra içinde neden ve yeniden alınan kullanılabilir toobe olun, ya da göre aynı uygulama veya başka bir kullanıcı uygulama tarafından tüketen hello.

Ayrıca hello kuyrukta kilitlenen iletiye ilişkin bir zaman aşımı vardır ve tooprocess selamlama iletisine önce hello uygulama başarısız olursa (örneğin, hello uygulama çökerse) Service Bus selamlama iletisine kilidini hello kilit zaman aşımı dolmadan otomatik olarak yeniden alınan kullanılabilir toobe olun.

Merhaba ileti işlenirken sonra ancak hello önce uygulama hello olay Hello çöküyor `deleteMessage` isteği bildirilmeden sonra başlatıldığında hello ileti yeniden teslim toohello uygulama olacaktır. Bu genellikle adlandırılır *en az bir kez* işleme; diğer bir deyişle, her ileti en az bir kez işlenir ancak belirli durumlarda hello aynı ileti yeniden teslim. Merhaba senaryo yinelenen işlemeyi kabul etmiyorsa, uygulama geliştiricilerinin ek mantık tooapplications toohandle yinelenen ileti teslimi eklemeniz gerekir. Bu genellikle hello kullanılarak elde edilen `getMessageId` teslimat denemelerinde hello iletisinin yöntemi.

## <a name="delete-topics-and-subscriptions"></a>Konu başlıklarını ve abonelikleri silme
bir konu veya abonelik, kullanım hello toodelete `ServiceBusRestProxy->deleteTopic` veya hello `ServiceBusRestProxy->deleteSubscripton` yöntemleri, sırasıyla. Konu başlığı silindiğinde, hello konu başlığıyla kaydedilen tüm abonelikler de silinir olduğunu unutmayın.

Merhaba aşağıdaki örnekte nasıl toodelete bir konu adlı gösterir `mytopic` ve kayıtlı abonelikler.

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

Hello kullanarak `deleteSubscription` yöntemi, bir abonelik bağımsız olarak silebilirsiniz:

```php
$serviceBusRestProxy->deleteSubscription("mytopic", "mysubscription");
```

## <a name="next-steps"></a>Sonraki adımlar
Artık Service Bus kuyruklarını hello temellerini öğrendiğinize göre bkz: [kuyruklar, konu başlıkları ve abonelikler] [ Queues, topics, and subscriptions] daha fazla bilgi için.

[BrokeredMessage]: https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.brokeredmessage
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[sqlfilter]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter
[require-once]: http://php.net/require_once
[Service Bus quotas]: service-bus-quotas.md
