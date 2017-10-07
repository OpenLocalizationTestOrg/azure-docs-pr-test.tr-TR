---
title: "Azure CosmosDB: İstek birimleri (RU/m) dakikada | Microsoft Docs"
description: "Nasıl aynı kullanarak tooreduce maliyet istek birimleri dakikada öğrenin."
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 
ms.service: cosmos-db
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: fcc3a92b9788750a2bfba361c3a9cebdb56eee05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="request-units-per-minute-in-azure-cosmos-db"></a>İstek birimleri dakikada Azure Cosmos veritabanı

Azure Cosmos DB hızlı ve tahmin edilebilir performans ve ölçek uygulamanızın büyüme birlikte sorunsuz bir şekilde elde tasarlanmış toohelp ' dir. Her iki saniyede ve dakika başına (RU/m) ayrıntı Cosmos DB kapsayıcısı üzerinde üretilen işi sağlayabilirsiniz. Merhaba dakika başına ayrıntı düzeyi, sağlanan işleme olduğu kullanılan toomanage saniyede bazda gerçekleşen hello iş yükü içindeki beklenmeyen ani. 

Bu makalede hello istek birimi (RU/m) dakikada sağlanmasını nasıl çalıştığını genel bir bakış sağlar. Merhaba RU/m sağlama ile aklınızda tooprovide öngörülebilir bir performans (özellikle toorun analytics işletimsel verilerinizi en üstünde gerekiyorsa) öngörülemeyen gereksinimlerini ve spiky iş yükleri çevresinde hedeftir. Toohave müşterilerimizin içiniz rahat ile hızlı bir şekilde ölçeklendirebilirsiniz şekilde sağladıkları daha fazla hello verimlilik kullanmak istiyoruz.

Bu makaleyi okuduktan sonra aşağıdaki soruları mümkün tooanswer hello olacaktır:

* Bir istek birimi dakikada nasıl çalışır?
* Merhaba istek birimi / dakika ve saniye başına istek birimi arasındaki fark nedir?
* Nasıl tooprovision RU/m?
* Hangi senaryosunda ı istek birimi dakikada sağlama düşünün?
* Nasıl toouse hello portal ölçümleri toooptimize my maliyet ve performansı?
* İstek türü RU/m bütçenizi tüketebileceği tanımla

## <a name="provisioning-request-units-per-minute-rum"></a>İstek birimleri (RU/m) dakikada sağlama

Azure Cosmos DB hello ikinci bazda (RU/s) sağlarken, üretilen iş o saniye içinde sağlanan hello kapasite aştı değil, düşük gecikme isteğiniz başarılı hello garantisi alın. RU/m ile bu dakika içinde isteğiniz başarılı hello garantisi hello MINUTE hello ayrıntı düzeyi altındadır. Toobursting sistemleri, biz hello performans elde tahmin edilebilir olduğundan ve ona planlayabilirsiniz emin olun.

Merhaba şekilde works sağlama dakikada basittir:

* RU/m saatlik ve ayrıca tooRU/s faturalandırılır. Daha fazla ayrıntı için lütfen Azure Cosmos DB ziyaret [fiyatlandırma sayfası](https://aka.ms/acdbpricing).
* Koleksiyon düzeyinde RU/m etkinleştirilebilir. Bu yapılabilir hello SDK (Node.js, Java ya da .net) veya hello portal üzerinden (aynı zamanda MongoDB API iş yükleri içerir)
* RU/m etkinleştirildiğinde her 100 RU/hazırlandı s için sağlanan 1.000 RU/m ayrıca Al (Merhaba orandır 10 x)
* Yalnızca aştınız varsa, RU/m sağlama sırasında belirtilen ikinci bir, bir istek birimi kullanır, bu saniye içinde ikinci sağlama başına
* Bir kez 60 saniye süre (UTC) uçları Merhaba, dakika sağlama başına hello refilled
* RU/m, yalnızca bir en fazla 5000 RU/s bölüm başına sağlama koleksiyonlar için etkinleştirilebilir. Üretilen iş gereksinimlerinize ölçeği ve bölüm başına sağlama böyle bir yüksek düzeyde varsa, bir uyarı iletisi alırsınız.

Aşağıda bir müşteri 10kRU/s 100kRU/m ile sağlayabilirsiniz somut bir örnek %73 90 saniyelik süre 10.000 sahip bir koleksiyonun üzerinde aracılığıyla (50kRU/sn) en yoğun RU/s ve sağlanan 100.000 RU/m sağlama karşı Maliyet: kaydediliyor.

* 1 saniye: hello RU/m bütçe 100.000 ayarlayın
* 3 ikinci: Bu ikinci hello sırasında istek birimi tüketimini edildi 11,010 RUs, hello RU/s sağlama yukarıda 1,010 RUs. Bu nedenle, 1,010 RUs hello RU/m bütçeden azaltılır. 98,990 RUs sonraki 57 saniye cinsinden hello RU/m bütçe hello için kullanılabilir
* 29 ikinci: Bu saniye boyunca büyük bir aşırı oldu (> 4 x saniyede sağlama daha yüksek) ve istek birimi hello tüketimini 46,920 RUs. 403 RUs (29 saniye) 92,323 RUs (28 saniye) too55 bırakılan hello RU/m bütçesi 36,920 RUs kesinti
* 61st ikinci: RU/m bütçe too100, 000 RUs geri ayarlanır.
 
![Merhaba tüketimini gösteren ve Azure Cosmos DB sağlama grafiği](./media/request-units-per-minute/azure-cosmos-db-request-units-per-minute.png)

## <a name="specifying-request-unit-capacity-with-rum"></a>İstek birimi kapasite RU/m ile belirtme

Bir Azure Cosmos DB koleksiyonunu oluştururken hello numarası belirtin (RU saniye başına) saniyede istek birimlerinin hello koleksiyonu için ayrılmış istiyor. Dakika başına tooadd RU isteyip istemediğinizi de karar verebilirsiniz. Bu hello portalı veya hello SDK aracılığıyla yapılabilir. 

### <a name="through-hello-portal"></a>Merhaba Portal

Yalnızca etkinleştirme veya dakikada RU devre dışı bırakma bir koleksiyonu sağlamada gerektirir. 

 ![Gösteren ekran görüntüsü nasıl hello Azure portal'ın tooset RU/m](./media/request-units-per-minute/azure-cosmos-db-request-unit-per-minute-portal.png)

### <a name="through-hello-sdk"></a>Merhaba SDK
İlk olarak, bu önemli toonote RU/m yalnızca SDK'ları aşağıdaki hello için kullanılabilir.

* .NET 1.14.0
* Java 1.11.0
* Node.js 1.12.0
* Python 2.2.0

Merhaba .NET SDK kullanarak dakika başına ikinci ve 30.000 isteği birim başına 3000 isteği birim içeren bir koleksiyon oluşturmak için bir kod parçacığı aşağıda verilmiştir:

```csharp
// Create a collection with RU/m enabled
DocumentCollection myCollection = new DocumentCollection();
myCollection.Id = "coll";
myCollection.PartitionKey.Paths.Add("/deviceId");

// Set hello throughput too3,000 request units per second which will give you 30,000 request units per minute as hello RU/m budget
await client.CreateDocumentCollectionAsync(
    UriFactory.CreateDatabaseUri("db"),
    myCollection,
    new RequestOptions { OfferThroughput = 3000, OfferEnableRUPerMinuteThroughput = true });
```

Bir koleksiyon too5 hello verimini değiştirmek için bir kod parçacığı aşağıda verilmiştir, .NET SDK'sı dakika kullanarak başına RU sağlama olmadan saniyede 000 istek birimleri hello:

```csharp
// Get hello current offer
Offer offer = client.CreateOfferQuery()
    .Where(r => r.ResourceLink == collection.SelfLink)    
    .AsEnumerable()
    .SingleOrDefault();

// Set hello throughput too5000 request units per second without RU/m enabled (hello last parameter tooOfferV2 constructor below)
OfferV2 offerV2 = new OfferV2(offer, 5000, false);

// Now persist these changes toohello database by replacing hello original resource
await client.ReplaceOfferAsync(offerV2);
```

## <a name="good-fit-scenarios"></a>İyi senaryoları Sığdır

Bu bölümde, dakika başına istek birimleri etkinleştirmek için iyi bir tercihtir senaryoların genel bir bakış sağlar.

**Geliştirme ve Test Ortamı:** iyi sığacak şekilde. Farklı iş yükleri ile uygulamanızı test ediyorsanız bu aşamada hello geliştirme aşamasında RU/m hello esneklik sağlayabilir. Merhaba sırasında [öykünücüsü](local-emulator.md) harika ücretsiz aracı tootest Azure Cosmos DB değil. Ancak, bir bulut ortamında toostart istiyorsanız, geçici performans gereksinimlerinizi RU/m ile büyük bir esneklik gerekir. Geliştirme, daha az düşünmeye ilk performans gereksinimleri hakkında daha fazla süre beklemesini. Biz hello minimum RU/s sağlama ile başlamanızı öneririz ve RU/m etkinleştirin.

**Öngörülemeyen, spiky, dakika ayrıntı düzeyi gerekiyor:** iyi sığacak – tasarrufları: % 25 75. Biz RU/m ve çoğu üretim senaryoları büyük geliştirme olan bu gruba gördünüz. Sorguları çalıştırma varsa birkaç kez bir dakika içinde depo olan bir IOT iş yükü varsa, sisteminizi zaman yapar toplu aynı hello Ekle zaman, handeling spiky gereken için ek kapasite gerekir. Adım adım yaklaşımımız aşağıdaki uygulayarak kaynak gereksinimlerinizi en iyi duruma getirme öneririz.

 ![5 dakikalık ayrıntı isteği tüketimini gösteren grafik](./media/request-units-per-minute/azure-cosmos-db-request-units-per-minute-consumption.png)
 
 *Şekil - RU tüketim Kıyaslama*

**İçiniz rahat:** iyi sığacak – tasarrufları: % 10-20. Bazı durumlarda, yalnızca toohave içiniz rahat istiyor ve olası yükselmeleri ve azaltma hakkında endişelenmeniz değil. Sizin için hello sağa bir özelliktir. Bu durumda, RU/m etkinleştirme öneririz ve biraz daha düşük, ikinci sağlama başına. Bu durumda hello öğesinden farklı aynıdır titizlikle, sağlama toooptimize denemez. Daha fazla olan bir "Sıfır azaltma" bakış budur.

Adhoc gereksinimleri olan kritik işlemler: bazen tooonly izin RU/m bütçe hello bütçe açılmıyor şekilde erişim tüketen geçici veya önemli işlemleri daha az kritik işlemler öneririz. Merhaba aşağıdaki bölümde, kolayca tanımlanabilir.

## <a name="using-hello-portal-metrics-toooptimize-cost-and-performance"></a>Merhaba portal ölçümleri toooptimize maliyet ve performansı kullanma

**Merhaba önümüzdeki haftalarda biz, üretilen iş gereken RUs dakika tüketim toooptimize izleme geçici hello içerik daha fazla geliştireceksiniz.**

Merhaba portal ölçümleri karşı RU tüketen normal RU saniye ne kadarının dakika görebilirsiniz. Bu ölçümleri izleme, sağlama en iyi hale getirmenize yardımcı olmalıdır. 

Adım adım bir yaklaşım nasıl öneririz toouse RU/m tooyour avantajı. Her adımı için (Bu olabilir saat, gün, veya hatta hafta), iş yükü tam döngüsünün temsil eden hello RU tüketim genel bir bakış olmalıdır ve ne sağlamak, hello kullanımı Öngörüler alın.

Merhaba bu yaklaşım arkasında olarak, işleme sağlama kapatın, performans ölçütlerle eşleşen noktası sağlama olası tooa toomake ilkesidir. 

![5 dakikalık ayrıntı isteği tüketimini gösteren grafik](./media/request-units-per-minute/azure-cosmos-db-request-units-per-minute-adjust-provisioning.png)
 
toounderstand hello en iyi sağlama noktası iş yükü, toounderstand gerekir:

* Tüketim desenleri: Hayır, kesintili veya sürekli ani? (2 x ortalama) küçük, Orta veya büyük (> 10 x ortalama) ani?
* Daraltılmış istekleri yüzdesi: hızlandırma biraz varsa rahat düşündüğünüz musunuz? Öyleyse, ne kadar? 

Hedefleriniz nelerdir belirledikten sonra mümkün tooget daha yakından toohello en iyi sağlama olacaktır.

tooassist tooprovide nasıl, RU/m tüketime, sağlama toooptimize dayanarak bir genel yönergeler, istiyoruz. Bu kılavuz tooall türdeki iş yüklerini uygulanmaz ancak hello özel Önizleme bilgisini temel alarak. Biz bu tür temelleri değişebilir olarak size daha fazla bilgi edinin:

|RU/m % kullanımı|RU/m kullanımını derecesini|Sağlama için Önerilen Eylemler|
|---|---|---|
|0-1%|Kullanımı altında|Daha fazla RU/m RU/s tooconsume alt|
|1-10%|Sağlıklı kullanın|Merhaba aynı düzeyi sağlamaya devam|
|Yukarıdaki % 10|Kullanımı|Toorely RU/s RU/m üzerinde daha az artırın|

## <a name="select-which-operations-can-consume-hello-rum-budget"></a>Hangi işlemleri hello RU/m bütçe tüketebileceği seçin

İsteği düzeyinde, ayrıca etkinleştirebilir/RU/m bütçe tooserve hello isteğini işlem türü ne olursa olsun devre dışı bırakabilir. Sağlanan normal RUs/sn bütçe tüketilen ve hello isteği hello RU/m bütçe kullanamayacaklarını, bu istek kısıtlanacak. RU/m verimlilik bütçe etkinleştirilmişse varsayılan olarak, herhangi bir istek RU/m bütçe tarafından sunulur. 

CRUD ve sorgu işlemleri için hello DocumentDB API kullanarak RU/m bütçe devre dışı bırakmak için bir kod parçacığı aşağıda verilmiştir.

```csharp
// In order toodisable any CRUD request for RU/m, set DisableRUPerMinuteUsage tootrue in RequestOptions
await client.CreateDocumentAsync(
    UriFactory.CreateDocumentCollectionUri("db", "container"),
    new Document { Id = "Cosmos DB" },
    new RequestOptions { DisableRUPerMinuteUsage = true });
// In order toodisable any query request for RU/m, set DisableRUPerMinuteOnRequest tootrue in RequestOptions
FeedOptions feedOptions = new FeedOptions();
feedOptions.DisableRUPerMinuteUsage = true;
var query = client.CreateDocumentQuery<Book>(
    UriFactory.CreateDocumentCollectionUri("db", "container"),
    "select * from c",feedOptions).AsDocumentQuery();
```

## <a name="next-steps"></a>Sonraki adımlar

Bu makalede, biz Azure Cosmos DB nasıl bölümleme çalışır, bölümlenmiş koleksiyonlar nasıl oluşturulur ve uygulamanız için iyi bir bölüm anahtarı nasıl seçim yapabilirsiniz açıklanan.

* Ölçek ve performans ile Azure Cosmos DB testi gerçekleştirin. Bkz: [performans ve ölçek testi Azure Cosmos DB ile](performance-testing.md) bir örnek için.
* Kodlama Hello ile çalışmaya başlama [SDK'ları](documentdb-sdk-dotnet.md) veya hello [REST API](/rest/api/documentdb/).
* Hakkında bilgi edinin [sağlanan işleme](request-units.md) Azure Cosmos veritabanı 

