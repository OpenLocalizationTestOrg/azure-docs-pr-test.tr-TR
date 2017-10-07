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
# <a name="how-toouse-service-bus-queues-with-php"></a>PHP ile nasıl toouse Service Bus kuyrukları
[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

Bu kılavuz size nasıl gösterir toouse Service Bus kuyruklarını. Merhaba örnekler PHP ile yazılmıştır ve hello kullan [PHP için Azure SDK](../php-download-sdk.md). Merhaba kapsanan senaryolar dahil **sıra oluşturma**, **ileti gönderme ve alma**, ve **sıraları silme**.

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

## <a name="create-a-php-application"></a>PHP uygulaması oluşturma
Merhaba hello Azure Blob hizmete erişen bir PHP uygulaması oluşturmaya yönelik gereksinim, yalnızca hello hello sınıfların başvuran [PHP için Azure SDK](../php-download-sdk.md) gelen kodunuzu içinde. Uygulama veya Notepad tüm geliştirme araçları toocreate kullanabilirsiniz.

> [!NOTE]
> PHP yüklemenizi de hello olmalıdır [OpenSSL uzantısı](http://php.net/openssl) yüklenir ve etkinleştirilir.
> 
> 

Bu kılavuzda, bir PHP uygulamanızda yerel olarak veya bir Azure web rolü, çalışan rolü veya Web sitesi içinde çalışan kodu çağrılabilir hizmet özelliklerini kullanır.

## <a name="get-hello-azure-client-libraries"></a>Hello Azure istemci kitaplıkları Al
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-toouse-service-bus"></a>Uygulama toouse Service Bus yapılandırın
toouse hello Service Bus kuyruğuna API'leri, hello aşağıdaki:

1. Hello kullanarak başvuru hello otomatik yükleyici dosyasını [require_once] [ require_once] deyimi.
2. Kullanabileceğinize sınıfları başvuru.

Merhaba aşağıdaki örnekte nasıl tooinclude hello otomatik Yükleyiciden dosya ve başvuru hello gösterir `ServicesBuilder` sınıfı.

> [!NOTE]
> Bu örnek (ve diğer örnekleri bu makalede) hello PHP istemci kitaplıkları oluşturucu aracılığıyla Azure yüklü olduğunu varsayar. El ile veya bir ARMUTLU paketi olarak hello kitaplıkları yüklediyseniz, hello başvurmalıdır **WindowsAzure.php** otomatik yükleyici dosyası.
> 
> 

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

Merhaba aşağıdaki örnekte, hello `require_once` deyimi her zaman gösterilecek, ancak yalnızca hello sınıfları hello örnek tooexecute için gereken başvuru.

## <a name="set-up-a-service-bus-connection"></a>Hizmet veri yolu bağlantı kurma
Service Bus istemci tooinstantiate, şu biçimde geçerli bir bağlantı dizesi ilk olması gerekir:

```
Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]
```

Burada `Endpoint` genellikle hello biçimidir `[yourNamespace].servicebus.windows.net`.

toocreate hello kullanmalıdır herhangi bir Azure hizmeti istemci `ServicesBuilder` sınıfı. Şunları yapabilirsiniz:

* Merhaba bağlantı geçirmek doğrudan tooit dize.
* Kullanım hello **CloudConfigurationManager (CCM)** toocheck birden çok dış kaynaklardan hello bağlantı dizesi:
  * Bir dış kaynak - ortam değişkenleri için destek ile birlikte varsayılan olarak
  * Merhaba genişleterek yeni kaynakları ekleyebilirsiniz `ConnectionStringSource` sınıfı

Burada özetlenen hello örnekler için başlangıç bağlantı dizesi doğrudan geçirilir.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$connectionString = "Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]";

$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);
```

## <a name="create-a-queue"></a>Bir kuyruk oluşturma
Service Bus kuyruklarını hello aracılığıyla yönelik yönetim işlemlerini gerçekleştirebilirsiniz `ServiceBusRestProxy` sınıfı. A `ServiceBusRestProxy` nesne hello oluşturulan `ServicesBuilder::createServiceBusService` Üreteç yöntemi hello belirteci izinleri toomanage yalıtan bir uygun bir bağlantı dizesi ile.

örnekte gösterildiği nasıl aşağıdaki hello tooinstantiate bir `ServiceBusRestProxy` ve arama `ServiceBusRestProxy->createQueue` toocreate adlandırılan bir kuyruğun `myqueue` içinde bir `MySBNamespace` hizmet ad alanı:

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
> Merhaba kullanabilirsiniz `listQueues` yöntemi `ServiceBusRestProxy` belirtilen ada sahip bir sıra içinde bir ad alanı zaten varsa toocheck nesneleri.
> 
> 

## <a name="send-messages-tooa-queue"></a>İletileri tooa sırası Gönder
ileti tooa Service Bus kuyruğuna toosend, uygulamanızın çağırır hello `ServiceBusRestProxy->sendQueueMessage` yöntemi. kodun gösterdiği nasıl aşağıdaki hello toosend ileti toohello `myqueue` içinde daha önce oluşturduğunuz sıra `MySBNamespace` hizmet ad alanı.

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

Service Bus kuyrukları çok gönderilen (ve öğesinden alınan) hello örneklerini iletileri [BrokeredMessage] [ BrokeredMessage] sınıfı. [BrokeredMessage] [ BrokeredMessage] nesnelerinin bir dizi standart yöntemleri ve kullanılan toohold özel uygulamaya özgü özellikler ve rastgele uygulama verileri gövdesi özellikleri vardır.

Service Bus kuyruklarını destek maksimum ileti boyutu 256 KB hello [standart katmanı](service-bus-premium-messaging.md) hello 1 MB [Premium katmanı](service-bus-premium-messaging.md). Merhaba standart ve özel uygulama özelliklerini içeren hello üstbilgi en büyük boyutu 64 KB olabilir. Merhaba bir kuyrukta tutulan ileti sayısına bir sınır yoktur ancak kuyruk tarafından tutulan hello iletilerin toplam boyutu hello bir sınır yoktur. Bu sıra boyutu üst sınır 5 GB'tır.

## <a name="receive-messages-from-a-queue"></a>Kuyruktan ileti alma

Merhaba en iyi şekilde tooreceive iletilerin bir kuyruktan toouse olan bir `ServiceBusRestProxy->receiveQueueMessage` yöntemi. İletileri iki farklı modda alınan: [ *ReceiveAndDelete* ](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) ve [ *PeekLock*](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock). **PeekLock** hello varsayılandır.

Kullanırken [ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) modu, alma bir tek işlemi; diğer bir deyişle, hizmet veri yolu bir kuyrukta İletiye yönelik Okuma isteği aldığında, hello iletiyi kullanılıyor olarak işaretler ve toohello uygulama döndürür. [ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) modu hello en basit modeldir ve senaryoları bir uygulama içinde tolerans bir hatanın hello Olay iletisinde işlenmiyor en iyi şekilde çalışır. toounderstand Bu, hangi hello tüketici sorunları hello alma isteği bir senaryo düşünün ve işlemeden önce çöküyor. Hizmet veri yolu selamlama iletisine hello uygulama yeniden başlatılıp iletileri tekrar kullanmaya başladığında olduğunda, ardından kullanılıyor olarak işaretlenmiş için onu olan hello iletiyi atlamış olur önceki toohello kilitlenme tüketilen.

Merhaba varsayılan [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock) bir ileti alma modu, iletilere olası toosupport uygulamaları iki aşamalı işlemi haline gelir. Service Bus bir istek aldığında, tüketilen hello sonraki ileti toobe bulur, tooprevent kilitler, almasını diğer tüketicilerin ve toohello uygulama döndürür. Merhaba uygulaması hello iletiyi işlemeyi tamamladıktan sonra (veya sonra işlemek için depoladıktan sonra), hello hello ikinci aşamasını tamamlar alınan selamlama iletisine çok geçirerek alma işleminin`ServiceBusRestProxy->deleteMessage`. Hizmet veri yolu hello gördüğünde `deleteMessage` çağrısı hello iletiyi kullanılıyor olarak işaretler ve hello sıradan kaldırın.

örnekte gösterildiği nasıl aşağıdaki hello tooreceive ve bir iletiyi kullanarak işlem [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock) (Merhaba varsayılan modu).

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

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a>Nasıl toohandle uygulaması kilitlenir ve Okunmayan iletileri

Hizmet veri yolu, gerçekleşen hataları uygulama ya da ileti işlenirken zorlukları rahat işlevselliği toohelp sağlar. Alıcı uygulamanın kaydedemediği tooprocess Merhaba ileti herhangi bir nedenden dolayı ardından hello çağırabilirsiniz `unlockMessage` hello alınan ileti üzerinde yöntemi (hello yerine `deleteMessage` yöntemi). Bu hizmet veri yolu toounlock selamlama iletisine hello sıra içinde neden ve yeniden alınan kullanılabilir toobe olun, ya da göre aynı uygulama veya başka bir kullanıcı uygulama tarafından tüketen hello.

Ayrıca hello kuyrukta kilitlenen iletiye ilişkin bir zaman aşımı vardır ve tooprocess selamlama iletisine önce hello uygulama başarısız olursa (örneğin, hello uygulama çökerse) Service Bus selamlama iletisine kilidini hello kilit zaman aşımı dolmadan otomatik olarak yeniden alınan kullanılabilir toobe olun.

Merhaba ileti işlenirken sonra ancak hello önce uygulama hello olay Hello çöküyor `deleteMessage` isteği bildirilmeden sonra başlatıldığında hello ileti yeniden teslim toohello uygulama olacaktır. Bu genellikle adlandırılır *en az bir kez* işleme; diğer bir deyişle, her ileti en az bir kez işlenir ancak belirli durumlarda hello aynı ileti yeniden teslim. Merhaba senaryo yinelenen işlemeyi sonra ek ekleme etmiyorsa mantığı tooapplications toohandle yinelenen ileti teslimi önerilir. Bu genellikle hello kullanılarak elde edilen `getMessageId` teslimat denemelerinde hello iletisinin yöntemi.

## <a name="next-steps"></a>Sonraki adımlar
Artık Service Bus kuyruklarını hello temellerini öğrendiğinize göre bkz: [kuyruklar, konu başlıkları ve abonelikler] [ Queues, topics, and subscriptions] daha fazla bilgi için.

Daha fazla bilgi için ayrıca hello ziyaret [PHP Geliştirici Merkezi](https://azure.microsoft.com/develop/php/).

[BrokeredMessage]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[require_once]: http://php.net/require_once


