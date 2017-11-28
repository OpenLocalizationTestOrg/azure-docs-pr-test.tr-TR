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
ms.openlocfilehash: 8daabcc9b3b4de121a309f21bb3325242cff06f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-queue-storage-from-php"></a><span data-ttu-id="2e0ab-104">Nasıl toouse php'den kuyruk depolama</span><span class="sxs-lookup"><span data-stu-id="2e0ab-104">How toouse Queue storage from PHP</span></span>
[!INCLUDE [storage-selector-queue-include](../../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="2e0ab-105">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="2e0ab-105">Overview</span></span>
<span data-ttu-id="2e0ab-106">Bu kılavuz size nasıl tooperform yaygın senaryolar kullanarak Azure kuyruk depolama hizmeti hello gösterir.</span><span class="sxs-lookup"><span data-stu-id="2e0ab-106">This guide will show you how tooperform common scenarios by using hello Azure Queue storage service.</span></span> <span data-ttu-id="2e0ab-107">Merhaba örnekleri sınıfları PHP için Windows SDK hello yazılır.</span><span class="sxs-lookup"><span data-stu-id="2e0ab-107">hello samples are written via classes from hello Windows SDK for PHP.</span></span> <span data-ttu-id="2e0ab-108">Hello kapsanan senaryolar ekleme gözatma, alma ve iletileri kuyruğa silme yanı sıra oluşturma ve silme yer alır.</span><span class="sxs-lookup"><span data-stu-id="2e0ab-108">hello covered scenarios include inserting, peeking, getting, and deleting queue messages, as well as creating and deleting queues.</span></span>

[!INCLUDE [storage-queue-concepts-include](../../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-php-application"></a><span data-ttu-id="2e0ab-109">PHP uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="2e0ab-109">Create a PHP application</span></span>
<span data-ttu-id="2e0ab-110">Azure kuyruk depolamaya erişen bir PHP uygulaması oluşturmak için gereksinim hello yalnızca hello hello Azure SDK sınıfları, PHP'nin için kodunuzu içinde başvuruyor.</span><span class="sxs-lookup"><span data-stu-id="2e0ab-110">hello only requirement for creating a PHP application that accesses Azure Queue storage is hello referencing of classes from hello Azure SDK for PHP from within your code.</span></span> <span data-ttu-id="2e0ab-111">Uygulamanızın, Not Defteri dahil olmak üzere tüm geliştirme araçları toocreate kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2e0ab-111">You can use any development tools toocreate your application, including Notepad.</span></span>

<span data-ttu-id="2e0ab-112">Bu kılavuzda, bir PHP uygulamanızda yerel olarak veya bir Azure web rolü, çalışan rolü veya Web sitesi içinde çalışan kodu çağrılabilir kuyruk depolama özelliklerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="2e0ab-112">In this guide, you will use Queue storage features that can be called within a PHP application locally, or in code running within an Azure web role, worker role, or website.</span></span>

## <a name="get-hello-azure-client-libraries"></a><span data-ttu-id="2e0ab-113">Hello Azure istemci kitaplıkları Al</span><span class="sxs-lookup"><span data-stu-id="2e0ab-113">Get hello Azure Client Libraries</span></span>
[!INCLUDE [get-client-libraries](../../../includes/get-client-libraries.md)]

## <a name="configure-your-application-tooaccess-queue-storage"></a><span data-ttu-id="2e0ab-114">Uygulama tooaccess kuyruk depolama yapılandırma</span><span class="sxs-lookup"><span data-stu-id="2e0ab-114">Configure your application tooaccess Queue storage</span></span>
<span data-ttu-id="2e0ab-115">toouse hello API'leri Azure kuyruk depolama için gerekir:</span><span class="sxs-lookup"><span data-stu-id="2e0ab-115">toouse hello APIs for Azure Queue storage, you need to:</span></span>

1. <span data-ttu-id="2e0ab-116">Hello kullanarak referans hello otomatik Yükleyiciden dosyasına [require_once] deyimi.</span><span class="sxs-lookup"><span data-stu-id="2e0ab-116">Reference hello autoloader file by using hello [require_once] statement.</span></span>
2. <span data-ttu-id="2e0ab-117">Kullanabileceğinize sınıfları başvuru.</span><span class="sxs-lookup"><span data-stu-id="2e0ab-117">Reference any classes that you might use.</span></span>

<span data-ttu-id="2e0ab-118">Merhaba aşağıdaki örnekte nasıl tooinclude hello otomatik Yükleyiciden dosya ve başvuru hello gösterir **ServicesBuilder** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="2e0ab-118">hello following example shows how tooinclude hello autoloader file and reference hello **ServicesBuilder** class.</span></span>

> [!NOTE]
> <span data-ttu-id="2e0ab-119">Bu örnek (ve diğer örnekleri bu makalede) hello PHP istemci kitaplıkları oluşturucu aracılığıyla Azure yüklediğinizi varsayar.</span><span class="sxs-lookup"><span data-stu-id="2e0ab-119">This example (and other examples in this article) assumes that you have installed hello PHP Client Libraries for Azure via Composer.</span></span> <span data-ttu-id="2e0ab-120">Merhaba kitaplıklarını el ile yüklediyseniz, tooreference hello gerekir `WindowsAzure.php` otomatik yükleyici dosyası.</span><span class="sxs-lookup"><span data-stu-id="2e0ab-120">If you installed hello libraries manually, you will need tooreference hello `WindowsAzure.php` autoloader file.</span></span>
> 
> 

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;

```

<span data-ttu-id="2e0ab-121">Merhaba aşağıdaki örnekte, hello `require_once` deyimi her zaman gösterilecek ancak hello örnek tooexecute için gerekli olan hello sınıfları başvurulur.</span><span class="sxs-lookup"><span data-stu-id="2e0ab-121">In hello examples below, hello `require_once` statement will be shown always, but only hello classes that are necessary for hello example tooexecute will be referenced.</span></span>

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="2e0ab-122">Bir Azure depolama bağlantı kurma</span><span class="sxs-lookup"><span data-stu-id="2e0ab-122">Set up an Azure storage connection</span></span>
<span data-ttu-id="2e0ab-123">bir Azure kuyruk depolama istemcisi tooinstantiate, öncelikle geçerli bir bağlantı dizesi olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="2e0ab-123">tooinstantiate an Azure Queue storage client, you must first have a valid connection string.</span></span> <span data-ttu-id="2e0ab-124">Merhaba kuyruk hizmeti bağlantı dizesini Hello biçimi aşağıdaki gibidir.</span><span class="sxs-lookup"><span data-stu-id="2e0ab-124">hello format for hello queue service connection string is as follows.</span></span>

<span data-ttu-id="2e0ab-125">Canlı hizmetine erişmek için:</span><span class="sxs-lookup"><span data-stu-id="2e0ab-125">For accessing a live service:</span></span>

```php
DefaultEndpointsProtocol=[http|https];AccountName=[yourAccount];AccountKey=[yourKey]
```

<span data-ttu-id="2e0ab-126">Merhaba öykünücüsü depolama erişmek için:</span><span class="sxs-lookup"><span data-stu-id="2e0ab-126">For accessing hello emulator storage:</span></span>

```php
UseDevelopmentStorage=true
```

<span data-ttu-id="2e0ab-127">toocreate herhangi bir Azure hizmeti istemci toouse hello gereksinim **ServicesBuilder** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="2e0ab-127">toocreate any Azure service client, you need toouse hello **ServicesBuilder** class.</span></span> <span data-ttu-id="2e0ab-128">Teknikleri izleyerek hello birini kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="2e0ab-128">You can use either of hello following techniques:</span></span>

* <span data-ttu-id="2e0ab-129">Merhaba bağlantı geçirmek doğrudan tooit dize.</span><span class="sxs-lookup"><span data-stu-id="2e0ab-129">Pass hello connection string directly tooit.</span></span>
* <span data-ttu-id="2e0ab-130">Kullanım **CloudConfigurationManager (CCM)** toocheck birden çok dış kaynaklardan hello bağlantı dizesi:</span><span class="sxs-lookup"><span data-stu-id="2e0ab-130">Use **CloudConfigurationManager (CCM)** toocheck multiple external sources for hello connection string:</span></span>
  * <span data-ttu-id="2e0ab-131">Bir dış kaynağa desteği ile birlikte varsayılan olarak, — ortam değişkenleri.</span><span class="sxs-lookup"><span data-stu-id="2e0ab-131">By default, it comes with support for one external source—environmental variables.</span></span>
  * <span data-ttu-id="2e0ab-132">Merhaba genişleterek yeni kaynakları ekleyebilirsiniz **ConnectionStringSource** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="2e0ab-132">You can add new sources by extending hello **ConnectionStringSource** class.</span></span>

<span data-ttu-id="2e0ab-133">Burada özetlenen hello örnekler için başlangıç bağlantı dizesi doğrudan geçirilir.</span><span class="sxs-lookup"><span data-stu-id="2e0ab-133">For hello examples outlined here, hello connection string will be passed directly.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);
```

## <a name="create-a-queue"></a><span data-ttu-id="2e0ab-134">Bir kuyruk oluşturma</span><span class="sxs-lookup"><span data-stu-id="2e0ab-134">Create a queue</span></span>
<span data-ttu-id="2e0ab-135">A **QueueRestProxy** nesne hello kullanarak bir kuyruk oluşturma olanak tanır **createQueue** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="2e0ab-135">A **QueueRestProxy** object lets you create a queue by using hello **createQueue** method.</span></span> <span data-ttu-id="2e0ab-136">Bir kuyruk oluştururken hello sıra seçeneklerini ayarlayabilirsiniz, ancak bunun nedenle gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="2e0ab-136">When creating a queue, you can set options on hello queue, but doing so is not required.</span></span> <span data-ttu-id="2e0ab-137">(gösterir aşağıdaki örnekte nasıl hello bir kuyruk tooset meta.)</span><span class="sxs-lookup"><span data-stu-id="2e0ab-137">(hello example below shows how tooset metadata on a queue.)</span></span>

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
> <span data-ttu-id="2e0ab-138">Meta veri anahtarları için büyük/küçük harfe duyarlılık dayanarak doğrulamamalısınız.</span><span class="sxs-lookup"><span data-stu-id="2e0ab-138">You should not rely on case sensitivity for metadata keys.</span></span> <span data-ttu-id="2e0ab-139">Tüm anahtarları küçük hello hizmetinden salt okunurdur.</span><span class="sxs-lookup"><span data-stu-id="2e0ab-139">All keys are read from hello service in lowercase.</span></span>
> 
> 

## <a name="add-a-message-tooa-queue"></a><span data-ttu-id="2e0ab-140">Bir ileti tooa sırası Ekle</span><span class="sxs-lookup"><span data-stu-id="2e0ab-140">Add a message tooa queue</span></span>
<span data-ttu-id="2e0ab-141">tooadd bir ileti tooa sırası kullanmak **QueueRestProxy -> CreateMessage nesne**.</span><span class="sxs-lookup"><span data-stu-id="2e0ab-141">tooadd a message tooa queue, use **QueueRestProxy->createMessage**.</span></span> <span data-ttu-id="2e0ab-142">Merhaba yöntemi hello kuyruk adı, hello ileti metni ve (olan isteğe bağlı) ileti seçeneklerini alır.</span><span class="sxs-lookup"><span data-stu-id="2e0ab-142">hello method takes hello queue name, hello message text, and message options (which are optional).</span></span>

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

## <a name="peek-at-hello-next-message"></a><span data-ttu-id="2e0ab-143">Merhaba sonraki iletiye gözatın</span><span class="sxs-lookup"><span data-stu-id="2e0ab-143">Peek at hello next message</span></span>
<span data-ttu-id="2e0ab-144">Size bir ileti (ya da iletileri) bir sıranın Merhaba öne hello sıradan çağırarak kaldırmadan iletiye göz atabilirsiniz **QueueRestProxy -> peekMessages**.</span><span class="sxs-lookup"><span data-stu-id="2e0ab-144">You can peek at a message (or messages) at hello front of a queue without removing it from hello queue by calling **QueueRestProxy->peekMessages**.</span></span> <span data-ttu-id="2e0ab-145">Varsayılan olarak, hello **peekMessage** yöntemi tek bir ileti döndürür, fakat hello kullanarak bu değeri değiştirebilirsiniz **PeekMessagesOptions -> setNumberOfMessages** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="2e0ab-145">By default, hello **peekMessage** method returns a single message, but you can change that value by using hello **PeekMessagesOptions->setNumberOfMessages** method.</span></span>

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

## <a name="de-queue-hello-next-message"></a><span data-ttu-id="2e0ab-146">Merhaba sonraki iletiyi sıradan çıkarmak</span><span class="sxs-lookup"><span data-stu-id="2e0ab-146">De-queue hello next message</span></span>
<span data-ttu-id="2e0ab-147">Kodunuzun bir iletiyi bir kuyruktan iki adımda kaldırır.</span><span class="sxs-lookup"><span data-stu-id="2e0ab-147">Your code removes a message from a queue in two steps.</span></span> <span data-ttu-id="2e0ab-148">İlk olarak, arama **QueueRestProxy -> listMessages**, hello sırasından okuma başka bir kod hello ileti görünmez tooany yapar.</span><span class="sxs-lookup"><span data-stu-id="2e0ab-148">First, you call **QueueRestProxy->listMessages**, which makes hello message invisible tooany other code that's reading from hello queue.</span></span> <span data-ttu-id="2e0ab-149">Varsayılan olarak, bu ileti 30 saniye görünmez kalır.</span><span class="sxs-lookup"><span data-stu-id="2e0ab-149">By default, this message will stay invisible for 30 seconds.</span></span> <span data-ttu-id="2e0ab-150">(Selamlama iletisine bu dönemde silinmez, onu yeniden hello sırasına görünür olur.) toofinish kaldırma selamlama iletisine hello sırasından çağırmalıdır **QueueRestProxy -> deleteMessage**.</span><span class="sxs-lookup"><span data-stu-id="2e0ab-150">(If hello message is not deleted in this time period, it will become visible on hello queue again.) toofinish removing hello message from hello queue, you must call **QueueRestProxy->deleteMessage**.</span></span> <span data-ttu-id="2e0ab-151">Aynı iletiyi ve try toohardware veya yazılım hatası, başka bir örneği kodunuzu nedeniyle bir ileti alabilir, kod başarısız tooprocess yeniden hello zaman bir ileti kaldırmanın bu iki adımlı işlem, sağlar.</span><span class="sxs-lookup"><span data-stu-id="2e0ab-151">This two-step process of removing a message assures that when your code fails tooprocess a message due toohardware or software failure, another instance of your code can get hello same message and try again.</span></span> <span data-ttu-id="2e0ab-152">Kod çağrılarınızı **deleteMessage** hello ileti işlendikten sonra sağ.</span><span class="sxs-lookup"><span data-stu-id="2e0ab-152">Your code calls **deleteMessage** right after hello message has been processed.</span></span>

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

## <a name="change-hello-contents-of-a-queued-message"></a><span data-ttu-id="2e0ab-153">Merhaba kuyruğa alınan iletinin içeriğini değiştirme</span><span class="sxs-lookup"><span data-stu-id="2e0ab-153">Change hello contents of a queued message</span></span>
<span data-ttu-id="2e0ab-154">Bir ileti yerinde hello sırasındaki Merhaba içeriğine çağırarak değiştirebileceğiniz **QueueRestProxy -> updateMessage**.</span><span class="sxs-lookup"><span data-stu-id="2e0ab-154">You can change hello contents of a message in-place in hello queue by calling **QueueRestProxy->updateMessage**.</span></span> <span data-ttu-id="2e0ab-155">Merhaba ileti bir iş görevini temsil ediyorsa, bu özellik tooupdate hello durumu hello iş görevi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2e0ab-155">If hello message represents a work task, you could use this feature tooupdate hello status of hello work task.</span></span> <span data-ttu-id="2e0ab-156">koddan hello hello kuyruk iletisini yeni içeriklerle güncelleştirir ve 60 saniye hello görünürlük zaman aşımı tooextend ayarlar.</span><span class="sxs-lookup"><span data-stu-id="2e0ab-156">hello following code updates hello queue message with new contents, and it sets hello visibility timeout tooextend another 60 seconds.</span></span> <span data-ttu-id="2e0ab-157">Bu hello hello ileti ile ilişkili iş durumunu kaydeder ve hello istemci selamlama iletisine üzerinde çalışan başka bir dakika toocontinue sağlar.</span><span class="sxs-lookup"><span data-stu-id="2e0ab-157">This saves hello state of work that's associated with hello message, and it gives hello client another minute toocontinue working on hello message.</span></span> <span data-ttu-id="2e0ab-158">Bir işleme adımı toohardware veya yazılım hatası başarısız olursa hello başından üzerinden toostart gerek kalmadan kuyruk iletilerindeki bu teknik tootrack çok adımlı iş akışlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2e0ab-158">You could use this technique tootrack multi-step workflows on queue messages, without having toostart over from hello beginning if a processing step fails due toohardware or software failure.</span></span> <span data-ttu-id="2e0ab-159">Genellikle, bir yeniden deneme sayısı da tutacak ve hello olursa ileti denenir birden fazla  *n*  kez silmeniz.</span><span class="sxs-lookup"><span data-stu-id="2e0ab-159">Typically, you would keep a retry count as well, and if hello message is retried more than *n* times, you would delete it.</span></span> <span data-ttu-id="2e0ab-160">Bu, her işlendiğinde bir uygulama hatası tetikleyen bir iletiye karşı koruma sağlar.</span><span class="sxs-lookup"><span data-stu-id="2e0ab-160">This protects against a message that triggers an application error each time it is processed.</span></span>

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

## <a name="additional-options-for-de-queuing-messages"></a><span data-ttu-id="2e0ab-161">Çıkarılması iletileri için ek seçenekleri</span><span class="sxs-lookup"><span data-stu-id="2e0ab-161">Additional options for de-queuing messages</span></span>
<span data-ttu-id="2e0ab-162">Bir sıradan ileti alma özelleştirebilirsiniz iki yolu vardır.</span><span class="sxs-lookup"><span data-stu-id="2e0ab-162">There are two ways that you can customize message retrieval from a queue.</span></span> <span data-ttu-id="2e0ab-163">İlk olarak toplu iletiler (yukarı too32) elde edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2e0ab-163">First, you can get a batch of messages (up too32).</span></span> <span data-ttu-id="2e0ab-164">İkinci olarak, kodunuzu daha fazla izin vererek daha uzun veya kısaysa görünürlük zaman aşımını ayarlayabilirsiniz veya daha az zaman toofully her ileti işlenemedi.</span><span class="sxs-lookup"><span data-stu-id="2e0ab-164">Second, you can set a longer or shorter visibility timeout, allowing your code more or less time toofully process each message.</span></span> <span data-ttu-id="2e0ab-165">Merhaba aşağıdaki kod örneği kullanır hello **getMessages** bir çağrı yöntemi tooget 16 iletileri.</span><span class="sxs-lookup"><span data-stu-id="2e0ab-165">hello following code example uses hello **getMessages** method tooget 16 messages in one call.</span></span> <span data-ttu-id="2e0ab-166">Kullanarak her ileti işler sonra bir **için** döngü.</span><span class="sxs-lookup"><span data-stu-id="2e0ab-166">Then it processes each message by using a **for** loop.</span></span> <span data-ttu-id="2e0ab-167">Ayrıca, her ileti için hello görünmezlik zaman aşımı toofive dakika ayarlar.</span><span class="sxs-lookup"><span data-stu-id="2e0ab-167">It also sets hello invisibility timeout toofive minutes for each message.</span></span>

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

## <a name="get-queue-length"></a><span data-ttu-id="2e0ab-168">Kuyruk uzunluğu alma</span><span class="sxs-lookup"><span data-stu-id="2e0ab-168">Get queue length</span></span>
<span data-ttu-id="2e0ab-169">Bir kuyruktaki ileti sayısı hello tahmini alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2e0ab-169">You can get an estimate of hello number of messages in a queue.</span></span> <span data-ttu-id="2e0ab-170">Merhaba **QueueRestProxy -> getQueueMetadata** yöntemi hello sırası hakkında hello kuyruk hizmeti tooreturn meta verileri sorar.</span><span class="sxs-lookup"><span data-stu-id="2e0ab-170">hello **QueueRestProxy->getQueueMetadata** method asks hello queue service tooreturn metadata about hello queue.</span></span> <span data-ttu-id="2e0ab-171">Arama hello **getApproximateMessageCount** hello yöntemi döndürülen nesnenin kaç iletiler bir kuyrukta olan sayısına sağlar.</span><span class="sxs-lookup"><span data-stu-id="2e0ab-171">Calling hello **getApproximateMessageCount** method on hello returned object provides a count of how many messages are in a queue.</span></span> <span data-ttu-id="2e0ab-172">iletileri eklenen veya hello sıra hizmeti tooyour isteği yanıtlar sonra kaldırıldığı için hello yalnızca yaklaşık sayısıdır.</span><span class="sxs-lookup"><span data-stu-id="2e0ab-172">hello count is only approximate because messages can be added or removed after hello queue service responds tooyour request.</span></span>

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

## <a name="delete-a-queue"></a><span data-ttu-id="2e0ab-173">Bir kuyruk silme</span><span class="sxs-lookup"><span data-stu-id="2e0ab-173">Delete a queue</span></span>
<span data-ttu-id="2e0ab-174">bir kuyruk ve içerisindeki tüm Merhaba iletileri toodelete çağrısı hello **QueueRestProxy -> deleteQueue** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="2e0ab-174">toodelete a queue and all hello messages in it, call hello **QueueRestProxy->deleteQueue** method.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="2e0ab-175">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2e0ab-175">Next steps</span></span>
<span data-ttu-id="2e0ab-176">Artık Azure kuyruk depolama hello temellerini öğrendiğinize göre bu bağlantıları toolearn daha karmaşık depolama görevleri hakkında izleyin:</span><span class="sxs-lookup"><span data-stu-id="2e0ab-176">Now that you've learned hello basics of Azure Queue storage, follow these links toolearn about more complex storage tasks:</span></span>

* <span data-ttu-id="2e0ab-177">Merhaba ziyaret [Azure Storage ekibi blog'u](http://blogs.msdn.com/b/windowsazurestorage/).</span><span class="sxs-lookup"><span data-stu-id="2e0ab-177">Visit hello [Azure Storage Team blog](http://blogs.msdn.com/b/windowsazurestorage/).</span></span>

<span data-ttu-id="2e0ab-178">Daha fazla bilgi için hello Ayrıca bkz. [PHP Geliştirici Merkezi](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="2e0ab-178">For more information, see also hello [PHP Developer Center](/develop/php/).</span></span>

[download]: http://go.microsoft.com/fwlink/?LinkID=252473
[require_once]: http://www.php.net/manual/en/function.require-once.php
[Azure Portal]: https://portal.azure.com

