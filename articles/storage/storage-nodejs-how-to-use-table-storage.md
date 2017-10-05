---
title: Azure Table storage node.js'den kullanma | Microsoft Docs
description: "Bir NoSQL veri deposu olan Azure Table Storage kullanarak bulutta yapılandırılmış veri depolayın."
services: storage
documentationcenter: nodejs
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: fc2e33d2-c5da-4861-8503-53fdc25750de
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: f004408910aecc380e20f7da54dbd155d179aaa5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-azure-table-storage-from-nodejs"></a><span data-ttu-id="721b3-103">Node.js'den Azure Table storage kullanma</span><span class="sxs-lookup"><span data-stu-id="721b3-103">How to use Azure Table storage from Node.js</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a><span data-ttu-id="721b3-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="721b3-104">Overview</span></span>
<span data-ttu-id="721b3-105">Bu konu Azure tablo hizmetinde bir Node.js uygulaması kullanarak genel senaryolar gerçekleştirme gösterir.</span><span class="sxs-lookup"><span data-stu-id="721b3-105">This topic shows how to perform common scenarios using the Azure Table service in a Node.js application.</span></span>

<span data-ttu-id="721b3-106">Bu konuda kod örnekleri, bir Node.js uygulaması zaten olduğunu varsayın.</span><span class="sxs-lookup"><span data-stu-id="721b3-106">The code examples in this topic assume you already have a Node.js application.</span></span> <span data-ttu-id="721b3-107">Azure'da bir Node.js uygulaması oluşturma hakkında daha fazla bilgi için aşağıdaki konulardan birini bakın:</span><span class="sxs-lookup"><span data-stu-id="721b3-107">For information about how to create a Node.js application in Azure, see any of these topics:</span></span>

