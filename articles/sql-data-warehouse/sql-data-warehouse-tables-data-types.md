---
title: "Veri türleri Kılavuzu - Azure SQL Data Warehouse | Microsoft Docs"
description: "SQL veri ambarı ile uyumlu olan veri türlerini tanımlamak için öneriler sunar."
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: barbkess
editor: 
ms.assetid: d4a1f0a3-ba9f-44b9-95f6-16a4f30746d6
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 06/02/2017
ms.author: shigu;barbkess
ms.openlocfilehash: 5c24c71af16bd9851d9caf15fecfa4bb76f5f77e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="guidance-for-defining-data-types-for-tables-in-sql-data-warehouse"></a><span data-ttu-id="673ed-103">SQL veri ambarı'nda tabloları veri türlerini tanımlama Kılavuzu</span><span class="sxs-lookup"><span data-stu-id="673ed-103">Guidance for defining data types for tables in SQL Data Warehouse</span></span>
<span data-ttu-id="673ed-104">Bu öneriler, SQL Data Warehouse ile uyumlu olan tablo veri türlerini tanımlamak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="673ed-104">Use these recommendations to define table data types that are compatible with SQL Data Warehouse.</span></span> <span data-ttu-id="673ed-105">Uyumluluk ek olarak, veri türlerinin boyutu en aza sorgu performansını artırır.</span><span class="sxs-lookup"><span data-stu-id="673ed-105">In addition to compatibility, minimizing the size of data types improves query performance.</span></span>

