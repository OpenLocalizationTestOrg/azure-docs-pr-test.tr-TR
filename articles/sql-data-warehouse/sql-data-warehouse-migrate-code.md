---
title: "SQL veri ambarına SQL kodunuzu geçirme | Microsoft Docs"
description: "Çözümleri geliştirme için Azure SQL Data Warehouse SQL kodunuzu geçirmek için ipuçları."
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: 19c252a3-0e41-4eec-9d3e-09a68c7e7add
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 06/23/2017
ms.author: joeyong;barbkess
ms.openlocfilehash: c6e6b890f5e2d0e31b10bbb6803adad02bf60248
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="migrate-your-sql-code-to-sql-data-warehouse"></a><span data-ttu-id="c8fbf-103">SQL kodunuzu SQL veri ambarına geçirme</span><span class="sxs-lookup"><span data-stu-id="c8fbf-103">Migrate your SQL code to SQL Data Warehouse</span></span>
<span data-ttu-id="c8fbf-104">Bu makalede, büyük olasılıkla kodunuzun başka bir veritabanından SQL veri ambarı'na geçirirken yapmanız gerekecektir kod değişiklikleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="c8fbf-104">This article explains code changes you will probably need to make when migrating your code from another database to SQL Data Warehouse.</span></span> <span data-ttu-id="c8fbf-105">Dağıtılmış bir şekilde çalışması için tasarlanmış gibi bazı SQL veri ambarı özellikleri önemli ölçüde performansını iyileştirebilir.</span><span class="sxs-lookup"><span data-stu-id="c8fbf-105">Some SQL Data Warehouse features can significantly improve performance as they are designed to work in a distributed fashion.</span></span> <span data-ttu-id="c8fbf-106">Ancak, performansı ve ölçeği korumak için bazı özellikler de kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="c8fbf-106">However, to maintain performance and scale, some features are also not available.</span></span>

## <a name="common-t-sql-limitations"></a><span data-ttu-id="c8fbf-107">Ortak T-SQL sınırlamaları</span><span class="sxs-lookup"><span data-stu-id="c8fbf-107">Common T-SQL Limitations</span></span>
<span data-ttu-id="c8fbf-108">Aşağıdaki listede, SQL Data Warehouse desteklemediği en yaygın özellikler özetlenmektedir.</span><span class="sxs-lookup"><span data-stu-id="c8fbf-108">The following list summarizes the most common features that SQL Data Warehouse does not support.</span></span> <span data-ttu-id="c8fbf-109">Bağlantılar için desteklenmeyen özellikler geçici çözümler için gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="c8fbf-109">The links take you to workarounds for the unsupported features:</span></span>

