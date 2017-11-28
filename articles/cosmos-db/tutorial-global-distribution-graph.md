---
title: "Grafik API'si için aaaAzure Cosmos DB genel dağıtım Öğreticisi | Microsoft Docs"
description: "Nasıl toosetup Azure Cosmos DB genel dağıtım kullanarak izin ver hello grafik API'si hakkında bilgi edinin."
services: cosmos-db
keywords: "genel dağıtım, grafik, gremlin"
documentationcenter: 
author: dennyglee
manager: jhubbard
editor: cgronlun
ms.assetid: 8b815047-2868-4b10-af1d-40a1af419a70
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: denlee
ms.openlocfilehash: 1629a31e12a18079f63e07c4909862b36b5f4c0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosetup-azure-cosmos-db-global-distribution-using-hello-graph-api"></a><span data-ttu-id="d8928-104">Nasıl toosetup Azure Cosmos DB genel dağıtım kullanarak izin ver hello grafik API'si</span><span class="sxs-lookup"><span data-stu-id="d8928-104">How toosetup Azure Cosmos DB global distribution using hello Graph API</span></span>

<span data-ttu-id="d8928-105">Bu makalede, nasıl toouse Azure portal toosetup Azure Cosmos DB genel dağıtım hello ve hello grafik API'si (Önizleme) kullanarak bağlanmak gösterir.</span><span class="sxs-lookup"><span data-stu-id="d8928-105">In this article, we show how toouse hello Azure portal toosetup Azure Cosmos DB global distribution and then connect using hello Graph API (preview).</span></span>

<span data-ttu-id="d8928-106">Bu makalede görevleri aşağıdaki hello yer almaktadır:</span><span class="sxs-lookup"><span data-stu-id="d8928-106">This article covers hello following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="d8928-107">Genel dağıtım Hello Azure portal kullanarak yapılandırma</span><span class="sxs-lookup"><span data-stu-id="d8928-107">Configure global distribution using hello Azure portal</span></span>
> * <span data-ttu-id="d8928-108">Hello kullanarak genel dağıtım yapılandırma [Graph API](graph-introduction.md) (Önizleme)</span><span class="sxs-lookup"><span data-stu-id="d8928-108">Configure global distribution using hello [Graph APIs](graph-introduction.md) (preview)</span></span>

[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]


## <a name="connecting-tooa-preferred-region-using-hello-graph-api-using-hello-net-sdk"></a><span data-ttu-id="d8928-109">Tooa tercih edilen bölge Hello .NET SDK kullanarak hello grafik API'sini kullanarak bağlanma</span><span class="sxs-lookup"><span data-stu-id="d8928-109">Connecting tooa preferred region using hello Graph API using hello .NET SDK</span></span>

<span data-ttu-id="d8928-110">Merhaba grafik API'si hello DocumentDB SDK'sı en üstünde bir uzantı kitaplığı olarak sunulur.</span><span class="sxs-lookup"><span data-stu-id="d8928-110">hello Graph API is exposed as an extension library on top of hello DocumentDB SDK.</span></span>

<span data-ttu-id="d8928-111">Sipariş tootake avantajlarından içinde [genel dağıtım](distribute-data-globally.md), istemci uygulamalarının hello sıralı kullanılan tooperform belge işlemleri bölgeleri toobe tercih listesi belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d8928-111">In order tootake advantage of [global distribution](distribute-data-globally.md), client applications can specify hello ordered preference list of regions toobe used tooperform document operations.</span></span> <span data-ttu-id="d8928-112">Bu, başlangıç bağlantı İlkesi ayarlayarak yapılabilir.</span><span class="sxs-lookup"><span data-stu-id="d8928-112">This can be done by setting hello connection policy.</span></span> <span data-ttu-id="d8928-113">Hello Azure Cosmos DB hesap yapılandırmasını temel alarak, geçerli bölge kullanılabilirliği ve hello tercih listesi belirtilmezse, çoğu en iyi uç noktası hello SDK tooperform yazma tarafından seçilen ve okuma işlemlerini hello.</span><span class="sxs-lookup"><span data-stu-id="d8928-113">Based on hello Azure Cosmos DB account configuration, current regional availability and hello preference list specified, hello most optimal endpoint will be chosen by hello SDK tooperform write and read operations.</span></span>

