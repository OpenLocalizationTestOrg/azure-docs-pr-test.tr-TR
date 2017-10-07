---
title: "SQL veri ambarı aaaPartitioning tablolarda | Microsoft Docs"
description: "Azure SQL Data Warehouse'da tablo bölümleme ile çalışmaya başlama."
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: jhubbard
editor: 
ms.assetid: 6cef870c-114f-470c-af10-02300c58885d
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 10/31/2016
ms.author: shigu;barbkess
ms.openlocfilehash: aa63c51562f3e6f83063320860b195e135a721e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="partitioning-tables-in-sql-data-warehouse"></a><span data-ttu-id="30868-103">SQL veri ambarı tablolarda bölümlendirme</span><span class="sxs-lookup"><span data-stu-id="30868-103">Partitioning tables in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="30868-104">[Genel bakış][Overview]</span><span class="sxs-lookup"><span data-stu-id="30868-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="30868-105">[Veri türleri][Data Types]</span><span class="sxs-lookup"><span data-stu-id="30868-105">[Data Types][Data Types]</span></span>
> * <span data-ttu-id="30868-106">[Dağıt][Distribute]</span><span class="sxs-lookup"><span data-stu-id="30868-106">[Distribute][Distribute]</span></span>
> * <span data-ttu-id="30868-107">[Dizin][Index]</span><span class="sxs-lookup"><span data-stu-id="30868-107">[Index][Index]</span></span>
> * <span data-ttu-id="30868-108">[Bölüm][Partition]</span><span class="sxs-lookup"><span data-stu-id="30868-108">[Partition][Partition]</span></span>
> * <span data-ttu-id="30868-109">[İstatistikleri][Statistics]</span><span class="sxs-lookup"><span data-stu-id="30868-109">[Statistics][Statistics]</span></span>
> * <span data-ttu-id="30868-110">[Geçici][Temporary]</span><span class="sxs-lookup"><span data-stu-id="30868-110">[Temporary][Temporary]</span></span>
> 
> 

<span data-ttu-id="30868-111">Bölümleme tüm SQL veri ambarı tablo türlerinde desteklenir; Kümelenmiş columnstore, kümelenmiş dizin ve yığın dahil.</span><span class="sxs-lookup"><span data-stu-id="30868-111">Partitioning is supported on all SQL Data Warehouse table types; including clustered columnstore, clustered index, and heap.</span></span>  <span data-ttu-id="30868-112">Bölümlendirme, karma veya dağıtılmış hepsini dahil olmak üzere tüm dağıtım türlerinde de desteklenir.</span><span class="sxs-lookup"><span data-stu-id="30868-112">Partitioning is also supported on all distribution types, including both hash or round robin distributed.</span></span>  <span data-ttu-id="30868-113">Bölümleme bölümleme daha küçük gruplar veri ve çoğu durumda, verilerinizi bir tarih sütunu yapılır toodivide sağlar.</span><span class="sxs-lookup"><span data-stu-id="30868-113">Partitioning enables you toodivide your data into smaller groups of data and in most cases, partitioning is done on a date column.</span></span>

## <a name="benefits-of-partitioning"></a><span data-ttu-id="30868-114">Bölümleme avantajları</span><span class="sxs-lookup"><span data-stu-id="30868-114">Benefits of partitioning</span></span>
<span data-ttu-id="30868-115">Bölümleme veri Bakım ve sorgu performansını yararlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="30868-115">Partitioning can benefit data maintenance and query performance.</span></span>  <span data-ttu-id="30868-116">Olup hem veya yalnızca bir avantaj verilerin nasıl yüklendiği ve bölümleme yalnızca bir sütun üzerinde yapılabilir beri hello aynı sütuna iki amaçlar için kullanılıp kullanılamayacağını bağımlıdır.</span><span class="sxs-lookup"><span data-stu-id="30868-116">Whether it benefits both or just one is dependent on how data is loaded and whether hello same column can be used for both purposes, since partitioning can only be done on one column.</span></span>

### <a name="benefits-tooloads"></a><span data-ttu-id="30868-117">Avantajları tooloads</span><span class="sxs-lookup"><span data-stu-id="30868-117">Benefits tooloads</span></span>
<span data-ttu-id="30868-118">SQL veri ambarı'nda bölümleme hello birincil yararı olduğu hello verimliliği ve bölüm silme işlemini kullanarak verileri yüklenirken, değiştirme ve birleştirme performansını artırır.</span><span class="sxs-lookup"><span data-stu-id="30868-118">hello primary benefit of partitioning in SQL Data Warehouse is improve hello efficiency and performance of loading data by use of partition deletion, switching and merging.</span></span>  <span data-ttu-id="30868-119">Çoğu durumda bir tarihte verileri bölümlenen toohello sırası hello veri yüklenen toohello veritabanı yakından sütuna bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="30868-119">In most cases data is partitioned on a date column that is closely tied toohello sequence which hello data is loaded toohello database.</span></span>  <span data-ttu-id="30868-120">İşlem günlüğü kaçınma hello bölümleri toomaintain veri kullanımının hello en büyük avantajlarından biri.</span><span class="sxs-lookup"><span data-stu-id="30868-120">One of hello greatest benefits of using partitions toomaintain data it hello avoidance of transaction logging.</span></span>  <span data-ttu-id="30868-121">Yalnızca ekleme, güncelleştirme veya verileri silme küçük bir düşünce ve çaba, hello en kolay yaklaşım olabileceği yükleme işlemi sırasında bölümleme kullanılarak önemli ölçüde performansı artırabilir.</span><span class="sxs-lookup"><span data-stu-id="30868-121">While simply inserting, updating or deleting data can be hello most straightforward approach, with a little thought and effort, using partitioning during your load process can substantially improve performance.</span></span>

