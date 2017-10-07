---
title: "aaaManage bekletme ilkesine sahip zamana bağlı tablolarda geçmiş verileri | Microsoft Docs"
description: "Bilgi nasıl toouse zamana bağlı bekletme ilkesi tookeep geçmiş verileri denetiminiz altında."
services: sql-database
documentationcenter: 
author: bonova
manager: drasumic
editor: 
ms.assetid: 76cfa06a-e758-453e-942c-9f1ed6a38c2a
ms.service: sql-database
ms.custom: develop databases
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: sql-database
ms.date: 10/12/2016
ms.author: bonova
ms.openlocfilehash: a72a6111a6cd7322d734d08bf3852e95f5ffea8b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-historical-data-in-temporal-tables-with-retention-policy"></a>Zamana bağlı tablolarda geçmiş verilerin bekletme ilkesi ile yönetme
Zamana bağlı tablolarda özellikle uzun bir süre için geçmiş verileri tut normal tablolardaki'birden fazla veritabanı boyutunu artırabilir. Bu nedenle, geçmiş verileri için bekletme ilkesi planlama ve her zamana bağlı tablo hello yaşam döngüsü yönetiminden önemli bir yönü ' dir. Azure SQL veritabanı zamana bağlı tablolarda, bu görevi gerçekleştirmenize yardımcı olan kullanımı kolay bekletme mekanizmasıyla sunulur.

Zamana bağlı geçmiş saklama toocreate esnek eskime ilkeleri kullanıcıların veren hello tek tek tablo düzeyinde yapılandırılabilir. Zamana bağlı bekletme uygulama basittir: Tablo oluşturma veya şema değişikliği sırasında kümesi yalnızca bir parametre toobe gerektirir.

Bekletme İlkesi tanımladıktan sonra Azure SQL veritabanı düzenli aralıklarla otomatik veri temizleme için uygun olan geçmiş satır olup olmadığını denetleme başlatır. Saydam, eşleşen satırları tanımlaması ve bunların kaldırılması hello geçmiş tablosundan zamanlanmış ve hello sistem tarafından çalıştırılan hello arka plan görevi oluşur. Merhaba geçmiş tablo satır için yaş koşul system_tıme süre sonunu temsil eden hello sütun göre denetlenir. Saklama dönemi, örneğin, toosix ayarlanmışsa, ay, temizleme için uygun tablo satırları koşul aşağıdaki hello karşılamak:

````
ValidTo < DATEADD (MONTH, -6, SYSUTCDATETIME())
````

Örnek önceki hello biz, kabul **ValidTo** sütun system_tıme dönemi toohello sonuna karşılık gelir.

## <a name="how-tooconfigure-retention-policy"></a>Nasıl tooconfigure bekletme ilkesi?
Bekletme İlkesi zamana bağlı tablo için yapılandırmadan önce ilk zamana bağlı geçmiş saklama etkinleştirilip etkinleştirilmediğini kontrol *hello veritabanı düzeyinde*.

````
SELECT is_temporal_history_retention_enabled, name
FROM sys.databases
````

Veritabanı bayrağı **is_temporal_history_retention_enabled** varsayılan kümesi tooON olmakla birlikte, kullanıcılar, ALTER DATABASE deyimi ile değiştirebilir. Aynı zamanda otomatik olarak ayarla tooOFF sonra olup [geri yükleme noktası](sql-database-recovery-using-backups.md) işlemi. tooenable zamana bağlı geçmiş saklama temizleme, veritabanınız için aşağıdaki ifadeyi hello yürütün:

````
ALTER DATABASE <myDB>
SET TEMPORAL_HISTORY_RETENTION  ON
````

> [!IMPORTANT]
> Bekletme olsa bile zamana bağlı tablolar için yapılandırabileceğiniz **is_temporal_history_retention_enabled** Kapalı'dır, ancak eski satırlar için otomatik temizleme değil tetiklenir bu durumda.
> 
> 

Bekletme İlkesi hello HISTORY_RETENTION_PERIOD parametresinin değeri belirterek tablo oluşturma sırasında yapılandırılır:

