---
title: "SQL veri ambarı değişkenlerde Ata | Microsoft Docs"
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
ms.openlocfilehash: 045d5148cd3f12dac63c961ccf7c953d355ed725
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="assign-variables-in-sql-data-warehouse"></a><span data-ttu-id="a8c24-103">SQL veri ambarı değişkenlerde atayın</span><span class="sxs-lookup"><span data-stu-id="a8c24-103">Assign variables in SQL Data Warehouse</span></span>
<span data-ttu-id="a8c24-104">SQL veri ambarı değişkenleri kullanılarak ayarlanır `DECLARE` deyimi veya `SET` deyimi.</span><span class="sxs-lookup"><span data-stu-id="a8c24-104">Variables in SQL Data Warehouse are set using the `DECLARE` statement or the `SET` statement.</span></span>

<span data-ttu-id="a8c24-105">Aşağıdakilerin tümü bir değişken değerini ayarlamak için mükemmel geçerli yöntemlerdir:</span><span class="sxs-lookup"><span data-stu-id="a8c24-105">All of the following are perfectly valid ways to set a variable value:</span></span>

## <a name="setting-variables-with-declare"></a><span data-ttu-id="a8c24-106">DECLARE değişkenlerle ayarlama</span><span class="sxs-lookup"><span data-stu-id="a8c24-106">Setting variables with DECLARE</span></span>
<span data-ttu-id="a8c24-107">DECLARE değişkenlerle başlatılıyor SQL veri ambarı'nda bir değişken değerini ayarlamak için en esnek yollardan biridir.</span><span class="sxs-lookup"><span data-stu-id="a8c24-107">Initializing variables with DECLARE is one of the most flexible ways to set a variable value in SQL Data Warehouse.</span></span>

```sql
DECLARE @v  int = 0
;
```

<span data-ttu-id="a8c24-108">DECLARE, aynı anda birden fazla değişken ayarlamak üzere de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a8c24-108">You can also use DECLARE to set more than one variable at a time.</span></span> <span data-ttu-id="a8c24-109">Kullanamazsınız `SELECT` veya `UPDATE` Bunu yapmak için:</span><span class="sxs-lookup"><span data-stu-id="a8c24-109">You cannot use `SELECT` or `UPDATE` to do this:</span></span>

```sql
DECLARE @v  INT = (SELECT TOP 1 c_customer_sk FROM Customer where c_last_name = 'Smith')
,       @v1 INT = (SELECT TOP 1 c_customer_sk FROM Customer where c_last_name = 'Jones')
;
```

<span data-ttu-id="a8c24-110">İnitialise ve bir değişkeni aynı DECLARE deyimi kullanın.</span><span class="sxs-lookup"><span data-stu-id="a8c24-110">You cannot initialise and use a variable in the same DECLARE statement.</span></span> <span data-ttu-id="a8c24-111">Aşağıdaki örnekte olduğu noktası göstermeye **değil** izin @p1 hem başlatılır ve aynı DECLARE deyiminde kullanılan.</span><span class="sxs-lookup"><span data-stu-id="a8c24-111">To illustrate the point the example below is **not** allowed as @p1 is both initialized and used in the same DECLARE statement.</span></span> <span data-ttu-id="a8c24-112">Bu bir hatayla sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="a8c24-112">This will result in an error.</span></span>

```sql
DECLARE @p1 int = 0
,       @p2 int = (SELECT COUNT (*) FROM sys.types where is_user_defined = @p1 )
;
```

## <a name="setting-values-with-set"></a><span data-ttu-id="a8c24-113">SET değerleri ayarlama</span><span class="sxs-lookup"><span data-stu-id="a8c24-113">Setting values with SET</span></span>
<span data-ttu-id="a8c24-114">Kümesi, tek bir değişken ayarlamak için yaygın bir yöntemdir.</span><span class="sxs-lookup"><span data-stu-id="a8c24-114">Set is a very common method for setting a single variable.</span></span>

<span data-ttu-id="a8c24-115">Tüm örnekler kümesine sahip bir değişken ayarı geçerli yöntemler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="a8c24-115">All of the examples below are valid ways of setting a variable with SET:</span></span>

```sql
SET     @v = (Select max(database_id) from sys.databases);
SET     @v = 1;
SET     @v = @v+1;
SET     @v +=1;
```

<span data-ttu-id="a8c24-116">KÜMESİYLE aynı anda yalnızca bir değişken ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a8c24-116">You can only set one variable at a time with SET.</span></span> <span data-ttu-id="a8c24-117">Ancak, yukarıda görüldüğü gibi bileşik işleçler kabul edilebilir değildir.</span><span class="sxs-lookup"><span data-stu-id="a8c24-117">However, as can be seen above compound operators are permissable.</span></span>

## <a name="limitations"></a><span data-ttu-id="a8c24-118">Sınırlamalar</span><span class="sxs-lookup"><span data-stu-id="a8c24-118">Limitations</span></span>
<span data-ttu-id="a8c24-119">Değişken ataması için SELECT veya UPDATE kullanamazsınız.</span><span class="sxs-lookup"><span data-stu-id="a8c24-119">You cannot use SELECT or UPDATE for variable assignment.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a8c24-120">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a8c24-120">Next steps</span></span>
<span data-ttu-id="a8c24-121">Daha fazla geliştirme ipuçları için bkz: [geliştirmeye genel bakış][development overview].</span><span class="sxs-lookup"><span data-stu-id="a8c24-121">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->

<!--Other Web references-->
