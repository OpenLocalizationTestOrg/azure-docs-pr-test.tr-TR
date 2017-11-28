---
title: SQL Data Warehouse'da PolyBase kullanarak aaaGuide | Microsoft Docs
description: "Kılavuzları ve PolyBase kullanarak SQL Data Warehouse senaryolarda ilgili öneriler."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: barbkess
editor: 
ms.assetid: 4757fce1-96b3-48ea-8a51-be1385705f9f
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 6/5/2016
ms.custom: loading
ms.author: cakarst;barbkess
ms.openlocfilehash: b05e4c5d528f2fe1c60d6855b5333065f0c908ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="guide-for-using-polybase-in-sql-data-warehouse"></a><span data-ttu-id="dca7d-103">SQL Data Warehouse'da PolyBase kullanarak Kılavuzu</span><span class="sxs-lookup"><span data-stu-id="dca7d-103">Guide for using PolyBase in SQL Data Warehouse</span></span>
<span data-ttu-id="dca7d-104">Bu kılavuz, SQL Data Warehouse'da PolyBase kullanmaya yönelik pratik bilgileri verir.</span><span class="sxs-lookup"><span data-stu-id="dca7d-104">This guide gives practical information for using PolyBase in SQL Data Warehouse.</span></span>

<span data-ttu-id="dca7d-105">başlatıldı, tooget bkz hello [PolyBase ile veri yükleme] [ Load data with PolyBase] Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="dca7d-105">tooget started, see hello [Load data with PolyBase][Load data with PolyBase] tutorial.</span></span>

## <a name="rotating-storage-keys"></a><span data-ttu-id="dca7d-106">Depolama anahtarları döndürme</span><span class="sxs-lookup"><span data-stu-id="dca7d-106">Rotating storage keys</span></span>
<span data-ttu-id="dca7d-107">Saat tootime güvenlik nedenleriyle toochange hello erişim anahtar tooyour blob depolama isteyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="dca7d-107">From time tootime you will want toochange hello access key tooyour blob storage for security reasons.</span></span>

<span data-ttu-id="dca7d-108">Bu görev toofollow "Merhaba anahtarları döndürme" olarak bilinen bir işlem olduğundan en Zarif yolu tooperform hello.</span><span class="sxs-lookup"><span data-stu-id="dca7d-108">hello most elegant way tooperform this task is toofollow a process known as "rotating hello keys".</span></span> <span data-ttu-id="dca7d-109">Blob depolama hesabınız için iki depolama anahtarınız olduğunu fark etmiş olabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dca7d-109">You may have noticed that you have two storage keys for your blob storage account.</span></span> <span data-ttu-id="dca7d-110">Böylece geçiş yapabileceğini budur</span><span class="sxs-lookup"><span data-stu-id="dca7d-110">This is so that you can transition</span></span>

<span data-ttu-id="dca7d-111">Azure depolama hesabı anahtarları döndürme basit üç adımı bir işlemdir</span><span class="sxs-lookup"><span data-stu-id="dca7d-111">Rotating your Azure storage account keys is a simple three step process</span></span>

1. <span data-ttu-id="dca7d-112">Merhaba ikincil depolama erişim anahtarı temel ikinci veritabanı kapsamlı kimlik bilgileri oluşturun</span><span class="sxs-lookup"><span data-stu-id="dca7d-112">Create second database scoped credential based on hello secondary storage access key</span></span>
2. <span data-ttu-id="dca7d-113">Bu yeni bir kimlik bilgisi dayalı ikinci dış veri kaynağı oluşturma</span><span class="sxs-lookup"><span data-stu-id="dca7d-113">Create second external data source based off this new credential</span></span>
3. <span data-ttu-id="dca7d-114">Bırakma ve toohello yeni dış veri kaynağına işaret eden hello dış tabloları oluşturma</span><span class="sxs-lookup"><span data-stu-id="dca7d-114">Drop and create hello external table(s) pointing toohello new external data source</span></span>

<span data-ttu-id="dca7d-115">Gerçekleştirebileceğiniz sonra tüm dış tablolara toohello yeni dış veri kaynağınızda geçirdikten sonra hello görevleri temizleyin:</span><span class="sxs-lookup"><span data-stu-id="dca7d-115">When you have migrated all your external tables toohello new external data source then you can perform hello clean up tasks:</span></span>

