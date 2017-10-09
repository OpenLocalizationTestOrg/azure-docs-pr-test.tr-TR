---
title: "SQL veri ambarı aaaDistributing tablolarda | Microsoft Docs"
description: "Azure SQL Data Warehouse tablolarda dağıtma ile çalışmaya başlama."
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: barbkess
editor: 
ms.assetid: 5ed4337f-7262-4ef6-8fd6-1809ce9634fc
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 10/31/2016
ms.author: shigu;barbkess
ms.openlocfilehash: 65093eeaeb00fef85aaa6070da2c976fed3f4bbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="distributing-tables-in-sql-data-warehouse"></a>SQL veri ambarı tablolarda dağıtma
> [!div class="op_single_selector"]
> * [Genel bakış][Overview]
> * [Veri türleri][Data Types]
> * [Dağıt][Distribute]
> * [Dizin][Index]
> * [Bölüm][Partition]
> * [İstatistikleri][Statistics]
> * [Geçici][Temporary]
>
>

SQL Veri Ambarı, yüksek düzeyde paralel işleme (MPP) ile dağıtılmış bir veritabanı sistemidir.  Birden fazla düğümde verileri ve işleme özelliğini bölerek, SQL Veri Ambarı tek bir sistemin sağlayabileceğinden çok büyük ölçeklenebilirlik sunabilir.  Toodistribute verilerinizi SQL veri ambarı içinde ne olduğuna karar vermeyle hello en önemli birini Etkenler tooachieving en iyi performans.   Veri taşıma Hello anahtar toooptimal performans en aza indirerek ve hello anahtar toominimizing veri taşıma hello doğru Dağıtım stratejisi sırayla seçme.

## <a name="understanding-data-movement"></a>Veri taşıma anlama
Bir MPP sisteminde hello veriler her tablodan birkaç temel veritabanları arasında bölünür.  en iyileştirilmiş hello sorguları bir MPP sistemde yalnızca geçirilebilir tooexecute üzerinde hello etkileşimi olmadan tek tek dağıtılan veritabanları arasında diğer veritabanlarına hello.  Örneğin, iki tablo, satış ve müşteriler içeren satış verilerini içeren bir veritabanına sahip varsayalım.  Satış tooyour müşteri tablo toojoin gerektiren bir sorgu varsa ve hem satış hem de müşteri tabloları müşteri numarası tarafından ayrı bir veritabanında her müşteri koyma bölme, satış ve müşteri birleştiren herhangi bir sorgu her içinde çözülebilir hiçbir bilgisine sahip veritabanı diğer veritabanlarından hello.  Sipariş numarası ve müşteri verilerinizi müşteri numarasına göre satış verilerinizi bölünmüş, buna karşılık, ardından tüm verilen veritabanı hello karşılık gelen verilerin her müşteri için sahip olmaz ve bu nedenle, satış verileri tooyour müşteri verilerinizi toojoin istediyseniz, gerekir tooget hello veri hello gelen her bir müşteri için diğer veritabanları.  Böylece Hello iki tabloları katılabilir bu ikinci örnekte toooccur toomove hello müşteri veri toohello satış verileri, veri taşıma gerekir.  

Veri taşıma her zaman hatalı bir şey değilse, bazen gerekli toosolve bir sorgu olabilir.  Ancak bu ek adım önlenebilir doğal olarak sorgunuzu daha hızlı çalışır.  Veri taşıma en yaygın olarak tablolar birleştirilir veya toplamalar gerçekleştirilen ortaya çıkar.  Genellikle mümkün olabilir ancak bir birleştirme, siz hala gibi bir senaryoya ihtiyaç için veri taşıma toohelp için çözmek toooptimize hello için bir toplama gibi diğer senaryo toodo ikisini olması gerekir.  Merhaba eli daha az iş olduğu çıkışı çıkarılıyor.  Çoğu durumda, büyük olgu tabloları genellikle birleştirilmiş bir sütunda dağıtma olduğu hello hello azaltma en etkili yöntemi çoğu veri taşıma.  Verileri birleştirme sütunlarda dağıtma veri bir toplama söz konusu sütunlarda dağıtma daha bir çok daha yaygın yöntemi tooreduce veri hareketi olur.

