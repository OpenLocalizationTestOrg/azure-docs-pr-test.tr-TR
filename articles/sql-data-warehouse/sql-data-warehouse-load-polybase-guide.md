---
title: "SQL Data Warehouse'da PolyBase kullanarak Kılavuzu | Microsoft Docs"
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
ms.openlocfilehash: 6938b92d8e5b46d908dc5b2155bdfdc89bb1dc8c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="guide-for-using-polybase-in-sql-data-warehouse"></a><span data-ttu-id="95350-103">SQL Data Warehouse'da PolyBase kullanarak Kılavuzu</span><span class="sxs-lookup"><span data-stu-id="95350-103">Guide for using PolyBase in SQL Data Warehouse</span></span>
<span data-ttu-id="95350-104">Bu kılavuz, SQL Data Warehouse'da PolyBase kullanmaya yönelik pratik bilgileri verir.</span><span class="sxs-lookup"><span data-stu-id="95350-104">This guide gives practical information for using PolyBase in SQL Data Warehouse.</span></span>

<span data-ttu-id="95350-105">Başlamak için bkz: [PolyBase ile veri yükleme] [ Load data with PolyBase] Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="95350-105">To get started, see the [Load data with PolyBase][Load data with PolyBase] tutorial.</span></span>

## <a name="rotating-storage-keys"></a><span data-ttu-id="95350-106">Depolama anahtarları döndürme</span><span class="sxs-lookup"><span data-stu-id="95350-106">Rotating storage keys</span></span>
<span data-ttu-id="95350-107">Zaman zaman güvenlik nedenleriyle blob depolama alanınızın erişim anahtarı değiştirmek isteyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="95350-107">From time to time you will want to change the access key to your blob storage for security reasons.</span></span>

<span data-ttu-id="95350-108">Bu görevi gerçekleştirmek için en Zarif yolu "anahtarları döndürme" olarak bilinen bir işlem izlemektir.</span><span class="sxs-lookup"><span data-stu-id="95350-108">The most elegant way to perform this task is to follow a process known as "rotating the keys".</span></span> <span data-ttu-id="95350-109">Blob depolama hesabınız için iki depolama anahtarınız olduğunu fark etmiş olabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="95350-109">You may have noticed that you have two storage keys for your blob storage account.</span></span> <span data-ttu-id="95350-110">Böylece geçiş yapabileceğini budur</span><span class="sxs-lookup"><span data-stu-id="95350-110">This is so that you can transition</span></span>

<span data-ttu-id="95350-111">Azure depolama hesabı anahtarları döndürme basit üç adımı bir işlemdir</span><span class="sxs-lookup"><span data-stu-id="95350-111">Rotating your Azure storage account keys is a simple three step process</span></span>

1. <span data-ttu-id="95350-112">İkincil depolama erişim anahtarı temel ikinci veritabanı kapsamlı kimlik bilgileri oluşturun</span><span class="sxs-lookup"><span data-stu-id="95350-112">Create second database scoped credential based on the secondary storage access key</span></span>
2. <span data-ttu-id="95350-113">Bu yeni bir kimlik bilgisi dayalı ikinci dış veri kaynağı oluşturma</span><span class="sxs-lookup"><span data-stu-id="95350-113">Create second external data source based off this new credential</span></span>
3. <span data-ttu-id="95350-114">Bırakın ve yeni dış veri kaynağına işaret eden dış tabloları oluşturma</span><span class="sxs-lookup"><span data-stu-id="95350-114">Drop and create the external table(s) pointing to the new external data source</span></span>

<span data-ttu-id="95350-115">Geçirdikten sonra yeni dış veri kaynağına tüm dış tablolar sonra temizleme görevleri gerçekleştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="95350-115">When you have migrated all your external tables to the new external data source then you can perform the clean up tasks:</span></span>

1. <span data-ttu-id="95350-116">Bırakma ilk dış veri kaynağı</span><span class="sxs-lookup"><span data-stu-id="95350-116">Drop first external data source</span></span>
2. <span data-ttu-id="95350-117">Birincil depolama erişim anahtarı temel kimlik bilgisi açılan ilk veritabanı kapsamlı</span><span class="sxs-lookup"><span data-stu-id="95350-117">Drop first database scoped credential based on the primary storage access key</span></span>
3. <span data-ttu-id="95350-118">Azure'da oturum ve bir sonraki seferde hazır birincil erişim anahtarını yeniden oluşturma</span><span class="sxs-lookup"><span data-stu-id="95350-118">Log into Azure and regenerate the primary access key ready for the next time</span></span>