1. <span data-ttu-id="dca7d-116">Bırakma ilk dış veri kaynağı</span><span class="sxs-lookup"><span data-stu-id="dca7d-116">Drop first external data source</span></span>
2. <span data-ttu-id="dca7d-117">Kimlik bilgisi hello birincil depolama erişim anahtarı temel açılan ilk veritabanı kapsamlı</span><span class="sxs-lookup"><span data-stu-id="dca7d-117">Drop first database scoped credential based on hello primary storage access key</span></span>
3. <span data-ttu-id="dca7d-118">Azure'da oturum açın ve hello birincil erişim anahtarı Merhaba hazır sonraki sefer yeniden</span><span class="sxs-lookup"><span data-stu-id="dca7d-118">Log into Azure and regenerate hello primary access key ready for hello next time</span></span>

## <a name="query-azure-blob-storage-data"></a><span data-ttu-id="dca7d-119">Azure blob depolama veri sorgulama</span><span class="sxs-lookup"><span data-stu-id="dca7d-119">Query Azure blob storage data</span></span>
<span data-ttu-id="dca7d-120">İlişkisel bir tablo olduğu gibi sorgulamanıza sorguları dış tablolara yönelik yalnızca hello tablo adı kullanın.</span><span class="sxs-lookup"><span data-stu-id="dca7d-120">Queries against external tables simply use hello table name as though it was a relational table.</span></span>

```sql
-- Query Azure storage resident data via external table.
SELECT * FROM [ext].[CarSensor_Data]
;
```

> [!NOTE]
> <span data-ttu-id="dca7d-121">Bir dış tablo sorgu hello hata ile başarısız olabilir *"Sorgu iptal edildi--hello maksimum Reddet eşik bir dış kaynaktan okurken ulaşıldı"*.</span><span class="sxs-lookup"><span data-stu-id="dca7d-121">A query on an external table can fail with hello error *"Query aborted-- hello maximum reject threshold was reached while reading from an external source"*.</span></span> <span data-ttu-id="dca7d-122">Bu, dış veri içerip içermediğini gösterir *kirli* kaydeder.</span><span class="sxs-lookup"><span data-stu-id="dca7d-122">This indicates that your external data contains *dirty* records.</span></span> <span data-ttu-id="dca7d-123">Bir veri kaydı hello gerçek veri türleri/sütun sayısı hello hello dış tablosunun sütun tanımları eşleşmiyorsa veya hello verileri toohello belirtilen dış dosya biçimi uygun değil 'kirli' olarak kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="dca7d-123">A data record is considered 'dirty' if hello actual data types/number of columns do not match hello column definitions of hello external table or if hello data doesn't conform toohello specified external file format.</span></span> <span data-ttu-id="dca7d-124">toofix Bu, dış tablo ve dış dosya biçimini tanımları doğru ve dış verilerinizi toothese tanımları uyumlu olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="dca7d-124">toofix this, ensure that your external table and external file format definitions are correct and your external data conforms toothese definitions.</span></span> <span data-ttu-id="dca7d-125">Dış veri kayıtların bir alt kümesini durumunda kirli, tooreject bu kayıtları sorgularınızı oluşturmak dış tablo DDL hello reddetme seçenekleri kullanılarak seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dca7d-125">In case a subset of external data records are dirty, you can choose tooreject these records for your queries by using hello reject options in CREATE EXTERNAL TABLE DDL.</span></span>
> 
> 

## <a name="load-data-from-azure-blob-storage"></a><span data-ttu-id="dca7d-126">Azure blob depolamadan veri yükleme</span><span class="sxs-lookup"><span data-stu-id="dca7d-126">Load data from Azure blob storage</span></span>
<span data-ttu-id="dca7d-127">Bu örnek verileri Azure blob depolama tooSQL veri ambarı veritabanından yükler.</span><span class="sxs-lookup"><span data-stu-id="dca7d-127">This example loads data from Azure blob storage tooSQL Data Warehouse database.</span></span>

