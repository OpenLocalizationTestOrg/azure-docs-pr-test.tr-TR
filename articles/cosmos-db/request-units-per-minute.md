---
title: "Azure CosmosDB: İstek birimleri (RU/m) dakikada | Microsoft Docs"
description: "Dakika başına istek birimleri yararlanarak maliyetini azaltmak öğrenin."
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
ms.openlocfilehash: 72d60d5656ad664e42a848fc9b372cb09e49b888
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="request-units-per-minute-in-azure-cosmos-db"></a>İstek birimleri dakikada Azure Cosmos veritabanı

Azure Cosmos DB hızlı ve tahmin edilebilir performansı ve ölçeği uygulamanızın büyüme sorunsuz bir şekilde birlikte yardımcı olmak için tasarlanmıştır. Her iki saniyede ve dakika başına (RU/m) ayrıntı Cosmos DB kapsayıcısı üzerinde üretilen işi sağlayabilirsiniz. Dakika başına ayrıntı düzeyinde sağlanan aktarım hızı, saniye başına ayrıntı düzeyinde iş yükünde oluşan beklenmedik artışları yönetmek için kullanılır. 

Bu makalede, istek birimi (RU/m) dakikada sağlama nasıl çalıştığını genel bir bakış sağlar. Hedef RU/m sağlama ile aklınızda öngörülebilir bir performans (özellikle işletimsel verilerinizi en üstünde analytics çalıştırmanız gerekiyorsa) öngörülemeyen gereksinimlerini ve spiky iş yükleri çevresinde sağlamaktır. Gönül rahatlığı ile hızlı bir şekilde ölçeklendirebilirsiniz şekilde sağladıkları daha fazla verimlilik tüketen müşterilerimizin olmasını istiyoruz.

Bu makaleyi okuduktan sonra aşağıdaki soruları yanıtlayın mümkün olacaktır:

* Bir istek birimi dakikada nasıl çalışır?
* İstek birimi / dakika ve saniye başına istek birimi arasındaki fark nedir?
* RU/m sağlamak nasıl?
* Hangi senaryosunda ı istek birimi dakikada sağlama düşünün?
* Portal ölçümleri my maliyet ve performansı iyileştirmek için nasıl kullanılacağını?
* İstek türü RU/m bütçenizi tüketebileceği tanımla

## <a name="provisioning-request-units-per-minute-rum"></a>İstek birimleri (RU/m) dakikada sağlama

İkinci bazda (RU/s) Azure Cosmos DB sağladığınızda, üretilen iş o saniye içinde sağlanan kapasite aştı değil, düşük gecikme isteğiniz başarılı garantisi alın. RU/m ile bu dakika içinde isteğiniz başarılı garantisi MINUTE ayrıntı altındadır. Sistemleri emniyeti için ile karşılaştırıldığında, biz elde performans tahmin edilebilir ve üzerinde planlayabilirsiniz emin olun.

Basit works sağlama dakikada yoludur:

* RU/m saatlik ve RU/s ek olarak faturalandırılır. Daha fazla ayrıntı için lütfen Azure Cosmos DB ziyaret [fiyatlandırma sayfası](https://aka.ms/acdbpricing).
* Koleksiyon düzeyinde RU/m etkinleştirilebilir. Bu yapılabilir SDK'ları (Node.js, Java ya da .net) veya portal üzerinden (aynı zamanda MongoDB API iş yükleri içerir)
* RU/m etkinleştirildiğinde her 100 RU/hazırlandı s için sağlanan 1.000 RU/m ayrıca Al (10 x orandır)
* Yalnızca aştınız varsa, RU/m sağlama sırasında belirtilen ikinci bir, bir istek birimi kullanır, bu saniye içinde ikinci sağlama başına
* (UTC) 60 saniye dönemi sona erince sağlama dakika başına refilled
* RU/m, yalnızca bir en fazla 5000 RU/s bölüm başına sağlama koleksiyonlar için etkinleştirilebilir. Üretilen iş gereksinimlerinize ölçeği ve bölüm başına sağlama böyle bir yüksek düzeyde varsa, bir uyarı iletisi alırsınız.

Aşağıda bir müşteri 10kRU/s 100kRU/m ile sağlayabilirsiniz somut bir örnek %73 90 saniyelik süre 10.000 sahip bir koleksiyonun üzerinde aracılığıyla (50kRU/sn) en yoğun RU/s ve sağlanan 100.000 RU/m sağlama karşı Maliyet: kaydediliyor.

* 1 saniye: RU/m bütçe 100.000 sırasında ayarlanır
* 3 ikinci: Bu saniye boyunca istek birimi tüketiminin edildi 11,010 RUs, RU/s sağlama yukarıda 1,010 RUs. Bu nedenle, 1,010 RUs RU/m bütçeden azaltılır. Sonraki 57 saniye cinsinden RU/m bütçe 98,990 RUs mevcuttur
* 29 ikinci: Bu saniye boyunca büyük bir aşırı oldu (> 4 x saniyede sağlama daha yüksek) ve istek birimi tüketiminin 46,920 RUs. 36,920 RUs 92,323 RUs (28 saniye) 55,403 RUs (29 saniye) bırakılan RU/m bütçesi kesinti
* 61st ikinci: RU/m bütçe 100.000 RUs geri ayarlanır.
 
![Azure Cosmos DB sağlama ve tüketimini gösteren grafik](./media/request-units-per-minute/azure-cosmos-db-request-units-per-minute.png)

## <a name="specifying-request-unit-capacity-with-rum"></a>İstek birimi kapasite RU/m ile belirtme

Bir Azure Cosmos DB koleksiyonunu oluştururken numarası belirtin (RU saniye başına) saniyede istek birimlerinin koleksiyon için ayrılmış istiyor. Dakika başına RU eklemek isteyip istemediğinizi de karar verebilirsiniz. Bu, Portal veya SDK yapılabilir. 

### <a name="through-the-portal"></a>Portalı aracılığıyla

Yalnızca etkinleştirme veya dakikada RU devre dışı bırakma bir koleksiyonu sağlamada gerektirir. 

 ![Azure portalında RU/m ayarlama gösteren ekran görüntüsü](./media/request-units-per-minute/azure-cosmos-db-request-unit-per-minute-portal.png)

### <a name="through-the-sdk"></a>SDK aracılığıyla
İlk olarak, bu RU/m yalnızca aşağıdaki SDK'ları için kullanılabilir olduğunu dikkate almak önemlidir:

* .NET 1.14.0
* Java 1.11.0
* Node.js 1.12.0
* Python 2.2.0

.NET SDK kullanarak dakika başına ikinci ve 30.000 isteği birim başına 3000 isteği birim içeren bir koleksiyon oluşturmak için bir kod parçacığı aşağıda verilmiştir:

```csharp
// Create a collection with RU/m enabled
DocumentCollection myCollection = new DocumentCollection();
myCollection.Id = "coll";
myCollection.PartitionKey.Paths.Add("/deviceId");

// Set the throughput to 3,000 request units per second which will give you 30,000 request units per minute as the RU/m budget
await client.CreateDocumentCollectionAsync(
    UriFactory.CreateDatabaseUri("db"),
    myCollection,
    new RequestOptions { OfferThroughput = 3000, OfferEnableRUPerMinuteThroughput = true });
```

.NET SDK kullanarak dakikada sağlama RU olmadan saniye başına 5.000 isteği birim için bir koleksiyon verimini değiştirmek için bir kod parçacığı aşağıda verilmiştir:

```csharp
// Get the current offer
Offer offer = client.CreateOfferQuery()
    .Where(r => r.ResourceLink == collection.SelfLink)    
    .AsEnumerable()
    .SingleOrDefault();

// Set the throughput to 5000 request units per second without RU/m enabled (the last parameter to OfferV2 constructor below)
OfferV2 offerV2 = new OfferV2(offer, 5000, false);

// Now persist these changes to the database by replacing the original resource
await client.ReplaceOfferAsync(offerV2);
```

## <a name="good-fit-scenarios"></a>İyi senaryoları Sığdır

Bu bölümde, dakika başına istek birimleri etkinleştirmek için iyi bir tercihtir senaryoların genel bir bakış sağlar.

**Geliştirme ve Test Ortamı:** iyi sığacak şekilde. Farklı iş yükleri ile uygulamanızı test ediyorsanız bu aşamada geliştirme aşamasında RU/m esneklik sağlayabilir. Sırada [öykünücüsü](local-emulator.md) Azure Cosmos DB test etmek için harika ücretsiz bir araçtır. Ancak bulut ortamında başlatmak istiyorsanız, geçici performans gereksinimlerinizi RU/m ile büyük bir esneklik gerekir. Geliştirme, daha az düşünmeye ilk performans gereksinimleri hakkında daha fazla süre beklemesini. Biz minimum sağlama RU/s ile başlamanızı öneririz ve RU/m etkinleştirin.

**Öngörülemeyen, spiky, dakika ayrıntı düzeyi gerekiyor:** iyi sığacak – tasarrufları: % 25 75. Biz RU/m ve çoğu üretim senaryoları büyük geliştirme olan bu gruba gördünüz. Sisteminiz aynı anda toplu ekleme yaptığında, çalışmakta olan sorgulara varsa birkaç kez bir dakika içinde depo olan bir IOT iş yükü varsa handeling spiky ihtiyaçları için ek kapasite gerekir. Adım adım yaklaşımımız aşağıdaki uygulayarak kaynak gereksinimlerinizi en iyi duruma getirme öneririz.

 ![5 dakikalık ayrıntı isteği tüketimini gösteren grafik](./media/request-units-per-minute/azure-cosmos-db-request-units-per-minute-consumption.png)
 
 *Şekil - RU tüketim Kıyaslama*

**İçiniz rahat:** iyi sığacak – tasarrufları: % 10-20. Bazı durumlarda, yalnızca içiniz rahat olmasını istediğiniz ve olası yükselmeleri ve azaltma hakkında endişelenmeniz değil. Sizin için doğru bir özelliktir. Bu durumda, RU/m etkinleştirme öneririz ve biraz daha düşük, ikinci sağlama başına. Bu durumda yukarıdaki farklı olarak titizlikle, sağlama iyileştirmek denemez. Daha fazla olan bir "Sıfır azaltma" bakış budur.

Adhoc gereksinimleri olan kritik işlemler: Bazı durumlarda yalnızca kritik işlemler RU/m bütçe bütçe açılmıyor şekilde erişim tüketen geçici veya önemli işlemleri daha az izin vermek için öneririz. Aşağıdaki bölümde, kolayca tanımlanabilir.

## <a name="using-the-portal-metrics-to-optimize-cost-and-performance"></a>Maliyet ve performansı en iyi duruma getirmek için portal ölçümleri kullanma

**Önümüzdeki haftalarda size daha fazla üretilen iş gereksinimlerinizi en iyi duruma getirme RUs dakika tüketim izleme geçici içerik geliştireceksiniz.**

Portal ölçümleri karşı RU tüketen normal RU saniye ne kadarının dakika görebilirsiniz. Bu ölçümleri izleme, sağlama en iyi hale getirmenize yardımcı olmalıdır. 

Kendi yararınıza RU/m kullanma hakkında adım adım bir yaklaşım öneririz. Her adımı için bir genel bakış (bunu olabilir saat, gün, veya hatta hafta), iş yükü tam döngüsünün temsil eden RU tüketiminin olmalıdır ve ne sağlamak kullanımı hakkında Öngörüler alın.

Bu yaklaşım arkasında ilkesini, işleme, performans ölçütlerle eşleşen bir sağlama noktasına olabildiğince yakın gibi sağlama olmasını sağlamaktır. 

![5 dakikalık ayrıntı isteği tüketimini gösteren grafik](./media/request-units-per-minute/azure-cosmos-db-request-units-per-minute-adjust-provisioning.png)
 
İş yükü için en iyi sağlama noktası anlamak için anlamanız gerekir:

* Tüketim desenleri: Hayır, kesintili veya sürekli ani? (2 x ortalama) küçük, Orta veya büyük (> 10 x ortalama) ani?
* Daraltılmış istekleri yüzdesi: hızlandırma biraz varsa rahat düşündüğünüz musunuz? Öyleyse, ne kadar? 

Hedefleriniz nelerdir belirledikten sonra en iyi sağlamak için daha yakından almak mümkün olacaktır.

Size yardımcı olmak üzere, sağlama, RU/m tüketime dayanarak en iyi duruma getirme hakkında genel bir kılavuz sağlamak istiyoruz. Bu kılavuz, tüm türdeki iş yüklerini uygulanmaz ancak özel Önizleme bilgisini temel alarak. Biz bu tür temelleri değişebilir olarak size daha fazla bilgi edinin:

|RU/m % kullanımı|RU/m kullanımını derecesini|Sağlama için Önerilen Eylemler|
|---|---|---|
|0-1%|Kullanımı altında|Daha fazla RU/m tüketmeye alt RU/s|
|1-10%|Sağlıklı kullanın|Aynı sağlama düzeyini koruyun|
|Yukarıdaki % 10|Kullanımı|Üzerinde daha az RU/m yararlanmayı RU/s artırın|

## <a name="select-which-operations-can-consume-the-rum-budget"></a>Hangi işlemleri RU/m bütçe tüketebileceği seçin

İsteği düzeyinde, ayrıca etkinleştirebilir/RU/m bütçe işlem türü ne olursa olsun isteğe hizmet devre dışı bırakabilir. Sağlanan normal RUs/sn bütçe tüketilen ve istek RU/m bütçe kullanamayacaklarını, bu istek kısıtlanacak. RU/m verimlilik bütçe etkinleştirilmişse varsayılan olarak, herhangi bir istek RU/m bütçe tarafından sunulur. 

CRUD ve sorgu işlemleri için DocumentDB API kullanarak RU/m bütçe devre dışı bırakmak için bir kod parçacığı aşağıda verilmiştir.

```csharp
// In order to disable any CRUD request for RU/m, set DisableRUPerMinuteUsage to true in RequestOptions
await client.CreateDocumentAsync(
    UriFactory.CreateDocumentCollectionUri("db", "container"),
    new Document { Id = "Cosmos DB" },
    new RequestOptions { DisableRUPerMinuteUsage = true });
// In order to disable any query request for RU/m, set DisableRUPerMinuteOnRequest to true in RequestOptions
FeedOptions feedOptions = new FeedOptions();
feedOptions.DisableRUPerMinuteUsage = true;
var query = client.CreateDocumentQuery<Book>(
    UriFactory.CreateDocumentCollectionUri("db", "container"),
    "select * from c",feedOptions).AsDocumentQuery();
```

## <a name="next-steps"></a>Sonraki adımlar

Bu makalede, biz Azure Cosmos DB nasıl bölümleme çalışır, bölümlenmiş koleksiyonlar nasıl oluşturulur ve uygulamanız için iyi bir bölüm anahtarı nasıl seçim yapabilirsiniz açıklanan.

* Ölçek ve performans ile Azure Cosmos DB testi gerçekleştirin. Bkz: [performans ve ölçek testi Azure Cosmos DB ile](performance-testing.md) bir örnek için.
* Kodlama ile çalışmaya başlama [SDK'ları](documentdb-sdk-dotnet.md) veya [REST API](/rest/api/documentdb/).
* Hakkında bilgi edinin [sağlanan işleme](request-units.md) Azure Cosmos veritabanı 

