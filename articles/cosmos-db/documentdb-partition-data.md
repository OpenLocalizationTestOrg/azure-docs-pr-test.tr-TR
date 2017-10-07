---
title: "aaaPartitioning ve Azure Cosmos DB'de ölçeklendirme | Microsoft Docs"
description: "Azure Cosmos veritabanı bölümleme nasıl çalıştığı hakkında tooconfigure bölümlendirme ve bölüm anahtarlarını ve toopick hello sağ nasıl nasıl bölüm anahtarı, uygulamanız için öğrenin."
services: cosmos-db
author: arramac
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: 702c39b4-1798-48dd-9993-4493a2f6df9e
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/24/2017
ms.author: arramac
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 30621d2ba0b89efb72005680d5f3a73998347514
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="partitioning-in-azure-cosmos-db-using-hello-documentdb-api"></a><span data-ttu-id="5ad3f-103">Merhaba DocumentDB API kullanarak Azure Cosmos DB içinde bölümlendirme</span><span class="sxs-lookup"><span data-stu-id="5ad3f-103">Partitioning in Azure Cosmos DB using hello DocumentDB API</span></span>

<span data-ttu-id="5ad3f-104">[Microsoft Azure Cosmos DB](../cosmos-db/introduction.md) ulaşmanıza hızlı ve tahmin edilebilir performansı ve ölçeği sorunsuz bir şekilde uygulamanızı yanı sıra, büyüdükçe Genel dağıtılmış, birden çok model veritabanı tasarlanan hizmet toohelp değil.</span><span class="sxs-lookup"><span data-stu-id="5ad3f-104">[Microsoft Azure Cosmos DB](../cosmos-db/introduction.md) is a global distributed, multi-model database service designed toohelp you achieve fast, predictable performance and scale seamlessly along with your application as it grows.</span></span> 

<span data-ttu-id="5ad3f-105">Bu makalede nasıl ile Cosmos DB kapsayıcıların bölümlendirme ile toowork hello DocumentDB API genel bir bakış sağlar.</span><span class="sxs-lookup"><span data-stu-id="5ad3f-105">This article provides an overview of how toowork with partitioning of Cosmos DB containers with hello DocumentDB API.</span></span> <span data-ttu-id="5ad3f-106">Bkz: [bölümlendirme ve yatay ölçekleme](../cosmos-db/partition-data.md) genel bir bakış kavramları ve tüm Azure Cosmos DB API'si ile bölümleme için en iyi uygulamalar için.</span><span class="sxs-lookup"><span data-stu-id="5ad3f-106">See [partitioning and horizontal scaling](../cosmos-db/partition-data.md) for an overview of concepts and best practices for partitioning with any Azure Cosmos DB API.</span></span> 

