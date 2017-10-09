---
title: aaaHow toouse php'den kuyruk depolama | Microsoft Docs
description: "Nasıl toouse hello Azure kuyruk depolama hizmeti toocreate ve delete kuyruklar ve Ekle, Al ve iletileri silmek öğrenin. Örnekleri PHP ile yazılmıştır."
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
ms.openlocfilehash: 5034faf3b5f28f72d5b56ac1ce7a5723be697ce6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-queue-storage-from-php"></a>Nasıl toouse php'den kuyruk depolama
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a>Genel Bakış
Bu kılavuz size nasıl tooperform yaygın senaryolar kullanarak Azure kuyruk depolama hizmeti hello gösterir. Merhaba örnekleri sınıfları PHP için Windows SDK hello yazılır. Hello kapsanan senaryolar ekleme gözatma, alma ve iletileri kuyruğa silme yanı sıra oluşturma ve silme yer alır.

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-php-application"></a>PHP uygulaması oluşturma
Azure kuyruk depolamaya erişen bir PHP uygulaması oluşturmak için gereksinim hello yalnızca hello hello Azure SDK sınıfları, PHP'nin için kodunuzu içinde başvuruyor. Uygulamanızın, Not Defteri dahil olmak üzere tüm geliştirme araçları toocreate kullanabilirsiniz.

Bu kılavuzda, bir PHP uygulamanızda yerel olarak veya bir Azure web rolü, çalışan rolü veya Web sitesi içinde çalışan kodu çağrılabilir kuyruk depolama özelliklerini kullanır.

## <a name="get-hello-azure-client-libraries"></a>Hello Azure istemci kitaplıkları Al
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-tooaccess-queue-storage"></a>Uygulama tooaccess kuyruk depolama yapılandırma
toouse hello API'leri Azure kuyruk depolama için gerekir:

1. Hello kullanarak referans hello otomatik Yükleyiciden dosyasına [require_once] deyimi.
2. Kullanabileceğinize sınıfları başvuru.

Merhaba aşağıdaki örnekte nasıl tooinclude hello otomatik Yükleyiciden dosya ve başvuru hello gösterir **ServicesBuilder** sınıfı.

> [!NOTE]
> Bu örnek (ve diğer örnekleri bu makalede) hello PHP istemci kitaplıkları oluşturucu aracılığıyla Azure yüklediğinizi varsayar. Merhaba kitaplıklarını el ile yüklediyseniz, tooreference hello gerekir `WindowsAzure.php` otomatik yükleyici dosyası.
> 
> 

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;

```

Merhaba aşağıdaki örnekte, hello `require_once` deyimi her zaman gösterilecek ancak hello örnek tooexecute için gerekli olan hello sınıfları başvurulur.

## <a name="set-up-an-azure-storage-connection"></a>Bir Azure depolama bağlantı kurma
bir Azure kuyruk depolama istemcisi tooinstantiate, öncelikle geçerli bir bağlantı dizesi olması gerekir. Merhaba kuyruk hizmeti bağlantı dizesini Hello biçimi aşağıdaki gibidir.

Canlı hizmetine erişmek için:

```php
DefaultEndpointsProtocol=[http|https];AccountName=[yourAccount];AccountKey=[yourKey]
```

Merhaba öykünücüsü depolama erişmek için:

```php
UseDevelopmentStorage=true
```

toocreate herhangi bir Azure hizmeti istemci toouse hello gereksinim **ServicesBuilder** sınıfı. Teknikleri izleyerek hello birini kullanabilirsiniz:

* Merhaba bağlantı geçirmek doğrudan tooit dize.
* Kullanım **CloudConfigurationManager (CCM)** toocheck birden çok dış kaynaklardan hello bağlantı dizesi:
  * Bir dış kaynağa desteği ile birlikte varsayılan olarak, — ortam değişkenleri.
  * Merhaba genişleterek yeni kaynakları ekleyebilirsiniz **ConnectionStringSource** sınıfı.

Burada özetlenen hello örnekler için başlangıç bağlantı dizesi doğrudan geçirilir.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);
```

## <a name="create-a-queue"></a>Bir kuyruk oluşturma
A **QueueRestProxy** nesne hello kullanarak bir kuyruk oluşturma olanak tanır **createQueue** yöntemi. Bir kuyruk oluştururken hello sıra seçeneklerini ayarlayabilirsiniz, ancak bunun nedenle gerekli değildir. (gösterir aşağıdaki örnekte nasıl hello bir kuyruk tooset meta.)

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
> Meta veri anahtarları için büyük/küçük harfe duyarlılık dayanarak doğrulamamalısınız. Tüm anahtarları küçük hello hizmetinden salt okunurdur.
> 
> 

## <a name="add-a-message-tooa-queue"></a>Bir ileti tooa sırası Ekle
tooadd bir ileti tooa sırası kullanmak **QueueRestProxy -> CreateMessage nesne**. Merhaba yöntemi hello kuyruk adı, hello ileti metni ve (olan isteğe bağlı) ileti seçeneklerini alır.

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