## <a name="select-distribution-method"></a>Dağıtım yöntemini seçin
Merhaba arka planda, SQL Data Warehouse verilerinizi 60 veritabanlarına böler.  Başvurulan tooas tek tek her veritabanı olan bir **dağıtım**.  Veri her tabloya yüklendiğinde, SQL Data Warehouse tooknow nasıl sahip toodivide verilerinizi 60 bu dağıtımlar arasında.  

Merhaba dağıtım yöntemini hello tablo düzeyinde tanımlanır ve şu anda iki seçeneğiniz vardır:

1. **Hepsini bir kez** eşit ancak rastgele veri dağıtın.
2. **Dağıtılmış karma** tek bir sütun değerlerinden karma göre verileri dağıtır

Bir veri dağıtım yöntemi olmayan tanımlarken varsayılan olarak, tablonuz hello kullanarak dağıtılacak **hepsini** dağıtım yöntemi.  Uygulamanızda daha karmaşık hale geldikçe ancak tooconsider kullanarak istediğiniz **dağıtılmış karma** tabloları sırayla sorgu performansı en iyi duruma getirir, toominimize veri taşıma.

### <a name="round-robin-tables"></a>Hepsini bir kez tabloları
Merhaba veri dağıtmanın hepsini bir kez yöntemi kullanarak çok nasıl, göründüğü değildir.  Verilerinizi yüklenen gibi her satır yalnızca toohello sonraki dağıtım gönderilir.  Merhaba veri dağıtmanın bu yöntem her zaman rastgele hello veri çok eşit tüm hello dağıtımlar arasında dağıtır.  Diğer bir deyişle, var. sıralama Bitti'yi verilerinizi koyan bir kez deneme işlemi round hello sırasında  Hepsini bir kez dağıtım, bu nedenle rastgele bir karma bazen denir.  Hepsini dağıtılmış tabloyla gerek toounderstand hello verisi yok.  Bu nedenle, hepsini tabloları genellikle iyi yükleme hedefleri olun.

Hiçbir dağıtım yöntemi seçilirse, varsayılan olarak, hello hepsini dağıtım yöntemi kullanılır.  Ancak, veri rastgele hello sistem hangi dağıtım garanti edemez anlamına gelir hello sistem dağıtıldığı hepsini bir kez tabloları kolay toouse durumdayken her satırın'dır.  Sonuç, bazen hello sistem tooinvoke veri taşıma işlemi toobetter gerektiği bir sorgu çözebilmek için önce verilerinizi düzenleyin.  Bu ek adım sorgularınızı yavaşlatabilir.

Hepsini bir kez dağıtım senaryoları aşağıdaki hello tablonuzda için kullanmayı dikkate alın:

* Basit bir başlangıç noktası olarak çalışmaya
* Hiçbir belirgin katılma anahtarı ise
* Karma hello tablo dağıtmak için iyi bir adaydır sütun değilse
* Merhaba, tablo ortak bir birleşim anahtar diğer tablolarla paylaşmaz
* Merhaba birleştirme hello sorgu diğer birleşimlerde'den daha az önemli ise
* Merhaba tablo geçici bir hazırlama tablosunda olduğunda

Bu örneklerin her ikisi de hepsini bir kez tablo oluşturacak:

