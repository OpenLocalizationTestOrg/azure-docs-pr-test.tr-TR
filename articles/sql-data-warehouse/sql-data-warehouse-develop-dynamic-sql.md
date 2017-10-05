---
title: "SQL veri ambarı dinamik SQL'de | Microsoft Docs"
description: "Çözümleri geliştirme için Azure SQL Data Warehouse'da dinamik SQL kullanma ipuçları."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: a948c2c3-3cd1-4373-90a9-79e59414b778
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: queries
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 29228676373aee8dbc7b1b2a7d92ffc978333804
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="dynamic-sql-in-sql-data-warehouse"></a><span data-ttu-id="ee16a-103">SQL veri ambarı dinamik SQL</span><span class="sxs-lookup"><span data-stu-id="ee16a-103">Dynamic SQL in SQL Data Warehouse</span></span>
<span data-ttu-id="ee16a-104">SQL Data Warehouse için uygulama kodu geliştirirken, esnek, genel ve modüler çözümler sunmak amacıyla dinamik sql kullanmanız gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="ee16a-104">When developing application code for SQL Data Warehouse you may need to use dynamic sql to help deliver flexible, generic and modular solutions.</span></span> <span data-ttu-id="ee16a-105">SQL veri ambarı blob veri türleri şu anda desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="ee16a-105">SQL Data Warehouse does not support blob data types at this time.</span></span> <span data-ttu-id="ee16a-106">Varchar(max) ve nvarchar(max) türlerini BLOB türler gibi bu dizelerinizi boyutunu sınırlayabilir.</span><span class="sxs-lookup"><span data-stu-id="ee16a-106">This may limit the size of your strings as blob types include both varchar(max) and nvarchar(max) types.</span></span> <span data-ttu-id="ee16a-107">Çok büyük dizeleri oluştururken, uygulama kodunuzda bu tür kullandıysanız, kodu parçalara Böl ve EXEC deyimi kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ee16a-107">If you have used these types in your application code when building very large strings, you will need to break the code into chunks and use the EXEC statement instead.</span></span>

<span data-ttu-id="ee16a-108">Basit bir örnek:</span><span class="sxs-lookup"><span data-stu-id="ee16a-108">A simple example:</span></span>

```sql
DECLARE @sql_fragment1 VARCHAR(8000)=' SELECT name '
,       @sql_fragment2 VARCHAR(8000)=' FROM sys.system_views '
,       @sql_fragment3 VARCHAR(8000)=' WHERE name like ''%table%''';

EXEC( @sql_fragment1 + @sql_fragment2 + @sql_fragment3);
```

<span data-ttu-id="ee16a-109">Dize kısaysa kullanabileceğiniz [sp_executesql] [ sp_executesql] normal olarak.</span><span class="sxs-lookup"><span data-stu-id="ee16a-109">If the string is short you can use [sp_executesql][sp_executesql] as normal.</span></span>

> [!NOTE]
> <span data-ttu-id="ee16a-110">Yürütülen dinamik SQL deyimleri tüm TSQL doğrulama kurallarını tabi olmaya devam eder.</span><span class="sxs-lookup"><span data-stu-id="ee16a-110">Statements executed as dynamic SQL will still be subject to all TSQL validation rules.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="ee16a-111">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ee16a-111">Next steps</span></span>
<span data-ttu-id="ee16a-112">Daha fazla geliştirme ipuçları için bkz: [geliştirmeye genel bakış][development overview].</span><span class="sxs-lookup"><span data-stu-id="ee16a-112">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[sp_executesql]: https://msdn.microsoft.com/library/ms188001.aspx

<!--Other Web references-->
