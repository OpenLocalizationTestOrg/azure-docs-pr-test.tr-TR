---
title: "aaaAzure Cosmos DB kaynak modeli ve kavramları | Microsoft Docs"
description: "Azure Cosmos veritabanı hiyerarşik modelinin veritabanları, koleksiyonları, kullanıcı tanımlı işlev (UDF), belgeler, izinleri toomanage kaynakları ve daha fazla hakkında bilgi edinin."
keywords: "Hiyerarşik modeli, cosmosdb, azure, Microsoft azure"
services: cosmos-db
documentationcenter: 
author: AndrewHoh
manager: jhubbard
editor: monicar
ms.assetid: ef9d5c0c-0867-4317-bb1b-98e219799fd5
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/24/2017
ms.author: anhoh
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: fc3642232b86cc27901ebd97456c386829324632
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-hierarchical-resource-model-and-core-concepts"></a>Azure Cosmos DB hiyerarşik kaynak modeli ve temel kavramları
Hello Azure Cosmos DB yöneten veritabanı başvurulan tooas varlıklardır **kaynakları**. Her kaynak mantıksal URI'leri ile benzersiz olarak tanımlanır. Standart HTTP fiillerini, istek/yanıt üstbilgilerini ve durum kodlarını kullanarak hello kaynakları ile etkileşim kurabilirsiniz. 

Bu makalede okuyarak sorular aşağıdaki mümkün tooanswer hello olması:

