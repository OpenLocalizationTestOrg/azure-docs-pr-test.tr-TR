---
title: "Merhaba değişiklikle aaaWorking akışı destek Azure Cosmos DB'de | Microsoft Docs"
description: "Kullanım Azure Cosmos DB akış destek tootrack değişiklik belgelerde ve tetikleyiciler gibi olay tabanlı işleme ve önbellekleri ve analizi sistemleri güncel tutma gerçekleştirin."
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
ms.openlocfilehash: a4dcf4ceb476e3e08266dbcdcbee1d75e1d1eed4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-hello-change-feed-support-in-azure-cosmos-db"></a>Merhaba değişiklik akış desteği Azure Cosmos DB ile çalışma
[Azure Cosmos DB](../cosmos-db/introduction.md) bir hızlı ve esnek genel olarak, yazma ve okuma için tahmin edilebilir tek basamaklı milisaniyelik gecikme süresine sahip yüksek hacimli işlem ve işletimsel verileri depolamak için kullanılan veritabanı hizmeti çoğaltılır. Bu, oldukça uygun perakende, oyun, IOT ve işlem günlüğü uygulamaları için kolaylaştırır. Bu uygulamalar ortak tasarım modelinde tootrack değişiklikleri tooAzure Cosmos DB verilerde yapılan ve gerçekleştirilmiş görünümlere güncelleştirme, bu değişikliklere dayalı belirli olaylar üzerinde gerçek zamanlı analytics, arşiv verileri toocold depolama ve bildirimlerini tetiklemesini gerçekleştirmek olur. Merhaba **değişiklik akışı Destek** Azure Cosmos DB'de toobuild verimli ve ölçeklenebilir çözümler her bu düzenleri için sağlar.

Destek akış değişiklikle Azure Cosmos DB hello sırada değiştirilmiş bir Azure Cosmos DB koleksiyonundaki belgelerin sıralanmış bir listesini sağlar. Bu akışın gibi eylemleri gerçekleştirmek ve değişiklikleri toodata hello koleksiyonundaki için kullanılan toolisten olmalıdır:

* Bir belge eklendiğinde veya çağrı tooan API Tetikle
* Gerçek zamanlı (akış) yönlendirilmeden güncelleştirmeleri
* Önbellek, arama motoru veya veri ambarı veri eşitleme

Azure Cosmos DB değişiklikler kalıcı zaman uyumsuz olarak işlenir ve Paralel işleme için bir veya daha fazla tüketiciye dağıtılmış. Merhaba API'leri değişiklik akış ve nasıl toobuild ölçeklenebilir gerçek zamanlı uygulamaları kullanabilmeniz için bakalım. Bu makalede, Azure Cosmos DB ile toowork nasıl değiştiğini akış ve hello DocumentDB API gösterilmektedir. 

![Akış toopower gerçek zamanlı analiz ve bilgi işlem senaryolarına olay denetimli Azure Cosmos DB Değiştir kullanma](./media/change-feed/changefeedoverview.png)

> [!NOTE]
> Destek akış değişiklik, yalnızca şu anda DocumentDB API hello için sağlanır; Merhaba grafik API'si ve tablo API şu anda desteklenmemektedir.

## <a name="use-cases-and-scenarios"></a>Kullanım örnekleri ve senaryoları
Değişiklik akış yüksek hacimli yazma ile büyük veri verimli işlemeye olanak sağlar ve bir alternatif tooquerying tüm veri kümeleri tooidentify nelerin değiştiğini sunar. Örneğin, görevleri verimli bir şekilde aşağıdaki hello gerçekleştirebilirsiniz:

* Bir önbellek, arama dizini ya da bir veri ambarı Azure Cosmos DB içinde depolanan veriler ile güncelleştirecek.
* Uygulama düzeyi verileri katmanlama ve arşivleme uygulamak, diğer bir deyişle, Azure Cosmos DB'de "etkin verileri" depolamak ve "soğuk veri çıkış" çok geçerlilik süresi[Azure Blob Storage](../storage/common/storage-introduction.md) veya [Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md).
* Verileri kullanarak toplu analizi uygulamak [Apache Hadoop](run-hadoop-with-hdinsight.md).
* Uygulama [lambda işlem hatları Azure üzerinde](https://blogs.technet.microsoft.com/msuspartner/2016/01/27/azure-partner-community-big-data-advanced-analytics-and-lambda-architecture/) Azure Cosmos DB ile. Azure Cosmos DB alımı ve sorgu işleyen ve düşük ile lambda mimariyi uygulayan ölçeklenebilir veritabanı çözümü sağlar. 
* Sıfır kapalı kalma süresi geçişler tooanother farklı bir bölümleme düzeni Azure Cosmos DB hesabıyla gerçekleştirin.

**Azure Cosmos DB alımı ve sorgu için sahip lambda ardışık düzenler:**

![Azure Cosmos DB lambda ardışık düzeni alımı ve sorgu için temel](./media/change-feed/lambda.png)

Azure Cosmos DB tooreceive kullanın ve cihazlar, algılayıcılar, altyapı ve uygulamaları olay verileri depolamak ve bu olayları işlem ile gerçek zamanlı [Azure akış analizi](../stream-analytics/stream-analytics-documentdb-output.md), [Apache Storm](../hdinsight/hdinsight-storm-overview.md), veya [Apache Spark](../hdinsight/hdinsight-apache-spark-overview.md). 

İçinde [sunucusuz](http://azure.com/serverless) web ve mobil uygulamaları, anında iletme bildirimleri tootheir aygıtlarını kullanarakgöndermegibibelirlieylemlerideğişiklikleritooyourMüşteri'ninprofili,tercihlerineveyakonumutootriggergibiizlemeolaylarıiçin[Azure işlevleri](../azure-functions/functions-bindings-documentdb.md) veya [uygulama hizmetleri](https://azure.microsoft.com/services/app-service/). Örneğin, Azure Cosmos DB toobuild oyun kullanıyorsanız, değişiklik akış tooimplement gerçek zamanlı liderlik tamamlanmış oyunlar gelen puanları temel kullanabilirsiniz.

## <a name="how-change-feed-works-in-azure-cosmos-db"></a>Değişiklik akış Azure Cosmos DB'de nasıl çalışır?
Azure Cosmos DB hello özelliği tooincrementally yapılan güncelleştirmeler tooan Azure Cosmos DB koleksiyonu okuma sağlar. Bu değişiklik akışın hello aşağıdaki özelliklere sahiptir:

* Değişiklikler Azure Cosmos DB'de kalıcı ve zaman uyumsuz olarak işlenir.
* Bir koleksiyon içinde değişiklikleri toodocuments hemen hello değişiklik akışta kullanılabilir.
* Her değişiklik tooa belge hello değişiklik akışta tam olarak bir kez görünür ve kendi denetim noktası oluşturma mantığı istemcilerini yönetme. Merhaba değişiklik akış işlemci kitaplığı otomatik denetim noktası oluşturma ve "en az bir kez" semantiği sağlar.
* Belirli bir belge için yalnızca hello en son değişiklik hello değişiklik günlüğünde yer alır. Ara değişikliklerin kullanılamayabilir.
* Merhaba değişiklik akışı, her bölüm anahtarı değerini içinde değişiklik sırasına göre sıralanır. Bölüm anahtarı değerleri arasında hiçbir garanti edilen sipariş yoktur.
* Değişiklikleri herhangi noktası zaman eşitlenebilir, diğer bir deyişle, değişiklikler kullanılabilir hiçbir sabit veri saklama süresi vardır.
* Değişiklikler bölüm anahtar aralıklarına yığınlar halinde kullanılabilir. Bu özellik paralel olarak birden çok tüketiciye/sunucuları tarafından işlenen büyük topluluklara toobe değişikliklerden sağlar.
* Uygulamaları birden çok değişikliği aynı anda hello üzerinde aynı akışları için isteyebileceği koleksiyonu.

Azure Cosmos veritabanı değişikliği akış tüm hesapları için varsayılan olarak etkindir. Kullanabilirsiniz, [sağlanan işleme](request-units.md) yazma bölgenize veya herhangi [bölge okuma](distribute-data-globally.md) hello gelen tooread akışı, başka bir işlem Azure Cosmos DB'den gibi değiştirin. Merhaba değişiklik akış ekler ve toodocuments hello koleksiyonundaki yapılan güncelleştirme işlemlerini içerir. Siler yakalayabilirsiniz belgelerinizi siler yerine içinde "soft-Sil" bayrağını ayarlayarak. Alternatif olarak, sınırlı bir süre hello aracılığıyla belgeleriniz için ayarlayabileceğiniz [TTL yetenek](time-to-live.md), örneğin, 24 saat ve kullanım değeri hello için bu özelliği toocapture siler. Bu çözüm ile Merhaba TTL sona erme süresinden daha kısa bir zaman aralığındaki tooprocess değişiklikleri sahip. Hello değişiklik akışı her bölüm anahtarı aralığının hello belge koleksiyonundaki için kullanılabilir ve bu nedenle bir veya daha fazla tüketiciye paralel işleme üzerinden dağıtılabilir. 

![Azure Cosmos DB değişimin dağıtılmış işlem akışı](./media/change-feed/changefeedvisual.png)

İstemci kodunuzda akışı bir değişiklik nasıl uygulayacağınıza, birkaç seçeneğiniz vardır. İzleme açıklamak hemen nasıl tooimplement hello Azure Cosmos DB REST API'sini kullanarak değişiklik akış hello ve DocumentDB SDK'ları hello Merhaba, bölümler. Ancak, .NET uygulamaları için hello yeni kullanmanızı öneririz [değişiklik akış işlemci Kitaplığı](#change-feed-processor) okuma değişiklikleri bölümler basitleştirir ve birden çok iş parçacığı üzerinde çalışırken etkinleştirir hello işleme olaylarından akış değiştirin Paralel. 

## <a id="rest-apis"></a>REST API ve DocumentDB SDK'ları Hello ile çalışma
Azure Cosmos DB sağlar, depolama ve işleme adlı esnek kapsayıcıları **koleksiyonları**. Veri koleksiyonları içinde mantıksal olarak gruplandırılmış kullanarak [bölüm anahtarlarını](partition-data.md) ölçeklenebilirlik ve performans. Azure Cosmos DB arama kimliği (okuma/Get), sorgu ve okuma beslemelerini (taramalar) dahil olmak üzere bu verilerine erişmek için çeşitli API'ler sağlar. Merhaba değişiklik akışı iki yeni istek üstbilgileri toohello DocumentDB doldurarak elde edilebilir `ReadDocumentFeed` API'sini ve bölüm anahtarlarını aralıklar paralel olarak işlenebilir.

### <a name="readdocumentfeed-api"></a>ReadDocumentFeed API
ReadDocumentFeed nasıl çalıştığı bir kısa bakalım. Azure Cosmos DB destekleyen bir akış hello aracılığıyla bir koleksiyon içinde belgelerin okuma `ReadDocumentFeed` API. Örneğin, hello aşağıdaki isteği belgeleri hello içinde bir sayfa döndürür `serverlogs` koleksiyonu. 

    GET https://mydocumentdb.documents.azure.com/dbs/smalldb/colls/serverlogs HTTP/1.1
    x-ms-date: Tue, 22 Nov 2016 17:05:14 GMT
    authorization: type%3dmaster%26ver%3d1.0%26sig%3dgo7JEogZDn6ritWhwc5hX%2fNTV4wwM1u9V2Is1H4%2bDRg%3d
    Cache-Control: no-cache
    x-ms-consistency-level: Strong
    User-Agent: Microsoft.Azure.Documents.Client/1.10.27.5
    x-ms-version: 2016-07-11
    Accept: application/json
    Host: mydocumentdb.documents.azure.com

Sonuçları hello kullanarak bunlarla sınırlı `x-ms-max-item-count` üstbilgi ve okuma sürdürüldü hello isteğini yeniden göndermeden bir `x-ms-continuation` üstbilgi hello önceki yanıtta döndürülen. Tek bir istemciden gerçekleştirildiğinde `ReadDocumentFeed` seri olarak bölümler sonuçları arasında yineler. 

**Seri belge akışı okuma**

Desteklenen hello birini kullanarak belgelerin hello akışı da alabilir [Azure Cosmos DB SDK'ları](documentdb-sdk-dotnet.md). Örneğin, kod parçacığında gösterildiği nasıl aşağıdaki hello toouse hello [ReadDocumentFeedAsync yöntemi](/dotnet/api/microsoft.azure.documents.client.documentclient.readdocumentfeedasync?view=azure-dotnet) .NET içinde.

```csharp
FeedResponse<dynamic> feedResponse = null;
do
{
    feedResponse = await client.ReadDocumentFeedAsync(collection, new FeedOptions { MaxItemCount = -1 });
}
while (feedResponse.ResponseContinuation != null);
```

### <a name="distributed-execution-of-readdocumentfeed"></a>ReadDocumentFeed dağıtılmış yürütülmesi
Veri ya da daha fazla terabayt içeren veya büyük miktarda güncelleştirme alma koleksiyonlar için tek istemci makineye okuma akıştan seri yürütülmesi pratik olmayabilir. Sipariş toosupport Azure Cosmos DB bu büyük veri senaryolarını sağlar API'leri toodistribute `ReadDocumentFeed` çağrıları saydam birden çok istemci okuyucular/tüketicileri arasında. 

**Dağıtılmış okuma belge besleme**

bölüm anahtarlarını aralıklarını temel alarak API Hello değişiklik akış için artımlı değişiklikler, Azure Cosmos DB ölçeklenebilir işlenmesini tooprovide genişleme modelini destekler.

* Bir koleksiyon gerçekleştirmek için anahtar aralıklarına bölüm listesini elde edebilirsiniz bir `ReadPartitionKeyRanges` çağırın. 
* Her bölüm anahtarı aralığının gerçekleştirdiğiniz bir `ReadDocumentFeed` bu aralıkta bölüm anahtarlarını tooread belgeler.

### <a name="retrieving-partition-key-ranges-for-a-collection"></a>Bir koleksiyon için bölüm anahtarı aralıkları alma
Hello bölüm anahtar aralıklarına göre isteyen hello alabilir `pkranges` bir koleksiyon içindeki kaynak. Örneğin hello aşağıdaki isteği hello listesini hello için bölüm anahtarı aralıkları alır `serverlogs` koleksiyonu:

    GET https://querydemo.documents.azure.com/dbs/bigdb/colls/serverlogs/pkranges HTTP/1.1
    x-ms-date: Tue, 15 Nov 2016 07:26:51 GMT
    authorization: type%3dmaster%26ver%3d1.0%26sig%3dEConYmRgDExu6q%2bZ8GjfUGOH0AcOx%2behkancw3LsGQ8%3d
    x-ms-consistency-level: Session
    x-ms-version: 2016-07-11
    Accept: application/json
    Host: querydemo.documents.azure.com

Bu istek hello bölüm anahtar aralıklarına hakkındaki meta verileri içeren bir yanıtı aşağıdaki hello döndürür:

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


**Bölüm anahtarı aralığının özellikleri**: her bölüm anahtarı aralığının aşağıdaki tablonun hello hello meta veri özelliklerini içerir:

<table>
    <tr>
        <th>Üstbilgi adı</th>
        <th>Açıklama</th>
    </tr>
    <tr>
        <td>id</td>
        <td>
            <p>Merhaba bölüm anahtarı aralığının Hello kimliği. Her bir koleksiyonun içindeki kararlı ve benzersiz bir kimliği budur.</p>
            <p>Aşağıdaki çağrı tooread değişiklikler hello bölüm anahtarı aralığının tarafından kullanılması gerekir.</p>
        </td>
    </tr>
    <tr>
        <td>maxExclusive</td>
        <td>Merhaba bölüm anahtarı aralığının için Hello en fazla bölüm anahtarı karma değer. İç kullanım için.</td>
    </tr>
    <tr>
        <td>minInclusive</td>
        <td>Merhaba bölüm anahtarı aralığının için Hello en az bölüm anahtarı karma değer. İç kullanım için.</td>
    </tr>       
</table>

Desteklenen hello birini kullanarak bunu yapabilirsiniz [Azure Cosmos DB SDK'ları](documentdb-sdk-dotnet.md). Örneğin, hello aşağıdaki kod parçacığında nasıl tooretrieve bölüm anahtarı .NET aralıkları hello kullanarak gösterir [ReadPartitionKeyRangeFeedAsync](/dotnet/api/microsoft.azure.documents.client.documentclient.readpartitionkeyrangefeedasync?view=azure-dotnet) yöntemi.

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

Azure Cosmos DB ayarı hello tarafından isteğe bağlı bölüm anahtarı aralığının başına belge alınmasını destekler `x-ms-documentdb-partitionkeyrangeid` üstbilgi. 

### <a name="performing-an-incremental-readdocumentfeed"></a>Bir artımlı ReadDocumentFeed gerçekleştirme
ReadDocumentFeed senaryoları/görevler değişiklikleri Azure Cosmos DB koleksiyonlarda artımlı işleme için aşağıdaki hello destekler:

* Tüm okuma hello başından toodocuments diğer bir deyişle, koleksiyon oluşturulması değiştirir.
* Tüm okuma toofuture güncelleştirmeleri toodocuments kullanıcı tarafından belirtilen bir tarihten geçerli saati veya herhangi bir değişiklik değiştirir.
* Tüm değişiklikleri toodocuments hello koleksiyonu (ETag) mantıksal bir sürümünden okuyun. Denetim noktası artımlı okuma akışı isteklerinden ETag döndürülen hello tüketicileriniz dayalı olabilir.

Merhaba değişiklikler ekler ve güncelleştirmeleri toodocuments içerir. toocapture siler, belgeler içinde "geçici silme" özelliğini kullanın veya hello kullan [yerleşik TTL özelliği](time-to-live.md) toosignal hello bekleyen bir değişikliği akış değiştirin.

Tablo listeleri hello Hello [isteği](/rest/api/documentdb/common-documentdb-rest-request-headers.md) ve [yanıt üstbilgilerini](/rest/api/documentdb/common-documentdb-rest-response-headers.md) ReadDocumentFeed işlemleri için.

**İstek üstbilgileri için artımlı ReadDocumentFeed**:

<table>
    <tr>
        <th>Üstbilgi adı</th>
        <th>Açıklama</th>
    </tr>
    <tr>
        <td>BİR IM</td>
        <td>Çok "Artımlı akış" olarak ayarlanması gerekir ya da aksi takdirde atlanmış</td>
    </tr>
    <tr>
        <td>If-None-Match</td>
        <td>
            <p>Başlık: (oluşturma koleksiyonu) itibaren hello tüm değişiklikleri döndürür</p>
            <p>"*": hello koleksiyonundaki tüm yeni değişiklikleri toodata döndürür</p>         
            <p>&lt;ETag&gt;: varsa tooa koleksiyonu ETag, mantıksal zaman damgası itibaren yapılan tüm değişiklikler döndürür</p>
        </td>
    </tr>
    <tr>    
        <td>If-Modified-Since</td> 
        <td>RFC 1123 saat biçimi; If-None-Match belirtilmişse göz ardı</td> 
    </tr> 
    <tr>
        <td>x-ms-documentdb-partitionkeyrangeid</td>
        <td>verilerin okunması için hello bölüm anahtarı aralığının kimliği.</td>
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
            <p>Merhaba yanıtında son belgenin Hello mantıksal sıra numarası (LSN).</p>
            <p>Artımlı ReadDocumentFeed If-None-Match bu değeri yeniden göndermeden ettirilebilir.</p>
        </td>
    </tr>
</table>

Örnek istek tooreturn İşte hello mantıksal sürüm/ETag koleksiyonda tüm artımlı değişiklikler `28535` ve bölüm anahtarı aralığının = `16`:

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

Değişiklikleri süre içinde hello bölüm anahtarı aralığının her bölüm anahtarı değerine göre sıralanır. Bölüm anahtarı değerleri arasında hiçbir garanti edilen sipariş yoktur. Tek bir sayfayla sığmayacak daha fazla sonuç yoksa hello hello isteğini yeniden göndermeden hello sonraki sonuç sayfasını okuyabilirsiniz `If-None-Match` değer eşit toohello üstbilgiyle `etag` hello önceki yanıt gelen. Birden çok belge eklendi veya işlemsel olarak bir saklı yordam veya tetikleyici içinde güncelleştirildi, bunlar tüm hello içinde aynı döndürülecek yanıt sayfası.

> [!NOTE]
> Değişiklik akış ile daha fazla öğe bir sayfa içinde belirtilenden döndürülen alabilirsiniz `x-ms-max-item-count` hello durumda eklenir veya güncelleştirilir saklı yordamların içinde birden fazla belge veya tetikler. 

Merhaba .NET SDK'sı (1.17.0) kullanırken, hello alan kümesi `StartTime` içinde `ChangeFeedOptions` beri değiştirilen toodirectly dönüş belgeleri `StartTime` çağrılırken `CreateDocumentChangeFeedQuery`. Belirterek `If-Modified-Since` hello REST API kullanarak, isteğiniz hello belgeleri değil kendilerini ancak bunun yerine hello devamlılık belirteci döndürür veya `etag` hello yanıt üstbilgisi içinde. Değiştirilen hello belirtilen süre, hello devamlılık belirteci tooreturn hello belgelerin `etag` sonra hello sonraki istekle kullanılmalıdır `If-None-Match` tooreturn hello gerçek belgeleri. 

Merhaba .NET SDK'sı sağlar hello [CreateDocumentChangeFeedQuery](/dotnet/api/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery?view=azure-dotnet) ve [ChangeFeedOptions](/dotnet/api/microsoft.azure.documents.client.changefeedoptions?view=azure-dotnet) yardımcı sınıfları tooaccess değişikliklerinin tooa koleksiyonu. Merhaba aşağıdaki kod parçacığında tooretrieve tüm tek bir istemciden gelen hello .NET SDK kullanarak hello başından nasıl değiştiğini gösterir.

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
Ve hello aşağıdaki kod parçacığında nasıl tooprocess gerçek zamanlı olarak değiştiğini gösterir hello değişiklik kullanarak Azure Cosmos DB ile destek akışı ve işlev önceki hello. Hello ilk çağrıda hello koleksiyonundaki tüm hello belgeleri döndürür ve hello ikinci yalnızca hello hello son denetim noktasının bu yana oluşturulan oluşturulan iki belgeler döndürür.

```csharp
// Returns all documents in hello collection.
Dictionary<string, string> checkpoints = await GetChanges(client, collection, new Dictionary<string, string>());

await client.CreateDocumentAsync(collection, new DeviceReading { DeviceId = "xsensr-201", MetricType = "Temperature", Unit = "Celsius", MetricValue = 1000 });
await client.CreateDocumentAsync(collection, new DeviceReading { DeviceId = "xsensr-212", MetricType = "Pressure", Unit = "psi", MetricValue = 1000 });

// Returns only hello two documents created above.
checkpoints = await GetChanges(client, collection, checkpoints);
```

İstemci tarafı mantığı tooselectively işlem olayları kullanarak hello değişiklik akış de filtre uygulayabilirsiniz. Örneğin, istemci tarafı LINQ tooprocess aygıt algılayıcılar olayları sıcaklık değiştirmek yalnızca kullanan bir parçacığı aşağıda verilmiştir.

```csharp
FeedResponse<DeviceReading> readChangesResponse = query.ExecuteNextAsync<DeviceReading>().Result;

foreach (DeviceReading changedDocument in 
    readChangesResponse.AsEnumerable().Where(d => d.MetricType == "Temperature" && d.MetricValue > 1000L))
{
    // trigger an action, like call an API
}
```

## <a id="change-feed-processor"></a>Değişiklik işlemci akışı kitaplığı
Başka bir seçenektir toouse hello [Azure Cosmos DB değiştirmek akış işlemci Kitaplığı](https://docs.microsoft.com/azure/cosmos-db/documentdb-sdk-dotnet-changefeed), hangi yardımcı olabilir, olay arasında birden çok tüketiciye akışı bir değişiklik gelen işleme kolayca dağıtabilirsiniz. Merhaba kitaplığı hello .NET platformu üzerinde okuyucular akış değişiklik oluşturmak için mükemmeldir. Hello dahil hello yöntemleri üzerinden hello değişiklik akış işlemci kitaplığı kullanılarak Basitleştirilmiş bazı iş akışları diğer Cosmos DB SDK aşağıdakileri içerir: 

* Birden çok bölüm arasında veri depolandığında değişiklik çekilmesini güncelleştirmelerini akışı
* Taşıma veya bir koleksiyon tooanother veri çoğaltma
* Paralel yürütme güncelleştirmeleri toodata tarafından tetiklenen eylemler ve akış Değiştir 

Merhaba Cosmos SDK'ları Hello API'lerini kullanarak kesin erişim toochange güncelleştirmeleri her bölüm akış sağlarken hello değişiklik akış işlemci kitaplığını kullanarak bölümler ve paralel çalışan birden çok iş parçacığı üzerinde okuma değişiklikleri basitleştirir. El ile değişiklikleri her kapsayıcıdan okuma ve kaydetme her bölüm için devamlılık belirteci yerine hello değişiklik akış işlemci okuma değişiklikleri bir kiralama mekanizması kullanarak bölümleri arasında otomatik olarak yönetir.

Merhaba kitaplığı NuGet paketi olarak kullanılabilir: [Microsoft.Azure.Documents.ChangeFeedProcessor](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.ChangeFeedProcessor/) ve bir Github olarak kaynak koddan [örnek](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/ChangeFeedProcessor). 

### <a name="understanding-change-feed-processor-library"></a>Anlama değişiklik akış işlemci kitaplığı 

Merhaba değişiklik akış işlemci gerçekleştirilmesinin dört ana bileşen mevcuttur: hello izlenen koleksiyonu, hello kira koleksiyonu, hello işleyicisi konağı ve hello tüketicileri. 

**İzlenen koleksiyonu:** izlenen hello koleksiyonudur hello veri hangi hello değişiklik akış oluşturulur. Herhangi bir eklemeleri ve değişiklikleri izlenen toohello koleksiyonu hello koleksiyonunun değişiklik akışta hello yansıtılır. 

**Kira koleksiyonu:** hello değişiklik arasında birden çok Worker akış işleme kira koleksiyonu koordinatları hello. Ayrı bir kira bölüm başına ile kullanılan toostore hello kiraları koleksiyonudur. Bu kira koleksiyonu hello ile farklı bir hesap üzerinde değişiklik akış işlemci çalıştıran bölge daha yakından toowhere hello yazmak avantajlı toostore olur. Bir kira nesnesi öznitelikleri aşağıdaki hello içerir: 
* Sahibi: hello kira sahibi hello konak belirtir
* Devamlılık: hello konumu (devamlılık belirteci) için belirli bir bölüm akış hello değişikliği belirtir.
* Zaman damgası: kira güncelleştirildi; son zamanı Merhaba kira süresi dolmuş olarak kabul edilir olup olmadığını Hello zaman damgası kullanılan toocheck olabilir 

**İşlemci ana bilgisayarı:** kaç bölümleri tooprocess etkin kiralamaları kaç ana örneklerini olmadığına göre her bir ana bilgisayar belirler. 
1.  Bir ana bilgisayar başlatıldığında tüm ana bilgisayarlar arasında kiraları toobalance hello iş yükünü devralır. Kira etkin şekilde bir ana bilgisayar kiralama, düzenli aralıklarla yeniler. 
2.  Bir ana bilgisayar kontrol noktaları hello son devamlılık belirteci tooits kira her okuyun. tooensure eşzamanlılık güvenliği, bir konak hello ETag her bir kira güncelleştirme denetler. Diğer denetim noktası stratejileri de desteklenir.  
3.  Kapatma, bağlı bir ana bilgisayar tüm kira serbest ancak daha sonra okuma hello saklı kontrol noktasından devam edebilmek için tutar devamlılık bilgi hello. 

Şu anda ana bilgisayar hello sayısı hello bölümleri (kiraları) sayısından büyük olamaz.

**Tüketiciler:** tüketici veya çalışanları olan her konak tarafından başlatılan işlem akışı hello değişikliği gerçekleştiren iş parçacığı. Her işlemci ana bilgisayarın birden çok tüketiciye sahip olabilir. Her bir tüketici okur hello değişiklik akış hello tooand atandı bölüm değişiklikleri ana bilgisayar bildirir ve kira süresi doldu.

toofurther değişiklik akış işlemci dört bu unsuru birlikte nasıl çalıştığını anlamak, diyagram aşağıdaki hello içinde bir örneğe bakalım. Merhaba koleksiyonu depoları belgeleri izlenen ve hello "Şehir" Merhaba bölüm anahtarı olarak kullanır. Merhaba mavi bölüm "A-E" hello "Şehir" alanını belgeler vb. içerdiğini görürsünüz. Her iki tüketicileri hello dört bölümü paralel okuma ile iki ana vardır. Merhaba oklar, akış hello belirli bir noktada okuma hello tüketicileri değiştirmek gösterir. Merhaba mavi zaten hello değişiklik akış değişiklikleri okuma hello temsil ederken hello ilk bölümünde hello Koyu mavi okunmamış değişiklikler temsil eder. Merhaba konakları hello kira koleksiyonu toostore hello her tüketici konumunu okuma geçerli "devamlılık" değeri tookeep izini kullanın. 

![Hello Azure Cosmos DB değişikliği kullanarak akış işlemcisi konağı](./media/change-feed/changefeedprocessornew.png)

### <a name="using-change-feed-processor-library"></a>Değişiklik kullanarak akış işlemci kitaplığı 
bölümden hello nasıl toouse hello kaynak koleksiyonu tooa hedef koleksiyondan değişiklikleri çoğaltmaya hello bağlamı değişiklik akış işlemci kitaplıkta açıklanmaktadır. Burada, hello kaynak koleksiyonu izlenen hello değişiklik akış işlemcide koleksiyonudur. 

**Yükleme ve hello değişiklik akış işlemci NuGet paketini ekleyin** 

Değişiklik akış işlemci NuGet paketini yüklemeden önce ilk yükleyin: 
* Microsoft.Azure.DocumentDB, sürüm 1.13.1 veya üstü 
* Newtonsoft.Json, sürüm 9.0.1 veya yükleme yukarıda `Microsoft.Azure.DocumentDB.ChangeFeedProcessor` ve bir başvuru olarak dahil edin.

**İzlenen, kiralama ve hedef koleksiyon oluşturma** 

Sipariş toouse hello değişiklik akış işlemci kitaplığı, hello kira koleksiyonu hello işlemci boşaltıyor çalıştırmadan önce oluşturulan toobe gerekir. Yeniden değişikliği akış işlemci çalıştıran farklı bir hesap üzerinde yazma bölge daha yakından toowhere hello ile bir kira koleksiyon depolamanızı öneririz. Bu veri taşıma örnekte hello değişiklik akış işleyicisi konağı çalıştırmadan önce toocreate hello hedef koleksiyonu gerekir. İzlenen bir yardımcı yöntem toocreate Merhaba diyoruz Hello örnek kodda kiralık ve zaten mevcut değilse hedef koleksiyonları. 

> [!WARNING]
> Üretilen iş ile Azure Cosmos DB hello uygulama toocommunicate için ayırma gibi bir koleksiyon oluşturma, fiyatlandırmaya vardır. Daha fazla ayrıntı için lütfen başlangıç adresini ziyaret edin [fiyatlandırma sayfası](https://azure.microsoft.com/pricing/details/cosmos-db/)
> 
> 

*İşlemci konak oluşturma*

Merhaba `ChangeFeedProcessorHost` sınıfı, olay işlemcisi uygulamaları için aynı zamanda denetim noktası oluşturma ve bölüm kiralama Yönetimi sağlayan bir iş parçacığı, çok işlemli, güvenli çalışma zamanı ortamı sağlar. toouse hello `ChangeFeedProcessorHost` sınıfı, uygulayabilirsiniz `IChangeFeedObserver`. Bu arabirim üç yöntem içerir:

* `OpenAsync`: Bu işlev, değişiklik akış gözlemci açıldığında çağrılır. Tüketici/gözlemci açıldığında değiştirilmiş tooperform belirli bir eylemi olabilir.  
* `CloseAsync`: Değişiklik akış gözlemci sonlandırıldığında bu işlev çağrılır. Tüketici/gözlemci kapatıldığında değiştirilmiş tooperform belirli bir eylemi olabilir.  
* `ProcessChangesAsync`: Belge yeni değişiklikleri değişiklik Besleme üzerindeki kullanılabilir olduğunda bu işlev çağrılır. Değiştirilen tooperform her akış değişiklik güncelleştirme sırasında belirli bir eylemi olabilir.  

Bizim örneğimizde, biz hello arabirimini uygulayan `IChangeFeedObserver` hello aracılığıyla `DocumentFeedObserver` sınıfı. Burada, hello `ProcessChangesAsync` işlev değişikliği belgeden akış hello hedef koleksiyona upserts (güncelleştirmeler). Bu örnek, bir koleksiyon tooanother sipariş toochange hello bölüm anahtarı, bir veri kümesinin veri taşıma için kullanışlıdır. 

*Çalışan hello işlemcisi konağı*

Olay işleme başlamadan önce her ikisi de akış seçeneklerini değiştirin ve akış konak seçeneklerini değiştirme özelleştirilebilir. 
```csharp
    // Customizable change feed option and host options 
    ChangeFeedOptions feedOptions = new ChangeFeedOptions();

    // ie customize StartFromBeginning so change feed reads from beginning
    // can customize MaxItemCount, PartitonKeyRangeId, RequestContinuation, SessionToken and StartFromBeginning
    feedOptions.StartFromBeginning = true;

    ChangeFeedHostOptions feedHostOptions = new ChangeFeedHostOptions();

    // ie. customizing lease renewal interval too15 seconds
    // can customize LeaseRenewInterval, LeaseAcquireInterval, LeaseExpirationInterval, FeedPollDelay 
    feedHostOptions.LeaseRenewInterval = TimeSpan.FromSeconds(15);

```
özelleştirilebilir hello belirli alanlar tabloları aşağıdaki hello özetlenir. 

**Akış seçeneklerini değiştirme**:
<table>
    <tr>
        <th>Özellik adı</th>
        <th>Açıklama</th>
    </tr>
    <tr>
        <td>MaxItemCount</td>
        <td>Alır veya hello Azure Cosmos DB veritabanı hizmeti hello numaralandırma işlemi döndürdü öğeleri toobe hello sayısını ayarlar.</td>
    </tr>
    <tr>
        <td>PartitionKeyRangeId</td>
        <td>Alır veya hello Azure Cosmos DB veritabanı hizmetinin hello bölüm anahtarı aralığının kimliği hello geçerli istek için ayarlar.</td>
    </tr>
    <tr>
        <td>RequestContinuation</td>
        <td>Alır veya hello Azure Cosmos DB veritabanı hizmetinin hello isteği devamlılık belirteci ayarlar.</td>
    </tr>
        <tr>
        <td>SessionToken</td>
        <td>Alır veya oturum tutarlılığı hello Azure Cosmos DB veritabanı hizmeti ile Merhaba Oturum belirteci kullanmak için ayarlar.</td>
    </tr>
        <tr>
        <td>StartFromBeginning</td>
        <td>Alır veya değişiklik hello Azure Cosmos DB veritabanı hizmetinin akış (true) itibaren hello ya da geçerli (false) başlamalıdır olup olmadığını ayarlar. Varsayılan olarak, geçerli (false) başlar.</td>
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
        <td>şu anda hello ChangeFeedEventHost örneği tarafından tutulan bölümler için tüm kiraları Hello aralığı.</td>
    </tr>
    <tr>
        <td>LeaseAcquireInterval</td>
        <td>TimeSpan</td>
        <td>bölümler dağılımla bilinen konak örnekler arasında olup olmadığını aralığı tookick görev toocompute kapalı hello.</td>
    </tr>
    <tr>
        <td>LeaseExpirationInterval</td>
        <td>TimeSpan</td>
        <td>Merhaba aralığı için hangi hello kira bir bölüm temsil eden bir kira alınır. Merhaba kira bu aralıkta yenilenmezse, süresi doldu ve tooanother ChangeFeedEventHost örneği hello bölüm sahipliğini taşır.</td>
    </tr>
    <tr>
        <td>FeedPollDelay</td>
        <td>TimeSpan</td>
        <td>Tüm geçerli değişiklikleri boşaltmış sonra bir bölüm hello yeni değişiklikleri için yoklama arasındaki hello gecikme akış.</td>
    </tr>
    <tr>
        <td>CheckpointFrequency</td>
        <td>CheckpointFrequency</td>
        <td>Merhaba sıklığı toocheckpoint kiralar.</td>
    </tr>
    <tr>
        <td>MinPartitionCount</td>
        <td>Int</td>
        <td>Merhaba ana Hello en düşük bölüm sayısı.</td>
    </tr>
    <tr>
        <td>MaxPartitionCount</td>
        <td>Int</td>
        <td>bölümler hello konak Hello sayısının hizmet verebilir.</td>
    </tr>
    <tr>
        <td>DiscardExistingLeases</td>
        <td>bool</td>
        <td>Merhaba tüm mevcut kiraları hello ana bilgisayarın Başlat olup olmadığını silineceğini ve hello konak baştan başlamanız gerekir.</td>
    </tr>
</table>


toostart olay işleme, örneği `ChangeFeedProcessorHost`, Azure Cosmos DB koleksiyonunuz için hello uygun parametreleri sağlayarak. Ardından, çağıran `RegisterObserverAsync` tooregister, `IChangeFeedObserver` hello çalışma zamanı (Bu örnekte DocumentFeedObserver) uygulaması. Bu noktada, hello konak tooacquire her bölüm anahtarı aralığının "Hızlı" algoritma kullanarak hello Azure Cosmos DB koleksiyonunda üzerinde bir kira çalışır. Bu kiralar belirli bir zaman çerçevesi için en son ve sonrasında yenilenmelidir. Yeni düğüm olarak çalışan örnekleri, bu durumda, çevrimiçi olması, kiralama ayırmaları yapar ve her konak tooacquire daha fazla kira girişimleri olarak zaman içinde hello yük düğümler arasında kayar.. 

Merhaba örnek kodda bir fabrika sınıfı (DocumentFeedObserverFactory.cs) toocreate bir gözlemci ve hello kullanırız `RegistObserverFactoryAsync` tooregister hello gözlemci. 

```csharp
using (DocumentClient destClient = new DocumentClient(destCollInfo.Uri, destCollInfo.MasterKey))
    {
        DocumentFeedObserverFactory docObserverFactory = new DocumentFeedObserverFactory(destClient, destCollInfo);
        ChangeFeedEventHost host = new ChangeFeedEventHost(hostName, documentCollectionLocation, leaseCollectionLocation, feedOptions, feedHostOptions);

        await host.RegisterObserverFactoryAsync(docObserverFactory);

        Console.WriteLine("Running... Press enter toostop.");
        Console.ReadLine();

        await host.UnregisterObserversAsync();
    }
```
Zaman içerisinde bir denge sağlanır. Bu dinamik özellik CPU tabanlı otomatik ölçeklendirme uygulanan toobe tooconsumers ölçek büyütme ve ölçek azaltma için etkinleştirir. Değişiklikler Azure Cosmos DB'de tüketicilerin işleyebileceğinden daha hızlı bir oranda kullanılabilir hello tüketiciler üzerindeki CPU artışı çalışan örnek sayısı üzerinde otomatik ölçeklendirmeye kullanılan toocause olabilir.

## <a name="next-steps"></a>Sonraki adımlar
* Merhaba deneyin [Github'da Azure Cosmos DB Değiştir Akış kod örnekleri](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples/ChangeFeed)
* Kodlama Hello ile çalışmaya başlama [Azure Cosmos DB SDK'ları](documentdb-sdk-dotnet.md) veya hello [REST API](/rest/api/documentdb/).
