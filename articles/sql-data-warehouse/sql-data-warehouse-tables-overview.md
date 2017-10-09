---
title: "SQL veri ambarı tablolarda aaaOverview | Microsoft Docs"
description: "Azure SQL veri ambarı tabloları ile çalışmaya başlama."
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: jhubbard
editor: 
ms.assetid: 2114d9ad-c113-43da-859f-419d72604bdf
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 06/29/2016
ms.author: shigu;jrj
ms.openlocfilehash: 4edabcb4b0754bf6c99c2b6b3f0c077749051d9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-tables-in-sql-data-warehouse"></a><span data-ttu-id="0b660-103">SQL veri ambarı tablolarda genel bakış</span><span class="sxs-lookup"><span data-stu-id="0b660-103">Overview of tables in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="0b660-104">[Genel bakış][Overview]</span><span class="sxs-lookup"><span data-stu-id="0b660-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="0b660-105">[Veri türleri][Data Types]</span><span class="sxs-lookup"><span data-stu-id="0b660-105">[Data Types][Data Types]</span></span>
> * <span data-ttu-id="0b660-106">[Dağıt][Distribute]</span><span class="sxs-lookup"><span data-stu-id="0b660-106">[Distribute][Distribute]</span></span>
> * <span data-ttu-id="0b660-107">[Dizin][Index]</span><span class="sxs-lookup"><span data-stu-id="0b660-107">[Index][Index]</span></span>
> * <span data-ttu-id="0b660-108">[Bölüm][Partition]</span><span class="sxs-lookup"><span data-stu-id="0b660-108">[Partition][Partition]</span></span>
> * <span data-ttu-id="0b660-109">[İstatistikleri][Statistics]</span><span class="sxs-lookup"><span data-stu-id="0b660-109">[Statistics][Statistics]</span></span>
> * <span data-ttu-id="0b660-110">[Geçici][Temporary]</span><span class="sxs-lookup"><span data-stu-id="0b660-110">[Temporary][Temporary]</span></span>
> 
> 

<span data-ttu-id="0b660-111">SQL Data Warehouse'da tablo oluşturma ile çalışmaya başlama basit bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="0b660-111">Getting started with creating tables in SQL Data Warehouse is simple.</span></span>  <span data-ttu-id="0b660-112">Merhaba temel [CREATE TABLE] [ CREATE TABLE] sözdizimi aşağıdaki hello yaygın sözdizimi büyük olasılıkla zaten aşina diğer veritabanlarıyla çalışma.</span><span class="sxs-lookup"><span data-stu-id="0b660-112">hello basic [CREATE TABLE][CREATE TABLE] syntax follows hello common syntax you are most likely already familiar with from working with other databases.</span></span>  <span data-ttu-id="0b660-113">toocreate bir tablo, yalnızca ihtiyacınız tooname, tablo, sütun adı ve her sütun için veri türlerini tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="0b660-113">toocreate a table, you simply need tooname your table, name your columns and define data types for each column.</span></span>  <span data-ttu-id="0b660-114">Diğer veritabanlarında tabloları olduğunuz oluşturursanız, bilgili tooyou görünmelidir.</span><span class="sxs-lookup"><span data-stu-id="0b660-114">If you've create tables in other databases, this should look very familiar tooyou.</span></span>

```sql  
CREATE TABLE Customers (FirstName VARCHAR(25), LastName VARCHAR(25))
 ``` 

<span data-ttu-id="0b660-115">Yukarıdaki örnek Hello müşteriler iki sütunlarla FirstName ve LastName adlı bir tablo oluşturur.</span><span class="sxs-lookup"><span data-stu-id="0b660-115">hello above example creates a table named Customers with two columns, FirstName and LastName.</span></span>  <span data-ttu-id="0b660-116">Her sütun hello veri too25 karakterleri sınırlar VARCHAR(25) veri türü ile tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="0b660-116">Each column is defined with a data type of VARCHAR(25), which limits hello data too25 characters.</span></span>  <span data-ttu-id="0b660-117">Bu temel tabloya yanı sıra diğer özniteliklerini olan çoğunlukla hello diğer veritabanları aynı.</span><span class="sxs-lookup"><span data-stu-id="0b660-117">These fundamental attributes of a table, as well as others, are mostly hello same as other databases.</span></span>  <span data-ttu-id="0b660-118">Veri türleri her sütun için tanımlanır ve verilerinizi hello bütünlüğünü sağlamak.</span><span class="sxs-lookup"><span data-stu-id="0b660-118">Data types are defined for each column and ensure hello integrity of your data.</span></span>  <span data-ttu-id="0b660-119">Dizinleri g/ç azaltarak tooimprove performans eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="0b660-119">Indexes can be added tooimprove performance by reducing I/O.</span></span>  <span data-ttu-id="0b660-120">Toomodify veri gerektiğinde bölümleme tooimprove performans eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="0b660-120">Partitioning can be added tooimprove performance when you need toomodify data.</span></span>

