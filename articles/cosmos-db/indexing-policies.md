---
title: "aaaAzure Cosmos DB dizin oluşturma ilkeleri | Microsoft Docs"
description: "Dizin oluşturma Azure Cosmos DB'de nasıl çalıştığını anlayın. Otomatik dizin oluşturma ve performans için dizin oluşturma ilkesini tooconfigure ve değişiklik nasıl hello öğrenin."
keywords: "Dizin oluşturma, otomatik işleyişi dizin oluşturma, veritabanının dizin oluşturma"
services: cosmos-db
documentationcenter: 
author: arramac
manager: jhubbard
editor: monicar
ms.assetid: d5e8f338-605d-4dff-8a61-7505d5fc46d7
ms.service: cosmos-db
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 08/17/2017
ms.author: arramac
ms.openlocfilehash: 4f77b352b89382aa3352136038cb0e95c7588aac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-does-azure-cosmos-db-index-data"></a>Azure Cosmos DB dizin verileri nasıl yapar?

Varsayılan olarak, tüm Azure Cosmos DB veri dizin. Ve birçok müşteri toolet Azure Cosmos DB tüm yönlerini dizin otomatik olarak işleyecek mutluluk olsa da, özel bir belirtme Azure Cosmos DB de destekler **dizin oluşturma ilkesi** oluşturma sırasında koleksiyonlar için. Tasarlama ve şema esnekliği ödün vermeden hello dizin hello şeklini özelleştirme izin vermek için dizin oluşturma Azure Cosmos veritabanı daha esnek ve diğer veritabanı platformlar sunulan ikincil dizinler daha güçlü ilkelerdir. toolearn dizin Azure Cosmos DB'de anlamanız gerekir işleyişi dizin oluşturma ilkesini yöneterek dizin depolama yükü, yazma ve sorgu işleme ve sorgu tutarlılık arasında hassas bileşim hale getirebilir.  

Bu makalede, biz Kapat Azure Cosmos DB ilkeleri dizin göz atın, nasıl dizin oluşturma ilkesini özelleştirebilir ve hello dengelemeler ilişkilendirilmiş. 

Bu makaleyi okuduktan sonra aşağıdaki soruları mümkün tooanswer hello olması:

* Merhaba özellikleri tooinclude geçersiz kılma veya nasıl dizine almasını hariç?
* Merhaba dizini son güncelleştirmeler için nasıl yapılandırabilir miyim?
* Dizin oluşturma tooperform Order By veya aralık sorguları nasıl yapılandırabilir miyim?
* Dizin oluşturma ilkesi değişiklikleri tooa koleksiyonunun nasıl sağlarım?
* Nasıl t depolama ve performans farklı dizin ilkelerinin karşılaştırması nedir?

## <a id="CustomizingIndexingPolicy"></a>Bir koleksiyonun Hello dizin oluşturma ilkesini özelleştirme
Geliştiriciler hello dengelemeler depolama, yazma/sorgu performansını ve sorgu tutarlılık arasında hello varsayılan dizin oluşturma ilkesini Azure Cosmos DB koleksiyonunda geçersiz kılma ve yönlerini aşağıdaki hello yapılandırma özelleştirebilirsiniz.

* **Dahil olmak üzere/belgeler ve yolları/dizinden hariç**. Geliştiriciler hariç veya hello dizine ekleme veya toohello koleksiyonu değiştirme hello zamanında dahil belirli belgeleri toobe seçebilirsiniz. Geliştiriciler, ayrıca tooinclude seçin veya belirli JSON özellikleri paketini Dışla (joker karakter düzenleri dahil) yolları toobe bir dizinde bulunan belgeler arasında dizin.
* **Dizin türleri çeşitli yapılandırma**. Her dahil hello yolları için geliştiriciler ayrıca hello veri ve beklenen sorgu iş yükü ve hello sayısal/dize her yolu için "duyarlık" göre bir koleksiyon üzerinden gereksinim duydukları dizin türünü belirtebilirsiniz.
* **Dizin güncelleştirme modlarını yapılandırma**. Azure Cosmos DB hello İlkesi Azure Cosmos DB koleksiyonunda dizin aracılığıyla yapılandırılabilir üç dizin oluşturma modu destekler: tutarlı, Lazy ve yok. 

.NET kod parçacığında gösterildiği nasıl aşağıdaki hello tooset koleksiyonu hello oluşturulması sırasında özel bir dizin oluşturma ilkesi. Burada hello İlkesi dizeler ve sayılar için aralık dizinine sahip hello en yüksek duyarlık ayarlarız. Bu ilke bize Order By dizeleri sorgu yürütebilir sağlar.

    DocumentCollection collection = new DocumentCollection { Id = "myCollection" };

    collection.IndexingPolicy = new IndexingPolicy(new RangeIndex(DataType.String) { Precision = -1 });
    collection.IndexingPolicy.IndexingMode = IndexingMode.Consistent;

    await client.CreateDocumentCollectionAsync(UriFactory.CreateDatabaseUri("db"), collection);   


