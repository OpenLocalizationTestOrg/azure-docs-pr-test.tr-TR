---
title: "Azure Cosmos DB: Merhaba DocumentDB API .NET geliştirme | Microsoft Docs"
description: "Bilgi nasıl toodevelop Azure Cosmos veritabanı DocumentDB .NET kullanarak API ile"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: cosmos-db
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 05/10/2017
ms.author: mimig
ms.custom: mvc
ms.openlocfilehash: 0d3d17afa782054c8fdf3cbac421e5a5d0a6800c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmosdb-develop-with-hello-documentdb-api-in-net"></a>Azure CosmosDB: hello .NET API DocumentDB ile geliştirme

Azure Cosmos DB, Microsoft'un genel olarak dağıtılmış çok modelli veritabanı hizmetidir. Hızlı bir şekilde oluşturmak ve belge, anahtar/değer ve grafik veritabanları, her biri hello genel dağıtım ve yatay ölçek özelliklerini Azure Cosmos DB'nin hello çekirdek yararlı sorgulayabilirsiniz. 

Bu öğretici nasıl toocreate bir Azure Cosmos DB hesabı kullanarak Azure portal hello ve ardından bir belge veritabanı ve koleksiyonu oluşturun gösterir bir [bölüm anahtarı](documentdb-partition-data.md#partition-keys) hello kullanarak [DocumentDB .NET API](documentdb-introduction.md). Verilerinizi büyüdükçe bir koleksiyon oluşturduğunuzda bir bölüm anahtarı tanımlayarak, uygulamanızın tooscale harcamadan hazırlanır. 

Bu öğretici kapsar hello aşağıdaki görevleri hello kullanarak [DocumentDB .NET API](documentdb-sdk-dotnet.md):

> [!div class="checklist"]
> * Azure Cosmos DB hesabı oluşturma
> * Bir bölüm anahtarının bir veritabanınızı ve koleksiyonunuzu oluşturun
> * JSON belgeleri oluşturma
> * Bir belgeyi güncelleştirme
> * Bölümlenmiş koleksiyonlar sorgulama
> * Saklı yordamları çalıştırma
> * Bir belgeyi silme
> * Bir veritabanını silin

## <a name="prerequisites"></a>Ön koşullar
Merhaba aşağıdaki sahip olduğunuzdan emin olun:

* Etkin bir Azure hesabı. Bir aboneliğiniz yoksa [ücretsiz bir hesap](https://azure.microsoft.com/free/) için kaydolabilirsiniz. 
    * Alternatif olarak, hello kullanabilirsiniz [Azure Cosmos DB öykünücüsü](local-emulator.md) toouse hello Azure DocumentDB hizmetinin Geliştirme amaçlı öykünen yerel bir ortam isterseniz bu öğretici için.
* [Visual Studio](http://www.visualstudio.com/).

## <a name="create-an-azure-cosmos-db-account"></a>Azure Cosmos DB hesabı oluşturma

Hello Azure portalında bir Azure Cosmos DB hesabı oluşturarak başlayalım.

> [!TIP]
> * Zaten Azure Cosmos DB hesabınız var mı? Bu durumda, İleri çok atlayabilirsiniz[, Visual Studio çözümü ayarlama](#SetupVS)
> * Bir Azure DocumentDB hesabına sahip miydiniz? Bu nedenle, hesabınızı şimdi bir Azure Cosmos DB hesabı ise ve şimdi çok atlayabilirsiniz[, Visual Studio çözümü ayarlama](#SetupVS).  
> * Hello Azure Cosmos DB öykünücüsü kullanıyorsanız, lütfen hello adımları izleyin [Azure Cosmos DB öykünücüsü](local-emulator.md) toosetup öykünücüsü hello ve İleri çok atlayabilirsiniz[, Visual Studio çözümünü kurmak](#SetupVS). 
>
>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a id="SetupVS"></a>Visual Studio çözümünüzü kurma
1. Bilgisayarınızda **Visual Studio**'yu açın.
2. Merhaba üzerinde **dosya** menüsünde, select **yeni**ve ardından **proje**.
3. Merhaba, **yeni proje** iletişim kutusunda **şablonları** / **Visual C#** / **konsol uygulaması (.NET Framework)**, projenizi adlandırın ve ardından **Tamam**.
   ![Merhaba yeni proje penceresinin ekran görüntüsü](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-new-project-2.png)

4. Merhaba, **Çözüm Gezgini**, Visual Studio çözümünüzün yeni konsol uygulamanızın üzerinde sağ tıklayın ve ardından **NuGet paketlerini Yönet...**
    
    ![Merhaba sağ tıklama menüsünün hello proje için ekran görüntüsü](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-manage-nuget-pacakges.png)
5. Merhaba, **NuGet** sekmesini tıklatın, **Gözat**ve türü **documentdb** hello arama kutusuna.
<!---stopped here--->
6. Merhaba sonuçları içinde bulmak **Microsoft.Azure.DocumentDB** tıklatıp **yükleme**.
   Merhaba hello Azure Cosmos DB istemci kitaplığı için paket kimliği [Microsoft.Azure.DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB).
   ![Azure Cosmos DB istemci SDK'sını bulmak için NuGet menüsünün hello ekran görüntüsü](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-manage-nuget-pacakges-2.png)

    Değişiklikleri toohello çözümü gözden geçirme hakkında bir ileti alırsanız tıklatın **Tamam**. Lisans kabulü hakkında bir ileti alırsanız **Kabul ediyorum**'a tıklayın.

## <a id="Connect"></a>Başvuruları tooyour proje ekleyin
Bu öğretici sağla hello DocumentDB API kod parçacıkları gerekli toocreate ve güncelleştirme Azure Cosmos DB kaynakları projenize hello kalan adımları.

İlk olarak, bu başvuruları tooyour uygulama ekleyin.
<!---These aren't added by default when you install hello pkg?--->

```csharp
using System.Net;
using Microsoft.Azure.Documents;
using Microsoft.Azure.Documents.Client;
using Newtonsoft.Json;
```

## <a id="add-references"></a>Uygulamanızı bağlama

Ardından, bu iki sabitleri ekleyin ve *istemci* uygulamanızda değişken.

```csharp
private const string EndpointUrl = "<your endpoint URL>";
private const string PrimaryKey = "<your primary key>";
private DocumentClient client;
```

Head toohello geri [Azure portal](https://portal.azure.com) tooretrieve uç noktasının URL'sini ve birincil anahtar. Merhaba uç noktasının URL'sini ve birincil anahtar, uygulama toounderstand için gerekli olan nerede tooconnect ve Azure Cosmos DB tootrust için uygulamanızın bağlantı.

İçinde Azure portal Merhaba, tooyour Azure Cosmos DB hesap gidin, tıklatın **anahtarları**ve ardından **okuma-yazma anahtarları**.

Merhaba URI hello Portal'dan kopyalayın ve üzerinden yapıştırın `<your endpoint URL>` hello program.cs dosyasındaki. BİRİNCİL anahtar hello portalından hello kopyalayıp üzerinden yapıştırın sonra `<your primary key>`. Emin tooremove hello olması `<` ve `>` , değerlerinden.

![Hello Azure portal ekran görüntüsü bir C# konsol uygulaması hello NoSQL Öğreticisi toocreate tarafından kullanılır. Merhaba hello Azure Cosmos DB hesabı dikey penceresinde, ANAHTARLARI ve hello URI ve birincil anahtar değerlerinin hello anahtarlar dikey penceresinde ile bir Azure Cosmos DB hesabını gösterir](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-keys.png)

## <a id="instantiate"></a>Merhaba DocumentClient örneği

Şimdi, hello yeni bir örneğini oluşturmak **DocumentClient**.

```csharp
DocumentClient client = new DocumentClient(new Uri(endpoint), authKey);
```

## <a id="create-database"></a>Bir veritabanı oluşturun

Ardından, bir Azure Cosmos DB Oluştur [veritabanı](documentdb-resources.md#databases) hello kullanarak [Documentclient](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) yöntemi veya [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) hello yöntemi  **DocumentClient** hello sınıfından [DocumentDB .NET SDK'sı](documentdb-sdk-dotnet.md). Bir veritabanı hello mantıksal, koleksiyonlar genelinde bölümlenmiş JSON belgesi depolama kapsayıcısıdır.

```csharp
await client.CreateDatabaseAsync(new Database { Id = "db" });
```
## <a name="decide-on-a-partition-key"></a>Bir bölüm anahtarı karar verin 

Koleksiyonlar, belgeleri depolamak için kapsayıcılardır. Mantıksal kaynaklar ve yapabilirsiniz [bir veya daha fazla fiziksel bölüm span](partition-data.md). A [bölüm anahtarı](documentdb-partition-data.md) özelliği (veya yol) verileriniz hello sunucuları veya bölümleri arasında kullanılan toodistribute olan belgelerinizi içinde bulunur. Tüm belgeleri aynı bölüm anahtarı depolanır hello ile aynı bölüme hello. 

Bir koleksiyon oluşturmadan önce bir bölüm anahtarı belirleme önemli karar toomake olur. Bölüm anahtarlarını olabilir, belgeler içinde bir özellik (veya yol) olan birden fazla sunucu veya bölümleri arasında verilerinizi Azure Cosmos DB toodistribute tarafından kullanılır. Cosmos DB hello bölüm anahtarı değerini karıştırır ve karma hello sonuç toodetermine hello bölüm hangi toostore hello belgede kullanır. Tüm belgeleri aynı bölüm anahtarı depolanır hello ile aynı bölüme hello ve bölüm anahtarlarını bir koleksiyon oluşturulduktan sonra değiştirilemez. 

Bu öğretici için tooset hello bölüm anahtarı çok yapacağız`/deviceId` bu nedenle, hello tüm hello verileri tek bir cihazı tek bir bölüm içinde depolanır. Toochoose her biri kullanılan değerleri, çok sayıda sahip bir bölüm anahtarı istediğiniz verilerinizi büyür ve hello koleksiyonunun hello tam verimlilik elde adresindeki hello hakkında aynı sıklığı tooensure Cosmos DB yükünü dengelemek. 

Bölümleme hakkında daha fazla bilgi için bkz: [nasıl toopartition ve Azure Cosmos veritabanı ölçek?](partition-data.md) 

## <a id="CreateColl"></a>Bir koleksiyon oluşturma 

Biz bizim bölüm anahtarı bildiğinize göre `/deviceId`, oluşturma sağlayan bir [koleksiyonu](documentdb-resources.md#collections) hello kullanarak [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) yöntemi veya [ CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) hello yöntemi **DocumentClient** sınıfı. Koleksiyon, JSON belgelerinin ve tüm ilişkili JavaScript uygulama mantığının bir kapsayıcısıdır. 

> [!WARNING]
> Üretilen iş ile Azure Cosmos DB hello uygulama toocommunicate için ayırma gibi bir koleksiyon oluşturma, fiyatlandırmaya vardır. Daha fazla ayrıntı için lütfen ziyaret bizim [fiyatlandırma sayfası](https://azure.microsoft.com/pricing/details/cosmos-db/)
> 
> 

```csharp
// Collection for device telemetry. Here hello JSON property deviceId is used  
// as hello partition key toospread across partitions. Configured for 2500 RU/s  
// throughput and an indexing policy that supports sorting against any  
// number or string property. .
DocumentCollection myCollection = new DocumentCollection();
myCollection.Id = "coll";
myCollection.PartitionKey.Paths.Add("/deviceId");

await client.CreateDocumentCollectionAsync(
    UriFactory.CreateDatabaseUri("db"),
    myCollection,
    new RequestOptions { OfferThroughput = 2500 });
```

Bu yöntem yaptığı bir REST API tooAzure Cosmos DB çağırın ve hizmet hükümleri hello istenen işlemeyi temel alan bölüm sayısı hello. Performansınızı hello SDK veya hello kullanarak gelişmesi gibi bir koleksiyon hello verimini değiştirebilirsiniz [Azure portal](set-throughput.md).

## <a id="CreateDoc"></a>JSON belgeleri oluşturma
Şimdi bazı JSON belgeleri Azure Cosmos Veritabanına ekler. A [belge](documentdb-resources.md#documents) hello kullanarak oluşturulan [Documentclient](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) hello yöntemi **DocumentClient** sınıfı. Belgeler, kullanıcı tanımlı (rastgele) JSON içerikleridir. Bu örnek sınıf bir koleksiyona okuma yeni bir cihaz aygıt okuma ve çağrısı tooCreateDocumentAsync tooinsert içerir.

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

// Create a document. Here hello partition key is extracted 
// as "XMS-0001" based on hello collection definition
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
## <a name="read-data"></a>Verileri okuma

Şimdi hello ReadDocumentAsync yöntemi kullanılarak kimliği ve bölüm anahtarı tarafından hello belgeyi okuyun. Merhaba okuma PartitionKey değeri içerdiğini unutmayın (karşılık gelen toohello `x-ms-documentdb-partitionkey` hello REST API istek üstbilgisinde).

```csharp
// Read document. Needs hello partition key and hello Id toobe specified
Document result = await client.ReadDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  new RequestOptions { PartitionKey = new PartitionKey("XMS-0001") });

DeviceReading reading = (DeviceReading)(dynamic)result;
```

## <a name="update-data"></a>Verileri güncelleştirme

Şimdi şimdi hello ReplaceDocumentAsync yöntemini kullanarak bazı verileri güncelleştirin.

```csharp
// Update hello document. Partition key is not required, again extracted from hello document
reading.MetricValue = 104;
reading.ReadingTime = DateTime.UtcNow;

await client.ReplaceDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  reading);
```

## <a name="delete-data"></a>Verileri silme

Şimdi bir belgenin bölüm anahtarı kimliği hello DeleteDocumentAsync yöntemini kullanarak silip olanak sağlar.

```csharp
// Delete a document. hello partition key is required.
await client.DeleteDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  new RequestOptions { PartitionKey = new PartitionKey("XMS-0001") });
```
## <a name="query-partitioned-collections"></a>Bölümlenmiş koleksiyonlar sorgulama

Bölümlenmiş koleksiyonlarda Azure Cosmos DB verileri otomatik olarak sorguladığınızda yolları (varsa) hello filtrede belirtilen toohello bölüm anahtar değerlerine karşılık gelen sorgu toohello bölümleri hello. Örneğin, bu sorgu yönlendirilmiş toojust hello bölüm içeren hello bölüm anahtarı "XMS-0001" olur.

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

## <a name="parallel-query-execution"></a>Paralel sorgu yürütme
Hello Azure Cosmos DB DocumentDB SDK'ları 1.9.0 ve Destek tooperform düşük gecikme süresi izin paralel sorgu yürütme seçeneklerini sorgular bölümlenmiş koleksiyonlar karşı bile tootouch gerektiğinde çok sayıda bölüm. Örneğin, sorgu aşağıdaki hello paralel yapılandırılmış toorun bölümler ' dir.

```csharp
// Cross-partition Order By queries
IQueryable<DeviceReading> crossPartitionQuery = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"), 
    new FeedOptions { EnableCrossPartitionQuery = true, MaxDegreeOfParallelism = 10, MaxBufferedItemCount = 100})
    .Where(m => m.MetricType == "Temperature" && m.MetricValue > 100)
    .OrderBy(m => m.MetricValue);
```
    
Şu parametreler hello ayarlama tarafından paralel sorgu yürütme yönetebilirsiniz:

* Ayarlayarak `MaxDegreeOfParallelism`, hello paralellik derecesi başka bir deyişle, hello en fazla eşzamanlı ağ bağlantıları toohello koleksiyonunun bölüm sayısı kontrol edebilirsiniz. Bu çok 1 ayarlarsanız, hello paralellik derecesi hello SDK tarafından yönetilir. Merhaba, `MaxDegreeOfParallelism` belirtilmemişse veya ayarlama hello varsayılan değer olan too0 bir tek bir ağ bağlantısı toohello koleksiyonunun bölümleri olacaktır.
* Ayarlayarak `MaxBufferedItemCount`, sorgu gecikme süresi ve istemci tarafı bellek kullanımı devre dışı ticari. Bu parametreyi veya bu çok 1 ayarlarsanız hello paralel sorgu yürütme sırasında arabelleğe alınan öğe sayısı hello SDK tarafından yönetilir.

Merhaba verilen aynı duruma hello koleksiyonunun bir paralel sorgu döndürecektir sonuçları seri yürütme olduğu gibi aynı sipariş hello içinde. (ORDER BY ve/veya üst) sıralama içeren bir çapraz bölüm sorgusu gerçekleştirirken hello DocumentDB SDK'sı hello sorgu paralel bölümler sorunları ve genel sonuçları sıralı hello istemci tarafı tooproduce kısmen sıralanmış sonuçları birleştirir.

## <a name="execute-stored-procedures"></a>Saklı yordam yürütme
Son olarak, atomik işlemleri belgelerle karşı yürütebilir aynı cihaz kimliği, örneğin hello toplamalar koruma veya kod tooyour projesi aşağıdaki hello ekleyerek bir cihazı tek bir belgenin en son durumunu hello.

```csharp
await client.ExecuteStoredProcedureAsync<DeviceReading>(
    UriFactory.CreateStoredProcedureUri("db", "coll", "SetLatestStateAcrossReadings"),
    new RequestOptions { PartitionKey = new PartitionKey("XMS-001") }, 
    "XMS-001-FE24C");
```

Ve bu kadar! Merhaba ana bölümleri arasında bir bölüm anahtarı tooefficiently ölçek veri dağıtım kullanan bir Azure Cosmos DB uygulama bileşenlerinin olanlardır.  

## <a name="clean-up-resources"></a>Kaynakları temizleme

Toocontinue toouse bu uygulamayı değil kullanacaksanız, Bu öğretici hello Azure portalında aşağıdaki adımları hello ile oluşturulan tüm kaynakları silin:

1. Merhaba sol taraftaki menüden hello Azure portal'ın, **kaynak grupları** ve benzersiz bir ad hello oluşturduğunuz hello kaynağının'ı tıklatın. 
2. Kaynak grubu sayfanızda tıklatın **silmek**hello metin kutusuna hello kaynak toodelete hello adını yazın ve ardından **silmek**.

## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide, hello aşağıdakileri yaptığınızdan: 

> [!div class="checklist"]
> * Bir Azure Cosmos DB hesabı oluşturuldu
> * Bir veritabanı ve koleksiyonu bir bölüm anahtarı ile oluşturulan
> * Oluşturulan JSON belgeleri
> * Bir belge güncelleştirildi
> * Sorgulanan bölümlenmiş koleksiyonlar
> * Saklı yordam çalıştı
> * Bir belge silindi
> * Bir veritabanı silindi

Şimdi toohello sonraki öğretici devam ve ek veri tooyour Cosmos DB hesap içeri aktarın. 

> [!div class="nextstepaction"]
> [Azure Cosmos DB hesabınıza veri aktarma](import-data.md)
