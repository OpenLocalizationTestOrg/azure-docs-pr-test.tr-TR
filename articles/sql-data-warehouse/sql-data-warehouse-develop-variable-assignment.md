---
title: "SQL veri ambarı aaaAssign değişkenleri | Microsoft Docs"
description: "Çözümleri geliştirme için Azure SQL Data Warehouse Transact-SQL değişkenleri atamak için ipuçları."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: 81ddc7cf-a6ba-4585-91a3-b6ea50f49227
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 9de48739bb0af80ff2a117704b31512c680f78d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="assign-variables-in-sql-data-warehouse"></a><span data-ttu-id="952d8-103">SQL veri ambarı değişkenlerde atayın</span><span class="sxs-lookup"><span data-stu-id="952d8-103">Assign variables in SQL Data Warehouse</span></span>
<span data-ttu-id="952d8-104">SQL veri ambarı değişkenlerde hello kullanılarak ayarlanır `DECLARE` deyimi veya hello `SET` deyimi.</span><span class="sxs-lookup"><span data-stu-id="952d8-104">Variables in SQL Data Warehouse are set using hello `DECLARE` statement or hello `SET` statement.</span></span>

<span data-ttu-id="952d8-105">Tüm hello aşağıdaki mükemmel geçerli yolları tooset bir değişken değeri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="952d8-105">All of hello following are perfectly valid ways tooset a variable value:</span></span>

## <a name="setting-variables-with-declare"></a><span data-ttu-id="952d8-106">DECLARE değişkenlerle ayarlama</span><span class="sxs-lookup"><span data-stu-id="952d8-106">Setting variables with DECLARE</span></span>
<span data-ttu-id="952d8-107">DECLARE değişkenlerle başlatılıyor hello en esnek şekilde tooset SQL Data warehouse'da bir değişken değeri biridir.</span><span class="sxs-lookup"><span data-stu-id="952d8-107">Initializing variables with DECLARE is one of hello most flexible ways tooset a variable value in SQL Data Warehouse.</span></span>

```sql
DECLARE @v  int = 0
;
```

<span data-ttu-id="952d8-108">Bir kerede bir değişken birden çok DECLARE tooset de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="952d8-108">You can also use DECLARE tooset more than one variable at a time.</span></span> <span data-ttu-id="952d8-109">Kullanamazsınız `SELECT` veya `UPDATE` toodo bu:</span><span class="sxs-lookup"><span data-stu-id="952d8-109">You cannot use `SELECT` or `UPDATE` toodo this:</span></span>

```sql
DECLARE @v  INT = (SELECT TOP 1 c_customer_sk FROM Customer where c_last_name = 'Smith')
,       @v1 INT = (SELECT TOP 1 c_customer_sk FROM Customer where c_last_name = 'Jones')
;
```

<span data-ttu-id="952d8-110">İnitialise ve bir değişkeni hello kullanın aynı DECLARE deyimi.</span><span class="sxs-lookup"><span data-stu-id="952d8-110">You cannot initialise and use a variable in hello same DECLARE statement.</span></span> <span data-ttu-id="952d8-111">tooillustrate hello noktası hello örnek aşağıdaki **değil** izin @p1 hem başlatılır ve hello kullanılan aynı DECLARE deyimi.</span><span class="sxs-lookup"><span data-stu-id="952d8-111">tooillustrate hello point hello example below is **not** allowed as @p1 is both initialized and used in hello same DECLARE statement.</span></span> <span data-ttu-id="952d8-112">Bu bir hatayla sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="952d8-112">This will result in an error.</span></span>

```sql
DECLARE @p1 int = 0
,       @p2 int = (SELECT COUNT (*) FROM sys.types where is_user_defined = @p1 )
;
```

## <a name="setting-values-with-set"></a><span data-ttu-id="952d8-113">SET değerleri ayarlama</span><span class="sxs-lookup"><span data-stu-id="952d8-113">Setting values with SET</span></span>
<span data-ttu-id="952d8-114">Kümesi, tek bir değişken ayarlamak için yaygın bir yöntemdir.</span><span class="sxs-lookup"><span data-stu-id="952d8-114">Set is a very common method for setting a single variable.</span></span>

<span data-ttu-id="952d8-115">Tüm hello örneklere kümesine sahip bir değişken ayarlama geçerli yöntemlerdir:</span><span class="sxs-lookup"><span data-stu-id="952d8-115">All of hello examples below are valid ways of setting a variable with SET:</span></span>

```sql
SET     @v = (Select max(database_id) from sys.databases);
SET     @v = 1;
SET     @v = @v+1;
SET     @v +=1;
```

<span data-ttu-id="952d8-116">KÜMESİYLE aynı anda yalnızca bir değişken ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="952d8-116">You can only set one variable at a time with SET.</span></span> <span data-ttu-id="952d8-117">Ancak, yukarıda görüldüğü gibi bileşik işleçler kabul edilebilir değildir.</span><span class="sxs-lookup"><span data-stu-id="952d8-117">However, as can be seen above compound operators are permissable.</span></span>

## <a name="limitations"></a><span data-ttu-id="952d8-118">Sınırlamalar</span><span class="sxs-lookup"><span data-stu-id="952d8-118">Limitations</span></span>
<span data-ttu-id="952d8-119">Değişken ataması için SELECT veya UPDATE kullanamazsınız.</span><span class="sxs-lookup"><span data-stu-id="952d8-119">You cannot use SELECT or UPDATE for variable assignment.</span></span>

## <a name="next-steps"></a><span data-ttu-id="952d8-120">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="952d8-120">Next steps</span></span>
<span data-ttu-id="952d8-121">Daha fazla geliştirme ipuçları için bkz: [geliştirmeye genel bakış][development overview].</span><span class="sxs-lookup"><span data-stu-id="952d8-121">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->

<!--Other Web references-->