> [!NOTE]
> Merhaba JSON şeması dizin oluşturma ilkesi için REST API sürümü hello sürümüyle 2015-06-03 toosupport aralığı dizinleri dizelere değiştirildi. .NET SDK'sı 1.2.0 ve Java, Python ve Node.js SDK'ları 1.1.0 hello yeni ilke şeması destekler. Eski SDK'ları hello REST API sürümü 2015-04-08 kullanın ve dizin oluşturma ilkesi hello daha eski şema destekler.
> 
> Varsayılan olarak, Azure Cosmos DB aralık dizinine tüm dize özellikleri tutarlı bir karma dizinine sahip belgelerde ve sayısal özellikleri dizin oluşturur.  
> 
> 

### <a name="customizing-hello-indexing-policy-using-hello-portal"></a>Merhaba portal kullanarak hello dizin oluşturma ilkesi özelleştirme

Dizin oluşturma ilkesi hello Azure portal kullanarak bir koleksiyonun hello değiştirebilirsiniz. Açık hello Azure portal, Azure Cosmos DB hesabınızı seçin, koleksiyonunuzu hello sol gezinti menüsünde tıklatın **ayarları**ve ardından **dizin oluşturma ilkesi**. Merhaba, **dizin oluşturma ilkesi** dikey penceresinde, dizin oluşturma ilkenizi değiştirin ve ardından **Tamam** toosave değişikliklerinizi. 

### <a id="indexing-modes"></a>Veritabanı dizin oluşturma modları
Azure Cosmos DB, bir Azure Cosmos DB koleksiyonunda – ilke dizin hello aracılığıyla yapılandırılabilir üç dizin oluşturma modu CONSISTENT, Lazy ve hiçbiri destekler.

**Tutarlı**: bir Azure Cosmos DB koleksiyonunun İlkesi "olarak tutarlı" olarak belirlendiyse, verilen Azure Cosmos DB koleksiyonu izleme hello sorgulamaları için başlangıç noktası-okuma (yani güçlü, sınırlanmış eskime durumu, belirtildiği gibi aynı tutarlılık düzeyi hello oturum veya son). Merhaba dizini hello belge güncelleştirme (yani Ekle, Değiştir, güncelleştirme ve silme Azure Cosmos DB koleksiyonunda belgenin) bir parçası olarak eşzamanlı olarak güncelleştirilir.  Tutarlı dizin oluşturma olası azaltma hello maliyetle tutarlı sorguları yazma performansı destekler. Bu azaltma dizine toobe gereken hello benzersiz yolları işlevinin ve hello "tutarlılık düzeyi" dir. Tutarlı dizin oluşturma modu "hızlı bir şekilde, hemen sorgu yazma" iş yükleri için tasarlanmıştır.

**Yavaş**: tooallow en fazla belge alım verimlilik, bir Azure Cosmos DB koleksiyonu ile yavaş tutarlılık yapılandırılabilir; anlamı sorguları sonuçta tutarlı. bir Azure Cosmos DB koleksiyon yani Hello koleksiyonunun işleme kapasitesi tam olarak kullanılan tooserve kullanıcı isteklerini değilse gerçekleştirilmeye olduğunda hello dizini zaman uyumsuz olarak güncelleştirilir. "Yavaş" dizin oluşturma modu unhindered belge alım gerektiren "sorgu daha sonra şimdi alma" iş yükleri için uygun olabilir.

**Hiçbiri**: kendisiyle ilişkilendirilmiş herhangi bir dizin dizini modu "Hiçbiri" ile işaretlenmiş bir koleksiyonu vardır. Bu, Azure Cosmos DB anahtar-değer depolama alanı olarak kullanılan ve belgeleri yalnızca kimliği özelliği tarafından erişilen yaygın olarak kullanılır. 

> [!NOTE]
> Dizin oluşturma ilkesi "Hiçbiri" ile yapılandırma hello hello yan etkisi varolan bir dizini bırakmadan vardır. Erişim alışkanlıklarınıza yalnızca gereksinim duyuyorsanız "id" ve/veya "kendi bağlantı" bunu kullanın.
> 
> 

Örnek göster nasıl aşağıdaki hello tutarlı otomatik tüm belge eklemeleri üzerinde dizin ile Merhaba .NET SDK kullanarak bir Azure Cosmos DB koleksiyonu oluşturun.

Aşağıdaki tablonun hello hello tutarlılık hello sorgu isteği için belirtilen hello toplama ve hello tutarlılık düzeyi için yapılandırılmış hello dizin oluşturma modunu (CONSISTENT ve Lazy) temel alan sorgular için gösterir. Bu yapılan tooqueries herhangi arabirimi - REST API SDK'ları kullanarak uygular veya içinden yordamları ve Tetikleyicileri depolanır. 

|Tutarlılık|Dizin oluşturma modu: tutarlı|Dizin oluşturma modu: geç|
|---|---|---|
|Güçlü|Güçlü|Nihai|
|Sınırlanmış Eskime Durumu|Sınırlanmış Eskime Durumu|Nihai|
|Oturum|Oturum|Nihai|
|Nihai|Nihai|Nihai|

