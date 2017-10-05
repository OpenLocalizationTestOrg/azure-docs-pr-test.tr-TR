---
title: "Azure SQL columnstore dizini performansını artırmak | Microsoft Docs"
description: "Bellek gereksinimlerini azaltın veya her satır grubu kimliğinde bir columnstore dizini sıkıştırır satırların sayısı en üst düzeye çıkarmak için kullanılabilir bellek artırın."
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: jhubbard
editor: 
ms.assetid: ef170f39-ae24-4b04-af76-53bb4c4d16d3
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: performance
ms.date: 6/2/2017
ms.author: shigu;barbkess
ms.openlocfilehash: f0e0b839b4a0c216eee2eb5134d43b91d8f83289
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="maximizing-rowgroup-quality-for-columnstore"></a><span data-ttu-id="cc069-103">Satır grubu kimliğinde kalitesi columnstore için en üst düzeye çıkarma</span><span class="sxs-lookup"><span data-stu-id="cc069-103">Maximizing rowgroup quality for columnstore</span></span>

<span data-ttu-id="cc069-104">Satır grubu kimliğinde kalite bir satır grubu kimliğinde satır sayısı tarafından belirlenir.</span><span class="sxs-lookup"><span data-stu-id="cc069-104">Rowgroup quality is determined by the number of rows in a rowgroup.</span></span> <span data-ttu-id="cc069-105">Bellek gereksinimlerini azaltın veya her satır grubu kimliğinde bir columnstore dizini sıkıştırır satırların sayısı en üst düzeye çıkarmak için kullanılabilir bellek artırın.</span><span class="sxs-lookup"><span data-stu-id="cc069-105">Reduce memory requirements or increase the available memory to maximize the number of rows a columnstore index compresses into each rowgroup.</span></span>  <span data-ttu-id="cc069-106">Sıkıştırma oranları artırmak ve performans columnstore dizinleri için sorgulamak için bu yöntemleri kullanın.</span><span class="sxs-lookup"><span data-stu-id="cc069-106">Use these methods to improve compression rates and query performance for columnstore indexes.</span></span>

## <a name="why-the-rowgroup-size-matters"></a><span data-ttu-id="cc069-107">Satır grubu kimliğinde boyutu neden önemlidir?</span><span class="sxs-lookup"><span data-stu-id="cc069-107">Why the rowgroup size matters</span></span>
<span data-ttu-id="cc069-108">Tek tek rowgroups sütun kesimleri tarayarak bir tabloda bir columnstore dizini tarar olduğundan, her satır grubu kimliğinde satır sayısı en üst düzeye çıkarma sorgu performansını geliştirir.</span><span class="sxs-lookup"><span data-stu-id="cc069-108">Since a columnstore index scans a table by scanning column segments of individual rowgroups, maximizing the number of rows in each rowgroup enhances query performance.</span></span> <span data-ttu-id="cc069-109">Çok sayıda satır RowGroups sahip olduğunuzda, veri sıkıştırma diskten okumak için daha az veri olmadığı anlamına gelir artırır.</span><span class="sxs-lookup"><span data-stu-id="cc069-109">When rowgroups have a high number of rows, data compression improves which means there is less data to read from disk.</span></span>

