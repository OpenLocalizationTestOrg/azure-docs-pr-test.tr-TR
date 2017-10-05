---
title: "Bölümlendirme ve yatay Azure Cosmos DB'de ölçekleme | Microsoft Docs"
description: "Azure Cosmos DB, bölümleme yapılandırmak ve anahtarları bölümlemek nasıl ve uygulamanız için doğru bölüm anahtarı almak nasıl bölümleme nasıl çalıştığı hakkında bilgi edinin."
services: cosmos-db
author: arramac
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: cac9a8cd-b5a3-4827-8505-d40bb61b2416
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: arramac
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e2d2847276e553d7511241ff323c3e00aad8e5c9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-partition-and-scale-in-azure-cosmos-db"></a><span data-ttu-id="92c01-103">Bölüm ve ölçek Azure Cosmos veritabanı</span><span class="sxs-lookup"><span data-stu-id="92c01-103">How to partition and scale in Azure Cosmos DB</span></span>

<span data-ttu-id="92c01-104">[Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) büyüdüğü gibi hızlı ve tahmin edilebilir performansı ve ölçeği sorunsuz bir şekilde uygulamanızı yanı sıra ulaşmak yardımcı olmak için tasarlanmış bir genel dağıtılmış, birden çok model veritabanı hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="92c01-104">[Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) is a global distributed, multi-model database service designed to help you achieve fast, predictable performance and scale seamlessly along with your application as it grows.</span></span> <span data-ttu-id="92c01-105">Bu makalede Azure Cosmos veritabanı tüm veri modelleri için nasıl bölümleme çalışır genel bir bakış sağlar ve Azure Cosmos DB kapsayıcıları, uygulamalarınızı etkili bir şekilde ölçeklendirmek için nasıl yapılandırılacağını anlatır.</span><span class="sxs-lookup"><span data-stu-id="92c01-105">This article provides an overview of how partitioning works for all the data models in Azure Cosmos DB, and describes how you can configure Azure Cosmos DB containers to effectively scale your applications.</span></span>

<span data-ttu-id="92c01-106">Ayrıca bölümleme ve bölüm anahtarlarını bu Azure Cuma Scott Hanselman ve Azure Cosmos DB sorumlu mühendislik Yöneticisi, Shireesh Thota ile video ele alınmıştır.</span><span class="sxs-lookup"><span data-stu-id="92c01-106">Partitioning and partition keys are also covered in this Azure Friday video with Scott Hanselman and Azure Cosmos DB Principal Engineering Manager, Shireesh Thota.</span></span>

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Azure-DocumentDB-Elastic-Scale-Partitioning/player]
> 

## <a name="partitioning-in-azure-cosmos-db"></a><span data-ttu-id="92c01-107">Azure Cosmos DB bölümlendirme</span><span class="sxs-lookup"><span data-stu-id="92c01-107">Partitioning in Azure Cosmos DB</span></span>
<span data-ttu-id="92c01-108">Azure Cosmos DB'de depolamak ve herhangi bir ölçekte milisaniyelik sipariş yanıt süreleri ile şema daha az veri sorgulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="92c01-108">In Azure Cosmos DB, you can store and query schema-less data with order-of-millisecond response times at any scale.</span></span> <span data-ttu-id="92c01-109">Cosmos DB veri depolama adı verilen kapsayıcıları sağlar **(belge için) koleksiyonlar, grafikleri veya tabloları**.</span><span class="sxs-lookup"><span data-stu-id="92c01-109">Cosmos DB provides containers for storing data called **collections (for document), graphs, or tables**.</span></span> <span data-ttu-id="92c01-110">Kapsayıcıları mantıksal kaynaklar ve bir veya daha fazla fiziksel bölümleri veya sunucuları yayılabilir.</span><span class="sxs-lookup"><span data-stu-id="92c01-110">Containers are logical resources and can span one or more physical partitions or servers.</span></span> <span data-ttu-id="92c01-111">Bölüm sayısı Cosmos depolama boyutu ve kapsayıcının sağlanan işleme dayalı DB tarafından belirlenir.</span><span class="sxs-lookup"><span data-stu-id="92c01-111">The number of partitions is determined by Cosmos DB based on the storage size and the provisioned throughput of the container.</span></span> <span data-ttu-id="92c01-112">Cosmos DB her bölümün SSD yedekli depolama ilişkili sabit bir tutar sahiptir ve yüksek kullanılabilirlik için çoğaltılır.</span><span class="sxs-lookup"><span data-stu-id="92c01-112">Every partition in Cosmos DB has a fixed amount of SSD-backed storage associated with it, and is replicated for high availability.</span></span> <span data-ttu-id="92c01-113">Bölüm yönetimi tam olarak Azure Cosmos DB tarafından yönetilen ve karmaşık kodlar yazmak veya bölüm yönetmek zorunda kalmazsınız.</span><span class="sxs-lookup"><span data-stu-id="92c01-113">Partition management is fully managed by Azure Cosmos DB, and you do not have to write complex code or manage your partitions.</span></span> <span data-ttu-id="92c01-114">Cosmos DB depolama ve işleme açısından sınırsız kapsayıcılardır.</span><span class="sxs-lookup"><span data-stu-id="92c01-114">Cosmos DB containers are unlimited in terms of storage and throughput.</span></span> 

![Yatay](./media/introduction/azure-cosmos-db-partitioning.png) 

