---
title: "aaaHow toouse Node.js Azure tablo depolamasından | Microsoft Docs"
description: "Bir NoSQL veri deposu olan Azure Table storage kullanılarak hello bulutta yapılandırılmış veri depolayın."
services: cosmos-db
documentationcenter: nodejs
author: mimig1
manager: jhubbard
editor: tysonn
ms.assetid: fc2e33d2-c5da-4861-8503-53fdc25750de
ms.service: cosmos-db
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/08/2016
ms.author: mimig
ms.openlocfilehash: 21022491a9a21a5365628de93582ea3a325ed869
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-table-storage-from-nodejs"></a><span data-ttu-id="1bb8e-103">Nasıl toouse Node.js Azure tablo depolamasından</span><span class="sxs-lookup"><span data-stu-id="1bb8e-103">How toouse Azure Table storage from Node.js</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a><span data-ttu-id="1bb8e-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="1bb8e-104">Overview</span></span>
<span data-ttu-id="1bb8e-105">Bu konu, nasıl tooperform yaygın senaryolar hello Azure Table kullanarak bir Node.js uygulamasında hizmet gösterir.</span><span class="sxs-lookup"><span data-stu-id="1bb8e-105">This topic shows how tooperform common scenarios using hello Azure Table service in a Node.js application.</span></span>

<span data-ttu-id="1bb8e-106">Bu konudaki Hello kod örnekleri, bir Node.js uygulaması zaten olduğunu varsayın.</span><span class="sxs-lookup"><span data-stu-id="1bb8e-106">hello code examples in this topic assume you already have a Node.js application.</span></span> <span data-ttu-id="1bb8e-107">Hakkında bilgi için toocreate Azure, bir Node.js uygulamasında aşağıdaki konulardan birini bakın:</span><span class="sxs-lookup"><span data-stu-id="1bb8e-107">For information about how toocreate a Node.js application in Azure, see any of these topics:</span></span>