````
CREATE TABLE dbo.WebsiteUserInfo
(  
    [UserID] int NOT NULL PRIMARY KEY CLUSTERED
  , [UserName] nvarchar(100) NOT NULL
  , [PagesVisited] int NOT NULL
  , [ValidFrom] datetime2 (0) GENERATED ALWAYS AS ROW START
  , [ValidTo] datetime2 (0) GENERATED ALWAYS AS ROW END
  , PERIOD FOR SYSTEM_TIME (ValidFrom, ValidTo)
 )  
 WITH
 (
     SYSTEM_VERSIONING = ON
     (
        HISTORY_TABLE = dbo.WebsiteUserInfoHistory,
        HISTORY_RETENTION_PERIOD = 6 MONTHS
     )
 );
````

Azure SQL veritabanı sağlar toospecify Bekletme dönemi farklı zaman birimleri kullanarak: gün, hafta, ay ve yıl. HISTORY_RETENTION_PERIOD atlanırsa, SONSUZ bekletme varsayılır. SONSUZ anahtar sözcüğü açıkça de kullanabilirsiniz.

Bazı senaryolarda tablo oluşturulduktan sonra tooconfigure bekletme isteyebilir veya toochange değer önceden yapılandırılmış. Bu durumda, ALTER TABLE deyimini kullanın:

````
ALTER TABLE dbo.WebsiteUserInfo
SET (SYSTEM_VERSIONING = ON (HISTORY_RETENTION_PERIOD = 9 MONTHS));
````

> [!IMPORTANT]
> System_versıonıng tooOFF ayarı *değil korumak* Bekletme dönemi değeri. System_versıonıng tooON HISTORY_RETENTION_PERIOD olmadan ayarlama açıkça sonuçları hello saklama süresi SONSUZ içinde belirtilen.
> 
> 

Merhaba bekletme ilkesi geçerli durumunu tooreview, o birleştirmeler zamana bağlı bekletme etkinleştirme bayrağını tek tek tablolar için bekletme süreleri ile Merhaba veritabanı düzeyinde kullanım hello aşağıdaki sorgu:

````
SELECT DB.is_temporal_history_retention_enabled,
SCHEMA_NAME(T1.schema_id) AS TemporalTableSchema,
T1.name as TemporalTableName,  SCHEMA_NAME(T2.schema_id) AS HistoryTableSchema,
T2.name as HistoryTableName,T1.history_retention_period,
T1.history_retention_period_unit_desc
FROM sys.tables T1  
OUTER APPLY (select is_temporal_history_retention_enabled from sys.databases
where name = DB_NAME()) AS DB
LEFT JOIN sys.tables T2   
ON T1.history_table_id = T2.object_id WHERE T1.temporal_type = 2
````


## <a name="how-sql-database-deletes-aged-rows"></a>SQL veritabanı nasıl siler satırları eski?
Merhaba temizleme işlemi hello geçmişi tablosunun dizin düzenini hello bağlıdır. Önemli toonotice olduğundan, *yalnızca geçmiş tabloları kümelenmiş bir dizin (B-ağacı veya columnstore) ile sınırlı bekletme ilkesi yapılandırılmış olabilir*. Bir arka plan görevi tooperform eski verileri temizleme tüm zamana bağlı tablolar için sınırlı bekletme süresi ile oluşturulur.
Merhaba rowstore (B-Ağacı) kümelenmiş dizini için Temizle mantığı (yukarı too10K) daha küçük parçalara eski satırda veritabanı günlüğü ve g/ç alt Basıncı en aza siler. Temizleme mantığı kullanır ancak B-Ağacı dizini, saklama dönemi sıkıca garanti edilemez daha eski hello satırları silme sırasını gereklidir. Bu nedenle, *hello temizleme siparişi uygulamalar üzerinde herhangi bir bağımlılığı almayan*.

