---
title: Php'den kuyruk depolama kullanma | Microsoft Docs
description: "Oluşturmak ve Kuyruklar silmek için Azure kuyruk depolama hizmeti kullanmayı öğrenin ve Ekle, Al ve iletilerini silin. Örnekleri PHP ile yazılmıştır."
documentationcenter: php
services: storage
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 7582b208-4851-4489-a74a-bb952569f55b
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: 3c8f799a917cfc9d74412d90f27f2ea8c21265d4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-queue-storage-from-php"></a>PHP’den Kuyruk depolama kullanma
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a>Genel Bakış
Bu kılavuz Azure kuyruk depolama hizmetini kullanarak yaygın senaryolar gerçekleştirmek nasıl yapacağınızı gösterir. Örnekler, PHP için Windows SDK sınıfları yazılır. Kapsanan senaryolar ekleme, gözatma, alma ve kuyruk iletileri silme yanı sıra oluşturma ve silme içerir.

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-php-application"></a>PHP uygulaması oluşturma
Azure kuyruk depolamaya erişen bir PHP uygulaması oluşturmak için yalnızca Azure SDK'sını sınıflardan, PHP'nin için kodunuzu içinde başvuran gereksinimdir. Not Defteri dahil olmak üzere uygulamanızı oluşturmak için tüm geliştirme araçlarını kullanabilirsiniz.

Bu kılavuzda, bir PHP uygulamanızda yerel olarak veya bir Azure web rolü, çalışan rolü veya Web sitesi içinde çalışan kodu çağrılabilir kuyruk depolama özelliklerini kullanır.

## <a name="get-the-azure-client-libraries"></a>Azure istemci kitaplıkları Al
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-to-access-queue-storage"></a>Kuyruk depolama erişmek için uygulamanızı yapılandırın
Azure kuyruk depolama API'leri kullanmak için aktarmanız gerekir:

1. Otomatik Yükleyici dosyasını kullanarak başvuru [require_once] deyimi.
2. Kullanabileceğinize sınıfları başvuru.

Aşağıdaki örnek otomatik Yükleyiciden dosya ve başvuru dahil gösterilmektedir **ServicesBuilder** sınıfı.

> [!NOTE]
> Bu örnek (ve diğer örnekleri bu makalede) oluşturucu aracılığıyla Azure için PHP istemci kitaplıkları yüklediğinizi varsayar. Kitaplıkları el ile yüklediyseniz, başvuru gerekir `WindowsAzure.php` otomatik yükleyici dosyası.
> 
> 

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;

```

Aşağıdaki örneklerde `require_once` deyimi her zaman gösterilecek ancak örneğin yürütmek için gerekli olan sınıfları başvurulacak.

## <a name="set-up-an-azure-storage-connection"></a>Bir Azure depolama bağlantı kurma
Bir Azure kuyruk depolama istemcisi örneği oluşturmak için öncelikle geçerli bir bağlantı dizesi olması gerekir. Kuyruk hizmeti bağlantı dizesi biçimi aşağıdaki gibidir.

Canlı hizmetine erişmek için:

```php
DefaultEndpointsProtocol=[http|https];AccountName=[yourAccount];AccountKey=[yourKey]
```

Öykünücü depolama erişmek için:

```php
UseDevelopmentStorage=true
```

Herhangi bir Azure hizmeti istemcisi oluşturmak için kullanmanız gerekir **ServicesBuilder** sınıfı. Aşağıdaki yöntemlerden birini kullanabilirsiniz:

* Bağlantı dizesi doğrudan geçirin.
* Kullanım **CloudConfigurationManager (CCM)** bağlantı dizesi için dış kaynaklardan denetlemek için:
  * Bir dış kaynağa desteği ile birlikte varsayılan olarak, — ortam değişkenleri.
  * Genişleterek yeni kaynakları ekleyebilirsiniz **ConnectionStringSource** sınıfı.

Burada özetlenen örnekler için bağlantı dizesi doğrudan geçirilir.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);
```

## <a name="create-a-queue"></a>Bir kuyruk oluşturma
A **QueueRestProxy** nesnesi kullanarak bir kuyruk oluşturma olanak tanır **createQueue** yöntemi. Bir kuyruk oluştururken, sıranın seçeneklerini ayarlayabilirsiniz, ancak bunun nedenle gerekli değildir. (Aşağıdaki örnekte nasıl bulunan bir sıra meta veri ayarlanacağını gösterir.)

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Queue\Models\CreateQueueOptions;

// Create queue REST proxy.
$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);