<span data-ttu-id="0b660-121">[Yeniden adlandırma] [ RENAME] bir SQL Data Warehouse tablo şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="0b660-121">[Renaming][RENAME] a SQL Data Warehouse table looks like this:</span></span>

```sql  
RENAME OBJECT Customer tooCustomerOrig; 
 ```

## <a name="distributed-tables"></a><span data-ttu-id="0b660-122">Dağıtılmış tablolar</span><span class="sxs-lookup"><span data-stu-id="0b660-122">Distributed tables</span></span>
<span data-ttu-id="0b660-123">SQL veri ambarı hello gibi dağıtılmış sistemleri tarafından sunulan yeni bir temel öznitelik **dağıtım sütun**.</span><span class="sxs-lookup"><span data-stu-id="0b660-123">A new fundamental attribute introduced by distributed systems like SQL Data Warehouse is hello **distribution column**.</span></span>  <span data-ttu-id="0b660-124">Merhaba dağıtım çok ne, gibi göründüğü sütundur.</span><span class="sxs-lookup"><span data-stu-id="0b660-124">hello distribution column is very much what it sounds like.</span></span>  <span data-ttu-id="0b660-125">Belirler hello sütun olduğunu nasıl toodistribute, veya bölme, verilerinizi hello perde arkasında.</span><span class="sxs-lookup"><span data-stu-id="0b660-125">It is hello column that determines how toodistribute, or divide, your data behind hello scenes.</span></span>  <span data-ttu-id="0b660-126">Merhaba dağıtım sütun belirtmeden bir tablo oluşturduğunuzda hello tablo otomatik kullanılarak dağıtılır **hepsini**.</span><span class="sxs-lookup"><span data-stu-id="0b660-126">When you create a table without specifying hello distribution column, hello table is automatically distributed using **round robin**.</span></span>  <span data-ttu-id="0b660-127">Hepsini bir kez tabloları bazı senaryolarda yeterli olabilirler, ancak dağıtım sütunları tanımlama büyük ölçüde veri taşıma böylece performansı en iyi duruma getirme sorguları sırasında azaltabilir.</span><span class="sxs-lookup"><span data-stu-id="0b660-127">While round robin tables can be sufficient in some scenarios, defining distribution columns can greatly reduce data movement during queries, thus optimizing performance.</span></span>  <span data-ttu-id="0b660-128">Durumlarda bir tablodaki verileri kısa süreli olduğu toocreate hello hello tabloyla seçme **çoğaltmak** dağıtım türü veri tooeach işlem düğümü kopyalar ve veri taşıma sorgu yürütme zaman kaydeder.</span><span class="sxs-lookup"><span data-stu-id="0b660-128">In situations where there is a small amount of data in a table, choosing toocreate hello table with hello **replicate** distribution type copies data tooeach compute node and saves data movement at query execution time.</span></span> <span data-ttu-id="0b660-129">Bkz: [tablo dağıtma] [ Distribute] toolearn nasıl hakkında daha fazla tooselect dağıtım sütun.</span><span class="sxs-lookup"><span data-stu-id="0b660-129">See [Distributing a Table][Distribute] toolearn more about how tooselect a distribution column.</span></span>