<span data-ttu-id="30868-122">Bölüm geçiş kullanılan tooquickly Kaldır yüklenebilir veya bir tablonun bölümünü değiştirmek.</span><span class="sxs-lookup"><span data-stu-id="30868-122">Partition switching can be used tooquickly remove or replace a section of a table.</span></span>  <span data-ttu-id="30868-123">Örneğin, satış olgu tablosunun son 36 ay hello için yalnızca verileri içerebilir.</span><span class="sxs-lookup"><span data-stu-id="30868-123">For example, a sales fact table might contain just data for hello past 36 months.</span></span>  <span data-ttu-id="30868-124">Her ayın Hello sonunda hello satış verileri eski ayın hello tablosundan silindi.</span><span class="sxs-lookup"><span data-stu-id="30868-124">At hello end of every month, hello oldest month of sales data is deleted from hello table.</span></span>  <span data-ttu-id="30868-125">Bu veriler, en eski ay Merhaba bir delete deyimi toodelete hello verileri kullanarak silinemedi.</span><span class="sxs-lookup"><span data-stu-id="30868-125">This data could be deleted by using a delete statement toodelete hello data for hello oldest month.</span></span>  <span data-ttu-id="30868-126">Ancak, büyük miktarda veri-satır delete deyimi ile silme çok uzun zaman yanı bir sorun yaşanırsa, uzun süre toorollback ele geçirebilir büyük işlemleri hello riskini oluşturun.</span><span class="sxs-lookup"><span data-stu-id="30868-126">However, deleting a large amount of data row-by-row with a delete statement can take a very long time, as well as create hello risk of large transactions which could take a long time toorollback if something goes wrong.</span></span>  <span data-ttu-id="30868-127">Daha iyi yaklaşımı toosimply açılan hello en eski veri bölümdür.</span><span class="sxs-lookup"><span data-stu-id="30868-127">A more optimal approach is toosimply drop hello oldest partition of data.</span></span>  <span data-ttu-id="30868-128">Burada, hello tek tek satırları silme saat ele geçirebilir bölümünün tamamını silme saniye sürebilir.</span><span class="sxs-lookup"><span data-stu-id="30868-128">Where deleting hello individual rows could take hours, deleting an entire partition could take seconds.</span></span>

### <a name="benefits-tooqueries"></a><span data-ttu-id="30868-129">Avantajları tooqueries</span><span class="sxs-lookup"><span data-stu-id="30868-129">Benefits tooqueries</span></span>
<span data-ttu-id="30868-130">Bölümleme kullanılan tooimprove sorgu performansını da olabilir.</span><span class="sxs-lookup"><span data-stu-id="30868-130">Partitioning can also be used tooimprove query performance.</span></span>  <span data-ttu-id="30868-131">Bir sorgu bölümlenmiş bir sütunda bir filtre geçerliyse, bu bir çok daha küçük veri alt kümesini tam tablo taraması önleme hello olabilen bölümleri niteleme hello tarama tooonly hello sınırlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="30868-131">If a query applies a filter on a partitioned column, this can limit hello scan tooonly hello qualifying partitions which may be a much smaller subset of hello data, avoiding a full table scan.</span></span>  <span data-ttu-id="30868-132">Merhaba giriş kümelenmiş columnstore dizinleri hello koşul eleme performans avantajı daha az faydalı bağlıdır, ancak bazı durumlarda olabilir avantajı tooqueries.</span><span class="sxs-lookup"><span data-stu-id="30868-132">With hello introduction of clustered columnstore indexes, hello predicate elimination performance benefits are less beneficial, but in some cases there can be a benefit tooqueries.</span></span>  <span data-ttu-id="30868-133">Merhaba satış Olgu Tablosu 36 hello satış tarihi alanını kullanarak ay bölümlenmiş, örneğin, ardından hello satış tarihte filtre sorguları hello filtre eşleşmeyen bölümlerinde arama atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="30868-133">For example, if hello sales fact table is partitioned into 36 months using hello sales date field, then queries that filter on hello sale date can skip searching in partitions that don’t match hello filter.</span></span>