* Cosmos veritabanı kaynak modeli nedir?
* Sistem nelerdir kaynakları tanımlanan karşılıklı toouser kaynaklar olarak tanımlanan?
* Bir kaynak nasıl ele?
* Koleksiyonları ile nasıl çalışır?
* Saklı yordamlar, tetikleyiciler ve kullanıcı tanımlı işlevler (UDF'ler) ile nasıl çalışırım?

## <a name="hierarchical-resource-model"></a>Hiyerarşik kaynak modeli
Cosmos DB hiyerarşik Hello Aşağıdaki diyagramda gösterildiği gibi hello **kaynak modeli** kaynaklar mantıksal ve kararlı bir URI her adreslenebilir bir veritabanı hesabı altında kümesi oluşur. Bir kaynak kümesi başvurulan tooas olacak bir **akış** bu makalede. 

> [!NOTE]
> Azure Cosmos DB sunar RESTful kendi iletişimi modelinde, hello kullanılabilir olan son derece verimli bir TCP Protokolü [DocumentDB .NET istemcisi API](documentdb-sdk-dotnet.md).
> 
> 

![Azure Cosmos DB hiyerarşik kaynak modeli][1]  
**Hiyerarşik kaynak modeli**   

kaynakları ile çalışma toostart gerekir [bir veritabanı hesabı oluşturma](create-documentdb-dotnet.md) Azure aboneliğinizi kullanarak. Veritabanı hesabı bir dizi oluşabilir **veritabanları**, her biri birden çok içeren **koleksiyonları**, her sırayla içerir, **saklı yordamlar, Tetikleyiciler, UDF'ler, belgeler**ve ilgili **ekleri**. Bir veritabanı da ilişkili **kullanıcılar**, her bir dizi **izinleri** tooaccess koleksiyonlar, depolanan yordamlar, Tetikleyiciler, UDF'ler, belgeler veya ekler. Veritabanları, kullanıcılar, izinler ve Koleksiyonlar iyi bilinen şemalar sahip sistem tanımlı kaynakları olsa da, belgeler ve ekleri rasgele içerir, kullanıcı tanımlı JSON içeriği bulunur.  

| Kaynak | Açıklama |
| --- | --- |
| Veritabanı hesabı |Veritabanı hesabı, bir dizi veritabanları ve ekleri için blob storage'nın sabit bir tutar ile ilişkilidir. Azure aboneliğinizi kullanarak bir veya daha fazla veritabanı hesabı oluşturabilirsiniz. Daha fazla bilgi için bizim [fiyatlandırma sayfası](https://azure.microsoft.com/pricing/details/cosmos-db/). |
| Database |Bir veritabanı, koleksiyonlar genelinde bölümlenmiş belge depolama alanının mantıksal bir kapsayıcısıdır. Ayrıca, Kullanıcılar kapsayıcısı unutulmamalıdır. |
| Kullanıcı |izinlerin kapsamını belirlerken için hello mantıksal ad alanı. |
| İzin |Bir kullanıcı için erişim tooa belirli kaynak ile ilişkili bir yetki belirteci. |
| Koleksiyon |Bir kapsayıcı JSON belgelerinin koleksiyonudur ve JavaScript uygulama mantığının hello ilişkili. Faturalanabilir bir varlık hello burada koleksiyonudur [maliyet](performance-levels.md) hello koleksiyonla ilişkilendirilen hello performans düzeyine göre belirlenir. Koleksiyonlar bir veya daha fazla bölümü/sunucuyu kapsayabilir ve toohandle ölçeklendirebilirsiniz neredeyse sınırsız miktarda depolama veya işlemeyi. |
| Saklı Yordam |Uygulama mantığı ile bir koleksiyon kayıtlı ve işlemsel olarak hello veritabanı altyapısı içinde yürütülen JavaScript'te yazılmış. |
| Tetikleyici |Önce veya sonra ya da bir ekleme yürütülen JavaScript'te yazılmış uygulama mantığını değiştirin ya da silme işlemi. |
| UDF |JavaScript'te yazılmış bir uygulama mantığı. UDF'ler özel sorgu işleci toomodel etkinleştirin ve böylelikle hello çekirdek DocumentDB API sorgu dili genişletir. |
| Belge |Kullanıcı tanımlı (rastgele) JSON içeriği bulunur. Varsayılan olarak, hiçbir şema tanımlanan toobe gerekir veya tüm Merhaba belgeleri tooa koleksiyonu eklenen sağlanan ikincil dizinlerin toobe gerek. |
| Eki |Ek başvurular ve dış blob/medya için ilişkili meta verileri içeren özel bir belgedir. Merhaba Geliştirici Cosmos DB tarafından yönetilen toohave hello blob seçin veya OneDrive, Dropbox, vb. gibi bir dış blob hizmeti sağlayıcısında saklayabilirsiniz. |

## <a name="system-vs-user-defined-resources"></a>Sistem kullanıcı tanımlı kaynakları karşılaştırması
Veritabanı hesaplarını, veritabanları, koleksiyonları, kullanıcılar, izinler, saklı yordamlar, tetikleyiciler ve UDF'ler - gibi kaynakları tüm sabit şemasına sahip ve sistem kaynaklarını denir. Buna karşılık, belgeler ve ekler gibi kaynakları herhangi bir kısıtlama hello şemasına sahip ve kullanıcı tanımlı kaynaklar olarak gösterilebilir. Cosmos içinde DB, sistem ve kullanıcı tanımlı kaynakları temsil ve standart uyumlu JSON olarak yönetilir. Tüm kaynaklar, sistem veya kullanıcı tanımlı, hello aşağıdaki ortak özelliklere sahiptir.

> [!NOTE]
> Tüm sistem kaynak özellikleri oluşturulan Not önekiyle kendi JSON gösterimi, alt çizgi (_).
> 
> 

<table>
    <tbody>
        <tr>
            <td valign="top"><p><strong>Özellik</strong></p></td>
            <td valign="top"><p><strong>Kullanıcı tarafından ayarlanabilir veya sistem tarafından oluşturulan?</strong></p></td>
            <td valign="top"><p><strong>Amacı</strong></p></td>
        </tr>
        <tr>
            <td valign="top"><p>_rid</p></td>
            <td valign="top"><p>Sistem tarafından oluşturulan</p></td>
            <td valign="top"><p>Sistem oluşturulan, benzersiz ve hiyerarşik hello kaynak tanıtıcısı</p></td>
        </tr>
        <tr>
            <td valign="top"><p>_etag</p></td>
            <td valign="top"><p>Sistem tarafından oluşturulan</p></td>
            <td valign="top"><p>İyimser eşzamanlılık denetimi için gerekli hello kaynağının ETag</p></td>
        </tr>
        <tr>
            <td valign="top"><p>_ts</p></td>
            <td valign="top"><p>Sistem tarafından oluşturulan</p></td>
            <td valign="top"><p>Merhaba kaynağının en son güncelleştirilen zaman damgası</p></td>
        </tr>
        <tr>
            <td valign="top"><p>_self</p></td>
            <td valign="top"><p>Sistem tarafından oluşturulan</p></td>
            <td valign="top"><p>Merhaba kaynağının benzersiz adreslenebilir URI</p></td>
        </tr>
        <tr>
            <td valign="top"><p>id</p></td>
            <td valign="top"><p>Sistem tarafından oluşturulan</p></td>
            <td valign="top"><p>Kullanıcı tanımlı hello kaynağının benzersiz bir ad (Merhaba ile aynı, anahtar değeri'bölüm). Merhaba kullanıcı kimliği belirtmiyorsa, sistem tarafından oluşturulan bir kimlik olacaktır</p></td>
        </tr>
    </tbody>
</table>

### <a name="wire-representation-of-resources"></a>Hat gösterimine kaynakların
Cosmos DB herhangi özel uzantıları toohello JSON standart veya özel Kodlamalar zorunlu kılabilir değil; Standart uyumlu JSON belgeleri ile çalışır.  

### <a name="addressing-a-resource"></a>Bir kaynak adresleme
URI adreslenebilir tüm kaynaklardır. Merhaba hello değerini **_self** özelliği bir kaynağı temsil hello kaynağının göreli URI hello. Merhaba hello URI biçimi oluşur hello /\<akış\>/ {_rid} yol kesimleri:  

| Merhaba _self değeri | Açıklama |
| --- | --- |
| /dbs |Bir veritabanı hesabı altında veritabanlarının besleme |
| /dbs/ {dbName} |{DbName} hello değerle eşleşen bir kimliğe sahip veritabanı |
| /dbs/ {dbName} /colls/ |Bir veritabanı altında koleksiyonların besleme |
| /dbs/ {dbName} /colls/ {collName} |{CollName} hello değerle eşleşen bir kimliğe sahip koleksiyonu |
| /dbs/ {dbName} /colls/ {collName} / docs |Bir koleksiyon altında belgelerin besleme |
| /dbs/ {dbName} /colls/ {collName} /docs/ {docId} |{Doc} Hello değerle eşleşen bir kimliğiyle belge |
| /dbs/ {dbName} /users/ |Kullanıcıların bir veritabanı altında besleme |
| /dbs/ {dbName} /users/ {UserID} |{Kullanıcısı} hello değerle eşleşen bir kimliğe sahip kullanıcı |
| /dbs/ {dbName} /users/ {UserID} / izinleri |Akış kapsamındaki bir kullanıcı izinleri |
| /dbs/ {dbName} /users/ {UserID} /permissions/ {permissionId} |{İzni} hello değerle eşleşen bir kimliğe sahip izni |

Her kaynak hello kimliği özelliği aracılığıyla kullanıma sunulan bir benzersiz kullanıcı tanımlı adı vardır. Not: hello kullanıcı kimliği, belirlemezse belgeler için bizim desteklenen SDK'ları otomatik olarak hello belge için benzersiz bir kimliği oluşturur. Merhaba, bir kullanıcı tanımlı dizesi, belirli üst kaynak hello bağlamı içinde benzersizdir too256 karakterleri yukarı kimliğidir. 

Her kaynak hello _rid özelliği aracılığıyla kullanılabilir olduğu bir sistem tarafından oluşturulan hiyerarşik kaynak tanımlayıcısı (Ayrıca başvurulan tooas bir RID), ayrıca vardır. Merhaba tüm belirli bir kaynak hiyerarşisini başlangıç RID kodlar ve bu kullanışlı bir iç gösterimi tooenforce başvuru bütünlüğü dağıtılmış bir şekilde kullanılır. Hello RID bir veritabanı hesabı içinde benzersizdir ve çapraz bölüm aramaları gerek kalmadan verimli yönlendirme için Cosmos DB tarafından dahili olarak kullanılır. Merhaba hello _self ve hello _rid özelliklerinin bir kaynak alternatif ve kurallı gösterimlerini değerlerdir. 

Merhaba kimliği ve hello _rid özellikleri tarafından isteklerinin kaynakları adreslenmesini ve hello REST API desteği.

## <a name="database-accounts"></a>Veritabanı hesapları
Azure aboneliğinizi kullanarak bir veya daha fazla Cosmos DB veritabanı hesaplarını sağlayabilirsiniz.

Oluşturun ve Cosmos DB veritabanı hesaplarını hello Azure Portal aracılığıyla yönetin adresindeki [http://portal.azure.com/](https://portal.azure.com/). Oluşturma ve bir veritabanı hesabı yönetme yönetimsel erişim gerektirir ve yalnızca Azure aboneliğinizde gerçekleştirilebilir. 

### <a name="database-account-properties"></a>Veritabanı hesabı özellikleri
Hazırlama ve bir veritabanı hesabı yönetme bir parçası olarak yapılandırın ve aşağıdaki özelliklere hello okuyun:  

<table border="0" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td valign="top"><p><strong>Özellik adı</strong></p></td>
            <td valign="top"><p><strong>Açıklama</strong></p></td>
        </tr>
        <tr>
            <td valign="top"><p>Tutarlılık İlkesi</p></td>
            <td valign="top"><p>Veritabanı hesabınız altındaki tüm hello koleksiyonlar için bu özelliği tooconfigure hello varsayılan tutarlılık düzeyini ayarlayın. Merhaba [x-ms-tutarlılık-düzey] istek üstbilgisi kullanarak bir istek başına hello tutarlılık düzeyinde geçersiz kılabilirsiniz. <p><p>Bu özellik yalnızca toohello geçerlidir Not <i>kullanıcı tanımlı kaynakları</i>. Tüm sistem tarafından tanımlanan yapılandırılmış toosupport okuma/sorguları güçlü tutarlılık kaynaklardır.</p></td>
        </tr>
        <tr>
            <td valign="top"><p>Yetkilendirme anahtarları</p></td>
            <td valign="top"><p>Merhaba birincil bunlar ve tooall hello veritabanı hesabı altında hello kaynakların erişim yönetim sağlayan ikincil ana ve salt okunur anahtarları.</p></td>
        </tr>
    </tbody>
</table>

Yapılandırma ve Azure Portal hello veritabanı hesabınızı yönetme ek tooprovisioning içinde program aracılığıyla da oluşturabilir ve hello kullanarak Cosmos DB veritabanı hesaplarını yönetme, Not [Azure Cosmos DB REST API'lerini](/rest/api/documentdb/) olarak hem de [istemci SDK'ları](documentdb-sdk-dotnet.md).  

## <a name="databases"></a>Veritabanları
Cosmos DB veritabanı bir mantıksal bir veya daha fazla koleksiyonlarını ve kullanıcılar, hello Aşağıdaki diyagramda gösterildiği gibi kapsayıcıdır. Cosmos DB veritabanı hesabı konu toooffer altındaki veritabanları herhangi bir sayıda sınırları oluşturabilirsiniz.  

![Veritabanı hesabı ve koleksiyonları hiyerarşik modeli][2]  
**Bir veritabanı kullanıcıları ve koleksiyonlar, mantıksal bir kapsayıcısıdır**

Bir veritabanı içinde koleksiyonlar bölümlenmiş neredeyse sınırsız belge depolama içerebilir.

### <a name="elastic-scale-of-a-cosmos-db-database"></a>Cosmos DB veritabanının esnek ölçeklendirme
Varsayılan olarak birkaç GB toopetabytes yedeklenen SSD belge depolama ve sağlanan işleme arasında değişen – esnek bir Cosmos DB veritabanıdır. 

Bir veritabanında geleneksel RDBMS Cosmos DB veritabanında kapsamlı tooa tek makine değil. Cosmos DB ile toogrow, uygulamanızın ölçek gereksinimleriniz değiştikçe koleksiyonlar, veritabanları veya her ikisi de oluşturabilirsiniz. Aslında, Microsoft içindeki çeşitli birinci taraf uygulamalardan Cosmos DB Tüketici ölçekte son derece büyük Cosmos DB veritabanları koleksiyonları içeren her binlerce belge depolama terabayt ile oluşturarak kullanmakta olduğunuz. Büyütür veya bir veritabanı ekleyerek veya uygulamanızın ölçek gereksinimlerine koleksiyonları toomeet kaldırarak küçültür. 

Herhangi bir sayıda veritabanı konu toohello teklif içinde koleksiyonlar oluşturabilirsiniz. Her koleksiyon yedeklenen SSD depolama ve işleme hello seçilen performans katmanına bağlı olarak sağladığınız vardır.

Cosmos DB veritabanı kullanıcı aynı zamanda bir kapsayıcıdır. Bir kullanıcı, Aç, hassas yetkilendirme ve erişim toocollections, belgeler ve ekleri sağlayan bir izin kümesi için bir mantıksal ad alanıdır.  

Merhaba Cosmos DB kaynak modeli diğer kaynaklar ile veritabanları oluşturulabilir olarak değiştirildi, silinmiş, okuma veya kolayca ya da hello kullanarak numaralandırılan [REST API'leri](/rest/api/documentdb/) veya hello [istemci SDK'ları](documentdb-sdk-dotnet.md). Cosmos DB okuma veya bir veritabanı kaynak hello meta verileri sorgulamak için güçlü tutarlılığı garanti altına alır. Veritabanını otomatik olarak silme hello koleksiyonları veya içerdiği kullanıcılar hiçbirine erişemiyor sağlar.   

## <a name="collections"></a>Koleksiyonlar
Cosmos DB koleksiyon, JSON belgeleri için bir kapsayıcıdır. 

### <a name="elastic-ssd-backed-document-storage"></a>Esnek yedeklenen SSD belge depolama
Bir koleksiyon doğası gereği esnek - otomatik olarak büyüdükçe ve belgeleri ekleyip olarak küçülür. Koleksiyonlar mantıksal kaynaklar ve bir veya daha fazla fiziksel bölümleri veya sunucuları yayılabilir. bir koleksiyon içinde bölüm Hello sayısı Cosmos hello depolama boyutu ve, koleksiyonun hello sağlanan işleme dayalı DB tarafından belirlenir. Cosmos DB her bölümün SSD yedekli depolama ilişkili sabit bir tutar sahiptir ve yüksek kullanılabilirlik için çoğaltılır. Bölüm yönetimi tam olarak Azure Cosmos DB tarafından yönetilen ve değil toowrite karmaşık koda sahip veya, bölümlerini yönetin. Cosmos DB koleksiyonlarıdır **neredeyse sınırsız** depolama ve işleme açısından. 

### <a name="automatic-indexing-of-collections"></a>Koleksiyonları otomatik dizin oluşturma
Cosmos DB true şemasız veritabanı sistemidir. Varsaymaz veya hello JSON belgeleri için herhangi bir şema gerektirir. Belgeleri tooa koleksiyonu ekledikçe Cosmos DB bunları otomatik olarak dizinler ve tooquery için kullanılabilir. Otomatik belgelerin dizin şemasını ya da ikincil dizinlerin gerek kalmadan Cosmos DB'nin anahtar bir özelliktir ve yazma iyileştirilmiş, kilidi serbest ve günlük yapılı dizin bakım teknikleri tarafından etkinleştirilir. Cosmos DB hala tutarlı sorguları hizmet veren sırasında son derece hızlı yazmalar sürekli hacmi destekler. Belge ve dizin depolama olan her koleksiyon tarafından tüketilen toocalculate hello depolama kullanılır. Merhaba depolama ve performans hello bir koleksiyon için dizin oluşturma ilkesini yapılandırarak dizin ile ilişkili dengelemeler kontrol edebilirsiniz. 

### <a name="configuring-hello-indexing-policy-of-a-collection"></a>Bir koleksiyonun Hello dizin oluşturma ilkesini yapılandırma
Dizin oluşturma ilkesi her koleksiyonun hello toomake performans ve depolama dizin ile ilişkili dengelemeler sağlar. Merhaba aşağıdaki seçenekler kullanılabilir tooyou dizin yapılandırmasının bir parçası olarak şunlardır:  

* Merhaba koleksiyonu otomatik olarak tüm hello belgelerin veya dizinleri olup olmadığını seçin. Varsayılan olarak, tüm belgeler otomatik olarak dizine alınır. Otomatik dizin oluşturma devre dışı tooturn seçin ve yalnızca belirli belgeleri toohello dizinini seçmeli olarak ekleyin. Buna karşılık, yalnızca belirli belgeleri tooexclude seçmeli olarak seçebilirsiniz. Bir koleksiyon hello indexingPolicy üzerinde hello otomatik özelliği toobe true veya false ayarlama ve hello [x-ms-indexingdirective] istek üstbilgisi ekleme, değiştirme veya bir belgeyi silme sırasında kullanarak gerçekleştirebilirsiniz.  
* Tooinclude veya hariç tutma belirli yollar veya belgelerinizi düzenleri dizin hello olup olmadığını seçin. Bu ayar includedPaths ve bir koleksiyonun hello indexingPolicy üzerinde excludedPaths sırasıyla elde edebilirsiniz. Ayrıca, hello depolama ve performans dengelemeler aralığı için yapılandırma ve sorguları belirli yolu desenler için karma. 
* Zaman uyumlu arasında (tutarlı) seçin ve zaman uyumsuz (yavaş) dizin güncelleştirmeleri. Varsayılan olarak, her ekleme, değiştirme veya belge toohello koleksiyonu silme işlemi hello dizini zaman uyumlu olarak güncelleştirilir. Bu hello sorgularını sağlayan toohonor hello hello belge okuma olarak aynı tutarlılık düzeyi. Cosmos DB yazma en iyi duruma getirilmiş ve zaman uyumlu dizin Bakım ve tutarlı sorguları hizmet veren birlikte belge yazma sürekli birimleri destekler, ancak belirli koleksiyonlar tooupdate kendi dizini gevşek yapılandırabilirsiniz. Yavaş dizin daha fazla hello yazma performansı artırır ve toplu alım senaryoları öncelikle okuma ağır koleksiyonları için idealdir.

Dizin oluşturma ilkesi hello hello koleksiyonunda PUT yürüterek değiştirilebilir. Bu olabilir ya da hello aracılığıyla elde [istemci SDK](documentdb-sdk-dotnet.md), hello [Azure Portal](https://portal.azure.com) veya hello [REST API'leri](/rest/api/documentdb/).

### <a name="querying-a-collection"></a>Bir koleksiyonu sorgulama
bir koleksiyon içinde Hello belgeleri rasgele şemalar sahip olabilir ve herhangi bir şemayı ya da ikincil dizinlerin önceden sağlamadan bir koleksiyon içinde belgeleri sorgulayabilirsiniz. Merhaba koleksiyonu hello kullanarak sorgulama yapabilirsiniz [Azure Cosmos DB DocumentDB API'si: SQL söz dizimi başvurusu](https://msdn.microsoft.com/library/azure/dn782250.aspx), zengin hiyerarşik, ilişkisel ve uzamsal işleçler ve genişletilebilirlik UDF'ler JavaScript tabanlı aracılığıyla sağlar. JSON dil bilgisi hello ağaç düğümleri olarak etiketli ağaçlar JSON belgeleri modellenmesini sağlar. Bu hem DocumentDB API'nin otomatik dizin oluşturma teknikleri ve bunun yanı sıra DocumentDB API'nin SQL diyalekti tarafından yararlanan. Merhaba DocumetDB API sorgu dili üç ana yönlerini oluşur:   

1. Doğal olarak hiyerarşik sorgular ve tahminleri dahil olmak üzere toohello ağaç yapısı eşleme sorgu işlemleri küçük bir dizi. 
2. Bir alt kümesini oluşturma, filtre, projeksiyonları, toplamalar ve kendi kendine birleşim dahil olmak üzere ilişkisel işlemler. 
3. Saf JavaScript çalışmak UDF'ler (1) ve (2) bağlı.  

Merhaba Cosmos DB sorgu modelini toostrike işlevselliği, verimliliği ve Basitlik arasında bir denge çalışır. Merhaba Cosmos DB veritabanı altyapısı yerel olarak derler ve hello SQL sorgu deyimi yürütür. Bir koleksiyon hello kullanarak sorgulama yapabilirsiniz [REST API'leri](/rest/api/documentdb/) veya hello [istemci SDK'ları](documentdb-sdk-dotnet.md). Merhaba .NET SDK'sı LINQ sağlayıcı ile birlikte gelir.

> [!TIP]
> DocumentDB API hello deneyin ve kümemize hello karşı SQL sorguları çalıştırma [Query Playground](https://www.documentdb.com/sql/demo).
> 
> 

## <a name="multi-document-transactions"></a>Çoklu belge işlemler
Veritabanı işlemleri eşzamanlı değişiklikleri toohello veri ilgilenmek için güvenli ve tahmin edilebilir bir programlama modeli sağlar. RDBMS içinde hello geleneksel bir şekilde toowrite iş mantığı toowrite olan **saklı yordamlar** ve/veya **Tetikleyicileri** ve işlem yürütme için toohello veritabanı sunucusu sevk. RDBMS iki farklı programlama dilleriyle gerekli toodeal hello uygulama Programcı şöyledir: 

* Merhaba (İşlemsel olmayan) uygulama programlama dili (örneğin JavaScript, Python, C#, Java, vb.)
* T-SQL, yerel olarak hello veritabanı tarafından yürütülen hello işlem programlama dili

Saklı yordamlar bakımından hello koleksiyonlar üzerinde doğrudan uygulama mantığını yürütülen JavaScript tabanlı için derin taahhüt tooJavaScript ve doğrudan hello veritabanı altyapısının içinde JSON, Cosmos DB sezgisel bir programlama modeli sağlar ve tetikler. Bu hem de hello aşağıdakileri sağlar:

* Eşzamanlılık verimli uyarlamasını denetlemek, Kurtarma, otomatik hello JSON nesnesi grafiklerin doğrudan hello Veritabanı Altyapısı'ndaki dizin oluşturma
* Denetim akışı, değişken kapsamı, atama ve özel durum işleme temelleri veritabanı işlemleri doğrudan hello JavaScript programlama dili açısından ile tümleştirilmesi doğal olarak belirtme

bir koleksiyon düzeyinde kayıtlı hello JavaScript mantığı, ardından koleksiyonu verilen hello hello belgelerde veritabanı işlemlerini verebilir. Cosmos DB JavaScript saklı yordamları ve Tetikleyicileri bir çevresel ACID işlemlerini arasında anlık görüntü yalıtımıyla içinde dayalı sarmalayan hello örtük olarak bir koleksiyon içinde belgelenmiştir. Merhaba, yürütme sürecinde JavaScript bir özel durum oluşturur hello sonra Merhaba, tüm işlem iptal edildi. Merhaba elde edilen programlama modeli bir oldukça basittir henüz güçlü. JavaScript geliştiricilerin kendi tanıdık dil yapıları ve kitaplık temelleri kullanmaya devam ederken "dayanıklı" programlama modeli alın.   

Merhaba doğrudan hello veritabanı içinde JavaScript özelliği tooexecute altyapısı hello aynı adres alanı gibi hello arabellek havuzu kullanıcı ve bir koleksiyon hello belgeleri karşı veritabanı işlemleri işlem tabanlı olarak yürütülmesini sağlar. Ayrıca, derin taahhüt toohello JSON Cosmos DB veritabanı altyapısı yapar ve JavaScript uygulama hello türü sistemlerinin ve hello veritabanı arasında herhangi empedanslı uyumsuzluğu ortadan kaldırır.   

Bir koleksiyonu oluşturduktan sonra saklı yordamlar, tetikleyiciler ve UDF'lerin hello kullanarak koleksiyonuyla kaydedebilirsiniz [REST API'leri](/rest/api/documentdb/) veya hello [istemci SDK'ları](documentdb-sdk-dotnet.md). Kayıttan sonra başvuru ve bunları yürütün. Merhaba aşağıdaki saklı yordamı aşağıdaki hello kodu (rehberi adını ve yazar adı) iki bağımsız değişken almayan tamamen JavaScript'te yazılmış ve yeni bir belge oluşturur, bir belge için sorgular ve ardından – tüm örtük ACID işlemi içinde güncelleştirdiği göz önünde bulundurun. JavaScript özel durum, hello yürütme sırasında herhangi bir noktada hello tüm işlemi durdurur.

    function businessLogic(name, author) {
        var context = getContext();
        var collectionManager = context.getCollection();        
        var collectionLink = collectionManager.getSelfLink()

        // create a new document.
        collectionManager.createDocument(collectionLink,
            {id: name, author: author},
            function(err, documentCreated) {
                if(err) throw new Error(err.message);

                // filter documents by author
                var filterQuery = "SELECT * from root r WHERE r.author = 'George R.'";
                collectionManager.queryDocuments(collectionLink,
                    filterQuery,
                    function(err, matchingDocuments) {
                        if(err) throw new Error(err.message);

                        context.getResponse().setBody(matchingDocuments.length);

                        // Replace hello author name for all documents that satisfied hello query.
                        for (var i = 0; i < matchingDocuments.length; i++) {
                            matchingDocuments[i].author = "George R. R. Martin";
                            // we don’t need tooexecute a callback because they are in parallel
                            collectionManager.replaceDocument(matchingDocuments[i]._self,
                                matchingDocuments[i]);   
                        }
                    })
            })
    };

Merhaba istemci "Merhaba JavaScript mantığı toohello veritabanı HTTP POST ile işlem yürütme için yukarıdaki sevk edebilir". HTTP yöntemleri kullanma hakkında daha fazla bilgi için bkz: [Azure Cosmos DB kaynakları ile RESTful etkileşimleri](https://msdn.microsoft.com/library/azure/mt622086.aspx). 

    client.createStoredProcedureAsync(collection._self, {id: "CRUDProc", body: businessLogic})
       .then(function(createdStoredProcedure) {
            return client.executeStoredProcedureAsync(createdStoredProcedure.resource._self,
                "NoSQL Distilled",
                "Martin Fowler");
        })
        .then(function(result) {
            console.log(result);
        },
        function(error) {
            console.log(error);
        });


Merhaba veritabanı JSON ve JavaScript'i yerel olarak anlar olduğundan, hiçbir tür sistemi uyuşmazlığı, yok "Veya eşleme" ya da gerekli kod oluşturma Sihirli fark.   

Saklı yordamları ve Tetikleyicileri hello geçerli koleksiyon içeriği sunan bir iyi tanımlanmış nesne modeli toplulukta yer alan bir koleksiyon ve hello belgeleri etkileşim.  

DocumentDB API oluşturulabilir, silinmiş hello koleksiyonlarda okuma veya kolayca ya da hello kullanarak numaralandırılan [REST API'leri](/rest/api/documentdb/) veya hello [istemci SDK'ları](documentdb-sdk-dotnet.md). Merhaba DocumentDB API her zaman okuma veya bir koleksiyon hello meta verileri sorgulamak için güçlü tutarlılık sağlar. Bir koleksiyonun otomatik olarak silineceği hello belgeleri, ekleri, saklı yordamlar, Tetikleyiciler hiçbirine erişemiyor ve UDF'ler içerdiği sağlar.   

## <a name="stored-procedures-triggers-and-user-defined-functions-udf"></a>Saklı yordamlar, tetikleyiciler ve kullanıcı tanımlı işlevler (UDF)
Merhaba önceki bölümde açıklandığı gibi hello veritabanı altyapısı içinde bir işlem içinde doğrudan uygulama mantığını toorun yazabilirsiniz. Merhaba uygulama mantığını tamamen JavaScript'te yazılmış ve bir saklı yordam, tetikleyici veya bir UDF olarak modellenir. Hello saklı yordam veya bir tetikleyici içinde JavaScript kodu eklemek, değiştirmek, bir koleksiyon içinde okuma veya sorgu belgeleri sil. Üzerindeki diğer yandan Merhaba, hello JavaScript bir UDF içinden eklenemiyor, Değiştir veya belgeleri silin. UDF'ler hello belgeleri sorgunun sonuç kümesinin numaralandırır ve başka bir sonuç kümesi üretir. Çoklu kiracı için bir temel katı ayırma kaynak İdaresi Cosmos DB zorlar. Her saklı yordam, tetikleyici veya bir UDF işletim sistemi kaynakları toodo, sabit Zamanlayıcının işini alır. Ayrıca, saklı yordamlar, Tetikleyiciler veya UDF'ler karşı dış JavaScript kitaplıklarını bağlayamazsınız ve toothem ayrılan hello kaynak bütçe aşarsanız kara listede. Kayıt, saklı yordamlar kaydı, REST API'leri Tetikleyiciler veya UDF'ler kullanarak koleksiyonu ile Merhaba.  Kayıt sırasında bir saklı yordam, tetikleyici veya bir UDF önceden derlenmiş ve daha sonra yürütülen bayt kod depolanır. bölümden hello nasıl hello Cosmos DB JavaScript SDK'sı tooregister ve için kullanabileceğiniz, yürütme, saklı yordam, tetikleyici ve bir UDF kaydı gösterilmektedir. Merhaba JavaScript SDK'sı olan basit bir sarmalayıcı hello [REST API'leri](/rest/api/documentdb/). 

### <a name="registering-a-stored-procedure"></a>Saklı yordam kaydetme
Kayıt bir saklı yordam yeni bir saklı yordam kaynak HTTP POST ile bir koleksiyon oluşturur.  

    var storedProc = {
        id: "validateAndCreate",
        body: function (documentToCreate) {
            documentToCreate.id = documentToCreate.id.toUpperCase();

            var collectionManager = getContext().getCollection();
            collectionManager.createDocument(collectionManager.getSelfLink(),
                documentToCreate,
                function(err, documentCreated) {
                    if(err) throw new Error('Error while creating document: ' + err.message;
                    getContext().getResponse().setBody('success - created ' + 
                            documentCreated.name);
                });
        }
    };

    client.createStoredProcedureAsync(collection._self, storedProc)
        .then(function (createdStoredProcedure) {
            console.log("Successfully created stored procedure");
        }, function(error) {
            console.log("Error");
        });

### <a name="executing-a-stored-procedure"></a>Saklı yordam yürütme
Bir saklı yordam yürütme, varolan bir saklı yordam kaynağı karşı bir HTTP POST parametreleri toohello yordamı hello istek gövdesinde geçirerek vererek yapılır.

    var inputDocument = {id : "document1", author: "G. G. Marquez"};
    client.executeStoredProcedureAsync(createdStoredProcedure.resource._self, inputDocument)
        .then(function(executionResult) {
            assert.equal(executionResult, "success - created DOCUMENT1");
        }, function(error) {
            console.log("Error");
        });

### <a name="unregistering-a-stored-procedure"></a>Saklı yordam kaydı siliniyor
Saklı yordam kaydını yalnızca bir HTTP DELETE varolan bir saklı yordam kaynağı karşı vererek yapılır.   

    client.deleteStoredProcedureAsync(createdStoredProcedure.resource._self)
        .then(function (response) {
            return;
        }, function(error) {
            console.log("Error");
        });


### <a name="registering-a-pre-trigger"></a>Ön tetikleyici kaydetme
Bir tetikleyici kaydını HTTP POST ile bir koleksiyon üzerinde yeni bir tetikleyici kaynak oluşturarak yapılır. Merhaba tetikleyici bir öncesi olduğu veya işlem bir post tetikleyici ve hello türü (örneğin oluşturma, değiştirme, silme veya tüm ile) ilişkili olabilir belirtebilirsiniz.   

    var preTrigger = {
        id: "upperCaseId",
        body: function() {
                var item = getContext().getRequest().getBody();
                item.id = item.id.toUpperCase();
                getContext().getRequest().setBody(item);
        },
        triggerType: TriggerType.Pre,
        triggerOperation: TriggerOperation.All
    }

    client.createTriggerAsync(collection._self, preTrigger)
        .then(function (createdPreTrigger) {
            console.log("Successfully created trigger");
        }, function(error) {
            console.log("Error");
        });

### <a name="executing-a-pre-trigger"></a>Ön tetikleyici yürütme
Bir tetikleyici yürütme hello sırasındaki hello PUT/POST/silme isteği bir belge kaynağın hello istek üstbilgisi aracılığıyla veren varolan bir tetikleyicinin hello adını belirterek yapılır.  

    client.createDocumentAsync(collection._self, { id: "doc1", key: "Love in hello Time of Cholera" }, { preTriggerInclude: "upperCaseId" })
        .then(function(createdDocument) {
            assert.equal(createdDocument.resource.id, "DOC1");
        }, function(error) {
            console.log("Error");
        });

### <a name="unregistering-a-pre-trigger"></a>Ön tetikleyici kaydını silme
Bir tetikleyici kaydını yalnızca bir HTTP DELETE varolan bir tetikleyici kaynağı karşı veren aracılığıyla yapılır.  

    client.deleteTriggerAsync(createdPreTrigger._self);
        .then(function(response) {
            return;
        }, function(error) {
            console.log("Error");
        });

### <a name="registering-a-udf"></a>Bir UDF kaydetme
Bir UDF kaydını HTTP POST ile bir koleksiyon üzerinde yeni bir UDF kaynak oluşturarak yapılır.  

    var udf = { 
        id: "mathSqrt",
        body: function(number) {
                return Math.sqrt(number);
        },
    };
    client.createUserDefinedFunctionAsync(collection._self, udf)
        .then(function (createdUdf) {
            console.log("Successfully created stored procedure");
        }, function(error) {
            console.log("Error");
        });

### <a name="executing-a-udf-as-part-of-hello-query"></a>UDF hello sorgu parçası olarak çalıştırma
Bir UDF hello SQL sorgusunun bir parçası olarak belirtilen ve bir şekilde tooextend hello çekirdek kullanılan [SQL sorgu dili hello DocumentDB API için](https://msdn.microsoft.com/library/azure/dn782250.aspx).

    var filterQuery = "SELECT udf.mathSqrt(r.Age) AS sqrtAge FROM root r WHERE r.FirstName='John'";
    client.queryDocuments(collection._self, filterQuery).toArrayAsync();
        .then(function(queryResponse) {
            var queryResponseDocuments = queryResponse.feed;
        }, function(error) {
            console.log("Error");
        });

### <a name="unregistering-a-udf"></a>Bir UDF kaydı siliniyor
Bir UDF kaydını yalnızca bir HTTP DELETE varolan bir UDF kaynağı karşı vererek yapılır.  

    client.deleteUserDefinedFunctionAsync(createdUdf._self)
        .then(function(response) {
            return;
        }, function(error) {
            console.log("Error");
        });

Yukarıdaki Hello parçacıkları hello kayıt (POST), kayıt silme (PUT), okuma/listesi (GET) ve yürütme (POST) hello aracılığıyla gösterdi rağmen [JavaScript SDK'sı](https://github.com/Azure/azure-documentdb-js), hello de kullanabilirsiniz [REST API'leri](/rest/api/documentdb/) veya diğer [istemci SDK'ları](documentdb-sdk-dotnet.md). 

## <a name="documents"></a>Belgeler
Eklemek, değiştirmek, silmek, okuyabilir, listeleme ve rastgele JSON belgelerinin bir koleksiyondaki sorgu. Cosmos DB herhangi bir şema zorunlu kılabilir değil ve bir koleksiyon belgelerde üzerinden sorgulama sipariş toosupport'deki ikincil dizinler gerektirmez. bir belge için maksimum boyut Hello 2 MB'tır.   

Gerçekten açık veritabanı hizmeti olan, Cosmos DB herhangi bir özel veri türleri (örneğin, tarih saat) ile stok değil ya da belirli kodlamaları JSON belgeleri için. Cosmos DB özel JSON kuralları toocodify hello ilişkileri çeşitli belgeler arasında gerektirmez unutmayın; Cosmos DB Hello SQL söz dizimini çok güçlü hiyerarşik ve ilişkisel sorgu işleçleri herhangi bir özel ek açıklama veya gereksinim toocodify ilişkileri ayırt edici özellikleri kullanarak belgeler arasında olmadan tooquery ve proje belgeler sağlar.  

Tüm diğer kaynaklarla belgeleri oluşturulabilir olarak değiştirildi, silinmiş, okuma, numaralandırılmış ve kolayca REST API'leri veya hello birini kullanarak sorgulanan [istemci SDK'ları](documentdb-sdk-dotnet.md). Bir belgeyi hemen silme hello kota karşılık gelen tooall iç içe geçmiş hello eklerin boşaltır. Merhaba, belgelerin tutarlılık düzeyi hello tutarlılık İlkesi hello veritabanı hesabındaki izleyen okuyun. Bu ilke, uygulamanızın veri tutarlılığı gereksinimlerine bağlı olarak istek başına temelinde geçersiz kılınabilir. Belgeleri sorgulanırken hello modu hello koleksiyonu dizin tutarlılık aşağıdaki hello okuyun. "İçin tutarlı", bu hello hesabın tutarlılık ilke aşağıdaki gibidir. 

## <a name="attachments-and-media"></a>Ekleri ve ortam
Cosmos DB toostore ikili BLOB'lar/medya, Cosmos DB (hesap başına en fazla 2 GB) veya tooyour kendi uzaktan medya depolama sağlar. Ayrıca, bir ortam eki adlı özel bir belge bakımından toorepresent hello meta verileri sağlar. Cosmos DB ek başvurular medya/blob başka bir yerde depolanan hello bir özel (JSON) belgedir. Merhaba meta verileri (ör. konum, yazar vb.) bir uzak medya depolamada depolanan bir medya yakalayan yalnızca bir özel belge ektir. 

Yer işaretleri, derecelendirme, yöntemlerine/Beğenmediklerinizi vb. bir e-kitap için belirli bir kullanıcının ilişkili meta verileri, Yorumlar dahil olmak üzere vurgular ve Cosmos DB toostore açıklamaların kullanan bir sosyal okuma uygulaması düşünün.   

* Merhaba hello kitap kendisini içeriğini hello medya deposunda ya da depolanan Cosmos DB veritabanı hesabı parçası veya bir uzak medya deposu olarak kullanılabilir. 
* Bir uygulamayı ayrı bir belge olarak her kullanıcının meta verileri depolayabilir--örneğin Kitap1 Can'ın meta verilerini /colls/joe/docs/book1 tarafından başvurulan bir belge depolanır. 
* Bir kullanıcının belirli bir rehberi toohello içerik sayfaları işaret eden ek hello karşılık gelen belge ör /colls/joe/docs/book1/chapter1 altında depolanan /colls/joe/docs/book1/chapter2 vs. 

Merhaba örnekleri yukarıda listelenen Not kolay kimlikleri tooconvey hello kaynak hiyerarşisi kullanın. Kaynakları benzersiz kaynak kimlikleri aracılığıyla hello REST API'leri aracılığıyla erişilir. 

Cosmos DB tarafından yönetilen hello medyayı hello _media özelliği hello ekin hello medya URI'sini tarafından başvurur. Tüm hello bekleyen başvurularını bırakıldığında cosmos DB toogarbage toplama hello medya güvence altına alır. Cosmos DB otomatik olarak hello yeni medya yüklediğinizde hello eki oluşturur ve hello _media toopoint toohello yeni eklenen medya doldurur. Sizin tarafınızdan (örn. OneDrive, Azure Storage, DropBox vb.) yönetilen bir uzak blob Mağazası'nda toostore hello medya seçerseniz, ekleri tooreference hello medya kullanmaya devam edebilirsiniz. Bu durumda, hello eki kendiniz oluşturmanız ve onun _media özelliğini doldurmak.   

Diğer tüm kaynaklar gibi ile ekleri oluşturulabilir, silinmiş, okuma veya değiştirilmesi kolayca REST API'leri veya hello istemci SDK'ları birini kullanarak numaralandırılır. Belgeler, ekleri tutarlılık düzeyi hello okurken hello tutarlılık ilke hello veritabanı hesabındaki aşağıdaki gibidir. Bu ilke, uygulamanızın veri tutarlılığı gereksinimlerine bağlı olarak istek başına temelinde geçersiz kılınabilir. Ekler için sorgulanırken hello modu hello koleksiyonu dizin tutarlılık aşağıdaki hello okuyun. "İçin tutarlı", bu hello hesabın tutarlılık ilke aşağıdaki gibidir. 
 

## <a name="users"></a>Kullanıcılar
Cosmos DB kullanıcı izinleri gruplandırması için mantıksal bir ad alanı temsil eder. Cosmos DB kullanıcı tooa kullanıcı bir kimlik yönetimi sistemi veya önceden tanımlanmış uygulama rolü karşılık gelebilir. Cosmos DB için bir kullanıcı yalnızca bir soyutlama toogroup bir veritabanı altında izinler kümesini temsil eder.   

Çoklu kiracı uygulamanızda uygulamak için kullanıcılar tooyour gerçek kullanıcıları veya uygulamanızın hello kiracılar karşılık gelen Cosmos DB içinde oluşturabilirsiniz. Daha sonra toohello erişim denetimi çeşitli koleksiyonlar, belgeler, ekleri, vb. üzerinden karşılık gelen belirli bir kullanıcının izinlerini oluşturabilirsiniz.   

Uygulamalarınızı, kullanıcı büyüme ile tooscale gerektiği verilerinizi çeşitli yolları tooshard benimseyebilirsiniz. Her kullanıcılarınızın gibi model oluşturabilirsiniz:   

* Her kullanıcı tooa veritabanı eşler.
* Her kullanıcı tooa koleksiyonu eşler. 
* Toomultiple kullanıcılar karşılık gelen belgeleri ayrılmış tooa koleksiyonu gidin. 
* Toomultiple kullanıcılar karşılık gelen belgeleri koleksiyonları tooa kümesi gidin.   

Seçtiğiniz hello belirli parçalama stratejisi bağımsız olarak Cosmos DB veritabanındaki kullanıcı olarak gerçek kullanıcılarınızın model ve ince tanecikli izinleri tooeach kullanıcı ilişkilendirin.  

![Kullanıcı koleksiyonları][3]  
**Parçalama stratejilerini ve modelleme kullanıcılar**

Diğer tüm kaynaklar gibi Cosmos DB kullanıcılar oluşturulabilir, silinmiş, okuma veya değiştirilmesi kolayca REST API'leri veya hello istemci SDK'ları birini kullanarak numaralandırılır. Cosmos DB her zaman okuma veya kullanıcı kaynağı hello meta verileri sorgulamak için güçlü tutarlılık sağlar. Kullanıcı otomatik olarak silme içerdiği hello izinleri hiçbirine erişemiyor sağlar işaret eden değer olur. Hello silinmiş kullanıcı hello arka planda bir parçası olarak hello kota hello izinleri Hello Cosmos DB kaldırsa olsa bile, silinen hello izinleri kullanılabilir hemen yeniden, toouse.  

## <a name="permissions"></a>İzinler
Bir veritabanı hesapları gibi kaynaklara erişim denetimi açısından veritabanları, kullanıcılar ve izni kabul edilen *Yönetim* bunlar yönetim izinleri gerektirir olduğundan kaynaklar. Diğer yandan, hello koleksiyonlar, belgeler, ekleri, saklı yordamlar, Tetikleyiciler, dahil olmak üzere kaynaklar üzerinde hello ve UDF'ler altında verilen bir veritabanı kapsamlı ve kabul *uygulama kaynakları*. Kaynakları ve bunlara (yani Merhaba yönetici ve kullanıcı) erişim hello rolleri iki tür toohello karşılık gelen, iki tür hello yetkilendirme modelini tanımlar *erişim anahtarları*: *ana anahtar* ve *kaynak anahtarı*. Merhaba ana anahtar hello veritabanı hesabı, bir parçasıdır ve toohello geliştirici (veya yönetici) sağlanan kimin hello veritabanı hesabı sağlama. Kullanılan tooauthorize erişim tooboth yönetim ve uygulama kaynakları olabilir, bu ana anahtar Yöneticisi semantiği sahiptir. Buna karşılık, kaynak anahtarı erişim tooa izin veren bir ayrıntılı erişim anahtarıdır *belirli* Uygulama kaynağı. Bu nedenle, bir veritabanının hello kullanıcı arasındaki ilişki hello yakalar ve hello izinleri hello kullanıcı belirli bir kaynak için (örneğin koleksiyonu, belge, ek, saklı yordam, tetikleyici veya UDF) sahiptir.   

belirli bir kullanıcının altında izni kaynak oluşturarak bir kaynak anahtardır hello tek yolu tooobtain. Sipariş toocreate dikkat edin veya izni almak, bir ana anahtar hello yetkilendirme üstbilgisinde sunulmalıdır. Merhaba kaynak, erişim ve hello kullanıcı izni kaynak bağlar. İzni kaynak oluşturduktan sonra hello kullanıcı yalnızca bir sipariş toogain erişim toohello ilgili kaynak toopresent hello ilişkili kaynak anahtarı gerekir. Bu nedenle, bir kaynak anahtarı hello izni kaynak mantıksal ve compact gösterimi görüntülenebilir.  

Diğer tüm kaynaklar gibi ile Cosmos DB izinleri oluşturulabilir, silinmiş, okuma veya değiştirilmesi kolayca REST API'leri veya hello istemci SDK'ları birini kullanarak numaralandırılır. Cosmos DB her zaman okuma veya izin hello meta verileri sorgulamak için güçlü tutarlılık sağlar. 

## <a name="next-steps"></a>Sonraki adımlar
HTTP komutları kullanarak kaynakları ile çalışma hakkında daha fazla bilgi [Cosmos DB kaynakları ile RESTful etkileşimleri](https://msdn.microsoft.com/library/azure/mt622086.aspx).

[1]: media/documentdb-resources/resources1.png
[2]: media/documentdb-resources/resources2.png
[3]: media/documentdb-resources/resources3.png