// OPTIONAL: Set queue metadata.
$createQueueOptions = new CreateQueueOptions();
$createQueueOptions->addMetaData("key1", "value1");
$createQueueOptions->addMetaData("key2", "value2");

try    {
    // Create queue.
    $queueRestProxy->createQueue("myqueue", $createQueueOptions);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179446.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

> [!NOTE]
> Meta veri anahtarları için büyük/küçük harfe duyarlılık dayanarak doğrulamamalısınız. Tüm anahtarları küçük hizmetinden salt okunurdur.
> 
> 

## <a name="add-a-message-to-a-queue"></a>Kuyruğa bir ileti Ekle
Kuyruğa bir ileti eklemek için kullanın **QueueRestProxy -> CreateMessage nesne**. Yöntem, kuyruk adı, ileti metni ve (olan isteğe bağlı) ileti seçeneklerini alır.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Queue\Models\CreateMessageOptions;

// Create queue REST proxy.
$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);

try    {
    // Create message.
    $builder = new ServicesBuilder();
    $queueRestProxy->createMessage("myqueue", "Hello World!");
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179446.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="peek-at-the-next-message"></a>Sonraki iletiye gözatın
Size bir ileti (ya da iletileri) bir sıranın öne sıradan çağırarak kaldırmadan iletiye göz atabilirsiniz **QueueRestProxy -> peekMessages**. Varsayılan olarak, **peekMessage** yöntemi tek bir ileti döndürür, fakat kullanarak bu değeri değiştirebilirsiniz **PeekMessagesOptions -> setNumberOfMessages** yöntemi.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Queue\Models\PeekMessagesOptions;

// Create queue REST proxy.
$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);

// OPTIONAL: Set peek message options.
$message_options = new PeekMessagesOptions();
$message_options->setNumberOfMessages(1); // Default value is 1.

try    {
    $peekMessagesResult = $queueRestProxy->peekMessages("myqueue", $message_options);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179446.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}

$messages = $peekMessagesResult->getQueueMessages();

