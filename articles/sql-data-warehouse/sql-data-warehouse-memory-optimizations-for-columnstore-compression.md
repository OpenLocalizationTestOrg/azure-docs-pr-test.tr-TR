---
title: Azure SQL aaaImprove columnstore dizini performans | Microsoft Docs
description: "Bellek gereksinimlerini azaltın veya hello kullanılabilir bellek toomaximize hello her satır grubu kimliğinde bir columnstore dizini sıkıştırır satır sayısını artırın."
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
ms.openlocfilehash: 2c5a68435aa200236a2dc8538aa4638b52a59093
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="maximizing-rowgroup-quality-for-columnstore"></a><span data-ttu-id="1918b-103">Satır grubu kimliğinde kalitesi columnstore için en üst düzeye çıkarma</span><span class="sxs-lookup"><span data-stu-id="1918b-103">Maximizing rowgroup quality for columnstore</span></span>

<span data-ttu-id="1918b-104">Satır grubu kimliğinde kalite hello bir satır grubu kimliğinde satır sayısı tarafından belirlenir.</span><span class="sxs-lookup"><span data-stu-id="1918b-104">Rowgroup quality is determined by hello number of rows in a rowgroup.</span></span> <span data-ttu-id="1918b-105">Bellek gereksinimlerini azaltın veya hello kullanılabilir bellek toomaximize hello her satır grubu kimliğinde bir columnstore dizini sıkıştırır satır sayısını artırın.</span><span class="sxs-lookup"><span data-stu-id="1918b-105">Reduce memory requirements or increase hello available memory toomaximize hello number of rows a columnstore index compresses into each rowgroup.</span></span>  <span data-ttu-id="1918b-106">Bu yöntemleri tooimprove sıkıştırma oranları ve sorgu performansı columnstore dizinleri için kullanın.</span><span class="sxs-lookup"><span data-stu-id="1918b-106">Use these methods tooimprove compression rates and query performance for columnstore indexes.</span></span>

## <a name="why-hello-rowgroup-size-matters"></a><span data-ttu-id="1918b-107">Merhaba satır grubu kimliğinde boyutu neden önemlidir?</span><span class="sxs-lookup"><span data-stu-id="1918b-107">Why hello rowgroup size matters</span></span>
<span data-ttu-id="1918b-108">Tek tek rowgroups sütun kesimleri tarayarak bir tabloda bir columnstore dizini tarar olduğundan, her satır grubu kimliğinde satır hello sayısı en üst düzeye çıkarma sorgu performansını geliştirir.</span><span class="sxs-lookup"><span data-stu-id="1918b-108">Since a columnstore index scans a table by scanning column segments of individual rowgroups, maximizing hello number of rows in each rowgroup enhances query performance.</span></span> <span data-ttu-id="1918b-109">Çok sayıda satır RowGroups sahip olduğunuzda, veri sıkıştırma daha az veri tooread diskten olmadığı anlamına gelir artırır.</span><span class="sxs-lookup"><span data-stu-id="1918b-109">When rowgroups have a high number of rows, data compression improves which means there is less data tooread from disk.</span></span>

