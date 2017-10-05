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
ms.openlocfilehash: 12ebb905184e74da534cd44e8314335145f7042d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-queue-storage-from-php"></a><span data-ttu-id="5073d-104">PHP’den Kuyruk depolama kullanma</span><span class="sxs-lookup"><span data-stu-id="5073d-104">How to use Queue storage from PHP</span></span>
[!INCLUDE [storage-selector-queue-include](../../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="5073d-105">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="5073d-105">Overview</span></span>
<span data-ttu-id="5073d-106">Bu kılavuz Azure kuyruk depolama hizmetini kullanarak yaygın senaryolar gerçekleştirmek nasıl yapacağınızı gösterir.</span><span class="sxs-lookup"><span data-stu-id="5073d-106">This guide will show you how to perform common scenarios by using the Azure Queue storage service.</span></span> <span data-ttu-id="5073d-107">Örnekler, PHP için Windows SDK sınıfları yazılır.</span><span class="sxs-lookup"><span data-stu-id="5073d-107">The samples are written via classes from the Windows SDK for PHP.</span></span> <span data-ttu-id="5073d-108">Kapsanan senaryolar ekleme, gözatma, alma ve kuyruk iletileri silme yanı sıra oluşturma ve silme içerir.</span><span class="sxs-lookup"><span data-stu-id="5073d-108">The covered scenarios include inserting, peeking, getting, and deleting queue messages, as well as creating and deleting queues.</span></span>

[!INCLUDE [storage-queue-concepts-include](../../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-php-application"></a><span data-ttu-id="5073d-109">PHP uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="5073d-109">Create a PHP application</span></span>
<span data-ttu-id="5073d-110">Azure kuyruk depolamaya erişen bir PHP uygulaması oluşturmak için yalnızca Azure SDK'sını sınıflardan, PHP'nin için kodunuzu içinde başvuran gereksinimdir.</span><span class="sxs-lookup"><span data-stu-id="5073d-110">The only requirement for creating a PHP application that accesses Azure Queue storage is the referencing of classes from the Azure SDK for PHP from within your code.</span></span> <span data-ttu-id="5073d-111">Not Defteri dahil olmak üzere uygulamanızı oluşturmak için tüm geliştirme araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5073d-111">You can use any development tools to create your application, including Notepad.</span></span>

<span data-ttu-id="5073d-112">Bu kılavuzda, bir PHP uygulamanızda yerel olarak veya bir Azure web rolü, çalışan rolü veya Web sitesi içinde çalışan kodu çağrılabilir kuyruk depolama özelliklerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="5073d-112">In this guide, you will use Queue storage features that can be called within a PHP application locally, or in code running within an Azure web role, worker role, or website.</span></span>

## <a name="get-the-azure-client-libraries"></a><span data-ttu-id="5073d-113">Azure istemci kitaplıkları Al</span><span class="sxs-lookup"><span data-stu-id="5073d-113">Get the Azure Client Libraries</span></span>
[!INCLUDE [get-client-libraries](../../../includes/get-client-libraries.md)]

## <a name="configure-your-application-to-access-queue-storage"></a><span data-ttu-id="5073d-114">Kuyruk depolama erişmek için uygulamanızı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="5073d-114">Configure your application to access Queue storage</span></span>
<span data-ttu-id="5073d-115">Azure kuyruk depolama API'leri kullanmak için aktarmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="5073d-115">To use the APIs for Azure Queue storage, you need to:</span></span>

1. <span data-ttu-id="5073d-116">Otomatik Yükleyici dosyasını kullanarak başvuru [require_once] deyimi.</span><span class="sxs-lookup"><span data-stu-id="5073d-116">Reference the autoloader file by using the [require_once] statement.</span></span>
2. <span data-ttu-id="5073d-117">Kullanabileceğinize sınıfları başvuru.</span><span class="sxs-lookup"><span data-stu-id="5073d-117">Reference any classes that you might use.</span></span>

<span data-ttu-id="5073d-118">Aşağıdaki örnek otomatik Yükleyiciden dosya ve başvuru dahil gösterilmektedir **ServicesBuilder** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="5073d-118">The following example shows how to include the autoloader file and reference the **ServicesBuilder** class.</span></span>

> [!NOTE]
> <span data-ttu-id="5073d-119">Bu örnek (ve diğer örnekleri bu makalede) oluşturucu aracılığıyla Azure için PHP istemci kitaplıkları yüklediğinizi varsayar.</span><span class="sxs-lookup"><span data-stu-id="5073d-119">This example (and other examples in this article) assumes that you have installed the PHP Client Libraries for Azure via Composer.</span></span> <span data-ttu-id="5073d-120">Kitaplıkları el ile yüklediyseniz, başvuru gerekir `WindowsAzure.php` otomatik yükleyici dosyası.</span><span class="sxs-lookup"><span data-stu-id="5073d-120">If you installed the libraries manually, you will need to reference the `WindowsAzure.php` autoloader file.</span></span>
> 
> 

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;

```

<span data-ttu-id="5073d-121">Aşağıdaki örneklerde `require_once` deyimi her zaman gösterilecek ancak örneğin yürütmek için gerekli olan sınıfları başvurulacak.</span><span class="sxs-lookup"><span data-stu-id="5073d-121">In the examples below, the `require_once` statement will be shown always, but only the classes that are necessary for the example to execute will be referenced.</span></span>

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="5073d-122">Bir Azure depolama bağlantı kurma</span><span class="sxs-lookup"><span data-stu-id="5073d-122">Set up an Azure storage connection</span></span>
<span data-ttu-id="5073d-123">Bir Azure kuyruk depolama istemcisi örneği oluşturmak için öncelikle geçerli bir bağlantı dizesi olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="5073d-123">To instantiate an Azure Queue storage client, you must first have a valid connection string.</span></span> <span data-ttu-id="5073d-124">Kuyruk hizmeti bağlantı dizesi biçimi aşağıdaki gibidir.</span><span class="sxs-lookup"><span data-stu-id="5073d-124">The format for the queue service connection string is as follows.</span></span>

<span data-ttu-id="5073d-125">Canlı hizmetine erişmek için:</span><span class="sxs-lookup"><span data-stu-id="5073d-125">For accessing a live service:</span></span>

```php
DefaultEndpointsProtocol=[http|https];AccountName=[yourAccount];AccountKey=[yourKey]
```

<span data-ttu-id="5073d-126">Öykünücü depolama erişmek için:</span><span class="sxs-lookup"><span data-stu-id="5073d-126">For accessing the emulator storage:</span></span>

```php
UseDevelopmentStorage=true
```

<span data-ttu-id="5073d-127">Herhangi bir Azure hizmeti istemcisi oluşturmak için kullanmanız gerekir **ServicesBuilder** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="5073d-127">To create any Azure service client, you need to use the **ServicesBuilder** class.</span></span> <span data-ttu-id="5073d-128">Aşağıdaki yöntemlerden birini kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="5073d-128">You can use either of the following techniques:</span></span>

* <span data-ttu-id="5073d-129">Bağlantı dizesi doğrudan geçirin.</span><span class="sxs-lookup"><span data-stu-id="5073d-129">Pass the connection string directly to it.</span></span>
* <span data-ttu-id="5073d-130">Kullanım **CloudConfigurationManager (CCM)** bağlantı dizesi için dış kaynaklardan denetlemek için:</span><span class="sxs-lookup"><span data-stu-id="5073d-130">Use **CloudConfigurationManager (CCM)** to check multiple external sources for the connection string:</span></span>
  * <span data-ttu-id="5073d-131">Bir dış kaynağa desteği ile birlikte varsayılan olarak, — ortam değişkenleri.</span><span class="sxs-lookup"><span data-stu-id="5073d-131">By default, it comes with support for one external source—environmental variables.</span></span>
  * <span data-ttu-id="5073d-132">Genişleterek yeni kaynakları ekleyebilirsiniz **ConnectionStringSource** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="5073d-132">You can add new sources by extending the **ConnectionStringSource** class.</span></span>

<span data-ttu-id="5073d-133">Burada özetlenen örnekler için bağlantı dizesi doğrudan geçirilir.</span><span class="sxs-lookup"><span data-stu-id="5073d-133">For the examples outlined here, the connection string will be passed directly.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);
```

## <a name="create-a-queue"></a><span data-ttu-id="5073d-134">Bir kuyruk oluşturma</span><span class="sxs-lookup"><span data-stu-id="5073d-134">Create a queue</span></span>
<span data-ttu-id="5073d-135">A **QueueRestProxy** nesnesi kullanarak bir kuyruk oluşturma olanak tanır **createQueue** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="5073d-135">A **QueueRestProxy** object lets you create a queue by using the **createQueue** method.</span></span> <span data-ttu-id="5073d-136">Bir kuyruk oluştururken, sıranın seçeneklerini ayarlayabilirsiniz, ancak bunun nedenle gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="5073d-136">When creating a queue, you can set options on the queue, but doing so is not required.</span></span> <span data-ttu-id="5073d-137">(Aşağıdaki örnekte nasıl bulunan bir sıra meta veri ayarlanacağını gösterir.)</span><span class="sxs-lookup"><span data-stu-id="5073d-137">(The example below shows how to set metadata on a queue.)</span></span>

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
> <span data-ttu-id="5073d-138">Meta veri anahtarları için büyük/küçük harfe duyarlılık dayanarak doğrulamamalısınız.</span><span class="sxs-lookup"><span data-stu-id="5073d-138">You should not rely on case sensitivity for metadata keys.</span></span> <span data-ttu-id="5073d-139">Tüm anahtarları küçük hizmetinden salt okunurdur.</span><span class="sxs-lookup"><span data-stu-id="5073d-139">All keys are read from the service in lowercase.</span></span>
> 
> 

## <a name="add-a-message-to-a-queue"></a><span data-ttu-id="5073d-140">Kuyruğa bir ileti Ekle</span><span class="sxs-lookup"><span data-stu-id="5073d-140">Add a message to a queue</span></span>
<span data-ttu-id="5073d-141">Kuyruğa bir ileti eklemek için kullanın **QueueRestProxy -> CreateMessage nesne**.</span><span class="sxs-lookup"><span data-stu-id="5073d-141">To add a message to a queue, use **QueueRestProxy->createMessage**.</span></span> <span data-ttu-id="5073d-142">Yöntem, kuyruk adı, ileti metni ve (olan isteğe bağlı) ileti seçeneklerini alır.</span><span class="sxs-lookup"><span data-stu-id="5073d-142">The method takes the queue name, the message text, and message options (which are optional).</span></span>

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

## <a name="peek-at-the-next-message"></a><span data-ttu-id="5073d-143">Sonraki iletiye gözatın</span><span class="sxs-lookup"><span data-stu-id="5073d-143">Peek at the next message</span></span>
<span data-ttu-id="5073d-144">Size bir ileti (ya da iletileri) bir sıranın öne sıradan çağırarak kaldırmadan iletiye göz atabilirsiniz **QueueRestProxy -> peekMessages**.</span><span class="sxs-lookup"><span data-stu-id="5073d-144">You can peek at a message (or messages) at the front of a queue without removing it from the queue by calling **QueueRestProxy->peekMessages**.</span></span> <span data-ttu-id="5073d-145">Varsayılan olarak, **peekMessage** yöntemi tek bir ileti döndürür, fakat kullanarak bu değeri değiştirebilirsiniz **PeekMessagesOptions -> setNumberOfMessages** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="5073d-145">By default, the **peekMessage** method returns a single message, but you can change that value by using the **PeekMessagesOptions->setNumberOfMessages** method.</span></span>

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

## <a name="de-queue-the-next-message"></a><span data-ttu-id="5073d-146">Sonraki iletiyi sıradan çıkarmak</span><span class="sxs-lookup"><span data-stu-id="5073d-146">De-queue the next message</span></span>
<span data-ttu-id="5073d-147">Kodunuzun bir iletiyi bir kuyruktan iki adımda kaldırır.</span><span class="sxs-lookup"><span data-stu-id="5073d-147">Your code removes a message from a queue in two steps.</span></span> <span data-ttu-id="5073d-148">İlk olarak, arama **QueueRestProxy -> listMessages**, hangi yapar iletiyi sıradan okuyan herhangi bir kod görünmez.</span><span class="sxs-lookup"><span data-stu-id="5073d-148">First, you call **QueueRestProxy->listMessages**, which makes the message invisible to any other code that's reading from the queue.</span></span> <span data-ttu-id="5073d-149">Varsayılan olarak, bu ileti 30 saniye görünmez kalır.</span><span class="sxs-lookup"><span data-stu-id="5073d-149">By default, this message will stay invisible for 30 seconds.</span></span> <span data-ttu-id="5073d-150">(İleti bu dönemde silinmez, onu yeniden sıraya görünür olur.) İletiyi kuyruktan kaldırmayı tamamlamak için çağırmalısınız **QueueRestProxy -> deleteMessage**.</span><span class="sxs-lookup"><span data-stu-id="5073d-150">(If the message is not deleted in this time period, it will become visible on the queue again.) To finish removing the message from the queue, you must call **QueueRestProxy->deleteMessage**.</span></span> <span data-ttu-id="5073d-151">Bir ileti kaldırmanın bu iki adımlı işlem donanım veya yazılım hatası nedeniyle bir ileti işlemek kodunuzu başarısız olduğunda, kodunuzu başka bir örneği aynı ileti alma ve yeniden deneyin sağlar.</span><span class="sxs-lookup"><span data-stu-id="5073d-151">This two-step process of removing a message assures that when your code fails to process a message due to hardware or software failure, another instance of your code can get the same message and try again.</span></span> <span data-ttu-id="5073d-152">Kod çağrılarınızı **deleteMessage** ileti işlendikten sonra sağ.</span><span class="sxs-lookup"><span data-stu-id="5073d-152">Your code calls **deleteMessage** right after the message has been processed.</span></span>

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

## <a name="change-the-contents-of-a-queued-message"></a><span data-ttu-id="5073d-153">Kuyruğa alınan iletinin içeriğini değiştirme</span><span class="sxs-lookup"><span data-stu-id="5073d-153">Change the contents of a queued message</span></span>
<span data-ttu-id="5073d-154">Çağırarak bir ileti yerinde sırasındaki içeriğini değiştirebilirsiniz **QueueRestProxy -> updateMessage**.</span><span class="sxs-lookup"><span data-stu-id="5073d-154">You can change the contents of a message in-place in the queue by calling **QueueRestProxy->updateMessage**.</span></span> <span data-ttu-id="5073d-155">Eğer ileti bir iş görevini temsil ediyorsa, bu özelliği kullanarak iş görevinin durumunu güncelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5073d-155">If the message represents a work task, you could use this feature to update the status of the work task.</span></span> <span data-ttu-id="5073d-156">Aşağıdaki kod kuyruk iletisini yeni içeriklerle güncelleştirir ve görünürlük zaman aşımını 60 saniye daha uzatır ayarlar.</span><span class="sxs-lookup"><span data-stu-id="5073d-156">The following code updates the queue message with new contents, and it sets the visibility timeout to extend another 60 seconds.</span></span> <span data-ttu-id="5073d-157">Bu iletiyle ilişkili iş durumunu kaydeder ve istemciye ileti üzerinde çalışmaya devam etmek için bir dakika daha zaman verir.</span><span class="sxs-lookup"><span data-stu-id="5073d-157">This saves the state of work that's associated with the message, and it gives the client another minute to continue working on the message.</span></span> <span data-ttu-id="5073d-158">Bir işleme adımı donanım veya yazılım arızasından dolayı başarısız olursa baştan başlamanıza gerek kalmadan kuyruk iletilerindeki çok adımlı iş akışlarını izlemek için bu yöntemi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5073d-158">You could use this technique to track multi-step workflows on queue messages, without having to start over from the beginning if a processing step fails due to hardware or software failure.</span></span> <span data-ttu-id="5073d-159">Genellikle bir yeniden deneme sayacı tutmanı gerekir ve bir ileti *n* seferden daha fazla yeniden denenirse, silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5073d-159">Typically, you would keep a retry count as well, and if the message is retried more than *n* times, you would delete it.</span></span> <span data-ttu-id="5073d-160">Bu, her işlendiğinde bir uygulama hatası tetikleyen bir iletiye karşı koruma sağlar.</span><span class="sxs-lookup"><span data-stu-id="5073d-160">This protects against a message that triggers an application error each time it is processed.</span></span>

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

## <a name="additional-options-for-de-queuing-messages"></a><span data-ttu-id="5073d-161">Çıkarılması iletileri için ek seçenekleri</span><span class="sxs-lookup"><span data-stu-id="5073d-161">Additional options for de-queuing messages</span></span>
<span data-ttu-id="5073d-162">Bir sıradan ileti alma özelleştirebilirsiniz iki yolu vardır.</span><span class="sxs-lookup"><span data-stu-id="5073d-162">There are two ways that you can customize message retrieval from a queue.</span></span> <span data-ttu-id="5073d-163">İlk olarak toplu iletiler alabilirsiniz (en fazla 32).</span><span class="sxs-lookup"><span data-stu-id="5073d-163">First, you can get a batch of messages (up to 32).</span></span> <span data-ttu-id="5073d-164">İkinci olarak, kodunuzun her iletiyi tamamen işlemesi için zaman daha az veya daha fazla izin vererek daha uzun veya kısaysa görünürlük zaman aşımını ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5073d-164">Second, you can set a longer or shorter visibility timeout, allowing your code more or less time to fully process each message.</span></span> <span data-ttu-id="5073d-165">Aşağıdaki kod örneğinde **getMessages** tek çağrıda 16 iletileri almak için yöntemi.</span><span class="sxs-lookup"><span data-stu-id="5073d-165">The following code example uses the **getMessages** method to get 16 messages in one call.</span></span> <span data-ttu-id="5073d-166">Kullanarak her ileti işler sonra bir **için** döngü.</span><span class="sxs-lookup"><span data-stu-id="5073d-166">Then it processes each message by using a **for** loop.</span></span> <span data-ttu-id="5073d-167">Ayrıca her ileti için görünmezlik zaman aşımı beş dakika olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="5073d-167">It also sets the invisibility timeout to five minutes for each message.</span></span>

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

## <a name="get-queue-length"></a><span data-ttu-id="5073d-168">Kuyruk uzunluğu alma</span><span class="sxs-lookup"><span data-stu-id="5073d-168">Get queue length</span></span>
<span data-ttu-id="5073d-169">Bir kuyruktaki ileti sayısı ile ilgili bir tahmin alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5073d-169">You can get an estimate of the number of messages in a queue.</span></span> <span data-ttu-id="5073d-170">**QueueRestProxy -> getQueueMetadata** yöntemi kuyruk hakkındaki meta verileri döndürmek için sıra hizmeti sorar.</span><span class="sxs-lookup"><span data-stu-id="5073d-170">The **QueueRestProxy->getQueueMetadata** method asks the queue service to return metadata about the queue.</span></span> <span data-ttu-id="5073d-171">Çağırma **getApproximateMessageCount** yöntemi döndürülen nesne üzerinde kaç iletiler bir kuyrukta olan sayısına sağlar.</span><span class="sxs-lookup"><span data-stu-id="5073d-171">Calling the **getApproximateMessageCount** method on the returned object provides a count of how many messages are in a queue.</span></span> <span data-ttu-id="5073d-172">İletileri eklenen veya sıra hizmeti isteğinize yanıt sonra kaldırıldığı için yalnızca yaklaşık sayısıdır.</span><span class="sxs-lookup"><span data-stu-id="5073d-172">The count is only approximate because messages can be added or removed after the queue service responds to your request.</span></span>

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

## <a name="delete-a-queue"></a><span data-ttu-id="5073d-173">Bir kuyruk silme</span><span class="sxs-lookup"><span data-stu-id="5073d-173">Delete a queue</span></span>
<span data-ttu-id="5073d-174">Bir kuyruk ve tüm iletileri silmek için arama **QueueRestProxy -> deleteQueue** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="5073d-174">To delete a queue and all the messages in it, call the **QueueRestProxy->deleteQueue** method.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="5073d-175">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5073d-175">Next steps</span></span>
<span data-ttu-id="5073d-176">Artık Azure kuyruk depolamanın temellerini öğrendiğinize göre daha karmaşık depolama görevleri hakkında bilgi edinmek için aşağıdaki bağlantıları izleyin:</span><span class="sxs-lookup"><span data-stu-id="5073d-176">Now that you've learned the basics of Azure Queue storage, follow these links to learn about more complex storage tasks:</span></span>

* <span data-ttu-id="5073d-177">Ziyaret [Azure Storage ekibi blog'u](http://blogs.msdn.com/b/windowsazurestorage/).</span><span class="sxs-lookup"><span data-stu-id="5073d-177">Visit the [Azure Storage Team blog](http://blogs.msdn.com/b/windowsazurestorage/).</span></span>

<span data-ttu-id="5073d-178">Daha fazla bilgi için Ayrıca bkz. [PHP Geliştirici Merkezi](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="5073d-178">For more information, see also the [PHP Developer Center](/develop/php/).</span></span>

[download]: http://go.microsoft.com/fwlink/?LinkID=252473
[require_once]: http://www.php.net/manual/en/function.require-once.php
[Azure Portal]: https://portal.azure.com

