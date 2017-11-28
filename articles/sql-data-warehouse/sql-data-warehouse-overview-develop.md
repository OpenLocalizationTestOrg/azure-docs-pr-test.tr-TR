---
title: "Azure veri ambarında geliştirmek için kaynaklar | Microsoft Docs"
description: "Geliştirme kavramları, tasarım kararları, öneriler ve SQL Data Warehouse için kodlama teknikleri."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: barbkess
editor: 
ms.assetid: 996e3afc-c21c-4e21-b9df-997f953f6dfd
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: develop
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: b85a4f09e561e429aa5bf46ec680014487fb40c7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="design-decisions-and-coding-techniques-for-sql-data-warehouse"></a><span data-ttu-id="8ad83-103">SQL Data Warehouse için tasarım kararları ve kodlama teknikleri</span><span class="sxs-lookup"><span data-stu-id="8ad83-103">Design decisions and coding techniques for SQL Data Warehouse</span></span>
<span data-ttu-id="8ad83-104">SQL Data Warehouse için temel tasarım kararları, öneriler ve kodlama teknikleri daha iyi anlamak için bu geliştirme makalelere göz atın.</span><span class="sxs-lookup"><span data-stu-id="8ad83-104">Take a look through these development articles to better understand key design decisions, recommendations and coding techniques for SQL Data Warehouse.</span></span>

## <a name="key-design-decisions"></a><span data-ttu-id="8ad83-105">Temel tasarım kararları</span><span class="sxs-lookup"><span data-stu-id="8ad83-105">Key design decisions</span></span>
<span data-ttu-id="8ad83-106">Aşağıdaki makaleler bazı temel kavramları ve SQL Data Warehouse kullanarak dağıtılmış veri ambarınız geliştirme için anlamak için gereken tasarım kararlarını vurgula:</span><span class="sxs-lookup"><span data-stu-id="8ad83-106">The following articles highlight some of the key concepts and design decisions you will need to understand for the development of your distributed data warehouse using SQL Data Warehouse:</span></span>

* <span data-ttu-id="8ad83-107">[bağlantıları][connections]</span><span class="sxs-lookup"><span data-stu-id="8ad83-107">[connections][connections]</span></span>
* <span data-ttu-id="8ad83-108">[Eşzamanlılık][concurrency]</span><span class="sxs-lookup"><span data-stu-id="8ad83-108">[concurrency][concurrency]</span></span>
* <span data-ttu-id="8ad83-109">[işlemler][transactions]</span><span class="sxs-lookup"><span data-stu-id="8ad83-109">[transactions][transactions]</span></span>
* <span data-ttu-id="8ad83-110">[Kullanıcı tanımlı şemaları][user-defined schemas]</span><span class="sxs-lookup"><span data-stu-id="8ad83-110">[user-defined schemas][user-defined schemas]</span></span>
* <span data-ttu-id="8ad83-111">[Tablo dağıtım][table distribution]</span><span class="sxs-lookup"><span data-stu-id="8ad83-111">[table distribution][table distribution]</span></span>
* <span data-ttu-id="8ad83-112">[Tablo dizinlerini][table indexes]</span><span class="sxs-lookup"><span data-stu-id="8ad83-112">[table indexes][table indexes]</span></span>
* <span data-ttu-id="8ad83-113">[Tablo bölümleri][table partitions]</span><span class="sxs-lookup"><span data-stu-id="8ad83-113">[table partitions][table partitions]</span></span>
* <span data-ttu-id="8ad83-114">[CTAS][CTAS]</span><span class="sxs-lookup"><span data-stu-id="8ad83-114">[CTAS][CTAS]</span></span>
* <span data-ttu-id="8ad83-115">[İstatistikleri][statistics]</span><span class="sxs-lookup"><span data-stu-id="8ad83-115">[statistics][statistics]</span></span>

