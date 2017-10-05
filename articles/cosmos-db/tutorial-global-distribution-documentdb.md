---
title: "DocumentDB API için Azure Cosmos DB genel dağıtım Öğreticisi | Microsoft Docs"
description: "DocumentDB API kullanarak Azure Cosmos DB genel dağıtım Kurulum öğrenin."
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
ms.openlocfilehash: f4d8efe9814bd28bb902567a23b541bc9b5414a1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-setup-azure-cosmos-db-global-distribution-using-the-documentdb-api"></a><span data-ttu-id="4d42d-104">DocumentDB API kullanarak Azure Cosmos DB genel dağıtım ayarlama</span><span class="sxs-lookup"><span data-stu-id="4d42d-104">How to setup Azure Cosmos DB global distribution using the DocumentDB API</span></span>

<span data-ttu-id="4d42d-105">Bu makalede, Azure portalında Azure Cosmos DB genel dağıtım kurulumu ve DocumentDB API kullanarak bağlanmak için nasıl kullanılacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="4d42d-105">In this article, we show how to use the Azure portal to setup Azure Cosmos DB global distribution and then connect using the DocumentDB API.</span></span>

<span data-ttu-id="4d42d-106">Bu makalede aşağıdaki görevleri içerir:</span><span class="sxs-lookup"><span data-stu-id="4d42d-106">This article covers the following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="4d42d-107">Azure portalını kullanarak genel dağıtım yapılandırma</span><span class="sxs-lookup"><span data-stu-id="4d42d-107">Configure global distribution using the Azure portal</span></span>
> * <span data-ttu-id="4d42d-108">Genel dağıtım kullanarak yapılandırma [DocumentDB API'leri](documentdb-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="4d42d-108">Configure global distribution using the [DocumentDB APIs](documentdb-introduction.md)</span></span>

<a id="portal"></a>
[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]


## <a name="connecting-to-a-preferred-region-using-the-documentdb-api"></a><span data-ttu-id="4d42d-109">DocumentDB API kullanarak bir tercih edilen bölge bağlanma</span><span class="sxs-lookup"><span data-stu-id="4d42d-109">Connecting to a preferred region using the DocumentDB API</span></span>

<span data-ttu-id="4d42d-110">Anlamıyla yararlanabilmek için [genel dağıtım](distribute-data-globally.md), istemci uygulamaları, belge işlemlerini gerçekleştirmek için kullanılacak bölgelerin sıralı tercih listesi belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4d42d-110">In order to take advantage of [global distribution](distribute-data-globally.md), client applications can specify the ordered preference list of regions to be used to perform document operations.</span></span> <span data-ttu-id="4d42d-111">Bu bağlantı İlkesi ayarlayarak yapılabilir.</span><span class="sxs-lookup"><span data-stu-id="4d42d-111">This can be done by setting the connection policy.</span></span> <span data-ttu-id="4d42d-112">Azure Cosmos DB hesabı yapılandırması, geçerli bölge kullanılabilirliği ve belirtilen tercih listesi bağlı olarak, en iyi endpoint yazma gerçekleştirmek ve okuma işlemleri için DocumentDB SDK tarafından seçilir.</span><span class="sxs-lookup"><span data-stu-id="4d42d-112">Based on the Azure Cosmos DB account configuration, current regional availability and the preference list specified, the most optimal endpoint will be chosen by the DocumentDB SDK to perform write and read operations.</span></span>

<span data-ttu-id="4d42d-113">Bu tercih listesi DocumentDB SDK'ları kullanarak bağlantı başlatırken belirtilir.</span><span class="sxs-lookup"><span data-stu-id="4d42d-113">This preference list is specified when initializing a connection using the DocumentDB SDKs.</span></span> <span data-ttu-id="4d42d-114">SDK'ları isteğe bağlı bir parametre "PreferredLocations" kabul Azure bölgeleri diğer bir deyişle sıralı bir listesi.</span><span class="sxs-lookup"><span data-stu-id="4d42d-114">The SDKs accept an optional parameter "PreferredLocations" that is an ordered list of Azure regions.</span></span>

<span data-ttu-id="4d42d-115">SDK, bölge geçerli tüm yazma işlemlerini yazma otomatik olarak gönderir.</span><span class="sxs-lookup"><span data-stu-id="4d42d-115">The SDK will automatically send all writes to the current write region.</span></span>

<span data-ttu-id="4d42d-116">İlk kullanılabilir bölge PreferredLocations listesindeki tüm okuma gönderilir.</span><span class="sxs-lookup"><span data-stu-id="4d42d-116">All reads will be sent to the first available region in the PreferredLocations list.</span></span> <span data-ttu-id="4d42d-117">İstek başarısız olursa, istemci listeyi sonraki bölgeyi başarısız ve benzeri.</span><span class="sxs-lookup"><span data-stu-id="4d42d-117">If the request fails, the client will fail down the list to the next region, and so on.</span></span>

<span data-ttu-id="4d42d-118">SDK'ları yalnızca PreferredLocations içinde belirtilen bölgeler okuma dener.</span><span class="sxs-lookup"><span data-stu-id="4d42d-118">The SDKs will only attempt to read from the regions specified in PreferredLocations.</span></span> <span data-ttu-id="4d42d-119">Bu nedenle, örneğin, veritabanı hesabı üç bölgelerde kullanılabilir, ancak PreferredLocations için iki yazma olmayan bölgeleri yalnızca istemci belirtir, sonra okuma yazma bölge, yük devretme durumunda bile dışında sunulacak.</span><span class="sxs-lookup"><span data-stu-id="4d42d-119">So, for example, if the Database Account is available in three regions, but the client only specifies two of the non-write regions for PreferredLocations, then no reads will be served out of the write region, even in the case of failover.</span></span>

<span data-ttu-id="4d42d-120">Uygulama, geçerli yazma uç noktası doğrulayın ve WriteEndpoint ve ReadEndpoint, SDK sürümü 1.8 ve üzeri kullanılabilir iki özelliklerini denetleyerek SDK tarafından seçilen endpoint okuyun.</span><span class="sxs-lookup"><span data-stu-id="4d42d-120">The application can verify the current write endpoint and read endpoint chosen by the SDK by checking two properties, WriteEndpoint and ReadEndpoint, available in SDK version 1.8 and above.</span></span>

<span data-ttu-id="4d42d-121">PreferredLocations özellik ayarlanmamışsa, tüm istekleri geçerli yazma bölgesinden sunulacak.</span><span class="sxs-lookup"><span data-stu-id="4d42d-121">If the PreferredLocations property is not set, all requests will be served from the current write region.</span></span>

## <a name="net-sdk"></a><span data-ttu-id="4d42d-122">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="4d42d-122">.NET SDK</span></span>
<span data-ttu-id="4d42d-123">SDK kod değişiklikleri kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="4d42d-123">The SDK can be used without any code changes.</span></span> <span data-ttu-id="4d42d-124">Bu durumda, SDK'yı otomatik olarak her iki okuma yönlendirir ve geçerli yazma bölgesine yazar.</span><span class="sxs-lookup"><span data-stu-id="4d42d-124">In this case, the SDK automatically directs both reads and writes to the current write region.</span></span>

<span data-ttu-id="4d42d-125">Sürüm 1,8 ve daha sonra .NET SDK'sına, ConnectionPolicy parametresi DocumentClient oluşturucusu için Microsoft.Azure.Documents.ConnectionPolicy.PreferredLocations adlı bir özelliğe sahiptir.</span><span class="sxs-lookup"><span data-stu-id="4d42d-125">In version 1.8 and later of the .NET SDK, the ConnectionPolicy parameter for the DocumentClient constructor has a property called Microsoft.Azure.Documents.ConnectionPolicy.PreferredLocations.</span></span> <span data-ttu-id="4d42d-126">Bu özellik koleksiyonu türünde `<string>` ve bölge adları listesi içermelidir.</span><span class="sxs-lookup"><span data-stu-id="4d42d-126">This property is of type Collection `<string>` and should contain a list of region names.</span></span> <span data-ttu-id="4d42d-127">Üzerinde biçimlendirilen dize değerleri bölge adı sütun başına [Azure bölgeleri] [ regions] boşluk önce veya sonra ilk sayfasında ve karakter sırasıyla en son.</span><span class="sxs-lookup"><span data-stu-id="4d42d-127">The string values are formatted per the Region Name column on the [Azure Regions][regions] page, with no spaces before or after the first and last character respectively.</span></span>

<span data-ttu-id="4d42d-128">Geçerli yazma ve okuma uç noktaları sırasıyla DocumentClient.WriteEndpoint ve DocumentClient.ReadEndpoint kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="4d42d-128">The current write and read endpoints are available in DocumentClient.WriteEndpoint and DocumentClient.ReadEndpoint respectively.</span></span>

> [!NOTE]
> <span data-ttu-id="4d42d-129">Uç noktalar için URL'leri uzun süreli sabitleri düşünülmemelidir.</span><span class="sxs-lookup"><span data-stu-id="4d42d-129">The URLs for the endpoints should not be considered as long-lived constants.</span></span> <span data-ttu-id="4d42d-130">Hizmet, bunlar herhangi bir noktada güncelleştirebilir.</span><span class="sxs-lookup"><span data-stu-id="4d42d-130">The service may update these at any point.</span></span> <span data-ttu-id="4d42d-131">SDK, bu değişiklik otomatik olarak yönetir.</span><span class="sxs-lookup"><span data-stu-id="4d42d-131">The SDK handles this change automatically.</span></span>
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

// connect to DocDB
await docClient.OpenAsync().ConfigureAwait(false);
```

## <a name="nodejs-javascript-and-python-sdks"></a><span data-ttu-id="4d42d-132">NodeJS, JavaScript ve Python SDK'ları</span><span class="sxs-lookup"><span data-stu-id="4d42d-132">NodeJS, JavaScript, and Python SDKs</span></span>
<span data-ttu-id="4d42d-133">SDK kod değişiklikleri kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="4d42d-133">The SDK can be used without any code changes.</span></span> <span data-ttu-id="4d42d-134">Bu durumda, SDK'yı otomatik olarak okuma ve yazma geçerli bölge yazma yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="4d42d-134">In this case, the SDK will automatically direct both reads and writes to the current write region.</span></span>

<span data-ttu-id="4d42d-135">Sürüm 1,8 ve her SDK'ın daha sonra ConnectionPolicy parametresi DocumentClient oluşturucusu için yeni bir özellik DocumentClient.ConnectionPolicy.PreferredLocations çağrılır.</span><span class="sxs-lookup"><span data-stu-id="4d42d-135">In version 1.8 and later of each SDK, the ConnectionPolicy parameter for the DocumentClient constructor a new property called DocumentClient.ConnectionPolicy.PreferredLocations.</span></span> <span data-ttu-id="4d42d-136">Bu parametre olan bölge adlarının bir listesini alan bir dizeler dizisi.</span><span class="sxs-lookup"><span data-stu-id="4d42d-136">This is parameter is an array of strings that takes a list of region names.</span></span> <span data-ttu-id="4d42d-137">Bölge adı sütununda başına biçimli adları [Azure bölgeleri] [ regions] sayfası.</span><span class="sxs-lookup"><span data-stu-id="4d42d-137">The names are formatted per the Region Name column in the [Azure Regions][regions] page.</span></span> <span data-ttu-id="4d42d-138">Önceden tanımlanmış sabitleri kolaylık nesnesinde AzureDocuments.Regions kullanabilirsiniz</span><span class="sxs-lookup"><span data-stu-id="4d42d-138">You can also use the predefined constants in the convenience object AzureDocuments.Regions</span></span>

<span data-ttu-id="4d42d-139">Geçerli yazma ve okuma uç noktaları sırasıyla DocumentClient.getWriteEndpoint ve DocumentClient.getReadEndpoint kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="4d42d-139">The current write and read endpoints are available in DocumentClient.getWriteEndpoint and DocumentClient.getReadEndpoint respectively.</span></span>

> [!NOTE]
> <span data-ttu-id="4d42d-140">Uç noktalar için URL'leri uzun süreli sabitleri düşünülmemelidir.</span><span class="sxs-lookup"><span data-stu-id="4d42d-140">The URLs for the endpoints should not be considered as long-lived constants.</span></span> <span data-ttu-id="4d42d-141">Hizmet, bunlar herhangi bir noktada güncelleştirebilir.</span><span class="sxs-lookup"><span data-stu-id="4d42d-141">The service may update these at any point.</span></span> <span data-ttu-id="4d42d-142">SDK bu değişikliği otomatik olarak işler.</span><span class="sxs-lookup"><span data-stu-id="4d42d-142">The SDK will handle this change automatically.</span></span>
>
>

<span data-ttu-id="4d42d-143">NodeJS/Javascript için bir kod örneği aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="4d42d-143">Below is a code example for NodeJS/Javascript.</span></span> <span data-ttu-id="4d42d-144">Python ve Java aynı düzeni izler.</span><span class="sxs-lookup"><span data-stu-id="4d42d-144">Python and Java will follow the same pattern.</span></span>

```java
// Creating a ConnectionPolicy object
var connectionPolicy = new DocumentBase.ConnectionPolicy();

// Setting read region selection preference, in the following order -
// 1 - West US
// 2 - East US
// 3 - North Europe
connectionPolicy.PreferredLocations = ['West US', 'East US', 'North Europe'];

// initialize the connection
var client = new DocumentDBClient(host, { masterKey: masterKey }, connectionPolicy);
```

## <a name="rest"></a><span data-ttu-id="4d42d-145">REST</span><span class="sxs-lookup"><span data-stu-id="4d42d-145">REST</span></span>
<span data-ttu-id="4d42d-146">Veritabanı hesabı birden çok bölgede kullanılabilir yapıldıktan sonra istemciler aşağıdaki URI üzerinde bir GET isteği gerçekleştirerek, kullanılabilirlik sorgulayabilir.</span><span class="sxs-lookup"><span data-stu-id="4d42d-146">Once a database account has been made available in multiple regions, clients can query its availability by performing a GET request on the following URI.</span></span>

    https://{databaseaccount}.documents.azure.com/

<span data-ttu-id="4d42d-147">Hizmet bölgeler ve bunların karşılık gelen Azure Cosmos DB uç noktası URI için çoğaltmaları listesini döndürür.</span><span class="sxs-lookup"><span data-stu-id="4d42d-147">The service will return a list of regions and their corresponding Azure Cosmos DB endpoint URIs for the replicas.</span></span> <span data-ttu-id="4d42d-148">Geçerli yazma bölgeyi yanıtında gösterilir.</span><span class="sxs-lookup"><span data-stu-id="4d42d-148">The current write region will be indicated in the response.</span></span> <span data-ttu-id="4d42d-149">İstemci ardından aşağıdaki gibi daha fazla tüm REST API istekleri için uygun uç noktası seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4d42d-149">The client can then select the appropriate endpoint for all further REST API requests as follows.</span></span>

<span data-ttu-id="4d42d-150">Örnek yanıt</span><span class="sxs-lookup"><span data-stu-id="4d42d-150">Example response</span></span>

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


* <span data-ttu-id="4d42d-151">Tüm PUT, POST ve DELETE isteklerini belirtilen yazma URI gitmeniz gerekir</span><span class="sxs-lookup"><span data-stu-id="4d42d-151">All PUT, POST and DELETE requests must go to the indicated write URI</span></span>
* <span data-ttu-id="4d42d-152">Tüm alır ve diğer salt okunur istekleri (örneğin sorgular) için istemcinin istediği herhangi bir uç nokta gidebilir</span><span class="sxs-lookup"><span data-stu-id="4d42d-152">All GETs and other read-only requests (for example queries) may go to any endpoint of the client’s choice</span></span>

<span data-ttu-id="4d42d-153">Yazma isteklerini salt okunur bölgelere 403 ("Yasak") HTTP hata koduyla başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="4d42d-153">Write requests to read-only regions will fail with HTTP error code 403 (“Forbidden”).</span></span>

<span data-ttu-id="4d42d-154">Yazma bölge sonra istemcinin ilk bulma aşama değişirse, önceki yazma bölgeye sonraki yazma 403 ("Yasak") HTTP hata koduyla başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="4d42d-154">If the write region changes after the client’s initial discovery phase, subsequent writes to the previous write region will fail with HTTP error code 403 (“Forbidden”).</span></span> <span data-ttu-id="4d42d-155">İstemci, daha sonra yeniden güncelleştirilmiş yazma bölge almak için bölgelerin listesi ALMANIZ gerekir.</span><span class="sxs-lookup"><span data-stu-id="4d42d-155">The client should then GET the list of regions again to get the updated write region.</span></span>

<span data-ttu-id="4d42d-156">Bu, bu öğreticinin tamamlanan kadar.</span><span class="sxs-lookup"><span data-stu-id="4d42d-156">That's it, that completes this tutorial.</span></span> <span data-ttu-id="4d42d-157">Genel olarak çoğaltılmış hesabınızı tutarlılığını okuyarak yönetmek nasıl öğrenebilirsiniz [Azure Cosmos veritabanı tutarlılık düzeylerini](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="4d42d-157">You can learn how to manage the consistency of your globally replicated account by reading [Consistency levels in Azure Cosmos DB](consistency-levels.md).</span></span> <span data-ttu-id="4d42d-158">Ve Azure Cosmos DB'de nasıl genel veritabanı çoğaltma hakkında daha fazla bilgi çalıştığı için bkz: [Azure Cosmos DB genel verilerle dağıtmak](distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="4d42d-158">And for more information about how global database replication works in Azure Cosmos DB, see [Distribute data globally with Azure Cosmos DB](distribute-data-globally.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4d42d-159">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4d42d-159">Next steps</span></span>

<span data-ttu-id="4d42d-160">Bu öğreticide, aşağıdakileri yaptığınızdan:</span><span class="sxs-lookup"><span data-stu-id="4d42d-160">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="4d42d-161">Azure portalını kullanarak genel dağıtım yapılandırma</span><span class="sxs-lookup"><span data-stu-id="4d42d-161">Configure global distribution using the Azure portal</span></span>
> * <span data-ttu-id="4d42d-162">DocumentDB API'lerini kullanarak genel dağıtım yapılandırma</span><span class="sxs-lookup"><span data-stu-id="4d42d-162">Configure global distribution using the DocumentDB APIs</span></span>

<span data-ttu-id="4d42d-163">Artık Azure Cosmos DB yerel öykünücüsü kullanarak yerel olarak geliştirme konusunda bilgi almak için sonraki öğretici devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4d42d-163">You can now proceed to the next tutorial to learn how to develop locally using the Azure Cosmos DB local emulator.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="4d42d-164">Yerel olarak öykünücü ile geliştirme</span><span class="sxs-lookup"><span data-stu-id="4d42d-164">Develop locally with the emulator</span></span>](local-emulator.md)

[regions]: https://azure.microsoft.com/regions/