## <a name="partition-sizing-guidance"></a><span data-ttu-id="30868-134">Bölüm boyutlandırma kılavuzluğu</span><span class="sxs-lookup"><span data-stu-id="30868-134">Partition sizing guidance</span></span>
<span data-ttu-id="30868-135">Bölümleme sırasında kullanılan tooimprove performans içeren bir tablo oluşturma bazı senaryolar olabilir **çok fazla** bölümleri bazı koşullarda performans ölçeklenme.</span><span class="sxs-lookup"><span data-stu-id="30868-135">While partitioning can be used tooimprove performance some scenarios, creating a table with **too many** partitions can hurt performance under some circumstances.</span></span>  <span data-ttu-id="30868-136">Bu sorunları için kümelenmiş columnstore tabloları özellikle doğrudur.</span><span class="sxs-lookup"><span data-stu-id="30868-136">These concerns are especially true for clustered columnstore tables.</span></span>  <span data-ttu-id="30868-137">Toobe yararlı bölümleme için önemli toounderstand olduğu zaman toouse bölümlendirme ve hello sayısı bölümleri toocreate.</span><span class="sxs-lookup"><span data-stu-id="30868-137">For partitioning toobe helpful, it is important toounderstand when toouse partitioning and hello number of partitions toocreate.</span></span>  <span data-ttu-id="30868-138">Var. toohow olarak sabit bir hızlı kural yok birçok bölüm çok fazla, verilerinizde bağlıdır ve kaç tane bölümler toosimultaneously yüklüyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="30868-138">There is no hard fast rule as toohow many partitions are too many, it depends on your data and how many partitions you are loading toosimultaneously.</span></span>  <span data-ttu-id="30868-139">Ancak genel altın kural, 10'luk ekleme düşündüğünüz bölümlerinin değil 1000'lik too100s.</span><span class="sxs-lookup"><span data-stu-id="30868-139">But as a general rule of thumb, think of adding 10s too100s of partitions, not 1000s.</span></span>

<span data-ttu-id="30868-140">Üzerinde bölümleme oluştururken **kümelenmiş columnstore** tablolar, satır sayısını her bölüm güden önemli tooconsider değil.</span><span class="sxs-lookup"><span data-stu-id="30868-140">When creating partitioning on **clustered columnstore** tables, it is important tooconsider how many rows will land in each partition.</span></span>  <span data-ttu-id="30868-141">Dağıtım ve bölüm başına 1 milyon satır en az, en iyi sıkıştırma ve kümelenmiş columnstore tabloları performansını için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="30868-141">For optimal compression and performance of clustered columnstore tables, a minimum of 1 million rows per distribution and partition is needed.</span></span>  <span data-ttu-id="30868-142">Bölümler oluşturulmadan önce SQL veri ambarı her tablo 60 dağıtılmış veritabanlarına zaten böler.</span><span class="sxs-lookup"><span data-stu-id="30868-142">Before partitions are created, SQL Data Warehouse already divides each table into 60 distributed databases.</span></span>  <span data-ttu-id="30868-143">Herhangi bir bölümleme eklenen tooa Tablo ayrıca hello arka planda oluşturulan toohello dağıtımları olur.</span><span class="sxs-lookup"><span data-stu-id="30868-143">Any partitioning added tooa table is in addition toohello distributions created behind hello scenes.</span></span>  <span data-ttu-id="30868-144">Bu örnekte, Hello satış Olgu Tablosu 36 aylık bölümleri içeriyordu ve SQL Data Warehouse 60 dağıtımları sahip o aylar yerleştirildiğinde tablo 60 milyon satır aylık veya 2.1 milyon satır içermelidir satış olgu hello kullanıyor.</span><span class="sxs-lookup"><span data-stu-id="30868-144">Using this example, if hello sales fact table contained 36 monthly partitions, and given that SQL Data Warehouse has 60 distributions, then hello sales fact table should contain 60 million rows per month, or 2.1 billion rows when all months are populated.</span></span>  <span data-ttu-id="30868-145">Bir tablo hello önerilen minimum bölüm başına satır sayısı çok önemli ölçüde daha az satır içeriyorsa, daha az bölümleri sipariş toomake artış hello bölüm başına satır sayısı kullanmayı düşünün.</span><span class="sxs-lookup"><span data-stu-id="30868-145">If a table contains significantly less rows than hello recommended minimum number of rows per partition, consider using fewer partitions in order toomake increase hello number of rows per partition.</span></span>  <span data-ttu-id="30868-146">Ayrıca bkz. hello [dizin] [ Index] Itanium tabanlı sistemler için SQL Data Warehouse tooassess hello kalitesi küme columnstore dizinleri, üzerinde çalışan sorguları içerir makale.</span><span class="sxs-lookup"><span data-stu-id="30868-146">Also see hello [Indexing][Index] article which includes queries that can be run on SQL Data Warehouse tooassess hello quality of cluster columnstore indexes.</span></span>

## <a name="syntax-difference-from-sql-server"></a><span data-ttu-id="30868-147">SQL Server sözdizimi farkı</span><span class="sxs-lookup"><span data-stu-id="30868-147">Syntax difference from SQL Server</span></span>
<span data-ttu-id="30868-148">SQL veri ambarı SQL Server'dan biraz farklıdır basitleştirilmiş bir bölüm tanımı tanıtır.</span><span class="sxs-lookup"><span data-stu-id="30868-148">SQL Data Warehouse introduces a simplified definition of partitions which is slightly different from SQL Server.</span></span>  <span data-ttu-id="30868-149">SQL Server'da olduğu gibi SQL veri ambarı'nda bölümleme işlevleri ve şeması kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="30868-149">Partitioning functions and schemes are not used in SQL Data Warehouse as they are in SQL Server.</span></span>  <span data-ttu-id="30868-150">Bunun yerine, tüm toodo gereken budur bölümlenmiş sütun ve hello sınır noktaları tanımlar.</span><span class="sxs-lookup"><span data-stu-id="30868-150">Instead, all you need toodo is identify partitioned column and hello boundary points.</span></span>  <span data-ttu-id="30868-151">Bölümleme hello sözdizimi SQL Server'dan biraz farklı olabilir, ancak hello temel kavramları şunlardır hello aynı.</span><span class="sxs-lookup"><span data-stu-id="30868-151">While hello syntax of partitioning may be slightly different from SQL Server, hello basic concepts are hello same.</span></span>  <span data-ttu-id="30868-152">SQL Server ve SQL Data Warehouse aralıklı bölüm olabilir tablo başına bir bölüm sütunu destekler.</span><span class="sxs-lookup"><span data-stu-id="30868-152">SQL Server and SQL Data Warehouse support one partition column per table, which can be ranged partition.</span></span>  <span data-ttu-id="30868-153">Bölümlendirme, hakkında daha fazla toolearn bkz [bölümlenmiş tablolar ve dizinler][Partitioned Tables and Indexes].</span><span class="sxs-lookup"><span data-stu-id="30868-153">toolearn more about partitioning, see [Partitioned Tables and Indexes][Partitioned Tables and Indexes].</span></span>

