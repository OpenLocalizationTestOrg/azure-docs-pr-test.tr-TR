---
title: "Azure Cosmos DB tarihleri ile çalışma | Microsoft Docs"
description: "Azure Cosmos veritabanı tarihleri ile birlikte çalışma hakkında bilgi edinin."
services: cosmos-db
author: arramac
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: e587772f-ce9f-498c-a017-a51e7265bb23
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: arramac
ms.openlocfilehash: b6a77e33eea24000037ffb31d7aae3cb1d345ce9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="working-with-dates-in-azure-cosmos-db"></a><span data-ttu-id="96cb6-103">Azure Cosmos DB tarihleri ile çalışma</span><span class="sxs-lookup"><span data-stu-id="96cb6-103">Working with Dates in Azure Cosmos DB</span></span>
<span data-ttu-id="96cb6-104">Azure Cosmos DB sunar şema esnekliği ve zengin bir yerel dizin oluşturma [JSON](http://www.json.org) veri modeli.</span><span class="sxs-lookup"><span data-stu-id="96cb6-104">Azure Cosmos DB delivers schema flexibility and rich indexing via a native [JSON](http://www.json.org) data model.</span></span> <span data-ttu-id="96cb6-105">Veritabanları, koleksiyonlar, belgeler ve saklı yordamları da dahil olmak üzere tüm Azure Cosmos DB kaynakları modellenir ve JSON belgeleri olarak depolanır.</span><span class="sxs-lookup"><span data-stu-id="96cb6-105">All Azure Cosmos DB resources including databases, collections, documents, and stored procedures are modeled and stored as JSON documents.</span></span> <span data-ttu-id="96cb6-106">Olma taşınabilir bir zorunluluk, JSON (ve Azure Cosmos DB) temel türleri, yalnızca küçük bir kümesini destekler: dize, sayı, Boole değeri, dizi, nesne ve Null.</span><span class="sxs-lookup"><span data-stu-id="96cb6-106">As a requirement for being portable, JSON (and Azure Cosmos DB) supports only a small set of basic types: String, Number, Boolean, Array, Object, and Null.</span></span> <span data-ttu-id="96cb6-107">Ancak, JSON esnektir ve geliştiriciler ve çerçeveleri nesneleri veya dizi oluşturma ve bu temelleri kullanarak daha karmaşık türleri temsil eden kullanmasına olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="96cb6-107">However, JSON is flexible and allow developers and frameworks to represent more complex types using these primitives and composing them as objects or arrays.</span></span> 

<span data-ttu-id="96cb6-108">Temel türlerine ek olarak birçok uygulama gereksinim [DateTime](https://msdn.microsoft.com/library/system.datetime(v=vs.110).aspx) tarihleri ve tarih damgası temsil eden tür.</span><span class="sxs-lookup"><span data-stu-id="96cb6-108">In addition to the basic types, many applications need the [DateTime](https://msdn.microsoft.com/library/system.datetime(v=vs.110).aspx) type to represent dates and timestamps.</span></span> <span data-ttu-id="96cb6-109">Bu makalede nasıl geliştiriciler depolamak, alabilir ve .NET SDK kullanarak Azure Cosmos DB tarihleri sorgu açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="96cb6-109">This article describes how developers can store, retrieve, and query dates in Azure Cosmos DB using the .NET SDK.</span></span>

## <a name="storing-datetimes"></a><span data-ttu-id="96cb6-110">Tarih/saat depolanması</span><span class="sxs-lookup"><span data-stu-id="96cb6-110">Storing DateTimes</span></span>
<span data-ttu-id="96cb6-111">Varsayılan olarak, [Azure Cosmos DB SDK](documentdb-sdk-dotnet.md) DateTime değerleri olarak serileştiren [ISO 8601](http://www.iso.org/iso/catalogue_detail?csnumber=40874) dizeleri.</span><span class="sxs-lookup"><span data-stu-id="96cb6-111">By default, the [Azure Cosmos DB SDK](documentdb-sdk-dotnet.md) serializes DateTime values as [ISO 8601](http://www.iso.org/iso/catalogue_detail?csnumber=40874) strings.</span></span> <span data-ttu-id="96cb6-112">Uygulamaların çoğu, aşağıdaki nedenlerle DateTime için varsayılan dize gösterimi kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="96cb6-112">Most applications can use the default string representation for DateTime for the following reasons:</span></span>

* <span data-ttu-id="96cb6-113">Dizeleri karşılaştırma ve dizeye dönüştürülen DateTime değerlerini göreli sıralama korunur.</span><span class="sxs-lookup"><span data-stu-id="96cb6-113">Strings can be compared, and the relative ordering of the DateTime values is preserved when they are transformed to strings.</span></span> 
* <span data-ttu-id="96cb6-114">Bu yaklaşım, JSON dönüştürme için herhangi bir özel kod veya öznitelikleri gerektirmez.</span><span class="sxs-lookup"><span data-stu-id="96cb6-114">This approach doesn't require any custom code or attributes for JSON conversion.</span></span>
* <span data-ttu-id="96cb6-115">JSON içinde depolanan tarihleri İnsan okunabilir.</span><span class="sxs-lookup"><span data-stu-id="96cb6-115">The dates as stored in JSON are human readable.</span></span>
* <span data-ttu-id="96cb6-116">Bu yaklaşım hızlı sorgu performansı için Azure Cosmos veritabanı dizin yararlanabilir.</span><span class="sxs-lookup"><span data-stu-id="96cb6-116">This approach can take advantage of Azure Cosmos DB's index for fast query performance.</span></span>

<span data-ttu-id="96cb6-117">Örneğin, aşağıdaki kod parçacığında depolayan bir `Order` içeren iki DateTime özellikleri - nesne `ShipDate` ve `OrderDate` .NET SDK kullanarak bir belge olarak:</span><span class="sxs-lookup"><span data-stu-id="96cb6-117">For example, the following snippet stores an `Order` object containing two DateTime properties - `ShipDate` and `OrderDate` as a document using the .NET SDK:</span></span>

    public class Order
    {
        [JsonProperty(PropertyName="id")]
        public string Id { get; set; }
        public DateTime OrderDate { get; set; }
        public DateTime ShipDate { get; set; }
        public double Total { get; set; }
    }

    await client.CreateDocumentAsync("/dbs/orderdb/colls/orders", 
        new Order 
        { 
            Id = "09152014101",
            OrderDate = DateTime.UtcNow.AddDays(-30),
            ShipDate = DateTime.UtcNow.AddDays(-14), 
            Total = 113.39
        });

<span data-ttu-id="96cb6-118">Bu belgede Azure Cosmos DB'de şekilde depolanır:</span><span class="sxs-lookup"><span data-stu-id="96cb6-118">This document is stored in Azure Cosmos DB as follows:</span></span>

    {
        "id": "09152014101",
        "OrderDate": "2014-09-15T23:14:25.7251173Z",
        "ShipDate": "2014-09-30T23:14:25.7251173Z",
        "Total": 113.39
    }
    

<span data-ttu-id="96cb6-119">Alternatif olarak, tarih/saat olarak UNIX zaman damgaları, diğer bir deyişle, 1 Ocak 1970'ten beri geçen saniyelerin sayısını gösteren bir sayı olarak saklayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="96cb6-119">Alternatively, you can store DateTimes as Unix timestamps, that is, as a number representing the number of elapsed seconds since January 1, 1970.</span></span> <span data-ttu-id="96cb6-120">Azure Cosmos DB'ın iç zaman damgası (`_ts`) özelliği, bu yaklaşım izler.</span><span class="sxs-lookup"><span data-stu-id="96cb6-120">Azure Cosmos DB's internal Timestamp (`_ts`) property follows this approach.</span></span> <span data-ttu-id="96cb6-121">Kullanabileceğiniz [UnixDateTimeConverter](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.unixdatetimeconverter.aspx) sayı olarak tarih/saat serileştirmek için sınıfı.</span><span class="sxs-lookup"><span data-stu-id="96cb6-121">You can use the [UnixDateTimeConverter](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.unixdatetimeconverter.aspx) class to serialize DateTimes as numbers.</span></span> 

## <a name="indexing-datetimes-for-range-queries"></a><span data-ttu-id="96cb6-122">Tarih/saat aralığı sorgular için dizin oluşturma</span><span class="sxs-lookup"><span data-stu-id="96cb6-122">Indexing DateTimes for range queries</span></span>
<span data-ttu-id="96cb6-123">Aralık sorguları içeren DateTime değerleri yaygındır.</span><span class="sxs-lookup"><span data-stu-id="96cb6-123">Range queries are common with DateTime values.</span></span> <span data-ttu-id="96cb6-124">Örneğin, dünden bu yana oluşturulan tüm siparişleri bulmak veya son beş dakika içinde gönderilen tüm siparişleri bulmak gerekiyorsa, aralık sorguları gerçekleştirmek için gerekir.</span><span class="sxs-lookup"><span data-stu-id="96cb6-124">For example, if you need to find all orders created since yesterday, or find all orders shipped in the last five minutes, you need to perform range queries.</span></span> <span data-ttu-id="96cb6-125">Bu sorguları verimli bir şekilde çalıştırmak için koleksiyonunuzu aralığı dizeleri dizin oluşturma için yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="96cb6-125">To execute these queries efficiently, you must configure your collection for Range indexing on strings.</span></span>

    DocumentCollection collection = new DocumentCollection { Id = "orders" };
    collection.IndexingPolicy = new IndexingPolicy(new RangeIndex(DataType.String) { Precision = -1 });
    await client.CreateDocumentCollectionAsync("/dbs/orderdb", collection);

<span data-ttu-id="96cb6-126">Dizin oluşturma ilkeleri yapılandırma hakkında daha fazla bilgi edinebilirsiniz [Azure Cosmos DB dizin oluşturma ilkeleri](indexing-policies.md).</span><span class="sxs-lookup"><span data-stu-id="96cb6-126">You can learn more about how to configure indexing policies at [Azure Cosmos DB Indexing Policies](indexing-policies.md).</span></span>

## <a name="querying-datetimes-in-linq"></a><span data-ttu-id="96cb6-127">Tarih/saat LINQ sorgulama</span><span class="sxs-lookup"><span data-stu-id="96cb6-127">Querying DateTimes in LINQ</span></span>
<span data-ttu-id="96cb6-128">DocumentDB .NET SDK'yı otomatik olarak LINQ aracılığıyla Azure Cosmos veritabanında depolanan verileri Sorgulama destekler.</span><span class="sxs-lookup"><span data-stu-id="96cb6-128">The DocumentDB .NET SDK automatically supports querying data stored in Azure Cosmos DB via LINQ.</span></span> <span data-ttu-id="96cb6-129">Örneğin, aşağıdaki kod parçacığını bir LINQ Sorgu son üç günde sevk edilen bu filtreler siparişleri gösterir.</span><span class="sxs-lookup"><span data-stu-id="96cb6-129">For example, the following snippet shows a LINQ query that filters orders that were shipped in the last three days.</span></span>

    IQueryable<Order> orders = client.CreateDocumentQuery<Order>("/dbs/orderdb/colls/orders")
        .Where(o => o.ShipDate >= DateTime.UtcNow.AddDays(-3));
          
    // Translated to the following SQL statement and executed on Azure Cosmos DB
    SELECT * FROM root WHERE (root["ShipDate"] >= "2016-12-18T21:55:03.45569Z")

<span data-ttu-id="96cb6-130">Azure Cosmos veritabanı SQL sorgu dili ve LINQ sağlayıcısındaki hakkında daha fazla bilgiyi [sorgulama Cosmos DB](documentdb-sql-query.md).</span><span class="sxs-lookup"><span data-stu-id="96cb6-130">You can learn more about Azure Cosmos DB's SQL query language and the LINQ provider at [Querying Cosmos DB](documentdb-sql-query.md).</span></span>

<span data-ttu-id="96cb6-131">Bu makalede, nasıl depolamak, dizin ve tarih/saat Azure Cosmos veritabanı sorgu inceledik.</span><span class="sxs-lookup"><span data-stu-id="96cb6-131">In this article, we looked at how to store, index, and query DateTimes in Azure Cosmos DB.</span></span>

## <a name="next-steps"></a><span data-ttu-id="96cb6-132">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="96cb6-132">Next Steps</span></span>
* <span data-ttu-id="96cb6-133">İndirme ve çalıştırma [github'daki kod örnekleri](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples)</span><span class="sxs-lookup"><span data-stu-id="96cb6-133">Download and run the [Code samples on GitHub](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples)</span></span>
* <span data-ttu-id="96cb6-134">Daha fazla bilgi edinmek [DocumentDB API sorgusu](documentdb-sql-query.md)</span><span class="sxs-lookup"><span data-stu-id="96cb6-134">Learn more about [DocumentDB API Query](documentdb-sql-query.md)</span></span>
* <span data-ttu-id="96cb6-135">Daha fazla bilgi edinmek [Azure Cosmos DB dizin oluşturma ilkeleri](indexing-policies.md)</span><span class="sxs-lookup"><span data-stu-id="96cb6-135">Learn more about [Azure Cosmos DB Indexing Policies](indexing-policies.md)</span></span>
