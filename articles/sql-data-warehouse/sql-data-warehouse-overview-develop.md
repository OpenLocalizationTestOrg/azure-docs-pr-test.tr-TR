---
title: "Azure veri ambarında geliştirmek için aaaResources | Microsoft Docs"
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
ms.openlocfilehash: 67e3a6a3e2664919c3445ea5d5eba251054de020
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="design-decisions-and-coding-techniques-for-sql-data-warehouse"></a><span data-ttu-id="34ee0-103">SQL Data Warehouse için tasarım kararları ve kodlama teknikleri</span><span class="sxs-lookup"><span data-stu-id="34ee0-103">Design decisions and coding techniques for SQL Data Warehouse</span></span>
<span data-ttu-id="34ee0-104">Bu geliştirme makalelere toobetter anlamak temel tasarım kararları, öneriler ve kodlama teknikleri SQL Data Warehouse için göz.</span><span class="sxs-lookup"><span data-stu-id="34ee0-104">Take a look through these development articles toobetter understand key design decisions, recommendations and coding techniques for SQL Data Warehouse.</span></span>

## <a name="key-design-decisions"></a><span data-ttu-id="34ee0-105">Temel tasarım kararları</span><span class="sxs-lookup"><span data-stu-id="34ee0-105">Key design decisions</span></span>
<span data-ttu-id="34ee0-106">Merhaba aşağıdaki makalelere hello temel kavramları ve SQL Data Warehouse kullanarak dağıtılmış veri ambarınız hello geliştirme için toounderstand gerekir tasarım kararları bazıları vurgula:</span><span class="sxs-lookup"><span data-stu-id="34ee0-106">hello following articles highlight some of hello key concepts and design decisions you will need toounderstand for hello development of your distributed data warehouse using SQL Data Warehouse:</span></span>

* <span data-ttu-id="34ee0-107">[bağlantıları][connections]</span><span class="sxs-lookup"><span data-stu-id="34ee0-107">[connections][connections]</span></span>
* <span data-ttu-id="34ee0-108">[Eşzamanlılık][concurrency]</span><span class="sxs-lookup"><span data-stu-id="34ee0-108">[concurrency][concurrency]</span></span>
* <span data-ttu-id="34ee0-109">[işlemler][transactions]</span><span class="sxs-lookup"><span data-stu-id="34ee0-109">[transactions][transactions]</span></span>
* <span data-ttu-id="34ee0-110">[Kullanıcı tanımlı şemaları][user-defined schemas]</span><span class="sxs-lookup"><span data-stu-id="34ee0-110">[user-defined schemas][user-defined schemas]</span></span>
* <span data-ttu-id="34ee0-111">[Tablo dağıtım][table distribution]</span><span class="sxs-lookup"><span data-stu-id="34ee0-111">[table distribution][table distribution]</span></span>
* <span data-ttu-id="34ee0-112">[Tablo dizinlerini][table indexes]</span><span class="sxs-lookup"><span data-stu-id="34ee0-112">[table indexes][table indexes]</span></span>
* <span data-ttu-id="34ee0-113">[Tablo bölümleri][table partitions]</span><span class="sxs-lookup"><span data-stu-id="34ee0-113">[table partitions][table partitions]</span></span>
* <span data-ttu-id="34ee0-114">[CTAS][CTAS]</span><span class="sxs-lookup"><span data-stu-id="34ee0-114">[CTAS][CTAS]</span></span>
* <span data-ttu-id="34ee0-115">[İstatistikleri][statistics]</span><span class="sxs-lookup"><span data-stu-id="34ee0-115">[statistics][statistics]</span></span>

## <a name="development-recommendations-and-coding-techniques"></a><span data-ttu-id="34ee0-116">Geliştirme önerileri ve kodlama teknikleri</span><span class="sxs-lookup"><span data-stu-id="34ee0-116">Development recommendations and coding techniques</span></span>
<span data-ttu-id="34ee0-117">Bu makaleler, belirli kodlama teknikleri, ipuçları ve öneriler SQL veri ambarı geliştirmek için vurgula:</span><span class="sxs-lookup"><span data-stu-id="34ee0-117">These articles highlight specific coding techniques, tips and recommendations for developing your SQL Data Warehouse:</span></span>

* <span data-ttu-id="34ee0-118">[saklı yordamlar][stored procedures]</span><span class="sxs-lookup"><span data-stu-id="34ee0-118">[stored procedures][stored procedures]</span></span>
* <span data-ttu-id="34ee0-119">[etiketleri][labels]</span><span class="sxs-lookup"><span data-stu-id="34ee0-119">[labels][labels]</span></span>
* <span data-ttu-id="34ee0-120">[Görünümler][views]</span><span class="sxs-lookup"><span data-stu-id="34ee0-120">[views][views]</span></span>
* <span data-ttu-id="34ee0-121">[geçici tablolar][temporary tables]</span><span class="sxs-lookup"><span data-stu-id="34ee0-121">[temporary tables][temporary tables]</span></span>
* <span data-ttu-id="34ee0-122">[dinamik SQL][dynamic SQL]</span><span class="sxs-lookup"><span data-stu-id="34ee0-122">[dynamic SQL][dynamic SQL]</span></span>
* <span data-ttu-id="34ee0-123">[döngü][looping]</span><span class="sxs-lookup"><span data-stu-id="34ee0-123">[looping][looping]</span></span>
* <span data-ttu-id="34ee0-124">[Gruplandırma seçenekleri][group by options]</span><span class="sxs-lookup"><span data-stu-id="34ee0-124">[group by options][group by options]</span></span>
* <span data-ttu-id="34ee0-125">[değişken ataması][variable assignment]</span><span class="sxs-lookup"><span data-stu-id="34ee0-125">[variable assignment][variable assignment]</span></span>

## <a name="next-steps"></a><span data-ttu-id="34ee0-126">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="34ee0-126">Next steps</span></span>
<span data-ttu-id="34ee0-127">Merhaba geliştirme makalelerine işlendikten sonra hello aracılığıyla göz [Transact-SQL Başvurusu] [ Transact-SQL reference] SQL Data Warehouse için desteklenen hello sözdizimi hakkında daha fazla ayrıntı için sayfa.</span><span class="sxs-lookup"><span data-stu-id="34ee0-127">Once you have been through hello development articles take a look through hello [Transact-SQL reference][Transact-SQL reference] page for more details on hello supported syntax for SQL Data Warehouse.</span></span>

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