```SQL
-- Round Robin created by default
CREATE TABLE [dbo].[FactInternetSales]
(   [ProductKey]            int          NOT NULL
,   [OrderDateKey]          int          NOT NULL
,   [CustomerKey]           int          NOT NULL
,   [PromotionKey]          int          NOT NULL
,   [SalesOrderNumber]      nvarchar(20) NOT NULL
,   [OrderQuantity]         smallint     NOT NULL
,   [UnitPrice]             money        NOT NULL
,   [SalesAmount]           money        NOT NULL
)
;

-- Explicitly Created Round Robin Table
CREATE TABLE [dbo].[FactInternetSales]
(   [ProductKey]            int          NOT NULL
,   [OrderDateKey]          int          NOT NULL
,   [CustomerKey]           int          NOT NULL
,   [PromotionKey]          int          NOT NULL
,   [SalesOrderNumber]      nvarchar(20) NOT NULL
,   [OrderQuantity]         smallint     NOT NULL
,   [UnitPrice]             money        NOT NULL
,   [SalesAmount]           money        NOT NULL
)
WITH
(   CLUSTERED COLUMNSTORE INDEX
,   DISTRIBUTION = ROUND_ROBIN
)
;
```

> [!NOTE]
> Hepsini bir kez olsa hello varsayılan tablo türü, DDL'de açık olan bir tablo düzeni hello amaçları Temizle tooothers; böylece en iyi yöntem olarak kabul edilir.
>
>

### <a name="hash-distributed-tables"></a>Dağıtılmış tabloları karma
Kullanarak bir **dağıtılmış karma** algoritması toodistribute tablolarınızı birçok senaryoları için sorgu zamanında veri taşıma azaltarak performansı artırabilir.  Dağıtılmış tablolar arasında hello bölünen tablolardır karma seçtiğiniz tek bir sütun üzerinde bir karma algoritması kullanarak veritabanlarını dağıtılmış.  Merhaba dağıtım ne hello veriler dağıtılan veritabanları arasında nasıl bölünür belirler bir sütundur.  Merhaba karma işlevi hello dağıtım sütun tooassign satırları toodistributions kullanır.  karma algoritma hello ve sonuçta elde edilen dağıtım belirleyici.  Diğer bir deyişle hello aynı veri türünde olacak her zaman hello ile aynı değere sahip toohello aynı dağıtım.    

Bu örnek kimliği, dağıtılmış bir tablo oluşturacak:

```SQL
CREATE TABLE [dbo].[FactInternetSales]
(   [ProductKey]            int          NOT NULL
,   [OrderDateKey]          int          NOT NULL
,   [CustomerKey]           int          NOT NULL
,   [PromotionKey]          int          NOT NULL
,   [SalesOrderNumber]      nvarchar(20) NOT NULL
,   [OrderQuantity]         smallint     NOT NULL
,   [UnitPrice]             money        NOT NULL
,   [SalesAmount]           money        NOT NULL
)
WITH
(   CLUSTERED COLUMNSTORE INDEX
,  DISTRIBUTION = HASH([ProductKey])
)
;
```

## <a name="select-distribution-column"></a>Dağıtım sütun seçin
Çok seçtiğinizde**karma dağıtmak** bir tablo tooselect tek dağıtım sütun gerekir.  Bir dağıtım sütun seçerken, üç ana Etkenler tooconsider vardır.  

Olur, tek bir sütun seçin:

1. Güncelleştirilmemiş
2. Veri eşit, veri eğme önleme Dağıt
3. Veri taşıma simge durumuna küçült

### <a name="select-distribution-column-which-will-not-be-updated"></a>Güncelleştirilmez dağıtım sütun seçin
Dağıtım sütunları bu nedenle güncelleştirilebilir, değildir, statik değerleri içeren bir sütun seçin.  Bir sütun güncelleştirilmiş toobe gerekecekse, genellikle iyi dağıtım aday değil.  Bir dağıtım sütun güncelleştirme söz konusu ise, bu ilk hello satırın silinmesi ve yeni satır ekleme yapılabilir.

