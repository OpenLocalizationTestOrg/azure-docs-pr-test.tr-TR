---
title: "Tablo API için aaaAzure Cosmos DB genel dağıtım Öğreticisi | Microsoft Docs"
description: "Nasıl toosetup Azure Cosmos DB genel dağıtım kullanarak izin ver hello tablo API öğrenin."
services: cosmos-db
keywords: "genel dağıtım, tablo"
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
ms.openlocfilehash: d2a995e09c37f9449856aef2ab707e95eb8a540c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosetup-azure-cosmos-db-global-distribution-using-hello-table-api"></a><span data-ttu-id="5e25b-104">Nasıl toosetup Azure Cosmos DB genel dağıtım kullanarak izin ver hello tablo API</span><span class="sxs-lookup"><span data-stu-id="5e25b-104">How toosetup Azure Cosmos DB global distribution using hello Table API</span></span>

<span data-ttu-id="5e25b-105">Bu makalede, nasıl toouse Azure portal toosetup Azure Cosmos DB genel dağıtım hello ve hello tablo API (Önizleme) kullanarak bağlanmak gösterir.</span><span class="sxs-lookup"><span data-stu-id="5e25b-105">In this article, we show how toouse hello Azure portal toosetup Azure Cosmos DB global distribution and then connect using hello Table API (preview).</span></span>