<span data-ttu-id="d8928-114">Bu tercih listesi hello SDK'ları kullanarak bağlantı başlatırken belirtilir.</span><span class="sxs-lookup"><span data-stu-id="d8928-114">This preference list is specified when initializing a connection using hello SDKs.</span></span> <span data-ttu-id="d8928-115">Merhaba SDK'ları isteğe bağlı bir parametre "PreferredLocations" kabul Azure bölgeleri diğer bir deyişle sıralı bir listesi.</span><span class="sxs-lookup"><span data-stu-id="d8928-115">hello SDKs accept an optional parameter "PreferredLocations" that is an ordered list of Azure regions.</span></span>

* <span data-ttu-id="d8928-116">**Yazar**: SDK otomatik olarak tüm gönderecek hello toohello geçerli yazma bölge yazar.</span><span class="sxs-lookup"><span data-stu-id="d8928-116">**Writes**: hello SDK will automatically send all writes toohello current write region.</span></span>
* <span data-ttu-id="d8928-117">**Okur**: tüm okuma hello PreferredLocations listesinde toohello ilk kullanılabilir bölge gönderilir.</span><span class="sxs-lookup"><span data-stu-id="d8928-117">**Reads**: All reads will be sent toohello first available region in hello PreferredLocations list.</span></span> <span data-ttu-id="d8928-118">Merhaba isteği başarısız olursa, hello istemci hello listesi toohello sonraki bölgeyi başarısız ve benzeri.</span><span class="sxs-lookup"><span data-stu-id="d8928-118">If hello request fails, hello client will fail down hello list toohello next region, and so on.</span></span> <span data-ttu-id="d8928-119">Merhaba SDK'ları yalnızca tooread PreferredLocations içinde belirtilen hello bölgelerinden deneyecek.</span><span class="sxs-lookup"><span data-stu-id="d8928-119">hello SDKs will only attempt tooread from hello regions specified in PreferredLocations.</span></span> <span data-ttu-id="d8928-120">Bu nedenle, örneğin, hello Cosmos DB hesap üç bölgelerde kullanılabilir, ancak PreferredLocations için iki hello yazma olmayan bölgeleri yalnızca hello istemci belirtir, sonra okuma yük devretme hello durumda bile hello yazma bölgesi dışında sunulacak.</span><span class="sxs-lookup"><span data-stu-id="d8928-120">So, for example, if hello Cosmos DB account is available in three regions, but hello client only specifies two of hello non-write regions for PreferredLocations, then no reads will be served out of hello write region, even in hello case of failover.</span></span>

<span data-ttu-id="d8928-121">Merhaba uygulaması hello geçerli yazma uç noktası doğrulayın ve uç nokta denetimi iki özellikleri, WriteEndpoint ve ReadEndpoint, SDK sürümü 1.8 ve üzeri kullanılabilir tarafından hello SDK tarafından seçilen okuyun.</span><span class="sxs-lookup"><span data-stu-id="d8928-121">hello application can verify hello current write endpoint and read endpoint chosen by hello SDK by checking two properties, WriteEndpoint and ReadEndpoint, available in SDK version 1.8 and above.</span></span> <span data-ttu-id="d8928-122">Merhaba PreferredLocations özellik ayarlanmamışsa, tüm istekleri hello geçerli yazma bölgesinden sunulacak.</span><span class="sxs-lookup"><span data-stu-id="d8928-122">If hello PreferredLocations property is not set, all requests will be served from hello current write region.</span></span>

### <a name="using-hello-sdk"></a><span data-ttu-id="d8928-123">Merhaba SDK kullanma</span><span class="sxs-lookup"><span data-stu-id="d8928-123">Using hello SDK</span></span>

