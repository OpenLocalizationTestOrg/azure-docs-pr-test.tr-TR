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
# <a name="manage-historical-data-in-temporal-tables-with-retention-policy"></a><span data-ttu-id="0955f-103">Zamana bağlı tablolarda geçmiş verilerin bekletme ilkesi ile yönetme</span><span class="sxs-lookup"><span data-stu-id="0955f-103">Manage historical data in Temporal Tables with retention policy</span></span>
<span data-ttu-id="0955f-104">Zamana bağlı tablolarda özellikle uzun bir süre için geçmiş verileri tut normal tablolardaki'birden fazla veritabanı boyutunu artırabilir.</span><span class="sxs-lookup"><span data-stu-id="0955f-104">Temporal Tables may increase database size more than regular tables, especially if you retain historical data for a longer period of time.</span></span> <span data-ttu-id="0955f-105">Bu nedenle, geçmiş verileri için bekletme ilkesi planlama ve her zamana bağlı tablo hello yaşam döngüsü yönetiminden önemli bir yönü ' dir.</span><span class="sxs-lookup"><span data-stu-id="0955f-105">Hence, retention policy for historical data is an important aspect of planning and managing hello lifecycle of every temporal table.</span></span> <span data-ttu-id="0955f-106">Azure SQL veritabanı zamana bağlı tablolarda, bu görevi gerçekleştirmenize yardımcı olan kullanımı kolay bekletme mekanizmasıyla sunulur.</span><span class="sxs-lookup"><span data-stu-id="0955f-106">Temporal Tables in Azure SQL Database come with easy-to-use retention mechanism that helps you accomplish this task.</span></span>

<span data-ttu-id="0955f-107">Zamana bağlı geçmiş saklama toocreate esnek eskime ilkeleri kullanıcıların veren hello tek tek tablo düzeyinde yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="0955f-107">Temporal history retention can be configured at hello individual table level, which allows users toocreate flexible aging polices.</span></span> <span data-ttu-id="0955f-108">Zamana bağlı bekletme uygulama basittir: Tablo oluşturma veya şema değişikliği sırasında kümesi yalnızca bir parametre toobe gerektirir.</span><span class="sxs-lookup"><span data-stu-id="0955f-108">Applying temporal retention is simple: it requires only one parameter toobe set during table creation or schema change.</span></span>

<span data-ttu-id="0955f-109">Bekletme İlkesi tanımladıktan sonra Azure SQL veritabanı düzenli aralıklarla otomatik veri temizleme için uygun olan geçmiş satır olup olmadığını denetleme başlatır.</span><span class="sxs-lookup"><span data-stu-id="0955f-109">After you define retention policy, Azure SQL Database starts checking regularly if there are historical rows that are eligible for automatic data cleanup.</span></span> <span data-ttu-id="0955f-110">Saydam, eşleşen satırları tanımlaması ve bunların kaldırılması hello geçmiş tablosundan zamanlanmış ve hello sistem tarafından çalıştırılan hello arka plan görevi oluşur.</span><span class="sxs-lookup"><span data-stu-id="0955f-110">Identification of matching rows and their removal from hello history table occur transparently, in hello background task that is scheduled and run by hello system.</span></span> <span data-ttu-id="0955f-111">Merhaba geçmiş tablo satır için yaş koşul system_tıme süre sonunu temsil eden hello sütun göre denetlenir.</span><span class="sxs-lookup"><span data-stu-id="0955f-111">Age condition for hello history table rows is checked based on hello column representing end of SYSTEM_TIME period.</span></span> <span data-ttu-id="0955f-112">Saklama dönemi, örneğin, toosix ayarlanmışsa, ay, temizleme için uygun tablo satırları koşul aşağıdaki hello karşılamak:</span><span class="sxs-lookup"><span data-stu-id="0955f-112">If retention period, for example, is set toosix months, table rows eligible for cleanup satisfy hello following condition:</span></span>

````
ValidTo < DATEADD (MONTH, -6, SYSUTCDATETIME())
````