* <span data-ttu-id="c8fbf-110">[ANSI birleştirmeler güncelleştirmeleri][ANSI joins on updates]</span><span class="sxs-lookup"><span data-stu-id="c8fbf-110">[ANSI joins on updates][ANSI joins on updates]</span></span>
* <span data-ttu-id="c8fbf-111">[ANSI birleştirmeler üzerinde siler][ANSI joins on deletes]</span><span class="sxs-lookup"><span data-stu-id="c8fbf-111">[ANSI joins on deletes][ANSI joins on deletes]</span></span>
* <span data-ttu-id="c8fbf-112">[Merge deyimi][merge statement]</span><span class="sxs-lookup"><span data-stu-id="c8fbf-112">[merge statement][merge statement]</span></span>
* <span data-ttu-id="c8fbf-113">veritabanları arası birleşimler</span><span class="sxs-lookup"><span data-stu-id="c8fbf-113">cross-database joins</span></span>
* <span data-ttu-id="c8fbf-114">[imleçler][cursors]</span><span class="sxs-lookup"><span data-stu-id="c8fbf-114">[cursors][cursors]</span></span>
* <span data-ttu-id="c8fbf-115">[EKLE... EXEC][INSERT..EXEC]</span><span class="sxs-lookup"><span data-stu-id="c8fbf-115">[INSERT..EXEC][INSERT..EXEC]</span></span>
* <span data-ttu-id="c8fbf-116">Output yan tümcesi</span><span class="sxs-lookup"><span data-stu-id="c8fbf-116">output clause</span></span>
* <span data-ttu-id="c8fbf-117">Satır içi kullanıcı tanımlı işlevler</span><span class="sxs-lookup"><span data-stu-id="c8fbf-117">inline user-defined functions</span></span>
* <span data-ttu-id="c8fbf-118">birden fazla deyim işlevleri</span><span class="sxs-lookup"><span data-stu-id="c8fbf-118">multi-statement functions</span></span>
* [<span data-ttu-id="c8fbf-119">Ortak tablo ifadeleri</span><span class="sxs-lookup"><span data-stu-id="c8fbf-119">common table expressions</span></span>](#Common-table-expressions)
* <span data-ttu-id="c8fbf-120">[özyinelemeli ortak tablo ifadeleri (CTE)] (#Recursive-common-table-expressions-(CTE)</span><span class="sxs-lookup"><span data-stu-id="c8fbf-120">[recursive common table expressions (CTE)](#Recursive-common-table-expressions-(CTE)</span></span>
* <span data-ttu-id="c8fbf-121">CLR işlevleri ve yordamları</span><span class="sxs-lookup"><span data-stu-id="c8fbf-121">CLR functions and procedures</span></span>
* <span data-ttu-id="c8fbf-122">$partition işlevi</span><span class="sxs-lookup"><span data-stu-id="c8fbf-122">$partition function</span></span>
* <span data-ttu-id="c8fbf-123">Tablo değişkenleri</span><span class="sxs-lookup"><span data-stu-id="c8fbf-123">table variables</span></span>
* <span data-ttu-id="c8fbf-124">Tablo değeri parametreleri</span><span class="sxs-lookup"><span data-stu-id="c8fbf-124">table value parameters</span></span>
* <span data-ttu-id="c8fbf-125">Dağıtılmış işlemler</span><span class="sxs-lookup"><span data-stu-id="c8fbf-125">distributed transactions</span></span>
* <span data-ttu-id="c8fbf-126">Commit / rollback çalışma</span><span class="sxs-lookup"><span data-stu-id="c8fbf-126">commit / rollback work</span></span>
* <span data-ttu-id="c8fbf-127">işlem Kaydet</span><span class="sxs-lookup"><span data-stu-id="c8fbf-127">save transaction</span></span>
* <span data-ttu-id="c8fbf-128">yürütme bağlamı (EXECUTE AS)</span><span class="sxs-lookup"><span data-stu-id="c8fbf-128">execution contexts (EXECUTE AS)</span></span>
* <span data-ttu-id="c8fbf-129">[Grup by tümcesi paketi / küp / gruplandırma kümeleri seçenekleri][group by clause with rollup / cube / grouping sets options]</span><span class="sxs-lookup"><span data-stu-id="c8fbf-129">[group by clause with rollup / cube / grouping sets options][group by clause with rollup / cube / grouping sets options]</span></span>
* <span data-ttu-id="c8fbf-130">[iç içe geçme düzeyi 8 ötesinde][nesting levels beyond 8]</span><span class="sxs-lookup"><span data-stu-id="c8fbf-130">[nesting levels beyond 8][nesting levels beyond 8]</span></span>
* <span data-ttu-id="c8fbf-131">[görünümleri aracılığıyla güncelleştirme][updating through views]</span><span class="sxs-lookup"><span data-stu-id="c8fbf-131">[updating through views][updating through views]</span></span>
* <span data-ttu-id="c8fbf-132">[değişken ataması için seçimi kullanın][use of select for variable assignment]</span><span class="sxs-lookup"><span data-stu-id="c8fbf-132">[use of select for variable assignment][use of select for variable assignment]</span></span>
* <span data-ttu-id="c8fbf-133">[dinamik SQL dizeleri için hiçbir en büyük veri türü][no MAX data type for dynamic SQL strings]</span><span class="sxs-lookup"><span data-stu-id="c8fbf-133">[no MAX data type for dynamic SQL strings][no MAX data type for dynamic SQL strings]</span></span>

<span data-ttu-id="c8fbf-134">Neyse ki bu sınırlamalara çoğunu geçici çalışılan.</span><span class="sxs-lookup"><span data-stu-id="c8fbf-134">Fortunately most of these limitations can be worked around.</span></span> <span data-ttu-id="c8fbf-135">Açıklamalar, yukarıda başvurulan ilgili geliştirme makalelerinde sağlanır.</span><span class="sxs-lookup"><span data-stu-id="c8fbf-135">Explanations are provided in the relevant development articles referenced above.</span></span>

## <a name="supported-cte-features"></a><span data-ttu-id="c8fbf-136">Desteklenen CTE Özellikler</span><span class="sxs-lookup"><span data-stu-id="c8fbf-136">Supported CTE features</span></span>
<span data-ttu-id="c8fbf-137">Ortak tablo ifadelerinde (Cte'lerin) SQL veri ambarı'nda kısmen desteklenir.</span><span class="sxs-lookup"><span data-stu-id="c8fbf-137">Common table expressions (CTEs) are partially supported in SQL Data Warehouse.</span></span>  <span data-ttu-id="c8fbf-138">Aşağıdaki CTE özellikleri şu anda desteklenir:</span><span class="sxs-lookup"><span data-stu-id="c8fbf-138">The following CTE features are currently supported:</span></span>

* <span data-ttu-id="c8fbf-139">SELECT deyiminde bir CTE belirtilebilir.</span><span class="sxs-lookup"><span data-stu-id="c8fbf-139">A CTE can be specified in a SELECT statement.</span></span>
* <span data-ttu-id="c8fbf-140">Bir CTE CREATE VIEW deyiminde belirtilebilir.</span><span class="sxs-lookup"><span data-stu-id="c8fbf-140">A CTE can be specified in a CREATE VIEW statement.</span></span>
* <span data-ttu-id="c8fbf-141">Bir CTE oluşturmak tablo AS seçin (CTAS) deyiminde belirtilebilir.</span><span class="sxs-lookup"><span data-stu-id="c8fbf-141">A CTE can be specified in a CREATE TABLE AS SELECT (CTAS) statement.</span></span>
* <span data-ttu-id="c8fbf-142">Bir CTE oluşturma uzak tablo AS seçin (CRTAS) deyiminde belirtilebilir.</span><span class="sxs-lookup"><span data-stu-id="c8fbf-142">A CTE can be specified in a CREATE REMOTE TABLE AS SELECT (CRTAS) statement.</span></span>
* <span data-ttu-id="c8fbf-143">Bir CTE oluşturmak dış tablo AS seçin (CETAS) deyiminde belirtilebilir.</span><span class="sxs-lookup"><span data-stu-id="c8fbf-143">A CTE can be specified in a CREATE EXTERNAL TABLE AS SELECT (CETAS) statement.</span></span>
* <span data-ttu-id="c8fbf-144">Bir uzak tablo CTE başvurulabilir.</span><span class="sxs-lookup"><span data-stu-id="c8fbf-144">A remote table can be referenced from a CTE.</span></span>
* <span data-ttu-id="c8fbf-145">Bir dış tablo CTE başvurulabilir.</span><span class="sxs-lookup"><span data-stu-id="c8fbf-145">An external table can be referenced from a CTE.</span></span>
* <span data-ttu-id="c8fbf-146">Birden fazla CTE sorgu tanımı bir CTE tanımlanabilir.</span><span class="sxs-lookup"><span data-stu-id="c8fbf-146">Multiple CTE query definitions can be defined in a CTE.</span></span>

## <a name="cte-limitations"></a><span data-ttu-id="c8fbf-147">CTE sınırlamaları</span><span class="sxs-lookup"><span data-stu-id="c8fbf-147">CTE Limitations</span></span>
<span data-ttu-id="c8fbf-148">Ortak tablo ifadelerinde SQL Data Warehouse dahil, bazı sınırlamalar vardır:</span><span class="sxs-lookup"><span data-stu-id="c8fbf-148">Common table expressions have some limitations in SQL Data Warehouse including:</span></span>

* <span data-ttu-id="c8fbf-149">Bir CTE tek bir SELECT deyimi tarafından izlenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="c8fbf-149">A CTE must be followed by a single SELECT statement.</span></span> <span data-ttu-id="c8fbf-150">INSERT, UPDATE, DELETE ve MERGE deyimleri desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="c8fbf-150">INSERT, UPDATE, DELETE, and MERGE statements are not supported.</span></span>
* <span data-ttu-id="c8fbf-151">Başvurular kendisi (bir özyinelemeli ortak tablo ifadesi) içeren bir ortak tablo ifadesi desteklenmiyor (bölüme bakın).</span><span class="sxs-lookup"><span data-stu-id="c8fbf-151">A common table expression that includes references to itself (a recursive common table expression) is not supported (see below section).</span></span>
* <span data-ttu-id="c8fbf-152">Birden çok yan tümcesi ile birlikte bir CTE belirtme izin verilmiyor.</span><span class="sxs-lookup"><span data-stu-id="c8fbf-152">Specifying more than one WITH clause in a CTE is not allowed.</span></span> <span data-ttu-id="c8fbf-153">Bir CTE_query_definition bir alt sorgu içeriyorsa, örneğin, bu alt sorgu iç içe bir başka bir CTE tanımlayan yan tümcesiyle birlikte içeremez.</span><span class="sxs-lookup"><span data-stu-id="c8fbf-153">For example, if a CTE_query_definition contains a subquery, that subquery cannot contain a nested WITH clause that defines another CTE.</span></span>
* <span data-ttu-id="c8fbf-154">TOP yan tümcesi belirtildiğinde ORDER BY yan tümcesi dışında CTE_query_definition içinde kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="c8fbf-154">An ORDER BY clause cannot be used in the CTE_query_definition, except when a TOP clause is specified.</span></span>
* <span data-ttu-id="c8fbf-155">Bir CTE bir toplu iş parçası olan bir deyimde kullanıldığında, önceki deyimi noktalı virgülle gelmelidir.</span><span class="sxs-lookup"><span data-stu-id="c8fbf-155">When a CTE is used in a statement that is part of a batch, the statement before it must be followed by a semicolon.</span></span>
* <span data-ttu-id="c8fbf-156">Sp_prepare tarafından hazırlanan deyimlerinde kullanıldığında, Cte'lerin PDW diğer SELECT deyimlerinde aynı şekilde davranır.</span><span class="sxs-lookup"><span data-stu-id="c8fbf-156">When used in statements prepared by sp_prepare, CTEs will behave the same way as other SELECT statements in PDW.</span></span> <span data-ttu-id="c8fbf-157">Cte'lerin CETAS sp_prepare tarafından hazırlanan bir parçası olarak kullanılıyorsa, ancak davranışı SQL Server ve diğer PDW deyimleri bağlama için sp_prepare uygulandığı yol nedeniyle erteleneceği.</span><span class="sxs-lookup"><span data-stu-id="c8fbf-157">However, if CTEs are used as part of CETAS prepared by sp_prepare, the behavior can defer from SQL Server and other PDW statements because of the way binding is implemented for sp_prepare.</span></span> <span data-ttu-id="c8fbf-158">SEÇİN, başvuruları CTE içinde yok yanlış bir sütun CTE kullanarak sp_prepare hata algılama olmadan geçirir, ancak hata sırasında sp_execute yerine oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="c8fbf-158">If SELECT that references CTE is using a wrong column that does not exist in CTE, the sp_prepare will pass without detecting the error, but the error will be thrown during sp_execute instead.</span></span>

## <a name="recursive-ctes"></a><span data-ttu-id="c8fbf-159">Özyinelemeli Cte'lerin</span><span class="sxs-lookup"><span data-stu-id="c8fbf-159">Recursive CTEs</span></span>
<span data-ttu-id="c8fbf-160">Özyinelemeli Cte'lerin SQL veri ambarı'nda desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="c8fbf-160">Recursive CTEs are not supported in SQL Data Warehouse.</span></span>  <span data-ttu-id="c8fbf-161">Özyinelemeli CTE geçişini biraz karmaşık olabilir ve içine birden çok adımı ayırmak için en iyi işlemidir.</span><span class="sxs-lookup"><span data-stu-id="c8fbf-161">The migration of recursive CTE can be somewhat complex and the best process is to break it into multiple steps.</span></span> <span data-ttu-id="c8fbf-162">Genellikle, bir döngü kullanın ve geçici bir tablo özyinelemeli geçici sorguları yinelemek gibi doldurun.</span><span class="sxs-lookup"><span data-stu-id="c8fbf-162">You can typically use a loop and populate a temporary table as you iterate over the recursive interim queries.</span></span> <span data-ttu-id="c8fbf-163">Geçici tablo doldurulduktan sonra için verileri tek bir sonuç kümesi olarak geri dönebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c8fbf-163">Once the temporary table is populated you can then return the data as a single result set.</span></span> <span data-ttu-id="c8fbf-164">Benzer bir yaklaşım çözmek için kullanılan `GROUP BY WITH CUBE` içinde [Grup by tümcesi paketi / küp / gruplandırma kümeleri seçenekleri] [ group by clause with rollup / cube / grouping sets options] makalesi.</span><span class="sxs-lookup"><span data-stu-id="c8fbf-164">A similar approach has been used to solve `GROUP BY WITH CUBE` in the [group by clause with rollup / cube / grouping sets options][group by clause with rollup / cube / grouping sets options] article.</span></span>

## <a name="unsupported-system-functions"></a><span data-ttu-id="c8fbf-165">Desteklenmeyen sistem işlevleri</span><span class="sxs-lookup"><span data-stu-id="c8fbf-165">Unsupported system functions</span></span>
<span data-ttu-id="c8fbf-166">Desteklenmeyen bazı sistem işlevleri de vardır.</span><span class="sxs-lookup"><span data-stu-id="c8fbf-166">There are also some system functions that are not supported.</span></span> <span data-ttu-id="c8fbf-167">Veri ambarı genellikle bulabileceğiniz Ana Kullanılanlar bazıları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="c8fbf-167">Some of the main ones you might typically find used in data warehousing are:</span></span>

* <span data-ttu-id="c8fbf-168">NEWSEQUENTIALID()</span><span class="sxs-lookup"><span data-stu-id="c8fbf-168">NEWSEQUENTIALID()</span></span>
* <span data-ttu-id="c8fbf-169">@@NESTLEVEL()</span><span class="sxs-lookup"><span data-stu-id="c8fbf-169">@@NESTLEVEL()</span></span>
* <span data-ttu-id="c8fbf-170">@@IDENTITY()</span><span class="sxs-lookup"><span data-stu-id="c8fbf-170">@@IDENTITY()</span></span>
* <span data-ttu-id="c8fbf-171">@@ROWCOUNT()</span><span class="sxs-lookup"><span data-stu-id="c8fbf-171">@@ROWCOUNT()</span></span>
* <span data-ttu-id="c8fbf-172">ROWCOUNT_BIG</span><span class="sxs-lookup"><span data-stu-id="c8fbf-172">ROWCOUNT_BIG</span></span>
* <span data-ttu-id="c8fbf-173">ERROR_LINE()</span><span class="sxs-lookup"><span data-stu-id="c8fbf-173">ERROR_LINE()</span></span>

<span data-ttu-id="c8fbf-174">Bu sorunlardan bazıları geçici çalışılan.</span><span class="sxs-lookup"><span data-stu-id="c8fbf-174">Some of these issues can be worked around.</span></span>

## <a name="rowcount-workaround"></a><span data-ttu-id="c8fbf-175">@@ROWCOUNT geçici çözüm</span><span class="sxs-lookup"><span data-stu-id="c8fbf-175">@@ROWCOUNT workaround</span></span>
<span data-ttu-id="c8fbf-176">Desteğinin geçici olarak çözmek için@ROWCOUNT, son satır sayısı sys.dm_pdw_request_steps almak ve sonra yürütün bir saklı yordam oluşturmak `EXEC LastRowCount` DML deyimi sonra.</span><span class="sxs-lookup"><span data-stu-id="c8fbf-176">To work around lack of support for @@ROWCOUNT, create a stored procedure that will retrieve the last row count from sys.dm_pdw_request_steps and then execute `EXEC LastRowCount` after a DML statement.</span></span>

```sql
CREATE PROCEDURE LastRowCount AS
WITH LastRequest as 
(   SELECT TOP 1    request_id
    FROM            sys.dm_pdw_exec_requests
    WHERE           session_id = SESSION_ID()
    AND             resource_class IS NOT NULL
    ORDER BY end_time DESC
),
LastRequestRowCounts as
(
    SELECT  step_index, row_count
    FROM    sys.dm_pdw_request_steps
    WHERE   row_count >= 0
    AND     request_id IN (SELECT request_id from LastRequest)
)
SELECT TOP 1 row_count FROM LastRequestRowCounts ORDER BY step_index DESC
;
```

## <a name="next-steps"></a><span data-ttu-id="c8fbf-177">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c8fbf-177">Next steps</span></span>
<span data-ttu-id="c8fbf-178">Tüm desteklenen T-SQL deyimlerini tam bir listesi için bkz: [Transact-SQL konuları][Transact-SQL topics].</span><span class="sxs-lookup"><span data-stu-id="c8fbf-178">For a complete list of all supported T-SQL statements, see [Transact-SQL topics][Transact-SQL topics].</span></span>

<!--Image references-->

<!--Article references-->
[ANSI joins on updates]: ./sql-data-warehouse-develop-ctas.md#ansi-join-replacement-for-update-statements
[ANSI joins on deletes]: ./sql-data-warehouse-develop-ctas.md#ansi-join-replacement-for-delete-statements
[merge statement]: ./sql-data-warehouse-develop-ctas.md#replace-merge-statements
[INSERT..EXEC]: ./sql-data-warehouse-tables-temporary.md#modularizing-code
[Transact-SQL topics]: ./sql-data-warehouse-reference-tsql-statements.md

[cursors]: ./sql-data-warehouse-develop-loops.md
[group by clause with rollup / cube / grouping sets options]: ./sql-data-warehouse-develop-group-by-options.md
[nesting levels beyond 8]: ./sql-data-warehouse-develop-transactions.md
[updating through views]: ./sql-data-warehouse-develop-views.md
[use of select for variable assignment]: ./sql-data-warehouse-develop-variable-assignment.md
[no MAX data type for dynamic SQL strings]: ./sql-data-warehouse-develop-dynamic-sql.md

<!--MSDN references-->

<!--Other Web references-->
