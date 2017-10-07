---
title: "MongoDB API için aaaAzure Cosmos DB genel dağıtım Öğreticisi | Microsoft Docs"
description: "Nasıl toosetup Azure Cosmos DB genel dağıtım kullanarak izin ver hello MongoDB API öğrenin."
services: cosmos-db
keywords: "genel dağıtım, MongoDB"
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
ms.openlocfilehash: 0fc2d670bb4e21ac5f813f9586b407ba06ccf354
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosetup-azure-cosmos-db-global-distribution-using-hello-mongodb-api"></a><span data-ttu-id="ea36d-104">Nasıl toosetup Azure Cosmos DB genel dağıtım kullanarak izin ver hello MongoDB API</span><span class="sxs-lookup"><span data-stu-id="ea36d-104">How toosetup Azure Cosmos DB global distribution using hello MongoDB API</span></span>

<span data-ttu-id="ea36d-105">Bu makalede, nasıl toouse Azure portal toosetup Azure Cosmos DB genel dağıtım hello ve hello MongoDB API kullanarak bağlanmak gösterir.</span><span class="sxs-lookup"><span data-stu-id="ea36d-105">In this article, we show how toouse hello Azure portal toosetup Azure Cosmos DB global distribution and then connect using hello MongoDB API.</span></span>

