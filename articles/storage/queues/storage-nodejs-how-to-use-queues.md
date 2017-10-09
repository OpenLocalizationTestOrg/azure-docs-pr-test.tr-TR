---
title: aaaHow toouse node.js'den kuyruk depolama | Microsoft Docs
description: "Nasıl toouse hello Azure kuyruk hizmeti toocreate ve delete kuyruklar ve Ekle, Al ve iletileri silmek öğrenin. Node.js içinde yazılmış örneklerini içerir."
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
ms.openlocfilehash: 7e9778da4efa69f2e9d8fd480b9b6f5ace85951e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-queue-storage-from-nodejs"></a><span data-ttu-id="45997-104">Nasıl toouse node.js'den kuyruk depolama</span><span class="sxs-lookup"><span data-stu-id="45997-104">How toouse Queue storage from Node.js</span></span>
[!INCLUDE [storage-selector-queue-include](../../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-check-out-samples-all](../../../includes/storage-check-out-samples-all.md)]

## <a name="overview"></a><span data-ttu-id="45997-105">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="45997-105">Overview</span></span>
<span data-ttu-id="45997-106">Bu kılavuz size nasıl Microsoft Azure Queue hizmetini kullanarak tooperform genel senaryolar hello gösterir.</span><span class="sxs-lookup"><span data-stu-id="45997-106">This guide shows you how tooperform common scenarios using hello Microsoft Azure Queue service.</span></span> <span data-ttu-id="45997-107">Merhaba örnekleri hello Node.js API kullanılarak yazılır.</span><span class="sxs-lookup"><span data-stu-id="45997-107">hello samples are written using hello Node.js API.</span></span> <span data-ttu-id="45997-108">Merhaba kapsamdaki senaryolar da dahil **ekleme**, **gözatma**, **alma**, ve **silme** kuyruk iletileri yanı  **oluşturma ve silme**.</span><span class="sxs-lookup"><span data-stu-id="45997-108">hello scenarios covered include **inserting**, **peeking**, **getting**, and **deleting** queue messages, as well as **creating and deleting queues**.</span></span>

