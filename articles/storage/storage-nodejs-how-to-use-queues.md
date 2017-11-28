---
title: Node.js'den kuyruk depolama kullanma | Microsoft Docs
description: "Oluşturmak ve Kuyruklar silmek için Azure Queue hizmetini kullanmayı öğrenin ve Ekle, Al ve iletilerini silin. Node.js içinde yazılmış örneklerini içerir."
services: storage
documentationcenter: nodejs
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: a8a92db0-4333-43dd-a116-28b3147ea401
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: e30297bd0cc65105c92d6428035d2e6c156448af
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-queue-storage-from-nodejs"></a><span data-ttu-id="35bef-104">Node.js’den Kuyruk depolama kullanma</span><span class="sxs-lookup"><span data-stu-id="35bef-104">How to use Queue storage from Node.js</span></span>
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-check-out-samples-all](../../includes/storage-check-out-samples-all.md)]

## <a name="overview"></a><span data-ttu-id="35bef-105">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="35bef-105">Overview</span></span>
<span data-ttu-id="35bef-106">Bu kılavuz Microsoft Azure Queue hizmetini kullanarak yaygın senaryolar gerçekleştirme gösterir.</span><span class="sxs-lookup"><span data-stu-id="35bef-106">This guide shows you how to perform common scenarios using the Microsoft Azure Queue service.</span></span> <span data-ttu-id="35bef-107">Örnekler, Node.js API kullanılarak yazılır.</span><span class="sxs-lookup"><span data-stu-id="35bef-107">The samples are written using the Node.js API.</span></span> <span data-ttu-id="35bef-108">Kapsamdaki senaryolar dahil **ekleme**, **gözatma**, **alma**, ve **silme** kuyruk iletileri yanı **oluşturma ve silme**.</span><span class="sxs-lookup"><span data-stu-id="35bef-108">The scenarios covered include **inserting**, **peeking**, **getting**, and **deleting** queue messages, as well as **creating and deleting queues**.</span></span>

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-nodejs-application"></a><span data-ttu-id="35bef-109">Bir Node.js uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="35bef-109">Create a Node.js Application</span></span>
<span data-ttu-id="35bef-110">Boş bir Node.js uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="35bef-110">Create a blank Node.js application.</span></span> <span data-ttu-id="35bef-111">Bir Node.js uygulaması oluşturma yönergeleri için bkz: [Azure App Service'te bir Node.js web uygulaması oluşturma], [derleme ve Azure bulut hizmeti bir Node.js uygulamasını dağıtma] Windows PowerShell kullanarak veya [derleme ve Web Matrix Azure'u Node.js web uygulamasına dağıtma].</span><span class="sxs-lookup"><span data-stu-id="35bef-111">For instructions creating a Node.js application, see [Create a Node.js web app in Azure App Service], [Build and deploy a Node.js application to an Azure Cloud Service] using Windows PowerShell, or [Build and deploy a Node.js web app to Azure using Web Matrix].</span></span>

## <a name="configure-your-application-to-access-storage"></a><span data-ttu-id="35bef-112">Uygulamanızı erişimli depolama için yapılandırın</span><span class="sxs-lookup"><span data-stu-id="35bef-112">Configure Your Application to Access Storage</span></span>
<span data-ttu-id="35bef-113">Azure depolama kullanmak için bir dizi depolama REST Hizmetleri ile iletişim kolaylık kitaplıkları içerir Node.js için Azure depolama SDK'sı gerekir.</span><span class="sxs-lookup"><span data-stu-id="35bef-113">To use Azure storage, you need the Azure Storage SDK for Node.js, which includes a set of convenience libraries that communicate with the storage REST services.</span></span>