<span data-ttu-id="cc069-110">Rowgroups hakkında daha fazla bilgi için bkz: [Columnstore dizinleri Kılavuzu](https://msdn.microsoft.com/library/gg492088.aspx).</span><span class="sxs-lookup"><span data-stu-id="cc069-110">For more information about rowgroups, see [Columnstore Indexes Guide](https://msdn.microsoft.com/library/gg492088.aspx).</span></span>

## <a name="target-size-for-rowgroups"></a><span data-ttu-id="cc069-111">Rowgroups ilişkin hedef boyutu</span><span class="sxs-lookup"><span data-stu-id="cc069-111">Target size for rowgroups</span></span>
<span data-ttu-id="cc069-112">En iyi sorgu performansını satır grubu kimliğinde bir columnstore dizininde başına satır sayısı en üst düzeye çıkarmak için belirtilir.</span><span class="sxs-lookup"><span data-stu-id="cc069-112">For best query performance, the goal is to maximize the number of rows per rowgroup in a columnstore index.</span></span> <span data-ttu-id="cc069-113">Bir satır grubu kimliğinde 1.048.576 satır en olabilir.</span><span class="sxs-lookup"><span data-stu-id="cc069-113">A rowgroup can have a maximum of 1,048,576 rows.</span></span> <span data-ttu-id="cc069-114">Satır grubu başına satır sayısının üst sınırını olmaması uygundur.</span><span class="sxs-lookup"><span data-stu-id="cc069-114">It's okay to not have the maximum number of rows per rowgroup.</span></span> <span data-ttu-id="cc069-115">Columnstore dizinleri RowGroups 100. 000'en az satır olduğunda iyi performans elde etmek.</span><span class="sxs-lookup"><span data-stu-id="cc069-115">Columnstore indexes achieve good performance when rowgroups have at least 100,000 rows.</span></span>

## <a name="rowgroups-can-get-trimmed-during-compression"></a><span data-ttu-id="cc069-116">Sıkıştırma sırasında RowGroups kırpılmış</span><span class="sxs-lookup"><span data-stu-id="cc069-116">Rowgroups can get trimmed during compression</span></span>

<span data-ttu-id="cc069-117">Bir toplu yükleme veya columnstore dizini yeniden oluşturma sırasında bazen yeterli bellek yok her satır grubu için belirlenen tüm satırları sıkıştırmak kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="cc069-117">During a bulk load or columnstore index rebuild, sometimes there isn't enough memory available to compress all the rows designated for each rowgroup.</span></span> <span data-ttu-id="cc069-118">Bellek baskısı olduğunda sıkıştırma columnstore içine başarılı şekilde columnstore dizinleri satır grubu kimliğinde boyutları kesim.</span><span class="sxs-lookup"><span data-stu-id="cc069-118">When there is memory pressure, columnstore indexes trim the rowgroup sizes so compression into the columnstore can succeed.</span></span> 

<span data-ttu-id="cc069-119">Her satır grubu 10. 000'en az satır sıkıştırmak için bellek yetersiz olduğunda, SQL Data Warehouse bir hata oluşturur.</span><span class="sxs-lookup"><span data-stu-id="cc069-119">When there is insufficient memory to compress at least 10,000 rows into each rowgroup, SQL Data Warehouse generates an error.</span></span>

<span data-ttu-id="cc069-120">Toplu yükleme hakkında daha fazla bilgi için bkz: [toplu yükleme kümelenmiş columnstore dizinine](https://msdn.microsoft.com/en-us/library/dn935008.aspx#Bulk load into a clustered columnstore index).</span><span class="sxs-lookup"><span data-stu-id="cc069-120">For more information on bulk loading, see [Bulk load into a clustered columnstore index](https://msdn.microsoft.com/en-us/library/dn935008.aspx#Bulk load into a clustered columnstore index).</span></span>

## <a name="how-to-monitor-rowgroup-quality"></a><span data-ttu-id="cc069-121">Satır grubu kimliğinde kalitesini izleme</span><span class="sxs-lookup"><span data-stu-id="cc069-121">How to monitor rowgroup quality</span></span>

<span data-ttu-id="cc069-122">Rowgroups ve orada kırpma, kırpma nedenini satır sayısı gibi yararlı bilgileri sunan bir DMV (sys.dm_pdw_nodes_db_column_store_row_group_physical_stats) yoktur.</span><span class="sxs-lookup"><span data-stu-id="cc069-122">There is a DMV (sys.dm_pdw_nodes_db_column_store_row_group_physical_stats) that exposes useful information such as number of rows in rowgroups and the reason for trimming if there was trimming.</span></span> <span data-ttu-id="cc069-123">Satır grubu kimliğinde kırpma hakkında bilgi almak için bu DMV sorgusu için kullanışlı bir yöntem olarak, aşağıdaki görünümü oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cc069-123">You can create the following view as a handy way to query this DMV to get information on rowgroup trimming.</span></span>

```sql
create view dbo.vCS_rg_physical_stats
as 
with cte
as
(
select   tb.[name]                    AS [logical_table_name]
,        rg.[row_group_id]            AS [row_group_id]
,        rg.[state]                   AS [state]
,        rg.[state_desc]              AS [state_desc]
,        rg.[total_rows]              AS [total_rows]
,        rg.[trim_reason_desc]        AS trim_reason_desc
,        mp.[physical_name]           AS physical_name
FROM    sys.[schemas] sm
JOIN    sys.[tables] tb               ON  sm.[schema_id]          = tb.[schema_id]                             
JOIN    sys.[pdw_table_mappings] mp   ON  tb.[object_id]          = mp.[object_id]
JOIN    sys.[pdw_nodes_tables] nt     ON  nt.[name]               = mp.[physical_name]
JOIN    sys.[dm_pdw_nodes_db_column_store_row_group_physical_stats] rg      ON  rg.[object_id]     = nt.[object_id]
                                                                            AND rg.[pdw_node_id]   = nt.[pdw_node_id]
                                        AND rg.[distribution_id]    = nt.[distribution_id]                                          
)
select *
from cte;
```

<span data-ttu-id="cc069-124">Trim_reason_desc satır grubu kimliğinde aynı olup olmadığını bildirir (trim_reason_desc = NO_TRIM hiçbir kırpma vardı ve satır grubu en iyi kalitesini olduğu anlamına gelir).</span><span class="sxs-lookup"><span data-stu-id="cc069-124">The trim_reason_desc tells whether the rowgroup was trimmed(trim_reason_desc = NO_TRIM implies there was no trimming and row group is of optimal quality).</span></span> <span data-ttu-id="cc069-125">Kırpma şunlardan satır grubu kimliğinde erken kırpılacağını belirtin:</span><span class="sxs-lookup"><span data-stu-id="cc069-125">The following trim reasons indicate premature trimming of the rowgroup:</span></span>
- <span data-ttu-id="cc069-126">BULKLOAD: gelen toplu iş yükü için satır 1 milyondan az satır varken bu kırpma neden kullanılır.</span><span class="sxs-lookup"><span data-stu-id="cc069-126">BULKLOAD: This trim reason is used when the incoming batch of rows for the load had less than 1 million rows.</span></span> <span data-ttu-id="cc069-127">Altyapısı varsa (delta deposuna ekleme aksine) eklenmekte 100.000 satırları büyük sıkıştırılmış satır grupları oluşturur, ancak kırpma neden BULKLOAD için ayarlar.</span><span class="sxs-lookup"><span data-stu-id="cc069-127">The engine will create compressed row groups if there are greater than 100,000 rows being inserted (as opposed to inserting into the delta store) but sets the trim reason to BULKLOAD.</span></span> <span data-ttu-id="cc069-128">Bu senaryoda, daha fazla satır birikmesine toplu iş yükü pencerenizi artırmayı düşünün.</span><span class="sxs-lookup"><span data-stu-id="cc069-128">In this scenario, consider increasing your batch load window to accumulate more rows.</span></span> <span data-ttu-id="cc069-129">Ayrıca, satır gruplarından bölüm sınırları yayılamaz gibi çok parçalı olmadığından emin olmak için bölümleme düzeni yeniden.</span><span class="sxs-lookup"><span data-stu-id="cc069-129">Also, reevaluate your partitioning scheme to ensure it is not too granular as row groups cannot span partition boundaries.</span></span>
- <span data-ttu-id="cc069-130">MEMORY_LIMITATION: 1 milyon satır satır grupları oluşturmak için belirli bir çalışma bellek miktarını altyapısı tarafından gereklidir.</span><span class="sxs-lookup"><span data-stu-id="cc069-130">MEMORY_LIMITATION: To create row groups with 1 million rows, a certain amount of working memory is required by the engine.</span></span> <span data-ttu-id="cc069-131">Kullanılabilir bellek yükleme oturumunun gerekli çalışma belleğinden daha az olduğunda, satır grupları erken kırpılmış.</span><span class="sxs-lookup"><span data-stu-id="cc069-131">When available memory of the loading session is less than the required working memory, row groups get prematurely trimmed.</span></span> <span data-ttu-id="cc069-132">Aşağıdaki bölümlerde, gerekli bellek tahmin etmek ve daha fazla bellek ayırmak açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="cc069-132">The following sections explain how to estimate memory required and allocate more memory.</span></span>
- <span data-ttu-id="cc069-133">DICTIONARY_SIZE: Kırpma bu nedenle, geniş ve/veya yüksek nicelik dizeleri içeren en az bir dize sütunu olduğundan satır grubu kimliğinde kırpma oluştuğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="cc069-133">DICTIONARY_SIZE: This trim reason indicates that rowgroup trimming occurred because there was at least one string column with wide and/or high cardinality strings.</span></span> <span data-ttu-id="cc069-134">Sözlük boyutu 16 MB bellek sınırlıdır ve satır grubu bu sınıra ulaşıldığında sıkıştırılmış.</span><span class="sxs-lookup"><span data-stu-id="cc069-134">The dictionary size is limited to 16 MB in memory and once this limit is reached the row group is compressed.</span></span> <span data-ttu-id="cc069-135">Bu durumla karşılaşırsanız, sorunlu sütun ayrı bir tabloya izole etmeyi düşünün.</span><span class="sxs-lookup"><span data-stu-id="cc069-135">If you do run into this situation, consider isolating the problematic column into a separate table.</span></span>

## <a name="how-to-estimate-memory-requirements"></a><span data-ttu-id="cc069-136">Bellek gereksinimlerini tahmin etme</span><span class="sxs-lookup"><span data-stu-id="cc069-136">How to estimate memory requirements</span></span>

<!--
To view an estimate of the memory requirements to compress a rowgroup of maximum size into a columnstore index, download and run the view [dbo.vCS_mon_mem_grant](). This view shows the size of the memory grant that a rowgroup requires for compression in to the columnstore.
-->

<span data-ttu-id="cc069-137">Bir satır grubu kimliğinde sıkıştırmak için gereken en fazla bellek yaklaşık olarak şöyledir</span><span class="sxs-lookup"><span data-stu-id="cc069-137">The maximum required memory to compress one rowgroup is approximately</span></span>

- <span data-ttu-id="cc069-138">72 MB +</span><span class="sxs-lookup"><span data-stu-id="cc069-138">72 MB +</span></span>
- <span data-ttu-id="cc069-139">\#Satır \* \#sütunları \* 8 bayt +</span><span class="sxs-lookup"><span data-stu-id="cc069-139">\#rows \* \#columns \* 8 bytes +</span></span>
- <span data-ttu-id="cc069-140">\#Satır \* \#kısa dize sütunlarındaki \* 32 bayt +</span><span class="sxs-lookup"><span data-stu-id="cc069-140">\#rows \* \#short-string-columns \* 32 bytes +</span></span>
- <span data-ttu-id="cc069-141">\#uzun dize sütunlarındaki \* sıkıştırma sözlüğü için 16 MB</span><span class="sxs-lookup"><span data-stu-id="cc069-141">\#long-string-columns \* 16 MB for compression dictionary</span></span>

<span data-ttu-id="cc069-142">Burada kısa dize sütunlarındaki dize veri türlerini kullanın < = 32 bayt ve > 32 bayt dizesi veri türlerini uzun dize sütunlarındaki kullanın.</span><span class="sxs-lookup"><span data-stu-id="cc069-142">where short-string-columns use string data types of <= 32 bytes and long-string-columns use string data types of > 32 bytes.</span></span>

<span data-ttu-id="cc069-143">Uzun dizeleri metin sıkıştırma için tasarlanmış bir sıkıştırma yöntemi ile sıkıştırılır.</span><span class="sxs-lookup"><span data-stu-id="cc069-143">Long strings are compressed with a compression method designed for compressing text.</span></span> <span data-ttu-id="cc069-144">Bu bir sıkıştırma yöntemi kullanan bir *sözlük* metin kalıplarını depolamak için.</span><span class="sxs-lookup"><span data-stu-id="cc069-144">This compression method uses a *dictionary* to store text patterns.</span></span> <span data-ttu-id="cc069-145">Bir sözlük maksimum boyutu 16 MB'tır.</span><span class="sxs-lookup"><span data-stu-id="cc069-145">The maximum size of a dictionary is 16 MB.</span></span> <span data-ttu-id="cc069-146">Satır grubu kimliğinde her uzun bir dize sütunu için yalnızca bir sözlük yoktur.</span><span class="sxs-lookup"><span data-stu-id="cc069-146">There is only one dictionary for each long string column in the rowgroup.</span></span>

<span data-ttu-id="cc069-147">Video columnstore bellek gereksinimlerini kapsamlı bir açıklama için bkz [Azure SQL Data Warehouse ölçeklendirme: yapılandırma ve Kılavuzu](https://myignite.microsoft.com/videos/14822).</span><span class="sxs-lookup"><span data-stu-id="cc069-147">For an in-depth discussion of columnstore memory requirements, see the video [Azure SQL Data Warehouse scaling: configuration and guidance](https://myignite.microsoft.com/videos/14822).</span></span>

## <a name="ways-to-reduce-memory-requirements"></a><span data-ttu-id="cc069-148">Bellek gereksinimlerini azaltmak için yollar</span><span class="sxs-lookup"><span data-stu-id="cc069-148">Ways to reduce memory requirements</span></span>

<span data-ttu-id="cc069-149">Columnstore dizinleri rowgroups sıkıştırma için bellek gereksinimlerini azaltmak için aşağıdaki tekniklerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="cc069-149">Use the following techniques to reduce the memory requirements for compressing rowgroups into columnstore indexes.</span></span>

### <a name="use-fewer-columns"></a><span data-ttu-id="cc069-150">Daha az sütun kullanın</span><span class="sxs-lookup"><span data-stu-id="cc069-150">Use fewer columns</span></span>
<span data-ttu-id="cc069-151">Mümkünse, daha az sütun içeren tablo tasarlayın.</span><span class="sxs-lookup"><span data-stu-id="cc069-151">If possible, design the table with fewer columns.</span></span> <span data-ttu-id="cc069-152">Columnstore dizinini bir satır grubu kimliğinde columnstore sıkıştırılmış olduğunda, her bir sütun segmenti ayrı olarak sıkıştırır.</span><span class="sxs-lookup"><span data-stu-id="cc069-152">When a rowgroup is compressed into the columnstore, the columnstore index compresses each column segment separately.</span></span> <span data-ttu-id="cc069-153">Bu nedenle bir satır grubu kimliğinde sıkıştırmak için bellek gereksinimleri sütunları artar artırın.</span><span class="sxs-lookup"><span data-stu-id="cc069-153">Therefore the memory requirements to compress a rowgroup increase as the number of columns increases.</span></span>


### <a name="use-fewer-string-columns"></a><span data-ttu-id="cc069-154">Daha az dize sütun kullanın</span><span class="sxs-lookup"><span data-stu-id="cc069-154">Use fewer string columns</span></span>
<span data-ttu-id="cc069-155">Dize veri türleri sütunlarının daha fazla bellek sayısal ve tarih veri türü gerektirir.</span><span class="sxs-lookup"><span data-stu-id="cc069-155">Columns of string data types require more memory than numeric and date data types.</span></span> <span data-ttu-id="cc069-156">Bellek gereksinimlerini azaltmak için dize sütunlarındaki olgu tablolarından kaldırarak ve daha küçük boyut tabloları koyma göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="cc069-156">To reduce memory requirements, consider removing string columns from fact tables and putting them in smaller dimension tables.</span></span>

<span data-ttu-id="cc069-157">Dize sıkıştırma için ek bellek gereksinimleri:</span><span class="sxs-lookup"><span data-stu-id="cc069-157">Additional memory requirements for string compression:</span></span>

- <span data-ttu-id="cc069-158">En çok 32 karakter dizesi veri türleriyle 32 ek bayt değeri başına gerektirebilir.</span><span class="sxs-lookup"><span data-stu-id="cc069-158">String data types up to 32 characters can require 32 additional bytes per value.</span></span>
- <span data-ttu-id="cc069-159">Birden fazla 32 karakter dizesi veri türleriyle sözlük yöntemleri kullanarak sıkıştırılır.</span><span class="sxs-lookup"><span data-stu-id="cc069-159">String data types with more than 32 characters are compressed using dictionary methods.</span></span>  <span data-ttu-id="cc069-160">Her sütunda satır grubu kimliğinde sözlük oluşturmak için ek 16 MB kadar gerektirebilir.</span><span class="sxs-lookup"><span data-stu-id="cc069-160">Each column in the rowgroup can require up to an additional 16 MB to build the dictionary.</span></span>

### <a name="avoid-over-partitioning"></a><span data-ttu-id="cc069-161">Aşırı bölümleme kaçının</span><span class="sxs-lookup"><span data-stu-id="cc069-161">Avoid over-partitioning</span></span>

<span data-ttu-id="cc069-162">Columnstore dizinleri bölüm başına bir veya daha fazla rowgroups oluşturun.</span><span class="sxs-lookup"><span data-stu-id="cc069-162">Columnstore indexes create one or more rowgroups per partition.</span></span> <span data-ttu-id="cc069-163">SQL veri ambarı'nda bölüm sayısı çünkü veri dağıtılır ve her dağıtım bölümlenmiş hızlı bir şekilde artar.</span><span class="sxs-lookup"><span data-stu-id="cc069-163">In SQL Data Warehouse, the number of partitions grows quickly because the data is distributed and each distribution is partitioned.</span></span> <span data-ttu-id="cc069-164">Tablonun çok fazla bölümleri varsa rowgroups doldurmak için yeterli satırları olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="cc069-164">If the table has too many partitions, there might not be enough rows to fill the rowgroups.</span></span> <span data-ttu-id="cc069-165">Satır eksikliği sıkıştırma sırasında bellek baskısı oluşturmaz, ancak en iyi columnstore sorgu performansı elde etmeyin rowgroups yol açar.</span><span class="sxs-lookup"><span data-stu-id="cc069-165">The lack of rows does not create memory pressure during compression, but it leads to rowgroups that do not achieve the best columnstore query performance.</span></span>

<span data-ttu-id="cc069-166">Aşırı bölümleme önlemek için başka bir nedenle bölümlenmiş bir tablodaki columnstore dizininin içine satırları yükleme için ek bellek olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="cc069-166">Another reason to avoid over-partitioning is there is a memory overhead for loading rows into a columnstore index on a partitioned table.</span></span> <span data-ttu-id="cc069-167">Bir yükleme sırasında her bir bölümü olan sıkıştırılabilmesi için yeterli satırlar kadar bellekte tutulan gelen satırlarını, birçok bölüm alabilir.</span><span class="sxs-lookup"><span data-stu-id="cc069-167">During a load, many partitions could receive the incoming rows, which are held in memory until each partition has enough rows to be compressed.</span></span> <span data-ttu-id="cc069-168">Çok fazla bölümlemeye sahip olmak için ek bellek baskısı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="cc069-168">Having too many partitions creates additional memory pressure.</span></span>

### <a name="simplify-the-load-query"></a><span data-ttu-id="cc069-169">Yük sorguyu basitleştirin</span><span class="sxs-lookup"><span data-stu-id="cc069-169">Simplify the load query</span></span>

<span data-ttu-id="cc069-170">Veritabanı bellek ataması sorgu yer alan tüm işleçler arasında bir sorgu için paylaşır.</span><span class="sxs-lookup"><span data-stu-id="cc069-170">The database shares the memory grant for a query among all the operators in the query.</span></span> <span data-ttu-id="cc069-171">Bir yük sorgu karmaşık sıralar ve birleşimler olduğunda, sıkıştırma kullanılabilir bellek azalır.</span><span class="sxs-lookup"><span data-stu-id="cc069-171">When a load query has complex sorts and joins, the memory available for compression is reduced.</span></span>

<span data-ttu-id="cc069-172">Yalnızca sorgu yüklenirken üzerinde odaklanmaya yük sorgu tasarlayın.</span><span class="sxs-lookup"><span data-stu-id="cc069-172">Design the load query to focus only on loading the query.</span></span> <span data-ttu-id="cc069-173">Üzerindeki veri dönüşümleri çalıştırmanız gerekiyorsa, bunları yük sorgudan ayrı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="cc069-173">If you need to run transformations on the data, run them separate from the load query.</span></span> <span data-ttu-id="cc069-174">Örneğin, öbek tablodaki verileri aşama, dönüştürmeleri çalıştırabilir ve sonra columnstore dizinini hazırlama tablosunda yükleyin.</span><span class="sxs-lookup"><span data-stu-id="cc069-174">For example, stage the data in a heap table, run the transformations, and then load the staging table into the columnstore index.</span></span> <span data-ttu-id="cc069-175">Ayrıca verileri ilk yükleme ve verileri dönüştürmek için MPP sistemi kullanın.</span><span class="sxs-lookup"><span data-stu-id="cc069-175">You can also load the data first and then use the MPP system to transform the data.</span></span>

### <a name="adjust-maxdop"></a><span data-ttu-id="cc069-176">MAXDOP Ayarla</span><span class="sxs-lookup"><span data-stu-id="cc069-176">Adjust MAXDOP</span></span>

<span data-ttu-id="cc069-177">Dağıtım birden çok CPU çekirdeği bulunmadığında her dağıtım rowgroups paralel columnstore içine sıkıştırır.</span><span class="sxs-lookup"><span data-stu-id="cc069-177">Each distribution compresses rowgroups into the columnstore in parallel when there is more than one CPU core available per distribution.</span></span> <span data-ttu-id="cc069-178">Paralellik bellek baskısı ve satır grubu kimliğinde kırpma neden olabilecek ek bellek kaynaklarının gerektirir.</span><span class="sxs-lookup"><span data-stu-id="cc069-178">The parallelism requires additional memory resources, which can lead to memory pressure and rowgroup trimming.</span></span>

<span data-ttu-id="cc069-179">Bellek baskısı azaltmak için her dağıtım içinde seri modunda çalıştırmak için yükleme işlemi zorlamak için MAXDOP sorgu ipucu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cc069-179">To reduce memory pressure, you can use the MAXDOP query hint to force the load operation to run in serial mode within each distribution.</span></span>

```
CREATE TABLE MyFactSalesQuota
WITH (DISTRIBUTION = ROUND_ROBIN)
AS SELECT * FROM FactSalesQUota
OPTION (MAXDOP 1);
```

## <a name="ways-to-allocate-more-memory"></a><span data-ttu-id="cc069-180">Daha fazla bellek yolları</span><span class="sxs-lookup"><span data-stu-id="cc069-180">Ways to allocate more memory</span></span>

<span data-ttu-id="cc069-181">DWU boyutu ve kullanıcı kaynak sınıfı birlikte ne kadar bellek kullanıcı sorgu için uygun olduğunu belirler.</span><span class="sxs-lookup"><span data-stu-id="cc069-181">DWU size and the user resource class together determine how much memory is available for a user query.</span></span> <span data-ttu-id="cc069-182">Bir yük sorgu için bellek ataması artırmak için Dwu sayısını artırmak veya kaynak sınıfı artırın.</span><span class="sxs-lookup"><span data-stu-id="cc069-182">To increase the memory grant for a load query, you can either increase the number of DWUs or increase the resource class.</span></span>

- <span data-ttu-id="cc069-183">Dwu artırmak için bkz: [nasıl ı ölçeklendirme performans?](sql-data-warehouse-manage-compute-overview.md#scale-compute)</span><span class="sxs-lookup"><span data-stu-id="cc069-183">To increase the DWUs, see [How do I scale performance?](sql-data-warehouse-manage-compute-overview.md#scale-compute)</span></span>
- <span data-ttu-id="cc069-184">Bir sorgu için kaynak sınıfı değiştirmek için bkz: [kullanıcı kaynak sınıfı örneğini değiştirmek](sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).</span><span class="sxs-lookup"><span data-stu-id="cc069-184">To change the resource class for a query, see [Change a user resource class example](sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).</span></span>

<span data-ttu-id="cc069-185">Örneğin, DWU 100 üzerinde smallrc kaynak sınıfında bir kullanıcı her dağıtım için 100 MB bellek kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="cc069-185">For example, on DWU 100 a user in the smallrc resource class can use 100 MB of memory for each distribution.</span></span> <span data-ttu-id="cc069-186">Ayrıntılar için bkz [eşzamanlılık SQL Data warehouse'da](sql-data-warehouse-develop-concurrency.md).</span><span class="sxs-lookup"><span data-stu-id="cc069-186">For the details, see [Concurrency in SQL Data Warehouse](sql-data-warehouse-develop-concurrency.md).</span></span>

<span data-ttu-id="cc069-187">Yüksek kaliteli satır grubu kimliğinde boyutları almak için 700 MB bellek gerektiğini belirlemek varsayalım.</span><span class="sxs-lookup"><span data-stu-id="cc069-187">Suppose you determine that you need 700 MB of memory to get high-quality rowgroup sizes.</span></span> <span data-ttu-id="cc069-188">Bu örnekler, yeterli belleğe sahip yük sorgu nasıl çalıştırabileceğiniz gösterir.</span><span class="sxs-lookup"><span data-stu-id="cc069-188">These examples show how you can run the load query with enough memory.</span></span>

- <span data-ttu-id="cc069-189">DWU 1000 ve mediumrc kullanarak, 800 MB bellek ataması</span><span class="sxs-lookup"><span data-stu-id="cc069-189">Using DWU 1000 and mediumrc, your memory grant is 800 MB</span></span>
- <span data-ttu-id="cc069-190">DWU 600 ve largerc kullanarak bellek ataması 800 MB'tır.</span><span class="sxs-lookup"><span data-stu-id="cc069-190">Using DWU 600 and largerc, your memory grant is 800 MB.</span></span>


## <a name="next-steps"></a><span data-ttu-id="cc069-191">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="cc069-191">Next steps</span></span>

<span data-ttu-id="cc069-192">SQL veri ambarı performansını artırmak için daha fazla yolunu öğrenmek için bkz: [performans genel bakış](sql-data-warehouse-overview-manage-user-queries.md).</span><span class="sxs-lookup"><span data-stu-id="cc069-192">To find more ways to improve performance in SQL Data Warehouse, see the [Performance overview](sql-data-warehouse-overview-manage-user-queries.md).</span></span>

<!--Image references-->

<!--Article references-->


<!--MSDN references-->

<!--Other Web references-->