## <a name="indexing-and-partitioning-tables"></a><span data-ttu-id="0b660-130">Dizin oluşturma ve tabloları bölümlendirme</span><span class="sxs-lookup"><span data-stu-id="0b660-130">Indexing and partitioning tables</span></span>
<span data-ttu-id="0b660-131">SQL veri ambarı kullanarak daha gelişmiş haline gelir ve toooptimize performans istediğiniz gibi toolearn tablo tasarımı hakkında daha fazla isteyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="0b660-131">As you become more advanced in using SQL Data Warehouse and want toooptimize performance, you'll want toolearn more about Table Design.</span></span>  <span data-ttu-id="0b660-132">toolearn daha hello makalelere bakın üzerinde [tablo veri türleri][Data Types], [tablo dağıtma][Distribute], [bir tablodizinoluşturma] [ Index] ve [bir tablo bölümleme][Partition].</span><span class="sxs-lookup"><span data-stu-id="0b660-132">toolearn more, see hello articles on [Table Data Types][Data Types], [Distributing a Table][Distribute], [Indexing a Table][Index] and  [Partitioning a Table][Partition].</span></span>

## <a name="table-statistics"></a><span data-ttu-id="0b660-133">Tablo istatistikleri</span><span class="sxs-lookup"><span data-stu-id="0b660-133">Table statistics</span></span>
<span data-ttu-id="0b660-134">SQL veri ambarı dışında bir son derece önemli toogetting hello en iyi performans istatistikleri şunlardır.</span><span class="sxs-lookup"><span data-stu-id="0b660-134">Statistics are an extremely important toogetting hello best performance out of your SQL Data Warehouse.</span></span>  <span data-ttu-id="0b660-135">SQL veri ambarı değil henüz otomatik oluşturma ve güncelleştirme istatistikleri sizin için Azure SQL veritabanında tooexpect gelebilir gibi beri bizim makale üzerinde okuma [istatistikleri] [ Statistics] hello biri olabilir en önemli makaleleri tooensure okuyun, sorgularından hello en iyi performansı elde.</span><span class="sxs-lookup"><span data-stu-id="0b660-135">Since SQL Data Warehouse does not yet automatically create and update statistics for you, like you may have come tooexpect in Azure SQL Database, reading our article on [Statistics][Statistics] might be one of hello most important articles you read tooensure that you get hello best performance from your queries.</span></span>

## <a name="temporary-tables"></a><span data-ttu-id="0b660-136">Geçici tablolar</span><span class="sxs-lookup"><span data-stu-id="0b660-136">Temporary tables</span></span>
<span data-ttu-id="0b660-137">Geçici tablolar yalnızca oturum açma işleminiz hello süresince var ve diğer kullanıcılar tarafından görülemeyen tablolardır.</span><span class="sxs-lookup"><span data-stu-id="0b660-137">Temporary tables are tables which only exist for hello duration of your logon and cannot be seen by other users.</span></span>  <span data-ttu-id="0b660-138">Geçici tablolara en iyi yolu tooprevent başkalarının geçici sonuçları görmesini olması ve ayrıca temizleme hello gereksinimini azaltır.</span><span class="sxs-lookup"><span data-stu-id="0b660-138">Temporary tables can be a good way tooprevent others from seeing temporary results and also reduce hello need for cleanup.</span></span>  <span data-ttu-id="0b660-139">Geçici tablolara ayrıca yerel depolama alanını olduğundan, bunlar bazı işlemler için daha hızlı performans sunabilir.</span><span class="sxs-lookup"><span data-stu-id="0b660-139">Since temporary tables also utilize local storage, they can offer faster performance for some operations.</span></span>  <span data-ttu-id="0b660-140">Merhaba bkz [geçici tablo] [ Temporary] makaleleri geçici tabloları hakkında daha fazla ayrıntı için.</span><span class="sxs-lookup"><span data-stu-id="0b660-140">See hello [Temporary Table][Temporary] articles for more details about temporary tables.</span></span>

## <a name="external-tables"></a><span data-ttu-id="0b660-141">Dış tablolar</span><span class="sxs-lookup"><span data-stu-id="0b660-141">External tables</span></span>
<span data-ttu-id="0b660-142">Dış tablolar, Polybase tablolar olarak da bilinen SQL Data Warehouse, ancak noktası toodata dış SQL veri ambarından sorgulanan tabloların değildir.</span><span class="sxs-lookup"><span data-stu-id="0b660-142">External tables, also known as Polybase tables, are tables which can be queried from SQL Data Warehouse, but point toodata external from SQL Data Warehouse.</span></span>  <span data-ttu-id="0b660-143">Örneğin, bir dış tablo hangi noktaları toofiles Azure Blob Storage oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0b660-143">For example, you can create an external table which points toofiles on Azure Blob Storage.</span></span>  <span data-ttu-id="0b660-144">Toocreate ve sorgu bir dış tablo nasıl görürüm hakkında daha fazla ayrıntı için [Polybase ile veri yükleme][Load data with Polybase].</span><span class="sxs-lookup"><span data-stu-id="0b660-144">For more details on how toocreate and query an external table, see [Load data with Polybase][Load data with Polybase].</span></span>  

