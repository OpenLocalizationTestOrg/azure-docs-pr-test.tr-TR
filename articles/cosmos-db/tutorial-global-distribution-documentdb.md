---
title: "DocumentDB API için aaaAzure Cosmos DB genel dağıtım Öğreticisi | Microsoft Docs"
description: "Nasıl toosetup Azure Cosmos DB genel dağıtım kullanarak izin ver hello DocumentDB API öğrenin."
services: cosmos-db
keywords: "genel dağıtım, documentdb"
documentationcenter: 
author: mimig1
manager: jhubbard
editor: cgronlun
ms.assetid: 8b815047-2868-4b10-af1d-40a1af419a70
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: a1d5f01faa62407fbbc9c078ef4a9589a1a29219
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosetup-azure-cosmos-db-global-distribution-using-hello-documentdb-api"></a><span data-ttu-id="efa2b-104">Nasıl toosetup Azure Cosmos DB genel dağıtım kullanarak izin ver hello DocumentDB API</span><span class="sxs-lookup"><span data-stu-id="efa2b-104">How toosetup Azure Cosmos DB global distribution using hello DocumentDB API</span></span>

<span data-ttu-id="efa2b-105">Bu makalede, nasıl toouse Azure portal toosetup Azure Cosmos DB genel dağıtım hello ve hello DocumentDB API kullanarak bağlanmak gösterir.</span><span class="sxs-lookup"><span data-stu-id="efa2b-105">In this article, we show how toouse hello Azure portal toosetup Azure Cosmos DB global distribution and then connect using hello DocumentDB API.</span></span>