Azure Cosmos DB koleksiyonunda yok modu dizin ile yapılan sorgular için bir hata döndürür. Sorguları hala yürütülebilir taramaları aracılığıyla hello açık olarak `x-ms-documentdb-enable-scan` hello REST API veya hello başlığı `EnableScanInQuery` seçeneğini kullanarak, .NET SDK'sı hello isteği. ORDER BY gibi bazı sorgu özellikleri ile taramaları olarak desteklenmez `EnableScanInQuery`.

Merhaba aşağıdaki tabloda gösterilmektedir hello tutarlılık hello dizin oluşturma modunu (CONSISTENT Lazy ve hiçbiri) temel alan sorgular için EnableScanInQuery belirtildiğinde.

|Tutarlılık|Dizin oluşturma modu: tutarlı|Dizin oluşturma modu: geç|Dizin oluşturma modu: yok|
|---|---|---|---|
|Güçlü|Güçlü|Nihai|Güçlü|
|Sınırlanmış Eskime Durumu|Sınırlanmış Eskime Durumu|Nihai|Sınırlanmış Eskime Durumu|
|Oturum|Oturum|Nihai|Oturum|
|Nihai|Nihai|Nihai|Nihai|

kod örnek Göster nasıl aşağıdaki hello tutarlı tüm belge eklemeleri üzerinde dizin ile Merhaba .NET SDK kullanarak bir Azure Cosmos DB koleksiyonu oluşturun.

     // Default collection creates a hash index for all string fields and a range index for all numeric    
     // fields. Hash indexes are compact and offer efficient performance for equality queries.

     var collection = new DocumentCollection { Id ="defaultCollection" };

     collection.IndexingPolicy.IndexingMode = IndexingMode.Consistent;

     collection = await client.CreateDocumentCollectionAsync(UriFactory.CreateDatabaseUri("mydb"), collection);


### <a name="index-paths"></a>Dizin yolları
Azure Cosmos DB JSON belgeleri ve hello dizin ağaçları modeller ve hello ağaç içindeki yollar için tootune toopolicies sağlar. Belgeler içinde hangi yolların dahil veya dizine almasını hariç seçebilirsiniz. Merhaba sorgu desenlerine önceden bilindiğinde Bu geliştirilmiş yazma performansı ve senaryolar için alt dizini depolama sunabilir.

Dizin yolları hello kök (/) ile başlamalı ve genellikle hello ile bitmelidir? Merhaba öneki için birden fazla olası değerler olduğunu belirten joker işleci. Örneğin, tooserve SELECT * aileleri F NEREYE F.familyName = "Andersen" /familyName/ için bir dizin yolu içermelidir? Merhaba koleksiyonunun dizin ilkesinde.

Dizin yolları da hello kullanma * yolları özyinelemeli hello ön ek altındaki için joker karakter işleci toospecify hello davranışı. Örneğin, / yükü / * kullanılan tooexclude dizin gelen hello yükü özellik altında her şey olabilir.

Dizin yolları belirtmek için ortak desenler hello şunlardır:

| Yol                | Açıklama/kullanım örneği                                                                                                                                                                                                                                                                                         |
| ------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| /                   | Koleksiyon için varsayılan yolu. Özyinelemeli ve toowhole belge ağacı uygular.                                                                                                                                                                                                                                   |
| / prop /?             | Dizin yolu tooserve sorguları hello aşağıdaki gibi gerekli (karma veya aralık türleri sırasıyla):<br><br>SELECT FROM koleksiyonu c WHERE c.prop = "değeri"<br><br>SELECT FROM koleksiyonu c WHERE c.prop > 5<br><br>SELECT FROM koleksiyonu c ORDER BY c.prop                                                                       |
| / prop / *             | Merhaba belirtilen etiket altındaki tüm yolları için dizin yolu. Sorguları aşağıdaki hello ile çalışır<br><br>SELECT FROM koleksiyonu c WHERE c.prop = "değeri"<br><br>SELECT FROM koleksiyonu c WHERE c.prop.subprop > 5<br><br>SELECT FROM koleksiyonu c WHERE c.prop.subprop.nextprop = "değeri"<br><br>SELECT FROM koleksiyonu c ORDER BY c.prop         |
| / özellik / [] /?         | Dizin yolu tooserve yineleme ve skalerler ["a", "b", "c"] gibi bir dizi birleşim sorguları gerekir:<br><br>SEÇİN etiket etiket IN collection.props WHERE etiketi = "değeri"<br><br>Koleksiyon c birleştirme etiketi IN c.props SELECT etiketinden burada > 5 etiketi                                                                         |
| /props/ [] /subprop/? | Nesne dizileri birleşim sorguları gibi ve dizin yolu gerekli tooserve yineleme [{subprop: "a"}, {subprop: "b"}]:<br><br>SEÇİN etiket etiket IN collection.props WHERE tag.subprop = "değeri"<br><br>SEÇİN etiket koleksiyonu c birleştirme etiketi IN c.props WHERE tag.subprop = "değeri"                                  |
| / prop/subprop /?     | Dizin yolu gerekli tooserve sorgular (karma veya aralık türleri sırasıyla):<br><br>SELECT FROM koleksiyonu c WHERE c.prop.subprop = "değeri"<br><br>SELECT FROM koleksiyonu c WHERE c.prop.subprop > 5                                                                                                                    |