### <a name="select-distribution-column-which-will-distribute-data-evenly"></a>Veri eşit olarak dağıtmanızı dağıtım sütun seçin
Dağıtılmış bir sistemde yalnızca olabildiğince hızlı şekilde kendi yavaş dağıtım gerçekleştirir olduğundan, bu önemli toodivide hello iş eşit sipariş dengeli tooachieve yürütmesinde hello dağıtımlar arasında hello arasında sistemidir.  Hello iş dağıtılmış bir sistemde ayrılmıştır hello yolu, her dağıtım için hello veri nerede yaşıyor temel alır.  Bu, böylece her dağıtım eşit iş sahiptir ve Al aynı zaman toocomplete hello iş kendi kısmı hello hello veri dağıtmak için çok önemli tooselect hello doğru dağıtım sütun kolaylaştırır.  İş iyi hello sistem ayrıldığında, hello veri hello dağıtımlar arasında dengelenir.  Veri eşit dengeli değil, bu diyoruz **veri eğme**.  

toodivide veri eşit ve veri eğme kaçınmak için dağıtım sütun seçerken hello aşağıdakileri dikkate alın:

1. Çok sayıda farklı değerleri içeren bir sütun seçin.
2. Veri birkaç farklı değerleri olan sütunlarda dağıtma kaçının.
3. Null değerlere yüksek sıklığını sahip sütunlarda veri dağıtma kaçının.
4. Veri tarih sütunlarda dağıtma kaçının.

Tooachieve bile dağıtım her değer 60 dağıtımları, karma too1 olduğundan, yüksek oranda benzersiz olan ve birden fazla 60 benzersiz değerler içeren bir sütun tooselect isteyeceksiniz.  tooillustrate, bir sütun yalnızca sahip olduğu 40 benzersiz değerler bir durum düşünün.  Bu sütun hello dağıtım anahtarı olarak seçtiyseniz, bu tablo için hello veri üzerinde 40 dağıtımları en fazla 20 dağıtımları hiçbir veri ve hiçbir işlem toodo bırakarak güden.  Buna karşılık, hello diğer 40 dağıtımları hello varsa veri eşit 60 dağıtımları yayılan, daha fazla iş toodo gerekir.  Bu senaryoda, veri eğme örneğidir.

MPP sistemdeki her sorgu adım için tüm dağıtımların toocomplete kendi paylaşımı hello iş bekler.  Bir dağıtım başkalarının hello daha fazla çalışma yapılması olduğu sonra hello kaynak hello diğer dağıtımlar temelde yalnızca hello meşgul dağıtım noktasında bekleme küçülttüğü iyi bir şekilde.  İş eşit tüm dağıtımlar arasında yayılır değil, bu diyoruz **işleme eğme**.  İşleme eğme sorguları toorun hello iş yükü hello dağıtımlar arasında eşit olarak yayılabilen varsa daha yavaş neden olur.  Veri eğme tooprocessing eğme götürür.

Merhaba null değerler tüm hello üzerinde aynı gideceksiniz gibi yüksek oranda boş değer atanabilir sütun dağıtmaktan kaçınmak dağıtım. Bir tarih sütunu dağıtma de neden olabilir işleme eğme belirli bir tarih için tüm veriler üzerinde hello aynı gideceksiniz çünkü dağıtım. Birkaç kullanıcı sorguları tüm filtreleme hello üzerinde çalıştırıyorsanız belirli bir tarih yalnızca bir dağıtım noktasında olacağından yalnızca 1'hello 60 dağıtımları, tüm hello iş istediğimizi sonra aynı, tarih. Bu senaryoda, hello sorguları büyük olasılıkla 60 kez hello veri eşit tüm hello dağıtımları yayılan, daha yavaş çalışır.

İyi bir adaydır sütun mevcut olduğunda hello dağıtım yöntemi olarak hepsini kullanarak düşünün.

### <a name="select-distribution-column-which-will-minimize-data-movement"></a>Veri taşıma en aza indirecek dağıtım sütun seçin
Veri taşıma hello doğru dağıtım sütun seçerek en aza SQL veri ambarı performansını iyileştirmek için en önemli stratejileri hello biridir.  Veri taşıma en yaygın olarak tablolar birleştirilir veya toplamalar gerçekleştirilen ortaya çıkar.  Kullanılan sütunlar `JOIN`, `GROUP BY`, `DISTINCT`, `OVER` ve `HAVING` tüm hale getirmek için yan tümceleri **iyi** dağıtım adayları karma.