<span data-ttu-id="30868-154">bölümlenmiş bir SQL veri ambarı örneği aşağıda Hello [CREATE TABLE] [ CREATE TABLE] deyimi, bölümler hello OrderDateKey sütun hello Factınternetsales tablosunda:</span><span class="sxs-lookup"><span data-stu-id="30868-154">hello below example of a SQL Data Warehouse partitioned [CREATE TABLE][CREATE TABLE] statement, partitions hello FactInternetSales table on hello OrderDateKey column:</span></span>

```sql
CREATE TABLE [dbo].[FactInternetSales]
(
    [ProductKey]            int          NOT NULL
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
,   DISTRIBUTION = HASH([ProductKey])
,   PARTITION   (   [OrderDateKey] RANGE RIGHT FOR VALUES
                    (20000101,20010101,20020101
                    ,20030101,20040101,20050101
                    )
                )
)
;
```

## <a name="migrating-partitioning-from-sql-server"></a><span data-ttu-id="30868-155">SQL Server'dan bölümleme geçirme</span><span class="sxs-lookup"><span data-stu-id="30868-155">Migrating partitioning from SQL Server</span></span>
<span data-ttu-id="30868-156">toomigrate SQL Server veri ambarı tanımları tooSQL yalnızca bölüm:</span><span class="sxs-lookup"><span data-stu-id="30868-156">toomigrate SQL Server partition definitions tooSQL Data Warehouse simply:</span></span>

* <span data-ttu-id="30868-157">SQL Server Hello ortadan [bölüm düzeni][partition scheme].</span><span class="sxs-lookup"><span data-stu-id="30868-157">Eliminate hello SQL Server [partition scheme][partition scheme].</span></span>
* <span data-ttu-id="30868-158">Merhaba eklemek [bölümleme işlevi] [ partition function] tanımı tooyour tablo oluştur.</span><span class="sxs-lookup"><span data-stu-id="30868-158">Add hello [partition function][partition function] definition tooyour CREATE TABLE.</span></span>

<span data-ttu-id="30868-159">Bölümlenmiş bir tablodaki bir SQL Server örneği hello SQL aşağıda geçiş durumunda toointerrogate hello her bölüm satır sayısı yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="30868-159">If you are migrating a partitioned table from a SQL Server instance hello below SQL can help you toointerrogate hello number of rows that are in each partition.</span></span>  <span data-ttu-id="30868-160">Merhaba aynı bölümleme ayrıntı SQL Data Warehouse kullanılırsa, bölüm başına satır sayısı hello 60 faktörüyle düşürür aklınızda bulundurun.</span><span class="sxs-lookup"><span data-stu-id="30868-160">Keep in mind that if hello same partitioning granularity is used on SQL Data Warehouse, hello number of rows per partition will decrease by a factor of 60.</span></span>  

```sql
-- Partition information for a SQL Server Database
SELECT      s.[name]                        AS      [schema_name]
,           t.[name]                        AS      [table_name]
,           i.[name]                        AS      [index_name]
,           p.[partition_number]            AS      [partition_number]
,           SUM(a.[used_pages]*8.0)         AS      [partition_size_kb]
,           SUM(a.[used_pages]*8.0)/1024    AS      [partition_size_mb]
,           SUM(a.[used_pages]*8.0)/1048576 AS      [partition_size_gb]
,           p.[rows]                        AS      [partition_row_count]
,           rv.[value]                      AS      [partition_boundary_value]
,           p.[data_compression_desc]       AS      [partition_compression_desc]
FROM        sys.schemas s
JOIN        sys.tables t                    ON      t.[schema_id]         = s.[schema_id]
JOIN        sys.partitions p                ON      p.[object_id]         = t.[object_id]
JOIN        sys.allocation_units a          ON      a.[container_id]      = p.[partition_id]
JOIN        sys.indexes i                   ON      i.[object_id]         = p.[object_id]
                                            AND     i.[index_id]          = p.[index_id]
JOIN        sys.data_spaces ds              ON      ds.[data_space_id]    = i.[data_space_id]
LEFT JOIN   sys.partition_schemes ps        ON      ps.[data_space_id]    = ds.[data_space_id]
LEFT JOIN   sys.partition_functions pf      ON      pf.[function_id]      = ps.[function_id]
LEFT JOIN   sys.partition_range_values rv   ON      rv.[function_id]      = pf.[function_id]
                                            AND     rv.[boundary_id]      = p.[partition_number]
WHERE       p.[index_id] <=1
GROUP BY    s.[name]
,           t.[name]
,           i.[name]
,           p.[partition_number]
,           p.[rows]
,           rv.[value]
,           p.[data_compression_desc]
;
```