> [!NOTE]
> Özel dizin yolları ayarlanırken, gerekli toospecify hello varsayılan dizin oluşturma kuralı hello özel yol tarafından gösterilen hello tüm belgeyi ağacı için olan "/ *". 
> 
> 

Merhaba aşağıdaki örnek aralığı dizin ile belirli bir yol ve özel duyarlılık değeri 20 bayt yapılandırır:

    var collection = new DocumentCollection { Id = "rangeSinglePathCollection" };    

    collection.IndexingPolicy.IncludedPaths.Add(
        new IncludedPath { 
            Path = "/Title/?", 
            Indexes = new Collection<Index> { 
                new RangeIndex(DataType.String) { Precision = 20 } } 
            });

    // Default for everything else
    collection.IndexingPolicy.IncludedPaths.Add(
        new IncludedPath { 
            Path = "/*" ,
            Indexes = new Collection<Index> {
                new HashIndex(DataType.String) { Precision = 3 }, 
                new RangeIndex(DataType.Number) { Precision = -1 } 
            }
        });

    collection = await client.CreateDocumentCollectionAsync(UriFactory.CreateDatabaseUri("db"), pathRange);


### <a name="index-data-types-kinds-and-precisions"></a>Dizin veri türleri, tür ve Precision bilgisayarlar
Biz nasıl göz ayırdıktan göre toospecify yolları göz atalım kullanabileceğiniz hello seçenekleri tooconfigure hello yolu için dizin oluşturma ilkesi. Her yol için bir veya daha fazla dizin tanımları belirtebilirsiniz:

* Veri türü: **dize**, **numarası**, **noktası**, **Çokgen**, veya **LineString** (yalnızca bir giriş veri türü yolu başına başına içerebilir)
* Dizin türü: **karma** (eşitlik sorguları) **aralığı** (eşitlik, aralığı veya Order By sorguları) veya **Spatial** (uzamsal sorguları) 
* Duyarlık: karma dizini için bu dizeler ve varsayılan numaralarıyla için 1 too8 gelen 3 olarak değişir. Bu değer aralığı dizini için -1 (en yüksek duyarlık) olması ve dize veya sayı değerleri için 1-100 (en yüksek duyarlık) arasında farklılık gösterir.

#### <a name="index-kind"></a>Dizin türü
Azure Cosmos DB karma ve aralık dizini (dizeler, sayılar veya her ikisi için yapılandırılmış) her yol için destekler.

* **Karma** verimli eşitlik ve JOIN sorguları destekler. Çoğu kullanım durumları için karma dizinleri hello varsayılan değer olan 3 bayt daha yüksek duyarlık gerekmez. Veri türü dize veya sayı olabilir.
* **Aralık** verimli eşitlik sorguları, aralık sorguları destekler (kullanarak >, <>, =, < =,! =) ve Order By sorgular. Order By sorguları varsayılan olarak, ayrıca dizin üst sınırından duyarlık (-1) gerektirir. Veri türü dize veya sayı olabilir.

Azure Cosmos DB hello uzamsal dizin türü, başlangıç noktası, çokgen veya LineString veri türleri için belirtilebilir her yolu için de destekler. Merhaba belirtilen yolda Hello değeri gibi geçerli bir GeoJSON parçası olmalıdır `{"type": "Point", "coordinates": [0.0, 10.0]}`.

* **Uzamsal** destekler verimli uzamsal (içinde ve uzaklık) sorgular. Veri noktası, çokgen veya LineString olabilir.

> [!NOTE]
> Azure Cosmos DB noktaları, çokgenler ve MultiPoint otomatik dizin oluşturma destekler.
> 
> 

Desteklenen hello dizin türleri ve kullanılan tooserve olabilirler sorguları örnekleri şunlardır:

| Dizin türü | Açıklama/kullanım örneği                                                                                                                                                                                                                                                                                                                                                                                                              |
| ---------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Karma       | / Prop / karma? (veya /) olması kullanılan tooserve hello aşağıdaki sorguları verimli bir şekilde:<br><br>SELECT FROM koleksiyonu c WHERE c.prop = "değeri"<br><br>Karma/özellik / [] üzerinden /? (veya / veya/özellik /) olması kullanılan tooserve hello aşağıdaki sorguları verimli bir şekilde:<br><br>WHERE etiketi seçin etiket koleksiyonu c birleştirme etiketi IN c.props = 5                                                                                                                       |
| Aralık      | / Prop / aralığı? (veya /) olması kullanılan tooserve hello aşağıdaki sorguları verimli bir şekilde:<br><br>SELECT FROM koleksiyonu c WHERE c.prop = "değeri"<br><br>SELECT FROM koleksiyonu c WHERE c.prop > 5<br><br>SELECT FROM koleksiyonu c ORDER BY c.prop                                                                                                                                                                                                              |
| Uzamsal     | / Prop / aralığı? (veya /) olması kullanılan tooserve hello aşağıdaki sorguları verimli bir şekilde:<br><br>SELECT FROM koleksiyonu c<br><br>WHERE st_dıstance (c.prop, {"tür": "Noktası", "coordinates": [0.0, 10.0]}) < 40<br><br>Etkin noktalarında dizin ile SELECT FROM koleksiyonu c nerede ST_WITHIN(c.prop, {"type": "Polygon",...})--<br><br>Etkin çokgenler üzerinde dizin ile SELECT FROM koleksiyonu c nerede ST_WITHIN({"type": "Point",...}, c.prop)--              |

