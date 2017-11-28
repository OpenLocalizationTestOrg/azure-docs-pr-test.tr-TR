---
title: "aaaPause, Sürdür, ölçeği T-SQL Azure SQL veri ambarı ile | Microsoft Docs"
description: "Dwu ayarlayarak görevleri tooscale kullanıma performans transact-SQL (T-SQL). Yoğun olmayan saatlerde ölçeklendirme tarafından maliyet tasarrufu."
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: jhubbard
editor: 
ms.assetid: a970d939-2adf-4856-8a78-d4fe8ab2cceb
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 03/30/2017
ms.author: elbutter;barbkess
ms.openlocfilehash: 84c6868acb673221d8853319ac9a05bb98b2b7c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-compute-power-in-azure-sql-data-warehouse-t-sql"></a><span data-ttu-id="5eef0-104">Azure SQL Data warehouse'da (T-SQL) işlem güç yönetimi</span><span class="sxs-lookup"><span data-stu-id="5eef0-104">Manage compute power in Azure SQL Data Warehouse (T-SQL)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5eef0-105">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="5eef0-105">Overview</span></span>](sql-data-warehouse-manage-compute-overview.md)
> * [<span data-ttu-id="5eef0-106">Portal</span><span class="sxs-lookup"><span data-stu-id="5eef0-106">Portal</span></span>](sql-data-warehouse-manage-compute-portal.md)
> * [<span data-ttu-id="5eef0-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5eef0-107">PowerShell</span></span>](sql-data-warehouse-manage-compute-powershell.md)
> * [<span data-ttu-id="5eef0-108">REST</span><span class="sxs-lookup"><span data-stu-id="5eef0-108">REST</span></span>](sql-data-warehouse-manage-compute-rest-api.md)
> * [<span data-ttu-id="5eef0-109">TSQL</span><span class="sxs-lookup"><span data-stu-id="5eef0-109">TSQL</span></span>](sql-data-warehouse-manage-compute-tsql.md)
>
>

<a name="current-dwu-bk"></a>

## <a name="view-current-dwu-settings"></a><span data-ttu-id="5eef0-110">Geçerli DWU ayarlarını görüntüle</span><span class="sxs-lookup"><span data-stu-id="5eef0-110">View current DWU settings</span></span>
<span data-ttu-id="5eef0-111">tooview hello geçerli DWU ayarlarına veritabanlarınız için:</span><span class="sxs-lookup"><span data-stu-id="5eef0-111">tooview hello current DWU settings for your databases:</span></span>

1. <span data-ttu-id="5eef0-112">SQL Server Nesne Gezgini Visual Studio'da açın.</span><span class="sxs-lookup"><span data-stu-id="5eef0-112">Open SQL Server Object Explorer in Visual Studio.</span></span>
2. <span data-ttu-id="5eef0-113">Merhaba mantıksal SQL veritabanı sunucusu ile ilişkili toohello ana veritabanına bağlanın.</span><span class="sxs-lookup"><span data-stu-id="5eef0-113">Connect toohello master database associated with hello logical SQL Database server.</span></span>
3. <span data-ttu-id="5eef0-114">Merhaba sys.database_service_objectives dinamik yönetim görünümünden seçin.</span><span class="sxs-lookup"><span data-stu-id="5eef0-114">Select from hello sys.database_service_objectives dynamic management view.</span></span> <span data-ttu-id="5eef0-115">Örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="5eef0-115">Here is an example:</span></span> 

```sql
SELECT
    db.name [Database]
,   ds.edition [Edition]
,   ds.service_objective [Service Objective]
FROM
    sys.database_service_objectives ds
JOIN
    sys.databases db ON ds.database_id = db.database_id
```

<a name="scale-dwu-bk"></a>
<a name="scale-compute-bk"></a>

## <a name="scale-compute"></a><span data-ttu-id="5eef0-116">Bilgi işlem</span><span class="sxs-lookup"><span data-stu-id="5eef0-116">Scale compute</span></span>
[!INCLUDE [SQL Data Warehouse scale DWUs description](../../includes/sql-data-warehouse-scale-dwus-description.md)]