## <a name="workload-management"></a><span data-ttu-id="30868-161">İş yükü yönetimi</span><span class="sxs-lookup"><span data-stu-id="30868-161">Workload management</span></span>
<span data-ttu-id="30868-162">Bir son parçası göz önünde bulundurarak toofactor toohello tablo bölüm karar içinde olduğu [iş yükü Yönetim][workload management].</span><span class="sxs-lookup"><span data-stu-id="30868-162">One final piece consideration toofactor in toohello table partition decision is [workload management][workload management].</span></span>  <span data-ttu-id="30868-163">SQL veri ambarı iş yükü yönetiminde öncelikle hello bellek ve eşzamanlılık yönetimidir.</span><span class="sxs-lookup"><span data-stu-id="30868-163">Workload management in SQL Data Warehouse is primarily hello management of memory and concurrency.</span></span>  <span data-ttu-id="30868-164">SQL veri ambarı hello tooeach dağıtım sorgu yürütme sırasında ayrılan en fazla bellek yönetilen kaynak sınıfları ' dir.</span><span class="sxs-lookup"><span data-stu-id="30868-164">In SQL Data Warehouse hello maximum memory allocated tooeach distribution during query execution is governed resource classes.</span></span>  <span data-ttu-id="30868-165">İdeal olarak, bölümler hello bellek gereksinimlerini kümelenmiş columnstore dizinleri oluşturma gibi diğer faktörlere söz konusu boyutta.</span><span class="sxs-lookup"><span data-stu-id="30868-165">Ideally your partitions will be sized in consideration of other factors like hello memory needs of building clustered columnstore indexes.</span></span>  <span data-ttu-id="30868-166">Daha fazla bellek ayırırken columnstore dizinleri avantajı büyük ölçüde kümelenmiş.</span><span class="sxs-lookup"><span data-stu-id="30868-166">Clustered columnstore indexes benefit greatly when they are allocated more memory.</span></span>  <span data-ttu-id="30868-167">Bu nedenle, bir bölüm dizini yeniden tooensure bellek gerek duyuldu değil isteyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="30868-167">Therefore, you will want tooensure that a partition index rebuild is not starved of memory.</span></span> <span data-ttu-id="30868-168">Merhaba kullanılabilir tooyour sorgu elde edilebilir hello varsayılan rol, smallrc, tooone, geçiş tarafından bellek miktarını artırmayı hello largerc gibi diğer rolleri.</span><span class="sxs-lookup"><span data-stu-id="30868-168">Increasing hello amount of memory available tooyour query can be achieved by switching from hello default role, smallrc, tooone of hello other roles such as largerc.</span></span>

<span data-ttu-id="30868-169">Dağıtım başına bellek hello ayrılması hakkında bilgi hello kaynak İdarecisi dinamik yönetim görünümlerini sorgulayarak kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="30868-169">Information on hello allocation of memory per distribution is available by querying hello resource governor dynamic management views.</span></span> <span data-ttu-id="30868-170">Gerçekte, bellek ataması hello resimde daha az olur.</span><span class="sxs-lookup"><span data-stu-id="30868-170">In reality your memory grant will be less than hello figures below.</span></span> <span data-ttu-id="30868-171">Ancak, bu veri yönetimi işlemleri için iyi bir bölüm boyutlandırma olduğunda kullanabileceğiniz kılavuzu düzeyi sağlar.</span><span class="sxs-lookup"><span data-stu-id="30868-171">However, this provides a level of guidance that you can use when sizing your partitions for data management operations.</span></span>  <span data-ttu-id="30868-172">Merhaba bellek ataması hello çok büyük kaynak sınıfı tarafından sağlanan dışında bir bölüm boyutlandırma tooavoid deneyin.</span><span class="sxs-lookup"><span data-stu-id="30868-172">Try tooavoid sizing your partitions beyond hello memory grant provided by hello extra large resource class.</span></span> <span data-ttu-id="30868-173">Bu şekil, bölümler büyümesine hangi sırayla tooless en iyi sıkıştırma müşteri adayları bellek baskısı hello riskini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="30868-173">If your partitions grow beyond this figure you run hello risk of memory pressure which in turn leads tooless optimal compression.</span></span>

```sql
SELECT  rp.[name]                                AS [pool_name]
,       rp.[max_memory_kb]                        AS [max_memory_kb]
,       rp.[max_memory_kb]/1024                    AS [max_memory_mb]
,       rp.[max_memory_kb]/1048576                AS [mex_memory_gb]
,       rp.[max_memory_percent]                    AS [max_memory_percent]
,       wg.[name]                                AS [group_name]
,       wg.[importance]                            AS [group_importance]
,       wg.[request_max_memory_grant_percent]    AS [request_max_memory_grant_percent]
FROM    sys.dm_pdw_nodes_resource_governor_workload_groups    wg
JOIN    sys.dm_pdw_nodes_resource_governor_resource_pools    rp ON wg.[pool_id] = rp.[pool_id]
WHERE   wg.[name] like 'SloDWGroup%'
AND     rp.[name]    = 'SloDWPool'
;
```