Üzerinde diğer yandan, hello sütunlarında hello `WHERE` yan tümcesi **değil** hangi dağıtımları işleme neden hello sorguda katılmak sınırlamak için iyi bir karma sütun adayları eğme olun.  İyi tempting toodistribute olabilir, ancak bu işleme eğme genellikle neden olabilir bir sütunun bir tarih sütunu bir örnektir.

Bir birleştirme sık söz konusu iki büyük olgu tabloları varsa, genel olarak bakıldığında, hello çoğu performans hello birleştirme sütunları her iki tablolarda dağıtarak elde edersiniz.  Hiçbir zaman birleştirilmiş tooanother büyük Olgu Tablosu olan bir tablo varsa, sık hello olan toocolumns Ara `GROUP BY` yan tümcesi.

Ölç tooavoid veri taşıma sırasında bir birleştirme olması gereken birkaç anahtar ölçütleri vardır:

1. Merhaba hello birleştirme söz konusu tablolar üzerinde dağıtılmış karma olmalıdır **bir** hello birleştirme katılan hello sütunların.
2. Merhaba birleştirme sütunların veri türlerini Hello her iki tablo arasında eşleşmelidir.
3. Merhaba sütunları olan bir eşittir işleci katılması gerekir.
4. Merhaba birleşim türü olamaz bir `CROSS JOIN`.

## <a name="troubleshooting-data-skew"></a>Veri eğme sorunlarını giderme
Tablo verisi yok hello karma dağıtım yöntemini kullanarak dağıtıldığında bazı dağıtımları olacak şansı toohave diğerlerinden orantısız daha fazla veri eğri. Dağıtılmış bir sorguyla Hello sonucunu hello uzun çalışan dağıtım toofinish için beklemeniz gerekir çünkü aşırı miktarda verinin eğme sorgu performansını etkileyebilir. Merhaba veri tooaddress gerekebilecek eğme Hello derecesini, bağlı olarak.

### <a name="identifying-skew"></a>Eğme tanımlama
Toouse basit yol tooidentify eğri gibi bir tablo olduğundan `DBCC PDW_SHOWSPACEUSED`.  Çok hızlı ve basit bir yol toosee budur hello her hello 60 dağıtımları veritabanınızın depolanır tablosu satır sayısı.  En dengeli hello performans için Dağıtılmış tablonuz hello satır eşit tüm hello dağıtımlar arasında yayılan olduğunu unutmayın.

```sql
-- Find data skew for a distributed table
DBCC PDW_SHOWSPACEUSED('dbo.FactInternetSales');
```

Ancak, hello Azure SQL Data Warehouse dinamik yönetim görünümlerini (DMV) sorgu varsa daha ayrıntılı bir analiz gerçekleştirebilir.  toostart, hello görünümü oluşturma [dbo.vTableSizes] [ dbo.vTableSizes] kullanarak görüntülemek SQL'den hello [tablo genel bakışı] [ Overview] makalesi.  Merhaba görünüm oluşturulduktan sonra hangi tabloları % 10 veri eğme birden fazla sahip bu sorgu tooidentify çalıştırın.

```sql
select *
from dbo.vTableSizes
where two_part_name in
    (
    select two_part_name
    from dbo.vTableSizes
    where row_count > 0
    group by two_part_name
    having min(row_count * 1.000)/max(row_count * 1.000) > .10
    )
order by two_part_name, row_count
;
```

### <a name="resolving-data-skew"></a>Veri eğme çözme
Tüm eğme yeterli toowarrant bir düzeltme bulunur.  Bazı durumlarda, bazı sorgular tabloda hello performansını hello zarar eğme verilerin daha ağır basar.  Veri çözümlenmelidir varsa toodecide eğme bir tabloda, hello veri birimleri ve sorguları hakkında mümkün olduğunca, iş yükü anlamalısınız.   Tek yönlü toolook eğme hello etkisini en olduğu toouse hello hello adımlarda [sorgu izleme] [ Query Monitoring] makale toomonitor hello etkisini sorgu performansı eğme ve özellikle etkisi toohow uzun sorguları hello toocomplete hello tek tek dağıtımları üzerinde gerçekleştirin.

