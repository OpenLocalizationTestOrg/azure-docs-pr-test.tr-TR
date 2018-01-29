---
title: "Bölümlendirme ve Azure Cosmos DB'de ölçeklendirme | Microsoft Docs"
description: "Azure Cosmos DB, bölümleme yapılandırmak ve anahtarları bölümlemek nasıl ve uygulamanız için doğru bölüm anahtarı almak nasıl bölümleme nasıl çalıştığı hakkında bilgi edinin."
services: cosmos-db
author: rafats
manager: jhubbard
documentationcenter: 
ms.assetid: 702c39b4-1798-48dd-9993-4493a2f6df9e
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/24/2017
ms.author: rafats
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: bfed50eef02c237ce0ea4480e2e208f2e61ccbef
ms.sourcegitcommit: 0e4491b7fdd9ca4408d5f2d41be42a09164db775
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/14/2017
---
# <a name="partitioning-in-azure-cosmos-db-using-the-sql-api"></a>Azure Cosmos SQL API'yi kullanarak DB'de bölümlendirme

[!INCLUDE [cosmos-db-sql-api](../../includes/cosmos-db-sql-api.md)]

[Microsoft Azure Cosmos DB](../cosmos-db/introduction.md) büyüdüğü gibi hızlı ve tahmin edilebilir performansı ve ölçeği sorunsuz bir şekilde uygulamanızı yanı sıra ulaşmak yardımcı olmak için tasarlanmış bir genel dağıtılmış, birden çok model veritabanı hizmetidir. 

Bu makalede SQL API ile Cosmos DB kapsayıcıların bölümlendirme ile çalışmak nasıl bir bakış sağlar. Bkz: [bölümlendirme ve yatay ölçekleme](../cosmos-db/partition-data.md) genel bir bakış kavramları ve tüm Azure Cosmos DB API'si ile bölümleme için en iyi uygulamalar için. 