## <a name="partition-switching"></a><span data-ttu-id="30868-174">Bölüm değiştirme</span><span class="sxs-lookup"><span data-stu-id="30868-174">Partition switching</span></span>
<span data-ttu-id="30868-175">SQL veri ambarı geçiş bölme ve birleştirme bölüm destekler.</span><span class="sxs-lookup"><span data-stu-id="30868-175">SQL Data Warehouse supports partition splitting, merging, and switching.</span></span> <span data-ttu-id="30868-176">Bu işlevlerin her biri hello kullanarak excuted olan [ALTER TABLE] [ ALTER TABLE] deyimi.</span><span class="sxs-lookup"><span data-stu-id="30868-176">Each of these functions is excuted using hello [ALTER TABLE][ALTER TABLE] statement.</span></span>

<span data-ttu-id="30868-177">tooswitch bölümleri iki tablo arasında hello bölümleri ilgili sınırlarının hizalama ve hello tablo tanımları eşleştiğinden emin olmalısınız.</span><span class="sxs-lookup"><span data-stu-id="30868-177">tooswitch partitions between two tables you must ensure that hello partitions align on their respective boundaries and that hello table definitions match.</span></span> <span data-ttu-id="30868-178">Denetim kısıtlamalarında kullanılabilir olmadığından bir tablo hello kaynak tablodaki değerleri tooenforce hello aralığı hello içermelidir hello hedef tablo olarak aynı bölüm sınırlar.</span><span class="sxs-lookup"><span data-stu-id="30868-178">As check constraints are not available tooenforce hello range of values in a table hello source table must contain hello same partition boundaries as hello target table.</span></span> <span data-ttu-id="30868-179">Merhaba durum bu değilse, hello bölüm meta verileri eşitlenmemiş hello bölüm anahtarı başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="30868-179">If this is not hello case, then hello partition switch will fail as hello partition metadata will not be synchronized.</span></span>

### <a name="how-toosplit-a-partition-that-contains-data"></a><span data-ttu-id="30868-180">Nasıl toosplit verileri içeren bir bölüm</span><span class="sxs-lookup"><span data-stu-id="30868-180">How toosplit a partition that contains data</span></span>
<span data-ttu-id="30868-181">Merhaba en verimli yöntemi toosplit zaten verileri içeren bir bölüm olduğundan toouse bir `CTAS` deyimi.</span><span class="sxs-lookup"><span data-stu-id="30868-181">hello most efficient method toosplit a partition that already contains data is toouse a `CTAS` statement.</span></span> <span data-ttu-id="30868-182">Merhaba bölümlenmiş tabloda kümelenmiş columnstore ise, bölünebilir önce sonra hello tablo bölüm boş olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="30868-182">If hello partitioned table is a clustered columnstore then hello table partition must be empty before it can be split.</span></span>

<span data-ttu-id="30868-183">Her bölümde bir satır içeren bir örnek bölümlenmiş columnstore tablo aşağıdadır:</span><span class="sxs-lookup"><span data-stu-id="30868-183">Below is a sample partitioned columnstore table containing one row in each partition:</span></span>

```sql
CREATE TABLE [dbo].[FactInternetSales]
(
        [ProductKey]            int          NOT NULL
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
,   DISTRIBUTION = HASH([ProductKey])
,   PARTITION   (   [OrderDateKey] RANGE RIGHT FOR VALUES
                    (20000101
                    )
                )
)
;

INSERT INTO dbo.FactInternetSales
VALUES (1,19990101,1,1,1,1,1,1);
INSERT INTO dbo.FactInternetSales
VALUES (1,20000101,1,1,1,1,1,1);


CREATE STATISTICS Stat_dbo_FactInternetSales_OrderDateKey ON dbo.FactInternetSales(OrderDateKey);
```

> [!NOTE]
> <span data-ttu-id="30868-184">Oluşturma hello istatistiği nesnesiyle Biz bu tablo meta veri daha doğru olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="30868-184">By Creating hello statistic object, we ensure that table metadata is more accurate.</span></span> <span data-ttu-id="30868-185">Biz istatistikleri oluşturma atlarsanız, SQL veri ambarı varsayılan değerleri kullanır.</span><span class="sxs-lookup"><span data-stu-id="30868-185">If we omit creating statistics, then SQL Data Warehouse will use default values.</span></span> <span data-ttu-id="30868-186">Lütfen istatistikleri ayrıntıları gözden geçirme için [istatistikleri][statistics].</span><span class="sxs-lookup"><span data-stu-id="30868-186">For details on statistics please review [statistics][statistics].</span></span>
> 
> 

<span data-ttu-id="30868-187">Biz sonra hello satır sayısı için hello kullanarak sorgulama yapabilirsiniz `sys.partitions` Katalog görünümü:</span><span class="sxs-lookup"><span data-stu-id="30868-187">We can then query for hello row count using hello `sys.partitions` catalog view:</span></span>

