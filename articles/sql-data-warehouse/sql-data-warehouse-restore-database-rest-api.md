---
title: aaaRestore Azure SQL Data Warehouse (REST API'si) | Microsoft Docs
description: "Azure SQL Data Warehouse geri yüklemek için REST API görevler."
services: sql-data-warehouse
documentationcenter: NA
author: Lakshmi1812
manager: jhubbard
editor: 
ms.assetid: fca922c6-b675-49c7-907e-5dcf26d451dd
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: backup-restore
ms.date: 10/31/2016
ms.author: lakshmir;barbkess
ms.openlocfilehash: cf6678d71aafff71b1ea715f447e41e25f20d1b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="restore-an-azure-sql-data-warehouse-rest-api"></a><span data-ttu-id="f6864-103">Bir Azure SQL veri ambarı (REST API'si) geri yükleme</span><span class="sxs-lookup"><span data-stu-id="f6864-103">Restore an Azure SQL Data Warehouse (REST API)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="f6864-104">[Genel bakış][Overview]</span><span class="sxs-lookup"><span data-stu-id="f6864-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="f6864-105">[Portal][Portal]</span><span class="sxs-lookup"><span data-stu-id="f6864-105">[Portal][Portal]</span></span>
> * <span data-ttu-id="f6864-106">[PowerShell][PowerShell]</span><span class="sxs-lookup"><span data-stu-id="f6864-106">[PowerShell][PowerShell]</span></span>
> * <span data-ttu-id="f6864-107">[REST][REST]</span><span class="sxs-lookup"><span data-stu-id="f6864-107">[REST][REST]</span></span>
> 
> 

<span data-ttu-id="f6864-108">Bu makalede, REST API kullanarak bir Azure SQL Data Warehouse toorestore hello nasıl öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="f6864-108">In this article you will learn how toorestore an Azure SQL Data Warehouse using hello REST API.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="f6864-109">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="f6864-109">Before you begin</span></span>
<span data-ttu-id="f6864-110">**DTU kapasitenizi doğrulayın.**</span><span class="sxs-lookup"><span data-stu-id="f6864-110">**Verify your DTU capacity.**</span></span> <span data-ttu-id="f6864-111">Her SQL veri ambarı varsayılan DTU kota olan bir SQL server tarafından (örneğin myserver.database.windows.net) barındırılıyor.</span><span class="sxs-lookup"><span data-stu-id="f6864-111">Each SQL Data Warehouse is hosted by a SQL server (e.g. myserver.database.windows.net) which has a default DTU quota.</span></span>  <span data-ttu-id="f6864-112">SQL Data Warehouse geri yüklemeden önce SQL server'ınızdaki hello veritabanı geri yükleniyor için yeterince kalan DTU kota sahip o hello doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="f6864-112">Before you can restore a SQL Data Warehouse, verify that hello your SQL server has enough remaining DTU quota for hello database being restored.</span></span> <span data-ttu-id="f6864-113">toolearn nasıl toocalculate DTU gerekli veya toorequest daha fazla DTU bkz [DTU kota değişiklik isteği][Request a DTU quota change].</span><span class="sxs-lookup"><span data-stu-id="f6864-113">toolearn how toocalculate DTU needed or toorequest more DTU, see [Request a DTU quota change][Request a DTU quota change].</span></span>

## <a name="restore-an-active-or-paused-database"></a><span data-ttu-id="f6864-114">Etkin ya da duraklatılmış bir veritabanını geri yükle</span><span class="sxs-lookup"><span data-stu-id="f6864-114">Restore an active or paused database</span></span>
<span data-ttu-id="f6864-115">bir veritabanı toorestore:</span><span class="sxs-lookup"><span data-stu-id="f6864-115">toorestore a database:</span></span>

1. <span data-ttu-id="f6864-116">Merhaba Get veritabanı geri yükleme noktaları işlemini kullanarak veritabanını geri yükleme noktaları Hello listesini alın.</span><span class="sxs-lookup"><span data-stu-id="f6864-116">Get hello list of database restore points using hello Get Database Restore Points operation.</span></span>
2. <span data-ttu-id="f6864-117">Hello kullanarak geri yüklemenizi başlayın [oluşturma veritabanı geri yükleme isteği] [ Create database restore request] işlemi.</span><span class="sxs-lookup"><span data-stu-id="f6864-117">Begin your restore by using hello [Create database restore request][Create database restore request] operation.</span></span>
3. <span data-ttu-id="f6864-118">Hello kullanarak geri yüklemenizi hello durumunu izlemek [veritabanı işlemi durumunu] [ Database operation status] işlemi.</span><span class="sxs-lookup"><span data-stu-id="f6864-118">Track hello status of your restore by using hello [Database operation status][Database operation status] operation.</span></span>

> [!NOTE]
> <span data-ttu-id="f6864-119">Merhaba geri yükleme tamamlandıktan sonra izleyerek, kurtarılan veritabanının yapılandırabilirsiniz [kurtarma işleminden sonra veritabanını yapılandırma][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="f6864-119">After hello restore has completed, you can configure your recovered database by following [Configure your database after recovery][Configure your database after recovery].</span></span>
> 
> 

## <a name="restore-a-deleted-database"></a><span data-ttu-id="f6864-120">Silinen veritabanını geri yükleme</span><span class="sxs-lookup"><span data-stu-id="f6864-120">Restore a deleted database</span></span>
<span data-ttu-id="f6864-121">Silinen bir veritabanını toorestore:</span><span class="sxs-lookup"><span data-stu-id="f6864-121">toorestore a deleted database:</span></span>

1. <span data-ttu-id="f6864-122">Tüm geri yüklenebilen silinmiş veritabanlarınızın hello kullanarak liste [listesi geri yüklenebilen bırakılan veritabanları] [ List restorable dropped databases] işlemi.</span><span class="sxs-lookup"><span data-stu-id="f6864-122">List all of your restorable deleted databases by using hello [List restorable dropped databases][List restorable dropped databases] operation.</span></span>
2. <span data-ttu-id="f6864-123">Merhaba istediğiniz silinmiş hello veritabanı için toorestore hello kullanarak ayrıntılara [Get geri yüklenebilen bırakılan veritabanı] [ Get restorable dropped database] işlemi.</span><span class="sxs-lookup"><span data-stu-id="f6864-123">Get hello details for hello deleted database you want toorestore by using hello [Get restorable dropped database][Get restorable dropped database] operation.</span></span>
3. <span data-ttu-id="f6864-124">Hello kullanarak geri yüklemenizi başlayın [oluşturma veritabanı geri yükleme isteği] [ Create database restore request] işlemi.</span><span class="sxs-lookup"><span data-stu-id="f6864-124">Begin your restore by using hello [Create database restore request][Create database restore request] operation.</span></span>
4. <span data-ttu-id="f6864-125">Hello kullanarak geri yüklemenizi hello durumunu izlemek [veritabanı işlemi durumunu] [ Database operation status] işlemi.</span><span class="sxs-lookup"><span data-stu-id="f6864-125">Track hello status of your restore by using hello [Database operation status][Database operation status] operation.</span></span>

> [!NOTE]
> <span data-ttu-id="f6864-126">Merhaba geri yükleme tamamlandıktan sonra veritabanınızı tooconfigure bkz [kurtarma işleminden sonra veritabanını yapılandırma][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="f6864-126">tooconfigure your database after hello restore has completed, see [Configure your database after recovery][Configure your database after recovery].</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="f6864-127">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f6864-127">Next steps</span></span>
<span data-ttu-id="f6864-128">Azure SQL veritabanı sürümlerini hello iş sürekliliği özellikleri hakkında toolearn hello okuyun [Azure SQL Database iş sürekliliğine genel bakış][Azure SQL Database business continuity overview].</span><span class="sxs-lookup"><span data-stu-id="f6864-128">toolearn about hello business continuity features of Azure SQL Database editions, please read hello [Azure SQL Database business continuity overview][Azure SQL Database business continuity overview].</span></span>

<!--Image references-->

<!--Article references-->
[Azure SQL Database business continuity overview]: ../sql-database/sql-database-business-continuity.md
[Request a DTU quota change]: ./sql-data-warehouse-get-started-create-support-ticket.md#request-quota-change
[Configure your database after recovery]: ../sql-database/sql-database-disaster-recovery.md#configure-your-database-after-recovery
[How tooinstall and configure Azure PowerShell]: /powershell/azureps-cmdlets-docs
[Overview]: ./sql-data-warehouse-restore-database-overview.md
[Portal]: ./sql-data-warehouse-restore-database-portal.md
[PowerShell]: ./sql-data-warehouse-restore-database-powershell.md
[REST]: ./sql-data-warehouse-restore-database-rest-api.md

<!--MSDN references-->
[Create database restore request]: https://msdn.microsoft.com/library/azure/dn509571.aspx
[Database operation status]: https://msdn.microsoft.com/library/azure/dn720371.aspx
[Get restorable dropped database]: https://msdn.microsoft.com/library/azure/dn509574.aspx
[List restorable dropped databases]: https://msdn.microsoft.com/library/azure/dn509562.aspx
[Restore-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt693390.aspx

<!--Other Web references-->
[Azure Portal]: https://portal.azure.com/
[Microsoft Web Platform Installer]: https://aka.ms/webpi-azps
