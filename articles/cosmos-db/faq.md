---
title: "aaaAzure Cosmos DB sık sorulan sorular | Microsoft Docs"
description: "Genel olarak dağıtılmış, birden çok model veritabanı hizmeti olan Azure Cosmos DB hakkında sorular yanıtlar toofrequently alın. Kapasite, performans düzeyleri ve ölçeklendirme hakkında bilgi edinin."
keywords: "Sık sorulan sorular, documentdb, azure, Microsoft azure veritabanı soruları"
services: cosmos-db
author: mimig1
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: b68d1831-35f9-443d-a0ac-dad0c89f245b
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: mimig
ms.openlocfilehash: 59e047d9acd8ac05facc96655747d7495a45317a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-faq"></a>Azure Cosmos DB SSS
## <a name="azure-cosmos-db-fundamentals"></a>Azure Cosmos DB temelleri
### <a name="what-is-azure-cosmos-db"></a>Azure Cosmos DB nedir?
Azure Cosmos DB, şemasız verilerde zengin sorgulama sunan yapılandırılabilir ve güvenilir performans sağlanmasına yardımcı olan bir genel çoğaltılmış, birden çok model veritabanı hizmetidir ve hızlı geliştirme sağlar. Tüm hello güç tarafından yedeklenir ve Microsoft Azure'nın bir yönetilen platform sağlanır. 

Azure Cosmos DB hello için doğru web, mobil, oyun çözümdür ve tahmin edilebilir iş çıkarma, yüksek kullanılabilirlik, düşük gecikme süresi ve şemasız veri modeli IOT uygulamaları anahtar gereksinimleridir. Şema esnekliği ve zengin dizin oluşturma sağlar ve tümleşik JavaScript ile çok belgeli işlem desteğini içerir. 

