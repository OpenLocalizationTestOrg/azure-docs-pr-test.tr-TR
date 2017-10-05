---
title: "Değişiklik çalışmak akışı destek Azure Cosmos DB'de | Microsoft Docs"
description: "Belgelerdeki değişiklikleri izlemek ve tetikleyiciler gibi olay tabanlı işleme ve önbellekleri ve analizi sistemleri güncel tutma gerçekleştirmek için Azure Cosmos DB Değiştir Akış desteği kullanın."
keywords: "Akış Değiştir"
services: cosmos-db
author: arramac
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: 2d7798db-857f-431a-b10f-3ccbc7d93b50
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: rest-api
ms.topic: article
ms.date: 08/15/2017
ms.author: arramac
ms.openlocfilehash: 160fbc98e0f3dcc7d17cbe0c7f7425811596a896
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="working-with-the-change-feed-support-in-azure-cosmos-db"></a>Destek Azure Cosmos DB'de akış değişiklik ile çalışma
[Azure Cosmos DB](../cosmos-db/introduction.md) bir hızlı ve esnek genel olarak, yazma ve okuma için tahmin edilebilir tek basamaklı milisaniyelik gecikme süresine sahip yüksek hacimli işlem ve işletimsel verileri depolamak için kullanılan veritabanı hizmeti çoğaltılır. Bu, oldukça uygun perakende, oyun, IOT ve işlem günlüğü uygulamaları için kolaylaştırır. Bu uygulamalar ortak tasarım modelinde olan Azure Cosmos DB verilerde yapılan değişiklikleri izlemek ve gerçekleştirilmiş görünümlere güncelleştirmek, gerçek zamanlı analiz gerçekleştirmek, verileri soğuk depolama ve bu değişikliklere dayalı belirli olayları bildirimlerini tetiklemesini arşivlemek için. **Değişiklik akışı Destek** Azure Cosmos DB'de, verimli ve ölçeklenebilir çözümler her bu düzenlerin oluşturmanıza olanak sağlar.

Destek akış değişiklikle Azure Cosmos DB belgelerinin Azure Cosmos DB koleksiyonu değiştirilmiş sırada içindeki sıralanmış bir listesini sağlar. Bu akışın koleksiyonundaki veri değişiklikleri dinler ve gibi eylemleri gerçekleştirmek için kullanılabilir:

* Bir belge eklendiğinde veya değiştiren bir API çağrısı Tetikle
* Gerçek zamanlı (akış) yönlendirilmeden güncelleştirmeleri
* Önbellek, arama motoru veya veri ambarı veri eşitleme

Azure Cosmos DB değişiklikler kalıcı zaman uyumsuz olarak işlenir ve Paralel işleme için bir veya daha fazla tüketiciye dağıtılmış. Değişiklik akış ve gerçek zamanlı ölçeklenebilir uygulamalar oluşturmak için bunları nasıl kullanabileceğiniz API'ler bakalım. Bu makalede Azure Cosmos DB Değiştir Akış ve DocumentDB API ile nasıl çalışılacağı gösterilmektedir. 

![Akış güç gerçek zamanlı analiz ve bilgi işlem senaryolarına olay denetimli için Azure Cosmos DB Değiştir kullanma](./media/change-feed/changefeedoverview.png)

> [!NOTE]
> Destek akış değişiklik, yalnızca şu anda DocumentDB API'si için sağlanır; Tablo API ve grafik API'si şu anda desteklenmemektedir.

## <a name="use-cases-and-scenarios"></a>Kullanım örnekleri ve senaryoları
Değişiklik akış yüksek hacimli yazma ile büyük veri verimli işlemeye olanak sağlar ve nelerin değiştiğini belirlemek için tüm veri kümeleri sorgulama için bir alternatif sunar. Örneğin, aşağıdaki görevleri etkin şekilde gerçekleştirebilirsiniz:

* Bir önbellek, arama dizini ya da bir veri ambarı Azure Cosmos DB içinde depolanan veriler ile güncelleştirecek.
* Uygulama düzeyi verileri katmanlama ve arşivleme uygulamak, diğer bir deyişle, Azure Cosmos DB'de "etkin verileri" depolamak ve "soğuk veri çıkış" geçerlilik süresi [Azure Blob Storage](../storage/common/storage-introduction.md) veya [Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md).
* Verileri kullanarak toplu analizi uygulamak [Apache Hadoop](run-hadoop-with-hdinsight.md).
* Uygulama [lambda işlem hatları Azure üzerinde](https://blogs.technet.microsoft.com/msuspartner/2016/01/27/azure-partner-community-big-data-advanced-analytics-and-lambda-architecture/) Azure Cosmos DB ile. Azure Cosmos DB alımı ve sorgu işleyen ve düşük ile lambda mimariyi uygulayan ölçeklenebilir veritabanı çözümü sağlar. 
* Farklı bir bölümleme düzeni ile başka bir Azure Cosmos DB hesabına sıfır kapalı kalma süresi geçişler gerçekleştirin.

**Azure Cosmos DB alımı ve sorgu için sahip lambda ardışık düzenler:**

![Azure Cosmos DB lambda ardışık düzeni alımı ve sorgu için temel](./media/change-feed/lambda.png)

Cihazlar, algılayıcılar, altyapı ve uygulamalardan olay veri depolamak ve almak için Azure Cosmos DB kullanın ve bu olayları işleme ile gerçek zamanlı [Azure akış analizi](../stream-analytics/stream-analytics-documentdb-output.md), [Apache Storm](../hdinsight/hdinsight-storm-overview.md), veya [Apache Spark](../hdinsight/hdinsight-apache-spark-overview.md). 

İçinde [sunucusuz](http://azure.com/serverless) web ve mobil uygulamaları, yapabilecekleriniz müşterinizin profili, tercihlerine veya konumu kullanarak cihazlarını anında iletme bildirimleri gönderme gibi belirli eylemleri tetiklemek için değişiklik izleme olaylarına [ Azure işlevleri](../azure-functions/functions-bindings-documentdb.md) veya [uygulama hizmetleri](https://azure.microsoft.com/services/app-service/). Oyun oluşturmak için Azure Cosmos DB kullanıyorsanız, şunları yapabilirsiniz, örneğin, kullanım tamamlanmış oyunlar gelen puanları göre gerçek zamanlı liderlik uygulamak için akış değiştirin.

## <a name="how-change-feed-works-in-azure-cosmos-db"></a>Değişiklik akış Azure Cosmos DB'de nasıl çalışır?
Azure Cosmos DB artımlı olarak bir Azure Cosmos DB koleksiyona yapılan güncelleştirmeler okuma özelliği sağlar. Bu değişiklik akışın aşağıdaki özelliklere sahiptir:

* Değişiklikler Azure Cosmos DB'de kalıcı ve zaman uyumsuz olarak işlenir.
* Bir koleksiyon içindeki belgelerde yapılan değişiklikler, akış değişikliği hemen kullanılabilir.
* Bir belgeyi her değişiklik akış değişikliği tam olarak bir kez görünür ve bunların denetim noktası oluşturma mantığı istemcileri yönetmek. Değişiklik akış işlemci kitaplığı otomatik denetim noktası oluşturma ve "en az bir kez" semantiği sağlar.
* Yalnızca en son değişiklik belirli bir belge için değişiklik günlüğünde yer alır. Ara değişikliklerin kullanılamayabilir.
* Değişiklik akışı, her bölüm anahtarı değerini içinde değişiklik sırasına göre sıralanır. Bölüm anahtarı değerleri arasında hiçbir garanti edilen sipariş yoktur.
* Değişiklikleri herhangi noktası zaman eşitlenebilir, diğer bir deyişle, değişiklikler kullanılabilir hiçbir sabit veri saklama süresi vardır.
* Değişiklikler bölüm anahtar aralıklarına yığınlar halinde kullanılabilir. Bu özellik paralel olarak birden çok tüketiciye/sunucuları tarafından işlenmek üzere büyük topluluklara değişikliklerden sağlar.
* Uygulamalar için aynı koleksiyon üzerinde eşzamanlı olarak birden çok değişikliği akışları isteyebilir.

Azure Cosmos veritabanı değişikliği akış tüm hesapları için varsayılan olarak etkindir. Kullanabilirsiniz, [sağlanan işleme](request-units.md) yazma bölgenize veya herhangi bir [bölge okuma](distribute-data-globally.md) akış değişikliği okumak için olduğu gibi Azure Cosmos DB'den başka bir işlem. Değişiklik akış ekler ve koleksiyon içindeki belgelerde yapılan güncelleştirme işlemlerini içerir. Siler yakalayabilirsiniz belgelerinizi siler yerine içinde "soft-Sil" bayrağını ayarlayarak. Alternatif olarak, sınırlı bir süre belgeleriniz için ayarlayabileceğiniz [TTL yetenek](time-to-live.md), örneğin, 24 saat ve siler yakalamak için o özelliğin değerini kullanın. Bu çözüm ile TTL sona erme süresinden daha kısa bir zaman aralığındaki değişiklikleri işlemeye sahip. Değişiklik akışı her bölüm anahtarı aralığının belge koleksiyonundaki için kullanılabilir ve bu nedenle bir veya daha fazla tüketiciye paralel işleme üzerinden dağıtılabilir. 

![Azure Cosmos DB değişimin dağıtılmış işlem akışı](./media/change-feed/changefeedvisual.png)

İstemci kodunuzda akışı bir değişiklik nasıl uygulayacağınıza, birkaç seçeneğiniz vardır. Hemen bölümlerde Azure Cosmos DB REST API ve DocumentDB SDK'ları kullanarak akış değişikliği uygulamak nasıl açıklar. Ancak, .NET uygulamaları için yeni kullanmanızı öneririz [değişiklik akış işlemci Kitaplığı](#change-feed-processor) değişikliği olayları işlemek için akış olarak bölümler okuma değişiklikleri basitleştirir ve birden çok iş parçacığı üzerinde çalışırken sağlar Paralel. 

## <a id="rest-apis"></a>REST API ve DocumentDB SDK'ları ile çalışma
Azure Cosmos DB sağlar, depolama ve işleme adlı esnek kapsayıcıları **koleksiyonları**. Veri koleksiyonları içinde mantıksal olarak gruplandırılmış kullanarak [bölüm anahtarlarını](partition-data.md) ölçeklenebilirlik ve performans. Azure Cosmos DB arama kimliği (okuma/Get), sorgu ve okuma beslemelerini (taramalar) dahil olmak üzere bu verilerine erişmek için çeşitli API'ler sağlar. DocumentDB için iki yeni istek üstbilgileri doldurarak değişiklik akış alınabilir `ReadDocumentFeed` API'sini ve bölüm anahtarlarını aralıklar paralel olarak işlenebilir.

### <a name="readdocumentfeed-api"></a>ReadDocumentFeed API
ReadDocumentFeed nasıl çalıştığı bir kısa bakalım. Azure Cosmos DB destekleyen bir akış bir koleksiyon içinde belgelerin okuma `ReadDocumentFeed` API. Örneğin, aşağıdaki isteği belgeleri içinde bir sayfasını döndürür `serverlogs` koleksiyonu. 

    GET https://mydocumentdb.documents.azure.com/dbs/smalldb/colls/serverlogs HTTP/1.1
    x-ms-date: Tue, 22 Nov 2016 17:05:14 GMT
    authorization: type%3dmaster%26ver%3d1.0%26sig%3dgo7JEogZDn6ritWhwc5hX%2fNTV4wwM1u9V2Is1H4%2bDRg%3d
    Cache-Control: no-cache
    x-ms-consistency-level: Strong
    User-Agent: Microsoft.Azure.Documents.Client/1.10.27.5
    x-ms-version: 2016-07-11
    Accept: application/json
    Host: mydocumentdb.documents.azure.com

Sonuçları kullanarak bunlarla sınırlı `x-ms-max-item-count` üstbilgi ve okuma sürdürüldü istekle yeniden göndermeden bir `x-ms-continuation` üstbilgi önceki yanıtta döndürülen. Tek bir istemciden gerçekleştirildiğinde `ReadDocumentFeed` seri olarak bölümler sonuçları arasında yineler. 

**Seri belge akışı okuma**

Desteklenen birini kullanarak belgelerin akış de alabilirsiniz [Azure Cosmos DB SDK'ları](documentdb-sdk-dotnet.md). Örneğin, aşağıdaki kod parçacığını nasıl kullanılacağını gösterir [ReadDocumentFeedAsync yöntemi](/dotnet/api/microsoft.azure.documents.client.documentclient.readdocumentfeedasync?view=azure-dotnet) .NET içinde.

```csharp
FeedResponse<dynamic> feedResponse = null;
do
{
    feedResponse = await client.ReadDocumentFeedAsync(collection, new FeedOptions { MaxItemCount = -1 });
}
while (feedResponse.ResponseContinuation != null);
```

### <a name="distributed-execution-of-readdocumentfeed"></a>ReadDocumentFeed dağıtılmış yürütülmesi
Veri ya da daha fazla terabayt içeren veya büyük miktarda güncelleştirme alma koleksiyonlar için tek istemci makineye okuma akıştan seri yürütülmesi pratik olmayabilir. Bu büyük veri senaryolarını desteklemek için Azure Cosmos DB dağıtmak için API'ler sağlar `ReadDocumentFeed` çağrıları saydam birden çok istemci okuyucular/tüketicileri arasında. 

**Dağıtılmış okuma belge besleme**

Sağlamak için ölçeklenebilir artımlı değişiklikler, işleme Azure Cosmos DB genişleme modeli için bölüm anahtarlarını aralıklarını temel alarak API akış değişiklik destekler.

* Bir koleksiyon gerçekleştirmek için anahtar aralıklarına bölüm listesini elde edebilirsiniz bir `ReadPartitionKeyRanges` çağırın. 
* Her bölüm anahtarı aralığının gerçekleştirdiğiniz bir `ReadDocumentFeed` bu aralıkta bölüm anahtarlarla belgeleri okumak için.

### <a name="retrieving-partition-key-ranges-for-a-collection"></a>Bir koleksiyon için bölüm anahtarı aralıkları alma
Bölüm anahtarı aralıkları isteyerek alabilir `pkranges` bir koleksiyon içindeki kaynak. Örneğin aşağıdaki isteği bölüm anahtarı aralıklarını listesini alır `serverlogs` koleksiyonu:

    GET https://querydemo.documents.azure.com/dbs/bigdb/colls/serverlogs/pkranges HTTP/1.1
    x-ms-date: Tue, 15 Nov 2016 07:26:51 GMT
    authorization: type%3dmaster%26ver%3d1.0%26sig%3dEConYmRgDExu6q%2bZ8GjfUGOH0AcOx%2behkancw3LsGQ8%3d
    x-ms-consistency-level: Session
    x-ms-version: 2016-07-11
    Accept: application/json
    Host: querydemo.documents.azure.com

Bu istek bölüm anahtar aralıklarına hakkındaki meta verileri içeren aşağıdaki yanıtı döndürür:

    HTTP/1.1 200 Ok
    Content-Type: application/json
    x-ms-item-count: 25
    x-ms-schemaversion: 1.1
    Date: Tue, 15 Nov 2016 07:26:51 GMT

    {
       "_rid":"qYcAAPEvJBQ=",
       "PartitionKeyRanges":[
          {
             "_rid":"qYcAAPEvJBQCAAAAAAAAUA==",
             "id":"0",
             "_etag":"\"00002800-0000-0000-0000-580ac4ea0000\"",
             "minInclusive":"",
             "maxExclusive":"05C1CFFFFFFFF8",
             "_self":"dbs\/qYcAAA==\/colls\/qYcAAPEvJBQ=\/pkranges\/qYcAAPEvJBQCAAAAAAAAUA==\/",
             "_ts":1477100776
          },
          ...
       ],
       "_count": 25
    }


**Bölüm anahtarı aralığının özellikleri**: her bölüm anahtarı aralığının aşağıdaki tabloda meta veri özelliklerini içerir:

<table>
    <tr>
        <th>Üstbilgi adı</th>
        <th>Açıklama</th>
    </tr>
    <tr>
        <td>id</td>
        <td>
            <p>Bölüm anahtarı aralığının kimliği. Her bir koleksiyonun içindeki kararlı ve benzersiz bir kimliği budur.</p>
            <p>Aşağıdaki çağrısında değişiklikleri okumak için bölüm anahtarı aralığının tarafından kullanılması gerekir.</p>
        </td>
    </tr>
    <tr>
        <td>maxExclusive</td>
        <td>Bölüm anahtarı aralığının en fazla bölüm anahtar karma değeri. İç kullanım için.</td>
    </tr>
    <tr>
        <td>minInclusive</td>
        <td>Bölüm anahtarı aralığının en düşük bölüm anahtar karma değeri. İç kullanım için.</td>
    </tr>       
</table>

Desteklenen birini kullanarak bunu yapabilirsiniz [Azure Cosmos DB SDK'ları](documentdb-sdk-dotnet.md). Örneğin, aşağıdaki kod parçacığında bölüm anahtar aralıklarına .NET kullanarak almak gösterilmiştir [ReadPartitionKeyRangeFeedAsync](/dotnet/api/microsoft.azure.documents.client.documentclient.readpartitionkeyrangefeedasync?view=azure-dotnet) yöntemi.

```csharp
string pkRangesResponseContinuation = null;
List<PartitionKeyRange> partitionKeyRanges = new List<PartitionKeyRange>();

do
{
    FeedResponse<PartitionKeyRange> pkRangesResponse = await client.ReadPartitionKeyRangeFeedAsync(
        collectionUri, 
        new FeedOptions { RequestContinuation = pkRangesResponseContinuation });

    partitionKeyRanges.AddRange(pkRangesResponse);
    pkRangesResponseContinuation = pkRangesResponse.ResponseContinuation;
}
while (pkRangesResponseContinuation != null);
```

Azure Cosmos DB isteğe bağlı ayarlayarak bölüm anahtarı aralığının başına belge alınmasını destekler `x-ms-documentdb-partitionkeyrangeid` üstbilgi. 

### <a name="performing-an-incremental-readdocumentfeed"></a>Bir artımlı ReadDocumentFeed gerçekleştirme
ReadDocumentFeed değişiklikleri Azure Cosmos DB koleksiyonlarda artımlı işleme için aşağıdaki senaryoları/görevleri destekler:

* Başlangıçtan itibaren belgelere tüm değişiklikler, diğer bir deyişle, koleksiyon oluşturulması okuyun.
* Geçerli zamandan ilerideki güncelleştirmeler belgeleri için yapılan tüm değişiklikler veya bir kullanıcı tarafından belirtilen zaman bu yana değişiklikler okuyun.
* Tüm değişiklikleri (ETag) koleksiyon mantıksal bir sürümünden belgeleri okuyun. Denetim noktası artımlı okuma akışı isteklerinden döndürülen ETag göre tüketicileriniz olabilir.

Değişiklikleri ekler içeren ve belge güncelleştirmeleri. Siler yakalamak için bir "geçici silme" özelliği, belgeler içinde veya kullanmanız gerekir, kullanmak [yerleşik TTL özelliği](time-to-live.md) akış değişiklik bekleyen bir değişikliği göstermek için.

Aşağıdaki tabloda [isteği](/rest/api/documentdb/common-documentdb-rest-request-headers.md) ve [yanıt üstbilgilerini](/rest/api/documentdb/common-documentdb-rest-response-headers.md) ReadDocumentFeed işlemleri için.

**İstek üstbilgileri için artımlı ReadDocumentFeed**:

<table>
    <tr>
        <th>Üstbilgi adı</th>
        <th>Açıklama</th>
    </tr>
    <tr>
        <td>BİR IM</td>
        <td>"Artımlı akışına" ayarlayın veya gerekir aksi takdirde atlanmış</td>
    </tr>
    <tr>
        <td>If-None-Match</td>
        <td>
            <p>Başlık: tüm değişiklikleri (oluşturma koleksiyonu) baştan döndürür</p>
            <p>"*": tüm yeni değişiklikleri veri koleksiyonundaki döndürür</p>           
            <p>&lt;ETag&gt;: ETag, koleksiyon kümesine döndürürse mantıksal zaman damgası itibaren yapılan tüm değişiklikler</p>
        </td>
    </tr>
    <tr>    
        <td>If-Modified-Since</td> 
        <td>RFC 1123 saat biçimi; If-None-Match belirtilmişse göz ardı</td> 
    </tr> 
    <tr>
        <td>x-ms-documentdb-partitionkeyrangeid</td>
        <td>Verilerin okunması için bölüm anahtarı aralığının kimliği.</td>
    </tr>
</table>

**Yanıt üstbilgileri için artımlı ReadDocumentFeed**:

<table> <tr>
        <th>Üstbilgi adı</th>
        <th>Açıklama</th>
    </tr>
    <tr>
        <td>ETag</td>
        <td>
            <p>Yanıtta döndürülen son belgenin mantıksal sıra numarası (LSN).</p>
            <p>Artımlı ReadDocumentFeed If-None-Match bu değeri yeniden göndermeden ettirilebilir.</p>
        </td>
    </tr>
</table>

Mantıksal sürüm/Etag'den koleksiyonundaki tüm artımlı değişiklikler döndürülecek bir örnek istek işte `28535` ve bölüm anahtarı aralığının = `16`:

    GET https://mydocumentdb.documents.azure.com/dbs/bigdb/colls/bigcoll/docs HTTP/1.1
    x-ms-max-item-count: 1
    If-None-Match: "28535"
    A-IM: Incremental feed
    x-ms-documentdb-partitionkeyrangeid: 16
    x-ms-date: Tue, 22 Nov 2016 20:43:01 GMT
    authorization: type%3dmaster%26ver%3d1.0%26sig%3dzdpL2QQ8TCfiNbW%2fEcT88JHNvWeCgDA8gWeRZ%2btfN5o%3d
    x-ms-version: 2016-07-11
    Accept: application/json
    Host: mydocumentdb.documents.azure.com

Değişiklikleri süre içinde bölüm anahtarı aralığının her bölüm anahtarı değerine göre sıralanır. Bölüm anahtarı değerleri arasında hiçbir garanti edilen sipariş yoktur. Tek bir sayfayla sığmayacak daha fazla sonuç yoksa istekle yeniden göndermeden sonraki sonuç sayfasını okuyabilirsiniz `If-None-Match` değerine eşit bir değer üstbilgiyle `etag` önceki yanıt gelen. Birden çok belge eklendi veya işlemsel olarak bir saklı yordam veya tetikleyici içinde güncelleştirildi, bunların tümü aynı yanıt sayfa içinde döndürülür.

> [!NOTE]
> Değişiklik akış ile daha fazla öğe bir sayfa içinde belirtilenden döndürülen alabilirsiniz `x-ms-max-item-count` eklenir veya güncelleştirilir saklı yordamların içinde birden çok belge durumunda veya tetikler. 

.NET SDK'sı (1.17.0) kullanırken, alan kümesi `StartTime` içinde `ChangeFeedOptions` bu yana değişen belgeleri doğrudan döndürülecek `StartTime` çağrılırken `CreateDocumentChangeFeedQuery`. Belirterek `If-Modified-Since` REST API kullanarak, isteğiniz belgelerin değil kendilerini ancak bunun yerine devamlılık belirteci döndürür veya `etag` yanıt üstbilgisi içinde. Belgeleri değiştiren devamlılık belirteci belirtilen zaman döndürülecek `etag` ardından sonraki istekle kullanılmalıdır `If-None-Match` gerçek belgeleri döndürülecek. 

.NET SDK'sı sağlar [CreateDocumentChangeFeedQuery](/dotnet/api/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery?view=azure-dotnet) ve [ChangeFeedOptions](/dotnet/api/microsoft.azure.documents.client.changefeedoptions?view=azure-dotnet) bir koleksiyona yapılan değişiklikler erişmek için yardımcı sınıfları. Aşağıdaki kod parçacığında, tek bir istemciden gelen .NET SDK kullanarak başından tüm değişiklikleri almak gösterilmiştir.

```csharp
private async Task<Dictionary<string, string>> GetChanges(
    DocumentClient client,
    string collection,
    Dictionary<string, string> checkpoints)
{
    string pkRangesResponseContinuation = null;
    List<PartitionKeyRange> partitionKeyRanges = new List<PartitionKeyRange>();

    do
    {
        FeedResponse<PartitionKeyRange> pkRangesResponse = await client.ReadPartitionKeyRangeFeedAsync(
            collectionUri, 
            new FeedOptions { RequestContinuation = pkRangesResponseContinuation });

        partitionKeyRanges.AddRange(pkRangesResponse);
        pkRangesResponseContinuation = pkRangesResponse.ResponseContinuation;
    }
    while (pkRangesResponseContinuation != null);

    foreach (PartitionKeyRange pkRange in partitionKeyRanges)
    {
        string continuation = null;
        checkpoints.TryGetValue(pkRange.Id, out continuation);

        IDocumentQuery<Document> query = client.CreateDocumentChangeFeedQuery(
            collection,
            new ChangeFeedOptions
            {
                PartitionKeyRangeId = pkRange.Id,
                StartFromBeginning = true,
                RequestContinuation = continuation,
                MaxItemCount = 1
            });

        while (query.HasMoreResults)
        {
            FeedResponse<DeviceReading> readChangesResponse = query.ExecuteNextAsync<DeviceReading>().Result;

            foreach (DeviceReading changedDocument in readChangesResponse)
            {
                Console.WriteLine(changedDocument.Id);
            }

            checkpoints[pkRange.Id] = readChangesResponse.ResponseContinuation;
        }
    }

    return checkpoints;
}
```
Ve aşağıdaki kod parçacığında, değişiklikleri işlemeye gösterilmiştir kullanarak Azure Cosmos DB ile gerçek zamanlı değişikliği desteği ve önceki işlevi akış. İlk çağrıda koleksiyondaki tüm belgeleri döndürür ve ikinci yalnızca en son kontrol bu yana oluşturulan iki belge oluşturulan döndürür.

```csharp
// Returns all documents in the collection.
Dictionary<string, string> checkpoints = await GetChanges(client, collection, new Dictionary<string, string>());

await client.CreateDocumentAsync(collection, new DeviceReading { DeviceId = "xsensr-201", MetricType = "Temperature", Unit = "Celsius", MetricValue = 1000 });
await client.CreateDocumentAsync(collection, new DeviceReading { DeviceId = "xsensr-212", MetricType = "Pressure", Unit = "psi", MetricValue = 1000 });

// Returns only the two documents created above.
checkpoints = await GetChanges(client, collection, checkpoints);
```

Seçmeli olarak olayları işlemek için istemci tarafı mantığı kullanarak akış değişiklik de filtre uygulayabilirsiniz. Örneğin, aygıt algılayıcılar yalnızca sıcaklık değişikliği olayları işlemek için istemci tarafı LINQ kullanan bir parçacığı aşağıda verilmiştir.

```csharp
FeedResponse<DeviceReading> readChangesResponse = query.ExecuteNextAsync<DeviceReading>().Result;

foreach (DeviceReading changedDocument in 
    readChangesResponse.AsEnumerable().Where(d => d.MetricType == "Temperature" && d.MetricValue > 1000L))
{
    // trigger an action, like call an API
}
```

## <a id="change-feed-processor"></a>Değişiklik işlemci akışı kitaplığı
Başka bir seçenek kullanmaktır [Azure Cosmos DB değiştirmek akış işlemci Kitaplığı](https://docs.microsoft.com/azure/cosmos-db/documentdb-sdk-dotnet-changefeed), hangi yardımcı olabilir, olay arasında birden çok tüketiciye akışı bir değişiklik gelen işleme kolayca dağıtabilirsiniz. Kitaplığı, .NET platformu üzerinde okuyucular akış değişiklik oluşturmak için mükemmeldir. Diğer Cosmos DB SDK içinde bulunan yöntemleri üzerinde değişiklik akış işlemci kitaplığı kullanılarak Basitleştirilmiş bazı iş akışları içerir: 

* Birden çok bölüm arasında veri depolandığında değişiklik çekilmesini güncelleştirmelerini akışı
* Taşıma veya verileri bir koleksiyondan çoğaltma
* Veri ve akış değişiklik güncelleştirmelerini tarafından tetiklenen eylemlerin Paralel yürütme 

Cosmos SDK API'leri kullanarak her bölüm akış güncelleştirmelerinde değiştirmek için kesin erişim sağlarken, akış işlemci değiştirmek kitaplığını kullanarak bölümler ve paralel çalışan birden çok iş parçacığı üzerinde okuma değişiklikleri basitleştirir. El ile değişiklikleri her kapsayıcıdan okuma ve kaydetme her bölüm için devamlılık belirteci yerine akış değişiklik işlemci okuma değişiklikleri bir kiralama mekanizması kullanarak bölümleri arasında otomatik olarak yönetir.

Bir NuGet paketi olarak kullanılabilir bir kitaplığıdır: [Microsoft.Azure.Documents.ChangeFeedProcessor](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.ChangeFeedProcessor/) ve bir Github olarak kaynak koddan [örnek](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/ChangeFeedProcessor). 

### <a name="understanding-change-feed-processor-library"></a>Anlama değişiklik akış işlemci kitaplığı 

Akış değişiklik işlemci gerçekleştirilmesinin dört ana bileşen mevcuttur: izlenen koleksiyonu, kira koleksiyonu, işlemci ana bilgisayar ve tüketicilerin. 

**İzlenen koleksiyonu:** değişiklik akış oluşturulan verileri izlenen koleksiyonudur. Tüm eklemeleri ve değişiklikleri izlenen koleksiyonu için koleksiyon değişiklik akışta yansıtılır. 

**Kira koleksiyonu:** arasında birden çok Worker akış değişiklik işleme kira koleksiyonu koordinatları. Ayrı bir koleksiyon, bölüm başına bir kiralama ile kiraları depolamak için kullanılır. Akış değişiklik işlemci çalıştığı yazma bölgeyi daha yakın olan farklı bir hesap üzerinde bu kira koleksiyon depolamak için avantajlıdır. Bir kira nesnesi aşağıdaki öznitelikleri içerir: 
* Sahibi: kira sahibi olan konak belirtir
* Devamlılık: belirli bir bölüm için akış değişiklik (devamlılık belirteci) konumu belirtir
* Zaman damgası: kira güncelleştirildi; son zamanı zaman damgası, kira süresi dolmuş olarak kabul edilip edilmediğini kontrol etmek için kullanılabilir 

**İşlemci ana bilgisayarı:** etkin kiralamaları kaç ana örneklerini olmadığına göre işlem kaç bölümler her konak belirler. 
1.  Bir ana bilgisayar başlatıldığında tüm ana bilgisayarlar arasında iş yükünü dengelemek için kiraları alır. Kira etkin şekilde bir ana bilgisayar kiralama, düzenli aralıklarla yeniler. 
2.  Bir ana bilgisayar kontrol noktaları da son kirasını her devamlılık belirteci okuyun. Eşzamanlılık güvenliği sağlamak için her bir kira güncelleştirme ETag bir ana bilgisayar denetler. Diğer denetim noktası stratejileri de desteklenir.  
3.  Kapatma, bağlı bir konak tüm kira serbest bırakır, ancak depolanan denetim noktası dosyasından okuma daha sonra devam edebilmek için devamlılık bilgileri tutar. 

Şu anda konakların sayısı bölümleri (kiraları) sayısından büyük olamaz.

**Tüketiciler:** tüketici veya çalışanları olan her konak tarafından başlatılan akış değişiklik yönlendirilmeden iş parçacığı. Her işlemci ana bilgisayarın birden çok tüketiciye sahip olabilir. Her bir tüketici değişikliği atandığı bölümünden akış ve değişiklikleri ana bilgisayar bildirir ve kira süresi okur.

Daha fazla değişiklik akış işlemci dört bu unsuru birlikte nasıl çalıştığını anlamak için aşağıdaki diyagramda bir örnekte bakalım. İzlenen koleksiyonu belgeleri depolar ve "Şehir" Bölüm anahtarı olarak kullanır. Mavi bölüm "Şehir" alanını "A-E" belgeler vb. içerdiğini görürsünüz. Her iki tüketicileri paralel dört bölümden okuma ile iki ana vardır. Oklar, belirli bir nokta akış değişikliği okuma tüketicileri gösterir. Mavi akış değişiklik zaten okuma değişiklikleri temsil ederken, ilk bölümü Koyu mavi okunmamış değişiklikler temsil eder. Ana bilgisayarlar, her tüketici geçerli okuma konumunu izlemek için bir "devamlılık" değeri depolamak için kira koleksiyonunu kullanın. 

![Azure Cosmos DB değişikliği kullanarak akış işlemcisi konağı](./media/change-feed/changefeedprocessornew.png)

### <a name="using-change-feed-processor-library"></a>Değişiklik kullanarak akış işlemci kitaplığı 
Aşağıdaki bölümde, bir hedef koleksiyona kaynak koleksiyondan değişiklikleri çoğaltmaya bağlamı değişiklik akış işlemci kitaplıkta kullanımı açıklanmaktadır. Burada, kaynak koleksiyonu değişiklik akış işlemcide izlenen koleksiyonudur. 

**Yükleme ve değişiklik akış işlemci NuGet paketini ekleyin** 

Değişiklik akış işlemci NuGet paketini yüklemeden önce ilk yükleyin: 
* Microsoft.Azure.DocumentDB, sürüm 1.13.1 veya üstü 
* Newtonsoft.Json, sürüm 9.0.1 veya yükleme yukarıda `Microsoft.Azure.DocumentDB.ChangeFeedProcessor` ve bir başvuru olarak dahil edin.

**İzlenen, kiralama ve hedef koleksiyon oluşturma** 

Değişiklik akış işlemci kitaplığı kullanmak için kira koleksiyonu işlemci boşaltıyor çalıştırmadan önce oluşturulması gerekir. Yeniden bölgesiyle akış değişiklik işlemci çalıştığı için yazma yakın farklı bir hesap üzerinde bir kira koleksiyon depolamanızı öneririz. Bu veri taşıma örneği oluşturmamız değişiklik akış işleyicisi konağı çalıştırmadan önce hedef koleksiyonu gerekir. Kiralanmış, izlenen, oluşturmak için yardımcı yöntem diyoruz örnek kod ve zaten mevcut değilse hedef koleksiyonları. 

> [!WARNING]
> Uygulamanın Azure Cosmos DB ile iletişim kurmak işleme ayırma gibi bir koleksiyon oluşturma, fiyatlandırmaya vardır. Daha fazla ayrıntı için lütfen ziyaret [fiyatlandırma sayfası](https://azure.microsoft.com/pricing/details/cosmos-db/)
> 
> 

*İşlemci konak oluşturma*

`ChangeFeedProcessorHost` Sınıfı, olay işlemcisi uygulamaları için aynı zamanda denetim noktası oluşturma ve bölüm kiralama Yönetimi sağlayan bir iş parçacığı, çok işlemli, güvenli çalışma zamanı ortamı sağlar. Kullanılacak `ChangeFeedProcessorHost` sınıfı, uygulayabilirsiniz `IChangeFeedObserver`. Bu arabirim üç yöntem içerir:

* `OpenAsync`: Bu işlev, değişiklik akış gözlemci açıldığında çağrılır. Tüketici/gözlemci açıldığında, belirli bir eylemi gerçekleştirmek için değiştirilebilir.  
* `CloseAsync`: Değişiklik akış gözlemci sonlandırıldığında bu işlev çağrılır. Tüketici/gözlemci kapatıldığında belirli bir eylemi gerçekleştirmek için değiştirilebilir.  
* `ProcessChangesAsync`: Belge yeni değişiklikleri değişiklik Besleme üzerindeki kullanılabilir olduğunda bu işlev çağrılır. Güncelleştirme akışı her değişiklik sırasında belirli bir eylemi gerçekleştirmek için değiştirilebilir.  

Bizim örneğimizde, biz arabirimini uygulayan `IChangeFeedObserver` aracılığıyla `DocumentFeedObserver` sınıfı. Burada, `ProcessChangesAsync` işlev değişikliği belgeden akışı hedef koleksiyona upserts (güncelleştirmeler). Bu örnek veri bir koleksiyondan başka bir veri kümesinin bölüm anahtarı değiştirmek için taşıma için kullanışlıdır. 

*İşlemci ana çalışan*

Olay işleme başlamadan önce her ikisi de akış seçeneklerini değiştirin ve akış konak seçeneklerini değiştirme özelleştirilebilir. 
```csharp
    // Customizable change feed option and host options 
    ChangeFeedOptions feedOptions = new ChangeFeedOptions();

    // ie customize StartFromBeginning so change feed reads from beginning
    // can customize MaxItemCount, PartitonKeyRangeId, RequestContinuation, SessionToken and StartFromBeginning
    feedOptions.StartFromBeginning = true;

    ChangeFeedHostOptions feedHostOptions = new ChangeFeedHostOptions();

    // ie. customizing lease renewal interval to 15 seconds
    // can customize LeaseRenewInterval, LeaseAcquireInterval, LeaseExpirationInterval, FeedPollDelay 
    feedHostOptions.LeaseRenewInterval = TimeSpan.FromSeconds(15);

```
Özelleştirilebilir belirli alanları aşağıdaki tabloda özetlenmiştir. 

**Akış seçeneklerini değiştirme**:
<table>
    <tr>
        <th>Özellik adı</th>
        <th>Açıklama</th>
    </tr>
    <tr>
        <td>MaxItemCount</td>
        <td>Alır veya numaralandırma işlemi Azure Cosmos DB veritabanı Hizmet döndürülecek öğe sayısının üst sınırını ayarlar.</td>
    </tr>
    <tr>
        <td>PartitionKeyRangeId</td>
        <td>Kimliğini alır veya bölüm anahtarı aralığının geçerli istek için Azure Cosmos DB veritabanı hizmetinin ayarlar.</td>
    </tr>
    <tr>
        <td>RequestContinuation</td>
        <td>Alır veya Azure Cosmos DB veritabanı hizmeti isteği devamlılık belirteci ayarlar.</td>
    </tr>
        <tr>
        <td>SessionToken</td>
        <td>Alır veya Azure Cosmos DB veritabanı hizmetinde oturum tutarlılığı ile kullanmak için oturum belirteci ayarlar.</td>
    </tr>
        <tr>
        <td>StartFromBeginning</td>
        <td>Alır veya Azure Cosmos DB veritabanı hizmetinin akış değişiklik başına (true) ya da geçerli (false) başlamalıdır olup olmadığını ayarlar. Varsayılan olarak, geçerli (false) başlar.</td>
    </tr>
</table>

**Akış konak seçeneklerini değiştirme**:
<table>
    <tr>
        <th>Özellik adı</th>
        <th>Tür</th>
        <th>Açıklama</th>
    </tr>
    <tr>
        <td>LeaseRenewInterval</td>
        <td>TimeSpan</td>
        <td>Şu anda ChangeFeedEventHost örneği tarafından tutulan bölümler için seçtiğiniz aralık tüm kiraları için.</td>
    </tr>
    <tr>
        <td>LeaseAcquireInterval</td>
        <td>TimeSpan</td>
        <td>Bölümler bilinen konak örnekler arasında eşit şekilde dağıtılıp dağıtılmadığını işlem için bir görevi devre dışı kazandırın aralığı.</td>
    </tr>
    <tr>
        <td>LeaseExpirationInterval</td>
        <td>TimeSpan</td>
        <td>Kira bir bölüm temsil eden bir kira alınır aralığı. Kira bu aralıkta yenilenmezse, süresi doldu ve bölüm sahipliğini başka bir ChangeFeedEventHost örneğine taşır.</td>
    </tr>
    <tr>
        <td>FeedPollDelay</td>
        <td>TimeSpan</td>
        <td>Akış, geçerli sonra tüm değişiklikler yeni değişiklikleri boşaltmış için bir bölüm yoklama arasındaki gecikme.</td>
    </tr>
    <tr>
        <td>CheckpointFrequency</td>
        <td>CheckpointFrequency</td>
        <td>Denetim noktası kiraları için sıklığı.</td>
    </tr>
    <tr>
        <td>MinPartitionCount</td>
        <td>Int</td>
        <td>Ana bilgisayar için en düşük bölüm sayısı.</td>
    </tr>
    <tr>
        <td>MaxPartitionCount</td>
        <td>Int</td>
        <td>Ana bilgisayar hizmet verebilir bölüm maksimum sayısı.</td>
    </tr>
    <tr>
        <td>DiscardExistingLeases</td>
        <td>bool</td>
        <td>Olup tüm mevcut kiraları konak başlangıcını silinmesi gerekir ve konak baştan başlamanız gerekir.</td>
    </tr>
</table>


Olay işlemeyi başlatmak için örneği `ChangeFeedProcessorHost`, Azure Cosmos DB koleksiyonunuz için uygun parametreleri sağlayarak. Ardından, çağıran `RegisterObserverAsync` kaydetmek için `IChangeFeedObserver` (Bu örnekte DocumentFeedObserver) uygulama çalışma zamanı ile. Bu noktada, ana bilgisayar "Hızlı" algoritma kullanarak Azure Cosmos DB koleksiyondaki her bölüm anahtarı aralığının üzerinde bir kira almaya çalışır. Bu kiralar belirli bir zaman çerçevesi için en son ve sonrasında yenilenmelidir. Yeni düğüm olarak çalışan örnekleri, bu durumda, çevrimiçi olması, kiralama ayırmaları yapar ve her bir ana bilgisayar daha fazla kira elde etmeye çalışır olarak zaman içinde yük düğümler arasında kayar.. 

Örnek kodda bir fabrika sınıfı (DocumentFeedObserverFactory.cs) bir gözlemci oluşturmak için kullanırız ve `RegistObserverFactoryAsync` gözlemci kaydetmek için. 

```csharp
using (DocumentClient destClient = new DocumentClient(destCollInfo.Uri, destCollInfo.MasterKey))
    {
        DocumentFeedObserverFactory docObserverFactory = new DocumentFeedObserverFactory(destClient, destCollInfo);
        ChangeFeedEventHost host = new ChangeFeedEventHost(hostName, documentCollectionLocation, leaseCollectionLocation, feedOptions, feedHostOptions);

        await host.RegisterObserverFactoryAsync(docObserverFactory);

        Console.WriteLine("Running... Press enter to stop.");
        Console.ReadLine();

        await host.UnregisterObserversAsync();
    }
```
Zaman içerisinde bir denge sağlanır. Bu dinamik özellik CPU tabanlı ölçek büyütme ve ölçek azaltma için tüketicilere uygulanması için otomatik ölçeklendirme sağlar. Değişiklikler Azure Cosmos DB'de tüketicilerin işleyebileceğinden daha hızlı bir oranda kullanılabilir, tüketiciler üzerindeki CPU artışı çalışan örnek sayısı üzerinde otomatik ölçeklendirmeye neden için kullanılabilir.

## <a name="next-steps"></a>Sonraki adımlar
* Deneyin [Github'da Azure Cosmos DB Değiştir Akış kod örnekleri](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples/ChangeFeed)
* Kodlama ile çalışmaya başlama [Azure Cosmos DB SDK'ları](documentdb-sdk-dotnet.md) veya [REST API](/rest/api/documentdb/).
