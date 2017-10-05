---
title: "Bir Azure SQL veri ambarı (REST API'si) geri | Microsoft Docs"
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
ms.openlocfilehash: 8656607611e7518e42b51b91774f55abec15c228
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="restore-an-azure-sql-data-warehouse-rest-api"></a><span data-ttu-id="b4c59-103">Bir Azure SQL veri ambarı (REST API'si) geri yükleme</span><span class="sxs-lookup"><span data-stu-id="b4c59-103">Restore an Azure SQL Data Warehouse (REST API)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="b4c59-104">[Genel bakış][Overview]</span><span class="sxs-lookup"><span data-stu-id="b4c59-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="b4c59-105">[Portal][Portal]</span><span class="sxs-lookup"><span data-stu-id="b4c59-105">[Portal][Portal]</span></span>
> * <span data-ttu-id="b4c59-106">[PowerShell][PowerShell]</span><span class="sxs-lookup"><span data-stu-id="b4c59-106">[PowerShell][PowerShell]</span></span>
> * <span data-ttu-id="b4c59-107">[REST][REST]</span><span class="sxs-lookup"><span data-stu-id="b4c59-107">[REST][REST]</span></span>
> 
> 

<span data-ttu-id="b4c59-108">Bu makalede, REST API kullanarak Azure SQL Data Warehouse geri yükleme öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="b4c59-108">In this article you will learn how to restore an Azure SQL Data Warehouse using the REST API.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="b4c59-109">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="b4c59-109">Before you begin</span></span>
<span data-ttu-id="b4c59-110">**DTU kapasitenizi doğrulayın.**</span><span class="sxs-lookup"><span data-stu-id="b4c59-110">**Verify your DTU capacity.**</span></span> <span data-ttu-id="b4c59-111">Her SQL veri ambarı varsayılan DTU kota olan bir SQL server tarafından (örneğin myserver.database.windows.net) barındırılıyor.</span><span class="sxs-lookup"><span data-stu-id="b4c59-111">Each SQL Data Warehouse is hosted by a SQL server (e.g. myserver.database.windows.net) which has a default DTU quota.</span></span>  <span data-ttu-id="b4c59-112">SQL Data Warehouse geri yükleyebilmeniz için önce doğrulayın yeterli kalan DTU kota geri yüklenen veritabanı için SQL server'ınızdaki sahiptir.</span><span class="sxs-lookup"><span data-stu-id="b4c59-112">Before you can restore a SQL Data Warehouse, verify that the your SQL server has enough remaining DTU quota for the database being restored.</span></span> <span data-ttu-id="b4c59-113">Gerekli DTU hesaplamak için ya da daha fazla DTU istemek için öğrenmek için bkz: [DTU kota değişiklik isteği][Request a DTU quota change].</span><span class="sxs-lookup"><span data-stu-id="b4c59-113">To learn how to calculate DTU needed or to request more DTU, see [Request a DTU quota change][Request a DTU quota change].</span></span>

## <a name="restore-an-active-or-paused-database"></a><span data-ttu-id="b4c59-114">Etkin ya da duraklatılmış bir veritabanını geri yükle</span><span class="sxs-lookup"><span data-stu-id="b4c59-114">Restore an active or paused database</span></span>
<span data-ttu-id="b4c59-115">Bir veritabanını geri yüklemek için:</span><span class="sxs-lookup"><span data-stu-id="b4c59-115">To restore a database:</span></span>

1. <span data-ttu-id="b4c59-116">Get veritabanı geri yükleme noktaları işlemi kullanarak veritabanını geri yükleme noktaları listesini alın.</span><span class="sxs-lookup"><span data-stu-id="b4c59-116">Get the list of database restore points using the Get Database Restore Points operation.</span></span>
2. <span data-ttu-id="b4c59-117">Geri yükleme kullanarak başlayın [oluşturma veritabanı geri yükleme isteği] [ Create database restore request] işlemi.</span><span class="sxs-lookup"><span data-stu-id="b4c59-117">Begin your restore by using the [Create database restore request][Create database restore request] operation.</span></span>
3. <span data-ttu-id="b4c59-118">Kullanarak geri yükleme durumunu izlemek [veritabanı işlemi durumunu] [ Database operation status] işlemi.</span><span class="sxs-lookup"><span data-stu-id="b4c59-118">Track the status of your restore by using the [Database operation status][Database operation status] operation.</span></span>

> [!NOTE]
> <span data-ttu-id="b4c59-119">Geri yükleme tamamlandıktan sonra izleyerek, kurtarılan veritabanının yapılandırabilirsiniz [kurtarma işleminden sonra veritabanını yapılandırma][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="b4c59-119">After the restore has completed, you can configure your recovered database by following [Configure your database after recovery][Configure your database after recovery].</span></span>
> 
> 

## <a name="restore-a-deleted-database"></a><span data-ttu-id="b4c59-120">Silinen veritabanını geri yükleme</span><span class="sxs-lookup"><span data-stu-id="b4c59-120">Restore a deleted database</span></span>
<span data-ttu-id="b4c59-121">Silinen bir veritabanını geri yüklemek için:</span><span class="sxs-lookup"><span data-stu-id="b4c59-121">To restore a deleted database:</span></span>

1. <span data-ttu-id="b4c59-122">Tüm geri yüklenebilen silinmiş veritabanlarınızın kullanarak liste [listesi geri yüklenebilen bırakılan veritabanları] [ List restorable dropped databases] işlemi.</span><span class="sxs-lookup"><span data-stu-id="b4c59-122">List all of your restorable deleted databases by using the [List restorable dropped databases][List restorable dropped databases] operation.</span></span>
2. <span data-ttu-id="b4c59-123">Kullanarak geri yüklemek istediğiniz silinmiş veritabanı için Ayrıntılar elde [Get geri yüklenebilen bırakılan veritabanı] [ Get restorable dropped database] işlemi.</span><span class="sxs-lookup"><span data-stu-id="b4c59-123">Get the details for the deleted database you want to restore by using the [Get restorable dropped database][Get restorable dropped database] operation.</span></span>
3. <span data-ttu-id="b4c59-124">Geri yükleme kullanarak başlayın [oluşturma veritabanı geri yükleme isteği] [ Create database restore request] işlemi.</span><span class="sxs-lookup"><span data-stu-id="b4c59-124">Begin your restore by using the [Create database restore request][Create database restore request] operation.</span></span>
4. <span data-ttu-id="b4c59-125">Kullanarak geri yükleme durumunu izlemek [veritabanı işlemi durumunu] [ Database operation status] işlemi.</span><span class="sxs-lookup"><span data-stu-id="b4c59-125">Track the status of your restore by using the [Database operation status][Database operation status] operation.</span></span>

> [!NOTE]
> <span data-ttu-id="b4c59-126">Geri yükleme tamamlandıktan sonra veritabanını yapılandırmak için bkz: [kurtarma işleminden sonra veritabanını yapılandırma][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="b4c59-126">To configure your database after the restore has completed, see [Configure your database after recovery][Configure your database after recovery].</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="b4c59-127">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b4c59-127">Next steps</span></span>
<span data-ttu-id="b4c59-128">Azure SQL veritabanı sürümlerini iş sürekliliği özellikleri hakkında bilgi edinmek için lütfen okuyun [Azure SQL Database iş sürekliliğine genel bakış][Azure SQL Database business continuity overview].</span><span class="sxs-lookup"><span data-stu-id="b4c59-128">To learn about the business continuity features of Azure SQL Database editions, please read the [Azure SQL Database business continuity overview][Azure SQL Database business continuity overview].</span></span>

<!--Image references-->

<!--Article references-->
[Azure SQL Database business continuity overview]: ../sql-database/sql-database-business-continuity.md
[Request a DTU quota change]: ./sql-data-warehouse-get-started-create-support-ticket.md#request-quota-change
[Configure your database after recovery]: ../sql-database/sql-database-disaster-recovery.md#configure-your-database-after-recovery
[How to install and configure Azure PowerShell]: /powershell/azureps-cmdlets-docs
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
