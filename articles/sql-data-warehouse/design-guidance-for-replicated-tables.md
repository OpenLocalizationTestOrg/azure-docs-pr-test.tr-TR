---
title: "aaaDesign yönergeler için çoğaltılmış tablolarda - Azure SQL Data Warehouse | Microsoft Docs"
description: "Çoğaltılmış tablolar, Azure SQL Data Warehouse şemasında tasarlama için öneriler."
services: sql-data-warehouse
documentationcenter: NA
author: ronortloff
manager: jhubbard
editor: 
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 07/14/2017
ms.author: rortloff;barbkess
ms.openlocfilehash: 5d405b8c404c65177b387ba959126839c1cf8799
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="design-guidance-for-using-replicated-tables-in-azure-sql-data-warehouse"></a>Azure SQL Data Warehouse'da çoğaltılmış tablolar kullanmaya yönelik kılavuz tasarım
Bu makalede SQL Data Warehouse şemanızı çoğaltılmış tablolarda tasarlamak için öneriler sağlar. Bu öneriler tooimprove sorgu performansı veri hareketlerini ve sorgu karmaşıklık azaltarak kullanın.

> [!NOTE]
> Merhaba çoğaltılmış tablo şu anda genel önizlemede özelliğidir. Bazı davranışları konu toochange ' dir.
> 

## <a name="prerequisites"></a>Ön koşullar
Bu makalede, veri dağıtımı ve SQL Data Warehouse veri taşıma kavramlarına alışık olduğunuz varsayılır.  Daha fazla bilgi için bkz: [Dağıtılmış veri](sql-data-warehouse-distributed-data.md). 

Tablo Tasarımı bir parçası olarak, verilerinizi ve hello verileri nasıl sorgulanır hakkında mümkün olduğunca anlayın.  Örneğin, aşağıdaki soruları göz önünde bulundurun:

- Merhaba tablo büyüklüğü nedir?   
- Merhaba tablo ne sıklıkla yenileniyor?   
- Bir veri ambarı olgu ve boyut tabloları var mı?   

## <a name="what-is-a-replicated-table"></a>Çoğaltılmış tablosu nedir?
Yinelenen Tablo Merhaba tablonun erişilebilir tam bir kopyasını her işlem düğümünde sahiptir. Tablo çoğaltma JOIN veya toplama önce işlem düğümleri arasında hello gerek tootransfer verileri kaldırır. Merhaba tablosunda birden çok kopya bulunduğundan hello tablo boyutunu sıkıştırılmış 2 GB'tan daha az olduğunda çoğaltılmış tablolarda en iyi çalışır.

Merhaba Aşağıdaki diyagramda her işlem düğümü üzerinde erişilebilir olan bir çoğaltılmış tablo gösterir. SQL veri ambarı'nda hello çoğaltılmış tablo tam kopyalanan tooa dağıtım her işlem düğümünde veritabanıdır. 

![Yinelenmiş tablo](media/guidance-for-using-replicated-tables/replicated-table.png "yinelenmiş tablosu")  

İyi bir yıldız şemasının küçük boyut tabloları için tabloları iş çoğaltılan. Boyut tabloları genellikle uygun toostore kolaylaştıran bir boyutta olduğundan ve birden çok kopyasını sürdürün. Boyutların müşteri adı ve adres ve ürün ayrıntıları gibi yavaş değişir açıklayıcı verileri depolar. yavaş hello veri yapısını değiştirme hello toofewer yeniden hello çoğaltılmış tablosunun yol açar. 

Çoğaltılan kullanmayı tablosundan:

- Merhaba tablo diskteki 2 GB'den az, satır sayısı hello bağımsız olarak boyutudur. bir tablonun toofind hello boyutunu, hello kullanabilir [DBCC PDW_SHOWSPACEUSED](https://docs.microsoft.com/en-us/sql/t-sql/database-console-commands/dbcc-pdw-showspaceused-transact-sql) komutu: `DBCC PDW_SHOWSPACEUSED('ReplTableCandidate')`. 
- Merhaba tablo, aksi halde veri taşıma gerektirecek birleştirme kullanılır. Örneğin, Hello katılma sütunları hello değil, aynı dağıtım sütun tablolarda karma dağıtılmış bir birleştirme veri taşıma gerektirir. Merhaba karma dağıtılmış tablolardan biri küçükse, çoğaltılmış bir tablo göz önünde bulundurun. Bir birleştirme hepsini tabloda veri taşıma gerektirir. Çoğu durumda hepsini tablolar yerine çoğaltılmış tablolar kullanmanızı öneririz. 