### <a name="use-node-package-manager-npm-to-obtain-the-package"></a><span data-ttu-id="35bef-114">Paket elde etmek için düğüm paketi Yöneticisi (NPM) kullanın</span><span class="sxs-lookup"><span data-stu-id="35bef-114">Use Node Package Manager (NPM) to obtain the package</span></span>
1. <span data-ttu-id="35bef-115">Bir komut satırı arabirimi gibi kullandığınız **PowerShell** (Windows) **Terminal** (Mac) veya **Bash** (UNIX) örnek uygulamanızı oluşturduğunuz klasöre gidin.</span><span class="sxs-lookup"><span data-stu-id="35bef-115">Use a command-line interface such as **PowerShell** (Windows,) **Terminal** (Mac,) or **Bash** (Unix), navigate to the folder where you created your sample application.</span></span>
2. <span data-ttu-id="35bef-116">Tür **npm yükleme azure depolama** komut penceresinde.</span><span class="sxs-lookup"><span data-stu-id="35bef-116">Type **npm install azure-storage** in the command window.</span></span> <span data-ttu-id="35bef-117">Komut çıktısı aşağıdaki örneğe benzer.</span><span class="sxs-lookup"><span data-stu-id="35bef-117">Output from the command is similar to the following example.</span></span>
 
    ```
    azure-storage@0.5.0 node_modules\azure-storage
    +-- extend@1.2.1
    +-- xmlbuilder@0.4.3
    +-- mime@1.2.11
    +-- node-uuid@1.4.3
    +-- validator@3.22.2
    +-- underscore@1.4.4
    +-- readable-stream@1.0.33 (string_decoder@0.10.31, isarray@0.0.1, inherits@2.0.1, core-util-is@1.0.1)
    +-- xml2js@0.2.7 (sax@0.5.2)
    +-- request@2.57.0 (caseless@0.10.0, aws-sign2@0.5.0, forever-agent@0.6.1, stringstream@0.0.4, oauth-sign@0.8.0, tunnel-agent@0.4.1, isstream@0.1.2, json-stringify-safe@5.0.1, bl@0.9.4, combined-stream@1.0.5, qs@3.1.0, mime-types@2.0.14, form-data@0.2.0, http-signature@0.11.0, tough-cookie@2.0.0, hawk@2.3.1, har-validator@1.8.0)
    ```

3. <span data-ttu-id="35bef-118">El ile çalıştırabilirsiniz **ls** doğrulamak için komutu bir **düğümü\_modülleri** klasörü oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="35bef-118">You can manually run the **ls** command to verify that a **node\_modules** folder was created.</span></span> <span data-ttu-id="35bef-119">Bu klasör içinde bulacaksınız **azure depolama** depolama birimine erişmesi gereken kitaplıkları içeren paket.</span><span class="sxs-lookup"><span data-stu-id="35bef-119">Inside that folder you will find the **azure-storage** package, which contains the libraries you need to access storage.</span></span>

### <a name="import-the-package"></a><span data-ttu-id="35bef-120">Paket alma</span><span class="sxs-lookup"><span data-stu-id="35bef-120">Import the package</span></span>
<span data-ttu-id="35bef-121">Not Defteri'nde veya başka bir metin düzenleyicisi kullanarak, en üstüne aşağıdakileri ekleyin **server.js** uygulamanın dosya depolama kullanmayı düşündüğünüz burada:</span><span class="sxs-lookup"><span data-stu-id="35bef-121">Using Notepad or another text editor, add the following to the top the **server.js** file of the application where you intend to use storage:</span></span>

```
var azure = require('azure-storage');
```

## <a name="setup-an-azure-storage-connection"></a><span data-ttu-id="35bef-122">Bir Azure depolama bağlantı Kur</span><span class="sxs-lookup"><span data-stu-id="35bef-122">Setup an Azure Storage Connection</span></span>
<span data-ttu-id="35bef-123">Azure modülü AZURE ortam değişkenleri okur\_depolama\_HESABINI ve AZURE\_depolama\_erişim\_anahtar ya da AZURE\_depolama\_bağlantı\_Azure depolama hesabınıza bağlanmak için gerekli bilgileri DİZESİ.</span><span class="sxs-lookup"><span data-stu-id="35bef-123">The azure module will read the environment variables AZURE\_STORAGE\_ACCOUNT and AZURE\_STORAGE\_ACCESS\_KEY, or AZURE\_STORAGE\_CONNECTION\_STRING for information required to connect to your Azure storage account.</span></span> <span data-ttu-id="35bef-124">Bu ortam değişkenleri ayarlanmamışsa çağrılırken hesap bilgileri belirtmelisiniz **createQueueService**.</span><span class="sxs-lookup"><span data-stu-id="35bef-124">If these environment variables are not set, you must specify the account information when calling **createQueueService**.</span></span>

