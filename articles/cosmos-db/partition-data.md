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
# <a name="how-to-partition-and-scale-in-azure-cosmos-db"></a>Bölüm ve ölçek Azure Cosmos veritabanı

[Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) büyüdüğü gibi hızlı ve tahmin edilebilir performansı ve ölçeği sorunsuz bir şekilde uygulamanızı yanı sıra ulaşmak yardımcı olmak için tasarlanmış bir genel dağıtılmış, birden çok model veritabanı hizmetidir. Bu makalede Azure Cosmos veritabanı tüm veri modelleri için nasıl bölümleme çalışır genel bir bakış sağlar ve Azure Cosmos DB kapsayıcıları, uygulamalarınızı etkili bir şekilde ölçeklendirmek için nasıl yapılandırılacağını anlatır.

Ayrıca bölümleme ve bölüm anahtarlarını bu Azure Cuma Scott Hanselman ve Azure Cosmos DB sorumlu mühendislik Yöneticisi, Shireesh Thota ile video ele alınmıştır.

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Azure-DocumentDB-Elastic-Scale-Partitioning/player]
> 

## <a name="partitioning-in-azure-cosmos-db"></a>Azure Cosmos DB bölümlendirme
Azure Cosmos DB'de depolamak ve herhangi bir ölçekte milisaniyelik sipariş yanıt süreleri ile şema daha az veri sorgulayabilirsiniz. Cosmos DB veri depolama adı verilen kapsayıcıları sağlar **(belge için) koleksiyonlar, grafikleri veya tabloları**. Kapsayıcıları mantıksal kaynaklar ve bir veya daha fazla fiziksel bölümleri veya sunucuları yayılabilir. Bölüm sayısı Cosmos depolama boyutu ve kapsayıcının sağlanan işleme dayalı DB tarafından belirlenir. Cosmos DB her bölümün SSD yedekli depolama ilişkili sabit bir tutar sahiptir ve yüksek kullanılabilirlik için çoğaltılır. Bölüm yönetimi tam olarak Azure Cosmos DB tarafından yönetilen ve karmaşık kodlar yazmak veya bölüm yönetmek zorunda kalmazsınız. Cosmos DB depolama ve işleme açısından sınırsız kapsayıcılardır. 

![Yatay](./media/introduction/azure-cosmos-db-partitioning.png) 

Bölümlendirme, uygulamanız için saydamdır. Cosmos DB hızlı okuma ve yazma, sorguları, işlem mantığı, tutarlılık düzeyleri ve ayrıntılı erişim denetimi yöntemlerini/API'leri tek kapsayıcı kaynağa yoluyla destekler. Hizmeti dağıtma verileri bölümleri ve doğru bölüm yönlendirme sorgu istekleri üzerinden işler. 

Bölümleme nasıl çalışır? Her bir öğeyi benzersiz olarak tanımlamak bölüm anahtarı ve bir satır anahtarı olması gerekir. Bölüm anahtarı, verileriniz için bir mantıksal bölüm görevi görür ve bölümler veri dağıtılmasında Cosmos DB ile doğal bir sınır sağlar. Kısaca, işte Azure Cosmos DB'de bölümleme nasıl çalışır:

* Cosmos DB kapsayıcıyla sağlamak `T` İsteği/sn üretilen iş
* Arka planda Cosmos DB sunmak için gereken bölümleri sağlar `T` İsteği/sn. Varsa `T` bölüm başına en fazla üretilen daha yüksek `t`, ardından Cosmos DB hükümleri `N`  =  `T/t` bölümleri
* Cosmos DB anahtar alanı bölümünün eşit yatay anahtar karmaları ayırır `N` bölümler. Bu nedenle, her bölüm (fiziksel bölüm) 1-N bölüm anahtarı değerlerini (mantıksal bölümler) barındırır
* Fiziksel bir bölüm olduğunda `p` Cosmos DB, depolama sınırına sorunsuz bir şekilde böler ulaştığında `p` iki yeni bölümlere `p1` ve `p2` ve her bölüm için kabaca yarım anahtarlara karşılık gelen değerleri dağıtır. Bu işlemi bölünmüş uygulamanıza görünmez durumdadır.
* Benzer şekilde, ne zaman sağlamanız daha yüksek verimlilik `t*N` verimlilik, Cosmos DB, bir veya daha yüksek verimlilik desteklemek için bölümler ayırır

Bölüm anahtarlarını anlamları aşağıdaki tabloda gösterildiği gibi her API semantiği eşleşmesi biraz farklılık gösterir:

| API | Bölüm anahtarı | Satır anahtarı |
| --- | --- | --- |
| DocumentDB | Özel bölüm anahtar yolu | Sabit`id` | 
| MongoDB | özel parça anahtarı  | Sabit`_id` | 
| Graph | Özel bölüm anahtar özelliği | Sabit`id` | 
| Tablo | Sabit`PartitionKey` | Sabit`RowKey` | 

Cosmos DB karma tabanlı bölümleme kullanır. Öğeyi yazdığınızda, Cosmos DB bölüm anahtarı değerini karma hale getirir ve karma hale getirilen sonuç öğesinde depolamak için hangi bölümünü belirlemek için kullanın. Cosmos DB tüm öğeleri aynı fiziksel bölümünde aynı bölüm anahtarına sahip depolar. Bölüm anahtarı seçimi tasarım zamanında yapmak zorunda önemli bir karardır. Çok çeşitli değerleri ve hatta erişim desenlerini sahip bir özellik adı seçmeniz gerekir.

> [!NOTE]
> Birçok farklı değerleri (100 s-1000'lik bloklar en az) sahip bir bölüm anahtarı için en iyi bir uygulamadır.
>

Azure Cosmos DB kapsayıcıları "sabit" veya "sınırsız." oluşturulabilir Sabit boyutlu kapsayıcıları 10 GB ve 10. 000'ru / s işleme üst sınırına sahip. Bazı API'ler için sabit boyutlu kapsayıcılar atlanacak bölüm anahtarı izin verir. Sınırsız olarak bir kapsayıcı oluşturmak için en düşük işleme 2500 RU/s belirtmeniz gerekir.

## <a name="partitioning-and-provisioned-throughput"></a>Bölümlendirme ve sağlanan işleme
Cosmos DB tahmin edilebilir performans için tasarlanmıştır. Bir kapsayıcı oluşturduğunuzda, üretilen iş açısından, yedek  **[istek birimleri](request-units.md) (RU) RU için olası eklentisinin dakika başına saniyede**. Her istek CPU, bellek ve g/ç işlemi tarafından tüketilen gibi sistem kaynaklarının miktarını orantılıdır bir istek birimi ücret atanır. Oturum tutarlılığı 1 KB belgeyle okuma bir istek birimi tüketir. Okuma 1. RU bağımsız olarak depolanan öğeler sayısını veya aynı anda çalıştırılması eşzamanlı istek sayısı. Büyük öğeleri boyutuna bağlı olarak daha yüksek istek birimleri gerektirir. Varlıklarınızı ve uygulamanız için desteklemeniz gereken okuma sayısını boyutunu biliyorsanız, verimlilik ihtiyaçlarını okuma, uygulama için gerekli miktarda sağlayabilirsiniz. 

> [!NOTE]
> Kapsayıcı tam verimini elde etmek için istekleri bazı farklı bölüm anahtar değerleri arasında eşit olarak dağıtmanızı sağlayan bir bölüm anahtarı seçmeniz gerekir.
> 
> 

<a name="designing-for-partitioning"></a>
## <a name="working-with-the-azure-cosmos-db-apis"></a>Azure Cosmos DB API'leri ile çalışma
Kapsayıcılar oluşturmak ve bunları herhangi bir anda ölçeklendirmek için Azure portalında veya Azure CLI kullanın. Bu bölümde, kapsayıcıları oluşturma ve üretilen iş ve bölüm anahtar tanımını her desteklenen API'ları belirtin gösterilmektedir.

### <a name="documentdb-api"></a>DocumentDB API’si
Aşağıdaki örnek DocumentDB API'sini kullanarak bir kapsayıcı (toplama) oluşturulacağını gösterir. Daha ayrıntılı bilgi bulabilirsiniz [DocumentDB API'si ile bölümleme](partition-data.md).

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

Bir öğe (belge) kullanarak okuyabilirsiniz `GET` REST API yönteminde veya kullanarak `ReadDocumentAsync` SDK'lar birinde.

```csharp
// Read document. Needs the partition key and the ID to be specified
DeviceReading document = await client.ReadDocumentAsync<DeviceReading>(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  new RequestOptions { PartitionKey = new PartitionKey("XMS-0001") });
```

### <a name="mongodb-api"></a>MongoDB API’si
MongoDB API'si ile sık kullanılan aracı, sürücü veya SDK aracılığıyla parçalı bir koleksiyon oluşturabilirsiniz. Bu örnekte koleksiyonu oluşturma işleminde Mongo kabuğunu kullanırız.

Mongo Kabuğu'nda:

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