<span data-ttu-id="dca7d-128">Verileri doğrudan depolamak hello veri aktarım süresini sorgular için kaldırır.</span><span class="sxs-lookup"><span data-stu-id="dca7d-128">Storing data directly removes hello data transfer time for queries.</span></span> <span data-ttu-id="dca7d-129">Bir columnstore dizini olan veri depolama too10x tarafından analiz sorguları için sorgu performansı geliştirir.</span><span class="sxs-lookup"><span data-stu-id="dca7d-129">Storing data with a columnstore index improves query performance for analysis queries by up too10x.</span></span>

<span data-ttu-id="dca7d-130">Bu örnek hello CREATE TABLE AS SELECT deyimi tooload verileri kullanır.</span><span class="sxs-lookup"><span data-stu-id="dca7d-130">This example uses hello CREATE TABLE AS SELECT statement tooload data.</span></span> <span data-ttu-id="dca7d-131">Merhaba yeni tablo hello sorguda adlandırılan hello sütunları devralır.</span><span class="sxs-lookup"><span data-stu-id="dca7d-131">hello new table inherits hello columns named in hello query.</span></span> <span data-ttu-id="dca7d-132">Bu sütunların veri türlerini hello hello dış tablo tanımından devralır.</span><span class="sxs-lookup"><span data-stu-id="dca7d-132">It inherits hello data types of those columns from hello external table definition.</span></span>

<span data-ttu-id="dca7d-133">CREATE TABLE AS SELECT bir yüksek oranda kullanıcı paralel tooall hello hello verileri yükler Transact-SQL deyimini işlem düğümleri, SQL Data warehouse'un olur.</span><span class="sxs-lookup"><span data-stu-id="dca7d-133">CREATE TABLE AS SELECT is a highly performant Transact-SQL statement that loads hello data in parallel tooall hello compute nodes of your SQL Data Warehouse.</span></span>  <span data-ttu-id="dca7d-134">Analiz platformu sistemi hello yüksek düzeyde paralel işleme (MPP) altyapısı için geliştirilmiştir ve SQL veri ambarı'nda sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="dca7d-134">It was originally developed for  hello massively parallel processing (MPP) engine in Analytics Platform System and is now in SQL Data Warehouse.</span></span>

```sql
-- Load data from Azure blob storage tooSQL Data Warehouse

CREATE TABLE [dbo].[Customer_Speed]
WITH
(   
    CLUSTERED COLUMNSTORE INDEX
,    DISTRIBUTION = HASH([CarSensor_Data].[CustomerKey])
)
AS
SELECT *
FROM   [ext].[CarSensor_Data]
;
```

<span data-ttu-id="dca7d-135">Bkz: [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)].</span><span class="sxs-lookup"><span data-stu-id="dca7d-135">See [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)].</span></span>

## <a name="create-statistics-on-newly-loaded-data"></a><span data-ttu-id="dca7d-136">Yeni yüklenen verilere ilişkin istatistikler oluşturma</span><span class="sxs-lookup"><span data-stu-id="dca7d-136">Create Statistics on newly loaded data</span></span>
<span data-ttu-id="dca7d-137">Azure SQL Data Warehouse henüz istatistiklerin otomatik olarak oluşturulup güncelleştirilmesini desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="dca7d-137">Azure SQL Data Warehouse does not yet support auto create or auto update statistics.</span></span>  <span data-ttu-id="dca7d-138">Sipariş tooget hello en iyi performansı sorgularınızı, istatistikleri hello ilk yükleme işleminden sonra tüm tabloların tüm sütunlarda oluşturulması önemlidir veya hello verilerde önemli değişikliklerden.</span><span class="sxs-lookup"><span data-stu-id="dca7d-138">In order tooget hello best performance from your queries, it's important that statistics be created on all columns of all tables after hello first load or any substantial changes occur in hello data.</span></span>  <span data-ttu-id="dca7d-139">Merhaba istatistikleri ayrıntılı bir açıklaması için bkz [istatistikleri] [ Statistics] konu hello geliştirme grubunu konuda.</span><span class="sxs-lookup"><span data-stu-id="dca7d-139">For a detailed explanation of statistics, see hello [Statistics][Statistics] topic in hello Develop group of topics.</span></span>  <span data-ttu-id="dca7d-140">Aşağıda bu örnekte toocreate istatistik oluşturacağınıza yönelik hello nasıl yüklenir, hızlı bir örnek verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="dca7d-140">Below is a quick example of how toocreate statistics on hello tabled loaded in this example.</span></span>

