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
# <a name="how-toouse-blob-storage-from-nodejs"></a><span data-ttu-id="3cb0a-103">Nasıl toouse node.js'den Blob storage</span><span class="sxs-lookup"><span data-stu-id="3cb0a-103">How toouse Blob storage from Node.js</span></span>
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-check-out-samples-all](../../../includes/storage-check-out-samples-all.md)]

## <a name="overview"></a><span data-ttu-id="3cb0a-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="3cb0a-104">Overview</span></span>
<span data-ttu-id="3cb0a-105">Bu makale size nasıl gösterir Blob storage kullanarak tooperform senaryoları.</span><span class="sxs-lookup"><span data-stu-id="3cb0a-105">This article shows you how tooperform common scenarios using Blob storage.</span></span> <span data-ttu-id="3cb0a-106">Merhaba örnekleri hello Node.js API yazılır.</span><span class="sxs-lookup"><span data-stu-id="3cb0a-106">hello samples are written via hello Node.js API.</span></span> <span data-ttu-id="3cb0a-107">Kapsanan hello senaryolar nasıl tooupload, liste, indirin ve BLOB'ları silme içerir.</span><span class="sxs-lookup"><span data-stu-id="3cb0a-107">hello scenarios covered include how tooupload, list, download, and delete blobs.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-nodejs-application"></a><span data-ttu-id="3cb0a-108">Node.js uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="3cb0a-108">Create a Node.js application</span></span>
<span data-ttu-id="3cb0a-109">Yönergeler için toocreate bir Node.js uygulaması bakın [oluşturma Azure App Service'te Node.js web uygulamasına] [derleme ve bir Node.js uygulaması tooan Azure bulut hizmeti dağıtma](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md) --Windows PowerShell kullanarak veya [yapı ve Web Matrix kullanarak bir Node.js web uygulaması tooAzure dağıtmak](https://www.microsoft.com/web/webmatrix/).</span><span class="sxs-lookup"><span data-stu-id="3cb0a-109">For instructions on how toocreate a Node.js application, see [Create a Node.js web app in Azure App Service], [Build and deploy a Node.js application tooan Azure Cloud Service](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md) -- using Windows PowerShell, or [Build and deploy a Node.js web app tooAzure using Web Matrix](https://www.microsoft.com/web/webmatrix/).</span></span>

## <a name="configure-your-application-tooaccess-storage"></a><span data-ttu-id="3cb0a-110">Uygulama tooaccess depolamayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="3cb0a-110">Configure your application tooaccess storage</span></span>
<span data-ttu-id="3cb0a-111">Azure depolama toouse hello storage REST Hizmetleri ile iletişim kuran bir dizi kolaylık içerir Node.js için hello Azure depolama SDK'sı gerekir.</span><span class="sxs-lookup"><span data-stu-id="3cb0a-111">toouse Azure storage, you need hello Azure Storage SDK for Node.js, which includes a set of convenience libraries that communicate with hello storage REST services.</span></span>

### <a name="use-node-package-manager-npm-tooobtain-hello-package"></a><span data-ttu-id="3cb0a-112">Düğüm paketi Yöneticisi (NPM) tooobtain hello paketini kullanın</span><span class="sxs-lookup"><span data-stu-id="3cb0a-112">Use Node Package Manager (NPM) tooobtain hello package</span></span>
1. <span data-ttu-id="3cb0a-113">Bir komut satırı arabirimini kullanın **PowerShell** (Windows), **Terminal** (Mac) veya **Bash** (UNIX) örneğinizi oluşturulduğu toonavigate toohello klasörü uygulama.</span><span class="sxs-lookup"><span data-stu-id="3cb0a-113">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix), toonavigate toohello folder where you created your sample application.</span></span>
2. <span data-ttu-id="3cb0a-114">Tür **npm yükleme azure depolama** hello komut penceresinde.</span><span class="sxs-lookup"><span data-stu-id="3cb0a-114">Type **npm install azure-storage** in hello command window.</span></span> <span data-ttu-id="3cb0a-115">Merhaba komut çıktısı aşağıdaki kod örneğine benzer toohello ' dir.</span><span class="sxs-lookup"><span data-stu-id="3cb0a-115">Output from hello command is similar toohello following code example.</span></span>

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
3. <span data-ttu-id="3cb0a-116">Merhaba el ile çalıştırabilirsiniz **ls** komutu tooverify, bir **düğümü\_modülleri** klasörü oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="3cb0a-116">You can manually run hello **ls** command tooverify that a **node\_modules** folder was created.</span></span> <span data-ttu-id="3cb0a-117">Bu klasör içinde hello bulur **azure depolama** tooaccess depolama ihtiyacınız hello kitaplıklarını içeren paket.</span><span class="sxs-lookup"><span data-stu-id="3cb0a-117">Inside that folder, find hello **azure-storage** package, which contains hello libraries that you need tooaccess storage.</span></span>

### <a name="import-hello-package"></a><span data-ttu-id="3cb0a-118">Merhaba paketi İçeri Aktar</span><span class="sxs-lookup"><span data-stu-id="3cb0a-118">Import hello package</span></span>
<span data-ttu-id="3cb0a-119">Not Defteri'nde veya başka bir metin düzenleyicisi kullanarak eklemek hello toohello üstündeki aşağıdaki hello **server.js** toouse depolama burada düşündüğünüz dosya hello uygulamasının:</span><span class="sxs-lookup"><span data-stu-id="3cb0a-119">Using Notepad or another text editor, add hello following toohello top of hello **server.js** file of hello application where you intend toouse storage:</span></span>

```nodejs
var azure = require('azure-storage');
```

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="3cb0a-120">Bir Azure depolama bağlantı kurma</span><span class="sxs-lookup"><span data-stu-id="3cb0a-120">Set up an Azure Storage connection</span></span>
<span data-ttu-id="3cb0a-121">Hello Azure modülü hello ortam değişkenleri okur `AZURE_STORAGE_ACCOUNT` ve `AZURE_STORAGE_ACCESS_KEY`, veya `AZURE_STORAGE_CONNECTION_STRING`, tooconnect tooyour Azure depolama hesabı için bilgi gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="3cb0a-121">hello Azure module will read hello environment variables `AZURE_STORAGE_ACCOUNT` and `AZURE_STORAGE_ACCESS_KEY`, or `AZURE_STORAGE_CONNECTION_STRING`, for information required tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="3cb0a-122">Bu ortam değişkenleri ayarlanmamışsa çağrılırken hello hesap bilgileri belirtmelisiniz **createBlobService**.</span><span class="sxs-lookup"><span data-stu-id="3cb0a-122">If these environment variables are not set, you must specify hello account information when calling **createBlobService**.</span></span>

