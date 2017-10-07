---
title: aaaHow toouse node.js'den Blob storage | Microsoft Docs
description: "Azure Blob storage (nesne depolama) ile Merhaba bulutta yapılandırılmamış veri depolayın."
services: storage
documentationcenter: nodejs
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 8b0df222-1ca8-4967-8248-6d6d720947b8
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: 572e7fc9f7b19ff01720a7cadd495c809ed49fb2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-nodejs"></a>Nasıl toouse node.js'den Blob storage
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-check-out-samples-all](../../../includes/storage-check-out-samples-all.md)]

## <a name="overview"></a>Genel Bakış
Bu makale size nasıl gösterir Blob storage kullanarak tooperform senaryoları. Merhaba örnekleri hello Node.js API yazılır. Kapsanan hello senaryolar nasıl tooupload, liste, indirin ve BLOB'ları silme içerir.

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-nodejs-application"></a>Node.js uygulaması oluşturma
Yönergeler için toocreate bir Node.js uygulaması bakın [oluşturma Azure App Service'te Node.js web uygulamasına] [derleme ve bir Node.js uygulaması tooan Azure bulut hizmeti dağıtma](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md) --Windows PowerShell kullanarak veya [yapı ve Web Matrix kullanarak bir Node.js web uygulaması tooAzure dağıtmak](https://www.microsoft.com/web/webmatrix/).

## <a name="configure-your-application-tooaccess-storage"></a>Uygulama tooaccess depolamayı yapılandırma
Azure depolama toouse hello storage REST Hizmetleri ile iletişim kuran bir dizi kolaylık içerir Node.js için hello Azure depolama SDK'sı gerekir.

### <a name="use-node-package-manager-npm-tooobtain-hello-package"></a>Düğüm paketi Yöneticisi (NPM) tooobtain hello paketini kullanın
1. Bir komut satırı arabirimini kullanın **PowerShell** (Windows), **Terminal** (Mac) veya **Bash** (UNIX) örneğinizi oluşturulduğu toonavigate toohello klasörü uygulama.
2. Tür **npm yükleme azure depolama** hello komut penceresinde. Merhaba komut çıktısı aşağıdaki kod örneğine benzer toohello ' dir.

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
3. Merhaba el ile çalıştırabilirsiniz **ls** komutu tooverify, bir **düğümü\_modülleri** klasörü oluşturuldu. Bu klasör içinde hello bulur **azure depolama** tooaccess depolama ihtiyacınız hello kitaplıklarını içeren paket.

### <a name="import-hello-package"></a>Merhaba paketi İçeri Aktar
Not Defteri'nde veya başka bir metin düzenleyicisi kullanarak eklemek hello toohello üstündeki aşağıdaki hello **server.js** toouse depolama burada düşündüğünüz dosya hello uygulamasının:

```nodejs
var azure = require('azure-storage');
```

## <a name="set-up-an-azure-storage-connection"></a>Bir Azure depolama bağlantı kurma
Hello Azure modülü hello ortam değişkenleri okur `AZURE_STORAGE_ACCOUNT` ve `AZURE_STORAGE_ACCESS_KEY`, veya `AZURE_STORAGE_CONNECTION_STRING`, tooconnect tooyour Azure depolama hesabı için bilgi gerekiyor. Bu ortam değişkenleri ayarlanmamışsa çağrılırken hello hesap bilgileri belirtmelisiniz **createBlobService**.

Hello hello ortam değişkenlerini ayarlama örneği için [Azure portal](https://portal.azure.com) Azure web uygulaması için bkz: [Node.js web app kullanarak hello Azure tablo hizmeti](../../app-service-web/storage-nodejs-use-table-storage-web-site.md).

## <a name="create-a-container"></a>Bir kapsayıcı oluşturma
Merhaba **BlobService** nesne kapsayıcıları ve blob'larla çalışmanıza olanak sağlar. Merhaba aşağıdaki kod oluşturur bir **BlobService** nesnesi. Merhaba üstündeki yakın Hello aşağıdakileri ekleyin **server.js**:

```nodejs
var blobSvc = azure.createBlobService();
```

> [!NOTE]
> Kullanarak bir blob anonim olarak erişebilir **createBlobServiceAnonymous** ve hello ana bilgisayar adresi sağlama. Örneğin, `var blobSvc = azure.createBlobServiceAnonymous('https://myblob.blob.core.windows.net/');`.
>
>

[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

Yeni bir kapsayıcı toocreate kullanmak **createContainerIfNotExists**. Merhaba aşağıdaki kod örneğinde 'mycontainer' adlı yeni bir kapsayıcı oluşturur:

```nodejs
blobSvc.createContainerIfNotExists('mycontainer', function(error, result, response){
    if(!error){
      // Container exists and is private
    }
});
```

Merhaba kapsayıcı yeni oluşturduysanız, `result.created` doğrudur. Merhaba kapsayıcısı zaten varsa, `result.created` false olur. `response`Merhaba kapsayıcısı için hello ETag bilgiler dahil olmak üzere hello işlemiyle ilgili bilgi içerir.

### <a name="container-security"></a>Kapsayıcı güvenlik
Varsayılan olarak yeni kapsayıcı özeldir ve anonim olarak erişilemez. Böylece anonim olarak erişebilir ortak toomake hello kapsayıcı, ayarlayabileceğiniz hello kapsayıcısının erişim düzeyi çok**blob** veya **kapsayıcı**.

* **BLOB** -anonim okuma erişimini tooblob içerik ve bu kapsayıcı içindeki meta verileri, ancak bir kapsayıcıdaki tüm blob'lara listeleme gibi değil toocontainer meta verileri sağlar
* **kapsayıcı** -kapsayıcı meta verileri yanı sıra anonim okuma erişimini tooblob içerik ve meta verileri sağlar

Merhaba aşağıdaki kod örneğinde ayarı hello erişim düzeyi çok gösterilmektedir**blob**:

```nodejs
blobSvc.createContainerIfNotExists('mycontainer', {publicAccessLevel : 'blob'}, function(error, result, response){
    if(!error){
      // Container exists and allows
      // anonymous read access tooblob
      // content and metadata within this container
    }
});
```

Alternatif olarak, bir kapsayıcı hello erişim düzeyi kullanarak değiştirebileceğiniz **setContainerAcl** toospecify hello erişim düzeyi. Merhaba aşağıdaki örnek değişiklikleri hello erişim düzeyi toocontainer kod:

```nodejs
blobSvc.setContainerAcl('mycontainer', null /* signedIdentifiers */, {publicAccessLevel : 'container'} /* publicAccessLevel*/, function(error, result, response){
  if(!error){
    // Container access level set too'container'
  }
});
```

Merhaba sonucunu içerir hello geçerli dahil olmak üzere hello işlemiyle ilgili bilgi **ETag** hello kapsayıcısı için.

### <a name="filters"></a>Filtreler
İsteğe bağlı filtreleme işlemleri gerçekleştirilen toooperations kullanarak uygulayabilirsiniz **BlobService**. İşlemleri filtreleme içerebilir günlüğe kaydetme, otomatik olarak yeniden deneniyor, vs. Filtreleri hello imza yöntemiyle uygulayan nesneler şunlardır:

```nodejs
function handle (requestOptions, next)
```

Kendi hello isteği seçenekleri ön işleme yaptıktan sonra hello yöntemi toocall "İleri", bir geri çağırma imza aşağıdaki hello ile geçirme gerekir:

```nodejs
function (returnObject, finalCallback, next)
```

Bu geri çağırma ve hello returnObject (Merhaba isteği toohello sunucusundan hello yanıt) işlemden sonra hello geri çağırma tooeither gereken diğer filtreleri işleme toocontinue varsa sonraki çağırma veya yalnızca finalCallback tooend hello hizmeti çağırma çağırma.

Yeniden deneme mantığını uygulaması iki filtre hello Node.js için Azure SDK ile birlikte **ExponentialRetryPolicyFilter** ve **LinearRetryPolicyFilter**. Merhaba aşağıdaki oluşturur bir **BlobService** hello kullanan nesneyi **ExponentialRetryPolicyFilter**:

```nodejs
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var blobSvc = azure.createBlobService().withFilter(retryOperations);
```

## <a name="upload-a-blob-into-a-container"></a>Bir kapsayıcıya bir blob yükleme
Üç BLOB türü vardır: blok blobları, sayfa blobları ve ilave blobları. Blok blobları izin toomore verimli bir şekilde büyük veri karşıya yükleyin. Ekleme blobları için iyileştirilmiş ekleme işlemleri. Sayfa bloblarını okuma/yazma işlemleri için en iyi duruma getirilir. Daha fazla bilgi için bkz: [anlama blok Blobları, ekleme Blobları ve sayfa Bloblarını](http://msdn.microsoft.com/library/azure/ee691964.aspx).

### <a name="block-blobs"></a>Blok blobları
tooupload veri tooa blok blobu, aşağıdaki kullanım hello:

* **createBlockBlobFromLocalFile** - yeni bir blok blobu oluşturur ve bir dosyanın içeriğini hello yükler
* **createBlockBlobFromStream** - yeni bir blok blobu oluşturur ve bir akış Merhaba içeriğine yükler
* **createBlockBlobFromText** - yeni bir blok blobu oluşturur ve bir dize Merhaba içeriğine yükler
* **createWriteStreamToBlockBlob** -yazma akışı tooa blok blobu sağlar

Merhaba aşağıdaki kod örneğinde yükleyen hello Merhaba içeriğine **sınama.txt** içine dosya **myblob**.

```nodejs
blobSvc.createBlockBlobFromLocalFile('mycontainer', 'myblob', 'test.txt', function(error, result, response){
  if(!error){
    // file uploaded
  }
});
```

Merhaba `result` bu yöntemler tarafından döndürülen hello gibi hello işlemi hakkında bilgi içeren **ETag** hello BLOB.

### <a name="append-blobs"></a>Ekleme blobları
tooupload veri tooa yeni blob ekleme, hello aşağıdakileri kullanın:

* **createAppendBlobFromLocalFile** - yeni bir ek blob oluşturur ve bir dosyanın içeriğini hello yükler
* **createAppendBlobFromStream** - yeni bir ek blob oluşturur ve bir akış Merhaba içeriğine yükler
* **createAppendBlobFromText** - yeni bir ek blob oluşturur ve bir dize Merhaba içeriğine yükler
* **createWriteStreamToNewAppendBlob** - yeni bir ek blob oluşturur ve ardından bir akış toowrite tooit sağlar

Merhaba aşağıdaki kod örneğinde yükleyen hello Merhaba içeriğine **sınama.txt** içine dosya **myappendblob**.

```nodejs
blobSvc.createAppendBlobFromLocalFile('mycontainer', 'myappendblob', 'test.txt', function(error, result, response){
  if(!error){
    // file uploaded
  }
});
```

tooappend blok varolan tooan blob, aşağıdaki kullanım hello ekleyin:

* **appendFromLocalFile** -hello içeriği ekleme dosya tooan blob append var
* **appendFromStream** -hello içeriği append akış tooan varolan blob ekleme
* **appendFromText** -hello içeriği ekleme dize tooan blob append var
* **appendBlockFromStream** -hello içeriği append akış tooan varolan blob ekleme
* **appendBlockFromText** -hello içeriği ekleme dize tooan blob append var

> [!NOTE]
> bazı istemci tarafı doğrulama toofail hızlı tooavoid gereksiz sunucu çağrılarını appendFromXXX API'leri yapın. appendBlockFromXXX olmaz.
>
>

Merhaba aşağıdaki kod örneğinde yükleyen hello Merhaba içeriğine **sınama.txt** içine dosya **myappendblob**.

```nodejs
blobSvc.appendFromText('mycontainer', 'myappendblob', 'text toobe appended', function(error, result, response){
  if(!error){
    // text appended
  }
});
```

### <a name="page-blobs"></a>Sayfa blobları
tooupload veri tooa sayfa blobu, aşağıdaki kullanım hello:

* **createPageBlob** -belirli bir uzunlukta yeni bir sayfa blob'u oluşturur
* **createPageBlobFromLocalFile** - yeni bir sayfa blob'u oluşturur ve bir dosyanın içeriğini hello yükler
* **createPageBlobFromStream** - yeni bir sayfa blob'u oluşturur ve bir akış Merhaba içeriğine yükler
* **createWriteStreamToExistingPageBlob** -yazma akışı tooan varolan sayfa blobu sağlar
* **createWriteStreamToNewPageBlob** - yeni bir sayfa blob'u oluşturur ve ardından bir akış toowrite tooit sağlar

Merhaba aşağıdaki kod örneğinde yükleyen hello Merhaba içeriğine **sınama.txt** içine dosya **mypageblob**.

```nodejs
blobSvc.createPageBlobFromLocalFile('mycontainer', 'mypageblob', 'test.txt', function(error, result, response){
  if(!error){
    // file uploaded
  }
});
```

> [!NOTE]
> Sayfa bloblarını 512 bayt 'sayfalar' oluşur. 512 birden fazla olmayan bir boyutu ile verileri karşıya yüklenirken bir hata alırsınız.
>
>

## <a name="list-hello-blobs-in-a-container"></a>Liste hello BLOB'ları bir kapsayıcıda
toolist hello BLOB'ları bir kapsayıcıda kullanmak hello **listBlobsSegmented** yöntemi. Belirli bir önek ile tooreturn BLOB'lar istiyorsanız kullanın **listBlobsSegmentedWithPrefix**.

```nodejs
blobSvc.listBlobsSegmented('mycontainer', null, function(error, result, response){
  if(!error){
      // result.entries contains hello entries
      // If not all blobs were returned, result.continuationToken has hello continuation token.
  }
});
```

Merhaba `result` içeren bir `entries` her bir blob açıklayan nesnelerinin bir dizisidir koleksiyonu. Tüm BLOB'lar döndürülemez, hello `result` de sağlar bir `continuationToken`, hangi hello ikinci parametre tooretrieve ek girişleri olarak kullanabilir.

## <a name="download-blobs"></a>Blob’ları indirme
bir blob toodownload verilerden hello aşağıdakileri kullanın:

* **getBlobToLocalFile** -hello blob içeriği toofile Yazar
* **getBlobToStream** -hello blob içeriği tooa akışa Yazar
* **getBlobToText** -tooa dize hello blob içeriklerini Yazar
* **createReadStream** -hello blob gelen bir akış tooread sağlar

Merhaba aşağıdaki kod örneğinde kullanarak gösterilmektedir **getBlobToStream** toodownload Merhaba içeriğine hello **myblob** toohello depolamak ve blob **çýktý.txt** kullanarak dosya bir Akış:

```nodejs
var fs = require('fs');
blobSvc.getBlobToStream('mycontainer', 'myblob', fs.createWriteStream('output.txt'), function(error, result, response){
  if(!error){
    // blob retrieved
  }
});
```

Merhaba `result` hello blob hakkında bilgi içeren dahil olmak üzere **ETag** bilgi.

## <a name="delete-a-blob"></a>Blob silme
Son olarak, bir blob toodelete çağrısı **deleteBlob**. Aşağıdaki kod örneğine siler hello adlı blob hello **myblob**.

```nodejs
blobSvc.deleteBlob(containerName, 'myblob', function(error, response){
  if(!error){
    // Blob has been deleted
  }
});
```

## <a name="concurrent-access"></a>Eş zamanlı erişim
kullanabileceğiniz toosupport eş zamanlı erişim tooa blob birden çok istemciden veya birden çok örneği **Etag'ler** veya **kiraları**.

* **ETag** -blob veya kapsayıcı hello bir şekilde toodetect başka bir işlem tarafından değiştirilmiş sağlar
* **Kira** - yolu tooobtain özel ve yenilenebilir, yazma sağlar veya bir süre için erişim tooa blob Sil

### <a name="etag"></a>ETag
Birden çok istemciler veya örnekleri toowrite toohello blok blobu veya sayfa Blob aynı anda tooallow gerekirse Etag'ler kullanın. Başlangıçta okumak veya başka bir istemci ya da işlem tarafından kaydedilen değişikliklerin üzerine tooavoid sağlayan, oluşturulan beri hello kapsayıcı veya blob değiştirilmişse hello ETag toodetermine sağlar.

İsteğe bağlı hello kullanarak ETag koşulları ayarlayabilirsiniz `options.accessConditions` parametresi. Merhaba aşağıdaki kod örneği yalnızca hello yükler **sınama.txt** hello blob zaten varsa ve hello ETag değerine sahip dosyasında alan tarafından `etagToMatch`.

```nodejs
blobSvc.createBlockBlobFromLocalFile('mycontainer', 'myblob', 'test.txt', { accessConditions: { EtagMatch: etagToMatch} }, function(error, result, response){
    if(!error){
    // file uploaded
  }
});
```

Etag'ler kullanırken hello genel modeli aşağıdaki gibidir:

1. Merhaba ETag oluşturma, liste veya alma işlemi hello sonucu olarak alın.
2. Bir eylem gerçekleştirmek, o hello ETag değeri denetleme değiştirilmedi.

Merhaba değeri değiştirilmişse, bu hello ETag değeri elde olduğundan başka bir istemci veya örnek hello blob veya kapsayıcı değiştirildiğini gösterir.

### <a name="lease"></a>Kira
Hello kullanarak yeni bir kira elde edebilirsiniz **acquireLease** yöntemi, üzerinde bir kira tooobtain istediğiniz hello blob veya kapsayıcı belirtme. Örneğin, kod aşağıdaki hello üzerinde bir kira alması **myblob**.

```nodejs
blobSvc.acquireLease('mycontainer', 'myblob', function(error, result, response){
  if(!error) {
    console.log('leaseId: ' + result.id);
  }
});
```

Sonraki işlemlerde **myblob** hello sağlamalısınız `options.leaseId` parametresi. Kimliği olarak döndürülür hello kira `result.id` gelen **acquireLease**.

> [!NOTE]
> Varsayılan olarak, hello kira süresi sonsuzdur. Merhaba sağlayarak (arasındaki 15 ila 60 saniye) sonsuz olmayan süre belirtebilirsiniz `options.leaseDuration` parametresi.
>
>

tooremove bir kira kullanmak **releaseLease**. toobreak bir kira ancak önlemek başkalarının hello özgün süresi sona erinceye kadar yeni bir kira elde etmesini kullanmak **breakLease**.

## <a name="work-with-shared-access-signatures"></a>Paylaşılan erişim imzaları ile çalışma
Paylaşılan erişim imzaları (SAS), güvenli şekilde tooprovide ayrıntılı erişim tooblobs ve depolama hesabı adı veya anahtarları sağlamadan kapsayıcıları ' dir. Paylaşılan erişim imzaları genellikle bir mobil uygulama tooaccess BLOB'lar izin verme gibi sınırlı kullanılan tooprovide erişim tooyour, verilerdir.

> [!NOTE]
> Anonim erişim tooblobs izin verebilir, ancak hello SAS oluşturmalıdır paylaşılan erişim imzaları daha kontrol tooprovide erişim olanak sağlar.
>
>

Paylaşılan erişim imzaları hello kullanarak bulut tabanlı bir hizmete gibi güvenilir bir uygulama oluşturur **generateSharedAccessSignature** Merhaba, **BlobService**, sağlar ve güvenilmeyen tooan veya Yarı güvenilir uygulama mobil uygulama gibi. Paylaşılan erişim imzaları hello başlangıç açıklayan bir ilkeyi kullanarak oluşturulan ve bitiş tarihleri sırasında hangi hello paylaşılan erişim imzaları geçerli yanı sıra, hello düzeyi verilen toohello paylaşılan erişim imzaları sahibi erişin.

Merhaba aşağıdaki kod örneği oluşturur hello paylaşılan erişim imzaları sahibi tooperform okuma işlemleri hello izin veren yeni bir paylaşılan erişim ilkesi **myblob** blob ve 100 dakika oluşturulan hello sonra süresi dolar.

```nodejs
var startDate = new Date();
var expiryDate = new Date(startDate);
expiryDate.setMinutes(startDate.getMinutes() + 100);
startDate.setMinutes(startDate.getMinutes() - 100);

var sharedAccessPolicy = {
  AccessPolicy: {
    Permissions: azure.BlobUtilities.SharedAccessPermissions.READ,
    Start: startDate,
    Expiry: expiryDate
  },
};

var blobSAS = blobSvc.generateSharedAccessSignature('mycontainer', 'myblob', sharedAccessPolicy);
var host = blobSvc.host;
```

Gerekli olduğu gibi aynı zamanda, hello paylaşılan erişim imzaları sahibi tooaccess hello kapsayıcı çalıştığında sağlanan hello ana bilgisayar bilgilerini olması gerektiğini unutmayın.

Merhaba sonra istemci uygulamanın kullandığı paylaşılan erişim imzaları ile **BlobServiceWithSAS** hello blob karşı tooperform işlemleri. Merhaba aşağıdaki bilgileri alır **myblob**.

```nodejs
var sharedBlobSvc = azure.createBlobServiceWithSas(host, blobSAS);
sharedBlobSvc.getBlobProperties('mycontainer', 'myblob', function (error, result, response) {
  if(!error) {
    // retrieved info
  }
});
```

Toomodify hello blob denemesi yapılırsa, salt okunur erişim ile Merhaba paylaşılan erişim imzaları oluşturulduktan sonra bir hata döndürülür.

### <a name="access-control-lists"></a>Erişim denetimi listeleri
Bir erişim denetimi listesi (ACL) tooset hello erişim ilkesi için SAS de kullanabilirsiniz. Birden çok istemcileri tooaccess bir kapsayıcı tooallow istiyor, ancak her istemci için farklı erişim ilkeleri sağlar, bu yararlı olur.

Bir ACL her ilkesiyle ilişkili bir Kimliğe sahip bir dizi erişim ilkeleri kullanılarak uygulanır. Aşağıdaki kod örneğine hello iki ilke, 'User1' diğeri için 'kullanıcı2' tanımlar:

```nodejs
var sharedAccessPolicy = {
  user1: {
    Permissions: azure.BlobUtilities.SharedAccessPermissions.READ,
    Start: startDate,
    Expiry: expiryDate
  },
  user2: {
    Permissions: azure.BlobUtilities.SharedAccessPermissions.WRITE,
    Start: startDate,
    Expiry: expiryDate
  }
};
```

Aşağıdaki kod örneği alır hello hello geçerli ACL'si **mycontainer**ve ardından hello yeni ilkeleri kullanılarak ekler **setBlobAcl**. Bu yaklaşım sağlar:

```nodejs
var extend = require('extend');
blobSvc.getBlobAcl('mycontainer', function(error, result, response) {
  if(!error){
    var newSignedIdentifiers = extend(true, result.signedIdentifiers, sharedAccessPolicy);
    blobSvc.setBlobAcl('mycontainer', newSignedIdentifiers, function(error, result, response){
      if(!error){
        // ACL set
      }
    });
  }
});
```

Bir kez hello ACL ayarlayın, bir ilke hello kimliği temel paylaşılan erişim imzaları sonra oluşturabilirsiniz. Aşağıdaki kod örneğine hello 'kullanıcı2' yeni paylaşılan erişim imzaları oluşturur:

```nodejs
blobSAS = blobSvc.generateSharedAccessSignature('mycontainer', { Id: 'user2' });
```

## <a name="next-steps"></a>Sonraki adımlar
Daha fazla bilgi için kaynakları aşağıdaki hello bakın.

* [Azure Depolama düğümü API Başvurusu için SDK] [Azure Depolama düğümü API Başvurusu için SDK]
* [Azure depolama ekibi blogu] [Azure depolama ekibi blogu]
* [Azure depolama SDK'sı düğüm için] [ Azure Storage SDK for Node] github'daki
* [Node.js Geliştirici Merkezi](https://azure.microsoft.com/develop/nodejs/)
* [Merhaba AzCopy komut satırı yardımcı programı ile veri aktarımı](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)

[Azure Storage SDK for Node]: https://github.com/Azure/azure-storage-node

[Hello Azure tablo hizmeti kullanarak Node.js web uygulaması](../../app-service-web/storage-nodejs-use-table-storage-web-site.md)    
[Derleme ve Web Matrix kullanarak bir Node.js web uygulaması tooAzure dağıtma]: https://www.microsoft.com/web/webmatrix/  
[REST API hello kullanarak]: [Azure portalı] http://msdn.microsoft.com/library/azure/hh264518.aspx: https://portal.azure.com [derleme ve bir Node.js uygulaması tooan Azure bulut hizmeti dağıtma](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md) [Azure depolama ekibi blogu]: http:// blogs.msdn.com/b/windowsazurestorage/ [Azure Depolama düğümü API Başvurusu için SDK]: http://dl.windowsazure.com/nodestoragedocs/index.html