// View messages.
$messageCount = count($messages);
if($messageCount <= 0){
    echo "There are no messages.<br />";
}
else{
    foreach($messages as $message)    {
        echo "Peeked message:<br />";
        echo "Message Id: ".$message->getMessageId()."<br />";
        echo "Date: ".date_format($message->getInsertionDate(), 'Y-m-d')."<br />";
        echo "Message text: ".$message->getMessageText()."<br /><br />";
    }
}
```

## <a name="de-queue-the-next-message"></a>Sonraki iletiyi sıradan çıkarmak
Kodunuzun bir iletiyi bir kuyruktan iki adımda kaldırır. İlk olarak, arama **QueueRestProxy -> listMessages**, hangi yapar iletiyi sıradan okuyan herhangi bir kod görünmez. Varsayılan olarak, bu ileti 30 saniye görünmez kalır. (İleti bu dönemde silinmez, onu yeniden sıraya görünür olur.) İletiyi kuyruktan kaldırmayı tamamlamak için çağırmalısınız **QueueRestProxy -> deleteMessage**. Bir ileti kaldırmanın bu iki adımlı işlem donanım veya yazılım hatası nedeniyle bir ileti işlemek kodunuzu başarısız olduğunda, kodunuzu başka bir örneği aynı ileti alma ve yeniden deneyin sağlar. Kod çağrılarınızı **deleteMessage** ileti işlendikten sonra sağ.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create queue REST proxy.
$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);

// Get message.
$listMessagesResult = $queueRestProxy->listMessages("myqueue");
$messages = $listMessagesResult->getQueueMessages();
$message = $messages[0];

/* ---------------------
    Process message.
   --------------------- */

// Get message ID and pop receipt.
$messageId = $message->getMessageId();
$popReceipt = $message->getPopReceipt();

try    {
    // Delete message.
    $queueRestProxy->deleteMessage("myqueue", $messageId, $popReceipt);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179446.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="change-the-contents-of-a-queued-message"></a>Kuyruğa alınan iletinin içeriğini değiştirme
Çağırarak bir ileti yerinde sırasındaki içeriğini değiştirebilirsiniz **QueueRestProxy -> updateMessage**. Eğer ileti bir iş görevini temsil ediyorsa, bu özelliği kullanarak iş görevinin durumunu güncelleştirebilirsiniz. Aşağıdaki kod kuyruk iletisini yeni içeriklerle güncelleştirir ve görünürlük zaman aşımını 60 saniye daha uzatır ayarlar. Bu iletiyle ilişkili iş durumunu kaydeder ve istemciye ileti üzerinde çalışmaya devam etmek için bir dakika daha zaman verir. Bir işleme adımı donanım veya yazılım arızasından dolayı başarısız olursa baştan başlamanıza gerek kalmadan kuyruk iletilerindeki çok adımlı iş akışlarını izlemek için bu yöntemi kullanabilirsiniz. Genellikle bir yeniden deneme sayacı tutmanı gerekir ve bir ileti *n* seferden daha fazla yeniden denenirse, silebilirsiniz. Bu, her işlendiğinde bir uygulama hatası tetikleyen bir iletiye karşı koruma sağlar.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create queue REST proxy.
$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);

// Get message.
$listMessagesResult = $queueRestProxy->listMessages("myqueue");
$messages = $listMessagesResult->getQueueMessages();
$message = $messages[0];

// Define new message properties.
$new_message_text = "New message text.";
$new_visibility_timeout = 5; // Measured in seconds.

// Get message ID and pop receipt.
$messageId = $message->getMessageId();
$popReceipt = $message->getPopReceipt();

try    {
    // Update message.
    $queueRestProxy->updateMessage("myqueue",
                                $messageId,
                                $popReceipt,
                                $new_message_text,
                                $new_visibility_timeout);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179446.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="additional-options-for-de-queuing-messages"></a>Çıkarılması iletileri için ek seçenekleri
Bir sıradan ileti alma özelleştirebilirsiniz iki yolu vardır. İlk olarak toplu iletiler alabilirsiniz (en fazla 32). İkinci olarak, kodunuzun her iletiyi tamamen işlemesi için zaman daha az veya daha fazla izin vererek daha uzun veya kısaysa görünürlük zaman aşımını ayarlayabilirsiniz. Aşağıdaki kod örneğinde **getMessages** tek çağrıda 16 iletileri almak için yöntemi. Kullanarak her ileti işler sonra bir **için** döngü. Ayrıca her ileti için görünmezlik zaman aşımı beş dakika olarak ayarlanır.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Queue\Models\ListMessagesOptions;

// Create queue REST proxy.
$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);

// Set list message options.
$message_options = new ListMessagesOptions();
$message_options->setVisibilityTimeoutInSeconds(300);
$message_options->setNumberOfMessages(16);

// Get messages.
try{
    $listMessagesResult = $queueRestProxy->listMessages("myqueue",
                                                     $message_options);
    $messages = $listMessagesResult->getQueueMessages();

    foreach($messages as $message){

        /* ---------------------
            Process message.
        --------------------- */

        // Get message Id and pop receipt.
        $messageId = $message->getMessageId();
        $popReceipt = $message->getPopReceipt();

        // Delete message.
        $queueRestProxy->deleteMessage("myqueue", $messageId, $popReceipt);
    }
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179446.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="get-queue-length"></a>Kuyruk uzunluğu alma
Bir kuyruktaki ileti sayısı ile ilgili bir tahmin alabilirsiniz. **QueueRestProxy -> getQueueMetadata** yöntemi kuyruk hakkındaki meta verileri döndürmek için sıra hizmeti sorar. Çağırma **getApproximateMessageCount** yöntemi döndürülen nesne üzerinde kaç iletiler bir kuyrukta olan sayısına sağlar. İletileri eklenen veya sıra hizmeti isteğinize yanıt sonra kaldırıldığı için yalnızca yaklaşık sayısıdır.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create queue REST proxy.
$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);

try    {
    // Get queue metadata.
    $queue_metadata = $queueRestProxy->getQueueMetadata("myqueue");
    $approx_msg_count = $queue_metadata->getApproximateMessageCount();
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179446.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}

echo $approx_msg_count;
```

## <a name="delete-a-queue"></a>Bir kuyruk silme
Bir kuyruk ve tüm iletileri silmek için arama **QueueRestProxy -> deleteQueue** yöntemi.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create queue REST proxy.
$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);

try    {
    // Delete queue.
    $queueRestProxy->deleteQueue("myqueue");
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179446.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="next-steps"></a>Sonraki adımlar
Artık Azure kuyruk depolamanın temellerini öğrendiğinize göre daha karmaşık depolama görevleri hakkında bilgi edinmek için aşağıdaki bağlantıları izleyin:

* Ziyaret [Azure Storage ekibi blog'u](http://blogs.msdn.com/b/windowsazurestorage/).

Daha fazla bilgi için Ayrıca bkz. [PHP Geliştirici Merkezi](/develop/php/).

[download]: http://go.microsoft.com/fwlink/?LinkID=252473
[require_once]: http://www.php.net/manual/en/function.require-once.php
[Azure Portal]: https://portal.azure.com

