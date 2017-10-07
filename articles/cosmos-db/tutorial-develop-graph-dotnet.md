---
title: "Azure Cosmos DB: Merhaba grafik API'si, .NET geliştirme | Microsoft Docs"
description: "Bilgi nasıl toodevelop Azure Cosmos veritabanı DocumentDB .NET kullanarak API ile"
services: cosmos-db
documentationcenter: 
author: dennyglee
manager: jhubbard
editor: 
ms.assetid: cc8df0be-672b-493e-95a4-26dd52632261
ms.service: cosmos-db
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/10/2017
ms.author: denlee
ms.custom: mvc
ms.openlocfilehash: 12e435d8169aeee6e818dac4a3b66c7a0ec5f2d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-develop-with-hello-graph-api-in-net"></a>Azure Cosmos DB: Merhaba grafik API'si, .NET geliştirin
Azure Cosmos DB Microsoft'un Genel dağıtılmış birden çok model veritabanı hizmetidir. Hızlı bir şekilde oluşturmak ve belge, anahtar/değer ve grafik veritabanları, her biri hello genel dağıtım ve yatay ölçek özelliklerini Azure Cosmos DB'nin hello çekirdek yararlı sorgulayabilirsiniz. 

Bu öğretici bir Azure Cosmos DB hesabı kullanarak toocreate hello nasıl Azure portal ve nasıl gösterir toocreate bir grafik veritabanı ve kapsayıcı. Merhaba uygulama dört kişiler hello kullanarak basit bir sosyal ağ oluşturur [grafik API'si](graph-sdk-dotnet.md) (Önizleme), ardından erişir ve Gremlin kullanarak hello grafik sorgular.

Bu öğretici hello aşağıdaki görevleri içerir:

> [!div class="checklist"]
> * Azure Cosmos DB hesabı oluşturma 
> * Bir grafik veritabanı ve kapsayıcı oluşturun
> * Köşeleri ve kenarları too.NET nesneleri seri hale
> * Köşeleri ve kenarları ekleme
> * Sorgu hello grafik Gremlin kullanma

## <a name="graphs-in-azure-cosmos-db"></a>Azure Cosmos DB grafiklerde
Azure Cosmos DB toocreate, güncelleştirme ve hello kullanarak sorgu grafikleri kullanabilirsiniz [Microsoft.Azure.Graphs](graph-sdk-dotnet.md) kitaplığı. Merhaba Microsoft.Azure.Graph kitaplığı, bir tek genişletme yöntemi sağlar `CreateGremlinQuery<T>` hello üstünde `DocumentClient` tooexecute Gremlin sorguları sınıfı.

Gremlin destekleyen işlevsel bir programlama dili yazma işlemleri (DML) ve sorgu ve çapraz geçişi işlemleri ' dir. Biz bu makalede tooget birkaç örneklerde, başlatılan Gremlin ile kapsar. Bkz: [Gremlin sorguları](gremlin-support.md) ayrıntılı kılavuz Gremlin özelliklerinden Azure Cosmos DB içinde kullanılabilir. 

## <a name="prerequisites"></a>Ön koşullar
Merhaba aşağıdaki sahip olduğunuzdan emin olun:

* Etkin bir Azure hesabı. Bir aboneliğiniz yoksa [ücretsiz bir hesap](https://azure.microsoft.com/free/) için kaydolabilirsiniz. 
    * Alternatif olarak, hello kullanabilirsiniz [Azure DocumentDB öykünücüsü](local-emulator.md) Bu öğretici için.
* [Visual Studio](http://www.visualstudio.com/).

## <a name="create-database-account"></a>Veritabanı hesabı oluşturma

Hello Azure portalında bir Azure Cosmos DB hesabı oluşturarak başlayalım.  

> [!TIP]
> * Zaten Azure Cosmos DB hesabınız var mı? Bu durumda, İleri çok atlayabilirsiniz[, Visual Studio çözümü ayarlama](#SetupVS)
> * Bir Azure DocumentDB hesabına sahip miydiniz? Bu nedenle, hesabınızı şimdi bir Azure Cosmos DB hesabı ise ve şimdi çok atlayabilirsiniz[, Visual Studio çözümü ayarlama](#SetupVS).  
> * Hello Azure Cosmos DB öykünücüsü kullanıyorsanız, lütfen hello adımları izleyin [Azure Cosmos DB öykünücüsü](local-emulator.md) toosetup öykünücüsü hello ve İleri çok atlayabilirsiniz[, Visual Studio çözümünü kurmak](#SetupVS). 
>
> 

[!INCLUDE [cosmos-db-create-dbaccount-graph](../../includes/cosmos-db-create-dbaccount-graph.md)]

## <a id="SetupVS"></a>Visual Studio çözümünüzü kurma
1. Bilgisayarınızda **Visual Studio**'yu açın.
2. Merhaba üzerinde **dosya** menüsünde, select **yeni**ve ardından **proje**.
3. Merhaba, **yeni proje** iletişim kutusunda **şablonları** / **Visual C#** / **konsol uygulaması (.NET Framework)**, projenizi adlandırın ve ardından **Tamam**.
4. Merhaba, **Çözüm Gezgini**, Visual Studio çözümünüzün yeni konsol uygulamanızın üzerinde sağ tıklayın ve ardından **NuGet paketlerini Yönet...**
5. Merhaba, **NuGet** sekmesini tıklatın, **Gözat**ve türü **Microsoft.Azure.Graphs** hello arama kutusu ve onay hello **yayın öncesi sürümleriiçerir**.
6. Merhaba sonuçları içinde bulmak **Microsoft.Azure.Graphs** tıklatıp **yükleme**.
   
   Değişiklikleri toohello çözümü gözden geçirme hakkında bir ileti alırsanız tıklatın **Tamam**. Lisans kabulü hakkında bir ileti alırsanız **Kabul ediyorum**'a tıklayın.
   
    Merhaba `Microsoft.Azure.Graphs` kitaplığı, bir tek genişletme yöntemi sağlar `CreateGremlinQuery<T>` Gremlin işlemleri yürütmek. Gremlin destekleyen işlevsel bir programlama dili yazma işlemleri (DML) ve sorgu ve çapraz geçişi işlemleri ' dir. Biz bu makalede tooget birkaç örneklerde, başlatılan Gremlin ile kapsar. [Gremlin sorguları](gremlin-support.md) Azure Cosmos DB'de Gremlin özelliklerinin ayrıntılı bir kılavuz vardır.

## <a id="add-references"></a>Uygulamanızı bağlama

Bu iki sabitleri ekleyin ve *istemci* uygulamanızda değişken. 

```csharp
string endpoint = ConfigurationManager.AppSettings["Endpoint"]; 
string authKey = ConfigurationManager.AppSettings["AuthKey"]; 
``` 
Ardından, head geri toohello [Azure portal](https://portal.azure.com) tooretrieve uç noktasının URL'sini ve birincil anahtar. Merhaba uç noktasının URL'sini ve birincil anahtar, uygulama toounderstand için gerekli olan nerede tooconnect ve Azure Cosmos DB tootrust için uygulamanızın bağlantı. 

İçinde Azure portal Merhaba, tooyour Azure Cosmos DB hesap gidin, tıklatın **anahtarları**ve ardından **okuma-yazma anahtarları**. 

Merhaba URI hello Portal'dan kopyalayın ve üzerinden yapıştırın `Endpoint` hello uç nokta özelliğinde yukarıdaki. Sonra birincil anahtar hello portalından hello kopyalayın ve hello yapıştırma `AuthKey` yukarıdaki özelliği. 

! [Hello Azure portal ekran görüntüsü bir C# uygulaması hello öğretici toocreate tarafından kullanılır. Bir Azure Cosmos DB hesap hello ANAHTARLAR düğmesi vurgulanmış üzerinde hello Azure Cosmos DB gezinti ve anahtarlar dikey penceresinde hello URI ve birincil anahtar değerleri vurgulanmış üzerinde hello gösterir] [Anahtarları] 
 
## <a id="instantiate"></a>Merhaba DocumentClient örneği 
Ardından, hello yeni bir örneğini oluşturun **DocumentClient**.  

```csharp 
DocumentClient client = new DocumentClient(new Uri(endpoint), authKey); 
``` 

## <a id="create-database"></a>Bir veritabanı oluşturun 

Şimdi bir Azure Cosmos DB Oluştur [veritabanı](documentdb-resources.md#databases) hello kullanarak [Documentclient](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) yöntemi veya [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) hello yöntemi  **DocumentClient** hello sınıfından [DocumentDB .NET SDK'sı](documentdb-sdk-dotnet.md).  

```csharp 
Database database = await client.CreateDatabaseIfNotExistsAsync(new Database { Id = "graphdb" }); 
``` 
 
## <a name="create-a-graph"></a>Bir grafik oluşturma 

Ardından, bir grafik kapsayıcı hello kullanarak hello kullanarak oluşturma [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) yöntemi veya [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) hello yöntemi **DocumentClient**  sınıfı. Bir koleksiyon, grafik varlıkların bir kapsayıcıdır. 

```csharp 
DocumentCollection graph = await client.CreateDocumentCollectionIfNotExistsAsync( 
    UriFactory.CreateDatabaseUri("graphdb"), 
    new DocumentCollection { Id = "graphcollz" }, 
    new RequestOptions { OfferThroughput = 1000 }); 
``` 

## <a id="serializing"></a>Köşeleri ve kenarları too.NET nesneleri seri hale
Azure Cosmos DB kullanır hello [GraphSON kablo biçiminde](gremlin-support.md), köşe, kenarları ve özellikleri için JSON şeması tanımlar. bir bağımlılık olarak JSON.NET Hello Azure Cosmos DB .NET SDK'sını içerir ve bu bize tooserialize/seri durumdan GraphSON biz kodda çalışabilirsiniz .NET nesneleri içine sağlar.

Örnek olarak, basit bir sosyal ağ dört kişilerle şimdi çalışır. Nasıl tümleştirildiği incelenmektedir toocreate `Person` köşeleri eklemek `Knows` arasındaki ilişkileri ardından sorgu ve çapraz hello grafik toofind "arkadaş arkadaş" ilişkiler. 

Merhaba `Microsoft.Azure.Graphs.Elements` ad alanı sağlar `Vertex`, `Edge`, `Property` ve `VertexProperty` GraphSON yanıtları toowell tanımlı .NET nesnelerini seri durumdan çıkarmak için sınıflar.

## <a name="run-gremlin-using-creategremlinquery"></a>Gremlin CreateGremlinQuery kullanarak çalıştırma
SQL gibi gremlin okuma, yazma ve sorgu işlemleri destekler. Örneğin, hello aşağıdaki kod parçacığında nasıl toocreate köşeleri kenarlar kullanan bazı örnek sorgular gerçekleştirmek gösterir `CreateGremlinQuery<T>`ve zaman uyumsuz olarak kullanarak bu sonuçlarını yinelemek `ExecuteNextAsync` ve ' HasMoreResults.

```cs
Dictionary<string, string> gremlinQueries = new Dictionary<string, string>
{
    { "Cleanup",        "g.V().drop()" },
    { "AddVertex 1",    "g.addV('person').property('id', 'thomas').property('firstName', 'Thomas').property('age', 44)" },
    { "AddVertex 2",    "g.addV('person').property('id', 'mary').property('firstName', 'Mary').property('lastName', 'Andersen').property('age', 39)" },
    { "AddVertex 3",    "g.addV('person').property('id', 'ben').property('firstName', 'Ben').property('lastName', 'Miller')" },
    { "AddVertex 4",    "g.addV('person').property('id', 'robin').property('firstName', 'Robin').property('lastName', 'Wakefield')" },
    { "AddEdge 1",      "g.V('thomas').addE('knows').to(g.V('mary'))" },
    { "AddEdge 2",      "g.V('thomas').addE('knows').to(g.V('ben'))" },
    { "AddEdge 3",      "g.V('ben').addE('knows').to(g.V('robin'))" },
    { "UpdateVertex",   "g.V('thomas').property('age', 44)" },
    { "CountVertices",  "g.V().count()" },
    { "Filter Range",   "g.V().hasLabel('person').has('age', gt(40))" },
    { "Project",        "g.V().hasLabel('person').values('firstName')" },
    { "Sort",           "g.V().hasLabel('person').order().by('firstName', decr)" },
    { "Traverse",       "g.V('thomas').outE('knows').inV().hasLabel('person')" },
    { "Traverse 2x",    "g.V('thomas').outE('knows').inV().hasLabel('person').outE('knows').inV().hasLabel('person')" },
    { "Loop",           "g.V('thomas').repeat(out()).until(has('id', 'robin')).path()" },
    { "DropEdge",       "g.V('thomas').outE('knows').where(inV().has('id', 'mary')).drop()" },
    { "CountEdges",     "g.E().count()" },
    { "DropVertex",     "g.V('thomas').drop()" },
};

foreach (KeyValuePair<string, string> gremlinQuery in gremlinQueries)
{
    Console.WriteLine($"Running {gremlinQuery.Key}: {gremlinQuery.Value}");

    // hello CreateGremlinQuery method extensions allow you tooexecute Gremlin queries and iterate
    // results asychronously
    IDocumentQuery<dynamic> query = client.CreateGremlinQuery<dynamic>(graph, gremlinQuery.Value);
    while (query.HasMoreResults)
    {
        foreach (dynamic result in await query.ExecuteNextAsync())
        {
            Console.WriteLine($"\t {JsonConvert.SerializeObject(result)}");
        }
    }

    Console.WriteLine();
}
```

## <a name="add-vertices-and-edges"></a>Köşeleri ve kenarları ekleme

Daha fazla ayrıntı bölüm önceki hello gösterilen hello Gremlin deyimlerini bakalım. İlk biz Gremlin'ın kullanarak bazı köşeleri `addV` yöntemi. Örneğin, hello aşağıdaki kod parçacığında "Kişi" türündeki "Thomas Andersen" köşe ad, Soyadı ve yaş özelliklerini oluşturur.

```cs
// Create a vertex
IDocumentQuery<Vertex> createVertexQuery = client.CreateGremlinQuery<Vertex>(
    graphCollection, 
    "g.addV('person').property('firstName', 'Thomas')");

while (createVertexQuery.HasMoreResults)
{
    Vertex thomas = (await create.ExecuteNextAsync<Vertex>()).First();
}
```

Biz Gremlin'ın kullanarak bu köşeleri arasında bazı kenarları oluşturup `addE` yöntemi. 

```cs
// Add a "knows" edge
IDocumentQuery<Edge> createEdgeQuery = client.CreateGremlinQuery<Edge>(
    graphCollection, 
    "g.V('thomas').addE('knows').to(g.V('mary'))");

while (create.HasMoreResults)
{
    Edge thomasKnowsMaryEdge = (await create.ExecuteNextAsync<Edge>()).First();
}
```

Biz kullanarak var olan bir köşe güncelleştirebilirsiniz `properties` Gremlin içinde adım. Biz hello çağrısı tooexecute hello sorgu aracılığıyla atla `HasMoreResults` ve `ExecuteNextAsync` hello örnekler hello geri kalanı için.

```cs
// Update a vertex
client.CreateGremlinQuery<Vertex>(
    graphCollection, 
    "g.V('thomas').property('age', 45)");
```

Kenarları ve Gremlin'ın kullanarak köşeleri düşürebilir `drop` adım. Gösteren parçacık İşte nasıl toodelete köşe ve bir sınır. Bir köşe bırakarak art arda silme hello işlemi gerçekleştirir Not kenarları ilişkilendirilmiş.

```cs
// Drop an edge
client.CreateGremlinQuery(graphCollection, "g.E('thomasKnowsRobin').drop()");

// Drop a vertex
client.CreateGremlinQuery(graphCollection, "g.V('robin').drop()");
```

## <a name="query-hello-graph"></a>Sorgu hello grafiği

Sorgular ve ayrıca Gremlin kullanarak çapraz geçişlerine gerçekleştirebilirsiniz. Örneğin, aşağıdaki kod parçacığında hello nasıl toocount hello hello grafik tepe sayısı gösterilir:

```cs
// Run a query toocount vertices
IDocumentQuery<int> countQuery = client.CreateGremlinQuery<int>(graphCollection, "g.V().count()");
```
Gremlin'ın kullanarak filtreler gerçekleştirebilirsiniz `has` ve `hasLabel` adımları ve bunları birleştirmek kullanarak `and`, `or`, ve `not` toobuild daha karmaşık filtreler:

```cs
// Run a query with filter
IDocumentQuery<Vertex> personsByAge = client.CreateGremlinQuery<Vertex>(
  graphCollection, 
  "g.V().hasLabel('person').has('age', gt(40))");
```

Belirli özellikler hello sorgu sonuçlarındaki hello kullanarak proje `values` . adım:

```cs
// Run a query with projection
IDocumentQuery<string> firstNames = client.CreateGremlinQuery<string>(
  graphCollection, 
  $"g.V().hasLabel('person').values('firstName')");
```

Şu ana kadar yalnızca tüm veritabanındaki iş sorgu işleçleri gördük. Toonavigate toorelated kenarları ve köşeleri gerektiğinde grafikleri hızlı ve verimli çapraz geçiş işlemleri için. Şimdi tüm arkadaşların Thomas bulun. Biz Gremlin'ın kullanarak bunu `outE` tüm hello dışarı Thomas kenarları toofind adım sonra içinde köşe için toohello Gremlin'ın kullanarak bu kenarlarından çapraz geçiş yapan `inV` . adım:

```cs
// Run a traversal (find friends of Thomas)
IDocumentQuery<Vertex> friendsOfThomas = client.CreateGremlinQuery<Vertex>(
  graphCollection,
  "g.V('thomas').outE('knows').inV().hasLabel('person')");
```

Merhaba sonraki sorgu gerçekleştirir iki atlama toofind tüm "çağırarak Thomas arkadaş arkadaş", `outE` ve `inV` iki kez. 

```cs
// Run a traversal (find friends of friends of Thomas)
IDocumentQuery<Vertex> friendsOfFriendsOfThomas = client.CreateGremlinQuery<Vertex>(
  graphCollection,
  "g.V('thomas').outE('knows').inV().hasLabel('person').outE('knows').inV().hasLabel('person')");
```

Daha karmaşık sorgular derlemek ve Gremlin, kullanarak döngü gerçekleştirme ifadeleri hello dahil olmak üzere karıştırma filtre kullanan güçlü grafik geçişi mantığı uygulamanıza `loop` adım ve hello kullanarak uygulama koşullu Gezinti `choose` adım. İle yapabilecekleriniz hakkında daha fazla bilgi [Gremlin Destek](gremlin-support.md)!

İşte bu kadar bu Azure Cosmos DB öğretici tamamlandı! 

## <a name="clean-up-resources"></a>Kaynakları temizleme

Bu uygulama toocontinue toouse denetlemeyecekseniz tüm kaynaklar Bu öğreticide hello Azure portal tarafından oluşturulan adımları toodelete aşağıdaki hello kullanın.  

1. Merhaba sol taraftaki menüden hello Azure portal'ın, **kaynak grupları** ve ardından oluşturduğunuz hello kaynak hello adına tıklayın. 
2. Kaynak grubu sayfanızda tıklatın **silmek**hello metin kutusuna hello kaynak toodelete hello adını yazın ve ardından **silmek**.

## <a name="next-steps"></a>Sonraki Adımlar

Bu öğreticide, hello aşağıdakileri yaptığınızdan:

> [!div class="checklist"]
> * Bir Azure Cosmos DB hesabı oluşturuldu 
> * Bir grafik veritabanı ve kapsayıcı oluşturuldu
> * Serileştirilmiş köşeleri ve kenarları too.NET nesneleri
> * Eklenen köşeleri ve kenarları
> * Sorgulanan hello grafik Gremlin kullanma

Artık daha karmaşık sorgular oluşturabilir ve Gremlin kullanarak güçlü grafik geçişi mantığını kullanabilirsiniz. 

> [!div class="nextstepaction"]
> [Gremlin kullanarak sorgulama](tutorial-query-graph.md)