Veri dağıtma veri eğme en aza indirerek ve veri taşıma en aza arasında doğru dengeyi hello bulma bir konudur. Bu hedefleri karşıt ve bazen tookeep veri sırası tooreduce veri taşıma eğme isteyeceksiniz. Merhaba dağıtım sütun sık birleşimler ve toplamalar paylaşılan sütununda hello olduğunda, örneğin, veri taşıma en aza indirme. Merhaba bir eğme verilere sahip olmak hello etkisi en hello en düşük düzeyde veri taşıma sahip olmanın avantajı üstün olabilir.

Merhaba normal şekilde tooresolve veri eğme olan toore-farklı dağıtım sütunla hello tablo oluşturun. Olduğundan toochange hello dağıtım sütun üzerinde var olan tablo, hello yolu toochange hello dağıtımı bir tablonun hiçbir şekilde bunu toorecreate [CTAS] [] ile.  İşte nasıl iki örnek veri eğme çözün:

### <a name="example-1-re-create-hello-table-with-a-new-distribution-column"></a>Örnek 1: yeni bir dağıtım sütun ile Merhaba tabloyu yeniden oluşturun
Bu örnek [CTAS] [] toore kullanır-farklı bir karma dağıtım sütun bir tablo oluşturun.

```sql
CREATE TABLE [dbo].[FactInternetSales_CustomerKey]
WITH (  CLUSTERED COLUMNSTORE INDEX
     ,  DISTRIBUTION =  HASH([CustomerKey])
     ,  PARTITION       ( [OrderDateKey] RANGE RIGHT FOR VALUES (   20000101, 20010101, 20020101, 20030101
                                                                ,   20040101, 20050101, 20060101, 20070101
                                                                ,   20080101, 20090101, 20100101, 20110101
                                                                ,   20120101, 20130101, 20140101, 20150101
                                                                ,   20160101, 20170101, 20180101, 20190101
                                                                ,   20200101, 20210101, 20220101, 20230101
                                                                ,   20240101, 20250101, 20260101, 20270101
                                                                ,   20280101, 20290101
                                                                )
                        )
    )
AS
SELECT  *
FROM    [dbo].[FactInternetSales]
OPTION  (LABEL  = 'CTAS : FactInternetSales_CustomerKey')
;

--Create statistics on new table
CREATE STATISTICS [ProductKey] ON [FactInternetSales_CustomerKey] ([ProductKey]);
CREATE STATISTICS [OrderDateKey] ON [FactInternetSales_CustomerKey] ([OrderDateKey]);
CREATE STATISTICS [CustomerKey] ON [FactInternetSales_CustomerKey] ([CustomerKey]);
CREATE STATISTICS [PromotionKey] ON [FactInternetSales_CustomerKey] ([PromotionKey]);
CREATE STATISTICS [SalesOrderNumber] ON [FactInternetSales_CustomerKey] ([SalesOrderNumber]);
CREATE STATISTICS [OrderQuantity] ON [FactInternetSales_CustomerKey] ([OrderQuantity]);
CREATE STATISTICS [UnitPrice] ON [FactInternetSales_CustomerKey] ([UnitPrice]);
CREATE STATISTICS [SalesAmount] ON [FactInternetSales_CustomerKey] ([SalesAmount]);

--Rename hello tables
RENAME OBJECT [dbo].[FactInternetSales] too[FactInternetSales_ProductKey];
RENAME OBJECT [dbo].[FactInternetSales_CustomerKey] too[FactInternetSales];
```