<span data-ttu-id="5ad3f-107">tooget kodu ile başlatıldı, hello projesinden indirmeniz [Github](https://github.com/Azure/azure-documentdb-dotnet/tree/a2d61ddb53f8ab2a23d3ce323c77afcf5a608f52/samples/documentdb-benchmark).</span><span class="sxs-lookup"><span data-stu-id="5ad3f-107">tooget started with code, download hello project from [Github](https://github.com/Azure/azure-documentdb-dotnet/tree/a2d61ddb53f8ab2a23d3ce323c77afcf5a608f52/samples/documentdb-benchmark).</span></span> 

<span data-ttu-id="5ad3f-108">Bu makaleyi okuduktan sonra aşağıdaki soruları mümkün tooanswer hello olacaktır:</span><span class="sxs-lookup"><span data-stu-id="5ad3f-108">After reading this article, you will be able tooanswer hello following questions:</span></span>   

* <span data-ttu-id="5ad3f-109">Nasıl yapılır Azure Cosmos veritabanı bölümleme iş?</span><span class="sxs-lookup"><span data-stu-id="5ad3f-109">How does partitioning work in Azure Cosmos DB?</span></span>
* <span data-ttu-id="5ad3f-110">Azure Cosmos DB'de bölümleme nasıl yapılandırabilirim</span><span class="sxs-lookup"><span data-stu-id="5ad3f-110">How do I configure partitioning in Azure Cosmos DB</span></span>
* <span data-ttu-id="5ad3f-111">Bölüm anahtarlarını nedir ve nasıl ı hello sağ bölüm anahtarı Uygulamam için çekme?</span><span class="sxs-lookup"><span data-stu-id="5ad3f-111">What are partition keys, and how do I pick hello right partition key for my application?</span></span>

<span data-ttu-id="5ad3f-112">tooget kodu ile başlatıldı, hello projesinden indirmeniz [Azure Cosmos DB performans testi sürücü örnek](https://github.com/Azure/azure-documentdb-dotnet/tree/a2d61ddb53f8ab2a23d3ce323c77afcf5a608f52/samples/documentdb-benchmark).</span><span class="sxs-lookup"><span data-stu-id="5ad3f-112">tooget started with code, download hello project from [Azure Cosmos DB Performance Testing Driver Sample](https://github.com/Azure/azure-documentdb-dotnet/tree/a2d61ddb53f8ab2a23d3ce323c77afcf5a608f52/samples/documentdb-benchmark).</span></span> 

<!-- placeholder until we have a permanent solution-->
<a name="partition-keys"></a>
<a name="single-partition-and-partitioned-collections"></a>
<a name="migrating-from-single-partition"></a>

## <a name="partition-keys"></a><span data-ttu-id="5ad3f-113">Bölüm anahtarlarını</span><span class="sxs-lookup"><span data-stu-id="5ad3f-113">Partition keys</span></span>

<span data-ttu-id="5ad3f-114">Hello DocumentDB API, JSON yolu hello biçiminde hello bölüm anahtar tanımı belirtin.</span><span class="sxs-lookup"><span data-stu-id="5ad3f-114">In hello DocumentDB API, you specify hello partition key definition in hello form of a JSON path.</span></span> <span data-ttu-id="5ad3f-115">Merhaba aşağıdaki tabloda bölüm temel tanımları ve tooeach karşılık gelen hello değerleri örnekleri gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="5ad3f-115">hello following table shows examples of partition key definitions and hello values corresponding tooeach.</span></span> <span data-ttu-id="5ad3f-116">Merhaba bölüm anahtarı belirtilen bir yolu olarak örneğin `/department` temsil hello özelliği departman.</span><span class="sxs-lookup"><span data-stu-id="5ad3f-116">hello partition key is specified as a path, e.g. `/department` represents hello property department.</span></span> 

<table border="0" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td valign="top"><p><span data-ttu-id="5ad3f-117"><strong>Bölüm anahtarı</strong></span><span class="sxs-lookup"><span data-stu-id="5ad3f-117"><strong>Partition Key</strong></span></span></p></td>
            <td valign="top"><p><span data-ttu-id="5ad3f-118"><strong>Açıklama</strong></span><span class="sxs-lookup"><span data-stu-id="5ad3f-118"><strong>Description</strong></span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="5ad3f-119">/Department</span><span class="sxs-lookup"><span data-stu-id="5ad3f-119">/department</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="5ad3f-120">Belge hello öğesi olduğu doc.department toohello değeri karşılık gelir.</span><span class="sxs-lookup"><span data-stu-id="5ad3f-120">Corresponds toohello value of doc.department where doc is hello item.</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="5ad3f-121">/ Özellikler/adı</span><span class="sxs-lookup"><span data-stu-id="5ad3f-121">/properties/name</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="5ad3f-122">Belge hello öğesi (iç içe özellik) olduğu doc.properties.name toohello değeri karşılık gelir.</span><span class="sxs-lookup"><span data-stu-id="5ad3f-122">Corresponds toohello value of doc.properties.name where doc is hello item (nested property).</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="5ad3f-123">/ID</span><span class="sxs-lookup"><span data-stu-id="5ad3f-123">/id</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="5ad3f-124">Doc.id toohello değeri karşılık gelir (kimliği ve bölüm anahtarı aynı hello olan özelliği).</span><span class="sxs-lookup"><span data-stu-id="5ad3f-124">Corresponds toohello value of doc.id (id and partition key are hello same property).</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="5ad3f-125">/ "bölüm adı"</span><span class="sxs-lookup"><span data-stu-id="5ad3f-125">/"department name"</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="5ad3f-126">Belge hello öğesi olduğu belge ["bölüm adı"] değerini toohello karşılık gelir.</span><span class="sxs-lookup"><span data-stu-id="5ad3f-126">Corresponds toohello value of doc["department name"] where doc is hello item.</span></span></p></td>
        </tr>
    </tbody>
</table>

> [!NOTE]
> <span data-ttu-id="5ad3f-127">toohello özellik başlangıç değeri yerine karşılık gelen ilke yolları, yol hello hello anahtar farkı dizin oluşturma için bölüm anahtarı hello sözdizimi benzer toohello yol belirtimi, yani var. hiçbir joker hello sonunda.</span><span class="sxs-lookup"><span data-stu-id="5ad3f-127">hello syntax for partition key is similar toohello path specification for indexing policy paths with hello key difference that hello path corresponds toohello property instead of hello value, i.e. there is no wild card at hello end.</span></span> <span data-ttu-id="5ad3f-128">Örneğin, / bölüm/belirtirsiniz?</span><span class="sxs-lookup"><span data-stu-id="5ad3f-128">For example, you would specify /department/?</span></span> <span data-ttu-id="5ad3f-129">tooindex hello departmanı altında değerleri, ancak /department hello bölüm anahtar tanımı olarak belirtin.</span><span class="sxs-lookup"><span data-stu-id="5ad3f-129">tooindex hello values under department, but specify /department as hello partition key definition.</span></span> <span data-ttu-id="5ad3f-130">Merhaba bölüm anahtarı örtük olarak dizine alınır ve dizin oluşturma ilkesi geçersiz kılmaları kullanarak dizin dışarıda bırakılamaz.</span><span class="sxs-lookup"><span data-stu-id="5ad3f-130">hello partition key is implicitly indexed and cannot be excluded from indexing using indexing policy overrides.</span></span>
> 
> 

<span data-ttu-id="5ad3f-131">Bölüm anahtarı hello seçimine hello uygulamanızın performansını nasıl etkilediğini adresindeki bakalım.</span><span class="sxs-lookup"><span data-stu-id="5ad3f-131">Let's look at how hello choice of partition key impacts hello performance of your application.</span></span>

## <a name="working-with-hello-azure-cosmos-db-sdks"></a><span data-ttu-id="5ad3f-132">Hello Azure Cosmos DB SDK'ları ile çalışma</span><span class="sxs-lookup"><span data-stu-id="5ad3f-132">Working with hello Azure Cosmos DB SDKs</span></span>
<span data-ttu-id="5ad3f-133">Azure Cosmos DB ile otomatik bölümleme için destek eklenmiştir [REST API sürümü 2015-12-16](/rest/api/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="5ad3f-133">Azure Cosmos DB added support for automatic partitioning with [REST API version 2015-12-16](/rest/api/documentdb/).</span></span> <span data-ttu-id="5ad3f-134">Sipariş bölümlenmiş toocreate kapsayıcılarında SDK sürümleri 1.6.0 indirmeniz gerekir veya daha yeni bir hello desteklenen SDK'sı platformlar (.NET, Node.js, Java, Python, MongoDB).</span><span class="sxs-lookup"><span data-stu-id="5ad3f-134">In order toocreate partitioned containers, you must download SDK versions 1.6.0 or newer in one of hello supported SDK platforms (.NET, Node.js, Java, Python, MongoDB).</span></span> 

### <a name="creating-containers"></a><span data-ttu-id="5ad3f-135">Kapsayıcıları oluşturma</span><span class="sxs-lookup"><span data-stu-id="5ad3f-135">Creating containers</span></span>
<span data-ttu-id="5ad3f-136">Merhaba aşağıdaki örnek .NET parçacığı toocreate bir kapsayıcı toostore cihaz telemetri verileri işleme saniye başına 20.000 istek birimlerinin gösterir.</span><span class="sxs-lookup"><span data-stu-id="5ad3f-136">hello following sample shows a .NET snippet toocreate a container toostore device telemetry data of 20,000 request units per second of throughput.</span></span> <span data-ttu-id="5ad3f-137">Merhaba SDK ayarlar hello OfferThroughput değeri (hangi sırayla ayarlar hello `x-ms-offer-throughput` hello REST API istek üstbilgisinde).</span><span class="sxs-lookup"><span data-stu-id="5ad3f-137">hello SDK sets hello OfferThroughput value (which in turn sets hello `x-ms-offer-throughput` request header in hello REST API).</span></span> <span data-ttu-id="5ad3f-138">Merhaba burada ayarlarız `/deviceId` hello bölüm anahtarı olarak.</span><span class="sxs-lookup"><span data-stu-id="5ad3f-138">Here we set hello `/deviceId` as hello partition key.</span></span> <span data-ttu-id="5ad3f-139">Bölüm anahtarı Hello seçimine hello kapsayıcı meta verilerinin adı ve dizin oluşturma ilkesini gibi hello rest birlikte kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="5ad3f-139">hello choice of partition key is saved along with hello rest of hello container metadata like name and indexing policy.</span></span>

<span data-ttu-id="5ad3f-140">Bu örnek için biz çekilen `deviceId` (a) olduğundan çok sayıda aygıtlar, biliyoruz olduğundan, yazma dağıtılabilir bölümleri arasında eşit olarak ve tooscale hello veritabanı tooingest büyük miktarda veriyi ve (b) birçok hello istekleri ister bize izin verme Merhaba son okuma getirme bir aygıt için kapsamlı tooa tek DeviceID olan ve tek bir bölümün dışında alınabilir.</span><span class="sxs-lookup"><span data-stu-id="5ad3f-140">For this sample, we picked `deviceId` since we know that (a) since there are a large number of devices, writes can be distributed across partitions evenly and allowing us tooscale hello database tooingest massive volumes of data and (b) many of hello requests like fetching hello latest reading for a device are scoped tooa single deviceId and can be retrieved from a single partition.</span></span>

```csharp
DocumentClient client = new DocumentClient(new Uri(endpoint), authKey);
await client.CreateDatabaseAsync(new Database { Id = "db" });

// Container for device telemetry. Here hello property deviceId will be used as hello partition key too
// spread across partitions. Configured for 10K RU/s throughput and an indexing policy that supports 
// sorting against any number or string property.
DocumentCollection myCollection = new DocumentCollection();
myCollection.Id = "coll";
myCollection.PartitionKey.Paths.Add("/deviceId");

await client.CreateDocumentCollectionAsync(
    UriFactory.CreateDatabaseUri("db"),
    myCollection,
    new RequestOptions { OfferThroughput = 20000 });
```

<span data-ttu-id="5ad3f-141">Bu yöntem tooCosmos DB çağrısı bir REST API yapar ve hello hizmet hello istenen işlemeyi temel alan bölüm sayısı hazırlayacağınız.</span><span class="sxs-lookup"><span data-stu-id="5ad3f-141">This method makes a REST API call tooCosmos DB, and hello service will provision a number of partitions based on hello requested throughput.</span></span> <span data-ttu-id="5ad3f-142">Performansınızı gelişmesi gerektiği bir kapsayıcı hello verimini değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5ad3f-142">You can change hello throughput of a container as your performance needs evolve.</span></span> 

### <a name="reading-and-writing-items"></a><span data-ttu-id="5ad3f-143">Okuma ve yazma öğeleri</span><span class="sxs-lookup"><span data-stu-id="5ad3f-143">Reading and writing items</span></span>
<span data-ttu-id="5ad3f-144">Şimdi, şimdi Cosmos Veritabanına veri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="5ad3f-144">Now, let's insert data into Cosmos DB.</span></span> <span data-ttu-id="5ad3f-145">Bir aygıt okuma ve çağrısı tooCreateDocumentAsync tooinsert bir kapsayıcıya okuma yeni bir cihaz içeren bir örnek sınıf İşte.</span><span class="sxs-lookup"><span data-stu-id="5ad3f-145">Here's a sample class containing a device reading, and a call tooCreateDocumentAsync tooinsert a new device reading into a container.</span></span> <span data-ttu-id="5ad3f-146">Bu, hello DocumentDB API yararlanan bir örnektir:</span><span class="sxs-lookup"><span data-stu-id="5ad3f-146">This is an example leveraging hello DocumentDB API:</span></span>

```csharp
public class DeviceReading
{
    [JsonProperty("id")]
    public string Id;

    [JsonProperty("deviceId")]
    public string DeviceId;

    [JsonConverter(typeof(IsoDateTimeConverter))]
    [JsonProperty("readingTime")]
    public DateTime ReadingTime;

    [JsonProperty("metricType")]
    public string MetricType;

    [JsonProperty("unit")]
    public string Unit;

    [JsonProperty("metricValue")]
    public double MetricValue;
  }

// Create a document. Here hello partition key is extracted as "XMS-0001" based on hello collection definition
await client.CreateDocumentAsync(
    UriFactory.CreateDocumentCollectionUri("db", "coll"),
    new DeviceReading
    {
        Id = "XMS-001-FE24C",
        DeviceId = "XMS-0001",
        MetricType = "Temperature",
        MetricValue = 105.00,
        Unit = "Fahrenheit",
        ReadingTime = DateTime.UtcNow
    });
```

<span data-ttu-id="5ad3f-147">Şimdi hello öğe kimliği ve bölüm anahtarı tarafından okunur, güncelleştirebilir ve son adım olarak kimliği ve bölüm anahtarı ile silin. Merhaba okuma PartitionKey değeri içerdiğini unutmayın (karşılık gelen toohello `x-ms-documentdb-partitionkey` hello REST API istek üstbilgisinde).</span><span class="sxs-lookup"><span data-stu-id="5ad3f-147">Let's read hello item by its partition key and id, update it, and then as a final step, delete it by partition key and id. Note that hello reads include a PartitionKey value (corresponding toohello `x-ms-documentdb-partitionkey` request header in hello REST API).</span></span>

```csharp
// Read document. Needs hello partition key and hello ID toobe specified
Document result = await client.ReadDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  new RequestOptions { PartitionKey = new PartitionKey("XMS-0001") });

DeviceReading reading = (DeviceReading)(dynamic)result;

// Update hello document. Partition key is not required, again extracted from hello document
reading.MetricValue = 104;
reading.ReadingTime = DateTime.UtcNow;

await client.ReplaceDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  reading);

// Delete document. Needs partition key
await client.DeleteDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  new RequestOptions { PartitionKey = new PartitionKey("XMS-0001") });
```

### <a name="querying-partitioned-containers"></a><span data-ttu-id="5ad3f-148">Bölümlenmiş kapsayıcıları sorgulama</span><span class="sxs-lookup"><span data-stu-id="5ad3f-148">Querying partitioned containers</span></span>
<span data-ttu-id="5ad3f-149">Bölümlenmiş kapsayıcılardaki Cosmos DB verilerini otomatik olarak sorgularken yolları (varsa) hello filtrede belirtilen toohello bölüm anahtar değerlerine karşılık gelen sorgu toohello bölümleri hello.</span><span class="sxs-lookup"><span data-stu-id="5ad3f-149">When you query data in partitioned containers, Cosmos DB automatically routes hello query toohello partitions corresponding toohello partition key values specified in hello filter (if there are any).</span></span> <span data-ttu-id="5ad3f-150">Örneğin, bu sorgu yönlendirilmiş toojust hello bölüm içeren hello bölüm anahtarı "XMS-0001" olur.</span><span class="sxs-lookup"><span data-stu-id="5ad3f-150">For example, this query is routed toojust hello partition containing hello partition key "XMS-0001".</span></span>

```csharp
// Query using partition key
IQueryable<DeviceReading> query = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"))
    .Where(m => m.MetricType == "Temperature" && m.DeviceId == "XMS-0001");
```
    
<span data-ttu-id="5ad3f-151">Merhaba aşağıdaki sorguyu hello bölüm anahtarı (DeviceID) üzerinde bir filtre yok ve hello bölümünün dizin karşı yürütüldüğü tooall bölümleri çıkışı dağıtılmış.</span><span class="sxs-lookup"><span data-stu-id="5ad3f-151">hello following query does not have a filter on hello partition key (DeviceId) and is fanned out tooall partitions where it is executed against hello partition's index.</span></span> <span data-ttu-id="5ad3f-152">Toospecify hello EnableCrossPartitionQuery sahip unutmayın (`x-ms-documentdb-query-enablecrosspartition` hello REST API içinde) toohave hello SDK tooexecute bölümleri arasında bir sorgu.</span><span class="sxs-lookup"><span data-stu-id="5ad3f-152">Note that you have toospecify hello EnableCrossPartitionQuery (`x-ms-documentdb-query-enablecrosspartition` in hello REST API) toohave hello SDK tooexecute a query across partitions.</span></span>

```csharp
// Query across partition keys
IQueryable<DeviceReading> crossPartitionQuery = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"), 
    new FeedOptions { EnableCrossPartitionQuery = true })
    .Where(m => m.MetricType == "Temperature" && m.MetricValue > 100);
```

<span data-ttu-id="5ad3f-153">Cosmos DB destekleyen [toplama işlevlerinin](documentdb-sql-query.md#Aggregates) `COUNT`, `MIN`, `MAX`, `SUM` ve `AVG` üzerinden ve üstü SDK'ları 1.12.0 ile başlayan SQL kullanarak kapsayıcıları bölümlenmiş.</span><span class="sxs-lookup"><span data-stu-id="5ad3f-153">Cosmos DB supports [aggregate functions](documentdb-sql-query.md#Aggregates) `COUNT`, `MIN`, `MAX`, `SUM` and `AVG` over partitioned containers using SQL starting with SDKs 1.12.0 and above.</span></span> <span data-ttu-id="5ad3f-154">Sorguları tek bir toplama işleci içermelidir ve hello projeksiyon tek bir değer içermelidir.</span><span class="sxs-lookup"><span data-stu-id="5ad3f-154">Queries must include a single aggregate operator, and must include a single value in hello projection.</span></span>

### <a name="parallel-query-execution"></a><span data-ttu-id="5ad3f-155">Paralel sorgu yürütme</span><span class="sxs-lookup"><span data-stu-id="5ad3f-155">Parallel query execution</span></span>
<span data-ttu-id="5ad3f-156">Merhaba Cosmos DB SDK'ları 1.9.0 ve Destek tooperform düşük gecikme süresi izin paralel sorgu yürütme seçeneklerini sorgular bölümlenmiş koleksiyonlar karşı bile tootouch gerektiğinde çok sayıda bölüm.</span><span class="sxs-lookup"><span data-stu-id="5ad3f-156">hello Cosmos DB SDKs 1.9.0 and above support parallel query execution options, which allow you tooperform low latency queries against partitioned collections, even when they need tootouch a large number of partitions.</span></span> <span data-ttu-id="5ad3f-157">Örneğin, sorgu aşağıdaki hello paralel yapılandırılmış toorun bölümler ' dir.</span><span class="sxs-lookup"><span data-stu-id="5ad3f-157">For example, hello following query is configured toorun in parallel across partitions.</span></span>

```csharp
// Cross-partition Order By Queries
IQueryable<DeviceReading> crossPartitionQuery = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"), 
    new FeedOptions { EnableCrossPartitionQuery = true, MaxDegreeOfParallelism = 10, MaxBufferedItemCount = 100})
    .Where(m => m.MetricType == "Temperature" && m.MetricValue > 100)
    .OrderBy(m => m.MetricValue);
```
    
<span data-ttu-id="5ad3f-158">Şu parametreler hello ayarlama tarafından paralel sorgu yürütme yönetebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="5ad3f-158">You can manage parallel query execution by tuning hello following parameters:</span></span>

* <span data-ttu-id="5ad3f-159">Ayarlayarak `MaxDegreeOfParallelism`, hello paralellik derecesi başka bir deyişle, hello en fazla eşzamanlı ağ bağlantıları toohello kapsayıcının bölüm sayısı kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5ad3f-159">By setting `MaxDegreeOfParallelism`, you can control hello degree of parallelism i.e., hello maximum number of simultaneous network connections toohello container's partitions.</span></span> <span data-ttu-id="5ad3f-160">Bu çok 1 ayarlarsanız, hello paralellik derecesi hello SDK tarafından yönetilir.</span><span class="sxs-lookup"><span data-stu-id="5ad3f-160">If you set this too-1, hello degree of parallelism is managed by hello SDK.</span></span> <span data-ttu-id="5ad3f-161">Merhaba, `MaxDegreeOfParallelism` belirtilmemişse veya ayarlama hello varsayılan değer olan too0 bir tek bir ağ bağlantısı toohello kapsayıcının bölümleri olacaktır.</span><span class="sxs-lookup"><span data-stu-id="5ad3f-161">If hello `MaxDegreeOfParallelism` is not specified or set too0, which is hello default value, there will be a single network connection toohello container's partitions.</span></span>
* <span data-ttu-id="5ad3f-162">Ayarlayarak `MaxBufferedItemCount`, sorgu gecikme süresi ve istemci tarafı bellek kullanımı devre dışı ticari.</span><span class="sxs-lookup"><span data-stu-id="5ad3f-162">By setting `MaxBufferedItemCount`, you can trade off query latency and client-side memory utilization.</span></span> <span data-ttu-id="5ad3f-163">Bu parametreyi veya bu çok 1 ayarlarsanız hello paralel sorgu yürütme sırasında arabelleğe alınan öğe sayısı hello SDK tarafından yönetilir.</span><span class="sxs-lookup"><span data-stu-id="5ad3f-163">If you omit this parameter or set this too-1, hello number of items buffered during parallel query execution is managed by hello SDK.</span></span>

<span data-ttu-id="5ad3f-164">Merhaba verilen aynı duruma hello koleksiyonunun bir paralel sorgu döndürecektir sonuçları seri yürütme olduğu gibi aynı sipariş hello içinde.</span><span class="sxs-lookup"><span data-stu-id="5ad3f-164">Given hello same state of hello collection, a parallel query will return results in hello same order as in serial execution.</span></span> <span data-ttu-id="5ad3f-165">(ORDER BY ve/veya üst) sıralama içeren bir çapraz bölüm sorgusu gerçekleştirirken hello Azure Cosmos DB SDK sorunları paralel sorgu sonuçları genel sıralı hello istemci tarafı tooproduce bölümleri ve birleştirmeler kısmen sıralanmış sonuçlarında arasında hello.</span><span class="sxs-lookup"><span data-stu-id="5ad3f-165">When performing a cross-partition query that includes sorting (ORDER BY and/or TOP), hello Azure Cosmos DB SDK issues hello query in parallel across partitions and merges partially sorted results in hello client side tooproduce globally ordered results.</span></span>

### <a name="executing-stored-procedures"></a><span data-ttu-id="5ad3f-166">Saklı yordamları çalıştırma</span><span class="sxs-lookup"><span data-stu-id="5ad3f-166">Executing stored procedures</span></span>
<span data-ttu-id="5ad3f-167">Belgelerle karşı atomik işlemleri de yürütebilir aynı cihaz kimliği, örneğin hello toplamalar koruma veya hello en son durumunu tek bir öğe bir aygıt.</span><span class="sxs-lookup"><span data-stu-id="5ad3f-167">You can also execute atomic transactions against documents with hello same device ID, e.g. if you're maintaining aggregates or hello latest state of a device in a single item.</span></span> 

```csharp
await client.ExecuteStoredProcedureAsync<DeviceReading>(
    UriFactory.CreateStoredProcedureUri("db", "coll", "SetLatestStateAcrossReadings"),
    new RequestOptions { PartitionKey = new PartitionKey("XMS-001") }, 
    "XMS-001-FE24C");
```
   
<span data-ttu-id="5ad3f-168">Merhaba sonraki bölümde, nasıl toopartitioned kapsayıcıları tek bölümlü kapsayıcılardan taşıyabilir arayın.</span><span class="sxs-lookup"><span data-stu-id="5ad3f-168">In hello next section, we look at how you can move toopartitioned containers from single-partition containers.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5ad3f-169">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5ad3f-169">Next steps</span></span>
<span data-ttu-id="5ad3f-170">Bu makalede, nasıl Azure Cosmos DB kapsayıcıların ile bölümleme ile toowork hello DocumentDB API genel bakış sağlanır.</span><span class="sxs-lookup"><span data-stu-id="5ad3f-170">In this article, we provided an overview of how toowork with partitioning of Azure Cosmos DB containers with hello DocumentDB API.</span></span> <span data-ttu-id="5ad3f-171">Ayrıca bkz. [bölümlendirme ve yatay ölçekleme](../cosmos-db/partition-data.md) genel bir bakış kavramları ve tüm Azure Cosmos DB API'si ile bölümleme için en iyi uygulamalar için.</span><span class="sxs-lookup"><span data-stu-id="5ad3f-171">Also see [partitioning and horizontal scaling](../cosmos-db/partition-data.md) for an overview of concepts and best practices for partitioning with any Azure Cosmos DB API.</span></span> 

* <span data-ttu-id="5ad3f-172">Ölçek ve performans ile Azure Cosmos DB testi gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="5ad3f-172">Perform scale and performance testing with Azure Cosmos DB.</span></span> <span data-ttu-id="5ad3f-173">Bkz: [performans ve ölçek testi Azure Cosmos DB ile](performance-testing.md) bir örnek için.</span><span class="sxs-lookup"><span data-stu-id="5ad3f-173">See [Performance and Scale Testing with Azure Cosmos DB](performance-testing.md) for a sample.</span></span>
* <span data-ttu-id="5ad3f-174">Kodlama Hello ile çalışmaya başlama [SDK'ları](documentdb-sdk-dotnet.md) veya hello [REST API'si](/rest/api/documentdb/)</span><span class="sxs-lookup"><span data-stu-id="5ad3f-174">Get started coding with hello [SDKs](documentdb-sdk-dotnet.md) or hello [REST API](/rest/api/documentdb/)</span></span>
* <span data-ttu-id="5ad3f-175">Hakkında bilgi edinin [Azure Cosmos veritabanı sağlanan işleme](request-units.md)</span><span class="sxs-lookup"><span data-stu-id="5ad3f-175">Learn about [provisioned throughput in Azure Cosmos DB](request-units.md)</span></span>