Varolan bir dönüştürme dağıtılmış çoğaltılmış tablo tooa göz önünde bulundurun tablosundan:

- Sorgu hello veri tooall hello işlem düğümleri yayını kullanımı veri taşıma işlemleri planlar. Merhaba BroadcastMoveOperation pahalıdır ve sorgu performansı yavaşlatır. Sorgu planlarda tooview veri taşıma işlemleri kullanmak [sys.dm_pdw_request_steps](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql).
 
Çoğaltılmış tablolar hello en iyi sorgu performansını değil verim zaman:

- Merhaba tablosu sık ekleme, güncelleştirme ve silme işlemleri sahiptir. Bu veri işleme dili (DML) işlemleri yeniden çoğaltılan Merhaba tablonun gerektirir. Yeniden derleme sık performans neden olabilir.
- Merhaba veri ambarı sık ölçeklendirilir. Veri ambarı ölçeklendirme hello yeniden oluşturur, işlem düğümleri sayısı değiştirir.
- Merhaba tablosunda çok sayıda sütun var, ancak veri işlemleri genellikle az sayıda sütun erişim. Merhaba tüm tablo çoğaltmak yerine bu senaryoda, daha etkili toohash olabilir hello tablo dağıtın ve ardından sık erişilen hello sütunlarda bir dizin oluşturun. Ne zaman hello taşır verilerde sütunları istenen yalnızca bir sorgu veri taşıma, SQL Data Warehouse gerektirir. 



## <a name="use-replicated-tables-with-simple-query-predicates"></a>Çoğaltılmış tablolar ile basit sorgu koşulları kullanın
Toodistribute seçin veya bir tablo çoğaltmak önce toorun hello tabloda plan sorgu hello türleri düşünün. Mümkün olduğunda,

- Eşitlik veya eşitsizlik gibi basit sorgu koşulları içeren sorgular için çoğaltılmış tablolarda kullanın.
- DEĞİL gibi veya benzer gibi karmaşık bir sorgu koşulları içeren sorgular için Dağıtılmış tabloları kullanın.

CPU-yoğun sorguları en iyi şekilde Hello iş tüm hello işlem düğümleri arasında dağıtıldığında gerçekleştirin. Örneğin, tablonun her satırında hesaplamaları çalıştırmak sorguları dağıtılmış tablolarda çoğaltılmış tablolar daha iyi gerçekleştirin. Çoğaltılmış tablo her işlem düğümü üzerinde tam kaydedildiği çoğaltılmış bir tabloda bir CPU-yoğun sorgu karşı hello tüm tablo her işlem düğümünde çalışır. Merhaba ek hesaplama sorgu performansı düşürebilir.

Örneğin, bu sorgu, bir karmaşık koşuluna sahip.  Sağlayıcı bir çoğaltılmış tablo yerine dağıtılmış bir tablo olduğunda daha hızlı çalışır. Bu örnekte, hepsini dağıtılmış veya tedarikçi karma dağıtılmış olabilir.

```sql

SELECT EnglishProductName 
FROM DimProduct 
WHERE EnglishDescription LIKE '%frame%comfortable%'

```

## <a name="convert-existing-round-robin-tables-tooreplicated-tables"></a>Varolan hepsini tabloları tooreplicated tabloları Dönüştür
Hepsini tablolar zaten varsa, bu makalede açıklanan ölçütlerle karşılıyorsa bunları dönüştürme tooreplicated tabloları öneririz. Veri taşıma hello gereksinimini ortadan kaldırdığı çoğaltılmış tablolar hepsini tablolar üzerindeki performansı.  Hepsini tablo, veri taşıma birleştirmeler için her zaman gerektirir. 