<span data-ttu-id="0955f-113">Örnek önceki hello biz, kabul **ValidTo** sütun system_tıme dönemi toohello sonuna karşılık gelir.</span><span class="sxs-lookup"><span data-stu-id="0955f-113">In hello preceding example, we assumed that **ValidTo** column corresponds toohello end of SYSTEM_TIME period.</span></span>

## <a name="how-tooconfigure-retention-policy"></a><span data-ttu-id="0955f-114">Nasıl tooconfigure bekletme ilkesi?</span><span class="sxs-lookup"><span data-stu-id="0955f-114">How tooconfigure retention policy?</span></span>
<span data-ttu-id="0955f-115">Bekletme İlkesi zamana bağlı tablo için yapılandırmadan önce ilk zamana bağlı geçmiş saklama etkinleştirilip etkinleştirilmediğini kontrol *hello veritabanı düzeyinde*.</span><span class="sxs-lookup"><span data-stu-id="0955f-115">Before you configure retention policy for a temporal table, check first whether temporal historical retention is enabled *at hello database level*.</span></span>

````
SELECT is_temporal_history_retention_enabled, name
FROM sys.databases
````

<span data-ttu-id="0955f-116">Veritabanı bayrağı **is_temporal_history_retention_enabled** varsayılan kümesi tooON olmakla birlikte, kullanıcılar, ALTER DATABASE deyimi ile değiştirebilir.</span><span class="sxs-lookup"><span data-stu-id="0955f-116">Database flag **is_temporal_history_retention_enabled** is set tooON by default, but users can change it with ALTER DATABASE statement.</span></span> <span data-ttu-id="0955f-117">Aynı zamanda otomatik olarak ayarla tooOFF sonra olup [geri yükleme noktası](sql-database-recovery-using-backups.md) işlemi.</span><span class="sxs-lookup"><span data-stu-id="0955f-117">It is also automatically set tooOFF after [point in time restore](sql-database-recovery-using-backups.md) operation.</span></span> <span data-ttu-id="0955f-118">tooenable zamana bağlı geçmiş saklama temizleme, veritabanınız için aşağıdaki ifadeyi hello yürütün:</span><span class="sxs-lookup"><span data-stu-id="0955f-118">tooenable temporal history retention cleanup for your database, execute hello following statement:</span></span>

````
ALTER DATABASE <myDB>
SET TEMPORAL_HISTORY_RETENTION  ON
````

> [!IMPORTANT]
> <span data-ttu-id="0955f-119">Bekletme olsa bile zamana bağlı tablolar için yapılandırabileceğiniz **is_temporal_history_retention_enabled** Kapalı'dır, ancak eski satırlar için otomatik temizleme değil tetiklenir bu durumda.</span><span class="sxs-lookup"><span data-stu-id="0955f-119">You can configure retention for temporal tables even if **is_temporal_history_retention_enabled** is OFF, but automatic cleanup for aged rows is not triggered in that case.</span></span>
> 
> 

<span data-ttu-id="0955f-120">Bekletme İlkesi hello HISTORY_RETENTION_PERIOD parametresinin değeri belirterek tablo oluşturma sırasında yapılandırılır:</span><span class="sxs-lookup"><span data-stu-id="0955f-120">Retention policy is configured during table creation by specifying value for hello HISTORY_RETENTION_PERIOD parameter:</span></span>

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

<span data-ttu-id="0955f-121">Azure SQL veritabanı sağlar toospecify Bekletme dönemi farklı zaman birimleri kullanarak: gün, hafta, ay ve yıl.</span><span class="sxs-lookup"><span data-stu-id="0955f-121">Azure SQL Database allows you toospecify retention period by using different time units: DAYS, WEEKS, MONTHS, and YEARS.</span></span> <span data-ttu-id="0955f-122">HISTORY_RETENTION_PERIOD atlanırsa, SONSUZ bekletme varsayılır.</span><span class="sxs-lookup"><span data-stu-id="0955f-122">If HISTORY_RETENTION_PERIOD is omitted, INFINITE retention is assumed.</span></span> <span data-ttu-id="0955f-123">SONSUZ anahtar sözcüğü açıkça de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0955f-123">You can also use INFINITE keyword explicitly.</span></span>

