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
# <a name="partitioning-in-azure-cosmos-db-using-hello-documentdb-api"></a>Merhaba DocumentDB API kullanarak Azure Cosmos DB içinde bölümlendirme

[Microsoft Azure Cosmos DB](../cosmos-db/introduction.md) ulaşmanıza hızlı ve tahmin edilebilir performansı ve ölçeği sorunsuz bir şekilde uygulamanızı yanı sıra, büyüdükçe Genel dağıtılmış, birden çok model veritabanı tasarlanan hizmet toohelp değil. 

Bu makalede nasıl ile Cosmos DB kapsayıcıların bölümlendirme ile toowork hello DocumentDB API genel bir bakış sağlar. Bkz: [bölümlendirme ve yatay ölçekleme](../cosmos-db/partition-data.md) genel bir bakış kavramları ve tüm Azure Cosmos DB API'si ile bölümleme için en iyi uygulamalar için. 

tooget kodu ile başlatıldı, hello projesinden indirmeniz [Github](https://github.com/Azure/azure-documentdb-dotnet/tree/a2d61ddb53f8ab2a23d3ce323c77afcf5a608f52/samples/documentdb-benchmark). 

Bu makaleyi okuduktan sonra aşağıdaki soruları mümkün tooanswer hello olacaktır:   

* Nasıl yapılır Azure Cosmos veritabanı bölümleme iş?
* Azure Cosmos DB'de bölümleme nasıl yapılandırabilirim
* Bölüm anahtarlarını nedir ve nasıl ı hello sağ bölüm anahtarı Uygulamam için çekme?

tooget kodu ile başlatıldı, hello projesinden indirmeniz [Azure Cosmos DB performans testi sürücü örnek](https://github.com/Azure/azure-documentdb-dotnet/tree/a2d61ddb53f8ab2a23d3ce323c77afcf5a608f52/samples/documentdb-benchmark). 

<!-- placeholder until we have a permanent solution-->
<a name="partition-keys"></a>
<a name="single-partition-and-partitioned-collections"></a>
<a name="migrating-from-single-partition"></a>

## <a name="partition-keys"></a>Bölüm anahtarlarını

Hello DocumentDB API, JSON yolu hello biçiminde hello bölüm anahtar tanımı belirtin. Merhaba aşağıdaki tabloda bölüm temel tanımları ve tooeach karşılık gelen hello değerleri örnekleri gösterilmektedir. Merhaba bölüm anahtarı belirtilen bir yolu olarak örneğin `/department` temsil hello özelliği departman. 

<table border="0" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td valign="top"><p><strong>Bölüm anahtarı</strong></p></td>
            <td valign="top"><p><strong>Açıklama</strong></p></td>
        </tr>
        <tr>
            <td valign="top"><p>/Department</p></td>
            <td valign="top"><p>Belge hello öğesi olduğu doc.department toohello değeri karşılık gelir.</p></td>
        </tr>
        <tr>
            <td valign="top"><p>/ Özellikler/adı</p></td>
            <td valign="top"><p>Belge hello öğesi (iç içe özellik) olduğu doc.properties.name toohello değeri karşılık gelir.</p></td>
        </tr>
        <tr>
            <td valign="top"><p>/ID</p></td>
            <td valign="top"><p>Doc.id toohello değeri karşılık gelir (kimliği ve bölüm anahtarı aynı hello olan özelliği).</p></td>
        </tr>
        <tr>
            <td valign="top"><p>/ "bölüm adı"</p></td>
            <td valign="top"><p>Belge hello öğesi olduğu belge ["bölüm adı"] değerini toohello karşılık gelir.</p></td>
        </tr>
    </tbody>
</table>

> [!NOTE]
> toohello özellik başlangıç değeri yerine karşılık gelen ilke yolları, yol hello hello anahtar farkı dizin oluşturma için bölüm anahtarı hello sözdizimi benzer toohello yol belirtimi, yani var. hiçbir joker hello sonunda. Örneğin, / bölüm/belirtirsiniz? tooindex hello departmanı altında değerleri, ancak /department hello bölüm anahtar tanımı olarak belirtin. Merhaba bölüm anahtarı örtük olarak dizine alınır ve dizin oluşturma ilkesi geçersiz kılmaları kullanarak dizin dışarıda bırakılamaz.
> 
> 

Bölüm anahtarı hello seçimine hello uygulamanızın performansını nasıl etkilediğini adresindeki bakalım.

## <a name="working-with-hello-azure-cosmos-db-sdks"></a>Hello Azure Cosmos DB SDK'ları ile çalışma
Azure Cosmos DB ile otomatik bölümleme için destek eklenmiştir [REST API sürümü 2015-12-16](/rest/api/documentdb/). Sipariş bölümlenmiş toocreate kapsayıcılarında SDK sürümleri 1.6.0 indirmeniz gerekir veya daha yeni bir hello desteklenen SDK'sı platformlar (.NET, Node.js, Java, Python, MongoDB). 

### <a name="creating-containers"></a>Kapsayıcıları oluşturma
Merhaba aşağıdaki örnek .NET parçacığı toocreate bir kapsayıcı toostore cihaz telemetri verileri işleme saniye başına 20.000 istek birimlerinin gösterir. Merhaba SDK ayarlar hello OfferThroughput değeri (hangi sırayla ayarlar hello `x-ms-offer-throughput` hello REST API istek üstbilgisinde). Merhaba burada ayarlarız `/deviceId` hello bölüm anahtarı olarak. Bölüm anahtarı Hello seçimine hello kapsayıcı meta verilerinin adı ve dizin oluşturma ilkesini gibi hello rest birlikte kaydedilir.

Bu örnek için biz çekilen `deviceId` (a) olduğundan çok sayıda aygıtlar, biliyoruz olduğundan, yazma dağıtılabilir bölümleri arasında eşit olarak ve tooscale hello veritabanı tooingest büyük miktarda veriyi ve (b) birçok hello istekleri ister bize izin verme Merhaba son okuma getirme bir aygıt için kapsamlı tooa tek DeviceID olan ve tek bir bölümün dışında alınabilir.

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

Bu yöntem tooCosmos DB çağrısı bir REST API yapar ve hello hizmet hello istenen işlemeyi temel alan bölüm sayısı hazırlayacağınız. Performansınızı gelişmesi gerektiği bir kapsayıcı hello verimini değiştirebilirsiniz. 

### <a name="reading-and-writing-items"></a>Okuma ve yazma öğeleri
Şimdi, şimdi Cosmos Veritabanına veri ekleyin. Bir aygıt okuma ve çağrısı tooCreateDocumentAsync tooinsert bir kapsayıcıya okuma yeni bir cihaz içeren bir örnek sınıf İşte. Bu, hello DocumentDB API yararlanan bir örnektir:

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

Şimdi hello öğe kimliği ve bölüm anahtarı tarafından okunur, güncelleştirebilir ve son adım olarak kimliği ve bölüm anahtarı ile silin. Merhaba okuma PartitionKey değeri içerdiğini unutmayın (karşılık gelen toohello `x-ms-documentdb-partitionkey` hello REST API istek üstbilgisinde).

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

### <a name="querying-partitioned-containers"></a>Bölümlenmiş kapsayıcıları sorgulama
Bölümlenmiş kapsayıcılardaki Cosmos DB verilerini otomatik olarak sorgularken yolları (varsa) hello filtrede belirtilen toohello bölüm anahtar değerlerine karşılık gelen sorgu toohello bölümleri hello. Örneğin, bu sorgu yönlendirilmiş toojust hello bölüm içeren hello bölüm anahtarı "XMS-0001" olur.

```csharp
// Query using partition key
IQueryable<DeviceReading> query = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"))
    .Where(m => m.MetricType == "Temperature" && m.DeviceId == "XMS-0001");
```
    
Merhaba aşağıdaki sorguyu hello bölüm anahtarı (DeviceID) üzerinde bir filtre yok ve hello bölümünün dizin karşı yürütüldüğü tooall bölümleri çıkışı dağıtılmış. Toospecify hello EnableCrossPartitionQuery sahip unutmayın (`x-ms-documentdb-query-enablecrosspartition` hello REST API içinde) toohave hello SDK tooexecute bölümleri arasında bir sorgu.

```csharp
// Query across partition keys
IQueryable<DeviceReading> crossPartitionQuery = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"), 
    new FeedOptions { EnableCrossPartitionQuery = true })
    .Where(m => m.MetricType == "Temperature" && m.MetricValue > 100);
```

Cosmos DB destekleyen [toplama işlevlerinin](documentdb-sql-query.md#Aggregates) `COUNT`, `MIN`, `MAX`, `SUM` ve `AVG` üzerinden ve üstü SDK'ları 1.12.0 ile başlayan SQL kullanarak kapsayıcıları bölümlenmiş. Sorguları tek bir toplama işleci içermelidir ve hello projeksiyon tek bir değer içermelidir.

### <a name="parallel-query-execution"></a>Paralel sorgu yürütme
Merhaba Cosmos DB SDK'ları 1.9.0 ve Destek tooperform düşük gecikme süresi izin paralel sorgu yürütme seçeneklerini sorgular bölümlenmiş koleksiyonlar karşı bile tootouch gerektiğinde çok sayıda bölüm. Örneğin, sorgu aşağıdaki hello paralel yapılandırılmış toorun bölümler ' dir.

```csharp
// Cross-partition Order By Queries
IQueryable<DeviceReading> crossPartitionQuery = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"), 
    new FeedOptions { EnableCrossPartitionQuery = true, MaxDegreeOfParallelism = 10, MaxBufferedItemCount = 100})
    .Where(m => m.MetricType == "Temperature" && m.MetricValue > 100)
    .OrderBy(m => m.MetricValue);
```
    
Şu parametreler hello ayarlama tarafından paralel sorgu yürütme yönetebilirsiniz:

* Ayarlayarak `MaxDegreeOfParallelism`, hello paralellik derecesi başka bir deyişle, hello en fazla eşzamanlı ağ bağlantıları toohello kapsayıcının bölüm sayısı kontrol edebilirsiniz. Bu çok 1 ayarlarsanız, hello paralellik derecesi hello SDK tarafından yönetilir. Merhaba, `MaxDegreeOfParallelism` belirtilmemişse veya ayarlama hello varsayılan değer olan too0 bir tek bir ağ bağlantısı toohello kapsayıcının bölümleri olacaktır.
* Ayarlayarak `MaxBufferedItemCount`, sorgu gecikme süresi ve istemci tarafı bellek kullanımı devre dışı ticari. Bu parametreyi veya bu çok 1 ayarlarsanız hello paralel sorgu yürütme sırasında arabelleğe alınan öğe sayısı hello SDK tarafından yönetilir.

Merhaba verilen aynı duruma hello koleksiyonunun bir paralel sorgu döndürecektir sonuçları seri yürütme olduğu gibi aynı sipariş hello içinde. (ORDER BY ve/veya üst) sıralama içeren bir çapraz bölüm sorgusu gerçekleştirirken hello Azure Cosmos DB SDK sorunları paralel sorgu sonuçları genel sıralı hello istemci tarafı tooproduce bölümleri ve birleştirmeler kısmen sıralanmış sonuçlarında arasında hello.

### <a name="executing-stored-procedures"></a>Saklı yordamları çalıştırma
Belgelerle karşı atomik işlemleri de yürütebilir aynı cihaz kimliği, örneğin hello toplamalar koruma veya hello en son durumunu tek bir öğe bir aygıt. 

```csharp
await client.ExecuteStoredProcedureAsync<DeviceReading>(
    UriFactory.CreateStoredProcedureUri("db", "coll", "SetLatestStateAcrossReadings"),
    new RequestOptions { PartitionKey = new PartitionKey("XMS-001") }, 
    "XMS-001-FE24C");
```
   
Merhaba sonraki bölümde, nasıl toopartitioned kapsayıcıları tek bölümlü kapsayıcılardan taşıyabilir arayın.

## <a name="next-steps"></a>Sonraki adımlar
Bu makalede, nasıl Azure Cosmos DB kapsayıcıların ile bölümleme ile toowork hello DocumentDB API genel bakış sağlanır. Ayrıca bkz. [bölümlendirme ve yatay ölçekleme](../cosmos-db/partition-data.md) genel bir bakış kavramları ve tüm Azure Cosmos DB API'si ile bölümleme için en iyi uygulamalar için. 

* Ölçek ve performans ile Azure Cosmos DB testi gerçekleştirin. Bkz: [performans ve ölçek testi Azure Cosmos DB ile](performance-testing.md) bir örnek için.
* Kodlama Hello ile çalışmaya başlama [SDK'ları](documentdb-sdk-dotnet.md) veya hello [REST API'si](/rest/api/documentdb/)
* Hakkında bilgi edinin [Azure Cosmos veritabanı sağlanan işleme](request-units.md)

