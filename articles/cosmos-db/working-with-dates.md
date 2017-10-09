---
title: "Azure Cosmos veritabanı tarihlerle aaaWorking | Microsoft Docs"
description: "Toowork ile Azure Cosmos DB'de nasıl tarihleri hakkında bilgi edinin."
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
ms.openlocfilehash: 27ec170e4bef72c0b5b456738f1275ef02543024
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-dates-in-azure-cosmos-db"></a><span data-ttu-id="ae285-103">Azure Cosmos DB tarihleri ile çalışma</span><span class="sxs-lookup"><span data-stu-id="ae285-103">Working with Dates in Azure Cosmos DB</span></span>
<span data-ttu-id="ae285-104">Azure Cosmos DB sunar şema esnekliği ve zengin bir yerel dizin oluşturma [JSON](http://www.json.org) veri modeli.</span><span class="sxs-lookup"><span data-stu-id="ae285-104">Azure Cosmos DB delivers schema flexibility and rich indexing via a native [JSON](http://www.json.org) data model.</span></span> <span data-ttu-id="ae285-105">Veritabanları, koleksiyonlar, belgeler ve saklı yordamları da dahil olmak üzere tüm Azure Cosmos DB kaynakları modellenir ve JSON belgeleri olarak depolanır.</span><span class="sxs-lookup"><span data-stu-id="ae285-105">All Azure Cosmos DB resources including databases, collections, documents, and stored procedures are modeled and stored as JSON documents.</span></span> <span data-ttu-id="ae285-106">Olma taşınabilir bir zorunluluk, JSON (ve Azure Cosmos DB) temel türleri, yalnızca küçük bir kümesini destekler: dize, sayı, Boole değeri, dizi, nesne ve Null.</span><span class="sxs-lookup"><span data-stu-id="ae285-106">As a requirement for being portable, JSON (and Azure Cosmos DB) supports only a small set of basic types: String, Number, Boolean, Array, Object, and Null.</span></span> <span data-ttu-id="ae285-107">Ancak, JSON esnektir ve geliştiriciler ve çerçeveleri toorepresent nesne veya dizi oluşturma ve bu temelleri kullanarak daha karmaşık türleri izin verir.</span><span class="sxs-lookup"><span data-stu-id="ae285-107">However, JSON is flexible and allow developers and frameworks toorepresent more complex types using these primitives and composing them as objects or arrays.</span></span> 

<span data-ttu-id="ae285-108">Toplama toohello temel türleri, birçok uygulama hello gereksinim [DateTime](https://msdn.microsoft.com/library/system.datetime(v=vs.110).aspx) toorepresent tarihleri ve tarih damgası yazın.</span><span class="sxs-lookup"><span data-stu-id="ae285-108">In addition toohello basic types, many applications need hello [DateTime](https://msdn.microsoft.com/library/system.datetime(v=vs.110).aspx) type toorepresent dates and timestamps.</span></span> <span data-ttu-id="ae285-109">Bu makalede nasıl geliştiriciler depolamak, alabilir ve tarihleri hello .NET SDK kullanarak Azure Cosmos veritabanı sorgu açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="ae285-109">This article describes how developers can store, retrieve, and query dates in Azure Cosmos DB using hello .NET SDK.</span></span>

## <a name="storing-datetimes"></a><span data-ttu-id="ae285-110">Tarih/saat depolanması</span><span class="sxs-lookup"><span data-stu-id="ae285-110">Storing DateTimes</span></span>
<span data-ttu-id="ae285-111">Varsayılan olarak, hello [Azure Cosmos DB SDK](documentdb-sdk-dotnet.md) DateTime değerleri olarak serileştiren [ISO 8601](http://www.iso.org/iso/catalogue_detail?csnumber=40874) dizeleri.</span><span class="sxs-lookup"><span data-stu-id="ae285-111">By default, hello [Azure Cosmos DB SDK](documentdb-sdk-dotnet.md) serializes DateTime values as [ISO 8601](http://www.iso.org/iso/catalogue_detail?csnumber=40874) strings.</span></span> <span data-ttu-id="ae285-112">Çoğu uygulama hello varsayılan dize gösterimi nedeni aşağıdaki Merhaba DateTime için kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="ae285-112">Most applications can use hello default string representation for DateTime for hello following reasons:</span></span>

* <span data-ttu-id="ae285-113">Dizeleri karşılaştırma ve dönüştürülen toostrings olduklarında hello hello DateTime değerleri sıralama göreli korunur.</span><span class="sxs-lookup"><span data-stu-id="ae285-113">Strings can be compared, and hello relative ordering of hello DateTime values is preserved when they are transformed toostrings.</span></span> 
* <span data-ttu-id="ae285-114">Bu yaklaşım, JSON dönüştürme için herhangi bir özel kod veya öznitelikleri gerektirmez.</span><span class="sxs-lookup"><span data-stu-id="ae285-114">This approach doesn't require any custom code or attributes for JSON conversion.</span></span>
* <span data-ttu-id="ae285-115">JSON içinde depolanan gibi hello tarihleri İnsan okunabilir.</span><span class="sxs-lookup"><span data-stu-id="ae285-115">hello dates as stored in JSON are human readable.</span></span>
* <span data-ttu-id="ae285-116">Bu yaklaşım hızlı sorgu performansı için Azure Cosmos veritabanı dizin yararlanabilir.</span><span class="sxs-lookup"><span data-stu-id="ae285-116">This approach can take advantage of Azure Cosmos DB's index for fast query performance.</span></span>

<span data-ttu-id="ae285-117">Örneğin, kod parçacığında depoları hello bir `Order` içeren iki DateTime özellikleri - nesne `ShipDate` ve `OrderDate` bir belge olarak .NET SDK'sı hello kullanarak:</span><span class="sxs-lookup"><span data-stu-id="ae285-117">For example, hello following snippet stores an `Order` object containing two DateTime properties - `ShipDate` and `OrderDate` as a document using hello .NET SDK:</span></span>

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

<span data-ttu-id="ae285-118">Bu belgede Azure Cosmos DB'de şekilde depolanır:</span><span class="sxs-lookup"><span data-stu-id="ae285-118">This document is stored in Azure Cosmos DB as follows:</span></span>

    {
        "id": "09152014101",
        "OrderDate": "2014-09-15T23:14:25.7251173Z",
        "ShipDate": "2014-09-30T23:14:25.7251173Z",
        "Total": 113.39
    }
    

<span data-ttu-id="ae285-119">Alternatif olarak, tarih/saat olarak UNIX zaman damgaları, diğer bir deyişle, hello 1 Ocak 1970'ten beri geçen saniyelerin sayısını gösteren bir sayı olarak saklayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ae285-119">Alternatively, you can store DateTimes as Unix timestamps, that is, as a number representing hello number of elapsed seconds since January 1, 1970.</span></span> <span data-ttu-id="ae285-120">Azure Cosmos DB'ın iç zaman damgası (`_ts`) özelliği, bu yaklaşım izler.</span><span class="sxs-lookup"><span data-stu-id="ae285-120">Azure Cosmos DB's internal Timestamp (`_ts`) property follows this approach.</span></span> <span data-ttu-id="ae285-121">Merhaba kullanabilirsiniz [UnixDateTimeConverter](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.unixdatetimeconverter.aspx) tooserialize sayı olarak tarih/saat sınıfı.</span><span class="sxs-lookup"><span data-stu-id="ae285-121">You can use hello [UnixDateTimeConverter](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.unixdatetimeconverter.aspx) class tooserialize DateTimes as numbers.</span></span> 

## <a name="indexing-datetimes-for-range-queries"></a><span data-ttu-id="ae285-122">Tarih/saat aralığı sorgular için dizin oluşturma</span><span class="sxs-lookup"><span data-stu-id="ae285-122">Indexing DateTimes for range queries</span></span>
<span data-ttu-id="ae285-123">Aralık sorguları içeren DateTime değerleri yaygındır.</span><span class="sxs-lookup"><span data-stu-id="ae285-123">Range queries are common with DateTime values.</span></span> <span data-ttu-id="ae285-124">Örneğin, toofind dünden bu yana oluşturulan tüm siparişleri gerekir ya da son beş dakika hello gönderilen tüm siparişleri bulmak, tooperform aralığı sorguları gerekir.</span><span class="sxs-lookup"><span data-stu-id="ae285-124">For example, if you need toofind all orders created since yesterday, or find all orders shipped in hello last five minutes, you need tooperform range queries.</span></span> <span data-ttu-id="ae285-125">Bu sorgular verimli bir şekilde tooexecute, koleksiyonunuzu aralığı dizeleri dizin oluşturma için yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ae285-125">tooexecute these queries efficiently, you must configure your collection for Range indexing on strings.</span></span>

    DocumentCollection collection = new DocumentCollection { Id = "orders" };
    collection.IndexingPolicy = new IndexingPolicy(new RangeIndex(DataType.String) { Precision = -1 });
    await client.CreateDocumentCollectionAsync("/dbs/orderdb", collection);

<span data-ttu-id="ae285-126">Hakkında daha fazla bilgi ilkeler dizin tooconfigure [Azure Cosmos DB dizin oluşturma ilkeleri](indexing-policies.md).</span><span class="sxs-lookup"><span data-stu-id="ae285-126">You can learn more about how tooconfigure indexing policies at [Azure Cosmos DB Indexing Policies](indexing-policies.md).</span></span>

## <a name="querying-datetimes-in-linq"></a><span data-ttu-id="ae285-127">Tarih/saat LINQ sorgulama</span><span class="sxs-lookup"><span data-stu-id="ae285-127">Querying DateTimes in LINQ</span></span>
<span data-ttu-id="ae285-128">LINQ aracılığıyla Azure Cosmos veritabanında depolanan verileri Sorgulama Hello DocumentDB .NET SDK'yı otomatik olarak destekler.</span><span class="sxs-lookup"><span data-stu-id="ae285-128">hello DocumentDB .NET SDK automatically supports querying data stored in Azure Cosmos DB via LINQ.</span></span> <span data-ttu-id="ae285-129">Örneğin, hello aşağıdaki kod parçacığında bir LINQ Sorgu hello son üç gün sevk edilen bu filtreler siparişleri gösterir.</span><span class="sxs-lookup"><span data-stu-id="ae285-129">For example, hello following snippet shows a LINQ query that filters orders that were shipped in hello last three days.</span></span>

    IQueryable<Order> orders = client.CreateDocumentQuery<Order>("/dbs/orderdb/colls/orders")
        .Where(o => o.ShipDate >= DateTime.UtcNow.AddDays(-3));
          
    // Translated toohello following SQL statement and executed on Azure Cosmos DB
    SELECT * FROM root WHERE (root["ShipDate"] >= "2016-12-18T21:55:03.45569Z")

<span data-ttu-id="ae285-130">Azure Cosmos veritabanı SQL sorgu dili ve hello LINQ sağlayıcısındaki hakkında daha fazla bilgiyi [sorgulama Cosmos DB](documentdb-sql-query.md).</span><span class="sxs-lookup"><span data-stu-id="ae285-130">You can learn more about Azure Cosmos DB's SQL query language and hello LINQ provider at [Querying Cosmos DB](documentdb-sql-query.md).</span></span>

<span data-ttu-id="ae285-131">Bu makalede, nasıl toostore, dizin ve tarih/saat Azure Cosmos veritabanı sorgu inceledik.</span><span class="sxs-lookup"><span data-stu-id="ae285-131">In this article, we looked at how toostore, index, and query DateTimes in Azure Cosmos DB.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ae285-132">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="ae285-132">Next Steps</span></span>
* <span data-ttu-id="ae285-133">İndirme ve çalıştırma hello [github'daki kod örnekleri](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples)</span><span class="sxs-lookup"><span data-stu-id="ae285-133">Download and run hello [Code samples on GitHub](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples)</span></span>
* <span data-ttu-id="ae285-134">Daha fazla bilgi edinmek [DocumentDB API sorgusu](documentdb-sql-query.md)</span><span class="sxs-lookup"><span data-stu-id="ae285-134">Learn more about [DocumentDB API Query](documentdb-sql-query.md)</span></span>
* <span data-ttu-id="ae285-135">Daha fazla bilgi edinmek [Azure Cosmos DB dizin oluşturma ilkeleri](indexing-policies.md)</span><span class="sxs-lookup"><span data-stu-id="ae285-135">Learn more about [Azure Cosmos DB Indexing Policies](indexing-policies.md)</span></span>