<span data-ttu-id="92c01-116">Bölümlendirme, uygulamanız için saydamdır.</span><span class="sxs-lookup"><span data-stu-id="92c01-116">Partitioning is transparent to your application.</span></span> <span data-ttu-id="92c01-117">Cosmos DB hızlı okuma ve yazma, sorguları, işlem mantığı, tutarlılık düzeyleri ve ayrıntılı erişim denetimi yöntemlerini/API'leri tek kapsayıcı kaynağa yoluyla destekler.</span><span class="sxs-lookup"><span data-stu-id="92c01-117">Cosmos DB supports fast reads and writes, queries, transactional logic, consistency levels, and fine-grained access control via methods/APIs to a single container resource.</span></span> <span data-ttu-id="92c01-118">Hizmeti dağıtma verileri bölümleri ve doğru bölüm yönlendirme sorgu istekleri üzerinden işler.</span><span class="sxs-lookup"><span data-stu-id="92c01-118">The service handles distributing data across partitions and routing query requests to the right partition.</span></span> 

<span data-ttu-id="92c01-119">Bölümleme nasıl çalışır?</span><span class="sxs-lookup"><span data-stu-id="92c01-119">How does partitioning work?</span></span> <span data-ttu-id="92c01-120">Her bir öğeyi benzersiz olarak tanımlamak bölüm anahtarı ve bir satır anahtarı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="92c01-120">Each item must have a partition key and a row key, which uniquely identify it.</span></span> <span data-ttu-id="92c01-121">Bölüm anahtarı, verileriniz için bir mantıksal bölüm görevi görür ve bölümler veri dağıtılmasında Cosmos DB ile doğal bir sınır sağlar.</span><span class="sxs-lookup"><span data-stu-id="92c01-121">Your partition key acts as a logical partition for your data, and provides Cosmos DB with a natural boundary for distributing data across partitions.</span></span> <span data-ttu-id="92c01-122">Kısaca, işte Azure Cosmos DB'de bölümleme nasıl çalışır:</span><span class="sxs-lookup"><span data-stu-id="92c01-122">In brief, here is how partitioning works in Azure Cosmos DB:</span></span>

* <span data-ttu-id="92c01-123">Cosmos DB kapsayıcıyla sağlamak `T` İsteği/sn üretilen iş</span><span class="sxs-lookup"><span data-stu-id="92c01-123">You provision a Cosmos DB container with `T` requests/s throughput</span></span>
* <span data-ttu-id="92c01-124">Arka planda Cosmos DB sunmak için gereken bölümleri sağlar `T` İsteği/sn.</span><span class="sxs-lookup"><span data-stu-id="92c01-124">Behind the scenes, Cosmos DB provisions partitions needed to serve `T` requests/s.</span></span> <span data-ttu-id="92c01-125">Varsa `T` bölüm başına en fazla üretilen daha yüksek `t`, ardından Cosmos DB hükümleri `N`  =  `T/t` bölümleri</span><span class="sxs-lookup"><span data-stu-id="92c01-125">If `T` is higher than the maximum throughput per partition `t`, then Cosmos DB provisions `N` = `T/t` partitions</span></span>
* <span data-ttu-id="92c01-126">Cosmos DB anahtar alanı bölümünün eşit yatay anahtar karmaları ayırır `N` bölümler.</span><span class="sxs-lookup"><span data-stu-id="92c01-126">Cosmos DB allocates the key space of partition key hashes evenly across the `N` partitions.</span></span> <span data-ttu-id="92c01-127">Bu nedenle, her bölüm (fiziksel bölüm) 1-N bölüm anahtarı değerlerini (mantıksal bölümler) barındırır</span><span class="sxs-lookup"><span data-stu-id="92c01-127">So, each partition (physical partition) hosts 1-N partition key values (logical partitions)</span></span>
* <span data-ttu-id="92c01-128">Fiziksel bir bölüm olduğunda `p` Cosmos DB, depolama sınırına sorunsuz bir şekilde böler ulaştığında `p` iki yeni bölümlere `p1` ve `p2` ve her bölüm için kabaca yarım anahtarlara karşılık gelen değerleri dağıtır.</span><span class="sxs-lookup"><span data-stu-id="92c01-128">When a physical partition `p` reaches its storage limit, Cosmos DB seamlessly splits `p` into two new partitions `p1` and `p2` and distributes values corresponding to roughly half the keys to each of the partitions.</span></span> <span data-ttu-id="92c01-129">Bu işlemi bölünmüş uygulamanıza görünmez durumdadır.</span><span class="sxs-lookup"><span data-stu-id="92c01-129">This split operation is invisible to your application.</span></span>
* <span data-ttu-id="92c01-130">Benzer şekilde, ne zaman sağlamanız daha yüksek verimlilik `t*N` verimlilik, Cosmos DB, bir veya daha yüksek verimlilik desteklemek için bölümler ayırır</span><span class="sxs-lookup"><span data-stu-id="92c01-130">Similarly, when you provision throughput higher than `t*N` throughput, Cosmos DB splits one or more of your partitions to support the higher throughput</span></span>

<span data-ttu-id="92c01-131">Bölüm anahtarlarını anlamları aşağıdaki tabloda gösterildiği gibi her API semantiği eşleşmesi biraz farklılık gösterir:</span><span class="sxs-lookup"><span data-stu-id="92c01-131">The semantics for partition keys are slightly different to match the semantics of each API, as shown in the following table:</span></span>