<span data-ttu-id="673ed-106">SQL veri ambarı desteklediği veri türleri en yaygın olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="673ed-106">SQL Data Warehouse supports the most commonly used data types.</span></span> <span data-ttu-id="673ed-107">Desteklenen veri türleri listesi için bkz: [veri türleri](/sql/docs/t-sql/statements/create-table-azure-sql-data-warehouse.md#datatypes) CREATE TABLE deyimi içinde.</span><span class="sxs-lookup"><span data-stu-id="673ed-107">For a list of the supported data types, see [data types](/sql/docs/t-sql/statements/create-table-azure-sql-data-warehouse.md#datatypes) in the CREATE TABLE statement.</span></span> 


## <a name="minimize-row-length"></a><span data-ttu-id="673ed-108">Satır uzunluğu simge durumuna küçült</span><span class="sxs-lookup"><span data-stu-id="673ed-108">Minimize row length</span></span>
<span data-ttu-id="673ed-109">Veri türlerinin boyutu en aza indirmek için daha iyi sorgu performansını müşteri adayları satır uzunluğu kısaltır.</span><span class="sxs-lookup"><span data-stu-id="673ed-109">Minimizing the size of data types shortens the row length, which leads to better query performance.</span></span> <span data-ttu-id="673ed-110">Çalışan en küçük veri türü, verileriniz için kullanın.</span><span class="sxs-lookup"><span data-stu-id="673ed-110">Use the smallest data type that works for your data.</span></span> 

- <span data-ttu-id="673ed-111">Büyük varsayılan uzunluk karakter sütunlarla tanımlamamaya özen gösterin.</span><span class="sxs-lookup"><span data-stu-id="673ed-111">Avoid defining character columns with a large default length.</span></span> <span data-ttu-id="673ed-112">Örneğin, en uzun değer 25 karakterden oluşuyorsa, sütun VARCHAR(25) tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="673ed-112">For example, if the longest value is 25 characters, then define your column as VARCHAR(25).</span></span> 
- <span data-ttu-id="673ed-113">Kullanmaktan kaçının [NVARCHAR] [ NVARCHAR] yalnızca gerektiğinde VARCHAR.</span><span class="sxs-lookup"><span data-stu-id="673ed-113">Avoid using [NVARCHAR][NVARCHAR] when you only need VARCHAR.</span></span>
- <span data-ttu-id="673ed-114">Mümkün olduğunda, NVARCHAR(4000) veya VARCHAR(8000) NVARCHAR(MAX) veya VARCHAR(MAX) yerine kullanın.</span><span class="sxs-lookup"><span data-stu-id="673ed-114">When possible, use NVARCHAR(4000) or VARCHAR(8000) instead of NVARCHAR(MAX) or VARCHAR(MAX).</span></span>

<span data-ttu-id="673ed-115">Polybase tablolarınızı yüklemek için kullanıyorsanız, tablo satırı tanımlanan uzunluğu 1 MB aşamaz.</span><span class="sxs-lookup"><span data-stu-id="673ed-115">If you are using Polybase to load your tables, the defined length of the table row cannot exceed 1 MB.</span></span> <span data-ttu-id="673ed-116">Değişken uzunluklu veri sahip bir satır 1 MB aşarsa, satır ile BCP, ancak değil PolyBase yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="673ed-116">When a row with variable-length data exceeds 1 MB, you can load the row with BCP, but not with PolyBase.</span></span>

## <a name="identify-unsupported-data-types"></a><span data-ttu-id="673ed-117">Desteklenmeyen veri türlerini tanımlayın</span><span class="sxs-lookup"><span data-stu-id="673ed-117">Identify unsupported data types</span></span>
<span data-ttu-id="673ed-118">Başka bir SQL veritabanı, veritabanınızı geçiriyorsanız, SQL veri ambarı'nda desteklenmeyen veri türleri karşılaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="673ed-118">If you are migrating your database from another SQL database, you might encounter data types that are not supported in SQL Data Warehouse.</span></span> <span data-ttu-id="673ed-119">Desteklenmeyen veri türleri, var olan SQL şemasında bulmak için bu sorguyu kullanın.</span><span class="sxs-lookup"><span data-stu-id="673ed-119">Use this query to discover unsupported data types in your existing SQL schema.</span></span>

```sql
SELECT  t.[name], c.[name], c.[system_type_id], c.[user_type_id], y.[is_user_defined], y.[name]
FROM sys.tables  t
JOIN sys.columns c on t.[object_id]    = c.[object_id]
JOIN sys.types   y on c.[user_type_id] = y.[user_type_id]
WHERE y.[name] IN ('geography','geometry','hierarchyid','image','text','ntext','sql_variant','timestamp','xml')
 AND  y.[is_user_defined] = 1;
```


## <span data-ttu-id="673ed-120"><a name="unsupported-data-types"></a>Desteklenmeyen veri türleri için kullanım geçici çözümler</span><span class="sxs-lookup"><span data-stu-id="673ed-120"><a name="unsupported-data-types"></a>Use workarounds for unsupported data types</span></span>

<span data-ttu-id="673ed-121">Aşağıdaki liste, veri türleri SQL Data Warehouse desteklemediği ve desteklenmeyen veri türleri yerine kullanabileceğiniz sunacaktır gösterir.</span><span class="sxs-lookup"><span data-stu-id="673ed-121">The following list shows the data types that SQL Data Warehouse does not support and gives alternatives that you can use instead of the unsupported data types.</span></span>

| <span data-ttu-id="673ed-122">Desteklenmeyen veri türü</span><span class="sxs-lookup"><span data-stu-id="673ed-122">Unsupported data type</span></span> | <span data-ttu-id="673ed-123">Geçici çözüm</span><span class="sxs-lookup"><span data-stu-id="673ed-123">Workaround</span></span> |
| --- | --- |
| <span data-ttu-id="673ed-124">[geometri][geometry]</span><span class="sxs-lookup"><span data-stu-id="673ed-124">[geometry][geometry]</span></span> |<span data-ttu-id="673ed-125">[varbinary][varbinary]</span><span class="sxs-lookup"><span data-stu-id="673ed-125">[varbinary][varbinary]</span></span> |
| <span data-ttu-id="673ed-126">[coğrafi konum][geography]</span><span class="sxs-lookup"><span data-stu-id="673ed-126">[geography][geography]</span></span> |<span data-ttu-id="673ed-127">[varbinary][varbinary]</span><span class="sxs-lookup"><span data-stu-id="673ed-127">[varbinary][varbinary]</span></span> |
| <span data-ttu-id="673ed-128">[HierarchyId][hierarchyid]</span><span class="sxs-lookup"><span data-stu-id="673ed-128">[hierarchyid][hierarchyid]</span></span> |<span data-ttu-id="673ed-129">[nvarchar][nvarchar](4000)</span><span class="sxs-lookup"><span data-stu-id="673ed-129">[nvarchar][nvarchar](4000)</span></span> |
| <span data-ttu-id="673ed-130">[Görüntü][ntext,text,image]</span><span class="sxs-lookup"><span data-stu-id="673ed-130">[image][ntext,text,image]</span></span> |<span data-ttu-id="673ed-131">[varbinary][varbinary]</span><span class="sxs-lookup"><span data-stu-id="673ed-131">[varbinary][varbinary]</span></span> |
| <span data-ttu-id="673ed-132">[metin][ntext,text,image]</span><span class="sxs-lookup"><span data-stu-id="673ed-132">[text][ntext,text,image]</span></span> |<span data-ttu-id="673ed-133">[varchar][varchar]</span><span class="sxs-lookup"><span data-stu-id="673ed-133">[varchar][varchar]</span></span> |
| <span data-ttu-id="673ed-134">[ntext][ntext,text,image]</span><span class="sxs-lookup"><span data-stu-id="673ed-134">[ntext][ntext,text,image]</span></span> |<span data-ttu-id="673ed-135">[nvarchar][nvarchar]</span><span class="sxs-lookup"><span data-stu-id="673ed-135">[nvarchar][nvarchar]</span></span> |
| <span data-ttu-id="673ed-136">[sql_variant][sql_variant]</span><span class="sxs-lookup"><span data-stu-id="673ed-136">[sql_variant][sql_variant]</span></span> |<span data-ttu-id="673ed-137">Sütun birkaç kesin türü belirtilmiş sütuna bölün.</span><span class="sxs-lookup"><span data-stu-id="673ed-137">Split column into several strongly typed columns.</span></span> |
| <span data-ttu-id="673ed-138">[Tablo][table]</span><span class="sxs-lookup"><span data-stu-id="673ed-138">[table][table]</span></span> |<span data-ttu-id="673ed-139">Geçici tablolara dönüşür.</span><span class="sxs-lookup"><span data-stu-id="673ed-139">Convert to temporary tables.</span></span> |
| <span data-ttu-id="673ed-140">[zaman damgası][timestamp]</span><span class="sxs-lookup"><span data-stu-id="673ed-140">[timestamp][timestamp]</span></span> |<span data-ttu-id="673ed-141">Kullanmak için kodu rework [datetime2] [ datetime2] ve `CURRENT_TIMESTAMP` işlevi.</span><span class="sxs-lookup"><span data-stu-id="673ed-141">Rework code to use [datetime2][datetime2] and `CURRENT_TIMESTAMP` function.</span></span>  <span data-ttu-id="673ed-142">Yalnızca sabit değerleri desteklenir varsayılan olarak, bu nedenle current_timestamp varsayılan kısıtlama olarak tanımlanamaz.</span><span class="sxs-lookup"><span data-stu-id="673ed-142">Only constants are supported as defaults, therefore current_timestamp cannot be defined as a default constraint.</span></span> <span data-ttu-id="673ed-143">Zaman damgası yazılan sütundan satır sürümü değerleri geçirmek gerekiyorsa, daha sonra kullanmak [ikili][BINARY](8) veya [VARBINARY][BINARY](8) için NOT NULL veya Satır sürümü değerleri NULL.</span><span class="sxs-lookup"><span data-stu-id="673ed-143">If you need to migrate row version values from a timestamp typed column, then use [BINARY][BINARY](8) or [VARBINARY][BINARY](8) for NOT NULL or NULL row version values.</span></span> |
| <span data-ttu-id="673ed-144">[XML][xml]</span><span class="sxs-lookup"><span data-stu-id="673ed-144">[xml][xml]</span></span> |<span data-ttu-id="673ed-145">[varchar][varchar]</span><span class="sxs-lookup"><span data-stu-id="673ed-145">[varchar][varchar]</span></span> |
| <span data-ttu-id="673ed-146">[Kullanıcı tanımlı tür][user defined types]</span><span class="sxs-lookup"><span data-stu-id="673ed-146">[user-defined type][user defined types]</span></span> |<span data-ttu-id="673ed-147">Geri mümkün olduğunda gibi bir yerel veri türüne dönüştürün.</span><span class="sxs-lookup"><span data-stu-id="673ed-147">Convert back to the native data type when possible.</span></span> |
| <span data-ttu-id="673ed-148">Varsayılan değerler</span><span class="sxs-lookup"><span data-stu-id="673ed-148">default values</span></span> | <span data-ttu-id="673ed-149">Varsayılan değerleri değişmez değerleri ve yalnızca sabitleri desteklemez.</span><span class="sxs-lookup"><span data-stu-id="673ed-149">Default values support literals and constants only.</span></span>  <span data-ttu-id="673ed-150">Belirleyici olmayan ifadeleri ve İşlevler, gibi `GETDATE()` veya `CURRENT_TIMESTAMP`, desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="673ed-150">Non-deterministic expressions or functions, such as `GETDATE()` or `CURRENT_TIMESTAMP`, are not supported.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="673ed-151">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="673ed-151">Next steps</span></span>
<span data-ttu-id="673ed-152">Daha fazla bilgi için bkz:</span><span class="sxs-lookup"><span data-stu-id="673ed-152">To learn more, see:</span></span>

- <span data-ttu-id="673ed-153">[SQL veri ambarı en iyi uygulamalar][SQL Data Warehouse Best Practices]</span><span class="sxs-lookup"><span data-stu-id="673ed-153">[SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices]</span></span>
- <span data-ttu-id="673ed-154">[Tablo genel bakış][Overview]</span><span class="sxs-lookup"><span data-stu-id="673ed-154">[Table Overview][Overview]</span></span>
- <span data-ttu-id="673ed-155">[Bir tablo dağıtma][Distribute]</span><span class="sxs-lookup"><span data-stu-id="673ed-155">[Distributing a Table][Distribute]</span></span>
- <span data-ttu-id="673ed-156">[Bir tablo dizin oluşturma][Index]</span><span class="sxs-lookup"><span data-stu-id="673ed-156">[Indexing a Table][Index]</span></span>
- <span data-ttu-id="673ed-157">[Bir tablo bölümleme][Partition]</span><span class="sxs-lookup"><span data-stu-id="673ed-157">[Partitioning a Table][Partition]</span></span>
- <span data-ttu-id="673ed-158">[Tablo istatistikleri koruma][Statistics]</span><span class="sxs-lookup"><span data-stu-id="673ed-158">[Maintaining Table Statistics][Statistics]</span></span>
- <span data-ttu-id="673ed-159">[Geçici tablolar][Temporary]</span><span class="sxs-lookup"><span data-stu-id="673ed-159">[Temporary Tables][Temporary]</span></span>

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

<!--MSDN references-->

<!--Other Web references-->
[create table]: https://msdn.microsoft.com/library/mt203953.aspx
[bigint]: https://msdn.microsoft.com/library/ms187745.aspx
[binary]: https://msdn.microsoft.com/library/ms188362.aspx
[bit]: https://msdn.microsoft.com/library/ms177603.aspx
[char]: https://msdn.microsoft.com/library/ms176089.aspx
[date]: https://msdn.microsoft.com/library/bb630352.aspx
[datetime]: https://msdn.microsoft.com/library/ms187819.aspx
[datetime2]: https://msdn.microsoft.com/library/bb677335.aspx
[datetimeoffset]: https://msdn.microsoft.com/library/bb630289.aspx
[decimal]: https://msdn.microsoft.com/library/ms187746.aspx
[float]: https://msdn.microsoft.com/library/ms173773.aspx
[geometry]: https://msdn.microsoft.com/library/cc280487.aspx
[geography]: https://msdn.microsoft.com/library/cc280766.aspx
[hierarchyid]: https://msdn.microsoft.com/library/bb677290.aspx
[int]: https://msdn.microsoft.com/library/ms187745.aspx
[money]: https://msdn.microsoft.com/library/ms179882.aspx
[nchar]: https://msdn.microsoft.com/library/ms186939.aspx
[nvarchar]: https://msdn.microsoft.com/library/ms186939.aspx
[ntext,text,image]: https://msdn.microsoft.com/library/ms187993.aspx
[real]: https://msdn.microsoft.com/library/ms173773.aspx
[smalldatetime]: https://msdn.microsoft.com/library/ms182418.aspx
[smallint]: https://msdn.microsoft.com/library/ms187745.aspx
[smallmoney]: https://msdn.microsoft.com/library/ms179882.aspx
[sql_variant]: https://msdn.microsoft.com/library/ms173829.aspx
[sysname]: https://msdn.microsoft.com/library/ms186939.aspx
[table]: https://msdn.microsoft.com/library/ms175010.aspx
[time]: https://msdn.microsoft.com/library/bb677243.aspx
[timestamp]: https://msdn.microsoft.com/library/ms182776.aspx
[tinyint]: https://msdn.microsoft.com/library/ms187745.aspx
[uniqueidentifier]: https://msdn.microsoft.com/library/ms187942.aspx
[varbinary]: https://msdn.microsoft.com/library/ms188362.aspx
[varchar]: https://msdn.microsoft.com/library/ms186939.aspx
[xml]: https://msdn.microsoft.com/library/ms187339.aspx
[user defined types]: https://msdn.microsoft.com/library/ms131694.aspx