Sorgularla işleçleri gibi aralığı için varsayılan olarak, bir hata döndürülür > = Sipariş toosignal tarama gerekli tooserve hello sorgu olabilir hiçbir aralık dizini (tüm duyarlık) olduğunda. Aralık belirtilen sorguların hello x-ms-documentdb-enable-tarama üstbilgisinde hello REST API veya hello .NET SDK kullanarak hello EnableScanInQuery isteği seçeneği kullanılarak bir aralık dizin olmadan gerçekleştirilebilir. Azure Cosmos DB hello dizin toofilter karşı kullanabilirsiniz hello sorgu herhangi bir filtre varsa herhangi bir hata döndürülür.

Merhaba aynı kuralları uzamsal sorguları için geçerlidir. Varsayılan olarak, uzamsal dizin yok ve hello dizinden sunulabilecek hiçbir bir filtre uzamsal sorguları için bir hata döndürülür. X-ms-documentdb-enable-tarama/EnableScanInQuery kullanarak bir tarama gerçekleştirilebilir.

#### <a name="index-precision"></a>Dizin duyarlık
Dizin duyarlık dizin depolama ek yükü ve sorgu performansı karşılaştırmasını olanak sağlar. Numaraları için başlangıç varsayılan duyarlık yapılandırma-1 ("en") kullanmanızı öneririz. Sayı JSON 8 bayt olduğundan, bu eşdeğer tooa 8 bayt yapılandırmadır. Kesinlik, 1-7 gibi daha düşük bir değere çekme değerlerini bazı aralıklar harita toohello içinde aynı anlamına gelir giriş dizini. Bu nedenle dizin depolama alanı azaltır, ancak sorgu yürütme tooprocess sahip daha fazla belgeler ve sonuç olarak daha fazla verimlilik başka bir deyişle, tüketen birimleri isteyin.

Dizin duyarlık yapılandırma dizesi aralıklarıyla daha pratik uygulama vardır. Dizeleri herhangi bir rastgele uzunlukta olabileceği için hello dizin duyarlık hello seçimine dize aralığı sorgular ve etkisi hello gerekli dizin depolama alanı miktarını hello performansını etkileyebilir. Dize aralığı dizinleri, 1-100 veya -1 ("en") ile yapılandırılabilir. Dize özellikleri Order By tooperform sorguları isterseniz, -1 hello karşılık gelen yollar için kesinliğini belirtmeniz gerekir.

Uzamsal dizinler her zaman hello varsayılan dizin duyarlık tüm türleri için (noktaları, MultiPoint ve çokgenler) kullanın ve kılınmadı olamaz. 

Aşağıdaki örnek hello nasıl tooincrease hello duyarlık aralığının hello .NET SDK kullanarak bir koleksiyonda bulunan dizinler gösterir. 

**Özel dizin duyarlık ile bir koleksiyon oluşturma**

    var rangeDefault = new DocumentCollection { Id = "rangeCollection" };

    // Override hello default policy for Strings toorange indexing and "max" (-1) precision
    rangeDefault.IndexingPolicy = new IndexingPolicy(new RangeIndex(DataType.String) { Precision = -1 });

    await client.CreateDocumentCollectionAsync(UriFactory.CreateDatabaseUri("db"), rangeDefault);   


> [!NOTE]
> Bir sorgu Order By kullanır ancak hello sorgulanan hello en yüksek duyarlık yoluyla karşı aralık dizinine sahip değil, azure Cosmos DB bir hata döndürür. 
> 
> 

Benzer şekilde, yolları tamamen dizine almasını tutulabilir. Merhaba sonraki örnek nasıl tooexclude hello bölümünün tamamını (paketini belgeleri gösterir bir alt ağacı) hello kullanarak dizin gelen "*" joker karakter.

    var collection = new DocumentCollection { Id = "excludedPathCollection" };
    collection.IndexingPolicy.IncludedPaths.Add(new IncludedPath { Path = "/*" });
    collection.IndexingPolicy.ExcludedPaths.Add(new ExcludedPath { Path = "/nonIndexedContent/*" });

    collection = await client.CreateDocumentCollectionAsync(UriFactory.CreateDatabaseUri("db"), excluded);



## <a name="opting-in-and-opting-out-of-indexing"></a>Seçim ve dizin oluşturma dışında kullanmama
Tüm belgeler hello koleksiyon tooautomatically dizini istediğinizi seçebilirsiniz. Varsayılan olarak, tüm belgeler otomatik olarak dizine alınır, ancak tooturn seçebilirsiniz, devre dışı. Dizin oluşturma devre dışı bırakıldığında, belgeleri yalnızca aracılığıyla erişilebilen kendi kendine bağlantılar veya kullanarak sorgular tarafından kimliği