<span data-ttu-id="0955f-124">Bazı senaryolarda tablo oluşturulduktan sonra tooconfigure bekletme isteyebilir veya toochange değer önceden yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="0955f-124">In some scenarios, you may want tooconfigure retention after table creation, or toochange previously configured value.</span></span> <span data-ttu-id="0955f-125">Bu durumda, ALTER TABLE deyimini kullanın:</span><span class="sxs-lookup"><span data-stu-id="0955f-125">In that case use ALTER TABLE statement:</span></span>

````
ALTER TABLE dbo.WebsiteUserInfo
SET (SYSTEM_VERSIONING = ON (HISTORY_RETENTION_PERIOD = 9 MONTHS));
````

> [!IMPORTANT]
> <span data-ttu-id="0955f-126">System_versıonıng tooOFF ayarı *değil korumak* Bekletme dönemi değeri.</span><span class="sxs-lookup"><span data-stu-id="0955f-126">Setting SYSTEM_VERSIONING tooOFF *does not preserve* retention period value.</span></span> <span data-ttu-id="0955f-127">System_versıonıng tooON HISTORY_RETENTION_PERIOD olmadan ayarlama açıkça sonuçları hello saklama süresi SONSUZ içinde belirtilen.</span><span class="sxs-lookup"><span data-stu-id="0955f-127">Setting SYSTEM_VERSIONING tooON without HISTORY_RETENTION_PERIOD specified explicitly results in hello INFINITE retention period.</span></span>
> 
> 

<span data-ttu-id="0955f-128">Merhaba bekletme ilkesi geçerli durumunu tooreview, o birleştirmeler zamana bağlı bekletme etkinleştirme bayrağını tek tek tablolar için bekletme süreleri ile Merhaba veritabanı düzeyinde kullanım hello aşağıdaki sorgu:</span><span class="sxs-lookup"><span data-stu-id="0955f-128">tooreview current state of hello retention policy, use hello following query that joins temporal retention enablement flag at hello database level with retention periods for individual tables:</span></span>

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


## <a name="how-sql-database-deletes-aged-rows"></a><span data-ttu-id="0955f-129">SQL veritabanı nasıl siler satırları eski?</span><span class="sxs-lookup"><span data-stu-id="0955f-129">How SQL Database deletes aged rows?</span></span>
<span data-ttu-id="0955f-130">Merhaba temizleme işlemi hello geçmişi tablosunun dizin düzenini hello bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="0955f-130">hello cleanup process depends on hello index layout of hello history table.</span></span> <span data-ttu-id="0955f-131">Önemli toonotice olduğundan, *yalnızca geçmiş tabloları kümelenmiş bir dizin (B-ağacı veya columnstore) ile sınırlı bekletme ilkesi yapılandırılmış olabilir*.</span><span class="sxs-lookup"><span data-stu-id="0955f-131">It is important toonotice that *only history tables with a clustered index (B-tree or columnstore) can have finite retention policy configured*.</span></span> <span data-ttu-id="0955f-132">Bir arka plan görevi tooperform eski verileri temizleme tüm zamana bağlı tablolar için sınırlı bekletme süresi ile oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="0955f-132">A background task is created tooperform aged data cleanup for all temporal tables with finite retention period.</span></span>
<span data-ttu-id="0955f-133">Merhaba rowstore (B-Ağacı) kümelenmiş dizini için Temizle mantığı (yukarı too10K) daha küçük parçalara eski satırda veritabanı günlüğü ve g/ç alt Basıncı en aza siler.</span><span class="sxs-lookup"><span data-stu-id="0955f-133">Cleanup logic for hello rowstore (B-tree) clustered index deletes aged row in smaller chunks (up too10K) minimizing pressure on database log and I/O subsystem.</span></span> <span data-ttu-id="0955f-134">Temizleme mantığı kullanır ancak B-Ağacı dizini, saklama dönemi sıkıca garanti edilemez daha eski hello satırları silme sırasını gereklidir.</span><span class="sxs-lookup"><span data-stu-id="0955f-134">Although cleanup logic utilizes required B-tree index, order of deletions for hello rows older than retention period cannot be firmly guaranteed.</span></span> <span data-ttu-id="0955f-135">Bu nedenle, *hello temizleme siparişi uygulamalar üzerinde herhangi bir bağımlılığı almayan*.</span><span class="sxs-lookup"><span data-stu-id="0955f-135">Hence, *do not take any dependency on hello cleanup order in your applications*.</span></span>