Tablo API ile tablolar için işleme, uygulamanız için appSettings yapılandırmasında belirtin:

```xml
<configuration>
    <appSettings>
      <!--Table creation options -->
      <add key="TableThroughput" value="700"/>
    </appSettings>
</configuration>
```

Ardından Azure Table depolama SDK'sını kullanarak bir tablo oluşturun. Bölüm anahtarı örtük olarak oluşturulmuş `PartitionKey` değeri. 

```csharp
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

CloudTable table = tableClient.GetTableReference("people");
table.CreateIfNotExists();
```

Aşağıdaki kod parçacığını kullanarak tek bir varlık alabilirsiniz:

```csharp
// Create a retrieve operation that takes a customer entity.
TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

// Execute the retrieve operation.
TableResult retrievedResult = table.Execute(retrieveOperation);
```
Bkz: [tablo API ile geliştirme](tutorial-develop-table-dotnet.md) daha fazla ayrıntı için.

### <a name="graph-api"></a>Graph API

Grafik API'si ile kapsayıcı oluşturmak için Azure portal veya CLI kullanmalısınız. Alternatif olarak, Azure Cosmos DB çok model olduğundan, bir başka modellerinin oluşturmak ve grafik kapsayıcı ölçeklendirmek için kullanabilirsiniz.

Herhangi bir köşe veya kimliği ve bölüm anahtarı Gremlin kullanarak kenar okuyabilir. Örneğin, bölgeye ("ABD") bölüm anahtarını ve satır anahtarı olarak "Seattle" ile bir grafik için aşağıdaki sözdizimini kullanarak bir köşe bulabilirsiniz:

```
g.V(['USA', 'Seattle'])
```

Kenarları aynı bölüm anahtarı ve satır anahtarı kullanarak bir sınır başvuruda bulunabilir.

```
g.E(['USA', 'I5'])
```

Bkz: [Cosmos DB Gremlin desteği](gremlin-support.md) daha fazla ayrıntı için.


<a name="designing-for-partitioning"></a>
## <a name="designing-for-partitioning"></a>Bölümleme için tasarlama
Etkili bir şekilde Azure Cosmos DB ile ölçeklendirmek için kapsayıcı oluştururken iyi bir bölüm anahtarı seçmeniz gerekir. Bölüm anahtarı seçmeye yönelik iki önemli noktalar şunlardır:

* **Sorgu ve işlemler için sınır**: bölüm anahtarı seçiminizi varlıklarınızı ölçeklenebilir bir çözüm sağlamak için birden çok bölüm anahtarları arasında dağıtmak için gereksinim karşı işlemleri kullanımını etkinleştirmek için gereken dengelemeniz. Bir extreme tüm öğeleri aynı bölüm anahtarı ayarlayabilirsiniz, ancak bu çözümünüzü ölçeklenebilirliğini sınırlayabilir. Diğer uçta yüksek düzeyde ölçeklenebilir kalır ancak saklı yordamları ve Tetikleyicileri aracılığıyla çapraz belge işlemleri kullanmasını önler her öğe için bir benzersiz bir bölüm anahtarı atayabilirsiniz. İdeal bölüm anahtarı verimli sorguları kullanmanıza olanak sağlayan ve çözümünüzü ölçeklenebilir olduğundan emin olmak için yeterli kardinalite sahip olan biridir. 
* **Hiçbir depolama ve performans sorunlarını**: çeşitli farklı değerleri arasında dağıtılacak yazma sağlayan bir özellik seçmek önemlidir. Aynı bölüm anahtarı isteklerini tek bir bölüm verimini aşamaz ve kısıtlanan. Böylece, uygulamanızda "etkin nokta" sonuçlanmaz bir bölüm anahtarı seçmek önemlidir. Tüm veriler tek bölüm anahtarı için bir bölüm içinde saklanmalıdır olduğundan, yüksek miktarda veriyi aynı değere sahip bölüm anahtarlarını önlemek için de önerilir. 

Birkaç gerçek dünya senaryoları ve iyi bölüm anahtarlarının her biri için bakalım:
* Bir kullanıcı profili arka uç uygulama, kullanıcı kimliği bölüm anahtarı için iyi bir seçimdir yoktur.
* Örneğin, Aygıt durumu IOT veri depoluyorsanız bir cihaz kimliği bölüm anahtarı için iyi bir seçimdir.
* Zaman serisi veri günlük kaydı için Azure Cosmos DB kullanıyorsanız, daha sonra ana bilgisayar adı veya işlem bölüm anahtarı için iyi bir seçimdir kimliğidir.
* Çok kiracılı mimari varsa, Kiracı kimliği bölüm anahtarı için iyi bir seçimdir.