<span data-ttu-id="efa2b-106">Bu makalede görevleri aşağıdaki hello yer almaktadır:</span><span class="sxs-lookup"><span data-stu-id="efa2b-106">This article covers hello following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="efa2b-107">Genel dağıtım Hello Azure portal kullanarak yapılandırma</span><span class="sxs-lookup"><span data-stu-id="efa2b-107">Configure global distribution using hello Azure portal</span></span>
> * <span data-ttu-id="efa2b-108">Hello kullanarak genel dağıtım yapılandırma [DocumentDB API'leri](documentdb-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="efa2b-108">Configure global distribution using hello [DocumentDB APIs](documentdb-introduction.md)</span></span>

<a id="portal"></a>
[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]


## <a name="connecting-tooa-preferred-region-using-hello-documentdb-api"></a><span data-ttu-id="efa2b-109">Tooa tercih edilen bölge Hello DocumentDB API kullanarak bağlanma</span><span class="sxs-lookup"><span data-stu-id="efa2b-109">Connecting tooa preferred region using hello DocumentDB API</span></span>

<span data-ttu-id="efa2b-110">Sipariş tootake avantajlarından içinde [genel dağıtım](distribute-data-globally.md), istemci uygulamalarının hello sıralı kullanılan tooperform belge işlemleri bölgeleri toobe tercih listesi belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="efa2b-110">In order tootake advantage of [global distribution](distribute-data-globally.md), client applications can specify hello ordered preference list of regions toobe used tooperform document operations.</span></span> <span data-ttu-id="efa2b-111">Bu, başlangıç bağlantı İlkesi ayarlayarak yapılabilir.</span><span class="sxs-lookup"><span data-stu-id="efa2b-111">This can be done by setting hello connection policy.</span></span> <span data-ttu-id="efa2b-112">Hello Azure Cosmos DB hesap yapılandırmasını temel alarak, geçerli bölge kullanılabilirliği ve hello tercih listesi, belirtilen hello çoğu en iyi bitiş noktası tarafından DocumentDB SDK'sı tooperform yazma ve okuma işlemlerini hello seçilir.</span><span class="sxs-lookup"><span data-stu-id="efa2b-112">Based on hello Azure Cosmos DB account configuration, current regional availability and hello preference list specified, hello most optimal endpoint will be chosen by hello DocumentDB SDK tooperform write and read operations.</span></span>

<span data-ttu-id="efa2b-113">Bu tercih listesi hello DocumentDB SDK'ları kullanarak bağlantı başlatırken belirtilir.</span><span class="sxs-lookup"><span data-stu-id="efa2b-113">This preference list is specified when initializing a connection using hello DocumentDB SDKs.</span></span> <span data-ttu-id="efa2b-114">Merhaba SDK'ları isteğe bağlı bir parametre "PreferredLocations" kabul Azure bölgeleri diğer bir deyişle sıralı bir listesi.</span><span class="sxs-lookup"><span data-stu-id="efa2b-114">hello SDKs accept an optional parameter "PreferredLocations" that is an ordered list of Azure regions.</span></span>

<span data-ttu-id="efa2b-115">Merhaba SDK tüm yazma toohello geçerli yazma bölge otomatik olarak gönderir.</span><span class="sxs-lookup"><span data-stu-id="efa2b-115">hello SDK will automatically send all writes toohello current write region.</span></span>

<span data-ttu-id="efa2b-116">Tüm okuma toohello ilk kullanılabilir bölge hello PreferredLocations listesinde gönderilir.</span><span class="sxs-lookup"><span data-stu-id="efa2b-116">All reads will be sent toohello first available region in hello PreferredLocations list.</span></span> <span data-ttu-id="efa2b-117">Merhaba isteği başarısız olursa, hello istemci hello listesi toohello sonraki bölgeyi başarısız ve benzeri.</span><span class="sxs-lookup"><span data-stu-id="efa2b-117">If hello request fails, hello client will fail down hello list toohello next region, and so on.</span></span>

<span data-ttu-id="efa2b-118">Merhaba SDK'ları yalnızca tooread PreferredLocations içinde belirtilen hello bölgelerinden deneyecek.</span><span class="sxs-lookup"><span data-stu-id="efa2b-118">hello SDKs will only attempt tooread from hello regions specified in PreferredLocations.</span></span> <span data-ttu-id="efa2b-119">Bu nedenle, örneğin, hello veritabanı hesabı üç bölgelerde kullanılabilir, ancak PreferredLocations için iki hello yazma olmayan bölgeleri yalnızca hello istemci belirtir, sonra okuma yük devretme hello durumda bile hello yazma bölgesi dışında sunulacak.</span><span class="sxs-lookup"><span data-stu-id="efa2b-119">So, for example, if hello Database Account is available in three regions, but hello client only specifies two of hello non-write regions for PreferredLocations, then no reads will be served out of hello write region, even in hello case of failover.</span></span>

<span data-ttu-id="efa2b-120">Merhaba uygulaması hello geçerli yazma uç noktası doğrulayın ve uç nokta denetimi iki özellikleri, WriteEndpoint ve ReadEndpoint, SDK sürümü 1.8 ve üzeri kullanılabilir tarafından hello SDK tarafından seçilen okuyun.</span><span class="sxs-lookup"><span data-stu-id="efa2b-120">hello application can verify hello current write endpoint and read endpoint chosen by hello SDK by checking two properties, WriteEndpoint and ReadEndpoint, available in SDK version 1.8 and above.</span></span>

<span data-ttu-id="efa2b-121">Merhaba PreferredLocations özellik ayarlanmamışsa, tüm istekleri hello geçerli yazma bölgesinden sunulacak.</span><span class="sxs-lookup"><span data-stu-id="efa2b-121">If hello PreferredLocations property is not set, all requests will be served from hello current write region.</span></span>

## <a name="net-sdk"></a><span data-ttu-id="efa2b-122">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="efa2b-122">.NET SDK</span></span>
<span data-ttu-id="efa2b-123">Merhaba SDK kod değişiklikleri kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="efa2b-123">hello SDK can be used without any code changes.</span></span> <span data-ttu-id="efa2b-124">Bu durumda, hello SDK otomatik olarak her iki okuma yönlendirir ve toohello geçerli yazma bölge yazar.</span><span class="sxs-lookup"><span data-stu-id="efa2b-124">In this case, hello SDK automatically directs both reads and writes toohello current write region.</span></span>

<span data-ttu-id="efa2b-125">Sürüm 1,8 ve sonraki hello .NET SDK'sı, hello ConnectionPolicy parametresi hello DocumentClient oluşturucusu için Microsoft.Azure.Documents.ConnectionPolicy.PreferredLocations adlı bir özelliğe sahiptir.</span><span class="sxs-lookup"><span data-stu-id="efa2b-125">In version 1.8 and later of hello .NET SDK, hello ConnectionPolicy parameter for hello DocumentClient constructor has a property called Microsoft.Azure.Documents.ConnectionPolicy.PreferredLocations.</span></span> <span data-ttu-id="efa2b-126">Bu özellik koleksiyonu türünde `<string>` ve bölge adları listesi içermelidir.</span><span class="sxs-lookup"><span data-stu-id="efa2b-126">This property is of type Collection `<string>` and should contain a list of region names.</span></span> <span data-ttu-id="efa2b-127">Merhaba hello bölge adı sütunu başına biçimlendirilen Hello dize değerleri [Azure bölgeleri] [ regions] , boşluk önce veya sonra hello ilk sayfa ve karakter sırasıyla en son.</span><span class="sxs-lookup"><span data-stu-id="efa2b-127">hello string values are formatted per hello Region Name column on hello [Azure Regions][regions] page, with no spaces before or after hello first and last character respectively.</span></span>

<span data-ttu-id="efa2b-128">Merhaba geçerli yazma ve okuma uç noktaları sırasıyla DocumentClient.WriteEndpoint ve DocumentClient.ReadEndpoint kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="efa2b-128">hello current write and read endpoints are available in DocumentClient.WriteEndpoint and DocumentClient.ReadEndpoint respectively.</span></span>

> [!NOTE]
> <span data-ttu-id="efa2b-129">Merhaba URL'leri hello uç noktalar için uzun süreli sabitleri düşünülmemelidir.</span><span class="sxs-lookup"><span data-stu-id="efa2b-129">hello URLs for hello endpoints should not be considered as long-lived constants.</span></span> <span data-ttu-id="efa2b-130">Merhaba hizmet bunlar herhangi bir noktada güncelleştirebilir.</span><span class="sxs-lookup"><span data-stu-id="efa2b-130">hello service may update these at any point.</span></span> <span data-ttu-id="efa2b-131">Merhaba SDK bu değişikliği otomatik olarak yönetir.</span><span class="sxs-lookup"><span data-stu-id="efa2b-131">hello SDK handles this change automatically.</span></span>
>
>

```csharp
// Getting endpoints from application settings or other configuration location
Uri accountEndPoint = new Uri(Properties.Settings.Default.GlobalDatabaseUri);
string accountKey = Properties.Settings.Default.GlobalDatabaseKey;
  
ConnectionPolicy connectionPolicy = new ConnectionPolicy();

//Setting read region selection preference
connectionPolicy.PreferredLocations.Add(LocationNames.WestUS); // first preference
connectionPolicy.PreferredLocations.Add(LocationNames.EastUS); // second preference
connectionPolicy.PreferredLocations.Add(LocationNames.NorthEurope); // third preference

// initialize connection
DocumentClient docClient = new DocumentClient(
    accountEndPoint,
    accountKey,
    connectionPolicy);

// connect tooDocDB
await docClient.OpenAsync().ConfigureAwait(false);
```

## <a name="nodejs-javascript-and-python-sdks"></a><span data-ttu-id="efa2b-132">NodeJS, JavaScript ve Python SDK'ları</span><span class="sxs-lookup"><span data-stu-id="efa2b-132">NodeJS, JavaScript, and Python SDKs</span></span>
<span data-ttu-id="efa2b-133">Merhaba SDK kod değişiklikleri kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="efa2b-133">hello SDK can be used without any code changes.</span></span> <span data-ttu-id="efa2b-134">Bu durumda, SDK otomatik olarak doğrudan hello hem okur ve toohello geçerli yazma bölge yazar.</span><span class="sxs-lookup"><span data-stu-id="efa2b-134">In this case, hello SDK will automatically direct both reads and writes toohello current write region.</span></span>

<span data-ttu-id="efa2b-135">Sürüm 1,8 ve daha sonra her SDK'sının hello ConnectionPolicy parametre hello DocumentClient Oluşturucusu DocumentClient.ConnectionPolicy.PreferredLocations adlı yeni bir özellik için.</span><span class="sxs-lookup"><span data-stu-id="efa2b-135">In version 1.8 and later of each SDK, hello ConnectionPolicy parameter for hello DocumentClient constructor a new property called DocumentClient.ConnectionPolicy.PreferredLocations.</span></span> <span data-ttu-id="efa2b-136">Bu parametre olan bölge adlarının bir listesini alan bir dizeler dizisi.</span><span class="sxs-lookup"><span data-stu-id="efa2b-136">This is parameter is an array of strings that takes a list of region names.</span></span> <span data-ttu-id="efa2b-137">Merhaba bölge adı hello sütununda başına biçimli Hello adları [Azure bölgeleri] [ regions] sayfası.</span><span class="sxs-lookup"><span data-stu-id="efa2b-137">hello names are formatted per hello Region Name column in hello [Azure Regions][regions] page.</span></span> <span data-ttu-id="efa2b-138">Önceden tanımlanmış hello sabitleri hello kolaylık nesne AzureDocuments.Regions kullanabilirsiniz</span><span class="sxs-lookup"><span data-stu-id="efa2b-138">You can also use hello predefined constants in hello convenience object AzureDocuments.Regions</span></span>

<span data-ttu-id="efa2b-139">Merhaba geçerli yazma ve okuma uç noktaları sırasıyla DocumentClient.getWriteEndpoint ve DocumentClient.getReadEndpoint kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="efa2b-139">hello current write and read endpoints are available in DocumentClient.getWriteEndpoint and DocumentClient.getReadEndpoint respectively.</span></span>

> [!NOTE]
> <span data-ttu-id="efa2b-140">Merhaba URL'leri hello uç noktalar için uzun süreli sabitleri düşünülmemelidir.</span><span class="sxs-lookup"><span data-stu-id="efa2b-140">hello URLs for hello endpoints should not be considered as long-lived constants.</span></span> <span data-ttu-id="efa2b-141">Merhaba hizmet bunlar herhangi bir noktada güncelleştirebilir.</span><span class="sxs-lookup"><span data-stu-id="efa2b-141">hello service may update these at any point.</span></span> <span data-ttu-id="efa2b-142">Merhaba SDK bu değişikliği otomatik olarak işler.</span><span class="sxs-lookup"><span data-stu-id="efa2b-142">hello SDK will handle this change automatically.</span></span>
>
>

<span data-ttu-id="efa2b-143">NodeJS/Javascript için bir kod örneği aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="efa2b-143">Below is a code example for NodeJS/Javascript.</span></span> <span data-ttu-id="efa2b-144">Python ve Java hello izleyecek aynı düzeni.</span><span class="sxs-lookup"><span data-stu-id="efa2b-144">Python and Java will follow hello same pattern.</span></span>

```java
// Creating a ConnectionPolicy object
var connectionPolicy = new DocumentBase.ConnectionPolicy();

// Setting read region selection preference, in hello following order -
// 1 - West US
// 2 - East US
// 3 - North Europe
connectionPolicy.PreferredLocations = ['West US', 'East US', 'North Europe'];

// initialize hello connection
var client = new DocumentDBClient(host, { masterKey: masterKey }, connectionPolicy);
```

## <a name="rest"></a><span data-ttu-id="efa2b-145">REST</span><span class="sxs-lookup"><span data-stu-id="efa2b-145">REST</span></span>
<span data-ttu-id="efa2b-146">Veritabanı hesabı birden çok bölgede kullanılabilir yapıldıktan sonra istemciler kendi kullanılabilirlik URI aşağıdaki hello üzerinde bir GET isteği gerçekleştirerek sorgulayabilir.</span><span class="sxs-lookup"><span data-stu-id="efa2b-146">Once a database account has been made available in multiple regions, clients can query its availability by performing a GET request on hello following URI.</span></span>

    https://{databaseaccount}.documents.azure.com/

<span data-ttu-id="efa2b-147">Merhaba hizmet bölgeler ve bunların karşılık gelen Azure Cosmos DB uç noktası URI için hello çoğaltmaları listesini döndürür.</span><span class="sxs-lookup"><span data-stu-id="efa2b-147">hello service will return a list of regions and their corresponding Azure Cosmos DB endpoint URIs for hello replicas.</span></span> <span data-ttu-id="efa2b-148">Merhaba geçerli yazma bölge hello yanıt olarak belirtilir.</span><span class="sxs-lookup"><span data-stu-id="efa2b-148">hello current write region will be indicated in hello response.</span></span> <span data-ttu-id="efa2b-149">Merhaba istemci hello uygun uç noktası daha fazla tüm REST API istekleri için daha sonra şu şekilde seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="efa2b-149">hello client can then select hello appropriate endpoint for all further REST API requests as follows.</span></span>

<span data-ttu-id="efa2b-150">Örnek yanıt</span><span class="sxs-lookup"><span data-stu-id="efa2b-150">Example response</span></span>

    {
        "_dbs": "//dbs/",
        "media": "//media/",
        "writableLocations": [
            {
                "Name": "West US",
                "DatabaseAccountEndpoint": "https://globaldbexample-westus.documents.azure.com:443/"
            }
        ],
        "readableLocations": [
            {
                "Name": "East US",
                "DatabaseAccountEndpoint": "https://globaldbexample-eastus.documents.azure.com:443/"
            }
        ],
        "MaxMediaStorageUsageInMB": 2048,
        "MediaStorageUsageInMB": 0,
        "ConsistencyPolicy": {
            "defaultConsistencyLevel": "Session",
            "maxStalenessPrefix": 100,
            "maxIntervalInSeconds": 5
        },
        "addresses": "//addresses/",
        "id": "globaldbexample",
        "_rid": "globaldbexample.documents.azure.com",
        "_self": "",
        "_ts": 0,
        "_etag": null
    }


* <span data-ttu-id="efa2b-151">Tüm PUT, POST ve DELETE isteklerini gitmelidir belirtilen toohello URI yazma</span><span class="sxs-lookup"><span data-stu-id="efa2b-151">All PUT, POST and DELETE requests must go toohello indicated write URI</span></span>
* <span data-ttu-id="efa2b-152">Tüm alır ve diğer salt okunur istekleri (örneğin sorgular) tooany endpoint hello istemcinin tercih gidebilir</span><span class="sxs-lookup"><span data-stu-id="efa2b-152">All GETs and other read-only requests (for example queries) may go tooany endpoint of hello client’s choice</span></span>

<span data-ttu-id="efa2b-153">Yazma isteklerini yalnızca tooread bölgeler 403 ("Yasak") HTTP hata koduyla başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="efa2b-153">Write requests tooread-only regions will fail with HTTP error code 403 (“Forbidden”).</span></span>

<span data-ttu-id="efa2b-154">Merhaba yazma bölge sonra değişirse hello istemcinin ilk bulma aşaması, sonraki toohello önceki yazma bölge 403 ("Yasak") HTTP hata koduyla başarısız olur yazar.</span><span class="sxs-lookup"><span data-stu-id="efa2b-154">If hello write region changes after hello client’s initial discovery phase, subsequent writes toohello previous write region will fail with HTTP error code 403 (“Forbidden”).</span></span> <span data-ttu-id="efa2b-155">Merhaba istemci sonra hello bölgelerin listesi yeniden tooget hello güncelleştirilmiş yazma bölge ALMANIZ gerekir.</span><span class="sxs-lookup"><span data-stu-id="efa2b-155">hello client should then GET hello list of regions again tooget hello updated write region.</span></span>

<span data-ttu-id="efa2b-156">Bu, bu öğreticinin tamamlanan kadar.</span><span class="sxs-lookup"><span data-stu-id="efa2b-156">That's it, that completes this tutorial.</span></span> <span data-ttu-id="efa2b-157">Nasıl toomanage hello genel çoğaltılmış hesabınızı tutarlılığını okuyarak öğrenebilirsiniz [Azure Cosmos veritabanı tutarlılık düzeylerini](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="efa2b-157">You can learn how toomanage hello consistency of your globally replicated account by reading [Consistency levels in Azure Cosmos DB](consistency-levels.md).</span></span> <span data-ttu-id="efa2b-158">Ve Azure Cosmos DB'de nasıl genel veritabanı çoğaltma hakkında daha fazla bilgi çalıştığı için bkz: [Azure Cosmos DB genel verilerle dağıtmak](distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="efa2b-158">And for more information about how global database replication works in Azure Cosmos DB, see [Distribute data globally with Azure Cosmos DB](distribute-data-globally.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="efa2b-159">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="efa2b-159">Next steps</span></span>

<span data-ttu-id="efa2b-160">Bu öğreticide, hello aşağıdakileri yaptığınızdan:</span><span class="sxs-lookup"><span data-stu-id="efa2b-160">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="efa2b-161">Genel dağıtım Hello Azure portal kullanarak yapılandırma</span><span class="sxs-lookup"><span data-stu-id="efa2b-161">Configure global distribution using hello Azure portal</span></span>
> * <span data-ttu-id="efa2b-162">Merhaba DocumentDB API'leri kullanılarak genel dağıtım yapılandırma</span><span class="sxs-lookup"><span data-stu-id="efa2b-162">Configure global distribution using hello DocumentDB APIs</span></span>

<span data-ttu-id="efa2b-163">Toohello sonraki öğretici toolearn şimdi devam etmek için nasıl Azure Cosmos DB yerel öykünücüsü kullanarak yerel olarak toodevelop hello.</span><span class="sxs-lookup"><span data-stu-id="efa2b-163">You can now proceed toohello next tutorial toolearn how toodevelop locally using hello Azure Cosmos DB local emulator.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="efa2b-164">Yerel olarak hello öykünücü ile geliştirme</span><span class="sxs-lookup"><span data-stu-id="efa2b-164">Develop locally with hello emulator</span></span>](local-emulator.md)

[regions]: https://azure.microsoft.com/regions/