| <span data-ttu-id="92c01-132">API</span><span class="sxs-lookup"><span data-stu-id="92c01-132">API</span></span> | <span data-ttu-id="92c01-133">Bölüm anahtarı</span><span class="sxs-lookup"><span data-stu-id="92c01-133">Partition Key</span></span> | <span data-ttu-id="92c01-134">Satır anahtarı</span><span class="sxs-lookup"><span data-stu-id="92c01-134">Row Key</span></span> |
| --- | --- | --- |
| <span data-ttu-id="92c01-135">DocumentDB</span><span class="sxs-lookup"><span data-stu-id="92c01-135">DocumentDB</span></span> | <span data-ttu-id="92c01-136">Özel bölüm anahtar yolu</span><span class="sxs-lookup"><span data-stu-id="92c01-136">custom partition key path</span></span> | <span data-ttu-id="92c01-137">Sabit`id`</span><span class="sxs-lookup"><span data-stu-id="92c01-137">fixed `id`</span></span> | 
| <span data-ttu-id="92c01-138">MongoDB</span><span class="sxs-lookup"><span data-stu-id="92c01-138">MongoDB</span></span> | <span data-ttu-id="92c01-139">özel parça anahtarı</span><span class="sxs-lookup"><span data-stu-id="92c01-139">custom shard key</span></span>  | <span data-ttu-id="92c01-140">Sabit`_id`</span><span class="sxs-lookup"><span data-stu-id="92c01-140">fixed `_id`</span></span> | 
| <span data-ttu-id="92c01-141">Graph</span><span class="sxs-lookup"><span data-stu-id="92c01-141">Graph</span></span> | <span data-ttu-id="92c01-142">Özel bölüm anahtar özelliği</span><span class="sxs-lookup"><span data-stu-id="92c01-142">custom partition key property</span></span> | <span data-ttu-id="92c01-143">Sabit`id`</span><span class="sxs-lookup"><span data-stu-id="92c01-143">fixed `id`</span></span> | 
| <span data-ttu-id="92c01-144">Tablo</span><span class="sxs-lookup"><span data-stu-id="92c01-144">Table</span></span> | <span data-ttu-id="92c01-145">Sabit`PartitionKey`</span><span class="sxs-lookup"><span data-stu-id="92c01-145">fixed `PartitionKey`</span></span> | <span data-ttu-id="92c01-146">Sabit`RowKey`</span><span class="sxs-lookup"><span data-stu-id="92c01-146">fixed `RowKey`</span></span> | 

<span data-ttu-id="92c01-147">Cosmos DB karma tabanlı bölümleme kullanır.</span><span class="sxs-lookup"><span data-stu-id="92c01-147">Cosmos DB uses hash-based partitioning.</span></span> <span data-ttu-id="92c01-148">Öğeyi yazdığınızda, Cosmos DB bölüm anahtarı değerini karma hale getirir ve karma hale getirilen sonuç öğesinde depolamak için hangi bölümünü belirlemek için kullanın.</span><span class="sxs-lookup"><span data-stu-id="92c01-148">When you write an item, Cosmos DB hashes the partition key value and use the hashed result to determine which partition to store the item in.</span></span> <span data-ttu-id="92c01-149">Cosmos DB tüm öğeleri aynı fiziksel bölümünde aynı bölüm anahtarına sahip depolar.</span><span class="sxs-lookup"><span data-stu-id="92c01-149">Cosmos DB stores all items with the same partition key in the same physical partition.</span></span> <span data-ttu-id="92c01-150">Bölüm anahtarı seçimi tasarım zamanında yapmak zorunda önemli bir karardır.</span><span class="sxs-lookup"><span data-stu-id="92c01-150">The choice of the partition key is an important decision that you have to make at design time.</span></span> <span data-ttu-id="92c01-151">Çok çeşitli değerleri ve hatta erişim desenlerini sahip bir özellik adı seçmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="92c01-151">You must pick a property name that has a wide range of values and has even access patterns.</span></span>