<span data-ttu-id="5e25b-106">Bu makalede görevleri aşağıdaki hello yer almaktadır:</span><span class="sxs-lookup"><span data-stu-id="5e25b-106">This article covers hello following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="5e25b-107">Genel dağıtım Hello Azure portal kullanarak yapılandırma</span><span class="sxs-lookup"><span data-stu-id="5e25b-107">Configure global distribution using hello Azure portal</span></span>
> * <span data-ttu-id="5e25b-108">Hello kullanarak genel dağıtım yapılandırma [tablo API](table-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="5e25b-108">Configure global distribution using hello [Table API](table-introduction.md)</span></span>

[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]


## <a name="connecting-tooa-preferred-region-using-hello-table-api"></a><span data-ttu-id="5e25b-109">Tooa tercih edilen bölge Hello tablo API kullanarak bağlanma</span><span class="sxs-lookup"><span data-stu-id="5e25b-109">Connecting tooa preferred region using hello Table API</span></span>

<span data-ttu-id="5e25b-110">Sipariş tootake avantajlarından içinde [genel dağıtım](distribute-data-globally.md), istemci uygulamalarının hello sıralı kullanılan tooperform belge işlemleri bölgeleri toobe tercih listesi belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5e25b-110">In order tootake advantage of [global distribution](distribute-data-globally.md), client applications can specify hello ordered preference list of regions toobe used tooperform document operations.</span></span> <span data-ttu-id="5e25b-111">Bu ayarı hello tarafından yapılabilir `TablePreferredLocations` hello uygulama yapılandırması hello Önizleme Azure depolama SDK'sı için yapılandırma değeri.</span><span class="sxs-lookup"><span data-stu-id="5e25b-111">This can be done by setting hello `TablePreferredLocations` configuration value in hello app config for hello preview Azure Storage SDK.</span></span> <span data-ttu-id="5e25b-112">Hello Azure Cosmos DB hesap yapılandırmasını temel alarak, geçerli bölge kullanılabilirliği ve belirtilen hello tercih listesi en iyi endpoint hello Azure depolama SDK'sı tooperform tarafından seçilir hello yazma ve okuma işlemleri.</span><span class="sxs-lookup"><span data-stu-id="5e25b-112">Based on hello Azure Cosmos DB account configuration, current regional availability and hello preference list specified, hello most optimal endpoint will be chosen by hello Azure Storage SDK tooperform write and read operations.</span></span>

<span data-ttu-id="5e25b-113">Merhaba `TablePreferredLocations` okuma için tercih edilen (çok girişli) konumları, virgülle ayrılmış listesini içermelidir.</span><span class="sxs-lookup"><span data-stu-id="5e25b-113">hello `TablePreferredLocations` should contain a comma-separated list of preferred (multi-homing) locations for reads.</span></span> <span data-ttu-id="5e25b-114">Her istemci örneği, düşük gecikme süresi okumalar için tercih edilen hello sırayla Bu bölgeler kümesini belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5e25b-114">Each client instance can specify a subset of these regions in hello preferred order for low latency reads.</span></span> <span data-ttu-id="5e25b-115">Merhaba bölgeler gerekir adlı kullanarak kendi [görünen adları](https://msdn.microsoft.com/library/azure/gg441293.aspx), örneğin, `West US`.</span><span class="sxs-lookup"><span data-stu-id="5e25b-115">hello regions must be named using their [display names](https://msdn.microsoft.com/library/azure/gg441293.aspx), for example, `West US`.</span></span>

<span data-ttu-id="5e25b-116">Tüm okuma toohello ilk kullanılabilir bölge hello gönderilecek `TablePreferredLocations` listesi.</span><span class="sxs-lookup"><span data-stu-id="5e25b-116">All reads will be sent toohello first available region in hello `TablePreferredLocations` list.</span></span> <span data-ttu-id="5e25b-117">Merhaba isteği başarısız olursa, hello istemci hello listesi toohello sonraki bölgeyi başarısız ve benzeri.</span><span class="sxs-lookup"><span data-stu-id="5e25b-117">If hello request fails, hello client will fail down hello list toohello next region, and so on.</span></span>

<span data-ttu-id="5e25b-118">Merhaba SDK yalnızca belirtilen hello bölgelerinden tooread denemesi `TablePreferredLocations`.</span><span class="sxs-lookup"><span data-stu-id="5e25b-118">hello SDK will only attempt tooread from hello regions specified in `TablePreferredLocations`.</span></span> <span data-ttu-id="5e25b-119">Bu nedenle, örneğin, hello veritabanı hesabı üç bölgelerde kullanılabilir, ancak hello istemci yalnızca belirtir iki yazma olmayan bölgeleri için hello `TablePreferredLocations`, yük devretme hello durumda bile hello yazma bölgesi dışında okuma sunulacak sonra.</span><span class="sxs-lookup"><span data-stu-id="5e25b-119">So, for example, if hello Database Account is available in three regions, but hello client only specifies two of hello non-write regions for `TablePreferredLocations`, then no reads will be served out of hello write region, even in hello case of failover.</span></span>

<span data-ttu-id="5e25b-120">Merhaba SDK tüm yazma toohello geçerli yazma bölge otomatik olarak gönderir.</span><span class="sxs-lookup"><span data-stu-id="5e25b-120">hello SDK will automatically send all writes toohello current write region.</span></span>

<span data-ttu-id="5e25b-121">Merhaba, `TablePreferredLocations` özellik ayarlanmamışsa, tüm istekleri hello geçerli yazma bölgesinden sunulacak.</span><span class="sxs-lookup"><span data-stu-id="5e25b-121">If hello `TablePreferredLocations` property is not set, all requests will be served from hello current write region.</span></span>

```xml
    <appSettings>
      <add key="TablePreferredLocations" value="East US, West US, North Europe"/>           
    </appSettings>
```

<span data-ttu-id="5e25b-122">Bu, bu öğreticinin tamamlanan kadar.</span><span class="sxs-lookup"><span data-stu-id="5e25b-122">That's it, that completes this tutorial.</span></span> <span data-ttu-id="5e25b-123">Nasıl toomanage hello genel çoğaltılmış hesabınızı tutarlılığını okuyarak öğrenebilirsiniz [Azure Cosmos veritabanı tutarlılık düzeylerini](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="5e25b-123">You can learn how toomanage hello consistency of your globally replicated account by reading [Consistency levels in Azure Cosmos DB](consistency-levels.md).</span></span> <span data-ttu-id="5e25b-124">Ve Azure Cosmos DB'de nasıl genel veritabanı çoğaltma hakkında daha fazla bilgi çalıştığı için bkz: [Azure Cosmos DB genel verilerle dağıtmak](distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="5e25b-124">And for more information about how global database replication works in Azure Cosmos DB, see [Distribute data globally with Azure Cosmos DB](distribute-data-globally.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="5e25b-125">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5e25b-125">Next steps</span></span>

<span data-ttu-id="5e25b-126">Bu öğreticide, hello aşağıdakileri yaptığınızdan:</span><span class="sxs-lookup"><span data-stu-id="5e25b-126">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="5e25b-127">Genel dağıtım Hello Azure portal kullanarak yapılandırma</span><span class="sxs-lookup"><span data-stu-id="5e25b-127">Configure global distribution using hello Azure portal</span></span>
> * <span data-ttu-id="5e25b-128">Merhaba DocumentDB API'leri kullanılarak genel dağıtım yapılandırma</span><span class="sxs-lookup"><span data-stu-id="5e25b-128">Configure global distribution using hello DocumentDB APIs</span></span>

<span data-ttu-id="5e25b-129">Toohello sonraki öğretici toolearn şimdi devam etmek için nasıl Azure Cosmos DB yerel öykünücüsü kullanarak yerel olarak toodevelop hello.</span><span class="sxs-lookup"><span data-stu-id="5e25b-129">You can now proceed toohello next tutorial toolearn how toodevelop locally using hello Azure Cosmos DB local emulator.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="5e25b-130">Yerel olarak hello öykünücü ile geliştirme</span><span class="sxs-lookup"><span data-stu-id="5e25b-130">Develop locally with hello emulator</span></span>](local-emulator.md)