<span data-ttu-id="5eef0-117">toochange hello Dwu:</span><span class="sxs-lookup"><span data-stu-id="5eef0-117">toochange hello DWUs:</span></span>

1. <span data-ttu-id="5eef0-118">Mantıksal SQL veritabanı sunucunuzla ilişkili toohello ana veritabanına bağlanın.</span><span class="sxs-lookup"><span data-stu-id="5eef0-118">Connect toohello master database associated with your logical SQL Database server.</span></span>
2. <span data-ttu-id="5eef0-119">Kullanım hello [ALTER DATABASE] [ ALTER DATABASE] TSQL deyimi.</span><span class="sxs-lookup"><span data-stu-id="5eef0-119">Use hello [ALTER DATABASE][ALTER DATABASE] TSQL statement.</span></span> <span data-ttu-id="5eef0-120">Merhaba aşağıdaki örnek hello hizmet düzeyi hedefi tooDW1000 hello veritabanı MySQLDW için ayarlar.</span><span class="sxs-lookup"><span data-stu-id="5eef0-120">hello following example sets hello service level objective tooDW1000 for hello database MySQLDW.</span></span> 

```Sql
ALTER DATABASE MySQLDW
MODIFY (SERVICE_OBJECTIVE = 'DW1000')
;
```

<a name="check-database-state-bk"></a>

## <a name="check-database-state-and-operation-progress"></a><span data-ttu-id="5eef0-121">Veritabanı durumunda ve işlem ilerleme durumunu denetleme</span><span class="sxs-lookup"><span data-stu-id="5eef0-121">Check database state and operation progress</span></span>

1. <span data-ttu-id="5eef0-122">Mantıksal SQL veritabanı sunucunuzla ilişkili toohello ana veritabanına bağlanın.</span><span class="sxs-lookup"><span data-stu-id="5eef0-122">Connect toohello master database associated with your logical SQL Database server.</span></span>
2. <span data-ttu-id="5eef0-123">Sorgu toocheck veritabanı durumu Gönder</span><span class="sxs-lookup"><span data-stu-id="5eef0-123">Submit query toocheck database state</span></span>

```sql
SELECT *
FROM
sys.databases
```

3. <span data-ttu-id="5eef0-124">Sorgu toocheck işlemin durumunu Gönder</span><span class="sxs-lookup"><span data-stu-id="5eef0-124">Submit query toocheck status of operation</span></span>

```sql
SELECT *
FROM
    sys.dm_operation_status
WHERE
    resource_type_desc = 'Database'
AND 
    major_resource_id = 'MySQLDW'
```

<span data-ttu-id="5eef0-125">Bu DMV SQL veri ambarı tamamlandı veya IN_PROGRESS olacaktır hello işlemi hello işlemi ve hello durumu gibi çeşitli yönetim işlemlerini hakkında bilgi döndürür.</span><span class="sxs-lookup"><span data-stu-id="5eef0-125">This DMV will return information about various management operations on your SQL Data Warehouse such as hello operation and hello state of hello operation, which will either be IN_PROGRESS or COMPLETED.</span></span>



<a name="next-steps-bk"></a>

## <a name="next-steps"></a><span data-ttu-id="5eef0-126">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5eef0-126">Next steps</span></span>
<span data-ttu-id="5eef0-127">Diğer yönetim görevleri için bkz: [yönetimine genel bakış][Management overview].</span><span class="sxs-lookup"><span data-stu-id="5eef0-127">For other management tasks, see [Management overview][Management overview].</span></span>

<!--Image references-->

<!--Article references-->
[Service capacity limits]: ./sql-data-warehouse-service-capacity-limits.md
[Management overview]: ./sql-data-warehouse-overview-manage.md
[Manage compute power overview]: ./sql-data-warehouse-manage-compute-overview.md

<!--MSDN references-->

[ALTER DATABASE]: https://msdn.microsoft.com/library/mt204042.aspx


<!--Other Web references-->

[Azure portal]: http://portal.azure.com/