> [!NOTE]
> <span data-ttu-id="92c01-152">Birçok farklı değerleri (100 s-1000'lik bloklar en az) sahip bir bölüm anahtarı için en iyi bir uygulamadır.</span><span class="sxs-lookup"><span data-stu-id="92c01-152">It is a best practice to have a partition key with many distinct values (100s-1000s at a minimum).</span></span>
>

<span data-ttu-id="92c01-153">Azure Cosmos DB kapsayıcıları "sabit" veya "sınırsız." oluşturulabilir</span><span class="sxs-lookup"><span data-stu-id="92c01-153">Azure Cosmos DB containers can be created as "fixed" or "unlimited."</span></span> <span data-ttu-id="92c01-154">Sabit boyutlu kapsayıcıları 10 GB ve 10. 000'ru / s işleme üst sınırına sahip.</span><span class="sxs-lookup"><span data-stu-id="92c01-154">Fixed-size containers have a maximum limit of 10 GB and 10,000 RU/s throughput.</span></span> <span data-ttu-id="92c01-155">Bazı API'ler için sabit boyutlu kapsayıcılar atlanacak bölüm anahtarı izin verir.</span><span class="sxs-lookup"><span data-stu-id="92c01-155">Some APIs allow the partition key to be omitted for fixed-size containers.</span></span> <span data-ttu-id="92c01-156">Sınırsız olarak bir kapsayıcı oluşturmak için en düşük işleme 2500 RU/s belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="92c01-156">To create a container as unlimited, you must specify a minimum throughput of 2500 RU/s.</span></span>

## <a name="partitioning-and-provisioned-throughput"></a><span data-ttu-id="92c01-157">Bölümlendirme ve sağlanan işleme</span><span class="sxs-lookup"><span data-stu-id="92c01-157">Partitioning and provisioned throughput</span></span>
<span data-ttu-id="92c01-158">Cosmos DB tahmin edilebilir performans için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="92c01-158">Cosmos DB is designed for predictable performance.</span></span> <span data-ttu-id="92c01-159">Bir kapsayıcı oluşturduğunuzda, üretilen iş açısından, yedek  **[istek birimleri](request-units.md) (RU) RU için olası eklentisinin dakika başına saniyede**.</span><span class="sxs-lookup"><span data-stu-id="92c01-159">When you create a container, you reserve throughput in terms of **[request units](request-units.md) (RU) per second with a potential add-on for RU per minute**.</span></span> <span data-ttu-id="92c01-160">Her istek CPU, bellek ve g/ç işlemi tarafından tüketilen gibi sistem kaynaklarının miktarını orantılıdır bir istek birimi ücret atanır.</span><span class="sxs-lookup"><span data-stu-id="92c01-160">Each request is assigned a request unit charge that is proportionate to the amount of system resources like CPU, Memory, and IO consumed by the operation.</span></span> <span data-ttu-id="92c01-161">Oturum tutarlılığı 1 KB belgeyle okuma bir istek birimi tüketir.</span><span class="sxs-lookup"><span data-stu-id="92c01-161">A read of a 1-KB document with Session consistency consumes one request unit.</span></span> <span data-ttu-id="92c01-162">Okuma 1. RU bağımsız olarak depolanan öğeler sayısını veya aynı anda çalıştırılması eşzamanlı istek sayısı.</span><span class="sxs-lookup"><span data-stu-id="92c01-162">A read is 1 RU regardless of the number of items stored or the number of concurrent requests running at the same time.</span></span> <span data-ttu-id="92c01-163">Büyük öğeleri boyutuna bağlı olarak daha yüksek istek birimleri gerektirir.</span><span class="sxs-lookup"><span data-stu-id="92c01-163">Larger items require higher request units depending on the size.</span></span> <span data-ttu-id="92c01-164">Varlıklarınızı ve uygulamanız için desteklemeniz gereken okuma sayısını boyutunu biliyorsanız, verimlilik ihtiyaçlarını okuma, uygulama için gerekli miktarda sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="92c01-164">If you know the size of your entities and the number of reads you need to support for your application, you can provision the exact amount of throughput required for your application's read needs.</span></span> 

> [!NOTE]
> <span data-ttu-id="92c01-165">Kapsayıcı tam verimini elde etmek için istekleri bazı farklı bölüm anahtar değerleri arasında eşit olarak dağıtmanızı sağlayan bir bölüm anahtarı seçmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="92c01-165">To achieve the full throughput of the container, you must choose a partition key that allows you to evenly distribute requests among some distinct partition key values.</span></span>
> 
> 

<a name="designing-for-partitioning"></a>
## <a name="working-with-the-azure-cosmos-db-apis"></a><span data-ttu-id="92c01-166">Azure Cosmos DB API'leri ile çalışma</span><span class="sxs-lookup"><span data-stu-id="92c01-166">Working with the Azure Cosmos DB APIs</span></span>
<span data-ttu-id="92c01-167">Kapsayıcılar oluşturmak ve bunları herhangi bir anda ölçeklendirmek için Azure portalında veya Azure CLI kullanın.</span><span class="sxs-lookup"><span data-stu-id="92c01-167">You can use the Azure portal or Azure CLI to create containers and scale them at any time.</span></span> <span data-ttu-id="92c01-168">Bu bölümde, kapsayıcıları oluşturma ve üretilen iş ve bölüm anahtar tanımını her desteklenen API'ları belirtin gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="92c01-168">This section shows how to create containers and specify the throughput and partition key definition in each of the supported APIs.</span></span>

### <a name="documentdb-api"></a><span data-ttu-id="92c01-169">DocumentDB API’si</span><span class="sxs-lookup"><span data-stu-id="92c01-169">DocumentDB API</span></span>
<span data-ttu-id="92c01-170">Aşağıdaki örnek DocumentDB API'sini kullanarak bir kapsayıcı (toplama) oluşturulacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="92c01-170">The following sample shows how to create a container (collection) using the DocumentDB API.</span></span> <span data-ttu-id="92c01-171">Daha ayrıntılı bilgi bulabilirsiniz [DocumentDB API'si ile bölümleme](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="92c01-171">You can find more details in [Partitioning with DocumentDB API](partition-data.md).</span></span>

```csharp
DocumentClient client = new DocumentClient(new Uri(endpoint), authKey);
await client.CreateDatabaseAsync(new Database { Id = "db" });

DocumentCollection myCollection = new DocumentCollection();
myCollection.Id = "coll";
myCollection.PartitionKey.Paths.Add("/deviceId");

await client.CreateDocumentCollectionAsync(
    UriFactory.CreateDatabaseUri("db"),
    myCollection,
    new RequestOptions { OfferThroughput = 20000 });
```

<span data-ttu-id="92c01-172">Bir öğe (belge) kullanarak okuyabilirsiniz `GET` REST API yönteminde veya kullanarak `ReadDocumentAsync` SDK'lar birinde.</span><span class="sxs-lookup"><span data-stu-id="92c01-172">You can read an item (document) using the `GET` method in the REST API or using `ReadDocumentAsync` in one of the SDKs.</span></span>

```csharp
// Read document. Needs the partition key and the ID to be specified
DeviceReading document = await client.ReadDocumentAsync<DeviceReading>(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  new RequestOptions { PartitionKey = new PartitionKey("XMS-0001") });
```

### <a name="mongodb-api"></a><span data-ttu-id="92c01-173">MongoDB API’si</span><span class="sxs-lookup"><span data-stu-id="92c01-173">MongoDB API</span></span>
<span data-ttu-id="92c01-174">MongoDB API'si ile sık kullanılan aracı, sürücü veya SDK aracılığıyla parçalı bir koleksiyon oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="92c01-174">With the MongoDB API, you can create a sharded collection through your favorite tool, driver, or SDK.</span></span> <span data-ttu-id="92c01-175">Bu örnekte koleksiyonu oluşturma işleminde Mongo kabuğunu kullanırız.</span><span class="sxs-lookup"><span data-stu-id="92c01-175">In this example, we use the Mongo Shell for the collection creation.</span></span>

<span data-ttu-id="92c01-176">Mongo Kabuğu'nda:</span><span class="sxs-lookup"><span data-stu-id="92c01-176">In the Mongo Shell:</span></span>

```
db.runCommand( { shardCollection: "admin.people", key: { region: "hashed" } } )
```
    
<span data-ttu-id="92c01-177">Sonuçları:</span><span class="sxs-lookup"><span data-stu-id="92c01-177">Results:</span></span>

```JSON
{
    "_t" : "ShardCollectionResponse",
    "ok" : 1,
    "collectionsharded" : "admin.people"
}
```

### <a name="table-api"></a><span data-ttu-id="92c01-178">Tablo API’si</span><span class="sxs-lookup"><span data-stu-id="92c01-178">Table API</span></span>

<span data-ttu-id="92c01-179">Tablo API ile tablolar için işleme, uygulamanız için appSettings yapılandırmasında belirtin:</span><span class="sxs-lookup"><span data-stu-id="92c01-179">With the Table API, you specify the throughput for tables in the appSettings configuration for your application:</span></span>

```xml
<configuration>
    <appSettings>
      <!--Table creation options -->
      <add key="TableThroughput" value="700"/>
    </appSettings>
</configuration>
```

<span data-ttu-id="92c01-180">Ardından Azure Table depolama SDK'sını kullanarak bir tablo oluşturun.</span><span class="sxs-lookup"><span data-stu-id="92c01-180">Then you create a table using the Azure Table storage SDK.</span></span> <span data-ttu-id="92c01-181">Bölüm anahtarı örtük olarak oluşturulmuş `PartitionKey` değeri.</span><span class="sxs-lookup"><span data-stu-id="92c01-181">The partition key is implicitly created as the `PartitionKey` value.</span></span> 

```csharp
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

CloudTable table = tableClient.GetTableReference("people");
table.CreateIfNotExists();
```

<span data-ttu-id="92c01-182">Aşağıdaki kod parçacığını kullanarak tek bir varlık alabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="92c01-182">You can retrieve a single entity using the following snippet:</span></span>

```csharp
// Create a retrieve operation that takes a customer entity.
TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

// Execute the retrieve operation.
TableResult retrievedResult = table.Execute(retrieveOperation);
```
<span data-ttu-id="92c01-183">Bkz: [tablo API ile geliştirme](tutorial-develop-table-dotnet.md) daha fazla ayrıntı için.</span><span class="sxs-lookup"><span data-stu-id="92c01-183">See [Developing with the Table API](tutorial-develop-table-dotnet.md) for more details.</span></span>

### <a name="graph-api"></a><span data-ttu-id="92c01-184">Graph API</span><span class="sxs-lookup"><span data-stu-id="92c01-184">Graph API</span></span>

<span data-ttu-id="92c01-185">Grafik API'si ile kapsayıcı oluşturmak için Azure portal veya CLI kullanmalısınız.</span><span class="sxs-lookup"><span data-stu-id="92c01-185">With the Graph API, you must use the Azure portal or CLI to create containers.</span></span> <span data-ttu-id="92c01-186">Alternatif olarak, Azure Cosmos DB çok model olduğundan, bir başka modellerinin oluşturmak ve grafik kapsayıcı ölçeklendirmek için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="92c01-186">Alternatively, since Azure Cosmos DB is multi-model, you can use one of the other models to create and scale your graph container.</span></span>

<span data-ttu-id="92c01-187">Herhangi bir köşe veya kimliği ve bölüm anahtarı Gremlin kullanarak kenar okuyabilir.</span><span class="sxs-lookup"><span data-stu-id="92c01-187">You can read any vertex or edge using the partition key and id in Gremlin.</span></span> <span data-ttu-id="92c01-188">Örneğin, bölgeye ("ABD") bölüm anahtarını ve satır anahtarı olarak "Seattle" ile bir grafik için aşağıdaki sözdizimini kullanarak bir köşe bulabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="92c01-188">For example, for a graph with region ("USA") as the partition key, and "Seattle" as the row key, you can find a vertex using the following syntax:</span></span>

```
g.V(['USA', 'Seattle'])
```

<span data-ttu-id="92c01-189">Kenarları aynı bölüm anahtarı ve satır anahtarı kullanarak bir sınır başvuruda bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="92c01-189">Same with edges, you can reference an edge using the partition key and row key.</span></span>

```
g.E(['USA', 'I5'])
```

<span data-ttu-id="92c01-190">Bkz: [Cosmos DB Gremlin desteği](gremlin-support.md) daha fazla ayrıntı için.</span><span class="sxs-lookup"><span data-stu-id="92c01-190">See [Gremlin support for Cosmos DB](gremlin-support.md) for more details.</span></span>


<a name="designing-for-partitioning"></a>
## <a name="designing-for-partitioning"></a><span data-ttu-id="92c01-191">Bölümleme için tasarlama</span><span class="sxs-lookup"><span data-stu-id="92c01-191">Designing for partitioning</span></span>
<span data-ttu-id="92c01-192">Etkili bir şekilde Azure Cosmos DB ile ölçeklendirmek için kapsayıcı oluştururken iyi bir bölüm anahtarı seçmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="92c01-192">To scale effectively with Azure Cosmos DB, you need to pick a good partition key when you create your container.</span></span> <span data-ttu-id="92c01-193">Bölüm anahtarı seçmeye yönelik iki önemli noktalar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="92c01-193">There are two key considerations for choosing a partition key:</span></span>

* <span data-ttu-id="92c01-194">**Sorgu ve işlemler için sınır**: bölüm anahtarı seçiminizi varlıklarınızı ölçeklenebilir bir çözüm sağlamak için birden çok bölüm anahtarları arasında dağıtmak için gereksinim karşı işlemleri kullanımını etkinleştirmek için gereken dengelemeniz.</span><span class="sxs-lookup"><span data-stu-id="92c01-194">**Boundary for query and transactions**: Your choice of partition key should balance the need to enable the use of transactions against the requirement to distribute your entities across multiple partition keys to ensure a scalable solution.</span></span> <span data-ttu-id="92c01-195">Bir extreme tüm öğeleri aynı bölüm anahtarı ayarlayabilirsiniz, ancak bu çözümünüzü ölçeklenebilirliğini sınırlayabilir.</span><span class="sxs-lookup"><span data-stu-id="92c01-195">At one extreme, you could set the same partition key for all your items, but this may limit the scalability of your solution.</span></span> <span data-ttu-id="92c01-196">Diğer uçta yüksek düzeyde ölçeklenebilir kalır ancak saklı yordamları ve Tetikleyicileri aracılığıyla çapraz belge işlemleri kullanmasını önler her öğe için bir benzersiz bir bölüm anahtarı atayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="92c01-196">At the other extreme, you could assign a unique partition key for each item, which would be highly scalable but would prevent you from using cross document transactions via stored procedures and triggers.</span></span> <span data-ttu-id="92c01-197">İdeal bölüm anahtarı verimli sorguları kullanmanıza olanak sağlayan ve çözümünüzü ölçeklenebilir olduğundan emin olmak için yeterli kardinalite sahip olan biridir.</span><span class="sxs-lookup"><span data-stu-id="92c01-197">An ideal partition key is one that enables you to use efficient queries and that has sufficient cardinality to ensure your solution is scalable.</span></span> 
* <span data-ttu-id="92c01-198">**Hiçbir depolama ve performans sorunlarını**: çeşitli farklı değerleri arasında dağıtılacak yazma sağlayan bir özellik seçmek önemlidir.</span><span class="sxs-lookup"><span data-stu-id="92c01-198">**No storage and performance bottlenecks**: It is important to pick a property that allows writes to be distributed across various distinct values.</span></span> <span data-ttu-id="92c01-199">Aynı bölüm anahtarı isteklerini tek bir bölüm verimini aşamaz ve kısıtlanan.</span><span class="sxs-lookup"><span data-stu-id="92c01-199">Requests to the same partition key cannot exceed the throughput of a single partition, and are throttled.</span></span> <span data-ttu-id="92c01-200">Böylece, uygulamanızda "etkin nokta" sonuçlanmaz bir bölüm anahtarı seçmek önemlidir.</span><span class="sxs-lookup"><span data-stu-id="92c01-200">So it is important to pick a partition key that does not result in "hot spots" within your application.</span></span> <span data-ttu-id="92c01-201">Tüm veriler tek bölüm anahtarı için bir bölüm içinde saklanmalıdır olduğundan, yüksek miktarda veriyi aynı değere sahip bölüm anahtarlarını önlemek için de önerilir.</span><span class="sxs-lookup"><span data-stu-id="92c01-201">Since all the data for a single partition key must be stored within a partition, it is also recommended to avoid partition keys that have high volumes of data for the same value.</span></span> 

<span data-ttu-id="92c01-202">Birkaç gerçek dünya senaryoları ve iyi bölüm anahtarlarının her biri için bakalım:</span><span class="sxs-lookup"><span data-stu-id="92c01-202">Let's look at a few real-world scenarios, and good partition keys for each:</span></span>
* <span data-ttu-id="92c01-203">Bir kullanıcı profili arka uç uygulama, kullanıcı kimliği bölüm anahtarı için iyi bir seçimdir yoktur.</span><span class="sxs-lookup"><span data-stu-id="92c01-203">If you’re implementing a user profile backend, then the user ID is a good choice for partition key.</span></span>
* <span data-ttu-id="92c01-204">Örneğin, Aygıt durumu IOT veri depoluyorsanız bir cihaz kimliği bölüm anahtarı için iyi bir seçimdir.</span><span class="sxs-lookup"><span data-stu-id="92c01-204">If you’re storing IoT data for example, device state, a device ID is a good choice for partition key.</span></span>
* <span data-ttu-id="92c01-205">Zaman serisi veri günlük kaydı için Azure Cosmos DB kullanıyorsanız, daha sonra ana bilgisayar adı veya işlem bölüm anahtarı için iyi bir seçimdir kimliğidir.</span><span class="sxs-lookup"><span data-stu-id="92c01-205">If you’re using Azure Cosmos DB for logging time-series data, then the hostname or process ID is a good choice for partition key.</span></span>
* <span data-ttu-id="92c01-206">Çok kiracılı mimari varsa, Kiracı kimliği bölüm anahtarı için iyi bir seçimdir.</span><span class="sxs-lookup"><span data-stu-id="92c01-206">If you have a multi-tenant architecture, the tenant ID is a good choice for partition key.</span></span>

<span data-ttu-id="92c01-207">IOT ve kullanıcı profilleri gibi bazı durumlarda kullanım, bölüm anahtarı, kimliğinizi (belge anahtarı) ile aynı olması.</span><span class="sxs-lookup"><span data-stu-id="92c01-207">In some use cases like IoT and user profiles, the partition key might be the same as your id (document key).</span></span> <span data-ttu-id="92c01-208">Bazı durumlarda zaman serisi veri gibi kimliğinden farklı bir bölüm anahtarı olabilir.</span><span class="sxs-lookup"><span data-stu-id="92c01-208">In others like the time series data, you might have a partition key that’s different than the id.</span></span>

### <a name="partitioning-and-loggingtime-series-data"></a><span data-ttu-id="92c01-209">Bölümlendirme ve zaman/günlüğü-serisi veri</span><span class="sxs-lookup"><span data-stu-id="92c01-209">Partitioning and logging/time-series data</span></span>
<span data-ttu-id="92c01-210">Cosmos DB'nin ortak kullanım durumları günlüğe kaydetme ve telemetri biridir.</span><span class="sxs-lookup"><span data-stu-id="92c01-210">One of the common use cases of Cosmos DB is for logging and telemetry.</span></span> <span data-ttu-id="92c01-211">Büyük miktarda veriyi okuma/yazma gerekebilecek beri iyi bir bölüm anahtarı seçmek önemlidir.</span><span class="sxs-lookup"><span data-stu-id="92c01-211">It is important to pick a good partition key since you might need to read/write vast volumes of data.</span></span> <span data-ttu-id="92c01-212">Seçim, okuma ve yazma hızları ve tür sorgular çalıştırmak için beklediğiniz bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="92c01-212">The choice depends on your read and write rates and kinds of queries you expect to run.</span></span> <span data-ttu-id="92c01-213">İyi bir bölüm anahtarı seçmek bazı ipuçları şunlardır.</span><span class="sxs-lookup"><span data-stu-id="92c01-213">Here are some tips on how to choose a good partition key.</span></span>

* <span data-ttu-id="92c01-214">Kullanım örneği küçük oranını içeriyorsa bu gibi bir durumda damgası dökümü kullanarak tarih sonra iyi bir yaklaşım bölüm anahtarı olduğu gibi zaman, sorgu zaman damgaları aralıklarına tarafından gerek ve diğer filtreleri uzun süre biriktirme yazar.</span><span class="sxs-lookup"><span data-stu-id="92c01-214">If your use case involves a small rate of writes accumulating over a long period of time, and need to query by ranges of timestamps and other filters, then using a rollup of the timestamp, for example,  date as a partition key is a good approach.</span></span> <span data-ttu-id="92c01-215">Bu sorguya tüm verileri için bir tarih tek bir bölümün dışında sağlar.</span><span class="sxs-lookup"><span data-stu-id="92c01-215">This allows you to query over all the data for a date from a single partition.</span></span> 
* <span data-ttu-id="92c01-216">İş yükünüzün daha yaygın bir durumdur, ağır yazılmışsa zaman damgasını dayalı olmayan ve böylece Cosmos DB yazma eşit çeşitli bölümler dağıtabilirsiniz bölüm anahtarı kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="92c01-216">If your workload is written heavy, which is more common, you should use a partition key that’s not based on timestamp so that Cosmos DB can distribute writes evenly across various partitions.</span></span> <span data-ttu-id="92c01-217">Burada bir ana bilgisayar adı, işlem kimliği, etkinlik kimliği veya başka bir özelliği yüksek önem düzeyi ile iyi bir seçimdir.</span><span class="sxs-lookup"><span data-stu-id="92c01-217">Here a hostname, process ID, activity ID, or another property with high cardinality is a good choice.</span></span> 
* <span data-ttu-id="92c01-218">Burada her gün/ay için birden çok kapsayıcı sahip ve bölüm anahtarı ana bilgisayar adı gibi ayrıntılı bir özelliği bir karma bir buna üçüncü bir yaklaşımdır.</span><span class="sxs-lookup"><span data-stu-id="92c01-218">A third approach is a hybrid one where you have multiple containers, one for each day/month and the partition key is a granular property like hostname.</span></span> <span data-ttu-id="92c01-219">Bu zaman penceresinde göre farklı verimlilik ayarlayabilirsiniz avantajına sahiptir, okuma ve yazma işlemleri, gördüğünden önceki ay ile üretilen iş bunlar bu yana yalnızca alt ancak örneğin, geçerli ay için kapsayıcı daha yüksek işleme ile sağlanır Hizmet vermemesini okur.</span><span class="sxs-lookup"><span data-stu-id="92c01-219">This has the benefit that you can set different throughput based on the time window, for example, the container for the current month is provisioned with higher throughput since it serves reads and writes, whereas previous months with lower throughput since they only serve reads.</span></span>

### <a name="partitioning-and-multi-tenancy"></a><span data-ttu-id="92c01-220">Bölümlendirme ve çoklu kiracı</span><span class="sxs-lookup"><span data-stu-id="92c01-220">Partitioning and multi-tenancy</span></span>
<span data-ttu-id="92c01-221">Cosmos DB kullanarak çok kiracılı uygulama uyguluyorsanız, iki popüler desenleri – Kiracı başına bir bölüm anahtarı ve Kiracı başına bir kapsayıcı vardır.</span><span class="sxs-lookup"><span data-stu-id="92c01-221">If you are implementing a multi-tenant application using Cosmos DB, there are two popular patterns – one partition key per tenant, and one container per tenant.</span></span> <span data-ttu-id="92c01-222">Artıları ve eksileri her şunlardır:</span><span class="sxs-lookup"><span data-stu-id="92c01-222">Here are the pros and cons for each:</span></span>

* <span data-ttu-id="92c01-223">Kiracı başına bir bölüm anahtarı: tek bir kapsayıcıda birlikte bu modelde, kiracılar.</span><span class="sxs-lookup"><span data-stu-id="92c01-223">One Partition Key per tenant: In this model, tenants are collocated within a single container.</span></span> <span data-ttu-id="92c01-224">Ancak, sorgular ve eklemeleri tek bir kiracı içinde öğeleri için tek bir bölüm karşı gerçekleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="92c01-224">But queries and inserts for items within a single tenant can be performed against a single partition.</span></span> <span data-ttu-id="92c01-225">İşlem mantığı, bir kiracı içindeki tüm öğeler arasında de uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="92c01-225">You can also implement transactional logic across all items within a tenant.</span></span> <span data-ttu-id="92c01-226">Birden çok kiracıya bir kapsayıcı paylaşmak olduğundan, her bir kiracı için ek boş alan sağlama yerine tek bir kapsayıcıdaki kiracılar için kaynak havuzu tarafından depolama ve işleme maliyetleri kaydedebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="92c01-226">Since multiple tenants share a container, you can save storage and throughput costs by pooling resources for tenants within a single container rather than provisioning extra headroom for each tenant.</span></span> <span data-ttu-id="92c01-227">Dezavantajı, performans yalıtımı Kiracı başına yok ' dir.</span><span class="sxs-lookup"><span data-stu-id="92c01-227">The drawback is that you do not have performance isolation per tenant.</span></span> <span data-ttu-id="92c01-228">Performans/verimliliği artırır, kiracılar için hedeflenen artar kapsayıcının tamamı vs uygulayın.</span><span class="sxs-lookup"><span data-stu-id="92c01-228">Performance/throughput increases apply to the entire container vs targeted increases for tenants.</span></span>
* <span data-ttu-id="92c01-229">Kiracı başına bir kapsayıcı: her bir kiracı kendi kapsayıcı vardır.</span><span class="sxs-lookup"><span data-stu-id="92c01-229">One Container per tenant: Each tenant has its own container.</span></span> <span data-ttu-id="92c01-230">Bu modelde, Kiracı başına performans ayırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="92c01-230">In this model, you can reserve performance per tenant.</span></span> <span data-ttu-id="92c01-231">Cosmos DB'ın yeni fiyatlandırma modeli sağlamada bu birkaç kiracılarla çok kiracılı uygulamalar için daha uygun maliyetli modelidir.</span><span class="sxs-lookup"><span data-stu-id="92c01-231">With Cosmos DB's new provisioning pricing model, this model is more cost-effective for multi-tenant applications with a few tenants.</span></span>

<span data-ttu-id="92c01-232">Ayrıca, küçük kiracılar collocates ve büyük kiracılar kendi kapsayıcıya Geçiren birleşimi ve katmanlı bir yaklaşım kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="92c01-232">You can also use a combination/tiered approach that collocates small tenants and migrates larger tenants to their own container.</span></span>

## <a name="next-steps"></a><span data-ttu-id="92c01-233">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="92c01-233">Next steps</span></span>
<span data-ttu-id="92c01-234">Bu makalede, bir genel bakış, kavramlar ve tüm Azure Cosmos DB API'si ile bölümleme için en iyi uygulamalar için genel bir bakış sağlanan.</span><span class="sxs-lookup"><span data-stu-id="92c01-234">In this article, we provided an overview for an overview of concepts and best practices for partitioning with any Azure Cosmos DB API.</span></span> 

* <span data-ttu-id="92c01-235">Hakkında bilgi edinin [Azure Cosmos veritabanı sağlanan işleme](request-units.md)</span><span class="sxs-lookup"><span data-stu-id="92c01-235">Learn about [provisioned throughput in Azure Cosmos DB](request-units.md)</span></span>
* <span data-ttu-id="92c01-236">Hakkında bilgi edinin [Azure Cosmos veritabanı genel dağıtım](distribute-data-globally.md)</span><span class="sxs-lookup"><span data-stu-id="92c01-236">Learn about [global distribution in Azure Cosmos DB](distribute-data-globally.md)</span></span>