<span data-ttu-id="d8928-124">Örneğin, hello .NET SDK'sı, hello `ConnectionPolicy` parametresi hello için `DocumentClient` Oluşturucusu adlı bir özelliği vardır `PreferredLocations`.</span><span class="sxs-lookup"><span data-stu-id="d8928-124">For example, in hello .NET SDK, hello `ConnectionPolicy` parameter for hello `DocumentClient` constructor has a property called `PreferredLocations`.</span></span> <span data-ttu-id="d8928-125">Bu özellik tooa bölge adları listesi ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d8928-125">This property can be set tooa list of region names.</span></span> <span data-ttu-id="d8928-126">Merhaba görünen adları için [Azure bölgeleri] [ regions] parçası olarak belirtilen `PreferredLocations`.</span><span class="sxs-lookup"><span data-stu-id="d8928-126">hello display names for [Azure Regions][regions] can be specified as part of `PreferredLocations`.</span></span>

> [!NOTE]
> <span data-ttu-id="d8928-127">Merhaba URL'leri hello uç noktalar için uzun süreli sabitleri düşünülmemelidir.</span><span class="sxs-lookup"><span data-stu-id="d8928-127">hello URLs for hello endpoints should not be considered as long-lived constants.</span></span> <span data-ttu-id="d8928-128">Merhaba hizmet bunlar herhangi bir noktada güncelleştirebilir.</span><span class="sxs-lookup"><span data-stu-id="d8928-128">hello service may update these at any point.</span></span> <span data-ttu-id="d8928-129">Merhaba SDK bu değişikliği otomatik olarak yönetir.</span><span class="sxs-lookup"><span data-stu-id="d8928-129">hello SDK handles this change automatically.</span></span>
>
>

```cs
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

// connect tooAzure Cosmos DB
await docClient.OpenAsync().ConfigureAwait(false);
```

<span data-ttu-id="d8928-130">Bu, bu öğreticinin tamamlanan kadar.</span><span class="sxs-lookup"><span data-stu-id="d8928-130">That's it, that completes this tutorial.</span></span> <span data-ttu-id="d8928-131">Nasıl toomanage hello genel çoğaltılmış hesabınızı tutarlılığını okuyarak öğrenebilirsiniz [Azure Cosmos veritabanı tutarlılık düzeylerini](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="d8928-131">You can learn how toomanage hello consistency of your globally replicated account by reading [Consistency levels in Azure Cosmos DB](consistency-levels.md).</span></span> <span data-ttu-id="d8928-132">Ve Azure Cosmos DB'de nasıl genel veritabanı çoğaltma hakkında daha fazla bilgi çalıştığı için bkz: [Azure Cosmos DB genel verilerle dağıtmak](distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="d8928-132">And for more information about how global database replication works in Azure Cosmos DB, see [Distribute data globally with Azure Cosmos DB](distribute-data-globally.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d8928-133">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d8928-133">Next steps</span></span>

<span data-ttu-id="d8928-134">Bu öğreticide, hello aşağıdakileri yaptığınızdan:</span><span class="sxs-lookup"><span data-stu-id="d8928-134">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d8928-135">Genel dağıtım Hello Azure portal kullanarak yapılandırma</span><span class="sxs-lookup"><span data-stu-id="d8928-135">Configure global distribution using hello Azure portal</span></span>
> * <span data-ttu-id="d8928-136">Merhaba DocumentDB API'leri kullanılarak genel dağıtım yapılandırma</span><span class="sxs-lookup"><span data-stu-id="d8928-136">Configure global distribution using hello DocumentDB APIs</span></span>

<span data-ttu-id="d8928-137">Toohello sonraki öğretici toolearn şimdi devam etmek için nasıl Azure Cosmos DB yerel öykünücüsü kullanarak yerel olarak toodevelop hello.</span><span class="sxs-lookup"><span data-stu-id="d8928-137">You can now proceed toohello next tutorial toolearn how toodevelop locally using hello Azure Cosmos DB local emulator.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d8928-138">Yerel olarak hello öykünücü ile geliştirme</span><span class="sxs-lookup"><span data-stu-id="d8928-138">Develop locally with hello emulator</span></span>](local-emulator.md)

[regions]: https://azure.microsoft.com/regions/