## <a name="query-azure-blob-storage-data"></a><span data-ttu-id="95350-119">Azure blob depolama veri sorgulama</span><span class="sxs-lookup"><span data-stu-id="95350-119">Query Azure blob storage data</span></span>
<span data-ttu-id="95350-120">İlişkisel bir tablo olduğu gibi sorgulamanıza sorguları dış tablolara yönelik yalnızca tablo adı kullanın.</span><span class="sxs-lookup"><span data-stu-id="95350-120">Queries against external tables simply use the table name as though it was a relational table.</span></span>

```sql
-- Query Azure storage resident data via external table.
SELECT * FROM [ext].[CarSensor_Data]
;
```

> [!NOTE]
> <span data-ttu-id="95350-121">Bir dış tablo üzerinde bir sorgu hatası ile başarısız olabilir *"Sorgu iptal edildi--bir dış kaynaktan okurken maksimum Reddet Eşiğe ulaşıldığında"*.</span><span class="sxs-lookup"><span data-stu-id="95350-121">A query on an external table can fail with the error *"Query aborted-- the maximum reject threshold was reached while reading from an external source"*.</span></span> <span data-ttu-id="95350-122">Bu, dış veri içerip içermediğini gösterir *kirli* kaydeder.</span><span class="sxs-lookup"><span data-stu-id="95350-122">This indicates that your external data contains *dirty* records.</span></span> <span data-ttu-id="95350-123">Bir veri kaydı gerçek veri türleri/sütun sayısı dış tablosunun sütun tanımları eşleşmiyorsa veya verileri belirtilen dış dosya biçimine uygun değil 'kirli' olarak kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="95350-123">A data record is considered 'dirty' if the actual data types/number of columns do not match the column definitions of the external table or if the data doesn't conform to the specified external file format.</span></span> <span data-ttu-id="95350-124">Bu sorunu gidermek için dış tablo ve dış dosya biçimini tanımları doğru olduğundan ve bu tanımları, dış veri uyan emin olun.</span><span class="sxs-lookup"><span data-stu-id="95350-124">To fix this, ensure that your external table and external file format definitions are correct and your external data conforms to these definitions.</span></span> <span data-ttu-id="95350-125">Dış veri kayıtların bir alt kümesini durumunda kirli, sorgularınızı bu kayıtları oluşturma dış tablo DDL Reddet seçeneklerini kullanarak reddetmek seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="95350-125">In case a subset of external data records are dirty, you can choose to reject these records for your queries by using the reject options in CREATE EXTERNAL TABLE DDL.</span></span>
> 
> 

## <a name="load-data-from-azure-blob-storage"></a><span data-ttu-id="95350-126">Azure blob depolamadan veri yükleme</span><span class="sxs-lookup"><span data-stu-id="95350-126">Load data from Azure blob storage</span></span>
<span data-ttu-id="95350-127">Bu örnek verileri Azure blob depolama alanından SQL Data Warehouse veritabanına yükler.</span><span class="sxs-lookup"><span data-stu-id="95350-127">This example loads data from Azure blob storage to SQL Data Warehouse database.</span></span>

<span data-ttu-id="95350-128">Verileri doğrudan depolama sorguları için veri aktarım süresini kaldırır.</span><span class="sxs-lookup"><span data-stu-id="95350-128">Storing data directly removes the data transfer time for queries.</span></span> <span data-ttu-id="95350-129">Bir columnstore dizini olan verileri depolamak için 10 kat analiz sorgular tarafından sorgu performansı geliştirir.</span><span class="sxs-lookup"><span data-stu-id="95350-129">Storing data with a columnstore index improves query performance for analysis queries by up to 10x.</span></span>

<span data-ttu-id="95350-130">Bu örnek CREATE TABLE AS SELECT deyimi veri yüklemek için kullanır.</span><span class="sxs-lookup"><span data-stu-id="95350-130">This example uses the CREATE TABLE AS SELECT statement to load data.</span></span> <span data-ttu-id="95350-131">Yeni bir tablo sorguda adlandırılan sütunları devralır.</span><span class="sxs-lookup"><span data-stu-id="95350-131">The new table inherits the columns named in the query.</span></span> <span data-ttu-id="95350-132">Dış tablo tanımı bu sütunların veri türlerini devralır.</span><span class="sxs-lookup"><span data-stu-id="95350-132">It inherits the data types of those columns from the external table definition.</span></span>