```sql
create statistics [SensorKey] on [Customer_Speed] ([SensorKey]);
create statistics [CustomerKey] on [Customer_Speed] ([CustomerKey]);
create statistics [GeographyKey] on [Customer_Speed] ([GeographyKey]);
create statistics [Speed] on [Customer_Speed] ([Speed]);
create statistics [YearMeasured] on [Customer_Speed] ([YearMeasured]);
```

## <a name="export-data-tooazure-blob-storage"></a><span data-ttu-id="dca7d-141">Veri tooAzure blob depolama dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="dca7d-141">Export data tooAzure blob storage</span></span>
<span data-ttu-id="dca7d-142">Bu bölümde, nasıl SQL Data Warehouse tooAzure tooexport verileri blob depolama gösterir.</span><span class="sxs-lookup"><span data-stu-id="dca7d-142">This section shows how tooexport data from SQL Data Warehouse tooAzure blob storage.</span></span> <span data-ttu-id="dca7d-143">Bu örnek, dış tablo AS yüksek oranda kullanıcı Transact-SQL deyimi tooexport hello veri paralel tüm hello işlem düğümlerinden olan Oluştur kullanır.</span><span class="sxs-lookup"><span data-stu-id="dca7d-143">This example uses CREATE EXTERNAL TABLE AS SELECT which is a highly performant Transact-SQL statement tooexport hello data in parallel from all hello compute nodes.</span></span>

<span data-ttu-id="dca7d-144">Merhaba aşağıdaki örnek sütun tanımları ve dbo verileri kullanarak bir dış tablo Weblogs2014 oluşturur. Web günlüklerini tablo.</span><span class="sxs-lookup"><span data-stu-id="dca7d-144">hello following example creates an external table Weblogs2014 using column definitions and data from dbo.Weblogs table.</span></span> <span data-ttu-id="dca7d-145">Merhaba dış tablo tanımındaki SQL veri ambarında depolanır ve hello SELECT deyimi hello sonuçlarını dışarı aktarılan toohello olan "/ / log2014/Arşiv" dizini hello veri kaynağı tarafından belirtilen hello blob kapsayıcısı altında.</span><span class="sxs-lookup"><span data-stu-id="dca7d-145">hello external table definition is stored in SQL Data Warehouse and hello results of hello SELECT statement are exported toohello "/archive/log2014/" directory under hello blob container specified by hello data source.</span></span> <span data-ttu-id="dca7d-146">Merhaba veri hello belirtilen metin dosyası biçiminde dışarı aktarılır.</span><span class="sxs-lookup"><span data-stu-id="dca7d-146">hello data is exported in hello specified text file format.</span></span>

```sql
CREATE EXTERNAL TABLE Weblogs2014 WITH
(
    LOCATION='/archive/log2014/',
    DATA_SOURCE=azure_storage,
    FILE_FORMAT=text_file_format
)
AS
SELECT
    Uri,
    DateRequested
FROM
    dbo.Weblogs
WHERE
    1=1
    AND DateRequested > '12/31/2013'
    AND DateRequested < '01/01/2015';
```
## <a name="isolate-loading-users"></a><span data-ttu-id="dca7d-147">Kullanıcıları yüklenirken yalıtma</span><span class="sxs-lookup"><span data-stu-id="dca7d-147">Isolate Loading Users</span></span>
<span data-ttu-id="dca7d-148">Verileri bir SQL DW yükleyebilirsiniz birden çok kullanıcı genellikle gerek toohave var.</span><span class="sxs-lookup"><span data-stu-id="dca7d-148">There is often a need toohave multiple users that can load data into a SQL DW.</span></span> <span data-ttu-id="dca7d-149">Çünkü hello [CREATE TABLE AS SELECT (Transact-SQL)] [ CREATE TABLE AS SELECT (Transact-SQL)] denetim izinleri gerektirir hello veritabanının, Denetim erişimi olan birden çok kullanıcıya sahip tüm şemaları son bulur.</span><span class="sxs-lookup"><span data-stu-id="dca7d-149">Because hello [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)] requires CONTROL permissions of hello database, you will end up with multiple users with control access over all schemas.</span></span> <span data-ttu-id="dca7d-150">toolimit bunu hello REDDET denetim deyimi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dca7d-150">toolimit this, you can use hello DENY CONTROL statement.</span></span>