Daha fazla veritabanı soruları yanıtlar ve dağıtma ve bu hizmeti kullanmak için yönergeler hello görmek için [Azure Cosmos DB belge sayfasının](https://azure.microsoft.com/documentation/services/cosmos-db/).

### <a name="what-happened-toodocumentdb"></a>Hangi happened tooDocumentDB?
Merhaba DocumentDB API desteklenen hello API'ler ve veri modelleri için Azure Cosmos DB biridir. Ayrıca, Azure Cosmos DB, grafik API'si (Önizleme), tablo API (Önizleme) ve MongoDB API ile destekler. Daha fazla bilgi için bkz: [DocumentDB müşterilerden sorular](#moving-to-cosmos-db).

### <a name="how-do-i-get-toomy-documentdb-account-in-hello-azure-portal"></a>Hello Azure portal toomy DocumentDB hesabı nasıl sağlarım?
Hello Azure portal, hello sol bölmede hello Azure Cosmos DB simgesine tıklayın. Bir DocumentDB hesabı önce olsaydı, artık bir Azure Cosmos DB hesabıyla hiçbir değişiklik tooyour faturalama sahipsiniz.

### <a name="what-are-hello-typical-use-cases-for-azure-cosmos-db"></a>Azure Cosmos DB için hello genel kullanım örnekleri nelerdir?
Azure Cosmos DB yeni web, mobil, oyun için iyi bir seçenektir ve burada otomatik ölçeğin, tahmin edilebilir performans, milisaniye yanıt sürelerinin sırasını hızlı ve şemasız verileri özelliği tooquery hello IOT uygulamaları önemlidir. Azure Cosmos DB kendisini toorapid geliştirme ve uygulama veri modellerinin sürekli yinelenmesini hello destekleyici uygundur. Kullanıcı tarafından oluşturulan içeriği ve verileri yöneten uygulamalar [ortak kullanım durumları için Azure Cosmos DB](use-cases.md). 

### <a name="how-does-azure-cosmos-db-offer-predictable-performance"></a>Azure Cosmos DB tahmin edilebilir performansı nasıl sunar?
A [istek birimi](request-units.md) (RU) Azure Cosmos veritabanı işleme hello ölçü değil. 1 RU verimlilik hello bir 1 KB belgenin GET toohello verimini karşılık gelir. Her işlem, okuma, yazma, SQL sorguları ve saklı yordam yürütmeleri dahil olmak üzere Azure Cosmos DB hello gerekli verimlilik toocomplete hello işlemi temel alan bir belirleyici RU değer içeriyor. CPU, IO, bellek ve bunların her birinin uygulama işlemenizi nasıl etkileyeceğini hakkında düşünmek yerine, tek bir RU ölçü açısından düşünebilirsiniz.

Saniye başına RUs bakımından sağlanan işleme sahip her Azure Cosmos DB kapsayıcısı ayırabilirsiniz. Her ölçekten uygulama için istekleri ayrı ayrı toomeasure RU değerlerine Kıyaslama ve tüm istekler genelinde istek birimlerinin kapsayıcı toohandle hello toplam sağlayın. Ayrıca, ölçeği veya hello uygulamanızın ihtiyaçları geliştikçe, kapsayıcının işleme ölçeklendirin. İstek birimleri hakkında daha fazla bilgi ve Yardım için kapsayıcı belirlemek bkz gereksinimlerini [üretilen iş gereksinimlerini tahmin etme](request-units.md#estimating-throughput-needs) ve hello deneyin [verimlilik hesaplayıcı](https://www.documentdb.com/capacityplanner). Merhaba terim *kapsayıcı* toorefers tooa DocumentDB API koleksiyonu, grafik API'si grafik, MongoDB API koleksiyonu ve tablo API tablo burada başvuruyor. 

### <a name="how-does-azure-cosmos-db-support-various-data-models-such-as-keyvalue-columnar-document-and-graph"></a>Azure Cosmos DB anahtar/değer, sütunlu, belge ve grafik gibi çeşitli veri modelleri nasıl destekler?

Anahtar/değer (tablo), sütunlu, belge ve tüm yerel olarak desteklenen hello ARS (atom, kaydeder ve dizileri) nedeniyle bu Azure Cosmos DB tasarım modelleri olan grafik verileri üzerine kurulmuştur. Atom, kaydeder ve dizilerini kolayca eşlenen ve tahmini toovarious veri modelleri olabilir. Merhaba API'leri modelleri alt kümeleri için olan kullanılabilir sağ şimdi (DocumentDB, MongoDB, tablo ve grafik API'leri) ve diğerleri belirli tooadditional veri modelleri kullanılabilir olması gelecekteki hello.

Azure Cosmos DB bir şema belirsiz dizin oluşturma altyapısı otomatik olarak herhangi bir şemayı ya da ikincil dizinlerin hello geliştiriciden gerek kalmadan alır tüm hello dizin oluşturma verileri özellikli vardır. Merhaba altyapısı, başlangıç dizini ve sorgu alt sistemleri işleme hello depolama düzeni ayırırsınız mantıksal dizin düzenleri (ters, sütunlu, ağaç) kümesi kullanır. Cosmos DB ayrıca hello özelliği toosupport genişletilebilir bir şekilde kablo protokolleri ve API'leri kümesine sahiptir ve bunları verimli bir şekilde (2) birden fazla veri modeli yerel olarak destekleyen benzersiz olarak özellikli kolaylaştırarak toohello çekirdek veri modeli (1) ve hello mantıksal dizin düzenlerini Çevir .

### <a name="is-azure-cosmos-db-hipaa-compliant"></a>Azure Cosmos DB HIPAA uyumlu mu?
Evet, Azure Cosmos DB HIPAA ile uyumlu değil. Hello gereksinimleri kullanımı, açıklanması ve bağımsız olarak tanımlanabilen sağlık bilgilerinin koruma HIPAA. Daha fazla bilgi için bkz: Merhaba [Microsoft Trust Center](https://www.microsoft.com/en-us/TrustCenter/Compliance/HIPAA).

### <a name="what-are-hello-storage-limits-of-azure-cosmos-db"></a>Azure Cosmos DB hello depolama sınırları nelerdir?
Hiçbir sınır toohello toplam Azure Cosmos DB içinde bir kapsayıcı depolayan veri miktarını yoktur.

### <a name="what-are-hello-throughput-limits-of-azure-cosmos-db"></a>Azure Cosmos DB hello işleme sınırları nelerdir?
Hiçbir sınır toohello toplam miktarı Azure Cosmos DB içinde bir kapsayıcı destekleyen verimlilik yoktur. Merhaba anahtar fikir toodistribute yükünüzü kabaca eşit bir yeterli büyüklükte bölüm anahtarlarını arasında sayısıdır.

### <a name="how-much-does-azure-cosmos-db-cost"></a>Nasıl Azure Cosmos DB maliyeti nedir?
Ayrıntılar için toohello başvurun [Azure Cosmos fiyatlandırma ayrıntıları DB](https://azure.microsoft.com/pricing/details/cosmos-db/) sayfası. Azure Cosmos DB kullanım ücretleri Merhaba kapsayıcılara çevrimiçi ve hello her kapsayıcı için işleme sağlanan sağlanan kapsayıcıları, hello kaç saat hello sayısına göre belirlenir. Merhaba terim *kapsayıcıları* toohello DocumentDB API koleksiyonu, grafik API'si grafik, MongoDB API koleksiyonu ve tablo API tabloları burada başvuruyor. 

### <a name="is-a-free-account-available"></a>Ücretsiz bir hesap var mı?
Yeni tooAzure varsa, için kaydolabilirsiniz bir [ücretsiz Azure hesabına](https://azure.microsoft.com/free/), hangi size 30 gün ve ve Azure Hizmetleri hello bir kredi tootry tüm. Visual Studio aboneliğiniz varsa, aynı zamanda hakkınız bulunur [ücretsiz Azure kredisi](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) toouse herhangi bir Azure hizmeti üzerinde. 

Merhaba de kullanabilirsiniz [Azure Cosmos DB öykünücüsü](local-emulator.md) toodevelop ve test uygulamanızı yerel olarak için ücretsiz, Azure aboneliği oluşturmadan. Uygulamanızı hello Azure Cosmos DB öykünücüsü nasıl çalıştığını ile memnun kaldığınızda, toousing hello buluttaki bir Azure Cosmos DB hesabını geçiş yapabilirsiniz.

### <a name="how-can-i-get-additional-help-with-azure-cosmos-db"></a>Ek Yardım Azure Cosmos DB ile nasıl alabilirim?
Yardıma ihtiyacınız olursa üzerinde toous ulaşmak [yığın taşması](http://stackoverflow.com/questions/tagged/azure-cosmosdb) veya hello [MSDN Forumu](https://social.msdn.microsoft.com/forums/azure/en-US/home?forum=AzureDocumentDB), veya posta çok göndererek hello Azure Cosmos DB mühendislik ekibi ile bire bir sohbet zamanlama[ askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com). 

## <a name="set-up-azure-cosmos-db"></a>Azure Cosmos DB'yi yedekleyin ayarlayın
### <a name="how-do-i-sign-up-for-azure-cosmos-db"></a>Nasıl Azure Cosmos DB kaydolabilirim?
Azure Cosmos DB hello Azure portalında kullanılabilir. İlk olarak, Azure aboneliği için kaydolun. Oturum açtığınız sonra DocumentDB API ekleyebilirsiniz, grafik API'si (Önizleme), tablo API (Önizleme) ya da MongoDB API tooyour Azure aboneliği hesap.

### <a name="what-is-a-master-key"></a>Ana anahtar nedir?
Bir ana anahtar bir güvenlik belirteci tooaccess olan bir hesap için tüm kaynakları. Merhaba anahtara sahip kişiler okuma ve yazma erişimi tooall kaynaklar hello veritabanı hesabında sahiptir. Ana anahtarları dağıtırken dikkatli olun. Merhaba birincil ana anahtar ve ikincil ana anahtar hello üzerinde kullanılabilir **anahtarları** hello dikey [Azure portal][azure-portal]. Anahtarlar hakkında daha fazla bilgi için bkz: [görüntüleme, kopyalama ve yeniden oluşturma erişim tuşları](manage-account.md#keys).

### <a name="what-are-hello-regions-that-preferredlocations-can-be-set-to"></a>PreferredLocations ayarlanabilir hello bölgeleri nelerdir? 
Merhaba PreferredLocations değeri hello Azure tooany ayarlanabilir bölgeleri Cosmos DB olduğu kullanılabilir. Kullanılabilir bölgelerin bir listesi için bkz: [Azure bölgeleri](https://azure.microsoft.com/regions/).

### <a name="is-there-anything-i-should-be-aware-of-when-distributing-data-across-hello-world-via-hello-azure-datacenters"></a>Veri hello world hello Azure veri merkezleri aracılığıyla arasında dağıtırken farkında olmalıdır bir şey var mı? 
Azure Cosmos DB mevcut tüm Azure bölgeleri arasında belirtilen hello [Azure bölgeleri](https://azure.microsoft.com/regions/) sayfası. Merhaba çekirdek hizmeti olduğundan, her yeni bir veri merkezine Azure Cosmos DB durum vardır. 

Bir bölge ayarladığınızda, Azure Cosmos DB sovereign ve kamu Bulutlar uyar unutmayın. Diğer bir deyişle, sovereign bir bölgede bir hesap oluşturursanız, o sovereign bölgesinin dışına çoğaltma yapamaz. Benzer şekilde, bir dış hesap sovereign diğer konumlardan içine çoğaltmayı etkinleştiremezsiniz. 

## <a name="develop-against-hello-documentdb-api"></a>DocumentDB API Hello karşı geliştirin

### <a name="how-do-i-start-developing-against-hello-documentdb-api"></a>DocumentDB API hello karşı geliştirme nasıl başlamanız gerekir?
Microsoft DocumentDB API hello kullanılabilir [Azure portal][azure-portal]. Önce Azure aboneliği için kaydolmanız gerekir. Azure aboneliği için kaydolduktan sonra DocumentDB API kapsayıcı tooyour Azure aboneliğiniz ekleyebilirsiniz. Bir Azure Cosmos DB hesap ekleme ile ilgili yönergeler için bkz: [Azure Cosmos DB veritabanı hesabı oluşturma](create-documentdb-dotnet.md#create-account). Merhaba son DocumentDB hesabı olsaydı, artık Azure Cosmos DB hesabınız var. 

.NET, Python, Node.js, JavaScript ve Java için [SDK'lar](documentdb-sdk-dotnet.md) kullanılabilir. Geliştiriciler ayrıca hello kullan [RESTful HTTP API'lerini](/rest/api/documentdb/) toointeract Azure Cosmos DB kaynaklardan çeşitli platformlar ve diller.

### <a name="can-i-access-some-ready-made-samples-tooget-a-head-start"></a>Bazı hazır örnekleri tooget başlangıç erişebilir mi?
Merhaba DocumentDB API için örnek [.NET](documentdb-dotnet-samples.md), [Java](https://github.com/Azure/azure-documentdb-java), [Node.js](documentdb-nodejs-samples.md), ve [Python](documentdb-python-samples.md) SDK'ları Github'da bulunmaktadır.


### <a name="does-hello-documentdb-api-database-support-schema-free-data"></a>Merhaba DocumentDB API veritabanı desteği şemasız verileri mu?
Evet, DocumentDB API hello uygulamaları toostore şema tanımları veya ipuçları olmadan rastgele JSON belgelerinin sağlar. Veriler hello Azure Cosmos DB SQL sorgu arabirimi yoluyla sorgu için hemen kullanılabilir.  

### <a name="does-hello-documentdb-api-support-acid-transactions"></a>Merhaba DocumentDB API ACID işlemlerini destekler mi?
Evet, DocumentDB API hello JavaScript saklı yordamları ve Tetikleyicileri ifade edilen belgeler arası işlemleri destekler. İşlemler her bir koleksiyonun içindeki tek bölüm tooa kapsamlı ve "tümü veya hiçbiri," olarak ACID semantiği ile yürütülen diğer eş zamanlı yürütme kodları ve kullanıcı isteklerinden ayrı. Merhaba sunucu tarafı JavaScript uygulama kodunun yürütülmesini özel durumlar varsa, hello tüm işlem geri alındı. İşlemler hakkında daha fazla bilgi için bkz: [veritabanı program işlemleri](programming.md#database-program-transactions).

### <a name="what-is-a-collection"></a>Koleksiyon nedir?
Bir koleksiyon, belgeler ve bunların ilişkili JavaScript uygulama mantığının grubudur. Faturalanabilir bir varlık hello burada koleksiyonudur [maliyet](performance-levels.md) hello verimlilik tarafından belirlenir ve depolama kullanılır. Koleksiyonlar bir veya daha fazla bölüm veya sunucuları kapsayabilir ve toohandle ölçeklendirebilirsiniz neredeyse sınırsız miktarda depolama veya işlemeyi.

Koleksiyonlar ayrıca Azure Cosmos DB hello fatura varlıklar içindir. Her koleksiyon saatlik olarak faturalandırılır hello sağlanan işlemeyi temel alan ve kullanılan depolama alanı. Daha fazla bilgi için bkz: [Azure DB Cosmos fiyatlandırma](https://azure.microsoft.com/pricing/details/cosmos-db/). 

### <a name="how-do-i-create-a-database"></a>Veritabanı nasıl oluşturulur?
Hello kullanarak veritabanları oluşturabilirsiniz [Azure portal](https://portal.azure.com)açıklandığı gibi [bir koleksiyon Ekle](create-documentdb-dotnet.md#create-collection), hello birini [Azure Cosmos DB SDK'ları](documentdb-sdk-dotnet.md), veya hello [REST API'leri](/rest/api/documentdb/). 

### <a name="how-do-i-set-up-users-and-permissions"></a>Kullanıcıları ve izinleri nasıl ayarlarım?
Merhaba birini kullanarak, kullanıcılar ve izinler oluşturabilirsiniz [Cosmos DB API SDK'ları](documentdb-sdk-dotnet.md) veya hello [REST API'leri](/rest/api/documentdb/).  

### <a name="does-hello-documentdb-api-support-sql"></a>Merhaba DocumentDB API SQL destekliyor mu?
Merhaba SQL sorgu dili Gelişmiş bir SQL tarafından desteklenen hello sorgu işlevi alt kümesidir. Hello Azure Cosmos DB SQL sorgu dili zengin hiyerarşik ve ilişkisel işleçler ve genişletilebilirlik JavaScript tabanlı, kullanıcı tanımlı işlevler (UDF'ler) aracılığıyla sağlar. JSON dil bilgisi hem hello Azure Cosmos DB otomatik dizin oluşturma teknikleri hem de Azure Cosmos DB hello SQL sorgu diyalekti tarafından kullanılan etiketli düğümleri ağaçlar JSON belgeleri modellenmesini sağlar. Merhaba SQL dil bilgisinin kullanma hakkında daha fazla bilgi için bkz: [QueryDocumentDB] [ query] makalesi.

### <a name="does-hello-documentdb-api-support-sql-aggregation-functions"></a>Merhaba DocumentDB API desteği SQL toplama işlevleri mu?
Merhaba DocumentDB API destekleyen düşük gecikme süreli toplama toplama işlevleri aracılığıyla herhangi bir ölçekte `COUNT`, `MIN`, `MAX`, `AVG`, ve `SUM` hello SQL dil bilgisinin aracılığıyla. Daha fazla bilgi için bkz: [toplama işlevlerinin](documentdb-sql-query.md#Aggregates).

### <a name="how-does-hello-documentdb-api-provide-concurrency"></a>Merhaba DocumentDB API eşzamanlılığı nasıl sağlar?
Merhaba DocumentDB API HTTP varlık etiketleri veya Etag'ler aracılığıyla iyimser eşzamanlılık denetimini (OCC) destekler. Her DocumentDB API kaynakları bir Etag'e sahiptir ve bir belgeyi her güncelleştirildiğinde hello ETag hello sunucu üzerinde ayarlanır. Merhaba ETag üstbilgi ve hello geçerli değer tüm yanıt iletileri dahil edilir. Bir kaynağın güncelleştirilmesi gerekip gerekmediğini Etag'ler hello IF-Match üstbilgisi tooallow hello sunucu toodecide ile kullanılabilir. Merhaba IF-Match değeri karşılaştırılarak hello ETag değeri toobe ' dir. Merhaba ETag değeri hello sunucu ETag değeri eşleşirse, hello kaynak güncelleştirilir. Merhaba ETag geçerli ise hello sunucu hello işlemiyle reddeder bir "HTTP 412 önkoşul hatası" yanıt kodu. Merhaba istemci ardından hello kaynak tooacquire hello geçerli ETag değeri hello kaynak için yeniden getirir. Ayrıca, bir kaynak yeniden getirin gerekip gerekmediğini Etag'ler hello If-None-Match üstbilgisi toodetermine ile kullanılabilir.

.NET, kullanım hello iyimser eşzamanlılık toouse [AccessCondition](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.accesscondition.aspx) sınıfı. .NET örnek için bkz: [Program.cs](https://github.com/Azure/azure-documentdb-dotnet/blob/master/samples/code-samples/DocumentManagement/Program.cs) github'da hello DocumentManagement örnekteki.

### <a name="how-do-i-perform-transactions-in-hello-documentdb-api"></a>Merhaba DocumentDB API nasıl işlemler gerçekleştirebilir?
Merhaba DocumentDB API JavaScript saklı yordamları ve Tetikleyicileri aracılığıyla dil ile tümleşik işlemleri destekler. Betiklerin içindeki tüm veritabanı işlemleri, anlık görüntü yalıtımı altında yürütülür. Tek bölümlü bir koleksiyon varsa hello yürütme kapsamlı toohello koleksiyonudur. Merhaba koleksiyon bölümlendiğinde hello yürütme hello ile kapsamlı toodocuments varsa, hello koleksiyondaki aynı bölüm anahtarı değeri. (Etag'ler) hello belge sürümlerinin anlık hello hello işlem başlangıcında alınır ve yalnızca hello betik başarılı olursa uygulanır. Merhaba JavaScript bir hata oluşturursa hello işlem geri alındı. Daha fazla bilgi için bkz: [Azure Cosmos DB için sunucu tarafı JavaScript programlama](programming.md).

### <a name="how-can-i-bulk-insert-documents-into-cosmos-db"></a>Nasıl ı toplu belgeleri Cosmos Veritabanına ekleme?
Toplu belgeleri Azure Cosmos Veritabanına iki yoldan biriyle ekleme:

* bölümünde açıklandığı gibi hello veri geçiş aracı [Azure Cosmos DB veritabanı geçiş aracını](import-data.md).
* Saklı yordamlar, açıklandığı gibi [Azure Cosmos DB için sunucu tarafı JavaScript programlama](programming.md).

### <a name="does-hello-documentdb-api-support-resource-link-caching"></a>Merhaba DocumentDB API kaynak bağlantıyı önbelleğe almayı destekliyor mu?
Evet, Azure Cosmos DB bir RESTful hizmeti olduğu için kaynak bağlantıları sabittir ve önbelleğe alınabilir. DocumentDB API istemciler, herhangi bir kaynak benzeri belge veya koleksiyon yapılan okumalar için bir "If-None-Match" üst bilgisi belirtin ve hello sunucu sürümü değiştikten sonra kendi yerel kopyalarını güncelleştirmek.

### <a name="is-a-local-instance-of-documentdb-api-available"></a>DocumentDB API yerel bir örneğini var mı?
Evet. Merhaba [Azure Cosmos DB öykünücüsü](local-emulator.md) hello Cosmos DB hizmeti, yüksek doğruluk öykünmesi sağlar. Aynı tooAzure sağlama Cosmos JSON belgelerini sorgulamak için destek dahil olmak üzere DB ile işlevselliği destekler ve koleksiyonları ölçekleme ve yürütme yordamları ve Tetikleyicileri depolanır. Geliştirme ve hello Azure Cosmos DB öykünücüsü kullanarak uygulamaları test edin ve bunları tek bir yapılandırma için Azure Cosmos DB toohello bağlantı uç noktasının değişikliği yaparak küresel ölçekli tooAzure dağıtabilirsiniz.

## <a name="develop-against-hello-api-for-mongodb"></a>Merhaba karşı API MongoDB için geliştirme
### <a name="what-is-hello-azure-cosmos-db-api-for-mongodb"></a>Hello Azure Cosmos DB API MongoDB için nedir?
Hello Azure Cosmos DB API MongoDB için uygulamaları tooeasily sağlar ve şeffaf bir şekilde hello yerel Azure Cosmos DB veritabanı altyapısı ile var olan, topluluk tarafından desteklenen Apache MongoDB API'leri ve sürücüleri kullanarak iletişim kuran bir uyumluluk katmanıdır. Geliştiriciler artık Azure Cosmos DB yararlanmak MongoDB aracı zincirlerini ve yetenekleri toobuild uygulamalarınız kullanabilirsiniz. Geliştiriciler otomatik dizin oluşturma işlemi, yedekleme bakım, mali yedeklenmiş hizmet düzeyi sözleşmelerine (SLA) vb. dahil hello benzersiz yeteneklerini Azure Cosmos DB yararlanır.

### <a name="how-do-i-connect-toomy-api-for-mongodb-database"></a>Toomy API MongoDB veritabanı için nasıl bağlayabilirim?
hızlı şekilde tooconnect toohello Azure Cosmos DB API MongoDB toohello toohead için hello [Azure portal](https://portal.azure.com). Tooyour hesabı gidin ve ardından, hello sol gezinti menüsünde **Hızlı Başlangıç**. Hızlı Başlangıç hello en iyi şekilde tooget kod parçacıkları tooconnect tooyour veritabanıdır. 

Azure Cosmos DB sıkı güvenlik gereksinimlerine ve standartlarını uygular. Azure Cosmos DB hesapları kimlik doğrulaması ve SSL üzerinden güvenli iletişim gerektirir, bu nedenle emin toouse TLSv1.2 olun.

Daha fazla bilgi için bkz: [tooyour API MongoDB veritabanı için bağlantı](connect-mongodb-account.md).

### <a name="are-there-additional-error-codes-for-an-api-for-mongodb-database"></a>API MongoDB veritabanı için ek hata kodları var mı?
Toplama toohello ortak MongoDB hata kodları, kendi özel hata kodlarını hello MongoDB API vardır:


| Hata               | Kod  | Açıklama  | Çözüm  |
|---------------------|-------|--------------|-----------|
| TooManyRequests     | 16500 | tüketilen istek birimleri toplam sayısı Hello hello sağlanan istek birimi oranı hello koleksiyon için aştı ve daraltıldı. | Hello Azure portal hello koleksiyonundan Hello verimini ölçekleme veya yeniden denemeden göz önünde bulundurun. |
| ExceededMemoryLimit | 16501 | Çok kiracılı bir hizmet hello işlemi hello istemcinin bellek birimi aştı. | Merhaba işlem daha kısıtlayıcı sorgu ölçütlerini aracılığıyla Hello kapsamını azaltmak veya başvurun hello Destek'ten [Azure portal](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade). <br><br>Örnek:  *&nbsp; &nbsp; &nbsp; &nbsp;db.getCollection('users').aggregate ([<br> &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;{$match: {adı: "Herkesi"}}, <br> &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;{$sort: {yaş: -1} }<br>&nbsp;&nbsp;&nbsp;&nbsp;])*) |

## <a name="develop-with-hello-table-api-preview"></a>Tablo API (Önizleme) Hello ile geliştirme

### <a name="terms"></a>Koşullar 
Hello Azure Cosmos DB: Tablo API (Önizleme) yapı 2017 duyurdu tablo desteği için toohello premium teklifi Azure Cosmos DB tarafından başvuruyor. 

Merhaba standart tablo SDK hello mevcut Azure Storage SDK tablodur. 

### <a name="how-can-i-use-hello-new-table-api-preview-offering"></a>Merhaba yenilik tablo API (Önizleme) nasıl kullanabilir miyim? 
Hello Azure Cosmos DB tablo API hello kullanılabilir [Azure portal][azure-portal]. Önce Azure aboneliği için kaydolmanız gerekir. Kaydolan sonra Azure Cosmos DB tablo API hesap tooyour Azure aboneliği ekleyin ve ardından tabloları tooyour hesabı ekleyin. 

Merhaba Önizleme dönemi sırasında zaman [SDK'ları](../cosmos-db/table-sdk-dotnet.md) olan .NET için kullanılabilir, hello tamamlayarak başlayabiliriz [tablo API](../cosmos-db/create-table-dotnet.md) hızlı başlangıç makalesi.

### <a name="do-i-need-a-new-sdk-toouse-hello-table-api-preview"></a>Yeni bir SDK toouse hello tablo API (Önizleme) gerekiyor mu? 
Evet, hello [Windows Azure depolama Premium tablosu (Önizleme) SDK](https://www.nuget.org/packages/WindowsAzure.Storage-PremiumTable) NuGet üzerinde kullanılabilir. Merhaba hakkında ek bilgi sağlanmıştır [Azure Cosmos DB tablo .NET API: indirme ve sürüm notları](https://github.com/Microsoft/azure-docs-pr/cosmos-db/table-sdk-dotnet.md) sayfası. 

### <a name="how-do-i-provide-feedback-about-hello-sdk-or-bugs"></a>Merhaba SDK veya hatalar hakkında geri bildirim nasıl sağlıyor mu?
Geri bildiriminiz herhangi bir yolu aşağıdaki hello paylaşabilirsiniz:

* [Uservoice](https://feedback.azure.com/forums/599062-azure-cosmos-db-table-api)
* [MSDN forumu](https://social.msdn.microsoft.com/forums/azure/en-US/home?forum=AzureDocumentDB)
* [Stackoverflow](http://stackoverflow.com/questions/tagged/azure-cosmosdb)

### <a name="what-is-hello-connection-string-that-i-need-toouse-tooconnect-toohello-table-api-preview"></a>Merhaba bağlantı dizesi toouse tooconnect toohello tablo API (Önizleme) ihtiyacım nedir?
Merhaba bağlantı dizesidir:
```
DefaultEndpointsProtocol=https;AccountName=<AccountNamefromCosmos DB;AccountKey=<FromKeysPaneofCosmosDB>;TableEndpoint=https://<AccountNameFromDocumentDB>.documents.azure.com
```
Merhaba bağlantı dizesi hello Azure Portalı'nda hello anahtarları sayfasından alabilirsiniz. 

### <a name="how-do-i-override-hello-config-settings-for-hello-request-options-in-hello-new-table-api-preview"></a>Hello isteği hello yeni tablo API (Önizleme) seçeneklerinde hello yapılandırma ayarlarını nasıl geçersiz kılma?
Yapılandırma ayarları hakkında daha fazla bilgi için bkz: [Azure Cosmos DB yetenekleri](../cosmos-db/tutorial-develop-table-dotnet.md#azure-cosmos-db-capabilities). Bunları tooapp.config Merhaba istemci uygulaması hello appSettings bölümünde ekleyerek hello ayarlarını değiştirebilirsiniz.

    <appSettings>
        <add key="TableConsistencyLevel" value="Eventual|Strong|Session|BoundedStaleness|ConsistentPrefix"/>
        <add key="TableThroughput" value="<PositiveIntegerValue"/>
        <add key="TableIndexingPolicy" value="<jsonindexdefn>"/>
        <add key="TableUseGatewayMode" value="True|False"/>
        <add key="TablePreferredLocations" value="Location1|Location2|Location3|Location4>"/>....
    </appSettings>


### <a name="are-there-any-changes-for-customers-who-are-using-hello-existing-standard-table-sdk"></a>Merhaba varolan standart tablo SDK kullanan müşteriler için herhangi bir değişiklik var mı?
yok. Merhaba varolan standart tablo SDK kullanan mevcut veya yeni müşteriler için bir değişiklik bulunmamaktadır. 

### <a name="how-do-i-view-table-data-that-is-stored-in-azure-cosmos-db-for-use-with-hello-table-api-review"></a>Azure Cosmos DB'de hello tablo API (revıew) ile kullanılmak üzere depolanır tablo verileri nasıl görüntüleyebilirim? 
Hello Azure portal toobrowse hello verileri kullanabilirsiniz. Merhaba tablo API (Önizleme) kod veya hello sonraki yanıt olarak belirtilen hello araçları de kullanabilirsiniz. 

### <a name="which-tools-work-with-hello-table-api-preview"></a>Hangi Araçlar hello tablo API (Önizleme) ile çalışır? 
Hello Azure Gezgini (0.8.9) daha eski sürümünü kullanabilirsiniz.

Yeni Tablo API (Önizleme) bir bağlantı dizesi belirtilen hello biçiminde önceden destekleyebilir hello esneklik tootake araçlarıyla hello. Tablo araçları listesini hello üzerinde sağlanan [Azure Storage istemci araçları](../storage/common/storage-explorers.md) sayfası. 

### <a name="do-powershell-or-azure-cli-work-with-hello-new-table-api-preview"></a>PowerShell veya Azure CLI hello yeni tablo API ile (Önizleme) çalışıyor mu?
Biz, PowerShell ve Azure CLI tablo API (Önizleme) için tooadd desteği planlayın. 

### <a name="is-hello-concurrency-on-operations-controlled"></a>Merhaba eşzamanlılık denetlenen işlemlerde mi?
Evet, iyimser eşzamanlılık hello ETag mekanizması hello kullanımı aracılığıyla sağlanır. 

### <a name="is-hello-odata-query-model-supported-for-entities"></a>Merhaba OData sorgu modelini varlıklar için desteklenir? 
Evet, OData sorgu ve LINQ sorgusu hello tablo API (Önizleme) destekler. 

### <a name="can-i-connect-toohello-standard-azure-table-and-hello-new-premium-table-api-preview-side-by-side-in-hello-same-application"></a>Toohello standart Azure tablo bağlanıp ve hello yeni premium tablo API (Önizleme) yan yana içinde hello aynı uygulama? 
Evet, iki ayrı işlem örneklerinin hello her işaret eden CloudTableClient oluşturarak bağlanabilir tooits kendi URI hello bağlantı dizesi.

### <a name="how-do-i-migrate-an-existing-azure-table-storage-application-toothis-new-offering"></a>Bir var olan Azure Table depolama uygulama toothis yeni sunum nasıl geçişini?
Merhaba yeni tablo API sunum var olan tablo depolama verileriniz üzerinde kişi tootake avantajlarından [ askcosmosdb@microsoft.com ](mailto:askcosmosdb@microsoft.com). 

### <a name="what-is-hello-roadmap-for-this-service-and-when-will-you-offer-other-standard-table-api-functionality"></a>Bu hizmet için hello yol haritası nedir ve ne zaman diğer standart tablo API işlevleri sunacaktır?
İST doğru ilerlemeden biz planlama tooadd desteği SAS belirteçleri, ServiceContext, istatistikleri, istemci tarafı şifreleme, analiz ve diğer özellikleri Bize geri bildirim üzerinde verebilirsiniz [Uservoice](https://feedback.azure.com/forums/599062-azure-cosmos-db-table-api). 

### <a name="how-is-expansion-of-hello-storage-size-done-for-this-service-if-for-example-i-start-with-n-gb-of-data-and-my-data-will-grow-too1-tb-over-time"></a>Örneğin, t ile başlatırsanız, bu hizmet için yapılan hello depolama boyutunu genişletme nasıl yapıldığını  *n*  GB veri ve verilerimi zamanla too1 TB büyümesine? 
Azure Cosmos DB olduğu tasarlanmış tooprovide hello kullanımını yatay ölçeklendirme aracılığıyla sınırsız depolama. Merhaba hizmet izlemek ve etkili bir şekilde depolama alanınızın artırın. 

### <a name="how-do-i-monitor-hello-table-api-preview-offering"></a>Merhaba tablo API (Önizleme) teklifi nasıl izlerim?
Merhaba tablo API (Önizleme) kullanabilirsiniz **ölçümleri** bölmesinde toomonitor istekleri ve depolama kullanımı. 

### <a name="how-do-i-calculate-hello-throughput-i-require"></a>I gerektiren hello verimlilik nasıl hesaplar?
Merhaba kapasitesini tahmin toocalculate hello hello işlemleri için gerekli olan TableThroughput kullanabilirsiniz. Daha fazla bilgi için bkz: [tahmin istek birimleri ve veri depolama](https://www.documentdb.com/capacityplanner). Genel olarak, JSON olarak, varlığı temsil eder ve işlemleri için hello numaraları sağlayın. 

### <a name="can-i-use-hello-new-table-api-preview-sdk-locally-with-hello-emulator"></a>Merhaba kullanabilirim yeni tablo API (Önizleme) SDK hello öykünücü ile yerel olarak?
Evet, kullanabileceğiniz hello tablo API (Önizleme) kullandığınızda hello yerel öykünücü ile Merhaba yeni SDK. toodownload yeni öykünücüsü, çok Git[yerel geliştirme ve test etme için kullanım hello Azure Cosmos DB öykünücüsü](local-emulator.md). Merhaba app.config StorageConnectionString değerinde toobe gerekir:

```
DefaultEndpointsProtocol=https;AccountName=localhost;AccountKey=C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==;TableEndpoint=https://localhost:8081`. 
```

### <a name="can-my-existing-application-work-with-hello-table-api-preview"></a>Varolan Uygulamam hello tablo API (Önizleme) ile çalışabilir mi? 
Merhaba Hello yüzey alanını yeni tablo API (Önizleme) SDK hello arasında oluşturma, silme, güncelleştirme ve hello .NET API işlemleri sorgu Azure standart tablo varolan hello ile uyumludur. Merhaba tablo API (Önizleme) hem Bölüm anahtarı hem de satır anahtarını gerektirdiğinden satır anahtarı olduğundan emin olun. Biz de tooadd bu hizmet sunumu GA doğru ilerlemeden daha fazla SDK desteği planlayın.

### <a name="do-i-need-toomigrate-my-existing-azure-table-based-applications-toohello-new-sdk-if-i-do-not-want-toouse-hello-table-api-preview-features"></a>My mevcut Azure tablo tabanlı uygulamalar toohello toomigrate zorunda toouse hello tablo API (Önizleme) özellikleri istemiyorsanız, yeni bir SDK?
Hayır, oluşturabilir ve varolan standart tablo varlıkları herhangi bir türde kesintisiz kullanın. Ancak, hello yeni tablo API (Önizleme) kullanmıyorsanız, hello otomatik dizin, hello ek tutarlılık seçeneği ya da genel dağıtım kazancı olmaz. 

### <a name="how-do-i-add-replication-of-hello-data-in-hello-premium-table-api-preview-across-multiple-regions-of-azure"></a>Merhaba veri çoğaltmasını Azure birden çok bölgede hello premium tablo API (Önizleme) içinde nasıl ekleyebilirim?
Hello Azure Cosmos DB portal'ın kullanabilirsiniz [genel çoğaltma ayarları](tutorial-global-distribution-documentdb.md#portal) uygulamanız için uygun tooadd bölgeleri. toodevelop genel olarak dağıtılmış bir uygulama, düşük okuma gecikmesi sağlama hello PreferredLocation bilgileri kümesi toohello yerel bölge uygulamanızla de eklemeniz gerekir. 

### <a name="how-do-i-change-hello-primary-write-region-for-hello-account-in-hello-premium-table-api-preview"></a>Merhaba birincil yazma bölge hello premium tablo API (Önizleme) hello hesap için nasıl değişiyor?
Hello Azure Cosmos DB genel çoğaltma portal bölmesinde tooadd bir bölge kullanın ve ardından toohello gerekli bölge başarısız. Yönergeler için bkz: [bölgeli Azure Cosmos DB hesaplarıyla geliştirme](regional-failover.md). 

### <a name="how-do-i-configure-my-preferred-read-regions-for-low-latency-when-i-distribute-my-data"></a>Verilerimi dağıttığınızda nasıl düşük gecikme süresi için tercih edilen my okuma bölgeler yapılandırırım? 
Merhaba yerel konumdan toohelp okuma hello app.config dosyasında hello PreferredLocation anahtarı kullanın. LocationMode ayarlanmışsa, var olan uygulamalar için hello tablo API (Önizleme) bir hata oluşturur. Tablo API (Önizleme) Hello premium hello app.config dosyasından bu bilgileri alır çünkü bu kodu kaldırın. Daha fazla bilgi için bkz: [Azure Cosmos DB yetenekleri](../cosmos-db/tutorial-develop-table-dotnet.md#azure-cosmos-db-capabilities).

### <a name="how-should-i-think-about-consistency-levels-in-hello-table-api-preview"></a>Merhaba tablo API (Önizleme) de tutarlılık düzeyleri hakkında ne düşünüyorsunuz? 
Azure Cosmos DB iyi reasoned dengelemeler tutarlılık, kullanılabilirlik ve gecikme süresi arasında sağlar. Merhaba tablo düzeyinde hello sağ tutarlılık modelini seçin ve hello veri sorgularken tek tek istekte azure Cosmos DB tooTable API (Önizleme) geliştiriciler, beş tutarlılık düzeyi sunar. Bir istemci bağlandığında, tutarlılık düzeyi belirtebilirsiniz. Merhaba hello TableConsistencyLevel anahtarının değerini hello app.config ayarı aracılığıyla hello düzeyini değiştirebilirsiniz. 

Merhaba tablo API (Önizleme) ile "kendi yazma hello varsayılan olarak oturum tutarlılığı ile okuma" Düşük gecikmeli okur sağlar. Daha fazla bilgi için bkz: [tutarlılık düzeylerini](consistency-levels.md). 

Varsayılan olarak, Azure Table storage bir bölgedeki güçlü tutarlılık ve hello ikincil konumlarda Eventual tutarlılık sağlar. 

### <a name="does-azure-cosmos-db-offer-more-consistency-levels-than-standard-tables"></a>Azure Cosmos DB standart tablolar'den daha fazla tutarlılık düzeyleri sunar?
Evet, nasıl Azure Cosmos DB yapısını hello gelen toobenefit dağıtılmış hakkında daha fazla bilgi için bkz: [tutarlılık düzeylerini](consistency-levels.md). Merhaba tutarlılık düzeylerini garanti sağlamadığı güvenle kullanabilirsiniz. Daha fazla bilgi için bkz: [Azure Cosmos DB yetenekleri](../cosmos-db/tutorial-develop-table-dotnet.md#azure-cosmos-db-capabilities).

### <a name="when-global-distribution-is-enabled-how-long-does-it-take-tooreplicate-hello-data"></a>Genel dağıtım etkinleştirildiğinde, tooreplicate hello verileri ne kadar sürer?
Biz hello veri hello yerel bölgede bulunan işlemi yürütme ve hello veri tooother bölgelerde hemen sağlasa da, milisaniye gönderme. Bu çoğaltma yalnızca hello gidiş dönüş süresini hello datacenter üzerinde (RTT) bağlıdır. toolearn hello genel dağıtım Özelliği Azure Cosmos DB'nin hakkında daha fazla bilgi görmek [Azure Cosmos DB: Azure ile ilgili genel dağıtılmış veritabanı hizmeti](distribute-data-globally.md).

### <a name="can-hello-read-request-consistency-level-be-changed"></a>Merhaba Okuma isteği tutarlılık düzeyi değiştirilebilir mi?
Azure Cosmos DB ile Merhaba tutarlılık düzeyi hello kapsayıcı düzeyinde (Merhaba tablosunda) ayarlayabilirsiniz. Merhaba SDK kullanarak hello app.config dosyasında TableConsistencyLevel anahtarının hello değeri sağlayarak hello düzeyini değiştirebilirsiniz. Merhaba olası değerler şunlardır: güçlü, sınırlanmış eskime durumu, oturum, tutarlı öneki ve Eventual. Daha fazla bilgi için bkz: [veri ince ayarlanabilir tutarlılık düzeyleri Azure Cosmos veritabanı](consistency-levels.md). Merhaba anahtar, hello isteği tutarlılık birden çok hello ayarı Merhaba tablonun en düzeyinde ayarlayamazsınız emin olur. Örneğin, güçlü Eventual hello tablosunda hello tutarlılık düzeyi ve hello isteği tutarlılık düzeyi ayarlanamıyor. 

### <a name="how-does-hello-premium-table-api-preview-account-handle-failover-if-a-region-goes-down"></a>Nasıl bir bölge kullanılamaz hale gelirse hello premium tablo API (Önizleme) hesabı yük devretme ele alıyor? 
Merhaba premium hello Genel dağıtılmış Azure Cosmos DB platformundan tablo API (Önizleme) taşır. Uygulamanız, veri merkezi kesinti dayanabileceği tooensure etkinleştirmek hello Azure Cosmos DB portalında hello hesabı için en az bir daha fazla bölge [bölgeli Azure Cosmos DB hesaplarıyla geliştirme](regional-failover.md). Merhaba portalını kullanarak hello bölge hello önceliğini ayarlayabilirsiniz [bölgeli Azure Cosmos DB hesaplarıyla geliştirme](regional-failover.md). 

Merhaba hesap için istediğiniz ve burada bir yük devretme öncelik sağlama tooby başarısız olabilir kontrol sayıda bölgeleri ekleyebilirsiniz. Elbette, toouse hello veritabanı tooprovide uygulamanın var. çok gerekir. Bunu yaptığınızda, müşterilerinizin kapalı kalma süresi karşılaşmazsınız. Merhaba SDK istemcidir otomatik homing. Diğer bir deyişle, aşağı ve otomatik olarak toohello yeni bölge başarısız hello bölge algılayabilir.

### <a name="is-hello-premium-table-api-preview-enabled-for-backups"></a>Merhaba premium tablo API (Önizleme) yedeklemeler için etkin mi?
Evet, hello premium platformdan hello Azure Cosmos DB'nin yedeklemeler için tablo API (Önizleme) taşır. Yedeklemeleri otomatik olarak yapılır. Daha fazla bilgi için bkz: [çevrimiçi yedekleme ve geri yükleme Azure Cosmos DB ile](online-backup-and-restore.md).

 
### <a name="does-hello-table-api-preview-index-all-attributes-of-an-entity-by-default"></a>Hello tablo API (Önizleme) bir varlığın tüm öznitelikleri varsayılan dizin mu?
Evet, bir varlığın tüm öznitelikleri varsayılan olarak dizine alınır. Daha fazla bilgi için bkz: [Azure Cosmos DB: ilkeleri dizin](indexing-policies.md). 

### <a name="does-this-mean-i-do-not-have-toocreate-multiple-indexes-toosatisfy-hello-queries"></a>Bu ortalama mu birden çok dizin toosatisfy hello sorgu toocreate sahip değil mi? 
Evet, Azure Cosmos DB herhangi bir şema tanımı olmadan tüm özniteliklerin otomatik dizin oluşturma sağlar. Bu Otomasyon geliştiriciler toofocus Merhaba uygulaması yerine dizin oluşturma ve yönetim boşaltır. Daha fazla bilgi için bkz: [Azure Cosmos DB: ilkeleri dizin](indexing-policies.md).

### <a name="can-i-change-hello-indexing-policy"></a>Merhaba dizin oluşturma ilkesini değiştirebilir miyim?
Evet, hello dizin tanımı sağlayarak hello dizin oluşturma ilkesini değiştirebilirsiniz. Daha fazla bilgi için bkz: [Azure Cosmos DB yetenekleri](../cosmos-db/tutorial-develop-table-dotnet.md#azure-cosmos-db-capabilities). Tooproperly ihtiyacınız kodlamak ve çıkış hello ayarları. 

Dize json biçiminde hello app.config dosyasında:
```
{
  "indexingMode": "consistent",
  "automatic": true,
  "includedPaths": [
    {
      "path": "/somepath",
      "indexes": [
        {
          "kind": "Range",
          "dataType": "Number",
          "precision": -1
        },
        {
          "kind": "Range",
          "dataType": "String",
          "precision": -1
        } 
      ]
    }
  ],
  "excludedPaths": 
[
 {
      "path": "/anotherpath"
 }
]
}
```

### <a name="azure-cosmos-db-as-a-platform-seems-toohave-lot-of-capabilities-such-as-sorting-aggregates-hierarchy-and-other-functionality-will-you-be-adding-these-capabilities-toohello-table-api"></a>Bir platform olarak Azure Cosmos DB toohave çok yeteneklerini sıralama, toplamlar, hiyerarşi ve diğer işlevleri gibi görünüyor. Bu özellikleri toohello tablo API ekleme? 
Önizleme'de, hello tablo API hello sağlar. Azure Table depolama işlevleri aynı sorgu. Azure Cosmos DB, sıralama, toplamalar, Jeo-uzamsal sorgu, hiyerarşi ve çok çeşitli yerleşik işlevler de destekler. Biz gelecekteki hizmet güncelleştirmesi hello tablo API ek işlevsellik sağlar. Daha fazla bilgi için bkz: [SQL sorgularını Azure Cosmos DB DocumentDB API için](../documentdb/documentdb-sql-query.md).
 
### <a name="when-should-i-change-tablethroughput-for-hello-table-api-preview"></a>I TableThroughput Merhaba tablo API (Önizleme) değiştirdiğinizde?
Aşağıdaki koşullar hello birini uyguladığında TableThroughput değiştirmeniz gerekir:
* Ayıklama, dönüştürme ve yükleme (ETL) veri gerçekleştiriyorsunuz veya kısa bir sürede tooupload çok miktarda veri istiyor. 
* Daha fazla verimlilik hello arka uçtaki hello kapsayıcısından gerekir. Örneğin, kullanılan hello verimlilik hello sağlanan işleme büyük ve, kısıtlanan bakın. Daha fazla bilgi için bkz: [Azure Cosmos DB kapsayıcıları için kümesi işleme](set-throughput.md).

### <a name="can-i-scale-up-or-scale-down-hello-throughput-of-my-table-api-preview-table"></a>Ölçeği artırma veya miyim my tablo API (Önizleme) tablosunun hello işleme ölçeğini? 
Evet, hello Azure Cosmos DB Portalı'nın ölçek bölmesinde tooscale hello verimlilik kullanabilirsiniz. Daha fazla bilgi için bkz: [kümesi işleme](set-throughput.md).

### <a name="is-a-default-tablethroughput-set-for-newly-provisioned-tables"></a>Varsayılan eylem TableThroughput için yeni sağlanan tabloları kümesi mi?
Evet, app.config aracılığıyla hello TableThroughput geçersiz kılmaz ve önceden oluşturulmuş bir kapsayıcı Azure Cosmos DB'de kullanmayın, hello hizmeti 400 işleme ile bir tablo oluşturur.
 
### <a name="is-there-any-change-of-pricing-for-existing-customers-of-hello-standard-table-api"></a>Merhaba standart tablo API mevcut müşteriler için fiyatlandırma herhangi bir değişiklik var mı?
yok. Var olan standart tablo API müşterileri için fiyatı değişiklik yoktur. 

### <a name="how-is-hello-price-calculated-for-hello-table-api-preview"></a>Merhaba Fiyat tablosu API (Önizleme) hello için nasıl hesaplanır? 
Merhaba fiyat TableThroughput ayrılan hello üzerinde bağlıdır. 

### <a name="how-do-i-handle-any-throttling-on-hello-tables-in-table-api-preview-offering"></a>Azaltma herhangi sunumu hello tablolar üzerinde tablo API (Önizleme) içinde nasıl işleneceğini? 
Merhaba istek oranı hello sağlanan işleme hello kapasitesini hello temel kapsayıcısı için aşarsa, bir hata alırsınız ve hello SDK hello yeniden deneme ilkesi uygulayarak hello çağrısı deneyecek.

### <a name="why-do-i-need-toochoose-a-throughput-apart-from-partitionkey-and-rowkey-tootake-advantage-of-hello-premium-table-api-preview-offering-of-azure-cosmos-db"></a>Toochoose hello premium tablo API (Önizleme) Azure Cosmos DB sunulması PartitionKey ve RowKey tootake avantajlarından dışında bir işleme neden gerekiyor mu?
Merhaba app.config dosyası birinde belirtmezseniz, azure Cosmos DB, kapsayıcı için bir varsayılan işleme ayarlar. 

Azure Cosmos DB, performansı ve gecikme süresi, üst sınır işlemi ile garantileri sağlar. Bu garantisi mümkün olduğunda Hello altyapısı hello kiracının işlemlerini İdaresi uygulayabilirsiniz. TableThroughput ayarlama, üretilen iş ve gecikmeyi, çünkü hello platform bu kapasite ayırır ve işletimsel başarı garanti garanti hello edinmenizi sağlar. 

Merhaba verimlilik belirtimi kullanarak, Özellikler esnek uygulamanızın hello mevsimselliğin toobenefit değiştirmek, hello verimlilik ihtiyaçlarını karşılamak ve maliyet tasarrufu.

### <a name="azure-storage-sdk-has-been-very-inexpensive-for-me-because-i-pay-only-toostore-hello-data-and-i-rarely-query-hello-new-azure-cosmos-db-offering-seems-toobe-charging-me-even-though-i-have-not-performed-a-single-transaction-or-stored-anything-can-you-please-explain"></a>Azure depolama SDK'sı, çünkü yalnızca toostore hello verileri ödeme ve nadiren sorgu benim için çok pahalı olmayan olmuştur. Merhaba yeni Azure Cosmos DB sunum ı değil tek bir işlem gerçekleştirilen veya hiçbir şey depolanan olsa bile bana şarj toobe gibi görünüyor. Lütfen açıklayabilir?

Azure Cosmos DB tasarlanmış toobe garanti kullanılabilirlik, gecikme ve verimlilik için Genel dağıtılmış, SLA tabanlı sistemiyle ' dir. Azure Cosmos veritabanı işleme ayırdığınızda, bu, diğer sistemler hello verimini farklı olarak sağlanır. Azure Cosmos DB müşteriler, ikincil dizinler ve genel dağıtım gibi istediniz ek özellikler sağlar. Merhaba Önizleme dönemi sırasında üretilen iş için iyileştirilmiş bir model sağlıyoruz ve sonuç olarak, biz tooprovide depolama iyileştirilmiş modeli toomeet müşterilerimizin gereksinimlerini planlayın. 

### <a name="i-never-get-a-quota-full-notification-indicating-that-a-partition-is-full-when-i-ingest-data-into-table-storage-with-hello-table-api-preview-i-do-get-this-message-is-this-offering-limiting-me-and-forcing-me-toochange-my-existing-application"></a>Hiçbir zaman (bir bölüm dolu belirten) bir "Kota tam" bildirim alıyorum zaman ı alma veri tablo depolama alanına. Bu ileti Hello tablo API (Önizleme) alıyorum. Varolan Uygulamam bu bana sınırlandırma ve bana toochange zorlama tanıyor mu?

Azure Cosmos DB sınırsız ölçek gecikme süresi, performans, kullanılabilirlik ve tutarlılığı garanti sağlayan bir SLA tabanlı bir sistemdir. Premium performans garanti tooensure veri boyutu ve dizin yönetilebilir ve ölçeklenebilir olduğundan emin olun. Merhaba 10 GB sınırını hello varlıklar ya da bölüm anahtarı başına öğe sayısı harika arama ve sorgu performansı sağladığımız tooensure ' dir. Uygulamanızı Azure Storage için bile iyi ölçeklendirilebilen tooensure öneririz, *değil* bölümde tüm bilgileri depolamak ve onu sorgulama hot bir bölüm oluşturun. 

### <a name="so-partitionkey-and-rowkey-are-still-required-with-hello-new-table-api-preview"></a>PartitionKey ve RowKey hala ile gereken şekilde yeni tablo API (Önizleme) hello? 
Evet. Merhaba tablo API (Önizleme) Hello yüzey alanını hello tablo depolama SDK'sı, benzer toothat olduğundan hello bölüm anahtarı verimli şekilde toodistribute hello veri sağlar. Merhaba satır anahtarı, bu bölüm içinde benzersizdir. Satır anahtar gereksinimlerini toobe mevcut hello ve null olarak olamaz standart SDK hello. RowKey Hello uzunluğu 255 bayttır ve PartitionKey hello uzunluğunu 100 (en kısa sürede toobe too1 KB artan) bayttır. 

### <a name="what-are-hello-error-messages-for-hello-table-api-preview"></a>Merhaba hata iletilerini hello tablo API (Önizleme) nedir?
Bu önizleme hello standart tablo ile uyumlu olduğundan hello hataların çoğu toohello hataları hello standart tablosundan eşleyin. 

### <a name="why-do-i-get-throttled-when-i-try-toocreate-lot-of-tables-one-after-another-in-hello-table-api-preview"></a>Tablolarda birbiri ardından hello tablo API (Önizleme) toocreate miktarda çalıştığınızda neden ı kısıtlanan?
Azure Cosmos DB gecikme süresi, performans, kullanılabilirlik ve tutarlılık sağlayan bir SLA tabanlı bir sistemdir. Sağlanan sistem olduğundan, bu gereksinimleri kaynakları tooguarantee saklı tutar. Hello hızlı tabloları oluşturulmasını oranını algıladı ve daraltma. Tablo oluşturma hello hızında arayın ve tooless dakikada 5'ten daha düşük öneririz. Sağlanan sistem bu hello tablo API (Önizleme) olduğunu unutmayın. Merhaba şu anda, sağlama ve bunun için toopay başlar. 

## <a name="develop-against-hello-graph-api-preview"></a>Grafik API'si (Önizleme) Hello karşı geliştirin
### <a name="how-can-i-apply-hello-functionality-of-graph-api-preview-tooazure-cosmos-db"></a>Grafik API'si (Önizleme) tooAzure Cosmos DB hello işlevselliğini nasıl uygulayabilir mi?
Grafik API'si (Önizleme) bir uzantı kitaplığı tooapply hello işlevlerini kullanabilirsiniz. Bu kitaplık Microsoft Azure grafikleri denir ve NuGet üzerinde kullanılabilir. 

### <a name="it-looks-like-you-support-hello-gremlin-graph-traversal-language-do-you-plan-tooadd-more-forms-of-query"></a>Merhaba Gremlin grafik geçişi dili desteği gibi görünüyor. Daha fazla form sorgusunun tooadd planlıyor musunuz?
Evet, biz tooadd hello gelecekteki sorguda için diğer mekanizmaları planlayın. 

### <a name="how-can-i-use-hello-new-graph-api-preview-offering"></a>Merhaba yenilik grafik API'si (Önizleme) nasıl kullanabilir miyim? 
tooget başlangıç, tam hello [grafik API'si](../cosmos-db/create-graph-dotnet.md) hızlı başlangıç makalesi.

<a id="moving-to-cosmos-db"></a>
## <a name="questions-from-documentdb-customers"></a>DocumentDB müşterilerden sorular
### <a name="why-are-you-moving-tooazure-cosmos-db"></a>TooAzure Cosmos DB neden taşıdığınız? 

Azure Cosmos DB hello sonraki büyük artık genel olarak dağıtılmış ölçekli bulut veritabanlarında ' dir. Bir DocumentDB müşterisi olarak, artık erişim toohello devrim niteliğinde sistem ve Azure Cosmos DB tarafından sunulan özelliklere sahip.

"Proje Microsoft içindeki büyük ölçekli uygulamalar oluşturmanın geliştiriciler tarafından karşılaştığı Floransa" 2010 tooaddress hello kalınan içinde olarak Azure Cosmos DB başlatıldı. Biz bu teknoloji hello ilk nesil 2015 tooAzure geliştiriciler bulunan Azure DocumentDB hello formunda yapılan şekilde genel dağıtılmış uygulamalar oluşturmanın hello zorluklar benzersiz tooMicrosoft değildir. 

O zamandan bu yana, eklenen yeni özellikler artık ve önemli yeni özellikler sunulmuştur. Azure Cosmos DB hello sonucudur. Bu sürümde bir parçası olarak verileriyle, DocumentDB müşterilerin Azure Cosmos DB müşteriler otomatik olarak ve sorunsuz bir şekilde haline gelir. Bu özellikler hello temel veritabanı motoru yanı sıra genel dağıtım, esnek ölçeklenebilirlik ve endüstri lideri, kapsamlı SLA hello alanlarında var. Özellikle, biz hello Azure Cosmos DB veritabanı altyapısı tooefficiently harita tüm popüler veri modelleri, türü sistemleri ve Azure Cosmos DB API'leri toohello temel alınan veri modeli gelişim göstermiştir. 

Merhaba bu çalışmanın geçerli Geliştirici dönük göstergeleri hello yeni desteğidir [Gremlin](../cosmos-db/graph-introduction.md) ve [depolama API'leri tablo](../cosmos-db/table-introduction.md). Ve yalnızca hello başına budur. Biz tooadd diğer popüler API'ler ve yeni veri modelleri ile performans ve küresel ölçekli depolama daha fazla gelişmeleri zamanla planlayın. 

Bu hello DocumentDB çıkışı önemli toopoint olan [SQL dialect](../documentdb/documentdb-sql-query.md) her zaman hello yalnızca biri birçok API'leri temel Azure Cosmos DB destekleyebilmesi bu hello olmuştur. Azure Cosmos DB gibi tam olarak yönetilen bir hizmet kullanan geliştiriciler için hello yalnızca arabirimi toohello hello hello hizmeti tarafından sunulan API'leri hizmetidir. Hiçbir şey gerçekten var olan DocumentDB müşteriler için değiştirir. Azure Cosmos DB içinde tam olarak aynı SQL API, DocumentDB sunar hello alın. Ve şimdi (ve gelecekteki hello), daha önce erişilemez diğer capabilities erişebilirsiniz 

Bizim devam eden iş başka bir göstergeleri, üretilen iş ve depolama genel ve esnek ölçeklenebilirlik sağlamak için genişletilmiş hello temelidir. Biz toohello genel dağıtım alt bazı temel geliştirmeler yapıldı. Merhaba birçok geliştirici dönük özelliklerden biri bir toplam beş iyi tanımlanmış tutarlılık modelleri sağlayan hello tutarlı önek tutarlılık modeli. Biz, bunlar yetişkin birçok daha ilginç özellikleri serbest bırakır. 

### <a name="what-do-i-need-toodo-tooensure-that-my-documentdb-resources-continue-toorun-on-azure-cosmos-db"></a>Ne DocumentDB Kaynaklarım Azure Cosmos DB'de toorun devam toodo tooensure gerekir?

Hiç değişiklik toomake gerekir. DocumentDB kaynakları artık Azure Cosmos DB kaynakları ve bu taşıma meydana geldiğinde kesinti olmadan hello hizmetindeki oluştu.

### <a name="what-changes-do-i-need-toomake-for-my-app-toowork-with-azure-cosmos-db"></a>Değişiklikleri ne Azure Cosmos DB ile my uygulama toowork için toomake kullanmam gerekiyor?

Hiçbir değişiklik toomake vardır. Sınıfları, ad alanları ve NuGet paket adlarının değişmemiştir. Her zaman olduğu gibi hello en son özellikleri ve geliştirmeleri avantajlarından toodate tootake yukarı, SDK'ları tutmanızı öneririz. 

### <a name="whats-changed-in-hello-azure-portal"></a>Hello Azure portal Değiştirilenler?

DocumentDB, artık bir Azure hizmeti olarak hello Portalı'nda görünür. Onun yerine yeni bir Azure Cosmos DB simge hello görüntü aşağıdaki gösterildiği gibi olur. Önce oldukları ve verimlilik, değişiklik tutarlılık düzeyleri ve İzleyici SLA hala ölçeği gibi tüm koleksiyonlar kullanılabilir. Veri Gezgini (Önizleme) Hello özellikleri geliştirilmiştir. Şimdi görüntüleyebilir ve belgeleri düzenlemesine, oluşturma ve sorguları çalıştırmak ve saklı yordamlar, tetikleyiciler ve UDF bir sayfadan hello görüntü aşağıdaki gösterildiği gibi çalışır: 

![Hello Azure Cosmos DB koleksiyonları dikey penceresi](./media/faq/cosmos-db-data-explorer.png)

### <a name="are-there-changes-toopricing"></a>Değişiklikleri toopricing var mı?

Hayır, uygulamanızı Azure Cosmos DB üzerinde çalıştığı hello maliyetini hello aynı önce olduğu gibi.

### <a name="are-there-changes-toohello-slas"></a>Değişiklikleri toohello SLA'ları var mı?

Hayır, SLA'ları için kullanılabilirlik Merhaba, tutarlılık, gecikme ve verimlilik değiştirilmemiştir ve hala hello Portalı'nda görüntülenir. Daha fazla bilgi için bkz: [Azure Cosmos DB SLA](https://azure.microsoft.com/support/legal/sla/cosmos-db/).
   
![Örnek verilerle Yapılacaklar uygulama](./media/faq/azure-cosmosdb-portal-metrics-slas.png)


[azure-portal]: https://portal.azure.com
[query]: documentdb-sql-query.md
