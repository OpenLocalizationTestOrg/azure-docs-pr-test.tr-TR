---
title: "aaaPerformance ipuçları - Azure Cosmos DB NoSQL | Microsoft Docs"
description: "İstemci yapılandırma seçenekleri tooimprove Azure Cosmos DB veritabanı performansını öğrenin"
keywords: "nasıl tooimprove veritabanı performansı"
services: cosmos-db
author: mimig1
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: 94ff155e-f9bc-488f-8c7a-5e7037091bb9
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/23/2017
ms.author: mimig
ms.openlocfilehash: 4f3e82ae5048e3dbc20b0fd891a2d3aa22adf3fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="performance-tips-for-azure-cosmos-db"></a>Azure Cosmos DB performans ipuçları
Azure Cosmos DB garantili gecikme süresi ve verimlilik ile sorunsuz bir şekilde ölçeklendirilebilen bir hızlı ve esnek dağıtılmış veritabanıdır. Değil toomake büyük mimari değişikliklerinin veya karmaşık kodlar tooscale veritabanınızla Cosmos DB yazma. Yukarı ve aşağı doğru ölçeklendirme tek bir API çağrısı yapma olarak kadar kolay veya [SDK yöntem çağrısı](set-throughput.md#set-throughput-sdk). Ancak, Cosmos DB aracılığıyla erişilir ağ çağrıları tooachieve en yüksek performans yapabileceğiniz istemci-tarafı iyileştirmeler değildir.

Soran, "nasıl ı my veritabanı performansını geliştirebilir şekilde?" Seçenekler aşağıdaki hello göz önünde bulundurun:

## <a name="networking"></a>Ağ
<a id="direct-connection"></a>

1. **Bağlantı İlkesi: doğrudan bağlantı modu kullan**

    Bir istemci tooCosmos DB nasıl bağlandığını gözlemlenen istemci-tarafı gecikme açısından özellikle performansı önemli etkilere sahiptir. İki anahtar yapılandırma ayarlarını istemci bağlantı İlkesi – hello bağlantısı yapılandırmak için kullanılabilir *modu* ve hello [bağlantı *Protokolü*](#connection-protocol).  Merhaba iki kullanılabilir modları şunlardır:

   1. Ağ geçidi modunda (varsayılan)
   2. Doğrudan modu

      Ağ geçidi modu tüm SDK platformlarda desteklenir ve yapılandırılmış hello varsayılandır.  Uygulamanız bir şirket ağı içinde katı güvenlik duvarı kısıtlamalarıyla çalışıyorsa hello standart HTTPS bağlantı noktası ve tek bir uç nokta kullandığından ağ geçidi modu hello en iyi seçimdir. Performans kolaylığını Merhaba, ancak veri okuma veya tooCosmos DB yazılan her zaman ağ geçidi modu ek ağ atlama içermesidir. Bu nedenle, doğrudan modu toofewer ağ atlamalarını nedeniyle daha iyi performans sunar.
<a id="use-tcp"></a>
2. **Bağlantı İlkesi: hello TCP protokolünü kullanır**

    Doğrudan modu kullanırken, kullanılabilir iki protokolü seçenek vardır:

   * TCP
   * HTTPS

     Cosmos DB Basit bir sunar ve HTTPS üzerinden RESTful programlama modeli açın. Ayrıca, aynı zamanda RESTful kendi iletişim modelini ve hello .NET İstemci SDK kullanılabilir verimli bir TCP protokolü sunar. Doğrudan TCP ve HTTPS SSL ilk kimlik doğrulaması ve şifreleme trafiği için kullanın. En iyi performans için mümkün olduğunda hello TCP protokolü kullanın.

     TCP ağ geçidi modunda kullanılırken, TCP bağlantı noktası 443 hello Cosmos DB bağlantı noktası ve 10255 değerini bulur hello MongoDB API bağlantı noktası. TCP toplama toohello ağ geçidi bağlantı noktaları, doğrudan modunda kullanırken tooensure hello bağlantı noktası gerekir Cosmos DB dinamik TCP bağlantı noktaları kullandığından 10000 20000 arasındaki aralığı açın. Bu bağlantı noktalarının açık değildir ve toouse TCP çalışırsanız, 503 Hizmet kullanılamıyor hatası alırsınız.

     Bağlantı modunu Hello hello ConnectionPolicy parametresiyle hello DocumentClient örneğinin hello oluşturma sırasında yapılandırılır. Doğrudan modunda kullanılırsa, hello Protokolü hello ConnectionPolicy parametresi içinde de ayarlayabilirsiniz.

    ```C#
    var serviceEndpoint = new Uri("https://contoso.documents.net");
    var authKey = new "your authKey from hello Azure portal";
    DocumentClient client = new DocumentClient(serviceEndpoint, authKey,
    new ConnectionPolicy
    {
        ConnectionMode = ConnectionMode.Direct,
        ConnectionProtocol = Protocol.Tcp
    });
    ```

    Ağ geçidi modunda kullanılırsa, TCP yalnızca doğrudan modunda desteklendiğinden, ardından HTTPS protokolünü her zaman olduğu hello toocommunicate hello ağ geçidi ile ve hello protokol değeri ConnectionPolicy göz ardı hello kullanılır.

    ![Hello Azure Cosmos DB bağlantı İlkesi çizimi](./media/performance-tips/connection-policy.png)

3. **İlk isteği OpenAsync tooavoid başlatma gecikmesi çağırın**

    Toofetch hello adresi yönlendirme tablosu olduğundan varsayılan olarak, daha yüksek gecikme hello ilk istek sahiptir. tooavoid hello bu başlangıç gecikmesine ilk istek, bir kez başlatma sırasında şu şekilde OpenAsync() çağırmalıdır.

        await client.OpenAsync();
   <a id="same-region"></a>
4. **Performans için aynı Azure bölgesinde istemciler birlikte bulundurma**

    Ne zaman mümkün Cosmos DB arayan herhangi bir uygulama ile aynı bölgeye hello yerine Cosmos DB veritabanı hello. Yaklaşık bir karşılaştırma için aynı bölgede tamamlamak 1-2 ms ancak hello Batı ve us Merhaba, Doğu Yakası arasındaki hello gecikme süresi içinde hello içinde tooCosmos DB çağırır > 50 ms. Bu gecikme, büyük olasılıkla gelen isteği toorequest hello istemci toohello Azure veri merkezi bir sınır geçerken hello istek tarafından alınan hello rota bağlı olarak değişebilir. Merhaba olası en düşük gecikme süresi hello arama sağlayarak gerçekleştirilir uygulama hello içinde bulunduğu hello olduğu Azure bölgesinin sağlanan Cosmos DB uç noktası. Kullanılabilir bölgelerin bir listesi için bkz: [Azure bölgeleri](https://azure.microsoft.com/regions/#services).

    ![Hello Azure Cosmos DB bağlantı İlkesi çizimi](./media/performance-tips/same-region.png)
   <a id="increase-threads"></a>
5. **İş parçacıkları/görevleri sayısını artırın**

    Merhaba ağ üzerinden çağrıları tooAzure Cosmos DB yapılma olduğundan, böylece hello istemci uygulamanın bekleyen istekler arasında çok az zaman geçirdiği toovary Merhaba, istekleri paralellik derecesini gerekebilir. Örneğin, kullanıyorsanız. NET'in [görev paralel Kitaplığı](https://msdn.microsoft.com//library/dd460717.aspx), okuma veya yazma tooCosmos DB görevlerin 100s hello sırada oluşturun.

## <a name="sdk-usage"></a>SDK kullanımı
1. **Yükleme son SDK hello**

    Merhaba Cosmos DB SDK'ları sürekli geliştirilmiş tooprovide hello en iyi performansı bırakılıyor. Merhaba bkz [Cosmos DB SDK](documentdb-sdk-dotnet.md) sayfaları toodetermine en son SDK hello ve geliştirmeleri gözden geçirin.
2. **Bir singleton Cosmos DB istemci uygulamanız hello ömrü boyunca kullanın**

    Her DocumentClient örnek iş parçacığı açısından güvenli ve verimli bağlantı yönetimi ve doğrudan modunda çalışırken adresi önbelleğe alma gerçekleştirir unutmayın. tooallow verimli bağlantı yönetimi ve daha iyi performans DocumentClient ile toouse DocumentClient AppDomain başına tek bir örneğini Merhaba uygulaması hello ömrü boyunca önerilir.

   <a id="max-connection"></a>
3. **Ağ geçidi modu kullanırken System.Net MaxConnections ana bilgisayar başına artırın**

    Cosmos DB istekler ağ geçidi modu kullanırken HTTPS/REST yapılan ve ana bilgisayar adı veya IP adresi başına tabi toohello varsayılan bağlantı sınırı. Böylece Hello istemci kitaplığı birden çok eşzamanlı bağlantı tooCosmos DB kullanabilir tooset hello MaxConnections tooa daha yüksek değere (100-1000) gerekebilir. .NET SDK'sı 1.8.0 hello ve yukarıdaki için varsayılan değer hello [ServicePointManager.DefaultConnectionLimit](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit.aspx) olan 50 ve toochange Merhaba değeri, hello ayarlayabilirsiniz [Documents.Client.ConnectionPolicy.MaxConnectionLimit ](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.connectionpolicy.maxconnectionlimit.aspx) tooa daha yüksek değer.   
4. **Paralel sorgular bölümlenmiş koleksiyonlar için ayarlama**

     DocumentDB .NET SDK sürüm 1.9.0 ve tooquery paralel bölümlendirilmiş bir koleksiyon etkinleştirme desteği paralel sorgular yukarıda (bkz [hello SDK'ları ile çalışma](documentdb-partition-data.md#working-with-the-azure-cosmos-db-sdks) ve ilgili hello [kod örnekleri](https://github.com/Azure/azure-documentdb-dotnet/blob/master/samples/code-samples/Queries/Program.cs) için Daha fazla bilgi). Paralel sorgular tasarlanmış tooimprove sorgu gecikme süresi ve verimlilik seri bunların karşılık gelen ' dir. Paralel sorgular sağlayan iki parametre kullanıcıların gereksinimlerine, (a) MaxDegreeOfParallelism toocustom sığacak şekilde ayarlayabilirsiniz: toocontrol hello en fazla bölüm sayısı ardından sorgulanan paralel ve (b) MaxBufferedItemCount: toocontrol hello sayısı önceden getirilen sonuç.

    (a) ***ayarlama MaxDegreeOfParallelism\: *** paralel sorgu works birden çok bölümü paralel sorgulayarak. Ancak, tek bir bölümlenmiş toplama verileri seri olarak saygı toohello sorguyla getirilir. Bu nedenle, ayarı hello MaxDegreeOfParallelism toohello bölüm sayısı çoğu kullanıcı sorgu Merhaba, diğer tüm sistem koşulları kalır sağlanan aynı hello elde hello maksimum fırsat sahiptir. Bölüm sayısı hello bilmiyorsanız, hello MaxDegreeOfParallelism tooa yüksek sayı ayarlayabilirsiniz ve MaxDegreeOfParallelism hello gibi hello sistem hello minimum (bölüm, kullanıcı tarafından sağlanan girdi sayısı) seçer.

    Merhaba veri saygı toohello sorgusuyla tüm bölümleri arasında eşit olarak dağıtılır, bu sorguları üretim hello en iyi avantajları paralel önemli toonote olur. Merhaba koleksiyon bölümlendiğinde ise (en kötü durumda bir bölüm) birkaç bölümlerdeki tamamı veya bir sorgu tarafından döndürülen hello veri çoğunluğu bir yoğunlaşmıştır sonra hello hello sorgu performansını tarafından bu bölümler nedeniyle düşük performansa şekilde bölümlenmiş.

    (b) ***ayarlama MaxBufferedItemCount\: *** paralel sorgudur hello istemci tarafından hello sonuçları geçerli toplu işlem gerçekleştirilirken tasarlanmış toopre fetch sonuçları. bir sorgunun genel gecikme geliştirme yardımcı önceden getirme hello. MaxBufferedItemCount hello parametresi toolimit hello önceden getirilen sonuçları sayısıdır. MaxBufferedItemCount ayarı toohello döndürülen sonuçları (veya daha yüksek bir sayı) sayısı önceden getirme gelen hello sorgu tooreceive maksimum avantajı sağlar bekleniyordu.

    Önceden getirilirken works MaxDegreeOfParallelism Merhaba şekilde belirtilmediğine aynı hello ve tüm bölümleri hello verileri için tek bir arabelleğe olduğunu unutmayın.  
5. **Sunucu tarafı GC üzerinde Aç**

    Çöp toplama Hello sıklığını azaltmayı bazı durumlarda yardımcı olabilir. .NET ile ayarlamak [gcServer](https://msdn.microsoft.com/library/ms229357.aspx) tootrue.
6. **Geri Çekilme RetryAfter aralıklarla uygulama**

    Performans testi sırasında istekleri küçük oranını kısıtlanan kadar yük artırmanız gerekir. Kısıtlanan, Merhaba istemci uygulaması kısıtlama üzerinde geri Çekilme hello sunucu belirtilen yeniden deneme aralığını gerekir. Merhaba geri Çekilme uyarak denemeler arasındaki bekleme süresi en az miktarda harcamanızı sağlar. Yeniden deneme ilkesi desteği eklenmiştir sürümünde 1.8.0 ve yukarıdaki hello DocumentDB, [.NET](documentdb-sdk-dotnet.md) ve [Java](documentdb-sdk-java.md), sürüm 1.9.0 ve yukarıdaki Merhaba, [Node.js](documentdb-sdk-node.md) ve [ Python](documentdb-sdk-python.md), ve tüm desteklenen sürümlerinde hello [.NET Core](documentdb-sdk-dotnet-core.md) SDK'ları. Daha fazla bilgi için bkz: [Exceeding ayrılmış işleme sınırları](request-units.md#RequestRateTooLarge) ve [RetryAfter](https://msdn.microsoft.com/library/microsoft.azure.documents.documentclientexception.retryafter.aspx).
7. **İstemci-iş yükünü ölçeklendirme**

    Yüksek işleme düzeyleri sınıyorsanız (> 50.000 RU/s), Merhaba istemci uygulaması toohello capping CPU veya ağ kullanımını makine çıkışı son hello performans sorunu hale. Bu noktaya ulaştıysanız, birden çok sunucu arasında istemci uygulamalarının ölçeklendirme tarafından toopush hello Cosmos DB hesap ek devam edebilirsiniz.
8. **Daha düşük okuma gecikmesi için önbellek belge URI'ler**

    Önbellek belge URI'ler hello okuma en iyi performans için mümkün.
   <a id="tune-page-size"></a>
9. **Merhaba sayfa boyutu sorguları/okuma akışları daha iyi performans için ayarlama**

    Bir toplu gerçekleştirme belgeleri okuma akışı işlevleri (örneğin, ReadDocumentFeedAsync) kullanarak veya bir DocumentDB SQL sorgu gönderirken okurken hello sonuç kümesi çok büyük ise hello sonuçları bölümlenmiş bir şekilde döndürülür. Varsayılan olarak, ilk isabet sınırlarından hangisi olduğunu, sonuçları 100 öğeleri ya da 1 MB yığınlar halinde döndürdü.

    tooreduce hello sayısı, tüm geçerli sonuçları gidiş dönüş gerekli tooretrieve ağ, x-ms-max-öğesi-count istek üstbilgisi tooup too1000 kullanarak hello sayfa boyutunu artırabilirsiniz. Yalnızca birkaç sonuçları toodisplay gereken yeri durumlarda Örneğin, kullanıcı arabirimi veya uygulama API yalnızca 10 döndürürse birer sonuçları, okuma ve sorgular için tüketilen hello sayfa boyutu too10 tooreduce hello üretilen iş da azaltabilirsiniz.

    Merhaba sayfa boyutu da yerleştirebilir hello kullanılabilir Cosmos DB SDK'ları kullanarak.  Örneğin:

        IQueryable<dynamic> authorResults = client.CreateDocumentQuery(documentCollection.SelfLink, "SELECT p.Author FROM Pages p WHERE p.Title = 'About Seattle'", new FeedOptions { MaxItemCount = 1000 });
10. **İş parçacıkları/görevleri sayısını artırın**

    Bkz: [iş parçacıkları/görevlerin sayısını artırmak](#increase-threads) hello ağ bölüm içinde.

11. **64-bit ana bilgisayar işleme kullanın**

    Hello DocumentDB SDK'sı, DocumentDB .NET SDK sürüm 1.11.4 kullanırken ve üzerini 32-bit ana işleminde çalışır. Ancak, çapraz bölüm sorguları kullanıyorsanız, 64-bit ana bilgisayar işleme Gelişmiş performans için önerilir. Şu uygulama türlerini hello hello varsayılan işlemi, sipariş toochange bu too64 bit'da, uygulamanızın hello türüne göre aşağıdaki adımları izleyin 32-bit barındırmasını:

    - Yürütülebilir uygulamalar için bu in işaretini kaldırarak hello tarafından yapılabilir **tercih 32-bit** hello seçeneğinde **proje özelliklerini** penceresinde hello **yapı** sekmesi.

    - Test projeleri VSTest tabanlı için bu seçerek yapılabilir **Test**->**Test ayarlarını**->**varsayılan İşlemci mimarisi X64 olarak**, Merhaba gelen **Visual Studio Test** menü seçeneği.

    - Yerel olarak dağıtılan ASP.NET Web uygulamaları için bu hello denetleyerek yapılabilir **hello 64-bit sürümünü kullanın IIS Express web siteleri ve projeler için**altında **Araçları** ->  **Seçenekler**->**projeler ve çözümler**->**Web projeleri**.

    - Azure üzerinde dağıtılan ASP.NET Web uygulamaları için bu hello seçerek yapılabilir **64-bit olarak Platform** hello içinde **uygulama ayarları** hello Azure portalı üzerinde.

## <a name="indexing-policy"></a>Dizin oluşturma ilkesi
1. **Kullanım için daha hızlı yoğun zamanı alım hızlarını dizin geç**

    Cosmos DB toospecify – hello koleksiyonu düzeyinde – otomatik olarak veya dizini oluşturulmuş bir koleksiyon toobe hello belgelerde istiyorsanız, toochoose sağlayan bir dizin oluşturma ilkesi sağlar.  Ayrıca, zaman uyumlu (CONSISTENT) ve zaman uyumsuz (Lazy) dizin güncelleştirmeleri arasında da seçebilirsiniz. Varsayılan olarak, her ekleme, değiştirme veya belge toohello koleksiyonu silme işlemi hello dizini zaman uyumlu olarak güncelleştirilir. Zaman uyumlu olarak modunu etkinleştirir hello sorguları toohonor hello aynı [tutarlılık düzeyi](consistency-levels.md) hello dizin için herhangi bir gecikme çok "Yakala olmadan" hello, belgesini okur.

    Yavaş dizin oluşturma verileri WINS'e içinde yazılmış senaryoları için düşünülebilecek ve tooamortize hello gerekli iş tooindex daha uzun bir süre boyunca içerik istiyorsunuz. Yavaş dizin de sağlar, toouse, üretilen iş etkili bir şekilde sağlanabilen ve hizmet vermemesini yazma isteği yoğun saatlerde en düşük gecikme süresine sahip. Yavaş dizin oluşturma etkin olduğunda, sorgu sonuçları hello Cosmos DB hesabı için yapılandırılan hello tutarlılık düzeyi bağımsız olarak tutarlı sonunda önemli toonote, ancak olur.

    Bu nedenle, (IndexingPolicy.IndexingMode tooConsistent ayarlanır) tutarlı dizin oluşturma modu hello en yüksek istek birimi ücret Lazy modu (IndexingPolicy.IndexingMode tooLazy ayarlanır) ve dizin oluşturma dizin oluşturma sırasında yazma başına doğurur (IndexingPolicy.Automatic ayarlanır tooFalse) yazma hello zamanda sıfır dizin maliyeti vardır.
2. **Daha hızlı yazmalar için dizin oluşturma kullanılmayan yolu dışla**

    Cosmos veritabanı dizin oluşturma ilkesi Ayrıca hangi yolları tooinclude belge veya dizin yolları (IndexingPolicy.IncludedPaths ve IndexingPolicy.ExcludedPaths) yararlanarak dizin hariç toospecify sağlar. Merhaba kullanımını yollarda dizin oluşturmayı, geliştirilmiş yazma performansı ve dizin oluşturma maliyetleri doğrudan olarak hangi hello sorgu desenlerine önceden bilinen senaryolar için alt dizini depolama dizini benzersiz yol toohello sayısını bağıntılı sunabilir.  Örneğin, kod aşağıdaki hello nasıl tooexclude hello bölümünün tamamını (paketini belgeleri gösterir. bir alt ağacı) hello kullanarak dizin gelen "*" joker karakter.

    ```C#
    var collection = new DocumentCollection { Id = "excludedPathCollection" };
    collection.IndexingPolicy.IncludedPaths.Add(new IncludedPath { Path = "/*" });
    collection.IndexingPolicy.ExcludedPaths.Add(new ExcludedPath { Path = "/nonIndexedContent/*");
    collection = await client.CreateDocumentCollectionAsync(UriFactory.CreateDatabaseUri("db"), excluded);
    ```

    Daha fazla bilgi için bkz: [Azure Cosmos ilkeleri dizin DB](indexing-policies.md).

## <a name="throughput"></a>Aktarım hızı
<a id="measure-rus"></a>

1. **Ölçmek ve alt istek için saniye başına birim kullanım ayarlayın.**

    Cosmos DB zengin bir ilişkisel ve hiyerarşik sorgularıyla UDF'ler, saklı yordamları ve Tetikleyicileri – hello belgelerde veritabanı koleksiyonundaki tüm işletim dahil olmak üzere veritabanı işlemleri sunar. Bu işlemlerin her biri ile ilişkili hello maliyet hello CPU, g/ç ve gerekli bellek toocomplete hello işlemi göre değişir. Göz önünde bulundurulması ve donanım kaynaklarını yönetmek yerine, bir istek birimi (RU) hello kaynakları gerekli tooperform için tek bir ölçü olarak çeşitli veritabanı işlemleri ve hizmeti bir uygulama isteği düşünebilirsiniz.

    [İstek birimleri](request-units.md) hello satın aldığınız kapasite birimlerinin sayısına göre her bir veritabanı hesabı için sağlanır. İstek birimi tüketim saniye başına oranı olarak değerlendirilir. Merhaba oranı hello hello hesabı için bir düzey ayrılmış altına düşene kadar hesaplarında sınırlıdır hello sağlanan istek birimi aşan uygulamaları oranı. Uygulamanız daha yüksek düzeyde üretilen iş gerektiriyorsa, ek kapasite birimleri satın alabilirsiniz.

    bir sorgu Hello karmaşıklığını kaç tane istek birimleri için bir işlem tüketilen etkiler. koşulları Hello sayısı, hello koşulları, UDF'ler sayısı ve tüm hello maliyetini etkilemek hello kaynak veri kümesinin hello boyutu yapısını işlemleri sorgu.

    herhangi bir işlem, toomeasure hello yükünü (oluşturma, güncelleştirme veya silme) hello x-ms-istek-ücret üstbilgi inceleyin (veya ResourceResponse eşdeğer RequestCharge özelliğinde hello<T> veya FeedResponse<T> hello .NET SDK içinde) toomeasure Bu işlemler tarafından tüketilen istek birimleri Hello sayısı.

    ```C#
    // Measure hello performance (request units) of writes
    ResourceResponse<Document> response = await client.CreateDocumentAsync(collectionSelfLink, myDocument);
    Console.WriteLine("Insert of document consumed {0} request units", response.RequestCharge);
    // Measure hello performance (request units) of queries
    IDocumentQuery<dynamic> queryable = client.CreateDocumentQuery(collectionSelfLink, queryString).AsDocumentQuery();
    while (queryable.HasMoreResults)
         {
              FeedResponse<dynamic> queryResponse = await queryable.ExecuteNextAsync<dynamic>();
              Console.WriteLine("Query batch consumed {0} request units", queryResponse.RequestCharge);
         }
    ```             

    Merhaba bu üstbilgisinde döndürülen istek ücret bir sağlanan işleme bölümüdür (yani, 2000 RUs / saniye). Örneğin, Hello önceki sorgu 1000 1 KB-belgeleri döndürürse, hello işlemi hello maliyetini 1000'dir. Bu nedenle, bir saniye içinde sonraki istekler azaltma önce hello sunucu yalnızca iki tür isteklere korur. Daha fazla bilgi için bkz: [istek birimleri](request-units.md) ve hello [istek birimi hesaplayıcı](https://www.documentdb.com/capacityplanner).
<a id="429"></a>
2. **Tanıtıcı oranı sınırlama istek oranı çok büyük**

    Bir istemci bir hesap için tooexceed hello ayrılmış işleme çalıştığında hello sunucuda bir performans düşüşü olmadan ve hiçbir ayrılmış hello düzeyinin ötesine işleme kapasitesi kullanımını yoktur. Merhaba sunucu erken önlem hello istekle RequestRateTooLarge (HTTP durum kodu 429) ve kullanıcı hello milisaniye cinsinden süre hello miktarını hello isteği reattempting önce beklemesi gereken x-ms-yeniden deneme-sonra-ms üstbilgi dönüş hello belirten sona erer.

        HTTP Status 429,
        Status Line: RequestRateTooLarge
        x-ms-retry-after-ms :100

    Merhaba SDK'ları tüm örtük olarak bu yanıt catch, yeniden deneme sonrasında hello sunucu belirtilen üstbilgi saygı ve hello isteği yeniden deneyin. Hesabınızı eşzamanlı olarak birden çok istemci tarafından erişilen sürece hello sonraki yeniden deneme işlemi başarılı olur.

    Üst üste hello istek hızı tutarlı bir şekilde işletim birden fazla istemciniz varsa kümesi too9 hello istemci tarafından dahili olarak değil yeterli varsayılan yeniden deneme sayısı şu anda hello; Bu durumda, hello istemci durum kodu 429 toohello uygulama ile bir DocumentClientException oluşturur. Hello varsayılan yeniden deneme sayısına ayar hello RetryOptions hello ConnectionPolicy örneğinde tarafından değiştirilebilir. Merhaba isteği hello istek hızı yukarıda toooperate devam ederse, varsayılan olarak 30 saniye sonra bir toplam bekleme süresi hello DocumentClientException 429 durum koduyla döndürülür. Merhaba varsayılan 9 veya kullanıcı tanımlı bir değer olması, bu hello geçerli yeniden deneme sayısı hello en fazla yeniden deneme sayısından daha az olduğunda bile oluşur.

    Merhaba otomatik sırada yeniden deneme davranışı tooimprove dayanıklılık ve kullanılabilirlik hello için uygulamaların çoğu yardımcı olur, bu performans kıyaslamaları, özellikle olduğunda gecikme süresini ölçme yaparken at odds gelebilir.  Merhaba deneme hello sunucu kısıtlama isabetler ve hello istemci SDK toosilently yeniden deneme neden olursa hello istemci gözlenen gecikme çıkmasına. tooavoid gecikme ölçü hello ücret her işlem tarafından döndürülen performans denemeleri sırasında ani ve istekleri hello ayrılmış istek hızı çalıştığından emin olun. Daha fazla bilgi için bkz: [istek birimleri](request-units.md).
3. **Daha fazla üretilen işi için daha küçük belgeler için Tasarım**

    Merhaba verilen işlemi isteği giderleri (yani istek işleme maliyet) doğrudan olduğu hello belgenin toohello boyutu bağıntılı. Büyük belgeleri işlemleri birden çok küçük belgeler için işlemleri maliyeti.

## <a name="next-steps"></a>Sonraki adımlar
Bir örnek kullanılan uygulama tooevaluate için Cosmos DB birkaç istemci makineler yüksek performanslı senaryoları için bkz: [performansı ve ölçeği Cosmos DB ile test](performance-testing.md).

Ayrıca, uygulamanız ölçeği ve yüksek performans için tasarlama hakkında daha fazla toolearn bkz [bölümleme ve Azure Cosmos DB'de ölçeklendirme](partition-data.md).