<span data-ttu-id="dca7d-151">Örnek: bir bölüm için veritabanı şemalarını schema_A ve Bölüm B izin veritabanı kullanıcıları user_A schema_B göz önünde bulundurun ve kullanıcılar için Bölüm A ve B, sırasıyla Polybase'in user_B olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="dca7d-151">Example: Consider database schemas schema_A for dept A, and schema_B for dept B Let database users user_A and user_B be users for PolyBase loading in dept A and B, respectively.</span></span> <span data-ttu-id="dca7d-152">Her ikisi de denetim veritabanı izinleri verildi.</span><span class="sxs-lookup"><span data-stu-id="dca7d-152">They both have been granted CONTROL database permissions.</span></span>
<span data-ttu-id="dca7d-153">Merhaba oluşturucuları şemasının A ve B şimdi REDDETME kullanılarak kendi şemaları kilitle:</span><span class="sxs-lookup"><span data-stu-id="dca7d-153">hello creators of schema A and B now lock down their schemas using DENY:</span></span>

```sql
   DENY CONTROL ON SCHEMA :: schema_A toouser_B;
   DENY CONTROL ON SCHEMA :: schema_B toouser_A;
```   
 <span data-ttu-id="dca7d-154">Bu, user_A ve user_B şimdi hello kilitlenmesi diğer bölüm 's şema.</span><span class="sxs-lookup"><span data-stu-id="dca7d-154">With this, user_A and user_B should now be locked out from hello other dept’s schema.</span></span>
 


## <a name="next-steps"></a><span data-ttu-id="dca7d-155">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="dca7d-155">Next steps</span></span>
<span data-ttu-id="dca7d-156">toolearn taşıma veri tooSQL veri ambarı hakkında daha fazla bilgi görmek hello [veri geçişine genel bakış][data migration overview].</span><span class="sxs-lookup"><span data-stu-id="dca7d-156">toolearn more about moving data tooSQL Data Warehouse, see hello [data migration overview][data migration overview].</span></span>

<!--Image references-->

<!--Article references-->
[Load data with bcp]: ./sql-data-warehouse-load-with-bcp.md
[Load data with PolyBase]: ./sql-data-warehouse-get-started-load-with-polybase.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[data migration overview]: ./sql-data-warehouse-overview-migrate.md

<!--MSDN references-->
[supported source/sink]: https://msdn.microsoft.com/library/dn894007.aspx
[copy activity]: https://msdn.microsoft.com/library/dn835035.aspx
[SQL Server destination adapter]: https://msdn.microsoft.com/library/ms141095.aspx
[SSIS]: https://msdn.microsoft.com/library/ms141026.aspx

[CREATE EXTERNAL DATA SOURCE (Transact-SQL)]: https://msdn.microsoft.com/library/dn935022.aspx
[CREATE EXTERNAL FILE FORMAT (Transact-SQL)]: https://msdn.microsoft.com/library/dn935026.aspx
[CREATE EXTERNAL TABLE (Transact-SQL)]: https://msdn.microsoft.com/library/dn935021.aspx

[DROP EXTERNAL DATA SOURCE (Transact-SQL)]: https://msdn.microsoft.com/library/mt146367.aspx
[DROP EXTERNAL FILE FORMAT (Transact-SQL)]: https://msdn.microsoft.com/library/mt146379.aspx
[DROP EXTERNAL TABLE (Transact-SQL)]: https://msdn.microsoft.com/library/mt130698.aspx

[CREATE TABLE AS SELECT (Transact-SQL)]: https://msdn.microsoft.com/library/mt204041.aspx
[INSERT...SELECT (Transact-SQL)]: https://msdn.microsoft.com/library/ms174335.aspx
[CREATE MASTER KEY (Transact-SQL)]: https://msdn.microsoft.com/library/ms174382.aspx
[CREATE CREDENTIAL (Transact-SQL)]: https://msdn.microsoft.com/library/ms189522.aspx
[CREATE DATABASE SCOPED CREDENTIAL (Transact-SQL)]: https://msdn.microsoft.com/library/mt270260.aspx
[DROP CREDENTIAL (Transact-SQL)]: https://msdn.microsoft.com/library/ms189450.aspx

<!-- External Links -->