* [<span data-ttu-id="1bb8e-108">Azure App Service'te bir Node.js web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="1bb8e-108">Create a Node.js web app in Azure App Service</span></span>](../app-service-web/app-service-web-get-started-nodejs.md)
* [<span data-ttu-id="1bb8e-109">Derleme ve Webmatrix'i kullanarak bir Node.js web uygulaması tooAzure dağıtma</span><span class="sxs-lookup"><span data-stu-id="1bb8e-109">Build and deploy a Node.js web app tooAzure using WebMatrix</span></span>](../app-service-web/web-sites-nodejs-use-webmatrix.md)
* <span data-ttu-id="1bb8e-110">[Derleme ve bir Node.js uygulaması tooan Azure bulut hizmeti dağıtma](../cloud-services/cloud-services-nodejs-develop-deploy-app.md) (Windows PowerShell kullanarak)</span><span class="sxs-lookup"><span data-stu-id="1bb8e-110">[Build and deploy a Node.js application tooan Azure Cloud Service](../cloud-services/cloud-services-nodejs-develop-deploy-app.md) (using Windows PowerShell)</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="configure-your-application-tooaccess-azure-storage"></a><span data-ttu-id="1bb8e-111">Uygulama tooaccess Azure Storage yapılandırın</span><span class="sxs-lookup"><span data-stu-id="1bb8e-111">Configure your application tooaccess Azure Storage</span></span>
<span data-ttu-id="1bb8e-112">toouse Azure Storage, hello storage REST Hizmetleri ile iletişim kuran bir dizi kolaylık içerir Node.js için Azure depolama SDK'sını hello gerekir.</span><span class="sxs-lookup"><span data-stu-id="1bb8e-112">toouse Azure Storage, you need hello Azure Storage SDK for Node.js, which includes a set of convenience libraries that communicate with hello storage REST services.</span></span>

### <a name="use-node-package-manager-npm-tooinstall-hello-package"></a><span data-ttu-id="1bb8e-113">Düğüm paketi Yöneticisi (NPM) tooinstall hello paketini kullanın</span><span class="sxs-lookup"><span data-stu-id="1bb8e-113">Use Node Package Manager (NPM) tooinstall hello package</span></span>
1. <span data-ttu-id="1bb8e-114">Bir komut satırı arabirimi gibi kullandığınız **PowerShell** (Windows) **Terminal** (Mac) veya **Bash** (UNIX) ve uygulamanızı oluşturulduğu toohello klasörüne gidin.</span><span class="sxs-lookup"><span data-stu-id="1bb8e-114">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix), and navigate toohello folder where you created your application.</span></span>
2. <span data-ttu-id="1bb8e-115">Tür **npm yükleme azure depolama** hello komut penceresinde.</span><span class="sxs-lookup"><span data-stu-id="1bb8e-115">Type **npm install azure-storage** in hello command window.</span></span> <span data-ttu-id="1bb8e-116">Merhaba komut çıktısı aşağıdaki örneğine benzer toohello ' dir.</span><span class="sxs-lookup"><span data-stu-id="1bb8e-116">Output from hello command is similar toohello following example.</span></span>

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
3. <span data-ttu-id="1bb8e-117">Merhaba el ile çalıştırabilirsiniz **ls** komutu tooverify, bir **düğümü\_modülleri** klasörü oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="1bb8e-117">You can manually run hello **ls** command tooverify that a **node\_modules** folder was created.</span></span> <span data-ttu-id="1bb8e-118">Bu klasöre hello bulacaksınız **azure depolama** tooaccess depolama ihtiyacınız hello kitaplıklarını içeren paket.</span><span class="sxs-lookup"><span data-stu-id="1bb8e-118">Inside that folder you will find hello **azure-storage** package, which contains hello libraries you need tooaccess storage.</span></span>

### <a name="import-hello-package"></a><span data-ttu-id="1bb8e-119">Merhaba paketi İçeri Aktar</span><span class="sxs-lookup"><span data-stu-id="1bb8e-119">Import hello package</span></span>
<span data-ttu-id="1bb8e-120">Kod toohello hello üstündeki aşağıdaki hello eklemek **server.js** uygulamanızı dosyasında:</span><span class="sxs-lookup"><span data-stu-id="1bb8e-120">Add hello following code toohello top of hello **server.js** file in your application:</span></span>

```nodejs
var azure = require('azure-storage');
```

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="1bb8e-121">Bir Azure depolama bağlantı kurma</span><span class="sxs-lookup"><span data-stu-id="1bb8e-121">Set up an Azure Storage connection</span></span>
<span data-ttu-id="1bb8e-122">Hello azure modülü hello ortam değişkenleri AZURE okuma\_depolama\_HESABINI ve AZURE\_depolama\_erişim\_anahtar ya da AZURE\_depolama\_bağlantı \_Gerekli bilgileri tooconnect tooyour Azure depolama hesabı için dize.</span><span class="sxs-lookup"><span data-stu-id="1bb8e-122">hello azure module will read hello environment variables AZURE\_STORAGE\_ACCOUNT and AZURE\_STORAGE\_ACCESS\_KEY, or AZURE\_STORAGE\_CONNECTION\_STRING for information required tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="1bb8e-123">Bu ortam değişkenleri ayarlanmamışsa çağrılırken hello hesap bilgileri belirtmelisiniz **TableService**.</span><span class="sxs-lookup"><span data-stu-id="1bb8e-123">If these environment variables are not set, you must specify hello account information when calling **TableService**.</span></span>

<span data-ttu-id="1bb8e-124">Hello hello ortam değişkenlerini ayarlama örneği için [Azure portal](https://portal.azure.com) bir Azure Web sitesi için bkz: [Node.js web app kullanarak hello Azure tablo hizmeti](../app-service-web/storage-nodejs-use-table-storage-web-site.md).</span><span class="sxs-lookup"><span data-stu-id="1bb8e-124">For an example of setting hello environment variables in hello [Azure portal](https://portal.azure.com) for an Azure Website, see [Node.js web app using hello Azure Table Service](../app-service-web/storage-nodejs-use-table-storage-web-site.md).</span></span>

## <a name="create-a-table"></a><span data-ttu-id="1bb8e-125">Bir tablo oluşturma</span><span class="sxs-lookup"><span data-stu-id="1bb8e-125">Create a table</span></span>
<span data-ttu-id="1bb8e-126">Merhaba aşağıdaki kod oluşturur bir **TableService** nesne ve toocreate yeni bir tablo kullanır.</span><span class="sxs-lookup"><span data-stu-id="1bb8e-126">hello following code creates a **TableService** object and uses it toocreate a new table.</span></span> <span data-ttu-id="1bb8e-127">Merhaba üstündeki yakın Hello aşağıdakileri ekleyin **server.js**.</span><span class="sxs-lookup"><span data-stu-id="1bb8e-127">Add hello following near hello top of **server.js**.</span></span>

```nodejs
var tableSvc = azure.createTableService();
```

<span data-ttu-id="1bb8e-128">Çağrı çok hello**createTableIfNotExists** zaten yoksa, hello belirtilen adla yeni bir tablo oluşturur.</span><span class="sxs-lookup"><span data-stu-id="1bb8e-128">hello call too**createTableIfNotExists** will create a new table with hello specified name if it does not already exist.</span></span> <span data-ttu-id="1bb8e-129">Merhaba aşağıdaki örnekte zaten yoksa, 'mytable' adlı yeni bir tablo oluşturur:</span><span class="sxs-lookup"><span data-stu-id="1bb8e-129">hello following example creates a new table named 'mytable' if it does not already exist:</span></span>

```nodejs
tableSvc.createTableIfNotExists('mytable', function(error, result, response){
  if(!error){
    // Table exists or created
  }
});
```

<span data-ttu-id="1bb8e-130">Merhaba `result.created` olacaktır `true` yeni bir tablo oluşturduysanız ve `false` hello tablo zaten varsa.</span><span class="sxs-lookup"><span data-stu-id="1bb8e-130">hello `result.created` will be `true` if a new table is created, and `false` if hello table already exists.</span></span> <span data-ttu-id="1bb8e-131">Merhaba `response` hello isteğiyle ilgili bilgileri içerir.</span><span class="sxs-lookup"><span data-stu-id="1bb8e-131">hello `response` will contain information about hello request.</span></span>

### <a name="filters"></a><span data-ttu-id="1bb8e-132">Filtreler</span><span class="sxs-lookup"><span data-stu-id="1bb8e-132">Filters</span></span>
<span data-ttu-id="1bb8e-133">İsteğe bağlı filtreleme operations kullanılarak gerçekleştirilen uygulanan toooperations olabilir **TableService**.</span><span class="sxs-lookup"><span data-stu-id="1bb8e-133">Optional filtering operations can be applied toooperations performed using **TableService**.</span></span> <span data-ttu-id="1bb8e-134">İşlemleri filtreleme içerebilir günlüğe kaydetme, otomatik olarak yeniden deneniyor, vs. Filtreleri hello imza yöntemiyle uygulayan nesneler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="1bb8e-134">Filtering operations can include logging, automatically retrying, etc. Filters are objects that implement a method with hello signature:</span></span>

```nodejs
function handle (requestOptions, next)
```

<span data-ttu-id="1bb8e-135">Kendi hello isteği seçenekleri ön işleme yaptıktan sonra hello yöntemi toocall "İleri", bir geri çağırma imza aşağıdaki hello ile geçirme gerekir:</span><span class="sxs-lookup"><span data-stu-id="1bb8e-135">After doing its preprocessing on hello request options, hello method needs toocall "next", passing a callback with hello following signature:</span></span>

```nodejs
function (returnObject, finalCallback, next)
```

<span data-ttu-id="1bb8e-136">Bu geri çağırma ve hello returnObject (Merhaba isteği toohello sunucusundan hello yanıt) işlemden sonra hello geri çağırma tooeither gereken diğer filtreleri işleme toocontinue varsa sonraki çağırma veya yalnızca finalCallback çağırma aksi tooend hello Hizmet başlatma.</span><span class="sxs-lookup"><span data-stu-id="1bb8e-136">In this callback, and after processing hello returnObject (hello response from hello request toohello server), hello callback needs tooeither invoke next if it exists toocontinue processing other filters or simply invoke finalCallback otherwise tooend hello service invocation.</span></span>

<span data-ttu-id="1bb8e-137">Yeniden deneme mantığını uygulaması iki filtre hello Node.js için Azure SDK ile birlikte **ExponentialRetryPolicyFilter** ve **LinearRetryPolicyFilter**.</span><span class="sxs-lookup"><span data-stu-id="1bb8e-137">Two filters that implement retry logic are included with hello Azure SDK for Node.js, **ExponentialRetryPolicyFilter** and **LinearRetryPolicyFilter**.</span></span> <span data-ttu-id="1bb8e-138">Merhaba aşağıdaki oluşturur bir **TableService** hello kullanan nesneyi **ExponentialRetryPolicyFilter**:</span><span class="sxs-lookup"><span data-stu-id="1bb8e-138">hello following creates a **TableService** object that uses hello **ExponentialRetryPolicyFilter**:</span></span>

```nodejs
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var tableSvc = azure.createTableService().withFilter(retryOperations);
```

## <a name="add-an-entity-tooa-table"></a><span data-ttu-id="1bb8e-139">Bir varlık tooa tablo ekleme</span><span class="sxs-lookup"><span data-stu-id="1bb8e-139">Add an entity tooa table</span></span>
<span data-ttu-id="1bb8e-140">bir varlık tooadd ilk varlık özelliklerinizi tanımlayan bir nesne oluşturun.</span><span class="sxs-lookup"><span data-stu-id="1bb8e-140">tooadd an entity, first create an object that defines your entity properties.</span></span> <span data-ttu-id="1bb8e-141">Tüm varlıklar içermesi gereken bir **PartitionKey** ve **RowKey**, hello varlık için benzersiz tanımlayıcı olduğu.</span><span class="sxs-lookup"><span data-stu-id="1bb8e-141">All entities must contain a **PartitionKey** and **RowKey**, which are unique identifiers for hello entity.</span></span>

* <span data-ttu-id="1bb8e-142">**PartitionKey** -hello varlık depolanan hello bölüm belirler</span><span class="sxs-lookup"><span data-stu-id="1bb8e-142">**PartitionKey** - determines hello partition that hello entity is stored in</span></span>
* <span data-ttu-id="1bb8e-143">**RowKey** - benzersiz şekilde hello varlığın hello bölüm içinde tanımlar</span><span class="sxs-lookup"><span data-stu-id="1bb8e-143">**RowKey** - uniquely identifies hello entity within hello partition</span></span>

<span data-ttu-id="1bb8e-144">Her ikisi de **PartitionKey** ve **RowKey** dize değerleri olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="1bb8e-144">Both **PartitionKey** and **RowKey** must be string values.</span></span> <span data-ttu-id="1bb8e-145">Daha fazla bilgi için bkz: [anlama hello tablo hizmeti veri modelini](http://msdn.microsoft.com/library/azure/dd179338.aspx).</span><span class="sxs-lookup"><span data-stu-id="1bb8e-145">For more information, see [Understanding hello Table Service Data Model](http://msdn.microsoft.com/library/azure/dd179338.aspx).</span></span>

<span data-ttu-id="1bb8e-146">Merhaba, bir varlığın tanımlama örneği aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="1bb8e-146">hello following is an example of defining an entity.</span></span> <span data-ttu-id="1bb8e-147">Unutmayın **vade tarihi** bir türü olarak tanımlanmış **Edm.DateTime**.</span><span class="sxs-lookup"><span data-stu-id="1bb8e-147">Note that **dueDate** is defined as a type of **Edm.DateTime**.</span></span> <span data-ttu-id="1bb8e-148">Belirten hello türü isteğe bağlıdır ve türleri çıkarımı yapılan belirtilen yoksa.</span><span class="sxs-lookup"><span data-stu-id="1bb8e-148">Specifying hello type is optional, and types will be inferred if not specified.</span></span>

```nodejs
var task = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '1'},
  description: {'_':'take out hello trash'},
  dueDate: {'_':new Date(2015, 6, 20), '$':'Edm.DateTime'}
};
```

> [!NOTE]
> <span data-ttu-id="1bb8e-149">Ayrıca bir **zaman damgası** bir varlık eklendiğinde veya, Azure tarafından ayarlanan her kayıt için alan.</span><span class="sxs-lookup"><span data-stu-id="1bb8e-149">There is also a **Timestamp** field for each record, which is set by Azure when an entity is inserted or updated.</span></span>
>
>

<span data-ttu-id="1bb8e-150">Merhaba de kullanabilirsiniz **entityGenerator** toocreate varlıklar.</span><span class="sxs-lookup"><span data-stu-id="1bb8e-150">You can also use hello **entityGenerator** toocreate entities.</span></span> <span data-ttu-id="1bb8e-151">Merhaba aşağıdaki örnekte oluşturur hello hello kullanarak aynı görev varlık **entityGenerator**.</span><span class="sxs-lookup"><span data-stu-id="1bb8e-151">hello following example creates hello same task entity using hello **entityGenerator**.</span></span>

```nodejs
var entGen = azure.TableUtilities.entityGenerator;
var task = {
  PartitionKey: entGen.String('hometasks'),
  RowKey: entGen.String('1'),
  description: entGen.String('take out hello trash'),
  dueDate: entGen.DateTime(new Date(Date.UTC(2015, 6, 20))),
};
```

<span data-ttu-id="1bb8e-152">bir varlık tooyour tablosu tooadd geçirmek hello varlık nesnesi toohello **insertEntity** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="1bb8e-152">tooadd an entity tooyour table, pass hello entity object toohello **insertEntity** method.</span></span>

```nodejs
tableSvc.insertEntity('mytable',task, function (error, result, response) {
  if(!error){
    // Entity inserted
  }
});
```

<span data-ttu-id="1bb8e-153">Merhaba işlemi başarılı olursa `result` hello içerecek [ETag](http://en.wikipedia.org/wiki/HTTP_ETag) kayda Merhaba eklenen ve `response` hello işlemiyle ilgili bilgi içerir.</span><span class="sxs-lookup"><span data-stu-id="1bb8e-153">If hello operation is successful, `result` will contain hello [ETag](http://en.wikipedia.org/wiki/HTTP_ETag) of hello inserted record and `response` will contain information about hello operation.</span></span>

<span data-ttu-id="1bb8e-154">Örnek yanıt:</span><span class="sxs-lookup"><span data-stu-id="1bb8e-154">Example response:</span></span>

```nodejs
{ '.metadata': { etag: 'W/"datetime\'2015-02-25T01%3A22%3A22.5Z\'"' } }
```

> [!NOTE]
> <span data-ttu-id="1bb8e-155">Varsayılan olarak, **insertEntity** hello bir parçası olarak eklenen hello varlık döndürmüyor `response` bilgi.</span><span class="sxs-lookup"><span data-stu-id="1bb8e-155">By default, **insertEntity** does not return hello inserted entity as part of hello `response` information.</span></span> <span data-ttu-id="1bb8e-156">Planı bu varlık üzerinde başka işlemler gerçekleştirmek ya da toocache hello bilgi istiyor hello bir parçası olarak döndürdüğü yararlı toohave olabilir `result`.</span><span class="sxs-lookup"><span data-stu-id="1bb8e-156">If you plan on performing other operations on this entity, or wish toocache hello information, it can be useful toohave it returned as part of hello `result`.</span></span> <span data-ttu-id="1bb8e-157">Etkinleştirerek bunu yapabilirsiniz **echoContent** gibi:</span><span class="sxs-lookup"><span data-stu-id="1bb8e-157">You can do this by enabling **echoContent** as follows:</span></span>
>
> `tableSvc.insertEntity('mytable', task, {echoContent: true}, function (error, result, response) {...}`
>
>

## <a name="update-an-entity"></a><span data-ttu-id="1bb8e-158">Bir varlığı güncelleştirir</span><span class="sxs-lookup"><span data-stu-id="1bb8e-158">Update an entity</span></span>
<span data-ttu-id="1bb8e-159">Var olan bir varlığı birden çok yöntemleri kullanılabilir tooupdate vardır:</span><span class="sxs-lookup"><span data-stu-id="1bb8e-159">There are multiple methods available tooupdate an existing entity:</span></span>

* <span data-ttu-id="1bb8e-160">**replaceEntity** -değiştirme tarafından var olan bir varlığı güncelleştirir</span><span class="sxs-lookup"><span data-stu-id="1bb8e-160">**replaceEntity** - updates an existing entity by replacing it</span></span>
* <span data-ttu-id="1bb8e-161">**mergeEntity** -hello varolan varlık kümesine yeni özellik değerlerinin birleştirerek var olan bir varlığı güncelleştirir</span><span class="sxs-lookup"><span data-stu-id="1bb8e-161">**mergeEntity** - updates an existing entity by merging new property values into hello existing entity</span></span>
* <span data-ttu-id="1bb8e-162">**insertOrReplaceEntity** -değiştirme tarafından var olan bir varlığı güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="1bb8e-162">**insertOrReplaceEntity** - updates an existing entity by replacing it.</span></span> <span data-ttu-id="1bb8e-163">Hiçbir varlık varsa, yeni bir tane eklenir</span><span class="sxs-lookup"><span data-stu-id="1bb8e-163">If no entity exists, a new one will be inserted</span></span>
* <span data-ttu-id="1bb8e-164">**insertOrMergeEntity** -hello varolan içine yeni özellik değerlerinin birleştirerek var olan bir varlığı güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="1bb8e-164">**insertOrMergeEntity** - updates an existing entity by merging new property values into hello existing.</span></span> <span data-ttu-id="1bb8e-165">Hiçbir varlık varsa, yeni bir tane eklenir</span><span class="sxs-lookup"><span data-stu-id="1bb8e-165">If no entity exists, a new one will be inserted</span></span>

<span data-ttu-id="1bb8e-166">Merhaba aşağıdaki örneği kullanarak bir varlık güncelleştirme gösterir **replaceEntity**:</span><span class="sxs-lookup"><span data-stu-id="1bb8e-166">hello following example demonstrates updating an entity using **replaceEntity**:</span></span>

```nodejs
tableSvc.replaceEntity('mytable', updatedTask, function(error, result, response){
  if(!error) {
    // Entity updated
  }
});
```

> [!NOTE]
> <span data-ttu-id="1bb8e-167">Güncelleştirilmekte hello veri daha önce başka bir işlem tarafından değiştirilmiş, varsayılan olarak, bir varlık güncelleştirme toosee denetlemez.</span><span class="sxs-lookup"><span data-stu-id="1bb8e-167">By default, updating an entity does not check toosee if hello data being updated has previously been modified by another process.</span></span> <span data-ttu-id="1bb8e-168">toosupport eşzamanlı güncelleştirmeleri:</span><span class="sxs-lookup"><span data-stu-id="1bb8e-168">toosupport concurrent updates:</span></span>
>
> 1. <span data-ttu-id="1bb8e-169">Merhaba güncelleştirilmekte hello nesnesinin ETag alın.</span><span class="sxs-lookup"><span data-stu-id="1bb8e-169">Get hello ETag of hello object being updated.</span></span> <span data-ttu-id="1bb8e-170">Bu hello bir parçası olarak döndürülür `response` tüm ilgili varlık işlemi için ve alınabilir `response['.metadata'].etag`.</span><span class="sxs-lookup"><span data-stu-id="1bb8e-170">This is returned as part of hello `response` for any entity-related operation and can be retrieved through `response['.metadata'].etag`.</span></span>
> 2. <span data-ttu-id="1bb8e-171">Bir varlık, bir güncelleştirme işlemi gerçekleştirilirken eklediğinizde hello ETag bilgi toohello yeni varlık daha önce alındı.</span><span class="sxs-lookup"><span data-stu-id="1bb8e-171">When performing an update operation on an entity, add hello ETag information previously retrieved toohello new entity.</span></span> <span data-ttu-id="1bb8e-172">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="1bb8e-172">For example:</span></span>
>
>       <span data-ttu-id="1bb8e-173">entity2 ['.metadata'] .etag currentEtag; =</span><span class="sxs-lookup"><span data-stu-id="1bb8e-173">entity2['.metadata'].etag = currentEtag;</span></span>
> 3. <span data-ttu-id="1bb8e-174">Merhaba güncelleştirme işlemini gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="1bb8e-174">Perform hello update operation.</span></span> <span data-ttu-id="1bb8e-175">Uygulamanızın, başka bir örneği gibi hello ETag değeri, alınan bu yana hello varlık güncellendiyse bir `error` hello istekte belirtilen hello güncelleştirme koşulu karşılanmadı belirten döndürülür.</span><span class="sxs-lookup"><span data-stu-id="1bb8e-175">If hello entity has been modified since you retrieved hello ETag value, such as another instance of your application, an `error` will be returned stating that hello update condition specified in hello request was not satisfied.</span></span>
>
>

<span data-ttu-id="1bb8e-176">İle **replaceEntity** ve **mergeEntity**, güncelleştirilen hello varlık yoksa hello güncelleştirme işlemi başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="1bb8e-176">With **replaceEntity** and **mergeEntity**, if hello entity that is being updated doesn't exist, then hello update operation will fail.</span></span> <span data-ttu-id="1bb8e-177">Bu nedenle olup zaten var. bakılmaksızın bir varlık toostore istiyorsanız, kullanmak **insertOrReplaceEntity** veya **insertOrMergeEntity**.</span><span class="sxs-lookup"><span data-stu-id="1bb8e-177">Therefore if you wish toostore an entity regardless of whether it already exists, use **insertOrReplaceEntity** or **insertOrMergeEntity**.</span></span>

<span data-ttu-id="1bb8e-178">Merhaba `result` başarılı güncelleştirmesi işlemleri hello içerecek **Etag** Merhaba varlık güncelleştirildi.</span><span class="sxs-lookup"><span data-stu-id="1bb8e-178">hello `result` for successful update operations will contain hello **Etag** of hello updated entity.</span></span>

## <a name="work-with-groups-of-entities"></a><span data-ttu-id="1bb8e-179">Varlıkları gruplarıyla çalışma</span><span class="sxs-lookup"><span data-stu-id="1bb8e-179">Work with groups of entities</span></span>
<span data-ttu-id="1bb8e-180">Bazen algılama toosubmit birden çok operations birlikte bir toplu tooensure atomik hello sunucusu tarafından işleme kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="1bb8e-180">Sometimes it makes sense toosubmit multiple operations together in a batch tooensure atomic processing by hello server.</span></span> <span data-ttu-id="1bb8e-181">kullanan, hello tooaccomplish **TableBatch** sınıf toocreate toplu ve sonra hello **executeBatch** yöntemi **TableService** tooperform hello toplu işlemler.</span><span class="sxs-lookup"><span data-stu-id="1bb8e-181">tooaccomplish that, use hello **TableBatch** class toocreate a batch, and then use hello **executeBatch** method of **TableService** tooperform hello batched operations.</span></span>

 <span data-ttu-id="1bb8e-182">bir toplu işte iki varlık gönderme aşağıdaki örneğine hello gösterir:</span><span class="sxs-lookup"><span data-stu-id="1bb8e-182">hello following example demonstrates submitting two entities in a batch:</span></span>

```nodejs
var task1 = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '1'},
  description: {'_':'Take out hello trash'},
  dueDate: {'_':new Date(2015, 6, 20)}
};
var task2 = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '2'},
  description: {'_':'Wash hello dishes'},
  dueDate: {'_':new Date(2015, 6, 20)}
};

var batch = new azure.TableBatch();

batch.insertEntity(task1, {echoContent: true});
batch.insertEntity(task2, {echoContent: true});

tableSvc.executeBatch('mytable', batch, function (error, result, response) {
  if(!error) {
    // Batch completed
  }
});
```

<span data-ttu-id="1bb8e-183">Başarılı toplu işlemler için `result` hello toplu her işlem için bilgiler içerir.</span><span class="sxs-lookup"><span data-stu-id="1bb8e-183">For successful batch operations, `result` will contain information for each operation in hello batch.</span></span>

### <a name="work-with-batched-operations"></a><span data-ttu-id="1bb8e-184">Toplu işlemleri ile çalışma</span><span class="sxs-lookup"><span data-stu-id="1bb8e-184">Work with batched operations</span></span>
<span data-ttu-id="1bb8e-185">Operations eklenen tooa toplu hello görüntüleyerek sahip denetlenir `operations` özelliği.</span><span class="sxs-lookup"><span data-stu-id="1bb8e-185">Operations added tooa batch can be inspected by viewing hello `operations` property.</span></span> <span data-ttu-id="1bb8e-186">İşlemlerle yöntemleri toowork aşağıdaki hello de kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="1bb8e-186">You can also use hello following methods toowork with operations:</span></span>

* <span data-ttu-id="1bb8e-187">**Clear** -tüm işlemler bir batch temizler</span><span class="sxs-lookup"><span data-stu-id="1bb8e-187">**clear** - clears all operations from a batch</span></span>
* <span data-ttu-id="1bb8e-188">**getOperations** -hello toplu işlemindeki bir işlem alır</span><span class="sxs-lookup"><span data-stu-id="1bb8e-188">**getOperations** - gets an operation from hello batch</span></span>
* <span data-ttu-id="1bb8e-189">**hasOperations** -hello toplu işlemler varsa true değerini döndürür</span><span class="sxs-lookup"><span data-stu-id="1bb8e-189">**hasOperations** - returns true if hello batch contains operations</span></span>
* <span data-ttu-id="1bb8e-190">**removeOperations** -bir işlem kaldırır</span><span class="sxs-lookup"><span data-stu-id="1bb8e-190">**removeOperations** - removes an operation</span></span>
* <span data-ttu-id="1bb8e-191">**boyutu** -döndürür hello hello toplu işlemi sayısı</span><span class="sxs-lookup"><span data-stu-id="1bb8e-191">**size** - returns hello number of operations in hello batch</span></span>

## <a name="retrieve-an-entity-by-key"></a><span data-ttu-id="1bb8e-192">Anahtara göre bir varlık alma</span><span class="sxs-lookup"><span data-stu-id="1bb8e-192">Retrieve an entity by key</span></span>
<span data-ttu-id="1bb8e-193">belirli bir varlık üzerinde hello dayalı tooreturn **PartitionKey** ve **RowKey**, hello kullan **retrieveEntity** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="1bb8e-193">tooreturn a specific entity based on hello **PartitionKey** and **RowKey**, use hello **retrieveEntity** method.</span></span>

```nodejs
tableSvc.retrieveEntity('mytable', 'hometasks', '1', function(error, result, response){
  if(!error){
    // result contains hello entity
  }
});
```

<span data-ttu-id="1bb8e-194">Bu işlem tamamlandıktan sonra `result` hello varlık içerir.</span><span class="sxs-lookup"><span data-stu-id="1bb8e-194">Once this operation is complete, `result` will contain hello entity.</span></span>

## <a name="query-a-set-of-entities"></a><span data-ttu-id="1bb8e-195">Varlık kümesi sorgulama</span><span class="sxs-lookup"><span data-stu-id="1bb8e-195">Query a set of entities</span></span>
<span data-ttu-id="1bb8e-196">tooquery bir tablo kullanmak hello **TableQuery** toobuild yan tümceleri aşağıdaki hello kullanarak bir sorgu ifadesi yukarı nesnesi:</span><span class="sxs-lookup"><span data-stu-id="1bb8e-196">tooquery a table, use hello **TableQuery** object toobuild up a query expression using hello following clauses:</span></span>

* <span data-ttu-id="1bb8e-197">**seçin** -hello alanları toobe hello sorgudan döndürülen</span><span class="sxs-lookup"><span data-stu-id="1bb8e-197">**select** - hello fields toobe returned from hello query</span></span>
* <span data-ttu-id="1bb8e-198">**Burada** - hello nerede yan tümcesi</span><span class="sxs-lookup"><span data-stu-id="1bb8e-198">**where** - hello where clause</span></span>

  * <span data-ttu-id="1bb8e-199">**ve** - bir `and` koşul</span><span class="sxs-lookup"><span data-stu-id="1bb8e-199">**and** - an `and` where condition</span></span>
  * <span data-ttu-id="1bb8e-200">**veya** - bir `or` koşul</span><span class="sxs-lookup"><span data-stu-id="1bb8e-200">**or** - an `or` where condition</span></span>
* <span data-ttu-id="1bb8e-201">**üst** -hello öğeleri toofetch sayısı</span><span class="sxs-lookup"><span data-stu-id="1bb8e-201">**top** - hello number of items toofetch</span></span>

<span data-ttu-id="1bb8e-202">Merhaba aşağıdaki örnek ilk beş öğelerinin bir PartitionKey ile 'hometasks' hello döndürülecek bir sorgu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="1bb8e-202">hello following example builds a query that will return hello top five items with a PartitionKey of 'hometasks'.</span></span>

```nodejs
var query = new azure.TableQuery()
  .top(5)
  .where('PartitionKey eq ?', 'hometasks');
```

<span data-ttu-id="1bb8e-203">Bu yana **seçin** , tüm alanları döndürülecek kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="1bb8e-203">Since **select** is not used, all fields will be returned.</span></span> <span data-ttu-id="1bb8e-204">Tablo, kullanım tooperform hello sorgusu **queryEntities**.</span><span class="sxs-lookup"><span data-stu-id="1bb8e-204">tooperform hello query against a table, use **queryEntities**.</span></span> <span data-ttu-id="1bb8e-205">Merhaba aşağıdaki örnekte bu 'mytable' sorgu tooreturn varlıklardan kullanır.</span><span class="sxs-lookup"><span data-stu-id="1bb8e-205">hello following example uses this query tooreturn entities from 'mytable'.</span></span>

```nodejs
tableSvc.queryEntities('mytable',query, null, function(error, result, response) {
  if(!error) {
    // query was successful
  }
});
```

<span data-ttu-id="1bb8e-206">Başarılı olursa, `result.entries` hello sorguyla eşleşen varlıkları dizisi içerir.</span><span class="sxs-lookup"><span data-stu-id="1bb8e-206">If successful, `result.entries` will contain an array of entities that match hello query.</span></span> <span data-ttu-id="1bb8e-207">Merhaba sorgu oluşturulamıyor tooreturn ise tüm varlıkları `result.continuationToken` olmayan olacaktır*null* ve üçüncü parametresi, hello olarak kullanılan **queryEntities** tooretrieve daha fazla sonuç.</span><span class="sxs-lookup"><span data-stu-id="1bb8e-207">If hello query was unable tooreturn all entities, `result.continuationToken` will be non-*null* and can be used as hello third parameter of **queryEntities** tooretrieve more results.</span></span> <span data-ttu-id="1bb8e-208">Merhaba ilk sorguyu *null* hello üçüncü parametre için.</span><span class="sxs-lookup"><span data-stu-id="1bb8e-208">For hello initial query, use *null* for hello third parameter.</span></span>

### <a name="query-a-subset-of-entity-properties"></a><span data-ttu-id="1bb8e-209">Giriş özellikleri alt kümesi sorgulama</span><span class="sxs-lookup"><span data-stu-id="1bb8e-209">Query a subset of entity properties</span></span>
<span data-ttu-id="1bb8e-210">Bir sorgu tooa tablosu yalnızca birkaç alanları bir varlıktan alabilir.</span><span class="sxs-lookup"><span data-stu-id="1bb8e-210">A query tooa table can retrieve just a few fields from an entity.</span></span>
<span data-ttu-id="1bb8e-211">Bu, bant genişliğini azaltır ve özellikle büyük varlıklar için sorgu performansını iyileştirebilir.</span><span class="sxs-lookup"><span data-stu-id="1bb8e-211">This reduces bandwidth and can improve query performance, especially for large entities.</span></span> <span data-ttu-id="1bb8e-212">Kullanım hello **seçin** hello alanları toobe yan tümcesi ve geçişi hello adlarını döndürdü.</span><span class="sxs-lookup"><span data-stu-id="1bb8e-212">Use hello **select** clause and pass hello names of hello fields toobe returned.</span></span> <span data-ttu-id="1bb8e-213">Örneğin, hello aşağıdaki sorguyu yalnızca hello döndürülecek **açıklama** ve **vade tarihi** alanları.</span><span class="sxs-lookup"><span data-stu-id="1bb8e-213">For example, hello following query will return only hello **description** and **dueDate** fields.</span></span>

```nodejs
var query = new azure.TableQuery()
  .select(['description', 'dueDate'])
  .top(5)
  .where('PartitionKey eq ?', 'hometasks');
```

## <a name="delete-an-entity"></a><span data-ttu-id="1bb8e-214">Bir varlığı silme</span><span class="sxs-lookup"><span data-stu-id="1bb8e-214">Delete an entity</span></span>
<span data-ttu-id="1bb8e-215">Bir varlığın bölüm ve satır anahtarını kullanarak silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1bb8e-215">You can delete an entity using its partition and row keys.</span></span> <span data-ttu-id="1bb8e-216">Bu örnekte, hello **task1** nesnesini içeren hello **RowKey** ve **PartitionKey** silinmiş hello varlık toobe değerleri.</span><span class="sxs-lookup"><span data-stu-id="1bb8e-216">In this example, hello **task1** object contains hello **RowKey** and **PartitionKey** values of hello entity toobe deleted.</span></span> <span data-ttu-id="1bb8e-217">Merhaba nesne toohello geçirilen sonra **deleteEntity** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="1bb8e-217">Then hello object is passed toohello **deleteEntity** method.</span></span>

```nodejs
var task = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '1'}
};

tableSvc.deleteEntity('mytable', task, function(error, response){
  if(!error) {
    // Entity deleted
  }
});
```

> [!NOTE]
> <span data-ttu-id="1bb8e-218">Öğe, öğe hello tooensure silme başka bir işlem tarafından değiştirilip değiştirilmediğini Etag'ler kullanmayı göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="1bb8e-218">Consider using ETags when deleting items, tooensure that hello item hasn't been modified by another process.</span></span> <span data-ttu-id="1bb8e-219">Bkz: [bir varlığı güncelleştirmek](#update-an-entity) Etag'ler kullanma hakkında bilgi için.</span><span class="sxs-lookup"><span data-stu-id="1bb8e-219">See [Update an entity](#update-an-entity) for information on using ETags.</span></span>
>
>

## <a name="delete-a-table"></a><span data-ttu-id="1bb8e-220">Bir tablo silme</span><span class="sxs-lookup"><span data-stu-id="1bb8e-220">Delete a table</span></span>
<span data-ttu-id="1bb8e-221">koddan hello bir depolama hesabından bir tablo siler.</span><span class="sxs-lookup"><span data-stu-id="1bb8e-221">hello following code deletes a table from a storage account.</span></span>

```nodejs
tableSvc.deleteTable('mytable', function(error, response){
    if(!error){
        // Table deleted
    }
});
```

<span data-ttu-id="1bb8e-222">Merhaba tablo var olup olmadığından emin değilseniz kullanmak **deleteTableIfExists**.</span><span class="sxs-lookup"><span data-stu-id="1bb8e-222">If you are uncertain whether hello table exists, use **deleteTableIfExists**.</span></span>

## <a name="use-continuation-tokens"></a><span data-ttu-id="1bb8e-223">Devamlılık belirteçleri kullanın</span><span class="sxs-lookup"><span data-stu-id="1bb8e-223">Use continuation tokens</span></span>
<span data-ttu-id="1bb8e-224">İçin devamlılık belirteci tablolar için sonuçları büyük miktarlarda sorgulanırken arayın.</span><span class="sxs-lookup"><span data-stu-id="1bb8e-224">When you are querying tables for large amounts of results, look for continuation tokens.</span></span> <span data-ttu-id="1bb8e-225">Sorgunuz için bir devamlılık belirteci mevcut olduğunda, toorecognize derleme değil, farkına varmazsınız olduğunu kullanılabilir büyük miktarlarda verinin olabilir.</span><span class="sxs-lookup"><span data-stu-id="1bb8e-225">There may be large amounts of data available for your query that you might not realize if you do not build toorecognize when a continuation token is present.</span></span>

<span data-ttu-id="1bb8e-226">Merhaba sonuçları nesne döndürülen varlık kümeleri sorgulama sırasında bir `continuationToken` böyle bir belirteç bulunduğunda özelliği.</span><span class="sxs-lookup"><span data-stu-id="1bb8e-226">hello results object returned during querying entities sets a `continuationToken` property when such a token is present.</span></span> <span data-ttu-id="1bb8e-227">Bu işlemi daha sonra bir sorgu toocontinue toomove hello bölüm ve tablo varlıkları arasında gerçekleştirirken da kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1bb8e-227">You can then use this when performing a query toocontinue toomove across hello partition and table entities.</span></span>

<span data-ttu-id="1bb8e-228">Sorgularken, continuationToken parametresi hello sorgu nesne örneği ile Merhaba geri çağırma işlevi arasında sağlanabilir:</span><span class="sxs-lookup"><span data-stu-id="1bb8e-228">When querying, a continuationToken parameter may be provided between hello query object instance and hello callback function:</span></span>

```nodejs
var nextContinuationToken = null;
dc.table.queryEntities(tableName,
    query,
    nextContinuationToken,
    function (error, results) {
        if (error) throw error;

        // iterate through results.entries with results

        if (results.continuationToken) {
            nextContinuationToken = results.continuationToken;
        }

    });
```

<span data-ttu-id="1bb8e-229">Merhaba inceleyin, `continuationToken` nesnesi bulacaksınız özellikler gibi `nextPartitionKey`, `nextRowKey` ve `targetLocation`, tüm hello sonuçları aracılığıyla kullanılan tooiterate olabilir.</span><span class="sxs-lookup"><span data-stu-id="1bb8e-229">If you inspect hello `continuationToken` object, you will find properties such as `nextPartitionKey`, `nextRowKey` and `targetLocation`, which can be used tooiterate through all hello results.</span></span>

<span data-ttu-id="1bb8e-230">Devamlılık örnek hello Azure depolama Node.js bağlantıların github'da içinde yok.</span><span class="sxs-lookup"><span data-stu-id="1bb8e-230">There is also a continuation sample within hello Azure Storage Node.js repo on GitHub.</span></span> <span data-ttu-id="1bb8e-231">Ara `examples/samples/continuationsample.js`.</span><span class="sxs-lookup"><span data-stu-id="1bb8e-231">Look for `examples/samples/continuationsample.js`.</span></span>

## <a name="work-with-shared-access-signatures"></a><span data-ttu-id="1bb8e-232">Paylaşılan erişim imzaları ile çalışma</span><span class="sxs-lookup"><span data-stu-id="1bb8e-232">Work with shared access signatures</span></span>
<span data-ttu-id="1bb8e-233">Paylaşılan erişim imzaları (SAS) depolama hesabı adı veya anahtarları sağlamadan güvenli şekilde tooprovide ayrıntılı erişim tootables ' dir.</span><span class="sxs-lookup"><span data-stu-id="1bb8e-233">Shared access signatures (SAS) are a secure way tooprovide granular access tootables without providing your storage account name or keys.</span></span> <span data-ttu-id="1bb8e-234">SAS genellikle bir mobil uygulama tooquery kayıtları izin verme gibi sınırlı kullanılan tooprovide erişim tooyour, verilerdir.</span><span class="sxs-lookup"><span data-stu-id="1bb8e-234">SAS are often used tooprovide limited access tooyour data, such as allowing a mobile app tooquery records.</span></span>

<span data-ttu-id="1bb8e-235">Bir bulut tabanlı hizmeti gibi güvenilir bir uygulama hello kullanarak bir SAS oluşturur **generateSharedAccessSignature** Merhaba, **TableService**, tooan sağlar ve güvenilmeyen veya yarı güvenilir uygulama Mobil uygulama gibi.</span><span class="sxs-lookup"><span data-stu-id="1bb8e-235">A trusted application such as a cloud-based service generates a SAS using hello **generateSharedAccessSignature** of hello **TableService**, and provides it tooan untrusted or semi-trusted application such as a mobile app.</span></span> <span data-ttu-id="1bb8e-236">Hello SAS hello başlangıç tanımlayan bir ilke ve bitiş tarihleri sırasında hangi hello SAS geçerlidir kullanılarak oluşturulan, aynı zamanda erişim düzeyi verilen toohello SAS sahibi hello.</span><span class="sxs-lookup"><span data-stu-id="1bb8e-236">hello SAS is generated using a policy, which describes hello start and end dates during which hello SAS is valid, as well as hello access level granted toohello SAS holder.</span></span>

<span data-ttu-id="1bb8e-237">Merhaba aşağıdaki örnek hello SAS sahibi tooquery ('r') hello tablo izin veren yeni bir paylaşılan erişim ilkesi oluşturur ve 100 dakika hello zaman oluşturulduktan sonra süresi dolar.</span><span class="sxs-lookup"><span data-stu-id="1bb8e-237">hello following example generates a new shared access policy that will allow hello SAS holder tooquery ('r') hello table, and expires 100 minutes after hello time it is created.</span></span>

```nodejs
var startDate = new Date();
var expiryDate = new Date(startDate);
expiryDate.setMinutes(startDate.getMinutes() + 100);
startDate.setMinutes(startDate.getMinutes() - 100);

var sharedAccessPolicy = {
  AccessPolicy: {
    Permissions: azure.TableUtilities.SharedAccessPermissions.QUERY,
    Start: startDate,
    Expiry: expiryDate
  },
};

var tableSAS = tableSvc.generateSharedAccessSignature('mytable', sharedAccessPolicy);
var host = tableSvc.host;
```

<span data-ttu-id="1bb8e-238">Gerekli olduğu gibi aynı zamanda, hello SAS sahibi tooaccess hello tablo çalıştığında sağlanan hello ana bilgisayar bilgilerini olması gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="1bb8e-238">Note that hello host information must be provided also, as it is required when hello SAS holder attempts tooaccess hello table.</span></span>

<span data-ttu-id="1bb8e-239">ile SAS kullanır hello sonra istemci uygulaması Hello **TableServiceWithSAS** hello tabloda tooperform işlemleri.</span><span class="sxs-lookup"><span data-stu-id="1bb8e-239">hello client application then uses hello SAS with **TableServiceWithSAS** tooperform operations against hello table.</span></span> <span data-ttu-id="1bb8e-240">Aşağıdaki örnek hello toohello tablo bağlanır ve bir sorgu gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="1bb8e-240">hello following example connects toohello table and performs a query.</span></span>

```nodejs
var sharedTableService = azure.createTableServiceWithSas(host, tableSAS);
var query = azure.TableQuery()
  .where('PartitionKey eq ?', 'hometasks');

sharedTableService.queryEntities(query, null, function(error, result, response) {
  if(!error) {
    // result contains hello entities
  }
});
```

<span data-ttu-id="1bb8e-241">Güncelleştirme veya silme varlıklar tooinsert girişiminde yapılmışsa hello SAS yalnızca sorgu erişimle oluşturulmasının üzerinden, bir hata döndürülür.</span><span class="sxs-lookup"><span data-stu-id="1bb8e-241">Since hello SAS was generated with only query access, if an attempt were made tooinsert, update, or delete entities, an error would be returned.</span></span>

### <a name="access-control-lists"></a><span data-ttu-id="1bb8e-242">Erişim denetim listeleri</span><span class="sxs-lookup"><span data-stu-id="1bb8e-242">Access Control Lists</span></span>
<span data-ttu-id="1bb8e-243">Erişim denetimi listesi (ACL) tooset hello erişim ilkesi için bir SAS de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1bb8e-243">You can also use an Access Control List (ACL) tooset hello access policy for a SAS.</span></span> <span data-ttu-id="1bb8e-244">Birden çok istemcileri tooaccess hello tablo tooallow istiyor, ancak her istemci için farklı erişim ilkeleri sağlar, bu yararlı olur.</span><span class="sxs-lookup"><span data-stu-id="1bb8e-244">This is useful if you wish tooallow multiple clients tooaccess hello table, but provide different access policies for each client.</span></span>

<span data-ttu-id="1bb8e-245">Bir ACL her ilkesiyle ilişkili bir Kimliğe sahip bir dizi erişim ilkeleri kullanılarak uygulanır.</span><span class="sxs-lookup"><span data-stu-id="1bb8e-245">An ACL is implemented using an array of access policies, with an ID associated with each policy.</span></span> <span data-ttu-id="1bb8e-246">iki ilke, 'User1' diğeri için 'kullanıcı2' hello aşağıdaki örneğine tanımlar:</span><span class="sxs-lookup"><span data-stu-id="1bb8e-246">hello following example defines two policies, one for 'user1' and one for 'user2':</span></span>

```nodejs
var sharedAccessPolicy = {
  user1: {
    Permissions: azure.TableUtilities.SharedAccessPermissions.QUERY,
    Start: startDate,
    Expiry: expiryDate
  },
  user2: {
    Permissions: azure.TableUtilities.SharedAccessPermissions.ADD,
    Start: startDate,
    Expiry: expiryDate
  }
};
```

<span data-ttu-id="1bb8e-247">Örnek alır aşağıdaki hello hello hello geçerli ACL'si **hometasks** tablo ve hello yeni ilkeleri kullanılarak ekler **setTableAcl**.</span><span class="sxs-lookup"><span data-stu-id="1bb8e-247">hello following example gets hello current ACL for hello **hometasks** table, and then adds hello new policies using **setTableAcl**.</span></span> <span data-ttu-id="1bb8e-248">Bu yaklaşım sağlar:</span><span class="sxs-lookup"><span data-stu-id="1bb8e-248">This approach allows:</span></span>

```nodejs
var extend = require('extend');
tableSvc.getTableAcl('hometasks', function(error, result, response) {
if(!error){
    var newSignedIdentifiers = extend(true, result.signedIdentifiers, sharedAccessPolicy);
    tableSvc.setTableAcl('hometasks', newSignedIdentifiers, function(error, result, response){
      if(!error){
        // ACL set
      }
    });
  }
});
```

<span data-ttu-id="1bb8e-249">Bir kez hello ACL ayarlayın, hello Kimliği İlkesi için temel bir SAS sonra oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1bb8e-249">Once hello ACL has been set, you can then create a SAS based on hello ID for a policy.</span></span> <span data-ttu-id="1bb8e-250">Aşağıdaki örnek hello 'kullanıcı2' için yeni bir SAS oluşturur:</span><span class="sxs-lookup"><span data-stu-id="1bb8e-250">hello following example creates a new SAS for 'user2':</span></span>

```nodejs
tableSAS = tableSvc.generateSharedAccessSignature('hometasks', { Id: 'user2' });
```

## <a name="next-steps"></a><span data-ttu-id="1bb8e-251">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1bb8e-251">Next steps</span></span>
<span data-ttu-id="1bb8e-252">Daha fazla bilgi için kaynakları aşağıdaki hello bakın.</span><span class="sxs-lookup"><span data-stu-id="1bb8e-252">For more information, see hello following resources.</span></span>

* <span data-ttu-id="1bb8e-253">[Microsoft Azure Storage Gezgini](../vs-azure-tools-storage-manage-with-storage-explorer.md) Windows, macOS ve Linux Azure Storage verilerle görsel olarak toowork sağlayan Microsoft boş bir tek başına uygulamadır.</span><span class="sxs-lookup"><span data-stu-id="1bb8e-253">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you toowork visually with Azure Storage data on Windows, macOS, and Linux.</span></span>
* <span data-ttu-id="1bb8e-254">[Azure depolama SDK'sı düğüm için](https://github.com/Azure/azure-storage-node) github'daki.</span><span class="sxs-lookup"><span data-stu-id="1bb8e-254">[Azure Storage SDK for Node](https://github.com/Azure/azure-storage-node) repository on GitHub.</span></span>
* [<span data-ttu-id="1bb8e-255">Node.js Geliştirici Merkezi</span><span class="sxs-lookup"><span data-stu-id="1bb8e-255">Node.js Developer Center</span></span>](/develop/nodejs/)
* [<span data-ttu-id="1bb8e-256">Oluşturma ve bir Node.js uygulaması tooan Azure Web sitesi dağıtma</span><span class="sxs-lookup"><span data-stu-id="1bb8e-256">Create and deploy a Node.js application tooan Azure website</span></span>](../app-service-web/app-service-web-get-started-nodejs.md)