<span data-ttu-id="95350-133">CREATE TABLE AS SELECT bir yüksek oranda kullanıcı verileri SQL veri ambarı tüm işlem düğümlerini paralel yükler Transact-SQL deyimini olur.</span><span class="sxs-lookup"><span data-stu-id="95350-133">CREATE TABLE AS SELECT is a highly performant Transact-SQL statement that loads the data in parallel to all the compute nodes of your SQL Data Warehouse.</span></span>  <span data-ttu-id="95350-134">Analiz platformu sistemi yüksek düzeyde paralel işleme (MPP) altyapısında için geliştirilmiştir ve SQL veri ambarı'nda sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="95350-134">It was originally developed for  the massively parallel processing (MPP) engine in Analytics Platform System and is now in SQL Data Warehouse.</span></span>

```sql
-- Load data from Azure blob storage to SQL Data Warehouse

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

<span data-ttu-id="95350-135">Bkz: [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)].</span><span class="sxs-lookup"><span data-stu-id="95350-135">See [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)].</span></span>

## <a name="create-statistics-on-newly-loaded-data"></a><span data-ttu-id="95350-136">Yeni yüklenen verilere ilişkin istatistikler oluşturma</span><span class="sxs-lookup"><span data-stu-id="95350-136">Create Statistics on newly loaded data</span></span>
<span data-ttu-id="95350-137">Azure SQL Data Warehouse henüz istatistiklerin otomatik olarak oluşturulup güncelleştirilmesini desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="95350-137">Azure SQL Data Warehouse does not yet support auto create or auto update statistics.</span></span>  <span data-ttu-id="95350-138">Sorgularınızdan en iyi performansı elde edebilmeniz için ilk yüklemeden veya verilerdeki önemli değişikliklerden sonra her tablonun her sütununa ilişkin istatistiklerin oluşturulması önemlidir.</span><span class="sxs-lookup"><span data-stu-id="95350-138">In order to get the best performance from your queries, it's important that statistics be created on all columns of all tables after the first load or any substantial changes occur in the data.</span></span>  <span data-ttu-id="95350-139">İstatistikler hakkında ayrıntılı bir açıklama için Geliştirme ile ilgili konu başlığı grubunda yer alan [İstatistikler][Statistics] bölümüne göz atın.</span><span class="sxs-lookup"><span data-stu-id="95350-139">For a detailed explanation of statistics, see the [Statistics][Statistics] topic in the Develop group of topics.</span></span>  <span data-ttu-id="95350-140">İstatistik oluşturacağınıza yönelik bu örnekte yüklenen oluşturmak nasıl hızlı bir örneği aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="95350-140">Below is a quick example of how to create statistics on the tabled loaded in this example.</span></span>

```sql
create statistics [SensorKey] on [Customer_Speed] ([SensorKey]);
create statistics [CustomerKey] on [Customer_Speed] ([CustomerKey]);
create statistics [GeographyKey] on [Customer_Speed] ([GeographyKey]);
create statistics [Speed] on [Customer_Speed] ([Speed]);
create statistics [YearMeasured] on [Customer_Speed] ([YearMeasured]);
```

## <a name="export-data-to-azure-blob-storage"></a><span data-ttu-id="95350-141">Azure blob depolama alanına veri dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="95350-141">Export data to Azure blob storage</span></span>
<span data-ttu-id="95350-142">Bu bölümde Azure blob depolama alanına SQL veri ambarından verilerin dışarı aktarma gösterir.</span><span class="sxs-lookup"><span data-stu-id="95350-142">This section shows how to export data from SQL Data Warehouse to Azure blob storage.</span></span> <span data-ttu-id="95350-143">Bu örnek, dış tablo AS bir yüksek oranda kullanıcı paralel veri tüm işlem düğümlerinden dışarı aktarmak için Transact-SQL deyimini olan Oluştur kullanır.</span><span class="sxs-lookup"><span data-stu-id="95350-143">This example uses CREATE EXTERNAL TABLE AS SELECT which is a highly performant Transact-SQL statement to export the data in parallel from all the compute nodes.</span></span>

<span data-ttu-id="95350-144">Aşağıdaki örnek, sütun tanımları ve dbo verileri kullanarak bir dış tablo Weblogs2014 oluşturur. Web günlüklerini tablo.</span><span class="sxs-lookup"><span data-stu-id="95350-144">The following example creates an external table Weblogs2014 using column definitions and data from dbo.Weblogs table.</span></span> <span data-ttu-id="95350-145">Dış tablo tanımındaki SQL veri ambarı'nda depolanır ve veri kaynağı tarafından belirtilen blob kapsayıcısı altında "/ / log2014/Arşiv" dizinine SELECT deyiminin sonuçlarını dışarı aktarılır.</span><span class="sxs-lookup"><span data-stu-id="95350-145">The external table definition is stored in SQL Data Warehouse and the results of the SELECT statement are exported to the "/archive/log2014/" directory under the blob container specified by the data source.</span></span> <span data-ttu-id="95350-146">Verileri belirtilen metin dosyası biçiminde dışarı aktarılır.</span><span class="sxs-lookup"><span data-stu-id="95350-146">The data is exported in the specified text file format.</span></span>

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
## <a name="isolate-loading-users"></a><span data-ttu-id="95350-147">Kullanıcıları yüklenirken yalıtma</span><span class="sxs-lookup"><span data-stu-id="95350-147">Isolate Loading Users</span></span>
<span data-ttu-id="95350-148">Genellikle verileri SQL DW yükleyebilirsiniz birden fazla kullanıcınız gerek yoktur.</span><span class="sxs-lookup"><span data-stu-id="95350-148">There is often a need to have multiple users that can load data into a SQL DW.</span></span> <span data-ttu-id="95350-149">Çünkü [CREATE TABLE AS SELECT (Transact-SQL)] [ CREATE TABLE AS SELECT (Transact-SQL)] denetim izinleri gerektirir, veritabanını, Denetim erişimi olan birden çok kullanıcıya sahip tüm şemaları son bulur.</span><span class="sxs-lookup"><span data-stu-id="95350-149">Because the [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)] requires CONTROL permissions of the database, you will end up with multiple users with control access over all schemas.</span></span> <span data-ttu-id="95350-150">Bu sınırlamak için REDDETME denetim deyimi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="95350-150">To limit this, you can use the DENY CONTROL statement.</span></span>

<span data-ttu-id="95350-151">Örnek: bir bölüm için veritabanı şemalarını schema_A ve Bölüm B izin veritabanı kullanıcıları user_A schema_B göz önünde bulundurun ve kullanıcılar için Bölüm A ve B, sırasıyla Polybase'in user_B olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="95350-151">Example: Consider database schemas schema_A for dept A, and schema_B for dept B Let database users user_A and user_B be users for PolyBase loading in dept A and B, respectively.</span></span> <span data-ttu-id="95350-152">Her ikisi de denetim veritabanı izinleri verildi.</span><span class="sxs-lookup"><span data-stu-id="95350-152">They both have been granted CONTROL database permissions.</span></span>
<span data-ttu-id="95350-153">Şema A ve B şimdi kilidi oluşturucuları REDDETME kullanılarak kendi şemaları aşağı:</span><span class="sxs-lookup"><span data-stu-id="95350-153">The creators of schema A and B now lock down their schemas using DENY:</span></span>

```sql
   DENY CONTROL ON SCHEMA :: schema_A TO user_B;
   DENY CONTROL ON SCHEMA :: schema_B TO user_A;
```   
 <span data-ttu-id="95350-154">Bu, user_A ve user_B şimdi diğer bölüm 's şemadan kilitlenmesi.</span><span class="sxs-lookup"><span data-stu-id="95350-154">With this, user_A and user_B should now be locked out from the other dept’s schema.</span></span>
 


## <a name="next-steps"></a><span data-ttu-id="95350-155">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="95350-155">Next steps</span></span>
<span data-ttu-id="95350-156">SQL Data Warehouse'a veri taşıma hakkında daha fazla bilgi için bkz: [veri geçişine genel bakış][data migration overview].</span><span class="sxs-lookup"><span data-stu-id="95350-156">To learn more about moving data to SQL Data Warehouse, see the [data migration overview][data migration overview].</span></span>

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
