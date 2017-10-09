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
# <a name="how-toouse-queue-storage-from-nodejs"></a>Nasıl toouse node.js'den kuyruk depolama
[!INCLUDE [storage-selector-queue-include](../../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-check-out-samples-all](../../../includes/storage-check-out-samples-all.md)]

## <a name="overview"></a>Genel Bakış
Bu kılavuz size nasıl Microsoft Azure Queue hizmetini kullanarak tooperform genel senaryolar hello gösterir. Merhaba örnekleri hello Node.js API kullanılarak yazılır. Merhaba kapsamdaki senaryolar da dahil **ekleme**, **gözatma**, **alma**, ve **silme** kuyruk iletileri yanı  **oluşturma ve silme**.

[!INCLUDE [storage-queue-concepts-include](../../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-nodejs-application"></a>Bir Node.js uygulaması oluşturma
Boş bir Node.js uygulaması oluşturun. Bir Node.js uygulaması oluşturma yönergeleri için bkz: [Azure App Service'te bir Node.js web uygulaması oluşturma](../../app-service-web/app-service-web-get-started-nodejs.md), [derleme ve bir Node.js uygulaması tooan Azure bulut hizmeti dağıtma](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md) Windows PowerShell veya kullanma[ Derleme ve Web Matrix kullanarak bir Node.js web uygulaması tooAzure dağıtma](https://www.microsoft.com/web/webmatrix/).

## <a name="configure-your-application-tooaccess-storage"></a>Uygulamanızı tooAccess depolama yapılandırma
Azure depolama toouse hello storage REST Hizmetleri ile iletişim kuran bir dizi kolaylık içerir Node.js için hello Azure depolama SDK'sı gerekir.

### <a name="use-node-package-manager-npm-tooobtain-hello-package"></a>Düğüm paketi Yöneticisi (NPM) tooobtain hello paketini kullanın
1. Bir komut satırı arabirimi gibi kullandığınız **PowerShell** (Windows) **Terminal** (Mac) veya **Bash** (UNIX) örnek uygulamanızı oluşturulduğu toohello klasörüne gidin.
2. Tür **npm yükleme azure depolama** hello komut penceresinde. Merhaba komut çıktısı aşağıdaki örneğine benzer toohello ' dir.
 
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

3. Merhaba el ile çalıştırabilirsiniz **ls** komutu tooverify, bir **düğümü\_modülleri** klasörü oluşturuldu. Bu klasöre hello bulacaksınız **azure depolama** depolama birimine erişmesi gereken hello kitaplıkları içeren paket.

### <a name="import-hello-package"></a>Merhaba paketi İçeri Aktar
Not Defteri'nde veya başka bir metin düzenleyicisi kullanarak ekleyin toohello üst aşağıdaki hello **server.js** toouse depolama burada düşündüğünüz dosya hello uygulamasının:

```
var azure = require('azure-storage');
```

## <a name="setup-an-azure-storage-connection"></a>Bir Azure depolama bağlantı Kur
Hello azure modülü hello ortam değişkenleri AZURE okuma\_depolama\_HESABINI ve AZURE\_depolama\_erişim\_anahtar ya da AZURE\_depolama\_bağlantı \_Gerekli bilgileri tooconnect tooyour Azure depolama hesabı için dize. Bu ortam değişkenleri ayarlanmamışsa çağrılırken hello hesap bilgileri belirtmelisiniz **createQueueService**.

Hello hello ortam değişkenlerini ayarlama örneği için [Azure Portal](https://portal.azure.com) [Node.js web uygulamasını Azure tablo hizmeti hello kullanarak] bir Azure Web sitesi için bkz.

## <a name="how-to-create-a-queue"></a>Nasıl yapılır: bir sıra oluşturun
Merhaba aşağıdaki kod oluşturur bir **QueueService** toowork kuyruklarla sağlayan nesne.

```
var queueSvc = azure.createQueueService();
```

Kullanım hello **createQueueIfNotExists** hello belirtilen sırayı zaten var veya zaten yoksa, hello belirtilen adla yeni bir sıra oluşturur döndüren yöntemi.

```
queueSvc.createQueueIfNotExists('myqueue', function(error, result, response){
  if(!error){
    // Queue created or exists
  }
});
```

Merhaba sıra oluşturduysanız, `result.created` doğrudur. Merhaba sırası varsa, `result.created` false olur.

### <a name="filters"></a>Filtreler
İsteğe bağlı filtreleme operations kullanılarak gerçekleştirilen uygulanan toooperations olabilir **QueueService**. İşlemleri filtreleme içerebilir günlüğe kaydetme, otomatik olarak yeniden deneniyor, vs. Filtreleri hello imza yöntemiyle uygulayan nesneler şunlardır:

```
function handle (requestOptions, next)
```

Kendi hello isteği seçenekleri ön işleme yaptıktan sonra "İleri" imza aşağıdaki hello ile bir geri çağırma geçirme toocall hello yöntemi gerekir:

```
function (returnObject, finalCallback, next)
```

Bu geri çağırma ve hello returnObject (Merhaba isteği toohello sunucusundan hello yanıt) işlemden sonra hello geri çağırma tooeither gereken diğer filtreleri işleme toocontinue varsa sonraki çağırma veya yalnızca finalCallback çağırma aksi tooend hello ayarlama Hizmet başlatma.

Yeniden deneme mantığını uygulaması iki filtre hello Node.js için Azure SDK ile birlikte **ExponentialRetryPolicyFilter** ve **LinearRetryPolicyFilter**. Merhaba aşağıdaki oluşturur bir **QueueService** hello kullanan nesneyi **ExponentialRetryPolicyFilter**:

```
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var queueSvc = azure.createQueueService().withFilter(retryOperations);
```

## <a name="how-to-insert-a-message-into-a-queue"></a>Nasıl yapılır: bir sıraya bir ileti Ekle
bir kuyruk, kullanım hello iletiye tooinsert **CreateMessage nesne** yeni bir ileti oluşturun ve toohello sırası eklemek için yöntem.

```
queueSvc.createMessage('myqueue', "Hello world!", function(error, result, response){
  if(!error){
    // Message inserted
  }
});
```

## <a name="how-to-peek-at-hello-next-message"></a>Nasıl yapılır: sonraki iletiyi hello Gözat
Bir sıra Merhaba öne hello iletiye tarafından arama hello hello kuyruktan kaldırmadan iletiye göz atabilirsiniz **peekMessages** yöntemi. Varsayılan olarak, **peekMessages** tek bir ileti iletiye göz atar.

```
queueSvc.peekMessages('myqueue', function(error, result, response){
  if(!error){
    // Message text is in messages[0].messageText
  }
});
```

Merhaba `result` selamlama iletisine içerir.

> [!NOTE]
> Kullanarak **peekMessages** hello sıraya ileti olduğunda ileti döndürdü ancak bir hata döndürmez.
> 
> 

## <a name="how-to-dequeue-hello-next-message"></a>Nasıl yapılır: hello sonraki iletiyi sıradan çıkarma
İleti işlenirken iki aşamalı bir işlemdir:

1. Selamlama iletisine dequeue.
2. Merhaba iletiyi silin.

toodequeue bir ileti kullanmak **getMessages**. Diğer bir istemcileri onları işleyebilmek için karışılama iletileri hello sırada görünmez kılar. Uygulamanızı bir ileti işlediğinde çağrısı **deleteMessage** toodelete onu hello sırasından. Aşağıdaki örneğine hello bir ileti alır, ardından da siler:

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
> Varsayılan olarak, bir ileti yalnızca 30 saniye boyunca geçmesi görünür tooother istemcileri olan gizlenir. Kullanarak farklı bir değer belirtebilirsiniz `options.visibilityTimeout` ile **getMessages**.
> 
> [!NOTE]
> Kullanarak **getMessages** hello sıraya ileti olduğunda ileti döndürdü ancak bir hata döndürmez.
> 
> 

## <a name="how-to-change-hello-contents-of-a-queued-message"></a>Nasıl yapılır: bir sıraya ileti hello içeriğini değiştirme
Bir ileti sırası hello kullanarak yerinde hello içeriğini değiştirebilirsiniz **updateMessage**. Aşağıdaki örneğine hello hello metin iletisinin güncelleştirir:

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

## <a name="how-to-additional-options-for-dequeuing-messages"></a>Nasıl yapılır: kuyruktan alma için ek seçenekler iletileri
Bir sıradan ileti alma özelleştirebilirsiniz iki yolu vardır:

* `options.numOfMessages`-Almak toplu iletiler (yukarı too32.)
* `options.visibilityTimeout`-Daha uzun veya kısaysa görünmezlik zaman aşımı ayarlayın.

Merhaba aşağıdaki örnek kullanır hello **getMessages** bir çağrı yöntemi tooget 15 iletileri. Her bir iletiyi kullanarak işler sonra bir döngü için. Ayrıca, bu yöntem tarafından döndürülen tüm iletiler için hello görünmezlik zaman aşımı toofive dakika ayarlar.

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

## <a name="how-to-get-hello-queue-length"></a>Nasıl yapılır: hello kuyruk uzunluğu alma
Merhaba **getQueueMetadata** hello yaklaşık hello kuyrukta ileti sayısı dahil olmak üzere hello kuyruk hakkındaki meta verileri döndürür.

```
queueSvc.getQueueMetadata('myqueue', function(error, result, response){
  if(!error){
    // Queue length is available in result.approximateMessageCount
  }
});
```

## <a name="how-to-list-queues"></a>Nasıl yapılır: Sorgular listesi
tooretrieve kuyrukların, kullanım listesini **listQueuesSegmented**. tooretrieve listesini filtre tarafından belirli bir önek, kullanın **listQueuesSegmentedWithPrefix**.

```
queueSvc.listQueuesSegmented(null, function(error, result, response){
  if(!error){
    // result.entries contains hello list of queues
  }
});
```

Tüm Kuyruklar döndürülemez, `result.continuationToken` öğesinin ilk parametresi, hello olarak kullanılan **listQueuesSegmented** veya ikinci parametresi, hello **listQueuesSegmentedWithPrefix** tooretrieve daha fazla sonuç.

## <a name="how-to-delete-a-queue"></a>Nasıl yapılır: bir kuyruk silme
toodelete bir sıra ve tüm karışılama iletileri bulunan içinde arama **deleteQueue** hello nesnesinde yöntemi.

```
queueSvc.deleteQueue(queueName, function(error, response){
  if(!error){
    // Queue has been deleted
  }
});
```

tüm iletileri silmeden, bir kuyruktan tooclear kullanan **clearMessages**.

## <a name="how-to-work-with-shared-access-signatures"></a>Nasıl yapılır: paylaşılan erişim imzaları ile çalışma
Paylaşılan erişim imzaları (SAS) depolama hesabı adı veya anahtarları sağlamadan güvenli şekilde tooprovide ayrıntılı erişim tooqueues ' dir. SAS toosubmit iletileri bir mobil uygulama izin verme gibi sınırlı kullanılan tooprovide tooyour sıralarına erişim, çoğunlukla olur.

Bir bulut tabanlı hizmeti gibi güvenilir bir uygulama hello kullanarak bir SAS oluşturur **generateSharedAccessSignature** Merhaba, **QueueService**, tooan sağlar ve güvenilmeyen veya yarı güvenilir uygulama. Örneğin, bir mobil uygulama. Hello SAS hello başlangıç tanımlayan bir ilke ve bitiş tarihleri sırasında hangi hello SAS geçerlidir kullanılarak oluşturulan, aynı zamanda erişim düzeyi verilen toohello SAS sahibi hello.

Aşağıdaki örnek hello hello SAS sahibi tooadd iletileri toohello sırası izin veren yeni bir paylaşılan erişim ilkesi oluşturur ve 100 dakika hello zaman oluşturulduktan sonra süresi dolar.

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

Gerekli olduğu gibi aynı zamanda, hello SAS sahibi tooaccess hello sıra çalıştığında sağlanan hello ana bilgisayar bilgilerini olması gerektiğini unutmayın.

ile SAS kullanır hello sonra istemci uygulaması Hello **QueueServiceWithSAS** hello sıra karşı tooperform işlemleri. Aşağıdaki örnek hello toohello sıra bağlanır ve bir ileti oluşturur.

```
var sharedQueueService = azure.createQueueServiceWithSas(host, queueSAS);
sharedQueueService.createMessage('myqueue', 'Hello world from SAS!', function(error, result, response){
  if(!error){
    //message added
  }
});
```

Update veya delete iletileri tooread girişiminde yapılmışsa hello SAS Ekle erişimle oluşturulmasının üzerinden, bir hata döndürülür.

### <a name="access-control-lists"></a>Erişim denetimi listeleri
Erişim denetimi listesi (ACL) tooset hello erişim ilkesi için bir SAS de kullanabilirsiniz. Birden çok istemcileri tooaccess hello sıra tooallow istiyor, ancak her istemci için farklı erişim ilkeleri sağlar, bu yararlı olur.

Bir ACL her ilkesiyle ilişkili bir Kimliğe sahip bir dizi erişim ilkeleri kullanılarak uygulanır. Aşağıdaki örnek hello iki ilke tanımlar; bir 'Kullanıcı1' ve 'kullanıcı2' için:

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

Aşağıdaki örnek alır hello hello geçerli ACL'si **Sıram**, hello yeni ilkeleri kullanılarak ekler **setQueueAcl**. Bu yaklaşım sağlar:

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

Bir kez hello ACL ayarlayın, hello Kimliği İlkesi için temel bir SAS sonra oluşturabilirsiniz. Aşağıdaki örnek hello 'kullanıcı2' için yeni bir SAS oluşturur:

```
queueSAS = queueSvc.generateSharedAccessSignature('myqueue', { Id: 'user2' });
```

## <a name="next-steps"></a>Sonraki Adımlar
Kuyruk depolamanın hello temel bilgileri öğrendiğinize göre bu bağlantıları toolearn daha karmaşık depolama görevleri hakkında izleyin.

* Merhaba [Azure depolama ekibi blogu] [Azure depolama ekibi blogu] ziyaret edin.
* Merhaba ziyaret [düğümü için Azure depolama SDK'sı] [ Azure Storage SDK for Node] github'daki.

[Azure Storage SDK for Node]: https://github.com/Azure/azure-storage-node
[using hello REST API]: http://msdn.microsoft.com/library/azure/hh264518.aspx
[Azure Portal]: https://portal.azure.com
[Azure App Service'te bir Node.js web uygulaması oluşturma](../../app-service-web/app-service-web-get-started-nodejs.md)   
[Hello Azure tablo hizmeti kullanarak Node.js web uygulaması](../../app-service-web/storage-nodejs-use-table-storage-web-site.md)
  


[Derleme ve bir Node.js uygulaması tooan Azure bulut hizmeti dağıtma](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md)   
[Azure depolama ekibi blogu]: http://blogs.msdn.com/b/windowsazurestorage/ [derleme ve Web Matrix kullanarak bir Node.js web uygulaması tooAzure dağıtma]: https://www.microsoft.com/web/webmatrix/   
