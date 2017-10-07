---
title: "aaaPartitioning ve yatay Azure Cosmos DB'de ölçeklendirme | Microsoft Docs"
description: "Azure Cosmos veritabanı bölümleme nasıl çalıştığı hakkında tooconfigure bölümlendirme ve bölüm anahtarlarını ve toopick hello sağ nasıl nasıl bölüm anahtarı, uygulamanız için öğrenin."
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
ms.openlocfilehash: 87d56db8c4ccc6b94b1650baff0fcfb3db6d1777
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toopartition-and-scale-in-azure-cosmos-db"></a>Nasıl toopartition ve ölçek Azure Cosmos veritabanı

[Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) ulaşmanıza hızlı ve tahmin edilebilir performansı ve ölçeği sorunsuz bir şekilde uygulamanızı yanı sıra, büyüdükçe Genel dağıtılmış, birden çok model veritabanı tasarlanan hizmet toohelp değil. Bu makalede nasıl çalıştığı tüm hello veriler için bölümleme Azure Cosmos DB'de modeller ve uygulamalarınızı Azure Cosmos DB kapsayıcıları tooeffectively ölçek nasıl yapılandırabileceğiniz anlatılmaktadır genel bir bakış sağlar.

Ayrıca bölümleme ve bölüm anahtarlarını bu Azure Cuma Scott Hanselman ve Azure Cosmos DB sorumlu mühendislik Yöneticisi, Shireesh Thota ile video ele alınmıştır.

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Azure-DocumentDB-Elastic-Scale-Partitioning/player]
> 

## <a name="partitioning-in-azure-cosmos-db"></a>Azure Cosmos DB bölümlendirme
Azure Cosmos DB'de depolamak ve herhangi bir ölçekte milisaniyelik sipariş yanıt süreleri ile şema daha az veri sorgulayabilirsiniz. Cosmos DB veri depolama adı verilen kapsayıcıları sağlar **(belge için) koleksiyonlar, grafikleri veya tabloları**. Kapsayıcıları mantıksal kaynaklar ve bir veya daha fazla fiziksel bölümleri veya sunucuları yayılabilir. bölüm sayısı Hello Cosmos hello depolama boyutu ve hello kapsayıcısının hello sağlanan işleme dayalı DB tarafından belirlenir. Cosmos DB her bölümün SSD yedekli depolama ilişkili sabit bir tutar sahiptir ve yüksek kullanılabilirlik için çoğaltılır. Bölüm yönetimi tam olarak Azure Cosmos DB tarafından yönetilen ve değil toowrite karmaşık koda sahip veya, bölümlerini yönetin. Cosmos DB depolama ve işleme açısından sınırsız kapsayıcılardır. 

![Yatay](./media/introduction/azure-cosmos-db-partitioning.png) 

Bölümleme saydam tooyour uygulamasıdır. Cosmos DB hızlı okuma ve yazma, sorguları, işlem mantığı, tutarlılık düzeyleri ve ayrıntılı erişim denetimi yöntemlerini/API'leri tooa tek kapsayıcı kaynağa yoluyla destekler. Merhaba hizmet bölüm ve yönlendirme sorgu istekleri toohello sağ bölüm arasında dağıtma verileri işler. 

Bölümleme nasıl çalışır? Her bir öğeyi benzersiz olarak tanımlamak bölüm anahtarı ve bir satır anahtarı olması gerekir. Bölüm anahtarı, verileriniz için bir mantıksal bölüm görevi görür ve bölümler veri dağıtılmasında Cosmos DB ile doğal bir sınır sağlar. Kısaca, işte Azure Cosmos DB'de bölümleme nasıl çalışır:

* Cosmos DB kapsayıcıyla sağlamak `T` İsteği/sn üretilen iş
* Merhaba arka planda Cosmos DB hükümleri bölümleri tooserve gerekli `T` İsteği/sn. Varsa `T` bölüm başına en fazla üretilen hello daha yüksek `t`, ardından Cosmos DB hükümleri `N`  =  `T/t` bölümleri
* Cosmos DB ayırır hello anahtar alanı bölümünün anahtar karmaları eşit hello arasında `N` bölümler. Bu nedenle, her bölüm (fiziksel bölüm) 1-N bölüm anahtarı değerlerini (mantıksal bölümler) barındırır
* Fiziksel bir bölüm olduğunda `p` Cosmos DB, depolama sınırına sorunsuz bir şekilde böler ulaştığında `p` iki yeni bölümlere `p1` ve `p2` ve tooroughly yarım hello anahtarları tooeach Merhaba, karşılık gelen değerleri dağıtır bölüm. Bu işlemi bölünmüş görünmez tooyour uygulamasıdır.
* Benzer şekilde, ne zaman sağlamanız daha yüksek verimlilik `t*N` verimlilik, Cosmos DB böler bir veya daha fazla, bölümler toosupport hello daha yüksek verimlilik

bölüm anahtarlarını Hello anlamları hello aşağıdaki tabloda gösterildiği gibi her API biraz farklı toomatch hello semantiği şunlardır:

| API | Bölüm anahtarı | Satır anahtarı |
| --- | --- | --- |
| DocumentDB | Özel bölüm anahtar yolu | Sabit`id` | 
| MongoDB | özel parça anahtarı  | Sabit`_id` | 
| Graph | Özel bölüm anahtar özelliği | Sabit`id` | 
| Tablo | Sabit`PartitionKey` | Sabit`RowKey` | 

Cosmos DB karma tabanlı bölümleme kullanır. Bir öğe yazdığınızda, Cosmos DB hello bölüm anahtarı değerini karma hale getirir ve kullanım hello sonuç toodetermine hangi bölüm toostore hello öğesinde karma. Tüm öğeleri aynı bölüm anahtarı hello cosmos DB depoları aynı fiziksel bölümünde hello. Merhaba hello bölüm anahtarı tasarım zamanında toomake sahip bir önemli karar seçimdir. Çok çeşitli değerleri ve hatta erişim desenlerini sahip bir özellik adı seçmeniz gerekir.

