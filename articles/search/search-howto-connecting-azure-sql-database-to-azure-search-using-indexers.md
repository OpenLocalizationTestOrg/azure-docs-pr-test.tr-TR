---
title: "aaaConnecting Azure SQL veritabanı tooAzure arama kullanarak dizin oluşturucular | Microsoft Docs"
description: "Dizin oluşturucular kullanarak Azure SQL veritabanı tooan Azure Search toopull verileri nasıl dizin öğrenin."
services: search
documentationcenter: 
author: chaosrealm
manager: pablocas
editor: 
ms.assetid: e9bbf352-dfff-4872-9b17-b1351aae519f
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/13/2017
ms.author: eugenesh
ms.openlocfilehash: b28a11cf18ef994de99e09af90bbfeb171ef3cde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connecting-azure-sql-database-tooazure-search-using-indexers"></a>Azure SQL veritabanı tooAzure bağlanma dizin oluşturucular kullanma arama

Sorgulayabileceğiniz önce bir [Azure Search dizini](search-what-is-an-index.md), verilerinizle doldurmanız gerekir. Merhaba verileri bir Azure SQL veritabanında yaşıyorsa bir **Azure SQL veritabanı için Azure Search dizin oluşturucusunu** (veya **Azure SQL dizin oluşturucu** kısaca) kod toowrite daha az ve daha az anlamına gelir hello dizin oluşturma işlemini otomatik hale getirebilirsiniz Altyapı toocare hakkında.

Bu makale kullanmanın hello mekanizması kapsamaktadır [dizin oluşturucular](search-indexer-overview.md), ancak aynı zamanda yalnızca Azure SQL veritabanları (örneğin, tümleşik değişiklik izleme) ile kullanılabilen özellikleri açıklar. 

Toplama tooAzure SQL veritabanlarında Azure Search'te dizin oluşturucular için sağlar [Azure Cosmos DB](search-howto-index-documentdb.md), [Azure Blob Depolama](search-howto-indexing-azure-blob-storage.md), ve [Azure tablo depolaması](search-howto-indexing-azure-tables.md). diğer veri kaynakları için toorequest destek hello üzerinde geri bildirim sağlamak [Azure Search geri bildirim Forumunda](https://feedback.azure.com/forums/263029-azure-search/).

## <a name="indexers-and-data-sources"></a>Dizin oluşturucular ve veri kaynakları

A **veri kaynağı** , kimlik bilgileri veri erişimi ve verimli bir şekilde (yeni, değiştirilen veya silinen satır) hello verilerde yapılan değişiklikler tanımlayan ilkeler için hangi veri tooindex belirtir. Böylece birden çok dizin oluşturucu tarafından kullanılan bağımsız bir kaynak olarak tanımlanır.

Bir **dizin oluşturucu** hedeflenen arama dizini ile tek bir veri kaynağına bağlanan bir kaynaktır. Bir dizin oluşturucu yolları aşağıdaki hello kullanılır:

* Merhaba veri toopopulate dizin tek seferlik bir kopyasını gerçekleştirin.
* Bir zamanlamada hello veri kaynağındaki değişikliklerle dizin güncelleştirin.
* İsteğe bağlı tooupdate gerektiği gibi bir dizin çalıştırın.

