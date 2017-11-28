---
title: "Duraklatma, sürdürme, ölçeklendirme ile Azure SQL Data Warehouse, KALAN | Microsoft Docs"
description: "İşlem gücü SQL Data warehouse'da REST, T-SQL ve PowerShell aracılığıyla yönetin."
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: johnmac
editor: 
ms.assetid: 21de7337-9356-49bb-a6eb-06c1beeba2c4
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 07/25/2017
ms.author: elbutter
ms.openlocfilehash: 24e43205c0c562fca9b1c2c0e5eed4da54e17ed7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="manage-compute-power-in-azure-sql-data-warehouse-rest"></a><span data-ttu-id="b9a46-103">İşlem güç Azure SQL veri ambarı (REST) yönetme</span><span class="sxs-lookup"><span data-stu-id="b9a46-103">Manage compute power in Azure SQL Data Warehouse (REST)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b9a46-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="b9a46-104">Overview</span></span>](sql-data-warehouse-manage-compute-overview.md)
> * [<span data-ttu-id="b9a46-105">Portal</span><span class="sxs-lookup"><span data-stu-id="b9a46-105">Portal</span></span>](sql-data-warehouse-manage-compute-portal.md)
> * [<span data-ttu-id="b9a46-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b9a46-106">PowerShell</span></span>](sql-data-warehouse-manage-compute-powershell.md)
> * [<span data-ttu-id="b9a46-107">REST</span><span class="sxs-lookup"><span data-stu-id="b9a46-107">REST</span></span>](sql-data-warehouse-manage-compute-rest-api.md)
> * [<span data-ttu-id="b9a46-108">TSQL</span><span class="sxs-lookup"><span data-stu-id="b9a46-108">TSQL</span></span>](sql-data-warehouse-manage-compute-tsql.md)
>
>

<a name="scale-performance-bk"></a>
<a name="scale-compute-bk"></a>

## <a name="scale-compute-power"></a><span data-ttu-id="b9a46-109">Ölçek işlem gücü</span><span class="sxs-lookup"><span data-stu-id="b9a46-109">Scale compute power</span></span>
[!INCLUDE [SQL Data Warehouse scale DWUs description](../../includes/sql-data-warehouse-scale-dwus-description.md)]

<span data-ttu-id="b9a46-110">Dwu değiştirmek için kullanın [oluşturma veya güncelleştirme veritabanı] [ Create or Update Database] REST API.</span><span class="sxs-lookup"><span data-stu-id="b9a46-110">To change the DWUs, use the [Create or Update Database][Create or Update Database] REST API.</span></span> <span data-ttu-id="b9a46-111">Aşağıdaki örnek, MyServer sunucusunda barındırılan MySQLDW veritabanı için DW1000 için hizmet düzeyi hedefi ayarlar.</span><span class="sxs-lookup"><span data-stu-id="b9a46-111">The following example sets the service level objective to DW1000 for the database MySQLDW which is hosted on server MyServer.</span></span> <span data-ttu-id="b9a46-112">Sunucu ResourceGroup1 adlı bir Azure kaynak grubunda yer alıyor.</span><span class="sxs-lookup"><span data-stu-id="b9a46-112">The server is in an Azure resource group named ResourceGroup1.</span></span>

```
PATCH https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Sql/servers/{server-name}/databases/{database-name}?api-version=2014-04-01-preview HTTP/1.1
Content-Type: application/json; charset=UTF-8

{
    "properties": {
        "requestedServiceObjectiveName": DW1000
    }
}
```

<a name="pause-compute-bk"></a>

## <a name="pause-compute"></a><span data-ttu-id="b9a46-113">Duraklatma işlem</span><span class="sxs-lookup"><span data-stu-id="b9a46-113">Pause compute</span></span>
[!INCLUDE [SQL Data Warehouse pause description](../../includes/sql-data-warehouse-pause-description.md)]

<span data-ttu-id="b9a46-114">Bir veritabanı duraklatmak için kullanmak [duraklatma veritabanı] [ Pause Database] REST API.</span><span class="sxs-lookup"><span data-stu-id="b9a46-114">To pause a database, use the [Pause Database][Pause Database] REST API.</span></span> <span data-ttu-id="b9a46-115">Aşağıdaki örnek Server01 adlı bir sunucuda barındırılan Database02 adlı bir veritabanı duraklatır.</span><span class="sxs-lookup"><span data-stu-id="b9a46-115">The following example pauses a database named Database02 hosted on a server named Server01.</span></span> <span data-ttu-id="b9a46-116">Sunucu ResourceGroup1 adlı bir Azure kaynak grubunda yer alıyor.</span><span class="sxs-lookup"><span data-stu-id="b9a46-116">The server is in an Azure resource group named ResourceGroup1.</span></span>

```
POST https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Sql/servers/{server-name}/databases/{database-name}/pause?api-version=2014-04-01-preview HTTP/1.1
```

<a name="resume-compute-bk"></a>

## <a name="resume-compute"></a><span data-ttu-id="b9a46-117">Resume işlem</span><span class="sxs-lookup"><span data-stu-id="b9a46-117">Resume compute</span></span>
[!INCLUDE [SQL Data Warehouse resume description](../../includes/sql-data-warehouse-resume-description.md)]

<span data-ttu-id="b9a46-118">Bir veritabanı başlatmak için kullanmak [Sürdür veritabanı] [ Resume Database] REST API.</span><span class="sxs-lookup"><span data-stu-id="b9a46-118">To start a database, use the [Resume Database][Resume Database] REST API.</span></span> <span data-ttu-id="b9a46-119">Aşağıdaki örnek Server01 adlı bir sunucuda barındırılan Database02 adlı bir veritabanı başlatır.</span><span class="sxs-lookup"><span data-stu-id="b9a46-119">The following example starts a database named Database02 hosted on a server named Server01.</span></span> <span data-ttu-id="b9a46-120">Sunucu ResourceGroup1 adlı bir Azure kaynak grubunda yer alıyor.</span><span class="sxs-lookup"><span data-stu-id="b9a46-120">The server is in an Azure resource group named ResourceGroup1.</span></span> 

```
POST https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Sql/servers/{server-name}/databases/{database-name}/resume?api-version=2014-04-01-preview HTTP/1.1
```

## <a name="check-database-state"></a><span data-ttu-id="b9a46-121">Veritabanı durumunu kontrol edin</span><span class="sxs-lookup"><span data-stu-id="b9a46-121">Check database state</span></span>

```
GET https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Sql/servers/{server-name}/databases/{database-name}?api-version=2014-04-01 HTTP/1.1
```

<a name="next-steps-bk"></a>

## <a name="next-steps"></a><span data-ttu-id="b9a46-122">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b9a46-122">Next steps</span></span>
<span data-ttu-id="b9a46-123">Diğer yönetim görevleri için bkz: [yönetimine genel bakış][Management overview].</span><span class="sxs-lookup"><span data-stu-id="b9a46-123">For other management tasks, see [Management overview][Management overview].</span></span>

<!--Image references-->

<!--Article references-->
[Management overview]: ./sql-data-warehouse-overview-manage.md
[Manage compute overview]: ./sql-data-warehouse-manage-compute-overview.md

<!--MSDN references-->
[Pause Database]: https://msdn.microsoft.com/library/azure/mt718817.aspx
[Resume Database]: https://msdn.microsoft.com/library/azure/mt718820.aspx
[Create or Update Database]: https://msdn.microsoft.com/library/azure/mt163685.aspx

<!--Other Web references-->

[Azure portal]: http://portal.azure.com/