## <a name="development-recommendations-and-coding-techniques"></a><span data-ttu-id="8ad83-116">Geliştirme önerileri ve kodlama teknikleri</span><span class="sxs-lookup"><span data-stu-id="8ad83-116">Development recommendations and coding techniques</span></span>
<span data-ttu-id="8ad83-117">Bu makaleler, belirli kodlama teknikleri, ipuçları ve öneriler SQL veri ambarı geliştirmek için vurgula:</span><span class="sxs-lookup"><span data-stu-id="8ad83-117">These articles highlight specific coding techniques, tips and recommendations for developing your SQL Data Warehouse:</span></span>

* <span data-ttu-id="8ad83-118">[saklı yordamlar][stored procedures]</span><span class="sxs-lookup"><span data-stu-id="8ad83-118">[stored procedures][stored procedures]</span></span>
* <span data-ttu-id="8ad83-119">[etiketleri][labels]</span><span class="sxs-lookup"><span data-stu-id="8ad83-119">[labels][labels]</span></span>
* <span data-ttu-id="8ad83-120">[Görünümler][views]</span><span class="sxs-lookup"><span data-stu-id="8ad83-120">[views][views]</span></span>
* <span data-ttu-id="8ad83-121">[geçici tablolar][temporary tables]</span><span class="sxs-lookup"><span data-stu-id="8ad83-121">[temporary tables][temporary tables]</span></span>
* <span data-ttu-id="8ad83-122">[dinamik SQL][dynamic SQL]</span><span class="sxs-lookup"><span data-stu-id="8ad83-122">[dynamic SQL][dynamic SQL]</span></span>
* <span data-ttu-id="8ad83-123">[döngü][looping]</span><span class="sxs-lookup"><span data-stu-id="8ad83-123">[looping][looping]</span></span>
* <span data-ttu-id="8ad83-124">[Gruplandırma seçenekleri][group by options]</span><span class="sxs-lookup"><span data-stu-id="8ad83-124">[group by options][group by options]</span></span>
* <span data-ttu-id="8ad83-125">[değişken ataması][variable assignment]</span><span class="sxs-lookup"><span data-stu-id="8ad83-125">[variable assignment][variable assignment]</span></span>

## <a name="next-steps"></a><span data-ttu-id="8ad83-126">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8ad83-126">Next steps</span></span>
<span data-ttu-id="8ad83-127">Geliştirme makalelerine işlendikten sonra aracılığıyla göz [Transact-SQL Başvurusu] [ Transact-SQL reference] SQL Data Warehouse için desteklenen sözdizimi hakkında daha fazla ayrıntı için sayfa.</span><span class="sxs-lookup"><span data-stu-id="8ad83-127">Once you have been through the development articles take a look through the [Transact-SQL reference][Transact-SQL reference] page for more details on the supported syntax for SQL Data Warehouse.</span></span>

<!--Image references-->

<!--Article references-->
[concurrency]: ./sql-data-warehouse-develop-concurrency.md
[connections]: ./sql-data-warehouse-connect-overview.md
[CTAS]: ./sql-data-warehouse-develop-ctas.md
[dynamic SQL]: ./sql-data-warehouse-develop-dynamic-sql.md
[group by options]: ./sql-data-warehouse-develop-group-by-options.md
[labels]: ./sql-data-warehouse-develop-label.md
[looping]: ./sql-data-warehouse-develop-loops.md
[statistics]: ./sql-data-warehouse-tables-statistics.md
[stored procedures]: ./sql-data-warehouse-develop-stored-procedures.md
[table distribution]: ./sql-data-warehouse-tables-distribute.md
[table indexes]: ./sql-data-warehouse-tables-index.md
[table partitions]: ./sql-data-warehouse-tables-partition.md
[temporary tables]: ./sql-data-warehouse-tables-temporary.md
[transactions]: ./sql-data-warehouse-develop-transactions.md
[user-defined schemas]: ./sql-data-warehouse-develop-user-defined-schemas.md
[variable assignment]: ./sql-data-warehouse-develop-variable-assignment.md
[views]: ./sql-data-warehouse-develop-views.md
[Transact-SQL reference]: ./sql-data-warehouse-overview-reference.md

<!--MSDN references-->
[renaming objects]: https://msdn.microsoft.com/library/mt631611.aspx

<!--Other Web references-->