Tek bir dizin oluşturucu, yalnızca bir tablo veya Görünüm kullanabilir, ancak birden çok arama dizinlerini toopopulate istiyorsanız birden çok dizin oluşturucu oluşturabilirsiniz. Kavramları hakkında daha fazla bilgi için bkz: [dizin oluşturucu işlemleri: normal iş akışı](https://docs.microsoft.com/rest/api/searchservice/Indexer-operations#typical-workflow).

Ayarlama ve bir Azure SQL Dizin Oluşturucu kullanarak yapılandırma:

* Merhaba, Veri Alma Sihirbazı [Azure portalı](https://portal.azure.com)
* Azure arama [.NET SDK'sı](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.indexer?view=azure-dotnet)
* Azure arama [REST API'si](https://docs.microsoft.com/en-us/rest/api/searchservice/indexer-operations)

Bu makalede, hello REST API toocreate kullanacağız **dizin oluşturucular** ve **veri kaynakları**.

## <a name="when-toouse-azure-sql-indexer"></a>Zaman toouse Azure SQL dizin oluşturucu
Tooyour veri ilgili çeşitli etkenlere bağlı olarak Azure SQL dizin oluşturucu kullanımını hello olabilir veya uygun olmayabilir. Verilerinizi hello gereksinimleri aşağıdaki uyuyorsa, Azure SQL dizin oluşturucu kullanabilirsiniz.

| Ölçütler | Ayrıntılar |
|----------|---------|
| Tek bir tablo veya Görünüm veri kaynağı | Merhaba veri arasında birden çok tablo dağılmış, hello verileri tek bir görünüm oluşturabilirsiniz. Ancak, bir görünüm kullanırsanız, mümkün toouse SQL Server'ın tümleşik değişiklik algılama toorefresh dizin artımlı değişiklikler ile olmayacaktır. Daha fazla bilgi için bkz: [yakalama değiştirilen ve silinen satır](#CaptureChangedRows) aşağıda. |
| Veri türlerinin uyumlu olduğundan | Bir Azure Search dizini tümünün değil ancak çoğu hello SQL türleri desteklenir. Bir listesi için bkz: [veri türlerini eşleştirme](#TypeMapping). |
| Gerçek zamanlı veri eşitleme gerekli değil | Bir dizin oluşturucu tablonuz en fazla beş dakikada yeniden dizin oluşturabilirsiniz. Veri değişikliklerini sık sık ve hello değişirse hello dizinde saniye ya da tek dakikalar içinde yansıtılan gerek toobe hello kullanmanızı öneririz [REST API](https://docs.microsoft.com/rest/api/searchservice/AddUpdate-or-Delete-Documents) veya [.NET SDK'sı](search-import-data-dotnet.md) toopush satırları doğrudan güncelleştirildi. |
| Artımlı dizin mümkündür | Büyük bir veri kümesi varsa ve Azure Search bir zamanlamaya göre plan toorun hello dizinleyici erişebilmeleri gerekir tooefficiently yeni, değiştirilen veya silinen satırları tanımlayın. İsteğe bağlı (zamanlamada değil) dizin oluşturma veya 100. 000'den az satır dizinini olmayan Artımlı dizin oluşturma işlemi yalnızca izin verilir. Daha fazla bilgi için bkz: [yakalama değiştirilen ve silinen satır](#CaptureChangedRows) aşağıda. |

## <a name="create-an-azure-sql-indexer"></a>Bir Azure SQL dizin oluşturucu yapın

1. Merhaba veri kaynağı oluşturun:

   ```
    POST https://myservice.search.windows.net/datasources?api-version=2016-09-01
    Content-Type: application/json
    api-key: admin-key

    {
        "name" : "myazuresqldatasource",
        "type" : "azuresql",
        "credentials" : { "connectionString" : "Server=tcp:<your server>.database.windows.net,1433;Database=<your database>;User ID=<your user name>;Password=<your password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30;" },
        "container" : { "name" : "name of hello table or view that you want tooindex" }
    }
   ```

   Hello hello bağlantı dizesi alma [Azure portal](https://portal.azure.com); hello kullan `ADO.NET connection string` seçeneği.

2. Zaten yoksa, hello hedef Azure Search dizini oluşturma. Hello kullanarak bir dizin oluşturabilirsiniz [portal](https://portal.azure.com) veya hello [oluşturma dizini API](https://docs.microsoft.com/rest/api/searchservice/Create-Index). Bu hello emin olun, hedef dizin şemasını hello kaynak tablosunun hello şemasıyla uyumlu - bkz [veri türleri SQL ve Azure search arasında eşleme](#TypeMapping).

3. Merhaba dizin oluşturucu, bir ad verip ve hello verilerin kaynak ve hedef dizin başvuran oluşturun:

    ```
    POST https://myservice.search.windows.net/indexers?api-version=2016-09-01
    Content-Type: application/json
    api-key: admin-key

    {
        "name" : "myindexer",
        "dataSourceName" : "myazuresqldatasource",
        "targetIndexName" : "target index name"
    }
    ```

Bu yolla oluşturulan bir dizin oluşturucu bir zamanlama yok. Ne zaman oluşturulduktan sonra otomatik olarak çalıştırılır. Yeniden miktar adresindeki kullanarak istediğiniz zaman çalıştırabilirsiniz bir **dizin** isteği:

    POST https://myservice.search.windows.net/indexers/myindexer/run?api-version=2016-09-01
    api-key: admin-key

Dizin Oluşturucu davranışı, toplu iş boyutu ve bir dizinleyici yürütme başarısız olmadan önce kaç tane belgeleri atlanabilir gibi çeşitli yönlerini özelleştirebilirsiniz. Daha fazla bilgi için bkz: [dizin oluşturucu API oluşturma](https://docs.microsoft.com/rest/api/searchservice/Create-Indexer).

Tooallow Azure Hizmetleri tooconnect tooyour veritabanı gerekebilir. Bkz: [Azure bağlanma](https://docs.microsoft.com/azure/sql-database/sql-database-firewall-configure) yönelik yönergeler toodo.

Dizin Oluşturucu durumu ve yürütme geçmişi (dizinli öğe sayısı, hatalar, vb.), kullanım toomonitor hello bir **dizin oluşturucu durumu** isteği:

    GET https://myservice.search.windows.net/indexers/myindexer/status?api-version=2016-09-01
    api-key: admin-key

Merhaba yanıt benzer toohello aşağıdaki gibi görünmelidir:

    {
        "@odata.context":"https://myservice.search.windows.net/$metadata#Microsoft.Azure.Search.V2015_02_28.IndexerExecutionInfo",
        "status":"running",
        "lastResult": {
            "status":"success",
            "errorMessage":null,
            "startTime":"2015-02-21T00:23:24.957Z",
            "endTime":"2015-02-21T00:36:47.752Z",
            "errors":[],
            "itemsProcessed":1599501,
            "itemsFailed":0,
            "initialTrackingState":null,
            "finalTrackingState":null
        },
        "executionHistory":
        [
            {
                "status":"success",
                "errorMessage":null,
                "startTime":"2015-02-21T00:23:24.957Z",
                "endTime":"2015-02-21T00:36:47.752Z",
                "errors":[],
                "itemsProcessed":1599501,
                "itemsFailed":0,
                "initialTrackingState":null,
                "finalTrackingState":null
            },
            ... earlier history items
        ]
    }

(Merhaba son yürütme hello yanıtta önce geliyorsa) böylece hello ters kronolojik sırada sıralanır en son tamamlandı hello yürütmeleri too50 yukarı yürütme geçmişini içerir.
Merhaba yanıt hakkında ek bilgiler bulunabilir [dizin oluşturucu durumunu Al](http://go.microsoft.com/fwlink/p/?LinkId=528198)

## <a name="run-indexers-on-a-schedule"></a>Dizin oluşturucular bir zamanlamaya göre Çalıştır
Merhaba dizin oluşturucu toorun düzenli bir zamanlamaya göre de sıralayabilirsiniz. toodo bunu hello eklemek **zamanlama** oluştururken veya güncelleştirirken hello dizin oluşturucu özelliği. Aşağıdaki Hello örnek bir PUT İsteği tooupdate hello dizin oluşturucu gösterir:

    PUT https://myservice.search.windows.net/indexers/myindexer?api-version=2016-09-01
    Content-Type: application/json
    api-key: admin-key

    {
        "dataSourceName" : "myazuresqldatasource",
        "targetIndexName" : "target index name",
        "schedule" : { "interval" : "PT10M", "startTime" : "2015-01-01T00:00:00Z" }
    }

Merhaba **aralığı** parametresi gereklidir. başlangıç aralığı iki ardışık dizin oluşturucu yürütmeleri hello başlangıcı arasındaki toohello süreyi ifade eder. en küçük Hello aralığı 5 dakika verilir; Merhaba uzun bir gündür. Bir XSD "dayTimeDuration" değeri biçimlendirilmelidir (sınırlı alt kümesi bir [ISO 8601 süre](http://www.w3.org/TR/xmlschema11-2/#dayTimeDuration) değeri). Bu Hello deseni: `P(nD)(T(nH)(nM))`. Örnekler: `PT15M` her 15 dakikada için `PT2H` için her 2 saatte bir.

İsteğe bağlı Hello **startTime** zaman hello zamanlanmış yürütmeleri başlamak gösterir. Merhaba geçerli UTC saat çıkarılırsa, kullanılır. Bu süre hello dizin oluşturucu hello startTime sürekli olarak çalışan sanki geçmiş – hello ilk yürütme; bu durumda Zamanlanmış hello olabilir.  

Bir dizin oluşturucu yalnızca bir yürütme aynı anda çalıştırabilirsiniz. Bir dizin oluşturucu yürütülmesinin zamanlandığı çalışıyorsa hello yürütme zamanlanan bir sonraki saatte hello kadar ertelenir.

Şimdi bir örnek toomake şunları göz önünde bulundurun daha somut. Biz yapılandırılmış saatlik zamanlaması hello varsayın:

    "schedule" : { "interval" : "PT1H", "startTime" : "2015-03-01T00:00:00Z" }

Şunlar olur:

1. Merhaba ilk dizin oluşturucusu yürütme sırasında veya 1 Mart 2015 12: 00'da çevresinde başlatır UTC.
2. Bu yürütme 20 dakika (veya her zaman değerinden 1 saat) alır varsayalım.
3. Merhaba ikinci yürütme sırasında veya 1 Mart 2015 1: 00'da çevresinde başlatır
4. Şimdi yaklaşık 2: 10'da tamamlandıktan böylece bu yürütme bir saatten – Örneğin, 70 dakika – aldığını varsayalım.
5. Saat 2:00 ' da artık hello üçüncü yürütme toostart olur. Ancak, çünkü hello 1 da ikinci yürütülmesini hala, çalışıyor hello üçüncü yürütme atlandı. 3 sabah Hello üçüncü yürütülmesine başlar

Eklemek, değiştirmek veya varolan bir dizin oluşturucu için bir zamanlama kullanarak silme bir **PUT dizin oluşturucu** isteği.

<a name="CaptureChangedRows"></a>

## <a name="capture-new-changed-and-deleted-rows"></a>Yeni, değiştirilen ve silinen satır yakalama

Azure Search kullanan **Artımlı dizin** tooavoid toore-Merhaba tablonun tümünü veya bir dizin oluşturucu her çalıştığında görüntüleyin dizine sahip. Azure arama, iki algılama ilkeleri toosupport artımlı dizinini değiştirme sağlar. 

### <a name="sql-integrated-change-tracking-policy"></a>SQL ile tümleştirilen değişiklik izleme ilkesinin
SQL veritabanınız destekliyorsa [değişiklik izleme](https://docs.microsoft.com/sql/relational-databases/track-changes/about-change-tracking-sql-server), kullanmanızı öneririz **SQL tümleşik değişiklik izleme İlkesi**. Bu hello en verimli ilkesidir. Ayrıca, bu Azure Search tooidentify silinen satır tooadd kalmadan bir açık "geçici silme" sütun tooyour tablosu sağlar.

#### <a name="requirements"></a>Gereksinimler 

+ Veritabanı sürüm gereksinimleri:
  * SQL Server 2012 SP3 ve daha sonra Azure Vm'lerinde SQL Server kullanıyorsanız.
  * Azure SQL veritabanı kullanıyorsanız, Azure SQL Database V12.
+ Tabloları yalnızca (Görünüm). 
+ Merhaba veritabanında [etkinleştir değişiklik izleme](https://docs.microsoft.com/sql/relational-databases/track-changes/enable-and-disable-change-tracking-sql-server) hello tablosu için. 
+ Birleşik birincil anahtar (bir birincil anahtar içeren birden fazla sütun) hello tablosunda.  

#### <a name="usage"></a>Kullanım

toouse Bu ilkeyi oluştur veya veri kaynağınızı şöyle güncelleştir:

    {
        "name" : "myazuresqldatasource",
        "type" : "azuresql",
        "credentials" : { "connectionString" : "connection string" },
        "container" : { "name" : "table or view name" },
        "dataChangeDetectionPolicy" : {
           "@odata.type" : "#Microsoft.Azure.Search.SqlIntegratedChangeTrackingPolicy"
      }
    }

Silinen satır zaman SQL tümleşik değişiklik izleme ilkesinin, kullanarak belirtme ayrı veri silme algılama İlkesi - bu ilkeyi tanımlamak için yerleşik destek yok. Ancak, hello siler algılanan toobe "automagically" Merhaba belge anahtarında search dizininizi gerekir olması hello hello SQL tablosu hello birincil anahtar ile aynı. 

<a name="HighWaterMarkPolicy"></a>

### <a name="high-water-mark-change-detection-policy"></a>Yüksek su işareti değişiklik algılama İlkesi

Bu değişiklik algılama İlkesi hello sürümü veya bir satır en son güncelleştirildiği zaman yakalama bir "yüksek su işareti" sütun kullanır. Bir görünüm kullanıyorsanız, yüksek su işareti İlkesi kullanmanız gerekir. Merhaba yüksek su işareti sütun hello aşağıdaki gereksinimleri karşılaması gerekir.

#### <a name="requirements"></a>Gereksinimler 

* Tüm eklemeleri hello sütun için bir değer belirtin.
* Tüm güncelleştirmeler tooan öğesi de hello sütun hello değerini değiştirin.
* Bu sütunun Hello değeri her INSERT veya update artırır.
* Sorguları yeri aşağıdaki hello ve ORDER BY yan tümceleri verimli bir şekilde çalıştırılabilir:`WHERE [High Water Mark Column] > [Current High Water Mark Value] ORDER BY [High Water Mark Column]`

> [!IMPORTANT] 
> Hello kullanarak önerilir [rowversion](https://docs.microsoft.com/sql/t-sql/data-types/rowversion-transact-sql) hello yüksek su işareti sütun için veri türü. Başka bir veri türü kullanılırsa, değişiklik izleme tüm değişiklikler eşzamanlı olarak bir dizin oluşturucu sorgusu yürütme işlemleri hello varlığını toocapture garanti edilmez. Kullanırken **rowversion** salt okunur çoğaltmaları bir yapılandırmada hello birincil kopyada hello dizin oluşturucu işaret etmelidir. Yalnızca birincil kopya veri eşitleme senaryoları için kullanılabilir.

#### <a name="usage"></a>Kullanım

toouse yüksek su işareti ilkesi oluşturun veya bu gibi veri kaynağınız güncelleştirin:

    {
        "name" : "myazuresqldatasource",
        "type" : "azuresql",
        "credentials" : { "connectionString" : "connection string" },
        "container" : { "name" : "table or view name" },
        "dataChangeDetectionPolicy" : {
           "@odata.type" : "#Microsoft.Azure.Search.HighWaterMarkChangeDetectionPolicy",
           "highWaterMarkColumnName" : "[a rowversion or last_updated column name]"
      }
    }

> [!WARNING]
> Merhaba kaynak tablosu hello yüksek su işareti sütunda dizin yoksa, hello SQL Oluşturucu tarafından kullanılan sorguları zaman aşımı olabilir. Özellikle, hello `ORDER BY [High Water Mark Column]` hello tablo satır sayısını içerdiğinde yan tümcesi bir dizin toorun verimli bir şekilde gerektirir..
>
>

Zaman aşımı hatalarla karşılaşırsanız, hello kullanabilirsiniz `queryTimeout` dizin oluşturucu yapılandırma ayarı tooset hello sorgu zaman aşımı tooa değerini hello varsayılan 5 dakikalık zaman aşımından daha yüksek. Örneğin, tooset hello zaman aşımı too10 dakika oluşturma veya yapılandırma aşağıdaki hello ile Merhaba dizin oluşturucusunu güncelleştirmek:

    {
      ... other indexer definition properties
     "parameters" : {
            "configuration" : { "queryTimeout" : "00:10:00" } }
    }

Merhaba da devre dışı bırakabilirsiniz `ORDER BY [High Water Mark Column]` yan tümcesi. Ancak, Hello dizin oluşturucusu yürütme bir hata nedeniyle kesintiye uğrarsa, daha sonra - çalıştırıyorsa hello dizin oluşturucu zaten neredeyse tüm hello satırları kesintiye uğradı hello tarafından işlendiği olsa bile hello dizin oluşturucu toore işlem tüm satırları içerdiğinden bu önerilmez. toodisable hello `ORDER BY` yan tümcesi, kullanım hello `disableOrderByHighWaterMarkColumn` hello dizin oluşturucu tanımında ayarı:  

    {
     ... other indexer definition properties
     "parameters" : {
            "configuration" : { "disableOrderByHighWaterMarkColumn" : true } }
    }

### <a name="soft-delete-column-deletion-detection-policy"></a>Yazılım silme sütun silme algılama İlkesi
Merhaba kaynak tablosundan silinen satır, satırları dizinden hello arama de büyük olasılıkla toodelete istersiniz. Kullanırsanız, değişiklik izleme ilkesinin hello SQL tümleşik, bunu sizin için dikkate. Ancak, hello yüksek su işareti değişiklik izleme ilkesinin silinen satırlarla yardımcı değil. Hangi toodo?

Merhaba satırları fiziksel olarak hello tablosundan kaldırılırsa, Azure Search artık mevcut kayıtları hiçbir şekilde tooinfer hello varlığını sahiptir.  Ancak, hello tablosundan kaldırmadan hello "soft-Sil" teknik toologically delete satırları kullanabilirsiniz. Sütun tooyour tablo veya görünüm ekleyin ve bu sütun kullanarak silinmiş olarak satırları işaretleyin.

Hello soft-delete teknik kullanırken, hello geçici silme ilkesi şu şekilde oluştururken veya güncelleştirirken hello veri kaynağı belirtebilirsiniz:

    {
        …,
        "dataDeletionDetectionPolicy" : {
           "@odata.type" : "#Microsoft.Azure.Search.SoftDeleteColumnDeletionDetectionPolicy",
           "softDeleteColumnName" : "[a column name]",
           "softDeleteMarkerValue" : "[hello value that indicates that a row is deleted]"
        }
    }

Merhaba **softDeleteMarkerValue** bir dize olması gerekir – gerçek değer hello dize gösterimini kullanın. Örneğin, burada silinen satır işaretlenir hello değeri 1 ile bir tamsayı sütunu varsa, kullanmak `"1"`. Burada silinen satır işaretlenir hello Boolean true değeri ile bir BIT sütun varsa, `"True"`.

<a name="TypeMapping"></a>

## <a name="mapping-between-sql-and-azure-search-data-types"></a>SQL ve Azure Search veri türleri arasında eşleme
| SQL veri türü | Hedef dizini izin alan türleri | Notlar |
| --- | --- | --- |
| bit |Edm.Boolean, Edm.String | |
| int, smallint, tinyint |EDM.Int32, EDM.Int64, Edm.String | |
| bigint |EDM.Int64, Edm.String | |
| Gerçek, kayan nokta |Edm.Double, Edm.String | |
| küçük para, para ondalık sayısal |Edm.String |Azure arama Bu duyarlık kaybeder çünkü Edm.Double ondalık türlerini dönüştürmeyi desteklemez |
| karakter, n karakter, değişken karakter, n değişken karakter |Edm.String<br/>Collection(Edm.String) |Hello dize bir JSON dizisini temsil ediyorsa, bir SQL dizesi kullanılan toopopulate Collection(Edm.String) alan olabilir:`["red", "white", "blue"]` |
| smalldatetime, datetime, datetime2, date, datetimeoffset |Edm.DateTimeOffset, Edm.String | |
| uniqueidentifer |Edm.String | |
| coğrafi konum |Edm.GeographyPoint |Yalnızca Coğrafya türünün örneklerini (Merhaba varsayılan değer olan) SRID 4326 NOKTASIYLA desteklenir |
| rowVersion |Yok |Satır sürümü sütunları hello arama dizinine depolanamaz ancak değişiklik izleme için kullanılabilir |
| zaman, timespan, ikili, değişken ikili, resim, xml, geometri, CLR Türleri |Yok |Desteklenmiyor |

## <a name="configuration-settings"></a>Yapılandırma ayarları
SQL dizin oluşturucu birkaç yapılandırma ayarlarını gösterir:

| Ayar | Veri türü | Amaç | Varsayılan değer |
| --- | --- | --- | --- |
| queryTimeout |Dize |SQL sorgusu yürütme için zaman aşımı ayarlar hello |5 dakika ("00: 05:00") |
| disableOrderByHighWaterMarkColumn |bool |Merhaba yüksek su işareti İlkesi tooomit hello ORDER BY yan tümcesi tarafından kullanılan hello SQL sorgusu neden olur. Bkz: [yüksek su işareti İlkesi](#HighWaterMarkPolicy) |False |

Bu ayarlar hello kullanılır `parameters.configuration` hello dizin oluşturucu tanımında nesne. Örneğin, tooset hello sorgu zaman aşımı too10 dakika, oluşturma veya yapılandırma aşağıdaki hello ile Merhaba dizin oluşturucusunu güncelleştirmek:

    {
      ... other indexer definition properties
     "parameters" : {
            "configuration" : { "queryTimeout" : "00:10:00" } }
    }

## <a name="faq"></a>SSS

**S: Azure SQL dizin oluşturucu Iaas VM'ler için Azure'da çalışan SQL veritabanları ile kullanabilirim?**

Evet. Ancak, arama hizmeti tooconnect tooyour veritabanınızı tooallow gerekir. Daha fazla bilgi için bkz: [Azure VM temelinde bir Azure Search dizin oluşturucu tooSQL Server öğesinden bir bağlantı yapılandırma](search-howto-connecting-azure-sql-iaas-to-azure-search-using-indexers.md).

**S: şirket içi çalışan SQL veritabanları ile Azure SQL dizin oluşturucu kullanabilir miyim?**

Doğrudan yönetilemez. Biz önermez ve bunu yapmak, bu nedenle, tooopen veritabanları tooInternet trafiğinizi gerektirecek şekilde doğrudan bir bağlantı desteklemez. Müşteriler, Azure Data Factory gibi köprüsü teknolojilerini kullanarak bu senaryo ile başarılı olduğunu. Daha fazla bilgi için bkz: [Azure Data Factory kullanarak anında iletme veri tooan Azure Search dizini](https://docs.microsoft.com/azure/data-factory/data-factory-azure-search-connector).

**S: Azure SQL dizin oluşturucu Iaas Azure üzerinde çalışan SQL Server dışındaki veritabanlarıyla kullanabilirim?**

Hayır. SQL Server dışındaki tüm veritabanları ile Merhaba dizinleyici test henüz çünkü bu senaryo, desteklemiyoruz.  

**S: bir zamanlamaya göre çalışan birden çok dizin oluşturucu oluşturma?**

Evet. Ancak, yalnızca bir dizin oluşturucu bir düğümde aynı anda çalışıyor olabilir. Eşzamanlı olarak çalışan birden çok dizin oluşturucu ihtiyacınız varsa, arama hizmeti toomore bir arama biriminden ölçeklendirme göz önünde bulundurun.

**S: bir dizin oluşturucu etkileyen my sorgu iş yükü çalıştıran mu?**

Evet. Dizin Oluşturucu arama hizmetinizde hello düğümlerin birinde çalışır ve bu düğümün kaynakları dizin oluşturma ve sorgu trafiğinin ve diğer API isteklerine hizmet veren arasında paylaşılır. Dizin oluşturma ve sorgu yoğun iş yükleri çalıştırın ve 503 hatalarıyla veya artan yanıt süreleri yüksek oranda karşılaşırsanız göz önünde bulundurun [arama hizmetinizi ölçeklendirme](search-capacity-planning.md).

**S: bir ikincil çoğaltma kullanabilirim bir [yük devretme kümesi](https://docs.microsoft.com/azure/sql-database/sql-database-geo-replication-overview) veri kaynağı olarak?**

Duruma göre değişir. Tam bir tablo veya görünüm için dizin, bir ikincil çoğaltma kullanabilirsiniz. 

Artımlı dizin oluşturma için Azure Search desteklediği iki algılama ilkeleri değiştirme: tümleşik SQL izleme ve yüksek su işareti değiştirin.

Salt okunur çoğaltmalar üzerinde tümleşik değişiklik izleme SQL veritabanı desteklemez. Bu nedenle, yüksek su işareti İlkesi kullanmanız gerekir. 

Standart Bizim önerimiz toouse hello rowversion veri türü hello yüksek su işareti sütun için tasarlanmıştır. Ancak, rowversion kullanarak SQL veritabanının üzerinde dayanır `MIN_ACTIVE_ROWVERSION` salt okunur çoğaltmaları desteklenmeyen işlev. Bu nedenle, rowversion kullanıyorsanız hello dizin oluşturucu tooa birincil çoğaltma işaret etmelidir.

Salt okunur bir çoğaltma toouse rowversion denerseniz, aşağıdaki hata hello görürsünüz: 

    "Using a rowversion column for change tracking is not supported on secondary (read-only) availability replicas. Please update hello datasource and specify a connection toohello primary availability replica.Current database 'Updateability' property is 'READ_ONLY'".

**S: yüksek su işareti değişiklik izleme için bir alternatif, rowversion olmayan sütun kullanabilir miyim?**

Bu önerilmez. Yalnızca **rowversion** için güvenilir veri eşitlenmesine izin verir. Ancak, uygulama mantığınızın bağlı olarak, güvenli olabilir varsa:

+ Merhaba dizin oluşturucu çalıştırıldığında, bekleyen işlem yoktur dizine hello tablosundaki emin olun (örneğin, tüm tablo güncelleştirmeleri toplu iş olarak bir zamanlamaya göre gerçekleşir ve hello Azure Search dizin oluşturucu zamanlaması hello tabloyla çakışan tooavoid ayarlayın güncelleştirme zamanlaması).  

+ Düzenli aralıklarla tam arat toopick kaçırılan herhangi bir satır yukarı yapabilirsiniz. 