Bu örnekte [CTAS](https://docs.microsoft.com/sql/t-sql/statements/create-table-as-select-azure-sql-data-warehouse) toochange hello DimSalesTerritory tablo tooa çoğaltılmış tablo. Bu örnek DimSalesTerritory karma dağıtılmış veya hepsini bağımsız olarak çalışır.

```sql
CREATE TABLE [dbo].[DimSalesTerritory_REPLICATE]   
WITH   
  (   
    CLUSTERED COLUMNSTORE INDEX,  
    DISTRIBUTION = REPLICATE  
  )  
AS SELECT * FROM [dbo].[DimSalesTerritory]
OPTION  (LABEL  = 'CTAS : DimSalesTerritory_REPLICATE') 

--Create statistics on new table
CREATE STATISTICS [SalesTerritoryKey] ON [DimSalesTerritory_REPLICATE] ([SalesTerritoryKey]);
CREATE STATISTICS [SalesTerritoryAlternateKey] ON [DimSalesTerritory_REPLICATE] ([SalesTerritoryAlternateKey]);
CREATE STATISTICS [SalesTerritoryRegion] ON [DimSalesTerritory_REPLICATE] ([SalesTerritoryRegion]);
CREATE STATISTICS [SalesTerritoryCountry] ON [DimSalesTerritory_REPLICATE] ([SalesTerritoryCountry]);
CREATE STATISTICS [SalesTerritoryGroup] ON [DimSalesTerritory_REPLICATE] ([SalesTerritoryGroup]);

-- Switch table names
RENAME OBJECT [dbo].[DimSalesTerritory] too[DimSalesTerritory_old];
RENAME OBJECT [dbo].[DimSalesTerritory_REPLICATE] too[DimSalesTerritory];

DROP TABLE [dbo].[DimSalesTerritory_old];
```  

### <a name="query-performance-example-for-round-robin-versus-replicated"></a>Sorgu performansı hepsini karşı örneğin çoğaltılan 

Merhaba tüm tablo her işlem düğümü üzerinde zaten varolduğundan çoğaltılmış tablo birleşimler için tüm veri hareketlerini gerektirmez. Merhaba boyut tabloları dağıtılmış hepsini varsa, bir birleştirme tam tooeach işlem düğümünde hello Boyut tablosuna kopyalar. toomove hello veri hello sorgu planı BroadcastMoveOperation adlı bir işlem içerir. Bu tür veri taşıma işlemi sorgu performansını yavaşlatır ve çoğaltılmış tablolar kullanarak ortadan kalkar. tooview sorgu planı adımları, kullanmak hello [sys.dm_pdw_request_steps](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql) sistem Katalog görünümü. 

Örneğin, hello AdventureWorks şemayla aşağıdaki sorguda hello ` FactInternetSales` tablo karma dağıtılmış. Merhaba `DimDate` ve `DimSalesTerritory` tablolardır daha küçük boyut tabloları. Bu sorgu, Kuzey Amerika'da mali yılın 2004 hello toplam satış döndürür:
 
```sql
SELECT [TotalSalesAmount] = SUM(SalesAmount)
FROM dbo.FactInternetSales s
INNER JOIN dbo.DimDate d
  ON d.DateKey = s.OrderDateKey
INNER JOIN dbo.DimSalesTerritory t
  ON t.SalesTerritoryKey = s.SalesTerritoryKey
WHERE d.FiscalYear = 2004
  AND t.SalesTerritoryGroup = 'North America'
```
Yeniden oluşturduğumuz `DimDate` ve `DimSalesTerritory` hepsini tabloları olarak. Sonuç olarak, hello sorgu işlemleri taşıdığınız çoklu yayın sahip sorgu planı aşağıdaki hello gösterilmiştir: 
 
![Hepsini sorgu planı](media/design-guidance-for-replicated-tables/round-robin-tables-query-plan.jpg) 

Yeniden oluşturduğumuz `DimDate` ve `DimSalesTerritory` olarak çoğaltılmış tablolar ve hello sorgu tekrar çalıştırılmıştır. Hello elde edilen sorgu planı daha kısadır ve mu değil sahip herhangi yayını taşır.

![Sorgu planı çoğaltılan](media/design-guidance-for-replicated-tables/replicated-tables-query-plan.jpg) 


## <a name="performance-considerations-for-modifying-replicated-tables"></a>Çoğaltılmış tabloları değiştirmek için başarım düşünceleri
SQL veri ambarı ana sürüm Merhaba tablonun tutarak çoğaltılmış tablo uygular. Merhaba ana sürüm tooone dağıtım veritabanı her işlem düğümü üzerinde kopyalar. Bir değişiklik olduğunda, SQL Data Warehouse hello ana tablo ilk güncelleştirir. Ardından her işlem düğümünde Merhaba tablonun yeniden gerektirir. Çoğaltılmış bir tablonun yeniden hello tablo tooeach işlem düğümü kopyalama ve hello dizinleri yeniden oluşturma içerir.

Sonra yeniden gereklidir:
- Veri yüklenen ya da değiştirilmiş
- ölçeklendirilmiş tooa farklı DWU ayarını Hello veri ambarıdır.
- Tablo tanımı güncelleştirildi

Yeniden sonra gerekli değildir:
- Duraklatma işlemi
- Sürdürme işlemi

Veri hemen değiştirildikten sonra hello yeniden gerçekleşmez. Bunun yerine, hello yeniden tetiklenir hello ilk kez bir sorgu hello tablosundan seçer.  Merhaba ilk select deyimi hello tablosundan adımları toorebuild hello çoğaltılmış tablo ağdadır.  Merhaba yeniden hello sorguyla yapıldığından hello etkisi toohello ilk select deyiminde hello tablo hello boyutuna bağlı olarak önemli olabilir.  Birden çok çoğaltılmış tablolar yeniden gereken söz konusuysa, her kopya seri olarak hello deyimi içindeki adımları olarak yeniden oluşturulur.  toomaintain veri tutarlılığını hello hello yeniden sırasında özel bir kilit hello tablo üzerinde gerçekleştirilecek tablo çoğaltılan.  Merhaba kilit tüm erişim toohello tablo hello yeniden hello süresince engeller. 

### <a name="use-indexes-conservatively"></a>Dizinleri ölçülü kullanın
Standart dizin oluşturma yöntemleri tooreplicated tabloları uygulayın. SQL veri ambarı her çoğaltılmış tablo dizin hello yeniden parçası olarak yeniden oluşturur. Merhaba performans kazancı hello dizinleri yeniden oluşturma, hello maliyetinden ağır yalnızca dizinler kullanın.  
 
### <a name="batch-data-loads"></a>Toplu veri yükler
Verileri çoğaltılmış tablolara yüklenirken yükleri birlikte toplu işleme tarafından toominimize yeniden deneyin. Select deyimi çalıştırmadan önce tüm toplu hale hello yükleri gerçekleştirin.

Örneğin, bu yük düzeni dört kaynaktan verileri yükler ve dört yeniden çalıştırır. 

- 1 kaynağından yükleyin.
- SELECT deyimi Tetikleyicileri 1 yeniden oluşturun.
- 2 kaynağından yükleyin.
- SELECT deyimi Tetikleyicileri 2 yeniden oluşturun.
- 3 kaynağından yükleyin.
- SELECT deyimi Tetikleyicileri 3 yeniden oluşturun.
- 4 kaynağından yükleyin.
- SELECT deyimi Tetikleyicileri 4 yeniden oluşturun.

Örneğin, bu yük düzeni dört kaynaktan verileri yükler, ancak yalnızca bir yeniden çağırır.

- 1 kaynağından yükleyin.
- 2 kaynağından yükleyin.
- 3 kaynağından yükleyin.
- 4 kaynağından yükleyin.
- SELECT deyimi Tetikleyicileri yeniden oluşturun.


### <a name="rebuild-a-replicated-table-after-a-batch-load"></a>Toplu yükleme sonrasında çoğaltılmış tablo yeniden oluşturma
tooensure tutarlı bir sorgu yürütme sürelerinin toplu yükleme sonrasında hello çoğaltılmış tablolar yenilenmesini zorlama öneririz. Aksi takdirde hello ilk sorgu hello dizinleri yeniden oluşturma içerir hello tabloları toorefresh için beklemeniz gerekir. Merhaba boyut ve etkilenen çoğaltılmış tablolar sayısına bağlı olarak hello performans etkisi önemli olabilir.  

Bu sorgu hello kullanan [sys.pdw_replicated_table_cache_state](https://docs.microsoft.com/sql/relational-databases/system-catalog-views/sys-pdw-replicated-table-cache-state-transact-sql) DMV toolist hello çoğaltılan değiştirildi, ancak değil yeniden tablolar.

```sql 
SELECT [ReplicatedTable] = t.[name]
  FROM sys.tables t  
  JOIN sys.pdw_replicated_table_cache_state c  
    ON c.object_id = t.object_id 
  JOIN sys.pdw_table_distribution_properties p 
    ON p.object_id = t.object_id 
  WHERE c.[state] = 'NotReady'
    AND p.[distribution_policy_desc] = 'REPLICATE'
```
 
Çıktı önceki hello her tablosunda deyiminden hello çalıştırmak tooforce bir yeniden oluşturma. 

```sql
SELECT TOP 1 * FROM [ReplicatedTable]
``` 
 
## <a name="next-steps"></a>Sonraki adımlar 
toocreate çoğaltılmış tablo, bu deyimleri birini kullanın:

- [TABLOSU (Azure SQL Data Warehouse) oluşturma](https://docs.microsoft.com/sql/t-sql/statements/create-table-azure-sql-data-warehouse)
- [TABLE AS SELECT (Azure SQL Data Warehouse oluşturma](https://docs.microsoft.com/sql/t-sql/statements/create-table-as-select-azure-sql-data-warehouse)

Dağıtılmış tabloları genel bakış için bkz: [dağıtılmış tabloları](sql-data-warehouse-tables-distribute.md).