* [<span data-ttu-id="721b3-108">Azure App Service'te bir Node.js web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="721b3-108">Create a Node.js web app in Azure App Service</span></span>](../app-service-web/app-service-web-get-started-nodejs.md)
* [<span data-ttu-id="721b3-109">Derleme ve Webmatrix'i kullanarak Azure Node.js web uygulamasına dağıtma</span><span class="sxs-lookup"><span data-stu-id="721b3-109">Build and deploy a Node.js web app to Azure using WebMatrix</span></span>](../app-service-web/web-sites-nodejs-use-webmatrix.md)
* <span data-ttu-id="721b3-110">[Derleme ve Azure bulut hizmeti bir Node.js uygulamasını dağıtma](../cloud-services/cloud-services-nodejs-develop-deploy-app.md) (Windows PowerShell kullanarak)</span><span class="sxs-lookup"><span data-stu-id="721b3-110">[Build and deploy a Node.js application to an Azure Cloud Service](../cloud-services/cloud-services-nodejs-develop-deploy-app.md) (using Windows PowerShell)</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="configure-your-application-to-access-azure-storage"></a><span data-ttu-id="721b3-111">Azure depolama alanına erişmek için uygulamanızı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="721b3-111">Configure your application to access Azure Storage</span></span>
<span data-ttu-id="721b3-112">Azure Storage kullanmak için bir dizi depolama REST Hizmetleri ile iletişim kolaylık kitaplıkları içerir Node.js için Azure depolama SDK'sı gerekir.</span><span class="sxs-lookup"><span data-stu-id="721b3-112">To use Azure Storage, you need the Azure Storage SDK for Node.js, which includes a set of convenience libraries that communicate with the storage REST services.</span></span>

### <a name="use-node-package-manager-npm-to-install-the-package"></a><span data-ttu-id="721b3-113">Paketi yüklemek için düğüm paketi Yöneticisi (NPM) kullanın</span><span class="sxs-lookup"><span data-stu-id="721b3-113">Use Node Package Manager (NPM) to install the package</span></span>
1. <span data-ttu-id="721b3-114">Bir komut satırı arabirimi gibi kullandığınız **PowerShell** (Windows) **Terminal** (Mac) veya **Bash** (UNIX) ve uygulamanızı oluşturduğunuz klasöre gidin.</span><span class="sxs-lookup"><span data-stu-id="721b3-114">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix), and navigate to the folder where you created your application.</span></span>
2. <span data-ttu-id="721b3-115">Tür **npm yükleme azure depolama** komut penceresinde.</span><span class="sxs-lookup"><span data-stu-id="721b3-115">Type **npm install azure-storage** in the command window.</span></span> <span data-ttu-id="721b3-116">Komut çıktısı aşağıdaki örneğe benzer.</span><span class="sxs-lookup"><span data-stu-id="721b3-116">Output from the command is similar to the following example.</span></span>

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
3. <span data-ttu-id="721b3-117">El ile çalıştırabilirsiniz **ls** doğrulamak için komutu bir **düğümü\_modülleri** klasörü oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="721b3-117">You can manually run the **ls** command to verify that a **node\_modules** folder was created.</span></span> <span data-ttu-id="721b3-118">Bu klasör içinde bulacaksınız **azure depolama** depolama birimine erişmesi gereken kitaplıkları içeren paket.</span><span class="sxs-lookup"><span data-stu-id="721b3-118">Inside that folder you will find the **azure-storage** package, which contains the libraries you need to access storage.</span></span>

### <a name="import-the-package"></a><span data-ttu-id="721b3-119">Paket alma</span><span class="sxs-lookup"><span data-stu-id="721b3-119">Import the package</span></span>
<span data-ttu-id="721b3-120">En üst kısmına aşağıdaki kodu ekleyin **server.js** uygulamanızı dosyasında:</span><span class="sxs-lookup"><span data-stu-id="721b3-120">Add the following code to the top of the **server.js** file in your application:</span></span>

```nodejs
var azure = require('azure-storage');
```

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="721b3-121">Bir Azure depolama bağlantı kurma</span><span class="sxs-lookup"><span data-stu-id="721b3-121">Set up an Azure Storage connection</span></span>
<span data-ttu-id="721b3-122">Azure modülü AZURE ortam değişkenleri okur\_depolama\_HESABINI ve AZURE\_depolama\_erişim\_anahtar ya da AZURE\_depolama\_bağlantı\_Azure depolama hesabınıza bağlanmak için gerekli bilgileri DİZESİ.</span><span class="sxs-lookup"><span data-stu-id="721b3-122">The azure module will read the environment variables AZURE\_STORAGE\_ACCOUNT and AZURE\_STORAGE\_ACCESS\_KEY, or AZURE\_STORAGE\_CONNECTION\_STRING for information required to connect to your Azure storage account.</span></span> <span data-ttu-id="721b3-123">Bu ortam değişkenleri ayarlanmamışsa çağrılırken hesap bilgileri belirtmelisiniz **TableService**.</span><span class="sxs-lookup"><span data-stu-id="721b3-123">If these environment variables are not set, you must specify the account information when calling **TableService**.</span></span>

<span data-ttu-id="721b3-124">Ortam değişkenlerini ayarlama örnek için [Azure portal](https://portal.azure.com) bir Azure Web sitesi için bkz: [Azure tablo hizmeti kullanarak Node.js web uygulaması](../app-service-web/storage-nodejs-use-table-storage-web-site.md).</span><span class="sxs-lookup"><span data-stu-id="721b3-124">For an example of setting the environment variables in the [Azure portal](https://portal.azure.com) for an Azure Website, see [Node.js web app using the Azure Table Service](../app-service-web/storage-nodejs-use-table-storage-web-site.md).</span></span>

## <a name="create-a-table"></a><span data-ttu-id="721b3-125">Bir tablo oluşturma</span><span class="sxs-lookup"><span data-stu-id="721b3-125">Create a table</span></span>
<span data-ttu-id="721b3-126">Aşağıdaki kod oluşturur bir **TableService** nesne ve yeni bir tablo oluşturmak için kullanır.</span><span class="sxs-lookup"><span data-stu-id="721b3-126">The following code creates a **TableService** object and uses it to create a new table.</span></span> <span data-ttu-id="721b3-127">Aşağıdaki üst kısmına yakın ekleyin **server.js**.</span><span class="sxs-lookup"><span data-stu-id="721b3-127">Add the following near the top of **server.js**.</span></span>

```nodejs
var tableSvc = azure.createTableService();
```

<span data-ttu-id="721b3-128">Çağrı **createTableIfNotExists** zaten yoksa, belirtilen ada sahip yeni bir tablo oluşturur.</span><span class="sxs-lookup"><span data-stu-id="721b3-128">The call to **createTableIfNotExists** will create a new table with the specified name if it does not already exist.</span></span> <span data-ttu-id="721b3-129">Aşağıdaki örnek, zaten yoksa, 'mytable' adlı yeni bir tablo oluşturur:</span><span class="sxs-lookup"><span data-stu-id="721b3-129">The following example creates a new table named 'mytable' if it does not already exist:</span></span>

```nodejs
tableSvc.createTableIfNotExists('mytable', function(error, result, response){
  if(!error){
    // Table exists or created
  }
});
```

<span data-ttu-id="721b3-130">`result.created` Olacaktır `true` yeni bir tablo oluşturduysanız ve `false` tablo zaten varsa.</span><span class="sxs-lookup"><span data-stu-id="721b3-130">The `result.created` will be `true` if a new table is created, and `false` if the table already exists.</span></span> <span data-ttu-id="721b3-131">`response` İsteğiyle ilgili bilgileri içerir.</span><span class="sxs-lookup"><span data-stu-id="721b3-131">The `response` will contain information about the request.</span></span>

### <a name="filters"></a><span data-ttu-id="721b3-132">Filtreler</span><span class="sxs-lookup"><span data-stu-id="721b3-132">Filters</span></span>
<span data-ttu-id="721b3-133">İsteğe bağlı filtreleme işlemleri kullanarak gerçekleştirilen işlemler için uygulanabilir **TableService**.</span><span class="sxs-lookup"><span data-stu-id="721b3-133">Optional filtering operations can be applied to operations performed using **TableService**.</span></span> <span data-ttu-id="721b3-134">İşlemleri filtreleme içerebilir günlüğe kaydetme, otomatik olarak yeniden deneniyor, vs. İmzalı bir yöntem uygulayan nesneler filtreleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="721b3-134">Filtering operations can include logging, automatically retrying, etc. Filters are objects that implement a method with the signature:</span></span>

```nodejs
function handle (requestOptions, next)
```

<span data-ttu-id="721b3-135">İstek seçenekleri önişleme yaptıktan sonra yöntemi "İleri", çağırmak bir geri çağırma aşağıdaki imzayla geçirme gerekir:</span><span class="sxs-lookup"><span data-stu-id="721b3-135">After doing its preprocessing on the request options, the method needs to call "next", passing a callback with the following signature:</span></span>

```nodejs
function (returnObject, finalCallback, next)
```

<span data-ttu-id="721b3-136">Bu geri çağırma ve (sunucunun istek yanıtı) returnObject işlemden sonra geri çağırma diğer filtreleri işleme devam etmek için varsa sonraki çağırma veya yalnızca finalCallback Aksi halde hizmet başlatma sonuna çağırma gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="721b3-136">In this callback, and after processing the returnObject (the response from the request to the server), the callback needs to either invoke next if it exists to continue processing other filters or simply invoke finalCallback otherwise to end the service invocation.</span></span>

<span data-ttu-id="721b3-137">Yeniden deneme mantığını uygulaması iki filtre Node.js için Azure SDK'sı ile birlikte **ExponentialRetryPolicyFilter** ve **LinearRetryPolicyFilter**.</span><span class="sxs-lookup"><span data-stu-id="721b3-137">Two filters that implement retry logic are included with the Azure SDK for Node.js, **ExponentialRetryPolicyFilter** and **LinearRetryPolicyFilter**.</span></span> <span data-ttu-id="721b3-138">Aşağıdaki oluşturur bir **TableService** kullanan nesneyi **ExponentialRetryPolicyFilter**:</span><span class="sxs-lookup"><span data-stu-id="721b3-138">The following creates a **TableService** object that uses the **ExponentialRetryPolicyFilter**:</span></span>

```nodejs
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var tableSvc = azure.createTableService().withFilter(retryOperations);
```

## <a name="add-an-entity-to-a-table"></a><span data-ttu-id="721b3-139">Tabloya bir varlık ekleme</span><span class="sxs-lookup"><span data-stu-id="721b3-139">Add an entity to a table</span></span>
<span data-ttu-id="721b3-140">Bir varlık eklemek için önce varlık özelliklerinizi tanımlayan bir nesne oluşturun.</span><span class="sxs-lookup"><span data-stu-id="721b3-140">To add an entity, first create an object that defines your entity properties.</span></span> <span data-ttu-id="721b3-141">Tüm varlıklar içermesi gereken bir **PartitionKey** ve **RowKey**, varlık için benzersiz tanımlayıcı olduğu.</span><span class="sxs-lookup"><span data-stu-id="721b3-141">All entities must contain a **PartitionKey** and **RowKey**, which are unique identifiers for the entity.</span></span>

* <span data-ttu-id="721b3-142">**PartitionKey** -varlık depolanan bölüm belirler</span><span class="sxs-lookup"><span data-stu-id="721b3-142">**PartitionKey** - determines the partition that the entity is stored in</span></span>
* <span data-ttu-id="721b3-143">**RowKey** - benzersiz olarak varlığın bölüm içinde tanımlar</span><span class="sxs-lookup"><span data-stu-id="721b3-143">**RowKey** - uniquely identifies the entity within the partition</span></span>

<span data-ttu-id="721b3-144">Her ikisi de **PartitionKey** ve **RowKey** dize değerleri olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="721b3-144">Both **PartitionKey** and **RowKey** must be string values.</span></span> <span data-ttu-id="721b3-145">Daha fazla bilgi için bkz: [tablo hizmeti veri modelini anlama](http://msdn.microsoft.com/library/azure/dd179338.aspx).</span><span class="sxs-lookup"><span data-stu-id="721b3-145">For more information, see [Understanding the Table Service Data Model](http://msdn.microsoft.com/library/azure/dd179338.aspx).</span></span>

<span data-ttu-id="721b3-146">Bir varlık tanımlayan bir örnek verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="721b3-146">The following is an example of defining an entity.</span></span> <span data-ttu-id="721b3-147">Unutmayın **vade tarihi** bir türü olarak tanımlanmış **Edm.DateTime**.</span><span class="sxs-lookup"><span data-stu-id="721b3-147">Note that **dueDate** is defined as a type of **Edm.DateTime**.</span></span> <span data-ttu-id="721b3-148">Türünü belirtme isteğe bağlıdır ve türleri çıkarımı yapılan belirtilen yoksa.</span><span class="sxs-lookup"><span data-stu-id="721b3-148">Specifying the type is optional, and types will be inferred if not specified.</span></span>

```nodejs
var task = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '1'},
  description: {'_':'take out the trash'},
  dueDate: {'_':new Date(2015, 6, 20), '$':'Edm.DateTime'}
};
```

> [!NOTE]
> <span data-ttu-id="721b3-149">Ayrıca bir **zaman damgası** bir varlık eklendiğinde veya, Azure tarafından ayarlanan her kayıt için alan.</span><span class="sxs-lookup"><span data-stu-id="721b3-149">There is also a **Timestamp** field for each record, which is set by Azure when an entity is inserted or updated.</span></span>
>
>

<span data-ttu-id="721b3-150">Aynı zamanda **entityGenerator** varlıklar oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="721b3-150">You can also use the **entityGenerator** to create entities.</span></span> <span data-ttu-id="721b3-151">Aşağıdaki örnek, varlık aynı görevini kullanarak oluşturur **entityGenerator**.</span><span class="sxs-lookup"><span data-stu-id="721b3-151">The following example creates the same task entity using the **entityGenerator**.</span></span>

```nodejs
var entGen = azure.TableUtilities.entityGenerator;
var task = {
  PartitionKey: entGen.String('hometasks'),
  RowKey: entGen.String('1'),
  description: entGen.String('take out the trash'),
  dueDate: entGen.DateTime(new Date(Date.UTC(2015, 6, 20))),
};
```

<span data-ttu-id="721b3-152">Bir varlığı tablonuza eklemek için varlık nesnesine geçirmek **insertEntity** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="721b3-152">To add an entity to your table, pass the entity object to the **insertEntity** method.</span></span>

```nodejs
tableSvc.insertEntity('mytable',task, function (error, result, response) {
  if(!error){
    // Entity inserted
  }
});
```

<span data-ttu-id="721b3-153">İşlem başarılı olursa `result` içerecek [ETag](http://en.wikipedia.org/wiki/HTTP_ETag) eklenen kaydın ve `response` işlemi hakkında bilgi içerir.</span><span class="sxs-lookup"><span data-stu-id="721b3-153">If the operation is successful, `result` will contain the [ETag](http://en.wikipedia.org/wiki/HTTP_ETag) of the inserted record and `response` will contain information about the operation.</span></span>

<span data-ttu-id="721b3-154">Örnek yanıt:</span><span class="sxs-lookup"><span data-stu-id="721b3-154">Example response:</span></span>

```nodejs
{ '.metadata': { etag: 'W/"datetime\'2015-02-25T01%3A22%3A22.5Z\'"' } }
```

> [!NOTE]
> <span data-ttu-id="721b3-155">Varsayılan olarak, **insertEntity** parçası olarak eklenen varlık döndürmüyor `response` bilgi.</span><span class="sxs-lookup"><span data-stu-id="721b3-155">By default, **insertEntity** does not return the inserted entity as part of the `response` information.</span></span> <span data-ttu-id="721b3-156">Planı bu varlık üzerinde başka işlemler gerçekleştirmek ya da bilgilerini önbelleğe istiyorsanız, bir parçası olarak döndürülen yararlı olabilir `result`.</span><span class="sxs-lookup"><span data-stu-id="721b3-156">If you plan on performing other operations on this entity, or wish to cache the information, it can be useful to have it returned as part of the `result`.</span></span> <span data-ttu-id="721b3-157">Etkinleştirerek bunu yapabilirsiniz **echoContent** gibi:</span><span class="sxs-lookup"><span data-stu-id="721b3-157">You can do this by enabling **echoContent** as follows:</span></span>
>
> `tableSvc.insertEntity('mytable', task, {echoContent: true}, function (error, result, response) {...}`
>
>

## <a name="update-an-entity"></a><span data-ttu-id="721b3-158">Bir varlığı güncelleştirir</span><span class="sxs-lookup"><span data-stu-id="721b3-158">Update an entity</span></span>
<span data-ttu-id="721b3-159">Var olan bir varlığı güncelleştirmek için kullanılabilir birden çok yöntemi vardır:</span><span class="sxs-lookup"><span data-stu-id="721b3-159">There are multiple methods available to update an existing entity:</span></span>

* <span data-ttu-id="721b3-160">**replaceEntity** -değiştirme tarafından var olan bir varlığı güncelleştirir</span><span class="sxs-lookup"><span data-stu-id="721b3-160">**replaceEntity** - updates an existing entity by replacing it</span></span>
* <span data-ttu-id="721b3-161">**mergeEntity** -var olan varlık kümesine yeni özellik değerlerinin birleştirerek var olan bir varlığı güncelleştirir</span><span class="sxs-lookup"><span data-stu-id="721b3-161">**mergeEntity** - updates an existing entity by merging new property values into the existing entity</span></span>
* <span data-ttu-id="721b3-162">**insertOrReplaceEntity** -değiştirme tarafından var olan bir varlığı güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="721b3-162">**insertOrReplaceEntity** - updates an existing entity by replacing it.</span></span> <span data-ttu-id="721b3-163">Hiçbir varlık varsa, yeni bir tane eklenir</span><span class="sxs-lookup"><span data-stu-id="721b3-163">If no entity exists, a new one will be inserted</span></span>
* <span data-ttu-id="721b3-164">**insertOrMergeEntity** -mevcut yeni özellik değerlerinin birleştirerek var olan bir varlığı güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="721b3-164">**insertOrMergeEntity** - updates an existing entity by merging new property values into the existing.</span></span> <span data-ttu-id="721b3-165">Hiçbir varlık varsa, yeni bir tane eklenir</span><span class="sxs-lookup"><span data-stu-id="721b3-165">If no entity exists, a new one will be inserted</span></span>

<span data-ttu-id="721b3-166">Aşağıdaki örnek, bir varlık kullanarak güncelleştirme gösterir **replaceEntity**:</span><span class="sxs-lookup"><span data-stu-id="721b3-166">The following example demonstrates updating an entity using **replaceEntity**:</span></span>

```nodejs
tableSvc.replaceEntity('mytable', updatedTask, function(error, result, response){
  if(!error) {
    // Entity updated
  }
});
```

> [!NOTE]
> <span data-ttu-id="721b3-167">Varsayılan olarak, bir varlık güncelleştirme güncelleştirilen veri daha önce başka bir işlem tarafından değiştirilip değiştirilmediğini görmek için kontrol etmez.</span><span class="sxs-lookup"><span data-stu-id="721b3-167">By default, updating an entity does not check to see if the data being updated has previously been modified by another process.</span></span> <span data-ttu-id="721b3-168">Eşzamanlı güncelleştirmelerini desteklemek için:</span><span class="sxs-lookup"><span data-stu-id="721b3-168">To support concurrent updates:</span></span>
>
> 1. <span data-ttu-id="721b3-169">Güncelleştirilecek nesnenin ETag alın.</span><span class="sxs-lookup"><span data-stu-id="721b3-169">Get the ETag of the object being updated.</span></span> <span data-ttu-id="721b3-170">Bu bir parçası olarak döndürülür `response` tüm ilgili varlık işlemi için ve alınabilir `response['.metadata'].etag`.</span><span class="sxs-lookup"><span data-stu-id="721b3-170">This is returned as part of the `response` for any entity-related operation and can be retrieved through `response['.metadata'].etag`.</span></span>
> 2. <span data-ttu-id="721b3-171">Bir varlık üzerinde bir güncelleştirme işlemi gerçekleştirirken, daha önce yeni varlığa alınan ETag bilgileri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="721b3-171">When performing an update operation on an entity, add the ETag information previously retrieved to the new entity.</span></span> <span data-ttu-id="721b3-172">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="721b3-172">For example:</span></span>
>
>       <span data-ttu-id="721b3-173">entity2 ['.metadata'] .etag currentEtag; =</span><span class="sxs-lookup"><span data-stu-id="721b3-173">entity2['.metadata'].etag = currentEtag;</span></span>
> 3. <span data-ttu-id="721b3-174">Güncelleştirme işlemi gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="721b3-174">Perform the update operation.</span></span> <span data-ttu-id="721b3-175">Varlık, uygulamanızın başka bir örneği gibi ETag değeri alınan beri değiştirilmişse bir `error` istekte belirtilen güncelleştirme koşulu karşılanmadı belirten döndürülür.</span><span class="sxs-lookup"><span data-stu-id="721b3-175">If the entity has been modified since you retrieved the ETag value, such as another instance of your application, an `error` will be returned stating that the update condition specified in the request was not satisfied.</span></span>
>
>

<span data-ttu-id="721b3-176">İle **replaceEntity** ve **mergeEntity**, güncelleştirilen varlığı yoksa güncelleştirme işlemi başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="721b3-176">With **replaceEntity** and **mergeEntity**, if the entity that is being updated doesn't exist, then the update operation will fail.</span></span> <span data-ttu-id="721b3-177">Bu nedenle bir varlık depolamak istiyorsanız bakılmaksızın, zaten var olup, kullanın **insertOrReplaceEntity** veya **insertOrMergeEntity**.</span><span class="sxs-lookup"><span data-stu-id="721b3-177">Therefore if you wish to store an entity regardless of whether it already exists, use **insertOrReplaceEntity** or **insertOrMergeEntity**.</span></span>

<span data-ttu-id="721b3-178">`result` Başarılı güncelleştirmesi işlemleri içerecek **Etag** güncelleştirilmiş varlık.</span><span class="sxs-lookup"><span data-stu-id="721b3-178">The `result` for successful update operations will contain the **Etag** of the updated entity.</span></span>

## <a name="work-with-groups-of-entities"></a><span data-ttu-id="721b3-179">Varlıkları gruplarıyla çalışma</span><span class="sxs-lookup"><span data-stu-id="721b3-179">Work with groups of entities</span></span>
<span data-ttu-id="721b3-180">Bazen birden çok sunucu tarafından işleme atomik emin olmak için birlikte toplu iş işlemlerinde göndermek için mantıklıdır.</span><span class="sxs-lookup"><span data-stu-id="721b3-180">Sometimes it makes sense to submit multiple operations together in a batch to ensure atomic processing by the server.</span></span> <span data-ttu-id="721b3-181">Bunu yapmaya yönelik kullanmak **TableBatch** toplu oluşturmak için sınıf ve sonra **executeBatch** yöntemi **TableService** toplu işlemleri gerçekleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="721b3-181">To accomplish that, use the **TableBatch** class to create a batch, and then use the **executeBatch** method of **TableService** to perform the batched operations.</span></span>

 <span data-ttu-id="721b3-182">Aşağıdaki örnek, bir toplu işte iki varlık gönderme gösterir:</span><span class="sxs-lookup"><span data-stu-id="721b3-182">The following example demonstrates submitting two entities in a batch:</span></span>

```nodejs
var task1 = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '1'},
  description: {'_':'Take out the trash'},
  dueDate: {'_':new Date(2015, 6, 20)}
};
var task2 = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '2'},
  description: {'_':'Wash the dishes'},
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

<span data-ttu-id="721b3-183">Başarılı toplu işlemler için `result` her bir toplu işlemde için bilgiler içerir.</span><span class="sxs-lookup"><span data-stu-id="721b3-183">For successful batch operations, `result` will contain information for each operation in the batch.</span></span>

### <a name="work-with-batched-operations"></a><span data-ttu-id="721b3-184">Toplu işlemleri ile çalışma</span><span class="sxs-lookup"><span data-stu-id="721b3-184">Work with batched operations</span></span>
<span data-ttu-id="721b3-185">Bir toplu iş eklenen işlemleri görüntüleyerek Denetlenmekte `operations` özelliği.</span><span class="sxs-lookup"><span data-stu-id="721b3-185">Operations added to a batch can be inspected by viewing the `operations` property.</span></span> <span data-ttu-id="721b3-186">İşlemleri ile çalışmak için aşağıdaki yöntemleri de kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="721b3-186">You can also use the following methods to work with operations:</span></span>

* <span data-ttu-id="721b3-187">**Clear** -tüm işlemler bir batch temizler</span><span class="sxs-lookup"><span data-stu-id="721b3-187">**clear** - clears all operations from a batch</span></span>
* <span data-ttu-id="721b3-188">**getOperations** -bir işlem toplu işten alır</span><span class="sxs-lookup"><span data-stu-id="721b3-188">**getOperations** - gets an operation from the batch</span></span>
* <span data-ttu-id="721b3-189">**hasOperations** -toplu işlemler varsa true değerini döndürür</span><span class="sxs-lookup"><span data-stu-id="721b3-189">**hasOperations** - returns true if the batch contains operations</span></span>
* <span data-ttu-id="721b3-190">**removeOperations** -bir işlem kaldırır</span><span class="sxs-lookup"><span data-stu-id="721b3-190">**removeOperations** - removes an operation</span></span>
* <span data-ttu-id="721b3-191">**boyutu** -toplu işlemde işlemlerinin sayısını döndürür</span><span class="sxs-lookup"><span data-stu-id="721b3-191">**size** - returns the number of operations in the batch</span></span>

## <a name="retrieve-an-entity-by-key"></a><span data-ttu-id="721b3-192">Anahtara göre bir varlık alma</span><span class="sxs-lookup"><span data-stu-id="721b3-192">Retrieve an entity by key</span></span>
<span data-ttu-id="721b3-193">Göre belirli bir varlık döndürülecek **PartitionKey** ve **RowKey**, kullanın **retrieveEntity** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="721b3-193">To return a specific entity based on the **PartitionKey** and **RowKey**, use the **retrieveEntity** method.</span></span>

```nodejs
tableSvc.retrieveEntity('mytable', 'hometasks', '1', function(error, result, response){
  if(!error){
    // result contains the entity
  }
});
```

<span data-ttu-id="721b3-194">Bu işlem tamamlandıktan sonra `result` varlık içerir.</span><span class="sxs-lookup"><span data-stu-id="721b3-194">Once this operation is complete, `result` will contain the entity.</span></span>

## <a name="query-a-set-of-entities"></a><span data-ttu-id="721b3-195">Varlık kümesi sorgulama</span><span class="sxs-lookup"><span data-stu-id="721b3-195">Query a set of entities</span></span>
<span data-ttu-id="721b3-196">Bir tabloyu sorgulamak için kullanın **TableQuery** nesne aşağıdaki yan tümceleri kullanarak bir sorgu ifadesi oluşturmak için:</span><span class="sxs-lookup"><span data-stu-id="721b3-196">To query a table, use the **TableQuery** object to build up a query expression using the following clauses:</span></span>

* <span data-ttu-id="721b3-197">**seçin** -sorgudan döndürülecek alanları</span><span class="sxs-lookup"><span data-stu-id="721b3-197">**select** - the fields to be returned from the query</span></span>
* <span data-ttu-id="721b3-198">**Burada** -where yan tümcesi</span><span class="sxs-lookup"><span data-stu-id="721b3-198">**where** - the where clause</span></span>

  * <span data-ttu-id="721b3-199">**ve** - bir `and` koşul</span><span class="sxs-lookup"><span data-stu-id="721b3-199">**and** - an `and` where condition</span></span>
  * <span data-ttu-id="721b3-200">**veya** - bir `or` koşul</span><span class="sxs-lookup"><span data-stu-id="721b3-200">**or** - an `or` where condition</span></span>
* <span data-ttu-id="721b3-201">**üst** -getirmek için öğe sayısı</span><span class="sxs-lookup"><span data-stu-id="721b3-201">**top** - the number of items to fetch</span></span>

<span data-ttu-id="721b3-202">Aşağıdaki örnek, bir PartitionKey 'hometasks' ın üst beş öğeleri döndürülecek bir sorgu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="721b3-202">The following example builds a query that will return the top five items with a PartitionKey of 'hometasks'.</span></span>

```nodejs
var query = new azure.TableQuery()
  .top(5)
  .where('PartitionKey eq ?', 'hometasks');
```

<span data-ttu-id="721b3-203">Bu yana **seçin** , tüm alanları döndürülecek kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="721b3-203">Since **select** is not used, all fields will be returned.</span></span> <span data-ttu-id="721b3-204">Tablo sorgusu gerçekleştirmek için kullanın **queryEntities**.</span><span class="sxs-lookup"><span data-stu-id="721b3-204">To perform the query against a table, use **queryEntities**.</span></span> <span data-ttu-id="721b3-205">Aşağıdaki örnekte, varlıklar 'mytable' döndürmek için bu sorguyu kullanır.</span><span class="sxs-lookup"><span data-stu-id="721b3-205">The following example uses this query to return entities from 'mytable'.</span></span>

```nodejs
tableSvc.queryEntities('mytable',query, null, function(error, result, response) {
  if(!error) {
    // query was successful
  }
});
```

<span data-ttu-id="721b3-206">Başarılı olursa, `result.entries` sorguyla eşleşen varlıkları dizisi içerir.</span><span class="sxs-lookup"><span data-stu-id="721b3-206">If successful, `result.entries` will contain an array of entities that match the query.</span></span> <span data-ttu-id="721b3-207">Sorgu tüm varlıkları döndüremedi varsa `result.continuationToken` olmayan olacaktır*null* ve üçüncü parametresi olarak kullanılabilir **queryEntities** daha fazla sonuç alınamadı.</span><span class="sxs-lookup"><span data-stu-id="721b3-207">If the query was unable to return all entities, `result.continuationToken` will be non-*null* and can be used as the third parameter of **queryEntities** to retrieve more results.</span></span> <span data-ttu-id="721b3-208">İlk sorguyu için *null* üçüncü parametre.</span><span class="sxs-lookup"><span data-stu-id="721b3-208">For the initial query, use *null* for the third parameter.</span></span>

### <a name="query-a-subset-of-entity-properties"></a><span data-ttu-id="721b3-209">Giriş özellikleri alt kümesi sorgulama</span><span class="sxs-lookup"><span data-stu-id="721b3-209">Query a subset of entity properties</span></span>
<span data-ttu-id="721b3-210">Sorguda bir tabloya bir varlık birkaç alanları alabilir.</span><span class="sxs-lookup"><span data-stu-id="721b3-210">A query to a table can retrieve just a few fields from an entity.</span></span>
<span data-ttu-id="721b3-211">Bu, bant genişliğini azaltır ve özellikle büyük varlıklar için sorgu performansını iyileştirebilir.</span><span class="sxs-lookup"><span data-stu-id="721b3-211">This reduces bandwidth and can improve query performance, especially for large entities.</span></span> <span data-ttu-id="721b3-212">Kullanım **seçin** yan tümcesi ve döndürülecek alanların adlarını geçirin.</span><span class="sxs-lookup"><span data-stu-id="721b3-212">Use the **select** clause and pass the names of the fields to be returned.</span></span> <span data-ttu-id="721b3-213">Örneğin, aşağıdaki sorguyu yalnızca döndürülecek **açıklama** ve **vade tarihi** alanları.</span><span class="sxs-lookup"><span data-stu-id="721b3-213">For example, the following query will return only the **description** and **dueDate** fields.</span></span>

```nodejs
var query = new azure.TableQuery()
  .select(['description', 'dueDate'])
  .top(5)
  .where('PartitionKey eq ?', 'hometasks');
```

## <a name="delete-an-entity"></a><span data-ttu-id="721b3-214">Bir varlığı silme</span><span class="sxs-lookup"><span data-stu-id="721b3-214">Delete an entity</span></span>
<span data-ttu-id="721b3-215">Bir varlığın bölüm ve satır anahtarını kullanarak silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="721b3-215">You can delete an entity using its partition and row keys.</span></span> <span data-ttu-id="721b3-216">Bu örnekte, **task1** nesnesini içeren **RowKey** ve **PartitionKey** silinecek varlığın değerleri.</span><span class="sxs-lookup"><span data-stu-id="721b3-216">In this example, the **task1** object contains the **RowKey** and **PartitionKey** values of the entity to be deleted.</span></span> <span data-ttu-id="721b3-217">Nesne geçirilir sonra **deleteEntity** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="721b3-217">Then the object is passed to the **deleteEntity** method.</span></span>

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
> <span data-ttu-id="721b3-218">Öğeleri silerken bir öğe başka bir işlem tarafından değiştirilip değiştirilmediğini emin olmak için Etag'ler kullanmayı düşünün.</span><span class="sxs-lookup"><span data-stu-id="721b3-218">Consider using ETags when deleting items, to ensure that the item hasn't been modified by another process.</span></span> <span data-ttu-id="721b3-219">Bkz: [bir varlığı güncelleştirmek](#update-an-entity) Etag'ler kullanma hakkında bilgi için.</span><span class="sxs-lookup"><span data-stu-id="721b3-219">See [Update an entity](#update-an-entity) for information on using ETags.</span></span>
>
>

## <a name="delete-a-table"></a><span data-ttu-id="721b3-220">Bir tablo silme</span><span class="sxs-lookup"><span data-stu-id="721b3-220">Delete a table</span></span>
<span data-ttu-id="721b3-221">Aşağıdaki kod, bir depolama hesabından bir tablo siler.</span><span class="sxs-lookup"><span data-stu-id="721b3-221">The following code deletes a table from a storage account.</span></span>

```nodejs
tableSvc.deleteTable('mytable', function(error, response){
    if(!error){
        // Table deleted
    }
});
```

<span data-ttu-id="721b3-222">Tablo var olup olmadığından emin değilseniz kullanmak **deleteTableIfExists**.</span><span class="sxs-lookup"><span data-stu-id="721b3-222">If you are uncertain whether the table exists, use **deleteTableIfExists**.</span></span>

## <a name="use-continuation-tokens"></a><span data-ttu-id="721b3-223">Devamlılık belirteçleri kullanın</span><span class="sxs-lookup"><span data-stu-id="721b3-223">Use continuation tokens</span></span>
<span data-ttu-id="721b3-224">İçin devamlılık belirteci tablolar için sonuçları büyük miktarlarda sorgulanırken arayın.</span><span class="sxs-lookup"><span data-stu-id="721b3-224">When you are querying tables for large amounts of results, look for continuation tokens.</span></span> <span data-ttu-id="721b3-225">Sorgunuz için bir devamlılık belirteci bulunduğunda tanımak için oluşturacağınız değil, farkına varmazsınız kullanılabilir büyük miktarlarda verinin olabilir.</span><span class="sxs-lookup"><span data-stu-id="721b3-225">There may be large amounts of data available for your query that you might not realize if you do not build to recognize when a continuation token is present.</span></span>

<span data-ttu-id="721b3-226">Sonuçlar nesne döndürülen varlık kümeleri sorgulama sırasında bir `continuationToken` böyle bir belirteç bulunduğunda özelliği.</span><span class="sxs-lookup"><span data-stu-id="721b3-226">The results object returned during querying entities sets a `continuationToken` property when such a token is present.</span></span> <span data-ttu-id="721b3-227">Ardından bu sorgu gerçekleştirirken bölüm ve tablo varlıkları arasında taşımak devam etmek için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="721b3-227">You can then use this when performing a query to continue to move across the partition and table entities.</span></span>

<span data-ttu-id="721b3-228">Sorgulama yapıldığında continuationToken parametre sorgu nesne örneği ile geri çağırma işlevi arasında sağlanabilir:</span><span class="sxs-lookup"><span data-stu-id="721b3-228">When querying, a continuationToken parameter may be provided between the query object instance and the callback function:</span></span>

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

<span data-ttu-id="721b3-229">İnceleyin, `continuationToken` nesnesi bulacaksınız özellikler gibi `nextPartitionKey`, `nextRowKey` ve `targetLocation`, tüm sonuçları yinelemek için kullanılabilecek.</span><span class="sxs-lookup"><span data-stu-id="721b3-229">If you inspect the `continuationToken` object, you will find properties such as `nextPartitionKey`, `nextRowKey` and `targetLocation`, which can be used to iterate through all the results.</span></span>

<span data-ttu-id="721b3-230">Github'daki Azure depolama Node.js deposu içinde devamlılık örnek yoktur.</span><span class="sxs-lookup"><span data-stu-id="721b3-230">There is also a continuation sample within the Azure Storage Node.js repo on GitHub.</span></span> <span data-ttu-id="721b3-231">Ara `examples/samples/continuationsample.js`.</span><span class="sxs-lookup"><span data-stu-id="721b3-231">Look for `examples/samples/continuationsample.js`.</span></span>

## <a name="work-with-shared-access-signatures"></a><span data-ttu-id="721b3-232">Paylaşılan erişim imzaları ile çalışma</span><span class="sxs-lookup"><span data-stu-id="721b3-232">Work with shared access signatures</span></span>
<span data-ttu-id="721b3-233">Paylaşılan erişim imzaları (SAS) depolama hesabı adı veya anahtarları sağlamadan tabloları ayrıntılı erişim sağlamak için güvenli bir yoludur.</span><span class="sxs-lookup"><span data-stu-id="721b3-233">Shared access signatures (SAS) are a secure way to provide granular access to tables without providing your storage account name or keys.</span></span> <span data-ttu-id="721b3-234">SAS genellikle, verileri kayıtlarını sorgulamak için mobil uygulama izin verme gibi sınırlı erişim sağlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="721b3-234">SAS are often used to provide limited access to your data, such as allowing a mobile app to query records.</span></span>

<span data-ttu-id="721b3-235">SAS kullanarak bulut tabanlı bir hizmete gibi güvenilir bir uygulama oluşturur **generateSharedAccessSignature** , **TableService**ve bir mobil uygulama gibi güvenilmeyen veya yarı güvenilir bir uygulama sağlar.</span><span class="sxs-lookup"><span data-stu-id="721b3-235">A trusted application such as a cloud-based service generates a SAS using the **generateSharedAccessSignature** of the **TableService**, and provides it to an untrusted or semi-trusted application such as a mobile app.</span></span> <span data-ttu-id="721b3-236">SAS SAS sahibi verilen erişim düzeyini yanı sıra SAS geçerli olduğu başlangıç ve bitiş tarihleri açıklar, bir ilke kullanılarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="721b3-236">The SAS is generated using a policy, which describes the start and end dates during which the SAS is valid, as well as the access level granted to the SAS holder.</span></span>

<span data-ttu-id="721b3-237">Aşağıdaki örnek, sorgu ('r') tablo için SAS sahibi izin veren yeni bir paylaşılan erişim ilkesi oluşturur ve 100 dakika oluşturulduktan sonra süresi dolar.</span><span class="sxs-lookup"><span data-stu-id="721b3-237">The following example generates a new shared access policy that will allow the SAS holder to query ('r') the table, and expires 100 minutes after the time it is created.</span></span>

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

<span data-ttu-id="721b3-238">SAS sahibi tablo erişmeyi denediğinde, gerekli olduğu gibi konak bilgileri'nin de, sağlanan gerekir unutmayın.</span><span class="sxs-lookup"><span data-stu-id="721b3-238">Note that the host information must be provided also, as it is required when the SAS holder attempts to access the table.</span></span>

<span data-ttu-id="721b3-239">İstemci uygulama ile SAS kullanan **TableServiceWithSAS** tablo karşı işlemlerini gerçekleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="721b3-239">The client application then uses the SAS with **TableServiceWithSAS** to perform operations against the table.</span></span> <span data-ttu-id="721b3-240">Aşağıdaki örnek, tabloya bağlanır ve bir sorgu gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="721b3-240">The following example connects to the table and performs a query.</span></span>

```nodejs
var sharedTableService = azure.createTableServiceWithSas(host, tableSAS);
var query = azure.TableQuery()
  .where('PartitionKey eq ?', 'hometasks');

sharedTableService.queryEntities(query, null, function(error, result, response) {
  if(!error) {
    // result contains the entities
  }
});
```

<span data-ttu-id="721b3-241">Ekle, Güncelleştir veya varlıklarını silme girişiminde yapılmışsa SAS yalnızca sorgu erişimle oluşturulmasının üzerinden bir hata döndürülür.</span><span class="sxs-lookup"><span data-stu-id="721b3-241">Since the SAS was generated with only query access, if an attempt were made to insert, update, or delete entities, an error would be returned.</span></span>

### <a name="access-control-lists"></a><span data-ttu-id="721b3-242">Erişim denetim listeleri</span><span class="sxs-lookup"><span data-stu-id="721b3-242">Access Control Lists</span></span>
<span data-ttu-id="721b3-243">Erişim ilkesi için bir SAS ayarlamak için erişim denetim listesi (ACL) da kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="721b3-243">You can also use an Access Control List (ACL) to set the access policy for a SAS.</span></span> <span data-ttu-id="721b3-244">Bu tabloya erişim, ancak her istemci için farklı erişim ilkeleri sağlamak birden çok istemciye izin vermek istiyorsanız yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="721b3-244">This is useful if you wish to allow multiple clients to access the table, but provide different access policies for each client.</span></span>

<span data-ttu-id="721b3-245">Bir ACL her ilkesiyle ilişkili bir Kimliğe sahip bir dizi erişim ilkeleri kullanılarak uygulanır.</span><span class="sxs-lookup"><span data-stu-id="721b3-245">An ACL is implemented using an array of access policies, with an ID associated with each policy.</span></span> <span data-ttu-id="721b3-246">Aşağıdaki örnekte, iki ilke, 'User1' diğeri için 'kullanıcı2' tanımlar:</span><span class="sxs-lookup"><span data-stu-id="721b3-246">The following example defines two policies, one for 'user1' and one for 'user2':</span></span>

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

<span data-ttu-id="721b3-247">Aşağıdaki örnek için geçerli ACL alır **hometasks** tablo ve yeni ilkeleri kullanılarak ekler **setTableAcl**.</span><span class="sxs-lookup"><span data-stu-id="721b3-247">The following example gets the current ACL for the **hometasks** table, and then adds the new policies using **setTableAcl**.</span></span> <span data-ttu-id="721b3-248">Bu yaklaşım sağlar:</span><span class="sxs-lookup"><span data-stu-id="721b3-248">This approach allows:</span></span>

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

<span data-ttu-id="721b3-249">ACL ayarladıktan sonra daha sonra bir ilke kimliği dayalı bir SAS oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="721b3-249">Once the ACL has been set, you can then create a SAS based on the ID for a policy.</span></span> <span data-ttu-id="721b3-250">Aşağıdaki örnek, 'kullanıcı2' için yeni bir SAS oluşturur:</span><span class="sxs-lookup"><span data-stu-id="721b3-250">The following example creates a new SAS for 'user2':</span></span>

```nodejs
tableSAS = tableSvc.generateSharedAccessSignature('hometasks', { Id: 'user2' });
```

## <a name="next-steps"></a><span data-ttu-id="721b3-251">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="721b3-251">Next steps</span></span>
<span data-ttu-id="721b3-252">Daha fazla bilgi için aşağıdaki kaynaklara bakın.</span><span class="sxs-lookup"><span data-stu-id="721b3-252">For more information, see the following resources.</span></span>

* <span data-ttu-id="721b3-253">[Microsoft Azure Depolama Gezgini](../vs-azure-tools-storage-manage-with-storage-explorer.md), Microsoft’un Windows, macOS ve Linux üzerinde Azure Depolama verileriyle görsel olarak çalışmanızı sağlayan ücretsiz ve tek başına uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="721b3-253">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you to work visually with Azure Storage data on Windows, macOS, and Linux.</span></span>
* <span data-ttu-id="721b3-254">[Azure depolama SDK'sı düğüm için](https://github.com/Azure/azure-storage-node) github'daki.</span><span class="sxs-lookup"><span data-stu-id="721b3-254">[Azure Storage SDK for Node](https://github.com/Azure/azure-storage-node) repository on GitHub.</span></span>
* [<span data-ttu-id="721b3-255">Node.js Geliştirici Merkezi</span><span class="sxs-lookup"><span data-stu-id="721b3-255">Node.js Developer Center</span></span>](/develop/nodejs/)
* [<span data-ttu-id="721b3-256">Bir Azure Web sitesine bir Node.js uygulama oluşturun ve dağıtın</span><span class="sxs-lookup"><span data-stu-id="721b3-256">Create and deploy a Node.js application to an Azure website</span></span>](../app-service-web/app-service-web-get-started-nodejs.md)