[!INCLUDE [storage-queue-concepts-include](../../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-nodejs-application"></a><span data-ttu-id="45997-109">Bir Node.js uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="45997-109">Create a Node.js Application</span></span>
<span data-ttu-id="45997-110">Boş bir Node.js uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="45997-110">Create a blank Node.js application.</span></span> <span data-ttu-id="45997-111">Bir Node.js uygulaması oluşturma yönergeleri için bkz: [Azure App Service'te bir Node.js web uygulaması oluşturma](../../app-service-web/app-service-web-get-started-nodejs.md), [derleme ve bir Node.js uygulaması tooan Azure bulut hizmeti dağıtma](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md) Windows PowerShell veya kullanma[ Derleme ve Web Matrix kullanarak bir Node.js web uygulaması tooAzure dağıtma](https://www.microsoft.com/web/webmatrix/).</span><span class="sxs-lookup"><span data-stu-id="45997-111">For instructions creating a Node.js application, see [Create a Node.js web app in Azure App Service](../../app-service-web/app-service-web-get-started-nodejs.md), [Build and deploy a Node.js application tooan Azure Cloud Service](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md) using Windows PowerShell, or [Build and deploy a Node.js web app tooAzure using Web Matrix](https://www.microsoft.com/web/webmatrix/).</span></span>

## <a name="configure-your-application-tooaccess-storage"></a><span data-ttu-id="45997-112">Uygulamanızı tooAccess depolama yapılandırma</span><span class="sxs-lookup"><span data-stu-id="45997-112">Configure Your Application tooAccess Storage</span></span>
<span data-ttu-id="45997-113">Azure depolama toouse hello storage REST Hizmetleri ile iletişim kuran bir dizi kolaylık içerir Node.js için hello Azure depolama SDK'sı gerekir.</span><span class="sxs-lookup"><span data-stu-id="45997-113">toouse Azure storage, you need hello Azure Storage SDK for Node.js, which includes a set of convenience libraries that communicate with hello storage REST services.</span></span>

### <a name="use-node-package-manager-npm-tooobtain-hello-package"></a><span data-ttu-id="45997-114">Düğüm paketi Yöneticisi (NPM) tooobtain hello paketini kullanın</span><span class="sxs-lookup"><span data-stu-id="45997-114">Use Node Package Manager (NPM) tooobtain hello package</span></span>
1. <span data-ttu-id="45997-115">Bir komut satırı arabirimi gibi kullandığınız **PowerShell** (Windows) **Terminal** (Mac) veya **Bash** (UNIX) örnek uygulamanızı oluşturulduğu toohello klasörüne gidin.</span><span class="sxs-lookup"><span data-stu-id="45997-115">Use a command-line interface such as **PowerShell** (Windows,) **Terminal** (Mac,) or **Bash** (Unix), navigate toohello folder where you created your sample application.</span></span>
2. <span data-ttu-id="45997-116">Tür **npm yükleme azure depolama** hello komut penceresinde.</span><span class="sxs-lookup"><span data-stu-id="45997-116">Type **npm install azure-storage** in hello command window.</span></span> <span data-ttu-id="45997-117">Merhaba komut çıktısı aşağıdaki örneğine benzer toohello ' dir.</span><span class="sxs-lookup"><span data-stu-id="45997-117">Output from hello command is similar toohello following example.</span></span>
 
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

3. <span data-ttu-id="45997-118">Merhaba el ile çalıştırabilirsiniz **ls** komutu tooverify, bir **düğümü\_modülleri** klasörü oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="45997-118">You can manually run hello **ls** command tooverify that a **node\_modules** folder was created.</span></span> <span data-ttu-id="45997-119">Bu klasöre hello bulacaksınız **azure depolama** depolama birimine erişmesi gereken hello kitaplıkları içeren paket.</span><span class="sxs-lookup"><span data-stu-id="45997-119">Inside that folder you will find hello **azure-storage** package, which contains hello libraries you need to access storage.</span></span>

### <a name="import-hello-package"></a><span data-ttu-id="45997-120">Merhaba paketi İçeri Aktar</span><span class="sxs-lookup"><span data-stu-id="45997-120">Import hello package</span></span>
<span data-ttu-id="45997-121">Not Defteri'nde veya başka bir metin düzenleyicisi kullanarak ekleyin toohello üst aşağıdaki hello **server.js** toouse depolama burada düşündüğünüz dosya hello uygulamasının:</span><span class="sxs-lookup"><span data-stu-id="45997-121">Using Notepad or another text editor, add hello following toohello top the **server.js** file of hello application where you intend toouse storage:</span></span>

```
var azure = require('azure-storage');
```

## <a name="setup-an-azure-storage-connection"></a><span data-ttu-id="45997-122">Bir Azure depolama bağlantı Kur</span><span class="sxs-lookup"><span data-stu-id="45997-122">Setup an Azure Storage Connection</span></span>
<span data-ttu-id="45997-123">Hello azure modülü hello ortam değişkenleri AZURE okuma\_depolama\_HESABINI ve AZURE\_depolama\_erişim\_anahtar ya da AZURE\_depolama\_bağlantı \_Gerekli bilgileri tooconnect tooyour Azure depolama hesabı için dize.</span><span class="sxs-lookup"><span data-stu-id="45997-123">hello azure module will read hello environment variables AZURE\_STORAGE\_ACCOUNT and AZURE\_STORAGE\_ACCESS\_KEY, or AZURE\_STORAGE\_CONNECTION\_STRING for information required tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="45997-124">Bu ortam değişkenleri ayarlanmamışsa çağrılırken hello hesap bilgileri belirtmelisiniz **createQueueService**.</span><span class="sxs-lookup"><span data-stu-id="45997-124">If these environment variables are not set, you must specify hello account information when calling **createQueueService**.</span></span>

<span data-ttu-id="45997-125">Hello hello ortam değişkenlerini ayarlama örneği için [Azure Portal](https://portal.azure.com) [Node.js web uygulamasını Azure tablo hizmeti hello kullanarak] bir Azure Web sitesi için bkz.</span><span class="sxs-lookup"><span data-stu-id="45997-125">For an example of setting hello environment variables in hello [Azure Portal](https://portal.azure.com) for an Azure Website, see [Node.js web app using hello Azure Table Service].</span></span>

## <a name="how-to-create-a-queue"></a><span data-ttu-id="45997-126">Nasıl yapılır: bir sıra oluşturun</span><span class="sxs-lookup"><span data-stu-id="45997-126">How To: Create a Queue</span></span>
<span data-ttu-id="45997-127">Merhaba aşağıdaki kod oluşturur bir **QueueService** toowork kuyruklarla sağlayan nesne.</span><span class="sxs-lookup"><span data-stu-id="45997-127">hello following code creates a **QueueService** object, which enables you toowork with queues.</span></span>

```
var queueSvc = azure.createQueueService();
```

<span data-ttu-id="45997-128">Kullanım hello **createQueueIfNotExists** hello belirtilen sırayı zaten var veya zaten yoksa, hello belirtilen adla yeni bir sıra oluşturur döndüren yöntemi.</span><span class="sxs-lookup"><span data-stu-id="45997-128">Use hello **createQueueIfNotExists** method, which returns hello specified queue if it already exists or creates a new queue with hello specified name if it does not already exist.</span></span>

```
queueSvc.createQueueIfNotExists('myqueue', function(error, result, response){
  if(!error){
    // Queue created or exists
  }
});
```

<span data-ttu-id="45997-129">Merhaba sıra oluşturduysanız, `result.created` doğrudur.</span><span class="sxs-lookup"><span data-stu-id="45997-129">If hello queue is created, `result.created` is true.</span></span> <span data-ttu-id="45997-130">Merhaba sırası varsa, `result.created` false olur.</span><span class="sxs-lookup"><span data-stu-id="45997-130">If hello queue exists, `result.created` is false.</span></span>

### <a name="filters"></a><span data-ttu-id="45997-131">Filtreler</span><span class="sxs-lookup"><span data-stu-id="45997-131">Filters</span></span>
<span data-ttu-id="45997-132">İsteğe bağlı filtreleme operations kullanılarak gerçekleştirilen uygulanan toooperations olabilir **QueueService**.</span><span class="sxs-lookup"><span data-stu-id="45997-132">Optional filtering operations can be applied toooperations performed using **QueueService**.</span></span> <span data-ttu-id="45997-133">İşlemleri filtreleme içerebilir günlüğe kaydetme, otomatik olarak yeniden deneniyor, vs. Filtreleri hello imza yöntemiyle uygulayan nesneler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="45997-133">Filtering operations can include logging, automatically retrying, etc. Filters are objects that implement a method with hello signature:</span></span>

```
function handle (requestOptions, next)
```

<span data-ttu-id="45997-134">Kendi hello isteği seçenekleri ön işleme yaptıktan sonra "İleri" imza aşağıdaki hello ile bir geri çağırma geçirme toocall hello yöntemi gerekir:</span><span class="sxs-lookup"><span data-stu-id="45997-134">After doing its preprocessing on hello request options, hello method needs toocall "next" passing a callback with hello following signature:</span></span>

```
function (returnObject, finalCallback, next)
```

<span data-ttu-id="45997-135">Bu geri çağırma ve hello returnObject (Merhaba isteği toohello sunucusundan hello yanıt) işlemden sonra hello geri çağırma tooeither gereken diğer filtreleri işleme toocontinue varsa sonraki çağırma veya yalnızca finalCallback çağırma aksi tooend hello ayarlama Hizmet başlatma.</span><span class="sxs-lookup"><span data-stu-id="45997-135">In this callback, and after processing hello returnObject (hello response from hello request toohello server), hello callback needs tooeither invoke next if it exists toocontinue processing other filters or simply invoke finalCallback otherwise tooend up hello service invocation.</span></span>

<span data-ttu-id="45997-136">Yeniden deneme mantığını uygulaması iki filtre hello Node.js için Azure SDK ile birlikte **ExponentialRetryPolicyFilter** ve **LinearRetryPolicyFilter**.</span><span class="sxs-lookup"><span data-stu-id="45997-136">Two filters that implement retry logic are included with hello Azure SDK for Node.js, **ExponentialRetryPolicyFilter** and **LinearRetryPolicyFilter**.</span></span> <span data-ttu-id="45997-137">Merhaba aşağıdaki oluşturur bir **QueueService** hello kullanan nesneyi **ExponentialRetryPolicyFilter**:</span><span class="sxs-lookup"><span data-stu-id="45997-137">hello following creates a **QueueService** object that uses hello **ExponentialRetryPolicyFilter**:</span></span>

```
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var queueSvc = azure.createQueueService().withFilter(retryOperations);
```

## <a name="how-to-insert-a-message-into-a-queue"></a><span data-ttu-id="45997-138">Nasıl yapılır: bir sıraya bir ileti Ekle</span><span class="sxs-lookup"><span data-stu-id="45997-138">How To: Insert a Message into a Queue</span></span>
<span data-ttu-id="45997-139">bir kuyruk, kullanım hello iletiye tooinsert **CreateMessage nesne** yeni bir ileti oluşturun ve toohello sırası eklemek için yöntem.</span><span class="sxs-lookup"><span data-stu-id="45997-139">tooinsert a message into a queue, use hello **createMessage** method to create a new message and add it toohello queue.</span></span>

```
queueSvc.createMessage('myqueue', "Hello world!", function(error, result, response){
  if(!error){
    // Message inserted
  }
});
```

## <a name="how-to-peek-at-hello-next-message"></a><span data-ttu-id="45997-140">Nasıl yapılır: sonraki iletiyi hello Gözat</span><span class="sxs-lookup"><span data-stu-id="45997-140">How To: Peek at hello Next Message</span></span>
<span data-ttu-id="45997-141">Bir sıra Merhaba öne hello iletiye tarafından arama hello hello kuyruktan kaldırmadan iletiye göz atabilirsiniz **peekMessages** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="45997-141">You can peek at hello message in hello front of a queue without removing it from hello queue by calling hello **peekMessages** method.</span></span> <span data-ttu-id="45997-142">Varsayılan olarak, **peekMessages** tek bir ileti iletiye göz atar.</span><span class="sxs-lookup"><span data-stu-id="45997-142">By default, **peekMessages** peeks at a single message.</span></span>

```
queueSvc.peekMessages('myqueue', function(error, result, response){
  if(!error){
    // Message text is in messages[0].messageText
  }
});
```

<span data-ttu-id="45997-143">Merhaba `result` selamlama iletisine içerir.</span><span class="sxs-lookup"><span data-stu-id="45997-143">hello `result` contains hello message.</span></span>

> [!NOTE]
> <span data-ttu-id="45997-144">Kullanarak **peekMessages** hello sıraya ileti olduğunda ileti döndürdü ancak bir hata döndürmez.</span><span class="sxs-lookup"><span data-stu-id="45997-144">Using **peekMessages** when there are no messages in hello queue will not return an error, however no messages will be returned.</span></span>
> 
> 

## <a name="how-to-dequeue-hello-next-message"></a><span data-ttu-id="45997-145">Nasıl yapılır: hello sonraki iletiyi sıradan çıkarma</span><span class="sxs-lookup"><span data-stu-id="45997-145">How To: Dequeue hello Next Message</span></span>
<span data-ttu-id="45997-146">İleti işlenirken iki aşamalı bir işlemdir:</span><span class="sxs-lookup"><span data-stu-id="45997-146">Processing a message is a two-stage process:</span></span>

1. <span data-ttu-id="45997-147">Selamlama iletisine dequeue.</span><span class="sxs-lookup"><span data-stu-id="45997-147">Dequeue hello message.</span></span>
2. <span data-ttu-id="45997-148">Merhaba iletiyi silin.</span><span class="sxs-lookup"><span data-stu-id="45997-148">Delete hello message.</span></span>

<span data-ttu-id="45997-149">toodequeue bir ileti kullanmak **getMessages**.</span><span class="sxs-lookup"><span data-stu-id="45997-149">toodequeue a message, use **getMessages**.</span></span> <span data-ttu-id="45997-150">Diğer bir istemcileri onları işleyebilmek için karışılama iletileri hello sırada görünmez kılar.</span><span class="sxs-lookup"><span data-stu-id="45997-150">This makes hello messages invisible in hello queue, so no other clients can process them.</span></span> <span data-ttu-id="45997-151">Uygulamanızı bir ileti işlediğinde çağrısı **deleteMessage** toodelete onu hello sırasından.</span><span class="sxs-lookup"><span data-stu-id="45997-151">Once your application has processed a message, call **deleteMessage** toodelete it from hello queue.</span></span> <span data-ttu-id="45997-152">Aşağıdaki örneğine hello bir ileti alır, ardından da siler:</span><span class="sxs-lookup"><span data-stu-id="45997-152">hello following example gets a message, then deletes it:</span></span>

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
> <span data-ttu-id="45997-153">Varsayılan olarak, bir ileti yalnızca 30 saniye boyunca geçmesi görünür tooother istemcileri olan gizlenir.</span><span class="sxs-lookup"><span data-stu-id="45997-153">By default, a message is only hidden for 30 seconds, after which it is visible tooother clients.</span></span> <span data-ttu-id="45997-154">Kullanarak farklı bir değer belirtebilirsiniz `options.visibilityTimeout` ile **getMessages**.</span><span class="sxs-lookup"><span data-stu-id="45997-154">You can specify a different value by using `options.visibilityTimeout` with **getMessages**.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="45997-155">Kullanarak **getMessages** hello sıraya ileti olduğunda ileti döndürdü ancak bir hata döndürmez.</span><span class="sxs-lookup"><span data-stu-id="45997-155">Using **getMessages** when there are no messages in hello queue will not return an error, however no messages will be returned.</span></span>
> 
> 

## <a name="how-to-change-hello-contents-of-a-queued-message"></a><span data-ttu-id="45997-156">Nasıl yapılır: bir sıraya ileti hello içeriğini değiştirme</span><span class="sxs-lookup"><span data-stu-id="45997-156">How To: Change hello Contents of a Queued Message</span></span>
<span data-ttu-id="45997-157">Bir ileti sırası hello kullanarak yerinde hello içeriğini değiştirebilirsiniz **updateMessage**.</span><span class="sxs-lookup"><span data-stu-id="45997-157">You can change hello contents of a message in-place in hello queue using **updateMessage**.</span></span> <span data-ttu-id="45997-158">Aşağıdaki örneğine hello hello metin iletisinin güncelleştirir:</span><span class="sxs-lookup"><span data-stu-id="45997-158">hello following example updates hello text of a message:</span></span>

```
queueSvc.getMessages('myqueue', function(error, result, response){
  if(!error){
    // Got hello message
    var message = result[0];
    queueSvc.updateMessage('myqueue', message.messageId, message.popReceipt, 10, {messageText: 'new text'}, function(error, result, response){
      if(!error){
        // Message updated successfully
      }
    });
  }
});
```

## <a name="how-to-additional-options-for-dequeuing-messages"></a><span data-ttu-id="45997-159">Nasıl yapılır: kuyruktan alma için ek seçenekler iletileri</span><span class="sxs-lookup"><span data-stu-id="45997-159">How To: Additional Options for Dequeuing Messages</span></span>
<span data-ttu-id="45997-160">Bir sıradan ileti alma özelleştirebilirsiniz iki yolu vardır:</span><span class="sxs-lookup"><span data-stu-id="45997-160">There are two ways you can customize message retrieval from a queue:</span></span>

* <span data-ttu-id="45997-161">`options.numOfMessages`-Almak toplu iletiler (yukarı too32.)</span><span class="sxs-lookup"><span data-stu-id="45997-161">`options.numOfMessages` - Retrieve a batch of messages (up too32.)</span></span>
* <span data-ttu-id="45997-162">`options.visibilityTimeout`-Daha uzun veya kısaysa görünmezlik zaman aşımı ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="45997-162">`options.visibilityTimeout` - Set a longer or shorter invisibility timeout.</span></span>

<span data-ttu-id="45997-163">Merhaba aşağıdaki örnek kullanır hello **getMessages** bir çağrı yöntemi tooget 15 iletileri.</span><span class="sxs-lookup"><span data-stu-id="45997-163">hello following example uses hello **getMessages** method tooget 15 messages in one call.</span></span> <span data-ttu-id="45997-164">Her bir iletiyi kullanarak işler sonra bir döngü için.</span><span class="sxs-lookup"><span data-stu-id="45997-164">Then it processes each message using a for loop.</span></span> <span data-ttu-id="45997-165">Ayrıca, bu yöntem tarafından döndürülen tüm iletiler için hello görünmezlik zaman aşımı toofive dakika ayarlar.</span><span class="sxs-lookup"><span data-stu-id="45997-165">It also sets hello invisibility timeout toofive minutes for all messages returned by this method.</span></span>

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

## <a name="how-to-get-hello-queue-length"></a><span data-ttu-id="45997-166">Nasıl yapılır: hello kuyruk uzunluğu alma</span><span class="sxs-lookup"><span data-stu-id="45997-166">How To: Get hello Queue Length</span></span>
<span data-ttu-id="45997-167">Merhaba **getQueueMetadata** hello yaklaşık hello kuyrukta ileti sayısı dahil olmak üzere hello kuyruk hakkındaki meta verileri döndürür.</span><span class="sxs-lookup"><span data-stu-id="45997-167">hello **getQueueMetadata** returns metadata about hello queue, including hello approximate number of messages waiting in hello queue.</span></span>

```
queueSvc.getQueueMetadata('myqueue', function(error, result, response){
  if(!error){
    // Queue length is available in result.approximateMessageCount
  }
});
```

## <a name="how-to-list-queues"></a><span data-ttu-id="45997-168">Nasıl yapılır: Sorgular listesi</span><span class="sxs-lookup"><span data-stu-id="45997-168">How To: List Queues</span></span>
<span data-ttu-id="45997-169">tooretrieve kuyrukların, kullanım listesini **listQueuesSegmented**.</span><span class="sxs-lookup"><span data-stu-id="45997-169">tooretrieve a list of queues, use **listQueuesSegmented**.</span></span> <span data-ttu-id="45997-170">tooretrieve listesini filtre tarafından belirli bir önek, kullanın **listQueuesSegmentedWithPrefix**.</span><span class="sxs-lookup"><span data-stu-id="45997-170">tooretrieve a list filtered by a specific prefix, use **listQueuesSegmentedWithPrefix**.</span></span>

```
queueSvc.listQueuesSegmented(null, function(error, result, response){
  if(!error){
    // result.entries contains hello list of queues
  }
});
```

<span data-ttu-id="45997-171">Tüm Kuyruklar döndürülemez, `result.continuationToken` öğesinin ilk parametresi, hello olarak kullanılan **listQueuesSegmented** veya ikinci parametresi, hello **listQueuesSegmentedWithPrefix** tooretrieve daha fazla sonuç.</span><span class="sxs-lookup"><span data-stu-id="45997-171">If all queues cannot be returned, `result.continuationToken` can be used as hello first parameter of **listQueuesSegmented** or hello second parameter of **listQueuesSegmentedWithPrefix** tooretrieve more results.</span></span>

## <a name="how-to-delete-a-queue"></a><span data-ttu-id="45997-172">Nasıl yapılır: bir kuyruk silme</span><span class="sxs-lookup"><span data-stu-id="45997-172">How To: Delete a Queue</span></span>
<span data-ttu-id="45997-173">toodelete bir sıra ve tüm karışılama iletileri bulunan içinde arama **deleteQueue** hello nesnesinde yöntemi.</span><span class="sxs-lookup"><span data-stu-id="45997-173">toodelete a queue and all hello messages contained in it, call the **deleteQueue** method on hello queue object.</span></span>

```
queueSvc.deleteQueue(queueName, function(error, response){
  if(!error){
    // Queue has been deleted
  }
});
```

<span data-ttu-id="45997-174">tüm iletileri silmeden, bir kuyruktan tooclear kullanan **clearMessages**.</span><span class="sxs-lookup"><span data-stu-id="45997-174">tooclear all messages from a queue without deleting it, use **clearMessages**.</span></span>

## <a name="how-to-work-with-shared-access-signatures"></a><span data-ttu-id="45997-175">Nasıl yapılır: paylaşılan erişim imzaları ile çalışma</span><span class="sxs-lookup"><span data-stu-id="45997-175">How to: Work with Shared Access Signatures</span></span>
<span data-ttu-id="45997-176">Paylaşılan erişim imzaları (SAS) depolama hesabı adı veya anahtarları sağlamadan güvenli şekilde tooprovide ayrıntılı erişim tooqueues ' dir.</span><span class="sxs-lookup"><span data-stu-id="45997-176">Shared Access Signatures (SAS) are a secure way tooprovide granular access tooqueues without providing your storage account name or keys.</span></span> <span data-ttu-id="45997-177">SAS toosubmit iletileri bir mobil uygulama izin verme gibi sınırlı kullanılan tooprovide tooyour sıralarına erişim, çoğunlukla olur.</span><span class="sxs-lookup"><span data-stu-id="45997-177">SAS are often used tooprovide limited access tooyour queues, such as allowing a mobile app toosubmit messages.</span></span>

<span data-ttu-id="45997-178">Bir bulut tabanlı hizmeti gibi güvenilir bir uygulama hello kullanarak bir SAS oluşturur **generateSharedAccessSignature** Merhaba, **QueueService**, tooan sağlar ve güvenilmeyen veya yarı güvenilir uygulama.</span><span class="sxs-lookup"><span data-stu-id="45997-178">A trusted application such as a cloud-based service generates a SAS using hello **generateSharedAccessSignature** of hello **QueueService**, and provides it tooan untrusted or semi-trusted application.</span></span> <span data-ttu-id="45997-179">Örneğin, bir mobil uygulama.</span><span class="sxs-lookup"><span data-stu-id="45997-179">For example, a mobile app.</span></span> <span data-ttu-id="45997-180">Hello SAS hello başlangıç tanımlayan bir ilke ve bitiş tarihleri sırasında hangi hello SAS geçerlidir kullanılarak oluşturulan, aynı zamanda erişim düzeyi verilen toohello SAS sahibi hello.</span><span class="sxs-lookup"><span data-stu-id="45997-180">hello SAS is generated using a policy, which describes hello start and end dates during which hello SAS is valid, as well as hello access level granted toohello SAS holder.</span></span>

<span data-ttu-id="45997-181">Aşağıdaki örnek hello hello SAS sahibi tooadd iletileri toohello sırası izin veren yeni bir paylaşılan erişim ilkesi oluşturur ve 100 dakika hello zaman oluşturulduktan sonra süresi dolar.</span><span class="sxs-lookup"><span data-stu-id="45997-181">hello following example generates a new shared access policy that will allow hello SAS holder tooadd messages toohello queue, and expires 100 minutes after hello time it is created.</span></span>

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

<span data-ttu-id="45997-182">Gerekli olduğu gibi aynı zamanda, hello SAS sahibi tooaccess hello sıra çalıştığında sağlanan hello ana bilgisayar bilgilerini olması gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="45997-182">Note that hello host information must be provided also, as it is required when hello SAS holder attempts tooaccess hello queue.</span></span>

<span data-ttu-id="45997-183">ile SAS kullanır hello sonra istemci uygulaması Hello **QueueServiceWithSAS** hello sıra karşı tooperform işlemleri.</span><span class="sxs-lookup"><span data-stu-id="45997-183">hello client application then uses hello SAS with **QueueServiceWithSAS** tooperform operations against hello queue.</span></span> <span data-ttu-id="45997-184">Aşağıdaki örnek hello toohello sıra bağlanır ve bir ileti oluşturur.</span><span class="sxs-lookup"><span data-stu-id="45997-184">hello following example connects toohello queue and creates a message.</span></span>

```
var sharedQueueService = azure.createQueueServiceWithSas(host, queueSAS);
sharedQueueService.createMessage('myqueue', 'Hello world from SAS!', function(error, result, response){
  if(!error){
    //message added
  }
});
```

<span data-ttu-id="45997-185">Update veya delete iletileri tooread girişiminde yapılmışsa hello SAS Ekle erişimle oluşturulmasının üzerinden, bir hata döndürülür.</span><span class="sxs-lookup"><span data-stu-id="45997-185">Since hello SAS was generated with add access, if an attempt were made tooread, update or delete messages, an error would be returned.</span></span>

### <a name="access-control-lists"></a><span data-ttu-id="45997-186">Erişim denetimi listeleri</span><span class="sxs-lookup"><span data-stu-id="45997-186">Access control lists</span></span>
<span data-ttu-id="45997-187">Erişim denetimi listesi (ACL) tooset hello erişim ilkesi için bir SAS de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="45997-187">You can also use an Access Control List (ACL) tooset hello access policy for a SAS.</span></span> <span data-ttu-id="45997-188">Birden çok istemcileri tooaccess hello sıra tooallow istiyor, ancak her istemci için farklı erişim ilkeleri sağlar, bu yararlı olur.</span><span class="sxs-lookup"><span data-stu-id="45997-188">This is useful if you wish tooallow multiple clients tooaccess hello queue, but provide different access policies for each client.</span></span>

<span data-ttu-id="45997-189">Bir ACL her ilkesiyle ilişkili bir Kimliğe sahip bir dizi erişim ilkeleri kullanılarak uygulanır.</span><span class="sxs-lookup"><span data-stu-id="45997-189">An ACL is implemented using an array of access policies, with an ID associated with each policy.</span></span> <span data-ttu-id="45997-190">Aşağıdaki örnek hello iki ilke tanımlar; bir 'Kullanıcı1' ve 'kullanıcı2' için:</span><span class="sxs-lookup"><span data-stu-id="45997-190">hello  following example defines two policies; one for 'user1' and one for 'user2':</span></span>

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

<span data-ttu-id="45997-191">Aşağıdaki örnek alır hello hello geçerli ACL'si **Sıram**, hello yeni ilkeleri kullanılarak ekler **setQueueAcl**.</span><span class="sxs-lookup"><span data-stu-id="45997-191">hello following example gets hello current ACL for **myqueue**, then adds hello new policies using **setQueueAcl**.</span></span> <span data-ttu-id="45997-192">Bu yaklaşım sağlar:</span><span class="sxs-lookup"><span data-stu-id="45997-192">This approach allows:</span></span>

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

<span data-ttu-id="45997-193">Bir kez hello ACL ayarlayın, hello Kimliği İlkesi için temel bir SAS sonra oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="45997-193">Once hello ACL has been set, you can then create a SAS based on hello ID for a policy.</span></span> <span data-ttu-id="45997-194">Aşağıdaki örnek hello 'kullanıcı2' için yeni bir SAS oluşturur:</span><span class="sxs-lookup"><span data-stu-id="45997-194">hello following example creates a new SAS for 'user2':</span></span>

```
queueSAS = queueSvc.generateSharedAccessSignature('myqueue', { Id: 'user2' });
```

## <a name="next-steps"></a><span data-ttu-id="45997-195">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="45997-195">Next Steps</span></span>
<span data-ttu-id="45997-196">Kuyruk depolamanın hello temel bilgileri öğrendiğinize göre bu bağlantıları toolearn daha karmaşık depolama görevleri hakkında izleyin.</span><span class="sxs-lookup"><span data-stu-id="45997-196">Now that you've learned hello basics of queue storage, follow these links toolearn about more complex storage tasks.</span></span>

* <span data-ttu-id="45997-197">Merhaba [Azure depolama ekibi blogu] [Azure depolama ekibi blogu] ziyaret edin.</span><span class="sxs-lookup"><span data-stu-id="45997-197">Visit hello [Azure Storage Team Blog][Azure Storage Team Blog].</span></span>
* <span data-ttu-id="45997-198">Merhaba ziyaret [düğümü için Azure depolama SDK'sı] [ Azure Storage SDK for Node] github'daki.</span><span class="sxs-lookup"><span data-stu-id="45997-198">Visit hello [Azure Storage SDK for Node][Azure Storage SDK for Node] repository on GitHub.</span></span>

[Azure Storage SDK for Node]: https://github.com/Azure/azure-storage-node
[using hello REST API]: http://msdn.microsoft.com/library/azure/hh264518.aspx
[Azure Portal]: https://portal.azure.com<span data-ttu-id="45997-199">
[Azure App Service'te bir Node.js web uygulaması oluşturma](../../app-service-web/app-service-web-get-started-nodejs.md) </span><span class="sxs-lookup"><span data-stu-id="45997-199">
[Create a Node.js web app in Azure App Service](../../app-service-web/app-service-web-get-started-nodejs.md) </span></span>  
<span data-ttu-id="45997-200">[Hello Azure tablo hizmeti kullanarak Node.js web uygulaması](../../app-service-web/storage-nodejs-use-table-storage-web-site.md)
</span><span class="sxs-lookup"><span data-stu-id="45997-200">[Node.js web app using hello Azure Table Service](../../app-service-web/storage-nodejs-use-table-storage-web-site.md)
</span></span>  


<span data-ttu-id="45997-201">[Derleme ve bir Node.js uygulaması tooan Azure bulut hizmeti dağıtma](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md) </span><span class="sxs-lookup"><span data-stu-id="45997-201">[Build and deploy a Node.js application tooan Azure Cloud Service](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md) </span></span>  
<span data-ttu-id="45997-202">[Azure depolama ekibi blogu]: http://blogs.msdn.com/b/windowsazurestorage/ [derleme ve Web Matrix kullanarak bir Node.js web uygulaması tooAzure dağıtma]: https://www.microsoft.com/web/webmatrix/</span><span class="sxs-lookup"><span data-stu-id="45997-202">[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/ [Build and deploy a Node.js web app tooAzure using Web Matrix]: https://www.microsoft.com/web/webmatrix/</span></span>   