<span data-ttu-id="35bef-125">Ortam değişkenlerini ayarlama örnek için [Azure Portal](https://portal.azure.com) bir Azure Web sitesi için bkz: [Azure tablo hizmeti kullanarak Node.js web uygulaması].</span><span class="sxs-lookup"><span data-stu-id="35bef-125">For an example of setting the environment variables in the [Azure Portal](https://portal.azure.com) for an Azure Website, see [Node.js web app using the Azure Table Service].</span></span>

## <a name="how-to-create-a-queue"></a><span data-ttu-id="35bef-126">Nasıl yapılır: bir sıra oluşturun</span><span class="sxs-lookup"><span data-stu-id="35bef-126">How To: Create a Queue</span></span>
<span data-ttu-id="35bef-127">Aşağıdaki kod oluşturur bir **QueueService** kuyruklarla çalışmanıza olanak tanır nesnesi.</span><span class="sxs-lookup"><span data-stu-id="35bef-127">The following code creates a **QueueService** object, which enables you to work with queues.</span></span>

```
var queueSvc = azure.createQueueService();
```

<span data-ttu-id="35bef-128">Kullanım **createQueueIfNotExists** zaten var veya zaten yoksa, belirtilen ada sahip yeni bir sıra oluşturur, belirtilen sırada döndüren yöntemi.</span><span class="sxs-lookup"><span data-stu-id="35bef-128">Use the **createQueueIfNotExists** method, which returns the specified queue if it already exists or creates a new queue with the specified name if it does not already exist.</span></span>

```
queueSvc.createQueueIfNotExists('myqueue', function(error, result, response){
  if(!error){
    // Queue created or exists
  }
});
```

<span data-ttu-id="35bef-129">Sıranın oluşturduysanız, `result.created` doğrudur.</span><span class="sxs-lookup"><span data-stu-id="35bef-129">If the queue is created, `result.created` is true.</span></span> <span data-ttu-id="35bef-130">Sıranın varsa `result.created` false olur.</span><span class="sxs-lookup"><span data-stu-id="35bef-130">If the queue exists, `result.created` is false.</span></span>

### <a name="filters"></a><span data-ttu-id="35bef-131">Filtreler</span><span class="sxs-lookup"><span data-stu-id="35bef-131">Filters</span></span>
<span data-ttu-id="35bef-132">İsteğe bağlı filtreleme işlemleri kullanarak gerçekleştirilen işlemler için uygulanabilir **QueueService**.</span><span class="sxs-lookup"><span data-stu-id="35bef-132">Optional filtering operations can be applied to operations performed using **QueueService**.</span></span> <span data-ttu-id="35bef-133">İşlemleri filtreleme içerebilir günlüğe kaydetme, otomatik olarak yeniden deneniyor, vs. İmzalı bir yöntem uygulayan nesneler filtreleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="35bef-133">Filtering operations can include logging, automatically retrying, etc. Filters are objects that implement a method with the signature:</span></span>

```
function handle (requestOptions, next)
```

<span data-ttu-id="35bef-134">İstek seçenekleri önişleme yaptıktan sonra "İleri" aşağıdaki imzalı bir geri çağırma geçirme çağrılacak yöntemi gerekir:</span><span class="sxs-lookup"><span data-stu-id="35bef-134">After doing its preprocessing on the request options, the method needs to call "next" passing a callback with the following signature:</span></span>

```
function (returnObject, finalCallback, next)
```

<span data-ttu-id="35bef-135">Bu geri çağırma ve (sunucunun istek yanıtı) returnObject işlemden sonra geri çağırma diğer filtreleri işleme devam etmek için varsa sonraki çağırma veya yalnızca finalCallback Aksi halde hizmet başlatma sonuna çağırma gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="35bef-135">In this callback, and after processing the returnObject (the response from the request to the server), the callback needs to either invoke next if it exists to continue processing other filters or simply invoke finalCallback otherwise to end up the service invocation.</span></span>

<span data-ttu-id="35bef-136">Yeniden deneme mantığını uygulaması iki filtre Node.js için Azure SDK'sı ile birlikte **ExponentialRetryPolicyFilter** ve **LinearRetryPolicyFilter**.</span><span class="sxs-lookup"><span data-stu-id="35bef-136">Two filters that implement retry logic are included with the Azure SDK for Node.js, **ExponentialRetryPolicyFilter** and **LinearRetryPolicyFilter**.</span></span> <span data-ttu-id="35bef-137">Aşağıdaki oluşturur bir **QueueService** kullanan nesneyi **ExponentialRetryPolicyFilter**:</span><span class="sxs-lookup"><span data-stu-id="35bef-137">The following creates a **QueueService** object that uses the **ExponentialRetryPolicyFilter**:</span></span>

```
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var queueSvc = azure.createQueueService().withFilter(retryOperations);
```

## <a name="how-to-insert-a-message-into-a-queue"></a><span data-ttu-id="35bef-138">Nasıl yapılır: bir sıraya bir ileti Ekle</span><span class="sxs-lookup"><span data-stu-id="35bef-138">How To: Insert a Message into a Queue</span></span>
<span data-ttu-id="35bef-139">Kuyruğa bir ileti eklemek için kullanın **CreateMessage nesne** yeni bir ileti oluşturun ve sıraya eklemek için yöntem.</span><span class="sxs-lookup"><span data-stu-id="35bef-139">To insert a message into a queue, use the **createMessage** method to create a new message and add it to the queue.</span></span>

```
queueSvc.createMessage('myqueue', "Hello world!", function(error, result, response){
  if(!error){
    // Message inserted
  }
});
```

## <a name="how-to-peek-at-the-next-message"></a><span data-ttu-id="35bef-140">Nasıl yapılır: sonraki iletiye</span><span class="sxs-lookup"><span data-stu-id="35bef-140">How To: Peek at the Next Message</span></span>
<span data-ttu-id="35bef-141">Kuyruğun önündeki iletiye sıradan çağırarak kaldırmadan iletiye göz atabilirsiniz **peekMessages** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="35bef-141">You can peek at the message in the front of a queue without removing it from the queue by calling the **peekMessages** method.</span></span> <span data-ttu-id="35bef-142">Varsayılan olarak, **peekMessages** tek bir ileti iletiye göz atar.</span><span class="sxs-lookup"><span data-stu-id="35bef-142">By default, **peekMessages** peeks at a single message.</span></span>

```
queueSvc.peekMessages('myqueue', function(error, result, response){
  if(!error){
    // Message text is in messages[0].messageText
  }
});
```

<span data-ttu-id="35bef-143">`result` İleti içerir.</span><span class="sxs-lookup"><span data-stu-id="35bef-143">The `result` contains the message.</span></span>

> [!NOTE]
> <span data-ttu-id="35bef-144">Kullanarak **peekMessages** sıraya ileti olduğunda ileti döndürdü ancak bir hata döndürmez.</span><span class="sxs-lookup"><span data-stu-id="35bef-144">Using **peekMessages** when there are no messages in the queue will not return an error, however no messages will be returned.</span></span>
> 
> 

## <a name="how-to-dequeue-the-next-message"></a><span data-ttu-id="35bef-145">Nasıl yapılır: sonraki iletiyi sıradan çıkarma</span><span class="sxs-lookup"><span data-stu-id="35bef-145">How To: Dequeue the Next Message</span></span>
<span data-ttu-id="35bef-146">İleti işlenirken iki aşamalı bir işlemdir:</span><span class="sxs-lookup"><span data-stu-id="35bef-146">Processing a message is a two-stage process:</span></span>

1. <span data-ttu-id="35bef-147">İleti dequeue.</span><span class="sxs-lookup"><span data-stu-id="35bef-147">Dequeue the message.</span></span>
2. <span data-ttu-id="35bef-148">İletiyi silin.</span><span class="sxs-lookup"><span data-stu-id="35bef-148">Delete the message.</span></span>

<span data-ttu-id="35bef-149">Bir ileti dequeue için kullanmak **getMessages**.</span><span class="sxs-lookup"><span data-stu-id="35bef-149">To dequeue a message, use **getMessages**.</span></span> <span data-ttu-id="35bef-150">Diğer bir istemcileri onları işleyebilmek için iletiler kuyrukta görünmez kılar.</span><span class="sxs-lookup"><span data-stu-id="35bef-150">This makes the messages invisible in the queue, so no other clients can process them.</span></span> <span data-ttu-id="35bef-151">Uygulamanızı bir ileti işlediğinde çağrısı **deleteMessage** kuyruktan silinemiyor.</span><span class="sxs-lookup"><span data-stu-id="35bef-151">Once your application has processed a message, call **deleteMessage** to delete it from the queue.</span></span> <span data-ttu-id="35bef-152">Aşağıdaki örnek bir ileti alır, ardından da siler:</span><span class="sxs-lookup"><span data-stu-id="35bef-152">The following example gets a message, then deletes it:</span></span>

```
queueSvc.getMessages('myqueue', function(error, result, response){
  if(!error){
    // Message text is in messages[0].messageText
    var message = result[0];
    queueSvc.deleteMessage('myqueue', message.messageId, message.popReceipt, function(error, response){
      if(!error){
        //message deleted
      }
    });
  }
});
```

> [!NOTE]
> <span data-ttu-id="35bef-153">Varsayılan olarak, bir ileti 30 saniye, daha sonra diğer istemcilere görünür yalnızca gizlenir.</span><span class="sxs-lookup"><span data-stu-id="35bef-153">By default, a message is only hidden for 30 seconds, after which it is visible to other clients.</span></span> <span data-ttu-id="35bef-154">Kullanarak farklı bir değer belirtebilirsiniz `options.visibilityTimeout` ile **getMessages**.</span><span class="sxs-lookup"><span data-stu-id="35bef-154">You can specify a different value by using `options.visibilityTimeout` with **getMessages**.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="35bef-155">Kullanarak **getMessages** sıraya ileti olduğunda ileti döndürdü ancak bir hata döndürmez.</span><span class="sxs-lookup"><span data-stu-id="35bef-155">Using **getMessages** when there are no messages in the queue will not return an error, however no messages will be returned.</span></span>
> 
> 

## <a name="how-to-change-the-contents-of-a-queued-message"></a><span data-ttu-id="35bef-156">Nasıl yapılır: kuyruğa alınan iletinin içeriğini değiştirme</span><span class="sxs-lookup"><span data-stu-id="35bef-156">How To: Change the Contents of a Queued Message</span></span>
<span data-ttu-id="35bef-157">Bir ileti sırası kullanarak yerinde içeriğini değiştirebilirsiniz **updateMessage**.</span><span class="sxs-lookup"><span data-stu-id="35bef-157">You can change the contents of a message in-place in the queue using **updateMessage**.</span></span> <span data-ttu-id="35bef-158">Aşağıdaki örnek ileti metnini güncelleştirir:</span><span class="sxs-lookup"><span data-stu-id="35bef-158">The following example updates the text of a message:</span></span>

```
queueSvc.getMessages('myqueue', function(error, result, response){
  if(!error){
    // Got the message
    var message = result[0];
    queueSvc.updateMessage('myqueue', message.messageId, message.popReceipt, 10, {messageText: 'new text'}, function(error, result, response){
      if(!error){
        // Message updated successfully
      }
    });
  }
});
```

## <a name="how-to-additional-options-for-dequeuing-messages"></a><span data-ttu-id="35bef-159">Nasıl yapılır: kuyruktan alma için ek seçenekler iletileri</span><span class="sxs-lookup"><span data-stu-id="35bef-159">How To: Additional Options for Dequeuing Messages</span></span>
<span data-ttu-id="35bef-160">Bir sıradan ileti alma özelleştirebilirsiniz iki yolu vardır:</span><span class="sxs-lookup"><span data-stu-id="35bef-160">There are two ways you can customize message retrieval from a queue:</span></span>

* <span data-ttu-id="35bef-161">`options.numOfMessages`-Almak toplu iletiler (en fazla 32.)</span><span class="sxs-lookup"><span data-stu-id="35bef-161">`options.numOfMessages` - Retrieve a batch of messages (up to 32.)</span></span>
* <span data-ttu-id="35bef-162">`options.visibilityTimeout`-Daha uzun veya kısaysa görünmezlik zaman aşımı ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="35bef-162">`options.visibilityTimeout` - Set a longer or shorter invisibility timeout.</span></span>

<span data-ttu-id="35bef-163">Aşağıdaki örnek kullanır **getMessages** tek çağrıda 15 iletileri almak için yöntemi.</span><span class="sxs-lookup"><span data-stu-id="35bef-163">The following example uses the **getMessages** method to get 15 messages in one call.</span></span> <span data-ttu-id="35bef-164">Her bir iletiyi kullanarak işler sonra bir döngü için.</span><span class="sxs-lookup"><span data-stu-id="35bef-164">Then it processes each message using a for loop.</span></span> <span data-ttu-id="35bef-165">Ayrıca bu yöntem tarafından döndürülen tüm iletiler için beş dakika için görünmezlik zaman aşımı ayarlar.</span><span class="sxs-lookup"><span data-stu-id="35bef-165">It also sets the invisibility timeout to five minutes for all messages returned by this method.</span></span>

```
queueSvc.getMessages('myqueue', {numOfMessages: 15, visibilityTimeout: 5 * 60}, function(error, result, response){
  if(!error){
    // Messages retreived
    for(var index in result){
      // text is available in result[index].messageText
      var message = result[index];
      queueSvc.deleteMessage(queueName, message.messageId, message.popReceipt, function(error, response){
        if(!error){
          // Message deleted
        }
      });
    }
  }
});
```

## <a name="how-to-get-the-queue-length"></a><span data-ttu-id="35bef-166">Nasıl yapılır: kuyruk uzunluğu alma</span><span class="sxs-lookup"><span data-stu-id="35bef-166">How To: Get the Queue Length</span></span>
<span data-ttu-id="35bef-167">**GetQueueMetadata** iletiler kuyrukta yaklaşık sayısı dahil olmak üzere kuyruk hakkındaki meta verileri döndürür.</span><span class="sxs-lookup"><span data-stu-id="35bef-167">The **getQueueMetadata** returns metadata about the queue, including the approximate number of messages waiting in the queue.</span></span>

```
queueSvc.getQueueMetadata('myqueue', function(error, result, response){
  if(!error){
    // Queue length is available in result.approximateMessageCount
  }
});
```

## <a name="how-to-list-queues"></a><span data-ttu-id="35bef-168">Nasıl yapılır: Sorgular listesi</span><span class="sxs-lookup"><span data-stu-id="35bef-168">How To: List Queues</span></span>
<span data-ttu-id="35bef-169">Kuyrukların listesini almak için kullanın **listQueuesSegmented**.</span><span class="sxs-lookup"><span data-stu-id="35bef-169">To retrieve a list of queues, use **listQueuesSegmented**.</span></span> <span data-ttu-id="35bef-170">Belirli bir önek tarafından filtre uygulanmış bir listesini almak için kullanmak **listQueuesSegmentedWithPrefix**.</span><span class="sxs-lookup"><span data-stu-id="35bef-170">To retrieve a list filtered by a specific prefix, use **listQueuesSegmentedWithPrefix**.</span></span>

```
queueSvc.listQueuesSegmented(null, function(error, result, response){
  if(!error){
    // result.entries contains the list of queues
  }
});
```

<span data-ttu-id="35bef-171">Tüm Kuyruklar döndürülemez, `result.continuationToken` ilk parametresi olarak kullanılabilir **listQueuesSegmented** veya öğesinin ikinci parametresi, **listQueuesSegmentedWithPrefix** daha fazla sonuç almak için.</span><span class="sxs-lookup"><span data-stu-id="35bef-171">If all queues cannot be returned, `result.continuationToken` can be used as the first parameter of **listQueuesSegmented** or the second parameter of **listQueuesSegmentedWithPrefix** to retrieve more results.</span></span>

## <a name="how-to-delete-a-queue"></a><span data-ttu-id="35bef-172">Nasıl yapılır: bir kuyruk silme</span><span class="sxs-lookup"><span data-stu-id="35bef-172">How To: Delete a Queue</span></span>
<span data-ttu-id="35bef-173">Bir kuyruk ve içerdiği tüm iletileri silmek için arama **deleteQueue** nesnesinde yöntemi.</span><span class="sxs-lookup"><span data-stu-id="35bef-173">To delete a queue and all the messages contained in it, call the **deleteQueue** method on the queue object.</span></span>

```
queueSvc.deleteQueue(queueName, function(error, response){
  if(!error){
    // Queue has been deleted
  }
});
```

<span data-ttu-id="35bef-174">Silmeden bir Sıraya alınan tüm iletileri silmek için kullanın **clearMessages**.</span><span class="sxs-lookup"><span data-stu-id="35bef-174">To clear all messages from a queue without deleting it, use **clearMessages**.</span></span>

## <a name="how-to-work-with-shared-access-signatures"></a><span data-ttu-id="35bef-175">Nasıl yapılır: paylaşılan erişim imzaları ile çalışma</span><span class="sxs-lookup"><span data-stu-id="35bef-175">How to: Work with Shared Access Signatures</span></span>
<span data-ttu-id="35bef-176">Paylaşılan erişim imzaları (SAS) depolama hesabı adı veya anahtarları sağlamadan sıraları ayrıntılı erişim sağlamak için güvenli bir yoludur.</span><span class="sxs-lookup"><span data-stu-id="35bef-176">Shared Access Signatures (SAS) are a secure way to provide granular access to queues without providing your storage account name or keys.</span></span> <span data-ttu-id="35bef-177">SAS genellikle iletiler göndermek bir mobil uygulama izin verme gibi sıralar, sınırlı erişim sağlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="35bef-177">SAS are often used to provide limited access to your queues, such as allowing a mobile app to submit messages.</span></span>

<span data-ttu-id="35bef-178">SAS kullanarak bulut tabanlı bir hizmete gibi güvenilir bir uygulama oluşturur **generateSharedAccessSignature** , **QueueService**ve güvenilmeyen veya yarı güvenilir uygulama sağlar.</span><span class="sxs-lookup"><span data-stu-id="35bef-178">A trusted application such as a cloud-based service generates a SAS using the **generateSharedAccessSignature** of the **QueueService**, and provides it to an untrusted or semi-trusted application.</span></span> <span data-ttu-id="35bef-179">Örneğin, bir mobil uygulama.</span><span class="sxs-lookup"><span data-stu-id="35bef-179">For example, a mobile app.</span></span> <span data-ttu-id="35bef-180">SAS SAS sahibi verilen erişim düzeyini yanı sıra SAS geçerli olduğu başlangıç ve bitiş tarihleri açıklar, bir ilke kullanılarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="35bef-180">The SAS is generated using a policy, which describes the start and end dates during which the SAS is valid, as well as the access level granted to the SAS holder.</span></span>

<span data-ttu-id="35bef-181">Aşağıdaki örnek, iletileri kuyruğa eklemek SAS sahibi izin veren yeni bir paylaşılan erişim ilkesi oluşturur ve 100 dakika oluşturulduktan sonra süresi dolar.</span><span class="sxs-lookup"><span data-stu-id="35bef-181">The following example generates a new shared access policy that will allow the SAS holder to add messages to the queue, and expires 100 minutes after the time it is created.</span></span>

```
var startDate = new Date();
var expiryDate = new Date(startDate);
expiryDate.setMinutes(startDate.getMinutes() + 100);
startDate.setMinutes(startDate.getMinutes() - 100);

var sharedAccessPolicy = {
  AccessPolicy: {
    Permissions: azure.QueueUtilities.SharedAccessPermissions.ADD,
    Start: startDate,
    Expiry: expiryDate
  }
};

var queueSAS = queueSvc.generateSharedAccessSignature('myqueue', sharedAccessPolicy);
var host = queueSvc.host;
```

<span data-ttu-id="35bef-182">SAS sahibi sıranın erişmeyi denediğinde, gerekli olduğu gibi konak bilgileri'nin de, sağlanan gerekir unutmayın.</span><span class="sxs-lookup"><span data-stu-id="35bef-182">Note that the host information must be provided also, as it is required when the SAS holder attempts to access the queue.</span></span>

<span data-ttu-id="35bef-183">İstemci uygulama ile SAS kullanan **QueueServiceWithSAS** sıranın karşı işlemlerini gerçekleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="35bef-183">The client application then uses the SAS with **QueueServiceWithSAS** to perform operations against the queue.</span></span> <span data-ttu-id="35bef-184">Aşağıdaki örnek, sıraya bağlanır ve bir ileti oluşturur.</span><span class="sxs-lookup"><span data-stu-id="35bef-184">The following example connects to the queue and creates a message.</span></span>

```
var sharedQueueService = azure.createQueueServiceWithSas(host, queueSAS);
sharedQueueService.createMessage('myqueue', 'Hello world from SAS!', function(error, result, response){
  if(!error){
    //message added
  }
});
```

<span data-ttu-id="35bef-185">Okuma, güncelleştirme veya iletileri silme girişiminde yapılmışsa SAS Ekle erişimle oluşturulmasının üzerinden bir hata döndürülür.</span><span class="sxs-lookup"><span data-stu-id="35bef-185">Since the SAS was generated with add access, if an attempt were made to read, update or delete messages, an error would be returned.</span></span>

### <a name="access-control-lists"></a><span data-ttu-id="35bef-186">Erişim denetimi listeleri</span><span class="sxs-lookup"><span data-stu-id="35bef-186">Access control lists</span></span>
<span data-ttu-id="35bef-187">Erişim ilkesi için bir SAS ayarlamak için erişim denetim listesi (ACL) da kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="35bef-187">You can also use an Access Control List (ACL) to set the access policy for a SAS.</span></span> <span data-ttu-id="35bef-188">Bu kuyruğa erişim, ancak her istemci için farklı erişim ilkeleri sağlamak birden çok istemciye izin vermek istiyorsanız yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="35bef-188">This is useful if you wish to allow multiple clients to access the queue, but provide different access policies for each client.</span></span>

<span data-ttu-id="35bef-189">Bir ACL her ilkesiyle ilişkili bir Kimliğe sahip bir dizi erişim ilkeleri kullanılarak uygulanır.</span><span class="sxs-lookup"><span data-stu-id="35bef-189">An ACL is implemented using an array of access policies, with an ID associated with each policy.</span></span> <span data-ttu-id="35bef-190">Aşağıdaki örnek, iki ilke tanımlar; bir 'Kullanıcı1' ve 'kullanıcı2' için:</span><span class="sxs-lookup"><span data-stu-id="35bef-190">The  following example defines two policies; one for 'user1' and one for 'user2':</span></span>

```
var sharedAccessPolicy = {
  user1: {
    Permissions: azure.QueueUtilities.SharedAccessPermissions.PROCESS,
    Start: startDate,
    Expiry: expiryDate
  },
  user2: {
    Permissions: azure.QueueUtilities.SharedAccessPermissions.ADD,
    Start: startDate,
    Expiry: expiryDate
  }
};
```

<span data-ttu-id="35bef-191">Aşağıdaki örnek için geçerli ACL alır **Sıram**, yeni ilkeleri kullanılarak ekler **setQueueAcl**.</span><span class="sxs-lookup"><span data-stu-id="35bef-191">The following example gets the current ACL for **myqueue**, then adds the new policies using **setQueueAcl**.</span></span> <span data-ttu-id="35bef-192">Bu yaklaşım sağlar:</span><span class="sxs-lookup"><span data-stu-id="35bef-192">This approach allows:</span></span>

```
var extend = require('extend');
queueSvc.getQueueAcl('myqueue', function(error, result, response) {
  if(!error){
    var newSignedIdentifiers = extend(true, result.signedIdentifiers, sharedAccessPolicy);
    queueSvc.setQueueAcl('myqueue', newSignedIdentifiers, function(error, result, response){
      if(!error){
        // ACL set
      }
    });
  }
});
```

<span data-ttu-id="35bef-193">ACL ayarladıktan sonra daha sonra bir ilke kimliği dayalı bir SAS oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="35bef-193">Once the ACL has been set, you can then create a SAS based on the ID for a policy.</span></span> <span data-ttu-id="35bef-194">Aşağıdaki örnek, 'kullanıcı2' için yeni bir SAS oluşturur:</span><span class="sxs-lookup"><span data-stu-id="35bef-194">The following example creates a new SAS for 'user2':</span></span>

```
queueSAS = queueSvc.generateSharedAccessSignature('myqueue', { Id: 'user2' });
```

## <a name="next-steps"></a><span data-ttu-id="35bef-195">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="35bef-195">Next Steps</span></span>
<span data-ttu-id="35bef-196">Kuyruk depolamanın temellerini öğrendiğinize göre daha karmaşık depolama görevleri hakkında bilgi edinmek için aşağıdaki bağlantıları izleyin.</span><span class="sxs-lookup"><span data-stu-id="35bef-196">Now that you've learned the basics of queue storage, follow these links to learn about more complex storage tasks.</span></span>

* <span data-ttu-id="35bef-197">Ziyaret [Azure depolama ekibi blogu][Azure Storage Team Blog].</span><span class="sxs-lookup"><span data-stu-id="35bef-197">Visit the [Azure Storage Team Blog][Azure Storage Team Blog].</span></span>
* <span data-ttu-id="35bef-198">Ziyaret [düğümü için Azure depolama SDK'sı] [ Azure Storage SDK for Node] github'daki.</span><span class="sxs-lookup"><span data-stu-id="35bef-198">Visit the [Azure Storage SDK for Node][Azure Storage SDK for Node] repository on GitHub.</span></span>

[Azure Storage SDK for Node]: https://github.com/Azure/azure-storage-node
[using the REST API]: http://msdn.microsoft.com/library/azure/hh264518.aspx
[Azure Portal]: https://portal.azure.com
<span data-ttu-id="35bef-199">[Azure App Service'te bir Node.js web uygulaması oluşturma]: ../app-service-web/app-service-web-get-started-nodejs.md</span><span class="sxs-lookup"><span data-stu-id="35bef-199">[Create a Node.js web app in Azure App Service]: ../app-service-web/app-service-web-get-started-nodejs.md</span></span>
<span data-ttu-id="35bef-200">[Azure tablo hizmeti kullanarak Node.js web uygulaması]: ../app-service-web/storage-nodejs-use-table-storage-web-site.md</span><span class="sxs-lookup"><span data-stu-id="35bef-200">[Node.js web app using the Azure Table Service]: ../app-service-web/storage-nodejs-use-table-storage-web-site.md</span></span>


<span data-ttu-id="35bef-201">[derleme ve Azure bulut hizmeti bir Node.js uygulamasını dağıtma]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md</span><span class="sxs-lookup"><span data-stu-id="35bef-201">[Build and deploy a Node.js application to an Azure Cloud Service]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md</span></span>
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
<span data-ttu-id="35bef-202">[derleme ve Web Matrix Azure'u Node.js web uygulamasına dağıtma]: ../app-service-web/web-sites-nodejs-use-webmatrix.md</span><span class="sxs-lookup"><span data-stu-id="35bef-202">[Build and deploy a Node.js web app to Azure using Web Matrix]: ../app-service-web/web-sites-nodejs-use-webmatrix.md</span></span>