<span data-ttu-id="3cb0a-123">Hello hello ortam değişkenlerini ayarlama örneği için [Azure portal](https://portal.azure.com) Azure web uygulaması için bkz: [Node.js web app kullanarak hello Azure tablo hizmeti](../../app-service-web/storage-nodejs-use-table-storage-web-site.md).</span><span class="sxs-lookup"><span data-stu-id="3cb0a-123">For an example of setting hello environment variables in hello [Azure portal](https://portal.azure.com) for an Azure web app, see [Node.js web app using hello Azure Table Service](../../app-service-web/storage-nodejs-use-table-storage-web-site.md).</span></span>

## <a name="create-a-container"></a><span data-ttu-id="3cb0a-124">Bir kapsayıcı oluşturma</span><span class="sxs-lookup"><span data-stu-id="3cb0a-124">Create a container</span></span>
<span data-ttu-id="3cb0a-125">Merhaba **BlobService** nesne kapsayıcıları ve blob'larla çalışmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="3cb0a-125">hello **BlobService** object lets you work with containers and blobs.</span></span> <span data-ttu-id="3cb0a-126">Merhaba aşağıdaki kod oluşturur bir **BlobService** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="3cb0a-126">hello following code creates a **BlobService** object.</span></span> <span data-ttu-id="3cb0a-127">Merhaba üstündeki yakın Hello aşağıdakileri ekleyin **server.js**:</span><span class="sxs-lookup"><span data-stu-id="3cb0a-127">Add hello following near hello top of **server.js**:</span></span>

```nodejs
var blobSvc = azure.createBlobService();
```

> [!NOTE]
> <span data-ttu-id="3cb0a-128">Kullanarak bir blob anonim olarak erişebilir **createBlobServiceAnonymous** ve hello ana bilgisayar adresi sağlama.</span><span class="sxs-lookup"><span data-stu-id="3cb0a-128">You can access a blob anonymously by using **createBlobServiceAnonymous** and providing hello host address.</span></span> <span data-ttu-id="3cb0a-129">Örneğin, `var blobSvc = azure.createBlobServiceAnonymous('https://myblob.blob.core.windows.net/');`.</span><span class="sxs-lookup"><span data-stu-id="3cb0a-129">For example, use `var blobSvc = azure.createBlobServiceAnonymous('https://myblob.blob.core.windows.net/');`.</span></span>
>
>

[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="3cb0a-130">Yeni bir kapsayıcı toocreate kullanmak **createContainerIfNotExists**.</span><span class="sxs-lookup"><span data-stu-id="3cb0a-130">toocreate a new container, use **createContainerIfNotExists**.</span></span> <span data-ttu-id="3cb0a-131">Merhaba aşağıdaki kod örneğinde 'mycontainer' adlı yeni bir kapsayıcı oluşturur:</span><span class="sxs-lookup"><span data-stu-id="3cb0a-131">hello following code example creates a new container named 'mycontainer':</span></span>

```nodejs
blobSvc.createContainerIfNotExists('mycontainer', function(error, result, response){
    if(!error){
      // Container exists and is private
    }
});
```

<span data-ttu-id="3cb0a-132">Merhaba kapsayıcı yeni oluşturduysanız, `result.created` doğrudur.</span><span class="sxs-lookup"><span data-stu-id="3cb0a-132">If hello container is newly created, `result.created` is true.</span></span> <span data-ttu-id="3cb0a-133">Merhaba kapsayıcısı zaten varsa, `result.created` false olur.</span><span class="sxs-lookup"><span data-stu-id="3cb0a-133">If hello container already exists, `result.created` is false.</span></span> <span data-ttu-id="3cb0a-134">`response`Merhaba kapsayıcısı için hello ETag bilgiler dahil olmak üzere hello işlemiyle ilgili bilgi içerir.</span><span class="sxs-lookup"><span data-stu-id="3cb0a-134">`response` contains information about hello operation, including hello ETag information for hello container.</span></span>

### <a name="container-security"></a><span data-ttu-id="3cb0a-135">Kapsayıcı güvenlik</span><span class="sxs-lookup"><span data-stu-id="3cb0a-135">Container security</span></span>
<span data-ttu-id="3cb0a-136">Varsayılan olarak yeni kapsayıcı özeldir ve anonim olarak erişilemez.</span><span class="sxs-lookup"><span data-stu-id="3cb0a-136">By default, new containers are private and cannot be accessed anonymously.</span></span> <span data-ttu-id="3cb0a-137">Böylece anonim olarak erişebilir ortak toomake hello kapsayıcı, ayarlayabileceğiniz hello kapsayıcısının erişim düzeyi çok**blob** veya **kapsayıcı**.</span><span class="sxs-lookup"><span data-stu-id="3cb0a-137">toomake hello container public so that you can access it anonymously, you can set hello container's access level too**blob** or **container**.</span></span>

* <span data-ttu-id="3cb0a-138">**BLOB** -anonim okuma erişimini tooblob içerik ve bu kapsayıcı içindeki meta verileri, ancak bir kapsayıcıdaki tüm blob'lara listeleme gibi değil toocontainer meta verileri sağlar</span><span class="sxs-lookup"><span data-stu-id="3cb0a-138">**blob** - allows anonymous read access tooblob content and metadata within this container, but not toocontainer metadata such as listing all blobs within a container</span></span>
* <span data-ttu-id="3cb0a-139">**kapsayıcı** -kapsayıcı meta verileri yanı sıra anonim okuma erişimini tooblob içerik ve meta verileri sağlar</span><span class="sxs-lookup"><span data-stu-id="3cb0a-139">**container** - allows anonymous read access tooblob content and metadata as well as container metadata</span></span>

<span data-ttu-id="3cb0a-140">Merhaba aşağıdaki kod örneğinde ayarı hello erişim düzeyi çok gösterilmektedir**blob**:</span><span class="sxs-lookup"><span data-stu-id="3cb0a-140">hello following code example demonstrates setting hello access level too**blob**:</span></span>

```nodejs
blobSvc.createContainerIfNotExists('mycontainer', {publicAccessLevel : 'blob'}, function(error, result, response){
    if(!error){
      // Container exists and allows
      // anonymous read access tooblob
      // content and metadata within this container
    }
});
```

<span data-ttu-id="3cb0a-141">Alternatif olarak, bir kapsayıcı hello erişim düzeyi kullanarak değiştirebileceğiniz **setContainerAcl** toospecify hello erişim düzeyi.</span><span class="sxs-lookup"><span data-stu-id="3cb0a-141">Alternatively, you can modify hello access level of a container by using **setContainerAcl** toospecify hello access level.</span></span> <span data-ttu-id="3cb0a-142">Merhaba aşağıdaki örnek değişiklikleri hello erişim düzeyi toocontainer kod:</span><span class="sxs-lookup"><span data-stu-id="3cb0a-142">hello following code example changes hello access level toocontainer:</span></span>

```nodejs
blobSvc.setContainerAcl('mycontainer', null /* signedIdentifiers */, {publicAccessLevel : 'container'} /* publicAccessLevel*/, function(error, result, response){
  if(!error){
    // Container access level set too'container'
  }
});
```

<span data-ttu-id="3cb0a-143">Merhaba sonucunu içerir hello geçerli dahil olmak üzere hello işlemiyle ilgili bilgi **ETag** hello kapsayıcısı için.</span><span class="sxs-lookup"><span data-stu-id="3cb0a-143">hello result contains information about hello operation, including hello current **ETag** for hello container.</span></span>

### <a name="filters"></a><span data-ttu-id="3cb0a-144">Filtreler</span><span class="sxs-lookup"><span data-stu-id="3cb0a-144">Filters</span></span>
<span data-ttu-id="3cb0a-145">İsteğe bağlı filtreleme işlemleri gerçekleştirilen toooperations kullanarak uygulayabilirsiniz **BlobService**.</span><span class="sxs-lookup"><span data-stu-id="3cb0a-145">You can apply optional filtering operations toooperations performed using **BlobService**.</span></span> <span data-ttu-id="3cb0a-146">İşlemleri filtreleme içerebilir günlüğe kaydetme, otomatik olarak yeniden deneniyor, vs. Filtreleri hello imza yöntemiyle uygulayan nesneler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="3cb0a-146">Filtering operations can include logging, automatically retrying, etc. Filters are objects that implement a method with hello signature:</span></span>

```nodejs
function handle (requestOptions, next)
```

<span data-ttu-id="3cb0a-147">Kendi hello isteği seçenekleri ön işleme yaptıktan sonra hello yöntemi toocall "İleri", bir geri çağırma imza aşağıdaki hello ile geçirme gerekir:</span><span class="sxs-lookup"><span data-stu-id="3cb0a-147">After doing its preprocessing on hello request options, hello method needs toocall "next", passing a callback with hello following signature:</span></span>

```nodejs
function (returnObject, finalCallback, next)
```

<span data-ttu-id="3cb0a-148">Bu geri çağırma ve hello returnObject (Merhaba isteği toohello sunucusundan hello yanıt) işlemden sonra hello geri çağırma tooeither gereken diğer filtreleri işleme toocontinue varsa sonraki çağırma veya yalnızca finalCallback tooend hello hizmeti çağırma çağırma.</span><span class="sxs-lookup"><span data-stu-id="3cb0a-148">In this callback, and after processing hello returnObject (hello response from hello request toohello server), hello callback needs tooeither invoke next if it exists toocontinue processing other filters or simply invoke finalCallback tooend hello service invocation.</span></span>

<span data-ttu-id="3cb0a-149">Yeniden deneme mantığını uygulaması iki filtre hello Node.js için Azure SDK ile birlikte **ExponentialRetryPolicyFilter** ve **LinearRetryPolicyFilter**.</span><span class="sxs-lookup"><span data-stu-id="3cb0a-149">Two filters that implement retry logic are included with hello Azure SDK for Node.js, **ExponentialRetryPolicyFilter** and **LinearRetryPolicyFilter**.</span></span> <span data-ttu-id="3cb0a-150">Merhaba aşağıdaki oluşturur bir **BlobService** hello kullanan nesneyi **ExponentialRetryPolicyFilter**:</span><span class="sxs-lookup"><span data-stu-id="3cb0a-150">hello following creates a **BlobService** object that uses hello **ExponentialRetryPolicyFilter**:</span></span>

```nodejs
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var blobSvc = azure.createBlobService().withFilter(retryOperations);
```

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="3cb0a-151">Bir kapsayıcıya bir blob yükleme</span><span class="sxs-lookup"><span data-stu-id="3cb0a-151">Upload a blob into a container</span></span>
<span data-ttu-id="3cb0a-152">Üç BLOB türü vardır: blok blobları, sayfa blobları ve ilave blobları.</span><span class="sxs-lookup"><span data-stu-id="3cb0a-152">There are three types of blobs: block blobs, page blobs and append blobs.</span></span> <span data-ttu-id="3cb0a-153">Blok blobları izin toomore verimli bir şekilde büyük veri karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="3cb0a-153">Block blobs allow you toomore efficiently upload large data.</span></span> <span data-ttu-id="3cb0a-154">Ekleme blobları için iyileştirilmiş ekleme işlemleri.</span><span class="sxs-lookup"><span data-stu-id="3cb0a-154">Append blobs are optimized for append operations.</span></span> <span data-ttu-id="3cb0a-155">Sayfa bloblarını okuma/yazma işlemleri için en iyi duruma getirilir.</span><span class="sxs-lookup"><span data-stu-id="3cb0a-155">Page blobs are optimized for read/write operations.</span></span> <span data-ttu-id="3cb0a-156">Daha fazla bilgi için bkz: [anlama blok Blobları, ekleme Blobları ve sayfa Bloblarını](http://msdn.microsoft.com/library/azure/ee691964.aspx).</span><span class="sxs-lookup"><span data-stu-id="3cb0a-156">For more information, see [Understanding Block Blobs, Append Blobs, and Page Blobs](http://msdn.microsoft.com/library/azure/ee691964.aspx).</span></span>

### <a name="block-blobs"></a><span data-ttu-id="3cb0a-157">Blok blobları</span><span class="sxs-lookup"><span data-stu-id="3cb0a-157">Block blobs</span></span>
<span data-ttu-id="3cb0a-158">tooupload veri tooa blok blobu, aşağıdaki kullanım hello:</span><span class="sxs-lookup"><span data-stu-id="3cb0a-158">tooupload data tooa block blob, use hello following:</span></span>

* <span data-ttu-id="3cb0a-159">**createBlockBlobFromLocalFile** - yeni bir blok blobu oluşturur ve bir dosyanın içeriğini hello yükler</span><span class="sxs-lookup"><span data-stu-id="3cb0a-159">**createBlockBlobFromLocalFile** - creates a new block blob and uploads hello contents of a file</span></span>
* <span data-ttu-id="3cb0a-160">**createBlockBlobFromStream** - yeni bir blok blobu oluşturur ve bir akış Merhaba içeriğine yükler</span><span class="sxs-lookup"><span data-stu-id="3cb0a-160">**createBlockBlobFromStream** - creates a new block blob and uploads hello contents of a stream</span></span>
* <span data-ttu-id="3cb0a-161">**createBlockBlobFromText** - yeni bir blok blobu oluşturur ve bir dize Merhaba içeriğine yükler</span><span class="sxs-lookup"><span data-stu-id="3cb0a-161">**createBlockBlobFromText** - creates a new block blob and uploads hello contents of a string</span></span>
* <span data-ttu-id="3cb0a-162">**createWriteStreamToBlockBlob** -yazma akışı tooa blok blobu sağlar</span><span class="sxs-lookup"><span data-stu-id="3cb0a-162">**createWriteStreamToBlockBlob** - provides a write stream tooa block blob</span></span>

<span data-ttu-id="3cb0a-163">Merhaba aşağıdaki kod örneğinde yükleyen hello Merhaba içeriğine **sınama.txt** içine dosya **myblob**.</span><span class="sxs-lookup"><span data-stu-id="3cb0a-163">hello following code example uploads hello contents of hello **test.txt** file into **myblob**.</span></span>

```nodejs
blobSvc.createBlockBlobFromLocalFile('mycontainer', 'myblob', 'test.txt', function(error, result, response){
  if(!error){
    // file uploaded
  }
});
```

<span data-ttu-id="3cb0a-164">Merhaba `result` bu yöntemler tarafından döndürülen hello gibi hello işlemi hakkında bilgi içeren **ETag** hello BLOB.</span><span class="sxs-lookup"><span data-stu-id="3cb0a-164">hello `result` returned by these methods contains information on hello operation, such as hello **ETag** of hello blob.</span></span>

### <a name="append-blobs"></a><span data-ttu-id="3cb0a-165">Ekleme blobları</span><span class="sxs-lookup"><span data-stu-id="3cb0a-165">Append blobs</span></span>
<span data-ttu-id="3cb0a-166">tooupload veri tooa yeni blob ekleme, hello aşağıdakileri kullanın:</span><span class="sxs-lookup"><span data-stu-id="3cb0a-166">tooupload data tooa new append blob, use hello following:</span></span>

* <span data-ttu-id="3cb0a-167">**createAppendBlobFromLocalFile** - yeni bir ek blob oluşturur ve bir dosyanın içeriğini hello yükler</span><span class="sxs-lookup"><span data-stu-id="3cb0a-167">**createAppendBlobFromLocalFile** - creates a new append blob and uploads hello contents of a file</span></span>
* <span data-ttu-id="3cb0a-168">**createAppendBlobFromStream** - yeni bir ek blob oluşturur ve bir akış Merhaba içeriğine yükler</span><span class="sxs-lookup"><span data-stu-id="3cb0a-168">**createAppendBlobFromStream** - creates a new append blob and uploads hello contents of a stream</span></span>
* <span data-ttu-id="3cb0a-169">**createAppendBlobFromText** - yeni bir ek blob oluşturur ve bir dize Merhaba içeriğine yükler</span><span class="sxs-lookup"><span data-stu-id="3cb0a-169">**createAppendBlobFromText** - creates a new append blob and uploads hello contents of a string</span></span>
* <span data-ttu-id="3cb0a-170">**createWriteStreamToNewAppendBlob** - yeni bir ek blob oluşturur ve ardından bir akış toowrite tooit sağlar</span><span class="sxs-lookup"><span data-stu-id="3cb0a-170">**createWriteStreamToNewAppendBlob** - creates a new append blob and then provides a stream toowrite tooit</span></span>

<span data-ttu-id="3cb0a-171">Merhaba aşağıdaki kod örneğinde yükleyen hello Merhaba içeriğine **sınama.txt** içine dosya **myappendblob**.</span><span class="sxs-lookup"><span data-stu-id="3cb0a-171">hello following code example uploads hello contents of hello **test.txt** file into **myappendblob**.</span></span>

```nodejs
blobSvc.createAppendBlobFromLocalFile('mycontainer', 'myappendblob', 'test.txt', function(error, result, response){
  if(!error){
    // file uploaded
  }
});
```

<span data-ttu-id="3cb0a-172">tooappend blok varolan tooan blob, aşağıdaki kullanım hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="3cb0a-172">tooappend a block tooan existing append blob, use hello following:</span></span>

* <span data-ttu-id="3cb0a-173">**appendFromLocalFile** -hello içeriği ekleme dosya tooan blob append var</span><span class="sxs-lookup"><span data-stu-id="3cb0a-173">**appendFromLocalFile** - append hello contents of a file tooan existing append blob</span></span>
* <span data-ttu-id="3cb0a-174">**appendFromStream** -hello içeriği append akış tooan varolan blob ekleme</span><span class="sxs-lookup"><span data-stu-id="3cb0a-174">**appendFromStream** - append hello contents of a stream tooan existing append blob</span></span>
* <span data-ttu-id="3cb0a-175">**appendFromText** -hello içeriği ekleme dize tooan blob append var</span><span class="sxs-lookup"><span data-stu-id="3cb0a-175">**appendFromText** - append hello contents of a string tooan existing append blob</span></span>
* <span data-ttu-id="3cb0a-176">**appendBlockFromStream** -hello içeriği append akış tooan varolan blob ekleme</span><span class="sxs-lookup"><span data-stu-id="3cb0a-176">**appendBlockFromStream** - append hello contents of a stream tooan existing append blob</span></span>
* <span data-ttu-id="3cb0a-177">**appendBlockFromText** -hello içeriği ekleme dize tooan blob append var</span><span class="sxs-lookup"><span data-stu-id="3cb0a-177">**appendBlockFromText** - append hello contents of a string tooan existing append blob</span></span>

> [!NOTE]
> <span data-ttu-id="3cb0a-178">bazı istemci tarafı doğrulama toofail hızlı tooavoid gereksiz sunucu çağrılarını appendFromXXX API'leri yapın.</span><span class="sxs-lookup"><span data-stu-id="3cb0a-178">appendFromXXX APIs will do some client-side validation toofail fast tooavoid unnecessary server calls.</span></span> <span data-ttu-id="3cb0a-179">appendBlockFromXXX olmaz.</span><span class="sxs-lookup"><span data-stu-id="3cb0a-179">appendBlockFromXXX won't.</span></span>
>
>

<span data-ttu-id="3cb0a-180">Merhaba aşağıdaki kod örneğinde yükleyen hello Merhaba içeriğine **sınama.txt** içine dosya **myappendblob**.</span><span class="sxs-lookup"><span data-stu-id="3cb0a-180">hello following code example uploads hello contents of hello **test.txt** file into **myappendblob**.</span></span>

```nodejs
blobSvc.appendFromText('mycontainer', 'myappendblob', 'text toobe appended', function(error, result, response){
  if(!error){
    // text appended
  }
});
```

### <a name="page-blobs"></a><span data-ttu-id="3cb0a-181">Sayfa blobları</span><span class="sxs-lookup"><span data-stu-id="3cb0a-181">Page blobs</span></span>
<span data-ttu-id="3cb0a-182">tooupload veri tooa sayfa blobu, aşağıdaki kullanım hello:</span><span class="sxs-lookup"><span data-stu-id="3cb0a-182">tooupload data tooa page blob, use hello following:</span></span>

* <span data-ttu-id="3cb0a-183">**createPageBlob** -belirli bir uzunlukta yeni bir sayfa blob'u oluşturur</span><span class="sxs-lookup"><span data-stu-id="3cb0a-183">**createPageBlob** - creates a new page blob of a specific length</span></span>
* <span data-ttu-id="3cb0a-184">**createPageBlobFromLocalFile** - yeni bir sayfa blob'u oluşturur ve bir dosyanın içeriğini hello yükler</span><span class="sxs-lookup"><span data-stu-id="3cb0a-184">**createPageBlobFromLocalFile** - creates a new page blob and uploads hello contents of a file</span></span>
* <span data-ttu-id="3cb0a-185">**createPageBlobFromStream** - yeni bir sayfa blob'u oluşturur ve bir akış Merhaba içeriğine yükler</span><span class="sxs-lookup"><span data-stu-id="3cb0a-185">**createPageBlobFromStream** - creates a new page blob and uploads hello contents of a stream</span></span>
* <span data-ttu-id="3cb0a-186">**createWriteStreamToExistingPageBlob** -yazma akışı tooan varolan sayfa blobu sağlar</span><span class="sxs-lookup"><span data-stu-id="3cb0a-186">**createWriteStreamToExistingPageBlob** - provides a write stream tooan existing page blob</span></span>
* <span data-ttu-id="3cb0a-187">**createWriteStreamToNewPageBlob** - yeni bir sayfa blob'u oluşturur ve ardından bir akış toowrite tooit sağlar</span><span class="sxs-lookup"><span data-stu-id="3cb0a-187">**createWriteStreamToNewPageBlob** - creates a new page blob and then provides a stream toowrite tooit</span></span>

<span data-ttu-id="3cb0a-188">Merhaba aşağıdaki kod örneğinde yükleyen hello Merhaba içeriğine **sınama.txt** içine dosya **mypageblob**.</span><span class="sxs-lookup"><span data-stu-id="3cb0a-188">hello following code example uploads hello contents of hello **test.txt** file into **mypageblob**.</span></span>

```nodejs
blobSvc.createPageBlobFromLocalFile('mycontainer', 'mypageblob', 'test.txt', function(error, result, response){
  if(!error){
    // file uploaded
  }
});
```

> [!NOTE]
> <span data-ttu-id="3cb0a-189">Sayfa bloblarını 512 bayt 'sayfalar' oluşur.</span><span class="sxs-lookup"><span data-stu-id="3cb0a-189">Page blobs consist of 512-byte 'pages'.</span></span> <span data-ttu-id="3cb0a-190">512 birden fazla olmayan bir boyutu ile verileri karşıya yüklenirken bir hata alırsınız.</span><span class="sxs-lookup"><span data-stu-id="3cb0a-190">You will receive an error when uploading data with a size that is not a multiple of 512.</span></span>
>
>

## <a name="list-hello-blobs-in-a-container"></a><span data-ttu-id="3cb0a-191">Liste hello BLOB'ları bir kapsayıcıda</span><span class="sxs-lookup"><span data-stu-id="3cb0a-191">List hello blobs in a container</span></span>
<span data-ttu-id="3cb0a-192">toolist hello BLOB'ları bir kapsayıcıda kullanmak hello **listBlobsSegmented** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="3cb0a-192">toolist hello blobs in a container, use hello **listBlobsSegmented** method.</span></span> <span data-ttu-id="3cb0a-193">Belirli bir önek ile tooreturn BLOB'lar istiyorsanız kullanın **listBlobsSegmentedWithPrefix**.</span><span class="sxs-lookup"><span data-stu-id="3cb0a-193">If you'd like tooreturn blobs with a specific prefix, use **listBlobsSegmentedWithPrefix**.</span></span>

```nodejs
blobSvc.listBlobsSegmented('mycontainer', null, function(error, result, response){
  if(!error){
      // result.entries contains hello entries
      // If not all blobs were returned, result.continuationToken has hello continuation token.
  }
});
```

<span data-ttu-id="3cb0a-194">Merhaba `result` içeren bir `entries` her bir blob açıklayan nesnelerinin bir dizisidir koleksiyonu.</span><span class="sxs-lookup"><span data-stu-id="3cb0a-194">hello `result` contains an `entries` collection, which is an array of objects that describe each blob.</span></span> <span data-ttu-id="3cb0a-195">Tüm BLOB'lar döndürülemez, hello `result` de sağlar bir `continuationToken`, hangi hello ikinci parametre tooretrieve ek girişleri olarak kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="3cb0a-195">If all blobs cannot be returned, hello `result` also provides a `continuationToken`, which you may use as hello second parameter tooretrieve additional entries.</span></span>

## <a name="download-blobs"></a><span data-ttu-id="3cb0a-196">Blob’ları indirme</span><span class="sxs-lookup"><span data-stu-id="3cb0a-196">Download blobs</span></span>
<span data-ttu-id="3cb0a-197">bir blob toodownload verilerden hello aşağıdakileri kullanın:</span><span class="sxs-lookup"><span data-stu-id="3cb0a-197">toodownload data from a blob, use hello following:</span></span>

* <span data-ttu-id="3cb0a-198">**getBlobToLocalFile** -hello blob içeriği toofile Yazar</span><span class="sxs-lookup"><span data-stu-id="3cb0a-198">**getBlobToLocalFile** - writes hello blob contents toofile</span></span>
* <span data-ttu-id="3cb0a-199">**getBlobToStream** -hello blob içeriği tooa akışa Yazar</span><span class="sxs-lookup"><span data-stu-id="3cb0a-199">**getBlobToStream** - writes hello blob contents tooa stream</span></span>
* <span data-ttu-id="3cb0a-200">**getBlobToText** -tooa dize hello blob içeriklerini Yazar</span><span class="sxs-lookup"><span data-stu-id="3cb0a-200">**getBlobToText** - writes hello blob contents tooa string</span></span>
* <span data-ttu-id="3cb0a-201">**createReadStream** -hello blob gelen bir akış tooread sağlar</span><span class="sxs-lookup"><span data-stu-id="3cb0a-201">**createReadStream** - provides a stream tooread from hello blob</span></span>

<span data-ttu-id="3cb0a-202">Merhaba aşağıdaki kod örneğinde kullanarak gösterilmektedir **getBlobToStream** toodownload Merhaba içeriğine hello **myblob** toohello depolamak ve blob **çýktý.txt** kullanarak dosya bir Akış:</span><span class="sxs-lookup"><span data-stu-id="3cb0a-202">hello following code example demonstrates using **getBlobToStream** toodownload hello contents of hello **myblob** blob and store it toohello **output.txt** file by using a stream:</span></span>

```nodejs
var fs = require('fs');
blobSvc.getBlobToStream('mycontainer', 'myblob', fs.createWriteStream('output.txt'), function(error, result, response){
  if(!error){
    // blob retrieved
  }
});
```

<span data-ttu-id="3cb0a-203">Merhaba `result` hello blob hakkında bilgi içeren dahil olmak üzere **ETag** bilgi.</span><span class="sxs-lookup"><span data-stu-id="3cb0a-203">hello `result` contains information about hello blob, including **ETag** information.</span></span>

## <a name="delete-a-blob"></a><span data-ttu-id="3cb0a-204">Blob silme</span><span class="sxs-lookup"><span data-stu-id="3cb0a-204">Delete a blob</span></span>
<span data-ttu-id="3cb0a-205">Son olarak, bir blob toodelete çağrısı **deleteBlob**.</span><span class="sxs-lookup"><span data-stu-id="3cb0a-205">Finally, toodelete a blob, call **deleteBlob**.</span></span> <span data-ttu-id="3cb0a-206">Aşağıdaki kod örneğine siler hello adlı blob hello **myblob**.</span><span class="sxs-lookup"><span data-stu-id="3cb0a-206">hello following code example deletes hello blob named **myblob**.</span></span>

```nodejs
blobSvc.deleteBlob(containerName, 'myblob', function(error, response){
  if(!error){
    // Blob has been deleted
  }
});
```

## <a name="concurrent-access"></a><span data-ttu-id="3cb0a-207">Eş zamanlı erişim</span><span class="sxs-lookup"><span data-stu-id="3cb0a-207">Concurrent access</span></span>
<span data-ttu-id="3cb0a-208">kullanabileceğiniz toosupport eş zamanlı erişim tooa blob birden çok istemciden veya birden çok örneği **Etag'ler** veya **kiraları**.</span><span class="sxs-lookup"><span data-stu-id="3cb0a-208">toosupport concurrent access tooa blob from multiple clients or multiple process instances, you can use **ETags** or **leases**.</span></span>

* <span data-ttu-id="3cb0a-209">**ETag** -blob veya kapsayıcı hello bir şekilde toodetect başka bir işlem tarafından değiştirilmiş sağlar</span><span class="sxs-lookup"><span data-stu-id="3cb0a-209">**Etag** - provides a way toodetect that hello blob or container has been modified by another process</span></span>
* <span data-ttu-id="3cb0a-210">**Kira** - yolu tooobtain özel ve yenilenebilir, yazma sağlar veya bir süre için erişim tooa blob Sil</span><span class="sxs-lookup"><span data-stu-id="3cb0a-210">**Lease** - provides a way tooobtain exclusive, renewable, write or delete access tooa blob for a period of time</span></span>

### <a name="etag"></a><span data-ttu-id="3cb0a-211">ETag</span><span class="sxs-lookup"><span data-stu-id="3cb0a-211">ETag</span></span>
<span data-ttu-id="3cb0a-212">Birden çok istemciler veya örnekleri toowrite toohello blok blobu veya sayfa Blob aynı anda tooallow gerekirse Etag'ler kullanın.</span><span class="sxs-lookup"><span data-stu-id="3cb0a-212">Use ETags if you need tooallow multiple clients or instances toowrite toohello block Blob or page Blob simultaneously.</span></span> <span data-ttu-id="3cb0a-213">Başlangıçta okumak veya başka bir istemci ya da işlem tarafından kaydedilen değişikliklerin üzerine tooavoid sağlayan, oluşturulan beri hello kapsayıcı veya blob değiştirilmişse hello ETag toodetermine sağlar.</span><span class="sxs-lookup"><span data-stu-id="3cb0a-213">hello ETag allows you toodetermine if hello container or blob was modified since you initially read or created it, which allows you tooavoid overwriting changes committed by another client or process.</span></span>

<span data-ttu-id="3cb0a-214">İsteğe bağlı hello kullanarak ETag koşulları ayarlayabilirsiniz `options.accessConditions` parametresi.</span><span class="sxs-lookup"><span data-stu-id="3cb0a-214">You can set ETag conditions by using hello optional `options.accessConditions` parameter.</span></span> <span data-ttu-id="3cb0a-215">Merhaba aşağıdaki kod örneği yalnızca hello yükler **sınama.txt** hello blob zaten varsa ve hello ETag değerine sahip dosyasında alan tarafından `etagToMatch`.</span><span class="sxs-lookup"><span data-stu-id="3cb0a-215">hello following code example only uploads hello **test.txt** file if hello blob already exists and has hello ETag value contained by `etagToMatch`.</span></span>

```nodejs
blobSvc.createBlockBlobFromLocalFile('mycontainer', 'myblob', 'test.txt', { accessConditions: { EtagMatch: etagToMatch} }, function(error, result, response){
    if(!error){
    // file uploaded
  }
});
```

<span data-ttu-id="3cb0a-216">Etag'ler kullanırken hello genel modeli aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="3cb0a-216">When you're using ETags, hello general pattern is:</span></span>

1. <span data-ttu-id="3cb0a-217">Merhaba ETag oluşturma, liste veya alma işlemi hello sonucu olarak alın.</span><span class="sxs-lookup"><span data-stu-id="3cb0a-217">Obtain hello ETag as hello result of a create, list, or get operation.</span></span>
2. <span data-ttu-id="3cb0a-218">Bir eylem gerçekleştirmek, o hello ETag değeri denetleme değiştirilmedi.</span><span class="sxs-lookup"><span data-stu-id="3cb0a-218">Perform an action, checking that hello ETag value has not been modified.</span></span>

<span data-ttu-id="3cb0a-219">Merhaba değeri değiştirilmişse, bu hello ETag değeri elde olduğundan başka bir istemci veya örnek hello blob veya kapsayıcı değiştirildiğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="3cb0a-219">If hello value was modified, this indicates that another client or instance modified hello blob or container since you obtained hello ETag value.</span></span>

### <a name="lease"></a><span data-ttu-id="3cb0a-220">Kira</span><span class="sxs-lookup"><span data-stu-id="3cb0a-220">Lease</span></span>
<span data-ttu-id="3cb0a-221">Hello kullanarak yeni bir kira elde edebilirsiniz **acquireLease** yöntemi, üzerinde bir kira tooobtain istediğiniz hello blob veya kapsayıcı belirtme.</span><span class="sxs-lookup"><span data-stu-id="3cb0a-221">You can acquire a new lease by using hello **acquireLease** method, specifying hello blob or container that you wish tooobtain a lease on.</span></span> <span data-ttu-id="3cb0a-222">Örneğin, kod aşağıdaki hello üzerinde bir kira alması **myblob**.</span><span class="sxs-lookup"><span data-stu-id="3cb0a-222">For example, hello following code acquires a lease on **myblob**.</span></span>

```nodejs
blobSvc.acquireLease('mycontainer', 'myblob', function(error, result, response){
  if(!error) {
    console.log('leaseId: ' + result.id);
  }
});
```

<span data-ttu-id="3cb0a-223">Sonraki işlemlerde **myblob** hello sağlamalısınız `options.leaseId` parametresi.</span><span class="sxs-lookup"><span data-stu-id="3cb0a-223">Subsequent operations on **myblob** must provide hello `options.leaseId` parameter.</span></span> <span data-ttu-id="3cb0a-224">Kimliği olarak döndürülür hello kira `result.id` gelen **acquireLease**.</span><span class="sxs-lookup"><span data-stu-id="3cb0a-224">hello lease ID is returned as `result.id` from **acquireLease**.</span></span>

> [!NOTE]
> <span data-ttu-id="3cb0a-225">Varsayılan olarak, hello kira süresi sonsuzdur.</span><span class="sxs-lookup"><span data-stu-id="3cb0a-225">By default, hello lease duration is infinite.</span></span> <span data-ttu-id="3cb0a-226">Merhaba sağlayarak (arasındaki 15 ila 60 saniye) sonsuz olmayan süre belirtebilirsiniz `options.leaseDuration` parametresi.</span><span class="sxs-lookup"><span data-stu-id="3cb0a-226">You can specify a non-infinite duration (between 15 and 60 seconds) by providing hello `options.leaseDuration` parameter.</span></span>
>
>

<span data-ttu-id="3cb0a-227">tooremove bir kira kullanmak **releaseLease**.</span><span class="sxs-lookup"><span data-stu-id="3cb0a-227">tooremove a lease, use **releaseLease**.</span></span> <span data-ttu-id="3cb0a-228">toobreak bir kira ancak önlemek başkalarının hello özgün süresi sona erinceye kadar yeni bir kira elde etmesini kullanmak **breakLease**.</span><span class="sxs-lookup"><span data-stu-id="3cb0a-228">toobreak a lease, but prevent others from obtaining a new lease until hello original duration has expired, use **breakLease**.</span></span>

## <a name="work-with-shared-access-signatures"></a><span data-ttu-id="3cb0a-229">Paylaşılan erişim imzaları ile çalışma</span><span class="sxs-lookup"><span data-stu-id="3cb0a-229">Work with shared access signatures</span></span>
<span data-ttu-id="3cb0a-230">Paylaşılan erişim imzaları (SAS), güvenli şekilde tooprovide ayrıntılı erişim tooblobs ve depolama hesabı adı veya anahtarları sağlamadan kapsayıcıları ' dir.</span><span class="sxs-lookup"><span data-stu-id="3cb0a-230">Shared access signatures (SAS) are a secure way tooprovide granular access tooblobs and containers without providing your storage account name or keys.</span></span> <span data-ttu-id="3cb0a-231">Paylaşılan erişim imzaları genellikle bir mobil uygulama tooaccess BLOB'lar izin verme gibi sınırlı kullanılan tooprovide erişim tooyour, verilerdir.</span><span class="sxs-lookup"><span data-stu-id="3cb0a-231">Shared access signatures are often used tooprovide limited access tooyour data, such as allowing a mobile app tooaccess blobs.</span></span>

> [!NOTE]
> <span data-ttu-id="3cb0a-232">Anonim erişim tooblobs izin verebilir, ancak hello SAS oluşturmalıdır paylaşılan erişim imzaları daha kontrol tooprovide erişim olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="3cb0a-232">While you can also allow anonymous access tooblobs, shared access signatures allow you tooprovide more controlled access, as you must generate hello SAS.</span></span>
>
>

<span data-ttu-id="3cb0a-233">Paylaşılan erişim imzaları hello kullanarak bulut tabanlı bir hizmete gibi güvenilir bir uygulama oluşturur **generateSharedAccessSignature** Merhaba, **BlobService**, sağlar ve güvenilmeyen tooan veya Yarı güvenilir uygulama mobil uygulama gibi.</span><span class="sxs-lookup"><span data-stu-id="3cb0a-233">A trusted application such as a cloud-based service generates shared access signatures using hello **generateSharedAccessSignature** of hello **BlobService**, and provides it tooan untrusted or semi-trusted application such as a mobile app.</span></span> <span data-ttu-id="3cb0a-234">Paylaşılan erişim imzaları hello başlangıç açıklayan bir ilkeyi kullanarak oluşturulan ve bitiş tarihleri sırasında hangi hello paylaşılan erişim imzaları geçerli yanı sıra, hello düzeyi verilen toohello paylaşılan erişim imzaları sahibi erişin.</span><span class="sxs-lookup"><span data-stu-id="3cb0a-234">Shared access signatures are generated using a policy, which describes hello start and end dates during which hello shared access signatures are valid, as well as hello access level granted toohello shared access signatures holder.</span></span>

<span data-ttu-id="3cb0a-235">Merhaba aşağıdaki kod örneği oluşturur hello paylaşılan erişim imzaları sahibi tooperform okuma işlemleri hello izin veren yeni bir paylaşılan erişim ilkesi **myblob** blob ve 100 dakika oluşturulan hello sonra süresi dolar.</span><span class="sxs-lookup"><span data-stu-id="3cb0a-235">hello following code example generates a new shared access policy that allows hello shared access signatures holder tooperform read operations on hello **myblob** blob, and expires 100 minutes after hello time it is created.</span></span>

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

<span data-ttu-id="3cb0a-236">Gerekli olduğu gibi aynı zamanda, hello paylaşılan erişim imzaları sahibi tooaccess hello kapsayıcı çalıştığında sağlanan hello ana bilgisayar bilgilerini olması gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="3cb0a-236">Note that hello host information must be provided also, as it is required when hello shared access signatures holder attempts tooaccess hello container.</span></span>

<span data-ttu-id="3cb0a-237">Merhaba sonra istemci uygulamanın kullandığı paylaşılan erişim imzaları ile **BlobServiceWithSAS** hello blob karşı tooperform işlemleri.</span><span class="sxs-lookup"><span data-stu-id="3cb0a-237">hello client application then uses shared access signatures with **BlobServiceWithSAS** tooperform operations against hello blob.</span></span> <span data-ttu-id="3cb0a-238">Merhaba aşağıdaki bilgileri alır **myblob**.</span><span class="sxs-lookup"><span data-stu-id="3cb0a-238">hello following gets information about **myblob**.</span></span>

```nodejs
var sharedBlobSvc = azure.createBlobServiceWithSas(host, blobSAS);
sharedBlobSvc.getBlobProperties('mycontainer', 'myblob', function (error, result, response) {
  if(!error) {
    // retrieved info
  }
});
```

<span data-ttu-id="3cb0a-239">Toomodify hello blob denemesi yapılırsa, salt okunur erişim ile Merhaba paylaşılan erişim imzaları oluşturulduktan sonra bir hata döndürülür.</span><span class="sxs-lookup"><span data-stu-id="3cb0a-239">Since hello shared access signatures were generated with read-only access, if an attempt is made toomodify hello blob, an error will be returned.</span></span>

### <a name="access-control-lists"></a><span data-ttu-id="3cb0a-240">Erişim denetimi listeleri</span><span class="sxs-lookup"><span data-stu-id="3cb0a-240">Access control lists</span></span>
<span data-ttu-id="3cb0a-241">Bir erişim denetimi listesi (ACL) tooset hello erişim ilkesi için SAS de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3cb0a-241">You can also use an access control list (ACL) tooset hello access policy for SAS.</span></span> <span data-ttu-id="3cb0a-242">Birden çok istemcileri tooaccess bir kapsayıcı tooallow istiyor, ancak her istemci için farklı erişim ilkeleri sağlar, bu yararlı olur.</span><span class="sxs-lookup"><span data-stu-id="3cb0a-242">This is useful if you wish tooallow multiple clients tooaccess a container but provide different access policies for each client.</span></span>

<span data-ttu-id="3cb0a-243">Bir ACL her ilkesiyle ilişkili bir Kimliğe sahip bir dizi erişim ilkeleri kullanılarak uygulanır.</span><span class="sxs-lookup"><span data-stu-id="3cb0a-243">An ACL is implemented using an array of access policies, with an ID associated with each policy.</span></span> <span data-ttu-id="3cb0a-244">Aşağıdaki kod örneğine hello iki ilke, 'User1' diğeri için 'kullanıcı2' tanımlar:</span><span class="sxs-lookup"><span data-stu-id="3cb0a-244">hello following code example defines two policies, one for 'user1' and one for 'user2':</span></span>

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

<span data-ttu-id="3cb0a-245">Aşağıdaki kod örneği alır hello hello geçerli ACL'si **mycontainer**ve ardından hello yeni ilkeleri kullanılarak ekler **setBlobAcl**.</span><span class="sxs-lookup"><span data-stu-id="3cb0a-245">hello following code example gets hello current ACL for **mycontainer**, and then adds hello new policies using **setBlobAcl**.</span></span> <span data-ttu-id="3cb0a-246">Bu yaklaşım sağlar:</span><span class="sxs-lookup"><span data-stu-id="3cb0a-246">This approach allows:</span></span>

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

<span data-ttu-id="3cb0a-247">Bir kez hello ACL ayarlayın, bir ilke hello kimliği temel paylaşılan erişim imzaları sonra oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3cb0a-247">Once hello ACL is set, you can then create shared access signatures based on hello ID for a policy.</span></span> <span data-ttu-id="3cb0a-248">Aşağıdaki kod örneğine hello 'kullanıcı2' yeni paylaşılan erişim imzaları oluşturur:</span><span class="sxs-lookup"><span data-stu-id="3cb0a-248">hello following code example creates new shared access signatures for 'user2':</span></span>

```nodejs
blobSAS = blobSvc.generateSharedAccessSignature('mycontainer', { Id: 'user2' });
```

## <a name="next-steps"></a><span data-ttu-id="3cb0a-249">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3cb0a-249">Next steps</span></span>
<span data-ttu-id="3cb0a-250">Daha fazla bilgi için kaynakları aşağıdaki hello bakın.</span><span class="sxs-lookup"><span data-stu-id="3cb0a-250">For more information, see hello following resources.</span></span>

* <span data-ttu-id="3cb0a-251">[Azure Depolama düğümü API Başvurusu için SDK] [Azure Depolama düğümü API Başvurusu için SDK]</span><span class="sxs-lookup"><span data-stu-id="3cb0a-251">[Azure Storage SDK for Node API Reference][Azure Storage SDK for Node API Reference]</span></span>
* <span data-ttu-id="3cb0a-252">[Azure depolama ekibi blogu] [Azure depolama ekibi blogu]</span><span class="sxs-lookup"><span data-stu-id="3cb0a-252">[Azure Storage Team Blog][Azure Storage Team Blog]</span></span>
* <span data-ttu-id="3cb0a-253">[Azure depolama SDK'sı düğüm için] [ Azure Storage SDK for Node] github'daki</span><span class="sxs-lookup"><span data-stu-id="3cb0a-253">[Azure Storage SDK for Node][Azure Storage SDK for Node] repository on GitHub</span></span>
* [<span data-ttu-id="3cb0a-254">Node.js Geliştirici Merkezi</span><span class="sxs-lookup"><span data-stu-id="3cb0a-254">Node.js Developer Center</span></span>](https://azure.microsoft.com/develop/nodejs/)
* [<span data-ttu-id="3cb0a-255">Merhaba AzCopy komut satırı yardımcı programı ile veri aktarımı</span><span class="sxs-lookup"><span data-stu-id="3cb0a-255">Transfer data with hello AzCopy command-line utility</span></span>](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)

[Azure Storage SDK for Node]: https://github.com/Azure/azure-storage-node

<span data-ttu-id="3cb0a-256">[Hello Azure tablo hizmeti kullanarak Node.js web uygulaması](../../app-service-web/storage-nodejs-use-table-storage-web-site.md)  </span><span class="sxs-lookup"><span data-stu-id="3cb0a-256">[Node.js web app using hello Azure Table Service](../../app-service-web/storage-nodejs-use-table-storage-web-site.md)  </span></span>  
<span data-ttu-id="3cb0a-257">[Derleme ve Web Matrix kullanarak bir Node.js web uygulaması tooAzure dağıtma]: https://www.microsoft.com/web/webmatrix/</span><span class="sxs-lookup"><span data-stu-id="3cb0a-257">[Build and deploy a Node.js web app tooAzure using Web Matrix]: https://www.microsoft.com/web/webmatrix/</span></span>  
<span data-ttu-id="3cb0a-258">[REST API hello kullanarak]: [Azure portalı] http://msdn.microsoft.com/library/azure/hh264518.aspx: https://portal.azure.com [derleme ve bir Node.js uygulaması tooan Azure bulut hizmeti dağıtma](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md) [Azure depolama ekibi blogu]: http:// blogs.msdn.com/b/windowsazurestorage/ [Azure Depolama düğümü API Başvurusu için SDK]: http://dl.windowsazure.com/nodestoragedocs/index.html</span><span class="sxs-lookup"><span data-stu-id="3cb0a-258">[Using hello REST API]: http://msdn.microsoft.com/library/azure/hh264518.aspx [Azure portal]: https://portal.azure.com [Build and deploy a Node.js application tooan Azure Cloud Service](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md) [Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/ [Azure Storage SDK for Node API Reference]: http://dl.windowsazure.com/nodestoragedocs/index.html</span></span>