Kodu ile çalışmaya başlamak için projesinden indirmeniz [Github](https://github.com/Azure/azure-documentdb-dotnet/tree/a2d61ddb53f8ab2a23d3ce323c77afcf5a608f52/samples/documentdb-benchmark). 

Bu makaleyi okuduktan sonra aşağıdaki soruları yanıtlayın mümkün olacaktır:   

* Nasıl yapılır Azure Cosmos veritabanı bölümleme iş?
* Azure Cosmos DB'de bölümleme nasıl yapılandırabilirim
* Bölüm anahtarlarını nedir ve nasıl t sağ bölüm anahtarı Uygulamam için çekme?

Kodu ile çalışmaya başlamak için projesinden indirmeniz [Azure Cosmos DB performans testi sürücü örnek](https://github.com/Azure/azure-documentdb-dotnet/tree/a2d61ddb53f8ab2a23d3ce323c77afcf5a608f52/samples/documentdb-benchmark). 

<!-- placeholder until we have a permanent solution-->
<a name="partition-keys"></a>
<a name="single-partition-and-partitioned-collections"></a>
<a name="migrating-from-single-partition"></a>

## <a name="partition-keys"></a>Bölüm anahtarlarını

SQL API bölüm anahtar tanımı JSON yolu biçiminde belirtin. Aşağıdaki tabloda bölüm temel tanımları ve her birine karşılık gelen değerleri örnekleri gösterilmektedir. Bölüm anahtarı örneğin bir yolu olarak belirtilen `/department` özelliği departmanı temsil eder. 

<table border="0" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td valign="top"><p><strong>Bölüm anahtarı</strong></p></td>
            <td valign="top"><p><strong>Açıklama</strong></p></td>
        </tr>
        <tr>
            <td valign="top"><p>/Department</p></td>
            <td valign="top"><p>Belge öğesi olduğu doc.department değerine karşılık gelir.</p></td>
        </tr>
        <tr>
            <td valign="top"><p>/ Özellikler/adı</p></td>
            <td valign="top"><p>Doc (iç içe özellik) öğesi olduğu doc.properties.name değerine karşılık gelir.</p></td>
        </tr>
        <tr>
            <td valign="top"><p>/ID</p></td>
            <td valign="top"><p>Doc.id değerine karşılık gelir (kimliği ve bölüm anahtarı olan aynı özelliğe).</p></td>
        </tr>
        <tr>
            <td valign="top"><p>/ "bölüm adı"</p></td>
            <td valign="top"><p>Belge öğesi olduğu belge ["bölüm adı"] değerine karşılık gelir.</p></td>
        </tr>
    </tbody>
</table>

> [!NOTE]
> Bölüm anahtarı sözdizimi İlkesi yollarını yolun özellik değeri yerine karşılık gelen en önemli fark ile dizin oluşturma için yol belirtimi benzer, yani hiçbir joker sonunda. Örneğin, / bölüm/belirtirsiniz? Departman altındaki değerleri dizine ancak /department bölüm anahtar tanımı belirtin. Bölüm anahtarı örtük olarak dizine alınır ve dizin oluşturma ilkesi geçersiz kılmaları kullanarak dizin dışarıda bırakılamaz.
> 
> 

Bölüm anahtarı seçimi, uygulamanızın performansını nasıl etkilediğini konumundaki bakalım.

## <a name="working-with-the-azure-cosmos-db-sdks"></a>Azure Cosmos DB SDK'ları ile çalışma
Azure Cosmos DB ile otomatik bölümleme için destek eklenmiştir [REST API sürümü 2015-12-16](/rest/api/documentdb/). Bölümlenmiş kapsayıcıları oluşturmak için SDK sürümleri 1.6.0 karşıdan ya da daha yeni bir desteklenen SDK'sı platformlar (.NET, Node.js, Java, Python, MongoDB). 

### <a name="creating-containers"></a>Kapsayıcıları oluşturma
Aşağıdaki örnek, üretilen iş saniye başına 20.000 istek birimlerinin cihaz telemetri verilerini depolamak için bir kapsayıcı oluşturmak için bir .NET parçacığı gösterir. SDK OfferThroughput değeri ayarlar (hangi sırayla ayarlar `x-ms-offer-throughput` REST API istek üstbilgisinde). Burada `/deviceId` bölüm anahtarı olarak. Bölüm anahtarı seçimi kapsayıcı meta veri adı ve dizin oluşturma ilkesini gibi rest birlikte kaydedilir.

Bu örnek için biz çekilen `deviceId` (a) olduğundan çok sayıda aygıtlar, biliyoruz olduğundan, yazma dağıtılabilir bölümleri arasında eşit olarak ve bize izin vererek büyük miktarda veriyi almak için veritabanı ölçeklendirme ve (b) birçok cihazı için en son okuma getirme gibi istekleri için tek bir DeviceID kapsamlı ve tek bir bölümün dışında alınabilir.

```csharp
DocumentClient client = new DocumentClient(new Uri(endpoint), authKey);
await client.CreateDatabaseAsync(new Database { Id = "db" });

// Container for device telemetry. Here the property deviceId will be used as the partition key to 
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

Bu yöntem Cosmos DB çağrısı bir REST API yapar ve hizmet istenen işlemeyi temel alan bölüm sayısı hazırlayacağınız. Performansınızı gelişmesi gerektiği bir kapsayıcı verimini değiştirebilirsiniz. 

### <a name="reading-and-writing-items"></a>Okuma ve yazma öğeleri
Şimdi, şimdi Cosmos Veritabanına veri ekleyin. İşte, okuma cihaz içeren bir örnek sınıf ve Documentclient bir kapsayıcıya okuma yeni aygıt eklemek için bir çağrı. Bu, SQL API'yi yararlanan bir örnektir:

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

// Create a document. Here the partition key is extracted as "XMS-0001" based on the collection definition
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

Şimdi öğe kimliği ve bölüm anahtarı tarafından okunur, güncelleştirebilir ve son adım olarak kimliği ve bölüm anahtarı ile silin. Okumaları PartitionKey değeri içerdiğini unutmayın (karşılık gelen `x-ms-documentdb-partitionkey` REST API istek üstbilgisinde).

```csharp
// Read document. Needs the partition key and the ID to be specified
Document result = await client.ReadDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  new RequestOptions { PartitionKey = new PartitionKey("XMS-0001") });

DeviceReading reading = (DeviceReading)(dynamic)result;

// Update the document. Partition key is not required, again extracted from the document
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

### <a name="querying-partitioned-containers"></a>Bölümlenmiş kapsayıcıları sorgulama
Bölümlenmiş kapsayıcıları verileri sorguladığınızda Cosmos DB sorgu otomatik olarak (varsa) filtrede belirtilen bölüm anahtarı değerine karşılık gelen bölümleri yönlendirir. Örneğin, bu sorgu "XMS-0001" Bölüm anahtarı içeren bölümün yalnızca yönlendirilir.

```csharp
// Query using partition key
IQueryable<DeviceReading> query = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"))
    .Where(m => m.MetricType == "Temperature" && m.DeviceId == "XMS-0001");
```
    
Aşağıdaki sorgu bir filtre bölüm anahtarı (DeviceID) sahip değil ve bölümün dizin karşı yürütüldüğü tüm bölümler için Dağıtılmış. EnableCrossPartitionQuery belirtmek zorunda Not (`x-ms-documentdb-query-enablecrosspartition` REST API'sindeki) SDK'sını bölümler bir sorguyu çalıştırmak için.

```csharp
// Query across partition keys
IQueryable<DeviceReading> crossPartitionQuery = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"), 
    new FeedOptions { EnableCrossPartitionQuery = true })
    .Where(m => m.MetricType == "Temperature" && m.MetricValue > 100);
```

Cosmos DB destekleyen [toplama işlevlerinin](sql-api-sql-query.md#Aggregates) `COUNT`, `MIN`, `MAX`, `SUM` ve `AVG` üzerinden ve üstü SDK'ları 1.12.0 ile başlayan SQL kullanarak kapsayıcıları bölümlenmiş. Sorguları tek bir toplama işleci içermelidir ve projeksiyon tek bir değer içermelidir.

### <a name="parallel-query-execution"></a>Paralel sorgu yürütme
Cosmos DB SDK'ları 1.9.0 ve hatta bunlar çok sayıda bölüm touch gerektiğinde bölümlenmiş koleksiyonlar, düşük gecikme süresi sorguları gerçekleştirmesine izin destek paralel sorgu yürütme seçenekleri üstünde. Örneğin, aşağıdaki sorguyu bölümler paralel olarak çalıştırmak için yapılandırılır.

```csharp
// Cross-partition Order By Queries
IQueryable<DeviceReading> crossPartitionQuery = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"), 
    new FeedOptions { EnableCrossPartitionQuery = true, MaxDegreeOfParallelism = 10, MaxBufferedItemCount = 100})
    .Where(m => m.MetricType == "Temperature" && m.MetricValue > 100)
    .OrderBy(m => m.MetricValue);
```
    
Aşağıdaki parametreleri ayarlama tarafından paralel sorgu yürütme yönetebilirsiniz:

* Ayarlayarak `MaxDegreeOfParallelism`, yani, en fazla eşzamanlı ağ bağlantı sayısı kapsayıcının bölümlere paralellik derecesini kontrol edebilirsiniz. Bu ayar, -1 olarak paralellik derecesini SDK tarafından yönetilir. Varsa `MaxDegreeOfParallelism` varsayılan değer, belirtilen veya ayarlanmış 0 değil, tek bir ağ bağlantısı kapsayıcının bölümlere olacaktır.
* Ayarlayarak `MaxBufferedItemCount`, sorgu gecikme süresi ve istemci tarafı bellek kullanımı devre dışı ticari. Bu parametreyi veya bu ayarlarsanız -1 olarak paralel sorgu yürütme sırasında arabelleğe alınan öğe sayısı SDK tarafından yönetilir.

Koleksiyon aynı durumu verildiğinde, paralel sorgu sonuçları seri yürütme olduğu gibi aynı sırada döndürür. (ORDER BY ve/veya üst) sıralama içeren bir çapraz bölüm sorgusu gerçekleştirirken Azure Cosmos DB SDK'sı paralel sorguda bölümler sorunları ve genel olarak sipariş edilen sonuçlar için istemci tarafı kısmen sıralanmış sonuçları birleştirir.

### <a name="executing-stored-procedures"></a>Saklı yordamları çalıştırma
Örneğin aynı cihaz kimliği belgelerle karşı atomik işlemleri yürütebilir toplamalar veya tek bir öğe bir aygıtta en son durumunu koruma durumunda. 

```csharp
await client.ExecuteStoredProcedureAsync<DeviceReading>(
    UriFactory.CreateStoredProcedureUri("db", "coll", "SetLatestStateAcrossReadings"),
    new RequestOptions { PartitionKey = new PartitionKey("XMS-001") }, 
    "XMS-001-FE24C");
```
   
Sonraki bölümde, nasıl bölümlenmiş kapsayıcılara tek bölümlü kapsayıcılardan taşıyabilir arayın.

## <a name="next-steps"></a>Sonraki adımlar
Bu makalede, SQL API ile Azure Cosmos DB kapsayıcıların bölümlendirme ile çalışmak nasıl bir genel bakış sağlanır. Ayrıca bkz. [bölümlendirme ve yatay ölçekleme](../cosmos-db/partition-data.md) genel bir bakış kavramları ve tüm Azure Cosmos DB API'si ile bölümleme için en iyi uygulamalar için. 

* Ölçek ve performans ile Azure Cosmos DB testi gerçekleştirin. Bkz: [performans ve ölçek testi Azure Cosmos DB ile](performance-testing.md) bir örnek için.
* Kodlama ile çalışmaya başlama [SDK'ları](sql-api-sdk-dotnet.md) veya [REST API'si](/rest/api/documentdb/)
* Hakkında bilgi edinin [Azure Cosmos veritabanı sağlanan işleme](request-units.md)

