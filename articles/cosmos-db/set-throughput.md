---
title: "Azure Cosmos DB aaaProvision verimliliğini | Microsoft Docs"
description: "Nasıl tooset, Azure Cosmos DB containsers, koleksiyonları, grafikler ve tablolar için işleme sağlanan öğrenin."
services: cosmos-db
author: mimig1
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: f98def7f-f012-4592-be03-f6fa185e1b1e
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/12/2017
ms.author: mimig
ms.openlocfilehash: c143f4aace466b7109168a50e2eb80ddeca6400e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="set-throughput-for-azure-cosmos-db-containers"></a><span data-ttu-id="ea8f4-103">Azure Cosmos DB kapsayıcıları için kümesi işleme</span><span class="sxs-lookup"><span data-stu-id="ea8f4-103">Set throughput for Azure Cosmos DB containers</span></span>

<span data-ttu-id="ea8f4-104">Hello Azure portal, Azure Cosmos DB kapsayıcıları için işleme ayarlayabilir veya istemci SDK'ları kullanarak hello.</span><span class="sxs-lookup"><span data-stu-id="ea8f4-104">You can set throughput for your Azure Cosmos DB containers in hello Azure portal or by using hello client SDKs.</span></span> 

<span data-ttu-id="ea8f4-105">Aşağıdaki tablonun hello hello işleme için kapsayıcıları kullanılabilir listeler:</span><span class="sxs-lookup"><span data-stu-id="ea8f4-105">hello following table lists hello throughput available for containers:</span></span>

<table border="0" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td valign="top"><p></p></td>
            <td valign="top"><p><span data-ttu-id="ea8f4-106"><strong>Tek bir bölüm kapsayıcısı</strong></span><span class="sxs-lookup"><span data-stu-id="ea8f4-106"><strong>Single Partition Container</strong></span></span></p></td>
            <td valign="top"><p><span data-ttu-id="ea8f4-107"><strong>Bölümlenmiş kapsayıcısı</strong></span><span class="sxs-lookup"><span data-stu-id="ea8f4-107"><strong>Partitioned Container</strong></span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="ea8f4-108">En düşük işleme</span><span class="sxs-lookup"><span data-stu-id="ea8f4-108">Minimum Throughput</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="ea8f4-109">saniye başına 400 istek birimleri</span><span class="sxs-lookup"><span data-stu-id="ea8f4-109">400 request units per second</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="ea8f4-110">saniye başına 2.500 istek birimleri</span><span class="sxs-lookup"><span data-stu-id="ea8f4-110">2,500 request units per second</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="ea8f4-111">En yüksek verimlilik</span><span class="sxs-lookup"><span data-stu-id="ea8f4-111">Maximum Throughput</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="ea8f4-112">saniye başına 10.000 istek birimleri</span><span class="sxs-lookup"><span data-stu-id="ea8f4-112">10,000 request units per second</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="ea8f4-113">Sınırsız</span><span class="sxs-lookup"><span data-stu-id="ea8f4-113">Unlimited</span></span></p></td>
        </tr>
    </tbody>
</table>

## <a name="tooset-hello-throughput-by-using-hello-azure-portal"></a><span data-ttu-id="ea8f4-114">hello Azure portal kullanarak tooset hello işleme</span><span class="sxs-lookup"><span data-stu-id="ea8f4-114">tooset hello throughput by using hello Azure portal</span></span>

