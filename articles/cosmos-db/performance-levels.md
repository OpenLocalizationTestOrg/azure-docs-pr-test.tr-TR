---
title: "aaaDocumentDB API performans düzeyleri | Microsoft Docs"
description: "Nasıl DocumentDB API performans düzeyleri, kapsayıcı başına temelinde tooreserve verimlilik etkinleştirme hakkında bilgi edinin."
services: cosmos-db
author: mimig1
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: 7dc21c71-47e2-4e06-aa21-e84af52866f4
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/24/2017
ms.author: mimig
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 716bc11ae238dbb0feebf004ed8d5f8a7515ec6f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="retiring-hello-s1-s2-and-s3-performance-levels"></a>Merhaba S1, S2 ve S3 performans düzeyleri devre dışı bırakma

> [!IMPORTANT] 
> Bu makalede açıklanan hello S1, S2 ve S3 performans düzeyleri kullanımdan kaldırılacak ve artık yeni DocumentDB API hesapları için kullanılabilir.
>

Bu makalede, S1, S2 ve S3 performans düzeyleri genel bir bakış sağlar ve bu performans düzeyleri kullanmak hello koleksiyonları 1 Ağustos 2017 geçirilen toosingle bölüm koleksiyonları nasıl olacaktır açıklanır. Bu makaleyi okuduktan sonra aşağıdaki soruları mümkün tooanswer hello olması:

- [Merhaba S1, S2 ve S3 performans neden olan kaldırılan düzeyleri?](#why-retired)
- [Nasıl tek bölüm koleksiyonları ve bölümlenmiş koleksiyonlar toohello S1, S2, S3 performans düzeyleri karşılaştırması nedir?](#compare)
- [I ne toodo tooensure kesintisiz toomy veri erişim?](#uninterrupted-access)
- [Nasıl kendi koleksiyonuma hello geçişten sonra değişir mi?](#collection-change)
- [Geçirilen toosingle bölüm koleksiyonları ben sonra my faturalama nasıl değiştirilir?](#billing-change)
- [Ne birden fazla 10 GB depolama alanı ihtiyacım var?](#more-storage-needed)
- [1 Ağustos 2017 önce hello S1, S2 ve S3 performans düzeyleri arasında değiştirebilir miyim?](#change-before)
- [Ne zaman kendi koleksiyonuma geçirildiğini nasıl anlarım?](#when-migrated)
- [Merhaba S1, S2, S3 performans düzeyleri toosingle bölüm koleksiyonlar üzerinde kendi gelen nasıl geçişini?](#migrate-diy)
- [Nasıl bir EA müşteri ben varsa ı etkilenen?](#ea-customer)

<a name="why-retired"></a>

## <a name="why-are-hello-s1-s2-and-s3-performance-levels-being-retired"></a>Merhaba S1, S2 ve S3 performans neden olan kaldırılan düzeyleri?

Merhaba S1, S2 ve S3 performans düzeyleri değil DocumentDB API koleksiyonları sunar teklif hello esneklik yapın. Merhaba S1, S2, S3 performans düzeyleri, her iki hello işleme ve depolama kapasitesini önceden ayarlanmış ve esneklik sunmadı. Azure Cosmos DB artık hello özelliği toocustomize üretilen iş ve depolama yeteneği tooscale gereksinimleriniz değiştikçe çok daha fazla esneklik sunumu sunar.

<a name="compare"></a>

## <a name="how-do-single-partition-collections-and-partitioned-collections-compare-toohello-s1-s2-s3-performance-levels"></a>Nasıl tek bölüm koleksiyonları ve bölümlenmiş koleksiyonlar toohello S1, S2, S3 performans düzeyleri karşılaştırması nedir?

Aşağıdaki tablonun hello hello işleme ve depolama seçenekleri tek bölüm koleksiyonları, bölümlenmiş koleksiyonlar ve S1, S2, S3 performans düzeyleri karşılaştırır. ABD Doğu 2 bölge için örnek aşağıda verilmiştir:

|   |Bölümlenmiş koleksiyonu|Tek bir bölüm koleksiyonu|S1|S2|S3|
|---|---|---|---|---|---|
|En yüksek verimlilik|Sınırsız|10 K RU/s|250 RU/s|1 K RU/s|2.5 K RU/s|
|En düşük işleme|2.5 K RU/s|400 RU/s|250 RU/s|1 K RU/s|2.5 K RU/s|
|Maksimum depolama|Sınırsız|10 GB|10 GB|10 GB|10 GB|
|Fiyat (ay)|Verimlilik: $6 / 100 RU/s<br><br>Depolama: $ 0,25/GB|Verimlilik: $6 / 100 RU/s<br><br>Depolama: $ 0,25/GB|$25 ABD DOLARI|$50 ABD DOLARI|$100 ABD DOLARI|

EA müşteri misiniz? Aksi takdirde bkz [nasıl ı etkilenen EA müşteri ben varsa?](#ea-customer)

<a name="uninterrupted-access"></a>

## <a name="what-do-i-need-toodo-tooensure-uninterrupted-access-toomy-data"></a>I ne toodo tooensure kesintisiz toomy veri erişim?

Hiçbir şey Cosmos DB hello geçiş sizin için işler. S1, S2 ve S3 koleksiyonu varsa, geçerli koleksiyonunuzu 31 Temmuz 2017 geçirilen tooa tek bölüm koleksiyonu olacaktır. 

<a name="collection-change"></a>

## <a name="how-will-my-collection-change-after-hello-migration"></a>Nasıl kendi koleksiyonuma hello geçişten sonra değişir mi?

S1 koleksiyonu varsa, 400 RU/s üretilen iş ile geçirilen tooa tek bölümlü bir koleksiyon olacaktır. 400 RU/s hello en düşük işleme sahip tek bölüm koleksiyonları kullanılabilir olur. Ancak, tek bölüm koleksiyonudur yaklaşık S1 koleksiyonunuzu aynı ödeme hello hello 400 RU/s ve 250 RU/sizin için ödeme yapıyorsanız olmayan şekilde s – hello maliyeti çok 150 RU/s kullanılabilir tooyou hello.

S2 koleksiyonu varsa, geçirilen tooa tek bölüm 1 K RU/s koleksiyonuyla olacaktır. Hiçbir değişiklik tooyour üretilen iş düzeyi görürsünüz.

S3 koleksiyonu varsa, geçirilen tooa tek bölümlü bir koleksiyon 2,5 K RU/s ile olacaktır. Hiçbir değişiklik tooyour üretilen iş düzeyi görürsünüz.

Her durumda, koleksiyonunuzu geçirildikten sonra üretilen iş düzeyi mümkün toocustomize olması, veya kaldıracak ölçeklemek yukarı ve aşağı gerekli tooprovide düşük gecikmeli erişim tooyour kullanıcılar olarak. koleksiyonunuz geçirildikten sonra toochange hello üretilen iş düzeyi Cosmos DB hesabınızı hello Azure portal açmanız yeterlidir, Ölçek'ı tıklatın, koleksiyonunuzu seçin ve sonra hello üretilen iş düzeyi hello ekran aşağıdaki gösterildiği gibi ayarlayın:

![Nasıl tooscale performansı hello Azure portalı](./media/performance-levels/portal-scale-throughput.png)

<a name="billing-change"></a>

## <a name="how-will-my-billing-change-after-im-migrated-toohello-single-partition-collections"></a>Geçirilen toohello tek bölüm koleksiyonları ben sonra my faturalama nasıl değiştirilir?

Varsayılmıştır 10 S1 koleksiyonları, 1 GB depolama alanı hello BİZE Doğu bölgede her sahiptir ve bu 10 S1 koleksiyonları too10 tek bölüm koleksiyonları 400 RU/sn (en düşük düzey hello) konumunda geçirme. Tam bir ay için hello 10 tek bölüm koleksiyonları tutarsanız faturanızı şu şekilde görünür:

![S1 10 koleksiyonlar için fiyatlandırma too10 koleksiyonları nasıl karşılaştırır tek bölümlü bir koleksiyon için fiyatlandırma kullanma](./media/performance-levels/s1-vs-standard-pricing.png)

<a name="more-storage-needed"></a>

## <a name="what-if-i-need-more-than-10-gb-of-storage"></a>Ne birden fazla 10 GB depolama alanı ihtiyacım var?

S1, S2 ve S3 bir performans düzeyine sahip bir koleksiyona sahip ya da 10 GB kullanılabilir depolama alanı olan bir tek bölümlü bir koleksiyona sahip olup olmadığını, verileri tooa koleksiyonuyla neredeyse bölümlenmiş hello Cosmos DB veri geçiş aracı toomigrate kullanabilirsiniz Sınırsız depolama. Bölümlendirilmiş bir koleksiyon hello avantajları hakkında daha fazla bilgi için bkz: [bölümleme ve Azure Cosmos DB'de ölçeklendirme](documentdb-partition-data.md). Hakkında bilgi için toomigrate S1, S2, S3 veya tek bölümlü bir koleksiyon bölümlenmiş tooa koleksiyonu, bkz: [tek bölümlü toopartitioned koleksiyonlarından geçiş](documentdb-partition-data.md#migrating-from-single-partition). 

<a name="change-before"></a>

## <a name="can-i-change-between-hello-s1-s2-and-s3-performance-levels-before-august-1-2017"></a>1 Ağustos 2017 önce hello S1, S2 ve S3 performans düzeyleri arasında değiştirebilir miyim?

S1, S2 ve S3 performans yalnızca var olan hesapları mümkün toochange olması ve performans düzeyi katmanları hello portalı üzerinden veya program aracılığıyla değiştirin. 1 Ağustos 2017 S1, S2, hello ve S3 performans düzeyleri artık kullanılabilir olmayacaktır. S1, S3 veya S3 tooa tek bölüm koleksiyonundan değiştirirseniz, S1, S2 ve S3 performans düzeyleri toohello döndüremez.

<a name="when-migrated"></a>

## <a name="how-will-i-know-when-my-collection-has-migrated"></a>Ne zaman kendi koleksiyonuma geçirildiğini nasıl anlarım?

Merhaba geçiş 31 Temmuz 2017 üzerinde meydana gelir. Bir koleksiyon varsa hello S1, S2 kullanan veya S3 performans düzeyleri, hello Cosmos DB takım hello geçiş gerçekleşmeden önce e-posta ile bağlantı kurar. Hello geçiş 1 Ağustos 2017 üzerinde tamamlandıktan sonra hello Azure portal, koleksiyonunuzu standart fiyatlandırma kullandığını gösterir.

![Koleksiyonunuz tooconfirm nasıl sahip toohello standart fiyatlandırma katmanı geçişi](./media/performance-levels/portal-standard-pricing-applied.png)

<a name="migrate-diy"></a>

## <a name="how-do-i-migrate-from-hello-s1-s2-s3-performance-levels-toosingle-partition-collections-on-my-own"></a>Merhaba S1, S2, S3 performans düzeyleri toosingle bölüm koleksiyonlar üzerinde kendi gelen nasıl geçişini?

Merhaba S1, S2, geçirebileceğiniz ve S3 performans hello Azure portal kullanarak toosingle bölüm koleksiyonları Düzeyler veya program aracılığıyla. 1 Ağustos önce kendi toobenefit üzerinde hello esnek işleme seçenekleri ile tek bölüm koleksiyonları kullanılabilir bunu yapabilirsiniz veya koleksiyonlarınızı sizin için 31 Temmuz 2017 üzerinde geçirirsiniz.

**Hello Azure portal kullanarak toomigrate toosingle bölüm koleksiyonları**

1. Merhaba, [ **Azure portal**](https://portal.azure.com), tıklatın **Azure Cosmos DB**, hello Cosmos DB hesap toomodify seçin. 
 
    Varsa **Azure Cosmos DB** üzerinde atlama çubuğu Merhaba, tıklatın değil >, çok kaydırma**veritabanları**seçin **Azure Cosmos DB**ve ardından hello DocumentDB hesabı seçin.  

2. Merhaba kaynak menüsünde altında **kapsayıcıları**, tıklatın **ölçek**hello koleksiyonu toomodify hello aşağı açılan listeden seçin ve ardından **fiyatlandırma katmanı**. Önceden tanımlanmış verimlilik kullanarak hesapları S1, S2 ve S3 fiyatlandırma katmanı vardır.  Merhaba, **fiyatlandırma katmanınızı seçin** dikey penceresinde tıklatın **standart** toochange toouser tanımlı verimlilik ve ardından **seçin** toosave değişikliğinizin.

    ![Burada toochange hello verimlilik değeri gösteren hello ayarları dikey penceresi ekran görüntüsü](./media/performance-levels/change-performance-set-thoughput.png)

3. Merhaba edilene **ölçek** dikey penceresinde, hello **fiyatlandırma katmanı** çok değiştirilir**standart** ve hello **üretilen işi (RU/s)** kutusu ile görüntülenir bir 400 varsayılan değeri. Set hello işleme 400-10.000 arasında [istek birimleri](request-units.md)/second (RU/s). Merhaba **tahmini aylık fatura** hello hello sonunda sayfa tooprovide aylık maliyeti hello tahmini otomatik olarak güncelleştirir. 

    >[!IMPORTANT] 
    > Yaptığınız değişiklikleri kaydedin ve toohello standart fiyatlandırma katmanını taşımak sonra toohello S1, S2 ve S3 performans düzeyleri geri alamazsınız.

4. Tıklatın **kaydetmek** toosave değişikliklerinizi.

    Daha fazla verimlilik (10. 000'ru / s büyük) veya daha fazla depolama alanı (10 GB'den büyük) gerekli belirlerseniz, bölümlendirilmiş bir koleksiyon oluşturabilirsiniz. toomigrate tek bölümlü bir koleksiyon bölümlenmiş tooa koleksiyonu bkz [tek bölümlü toopartitioned koleksiyonlarından geçiş](documentdb-partition-data.md#migrating-from-single-partition).

    > [!NOTE]
    > S1, S2 ve S3 tooStandard değiştirme too2 dakika sürebilir.
    > 
    > 

**Merhaba .NET SDK kullanarak toomigrate toosingle bölüm koleksiyonları**

Koleksiyonlarınızı performans düzeylerini değiştirmek için başka bir seçenek bizim SDK olur. Bu bölüm, yalnızca bir koleksiyona ait performansının değiştirilmesi kapsar kullanarak düzey bizim [DocumentDB .NET API](documentdb-sdk-dotnet.md), ancak bizim diğer SDK için hello işlemi benzerdir.

Saniye başına 000 isteği birim hello koleksiyonu verimlilik too5 değiştirmek için bir kod parçacığı aşağıda verilmiştir:
    
```C#
    //Fetch hello resource toobe updated
    Offer offer = client.CreateOfferQuery()
                      .Where(r => r.ResourceLink == collection.SelfLink)    
                      .AsEnumerable()
                      .SingleOrDefault();

    // Set hello throughput too5000 request units per second
    offer = new OfferV2(offer, 5000);

    //Now persist these changes toohello database by replacing hello original resource
    await client.ReplaceOfferAsync(offer);
```

Ziyaret [MSDN](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.aspx) tooview ek örnekler ve bizim teklif yöntemleri hakkında daha fazla bilgi edinin:

* [**ReadOfferAsync**](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.readofferasync.aspx)
* [**ReadOffersFeedAsync**](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.readoffersfeedasync.aspx)
* [**ReplaceOfferAsync**](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.replaceofferasync.aspx)
* [**CreateOfferQuery**](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.linq.documentqueryable.createofferquery.aspx)

<a name="ea-customer"></a>

## <a name="how-am-i-impacted-if-im-an-ea-customer"></a>Nasıl bir EA müşteri ben varsa ı etkilenen?

EA müşteriler kendi geçerli sözleşmenin hello sonuna kadar korumalı fiyat olacaktır.

## <a name="next-steps"></a>Sonraki adımlar
Fiyatlandırma ve Azure Cosmos DB ile verileri yönetme hakkında daha fazla toolearn şu kaynakları araştırın:

1.  [Cosmos DB'de veri bölümlendirme](documentdb-partition-data.md). Merhaba birbirinden bölümleme stratejisi tooscale sorunsuz bir şekilde uygulama ipuçları yanı sıra tek bölümlü bir kapsayıcı ve bölümlenmiş kapsayıcıları anlayın.
2.  [Cosmos DB fiyatlandırma](https://azure.microsoft.com/pricing/details/cosmos-db/). Üretilen iş sağlama ve depolama tüketme hello maliyeti hakkında bilgi edinin.
3.  [İstek birimleri](request-units.md). Farklı işlem türleri için örneğin okuma, yazma, sorgu işleme Hello tüketimini anlayın.