<span data-ttu-id="1918b-110">Rowgroups hakkında daha fazla bilgi için bkz: [Columnstore dizinleri Kılavuzu](https://msdn.microsoft.com/library/gg492088.aspx).</span><span class="sxs-lookup"><span data-stu-id="1918b-110">For more information about rowgroups, see [Columnstore Indexes Guide](https://msdn.microsoft.com/library/gg492088.aspx).</span></span>

## <a name="target-size-for-rowgroups"></a><span data-ttu-id="1918b-111">Rowgroups ilişkin hedef boyutu</span><span class="sxs-lookup"><span data-stu-id="1918b-111">Target size for rowgroups</span></span>
<span data-ttu-id="1918b-112">En iyi sorgu performansını hello hedef toomaximize hello satır grubu kimliğinde bir columnstore dizininde başına satır sayısıdır.</span><span class="sxs-lookup"><span data-stu-id="1918b-112">For best query performance, hello goal is toomaximize hello number of rows per rowgroup in a columnstore index.</span></span> <span data-ttu-id="1918b-113">Bir satır grubu kimliğinde 1.048.576 satır en olabilir.</span><span class="sxs-lookup"><span data-stu-id="1918b-113">A rowgroup can have a maximum of 1,048,576 rows.</span></span> <span data-ttu-id="1918b-114">Merhaba en fazla satır grubu başına satır sayısı, sorunsuz toonot var.</span><span class="sxs-lookup"><span data-stu-id="1918b-114">It's okay toonot have hello maximum number of rows per rowgroup.</span></span> <span data-ttu-id="1918b-115">Columnstore dizinleri RowGroups 100. 000'en az satır olduğunda iyi performans elde etmek.</span><span class="sxs-lookup"><span data-stu-id="1918b-115">Columnstore indexes achieve good performance when rowgroups have at least 100,000 rows.</span></span>

## <a name="rowgroups-can-get-trimmed-during-compression"></a><span data-ttu-id="1918b-116">Sıkıştırma sırasında RowGroups kırpılmış</span><span class="sxs-lookup"><span data-stu-id="1918b-116">Rowgroups can get trimmed during compression</span></span>

<span data-ttu-id="1918b-117">Bir toplu yükleme veya columnstore dizini yeniden oluşturma sırasında bazen hiç tüm her satır grubu için belirtilen satır hello yeterli bellek kullanılabilir toocompress.</span><span class="sxs-lookup"><span data-stu-id="1918b-117">During a bulk load or columnstore index rebuild, sometimes there isn't enough memory available toocompress all hello rows designated for each rowgroup.</span></span> <span data-ttu-id="1918b-118">Bellek baskısı olduğunda sıkıştırma hello columnstore içine başarılı şekilde columnstore dizinleri hello satır grubu kimliğinde boyutları kesim.</span><span class="sxs-lookup"><span data-stu-id="1918b-118">When there is memory pressure, columnstore indexes trim hello rowgroup sizes so compression into hello columnstore can succeed.</span></span> 

<span data-ttu-id="1918b-119">Her satır grubu kimliğinde toocompress 10. 000'en az satırlara bellek yetersiz olduğunda, SQL Data Warehouse bir hata oluşturur.</span><span class="sxs-lookup"><span data-stu-id="1918b-119">When there is insufficient memory toocompress at least 10,000 rows into each rowgroup, SQL Data Warehouse generates an error.</span></span>

<span data-ttu-id="1918b-120">Toplu yükleme hakkında daha fazla bilgi için bkz: [toplu yükleme kümelenmiş columnstore dizinine](https://msdn.microsoft.com/en-us/library/dn935008.aspx#Bulk load into a clustered columnstore index).</span><span class="sxs-lookup"><span data-stu-id="1918b-120">For more information on bulk loading, see [Bulk load into a clustered columnstore index](https://msdn.microsoft.com/en-us/library/dn935008.aspx#Bulk load into a clustered columnstore index).</span></span>

## <a name="how-toomonitor-rowgroup-quality"></a><span data-ttu-id="1918b-121">Nasıl toomonitor satır grubu kimliğinde kalitesi</span><span class="sxs-lookup"><span data-stu-id="1918b-121">How toomonitor rowgroup quality</span></span>

<span data-ttu-id="1918b-122">Kırpma rowgroups ve hello nedeni satır sayısı gibi yararlı bilgileri var. kırpma olmadığını gösteren bir DMV (sys.dm_pdw_nodes_db_column_store_row_group_physical_stats) yoktur.</span><span class="sxs-lookup"><span data-stu-id="1918b-122">There is a DMV (sys.dm_pdw_nodes_db_column_store_row_group_physical_stats) that exposes useful information such as number of rows in rowgroups and hello reason for trimming if there was trimming.</span></span> <span data-ttu-id="1918b-123">Görünüm kullanışlı şekilde tooquery olarak aşağıdaki hello satır grubu kimliğinde kırpma üzerinde bu DMV tooget bilgileri oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1918b-123">You can create hello following view as a handy way tooquery this DMV tooget information on rowgroup trimming.</span></span>

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

<span data-ttu-id="1918b-124">Merhaba trim_reason_desc söyler hello satır grubu kimliğinde aynı olup olmadığını (trim_reason_desc = NO_TRIM hiçbir kırpma vardı ve satır grubu en iyi kalitesini olduğu anlamına gelir).</span><span class="sxs-lookup"><span data-stu-id="1918b-124">hello trim_reason_desc tells whether hello rowgroup was trimmed(trim_reason_desc = NO_TRIM implies there was no trimming and row group is of optimal quality).</span></span> <span data-ttu-id="1918b-125">Merhaba kırpma şunlardan hello satır grubu kimliğinde erken kırpılacağını belirtin:</span><span class="sxs-lookup"><span data-stu-id="1918b-125">hello following trim reasons indicate premature trimming of hello rowgroup:</span></span>
- <span data-ttu-id="1918b-126">BULKLOAD: hello gelen toplu satır hello yük için 1 milyondan az satır varken bu kırpma neden kullanılır.</span><span class="sxs-lookup"><span data-stu-id="1918b-126">BULKLOAD: This trim reason is used when hello incoming batch of rows for hello load had less than 1 million rows.</span></span> <span data-ttu-id="1918b-127">Merhaba altyapısı vardır (olarak karşılıklı tooinserting hello delta deposuna) eklenmekte 100.000 satırları büyük ancak kümeleri kırpma neden tooBULKLOAD hello sıkıştırılmış satır grupları oluşturur.</span><span class="sxs-lookup"><span data-stu-id="1918b-127">hello engine will create compressed row groups if there are greater than 100,000 rows being inserted (as opposed tooinserting into hello delta store) but sets hello trim reason tooBULKLOAD.</span></span> <span data-ttu-id="1918b-128">Bu senaryoda, daha fazla satır, toplu iş yükü penceresi tooaccumulate artırmayı düşünün.</span><span class="sxs-lookup"><span data-stu-id="1918b-128">In this scenario, consider increasing your batch load window tooaccumulate more rows.</span></span> <span data-ttu-id="1918b-129">Ayrıca, satır gruplarından bölüm sınırları yayılamaz gibi çok parçalı değil, bölümleme düzeni tooensure yeniden.</span><span class="sxs-lookup"><span data-stu-id="1918b-129">Also, reevaluate your partitioning scheme tooensure it is not too granular as row groups cannot span partition boundaries.</span></span>
- <span data-ttu-id="1918b-130">MEMORY_LIMITATION: toocreate satır grupları 1 milyon satır, belirli bir çalışma bellek miktarı ile Merhaba altyapısı tarafından gereklidir.</span><span class="sxs-lookup"><span data-stu-id="1918b-130">MEMORY_LIMITATION: toocreate row groups with 1 million rows, a certain amount of working memory is required by hello engine.</span></span> <span data-ttu-id="1918b-131">Oturum yüklenirken hello kullanılabilir belleğin hello bellek çalışma gerekenden daha az olduğunda, satır gruplarından erken kırpılır.</span><span class="sxs-lookup"><span data-stu-id="1918b-131">When available memory of hello loading session is less than hello required working memory, row groups get prematurely trimmed.</span></span> <span data-ttu-id="1918b-132">Aşağıdaki bölümlerde hello nasıl tooestimate bellek gerekli ve daha fazla bellek açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="1918b-132">hello following sections explain how tooestimate memory required and allocate more memory.</span></span>
- <span data-ttu-id="1918b-133">DICTIONARY_SIZE: Kırpma bu nedenle, geniş ve/veya yüksek nicelik dizeleri içeren en az bir dize sütunu olduğundan satır grubu kimliğinde kırpma oluştuğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="1918b-133">DICTIONARY_SIZE: This trim reason indicates that rowgroup trimming occurred because there was at least one string column with wide and/or high cardinality strings.</span></span> <span data-ttu-id="1918b-134">Merhaba sözlük MB bellek ve hello satır grubu bu sınıra ulaşıldığında sıkıştırılmış sınırlı too16 boyutudur.</span><span class="sxs-lookup"><span data-stu-id="1918b-134">hello dictionary size is limited too16 MB in memory and once this limit is reached hello row group is compressed.</span></span> <span data-ttu-id="1918b-135">Bu durumla karşılaşırsanız hello sorunlu sütun ayrı bir tabloya izole etmeyi düşünün.</span><span class="sxs-lookup"><span data-stu-id="1918b-135">If you do run into this situation, consider isolating hello problematic column into a separate table.</span></span>

## <a name="how-tooestimate-memory-requirements"></a><span data-ttu-id="1918b-136">Nasıl tooestimate bellek gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="1918b-136">How tooestimate memory requirements</span></span>

<!--
tooview an estimate of hello memory requirements toocompress a rowgroup of maximum size into a columnstore index, download and run hello view [dbo.vCS_mon_mem_grant](). This view shows hello size of hello memory grant that a rowgroup requires for compression in toohello columnstore.
-->

<span data-ttu-id="1918b-137">Merhaba maksimum gerekli bellek toocompress bir satır grubu kimliğinde yaklaşık olarak şöyledir</span><span class="sxs-lookup"><span data-stu-id="1918b-137">hello maximum required memory toocompress one rowgroup is approximately</span></span>

- <span data-ttu-id="1918b-138">72 MB +</span><span class="sxs-lookup"><span data-stu-id="1918b-138">72 MB +</span></span>
- <span data-ttu-id="1918b-139">\#Satır \* \#sütunları \* 8 bayt +</span><span class="sxs-lookup"><span data-stu-id="1918b-139">\#rows \* \#columns \* 8 bytes +</span></span>
- <span data-ttu-id="1918b-140">\#Satır \* \#kısa dize sütunlarındaki \* 32 bayt +</span><span class="sxs-lookup"><span data-stu-id="1918b-140">\#rows \* \#short-string-columns \* 32 bytes +</span></span>
- <span data-ttu-id="1918b-141">\#uzun dize sütunlarındaki \* sıkıştırma sözlüğü için 16 MB</span><span class="sxs-lookup"><span data-stu-id="1918b-141">\#long-string-columns \* 16 MB for compression dictionary</span></span>

<span data-ttu-id="1918b-142">Burada kısa dize sütunlarındaki dize veri türlerini kullanın < = 32 bayt ve > 32 bayt dizesi veri türlerini uzun dize sütunlarındaki kullanın.</span><span class="sxs-lookup"><span data-stu-id="1918b-142">where short-string-columns use string data types of <= 32 bytes and long-string-columns use string data types of > 32 bytes.</span></span>

<span data-ttu-id="1918b-143">Uzun dizeleri metin sıkıştırma için tasarlanmış bir sıkıştırma yöntemi ile sıkıştırılır.</span><span class="sxs-lookup"><span data-stu-id="1918b-143">Long strings are compressed with a compression method designed for compressing text.</span></span> <span data-ttu-id="1918b-144">Bu bir sıkıştırma yöntemi kullanan bir *sözlük* toostore metin kalıplarını.</span><span class="sxs-lookup"><span data-stu-id="1918b-144">This compression method uses a *dictionary* toostore text patterns.</span></span> <span data-ttu-id="1918b-145">bir sözlük Hello en büyük boyutu 16 MB'tır.</span><span class="sxs-lookup"><span data-stu-id="1918b-145">hello maximum size of a dictionary is 16 MB.</span></span> <span data-ttu-id="1918b-146">Merhaba satır grubu kimliğinde her uzun bir dize sütunu için yalnızca bir sözlük yoktur.</span><span class="sxs-lookup"><span data-stu-id="1918b-146">There is only one dictionary for each long string column in hello rowgroup.</span></span>

<span data-ttu-id="1918b-147">Video columnstore bellek gereksinimlerini kapsamlı bir açıklama için bkz [Azure SQL Data Warehouse ölçeklendirme: yapılandırma ve Kılavuzu](https://myignite.microsoft.com/videos/14822).</span><span class="sxs-lookup"><span data-stu-id="1918b-147">For an in-depth discussion of columnstore memory requirements, see the video [Azure SQL Data Warehouse scaling: configuration and guidance](https://myignite.microsoft.com/videos/14822).</span></span>

## <a name="ways-tooreduce-memory-requirements"></a><span data-ttu-id="1918b-148">Yolları tooreduce bellek gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="1918b-148">Ways tooreduce memory requirements</span></span>

<span data-ttu-id="1918b-149">Columnstore dizinleri rowgroups sıkıştırma teknikleri tooreduce hello bellek gereksinimleri aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="1918b-149">Use hello following techniques tooreduce hello memory requirements for compressing rowgroups into columnstore indexes.</span></span>

### <a name="use-fewer-columns"></a><span data-ttu-id="1918b-150">Daha az sütun kullanın</span><span class="sxs-lookup"><span data-stu-id="1918b-150">Use fewer columns</span></span>
<span data-ttu-id="1918b-151">Mümkünse, daha az sütun içeren hello tablo tasarlayın.</span><span class="sxs-lookup"><span data-stu-id="1918b-151">If possible, design hello table with fewer columns.</span></span> <span data-ttu-id="1918b-152">Bir satır grubu kimliğinde hello columnstore sıkıştırılmış zaman hello columnstore dizini her bir sütun segmenti ayrı olarak sıkıştırır.</span><span class="sxs-lookup"><span data-stu-id="1918b-152">When a rowgroup is compressed into hello columnstore, hello columnstore index compresses each column segment separately.</span></span> <span data-ttu-id="1918b-153">Bu nedenle toocompress bir satır grubu kimliğinde hello sütunları artar artırın bellek gereksinimlerini hello.</span><span class="sxs-lookup"><span data-stu-id="1918b-153">Therefore hello memory requirements toocompress a rowgroup increase as hello number of columns increases.</span></span>


### <a name="use-fewer-string-columns"></a><span data-ttu-id="1918b-154">Daha az dize sütun kullanın</span><span class="sxs-lookup"><span data-stu-id="1918b-154">Use fewer string columns</span></span>
<span data-ttu-id="1918b-155">Dize veri türleri sütunlarının daha fazla bellek sayısal ve tarih veri türü gerektirir.</span><span class="sxs-lookup"><span data-stu-id="1918b-155">Columns of string data types require more memory than numeric and date data types.</span></span> <span data-ttu-id="1918b-156">tooreduce bellek gereksinimleri, dize sütunlarındaki olgu tablolarından kaldırarak ve daha küçük boyut tabloları koyma göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="1918b-156">tooreduce memory requirements, consider removing string columns from fact tables and putting them in smaller dimension tables.</span></span>

<span data-ttu-id="1918b-157">Dize sıkıştırma için ek bellek gereksinimleri:</span><span class="sxs-lookup"><span data-stu-id="1918b-157">Additional memory requirements for string compression:</span></span>

- <span data-ttu-id="1918b-158">Değer başına 32 ek bayt too32 karakter dizesi veri türlerini gerektirebilir.</span><span class="sxs-lookup"><span data-stu-id="1918b-158">String data types up too32 characters can require 32 additional bytes per value.</span></span>
- <span data-ttu-id="1918b-159">Birden fazla 32 karakter dizesi veri türleriyle sözlük yöntemleri kullanarak sıkıştırılır.</span><span class="sxs-lookup"><span data-stu-id="1918b-159">String data types with more than 32 characters are compressed using dictionary methods.</span></span>  <span data-ttu-id="1918b-160">Her sütunda hello satır grubu kimliğinde tooan ek 16 MB toobuild hello sözlüğünü gerektirebilir.</span><span class="sxs-lookup"><span data-stu-id="1918b-160">Each column in hello rowgroup can require up tooan additional 16 MB toobuild hello dictionary.</span></span>

### <a name="avoid-over-partitioning"></a><span data-ttu-id="1918b-161">Aşırı bölümleme kaçının</span><span class="sxs-lookup"><span data-stu-id="1918b-161">Avoid over-partitioning</span></span>

<span data-ttu-id="1918b-162">Columnstore dizinleri bölüm başına bir veya daha fazla rowgroups oluşturun.</span><span class="sxs-lookup"><span data-stu-id="1918b-162">Columnstore indexes create one or more rowgroups per partition.</span></span> <span data-ttu-id="1918b-163">SQL veri ambarı'nda hello bölüm sayısı çünkü hello verileri dağıtılır ve her dağıtım bölümlenmiş hızlı bir şekilde artar.</span><span class="sxs-lookup"><span data-stu-id="1918b-163">In SQL Data Warehouse, hello number of partitions grows quickly because hello data is distributed and each distribution is partitioned.</span></span> <span data-ttu-id="1918b-164">Merhaba tablonun çok fazla bölümleri varsa yeterli satırları toofill hello rowgroups olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="1918b-164">If hello table has too many partitions, there might not be enough rows toofill hello rowgroups.</span></span> <span data-ttu-id="1918b-165">Satır Hello eksikliği sıkıştırma sırasında bellek baskısı oluşturmaz, ancak hello en iyi columnstore sorgu performansı elde etmeyin toorowgroups yol açar.</span><span class="sxs-lookup"><span data-stu-id="1918b-165">hello lack of rows does not create memory pressure during compression, but it leads toorowgroups that do not achieve hello best columnstore query performance.</span></span>

<span data-ttu-id="1918b-166">Başka bir nedenle tooavoid aşırı bölümleme bölümlenmiş bir tablodaki columnstore dizininin içine satırları yükleme için ek bellek olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="1918b-166">Another reason tooavoid over-partitioning is there is a memory overhead for loading rows into a columnstore index on a partitioned table.</span></span> <span data-ttu-id="1918b-167">Bir yükleme sırasında her bölüm sıkıştırılmış yeterli satırları toobe olana kadar bellekte tutulan hello gelen satırlarını, birçok bölüm alabilir.</span><span class="sxs-lookup"><span data-stu-id="1918b-167">During a load, many partitions could receive hello incoming rows, which are held in memory until each partition has enough rows toobe compressed.</span></span> <span data-ttu-id="1918b-168">Çok fazla bölümlemeye sahip olmak için ek bellek baskısı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="1918b-168">Having too many partitions creates additional memory pressure.</span></span>

### <a name="simplify-hello-load-query"></a><span data-ttu-id="1918b-169">Merhaba yük sorguyu basitleştirin</span><span class="sxs-lookup"><span data-stu-id="1918b-169">Simplify hello load query</span></span>

<span data-ttu-id="1918b-170">Merhaba veritabanı hello bellek ataması hello sorgudaki tüm hello işleçleri arasında bir sorgu için paylaşır.</span><span class="sxs-lookup"><span data-stu-id="1918b-170">hello database shares hello memory grant for a query among all hello operators in hello query.</span></span> <span data-ttu-id="1918b-171">Bir yük sorgu karmaşık sıralar ve birleşimler olduğunda, sıkıştırma hello bellek azalır.</span><span class="sxs-lookup"><span data-stu-id="1918b-171">When a load query has complex sorts and joins, hello memory available for compression is reduced.</span></span>

<span data-ttu-id="1918b-172">Merhaba yük sorgu toofocus'hello sorgu yüklenirken üzerinde yalnızca tasarlayın.</span><span class="sxs-lookup"><span data-stu-id="1918b-172">Design hello load query toofocus only on loading hello query.</span></span> <span data-ttu-id="1918b-173">Merhaba veri toorun dönüşümler ihtiyacınız varsa, bunları hello yük sorgudan ayrı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="1918b-173">If you need toorun transformations on hello data, run them separate from hello load query.</span></span> <span data-ttu-id="1918b-174">Örneğin, bir yığın tablosunda aşama hello veri hello dönüşümleri çalıştırın ve hazırlama tablosuna hello columnstore dizinine hello yük.</span><span class="sxs-lookup"><span data-stu-id="1918b-174">For example, stage hello data in a heap table, run hello transformations, and then load hello staging table into hello columnstore index.</span></span> <span data-ttu-id="1918b-175">Ayrıca hello verileri ilk yüklemek ve hello MPP sistem tootransform hello verileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="1918b-175">You can also load hello data first and then use hello MPP system tootransform hello data.</span></span>

### <a name="adjust-maxdop"></a><span data-ttu-id="1918b-176">MAXDOP Ayarla</span><span class="sxs-lookup"><span data-stu-id="1918b-176">Adjust MAXDOP</span></span>

<span data-ttu-id="1918b-177">Dağıtım birden çok CPU çekirdeği bulunmadığında her dağıtım rowgroups hello columnstore paralel içine sıkıştırır.</span><span class="sxs-lookup"><span data-stu-id="1918b-177">Each distribution compresses rowgroups into hello columnstore in parallel when there is more than one CPU core available per distribution.</span></span> <span data-ttu-id="1918b-178">Merhaba paralellik toomemory baskısı ve satır grubu kimliğinde kırpma neden olabilecek ek bellek kaynaklarının gerektirir.</span><span class="sxs-lookup"><span data-stu-id="1918b-178">hello parallelism requires additional memory resources, which can lead toomemory pressure and rowgroup trimming.</span></span>

<span data-ttu-id="1918b-179">tooreduce bellek baskısı, her dağıtım içinde seri modunda hello MAXDOP sorgu ipucu tooforce hello yükleme işlemi toorun kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1918b-179">tooreduce memory pressure, you can use hello MAXDOP query hint tooforce hello load operation toorun in serial mode within each distribution.</span></span>

```
CREATE TABLE MyFactSalesQuota
WITH (DISTRIBUTION = ROUND_ROBIN)
AS SELECT * FROM FactSalesQUota
OPTION (MAXDOP 1);
```

## <a name="ways-tooallocate-more-memory"></a><span data-ttu-id="1918b-180">Yolları tooallocate daha fazla bellek</span><span class="sxs-lookup"><span data-stu-id="1918b-180">Ways tooallocate more memory</span></span>

<span data-ttu-id="1918b-181">DWU boyutu ve hello kullanıcı kaynak sınıfı birlikte belirlemek için bir kullanıcı sorgu ne kadar kullanılabilir bellek yok.</span><span class="sxs-lookup"><span data-stu-id="1918b-181">DWU size and hello user resource class together determine how much memory is available for a user query.</span></span> <span data-ttu-id="1918b-182">tooincrease hello bellek Dwu hello sayısını artırmak veya hello kaynak sınıfı artırmak için yük sorgu, verin.</span><span class="sxs-lookup"><span data-stu-id="1918b-182">tooincrease hello memory grant for a load query, you can either increase hello number of DWUs or increase hello resource class.</span></span>

- <span data-ttu-id="1918b-183">tooincrease hello Dwu, bkz: [nasıl ı ölçeklendirme performans?](sql-data-warehouse-manage-compute-overview.md#scale-compute)</span><span class="sxs-lookup"><span data-stu-id="1918b-183">tooincrease hello DWUs, see [How do I scale performance?](sql-data-warehouse-manage-compute-overview.md#scale-compute)</span></span>
- <span data-ttu-id="1918b-184">toochange hello kaynak sınıfı bir sorgu için bkz: [kullanıcı kaynak sınıfı örneğini değiştirmek](sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).</span><span class="sxs-lookup"><span data-stu-id="1918b-184">toochange hello resource class for a query, see [Change a user resource class example](sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).</span></span>

<span data-ttu-id="1918b-185">Örneğin, DWU 100 üzerinde hello smallrc kaynak sınıfında bir kullanıcı her dağıtım için 100 MB bellek kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="1918b-185">For example, on DWU 100 a user in hello smallrc resource class can use 100 MB of memory for each distribution.</span></span> <span data-ttu-id="1918b-186">Merhaba Ayrıntılar için bkz [eşzamanlılık SQL Data warehouse'da](sql-data-warehouse-develop-concurrency.md).</span><span class="sxs-lookup"><span data-stu-id="1918b-186">For hello details, see [Concurrency in SQL Data Warehouse](sql-data-warehouse-develop-concurrency.md).</span></span>

<span data-ttu-id="1918b-187">Bellek tooget yüksek kaliteli satır grubu kimliğinde boyutları 700 MB gerektiğini belirlemek varsayalım.</span><span class="sxs-lookup"><span data-stu-id="1918b-187">Suppose you determine that you need 700 MB of memory tooget high-quality rowgroup sizes.</span></span> <span data-ttu-id="1918b-188">Bu örnekler, yeterli belleğe sahip hello yük sorgu nasıl çalıştırabileceğiniz gösterir.</span><span class="sxs-lookup"><span data-stu-id="1918b-188">These examples show how you can run hello load query with enough memory.</span></span>

- <span data-ttu-id="1918b-189">DWU 1000 ve mediumrc kullanarak, 800 MB bellek ataması</span><span class="sxs-lookup"><span data-stu-id="1918b-189">Using DWU 1000 and mediumrc, your memory grant is 800 MB</span></span>
- <span data-ttu-id="1918b-190">DWU 600 ve largerc kullanarak bellek ataması 800 MB'tır.</span><span class="sxs-lookup"><span data-stu-id="1918b-190">Using DWU 600 and largerc, your memory grant is 800 MB.</span></span>


## <a name="next-steps"></a><span data-ttu-id="1918b-191">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1918b-191">Next steps</span></span>

<span data-ttu-id="1918b-192">toofind SQL Data Warehouse, daha fazla yol tooimprove performans bkz hello [performans genel bakış](sql-data-warehouse-overview-manage-user-queries.md).</span><span class="sxs-lookup"><span data-stu-id="1918b-192">toofind more ways tooimprove performance in SQL Data Warehouse, see hello [Performance overview](sql-data-warehouse-overview-manage-user-queries.md).</span></span>

<!--Image references-->

<!--Article references-->


<!--MSDN references-->

<!--Other Web references-->
