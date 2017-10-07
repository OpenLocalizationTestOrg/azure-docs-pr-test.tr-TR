---
title: "aaaRequest birimler ve üretilen işi tahmin etme - Azure Cosmos DB | Microsoft Docs"
description: "Toounderstand, belirtin ve Azure Cosmos veritabanı istek birimi gereksinimlerini tahmin etme hakkında bilgi edinin."
services: cosmos-db
author: mimig1
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: d0a3c310-eb63-4e45-8122-b7724095c32f
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: 13c4e7aeb6222fa14ef982e238716e15a0159fd5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="request-units-in-azure-cosmos-db"></a>Azure Cosmos DB birimlerinde isteği
Artık kullanılabilir: Azure Cosmos DB [istek birimi hesaplayıcı](https://www.documentdb.com/capacityplanner). Daha fazla bilgi edinin [, üretilen iş gerektiğini tahmin etme](request-units.md#estimating-throughput-needs).

![Üretilen iş hesaplayıcısı][5]

## <a name="introduction"></a>Giriş
[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) Microsoft'un Genel dağıtılmış birden çok model veritabanıdır. Azure Cosmos DB ile toorent sanal makineye sahip olmayan, yazılım dağıtma veya veritabanlarını izleyin. Azure Cosmos DB işletilen ve sürekli olarak Microsoft üst mühendisleri toodeliver world sınıfı kullanılabilirliği, performansı ve veri koruma tarafından izlenir. Tercih ettiğiniz API'lerini kullanarak verilerinize erişebilir [DocumentDB SQL](documentdb-sql-query.md) (belge), MongoDB (belge) [Azure Table Storage](https://azure.microsoft.com/services/storage/tables/) (anahtar-değer) ve [Gremlin](https://tinkerpop.apache.org/gremlin.html) (tüm grafik) yerel olarak desteklenir. Azure Cosmos DB Hello para hello istek birimi (RU) birimidir. RUs ile tooreserve okuma/yazma kapasiteleri veya sağlama CPU, bellek ve IOPS gerekmez.

Azure Cosmos DB Basit okuma arasında değişen farklı işlemlerle API'lerini destekler ve grafik sorguları toocomplex yazar. Tüm istekleri eşit olduğundan, normalleştirilmiş bir miktar atanan **istek birimleri** hello hesaplama gerekli tooserve hello isteği miktarına göre. bir işlem için istek birim Hello Sayısı belirleyici ve bir yanıt üstbilgisi aracılığıyla Azure Cosmos veritabanı herhangi bir işlem tarafından kullanılan istek birimlerinin sayısı hello izleyebilirsiniz. 

tooprovide tahmin edilebilir performans, tooreserve işleme birimi 100 RU/saniye gerekir. 

Bu makaleyi okuduktan sonra aşağıdaki soruları mümkün tooanswer hello olması:  

* Hangi birimleri istemek ve ücretleri isteği?
* Bir koleksiyon için istek birim kapasitesi nasıl belirteceğinizi?
* My uygulamanın istek birimi gereken nasıl tahmin?
* Bir koleksiyon için istek birim kapasitesi aşmanız durumunda ne olur?

Azure Cosmos DB çok model bir veritabanıdır, biz tooa koleksiyonu/belge belge API, grafik API'si için bir grafik/düğümü ve tablo API için bir tablo/varlık başvurur önemli toonote olur. Üretilen iş bu belge size kapsayıcı/öğe toohello kavramlarını generalize.

## <a name="request-units-and-request-charges"></a>İstek birimleri ve istek ücretleri
Azure Cosmos DB tarafından hızlı ve tahmin edilebilir performans sunar *ayırma* kaynakları toosatisfy uygulamanızın işleme gerekir.  Uygulama yüklemek ve zaman içinde desenleri değişiklik erişmek için Azure Cosmos DB tooeasily artış izin verir veya ayrılmış işleme kullanılabilir tooyour uygulama hello miktarını azaltın.

Azure Cosmos DB ile ayrılmış işleme saniyede işlediği istek birimler cinsinden belirtilir. İstek birimleri yapabildiği verimlilik para birimi olarak düşünebilirsiniz, *yedek* miktardaki kullanılabilir tooyour uygulama başına saniye başına istek birimleri garanti.  Azure Cosmos - bir belge yazma, bir belge güncelleştirme bir sorgu gerçekleştirme - DB her bir işlemin CPU, bellek ve IOPS tüketir.  Diğer bir deyişle, her işlemi uygulanan bir *isteği ücret*, içinde ifade *istek birimleri*.  İstek birimi ücretleri, uygulamanızın işleme gereksinimleri etkiler hello Etkenler anlama, toorun uygulamanızın maliyet etkili bir şekilde mümkün olduğunca sağlar. Merhaba sorgu Gezgini de, bir sorgu harika aracı tootest hello çekirdek olur.

İstek birimleri ve Azure Cosmos DB tahmin edilebilir performansla Aravind Ramachandran burada açıklanmaktadır video, aşağıdaki hello izleyerek çalışmaya başlamanızı öneririz.

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Predictable-Performance-with-DocumentDB/player]
> 
> 

## <a name="specifying-request-unit-capacity-in-azure-cosmos-db"></a>İstek birimi kapasite Azure Cosmos DB'de belirtme
Yeni koleksiyon, tablo veya grafik başlatırken hello numarası belirtin (RU saniye başına) saniyede istek birimlerinin ayrılmış istiyor. Hello üzerinde sağlanan işleme bağlı olarak, Azure Cosmos DB fiziksel bölümleri toohost koleksiyonunuzu ayırır ve bölmelerini/veri bölümler, büyüdükçe rebalances.

Bir koleksiyon 2.500 istek birimleri ile sağlanan ya da daha yüksek olduğunda bir bölüm anahtarı toobe belirtilen Azure Cosmos DB gerektirir. Bölüm anahtarı da gerekli tooscale koleksiyonunuzun işleme hello gelecekteki 2.500 istek birimleri ötesinde olan. Bu nedenle, tooconfigure önerilir bir [bölüm anahtarı](partition-data.md) ilk işleme bakılmaksızın bir kapsayıcı oluştururken. Verilerinizin birden çok bölüm arasında bölme toobe olabilir olduğundan, gerekli toopick yüksek kardinalite (100 toomillions farklı değerlerin) vardır ve böylece tablo/koleksiyonu/grafik ve istekleri Azure Cosmos DB tarafından hep genişletilebilir bir bölüm anahtarı kalır. 

> [!NOTE]
> Bölüm anahtarı mantıksal bir sınır ve fiziksel bir tane ' dir. Bu nedenle, toolimit hello farklı bölüm anahtar değerlerinin sayısı gerekmez. Aslında daha iyi toohave daha farklı olduğundan daha fazla yük dengeleme seçeneklerini Azure Cosmos DB olduğu gibi daha az anahtar değerden bölüm.

3, 000'ile bir koleksiyon oluşturmak için bir kod parçacığı aşağıda verilmiştir .NET SDK kullanarak saniye başına birim hello isteği:

```csharp
DocumentCollection myCollection = new DocumentCollection();
myCollection.Id = "coll";
myCollection.PartitionKey.Paths.Add("/deviceId");

await client.CreateDocumentCollectionAsync(
    UriFactory.CreateDatabaseUri("db"),
    myCollection,
    new RequestOptions { OfferThroughput = 3000 });
```

Azure Cosmos DB akışındaki bir ayırma modeli çalıştırır. Diğer bir deyişle, üretilen iş hello miktarı için faturalandırılır *ayrılmış*ne olursa olsun, üretilen işi ne kadarının etkin olduğundan, *kullanılan*. SDK'ları ile ayrılmış RUs miktarı, kolayca ölçeklendirilebilir yukarı ve aşağı uygulamanızın yük, veri ve kullanım desenlerini değiştikçe hello veya hello kullanarak [Azure Portal](https://portal.azure.com).

Her koleksiyon/tablo/grafik eşlendi tooan `Offer` kaynak hello sağlanan işleme hakkındaki meta verileri olan Azure Cosmos veritabanı. Kapsayıcı için ilgili teklif kaynak hello bakarak sonra hello yeni işleme değeri ile güncelleştirme tarafından ayrılan hello verimlilik değiştirebilirsiniz. Bir koleksiyon too5 hello verimini değiştirmek için bir kod parçacığı aşağıda verilmiştir, .NET SDK kullanarak saniye başına istek birimleri 000 hello:

```csharp
// Fetch hello resource toobe updated
Offer offer = client.CreateOfferQuery()
                .Where(r => r.ResourceLink == collection.SelfLink)    
                .AsEnumerable()
                .SingleOrDefault();

// Set hello throughput too5000 request units per second
offer = new OfferV2(offer, 5000);

// Now persist these changes toohello database by replacing hello original resource
await client.ReplaceOfferAsync(offer);
```

Merhaba verimlilik değiştirdiğinizde, kapsayıcının etkisi toohello kullanılabilirliği yok. Genellikle hello yeni ayrılmış işleme hello yeni işleme, uygulama üzerinde saniye içinde etkili olur.

## <a name="request-unit-considerations"></a>İstek birimi konuları
İstek birimleri tooreserve Azure Cosmos DB kapsayıcısı için Hello sayısını tahmin etme dikkate değişkenleri aşağıdaki önemli tootake hello olur:

* **Öğe boyutunu**. Boyutu artar hello birimleri tooread tüketilen veya hello veri yazma da artacaktır.
* **Madde özellik sayısı**. Tüm özelliklerin, bir belge/düğümü/ntity hello özellik sayısı arttıkça artıracaktır hello tüketilen birim toowrite varsayılan dizin varsayılır.
* **Veri tutarlılığı**. Veri tutarlılık düzeylerini güçlü veya sınırlanmış eskime durumu kullanırken, ek birimler tüketilen tooread öğeleri olacaktır.
* **Dizin oluşturulmuş özellikleri**. Bir dizin İlkesi her kapsayıcısı üzerinde varsayılan olarak hangi özellikleri dizinlenir belirler. Dizinli Özellikler hello sayısını sınırlayarak veya yavaş dizin etkinleştirerek, istek birimi tüketimini azaltabilirsiniz.
* **Belge dizine**. Bazı öğelerinizi değil tooindex seçerseniz, her bir öğeyi otomatik olarak dizine varsayılan olarak, daha az istek birimleri tüketir.
* **Sorgu desenleri**. bir sorgu Hello karmaşıklığını kaç tane istek birimleri için bir işlem tüketilen etkiler. koşulları Hello sayısı, hello koşulları projeksiyonları, UDF'ler sayısı ve tüm hello maliyetini etkilemek hello kaynak veri kümesinin hello boyutu yapısını işlemleri sorgu.
* **Komut dosyası kullanımı**.  Sorguları olarak gerçekleştirilen hello işlemler hello kapsamına bağlı istek birimleri saklı yordamları ve Tetikleyicileri tüketir. Uygulamanızı geliştirirken hello isteği ücret incelemek üstbilgi toobetter anlamak her işlemi isteği birim kapasitesi nasıl tüketilmesine neden olabilir.

## <a name="estimating-throughput-needs"></a>Üretilen iş gereksinimlerini tahmin etme
Bir istek birimi istek maliyet işleme normalleştirilmiş ölçüsüdür. Bir tek istek birimi öğesi 10 benzersiz özellik değerlerini (Sistem özellikleri dışında) oluşan tek 1 bb hello işleme gerekli kapasite tooread (aracılığıyla kendi bağlantısını veya kimliği) temsil eder. İstek toocreate (Ekle) değiştirmek veya aynı öğesi daha hello hizmetinden işleme tüketir hello silin ve böylece daha fazla birim isteyin.   

> [!NOTE]
> 1 isteği biriminin Hello temel öğesi karşılık gelen tooa basit bir 1 KB için kendi bağlantısını veya hello öğenin kimliği alın.
> 
> 

Örneğin, kaç tane isteği gösteren bir tablo İşte birimleri tooprovision boyutlarında üç farklı öğe (1KB, 4KB ve 64KB) ve iki farklı performans düzeyleri (500 Okuma/saniye 100 yazma/saniye ve 500 Okuma/saniye + 500 yazma/saniye). Merhaba veri tutarlılığını oturumunda yapılandırılmış ve dizin oluşturma ilkesi hello tooNone ayarlayın.

<table border="0" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td valign="top"><p><strong>Öğesi boyutu</strong></p></td>
            <td valign="top"><p><strong>Okuma/saniye</strong></p></td>
            <td valign="top"><p><strong>Yazma/saniye</strong></p></td>
            <td valign="top"><p><strong>İstek birimleri</strong></p></td>
        </tr>
        <tr>
            <td valign="top"><p>1 KB</p></td>
            <td valign="top"><p>500</p></td>
            <td valign="top"><p>100</p></td>
            <td valign="top"><p>(500 * 1) + (100 * 5) = 1.000 RU/s</p></td>
        </tr>
        <tr>
            <td valign="top"><p>1 KB</p></td>
            <td valign="top"><p>500</p></td>
            <td valign="top"><p>500</p></td>
            <td valign="top"><p>(500 * 1) + (500 * 5) = 3000 RU/s</p></td>
        </tr>
        <tr>
            <td valign="top"><p>4 KB</p></td>
            <td valign="top"><p>500</p></td>
            <td valign="top"><p>100</p></td>
            <td valign="top"><p>(500 * 1,3) + (100 * 7) = 1,350 RU/s</p></td>
        </tr>
        <tr>
            <td valign="top"><p>4 KB</p></td>
            <td valign="top"><p>500</p></td>
            <td valign="top"><p>500</p></td>
            <td valign="top"><p>(500 * 1,3) + (500 * 7) = 4,150 RU/s</p></td>
        </tr>
        <tr>
            <td valign="top"><p>64 KB</p></td>
            <td valign="top"><p>500</p></td>
            <td valign="top"><p>100</p></td>
            <td valign="top"><p>(500 * 10) + (100 * 48) = 9,800 RU/s</p></td>
        </tr>
        <tr>
            <td valign="top"><p>64 KB</p></td>
            <td valign="top"><p>500</p></td>
            <td valign="top"><p>500</p></td>
            <td valign="top"><p>(500 * 10) + (500 * 48) = 29,000 RU/s</p></td>
        </tr>
    </tbody>
</table>

### <a name="use-hello-request-unit-calculator"></a>Merhaba istek birimi hesaplayıcı kullanın
İnce toohelp müşteriler kendi verimlilik tahminler ince ayar, bir web tabanlı [istek birimi hesaplayıcı](https://www.documentdb.com/capacityplanner) toohelp tahmin hello isteği birim gereksinimleri dahil olmak üzere, normal işlemleri için:

* (Yazar) öğesi oluşturur
* Öğe okur
* Öğeyi siler
* Öğesi güncelleştirmeleri

Merhaba aracı sağladığınız hello örnek öğeleri temel alan veri depolama gereksinimlerini tahmin etmek için destek de içerir.

Merhaba aracını kullanarak basit bir işlemdir:

1. Bir veya daha fazla temsilcisi öğeleri karşıya yükleyin.
   
    ![Öğeleri toohello istek birimi hesaplayıcı karşıya yükle][2]
2. tooestimate veri depolama gereksinimleri hello toplam sayısını girin öğelerinin toostore bekler.
3. Girin hello öğe sayısı oluşturma, okuma, güncelleştirme ve silme işlemleri (bir saniye başına temelinde) gerektirir. tooestimate hello istek birimi ücretleri öğesi güncelleştirme işlemlerinin tipik alan güncelleştirmeleri içeren yukarıdaki adım 1'den hello örnek öğenin bir kopyasını yükleyin.  Örneğin, öğesi güncelleştirmeler genellikle lastLogin ve userVisits adlı iki özellikleri değiştirin ve ardından sadece hello örnek öğesi kopyalayın, bu iki özellik için hello değerleri güncelleştirmek ve kopyalanan hello öğesi yükleyin.
   
    ![Üretilen iş gereksinimleri hello istek birimi hesaplayıcı girin][3]
4. Tıklatın hesaplamak ve hello sonuçlarını inceleyin.
   
    ![Birim hesaplayıcı sonuçları isteği][4]

> [!NOTE]
> Dizinli Özellikler boyutu ve hello sayısı bakımından önemli ölçüde farklılık gösterecektir öğesi türleri varsa, her bir örnek karşıya *türü* tipik öğesi toohello, hello sonuçları hesaplamak ve aracı.
> 
> 

### <a name="use-hello-azure-cosmos-db-request-charge-response-header"></a>Hello Azure Cosmos DB istek ücret yanıt üstbilgisi kullanın
Bir özel üst bilgi hello Azure Cosmos DB hizmet gelen her yanıtı içerir (`x-ms-request-charge`) hello istek için harcanan hello istek birimleri içerir. Bu üst ayrıca Azure Cosmos DB SDK'ları hello erişilebilir. Hello .NET SDK'sı, RequestCharge hello ResourceResponse nesnesinin bir özelliğidir.  Sorgular için hello Azure portalında Azure Cosmos DB sorgu Gezgini hello yürütülen sorgular için istek ücret bilgileri sağlar.

![Merhaba sorgu Gezgini RU ücretlere inceleniyor][1]

Bu aklınızda uygulamanızın gerektirdiği ayrılmış işleme hello miktarı tahmin etmek için bir yöntem toorecord hello istek birimi ücret uygulamanız tarafından kullanılan bir temsili öğesi karşı normal işlemleri çalıştırılması ile ilişkili olan ve ardından işlem Hello sayısını tahmin etme saniyede gerçekleştirme beklenir.  Emin toomeasure olması ve tipik sorgular ve Azure Cosmos DB komut dosyası kullanımı da içerir.

> [!NOTE]
> Dizinli Özellikler boyutu ve hello sayısı bakımından önemli ölçüde farklılık gösterecektir öğesi türleri varsa, her ilişkilendirilmiş hello geçerli işlemi istek birimi ücret kayıt *türü* tipik öğesi.
> 
> 

Örneğin:

1. Kayıt (ekleme) oluşturma hello istek birimi ücret tipik bir öğe. 
2. Tipik bir öğe okuma kayıt hello istek birimi gider.
3. Tipik bir öğesi güncelleştirme kayıt hello istek birimi gider.
4. Kayıt hello istek birimi gider tipik, ortak öğesi sorgular.
5. Tüm özel komut dosyalarını (saklı yordamlar, Tetikleyiciler, kullanıcı tanımlı işlevler), kayıt hello istek birimi ücret Hello uygulama tarafından kullanılabilir
6. Tahmini hello işlemlerinin sayısı verilen birimleri saniyede toorun düşündüğünüz hello gerekli isteği hesaplayın.

### <a id="GetLastRequestStatistics"></a>API MongoDB'ın GetLastRequestStatistics komutu için kullanın
API MongoDB için özel bir komut destekler *getLastRequestStatistics*, belirtilen işlemleri için hello isteği ücret alma.

Örneğin, hello Mongo kabuğunu, tooverify hello isteği Ücret için istediğiniz hello işlemi yürütün.
```
> db.sample.find()
```

Ardından, hello bağlamını *getLastRequestStatistics*.
```
> db.runCommand({getLastRequestStatistics: 1})
{
    "_t": "GetRequestStatisticsResponse",
    "ok": 1,
    "CommandName": "OP_QUERY",
    "RequestCharge": 2.48,
    "RequestDurationInMilliSeconds" : 4.0048
}
```

Bu aklınızda uygulamanızın gerektirdiği ayrılmış işleme hello miktarı tahmin etmek için bir yöntem toorecord hello istek birimi ücret uygulamanız tarafından kullanılan bir temsili öğesi karşı normal işlemleri çalıştırılması ile ilişkili olan ve ardından işlem Hello sayısını tahmin etme saniyede gerçekleştirme beklenir.

> [!NOTE]
> Dizinli Özellikler boyutu ve hello sayısı bakımından önemli ölçüde farklılık gösterecektir öğesi türleri varsa, her ilişkilendirilmiş hello geçerli işlemi istek birimi ücret kayıt *türü* tipik öğesi.
> 
> 

## <a name="use-api-for-mongodbs-portal-metrics"></a>API MongoDB'ın portal ölçümleri kullanın
İstek birimi iyi tahmini ücretlendirilen API'nize MongoDB veritabanı toouse hello için en basit yolu tooget hello [Azure portal](https://portal.azure.com) ölçümleri. Merhaba ile *istek sayısı* ve *isteği ücret* grafikler, alabilirsiniz her işlem kaç tane istek birimlerinin tahmin harcayan ve kaç tane istek birimleri göreli tooone tüketen başka bir.

![API MongoDB portal ölçümleri için][6]

## <a name="a-request-unit-estimation-example"></a>Bir istek birimi tahmin örneği
~ 1 KB belge aşağıdaki hello göz önünde bulundurun:

```json
{
 "id": "08259",
  "description": "Cereals ready-to-eat, KELLOGG, KELLOGG'S CRISPIX",
  "tags": [
    {
      "name": "cereals ready-to-eat"
    },
    {
      "name": "kellogg"
    },
    {
      "name": "kellogg's crispix"
    }
  ],
  "version": 1,
  "commonName": "Includes USDA Commodity B855",
  "manufacturerName": "Kellogg, Co.",
  "isFromSurvey": false,
  "foodGroup": "Breakfast Cereals",
  "nutrients": [
    {
      "id": "262",
      "description": "Caffeine",
      "nutritionValue": 0,
      "units": "mg"
    },
    {
      "id": "307",
      "description": "Sodium, Na",
      "nutritionValue": 611,
      "units": "mg"
    },
    {
      "id": "309",
      "description": "Zinc, Zn",
      "nutritionValue": 5.2,
      "units": "mg"
    }
  ],
  "servings": [
    {
      "amount": 1,
      "description": "cup (1 NLEA serving)",
      "weightInGrams": 29
    }
  ]
}
```

> [!NOTE]
> Hello sistem yukarıdaki hello belgenin boyutu 1 KB biraz değerinden hesaplanır şekilde belgeler Azure Cosmos DB'de küçültülmüş.
> 
> 

Merhaba aşağıdaki tabloda yaklaşık istek birimi ücretleri bu öğeyi genel işlemler için gösterilir (Merhaba yaklaşık istek birimi ücret varsayar hello hesap tutarlılık düzeyi çok ayarlanır "Oturum" ve tüm öğeler otomatik olarak dizine):

| İşlem | İstek birimi ücret |
| --- | --- |
| Öğesi oluşturma |~ 15 RU |
| Öğe Okuma |~ 1 RU |
| Sorgu öğesi kimliği |~2.5 RU |

Ayrıca, bu tabloda yaklaşık istek birimi ücretleri hello uygulamada kullanılan tipik sorguları için gösterilir:

| Sorgu | İstek birimi ücret | Döndürülen öğe sayısı |
| --- | --- | --- |
| Kimliğe göre yemek seçin |~2.5 RU |1 |
| Üretici tarafından foods seçin |~ 7 RU |7 |
| Yemek grup ve sipariş ağırlığa göre seçin |~ 70 RU |100 |
| Üst 10 foods yemek grubunda seçin |~ 10 RU |10 |

> [!NOTE]
> RU ücretleri hello döndürülen öğe sayısını göre farklılık gösterir.
> 
> 

Bu bilgi ile biz hello RU gereksinimleri işlemler ve saniye başına bekliyoruz sorgular, bu verilen uygulama hello sayısını tahmin edebilirsiniz:

| İşlem/sorgu | Saniye başına tahmini sayısı | Gerekli RUs |
| --- | --- | --- |
| Öğesi oluşturma |10 |150 |
| Öğe Okuma |100 |100 |
| Üretici tarafından foods seçin |25 |175 |
| Yemek gruplandırma ölçütü seçin |10 |700 |
| İlk 10 seçin |15 |150 toplam |

Bu durumda, bir ortalama verimi gereksinimi 1,275 RU/s bekliyoruz.  100 en yakın toohello Yukarı yuvarlama, biz 1300 RU/s Bu uygulamanın koleksiyon için hazırlamanız.

## <a id="RequestRateTooLarge"></a>Azure Cosmos DB aşan ayrılmış işleme sınırları
İstek birimi tüketim Hello bütçe boşsa, saniye başına oranı olarak değerlendirilir, geri çağırma. Hello aşan uygulamalar için bir kapsayıcı için sağlanan istek birimi hızı istekleri hello oranı ayrılmış hello düzeyin altına düşene kadar toothat koleksiyonu kısıtlanacak. Bir kısıtlama oluştuğunda hello sunucu erken önlem hello istekle RequestRateTooLargeException (HTTP durum kodu 429) ve kullanıcı hello milisaniye cinsinden süre hello miktarını önce beklemesi gereken x-ms-yeniden deneme-sonra-ms üstbilgi dönüş hello belirten sona erer reattempting hello isteği.

    HTTP Status 429
    Status Line: RequestRateTooLarge
    x-ms-retry-after-ms :100

Merhaba .NET İstemci SDK'sını ve LINQ sorgularını sonra hiçbir zaman gereken bu özel durumla toodeal hello geçerli sürümü hello .NET İstemci SDK'sı, bu yanıt örtük olarak yakalar gibi hello zamanı çoğu kullanıyorsanız, sunucu tarafından belirtilen yeniden deneme sonrasında, üst gizliliğinize hello ve yeniden deneme hello isteği. Hesabınızı eşzamanlı olarak birden çok istemci tarafından erişilen sürece hello sonraki yeniden deneme işlemi başarılı olur.

Merhaba istek hızı işletim üst üste birden fazla istemciniz varsa hello varsayılan yeniden deneme davranışı değil yeterli ve hello istemci durum kodu 429 toohello uygulama ile bir DocumentClientException atar. Bu gibi durumlarda, yeniden deneme davranışı ve yordamları işleme veya hello kapsayıcısı için hello ayrılmış verim artar, uygulamanızın hata mantığının işleme düşünebilirsiniz.

## <a id="RequestRateTooLargeAPIforMongoDB"></a>API MongoDB için aşan ayrılmış işleme sınırları
Merhaba oranı ayrılmış hello düzeyin altına düşene kadar bir koleksiyon için sağlanan hello istek birimleri aşan uygulamaları kısıtlanacak. Bir azaltma oluştuğunda hello arka uç hello istekle erken önlem sona erer bir *16500* hata kodu - *çok fazla istek*. Varsayılan olarak, API MongoDB için otomatik olarak dönmeden önce too10 kez yukarı yeniden deneyecek bir *çok fazla istek* hata kodu. Birçok alıyorsanız *çok fazla istek* hata kodları, uygulamanızın hata yordamları işlemedeki ekleme ya da yeniden deneme davranışı dikkate veya [hello ayrılmış işleme hello koleksiyonuartırma](set-throughput.md).

## <a name="next-steps"></a>Sonraki adımlar
ayrılmış işleme ile Azure Cosmos DB veritabanları hakkında daha fazla toolearn bu kaynakları araştırın:

* [Cosmos DB Azure fiyatlandırması](https://azure.microsoft.com/pricing/details/cosmos-db/)
* [Azure Cosmos veritabanı veri bölümlendirme](partition-data.md)

toolearn Azure Cosmos DB hakkında daha fazla bilgi görmek hello Azure Cosmos DB [belgelerine](https://azure.microsoft.com/documentation/services/cosmos-db/). 

Ölçek ve performans testi Azure Cosmos DB ile kullanmaya tooget bkz [performans ve ölçek testi Azure Cosmos DB ile](performance-testing.md).

[1]: ./media/request-units/queryexplorer.png 
[2]: ./media/request-units/RUEstimatorUpload.png
[3]: ./media/request-units/RUEstimatorDocuments.png
[4]: ./media/request-units/RUEstimatorResults.png
[5]: ./media/request-units/RUCalculator2.png
[6]: ./media/request-units/api-for-mongodb-metrics.png