Otomatik kapalı ile dizin oluşturma, yalnızca belirli belgeleri toohello dizin hala seçmeli olarak ekleyebilirsiniz. Buna karşılık, üzerinde dizin otomatik bırakın ve seçmeli olarak yalnızca belirli belgeleri tooexclude'ı seçin. Açık/kapalı yapılandırmaları dizin yararlı sorgulanan toobe gereken belgeleri yalnızca bir kısmı sahip olduğunuzda.

Örneğin, hello aşağıdaki gösterir nasıl örnek açıkça hello kullanarak belgeyi tooinclude [DocumentDB API .NET SDK'sını](https://docs.microsoft.com/en-us/azure/cosmos-db/documentdb-sdk-dotnet) ve hello [RequestOptions.IndexingDirective](http://msdn.microsoft.com/library/microsoft.azure.documents.client.requestoptions.indexingdirective.aspx) özelliği.

    // If you want toooverride hello default collection behavior tooeither
    // exclude (or include) a Document from indexing,
    // use hello RequestOptions.IndexingDirective property.
    client.CreateDocumentAsync(UriFactory.CreateDocumentCollectionUri("db", "coll"),
        new { id = "AndersenFamily", isRegistered = true },
        new RequestOptions { IndexingDirective = IndexingDirective.Include });

## <a name="modifying-hello-indexing-policy-of-a-collection"></a>Bir koleksiyonun Hello dizin oluşturma ilkesini değiştirme
Azure Cosmos DB hello anında toomake değişiklikleri toohello dizin oluşturma ilkesini bir koleksiyonun sağlar. Dizin oluşturma ilkesi Azure Cosmos DB koleksiyonunda bir değişikliğin tooa değişiklik hello dizin yolları dizine Merhaba, kendi duyarlık yanı sıra hello tutarlılık modeli hello dizininin kendisi de dahil olmak üzere hello şeklinde yol açabilir. Böylece dizin oluşturma ilkesi değişikliği etkili bir şekilde gerektirir bir hello eski dizin dönüştürmesi içine yeni bir tane. 

**Çevrimiçi dizin dönüşümleri**

![Dizin oluşturma şeklini – Azure Cosmos DB çevrimiçi dizin dönüşümleri](./media/indexing-policies/index-transformations.png)

Dizin dönüşümleri hello eski ilke dizine hello belgeleri hello yeni ilke verimli bir şekilde dönüştürülmeden anlamı çevrimiçi yapılma **hello yazma kullanılabilirlik veya hello sağlanan işleme etkilemeden** , Merhaba koleksiyonu. Okuma tutarlılığı hello ve yazma işlemleri hello REST API SDK kullanılarak yapılan veya gelen saklı yordamları ve Tetikleyicileri içinde dizin dönüştürme sırasında etkilenmez. Bu, olduğunu hiçbir performans düşüşü veya kapalı kalma süresi tooyour uygulamaları değiştirme bir dizin oluşturma ilkesi yaptığınızda anlamına gelir.

Ancak, ilerleme dizin dönüşümü gerçekleşir hello süre boyunca sorguları sonunda modunu yapılandırma (CONSISTENT veya Lazy) dizin hello bağımsız olarak tutarlı değil. Bu ayrıca tüm arabirimlerinden – REST API SDK'ları, tooqueries uygular ve yordamları ve Tetikleyicileri içinden depolanır. Gibi dizin oluşturma, Lazy ile dizin dönüştürme zaman uyumsuz olarak hello yedek kaynaklar için belirli bir çoğaltma kullanarak hello çoğaltmalar üzerinde hello arka planda gerçekleştirilir. 

Dizin dönüşümleri ayrıca yapılan **situ** (yerinde), Azure Cosmos DB yani hello dizini ile takas hello eski dizin çıkışı hello yeni bir tane ile iki kopyasını tutmaz. Bu, hiçbir ek disk alanı gerekli veya dizin dönüşümleri gerçekleştirirken, koleksiyonlarda tüketilen anlamına gelir.

Dizin oluşturma ilkesini değiştirdiğinizde, nasıl hello bir bağımlı öncelikle hello diğer değerleri dahil ve Dışlanan yollar, dizin türleri ve Precision bilgisayarlar gibi şekilde modu yapılandırmaları daha dizin hello üzerinde hello eski dizin toohello yeni gelen uygulanan toomove değişir. Her iki eski ve yeni ilkelerinizi tutarlı dizin kullanırsanız, Azure Cosmos DB bir çevrimiçi dizin dönüşümü gerçekleştirir. Merhaba dönüştürme işlemi devam ederken, başka bir dizin oluşturma ilkesi değişikliği tutarlı dizin oluşturma modu ile uygulayamazsınız.

TooLazy veya hiçbiri dönüştürme sırasında dizin oluşturma modu devam ediyor ancak taşıyabilirsiniz. 

* TooLazy taşıdığınızda, hello dizin ilke hemen etkili değişiklik ve Azure Cosmos DB hello dizin zaman uyumsuz olarak yeniden başlatır. 
* TooNone taşıdığınızda, ardından hello dizin etkili hemen bırakılır. TooNone, toocancel etmekte istediğinizde kullanışlıdır taşıma dönüştürme ve farklı bir dizin oluşturma ilkesi temiz başlat. 

Merhaba .NET SDK'sı kullanıyorsanız, hello kullanarak yeni bir dizin oluşturma ilkesi değişikliği kazandırın **ReplaceDocumentCollectionAsync** hello dizin dönüşümünün hello kullanarak yöntemi ve izleme hello yüzdesi ilerlemesini  **IndexTransformationProgress** yanıt özelliğinden bir **ReadDocumentCollectionAsync** çağırın. Diğer SDK'ları ve hello REST API dizin oluşturma ilkesi değişiklikleri yapmak için eşdeğer özellikleri ve yöntemleri destekler.

Toomodify koleksiyonu tutarlı dizin oluşturma modu tooLazy ilkesinden nasıl dizin gösteren bir kod parçacığı aşağıda verilmiştir.

**Tutarlı tooLazy dizin oluşturma ilkesini değiştirme**

    // Switch toolazy indexing.
    Console.WriteLine("Changing from Default tooLazy IndexingMode.");

    collection.IndexingPolicy.IndexingMode = IndexingMode.Lazy;

    await client.ReplaceDocumentCollectionAsync(collection);


Aşağıda gösterildiği gibi bir dizin dönüştürme Örneğin, arama ReadDocumentCollectionAsync tarafından hello ilerlemesini kontrol edebilirsiniz.

**Dizin dönüştürme ilerlemesini izlemek**

    long smallWaitTimeMilliseconds = 1000;
    long progress = 0;

    while (progress < 100)
    {
        ResourceResponse<DocumentCollection> collectionReadResponse = await client.ReadDocumentCollectionAsync(
            UriFactory.CreateDocumentCollectionUri("db", "coll"));

        progress = collectionReadResponse.IndexTransformationProgress;

        await Task.Delay(TimeSpan.FromMilliseconds(smallWaitTimeMilliseconds));
    }

Bir koleksiyon için başlangıç dizini toohello hiçbiri modu dizin taşıyarak düşürebilir. Yeni bir tane hemen başlatmak ve toocancel bir sürüyor dönüşümü isterseniz bu yararlı bir işlemsel aracı olabilir.

**Bir koleksiyon için başlangıç dizinini kaldırma**

    // Switch toolazy indexing.
    Console.WriteLine("Dropping index by changing tootoohello None IndexingMode.");

    collection.IndexingPolicy.IndexingMode = IndexingMode.None;

    await client.ReplaceDocumentCollectionAsync(collection);

Dizin oluşturma ilkesi değişiklikleri tooyour Azure Cosmos DB koleksiyonları yaptığınızda? Merhaba, hello en yaygın kullanım örnekleri şunlardır:

* Normal işlem sırasında tutarlı sonuçlar sunar ancak geri dönüş toolazy toplu veri içeri aktarmaları sırasında dizin oluşturma
* Hangi hello uzamsal dizin türü gerektiren veya sıralama ölçütü sorgulama Jeo-uzamsal gibi geçerli Azure Cosmos DB koleksiyonlarınızı, örn., yeni dizin oluşturma özellikleri'ni kullanmaya başlamak / hello dize aralığı dizin türü gerektiren aralığı sorgu dizesi
* Elle seçin Dizinli Özellikler toobe hello ve zaman içinde değiştirme
* Dizin oluşturma duyarlık tooimprove sorgu performansı ayarlamak veya tüketilen depolama azaltın

> [!NOTE]
> Dizin oluşturma ilkesi toomodify ReplaceDocumentCollectionAsync kullanmadan, sürüm gerekir > merhaba .NET SDK'sı 1.3.0 =
> 
> Dizin dönüştürme toocomplete için başarılı bir şekilde, yeterli boş depolama alanı kullanılabilir olduğunu hello koleksiyonunda sağlamalısınız. Merhaba toplama, depolama kotasını ulaşırsa, başlangıç dizini dönüştürme duraklatılır. Dizin dönüştürme otomatik olarak devam edecek örneğin depolama alanı kullanılabilir sonra bazı belgeleri silerseniz.
> 
> 

## <a name="performance-tuning"></a>Performans ayarı
Merhaba DocumentDB API'leri hello dizin depolama kullanılan ve hello işleme (istek birimleri) her işlem için maliyet gibi performans ölçümleri hakkında bilgi sağlar. Bu bilgiler kullanılan toocompare çeşitli dizin oluşturma ilkeleri olabilir ve performans ayarlama.

toocheck hello depolama kotası ve kullanımı bir koleksiyonun HEAD veya GET isteği hello koleksiyon kaynağı karşı çalıştırın ve hello x-ms-istek-quota ve hello x-ms-istek kullanım üstbilgileri inceleyin. Hello .NET SDK'sı, hello [DocumentSizeQuota](http://msdn.microsoft.com/library/dn850325.aspx) ve [DocumentSizeUsage](http://msdn.microsoft.com/library/azure/dn850324.aspx) özelliklerinde [ResourceResponse < T\> ](http://msdn.microsoft.com/library/dn799209.aspx) bu karşılık gelen değerleri içeren .

     // Measure hello document size usage (which includes hello index size) against   
     // different policies.
     ResourceResponse<DocumentCollection> collectionInfo = await client.ReadDocumentCollectionAsync(UriFactory.CreateDocumentCollectionUri("db", "coll"));  
     Console.WriteLine("Document size quota: {0}, usage: {1}", collectionInfo.DocumentQuota, collectionInfo.DocumentUsage);


Her yazma işlemi dizin toomeasure hello yükünü (oluşturma, güncelleştirme veya silme) hello x-ms-istek-ücret üstbilgi inceleyin (veya eşdeğer hello [RequestCharge](http://msdn.microsoft.com/library/dn799099.aspx) özelliğinde [ResourceResponse < T\> ](http://msdn.microsoft.com/library/dn799209.aspx) hello .NET SDK içinde) toomeasure hello bu işlemler tarafından tüketilen istek birimlerinin sayısı.

     // Measure hello performance (request units) of writes.     
     ResourceResponse<Document> response = await client.CreateDocumentAsync(UriFactory.CreateDocumentCollectionUri("db", "coll"), myDocument);              
     Console.WriteLine("Insert of document consumed {0} request units", response.RequestCharge);

     // Measure hello performance (request units) of queries.    
     IDocumentQuery<dynamic> queryable =  client.CreateDocumentQuery(UriFactory.CreateDocumentCollectionUri("db", "coll"), queryString).AsDocumentQuery();

     double totalRequestCharge = 0;
     while (queryable.HasMoreResults)
     {
        FeedResponse<dynamic> queryResponse = await queryable.ExecuteNextAsync<dynamic>(); 
        Console.WriteLine("Query batch consumed {0} request units",queryResponse.RequestCharge);
        totalRequestCharge += queryResponse.RequestCharge;
     }

     Console.WriteLine("Query consumed {0} request units in total", totalRequestCharge);

## <a name="changes-toohello-indexing-policy-specification"></a>Değişiklikleri toohello İlkesi belirtimi dizin oluşturma
Dizin oluşturma ilkesi için hello şema değişikliği 7 Temmuz 2015 REST API sürümü 2015-06-03 ile kullanılmaya başlanmıştır. Merhaba ilgili sınıfları hello SDK sürümlerinde yeni uygulamaları toomatch hello şeması sahiptir. 

aşağıdaki değişiklikler hello hello JSON belirtimi uygulanan:

* Dizin oluşturma ilkesi aralığı dizinler için dizeleri destekler
* Her yol birden çok dizin tanımları, her bir veri türü için bir tane olabilir
* Duyarlık dizin 1-8 numaraları, 1-100 dizeleri ve -1 (en yüksek duyarlık) destekler
* Yol kesimleri her yol bir çift tırnak tooescape gerektirmez. Örneğin, / başlık/için bir yol ekleyebilir miyim? yerine / "title" /?
* "tüm yolları" temsil eden hello kök yolu temsil olarak / * (Ayrıca çok /)

.NET SDK sürümüyle 1.1.0 yazılmış özel bir dizin oluşturma ilkesi ile koleksiyonları sağlar kodunuz varsa hello veya daha eski, toochange gerekir uygulamanız bu değişiklikleri sipariş toomove tooSDK sürümünde 1.2.0 toohandle kod. Değil dizin oluşturma ilkesini yapılandırır koduna sahip veya eski bir SDK sürümüyle toocontinue planlama, değişiklik gerekmez.

Pratik karşılaştırması için önceki sürüm 2015-04-08 hello yanı sıra bir örnek kullanılarak yazılmış özel bir dizin oluşturma ilkesini hello REST API sürümü 2015-06-03 aşağıda verilmiştir.

**JSON önceki dizin oluşturma ilkesi**

    {
       "automatic":true,
       "indexingMode":"Consistent",
       "IncludedPaths":[
          {
             "IndexType":"Hash",
             "Path":"/",
             "NumericPrecision":7,
             "StringPrecision":3
          }
       ],
       "ExcludedPaths":[
          "/\"nonIndexedContent\"/*"
       ]
    }

**Geçerli dizin oluşturma ilkesi JSON**

    {
       "automatic":true,
       "indexingMode":"Consistent",
       "includedPaths":[
          {
             "path":"/*",
             "indexes":[
                {
                   "kind":"Hash",
                   "dataType":"String",
                   "precision":3
                },
                {
                   "kind":"Hash",
                   "dataType":"Number",
                   "precision":7
                }
             ]
          }
       ],
       "ExcludedPaths":[
          {
             "path":"/nonIndexedContent/*"
          }
       ]
    }

## <a name="next-steps"></a>Sonraki Adımlar
Hello dizin ilke yönetimi örnekleri ve toolearn Azure Cosmos veritabanı sorgu dili hakkında daha fazla bilgi için aşağıdaki bağlantıları izleyin.

1. [DocumentDB API .NET dizin yönetimi kod örnekleri](https://github.com/Azure/azure-documentdb-net/blob/master/samples/code-samples/IndexManagement/Program.cs)
2. [DocumentDB API REST toplama işlemleri](https://msdn.microsoft.com/library/azure/dn782195.aspx)
3. [SQL sorgusu](documentdb-sql-query.md)