<span data-ttu-id="ea36d-106">Bu makalede görevleri aşağıdaki hello yer almaktadır:</span><span class="sxs-lookup"><span data-stu-id="ea36d-106">This article covers hello following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="ea36d-107">Genel dağıtım Hello Azure portal kullanarak yapılandırma</span><span class="sxs-lookup"><span data-stu-id="ea36d-107">Configure global distribution using hello Azure portal</span></span>
> * <span data-ttu-id="ea36d-108">Hello kullanarak genel dağıtım yapılandırma [MongoDB API](mongodb-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="ea36d-108">Configure global distribution using hello [MongoDB API](mongodb-introduction.md)</span></span>

[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]

## <a name="verifying-your-regional-setup-using-hello-mongodb-api"></a><span data-ttu-id="ea36d-109">Merhaba MongoDB API kullanarak bölgesel kurulumunuzu doğrulanıyor</span><span class="sxs-lookup"><span data-stu-id="ea36d-109">Verifying your regional setup using hello MongoDB API</span></span>
<span data-ttu-id="ea36d-110">en basit yolu MongoDB toorun hello için genel yapılandırmanızı API içinde denetleme çift Hello *isMaster()* hello Mongo kabuğunu komutunu.</span><span class="sxs-lookup"><span data-stu-id="ea36d-110">hello simplest way of double checking your global configuration within API for MongoDB is toorun hello *isMaster()* command from hello Mongo Shell.</span></span>

<span data-ttu-id="ea36d-111">Mongo kabuğunu:</span><span class="sxs-lookup"><span data-stu-id="ea36d-111">From your Mongo Shell:</span></span>

   ```
      db.isMaster()
   ```
   
<span data-ttu-id="ea36d-112">Örnek sonuçları:</span><span class="sxs-lookup"><span data-stu-id="ea36d-112">Example results:</span></span>

   ```JSON
      {
         "_t": "IsMasterResponse",
         "ok": 1,
         "ismaster": true,
         "maxMessageSizeBytes": 4194304,
         "maxWriteBatchSize": 1000,
         "minWireVersion": 0,
         "maxWireVersion": 2,
         "tags": {
            "region": "South India"
         },
         "hosts": [
            "vishi-api-for-mongodb-southcentralus.documents.azure.com:10255",
            "vishi-api-for-mongodb-westeurope.documents.azure.com:10255",
            "vishi-api-for-mongodb-southindia.documents.azure.com:10255"
         ],
         "setName": "globaldb",
         "setVersion": 1,
         "primary": "vishi-api-for-mongodb-southindia.documents.azure.com:10255",
         "me": "vishi-api-for-mongodb-southindia.documents.azure.com:10255"
      }
   ```

## <a name="connecting-tooa-preferred-region-using-hello-mongodb-api"></a><span data-ttu-id="ea36d-113">Tooa tercih edilen bölge Hello MongoDB API kullanarak bağlanma</span><span class="sxs-lookup"><span data-stu-id="ea36d-113">Connecting tooa preferred region using hello MongoDB API</span></span>

<span data-ttu-id="ea36d-114">Merhaba MongoDB API, toospecify genel olarak dağıtılmış bir veritabanı için okuma tercih koleksiyonunuzun sağlar.</span><span class="sxs-lookup"><span data-stu-id="ea36d-114">hello MongoDB API enables you toospecify your collection's read preference for a globally distributed database.</span></span> <span data-ttu-id="ea36d-115">Her ikisi de düşük gecikme süresi okur ve genel yüksek kullanılabilirlik için koleksiyonunuzun okuma tercih çok ayarlamanız önerilir*yakın*.</span><span class="sxs-lookup"><span data-stu-id="ea36d-115">For both low latency reads and global high availability, we recommend setting your collection's read preference too*nearest*.</span></span> <span data-ttu-id="ea36d-116">Bir okuma tercih *yakın* yapılandırılmış tooread hello en yakın bölgesinden olduğunu.</span><span class="sxs-lookup"><span data-stu-id="ea36d-116">A read preference of *nearest* is configured tooread from hello closest region.</span></span>

```csharp
var collection = database.GetCollection<BsonDocument>(collectionName);
collection = collection.WithReadPreference(new ReadPreference(ReadPreferenceMode.Nearest));
```

<span data-ttu-id="ea36d-117">Birincil uygulamalarla okuma/bölgeye ve bir ikincil bölge'olağanüstü durum kurtarma (DR) senaryoları yazma için koleksiyonunuzun okuma tercih çok ayarlamanız önerilir*tercih edilen ikincil*.</span><span class="sxs-lookup"><span data-stu-id="ea36d-117">For applications with a primary read/write region and a secondary region for disaster recovery (DR) scenarios, we recommend setting your collection's read preference too*secondary preferred*.</span></span> <span data-ttu-id="ea36d-118">Bir okuma tercih *tercih edilen ikincil* hello birincil bölge kullanılamıyor hello ikincil bölgesinden yapılandırılmış tooread olur.</span><span class="sxs-lookup"><span data-stu-id="ea36d-118">A read preference of *secondary preferred* is configured tooread from hello secondary region when hello primary region is unavailable.</span></span>

```csharp
var collection = database.GetCollection<BsonDocument>(collectionName);
collection = collection.WithReadPreference(new ReadPreference(ReadPreferenceMode.SecondaryPreferred));
```

<span data-ttu-id="ea36d-119">Son olarak, okuma, bölgeler gibi toomanually belirtirseniz.</span><span class="sxs-lookup"><span data-stu-id="ea36d-119">Lastly, if you would like toomanually specify your read regions.</span></span> <span data-ttu-id="ea36d-120">Okuma tercihinizi içinde hello bölge etiket ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ea36d-120">You can set hello region Tag within your read preference.</span></span>

```csharp
var collection = database.GetCollection<BsonDocument>(collectionName);
var tag = new Tag("region", "Southeast Asia");
collection = collection.WithReadPreference(new ReadPreference(ReadPreferenceMode.Secondary, new[] { new TagSet(new[] { tag }) }));
```

<span data-ttu-id="ea36d-121">Bu, bu öğreticinin tamamlanan kadar.</span><span class="sxs-lookup"><span data-stu-id="ea36d-121">That's it, that completes this tutorial.</span></span> <span data-ttu-id="ea36d-122">Nasıl toomanage hello genel çoğaltılmış hesabınızı tutarlılığını okuyarak öğrenebilirsiniz [Azure Cosmos veritabanı tutarlılık düzeylerini](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="ea36d-122">You can learn how toomanage hello consistency of your globally replicated account by reading [Consistency levels in Azure Cosmos DB](consistency-levels.md).</span></span> <span data-ttu-id="ea36d-123">Ve Azure Cosmos DB'de nasıl genel veritabanı çoğaltma hakkında daha fazla bilgi çalıştığı için bkz: [Azure Cosmos DB genel verilerle dağıtmak](distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="ea36d-123">And for more information about how global database replication works in Azure Cosmos DB, see [Distribute data globally with Azure Cosmos DB](distribute-data-globally.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ea36d-124">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ea36d-124">Next steps</span></span>

<span data-ttu-id="ea36d-125">Bu öğreticide, hello aşağıdakileri yaptığınızdan:</span><span class="sxs-lookup"><span data-stu-id="ea36d-125">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ea36d-126">Genel dağıtım Hello Azure portal kullanarak yapılandırma</span><span class="sxs-lookup"><span data-stu-id="ea36d-126">Configure global distribution using hello Azure portal</span></span>
> * <span data-ttu-id="ea36d-127">Merhaba DocumentDB API'leri kullanılarak genel dağıtım yapılandırma</span><span class="sxs-lookup"><span data-stu-id="ea36d-127">Configure global distribution using hello DocumentDB APIs</span></span>

<span data-ttu-id="ea36d-128">Toohello sonraki öğretici toolearn şimdi devam etmek için nasıl Azure Cosmos DB yerel öykünücüsü kullanarak yerel olarak toodevelop hello.</span><span class="sxs-lookup"><span data-stu-id="ea36d-128">You can now proceed toohello next tutorial toolearn how toodevelop locally using hello Azure Cosmos DB local emulator.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ea36d-129">Yerel olarak hello öykünücü ile geliştirme</span><span class="sxs-lookup"><span data-stu-id="ea36d-129">Develop locally with hello emulator</span></span>](local-emulator.md)
