---
title: "aaaRequest birimler ve üretilen işi tahmin etme - Azure Cosmos DB | Microsoft Docs"
description: "Toounderstand, belirtin ve Azure Cosmos veritabanı istek birimi gereksinimlerini tahmin etme hakkında bilgi edinin."
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
ms.openlocfilehash: 13c4e7aeb6222fa14ef982e238716e15a0159fd5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="request-units-in-azure-cosmos-db"></a><span data-ttu-id="860e4-103">Azure Cosmos DB birimlerinde isteği</span><span class="sxs-lookup"><span data-stu-id="860e4-103">Request Units in Azure Cosmos DB</span></span>
<span data-ttu-id="860e4-104">Artık kullanılabilir: Azure Cosmos DB [istek birimi hesaplayıcı](https://www.documentdb.com/capacityplanner).</span><span class="sxs-lookup"><span data-stu-id="860e4-104">Now available: Azure Cosmos DB [request unit calculator](https://www.documentdb.com/capacityplanner).</span></span> <span data-ttu-id="860e4-105">Daha fazla bilgi edinin [, üretilen iş gerektiğini tahmin etme](request-units.md#estimating-throughput-needs).</span><span class="sxs-lookup"><span data-stu-id="860e4-105">Learn more in [Estimating your throughput needs](request-units.md#estimating-throughput-needs).</span></span>

![Üretilen iş hesaplayıcısı][5]

## <a name="introduction"></a><span data-ttu-id="860e4-107">Giriş</span><span class="sxs-lookup"><span data-stu-id="860e4-107">Introduction</span></span>
<span data-ttu-id="860e4-108">[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) Microsoft'un Genel dağıtılmış birden çok model veritabanıdır.</span><span class="sxs-lookup"><span data-stu-id="860e4-108">[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) is Microsoft's globally distributed multi-model database.</span></span> <span data-ttu-id="860e4-109">Azure Cosmos DB ile toorent sanal makineye sahip olmayan, yazılım dağıtma veya veritabanlarını izleyin.</span><span class="sxs-lookup"><span data-stu-id="860e4-109">With Azure Cosmos DB, you don't have toorent virtual machines, deploy software, or monitor databases.</span></span> <span data-ttu-id="860e4-110">Azure Cosmos DB işletilen ve sürekli olarak Microsoft üst mühendisleri toodeliver world sınıfı kullanılabilirliği, performansı ve veri koruma tarafından izlenir.</span><span class="sxs-lookup"><span data-stu-id="860e4-110">Azure Cosmos DB is operated and continuously monitored by Microsoft top engineers toodeliver world class availability, performance, and data protection.</span></span> <span data-ttu-id="860e4-111">Tercih ettiğiniz API'lerini kullanarak verilerinize erişebilir [DocumentDB SQL](documentdb-sql-query.md) (belge), MongoDB (belge) [Azure Table Storage](https://azure.microsoft.com/services/storage/tables/) (anahtar-değer) ve [Gremlin](https://tinkerpop.apache.org/gremlin.html) (tüm grafik) yerel olarak desteklenir.</span><span class="sxs-lookup"><span data-stu-id="860e4-111">You can access your data using APIs of your choice, as [DocumentDB SQL](documentdb-sql-query.md) (document), MongoDB (document), [Azure Table Storage](https://azure.microsoft.com/services/storage/tables/) (key-value), and [Gremlin](https://tinkerpop.apache.org/gremlin.html) (graph) are all natively supported.</span></span> <span data-ttu-id="860e4-112">Azure Cosmos DB Hello para hello istek birimi (RU) birimidir.</span><span class="sxs-lookup"><span data-stu-id="860e4-112">hello currency of Azure Cosmos DB is hello Request Unit (RU).</span></span> <span data-ttu-id="860e4-113">RUs ile tooreserve okuma/yazma kapasiteleri veya sağlama CPU, bellek ve IOPS gerekmez.</span><span class="sxs-lookup"><span data-stu-id="860e4-113">With RUs, you do not need tooreserve read/write capacities or provision CPU, Memory and IOPS.</span></span>

<span data-ttu-id="860e4-114">Azure Cosmos DB Basit okuma arasında değişen farklı işlemlerle API'lerini destekler ve grafik sorguları toocomplex yazar.</span><span class="sxs-lookup"><span data-stu-id="860e4-114">Azure Cosmos DB supports a number of APIs with different operations ranging from simple reads and writes toocomplex graph queries.</span></span> <span data-ttu-id="860e4-115">Tüm istekleri eşit olduğundan, normalleştirilmiş bir miktar atanan **istek birimleri** hello hesaplama gerekli tooserve hello isteği miktarına göre.</span><span class="sxs-lookup"><span data-stu-id="860e4-115">Since not all requests are equal, they are assigned a normalized quantity of **request units** based on hello amount of computation required tooserve hello request.</span></span> <span data-ttu-id="860e4-116">bir işlem için istek birim Hello Sayısı belirleyici ve bir yanıt üstbilgisi aracılığıyla Azure Cosmos veritabanı herhangi bir işlem tarafından kullanılan istek birimlerinin sayısı hello izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="860e4-116">hello number of request units for an operation is deterministic, and you can track hello number of request units consumed by any operation in Azure Cosmos DB via a response header.</span></span> 

<span data-ttu-id="860e4-117">tooprovide tahmin edilebilir performans, tooreserve işleme birimi 100 RU/saniye gerekir.</span><span class="sxs-lookup"><span data-stu-id="860e4-117">tooprovide predictable performance, you need tooreserve throughput in units of 100 RU/second.</span></span> 

<span data-ttu-id="860e4-118">Bu makaleyi okuduktan sonra aşağıdaki soruları mümkün tooanswer hello olması:</span><span class="sxs-lookup"><span data-stu-id="860e4-118">After reading this article, you'll be able tooanswer hello following questions:</span></span>  

* <span data-ttu-id="860e4-119">Hangi birimleri istemek ve ücretleri isteği?</span><span class="sxs-lookup"><span data-stu-id="860e4-119">What are request units and request charges?</span></span>
* <span data-ttu-id="860e4-120">Bir koleksiyon için istek birim kapasitesi nasıl belirteceğinizi?</span><span class="sxs-lookup"><span data-stu-id="860e4-120">How do I specify request unit capacity for a collection?</span></span>
* <span data-ttu-id="860e4-121">My uygulamanın istek birimi gereken nasıl tahmin?</span><span class="sxs-lookup"><span data-stu-id="860e4-121">How do I estimate my application's request unit needs?</span></span>
* <span data-ttu-id="860e4-122">Bir koleksiyon için istek birim kapasitesi aşmanız durumunda ne olur?</span><span class="sxs-lookup"><span data-stu-id="860e4-122">What happens if I exceed request unit capacity for a collection?</span></span>

<span data-ttu-id="860e4-123">Azure Cosmos DB çok model bir veritabanıdır, biz tooa koleksiyonu/belge belge API, grafik API'si için bir grafik/düğümü ve tablo API için bir tablo/varlık başvurur önemli toonote olur.</span><span class="sxs-lookup"><span data-stu-id="860e4-123">As Azure Cosmos DB is a multi-model database, it is important toonote that we will refer tooa collection/document for a document API, a graph/node for a graph API and a table/entity for table API.</span></span> <span data-ttu-id="860e4-124">Üretilen iş bu belge size kapsayıcı/öğe toohello kavramlarını generalize.</span><span class="sxs-lookup"><span data-stu-id="860e4-124">Throughput this document we will generalize toohello concepts of container/item.</span></span>

## <a name="request-units-and-request-charges"></a><span data-ttu-id="860e4-125">İstek birimleri ve istek ücretleri</span><span class="sxs-lookup"><span data-stu-id="860e4-125">Request units and request charges</span></span>
<span data-ttu-id="860e4-126">Azure Cosmos DB tarafından hızlı ve tahmin edilebilir performans sunar *ayırma* kaynakları toosatisfy uygulamanızın işleme gerekir.</span><span class="sxs-lookup"><span data-stu-id="860e4-126">Azure Cosmos DB delivers fast, predictable performance by *reserving* resources toosatisfy your application's throughput needs.</span></span>  <span data-ttu-id="860e4-127">Uygulama yüklemek ve zaman içinde desenleri değişiklik erişmek için Azure Cosmos DB tooeasily artış izin verir veya ayrılmış işleme kullanılabilir tooyour uygulama hello miktarını azaltın.</span><span class="sxs-lookup"><span data-stu-id="860e4-127">Because application load and access patterns change over time, Azure Cosmos DB allows you tooeasily increase or decrease hello amount of reserved throughput available tooyour application.</span></span>

<span data-ttu-id="860e4-128">Azure Cosmos DB ile ayrılmış işleme saniyede işlediği istek birimler cinsinden belirtilir.</span><span class="sxs-lookup"><span data-stu-id="860e4-128">With Azure Cosmos DB, reserved throughput is specified in terms of request units processing per second.</span></span> <span data-ttu-id="860e4-129">İstek birimleri yapabildiği verimlilik para birimi olarak düşünebilirsiniz, *yedek* miktardaki kullanılabilir tooyour uygulama başına saniye başına istek birimleri garanti.</span><span class="sxs-lookup"><span data-stu-id="860e4-129">You can think of request units as throughput currency, whereby you *reserve* an amount of guaranteed request units available tooyour application on per second basis.</span></span>  <span data-ttu-id="860e4-130">Azure Cosmos - bir belge yazma, bir belge güncelleştirme bir sorgu gerçekleştirme - DB her bir işlemin CPU, bellek ve IOPS tüketir.</span><span class="sxs-lookup"><span data-stu-id="860e4-130">Each operation in Azure Cosmos DB - writing a document, performing a query, updating a document - consumes CPU, memory, and IOPS.</span></span>  <span data-ttu-id="860e4-131">Diğer bir deyişle, her işlemi uygulanan bir *isteği ücret*, içinde ifade *istek birimleri*.</span><span class="sxs-lookup"><span data-stu-id="860e4-131">That is, each operation incurs a *request charge*, which is expressed in *request units*.</span></span>  <span data-ttu-id="860e4-132">İstek birimi ücretleri, uygulamanızın işleme gereksinimleri etkiler hello Etkenler anlama, toorun uygulamanızın maliyet etkili bir şekilde mümkün olduğunca sağlar.</span><span class="sxs-lookup"><span data-stu-id="860e4-132">Understanding hello factors which impact request unit charges, along with your application's throughput requirements, enables you toorun your application as cost effectively as possible.</span></span> <span data-ttu-id="860e4-133">Merhaba sorgu Gezgini de, bir sorgu harika aracı tootest hello çekirdek olur.</span><span class="sxs-lookup"><span data-stu-id="860e4-133">hello query explorer is also a wonderful tool tootest hello core of a query.</span></span>

<span data-ttu-id="860e4-134">İstek birimleri ve Azure Cosmos DB tahmin edilebilir performansla Aravind Ramachandran burada açıklanmaktadır video, aşağıdaki hello izleyerek çalışmaya başlamanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="860e4-134">We recommend getting started by watching hello following video, where Aravind Ramachandran explains request units and predictable performance with Azure Cosmos DB.</span></span>

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Predictable-Performance-with-DocumentDB/player]
> 
> 

## <a name="specifying-request-unit-capacity-in-azure-cosmos-db"></a><span data-ttu-id="860e4-135">İstek birimi kapasite Azure Cosmos DB'de belirtme</span><span class="sxs-lookup"><span data-stu-id="860e4-135">Specifying request unit capacity in Azure Cosmos DB</span></span>
<span data-ttu-id="860e4-136">Yeni koleksiyon, tablo veya grafik başlatırken hello numarası belirtin (RU saniye başına) saniyede istek birimlerinin ayrılmış istiyor.</span><span class="sxs-lookup"><span data-stu-id="860e4-136">When starting a new collection, table or graph, you specify hello number of request units per second (RU per second) you want reserved.</span></span> <span data-ttu-id="860e4-137">Hello üzerinde sağlanan işleme bağlı olarak, Azure Cosmos DB fiziksel bölümleri toohost koleksiyonunuzu ayırır ve bölmelerini/veri bölümler, büyüdükçe rebalances.</span><span class="sxs-lookup"><span data-stu-id="860e4-137">Based on hello provisioned throughput, Azure Cosmos DB allocates physical partitions toohost your collection and splits/rebalances data across partitions as it grows.</span></span>

<span data-ttu-id="860e4-138">Bir koleksiyon 2.500 istek birimleri ile sağlanan ya da daha yüksek olduğunda bir bölüm anahtarı toobe belirtilen Azure Cosmos DB gerektirir.</span><span class="sxs-lookup"><span data-stu-id="860e4-138">Azure Cosmos DB requires a partition key toobe specified when a collection is provisioned with 2,500 request units or higher.</span></span> <span data-ttu-id="860e4-139">Bölüm anahtarı da gerekli tooscale koleksiyonunuzun işleme hello gelecekteki 2.500 istek birimleri ötesinde olan.</span><span class="sxs-lookup"><span data-stu-id="860e4-139">A partition key is also required tooscale your collection's throughput beyond 2,500 request units in hello future.</span></span> <span data-ttu-id="860e4-140">Bu nedenle, tooconfigure önerilir bir [bölüm anahtarı](partition-data.md) ilk işleme bakılmaksızın bir kapsayıcı oluştururken.</span><span class="sxs-lookup"><span data-stu-id="860e4-140">Therefore, it is highly recommended tooconfigure a [partition key](partition-data.md) when creating a container regardless of your initial throughput.</span></span> <span data-ttu-id="860e4-141">Verilerinizin birden çok bölüm arasında bölme toobe olabilir olduğundan, gerekli toopick yüksek kardinalite (100 toomillions farklı değerlerin) vardır ve böylece tablo/koleksiyonu/grafik ve istekleri Azure Cosmos DB tarafından hep genişletilebilir bir bölüm anahtarı kalır.</span><span class="sxs-lookup"><span data-stu-id="860e4-141">Since your data might have toobe split across multiple partitions, it is necessary toopick a partition key that has a high cardinality (100 toomillions of distinct values) so that your collection/table/graph and requests can be scaled uniformly by Azure Cosmos DB.</span></span> 

> [!NOTE]
> <span data-ttu-id="860e4-142">Bölüm anahtarı mantıksal bir sınır ve fiziksel bir tane ' dir.</span><span class="sxs-lookup"><span data-stu-id="860e4-142">A partition key is a logical boundary, and not a physical one.</span></span> <span data-ttu-id="860e4-143">Bu nedenle, toolimit hello farklı bölüm anahtar değerlerinin sayısı gerekmez.</span><span class="sxs-lookup"><span data-stu-id="860e4-143">Therefore, you do not need toolimit hello number of distinct partition key values.</span></span> <span data-ttu-id="860e4-144">Aslında daha iyi toohave daha farklı olduğundan daha fazla yük dengeleme seçeneklerini Azure Cosmos DB olduğu gibi daha az anahtar değerden bölüm.</span><span class="sxs-lookup"><span data-stu-id="860e4-144">It is in fact better toohave more distinct partition key values than less, as Azure Cosmos DB has more load balancing options.</span></span>

<span data-ttu-id="860e4-145">3, 000'ile bir koleksiyon oluşturmak için bir kod parçacığı aşağıda verilmiştir .NET SDK kullanarak saniye başına birim hello isteği:</span><span class="sxs-lookup"><span data-stu-id="860e4-145">Here is a code snippet for creating a collection with 3,000 request units per second using hello .NET SDK:</span></span>

```csharp
DocumentCollection myCollection = new DocumentCollection();
myCollection.Id = "coll";
myCollection.PartitionKey.Paths.Add("/deviceId");

await client.CreateDocumentCollectionAsync(
    UriFactory.CreateDatabaseUri("db"),
    myCollection,
    new RequestOptions { OfferThroughput = 3000 });
```

<span data-ttu-id="860e4-146">Azure Cosmos DB akışındaki bir ayırma modeli çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="860e4-146">Azure Cosmos DB operates on a reservation model on throughput.</span></span> <span data-ttu-id="860e4-147">Diğer bir deyişle, üretilen iş hello miktarı için faturalandırılır *ayrılmış*ne olursa olsun, üretilen işi ne kadarının etkin olduğundan, *kullanılan*.</span><span class="sxs-lookup"><span data-stu-id="860e4-147">That is, you are billed for hello amount of throughput *reserved*, regardless of how much of that throughput is actively *used*.</span></span> <span data-ttu-id="860e4-148">SDK'ları ile ayrılmış RUs miktarı, kolayca ölçeklendirilebilir yukarı ve aşağı uygulamanızın yük, veri ve kullanım desenlerini değiştikçe hello veya hello kullanarak [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="860e4-148">As your application's load, data, and usage patterns change you can easily scale up and down hello amount of reserved RUs through SDKs or using hello [Azure Portal](https://portal.azure.com).</span></span>

<span data-ttu-id="860e4-149">Her koleksiyon/tablo/grafik eşlendi tooan `Offer` kaynak hello sağlanan işleme hakkındaki meta verileri olan Azure Cosmos veritabanı.</span><span class="sxs-lookup"><span data-stu-id="860e4-149">Each collection/table/graph are mapped tooan `Offer` resource in Azure Cosmos DB, which has metadata about hello provisioned throughput.</span></span> <span data-ttu-id="860e4-150">Kapsayıcı için ilgili teklif kaynak hello bakarak sonra hello yeni işleme değeri ile güncelleştirme tarafından ayrılan hello verimlilik değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="860e4-150">You can change hello allocated throughput by looking up hello corresponding offer resource for a container, then updating it with hello new throughput value.</span></span> <span data-ttu-id="860e4-151">Bir koleksiyon too5 hello verimini değiştirmek için bir kod parçacığı aşağıda verilmiştir, .NET SDK kullanarak saniye başına istek birimleri 000 hello:</span><span class="sxs-lookup"><span data-stu-id="860e4-151">Here is a code snippet for changing hello throughput of a collection too5,000 request units per second using hello .NET SDK:</span></span>

```csharp
// Fetch hello resource toobe updated
Offer offer = client.CreateOfferQuery()
                .Where(r => r.ResourceLink == collection.SelfLink)    
                .AsEnumerable()
                .SingleOrDefault();

// Set hello throughput too5000 request units per second
offer = new OfferV2(offer, 5000);

// Now persist these changes toohello database by replacing hello original resource
await client.ReplaceOfferAsync(offer);
```

<span data-ttu-id="860e4-152">Merhaba verimlilik değiştirdiğinizde, kapsayıcının etkisi toohello kullanılabilirliği yok.</span><span class="sxs-lookup"><span data-stu-id="860e4-152">There is no impact toohello availability of your container when you change hello throughput.</span></span> <span data-ttu-id="860e4-153">Genellikle hello yeni ayrılmış işleme hello yeni işleme, uygulama üzerinde saniye içinde etkili olur.</span><span class="sxs-lookup"><span data-stu-id="860e4-153">Typically hello new reserved throughput is effective within seconds on application of hello new throughput.</span></span>

## <a name="request-unit-considerations"></a><span data-ttu-id="860e4-154">İstek birimi konuları</span><span class="sxs-lookup"><span data-stu-id="860e4-154">Request unit considerations</span></span>
<span data-ttu-id="860e4-155">İstek birimleri tooreserve Azure Cosmos DB kapsayıcısı için Hello sayısını tahmin etme dikkate değişkenleri aşağıdaki önemli tootake hello olur:</span><span class="sxs-lookup"><span data-stu-id="860e4-155">When estimating hello number of request units tooreserve for your Azure Cosmos DB container, it is important tootake hello following variables into consideration:</span></span>

* <span data-ttu-id="860e4-156">**Öğe boyutunu**.</span><span class="sxs-lookup"><span data-stu-id="860e4-156">**Item size**.</span></span> <span data-ttu-id="860e4-157">Boyutu artar hello birimleri tooread tüketilen veya hello veri yazma da artacaktır.</span><span class="sxs-lookup"><span data-stu-id="860e4-157">As size increases hello units consumed tooread or write hello data will also increase.</span></span>
* <span data-ttu-id="860e4-158">**Madde özellik sayısı**.</span><span class="sxs-lookup"><span data-stu-id="860e4-158">**Item property count**.</span></span> <span data-ttu-id="860e4-159">Tüm özelliklerin, bir belge/düğümü/ntity hello özellik sayısı arttıkça artıracaktır hello tüketilen birim toowrite varsayılan dizin varsayılır.</span><span class="sxs-lookup"><span data-stu-id="860e4-159">Assuming default indexing of all properties, hello units consumed toowrite a document/node/ntity will increase as hello property count increases.</span></span>
* <span data-ttu-id="860e4-160">**Veri tutarlılığı**.</span><span class="sxs-lookup"><span data-stu-id="860e4-160">**Data consistency**.</span></span> <span data-ttu-id="860e4-161">Veri tutarlılık düzeylerini güçlü veya sınırlanmış eskime durumu kullanırken, ek birimler tüketilen tooread öğeleri olacaktır.</span><span class="sxs-lookup"><span data-stu-id="860e4-161">When using data consistency levels of Strong or Bounded Staleness, additional units will be consumed tooread items.</span></span>
* <span data-ttu-id="860e4-162">**Dizin oluşturulmuş özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="860e4-162">**Indexed properties**.</span></span> <span data-ttu-id="860e4-163">Bir dizin İlkesi her kapsayıcısı üzerinde varsayılan olarak hangi özellikleri dizinlenir belirler.</span><span class="sxs-lookup"><span data-stu-id="860e4-163">An index policy on each container determines which properties are indexed by default.</span></span> <span data-ttu-id="860e4-164">Dizinli Özellikler hello sayısını sınırlayarak veya yavaş dizin etkinleştirerek, istek birimi tüketimini azaltabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="860e4-164">You can reduce your request unit consumption by limiting hello number of indexed properties or by enabling lazy indexing.</span></span>
* <span data-ttu-id="860e4-165">**Belge dizine**.</span><span class="sxs-lookup"><span data-stu-id="860e4-165">**Document indexing**.</span></span> <span data-ttu-id="860e4-166">Bazı öğelerinizi değil tooindex seçerseniz, her bir öğeyi otomatik olarak dizine varsayılan olarak, daha az istek birimleri tüketir.</span><span class="sxs-lookup"><span data-stu-id="860e4-166">By default each item is automatically indexed, you will consume fewer request units if you choose not tooindex some of your items.</span></span>
* <span data-ttu-id="860e4-167">**Sorgu desenleri**.</span><span class="sxs-lookup"><span data-stu-id="860e4-167">**Query patterns**.</span></span> <span data-ttu-id="860e4-168">bir sorgu Hello karmaşıklığını kaç tane istek birimleri için bir işlem tüketilen etkiler.</span><span class="sxs-lookup"><span data-stu-id="860e4-168">hello complexity of a query impacts how many Request Units are consumed for an operation.</span></span> <span data-ttu-id="860e4-169">koşulları Hello sayısı, hello koşulları projeksiyonları, UDF'ler sayısı ve tüm hello maliyetini etkilemek hello kaynak veri kümesinin hello boyutu yapısını işlemleri sorgu.</span><span class="sxs-lookup"><span data-stu-id="860e4-169">hello number of predicates, nature of hello predicates, projections, number of UDFs, and hello size of hello source data set all influence hello cost of query operations.</span></span>
* <span data-ttu-id="860e4-170">**Komut dosyası kullanımı**.</span><span class="sxs-lookup"><span data-stu-id="860e4-170">**Script usage**.</span></span>  <span data-ttu-id="860e4-171">Sorguları olarak gerçekleştirilen hello işlemler hello kapsamına bağlı istek birimleri saklı yordamları ve Tetikleyicileri tüketir.</span><span class="sxs-lookup"><span data-stu-id="860e4-171">As with queries, stored procedures and triggers consume request units based on hello complexity of hello operations being performed.</span></span> <span data-ttu-id="860e4-172">Uygulamanızı geliştirirken hello isteği ücret incelemek üstbilgi toobetter anlamak her işlemi isteği birim kapasitesi nasıl tüketilmesine neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="860e4-172">As you develop your application, inspect hello request charge header toobetter understand how each operation is consuming request unit capacity.</span></span>

## <a name="estimating-throughput-needs"></a><span data-ttu-id="860e4-173">Üretilen iş gereksinimlerini tahmin etme</span><span class="sxs-lookup"><span data-stu-id="860e4-173">Estimating throughput needs</span></span>
<span data-ttu-id="860e4-174">Bir istek birimi istek maliyet işleme normalleştirilmiş ölçüsüdür.</span><span class="sxs-lookup"><span data-stu-id="860e4-174">A request unit is a normalized measure of request processing cost.</span></span> <span data-ttu-id="860e4-175">Bir tek istek birimi öğesi 10 benzersiz özellik değerlerini (Sistem özellikleri dışında) oluşan tek 1 bb hello işleme gerekli kapasite tooread (aracılığıyla kendi bağlantısını veya kimliği) temsil eder.</span><span class="sxs-lookup"><span data-stu-id="860e4-175">A single request unit represents hello processing capacity required tooread (via self link or id) a single 1KB item consisting of 10 unique property values (excluding system properties).</span></span> <span data-ttu-id="860e4-176">İstek toocreate (Ekle) değiştirmek veya aynı öğesi daha hello hizmetinden işleme tüketir hello silin ve böylece daha fazla birim isteyin.</span><span class="sxs-lookup"><span data-stu-id="860e4-176">A request toocreate (insert), replace or delete hello same item will consume more processing from hello service and thereby more request units.</span></span>   

> [!NOTE]
> <span data-ttu-id="860e4-177">1 isteği biriminin Hello temel öğesi karşılık gelen tooa basit bir 1 KB için kendi bağlantısını veya hello öğenin kimliği alın.</span><span class="sxs-lookup"><span data-stu-id="860e4-177">hello baseline of 1 request unit for a 1KB item corresponds tooa simple GET by self link or id of hello item.</span></span>
> 
> 

<span data-ttu-id="860e4-178">Örneğin, kaç tane isteği gösteren bir tablo İşte birimleri tooprovision boyutlarında üç farklı öğe (1KB, 4KB ve 64KB) ve iki farklı performans düzeyleri (500 Okuma/saniye 100 yazma/saniye ve 500 Okuma/saniye + 500 yazma/saniye).</span><span class="sxs-lookup"><span data-stu-id="860e4-178">For example, here's a table that shows how many request units tooprovision at three different item sizes (1KB, 4KB, and 64KB) and at two different performance levels (500 reads/second + 100 writes/second and 500 reads/second + 500 writes/second).</span></span> <span data-ttu-id="860e4-179">Merhaba veri tutarlılığını oturumunda yapılandırılmış ve dizin oluşturma ilkesi hello tooNone ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="860e4-179">hello data consistency was configured at Session, and hello indexing policy was set tooNone.</span></span>

<table border="0" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td valign="top"><p><span data-ttu-id="860e4-180"><strong>Öğesi boyutu</strong></span><span class="sxs-lookup"><span data-stu-id="860e4-180"><strong>Item size</strong></span></span></p></td>
            <td valign="top"><p><span data-ttu-id="860e4-181"><strong>Okuma/saniye</strong></span><span class="sxs-lookup"><span data-stu-id="860e4-181"><strong>Reads/second</strong></span></span></p></td>
            <td valign="top"><p><span data-ttu-id="860e4-182"><strong>Yazma/saniye</strong></span><span class="sxs-lookup"><span data-stu-id="860e4-182"><strong>Writes/second</strong></span></span></p></td>
            <td valign="top"><p><span data-ttu-id="860e4-183"><strong>İstek birimleri</strong></span><span class="sxs-lookup"><span data-stu-id="860e4-183"><strong>Request units</strong></span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="860e4-184">1 KB</span><span class="sxs-lookup"><span data-stu-id="860e4-184">1 KB</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="860e4-185">500</span><span class="sxs-lookup"><span data-stu-id="860e4-185">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="860e4-186">100</span><span class="sxs-lookup"><span data-stu-id="860e4-186">100</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="860e4-187">(500 * 1) + (100 * 5) = 1.000 RU/s</span><span class="sxs-lookup"><span data-stu-id="860e4-187">(500 * 1) + (100 * 5) = 1,000 RU/s</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="860e4-188">1 KB</span><span class="sxs-lookup"><span data-stu-id="860e4-188">1 KB</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="860e4-189">500</span><span class="sxs-lookup"><span data-stu-id="860e4-189">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="860e4-190">500</span><span class="sxs-lookup"><span data-stu-id="860e4-190">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="860e4-191">(500 * 1) + (500 * 5) = 3000 RU/s</span><span class="sxs-lookup"><span data-stu-id="860e4-191">(500 * 1) + (500 * 5) = 3,000 RU/s</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="860e4-192">4 KB</span><span class="sxs-lookup"><span data-stu-id="860e4-192">4 KB</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="860e4-193">500</span><span class="sxs-lookup"><span data-stu-id="860e4-193">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="860e4-194">100</span><span class="sxs-lookup"><span data-stu-id="860e4-194">100</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="860e4-195">(500 * 1,3) + (100 * 7) = 1,350 RU/s</span><span class="sxs-lookup"><span data-stu-id="860e4-195">(500 * 1.3) + (100 * 7) = 1,350 RU/s</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="860e4-196">4 KB</span><span class="sxs-lookup"><span data-stu-id="860e4-196">4 KB</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="860e4-197">500</span><span class="sxs-lookup"><span data-stu-id="860e4-197">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="860e4-198">500</span><span class="sxs-lookup"><span data-stu-id="860e4-198">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="860e4-199">(500 * 1,3) + (500 * 7) = 4,150 RU/s</span><span class="sxs-lookup"><span data-stu-id="860e4-199">(500 * 1.3) + (500 * 7) = 4,150 RU/s</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="860e4-200">64 KB</span><span class="sxs-lookup"><span data-stu-id="860e4-200">64 KB</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="860e4-201">500</span><span class="sxs-lookup"><span data-stu-id="860e4-201">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="860e4-202">100</span><span class="sxs-lookup"><span data-stu-id="860e4-202">100</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="860e4-203">(500 * 10) + (100 * 48) = 9,800 RU/s</span><span class="sxs-lookup"><span data-stu-id="860e4-203">(500 * 10) + (100 * 48) = 9,800 RU/s</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="860e4-204">64 KB</span><span class="sxs-lookup"><span data-stu-id="860e4-204">64 KB</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="860e4-205">500</span><span class="sxs-lookup"><span data-stu-id="860e4-205">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="860e4-206">500</span><span class="sxs-lookup"><span data-stu-id="860e4-206">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="860e4-207">(500 * 10) + (500 * 48) = 29,000 RU/s</span><span class="sxs-lookup"><span data-stu-id="860e4-207">(500 * 10) + (500 * 48) = 29,000 RU/s</span></span></p></td>
        </tr>
    </tbody>
</table>

### <a name="use-hello-request-unit-calculator"></a><span data-ttu-id="860e4-208">Merhaba istek birimi hesaplayıcı kullanın</span><span class="sxs-lookup"><span data-stu-id="860e4-208">Use hello request unit calculator</span></span>
<span data-ttu-id="860e4-209">İnce toohelp müşteriler kendi verimlilik tahminler ince ayar, bir web tabanlı [istek birimi hesaplayıcı](https://www.documentdb.com/capacityplanner) toohelp tahmin hello isteği birim gereksinimleri dahil olmak üzere, normal işlemleri için:</span><span class="sxs-lookup"><span data-stu-id="860e4-209">toohelp customers fine tune their throughput estimations, there is a web based [request unit calculator](https://www.documentdb.com/capacityplanner) toohelp estimate hello request unit requirements for typical operations, including:</span></span>

* <span data-ttu-id="860e4-210">(Yazar) öğesi oluşturur</span><span class="sxs-lookup"><span data-stu-id="860e4-210">Item creates (writes)</span></span>
* <span data-ttu-id="860e4-211">Öğe okur</span><span class="sxs-lookup"><span data-stu-id="860e4-211">Item reads</span></span>
* <span data-ttu-id="860e4-212">Öğeyi siler</span><span class="sxs-lookup"><span data-stu-id="860e4-212">Item deletes</span></span>
* <span data-ttu-id="860e4-213">Öğesi güncelleştirmeleri</span><span class="sxs-lookup"><span data-stu-id="860e4-213">Item updates</span></span>

<span data-ttu-id="860e4-214">Merhaba aracı sağladığınız hello örnek öğeleri temel alan veri depolama gereksinimlerini tahmin etmek için destek de içerir.</span><span class="sxs-lookup"><span data-stu-id="860e4-214">hello tool also includes support for estimating data storage needs based on hello sample items you provide.</span></span>

<span data-ttu-id="860e4-215">Merhaba aracını kullanarak basit bir işlemdir:</span><span class="sxs-lookup"><span data-stu-id="860e4-215">Using hello tool is simple:</span></span>

1. <span data-ttu-id="860e4-216">Bir veya daha fazla temsilcisi öğeleri karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="860e4-216">Upload one or more representative items.</span></span>
   
    ![Öğeleri toohello istek birimi hesaplayıcı karşıya yükle][2]
2. <span data-ttu-id="860e4-218">tooestimate veri depolama gereksinimleri hello toplam sayısını girin öğelerinin toostore bekler.</span><span class="sxs-lookup"><span data-stu-id="860e4-218">tooestimate data storage requirements, enter hello total number of items you expect toostore.</span></span>
3. <span data-ttu-id="860e4-219">Girin hello öğe sayısı oluşturma, okuma, güncelleştirme ve silme işlemleri (bir saniye başına temelinde) gerektirir.</span><span class="sxs-lookup"><span data-stu-id="860e4-219">Enter hello number of items create, read, update, and delete operations you require (on a per-second basis).</span></span> <span data-ttu-id="860e4-220">tooestimate hello istek birimi ücretleri öğesi güncelleştirme işlemlerinin tipik alan güncelleştirmeleri içeren yukarıdaki adım 1'den hello örnek öğenin bir kopyasını yükleyin.</span><span class="sxs-lookup"><span data-stu-id="860e4-220">tooestimate hello request unit charges of item update operations, upload a copy of hello sample item from step 1 above that includes typical field updates.</span></span>  <span data-ttu-id="860e4-221">Örneğin, öğesi güncelleştirmeler genellikle lastLogin ve userVisits adlı iki özellikleri değiştirin ve ardından sadece hello örnek öğesi kopyalayın, bu iki özellik için hello değerleri güncelleştirmek ve kopyalanan hello öğesi yükleyin.</span><span class="sxs-lookup"><span data-stu-id="860e4-221">For example, if item updates typically modify two properties named lastLogin and userVisits, then simply copy hello sample item, update hello values for those two properties, and upload hello copied item.</span></span>
   
    ![Üretilen iş gereksinimleri hello istek birimi hesaplayıcı girin][3]
4. <span data-ttu-id="860e4-223">Tıklatın hesaplamak ve hello sonuçlarını inceleyin.</span><span class="sxs-lookup"><span data-stu-id="860e4-223">Click calculate and examine hello results.</span></span>
   
    ![Birim hesaplayıcı sonuçları isteği][4]

> [!NOTE]
> <span data-ttu-id="860e4-225">Dizinli Özellikler boyutu ve hello sayısı bakımından önemli ölçüde farklılık gösterecektir öğesi türleri varsa, her bir örnek karşıya *türü* tipik öğesi toohello, hello sonuçları hesaplamak ve aracı.</span><span class="sxs-lookup"><span data-stu-id="860e4-225">If you have item types which will differ dramatically in terms of size and hello number of indexed properties, then upload a sample of each *type* of typical item toohello tool and then calculate hello results.</span></span>
> 
> 

### <a name="use-hello-azure-cosmos-db-request-charge-response-header"></a><span data-ttu-id="860e4-226">Hello Azure Cosmos DB istek ücret yanıt üstbilgisi kullanın</span><span class="sxs-lookup"><span data-stu-id="860e4-226">Use hello Azure Cosmos DB request charge response header</span></span>
<span data-ttu-id="860e4-227">Bir özel üst bilgi hello Azure Cosmos DB hizmet gelen her yanıtı içerir (`x-ms-request-charge`) hello istek için harcanan hello istek birimleri içerir.</span><span class="sxs-lookup"><span data-stu-id="860e4-227">Every response from hello Azure Cosmos DB service includes a custom header (`x-ms-request-charge`) that contains hello request units consumed for hello request.</span></span> <span data-ttu-id="860e4-228">Bu üst ayrıca Azure Cosmos DB SDK'ları hello erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="860e4-228">This header is also accessible through hello Azure Cosmos DB SDKs.</span></span> <span data-ttu-id="860e4-229">Hello .NET SDK'sı, RequestCharge hello ResourceResponse nesnesinin bir özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="860e4-229">In hello .NET SDK, RequestCharge is a property of hello ResourceResponse object.</span></span>  <span data-ttu-id="860e4-230">Sorgular için hello Azure portalında Azure Cosmos DB sorgu Gezgini hello yürütülen sorgular için istek ücret bilgileri sağlar.</span><span class="sxs-lookup"><span data-stu-id="860e4-230">For queries, hello Azure Cosmos DB Query Explorer in hello Azure portal provides request charge information for executed queries.</span></span>

![Merhaba sorgu Gezgini RU ücretlere inceleniyor][1]

<span data-ttu-id="860e4-232">Bu aklınızda uygulamanızın gerektirdiği ayrılmış işleme hello miktarı tahmin etmek için bir yöntem toorecord hello istek birimi ücret uygulamanız tarafından kullanılan bir temsili öğesi karşı normal işlemleri çalıştırılması ile ilişkili olan ve ardından işlem Hello sayısını tahmin etme saniyede gerçekleştirme beklenir.</span><span class="sxs-lookup"><span data-stu-id="860e4-232">With this in mind, one method for estimating hello amount of reserved throughput required by your application is toorecord hello request unit charge associated with running typical operations against a representative item used by your application and then estimating hello number of operations you anticipate performing each second.</span></span>  <span data-ttu-id="860e4-233">Emin toomeasure olması ve tipik sorgular ve Azure Cosmos DB komut dosyası kullanımı da içerir.</span><span class="sxs-lookup"><span data-stu-id="860e4-233">Be sure toomeasure and include typical queries and Azure Cosmos DB script usage as well.</span></span>

> [!NOTE]
> <span data-ttu-id="860e4-234">Dizinli Özellikler boyutu ve hello sayısı bakımından önemli ölçüde farklılık gösterecektir öğesi türleri varsa, her ilişkilendirilmiş hello geçerli işlemi istek birimi ücret kayıt *türü* tipik öğesi.</span><span class="sxs-lookup"><span data-stu-id="860e4-234">If you have item types which will differ dramatically in terms of size and hello number of indexed properties, then record hello applicable operation request unit charge associated with each *type* of typical item.</span></span>
> 
> 

<span data-ttu-id="860e4-235">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="860e4-235">For example:</span></span>

1. <span data-ttu-id="860e4-236">Kayıt (ekleme) oluşturma hello istek birimi ücret tipik bir öğe.</span><span class="sxs-lookup"><span data-stu-id="860e4-236">Record hello request unit charge of creating (inserting) a typical item.</span></span> 
2. <span data-ttu-id="860e4-237">Tipik bir öğe okuma kayıt hello istek birimi gider.</span><span class="sxs-lookup"><span data-stu-id="860e4-237">Record hello request unit charge of reading a typical item.</span></span>
3. <span data-ttu-id="860e4-238">Tipik bir öğesi güncelleştirme kayıt hello istek birimi gider.</span><span class="sxs-lookup"><span data-stu-id="860e4-238">Record hello request unit charge of updating a typical item.</span></span>
4. <span data-ttu-id="860e4-239">Kayıt hello istek birimi gider tipik, ortak öğesi sorgular.</span><span class="sxs-lookup"><span data-stu-id="860e4-239">Record hello request unit charge of typical, common item queries.</span></span>
5. <span data-ttu-id="860e4-240">Tüm özel komut dosyalarını (saklı yordamlar, Tetikleyiciler, kullanıcı tanımlı işlevler), kayıt hello istek birimi ücret Hello uygulama tarafından kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="860e4-240">Record hello request unit charge of any custom scripts (stored procedures, triggers, user-defined functions) leveraged by hello application</span></span>
6. <span data-ttu-id="860e4-241">Tahmini hello işlemlerinin sayısı verilen birimleri saniyede toorun düşündüğünüz hello gerekli isteği hesaplayın.</span><span class="sxs-lookup"><span data-stu-id="860e4-241">Calculate hello required request units given hello estimated number of operations you anticipate toorun each second.</span></span>

### <span data-ttu-id="860e4-242"><a id="GetLastRequestStatistics"></a>API MongoDB'ın GetLastRequestStatistics komutu için kullanın</span><span class="sxs-lookup"><span data-stu-id="860e4-242"><a id="GetLastRequestStatistics"></a>Use API for MongoDB's GetLastRequestStatistics command</span></span>
<span data-ttu-id="860e4-243">API MongoDB için özel bir komut destekler *getLastRequestStatistics*, belirtilen işlemleri için hello isteği ücret alma.</span><span class="sxs-lookup"><span data-stu-id="860e4-243">API for MongoDB supports a custom command, *getLastRequestStatistics*, for retrieving hello request charge for specified operations.</span></span>

<span data-ttu-id="860e4-244">Örneğin, hello Mongo kabuğunu, tooverify hello isteği Ücret için istediğiniz hello işlemi yürütün.</span><span class="sxs-lookup"><span data-stu-id="860e4-244">For example, in hello Mongo Shell, execute hello operation you want tooverify hello request charge for.</span></span>
```
> db.sample.find()
```

<span data-ttu-id="860e4-245">Ardından, hello bağlamını *getLastRequestStatistics*.</span><span class="sxs-lookup"><span data-stu-id="860e4-245">Next, execute hello command *getLastRequestStatistics*.</span></span>
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

<span data-ttu-id="860e4-246">Bu aklınızda uygulamanızın gerektirdiği ayrılmış işleme hello miktarı tahmin etmek için bir yöntem toorecord hello istek birimi ücret uygulamanız tarafından kullanılan bir temsili öğesi karşı normal işlemleri çalıştırılması ile ilişkili olan ve ardından işlem Hello sayısını tahmin etme saniyede gerçekleştirme beklenir.</span><span class="sxs-lookup"><span data-stu-id="860e4-246">With this in mind, one method for estimating hello amount of reserved throughput required by your application is toorecord hello request unit charge associated with running typical operations against a representative item used by your application and then estimating hello number of operations you anticipate performing each second.</span></span>

> [!NOTE]
> <span data-ttu-id="860e4-247">Dizinli Özellikler boyutu ve hello sayısı bakımından önemli ölçüde farklılık gösterecektir öğesi türleri varsa, her ilişkilendirilmiş hello geçerli işlemi istek birimi ücret kayıt *türü* tipik öğesi.</span><span class="sxs-lookup"><span data-stu-id="860e4-247">If you have item types which will differ dramatically in terms of size and hello number of indexed properties, then record hello applicable operation request unit charge associated with each *type* of typical item.</span></span>
> 
> 

## <a name="use-api-for-mongodbs-portal-metrics"></a><span data-ttu-id="860e4-248">API MongoDB'ın portal ölçümleri kullanın</span><span class="sxs-lookup"><span data-stu-id="860e4-248">Use API for MongoDB's portal metrics</span></span>
<span data-ttu-id="860e4-249">İstek birimi iyi tahmini ücretlendirilen API'nize MongoDB veritabanı toouse hello için en basit yolu tooget hello [Azure portal](https://portal.azure.com) ölçümleri.</span><span class="sxs-lookup"><span data-stu-id="860e4-249">hello simplest way tooget a good estimation of request unit charges for your API for MongoDB database is toouse hello [Azure portal](https://portal.azure.com) metrics.</span></span> <span data-ttu-id="860e4-250">Merhaba ile *istek sayısı* ve *isteği ücret* grafikler, alabilirsiniz her işlem kaç tane istek birimlerinin tahmin harcayan ve kaç tane istek birimleri göreli tooone tüketen başka bir.</span><span class="sxs-lookup"><span data-stu-id="860e4-250">With hello *Number of requests* and *Request Charge* charts, you can get an estimation of how many request units each operation is consuming and how many request units they consume relative tooone another.</span></span>

![API MongoDB portal ölçümleri için][6]

## <a name="a-request-unit-estimation-example"></a><span data-ttu-id="860e4-252">Bir istek birimi tahmin örneği</span><span class="sxs-lookup"><span data-stu-id="860e4-252">A request unit estimation example</span></span>
<span data-ttu-id="860e4-253">~ 1 KB belge aşağıdaki hello göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="860e4-253">Consider hello following ~1KB document:</span></span>

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
> <span data-ttu-id="860e4-254">Hello sistem yukarıdaki hello belgenin boyutu 1 KB biraz değerinden hesaplanır şekilde belgeler Azure Cosmos DB'de küçültülmüş.</span><span class="sxs-lookup"><span data-stu-id="860e4-254">Documents are minified in Azure Cosmos DB, so hello system calculated size of hello document above is slightly less than 1KB.</span></span>
> 
> 

<span data-ttu-id="860e4-255">Merhaba aşağıdaki tabloda yaklaşık istek birimi ücretleri bu öğeyi genel işlemler için gösterilir (Merhaba yaklaşık istek birimi ücret varsayar hello hesap tutarlılık düzeyi çok ayarlanır "Oturum" ve tüm öğeler otomatik olarak dizine):</span><span class="sxs-lookup"><span data-stu-id="860e4-255">hello following table shows approximate request unit charges for typical operations on this item (hello approximate request unit charge assumes that hello account consistency level is set too“Session” and that all items are automatically indexed):</span></span>

| <span data-ttu-id="860e4-256">İşlem</span><span class="sxs-lookup"><span data-stu-id="860e4-256">Operation</span></span> | <span data-ttu-id="860e4-257">İstek birimi ücret</span><span class="sxs-lookup"><span data-stu-id="860e4-257">Request Unit Charge</span></span> |
| --- | --- |
| <span data-ttu-id="860e4-258">Öğesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="860e4-258">Create item</span></span> |<span data-ttu-id="860e4-259">~ 15 RU</span><span class="sxs-lookup"><span data-stu-id="860e4-259">~15 RU</span></span> |
| <span data-ttu-id="860e4-260">Öğe Okuma</span><span class="sxs-lookup"><span data-stu-id="860e4-260">Read item</span></span> |<span data-ttu-id="860e4-261">~ 1 RU</span><span class="sxs-lookup"><span data-stu-id="860e4-261">~1 RU</span></span> |
| <span data-ttu-id="860e4-262">Sorgu öğesi kimliği</span><span class="sxs-lookup"><span data-stu-id="860e4-262">Query item by id</span></span> |<span data-ttu-id="860e4-263">~2.5 RU</span><span class="sxs-lookup"><span data-stu-id="860e4-263">~2.5 RU</span></span> |

<span data-ttu-id="860e4-264">Ayrıca, bu tabloda yaklaşık istek birimi ücretleri hello uygulamada kullanılan tipik sorguları için gösterilir:</span><span class="sxs-lookup"><span data-stu-id="860e4-264">Additionally, this table shows approximate request unit charges for typical queries used in hello application:</span></span>

| <span data-ttu-id="860e4-265">Sorgu</span><span class="sxs-lookup"><span data-stu-id="860e4-265">Query</span></span> | <span data-ttu-id="860e4-266">İstek birimi ücret</span><span class="sxs-lookup"><span data-stu-id="860e4-266">Request Unit Charge</span></span> | <span data-ttu-id="860e4-267">Döndürülen öğe sayısı</span><span class="sxs-lookup"><span data-stu-id="860e4-267"># of Returned Items</span></span> |
| --- | --- | --- |
| <span data-ttu-id="860e4-268">Kimliğe göre yemek seçin</span><span class="sxs-lookup"><span data-stu-id="860e4-268">Select food by id</span></span> |<span data-ttu-id="860e4-269">~2.5 RU</span><span class="sxs-lookup"><span data-stu-id="860e4-269">~2.5 RU</span></span> |<span data-ttu-id="860e4-270">1</span><span class="sxs-lookup"><span data-stu-id="860e4-270">1</span></span> |
| <span data-ttu-id="860e4-271">Üretici tarafından foods seçin</span><span class="sxs-lookup"><span data-stu-id="860e4-271">Select foods by manufacturer</span></span> |<span data-ttu-id="860e4-272">~ 7 RU</span><span class="sxs-lookup"><span data-stu-id="860e4-272">~7 RU</span></span> |<span data-ttu-id="860e4-273">7</span><span class="sxs-lookup"><span data-stu-id="860e4-273">7</span></span> |
| <span data-ttu-id="860e4-274">Yemek grup ve sipariş ağırlığa göre seçin</span><span class="sxs-lookup"><span data-stu-id="860e4-274">Select by food group and order by weight</span></span> |<span data-ttu-id="860e4-275">~ 70 RU</span><span class="sxs-lookup"><span data-stu-id="860e4-275">~70 RU</span></span> |<span data-ttu-id="860e4-276">100</span><span class="sxs-lookup"><span data-stu-id="860e4-276">100</span></span> |
| <span data-ttu-id="860e4-277">Üst 10 foods yemek grubunda seçin</span><span class="sxs-lookup"><span data-stu-id="860e4-277">Select top 10 foods in a food group</span></span> |<span data-ttu-id="860e4-278">~ 10 RU</span><span class="sxs-lookup"><span data-stu-id="860e4-278">~10 RU</span></span> |<span data-ttu-id="860e4-279">10</span><span class="sxs-lookup"><span data-stu-id="860e4-279">10</span></span> |

> [!NOTE]
> <span data-ttu-id="860e4-280">RU ücretleri hello döndürülen öğe sayısını göre farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="860e4-280">RU charges vary based on hello number of items returned.</span></span>
> 
> 

<span data-ttu-id="860e4-281">Bu bilgi ile biz hello RU gereksinimleri işlemler ve saniye başına bekliyoruz sorgular, bu verilen uygulama hello sayısını tahmin edebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="860e4-281">With this information, we can estimate hello RU requirements for this application given hello number of operations and queries we expect per second:</span></span>

| <span data-ttu-id="860e4-282">İşlem/sorgu</span><span class="sxs-lookup"><span data-stu-id="860e4-282">Operation/Query</span></span> | <span data-ttu-id="860e4-283">Saniye başına tahmini sayısı</span><span class="sxs-lookup"><span data-stu-id="860e4-283">Estimated number per second</span></span> | <span data-ttu-id="860e4-284">Gerekli RUs</span><span class="sxs-lookup"><span data-stu-id="860e4-284">Required RUs</span></span> |
| --- | --- | --- |
| <span data-ttu-id="860e4-285">Öğesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="860e4-285">Create item</span></span> |<span data-ttu-id="860e4-286">10</span><span class="sxs-lookup"><span data-stu-id="860e4-286">10</span></span> |<span data-ttu-id="860e4-287">150</span><span class="sxs-lookup"><span data-stu-id="860e4-287">150</span></span> |
| <span data-ttu-id="860e4-288">Öğe Okuma</span><span class="sxs-lookup"><span data-stu-id="860e4-288">Read item</span></span> |<span data-ttu-id="860e4-289">100</span><span class="sxs-lookup"><span data-stu-id="860e4-289">100</span></span> |<span data-ttu-id="860e4-290">100</span><span class="sxs-lookup"><span data-stu-id="860e4-290">100</span></span> |
| <span data-ttu-id="860e4-291">Üretici tarafından foods seçin</span><span class="sxs-lookup"><span data-stu-id="860e4-291">Select foods by manufacturer</span></span> |<span data-ttu-id="860e4-292">25</span><span class="sxs-lookup"><span data-stu-id="860e4-292">25</span></span> |<span data-ttu-id="860e4-293">175</span><span class="sxs-lookup"><span data-stu-id="860e4-293">175</span></span> |
| <span data-ttu-id="860e4-294">Yemek gruplandırma ölçütü seçin</span><span class="sxs-lookup"><span data-stu-id="860e4-294">Select by food group</span></span> |<span data-ttu-id="860e4-295">10</span><span class="sxs-lookup"><span data-stu-id="860e4-295">10</span></span> |<span data-ttu-id="860e4-296">700</span><span class="sxs-lookup"><span data-stu-id="860e4-296">700</span></span> |
| <span data-ttu-id="860e4-297">İlk 10 seçin</span><span class="sxs-lookup"><span data-stu-id="860e4-297">Select top 10</span></span> |<span data-ttu-id="860e4-298">15</span><span class="sxs-lookup"><span data-stu-id="860e4-298">15</span></span> |<span data-ttu-id="860e4-299">150 toplam</span><span class="sxs-lookup"><span data-stu-id="860e4-299">150 Total</span></span> |

<span data-ttu-id="860e4-300">Bu durumda, bir ortalama verimi gereksinimi 1,275 RU/s bekliyoruz.</span><span class="sxs-lookup"><span data-stu-id="860e4-300">In this case, we expect an average throughput requirement of 1,275 RU/s.</span></span>  <span data-ttu-id="860e4-301">100 en yakın toohello Yukarı yuvarlama, biz 1300 RU/s Bu uygulamanın koleksiyon için hazırlamanız.</span><span class="sxs-lookup"><span data-stu-id="860e4-301">Rounding up toohello nearest 100, we would provision 1,300 RU/s for this application's collection.</span></span>

## <span data-ttu-id="860e4-302"><a id="RequestRateTooLarge"></a>Azure Cosmos DB aşan ayrılmış işleme sınırları</span><span class="sxs-lookup"><span data-stu-id="860e4-302"><a id="RequestRateTooLarge"></a> Exceeding reserved throughput limits in Azure Cosmos DB</span></span>
<span data-ttu-id="860e4-303">İstek birimi tüketim Hello bütçe boşsa, saniye başına oranı olarak değerlendirilir, geri çağırma.</span><span class="sxs-lookup"><span data-stu-id="860e4-303">Recall that request unit consumption is evaluated as a rate per second if hello budget is empty.</span></span> <span data-ttu-id="860e4-304">Hello aşan uygulamalar için bir kapsayıcı için sağlanan istek birimi hızı istekleri hello oranı ayrılmış hello düzeyin altına düşene kadar toothat koleksiyonu kısıtlanacak.</span><span class="sxs-lookup"><span data-stu-id="860e4-304">For applications that exceed hello provisioned request unit rate for a container, requests toothat collection will be throttled until hello rate drops below hello reserved level.</span></span> <span data-ttu-id="860e4-305">Bir kısıtlama oluştuğunda hello sunucu erken önlem hello istekle RequestRateTooLargeException (HTTP durum kodu 429) ve kullanıcı hello milisaniye cinsinden süre hello miktarını önce beklemesi gereken x-ms-yeniden deneme-sonra-ms üstbilgi dönüş hello belirten sona erer reattempting hello isteği.</span><span class="sxs-lookup"><span data-stu-id="860e4-305">When a throttle occurs, hello server will preemptively end hello request with RequestRateTooLargeException (HTTP status code 429) and return hello x-ms-retry-after-ms header indicating hello amount of time, in milliseconds, that hello user must wait before reattempting hello request.</span></span>

    HTTP Status 429
    Status Line: RequestRateTooLarge
    x-ms-retry-after-ms :100

<span data-ttu-id="860e4-306">Merhaba .NET İstemci SDK'sını ve LINQ sorgularını sonra hiçbir zaman gereken bu özel durumla toodeal hello geçerli sürümü hello .NET İstemci SDK'sı, bu yanıt örtük olarak yakalar gibi hello zamanı çoğu kullanıyorsanız, sunucu tarafından belirtilen yeniden deneme sonrasında, üst gizliliğinize hello ve yeniden deneme hello isteği.</span><span class="sxs-lookup"><span data-stu-id="860e4-306">If you are using hello .NET Client SDK and LINQ queries, then most of hello time you never have toodeal with this exception, as hello current version of hello .NET Client SDK implicitly catches this response, respects hello server-specified retry-after header, and retries hello request.</span></span> <span data-ttu-id="860e4-307">Hesabınızı eşzamanlı olarak birden çok istemci tarafından erişilen sürece hello sonraki yeniden deneme işlemi başarılı olur.</span><span class="sxs-lookup"><span data-stu-id="860e4-307">Unless your account is being accessed concurrently by multiple clients, hello next retry will succeed.</span></span>

<span data-ttu-id="860e4-308">Merhaba istek hızı işletim üst üste birden fazla istemciniz varsa hello varsayılan yeniden deneme davranışı değil yeterli ve hello istemci durum kodu 429 toohello uygulama ile bir DocumentClientException atar.</span><span class="sxs-lookup"><span data-stu-id="860e4-308">If you have more than one client cumulatively operating above hello request rate, hello default retry behavior may not suffice, and hello client will throw a DocumentClientException with status code 429 toohello application.</span></span> <span data-ttu-id="860e4-309">Bu gibi durumlarda, yeniden deneme davranışı ve yordamları işleme veya hello kapsayıcısı için hello ayrılmış verim artar, uygulamanızın hata mantığının işleme düşünebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="860e4-309">In cases such as this, you may consider handling retry behavior and logic in your application's error handling routines or increasing hello reserved throughput for hello container.</span></span>

## <span data-ttu-id="860e4-310"><a id="RequestRateTooLargeAPIforMongoDB"></a>API MongoDB için aşan ayrılmış işleme sınırları</span><span class="sxs-lookup"><span data-stu-id="860e4-310"><a id="RequestRateTooLargeAPIforMongoDB"></a> Exceeding reserved throughput limits in API for MongoDB</span></span>
<span data-ttu-id="860e4-311">Merhaba oranı ayrılmış hello düzeyin altına düşene kadar bir koleksiyon için sağlanan hello istek birimleri aşan uygulamaları kısıtlanacak.</span><span class="sxs-lookup"><span data-stu-id="860e4-311">Applications that exceed hello provisioned request units for a collection will be throttled until hello rate drops below hello reserved level.</span></span> <span data-ttu-id="860e4-312">Bir azaltma oluştuğunda hello arka uç hello istekle erken önlem sona erer bir *16500* hata kodu - *çok fazla istek*.</span><span class="sxs-lookup"><span data-stu-id="860e4-312">When a throttle occurs, hello backend will preemptively end hello request with a *16500* error code - *Too Many Requests*.</span></span> <span data-ttu-id="860e4-313">Varsayılan olarak, API MongoDB için otomatik olarak dönmeden önce too10 kez yukarı yeniden deneyecek bir *çok fazla istek* hata kodu.</span><span class="sxs-lookup"><span data-stu-id="860e4-313">By default, API for MongoDB will automatically retry up too10 times before returning a *Too Many Requests* error code.</span></span> <span data-ttu-id="860e4-314">Birçok alıyorsanız *çok fazla istek* hata kodları, uygulamanızın hata yordamları işlemedeki ekleme ya da yeniden deneme davranışı dikkate veya [hello ayrılmış işleme hello koleksiyonuartırma](set-throughput.md).</span><span class="sxs-lookup"><span data-stu-id="860e4-314">If you are receiving many *Too Many Requests* error codes, you may consider either adding retry behavior in your application's error handling routines or [increasing hello reserved throughput for hello collection](set-throughput.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="860e4-315">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="860e4-315">Next steps</span></span>
<span data-ttu-id="860e4-316">ayrılmış işleme ile Azure Cosmos DB veritabanları hakkında daha fazla toolearn bu kaynakları araştırın:</span><span class="sxs-lookup"><span data-stu-id="860e4-316">toolearn more about reserved throughput with Azure Cosmos DB databases, explore these resources:</span></span>

* [<span data-ttu-id="860e4-317">Cosmos DB Azure fiyatlandırması</span><span class="sxs-lookup"><span data-stu-id="860e4-317">Azure Cosmos DB pricing</span></span>](https://azure.microsoft.com/pricing/details/cosmos-db/)
* [<span data-ttu-id="860e4-318">Azure Cosmos veritabanı veri bölümlendirme</span><span class="sxs-lookup"><span data-stu-id="860e4-318">Partitioning data in Azure Cosmos DB</span></span>](partition-data.md)

<span data-ttu-id="860e4-319">toolearn Azure Cosmos DB hakkında daha fazla bilgi görmek hello Azure Cosmos DB [belgelerine](https://azure.microsoft.com/documentation/services/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="860e4-319">toolearn more about Azure Cosmos DB, see hello Azure Cosmos DB [documentation](https://azure.microsoft.com/documentation/services/cosmos-db/).</span></span> 

<span data-ttu-id="860e4-320">Ölçek ve performans testi Azure Cosmos DB ile kullanmaya tooget bkz [performans ve ölçek testi Azure Cosmos DB ile](performance-testing.md).</span><span class="sxs-lookup"><span data-stu-id="860e4-320">tooget started with scale and performance testing with Azure Cosmos DB, see [Performance and Scale Testing with Azure Cosmos DB](performance-testing.md).</span></span>

[1]: ./media/request-units/queryexplorer.png 
[2]: ./media/request-units/RUEstimatorUpload.png
[3]: ./media/request-units/RUEstimatorDocuments.png
[4]: ./media/request-units/RUEstimatorResults.png
[5]: ./media/request-units/RUCalculator2.png
[6]: ./media/request-units/api-for-mongodb-metrics.png