## <a name="unsupported-table-features"></a><span data-ttu-id="0b660-145">Desteklenmeyen tablo özellikleri</span><span class="sxs-lookup"><span data-stu-id="0b660-145">Unsupported table features</span></span>
<span data-ttu-id="0b660-146">SQL Data Warehouse aynı tablo özellikleri diğer veritabanı tarafından sunulan hello çoğunu içerirken, henüz desteklenmeyen bazı özellikler vardır.</span><span class="sxs-lookup"><span data-stu-id="0b660-146">While SQL Data Warehouse contains many of hello same table features offered by other databases, there are some features which are not yet supported.</span></span>  <span data-ttu-id="0b660-147">Aşağıda bazı hello henüz desteklenmeyen tablo özellikler listelenmiştir.</span><span class="sxs-lookup"><span data-stu-id="0b660-147">Below is a list of some of hello table features which are not yet supported.</span></span>

| <span data-ttu-id="0b660-148">Desteklenmeyen özellikler</span><span class="sxs-lookup"><span data-stu-id="0b660-148">Unsupported features</span></span> |
| --- |
| <span data-ttu-id="0b660-149">Birincil anahtar, yabancı anahtarları, benzersiz ve onay [Tablo sınırlamaları][Table Constraints]</span><span class="sxs-lookup"><span data-stu-id="0b660-149">Primary key, Foreign keys, Unique and Check [Table Constraints][Table Constraints]</span></span> |
| <span data-ttu-id="0b660-150">[Benzersiz dizinler][Unique Indexes]</span><span class="sxs-lookup"><span data-stu-id="0b660-150">[Unique Indexes][Unique Indexes]</span></span> |
| <span data-ttu-id="0b660-151">[Hesaplanan sütunlar][Computed Columns]</span><span class="sxs-lookup"><span data-stu-id="0b660-151">[Computed Columns][Computed Columns]</span></span> |
| <span data-ttu-id="0b660-152">[Seyrek sütun][Sparse Columns]</span><span class="sxs-lookup"><span data-stu-id="0b660-152">[Sparse Columns][Sparse Columns]</span></span> |
| <span data-ttu-id="0b660-153">[Kullanıcı tanımlı türler][User-Defined Types]</span><span class="sxs-lookup"><span data-stu-id="0b660-153">[User-Defined Types][User-Defined Types]</span></span> |
| <span data-ttu-id="0b660-154">[Sırası][Sequence]</span><span class="sxs-lookup"><span data-stu-id="0b660-154">[Sequence][Sequence]</span></span> |
| <span data-ttu-id="0b660-155">[Tetikleyicileri][Triggers]</span><span class="sxs-lookup"><span data-stu-id="0b660-155">[Triggers][Triggers]</span></span> |
| <span data-ttu-id="0b660-156">[Dizin oluşturulmuş görünümler][Indexed Views]</span><span class="sxs-lookup"><span data-stu-id="0b660-156">[Indexed Views][Indexed Views]</span></span> |
| <span data-ttu-id="0b660-157">[Eş anlamlıları][Synonyms]</span><span class="sxs-lookup"><span data-stu-id="0b660-157">[Synonyms][Synonyms]</span></span> |

## <a name="table-size-queries"></a><span data-ttu-id="0b660-158">Tablo boyutu sorguları</span><span class="sxs-lookup"><span data-stu-id="0b660-158">Table size queries</span></span>
<span data-ttu-id="0b660-159">Bir basit yol tooidentify alanı hello 60 dağıtımları, her bir tablo tarafından tüketilen satırları ise toouse [DBCC PDW_SHOWSPACEUSED][DBCC PDW_SHOWSPACEUSED].</span><span class="sxs-lookup"><span data-stu-id="0b660-159">One simple way tooidentify space and rows consumed by a table in each of hello 60 distributions, is toouse [DBCC PDW_SHOWSPACEUSED][DBCC PDW_SHOWSPACEUSED].</span></span>

```sql
DBCC PDW_SHOWSPACEUSED('dbo.FactInternetSales');
```

