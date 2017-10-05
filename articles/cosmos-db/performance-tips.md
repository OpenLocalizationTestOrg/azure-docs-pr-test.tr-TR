---
title: "Performans İpuçları - Azure Cosmos DB NoSQL | Microsoft Docs"
description: "Azure Cosmos DB veritabanı performansını iyileştirmek için istemci yapılandırma seçenekleri öğrenin"
keywords: "Veritabanı performansı nasıl"
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
ms.openlocfilehash: a94cda90eca9dca2b93adb8f5091d829e7375aa5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="performance-tips-for-azure-cosmos-db"></a>Azure Cosmos DB performans ipuçları
Azure Cosmos DB garantili gecikme süresi ve verimlilik ile sorunsuz bir şekilde ölçeklendirilebilen bir hızlı ve esnek dağıtılmış veritabanıdır. Büyük mimari değişiklikler yaptığınızda veya veritabanınızla Cosmos DB ölçeklendirmek için karmaşık kodlar yazmak zorunda değildir. Yukarı ve aşağı doğru ölçeklendirme tek bir API çağrısı yapma olarak kadar kolay veya [SDK yöntem çağrısı](set-throughput.md#set-throughput-sdk). Ancak, Cosmos DB ağ çağrıları erişilir en yüksek performans elde etmek için yapabileceğiniz istemci-tarafı iyileştirmeler vardır.

Soran, "nasıl ı my veritabanı performansını geliştirebilir şekilde?" Aşağıdaki seçenekleri göz önünde bulundurun:

## <a name="networking"></a>Ağ
<a id="direct-connection"></a>

1. **Bağlantı İlkesi: doğrudan bağlantı modu kullan**

    Bir istemci Cosmos DB nasıl bağlandığını gözlemlenen istemci-tarafı gecikme açısından özellikle performansı önemli etkilere sahiptir. İki anahtar yapılandırma ayarlarını istemci bağlantı İlkesi – bağlantı yapılandırmak için kullanılabilir *modu* ve [bağlantı *Protokolü*](#connection-protocol).  İki kullanılabilir modları şunlardır:

   1. Ağ geçidi modunda (varsayılan)
   2. Doğrudan modu

      Ağ geçidi modu tüm SDK platformlarda desteklenir ve yapılandırılmış varsayılandır.  Uygulamanız bir şirket ağı içinde katı güvenlik duvarı kısıtlamalarıyla çalışıyorsa standart HTTPS bağlantı noktası ve tek bir uç nokta kullandığından ağ geçidi modu en iyi seçimdir. Performans kolaylığını ancak, veri okuma veya Cosmos Veritabanına yazılan her zaman ağ geçidi modu ek ağ atlama içermesidir. Bu nedenle, doğrudan modu daha az ağ atlamalarını nedeniyle daha iyi performans sunar.
<a id="use-tcp"></a>
2. **Bağlantı İlkesi: TCP protokolünü kullanır**

    Doğrudan modu kullanırken, kullanılabilir iki protokolü seçenek vardır:

   * TCP
   * HTTPS

     Cosmos DB Basit bir sunar ve HTTPS üzerinden RESTful programlama modeli açın. Ayrıca, aynı zamanda RESTful kendi iletişim modelini ve .NET İstemci SDK kullanılabilir verimli bir TCP protokolü sunar. Doğrudan TCP ve HTTPS SSL ilk kimlik doğrulaması ve şifreleme trafiği için kullanın. En iyi performans için mümkün olduğunda TCP protokolünü kullanır.

     TCP ağ geçidi modunda kullanılırken, TCP bağlantı noktası 443 Cosmos DB bağlantı noktası ve 10255 değerini bulur MongoDB API bağlantı noktası. TCP ağ geçidi bağlantı noktalarına ek olarak doğrudan modunda kullanılırken, bağlantı noktası sağlamak zorunda Cosmos DB dinamik TCP bağlantı noktaları kullandığından 10000 20000 arasındaki aralığı açın. Bu bağlantı noktalarının açık değildir ve TCP kullanma girişimi 503 Hizmet kullanılamıyor hatası alıyorsunuz.

     Bağlantı modunu ConnectionPolicy parametresi DocumentClient örneğiyle yapımı sırasında yapılandırılır. Doğrudan modunda kullanılırsa, Protokolü içinde ConnectionPolicy parametresi de ayarlayabilirsiniz.

    ```C#
    var serviceEndpoint = new Uri("https://contoso.documents.net");
    var authKey = new "your authKey from the Azure portal";
    DocumentClient client = new DocumentClient(serviceEndpoint, authKey,
    new ConnectionPolicy
    {
        ConnectionMode = ConnectionMode.Direct,
        ConnectionProtocol = Protocol.Tcp
    });
    ```

    Ağ geçidi modunda kullanılırsa, TCP yalnızca doğrudan modunda desteklendiğinden, HTTPS protokolünü her zaman ağ geçidi ile iletişim kurmak için kullanılır ve ConnectionPolicy Protokolü değeri yoksayılır.

    ![Azure Cosmos DB bağlantı İlkesi çizimi](./media/performance-tips/connection-policy.png)

3. **İlk istek başlatma gecikmesine önlemek için OpenAsync çağırın**

    Adres yönlendirme tablosu getirilemedi içerdiğinden varsayılan olarak, ilk isteği daha yüksek gecikme vardır. Bu ilk istek başlatma gecikmesine önlemek için OpenAsync() kez başlatma sırasında şu şekilde çağırmalıdır.

        await client.OpenAsync();
   <a id="same-region"></a>
4. **Performans için aynı Azure bölgesinde istemciler birlikte bulundurma**

    Mümkün olduğunda, Cosmos DB veritabanı ile aynı bölgede Cosmos DB çağırma herhangi bir uygulama yerleştirin. Yaklaşık bir karşılaştırma için 1-2 ms içinde Cosmos DB çağrıları aynı bölge içinde tamamlanması, ancak Batı ABD, Doğu Yakası arasındaki gecikme süresi > 50 ms. Bu gecikme, Azure veri merkezi sınır istemciden geçerken istek tarafından izlenen yolu bağlı olarak istemek için büyük olasılıkla farklılık gösterebilir. Olası en düşük gecikme, çağıran uygulama sağlanan Cosmos DB uç nokta olduğu Azure bölgesinin içinde bulunduğu sağlanarak elde edilir. Kullanılabilir bölgelerin bir listesi için bkz: [Azure bölgeleri](https://azure.microsoft.com/regions/#services).

    ![Azure Cosmos DB bağlantı İlkesi çizimi](./media/performance-tips/same-region.png)
   <a id="increase-threads"></a>
5. **İş parçacıkları/görevleri sayısını artırın**

    Azure Cosmos DB çağrıları ağ üzerinden yapılan olduğundan, böylece istemci uygulaması bekleyen istekler arasında çok az zaman harcayan, istekleri paralellik derecesini farklılık gerekebilir. Örneğin, kullanıyorsanız. NET'in [görev paralel Kitaplığı](https://msdn.microsoft.com//library/dd460717.aspx), 100s okunurken veya yazılırken Cosmos DB görev sırasına göre oluşturun.

## <a name="sdk-usage"></a>SDK kullanımı
1. **En son SDK'sını yükleyin**

    Cosmos DB SDK'ları en iyi performansı sağlamak için sürekli geliştirilen. Bkz: [Cosmos DB SDK](documentdb-sdk-dotnet.md) en son SDK belirlemek ve geliştirmeleri gözden geçirmek için sayfaları.
2. **Bir singleton Cosmos DB istemci uygulamanızın ömrü boyunca kullanın**

    Her DocumentClient örnek iş parçacığı açısından güvenli ve verimli bağlantı yönetimi ve doğrudan modunda çalışırken adresi önbelleğe alma gerçekleştirir unutmayın. Verimli bağlantı yönetimi ve daha iyi performans DocumentClient ile izin vermek için uygulama yaşam süresi için DocumentClient AppDomain başına tek bir örneğini kullanmak için önerilir.

   <a id="max-connection"></a>
3. **Ağ geçidi modu kullanırken System.Net MaxConnections ana bilgisayar başına artırın**

    Cosmos DB istekleri, HTTPS/REST yapılır, ağ geçidi modu kullanırken ve varsayılan bağlantı sınırını ana bilgisayar adı veya IP adresi başına tabi. Böylece istemci kitaplığı Cosmos DB birden çok eşzamanlı bağlantıların kullanabilir MaxConnections daha yüksek bir değer (100-1000) ayarlamanız gerekebilir. .NET SDK'sındaki 1.8.0 ve varsayılan değerin üzerinde [ServicePointManager.DefaultConnectionLimit](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit.aspx) 50'dir ve değerini değiştirmek için ayarlayabileceğiniz [Documents.Client.ConnectionPolicy.MaxConnectionLimit](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.connectionpolicy.maxconnectionlimit.aspx)daha yüksek bir değere.   
4. **Paralel sorgular bölümlenmiş koleksiyonlar için ayarlama**

     DocumentDB .NET SDK sürüm 1.9.0 ve paralel bölümlendirilmiş bir koleksiyon sorgulamak etkinleştirme desteği paralel sorgular yukarıda (bkz [SDK'ları ile çalışma](documentdb-partition-data.md#working-with-the-azure-cosmos-db-sdks) ve ilgili [kod örnekleri](https://github.com/Azure/azure-documentdb-dotnet/blob/master/samples/code-samples/Queries/Program.cs) daha fazla bilgi için bilgileri). Paralel sorgular seri bunların karşılık gelen sorgu gecikme süresi ve üretilen işi artırmak için tasarlanmıştır. Paralel sorguları, kullanıcılar için özel Sığdır gereksinimlerine, (a) MaxDegreeOfParallelism ayarlayabilirsiniz iki parametre sağlar: en çok sonra bölüm sayısı sorgulanan paralel ve (b) MaxBufferedItemCount denetlemek için: sayısını kontrol etmek için önceden getirilen sonuç.

    (a) ***ayarlama MaxDegreeOfParallelism\: *** paralel sorgu works birden çok bölümü paralel sorgulayarak. Ancak, tek bir bölümlenmiş toplama verileri seri olarak sorgu göre getirilir. Bu nedenle, diğer tüm sistem koşulları aynı kalır sağlanan çoğu kullanıcı sorgu elde maksimum fırsat bir bölüm sayısı MaxDegreeOfParallelism ayarlama sahiptir. Bölüm sayısı bilmiyorsanız, yüksek bir sayıya MaxDegreeOfParallelism ayarlayabilir ve sistem MaxDegreeOfParallelism en az (bölüm, kullanıcı tarafından sağlanan girdi sayısı) seçer.

    Verileri sorgu göre tüm bölümleri arasında eşit olarak dağıtılır, paralel sorgular en iyi avantajları oluşturduğunun dikkate almak önemlidir. Bölümlenmiş koleksiyonu (en kötü durumda bir bölüm) birkaç bölümlerdeki tamamı veya bir sorgu tarafından döndürülen verilerin çoğunu bir yoğunlaşmıştır, ardından sorgu performansını tarafından bu bölümler nedeniyle düşük performansa şekilde bölümlenmiş durumunda.

    (b) ***ayarlama MaxBufferedItemCount\: *** paralel sorgu sonuçlarının geçerli toplu işlem istemci tarafından gerçekleştirilirken sonuçları önceden getirmek için tasarlanmıştır. Önceden getirme sorgu genel gecikme gelişme yardımcı olur. MaxBufferedItemCount önceden getirilen sonuç sayısını sınırlamak için parametresidir. Döndürülen sonuçları beklenen sayıda MaxBufferedItemCount (veya daha yüksek bir sayı) ayarlamayı önceden getirme maksimum avantajı almak sorgu sağlar.

    Önceden getirme MaxDegreeOfParallelism bağımsız olarak aynı şekilde çalışır ve tüm bölümleri verileri için tek bir arabelleğe olduğunu unutmayın.  
5. **Sunucu tarafı GC üzerinde Aç**

    Çöp toplama sıklığını azaltmayı bazı durumlarda yardımcı olabilir. .NET ile ayarlamak [gcServer](https://msdn.microsoft.com/library/ms229357.aspx) true.
6. **Geri Çekilme RetryAfter aralıklarla uygulama**

    Performans testi sırasında istekleri küçük oranını kısıtlanan kadar yük artırmanız gerekir. Kısıtlanan, istemci uygulamasına geri Çekilme kısıtlama üzerinde sunucu belirtilen yeniden deneme aralığını gerekir. Geri Çekilme uyarak denemeler arasındaki bekleme süresi en az miktarda harcamanızı sağlar. Yeniden deneme ilkesi desteği eklenmiştir sürümünde 1.8.0 ve yukarıdaki documentdb'nin [.NET](documentdb-sdk-dotnet.md) ve [Java](documentdb-sdk-java.md), sürüm 1.9.0 ve üstü, [Node.js](documentdb-sdk-node.md) ve [Python ](documentdb-sdk-python.md), ve tüm desteklenen sürümlerinde [.NET Core](documentdb-sdk-dotnet-core.md) SDK'ları. Daha fazla bilgi için bkz: [Exceeding ayrılmış işleme sınırları](request-units.md#RequestRateTooLarge) ve [RetryAfter](https://msdn.microsoft.com/library/microsoft.azure.documents.documentclientexception.retryafter.aspx).
7. **İstemci-iş yükünü ölçeklendirme**

    Yüksek işleme düzeyleri sınıyorsanız (> 50.000 RU/s), istemci uygulaması makine çıkışı CPU veya ağ kullanımını capping nedeniyle ayak bağı. Bu noktaya ulaştıysanız, birden çok sunucu arasında istemci uygulamalarının ölçeklendirme tarafından Cosmos DB hesap ek itme devam edebilirsiniz.
8. **Daha düşük okuma gecikmesi için önbellek belge URI'ler**

    Önbellek belge URI'ler okuma en iyi performans için mümkün.
   <a id="tune-page-size"></a>
9. **Sorguları/okuma akışları daha iyi performans için sayfa boyutunu ayarlama**

    Bir toplu gerçekleştirme belgeleri okuma akışı işlevleri (örneğin, ReadDocumentFeedAsync) kullanarak veya bir DocumentDB SQL sorgu gönderirken okurken sonuç kümesi çok büyük ise sonuçları bölümlenmiş bir şekilde döndürülür. Varsayılan olarak, ilk isabet sınırlarından hangisi olduğunu, sonuçları 100 öğeleri ya da 1 MB yığınlar halinde döndürdü.

    Sayısını azaltmak için ağ gidiş dönüşleri tüm geçerli sonuçları almak için gerekli, en fazla 1000 x-ms-max-öğesi-count istek üstbilgisi kullanarak sayfa boyutunu artırabilirsiniz. Burada yalnızca birkaç sonuçları görüntülemek için gereken durumlarda Örneğin, kullanıcı arabirimi veya uygulama API yalnızca 10 döndürürse birer sonuçları, aynı zamanda okuma ve sorgular için tüketilen verimlilik azaltmak için 10 sayfa boyutunu azaltabilirsiniz.

    Sayfa boyutu kullanılabilir Cosmos DB SDK'ları kullanarak da ayarlayabilirsiniz.  Örneğin:

        IQueryable<dynamic> authorResults = client.CreateDocumentQuery(documentCollection.SelfLink, "SELECT p.Author FROM Pages p WHERE p.Title = 'About Seattle'", new FeedOptions { MaxItemCount = 1000 });
10. **İş parçacıkları/görevleri sayısını artırın**

    Bkz: [iş parçacıkları/görevlerin sayısını artırmak](#increase-threads) ağ bölümünde.

11. **64-bit ana bilgisayar işleme kullanın**

    DocumentDB SDK'sı bir 32-bit ana işlem DocumentDB .NET SDK sürüm 1.11.4 kullanırken ve üstünde çalışır. Ancak, çapraz bölüm sorguları kullanıyorsanız, 64-bit ana bilgisayar işleme Gelişmiş performans için önerilir. 64 bit izleyin değiştirmek için aşağıdaki adımları uygulamanız türüne bağlı şekilde aşağıdaki uygulama türlerini varsayılan olarak, 32-bit ana bilgisayar işlemi vardır:

    - Yürütülebilir uygulamalar için bu kaldırarak yapılabilir **tercih 32-bit** seçeneğini **proje özelliklerini** penceresi, **yapı** sekmesi.

    - Test projeleri VSTest tabanlı için bu seçerek yapılabilir **Test**->**Test ayarlarını**->**varsayılan İşlemci mimarisi X64 olarak**, gelen **Visual Studio Test** menü seçeneği.

    - Yerel olarak dağıtılan ASP.NET Web uygulamaları için bu kontrol ederek yapılabilir **web siteleri ve projeler için IIS Express 64-bit sürümünü kullanmanız**altında **Araçları**->**seçenekleri**  -> **Projeler ve çözümler**->**Web projeleri**.

    - Azure üzerinde dağıtılan ASP.NET Web uygulamaları için bu seçerek yapılabilir **64-bit olarak Platform** içinde **uygulama ayarları** Azure portalındaki.

## <a name="indexing-policy"></a>Dizin oluşturma ilkesi
1. **Kullanım için daha hızlı yoğun zamanı alım hızlarını dizin geç**

    Cosmos DB belgeleri otomatik olarak veya olmayan listelenecek koleksiyonundaki isteyip istemediğinizi seçmenize olanak tanıyan bir dizin oluşturma ilkesi – koleksiyon düzeyinde – belirtmenize olanak tanır.  Ayrıca, zaman uyumlu (CONSISTENT) ve zaman uyumsuz (Lazy) dizin güncelleştirmeleri arasında da seçebilirsiniz. Varsayılan olarak, dizin her ekleme, değiştirme veya koleksiyona bir belgeyi silme zaman uyumlu olarak güncelleştirilir. Zaman uyumlu olarak aynı vermenizin sorguları modunu etkinleştirir [tutarlılık düzeyi](consistency-levels.md) belgenin "yakala" dizin için herhangi bir gecikme olmadan okuyan gibi.

    Yavaş dizin oluşturma verileri WINS'e içinde yazılmış senaryoları için düşünülebilecek ve daha uzun bir süre boyunca dizin içerik için gereken iş İtfası istiyorsunuz. Yavaş dizin oluşturma, sağlanan işleme etkili bir şekilde kullanmak ve en düşük gecikme süresi ile yoğun saatlerde yazma isteklerine hizmet sağlar. Ancak, yavaş dizin oluşturma etkin olduğunda, sorgu sonuçları Cosmos DB hesabı için yapılandırılan tutarlılık düzeyi bakılmaksızın sonunda tutarlı olduğunu dikkate almak önemlidir.

    Bu nedenle, (IndexingPolicy.IndexingMode CONSISTENT için ayarlanır) tutarlı dizin oluşturma modu Lazy modu (Lazy için IndexingPolicy.IndexingMode ayarlanır) ve dizin oluşturma dizin oluşturma işlemi sırasında yazma başına en yüksek istek birimi ücret doğurur (IndexingPolicy.Automatic ayarlanır False) dizin sıfır maliyet yazma zamanda vardır.
2. **Daha hızlı yazmalar için dizin oluşturma kullanılmayan yolu dışla**

    Cosmos veritabanı dizin oluşturma ilkesini de dahil etmek veya hariç dizin yolları (IndexingPolicy.IncludedPaths ve IndexingPolicy.ExcludedPaths) yararlanarak dizin hangi belge yolları belirtmenize olanak tanır. Dizin oluşturma maliyetleri doğrudan dizine benzersiz yolları sayısı bağıntılı gibi yolları dizin kullanımını geliştirilmiş yazma performansı ve sorgu desenlerine önceden bilinir senaryoları için alt dizini depolama sunabilir.  Örneğin, aşağıdaki kod belgeleri bölümünün tamamını (paketini dışlama gösterir bir alt ağacı) dizin kullanarak "*" joker karakter.

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

    Cosmos DB zengin bir ilişkisel ve hiyerarşik sorgularıyla UDF'ler, saklı yordamları ve Tetikleyicileri – tüm işletim veritabanı koleksiyon içindeki belgelerde dahil olmak üzere veritabanı işlemleri sunar. Bu işlemlerin her biri ile ilişkili maliyet CPU, g/ç ve işlemi tamamlamak için gereken bellek göre değişir. Göz önünde bulundurulması ve donanım kaynaklarını yönetmek yerine, bir uygulama isteği hizmet ve çeşitli veritabanı işlemlerini gerçekleştirmek için gereken kaynakları için tek bir ölçü olarak bir istek birimi (RU) düşünebilirsiniz.

    [İstek birimleri](request-units.md) satın aldığınız kapasite birimlerinin sayısına göre her bir veritabanı hesabı için sağlanır. İstek birimi tüketim saniye başına oranı olarak değerlendirilir. Sağlanan istek birimi oranı oranı hesabı için ayrılmış düzeyinin altına düşene kadar hesaplarında sınırlıdır aşan uygulamalar. Uygulamanız daha yüksek düzeyde üretilen iş gerektiriyorsa, ek kapasite birimleri satın alabilirsiniz.

    Kaç tane istek birimlerine bir işlem için kullanılan bir sorgu karmaşıklığını etkiler. Koşulları sayısı, koşulları, UDF'ler sayısı ve tüm kaynak veri kümesi boyutunu yapısını sorgu işlemlerinin maliyetini etkiler.

    Herhangi bir işlem yükü ölçmek için (oluşturma, güncelleştirme veya silme), x-ms-istek-ücret üstbilgi inceleyin (veya eşdeğer RequestCharge özelliği ResourceResponse ile<T> veya FeedResponse<T> .NET SDK'sındaki) sayısını ölçmek için Bu işlemler tarafından tüketilen istek birimleri.

    ```C#
    // Measure the performance (request units) of writes
    ResourceResponse<Document> response = await client.CreateDocumentAsync(collectionSelfLink, myDocument);
    Console.WriteLine("Insert of document consumed {0} request units", response.RequestCharge);
    // Measure the performance (request units) of queries
    IDocumentQuery<dynamic> queryable = client.CreateDocumentQuery(collectionSelfLink, queryString).AsDocumentQuery();
    while (queryable.HasMoreResults)
         {
              FeedResponse<dynamic> queryResponse = await queryable.ExecuteNextAsync<dynamic>();
              Console.WriteLine("Query batch consumed {0} request units", queryResponse.RequestCharge);
         }
    ```             

    Bu üstbilgisinde döndürülen istek ücret bir sağlanan işleme bölümüdür (yani, 2000 RUs / saniye). Örneğin, önceki sorgunun 1000 1 KB-belgeleri döndürürse, işlem maliyetini 1000'dir. Bu nedenle, bir saniye içinde sonraki istekler azaltma önce sunucunun yalnızca iki tür isteklere korur. Daha fazla bilgi için bkz: [istek birimleri](request-units.md) ve [istek birimi hesaplayıcı](https://www.documentdb.com/capacityplanner).
<a id="429"></a>
2. **Tanıtıcı oranı sınırlama istek oranı çok büyük**

    Bir istemci bir hesap için ayrılmış işleme aşan girişiminde bulunduğunda, sunucuda bir performans düşüşü olmadan ve işleme kapasitesi ayrılmış düzeyinin ötesine hiçbir kullanımını yoktur. Sunucu erken önlem isteği RequestRateTooLarge (HTTP durum kodu 429) ile bitmelidir ve kullanıcı isteği reattempting önce beklemesi gereken milisaniye cinsinden süreyi belirten x-ms-yeniden deneme-sonra-ms üstbilgi döndürür.

        HTTP Status 429,
        Status Line: RequestRateTooLarge
        x-ms-retry-after-ms :100

    SDK'ları tüm örtük olarak bu yanıt catch, yeniden deneme sonra sunucu tarafından belirtilen üstbilgi saygı ve isteği yeniden deneyin. Hesabınızı eşzamanlı olarak birden çok istemci tarafından erişilen sürece, sonraki yeniden deneme işlemi başarılı olur.

    Birden fazla istemci üst üste istek hızı tutarlı bir şekilde işletim varsa, 9 istemci tarafından dahili olarak ayarlanmış varsayılan yeniden deneme sayısı yeterli değil; Bu durumda, istemci uygulamaya 429 durum koduyla bir DocumentClientException oluşturur. Varsayılan yeniden deneme sayısı ConnectionPolicy örneğinde RetryOptions ayarlayarak değiştirilebilir. İstek istek hızı çalışmaya devam ederse, varsayılan olarak, 30 saniye sonra bir toplam bekleme süresi 429 durum koduyla DocumentClientException döndürülür. Bu geçerli yeniden deneme sayısı en fazla yeniden deneme sayısından daha az olduğunda bile oluşur, varsayılan 9 veya kullanıcı tanımlı bir değer olmalıdır.

    Dayanıklılık ve kullanılabilirlik çoğu uygulamalar geliştirmek için otomatik yeniden deneme davranışı yardımcı olsa da, bu performans kıyaslamaları, özellikle gecikme süresini ölçme zaman yaparken at odds gelebilir.  Denemeyi sunucu kısıtlama isabetler ve sessiz bir şekilde yeniden denemek için SDK istemci neden olursa istemci gözlenen gecikme çıkmasına. Performans denemeleri sırasında gecikme ani önlemek için her işlem tarafından döndürülen farkı ölçmek ve istekleri ayrılmış istek hızı çalıştığından emin olun. Daha fazla bilgi için bkz: [istek birimleri](request-units.md).
3. **Daha fazla üretilen işi için daha küçük belgeler için Tasarım**

    Belirli bir işlemi isteği giderleri (yani istek işleme maliyet) doğrudan belgenin boyutunu ilişkilendirilir. Büyük belgeleri işlemleri birden çok küçük belgeler için işlemleri maliyeti.

## <a name="next-steps"></a>Sonraki adımlar
Birkaç istemci makineler yüksek performanslı senaryoları için Cosmos DB değerlendirmek için kullanılan örnek bir uygulama için bkz: [performansı ve ölçeği Cosmos DB ile test](performance-testing.md).

Ayrıca, uygulamanız ölçeği ve yüksek performans için tasarlama hakkında daha fazla bilgi için bkz. [bölümleme ve Azure Cosmos DB'de ölçeklendirme](partition-data.md).