IOT ve kullanıcı profilleri gibi bazı durumlarda kullanım, bölüm anahtarı, kimliğinizi (belge anahtarı) ile aynı olması. Bazı durumlarda zaman serisi veri gibi kimliğinden farklı bir bölüm anahtarı olabilir.

### <a name="partitioning-and-loggingtime-series-data"></a>Bölümlendirme ve zaman/günlüğü-serisi veri
Cosmos DB'nin ortak kullanım durumları günlüğe kaydetme ve telemetri biridir. Büyük miktarda veriyi okuma/yazma gerekebilecek beri iyi bir bölüm anahtarı seçmek önemlidir. Seçim, okuma ve yazma hızları ve tür sorgular çalıştırmak için beklediğiniz bağlıdır. İyi bir bölüm anahtarı seçmek bazı ipuçları şunlardır.

* Kullanım örneği küçük oranını içeriyorsa bu gibi bir durumda damgası dökümü kullanarak tarih sonra iyi bir yaklaşım bölüm anahtarı olduğu gibi zaman, sorgu zaman damgaları aralıklarına tarafından gerek ve diğer filtreleri uzun süre biriktirme yazar. Bu sorguya tüm verileri için bir tarih tek bir bölümün dışında sağlar. 
* İş yükünüzün daha yaygın bir durumdur, ağır yazılmışsa zaman damgasını dayalı olmayan ve böylece Cosmos DB yazma eşit çeşitli bölümler dağıtabilirsiniz bölüm anahtarı kullanmanız gerekir. Burada bir ana bilgisayar adı, işlem kimliği, etkinlik kimliği veya başka bir özelliği yüksek önem düzeyi ile iyi bir seçimdir. 
* Burada her gün/ay için birden çok kapsayıcı sahip ve bölüm anahtarı ana bilgisayar adı gibi ayrıntılı bir özelliği bir karma bir buna üçüncü bir yaklaşımdır. Bu zaman penceresinde göre farklı verimlilik ayarlayabilirsiniz avantajına sahiptir, okuma ve yazma işlemleri, gördüğünden önceki ay ile üretilen iş bunlar bu yana yalnızca alt ancak örneğin, geçerli ay için kapsayıcı daha yüksek işleme ile sağlanır Hizmet vermemesini okur.

### <a name="partitioning-and-multi-tenancy"></a>Bölümlendirme ve çoklu kiracı
Cosmos DB kullanarak çok kiracılı uygulama uyguluyorsanız, iki popüler desenleri – Kiracı başına bir bölüm anahtarı ve Kiracı başına bir kapsayıcı vardır. Artıları ve eksileri her şunlardır:

* Kiracı başına bir bölüm anahtarı: tek bir kapsayıcıda birlikte bu modelde, kiracılar. Ancak, sorgular ve eklemeleri tek bir kiracı içinde öğeleri için tek bir bölüm karşı gerçekleştirilebilir. İşlem mantığı, bir kiracı içindeki tüm öğeler arasında de uygulayabilirsiniz. Birden çok kiracıya bir kapsayıcı paylaşmak olduğundan, her bir kiracı için ek boş alan sağlama yerine tek bir kapsayıcıdaki kiracılar için kaynak havuzu tarafından depolama ve işleme maliyetleri kaydedebilirsiniz. Dezavantajı, performans yalıtımı Kiracı başına yok ' dir. Performans/verimliliği artırır, kiracılar için hedeflenen artar kapsayıcının tamamı vs uygulayın.
* Kiracı başına bir kapsayıcı: her bir kiracı kendi kapsayıcı vardır. Bu modelde, Kiracı başına performans ayırabilirsiniz. Cosmos DB'ın yeni fiyatlandırma modeli sağlamada bu birkaç kiracılarla çok kiracılı uygulamalar için daha uygun maliyetli modelidir.

Ayrıca, küçük kiracılar collocates ve büyük kiracılar kendi kapsayıcıya Geçiren birleşimi ve katmanlı bir yaklaşım kullanabilirsiniz.

## <a name="next-steps"></a>Sonraki adımlar
Bu makalede, bir genel bakış, kavramlar ve tüm Azure Cosmos DB API'si ile bölümleme için en iyi uygulamalar için genel bir bakış sağlanan. 

* Hakkında bilgi edinin [Azure Cosmos veritabanı sağlanan işleme](request-units.md)
* Hakkında bilgi edinin [Azure Cosmos veritabanı genel dağıtım](distribute-data-globally.md)