```sql
SELECT  QUOTENAME(s.[name])+'.'+QUOTENAME(t.[name]) as Table_name
,       i.[name] as Index_name
,       p.partition_number as Partition_nmbr
,       p.[rows] as Row_count
,       p.[data_compression_desc] as Data_Compression_desc
FROM    sys.partitions p
JOIN    sys.tables     t    ON    p.[object_id]   = t.[object_id]
JOIN    sys.schemas    s    ON    t.[schema_id]   = s.[schema_id]
JOIN    sys.indexes    i    ON    p.[object_id]   = i.[object_Id]
                            AND   p.[index_Id]    = i.[index_Id]
WHERE t.[name] = 'FactInternetSales'
;
```

<span data-ttu-id="30868-188">Toosplit Bu tablo çalışırsanız şu hata iletisini alırsınız:</span><span class="sxs-lookup"><span data-stu-id="30868-188">If we try toosplit this table, we will get an error:</span></span>

```sql
ALTER TABLE FactInternetSales SPLIT RANGE (20010101);
```

<span data-ttu-id="30868-189">Msg 35346, düzey 15, State 1, ALTER PARTITION deyiminin yan tümcesi 44 Satırı Böl Hello bölüm boş olmadığından başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="30868-189">Msg 35346, Level 15, State 1, Line 44 SPLIT clause of ALTER PARTITION statement failed because hello partition is not empty.</span></span>  <span data-ttu-id="30868-190">Merhaba tabloda bir columnstore dizini mevcut olduğunda, yalnızca boş bölümler bölünebilir.</span><span class="sxs-lookup"><span data-stu-id="30868-190">Only empty partitions can be split in when a columnstore index exists on hello table.</span></span> <span data-ttu-id="30868-191">Merhaba ALTER PARTITION deyimini yürütmeden, ardından ALTER PARTITION tamamlandıktan sonra hello columnstore dizinini yeniden oluşturmayı önce hello columnstore dizinini devre dışı bırakın.</span><span class="sxs-lookup"><span data-stu-id="30868-191">Consider disabling hello columnstore index before issuing hello ALTER PARTITION statement, then rebuilding hello columnstore index after ALTER PARTITION is complete.</span></span>

<span data-ttu-id="30868-192">Ancak, biz kullanabilirsiniz `CTAS` toocreate yeni bir tablo toohold verilerimizi.</span><span class="sxs-lookup"><span data-stu-id="30868-192">However, we can use `CTAS` toocreate a new table toohold our data.</span></span>

```sql
CREATE TABLE dbo.FactInternetSales_20000101
    WITH    (   DISTRIBUTION = HASH(ProductKey)
            ,   CLUSTERED COLUMNSTORE INDEX
            ,   PARTITION   (   [OrderDateKey] RANGE RIGHT FOR VALUES
                                (20000101
                                )
                            )
            )
AS
SELECT *
FROM    FactInternetSales
WHERE   1=2
;
```

<span data-ttu-id="30868-193">Merhaba bölüm sınırları hizalı gibi bir anahtar izin verilir.</span><span class="sxs-lookup"><span data-stu-id="30868-193">As hello partition boundaries are aligned a switch is permitted.</span></span> <span data-ttu-id="30868-194">Biz sonradan bölebilirsiniz boş bir bölüm ile bu hello kaynak tablosu bırakır.</span><span class="sxs-lookup"><span data-stu-id="30868-194">This will leave hello source table with an empty partition that we can subsequently split.</span></span>

```sql
ALTER TABLE FactInternetSales SWITCH PARTITION 2 too FactInternetSales_20000101 PARTITION 2;

ALTER TABLE FactInternetSales SPLIT RANGE (20010101);
```

<span data-ttu-id="30868-195">Toodo kalan tek şey bizim veri toohello yeni bölüm kullanarak sınırları tooalign `CTAS` ve verilerimizi toohello ana tabloda geçiş</span><span class="sxs-lookup"><span data-stu-id="30868-195">All that is left toodo is tooalign our data toohello new partition boundaries using `CTAS` and switch our data back in toohello main table</span></span>

```sql
CREATE TABLE [dbo].[FactInternetSales_20000101_20010101]
    WITH    (   DISTRIBUTION = HASH([ProductKey])
            ,   CLUSTERED COLUMNSTORE INDEX
            ,   PARTITION   (   [OrderDateKey] RANGE RIGHT FOR VALUES
                                (20000101,20010101
                                )
                            )
            )
AS
SELECT  *
FROM    [dbo].[FactInternetSales_20000101]
WHERE   [OrderDateKey] >= 20000101
AND     [OrderDateKey] <  20010101
;

ALTER TABLE dbo.FactInternetSales_20000101_20010101 SWITCH PARTITION 2 toodbo.FactInternetSales PARTITION 2;
```

<span data-ttu-id="30868-196">Merhaba veri hello hareketini tamamladıktan sonra bir fikir toorefresh hello istatistikleri olduğu hello hedef tablo tooensure üzerinde bunlar doğru bir şekilde hello yeni dağıtım ilgili bölümlerinin hello veri yansıtmak:</span><span class="sxs-lookup"><span data-stu-id="30868-196">Once you have completed hello movement of hello data it is a good idea toorefresh hello statistics on hello target table tooensure they accurately reflect hello new distribution of hello data in their respective partitions:</span></span>

```sql
UPDATE STATISTICS [dbo].[FactInternetSales];
```

