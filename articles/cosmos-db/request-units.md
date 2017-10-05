---
title: Birimleri iste & verimlilik - Azure Cosmos DB tahmin etme | Microsoft Docs
description: "Anlamak, belirtin ve Azure Cosmos veritabanı istek birimi gereksinimlerini tahmin etme hakkında bilgi edinin."
services: cosmos-db
author: mimig1
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: d0a3c310-eb63-4e45-8122-b7724095c32f
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: 7a4efc0fb9b3855b9dbbe445768ceb2a9940d0b2
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="request-units-in-azure-cosmos-db"></a><span data-ttu-id="21110-103">Azure Cosmos DB birimlerinde isteği</span><span class="sxs-lookup"><span data-stu-id="21110-103">Request Units in Azure Cosmos DB</span></span>
<span data-ttu-id="21110-104">Artık kullanılabilir: Azure Cosmos DB [istek birimi hesaplayıcı](https://www.documentdb.com/capacityplanner).</span><span class="sxs-lookup"><span data-stu-id="21110-104">Now available: Azure Cosmos DB [request unit calculator](https://www.documentdb.com/capacityplanner).</span></span> <span data-ttu-id="21110-105">Daha fazla bilgi edinin [, üretilen iş gerektiğini tahmin etme](request-units.md#estimating-throughput-needs).</span><span class="sxs-lookup"><span data-stu-id="21110-105">Learn more in [Estimating your throughput needs](request-units.md#estimating-throughput-needs).</span></span>

![Üretilen iş hesaplayıcısı][5]

## <a name="introduction"></a><span data-ttu-id="21110-107">Giriş</span><span class="sxs-lookup"><span data-stu-id="21110-107">Introduction</span></span>
<span data-ttu-id="21110-108">[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) Microsoft'un Genel dağıtılmış birden çok model veritabanıdır.</span><span class="sxs-lookup"><span data-stu-id="21110-108">[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) is Microsoft's globally distributed multi-model database.</span></span> <span data-ttu-id="21110-109">Azure Cosmos DB ile sanal makineleri kiralamak, yazılım dağıtma veya veritabanlarını izleme gerekmez.</span><span class="sxs-lookup"><span data-stu-id="21110-109">With Azure Cosmos DB, you don't have to rent virtual machines, deploy software, or monitor databases.</span></span> <span data-ttu-id="21110-110">Azure Cosmos DB işletilen ve sürekli olarak world sınıfı kullanılabilirliği, performansı ve veri koruma sağlamak üzere Microsoft üst mühendisleri tarafından izlenir.</span><span class="sxs-lookup"><span data-stu-id="21110-110">Azure Cosmos DB is operated and continuously monitored by Microsoft top engineers to deliver world class availability, performance, and data protection.</span></span> <span data-ttu-id="21110-111">Tercih ettiğiniz API'lerini kullanarak verilerinize erişebilir [DocumentDB SQL](documentdb-sql-query.md) (belge), MongoDB (belge) [Azure Table Storage](https://azure.microsoft.com/services/storage/tables/) (anahtar-değer) ve [Gremlin](https://tinkerpop.apache.org/gremlin.html) (tüm grafik) yerel olarak desteklenir.</span><span class="sxs-lookup"><span data-stu-id="21110-111">You can access your data using APIs of your choice, as [DocumentDB SQL](documentdb-sql-query.md) (document), MongoDB (document), [Azure Table Storage](https://azure.microsoft.com/services/storage/tables/) (key-value), and [Gremlin](https://tinkerpop.apache.org/gremlin.html) (graph) are all natively supported.</span></span> <span data-ttu-id="21110-112">Azure Cosmos DB para istek birimi (RU) birimidir.</span><span class="sxs-lookup"><span data-stu-id="21110-112">The currency of Azure Cosmos DB is the Request Unit (RU).</span></span> <span data-ttu-id="21110-113">RUs ile okuma/yazma kapasiteleri veya sağlama CPU, bellek ve IOPS ayırmak gerekmez.</span><span class="sxs-lookup"><span data-stu-id="21110-113">With RUs, you do not need to reserve read/write capacities or provision CPU, Memory and IOPS.</span></span>

<span data-ttu-id="21110-114">Azure Cosmos DB Basit okuma arasında değişen farklı işlemlerle API'lerini destekler ve karmaşık grafik sorguları yazar.</span><span class="sxs-lookup"><span data-stu-id="21110-114">Azure Cosmos DB supports a number of APIs with different operations ranging from simple reads and writes to complex graph queries.</span></span> <span data-ttu-id="21110-115">Tüm istekleri eşit olduğundan, normalleştirilmiş bir miktar atanan **istek birimleri** isteğe hizmet vermek için gerekli hesaplama miktarına göre.</span><span class="sxs-lookup"><span data-stu-id="21110-115">Since not all requests are equal, they are assigned a normalized quantity of **request units** based on the amount of computation required to serve the request.</span></span> <span data-ttu-id="21110-116">Bir işlem için istek birim sayısı belirleyici ve bir yanıt üstbilgisi aracılığıyla Azure Cosmos veritabanı herhangi bir işlem tarafından kullanılan istek birim sayısını izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="21110-116">The number of request units for an operation is deterministic, and you can track the number of request units consumed by any operation in Azure Cosmos DB via a response header.</span></span> 

<span data-ttu-id="21110-117">Tahmin edilebilir performans sağlamak için işleme birimi 100 RU/saniye yedek gerekir.</span><span class="sxs-lookup"><span data-stu-id="21110-117">To provide predictable performance, you need to reserve throughput in units of 100 RU/second.</span></span> 

<span data-ttu-id="21110-118">Bu makaleyi okuduktan sonra aşağıdaki soruları yanıtlayın mümkün olacaktır:</span><span class="sxs-lookup"><span data-stu-id="21110-118">After reading this article, you'll be able to answer the following questions:</span></span>  

* <span data-ttu-id="21110-119">Hangi birimleri istemek ve ücretleri isteği?</span><span class="sxs-lookup"><span data-stu-id="21110-119">What are request units and request charges?</span></span>
* <span data-ttu-id="21110-120">Bir koleksiyon için istek birim kapasitesi nasıl belirteceğinizi?</span><span class="sxs-lookup"><span data-stu-id="21110-120">How do I specify request unit capacity for a collection?</span></span>
* <span data-ttu-id="21110-121">My uygulamanın istek birimi gereken nasıl tahmin?</span><span class="sxs-lookup"><span data-stu-id="21110-121">How do I estimate my application's request unit needs?</span></span>
* <span data-ttu-id="21110-122">Bir koleksiyon için istek birim kapasitesi aşmanız durumunda ne olur?</span><span class="sxs-lookup"><span data-stu-id="21110-122">What happens if I exceed request unit capacity for a collection?</span></span>

<span data-ttu-id="21110-123">Azure Cosmos DB çok model veritabanı olduğundan, biz koleksiyonu/belge belge API, grafik API'si için bir grafik/düğümü ve tablo/varlık tablo API için başvurur dikkate almak önemlidir.</span><span class="sxs-lookup"><span data-stu-id="21110-123">As Azure Cosmos DB is a multi-model database, it is important to note that we will refer to a collection/document for a document API, a graph/node for a graph API and a table/entity for table API.</span></span> <span data-ttu-id="21110-124">Üretilen iş bu belge size kapsayıcı/öğe kavramlarını generalize.</span><span class="sxs-lookup"><span data-stu-id="21110-124">Throughput this document we will generalize to the concepts of container/item.</span></span>

## <a name="request-units-and-request-charges"></a><span data-ttu-id="21110-125">İstek birimleri ve istek ücretleri</span><span class="sxs-lookup"><span data-stu-id="21110-125">Request units and request charges</span></span>
<span data-ttu-id="21110-126">Azure Cosmos DB tarafından hızlı ve tahmin edilebilir performans sunar *ayırma* uygulamanızın verimlilik gereken karşılamak için kaynakları.</span><span class="sxs-lookup"><span data-stu-id="21110-126">Azure Cosmos DB delivers fast, predictable performance by *reserving* resources to satisfy your application's throughput needs.</span></span>  <span data-ttu-id="21110-127">Uygulama yüklemek ve zaman içinde desenleri değişiklik erişmek için Azure Cosmos DB kolayca artırın veya uygulamanız için kullanılabilir ayrılmış işleme miktarını azaltmak sağlar.</span><span class="sxs-lookup"><span data-stu-id="21110-127">Because application load and access patterns change over time, Azure Cosmos DB allows you to easily increase or decrease the amount of reserved throughput available to your application.</span></span>

<span data-ttu-id="21110-128">Azure Cosmos DB ile ayrılmış işleme saniyede işlediği istek birimler cinsinden belirtilir.</span><span class="sxs-lookup"><span data-stu-id="21110-128">With Azure Cosmos DB, reserved throughput is specified in terms of request units processing per second.</span></span> <span data-ttu-id="21110-129">İstek birimleri yapabildiği verimlilik para birimi olarak düşünebilirsiniz, *yedek* garantili istek birimleri uygulamanıza kullanılabilir miktardaki saniye başına temelinde.</span><span class="sxs-lookup"><span data-stu-id="21110-129">You can think of request units as throughput currency, whereby you *reserve* an amount of guaranteed request units available to your application on per second basis.</span></span>  <span data-ttu-id="21110-130">Azure Cosmos - bir belge yazma, bir belge güncelleştirme bir sorgu gerçekleştirme - DB her bir işlemin CPU, bellek ve IOPS tüketir.</span><span class="sxs-lookup"><span data-stu-id="21110-130">Each operation in Azure Cosmos DB - writing a document, performing a query, updating a document - consumes CPU, memory, and IOPS.</span></span>  <span data-ttu-id="21110-131">Diğer bir deyişle, her işlemi uygulanan bir *isteği ücret*, içinde ifade *istek birimleri*.</span><span class="sxs-lookup"><span data-stu-id="21110-131">That is, each operation incurs a *request charge*, which is expressed in *request units*.</span></span>  <span data-ttu-id="21110-132">İstek birimi ücretleri, uygulamanızın işleme gereksinimleri etkileyen faktörler anlama, uygulamanızı maliyeti etkili bir şekilde olabildiğince olarak çalıştırmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="21110-132">Understanding the factors which impact request unit charges, along with your application's throughput requirements, enables you to run your application as cost effectively as possible.</span></span> <span data-ttu-id="21110-133">Sorgu Gezgini ayrıca bir sorgu çekirdek test etmek için bir harika aracıdır.</span><span class="sxs-lookup"><span data-stu-id="21110-133">The query explorer is also a wonderful tool to test the core of a query.</span></span>

<span data-ttu-id="21110-134">İstek birimleri ve Azure Cosmos DB tahmin edilebilir performansla Aravind Ramachandran burada açıklanmaktadır aşağıdaki videoyu izleyerek çalışmaya başlamanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="21110-134">We recommend getting started by watching the following video, where Aravind Ramachandran explains request units and predictable performance with Azure Cosmos DB.</span></span>

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Predictable-Performance-with-DocumentDB/player]
> 
> 

## <a name="specifying-request-unit-capacity-in-azure-cosmos-db"></a><span data-ttu-id="21110-135">İstek birimi kapasite Azure Cosmos DB'de belirtme</span><span class="sxs-lookup"><span data-stu-id="21110-135">Specifying request unit capacity in Azure Cosmos DB</span></span>
<span data-ttu-id="21110-136">Yeni koleksiyon, tablo veya grafik başlatırken numarası belirtin (RU saniye başına) saniyede istek birimlerinin ayrılmış istiyor.</span><span class="sxs-lookup"><span data-stu-id="21110-136">When starting a new collection, table or graph, you specify the number of request units per second (RU per second) you want reserved.</span></span> <span data-ttu-id="21110-137">Üzerinde sağlanan işleme bağlı olarak, Azure Cosmos DB koleksiyonunuzu barındırmak için fiziksel bölümleri ayırır ve bölmelerini/veri bölümler, büyüdükçe rebalances.</span><span class="sxs-lookup"><span data-stu-id="21110-137">Based on the provisioned throughput, Azure Cosmos DB allocates physical partitions to host your collection and splits/rebalances data across partitions as it grows.</span></span>

<span data-ttu-id="21110-138">Azure Cosmos DB koleksiyonu 2.500 istek birimleri ile sağlanan ya da daha yüksek olduğunda belirtilmesi için bir bölüm anahtarı gerektirir.</span><span class="sxs-lookup"><span data-stu-id="21110-138">Azure Cosmos DB requires a partition key to be specified when a collection is provisioned with 2,500 request units or higher.</span></span> <span data-ttu-id="21110-139">Bölüm anahtarı koleksiyonunuzun işleme 2.500 istek birimleri ötesinde gelecekte ölçeklendirmek için de gereklidir.</span><span class="sxs-lookup"><span data-stu-id="21110-139">A partition key is also required to scale your collection's throughput beyond 2,500 request units in the future.</span></span> <span data-ttu-id="21110-140">Bu nedenle, yüksek oranda yapılandırmak için önerilir bir [bölüm anahtarı](partition-data.md) ilk işleme bakılmaksızın bir kapsayıcı oluştururken.</span><span class="sxs-lookup"><span data-stu-id="21110-140">Therefore, it is highly recommended to configure a [partition key](partition-data.md) when creating a container regardless of your initial throughput.</span></span> <span data-ttu-id="21110-141">Verilerinizin birden çok bölüm arasında bölünmesi gerekebilir olduğundan, yüksek kardinalite (100 farklı değerleri milyonlarca) vardır ve böylece tablo/koleksiyonu/grafik ve istekleri Azure Cosmos DB tarafından hep genişletilebilir bir bölüm anahtarı almak gereklidir.</span><span class="sxs-lookup"><span data-stu-id="21110-141">Since your data might have to be split across multiple partitions, it is necessary to pick a partition key that has a high cardinality (100 to millions of distinct values) so that your collection/table/graph and requests can be scaled uniformly by Azure Cosmos DB.</span></span> 

> [!NOTE]
> <span data-ttu-id="21110-142">Bölüm anahtarı mantıksal bir sınır ve fiziksel bir tane ' dir.</span><span class="sxs-lookup"><span data-stu-id="21110-142">A partition key is a logical boundary, and not a physical one.</span></span> <span data-ttu-id="21110-143">Bu nedenle, farklı bölüm anahtar değerlerin sayısını sınırlamak gerekmez.</span><span class="sxs-lookup"><span data-stu-id="21110-143">Therefore, you do not need to limit the number of distinct partition key values.</span></span> <span data-ttu-id="21110-144">Aslında, daha fazla yük dengeleme seçeneklerini Azure Cosmos DB sahip daha farklı bölüm anahtarı değerden daha az olması iyidir.</span><span class="sxs-lookup"><span data-stu-id="21110-144">It is in fact better to have more distinct partition key values than less, as Azure Cosmos DB has more load balancing options.</span></span>

<span data-ttu-id="21110-145">.NET SDK kullanarak saniye başına istek birimleri 3000 ile bir koleksiyon oluşturmak için bir kod parçacığı aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="21110-145">Here is a code snippet for creating a collection with 3,000 request units per second using the .NET SDK:</span></span>

```csharp
DocumentCollection myCollection = new DocumentCollection();
myCollection.Id = "coll";
myCollection.PartitionKey.Paths.Add("/deviceId");

await client.CreateDocumentCollectionAsync(
    UriFactory.CreateDatabaseUri("db"),
    myCollection,
    new RequestOptions { OfferThroughput = 3000 });
```

<span data-ttu-id="21110-146">Azure Cosmos DB akışındaki bir ayırma modeli çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="21110-146">Azure Cosmos DB operates on a reservation model on throughput.</span></span> <span data-ttu-id="21110-147">Diğer bir deyişle, işleme miktarı faturalandırılır *ayrılmış*ne olursa olsun, üretilen işi ne kadarının etkin olduğundan, *kullanılan*.</span><span class="sxs-lookup"><span data-stu-id="21110-147">That is, you are billed for the amount of throughput *reserved*, regardless of how much of that throughput is actively *used*.</span></span> <span data-ttu-id="21110-148">Uygulamanızı olarak kullanıcının, kolayca ölçeklendirilebilir miktarını yukarı ve aşağı yük, veri ve kullanım desenlerini değişiklik ayrılmış RUs üzerinden SDK'ları veya kullanarak [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="21110-148">As your application's load, data, and usage patterns change you can easily scale up and down the amount of reserved RUs through SDKs or using the [Azure Portal](https://portal.azure.com).</span></span>

<span data-ttu-id="21110-149">Her koleksiyon/tablo/grafik eşleştirilmiş bir `Offer` kaynak, sağlanan işleme hakkındaki meta verileri olan Azure Cosmos veritabanı.</span><span class="sxs-lookup"><span data-stu-id="21110-149">Each collection/table/graph are mapped to an `Offer` resource in Azure Cosmos DB, which has metadata about the provisioned throughput.</span></span> <span data-ttu-id="21110-150">Kapsayıcı için ilgili teklif kaynak bakarak, ardından yeni işleme değeri ile güncelleştirme ayrılmış işleme değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="21110-150">You can change the allocated throughput by looking up the corresponding offer resource for a container, then updating it with the new throughput value.</span></span> <span data-ttu-id="21110-151">.NET SDK kullanarak saniye başına 5.000 istek birimi için bir koleksiyon verimini değiştirmek için bir kod parçacığı aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="21110-151">Here is a code snippet for changing the throughput of a collection to 5,000 request units per second using the .NET SDK:</span></span>

```csharp
// Fetch the resource to be updated
Offer offer = client.CreateOfferQuery()
                .Where(r => r.ResourceLink == collection.SelfLink)    
                .AsEnumerable()
                .SingleOrDefault();

// Set the throughput to 5000 request units per second
offer = new OfferV2(offer, 5000);

// Now persist these changes to the database by replacing the original resource
await client.ReplaceOfferAsync(offer);
```

<span data-ttu-id="21110-152">Üretilen iş değiştirdiğinizde, kapsayıcı kullanılabilirliğine hiçbir etkisi yoktur.</span><span class="sxs-lookup"><span data-stu-id="21110-152">There is no impact to the availability of your container when you change the throughput.</span></span> <span data-ttu-id="21110-153">Genellikle yeni ayrılmış işleme yeni işleme, uygulama üzerinde saniye içinde etkili olur.</span><span class="sxs-lookup"><span data-stu-id="21110-153">Typically the new reserved throughput is effective within seconds on application of the new throughput.</span></span>

## <a name="request-unit-considerations"></a><span data-ttu-id="21110-154">İstek birimi konuları</span><span class="sxs-lookup"><span data-stu-id="21110-154">Request unit considerations</span></span>
<span data-ttu-id="21110-155">Azure Cosmos DB kapsayıcısı için ayrılacak isteği birim sayısını tahmin yaparken, aşağıdaki değişkenleri dikkate önemlidir:</span><span class="sxs-lookup"><span data-stu-id="21110-155">When estimating the number of request units to reserve for your Azure Cosmos DB container, it is important to take the following variables into consideration:</span></span>

* <span data-ttu-id="21110-156">**Öğe boyutunu**.</span><span class="sxs-lookup"><span data-stu-id="21110-156">**Item size**.</span></span> <span data-ttu-id="21110-157">Boyutu okumak veya verileri de artıracaktır yazmak için kullanılan birimleri arttıkça.</span><span class="sxs-lookup"><span data-stu-id="21110-157">As size increases the units consumed to read or write the data will also increase.</span></span>
* <span data-ttu-id="21110-158">**Madde özellik sayısı**.</span><span class="sxs-lookup"><span data-stu-id="21110-158">**Item property count**.</span></span> <span data-ttu-id="21110-159">Tüm özellikleri, bir belge/düğümü/ntity yazmak için kullanılan birimleri olduğunu varsayarak varsayılan dizin özellik sayısı arttıkça artmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="21110-159">Assuming default indexing of all properties, the units consumed to write a document/node/ntity will increase as the property count increases.</span></span>
* <span data-ttu-id="21110-160">**Veri tutarlılığı**.</span><span class="sxs-lookup"><span data-stu-id="21110-160">**Data consistency**.</span></span> <span data-ttu-id="21110-161">Veri tutarlılık düzeylerini güçlü veya sınırlanmış eskime durumu kullanırken, ek birimler öğeleri okumak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="21110-161">When using data consistency levels of Strong or Bounded Staleness, additional units will be consumed to read items.</span></span>
* <span data-ttu-id="21110-162">**Dizin oluşturulmuş özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="21110-162">**Indexed properties**.</span></span> <span data-ttu-id="21110-163">Bir dizin İlkesi her kapsayıcısı üzerinde varsayılan olarak hangi özellikleri dizinlenir belirler.</span><span class="sxs-lookup"><span data-stu-id="21110-163">An index policy on each container determines which properties are indexed by default.</span></span> <span data-ttu-id="21110-164">Dizinli Özellikler sayısını sınırlayarak veya yavaş dizin etkinleştirerek, istek birimi tüketimini azaltabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="21110-164">You can reduce your request unit consumption by limiting the number of indexed properties or by enabling lazy indexing.</span></span>
* <span data-ttu-id="21110-165">**Belge dizine**.</span><span class="sxs-lookup"><span data-stu-id="21110-165">**Document indexing**.</span></span> <span data-ttu-id="21110-166">Bazı öğelerinizi dizin kullanılamıyor seçerseniz, her bir öğeyi otomatik olarak dizine varsayılan olarak, daha az istek birimleri tüketir.</span><span class="sxs-lookup"><span data-stu-id="21110-166">By default each item is automatically indexed, you will consume fewer request units if you choose not to index some of your items.</span></span>
* <span data-ttu-id="21110-167">**Sorgu desenleri**.</span><span class="sxs-lookup"><span data-stu-id="21110-167">**Query patterns**.</span></span> <span data-ttu-id="21110-168">Kaç tane istek birimlerine bir işlem için kullanılan bir sorgu karmaşıklığını etkiler.</span><span class="sxs-lookup"><span data-stu-id="21110-168">The complexity of a query impacts how many Request Units are consumed for an operation.</span></span> <span data-ttu-id="21110-169">Koşulları sayısı, koşulları, projeksiyonları, UDF'ler sayısı ve tüm kaynak veri kümesi boyutunu yapısını sorgu işlemlerinin maliyetini etkiler.</span><span class="sxs-lookup"><span data-stu-id="21110-169">The number of predicates, nature of the predicates, projections, number of UDFs, and the size of the source data set all influence the cost of query operations.</span></span>
* <span data-ttu-id="21110-170">**Komut dosyası kullanımı**.</span><span class="sxs-lookup"><span data-stu-id="21110-170">**Script usage**.</span></span>  <span data-ttu-id="21110-171">Sorguları olarak gerçekleştirilen işlemler kapsamına bağlı istek birimleri saklı yordamları ve Tetikleyicileri tüketir.</span><span class="sxs-lookup"><span data-stu-id="21110-171">As with queries, stored procedures and triggers consume request units based on the complexity of the operations being performed.</span></span> <span data-ttu-id="21110-172">Uygulamanızı geliştirirken, her işlem isteği birim kapasitesi nasıl tüketen daha iyi anlamak için istek ücret üstbilgisi inceleyin.</span><span class="sxs-lookup"><span data-stu-id="21110-172">As you develop your application, inspect the request charge header to better understand how each operation is consuming request unit capacity.</span></span>

## <a name="estimating-throughput-needs"></a><span data-ttu-id="21110-173">Üretilen iş gereksinimlerini tahmin etme</span><span class="sxs-lookup"><span data-stu-id="21110-173">Estimating throughput needs</span></span>
<span data-ttu-id="21110-174">Bir istek birimi istek maliyet işleme normalleştirilmiş ölçüsüdür.</span><span class="sxs-lookup"><span data-stu-id="21110-174">A request unit is a normalized measure of request processing cost.</span></span> <span data-ttu-id="21110-175">Bir tek istek birimi (kendi bağlantısını veya kimliği) öğesi 10 benzersiz özellik değerlerini (Sistem özellikleri dışında) oluşan tek 1 bb okumak için gereken işlem kapasitesi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="21110-175">A single request unit represents the processing capacity required to read (via self link or id) a single 1KB item consisting of 10 unique property values (excluding system properties).</span></span> <span data-ttu-id="21110-176">Daha fazla hizmet ve böylece işleme daha fazla istek birimi (Ekle) oluşturmak, değiştirmek veya aynı öğeyi silmek için bir istek tüketir.</span><span class="sxs-lookup"><span data-stu-id="21110-176">A request to create (insert), replace or delete the same item will consume more processing from the service and thereby more request units.</span></span>   

> [!NOTE]
> <span data-ttu-id="21110-177">1 istek birimi bir 1KB için temel kendi bağlantısını veya öğenin kimliği için basit bir GET öğesi karşılık gelir.</span><span class="sxs-lookup"><span data-stu-id="21110-177">The baseline of 1 request unit for a 1KB item corresponds to a simple GET by self link or id of the item.</span></span>
> 
> 

<span data-ttu-id="21110-178">Örneğin, üç farklı öğe boyut (1 KB, 4 KB ve 64 KB) ve iki farklı performans düzeyleri sağlamak için kaç tane istek birimleri gösteren bir tablo İşte (500 Okuma/saniye 100 yazma/saniye ve 500 Okuma/saniye + 500 yazma/saniye).</span><span class="sxs-lookup"><span data-stu-id="21110-178">For example, here's a table that shows how many request units to provision at three different item sizes (1KB, 4KB, and 64KB) and at two different performance levels (500 reads/second + 100 writes/second and 500 reads/second + 500 writes/second).</span></span> <span data-ttu-id="21110-179">Veri tutarlılığı oturumunda yapılandırılmış ve dizin oluşturma ilkesi None olarak ayarlanmış.</span><span class="sxs-lookup"><span data-stu-id="21110-179">The data consistency was configured at Session, and the indexing policy was set to None.</span></span>

<table border="0" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td valign="top"><p><span data-ttu-id="21110-180"><strong>Öğesi boyutu</strong></span><span class="sxs-lookup"><span data-stu-id="21110-180"><strong>Item size</strong></span></span></p></td>
            <td valign="top"><p><span data-ttu-id="21110-181"><strong>Okuma/saniye</strong></span><span class="sxs-lookup"><span data-stu-id="21110-181"><strong>Reads/second</strong></span></span></p></td>
            <td valign="top"><p><span data-ttu-id="21110-182"><strong>Yazma/saniye</strong></span><span class="sxs-lookup"><span data-stu-id="21110-182"><strong>Writes/second</strong></span></span></p></td>
            <td valign="top"><p><span data-ttu-id="21110-183"><strong>İstek birimleri</strong></span><span class="sxs-lookup"><span data-stu-id="21110-183"><strong>Request units</strong></span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="21110-184">1 KB</span><span class="sxs-lookup"><span data-stu-id="21110-184">1 KB</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="21110-185">500</span><span class="sxs-lookup"><span data-stu-id="21110-185">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="21110-186">100</span><span class="sxs-lookup"><span data-stu-id="21110-186">100</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="21110-187">(500 * 1) + (100 * 5) = 1.000 RU/s</span><span class="sxs-lookup"><span data-stu-id="21110-187">(500 * 1) + (100 * 5) = 1,000 RU/s</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="21110-188">1 KB</span><span class="sxs-lookup"><span data-stu-id="21110-188">1 KB</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="21110-189">500</span><span class="sxs-lookup"><span data-stu-id="21110-189">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="21110-190">500</span><span class="sxs-lookup"><span data-stu-id="21110-190">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="21110-191">(500 * 1) + (500 * 5) = 3000 RU/s</span><span class="sxs-lookup"><span data-stu-id="21110-191">(500 * 1) + (500 * 5) = 3,000 RU/s</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="21110-192">4 KB</span><span class="sxs-lookup"><span data-stu-id="21110-192">4 KB</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="21110-193">500</span><span class="sxs-lookup"><span data-stu-id="21110-193">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="21110-194">100</span><span class="sxs-lookup"><span data-stu-id="21110-194">100</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="21110-195">(500 * 1,3) + (100 * 7) = 1,350 RU/s</span><span class="sxs-lookup"><span data-stu-id="21110-195">(500 * 1.3) + (100 * 7) = 1,350 RU/s</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="21110-196">4 KB</span><span class="sxs-lookup"><span data-stu-id="21110-196">4 KB</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="21110-197">500</span><span class="sxs-lookup"><span data-stu-id="21110-197">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="21110-198">500</span><span class="sxs-lookup"><span data-stu-id="21110-198">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="21110-199">(500 * 1,3) + (500 * 7) = 4,150 RU/s</span><span class="sxs-lookup"><span data-stu-id="21110-199">(500 * 1.3) + (500 * 7) = 4,150 RU/s</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="21110-200">64 KB</span><span class="sxs-lookup"><span data-stu-id="21110-200">64 KB</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="21110-201">500</span><span class="sxs-lookup"><span data-stu-id="21110-201">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="21110-202">100</span><span class="sxs-lookup"><span data-stu-id="21110-202">100</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="21110-203">(500 * 10) + (100 * 48) = 9,800 RU/s</span><span class="sxs-lookup"><span data-stu-id="21110-203">(500 * 10) + (100 * 48) = 9,800 RU/s</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="21110-204">64 KB</span><span class="sxs-lookup"><span data-stu-id="21110-204">64 KB</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="21110-205">500</span><span class="sxs-lookup"><span data-stu-id="21110-205">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="21110-206">500</span><span class="sxs-lookup"><span data-stu-id="21110-206">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="21110-207">(500 * 10) + (500 * 48) = 29,000 RU/s</span><span class="sxs-lookup"><span data-stu-id="21110-207">(500 * 10) + (500 * 48) = 29,000 RU/s</span></span></p></td>
        </tr>
    </tbody>
</table>

### <a name="use-the-request-unit-calculator"></a><span data-ttu-id="21110-208">İstek birimi hesaplayıcı kullanın</span><span class="sxs-lookup"><span data-stu-id="21110-208">Use the request unit calculator</span></span>
<span data-ttu-id="21110-209">İnce müşterilere yardımcı olmak için kendi verimlilik tahminler ince ayar, bir web tabanlı [istek birimi hesaplayıcı](https://www.documentdb.com/capacityplanner) genel işlemler de dahil olmak üzere, istek birimi gereksinimlerini tahmin etmeye yardımcı olması için:</span><span class="sxs-lookup"><span data-stu-id="21110-209">To help customers fine tune their throughput estimations, there is a web based [request unit calculator](https://www.documentdb.com/capacityplanner) to help estimate the request unit requirements for typical operations, including:</span></span>

* <span data-ttu-id="21110-210">(Yazar) öğesi oluşturur</span><span class="sxs-lookup"><span data-stu-id="21110-210">Item creates (writes)</span></span>
* <span data-ttu-id="21110-211">Öğe okur</span><span class="sxs-lookup"><span data-stu-id="21110-211">Item reads</span></span>
* <span data-ttu-id="21110-212">Öğeyi siler</span><span class="sxs-lookup"><span data-stu-id="21110-212">Item deletes</span></span>
* <span data-ttu-id="21110-213">Öğesi güncelleştirmeleri</span><span class="sxs-lookup"><span data-stu-id="21110-213">Item updates</span></span>

<span data-ttu-id="21110-214">Aracı, sağladığınız örnek öğeleri temel alan veri depolama gereksinimlerini tahmin etmek için destek de içerir.</span><span class="sxs-lookup"><span data-stu-id="21110-214">The tool also includes support for estimating data storage needs based on the sample items you provide.</span></span>

<span data-ttu-id="21110-215">Aracını kullanarak basit bir işlemdir:</span><span class="sxs-lookup"><span data-stu-id="21110-215">Using the tool is simple:</span></span>

1. <span data-ttu-id="21110-216">Bir veya daha fazla temsilcisi öğeleri karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="21110-216">Upload one or more representative items.</span></span>
   
    ![İstek birimi makinesine öğeleri karşıya yükle][2]
2. <span data-ttu-id="21110-218">Veri depolama gereksinimlerini tahmin etmek için toplam depolamayı beklediğiniz öğe sayısını girin.</span><span class="sxs-lookup"><span data-stu-id="21110-218">To estimate data storage requirements, enter the total number of items you expect to store.</span></span>
3. <span data-ttu-id="21110-219">Girin öğe sayısı oluşturma, okuma, güncelleştirme ve silme işlemleri (bir saniye başına temelinde) gerektirir.</span><span class="sxs-lookup"><span data-stu-id="21110-219">Enter the number of items create, read, update, and delete operations you require (on a per-second basis).</span></span> <span data-ttu-id="21110-220">İstek birimi ücretleri öğesi güncelleştirme işlemlerinin tahmin etmek için 1. adımdaki tipik alan güncelleştirmeleri içeren Yukarıdaki örnek öğenin bir kopyasını yükleyin.</span><span class="sxs-lookup"><span data-stu-id="21110-220">To estimate the request unit charges of item update operations, upload a copy of the sample item from step 1 above that includes typical field updates.</span></span>  <span data-ttu-id="21110-221">Örneğin, öğesi güncelleştirmeler genellikle lastLogin ve userVisits adlı iki özellik değiştirirseniz, ardından yalnızca örnek öğesi kopyalayın, bu iki özellik için değerleri güncelleştirmek ve kopyalanan öğeyi karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="21110-221">For example, if item updates typically modify two properties named lastLogin and userVisits, then simply copy the sample item, update the values for those two properties, and upload the copied item.</span></span>
   
    ![Üretilen iş gereksinimleri istek birimi hesaplayıcı girin][3]
4. <span data-ttu-id="21110-223">Tıklatın hesaplamak ve sonuçları inceleyin.</span><span class="sxs-lookup"><span data-stu-id="21110-223">Click calculate and examine the results.</span></span>
   
    ![Birim hesaplayıcı sonuçları isteği][4]

> [!NOTE]
> <span data-ttu-id="21110-225">Boyutu ve Dizinli Özellikler sayısı bakımından önemli ölçüde farklılık gösterecektir öğesi türleri varsa, her bir örnek karşıya yükleme *türü* tipik öğesi için araç ve sonuçları hesaplayın.</span><span class="sxs-lookup"><span data-stu-id="21110-225">If you have item types which will differ dramatically in terms of size and the number of indexed properties, then upload a sample of each *type* of typical item to the tool and then calculate the results.</span></span>
> 
> 

### <a name="use-the-azure-cosmos-db-request-charge-response-header"></a><span data-ttu-id="21110-226">Azure Cosmos DB istek ücret yanıt üstbilgisi kullanın</span><span class="sxs-lookup"><span data-stu-id="21110-226">Use the Azure Cosmos DB request charge response header</span></span>
<span data-ttu-id="21110-227">Her yanıt Azure Cosmos DB hizmetinden bir özel üst bilgi içeriyor (`x-ms-request-charge`) istek için kullanılan istek birimleri içerir.</span><span class="sxs-lookup"><span data-stu-id="21110-227">Every response from the Azure Cosmos DB service includes a custom header (`x-ms-request-charge`) that contains the request units consumed for the request.</span></span> <span data-ttu-id="21110-228">Bu üst ayrıca Azure Cosmos DB SDK erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="21110-228">This header is also accessible through the Azure Cosmos DB SDKs.</span></span> <span data-ttu-id="21110-229">.NET SDK'ın RequestCharge ResourceResponse nesnesinin bir özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="21110-229">In the .NET SDK, RequestCharge is a property of the ResourceResponse object.</span></span>  <span data-ttu-id="21110-230">Sorgular için Azure portalında Azure Cosmos DB sorgu Gezgini yürütülen sorgular için istek ücret bilgileri sağlar.</span><span class="sxs-lookup"><span data-stu-id="21110-230">For queries, the Azure Cosmos DB Query Explorer in the Azure portal provides request charge information for executed queries.</span></span>

![Sorgu Gezgini RU ücretlere inceleniyor][1]

<span data-ttu-id="21110-232">Bu durum dikkate alınarak, uygulamanızın gerektirdiği ayrılmış işleme miktarı tahmin etmek için bir yöntem, uygulamanız tarafından kullanılan ve ardından tahmin etme temsili bir öğe karşı çalışan tipik işlemlerle ilişkili istek birimi ücret kaydetmektir saniyede gerçekleştirme düşündüğünüz işlemlerinin sayısı.</span><span class="sxs-lookup"><span data-stu-id="21110-232">With this in mind, one method for estimating the amount of reserved throughput required by your application is to record the request unit charge associated with running typical operations against a representative item used by your application and then estimating the number of operations you anticipate performing each second.</span></span>  <span data-ttu-id="21110-233">Ölçmek ve tipik sorgular ve Azure Cosmos DB komut dosyası kullanımı da dahil emin olun.</span><span class="sxs-lookup"><span data-stu-id="21110-233">Be sure to measure and include typical queries and Azure Cosmos DB script usage as well.</span></span>

> [!NOTE]
> <span data-ttu-id="21110-234">Hangi boyutu ve Dizinli Özellikler sayısı bakımından önemli ölçüde farklılık gösterecektir öğesi türleriniz varsa, her ilişkilendirilmiş geçerli işlem istek birimi ücret kayıt *türü* tipik öğesi.</span><span class="sxs-lookup"><span data-stu-id="21110-234">If you have item types which will differ dramatically in terms of size and the number of indexed properties, then record the applicable operation request unit charge associated with each *type* of typical item.</span></span>
> 
> 

<span data-ttu-id="21110-235">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="21110-235">For example:</span></span>

1. <span data-ttu-id="21110-236">(Ekleme) oluşturma isteği birim ücret kayıt tipik bir öğe.</span><span class="sxs-lookup"><span data-stu-id="21110-236">Record the request unit charge of creating (inserting) a typical item.</span></span> 
2. <span data-ttu-id="21110-237">Tipik bir öğe Okuma isteği birim ücret kaydedin.</span><span class="sxs-lookup"><span data-stu-id="21110-237">Record the request unit charge of reading a typical item.</span></span>
3. <span data-ttu-id="21110-238">Tipik bir öğesi güncelleştirme isteği birim ücret kaydedin.</span><span class="sxs-lookup"><span data-stu-id="21110-238">Record the request unit charge of updating a typical item.</span></span>
4. <span data-ttu-id="21110-239">Tipik, ortak öğesi sorgularını istek birimi olarak kaydedin.</span><span class="sxs-lookup"><span data-stu-id="21110-239">Record the request unit charge of typical, common item queries.</span></span>
5. <span data-ttu-id="21110-240">Uygulama tarafından işlevden istek birimi ücret tüm özel komut dosyalarını (saklı yordamlar, Tetikleyiciler, kullanıcı tanımlı işlevler), kayıt</span><span class="sxs-lookup"><span data-stu-id="21110-240">Record the request unit charge of any custom scripts (stored procedures, triggers, user-defined functions) leveraged by the application</span></span>
6. <span data-ttu-id="21110-241">Saniyede çalıştırmayı düşündüğünüz operations tahmini sayısını verilen gerekli istek birimleri hesaplayın.</span><span class="sxs-lookup"><span data-stu-id="21110-241">Calculate the required request units given the estimated number of operations you anticipate to run each second.</span></span>

### <span data-ttu-id="21110-242"><a id="GetLastRequestStatistics"></a>API MongoDB'ın GetLastRequestStatistics komutu için kullanın</span><span class="sxs-lookup"><span data-stu-id="21110-242"><a id="GetLastRequestStatistics"></a>Use API for MongoDB's GetLastRequestStatistics command</span></span>
<span data-ttu-id="21110-243">API MongoDB için özel bir komut destekler *getLastRequestStatistics*, belirtilen işlem için istek ücret alma.</span><span class="sxs-lookup"><span data-stu-id="21110-243">API for MongoDB supports a custom command, *getLastRequestStatistics*, for retrieving the request charge for specified operations.</span></span>

<span data-ttu-id="21110-244">Örneğin, istek ücreti doğrulamak istediğiniz işlem Mongo kabuğunu yürütün.</span><span class="sxs-lookup"><span data-stu-id="21110-244">For example, in the Mongo Shell, execute the operation you want to verify the request charge for.</span></span>
```
> db.sample.find()
```

<span data-ttu-id="21110-245">Ardından, komutu yürütün *getLastRequestStatistics*.</span><span class="sxs-lookup"><span data-stu-id="21110-245">Next, execute the command *getLastRequestStatistics*.</span></span>
```
> db.runCommand({getLastRequestStatistics: 1})
{
    "_t": "GetRequestStatisticsResponse",
    "ok": 1,
    "CommandName": "OP_QUERY",
    "RequestCharge": 2.48,
    "RequestDurationInMilliSeconds" : 4.0048
}
```

<span data-ttu-id="21110-246">Bu durum dikkate alınarak, uygulamanızın gerektirdiği ayrılmış işleme miktarı tahmin etmek için bir yöntem, uygulamanız tarafından kullanılan ve ardından tahmin etme temsili bir öğe karşı çalışan tipik işlemlerle ilişkili istek birimi ücret kaydetmektir saniyede gerçekleştirme düşündüğünüz işlemlerinin sayısı.</span><span class="sxs-lookup"><span data-stu-id="21110-246">With this in mind, one method for estimating the amount of reserved throughput required by your application is to record the request unit charge associated with running typical operations against a representative item used by your application and then estimating the number of operations you anticipate performing each second.</span></span>

> [!NOTE]
> <span data-ttu-id="21110-247">Hangi boyutu ve Dizinli Özellikler sayısı bakımından önemli ölçüde farklılık gösterecektir öğesi türleriniz varsa, her ilişkilendirilmiş geçerli işlem istek birimi ücret kayıt *türü* tipik öğesi.</span><span class="sxs-lookup"><span data-stu-id="21110-247">If you have item types which will differ dramatically in terms of size and the number of indexed properties, then record the applicable operation request unit charge associated with each *type* of typical item.</span></span>
> 
> 

## <a name="use-api-for-mongodbs-portal-metrics"></a><span data-ttu-id="21110-248">API MongoDB'ın portal ölçümleri kullanın</span><span class="sxs-lookup"><span data-stu-id="21110-248">Use API for MongoDB's portal metrics</span></span>
<span data-ttu-id="21110-249">MongoDB veritabanı kullanmak için iyi tahmini isteğinin birim ücretleri API için almanın en basit yolu [Azure portal](https://portal.azure.com) ölçümleri.</span><span class="sxs-lookup"><span data-stu-id="21110-249">The simplest way to get a good estimation of request unit charges for your API for MongoDB database is to use the [Azure portal](https://portal.azure.com) metrics.</span></span> <span data-ttu-id="21110-250">İle *istek sayısı* ve *isteği ücret* grafikler, kaç tane isteği birimlerin her işlem harcayan ve kaç tane istek birimleri bunlar tüketen birbirine göre bir tahmin alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="21110-250">With the *Number of requests* and *Request Charge* charts, you can get an estimation of how many request units each operation is consuming and how many request units they consume relative to one another.</span></span>

![API MongoDB portal ölçümleri için][6]

## <a name="a-request-unit-estimation-example"></a><span data-ttu-id="21110-252">Bir istek birimi tahmin örneği</span><span class="sxs-lookup"><span data-stu-id="21110-252">A request unit estimation example</span></span>
<span data-ttu-id="21110-253">Aşağıdaki ~ 1 KB belge göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="21110-253">Consider the following ~1KB document:</span></span>

```json
{
 "id": "08259",
  "description": "Cereals ready-to-eat, KELLOGG, KELLOGG'S CRISPIX",
  "tags": [
    {
      "name": "cereals ready-to-eat"
    },
    {
      "name": "kellogg"
    },
    {
      "name": "kellogg's crispix"
    }
  ],
  "version": 1,
  "commonName": "Includes USDA Commodity B855",
  "manufacturerName": "Kellogg, Co.",
  "isFromSurvey": false,
  "foodGroup": "Breakfast Cereals",
  "nutrients": [
    {
      "id": "262",
      "description": "Caffeine",
      "nutritionValue": 0,
      "units": "mg"
    },
    {
      "id": "307",
      "description": "Sodium, Na",
      "nutritionValue": 611,
      "units": "mg"
    },
    {
      "id": "309",
      "description": "Zinc, Zn",
      "nutritionValue": 5.2,
      "units": "mg"
    }
  ],
  "servings": [
    {
      "amount": 1,
      "description": "cup (1 NLEA serving)",
      "weightInGrams": 29
    }
  ]
}
```

> [!NOTE]
> <span data-ttu-id="21110-254">Sistem yukarıdaki belgenin boyutu 1 KB biraz değerinden hesaplanır şekilde belgeler Azure Cosmos DB'de küçültülmüş.</span><span class="sxs-lookup"><span data-stu-id="21110-254">Documents are minified in Azure Cosmos DB, so the system calculated size of the document above is slightly less than 1KB.</span></span>
> 
> 

<span data-ttu-id="21110-255">Aşağıdaki tabloda yaklaşık istek birimi giderleri (yaklaşık istek birimi ücret hesabı tutarlılık düzeyi "Oturumuna" olarak ayarlandığından ve tüm öğeler otomatik olarak dizine varsayar) öğenin normal işlemleri için gösterilir:</span><span class="sxs-lookup"><span data-stu-id="21110-255">The following table shows approximate request unit charges for typical operations on this item (the approximate request unit charge assumes that the account consistency level is set to “Session” and that all items are automatically indexed):</span></span>

| <span data-ttu-id="21110-256">İşlem</span><span class="sxs-lookup"><span data-stu-id="21110-256">Operation</span></span> | <span data-ttu-id="21110-257">İstek birimi ücret</span><span class="sxs-lookup"><span data-stu-id="21110-257">Request Unit Charge</span></span> |
| --- | --- |
| <span data-ttu-id="21110-258">Öğesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="21110-258">Create item</span></span> |<span data-ttu-id="21110-259">~ 15 RU</span><span class="sxs-lookup"><span data-stu-id="21110-259">~15 RU</span></span> |
| <span data-ttu-id="21110-260">Öğe Okuma</span><span class="sxs-lookup"><span data-stu-id="21110-260">Read item</span></span> |<span data-ttu-id="21110-261">~ 1 RU</span><span class="sxs-lookup"><span data-stu-id="21110-261">~1 RU</span></span> |
| <span data-ttu-id="21110-262">Sorgu öğesi kimliği</span><span class="sxs-lookup"><span data-stu-id="21110-262">Query item by id</span></span> |<span data-ttu-id="21110-263">~2.5 RU</span><span class="sxs-lookup"><span data-stu-id="21110-263">~2.5 RU</span></span> |

<span data-ttu-id="21110-264">Ayrıca, bu tabloda yaklaşık istek birimi ücretleri uygulamada kullanılan tipik sorguları için gösterilir:</span><span class="sxs-lookup"><span data-stu-id="21110-264">Additionally, this table shows approximate request unit charges for typical queries used in the application:</span></span>

| <span data-ttu-id="21110-265">Sorgu</span><span class="sxs-lookup"><span data-stu-id="21110-265">Query</span></span> | <span data-ttu-id="21110-266">İstek birimi ücret</span><span class="sxs-lookup"><span data-stu-id="21110-266">Request Unit Charge</span></span> | <span data-ttu-id="21110-267">Döndürülen öğe sayısı</span><span class="sxs-lookup"><span data-stu-id="21110-267"># of Returned Items</span></span> |
| --- | --- | --- |
| <span data-ttu-id="21110-268">Kimliğe göre yemek seçin</span><span class="sxs-lookup"><span data-stu-id="21110-268">Select food by id</span></span> |<span data-ttu-id="21110-269">~2.5 RU</span><span class="sxs-lookup"><span data-stu-id="21110-269">~2.5 RU</span></span> |<span data-ttu-id="21110-270">1</span><span class="sxs-lookup"><span data-stu-id="21110-270">1</span></span> |
| <span data-ttu-id="21110-271">Üretici tarafından foods seçin</span><span class="sxs-lookup"><span data-stu-id="21110-271">Select foods by manufacturer</span></span> |<span data-ttu-id="21110-272">~ 7 RU</span><span class="sxs-lookup"><span data-stu-id="21110-272">~7 RU</span></span> |<span data-ttu-id="21110-273">7</span><span class="sxs-lookup"><span data-stu-id="21110-273">7</span></span> |
| <span data-ttu-id="21110-274">Yemek grup ve sipariş ağırlığa göre seçin</span><span class="sxs-lookup"><span data-stu-id="21110-274">Select by food group and order by weight</span></span> |<span data-ttu-id="21110-275">~ 70 RU</span><span class="sxs-lookup"><span data-stu-id="21110-275">~70 RU</span></span> |<span data-ttu-id="21110-276">100</span><span class="sxs-lookup"><span data-stu-id="21110-276">100</span></span> |
| <span data-ttu-id="21110-277">Üst 10 foods yemek grubunda seçin</span><span class="sxs-lookup"><span data-stu-id="21110-277">Select top 10 foods in a food group</span></span> |<span data-ttu-id="21110-278">~ 10 RU</span><span class="sxs-lookup"><span data-stu-id="21110-278">~10 RU</span></span> |<span data-ttu-id="21110-279">10</span><span class="sxs-lookup"><span data-stu-id="21110-279">10</span></span> |

> [!NOTE]
> <span data-ttu-id="21110-280">RU ücretleri döndürülen öğe sayısını göre farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="21110-280">RU charges vary based on the number of items returned.</span></span>
> 
> 

<span data-ttu-id="21110-281">Bu bilgi ile biz işlemler ve saniye başına bekliyoruz sorguları sayısı verilen bu uygulama için RU gereksinimlerini tahmin edebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="21110-281">With this information, we can estimate the RU requirements for this application given the number of operations and queries we expect per second:</span></span>

| <span data-ttu-id="21110-282">İşlem/sorgu</span><span class="sxs-lookup"><span data-stu-id="21110-282">Operation/Query</span></span> | <span data-ttu-id="21110-283">Saniye başına tahmini sayısı</span><span class="sxs-lookup"><span data-stu-id="21110-283">Estimated number per second</span></span> | <span data-ttu-id="21110-284">Gerekli RUs</span><span class="sxs-lookup"><span data-stu-id="21110-284">Required RUs</span></span> |
| --- | --- | --- |
| <span data-ttu-id="21110-285">Öğesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="21110-285">Create item</span></span> |<span data-ttu-id="21110-286">10</span><span class="sxs-lookup"><span data-stu-id="21110-286">10</span></span> |<span data-ttu-id="21110-287">150</span><span class="sxs-lookup"><span data-stu-id="21110-287">150</span></span> |
| <span data-ttu-id="21110-288">Öğe Okuma</span><span class="sxs-lookup"><span data-stu-id="21110-288">Read item</span></span> |<span data-ttu-id="21110-289">100</span><span class="sxs-lookup"><span data-stu-id="21110-289">100</span></span> |<span data-ttu-id="21110-290">100</span><span class="sxs-lookup"><span data-stu-id="21110-290">100</span></span> |
| <span data-ttu-id="21110-291">Üretici tarafından foods seçin</span><span class="sxs-lookup"><span data-stu-id="21110-291">Select foods by manufacturer</span></span> |<span data-ttu-id="21110-292">25</span><span class="sxs-lookup"><span data-stu-id="21110-292">25</span></span> |<span data-ttu-id="21110-293">175</span><span class="sxs-lookup"><span data-stu-id="21110-293">175</span></span> |
| <span data-ttu-id="21110-294">Yemek gruplandırma ölçütü seçin</span><span class="sxs-lookup"><span data-stu-id="21110-294">Select by food group</span></span> |<span data-ttu-id="21110-295">10</span><span class="sxs-lookup"><span data-stu-id="21110-295">10</span></span> |<span data-ttu-id="21110-296">700</span><span class="sxs-lookup"><span data-stu-id="21110-296">700</span></span> |
| <span data-ttu-id="21110-297">İlk 10 seçin</span><span class="sxs-lookup"><span data-stu-id="21110-297">Select top 10</span></span> |<span data-ttu-id="21110-298">15</span><span class="sxs-lookup"><span data-stu-id="21110-298">15</span></span> |<span data-ttu-id="21110-299">150 toplam</span><span class="sxs-lookup"><span data-stu-id="21110-299">150 Total</span></span> |

<span data-ttu-id="21110-300">Bu durumda, bir ortalama verimi gereksinimi 1,275 RU/s bekliyoruz.</span><span class="sxs-lookup"><span data-stu-id="21110-300">In this case, we expect an average throughput requirement of 1,275 RU/s.</span></span>  <span data-ttu-id="21110-301">Yuvarlama kadar yakın 100, biz bu uygulamanın koleksiyon için 1300 RU/s sağlamak.</span><span class="sxs-lookup"><span data-stu-id="21110-301">Rounding up to the nearest 100, we would provision 1,300 RU/s for this application's collection.</span></span>

## <span data-ttu-id="21110-302"><a id="RequestRateTooLarge"></a>Azure Cosmos DB aşan ayrılmış işleme sınırları</span><span class="sxs-lookup"><span data-stu-id="21110-302"><a id="RequestRateTooLarge"></a> Exceeding reserved throughput limits in Azure Cosmos DB</span></span>
<span data-ttu-id="21110-303">İstek birimi tüketim bütçe boşsa, saniye başına oranı olarak değerlendirilir, geri çağırma.</span><span class="sxs-lookup"><span data-stu-id="21110-303">Recall that request unit consumption is evaluated as a rate per second if the budget is empty.</span></span> <span data-ttu-id="21110-304">Hızı ayrılmış düzeyin altına düşene kadar kapsayıcı için sağlanan istek birimi hızı aşan uygulamalar için o koleksiyona istekleri kısıtlanacak.</span><span class="sxs-lookup"><span data-stu-id="21110-304">For applications that exceed the provisioned request unit rate for a container, requests to that collection will be throttled until the rate drops below the reserved level.</span></span> <span data-ttu-id="21110-305">Bir kısıtlama oluştuğunda sunucusu erken önlem isteği RequestRateTooLargeException (HTTP durum kodu 429) ile bitmelidir ve kullanıcı reattempting önce beklemesi gereken milisaniye cinsinden süreyi belirten x-ms-yeniden deneme-sonra-ms üstbilgisi döndürme İstek.</span><span class="sxs-lookup"><span data-stu-id="21110-305">When a throttle occurs, the server will preemptively end the request with RequestRateTooLargeException (HTTP status code 429) and return the x-ms-retry-after-ms header indicating the amount of time, in milliseconds, that the user must wait before reattempting the request.</span></span>

    HTTP Status 429
    Status Line: RequestRateTooLarge
    x-ms-retry-after-ms :100

<span data-ttu-id="21110-306">.NET İstemci SDK'sını ve LINQ sorgularını sonra hiçbir zaman sahip geçerli sürümü .NET İstemci SDK'sı, bu yanıt örtük olarak yakalar gibi bu özel durumu ile mücadele etmek için çoğunlukla kullanıyorsanız, sunucu tarafından belirtilen yeniden deneme sonrasında üstbilgi dikkate alır ve yeniden deneme sayısı İstek.</span><span class="sxs-lookup"><span data-stu-id="21110-306">If you are using the .NET Client SDK and LINQ queries, then most of the time you never have to deal with this exception, as the current version of the .NET Client SDK implicitly catches this response, respects the server-specified retry-after header, and retries the request.</span></span> <span data-ttu-id="21110-307">Hesabınızı eşzamanlı olarak birden çok istemci tarafından erişilen sürece, sonraki yeniden deneme işlemi başarılı olur.</span><span class="sxs-lookup"><span data-stu-id="21110-307">Unless your account is being accessed concurrently by multiple clients, the next retry will succeed.</span></span>

<span data-ttu-id="21110-308">İstek hızı işletim üst üste birden fazla istemciniz varsa varsayılan yeniden deneme davranışı değil yeterli olacaktır ve istemci uygulamaya 429 durum koduyla bir DocumentClientException atar.</span><span class="sxs-lookup"><span data-stu-id="21110-308">If you have more than one client cumulatively operating above the request rate, the default retry behavior may not suffice, and the client will throw a DocumentClientException with status code 429 to the application.</span></span> <span data-ttu-id="21110-309">Bu gibi durumlarda, yeniden deneme davranışı ve yordamları işleme veya kapsayıcı için ayrılmış verimliliği artırma uygulamanızın hata mantığının işleme düşünebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="21110-309">In cases such as this, you may consider handling retry behavior and logic in your application's error handling routines or increasing the reserved throughput for the container.</span></span>

## <span data-ttu-id="21110-310"><a id="RequestRateTooLargeAPIforMongoDB"></a>API MongoDB için aşan ayrılmış işleme sınırları</span><span class="sxs-lookup"><span data-stu-id="21110-310"><a id="RequestRateTooLargeAPIforMongoDB"></a> Exceeding reserved throughput limits in API for MongoDB</span></span>
<span data-ttu-id="21110-311">Bir koleksiyon için sağlanan istek birimleri aşan uygulamaları oranı ayrılmış düzeyin altına düşene kadar kısıtlanacak.</span><span class="sxs-lookup"><span data-stu-id="21110-311">Applications that exceed the provisioned request units for a collection will be throttled until the rate drops below the reserved level.</span></span> <span data-ttu-id="21110-312">Bir azaltma ortaya çıktığında, arka uç istekle erken önlem sona erer bir *16500* hata kodu - *çok fazla istek*.</span><span class="sxs-lookup"><span data-stu-id="21110-312">When a throttle occurs, the backend will preemptively end the request with a *16500* error code - *Too Many Requests*.</span></span> <span data-ttu-id="21110-313">Varsayılan olarak, API MongoDB için otomatik olarak en fazla 10 kez döndürmeden önce yeniden deneyecek bir *çok fazla istek* hata kodu.</span><span class="sxs-lookup"><span data-stu-id="21110-313">By default, API for MongoDB will automatically retry up to 10 times before returning a *Too Many Requests* error code.</span></span> <span data-ttu-id="21110-314">Birçok alıyorsanız *çok fazla istek* hata kodları, uygulamanızın hata yordamları işlemedeki ekleme ya da yeniden deneme davranışı dikkate veya [koleksiyoniçinayrılmışverimliliğiartırma](set-throughput.md).</span><span class="sxs-lookup"><span data-stu-id="21110-314">If you are receiving many *Too Many Requests* error codes, you may consider either adding retry behavior in your application's error handling routines or [increasing the reserved throughput for the collection](set-throughput.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="21110-315">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="21110-315">Next steps</span></span>
<span data-ttu-id="21110-316">Ayrılmış işleme ile Azure Cosmos DB veritabanları hakkında daha fazla bilgi edinmek için şu kaynakları araştırın:</span><span class="sxs-lookup"><span data-stu-id="21110-316">To learn more about reserved throughput with Azure Cosmos DB databases, explore these resources:</span></span>

* [<span data-ttu-id="21110-317">Cosmos DB Azure fiyatlandırması</span><span class="sxs-lookup"><span data-stu-id="21110-317">Azure Cosmos DB pricing</span></span>](https://azure.microsoft.com/pricing/details/cosmos-db/)
* [<span data-ttu-id="21110-318">Azure Cosmos veritabanı veri bölümlendirme</span><span class="sxs-lookup"><span data-stu-id="21110-318">Partitioning data in Azure Cosmos DB</span></span>](partition-data.md)

<span data-ttu-id="21110-319">Azure Cosmos DB hakkında daha fazla bilgi için Azure Cosmos DB bkz [belgelerine](https://azure.microsoft.com/documentation/services/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="21110-319">To learn more about Azure Cosmos DB, see the Azure Cosmos DB [documentation](https://azure.microsoft.com/documentation/services/cosmos-db/).</span></span> 

<span data-ttu-id="21110-320">Ölçek ve performans testi Azure Cosmos DB ile kullanmaya başlamak için bkz: [performans ve ölçek testi Azure Cosmos DB ile](performance-testing.md).</span><span class="sxs-lookup"><span data-stu-id="21110-320">To get started with scale and performance testing with Azure Cosmos DB, see [Performance and Scale Testing with Azure Cosmos DB](performance-testing.md).</span></span>

[1]: ./media/request-units/queryexplorer.png 
[2]: ./media/request-units/RUEstimatorUpload.png
[3]: ./media/request-units/RUEstimatorDocuments.png
[4]: ./media/request-units/RUEstimatorResults.png
[5]: ./media/request-units/RUCalculator2.png
[6]: ./media/request-units/api-for-mongodb-metrics.png
