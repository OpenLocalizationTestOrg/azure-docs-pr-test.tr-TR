---
title: "Azure Cosmos DB sağlama verimliliğini | Microsoft Docs"
description: "Azure Cosmos DB containsers, koleksiyonları, grafikler ve tablolar için sağlanan işleme ayarlanacağını öğrenin."
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
ms.openlocfilehash: d541bb19ba7e5ecb44c9fe91b1e232d4d9c2170e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="set-throughput-for-azure-cosmos-db-containers"></a><span data-ttu-id="31aee-103">Azure Cosmos DB kapsayıcıları için kümesi işleme</span><span class="sxs-lookup"><span data-stu-id="31aee-103">Set throughput for Azure Cosmos DB containers</span></span>

<span data-ttu-id="31aee-104">Azure portalında veya istemci SDK'ları kullanarak, Azure Cosmos DB kapsayıcıları için işleme ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="31aee-104">You can set throughput for your Azure Cosmos DB containers in the Azure portal or by using the client SDKs.</span></span> 

<span data-ttu-id="31aee-105">Aşağıdaki tabloda, üretilen iş için kapsayıcıları kullanılabilir listelenmektedir:</span><span class="sxs-lookup"><span data-stu-id="31aee-105">The following table lists the throughput available for containers:</span></span>

<table border="0" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td valign="top"><p></p></td>
            <td valign="top"><p><span data-ttu-id="31aee-106"><strong>Tek bir bölüm kapsayıcısı</strong></span><span class="sxs-lookup"><span data-stu-id="31aee-106"><strong>Single Partition Container</strong></span></span></p></td>
            <td valign="top"><p><span data-ttu-id="31aee-107"><strong>Bölümlenmiş kapsayıcısı</strong></span><span class="sxs-lookup"><span data-stu-id="31aee-107"><strong>Partitioned Container</strong></span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="31aee-108">En düşük işleme</span><span class="sxs-lookup"><span data-stu-id="31aee-108">Minimum Throughput</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="31aee-109">saniye başına 400 istek birimleri</span><span class="sxs-lookup"><span data-stu-id="31aee-109">400 request units per second</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="31aee-110">saniye başına 2.500 istek birimleri</span><span class="sxs-lookup"><span data-stu-id="31aee-110">2,500 request units per second</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="31aee-111">En yüksek verimlilik</span><span class="sxs-lookup"><span data-stu-id="31aee-111">Maximum Throughput</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="31aee-112">saniye başına 10.000 istek birimleri</span><span class="sxs-lookup"><span data-stu-id="31aee-112">10,000 request units per second</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="31aee-113">Sınırsız</span><span class="sxs-lookup"><span data-stu-id="31aee-113">Unlimited</span></span></p></td>
        </tr>
    </tbody>
</table>

## <a name="to-set-the-throughput-by-using-the-azure-portal"></a><span data-ttu-id="31aee-114">Azure portalını kullanarak üretilen işi ayarlamak için</span><span class="sxs-lookup"><span data-stu-id="31aee-114">To set the throughput by using the Azure portal</span></span>