1. <span data-ttu-id="ea8f4-115">Merhaba yeni bir pencerede açmak [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ea8f4-115">In a new window, open hello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="ea8f4-116">Merhaba sol çubuğunda **Azure Cosmos DB**, veya **daha Hizmetleri** hello kısımda, ardından çok kaydırın**veritabanları**ve ardından **Azure Cosmos DB**.</span><span class="sxs-lookup"><span data-stu-id="ea8f4-116">On hello left bar, click **Azure Cosmos DB**, or click **More Services** at hello bottom, then scroll too**Databases**, and then click **Azure Cosmos DB**.</span></span>
3. <span data-ttu-id="ea8f4-117">Cosmos DB hesabınızı seçin.</span><span class="sxs-lookup"><span data-stu-id="ea8f4-117">Select your Cosmos DB account.</span></span>
4. <span data-ttu-id="ea8f4-118">Merhaba yeni penceresinde **Veri Gezgini (Önizleme)** hello Gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="ea8f4-118">In hello new window, click **Data Explorer (Preview)** in hello navigation menu.</span></span>
5. <span data-ttu-id="ea8f4-119">Merhaba yeni pencerede, veritabanı ve kapsayıcısını genişletin ve ardından **ölçek & ayarları**.</span><span class="sxs-lookup"><span data-stu-id="ea8f4-119">In hello new window, expand your database and container and then click **Scale & Settings**.</span></span>
6. <span data-ttu-id="ea8f4-120">Merhaba yeni penceresinde hello hello yeni işleme değeri yazın **işleme** kutusuna ve ardından **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="ea8f4-120">In hello new window, type hello new throughput value in hello **Throughput** box, and then click **Save**.</span></span>

<a id="set-throughput-sdk"></a>

## <a name="tooset-hello-throughput-by-using-hello-documentdb-api-for-net"></a><span data-ttu-id="ea8f4-121">.NET için hello DocumentDB API kullanarak tooset hello işleme</span><span class="sxs-lookup"><span data-stu-id="ea8f4-121">tooset hello throughput by using hello DocumentDB API for .NET</span></span>

```C#
//Fetch hello resource toobe updated
Offer offer = client.CreateOfferQuery()
    .Where(r => r.ResourceLink == collection.SelfLink)    
    .AsEnumerable()
    .SingleOrDefault();

// Set hello throughput toohello new value, for example 12,000 request units per second
offer = new OfferV2(offer, 12000);

//Now persist these changes toohello database by replacing hello original resource
await client.ReplaceOfferAsync(offer);
```

## <a name="throughput-faq"></a><span data-ttu-id="ea8f4-122">Üretilen iş ile ilgili SSS</span><span class="sxs-lookup"><span data-stu-id="ea8f4-122">Throughput FAQ</span></span>

<span data-ttu-id="ea8f4-123">**My verimlilik tooless 400 RU/s daha ayarlayabilir miyim?**</span><span class="sxs-lookup"><span data-stu-id="ea8f4-123">**Can I set my throughput tooless than 400 RU/s?**</span></span>

<span data-ttu-id="ea8f4-124">400 RU/s hello en düşük işleme Cosmos DB tek bölüm koleksiyonları (2500 RU/s hello bölümlenmiş koleksiyonlar için en düşük olduğu) üzerinde kullanılabilir değil.</span><span class="sxs-lookup"><span data-stu-id="ea8f4-124">400 RU/s is hello minimum throughput available on Cosmos DB single partition collections (2500 RU/s is hello minimum for partitioned collections).</span></span> <span data-ttu-id="ea8f4-125">İstek birimleri 100 RU/s aralıklarla ayarlanmış, ancak işleme too100 RU/s veya herhangi bir değer 400 RU/s değerinden küçük olacak şekilde ayarlanamaz.</span><span class="sxs-lookup"><span data-stu-id="ea8f4-125">Request units are set in 100 RU/s intervals, but throughput cannot be set too100 RU/s or any value smaller than 400 RU/s.</span></span> <span data-ttu-id="ea8f4-126">İçin uygun maliyetli yöntemi toodevelop arıyorsanız ve Cosmos DB test, hello ücretsiz kullanabilirsiniz [Azure Cosmos DB öykünücüsü](local-emulator.md), hangi hiçbir ücret yerel olarak dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ea8f4-126">If you're looking for a cost effective method toodevelop and test Cosmos DB, you can use hello free [Azure Cosmos DB Emulator](local-emulator.md), which you can deploy locally at no cost.</span></span> 

<span data-ttu-id="ea8f4-127">**Merhaba MongoDB API kullanarak througput nasıl ayarlarım?**</span><span class="sxs-lookup"><span data-stu-id="ea8f4-127">**How do I set througput using hello MongoDB API?**</span></span>

<span data-ttu-id="ea8f4-128">Hiçbir MongoDB API uzantısı tooset verimlilik yoktur.</span><span class="sxs-lookup"><span data-stu-id="ea8f4-128">There's no MongoDB API extension tooset throughput.</span></span> <span data-ttu-id="ea8f4-129">Merhaba toouse hello DocumentDB API gösterildiği gibi önerilir [tooset hello işleme için .NET hello DocumentDB API kullanarak](#set-throughput-sdk).</span><span class="sxs-lookup"><span data-stu-id="ea8f4-129">hello recommendation is toouse hello DocumentDB API, as shown in [tooset hello throughput by using hello DocumentDB API for .NET](#set-throughput-sdk).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ea8f4-130">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ea8f4-130">Next steps</span></span>

<span data-ttu-id="ea8f4-131">sağlama ve devam eden planet ölçekli Cosmos DB ile hakkında daha fazla toolearn bkz [bölümleme ve Cosmos DB ile ölçeklendirme](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="ea8f4-131">toolearn more about provisioning and going planet-scale with Cosmos DB, see [Partitioning and scaling with Cosmos DB](partition-data.md).</span></span>