### <a name="example-2-re-create-hello-table-using-round-robin-distribution"></a>Örnek 2: hello tabloyu hepsini dağıtım kullanarak yeniden oluşturun
Bu örnek [CTAS] [] toore kullanır-hepsini bir karma dağıtım yerine bir tablo oluşturun. Bu değişiklik, hatta veri dağıtımını hello maliyetle artan veri taşıma oluşturur.

```sql
CREATE TABLE [dbo].[FactInternetSales_ROUND_ROBIN]
WITH (  CLUSTERED COLUMNSTORE INDEX
     ,  DISTRIBUTION =  ROUND_ROBIN
     ,  PARTITION       ( [OrderDateKey] RANGE RIGHT FOR VALUES (   20000101, 20010101, 20020101, 20030101
                                                                ,   20040101, 20050101, 20060101, 20070101
                                                                ,   20080101, 20090101, 20100101, 20110101
                                                                ,   20120101, 20130101, 20140101, 20150101
                                                                ,   20160101, 20170101, 20180101, 20190101
                                                                ,   20200101, 20210101, 20220101, 20230101
                                                                ,   20240101, 20250101, 20260101, 20270101
                                                                ,   20280101, 20290101
                                                                )
                        )
    )
AS
SELECT  *
FROM    [dbo].[FactInternetSales]
OPTION  (LABEL  = 'CTAS : FactInternetSales_ROUND_ROBIN')
;

--Create statistics on new table
CREATE STATISTICS [ProductKey] ON [FactInternetSales_ROUND_ROBIN] ([ProductKey]);
CREATE STATISTICS [OrderDateKey] ON [FactInternetSales_ROUND_ROBIN] ([OrderDateKey]);
CREATE STATISTICS [CustomerKey] ON [FactInternetSales_ROUND_ROBIN] ([CustomerKey]);
CREATE STATISTICS [PromotionKey] ON [FactInternetSales_ROUND_ROBIN] ([PromotionKey]);
CREATE STATISTICS [SalesOrderNumber] ON [FactInternetSales_ROUND_ROBIN] ([SalesOrderNumber]);
CREATE STATISTICS [OrderQuantity] ON [FactInternetSales_ROUND_ROBIN] ([OrderQuantity]);
CREATE STATISTICS [UnitPrice] ON [FactInternetSales_ROUND_ROBIN] ([UnitPrice]);
CREATE STATISTICS [SalesAmount] ON [FactInternetSales_ROUND_ROBIN] ([SalesAmount]);

--Rename hello tables
RENAME OBJECT [dbo].[FactInternetSales] too[FactInternetSales_HASH];
RENAME OBJECT [dbo].[FactInternetSales_ROUND_ROBIN] too[FactInternetSales];
```

## <a name="next-steps"></a>Sonraki adımlar
Tablo tasarımı hakkında daha fazla toolearn bkz hello [Dağıt][Distribute], [dizin][Index], [bölüm] [ Partition], [Veri türleri][Data Types], [istatistikleri] [ Statistics] ve [geçici tablolar] [ Temporary] makaleleri.

En iyi yöntemler genel bakış için bkz: [SQL veri ambarı en iyi uygulamalar][SQL Data Warehouse Best Practices].

<!--Image references-->

<!--Article references-->
[Overview]: ./sql-data-warehouse-tables-overview.md
[Data Types]: ./sql-data-warehouse-tables-data-types.md
[Distribute]: ./sql-data-warehouse-tables-distribute.md
[Index]: ./sql-data-warehouse-tables-index.md
[Partition]: ./sql-data-warehouse-tables-partition.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[Temporary]: ./sql-data-warehouse-tables-temporary.md
[SQL Data Warehouse Best Practices]: ./sql-data-warehouse-best-practices.md
[Query Monitoring]: ./sql-data-warehouse-manage-monitor.md
[dbo.vTableSizes]: ./sql-data-warehouse-tables-overview.md#table-size-queries

<!--MSDN references-->
[DBCC PDW_SHOWSPACEUSED()]: https://msdn.microsoft.com/library/mt204028.aspx

<!--Other Web references-->