> [!NOTE]
> En iyi yöntem toohave bir bölüm anahtarı birçok farklı değerleri (100 s-1000'lik bloklar en az) sahip olur.
>

Azure Cosmos DB kapsayıcıları "sabit" veya "sınırsız." oluşturulabilir Sabit boyutlu kapsayıcıları 10 GB ve 10. 000'ru / s işleme üst sınırına sahip. Bazı API'ler hello bölüm anahtarı toobe sabit boyutlu kapsayıcıları için atlanmış izin verir. toocreate kapsayıcı sınırsız olarak, en düşük işleme 2500 RU/s belirtmeniz gerekir.

## <a name="partitioning-and-provisioned-throughput"></a>Bölümlendirme ve sağlanan işleme
Cosmos DB tahmin edilebilir performans için tasarlanmıştır. Bir kapsayıcı oluşturduğunuzda, üretilen iş açısından, yedek  **[istek birimleri](request-units.md) (RU) RU için olası eklentisinin dakika başına saniyede**. Her istek ile orantılı toohello miktarı CPU, bellek ve g/ç hello işlemi tarafından tüketilen gibi sistem kaynaklarının bir istek birimi ücret atanır. Oturum tutarlılığı 1 KB belgeyle okuma bir istek birimi tüketir. Okuma 1. öğe sayısı hello bakılmaksızın RU depolanır veya hello hello çalıştıran eşzamanlı istek sayısı aynı anda. Daha büyük öğelerin hello boyutuna bağlı olarak daha yüksek istek birimleri gerektirir. Varlıklarınızı hello boyutunu bildiğiniz ve okuma sayısını hello toosupport uygulamanız için gereken, uygulamanızın ihtiyaçlarını okuma için gereken işleme hello miktarda sağlayabilirsiniz. 

> [!NOTE]
> Merhaba kapsayıcısının tooachieve hello tam verimlilik, tooevenly sağlayan bir bölüm anahtarı isteklerini bazı farklı bölüm anahtarı değerleri arasında dağıtmak seçmeniz gerekir.
> 
> 

<a name="designing-for-partitioning"></a>
## <a name="working-with-hello-azure-cosmos-db-apis"></a>Hello Azure Cosmos DB API'leri ile çalışma
Hello Azure portalında veya Azure CLI toocreate kapsayıcıların kullanılması ve herhangi bir zamanda ölçeklendirin. Bu bölümde gösterilmiştir nasıl toocreate kapsayıcıları ve hello üretilen iş ve bölüm anahtar tanımında her hello desteklenen API'ları belirtin.

### <a name="documentdb-api"></a>DocumentDB API’si
Aşağıdaki örnek hello nasıl bir kapsayıcı (toplama) kullanılarak toocreate hello DocumentDB API gösterir. Daha ayrıntılı bilgi bulabilirsiniz [DocumentDB API'si ile bölümleme](partition-data.md).

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

Hello kullanarak bir öğe (belge) okuyabilir `GET` yöntemi hello REST API veya kullanılarak `ReadDocumentAsync` hello SDK'ları birinde.

```csharp
// Read document. Needs hello partition key and hello ID toobe specified
DeviceReading document = await client.ReadDocumentAsync<DeviceReading>(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  new RequestOptions { PartitionKey = new PartitionKey("XMS-0001") });
```

### <a name="mongodb-api"></a>MongoDB API’si
Merhaba MongoDB API ile sık kullanılan aracı, sürücü veya SDK aracılığıyla parçalı bir koleksiyon oluşturabilirsiniz. Bu örnekte, hello koleksiyonu oluşturmak için hello Mongo kabuğunu kullanırız.

Merhaba Mongo kabuğunu:

```
db.runCommand( { shardCollection: "admin.people", key: { region: "hashed" } } )
```
    
Sonuçları:

```JSON
{
    "_t" : "ShardCollectionResponse",
    "ok" : 1,
    "collectionsharded" : "admin.people"
}
```

### <a name="table-api"></a>Tablo API’si

Merhaba tablo API hello verimlilik tablolar için uygulamanız için hello appSettings yapılandırmasında belirtin:

```xml
<configuration>
    <appSettings>
      <!--Table creation options -->
      <add key="TableThroughput" value="700"/>
    </appSettings>
</configuration>
```

Ardından hello Azure Table depolama SDK'sını kullanarak bir tablo oluşturun. Merhaba bölüm anahtarı hello örtük olarak oluşturulmuş `PartitionKey` değeri. 

```csharp
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

CloudTable table = tableClient.GetTableReference("people");
table.CreateIfNotExists();
```

Aşağıdaki kod parçacığında hello kullanarak tek bir varlık alabilirsiniz:

```csharp
// Create a retrieve operation that takes a customer entity.
TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

// Execute hello retrieve operation.
TableResult retrievedResult = table.Execute(retrieveOperation);
```
Bkz: [hello tablo API ile geliştirme](tutorial-develop-table-dotnet.md) daha fazla ayrıntı için.

### <a name="graph-api"></a>Graph API

Merhaba grafik API'si hello Azure portal veya CLI toocreate kapsayıcıları kullanmanız gerekir. Alternatif olarak, Azure Cosmos DB çok model olduğundan başka modellerinin toocreate hello birini kullanın ve grafik kapsayıcı ölçeklendirin.

Herhangi bir köşe veya hello bölüm anahtarı ve kimliği içinde Gremlin kullanarak kenar okuyabilir. Örneğin, hello bölüm anahtarı olarak ve "Seattle" Merhaba satır anahtarı olarak bölgesi ("ABD") ile bir grafik için sözdizimi aşağıdaki hello kullanarak köşe bulabilirsiniz:

```
g.V(['USA', 'Seattle'])
```

Aynı kenarları hello bölüm anahtarı ve satır anahtarı kullanarak bir sınır başvuruda bulunabilir.

```
g.E(['USA', 'I5'])
```

Bkz: [Cosmos DB Gremlin desteği](gremlin-support.md) daha fazla ayrıntı için.


<a name="designing-for-partitioning"></a>
## <a name="designing-for-partitioning"></a>Bölümleme için tasarlama
kapsayıcı oluşturduğunuzda tooscale etkili bir şekilde Azure Cosmos DB ile toopick iyi bir bölüm anahtarı gerekir. Bölüm anahtarı seçmeye yönelik iki önemli noktalar şunlardır:

* **Sorgu ve işlemler için sınır**: seçiminizi bölüm anahtarı hello gerek tooenable hello kullan hello gereksinim toodistribute karşı hareketlerinin varlıklarınızı birden çok bölüm anahtarlarını tooensure ölçeklenebilir bir çözüm arasında dengelemeniz. Bir uçta hello ayarlayabilirsiniz aynı bölüm anahtarı tüm öğeler, ancak bunun için çözümünüzün hello ölçeklenebilirlik sınırlayabilir. Merhaba diğer uç yüksek düzeyde ölçeklenebilir kalır ancak saklı yordamları ve Tetikleyicileri aracılığıyla çapraz belge işlemleri kullanmasını önler her öğe için bir benzersiz bir bölüm anahtarı atayabilirsiniz. İdeal bölüm anahtarı, toouse verimli sorguları sağlar ve yeterli kardinalite sahip biridir tooensure çözümünüzü ölçeklenebilir. 
* **Hiçbir depolama ve performans sorunlarını**: toopick sağlayan bir özellik Yazar çeşitli farklı değerleri arasında dağıtılmış toobe önemlidir. Aynı bölüm anahtarı tek bir bölüm hello verimini aşamaz ve kısıtlanan istekleri toohello. Bu nedenle önemli toopick, uygulamanızda "etkin nokta" sonuçlanmaz bir bölüm anahtarı olur. Tek bölüm anahtarı bölüm içinde depolanması için tüm hello veriler ayrıca yüksek miktarda veriyi hello için sahip tooavoid bölüm anahtarlarını önerilir aynı değeri. 

Birkaç gerçek dünya senaryoları ve iyi bölüm anahtarlarının her biri için bakalım:
* Bir kullanıcı profili arka uç uyguluyorsanız hello kullanıcı kimliği bölüm anahtarı için iyi bir seçimdir değil.
* Örneğin, Aygıt durumu IOT veri depoluyorsanız bir cihaz kimliği bölüm anahtarı için iyi bir seçimdir.
* Zaman serisi veri günlük kaydı için Azure Cosmos DB kullanıyorsanız, ana bilgisayar adı hello veya işlem kimliği bölüm anahtarı için iyi bir seçimdir.
* Çok kiracılı mimari varsa, hello Kiracı kimliği bölüm anahtarı için iyi bir seçimdir.

IOT gibi bazı durumlarda kullanım ve kullanıcı profilleri, hello bölüm anahtarı olması hello aynı kimliği (belge anahtar). Bazı durumlarda hello zaman serisi veri gibi hello kimliğinden farklı bir bölüm anahtarı olabilir.

### <a name="partitioning-and-loggingtime-series-data"></a>Bölümlendirme ve zaman/günlüğü-serisi veri
Merhaba ortak kullanım durumları Cosmos DB'nin günlüğe kaydetme ve telemetri biridir. Büyük miktarda veriyi tooread/yazma gerekebilecek olduğundan önemli toopick iyi bir bölüm anahtarı kalır. Merhaba seçim, okuma ve yazma hızları ve tür toorun beklediğiniz sorgular bağlıdır. Bazı ipuçları nasıl toochoose iyi bir bölüm anahtarı.

* Kullanım örneği küçük oranını içeriyorsa zaman damgaları ve diğer filtreleri aralıklarına göre süresi gereksinimini tooquery ve uzun süre biriktirme hello zaman damgası, örneğin, dökümü kullanarak tarih sonra iyi bir yaklaşım bölüm anahtarı olarak yazar. Bu, tooquery tüm hello verileri tek bir bölüm tarihinden sağlar. 
* İş yükünüzün daha yaygın bir durumdur, ağır yazılmışsa zaman damgasını dayalı olmayan ve böylece Cosmos DB yazma eşit çeşitli bölümler dağıtabilirsiniz bölüm anahtarı kullanmanız gerekir. Burada bir ana bilgisayar adı, işlem kimliği, etkinlik kimliği veya başka bir özelliği yüksek önem düzeyi ile iyi bir seçimdir. 
* Burada her gün/ay için birden çok kapsayıcı sahip ve hello bölüm anahtarı ana bilgisayar adı gibi ayrıntılı bir özelliği bir karma bir buna üçüncü bir yaklaşımdır. Bu, farklı verimlilik üzerinde hello zaman penceresi göre ayarlayabilirsiniz hello avantajına sahiptir, okuma ve yazma işlemleri, gördüğünden bu yana üretilen iş ile önceki ay alt ancak gibi hello kapsayıcı hello geçerli ay için daha yüksek işleme ile sağlanır Bunlar yalnızca okuma hizmet.

### <a name="partitioning-and-multi-tenancy"></a>Bölümlendirme ve çoklu kiracı
Cosmos DB kullanarak çok kiracılı uygulama uyguluyorsanız, iki popüler desenleri – Kiracı başına bir bölüm anahtarı ve Kiracı başına bir kapsayıcı vardır. Merhaba Artıları ve eksileri her şunlardır:

* Kiracı başına bir bölüm anahtarı: tek bir kapsayıcıda birlikte bu modelde, kiracılar. Ancak, sorgular ve eklemeleri tek bir kiracı içinde öğeleri için tek bir bölüm karşı gerçekleştirilebilir. İşlem mantığı, bir kiracı içindeki tüm öğeler arasında de uygulayabilirsiniz. Birden çok kiracıya bir kapsayıcı paylaşmak olduğundan, her bir kiracı için ek boş alan sağlama yerine tek bir kapsayıcıdaki kiracılar için kaynak havuzu tarafından depolama ve işleme maliyetleri kaydedebilirsiniz. Merhaba dezavantajı, performans yalıtımı Kiracı başına yok ' dir. Performans/verimliliği artırır toohello kapsayıcının tamamı hedeflenen vs artar kiracılar için geçerlidir.
* Kiracı başına bir kapsayıcı: her bir kiracı kendi kapsayıcı vardır. Bu modelde, Kiracı başına performans ayırabilirsiniz. Cosmos DB'ın yeni fiyatlandırma modeli sağlamada bu birkaç kiracılarla çok kiracılı uygulamalar için daha uygun maliyetli modelidir.

Ayrıca, küçük kiracılar collocates ve büyük kiracılar tootheir kendi kapsayıcı Geçiren birleşimi ve katmanlı bir yaklaşım kullanabilirsiniz.

## <a name="next-steps"></a>Sonraki adımlar
Bu makalede, bir genel bakış, kavramlar ve tüm Azure Cosmos DB API'si ile bölümleme için en iyi uygulamalar için genel bir bakış sağlanan. 

* Hakkında bilgi edinin [Azure Cosmos veritabanı sağlanan işleme](request-units.md)
* Hakkında bilgi edinin [Azure Cosmos veritabanı genel dağıtım](distribute-data-globally.md)