1. <span data-ttu-id="31aee-115">Yeni bir pencerede açmak [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="31aee-115">In a new window, open the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="31aee-116">Sol çubuğunda **Azure Cosmos DB**, veya **daha Hizmetleri** kısımda, daha sonra kaydırın **veritabanları**ve ardından **Azure Cosmos DB**.</span><span class="sxs-lookup"><span data-stu-id="31aee-116">On the left bar, click **Azure Cosmos DB**, or click **More Services** at the bottom, then scroll to **Databases**, and then click **Azure Cosmos DB**.</span></span>
3. <span data-ttu-id="31aee-117">Cosmos DB hesabınızı seçin.</span><span class="sxs-lookup"><span data-stu-id="31aee-117">Select your Cosmos DB account.</span></span>
4. <span data-ttu-id="31aee-118">Yeni pencerede **Veri Gezgini (Önizleme)** Gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="31aee-118">In the new window, click **Data Explorer (Preview)** in the navigation menu.</span></span>
5. <span data-ttu-id="31aee-119">Yeni pencerede, veritabanı ve kapsayıcısını genişletin ve ardından **ölçek & ayarları**.</span><span class="sxs-lookup"><span data-stu-id="31aee-119">In the new window, expand your database and container and then click **Scale & Settings**.</span></span>
6. <span data-ttu-id="31aee-120">Yeni pencerede yeni işleme değeri yazın **işleme** kutusuna ve ardından **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="31aee-120">In the new window, type the new throughput value in the **Throughput** box, and then click **Save**.</span></span>

<a id="set-throughput-sdk"></a>

## <a name="to-set-the-throughput-by-using-the-documentdb-api-for-net"></a><span data-ttu-id="31aee-121">.NET için DocumentDB API'sini kullanarak üretilen işi ayarlamak için</span><span class="sxs-lookup"><span data-stu-id="31aee-121">To set the throughput by using the DocumentDB API for .NET</span></span>

```C#
//Fetch the resource to be updated
Offer offer = client.CreateOfferQuery()
    .Where(r => r.ResourceLink == collection.SelfLink)    
    .AsEnumerable()
    .SingleOrDefault();

// Set the throughput to the new value, for example 12,000 request units per second
offer = new OfferV2(offer, 12000);

//Now persist these changes to the database by replacing the original resource
await client.ReplaceOfferAsync(offer);
```

## <a name="throughput-faq"></a><span data-ttu-id="31aee-122">Üretilen iş ile ilgili SSS</span><span class="sxs-lookup"><span data-stu-id="31aee-122">Throughput FAQ</span></span>

<span data-ttu-id="31aee-123">**My verimlilik değerinden 400 RU/s ayarlayabilir miyim?**</span><span class="sxs-lookup"><span data-stu-id="31aee-123">**Can I set my throughput to less than 400 RU/s?**</span></span>

<span data-ttu-id="31aee-124">Cosmos DB tek bölüm koleksiyonları (2500 RU/s bölümlenmiş koleksiyonlar için en düşük gereksinimdir) üzerinde kullanılabilir en düşük işleme 400 RU/s olur.</span><span class="sxs-lookup"><span data-stu-id="31aee-124">400 RU/s is the minimum throughput available on Cosmos DB single partition collections (2500 RU/s is the minimum for partitioned collections).</span></span> <span data-ttu-id="31aee-125">İstek birimleri 100 RU/s aralıklarla ayarlanmış, ancak işleme 100 RU/s veya herhangi bir değer 400 RU/s küçük olacak şekilde ayarlanamaz.</span><span class="sxs-lookup"><span data-stu-id="31aee-125">Request units are set in 100 RU/s intervals, but throughput cannot be set to 100 RU/s or any value smaller than 400 RU/s.</span></span> <span data-ttu-id="31aee-126">Geliştirmek ve Cosmos DB sınamak için uygun maliyetli bir yöntem arıyorsanız, ücretsiz kullanabileceğiniz [Azure Cosmos DB öykünücüsü](local-emulator.md), hangi hiçbir ücret yerel olarak dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="31aee-126">If you're looking for a cost effective method to develop and test Cosmos DB, you can use the free [Azure Cosmos DB Emulator](local-emulator.md), which you can deploy locally at no cost.</span></span> 

<span data-ttu-id="31aee-127">**MongoDB API kullanarak througput nasıl ayarlarım?**</span><span class="sxs-lookup"><span data-stu-id="31aee-127">**How do I set througput using the MongoDB API?**</span></span>

<span data-ttu-id="31aee-128">Üretilen iş ayarlamak için MongoDB API uzantısı yok.</span><span class="sxs-lookup"><span data-stu-id="31aee-128">There's no MongoDB API extension to set throughput.</span></span> <span data-ttu-id="31aee-129">DocumentDB API kullanan gösterildiği gibi önerilir [.NET için DocumentDB API'sini kullanarak üretilen işi ayarlamak için](#set-throughput-sdk).</span><span class="sxs-lookup"><span data-stu-id="31aee-129">The recommendation is to use the DocumentDB API, as shown in [To set the throughput by using the DocumentDB API for .NET](#set-throughput-sdk).</span></span>

## <a name="next-steps"></a><span data-ttu-id="31aee-130">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="31aee-130">Next steps</span></span>

<span data-ttu-id="31aee-131">Sağlama ve devam eden planet ölçekli Cosmos DB ile hakkında daha fazla bilgi için bkz: [bölümleme ve Cosmos DB ile ölçeklendirme](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="31aee-131">To learn more about provisioning and going planet-scale with Cosmos DB, see [Partitioning and scaling with Cosmos DB](partition-data.md).</span></span>