<span data-ttu-id="0b660-160">Ancak, DBCC komutlarını kullanarak oldukça sınırlama.</span><span class="sxs-lookup"><span data-stu-id="0b660-160">However, using DBCC commands can be quite limiting.</span></span>  <span data-ttu-id="0b660-161">Dinamik Yönetim görünümlerini (Dmv'leri) etmenizi sağlar toosee çok daha ayrıntılı yanı sıra hello sorgu sonuçları üzerinde çok daha fazla denetim sağlar.</span><span class="sxs-lookup"><span data-stu-id="0b660-161">Dynamic management views (DMVs) will allow you toosee much more detail as well as give you much greater control over hello query results.</span></span>  <span data-ttu-id="0b660-162">Bu görünüm başvurulan tooby olacaktır pek çok örnekte bu ve diğer makaleler oluşturarak başlayın.</span><span class="sxs-lookup"><span data-stu-id="0b660-162">Start by creating this view, which will be referred tooby many of our examples in this and other articles.</span></span>

```sql
CREATE VIEW dbo.vTableSizes
AS
WITH base
AS
(
SELECT 
 GETDATE()                                                             AS  [execution_time]
, DB_NAME()                                                            AS  [database_name]
, s.name                                                               AS  [schema_name]
, t.name                                                               AS  [table_name]
, QUOTENAME(s.name)+'.'+QUOTENAME(t.name)                              AS  [two_part_name]
, nt.[name]                                                            AS  [node_table_name]
, ROW_NUMBER() OVER(PARTITION BY nt.[name] ORDER BY (SELECT NULL))     AS  [node_table_name_seq]
, tp.[distribution_policy_desc]                                        AS  [distribution_policy_name]
, c.[name]                                                             AS  [distribution_column]
, nt.[distribution_id]                                                 AS  [distribution_id]
, i.[type]                                                             AS  [index_type]
, i.[type_desc]                                                        AS  [index_type_desc]
, nt.[pdw_node_id]                                                     AS  [pdw_node_id]
, pn.[type]                                                            AS  [pdw_node_type]
, pn.[name]                                                            AS  [pdw_node_name]
, di.name                                                              AS  [dist_name]
, di.position                                                          AS  [dist_position]
, nps.[partition_number]                                               AS  [partition_nmbr]
, nps.[reserved_page_count]                                            AS  [reserved_space_page_count]
, nps.[reserved_page_count] - nps.[used_page_count]                    AS  [unused_space_page_count]
, nps.[in_row_data_page_count] 
    + nps.[row_overflow_used_page_count] 
    + nps.[lob_used_page_count]                                        AS  [data_space_page_count]
, nps.[reserved_page_count] 
 - (nps.[reserved_page_count] - nps.[used_page_count]) 
 - ([in_row_data_page_count] 
         + [row_overflow_used_page_count]+[lob_used_page_count])       AS  [index_space_page_count]
, nps.[row_count]                                                      AS  [row_count]
from 
    sys.schemas s
INNER JOIN sys.tables t
    ON s.[schema_id] = t.[schema_id]
INNER JOIN sys.indexes i
    ON  t.[object_id] = i.[object_id]
    AND i.[index_id] <= 1
INNER JOIN sys.pdw_table_distribution_properties tp
    ON t.[object_id] = tp.[object_id]
INNER JOIN sys.pdw_table_mappings tm
    ON t.[object_id] = tm.[object_id]
INNER JOIN sys.pdw_nodes_tables nt
    ON tm.[physical_name] = nt.[name]
INNER JOIN sys.dm_pdw_nodes pn
    ON  nt.[pdw_node_id] = pn.[pdw_node_id]
INNER JOIN sys.pdw_distributions di
    ON  nt.[distribution_id] = di.[distribution_id]
INNER JOIN sys.dm_pdw_nodes_db_partition_stats nps
    ON nt.[object_id] = nps.[object_id]
    AND nt.[pdw_node_id] = nps.[pdw_node_id]
    AND nt.[distribution_id] = nps.[distribution_id]
LEFT OUTER JOIN (select * from sys.pdw_column_distribution_properties where distribution_ordinal = 1) cdp
    ON t.[object_id] = cdp.[object_id]
LEFT OUTER JOIN sys.columns c
    ON cdp.[object_id] = c.[object_id]
    AND cdp.[column_id] = c.[column_id]
)
, size
AS
(
SELECT
   [execution_time]
,  [database_name]
,  [schema_name]
,  [table_name]
,  [two_part_name]
,  [node_table_name]
,  [node_table_name_seq]
,  [distribution_policy_name]
,  [distribution_column]
,  [distribution_id]
,  [index_type]
,  [index_type_desc]
,  [pdw_node_id]
,  [pdw_node_type]
,  [pdw_node_name]
,  [dist_name]
,  [dist_position]
,  [partition_nmbr]
,  [reserved_space_page_count]
,  [unused_space_page_count]
,  [data_space_page_count]
,  [index_space_page_count]
,  [row_count]
,  ([reserved_space_page_count] * 8.0)                                 AS [reserved_space_KB]
,  ([reserved_space_page_count] * 8.0)/1000                            AS [reserved_space_MB]
,  ([reserved_space_page_count] * 8.0)/1000000                         AS [reserved_space_GB]
,  ([reserved_space_page_count] * 8.0)/1000000000                      AS [reserved_space_TB]
,  ([unused_space_page_count]   * 8.0)                                 AS [unused_space_KB]
,  ([unused_space_page_count]   * 8.0)/1000                            AS [unused_space_MB]
,  ([unused_space_page_count]   * 8.0)/1000000                         AS [unused_space_GB]
,  ([unused_space_page_count]   * 8.0)/1000000000                      AS [unused_space_TB]
,  ([data_space_page_count]     * 8.0)                                 AS [data_space_KB]
,  ([data_space_page_count]     * 8.0)/1000                            AS [data_space_MB]
,  ([data_space_page_count]     * 8.0)/1000000                         AS [data_space_GB]
,  ([data_space_page_count]     * 8.0)/1000000000                      AS [data_space_TB]
,  ([index_space_page_count]  * 8.0)                                   AS [index_space_KB]
,  ([index_space_page_count]  * 8.0)/1000                              AS [index_space_MB]
,  ([index_space_page_count]  * 8.0)/1000000                           AS [index_space_GB]
,  ([index_space_page_count]  * 8.0)/1000000000                        AS [index_space_TB]
FROM base
)
SELECT * 
FROM size
;
```

### <a name="table-space-summary"></a><span data-ttu-id="0b660-163">Özet Tablo alanı</span><span class="sxs-lookup"><span data-stu-id="0b660-163">Table space summary</span></span>
<span data-ttu-id="0b660-164">Bu sorgu, tablo tarafından hello satır ve alan döndürür.</span><span class="sxs-lookup"><span data-stu-id="0b660-164">This query returns hello rows and space by table.</span></span>  <span data-ttu-id="0b660-165">En büyük tabloları ve hepsini, çoğaltılmış veya dağıtılmış karma olup olmadıkları hangi tablolardır harika sorgu toosee olur.</span><span class="sxs-lookup"><span data-stu-id="0b660-165">It is a great query toosee which tables are your largest tables and whether they are round robin, replicated or hash distributed.</span></span>  <span data-ttu-id="0b660-166">Dağıtılmış karma tablolar için hello dağıtım sütun da gösterir.</span><span class="sxs-lookup"><span data-stu-id="0b660-166">For hash distributed tables it also shows hello distribution column.</span></span>  <span data-ttu-id="0b660-167">Çoğu durumda, en büyük tabloları karma bir kümelenmiş columnstore dizini ile dağıtılmış olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="0b660-167">In most cases your largest tables should be hash distributed with a clustered columnstore index.</span></span>

```sql
SELECT 
     database_name
,    schema_name
,    table_name
,    distribution_policy_name
,      distribution_column
,    index_type_desc
,    COUNT(distinct partition_nmbr) as nbr_partitions
,    SUM(row_count)                 as table_row_count
,    SUM(reserved_space_GB)         as table_reserved_space_GB
,    SUM(data_space_GB)             as table_data_space_GB
,    SUM(index_space_GB)            as table_index_space_GB
,    SUM(unused_space_GB)           as table_unused_space_GB
FROM 
    dbo.vTableSizes
GROUP BY 
     database_name
,    schema_name
,    table_name
,    distribution_policy_name
,      distribution_column
,    index_type_desc
ORDER BY
    table_reserved_space_GB desc
;
```

### <a name="table-space-by-distribution-type"></a><span data-ttu-id="0b660-168">Dağıtım türüne göre tablo alanı</span><span class="sxs-lookup"><span data-stu-id="0b660-168">Table space by distribution type</span></span>
```sql
SELECT 
     distribution_policy_name
,    SUM(row_count)                as table_type_row_count
,    SUM(reserved_space_GB)        as table_type_reserved_space_GB
,    SUM(data_space_GB)            as table_type_data_space_GB
,    SUM(index_space_GB)           as table_type_index_space_GB
,    SUM(unused_space_GB)          as table_type_unused_space_GB
FROM dbo.vTableSizes
GROUP BY distribution_policy_name
;
```

### <a name="table-space-by-index-type"></a><span data-ttu-id="0b660-169">Dizin türü tablo boşluk</span><span class="sxs-lookup"><span data-stu-id="0b660-169">Table space by index type</span></span>
```sql
SELECT 
     index_type_desc
,    SUM(row_count)                as table_type_row_count
,    SUM(reserved_space_GB)        as table_type_reserved_space_GB
,    SUM(data_space_GB)            as table_type_data_space_GB
,    SUM(index_space_GB)           as table_type_index_space_GB
,    SUM(unused_space_GB)          as table_type_unused_space_GB
FROM dbo.vTableSizes
GROUP BY index_type_desc
;
```

### <a name="distribution-space-summary"></a><span data-ttu-id="0b660-170">Dağıtım alanı özeti</span><span class="sxs-lookup"><span data-stu-id="0b660-170">Distribution space summary</span></span>
```sql
SELECT 
    distribution_id
,    SUM(row_count)                as total_node_distribution_row_count
,    SUM(reserved_space_MB)        as total_node_distribution_reserved_space_MB
,    SUM(data_space_MB)            as total_node_distribution_data_space_MB
,    SUM(index_space_MB)           as total_node_distribution_index_space_MB
,    SUM(unused_space_MB)          as total_node_distribution_unused_space_MB
FROM dbo.vTableSizes
GROUP BY     distribution_id
ORDER BY    distribution_id
;
```

## <a name="next-steps"></a><span data-ttu-id="0b660-171">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="0b660-171">Next steps</span></span>
<span data-ttu-id="0b660-172">toolearn daha hello makalelere bakın üzerinde [tablo veri türleri][Data Types], [tablo dağıtma][Distribute], [bir tablodizinoluşturma] [ Index], [Bir tablo bölümleme][Partition], [tablo istatistikleri koruma] [ Statistics] ve [ Geçici tablolara][Temporary].</span><span class="sxs-lookup"><span data-stu-id="0b660-172">toolearn more, see hello articles on [Table Data Types][Data Types], [Distributing a Table][Distribute], [Indexing a Table][Index],  [Partitioning a Table][Partition], [Maintaining Table Statistics][Statistics] and [Temporary Tables][Temporary].</span></span>  <span data-ttu-id="0b660-173">En iyi uygulamalar hakkında daha fazla bilgi için bkz: [SQL veri ambarı en iyi uygulamalar][SQL Data Warehouse Best Practices].</span><span class="sxs-lookup"><span data-stu-id="0b660-173">For more about best practices, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>

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
[Load data with Polybase]: ./sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md

<!--MSDN references-->
[CREATE TABLE]: https://msdn.microsoft.com/library/mt203953.aspx
[RENAME]: https://msdn.microsoft.com/library/mt631611.aspx
[DBCC PDW_SHOWSPACEUSED]: https://msdn.microsoft.com/library/mt204028.aspx
[Table Constraints]: https://msdn.microsoft.com/library/ms188066.aspx
[Computed Columns]: https://msdn.microsoft.com/library/ms186241.aspx
[Sparse Columns]: https://msdn.microsoft.com/library/cc280604.aspx
[User-Defined Types]: https://msdn.microsoft.com/library/ms131694.aspx
[Sequence]: https://msdn.microsoft.com/library/ff878091.aspx
[Triggers]: https://msdn.microsoft.com/library/ms189799.aspx
[Indexed Views]: https://msdn.microsoft.com/library/ms191432.aspx
[Synonyms]: https://msdn.microsoft.com/library/ms177544.aspx
[Unique Indexes]: https://msdn.microsoft.com/library/ms188783.aspx

<!--Other Web references-->
