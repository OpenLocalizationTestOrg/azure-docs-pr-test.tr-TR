---
title: "aaaLeverage T-SQL Azure SQL Data Warehouse'da döngü | Microsoft Docs"
description: "Transact-SQL döngüler ve çözümleri geliştirmek için Azure SQL Data Warehouse değiştirerek imleçler için ipuçları."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: f3384b81-b943-431b-bc73-90e47e4c195f
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: c7e8f71b910d00d0dfc30f6e5eba190fd05014b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="loops-in-sql-data-warehouse"></a><span data-ttu-id="9f22c-103">SQL Data warehouse'da döngüler</span><span class="sxs-lookup"><span data-stu-id="9f22c-103">Loops in SQL Data Warehouse</span></span>
<span data-ttu-id="9f22c-104">SQL veri ambarı destekleyen hello [sırada][sırada] art arda deyim blokları yürütmek döngü.</span><span class="sxs-lookup"><span data-stu-id="9f22c-104">SQL Data Warehouse supports hello [WHILE][WHILE] loop for repeatedly executing statement blocks.</span></span> <span data-ttu-id="9f22c-105">Koşullar doğru olduğunda Hello belirtilen sürece veya kadar hello kod özellikle hello kullanarak hello döngü sonlandırır için devam eder `BREAK` anahtar sözcüğü.</span><span class="sxs-lookup"><span data-stu-id="9f22c-105">This will continue for as long as hello specified conditions are true or until hello code specifically terminates hello loop using hello `BREAK` keyword.</span></span> <span data-ttu-id="9f22c-106">Döngüler SQL kod içinde tanımlanan imleçler değiştirme için özellikle yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="9f22c-106">Loops are particularly useful for replacing cursors defined in SQL code.</span></span> <span data-ttu-id="9f22c-107">Neyse ki, SQL kodda yazılır neredeyse tüm imleçler Merhaba Hızlı İleri, yalnızca çeşitli salt okunurdur.</span><span class="sxs-lookup"><span data-stu-id="9f22c-107">Fortunately, almost all cursors that are written in SQL code are of hello fast forward, read only variety.</span></span> <span data-ttu-id="9f22c-108">Bu nedenle [sırada] döngüler kendinizi tooreplace bir sahip bulursanız mükemmel bir alternatif olan.</span><span class="sxs-lookup"><span data-stu-id="9f22c-108">Therefore [WHILE] loops are a great alternative if you find yourself having tooreplace one.</span></span>

## <a name="leveraging-loops-and-replacing-cursors-in-sql-data-warehouse"></a><span data-ttu-id="9f22c-109">Döngüler yararlanan ve SQL Data Warehouse imleçler değiştirme</span><span class="sxs-lookup"><span data-stu-id="9f22c-109">Leveraging loops and replacing cursors in SQL Data Warehouse</span></span>
<span data-ttu-id="9f22c-110">Ancak, head ilk girmeden önce kendinize sorun hello Soru: "Bu imleç olabilir yeniden yazılı toouse ayarlama işlemleri göre mi?".</span><span class="sxs-lookup"><span data-stu-id="9f22c-110">However, before diving in head first you should ask yourself hello following question: "Could this cursor be re-written toouse set based operations?".</span></span> <span data-ttu-id="9f22c-111">Çoğu durumda hello yanıt Evet olacaktır ve genellikle hello en iyi yaklaşımdır.</span><span class="sxs-lookup"><span data-stu-id="9f22c-111">In many cases hello answer will be yes and is often hello best approach.</span></span> <span data-ttu-id="9f22c-112">Temel ayarlama işlemi genellikle yinelemeli, satır temelinde bir yaklaşım daha önemli ölçüde daha hızlı gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="9f22c-112">A set based operation often performs significantly faster than an iterative, row by row approach.</span></span>

<span data-ttu-id="9f22c-113">İleri Sarma salt okunur imleçler, döngü yapısı ile kolayca değiştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="9f22c-113">Fast forward read-only cursors can be easily replaced with a looping construct.</span></span> <span data-ttu-id="9f22c-114">Basit bir örnek aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="9f22c-114">Below is a simple example.</span></span> <span data-ttu-id="9f22c-115">Bu kod örneği hello veritabanındaki her tablo için hello istatistiklerini güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="9f22c-115">This code example updates hello statistics for every table in hello database.</span></span> <span data-ttu-id="9f22c-116">Yineleme hello döngü hello tablolarda üzerinden biz tarafından mümkün tooexecute olan her bir komut dizisi.</span><span class="sxs-lookup"><span data-stu-id="9f22c-116">By iterating over hello tables in hello loop we are able tooexecute each command in sequence.</span></span>

<span data-ttu-id="9f22c-117">İlk olarak, bir benzersiz bir satır numarası kullanılan tooidentify hello tek tek deyimleri içeren geçici bir tablo oluşturun:</span><span class="sxs-lookup"><span data-stu-id="9f22c-117">First, create a temporary table containing a unique row number used tooidentify hello individual statements:</span></span>

```
CREATE TABLE #tbl
WITH
( DISTRIBUTION = ROUND_ROBIN
)
AS
SELECT  ROW_NUMBER() OVER(ORDER BY (SELECT NULL)) AS Sequence
,       [name]
,       'UPDATE STATISTICS '+QUOTENAME([name]) AS sql_code
FROM    sys.tables
;
```

<span data-ttu-id="9f22c-118">İkinci olarak, hello değişkenleri gerekli tooperform hello döngü başlatılamadı:</span><span class="sxs-lookup"><span data-stu-id="9f22c-118">Second, initialize hello variables required tooperform hello loop:</span></span>

```
DECLARE @nbr_statements INT = (SELECT COUNT(*) FROM #tbl)
,       @i INT = 1
;
```

<span data-ttu-id="9f22c-119">Şimdi bir yürütme deyimleri döngü birer birer:</span><span class="sxs-lookup"><span data-stu-id="9f22c-119">Now loop over statements executing them one at a time:</span></span>

```
WHILE   @i <= @nbr_statements
BEGIN
    DECLARE @sql_code NVARCHAR(4000) = (SELECT sql_code FROM #tbl WHERE Sequence = @i);
    EXEC    sp_executesql @sql_code;
    SET     @i +=1;
END
```

<span data-ttu-id="9f22c-120">Son olarak hello ilk adımda oluşturduğunuz hello geçici tablo bırakma</span><span class="sxs-lookup"><span data-stu-id="9f22c-120">Finally drop hello temporary table created in hello first step</span></span>

```
DROP TABLE #tbl;
```


<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->

## <a name="next-steps"></a><span data-ttu-id="9f22c-121">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9f22c-121">Next steps</span></span>
<span data-ttu-id="9f22c-122">Daha fazla geliştirme ipuçları için bkz: [geliştirmeye genel bakış][development overview].</span><span class="sxs-lookup"><span data-stu-id="9f22c-122">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[sırada]: https://msdn.microsoft.com/library/ms178642.aspx


<!--Other Web references-->
