---
title: "aaaMigrate SQL kodu tooSQL veri ambarı | Microsoft Docs"
description: "SQL geçirmek için ipuçları tooAzure SQL Data Warehouse çözümleri geliştirmek için kod."
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
ms.openlocfilehash: 7a16d579d068e9df9aba3dc61e4a09bcaa551588
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-sql-code-toosql-data-warehouse"></a>SQL kod tooSQL veri ambarına geçirme
Bu makalede, büyük olasılıkla toomake kodunuzun başka bir veritabanı tooSQL veri ambarı geçirilirken gerekir kod değişiklikleri açıklanmaktadır. Dağıtılmış bir şekilde tasarlanmış toowork oldukları gibi bazı SQL veri ambarı özellikleri önemli ölçüde performansını iyileştirebilir. Ancak, toomaintain performansı ve ölçeği, bazı özellikler de kullanılamaz.

## <a name="common-t-sql-limitations"></a>Ortak T-SQL sınırlamaları
liste aşağıdaki hello SQL Data Warehouse desteklemediği hello en yaygın özellikler özetlenmektedir. Merhaba bağlantılar hello desteklenmeyen özellikler için tooworkarounds götürür:

* [ANSI birleştirmeler güncelleştirmeleri][ANSI joins on updates]
* [ANSI birleştirmeler üzerinde siler][ANSI joins on deletes]
* [Merge deyimi][merge statement]
* veritabanları arası birleşimler
* [imleçler][cursors]
* [EKLE... EXEC][INSERT..EXEC]
* Output yan tümcesi
* Satır içi kullanıcı tanımlı işlevler
* birden fazla deyim işlevleri
* [Ortak tablo ifadeleri](#Common-table-expressions)
* [özyinelemeli ortak tablo ifadeleri (CTE)] (#Recursive-common-table-expressions-(CTE)
* CLR işlevleri ve yordamları
* $partition işlevi
* Tablo değişkenleri
* Tablo değeri parametreleri
* Dağıtılmış işlemler
* Commit / rollback çalışma
* işlem Kaydet
* yürütme bağlamı (EXECUTE AS)
* [Grup by tümcesi paketi / küp / gruplandırma kümeleri seçenekleri][group by clause with rollup / cube / grouping sets options]
* [iç içe geçme düzeyi 8 ötesinde][nesting levels beyond 8]
* [görünümleri aracılığıyla güncelleştirme][updating through views]
* [değişken ataması için seçimi kullanın][use of select for variable assignment]
* [dinamik SQL dizeleri için hiçbir en büyük veri türü][no MAX data type for dynamic SQL strings]

Neyse ki bu sınırlamalara çoğunu geçici çalışılan. Açıklamalar, yukarıda başvurulan hello ilgili geliştirme makalelerinde sağlanır.

## <a name="supported-cte-features"></a>Desteklenen CTE Özellikler
Ortak tablo ifadelerinde (Cte'lerin) SQL veri ambarı'nda kısmen desteklenir.  şu anda CTE özellikler aşağıdaki hello desteklenir:

* SELECT deyiminde bir CTE belirtilebilir.
* Bir CTE CREATE VIEW deyiminde belirtilebilir.
* Bir CTE oluşturmak tablo AS seçin (CTAS) deyiminde belirtilebilir.
* Bir CTE oluşturma uzak tablo AS seçin (CRTAS) deyiminde belirtilebilir.
* Bir CTE oluşturmak dış tablo AS seçin (CETAS) deyiminde belirtilebilir.
* Bir uzak tablo CTE başvurulabilir.
* Bir dış tablo CTE başvurulabilir.
* Birden fazla CTE sorgu tanımı bir CTE tanımlanabilir.

## <a name="cte-limitations"></a>CTE sınırlamaları
Ortak tablo ifadelerinde SQL Data Warehouse dahil, bazı sınırlamalar vardır:

* Bir CTE tek bir SELECT deyimi tarafından izlenmesi gerekir. INSERT, UPDATE, DELETE ve MERGE deyimleri desteklenmiyor.
* Başvuruları tooitself (bir özyinelemeli ortak tablo ifadesi) içeren bir ortak tablo ifadesi desteklenmiyor (bölüme bakın).
* Birden çok yan tümcesi ile birlikte bir CTE belirtme izin verilmiyor. Bir CTE_query_definition bir alt sorgu içeriyorsa, örneğin, bu alt sorgu iç içe bir başka bir CTE tanımlayan yan tümcesiyle birlikte içeremez.
* TOP yan tümcesi belirtildiğinde ORDER BY yan tümcesi hello CTE_query_definition, dışında kullanılamaz.
* Bir CTE bir toplu iş parçası olan bir deyimde kullanıldığında, kendisinden önce hello deyimi noktalı virgülle gelmelidir.
* Sp_prepare tarafından hazırlanan deyimlerinde kullanıldığında, Cte'lerin hello davranacak PDW diğer SELECT deyimlerinde aynı şekilde. Cte'lerin CETAS sp_prepare tarafından hazırlanan bir parçası olarak kullanılıyorsa, ancak hello davranışı SQL Server ve diğer PDW deyimleri bağlama için sp_prepare uygulanan hello şekilde nedeniyle erteleneceği. SEÇİN, başvuruları CTE içinde yok yanlış bir sütun CTE kullanarak hello sp_prepare hello hata algılama olmadan geçirir, ancak hello hata sırasında sp_execute yerine oluşturulur.

## <a name="recursive-ctes"></a>Özyinelemeli Cte'lerin
Özyinelemeli Cte'lerin SQL veri ambarı'nda desteklenmez.  özyinelemeli CTE Hello geçişini biraz karmaşık olabilir ve hello en iyi işlemdir toobreak içine birden çok adımı. Genellikle, bir döngü kullanın ve geçici bir tablo hello özyinelemeli geçici sorguları yinelemek gibi doldurun. Merhaba geçici tablo doldurulduktan sonra için hello verileri tek bir sonuç kümesi olarak geri dönebilirsiniz. Benzer bir yaklaşım kullanılan toosolve bırakıldı `GROUP BY WITH CUBE` hello içinde [Grup by tümcesi paketi / küp / gruplandırma kümeleri seçenekleri] [ group by clause with rollup / cube / grouping sets options] makalesi.

## <a name="unsupported-system-functions"></a>Desteklenmeyen sistem işlevleri
Desteklenmeyen bazı sistem işlevleri de vardır. Veri ambarı kullanılan genellikle bulabileceğiniz hello ana olanları bazıları şunlardır:

* NEWSEQUENTIALID()
* @@NESTLEVEL()
* @@IDENTITY()
* @@ROWCOUNT()
* ROWCOUNT_BIG
* ERROR_LINE()

Bu sorunlardan bazıları geçici çalışılan.

## <a name="rowcount-workaround"></a>@@ROWCOUNT geçici çözüm
desteğinin geçici toowork@ROWCOUNT, sys.dm_pdw_request_steps hello son satır sayısı almak ve sonra yürütün bir saklı yordam oluşturmak `EXEC LastRowCount` DML deyimi sonra.

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

## <a name="next-steps"></a>Sonraki adımlar
Tüm desteklenen T-SQL deyimlerini tam bir listesi için bkz: [Transact-SQL konuları][Transact-SQL topics].

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