<span data-ttu-id="0955f-136">Merhaba temizleme hello kümelenmiş columnstore için tüm kaldırdığı [satır grupları](https://msdn.microsoft.com/library/gg492088.aspx) aynı anda (genellikle 1 milyon satır her, özellikle geçmiş verileri yüksek hızı oluşturulduğunda çok verimli olduğu içerir).</span><span class="sxs-lookup"><span data-stu-id="0955f-136">hello cleanup task for hello clustered columnstore removes entire [row groups](https://msdn.microsoft.com/library/gg492088.aspx) at once (typically contain 1 million of rows each), which is very efficient, especially when historical data is generated at a high pace.</span></span>

![Kümelenmiş columnstore bekletme](./media/sql-database-temporal-tables-retention-policy/cciretention.png)

<span data-ttu-id="0955f-138">İş yükünüzün yüksek miktarda geçmiş verileri hızlı bir şekilde oluşturduğunda mükemmel veri sıkıştırma ve verimli bekletme temizleme yapar columnstore dizini senaryoları için mükemmel bir seçim kümelenmiş.</span><span class="sxs-lookup"><span data-stu-id="0955f-138">Excellent data compression and efficient retention cleanup makes clustered columnstore index a perfect choice for scenarios when your workload rapidly generates high amount of historical data.</span></span> <span data-ttu-id="0955f-139">Bu desene yoğun için tipik [zamana bağlı tablolarda kullanmak işlemsel işleme iş yüklerinin](https://msdn.microsoft.com/library/mt631669.aspx) değişiklik izleme ve denetleme, eğilim analizi veya IOT veri alımı için.</span><span class="sxs-lookup"><span data-stu-id="0955f-139">That pattern is typical for intensive [transactional processing workloads that use temporal tables](https://msdn.microsoft.com/library/mt631669.aspx) for change tracking and auditing, trend analysis, or IoT data ingestion.</span></span>

## <a name="index-considerations"></a><span data-ttu-id="0955f-140">Dizin konuları</span><span class="sxs-lookup"><span data-stu-id="0955f-140">Index considerations</span></span>
<span data-ttu-id="0955f-141">Merhaba temizleme görevini rowstore kümelenmiş dizine sahip tablolar için dizin toostart hello sütun karşılık gelen hello sonuna system_tıme dönemi ile gerektirir.</span><span class="sxs-lookup"><span data-stu-id="0955f-141">hello cleanup task for tables with rowstore clustered index requires index toostart with hello column corresponding hello end of SYSTEM_TIME period.</span></span> <span data-ttu-id="0955f-142">Bu tür dizin yoksa, sonlu saklama dönemi yapılandıramazsınız:</span><span class="sxs-lookup"><span data-stu-id="0955f-142">If such index doesn't exist, you cannot configure a finite retention period:</span></span>

<span data-ttu-id="0955f-143">*Msg 13765, Level 16, State 1 <br> </br> sonlu saklama dönemi ayarlama başarısız oldu: 'temporalstagetestdb.dbo.WebsiteUserInfo' sistem sürümü tutulan zamana bağlı tablo üzerinde olduğundan hello geçmiş tablosu ' temporalstagetestdb.dbo.WebsiteUserInfoHistory' gerekli kümelenmiş dizin içermiyor. Kümelenmiş columnstore veya system_tıme sonuna eşleşen hello sütundan başlayarak B-Ağacı dizini oluşturmayı düşünün hello geçmiş tablosunda, dönem.*</span><span class="sxs-lookup"><span data-stu-id="0955f-143">*Msg 13765, Level 16, State 1 <br></br> Setting finite retention period failed on system-versioned temporal table 'temporalstagetestdb.dbo.WebsiteUserInfo' because hello history table 'temporalstagetestdb.dbo.WebsiteUserInfoHistory' does not contain required clustered index. Consider creating a clustered columnstore or B-tree index starting with hello column that matches end of SYSTEM_TIME period, on hello history table.*</span></span>

<span data-ttu-id="0955f-144">Azure SQL veritabanı tarafından önceden oluşturulmuş varsayılan geçmiş tablosu hello toonotice bekletme ilkesi uyumlu dizin kümelenmiş önemlidir.</span><span class="sxs-lookup"><span data-stu-id="0955f-144">It is important toonotice that hello default history table created by Azure SQL Database already has clustered index, which is compliant for retention policy.</span></span> <span data-ttu-id="0955f-145">Bu dizin sonlu saklama süresi olan bir tabloda tooremove çalışırsanız, işlem hello aşağıdaki hata ile başarısız olur:</span><span class="sxs-lookup"><span data-stu-id="0955f-145">If you try tooremove that index on a table with finite retention period, operation fails with hello following error:</span></span>

<span data-ttu-id="0955f-146">*Msg 13766, Level 16, State 1 <br> </br> eski verileri otomatik temizleme için kullanıldığından 'WebsiteUserInfoHistory.IX_WebsiteUserInfoHistory' hello kümelenmiş dizini bırakılamıyor. Bu dizin toodrop gerekirse ayarı HISTORY_RETENTION_PERIOD tooINFINITE hello karşılık gelen sistem sürümü tutulan zamana bağlı tabloda göz önünde bulundurun.*</span><span class="sxs-lookup"><span data-stu-id="0955f-146">*Msg 13766, Level 16, State 1 <br></br> Cannot drop hello clustered index 'WebsiteUserInfoHistory.IX_WebsiteUserInfoHistory' because it is being used for automatic cleanup of aged data. Consider setting HISTORY_RETENTION_PERIOD tooINFINITE on hello corresponding system-versioned temporal table if you need toodrop this index.*</span></span>

<span data-ttu-id="0955f-147">Geçmiş satırları hello geçmiş tablosu hello tarafından özel olarak sistemi_ doldurulduğunda olduğu her zaman hello olduğu (Merhaba dönem sütunu sonuna sıralı), artan hello eklenirse temizleme hello kümelenmiş columnstore dizini üzerinde en iyi şekilde çalışır VERSIONIOING mekanizması.</span><span class="sxs-lookup"><span data-stu-id="0955f-147">Cleanup on hello clustered columnstore index works optimally if historical rows are inserted in hello ascending order (ordered by hello end of period column), which is always hello case when hello history table is populated exclusively by hello SYSTEM_VERSIONIOING mechanism.</span></span> <span data-ttu-id="0955f-148">Merhaba geçmiş tablosundaki satırları (var olan geçmiş veri geçişi yaptıysanız olabilen hello çalışması) dönem sütunu sonuna sıralanmaz, doğru en iyi tooachieve sıralanır B-Ağacı rowstore dizini üstünde kümelenmiş columnstore dizini yeniden oluşturmanız gerekir performans.</span><span class="sxs-lookup"><span data-stu-id="0955f-148">If rows in hello history table are not ordered by end of period column (which may be hello case if you migrated existing historical data), you should re-create clustered columnstore index on top of B-tree rowstore index that is properly ordered, tooachieve optimal performance.</span></span>

<span data-ttu-id="0955f-149">Hello sınırlı bekletme süresi ile Merhaba geçmiş tablosunda kümelenmiş columnstore dizinini yeniden oluşturmayı kaçının, çünkü hello satır grupları doğal hello sistem sürümü oluşturma işlemi tarafından uygulanan sıralama değişebilir.</span><span class="sxs-lookup"><span data-stu-id="0955f-149">Avoid rebuilding clustered columnstore index on hello history table with hello finite retention period, because it may change ordering in hello row groups naturally imposed by hello system-versioning operation.</span></span> <span data-ttu-id="0955f-150">Hello geçmiş tablosu toorebuild kümelenmiş columnstore dizini ihtiyacınız varsa, onu hello rowgroups normal veri temizleme için gerekli sıralama koruma uyumlu B-Ağacı dizini üstünde yeniden oluşturarak yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0955f-150">If you need toorebuild clustered columnstore index on hello history table, do that by re-creating it on top of compliant B-tree index, preserving ordering in hello rowgroups necessary for regular data cleanup.</span></span> <span data-ttu-id="0955f-151">sütun dizini garantili veri sırası olmadan kümelenmiş varolan geçmiş tablosu ile zamana bağlı tablo oluşturursanız, aynı yaklaşımı alınıp alınmayacağını hello:</span><span class="sxs-lookup"><span data-stu-id="0955f-151">hello same approach should be taken if you create temporal table with existing history table that has clustered column index without guaranteed data order:</span></span>

````
/*Create B-tree ordered by hello end of period column*/
CREATE CLUSTERED INDEX IX_WebsiteUserInfoHistory ON WebsiteUserInfoHistory (ValidTo)
WITH (DROP_EXISTING = ON);
GO
/*Re-create clustered columnstore index*/
CREATE CLUSTERED COLUMNSTORE INDEX IX_WebsiteUserInfoHistory ON WebsiteUserInfoHistory
WITH (DROP_EXISTING = ON);
````

<span data-ttu-id="0955f-152">Sınırlı saklama dönemi hello kümelenmiş columnstore dizini olan hello geçmiş tablosu için yapılandırıldığında, o tablosunda kümelenmemiş ek B-Ağacı dizinleri oluşturulamıyor:</span><span class="sxs-lookup"><span data-stu-id="0955f-152">When finite retention period is configured for hello history table with hello clustered columnstore index, you cannot create additional non-clustered B-tree indexes on that table:</span></span>

````
CREATE NONCLUSTERED INDEX IX_WebHistNCI ON WebsiteUserInfoHistory ([UserName])
````

<span data-ttu-id="0955f-153">Bir girişim tooexecute deyimi yukarıda hello aşağıdaki hata ile başarısız olur:</span><span class="sxs-lookup"><span data-stu-id="0955f-153">An attempt tooexecute above statement fails with hello following error:</span></span>

<span data-ttu-id="0955f-154">*Msg 13772, Level 16, State 1 <br> </br> sonlu saklama dönemi ve tanımlanan kümelenmiş columnstore dizini bulunduğundan kümelenmemiş dizin 'WebsiteUserInfoHistory' zamana bağlı geçmiş tablosu üzerinde oluşturulamıyor.*</span><span class="sxs-lookup"><span data-stu-id="0955f-154">*Msg 13772, Level 16, State 1 <br></br> Cannot create non-clustered index on a temporal history table 'WebsiteUserInfoHistory' since it has finite retention period and clustered columnstore index defined.*</span></span>

## <a name="querying-tables-with-retention-policy"></a><span data-ttu-id="0955f-155">Bekletme İlkesi tablolarla sorgulama</span><span class="sxs-lookup"><span data-stu-id="0955f-155">Querying tables with retention policy</span></span>
<span data-ttu-id="0955f-156">Merhaba zamana bağlı tabloda tüm sorguları otomatik olarak eski satırlar hello temizleme görevi tarafından silinebilir beri sınırlı bekletme ilkesi, tooavoid öngörülemeyen ve tutarsız sonuçlar eşleşen geçmiş satırları filtreler *herhangi bir noktada zaman hem de rastgele sipariş*.</span><span class="sxs-lookup"><span data-stu-id="0955f-156">All queries on hello temporal table automatically filter out historical rows matching finite retention policy, tooavoid unpredictable and inconsistent results, since aged rows can be deleted by hello cleanup task, *at any point in time and in arbitrary order*.</span></span>

<span data-ttu-id="0955f-157">Merhaba aşağıdaki resimde hello basit bir sorgu için sorgu planı gösterilmiştir:</span><span class="sxs-lookup"><span data-stu-id="0955f-157">hello following picture shows hello query plan for a simple query:</span></span>

````
SELECT * FROM dbo.WebsiteUserInfo FOR SYSTEM_TIME ALL;
````

<span data-ttu-id="0955f-158">Merhaba sorgu planı ek filtre ekler dönem sütunu (ValidTo) tooend hello kümelenmiş dizin tarama işleci (vurgulanan) hello geçmiş tablosu üzerinde uygulanır.</span><span class="sxs-lookup"><span data-stu-id="0955f-158">hello query plan includes additional filter applied tooend of period column (ValidTo) in hello Clustered Index Scan operator on hello history table (highlighted).</span></span> <span data-ttu-id="0955f-159">Bu örnek, bir ay saklama dönemi WebsiteUserInfo tablosunda ayarlamak varsayar.</span><span class="sxs-lookup"><span data-stu-id="0955f-159">This example assumes that one MONTH retention period was set on WebsiteUserInfo table.</span></span>

![Bekletme sorgu filtresi](./media/sql-database-temporal-tables-retention-policy/queryexecplanwithretention.png)

<span data-ttu-id="0955f-161">Ancak, geçmiş tablosu doğrudan sorgu, dönem ancak hiçbir garanti olmaksızın yinelenebilir sorgu sonuçları için belirtilen bekletme eski olan satırları görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0955f-161">However, if you query history table directly, you may see rows that are older than specified retention period, but without any guarantee for repeatable query results.</span></span> <span data-ttu-id="0955f-162">Merhaba aşağıdaki resimde hello sorgu için sorgu yürütme planı hello geçmiş tablosunda uygulanan ek filtreler gösterilmiştir:</span><span class="sxs-lookup"><span data-stu-id="0955f-162">hello following picture shows query execution plan for hello query on hello history table without additional filters applied:</span></span>

![Geçmiş saklama filtresi olmadan sorgulama](./media/sql-database-temporal-tables-retention-policy/queryexecplanhistorytable.png)

<span data-ttu-id="0955f-164">İş mantığınızın tutarsız veya beklenmeyen sonuçlar alabilirsiniz gibi geçmiş tablosu saklama dönemi ötesinde okuma kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="0955f-164">Do not rely your business logic on reading history table beyond retention period as you may get inconsistent or unexpected results.</span></span> <span data-ttu-id="0955f-165">Zamana bağlı sorguları zamana bağlı tablolardaki verileri çözümlemek için FOR system_tıme yan tümcesiyle birlikte kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="0955f-165">We recommend that you use temporal queries with FOR SYSTEM_TIME clause for analyzing data in temporal tables.</span></span>

## <a name="point-in-time-restore-considerations"></a><span data-ttu-id="0955f-166">Zaman geri yükleme hakkında önemli noktalar noktası</span><span class="sxs-lookup"><span data-stu-id="0955f-166">Point in time restore considerations</span></span>
<span data-ttu-id="0955f-167">Yeni veritabanı tarafından oluşturduğunuzda [zamanında varolan veritabanı tooa belirli noktası geri](sql-database-recovery-using-backups.md), hello veritabanı düzeyinde devre dışı zamana bağlı bekletme sahiptir.</span><span class="sxs-lookup"><span data-stu-id="0955f-167">When you create new database by [restoring existing database tooa specific point in time](sql-database-recovery-using-backups.md), it has temporal retention disabled at hello database level.</span></span> <span data-ttu-id="0955f-168">(**is_temporal_history_retention_enabled** bayrağı ayarlanmış tooOFF).</span><span class="sxs-lookup"><span data-stu-id="0955f-168">(**is_temporal_history_retention_enabled** flag set tooOFF).</span></span> <span data-ttu-id="0955f-169">Bu işlev satır eski tüm geçmiş satırları kaygısı olmadan geri yükleme sırasında tooquery ulaşmadan kaldırılır tooexamine sağlar bunları.</span><span class="sxs-lookup"><span data-stu-id="0955f-169">This functionality allows you tooexamine all historical rows upon restore, without worrying that aged rows are removed before you get tooquery them.</span></span> <span data-ttu-id="0955f-170">Çok kullanabilirsiniz*ötesinde yapılandırılan saklama süresi geçmiş verileri*.</span><span class="sxs-lookup"><span data-stu-id="0955f-170">You can use it too*inspect historical data beyond configured retention period*.</span></span>

<span data-ttu-id="0955f-171">Zamana bağlı tablo bir ay Bekletme dönemi belirtilen olduğunu varsayalım.</span><span class="sxs-lookup"><span data-stu-id="0955f-171">Say that a temporal table has one MONTH retention period specified.</span></span> <span data-ttu-id="0955f-172">Veritabanınızı Premium hizmet katmanında oluşturduysanız mümkün toocreate veritabanı kopyası too35 günlerini hello geçmiş edilene hello veritabanı durumuyla olacaktır.</span><span class="sxs-lookup"><span data-stu-id="0955f-172">If your database was created in Premium Service tier, you would be able toocreate database copy with hello database state up too35 days back in hello past.</span></span> <span data-ttu-id="0955f-173">Etkili bir şekilde, too65 günden eski hello geçmiş tablosu doğrudan sorgulayarak tooanalyze geçmiş satır olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="0955f-173">That effectively would allow you tooanalyze historical rows that are up too65 days old by querying hello history table directly.</span></span>

<span data-ttu-id="0955f-174">Tooactivate zamana bağlı bekletme temizleme istiyorsanız, bir noktaya geri yükleme sonrasında Transact-SQL deyimi aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="0955f-174">If you want tooactivate temporal retention cleanup, run hello following Transact-SQL statement after point in time restore:</span></span>

````
ALTER DATABASE <myDB>
SET TEMPORAL_HISTORY_RETENTION  ON
````

## <a name="next-steps"></a><span data-ttu-id="0955f-175">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="0955f-175">Next steps</span></span>
<span data-ttu-id="0955f-176">uygulamalarınızı, zamana bağlı tablolarda toouse nasıl kullanıma toolearn [zamana bağlı tablolarda Azure SQL veritabanı ile çalışmaya başlama](sql-database-temporal-tables.md).</span><span class="sxs-lookup"><span data-stu-id="0955f-176">toolearn how toouse Temporal Tables in your applications, check out [Getting Started with Temporal Tables in Azure SQL Database](sql-database-temporal-tables.md).</span></span>

<span data-ttu-id="0955f-177">Ziyaret kanal 9 toohear bir [gerçek müşteri zamana bağlı uygulama başarı Öykü](https://channel9.msdn.com/Blogs/jsturtevant/Azure-SQL-Temporal-Tables-with-RockStep-Solutions) ve izleme bir [zamana bağlı tanıtım canlı](https://channel9.msdn.com/Shows/Data-Exposed/Temporal-in-SQL-Server-2016).</span><span class="sxs-lookup"><span data-stu-id="0955f-177">Visit Channel 9 toohear a [real customer temporal implementation success story](https://channel9.msdn.com/Blogs/jsturtevant/Azure-SQL-Temporal-Tables-with-RockStep-Solutions) and watch a [live temporal demonstration](https://channel9.msdn.com/Shows/Data-Exposed/Temporal-in-SQL-Server-2016).</span></span>

<span data-ttu-id="0955f-178">Zamana bağlı tablolarda hakkında ayrıntılı bilgi için gözden [MSDN belgelerine](https://msdn.microsoft.com/library/dn935015.aspx).</span><span class="sxs-lookup"><span data-stu-id="0955f-178">For detailed information about Temporal Tables, review [MSDN documentation](https://msdn.microsoft.com/library/dn935015.aspx).</span></span>