### <a name="table-partitioning-source-control"></a><span data-ttu-id="30868-197">Kaynak denetimi bölümleme tablosu</span><span class="sxs-lookup"><span data-stu-id="30868-197">Table partitioning source control</span></span>
<span data-ttu-id="30868-198">tooavoid tablosu tanımınızı **paslanma** kaynak denetim sisteminiz yaklaşımı izleyerek tooconsider hello isteyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="30868-198">tooavoid your table definition from **rusting** in your source control system you may want tooconsider hello following approach:</span></span>

1. <span data-ttu-id="30868-199">Bölümlenmiş bir tablodaki olarak ancak hiç bölüm değerlerle Hello tablosu oluşturma</span><span class="sxs-lookup"><span data-stu-id="30868-199">Create hello table as a partitioned table but with no partition values</span></span>

```sql
CREATE TABLE [dbo].[FactInternetSales]
(
    [ProductKey]            int          NOT NULL
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
,   DISTRIBUTION = HASH([ProductKey])
,   PARTITION   (   [OrderDateKey] RANGE RIGHT FOR VALUES
                    ()
                )
)
;
```

1. <span data-ttu-id="30868-200">`SPLIT`Merhaba tablo hello dağıtım işleminin bir parçası olarak:</span><span class="sxs-lookup"><span data-stu-id="30868-200">`SPLIT` hello table as part of hello deployment process:</span></span>

```sql
-- Create a table containing hello partition boundaries

CREATE TABLE #partitions
WITH
(
    LOCATION = USER_DB
,   DISTRIBUTION = HASH(ptn_no)
)
AS
SELECT  ptn_no
,       ROW_NUMBER() OVER (ORDER BY (ptn_no)) as seq_no
FROM    (
        SELECT CAST(20000101 AS INT) ptn_no
        UNION ALL
        SELECT CAST(20010101 AS INT)
        UNION ALL
        SELECT CAST(20020101 AS INT)
        UNION ALL
        SELECT CAST(20030101 AS INT)
        UNION ALL
        SELECT CAST(20040101 AS INT)
        ) a
;

-- Iterate over hello partition boundaries and split hello table

DECLARE @c INT = (SELECT COUNT(*) FROM #partitions)
,       @i INT = 1                                 --iterator for while loop
,       @q NVARCHAR(4000)                          --query
,       @p NVARCHAR(20)     = N''                  --partition_number
,       @s NVARCHAR(128)    = N'dbo'               --schema
,       @t NVARCHAR(128)    = N'FactInternetSales' --table
;

WHILE @i <= @c
BEGIN
    SET @p = (SELECT ptn_no FROM #partitions WHERE seq_no = @i);
    SET @q = (SELECT N'ALTER TABLE '+@s+N'.'+@t+N' SPLIT RANGE ('+@p+N');');

    -- PRINT @q;
    EXECUTE sp_executesql @q;

    SET @i+=1;
END

-- Code clean-up

DROP TABLE #partitions;
```

<span data-ttu-id="30868-201">Bu yaklaşım hello ile kaynak denetimi kodu statik kalır ve hello bölümleme sınır değerleri toobe dinamik izin verilir; Merhaba ambarıyla zamanla gelişen.</span><span class="sxs-lookup"><span data-stu-id="30868-201">With this approach hello code in source control remains static and hello partitioning boundary values are allowed toobe dynamic; evolving with hello warehouse over time.</span></span>

## <a name="next-steps"></a><span data-ttu-id="30868-202">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="30868-202">Next steps</span></span>
<span data-ttu-id="30868-203">toolearn daha hello makalelere bakın üzerinde [tablo genel bakışı][Overview], [tablo veri türleri][Data Types], [bir tablodağıtma] [ Distribute], [Tablo dizin][Index], [tablo istatistikleri koruma] [ Statistics] ve [ Geçici tablolara][Temporary].</span><span class="sxs-lookup"><span data-stu-id="30868-203">toolearn more, see hello articles on [Table Overview][Overview], [Table Data Types][Data Types], [Distributing a Table][Distribute], [Indexing a Table][Index], [Maintaining Table Statistics][Statistics] and [Temporary Tables][Temporary].</span></span>  <span data-ttu-id="30868-204">En iyi uygulamalar hakkında daha fazla bilgi için bkz: [SQL veri ambarı en iyi uygulamalar][SQL Data Warehouse Best Practices].</span><span class="sxs-lookup"><span data-stu-id="30868-204">For more about best practices, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>

<!--Image references-->

<!--Article references-->
[Overview]: ./sql-data-warehouse-tables-overview.md
[Data Types]: ./sql-data-warehouse-tables-data-types.md
[Distribute]: ./sql-data-warehouse-tables-distribute.md
[Index]: ./sql-data-warehouse-tables-index.md
[Partition]: ./sql-data-warehouse-tables-partition.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[Temporary]: ./sql-data-warehouse-tables-temporary.md
[workload management]: ./sql-data-warehouse-develop-concurrency.md
[SQL Data Warehouse Best Practices]: ./sql-data-warehouse-best-practices.md

<!-- MSDN Articles -->
[Partitioned Tables and Indexes]: https://msdn.microsoft.com/library/ms190787.aspx
[ALTER TABLE]: https://msdn.microsoft.com/en-us/library/ms190273.aspx
[CREATE TABLE]: https://msdn.microsoft.com/library/mt203953.aspx
[partition function]: https://msdn.microsoft.com/library/ms187802.aspx
[partition scheme]: https://msdn.microsoft.com/library/ms179854.aspx


<!-- Other web references -->