Merhaba temizleme hello kümelenmiş columnstore için tüm kaldırdığı [satır grupları](https://msdn.microsoft.com/library/gg492088.aspx) aynı anda (genellikle 1 milyon satır her, özellikle geçmiş verileri yüksek hızı oluşturulduğunda çok verimli olduğu içerir).

![Kümelenmiş columnstore bekletme](./media/sql-database-temporal-tables-retention-policy/cciretention.png)

İş yükünüzün yüksek miktarda geçmiş verileri hızlı bir şekilde oluşturduğunda mükemmel veri sıkıştırma ve verimli bekletme temizleme yapar columnstore dizini senaryoları için mükemmel bir seçim kümelenmiş. Bu desene yoğun için tipik [zamana bağlı tablolarda kullanmak işlemsel işleme iş yüklerinin](https://msdn.microsoft.com/library/mt631669.aspx) değişiklik izleme ve denetleme, eğilim analizi veya IOT veri alımı için.

## <a name="index-considerations"></a>Dizin konuları
Merhaba temizleme görevini rowstore kümelenmiş dizine sahip tablolar için dizin toostart hello sütun karşılık gelen hello sonuna system_tıme dönemi ile gerektirir. Bu tür dizin yoksa, sonlu saklama dönemi yapılandıramazsınız:

*Msg 13765, Level 16, State 1 <br> </br> sonlu saklama dönemi ayarlama başarısız oldu: 'temporalstagetestdb.dbo.WebsiteUserInfo' sistem sürümü tutulan zamana bağlı tablo üzerinde olduğundan hello geçmiş tablosu ' temporalstagetestdb.dbo.WebsiteUserInfoHistory' gerekli kümelenmiş dizin içermiyor. Kümelenmiş columnstore veya system_tıme sonuna eşleşen hello sütundan başlayarak B-Ağacı dizini oluşturmayı düşünün hello geçmiş tablosunda, dönem.*

Azure SQL veritabanı tarafından önceden oluşturulmuş varsayılan geçmiş tablosu hello toonotice bekletme ilkesi uyumlu dizin kümelenmiş önemlidir. Bu dizin sonlu saklama süresi olan bir tabloda tooremove çalışırsanız, işlem hello aşağıdaki hata ile başarısız olur:

*Msg 13766, Level 16, State 1 <br> </br> eski verileri otomatik temizleme için kullanıldığından 'WebsiteUserInfoHistory.IX_WebsiteUserInfoHistory' hello kümelenmiş dizini bırakılamıyor. Bu dizin toodrop gerekirse ayarı HISTORY_RETENTION_PERIOD tooINFINITE hello karşılık gelen sistem sürümü tutulan zamana bağlı tabloda göz önünde bulundurun.*

Geçmiş satırları hello geçmiş tablosu hello tarafından özel olarak sistemi_ doldurulduğunda olduğu her zaman hello olduğu (Merhaba dönem sütunu sonuna sıralı), artan hello eklenirse temizleme hello kümelenmiş columnstore dizini üzerinde en iyi şekilde çalışır VERSIONIOING mekanizması. Merhaba geçmiş tablosundaki satırları (var olan geçmiş veri geçişi yaptıysanız olabilen hello çalışması) dönem sütunu sonuna sıralanmaz, doğru en iyi tooachieve sıralanır B-Ağacı rowstore dizini üstünde kümelenmiş columnstore dizini yeniden oluşturmanız gerekir performans.

Hello sınırlı bekletme süresi ile Merhaba geçmiş tablosunda kümelenmiş columnstore dizinini yeniden oluşturmayı kaçının, çünkü hello satır grupları doğal hello sistem sürümü oluşturma işlemi tarafından uygulanan sıralama değişebilir. Hello geçmiş tablosu toorebuild kümelenmiş columnstore dizini ihtiyacınız varsa, onu hello rowgroups normal veri temizleme için gerekli sıralama koruma uyumlu B-Ağacı dizini üstünde yeniden oluşturarak yapabilirsiniz. sütun dizini garantili veri sırası olmadan kümelenmiş varolan geçmiş tablosu ile zamana bağlı tablo oluşturursanız, aynı yaklaşımı alınıp alınmayacağını hello:

````
/*Create B-tree ordered by hello end of period column*/
CREATE CLUSTERED INDEX IX_WebsiteUserInfoHistory ON WebsiteUserInfoHistory (ValidTo)
WITH (DROP_EXISTING = ON);
GO
/*Re-create clustered columnstore index*/
CREATE CLUSTERED COLUMNSTORE INDEX IX_WebsiteUserInfoHistory ON WebsiteUserInfoHistory
WITH (DROP_EXISTING = ON);
````

Sınırlı saklama dönemi hello kümelenmiş columnstore dizini olan hello geçmiş tablosu için yapılandırıldığında, o tablosunda kümelenmemiş ek B-Ağacı dizinleri oluşturulamıyor:

````
CREATE NONCLUSTERED INDEX IX_WebHistNCI ON WebsiteUserInfoHistory ([UserName])
````

Bir girişim tooexecute deyimi yukarıda hello aşağıdaki hata ile başarısız olur:

*Msg 13772, Level 16, State 1 <br> </br> sonlu saklama dönemi ve tanımlanan kümelenmiş columnstore dizini bulunduğundan kümelenmemiş dizin 'WebsiteUserInfoHistory' zamana bağlı geçmiş tablosu üzerinde oluşturulamıyor.*

## <a name="querying-tables-with-retention-policy"></a>Bekletme İlkesi tablolarla sorgulama
Merhaba zamana bağlı tabloda tüm sorguları otomatik olarak eski satırlar hello temizleme görevi tarafından silinebilir beri sınırlı bekletme ilkesi, tooavoid öngörülemeyen ve tutarsız sonuçlar eşleşen geçmiş satırları filtreler *herhangi bir noktada zaman hem de rastgele sipariş*.

Merhaba aşağıdaki resimde hello basit bir sorgu için sorgu planı gösterilmiştir:

````
SELECT * FROM dbo.WebsiteUserInfo FOR SYSTEM_TIME ALL;
````

Merhaba sorgu planı ek filtre ekler dönem sütunu (ValidTo) tooend hello kümelenmiş dizin tarama işleci (vurgulanan) hello geçmiş tablosu üzerinde uygulanır. Bu örnek, bir ay saklama dönemi WebsiteUserInfo tablosunda ayarlamak varsayar.

![Bekletme sorgu filtresi](./media/sql-database-temporal-tables-retention-policy/queryexecplanwithretention.png)

Ancak, geçmiş tablosu doğrudan sorgu, dönem ancak hiçbir garanti olmaksızın yinelenebilir sorgu sonuçları için belirtilen bekletme eski olan satırları görebilirsiniz. Merhaba aşağıdaki resimde hello sorgu için sorgu yürütme planı hello geçmiş tablosunda uygulanan ek filtreler gösterilmiştir:

![Geçmiş saklama filtresi olmadan sorgulama](./media/sql-database-temporal-tables-retention-policy/queryexecplanhistorytable.png)

İş mantığınızın tutarsız veya beklenmeyen sonuçlar alabilirsiniz gibi geçmiş tablosu saklama dönemi ötesinde okuma kullanmayın. Zamana bağlı sorguları zamana bağlı tablolardaki verileri çözümlemek için FOR system_tıme yan tümcesiyle birlikte kullanmanızı öneririz.

## <a name="point-in-time-restore-considerations"></a>Zaman geri yükleme hakkında önemli noktalar noktası
Yeni veritabanı tarafından oluşturduğunuzda [zamanında varolan veritabanı tooa belirli noktası geri](sql-database-recovery-using-backups.md), hello veritabanı düzeyinde devre dışı zamana bağlı bekletme sahiptir. (**is_temporal_history_retention_enabled** bayrağı ayarlanmış tooOFF). Bu işlev satır eski tüm geçmiş satırları kaygısı olmadan geri yükleme sırasında tooquery ulaşmadan kaldırılır tooexamine sağlar bunları. Çok kullanabilirsiniz*ötesinde yapılandırılan saklama süresi geçmiş verileri*.

Zamana bağlı tablo bir ay Bekletme dönemi belirtilen olduğunu varsayalım. Veritabanınızı Premium hizmet katmanında oluşturduysanız mümkün toocreate veritabanı kopyası too35 günlerini hello geçmiş edilene hello veritabanı durumuyla olacaktır. Etkili bir şekilde, too65 günden eski hello geçmiş tablosu doğrudan sorgulayarak tooanalyze geçmiş satır olanak tanır.

Tooactivate zamana bağlı bekletme temizleme istiyorsanız, bir noktaya geri yükleme sonrasında Transact-SQL deyimi aşağıdaki hello çalıştırın:

````
ALTER DATABASE <myDB>
SET TEMPORAL_HISTORY_RETENTION  ON
````

## <a name="next-steps"></a>Sonraki adımlar
uygulamalarınızı, zamana bağlı tablolarda toouse nasıl kullanıma toolearn [zamana bağlı tablolarda Azure SQL veritabanı ile çalışmaya başlama](sql-database-temporal-tables.md).

Ziyaret kanal 9 toohear bir [gerçek müşteri zamana bağlı uygulama başarı Öykü](https://channel9.msdn.com/Blogs/jsturtevant/Azure-SQL-Temporal-Tables-with-RockStep-Solutions) ve izleme bir [zamana bağlı tanıtım canlı](https://channel9.msdn.com/Shows/Data-Exposed/Temporal-in-SQL-Server-2016).

Zamana bağlı tablolarda hakkında ayrıntılı bilgi için gözden [MSDN belgelerine](https://msdn.microsoft.com/library/dn935015.aspx).