## <a name="peek-at-hello-next-message"></a>Merhaba sonraki iletiye gözatın
Size bir ileti (ya da iletileri) bir sıranın Merhaba öne hello sıradan çağırarak kaldırmadan iletiye göz atabilirsiniz **QueueRestProxy -> peekMessages**. Varsayılan olarak, hello **peekMessage** yöntemi tek bir ileti döndürür, fakat hello kullanarak bu değeri değiştirebilirsiniz **PeekMessagesOptions -> setNumberOfMessages** yöntemi.

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

## <a name="de-queue-hello-next-message"></a>Merhaba sonraki iletiyi sıradan çıkarmak
Kodunuzun bir iletiyi bir kuyruktan iki adımda kaldırır. İlk olarak, arama **QueueRestProxy -> listMessages**, hello sırasından okuma başka bir kod hello ileti görünmez tooany yapar. Varsayılan olarak, bu ileti 30 saniye görünmez kalır. (Selamlama iletisine bu dönemde silinmez, onu yeniden hello sırasına görünür olur.) toofinish kaldırma selamlama iletisine hello sırasından çağırmalıdır **QueueRestProxy -> deleteMessage**. Aynı iletiyi ve try toohardware veya yazılım hatası, başka bir örneği kodunuzu nedeniyle bir ileti alabilir, kod başarısız tooprocess yeniden hello zaman bir ileti kaldırmanın bu iki adımlı işlem, sağlar. Kod çağrılarınızı **deleteMessage** hello ileti işlendikten sonra sağ.

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

## <a name="change-hello-contents-of-a-queued-message"></a>Merhaba kuyruğa alınan iletinin içeriğini değiştirme
Bir ileti yerinde hello sırasındaki Merhaba içeriğine çağırarak değiştirebileceğiniz **QueueRestProxy -> updateMessage**. Merhaba ileti bir iş görevini temsil ediyorsa, bu özellik tooupdate hello durumu hello iş görevi kullanabilirsiniz. koddan hello hello kuyruk iletisini yeni içeriklerle güncelleştirir ve 60 saniye hello görünürlük zaman aşımı tooextend ayarlar. Bu hello hello ileti ile ilişkili iş durumunu kaydeder ve hello istemci selamlama iletisine üzerinde çalışan başka bir dakika toocontinue sağlar. Bir işleme adımı toohardware veya yazılım hatası başarısız olursa hello başından üzerinden toostart gerek kalmadan kuyruk iletilerindeki bu teknik tootrack çok adımlı iş akışlarını kullanabilirsiniz. Genellikle, bir yeniden deneme sayısı da tutacak ve hello olursa ileti denenir birden fazla  *n*  kez silmeniz. Bu, her işlendiğinde bir uygulama hatası tetikleyen bir iletiye karşı koruma sağlar.

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
Bir sıradan ileti alma özelleştirebilirsiniz iki yolu vardır. İlk olarak toplu iletiler (yukarı too32) elde edebilirsiniz. İkinci olarak, kodunuzu daha fazla izin vererek daha uzun veya kısaysa görünürlük zaman aşımını ayarlayabilirsiniz veya daha az zaman toofully her ileti işlenemedi. Merhaba aşağıdaki kod örneği kullanır hello **getMessages** bir çağrı yöntemi tooget 16 iletileri. Kullanarak her ileti işler sonra bir **için** döngü. Ayrıca, her ileti için hello görünmezlik zaman aşımı toofive dakika ayarlar.

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
Bir kuyruktaki ileti sayısı hello tahmini alabilirsiniz. Merhaba **QueueRestProxy -> getQueueMetadata** yöntemi hello sırası hakkında hello kuyruk hizmeti tooreturn meta verileri sorar. Arama hello **getApproximateMessageCount** hello yöntemi döndürülen nesnenin kaç iletiler bir kuyrukta olan sayısına sağlar. iletileri eklenen veya hello sıra hizmeti tooyour isteği yanıtlar sonra kaldırıldığı için hello yalnızca yaklaşık sayısıdır.

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
bir kuyruk ve içerisindeki tüm Merhaba iletileri toodelete çağrısı hello **QueueRestProxy -> deleteQueue** yöntemi.

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
Artık Azure kuyruk depolama hello temellerini öğrendiğinize göre bu bağlantıları toolearn daha karmaşık depolama görevleri hakkında izleyin:

* Merhaba ziyaret [Azure Storage ekibi blog'u](http://blogs.msdn.com/b/windowsazurestorage/).

Daha fazla bilgi için hello Ayrıca bkz. [PHP Geliştirici Merkezi](/develop/php/).

[download]: http://go.microsoft.com/fwlink/?LinkID=252473
[require_once]: http://www.php.net/manual/en/function.require-once.php
[Azure Portal]: https://portal.azure.com

