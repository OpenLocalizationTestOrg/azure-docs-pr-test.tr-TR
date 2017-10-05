---
title: "Bir Azure SQL veri ambarı (PowerShell) geri | Microsoft Docs"
description: "Azure SQL Data Warehouse geri yüklemek için PowerShell görevler."
services: sql-data-warehouse
documentationcenter: NA
author: Lakshmi1812
manager: jhubbard
editor: 
ms.assetid: ac62f154-c8b0-4c33-9c42-f480808aa1d2
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: backup-restore
ms.date: 10/31/2016
ms.author: lakshmir;barbkess
ms.openlocfilehash: 6286c0e682bae2d3bf0435a25b8077a53b117b25
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="restore-an-azure-sql-data-warehouse-powershell"></a><span data-ttu-id="4ca7a-103">Bir Azure SQL veri ambarı (PowerShell) geri yükleme</span><span class="sxs-lookup"><span data-stu-id="4ca7a-103">Restore an Azure SQL Data Warehouse (PowerShell)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="4ca7a-104">[Genel bakış][Overview]</span><span class="sxs-lookup"><span data-stu-id="4ca7a-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="4ca7a-105">[Portal][Portal]</span><span class="sxs-lookup"><span data-stu-id="4ca7a-105">[Portal][Portal]</span></span>
> * <span data-ttu-id="4ca7a-106">[PowerShell][PowerShell]</span><span class="sxs-lookup"><span data-stu-id="4ca7a-106">[PowerShell][PowerShell]</span></span>
> * <span data-ttu-id="4ca7a-107">[REST][REST]</span><span class="sxs-lookup"><span data-stu-id="4ca7a-107">[REST][REST]</span></span>
> 
> 

<span data-ttu-id="4ca7a-108">Bu makalede PowerShell kullanarak Azure SQL Data Warehouse geri yükleme öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="4ca7a-108">In this article you will learn how to restore an Azure SQL Data Warehouse using PowerShell.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="4ca7a-109">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="4ca7a-109">Before you begin</span></span>
<span data-ttu-id="4ca7a-110">**DTU kapasitenizi doğrulayın.**</span><span class="sxs-lookup"><span data-stu-id="4ca7a-110">**Verify your DTU capacity.**</span></span> <span data-ttu-id="4ca7a-111">Her SQL veri ambarı varsayılan DTU kota olan bir SQL server tarafından (örneğin myserver.database.windows.net) barındırılıyor.</span><span class="sxs-lookup"><span data-stu-id="4ca7a-111">Each SQL Data Warehouse is hosted by a SQL server (e.g. myserver.database.windows.net) which has a default DTU quota.</span></span>  <span data-ttu-id="4ca7a-112">SQL Data Warehouse geri yükleyebilmeniz için önce doğrulayın yeterli kalan DTU kota geri yüklenen veritabanı için SQL server'ınızdaki sahiptir.</span><span class="sxs-lookup"><span data-stu-id="4ca7a-112">Before you can restore a SQL Data Warehouse, verify that the your SQL server has enough remaining DTU quota for the database being restored.</span></span> <span data-ttu-id="4ca7a-113">Gerekli DTU hesaplamak için ya da daha fazla DTU istemek için öğrenmek için bkz: [DTU kota değişiklik isteği][Request a DTU quota change].</span><span class="sxs-lookup"><span data-stu-id="4ca7a-113">To learn how to calculate DTU needed or to request more DTU, see [Request a DTU quota change][Request a DTU quota change].</span></span>

### <a name="install-powershell"></a><span data-ttu-id="4ca7a-114">PowerShell yükleme</span><span class="sxs-lookup"><span data-stu-id="4ca7a-114">Install PowerShell</span></span>
<span data-ttu-id="4ca7a-115">SQL Data Warehouse ile Azure PowerShell kullanmak için Azure PowerShell 1.0 veya büyük bir sürümü yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="4ca7a-115">In order to use Azure PowerShell with SQL Data Warehouse, you will need to install Azure PowerShell version 1.0 or greater.</span></span>  <span data-ttu-id="4ca7a-116">Çalıştırarak sürümünüzü kontrol edebilirsiniz **Get-Module - listavailable birlikte-adı AzureRM**.</span><span class="sxs-lookup"><span data-stu-id="4ca7a-116">You can check your version by running **Get-Module -ListAvailable -Name AzureRM**.</span></span>  <span data-ttu-id="4ca7a-117">En son sürümünü yüklenebilir [Microsoft Web Platformu yükleyicisi][Microsoft Web Platform Installer].</span><span class="sxs-lookup"><span data-stu-id="4ca7a-117">The latest version can be installed from  [Microsoft Web Platform Installer][Microsoft Web Platform Installer].</span></span>  <span data-ttu-id="4ca7a-118">En son sürümü yükleme hakkında daha fazla bilgi için bkz. [Azure PowerShell'i yükleme ve yapılandırma][How to install and configure Azure PowerShell].</span><span class="sxs-lookup"><span data-stu-id="4ca7a-118">For more information on installing the latest version, see [How to install and configure Azure PowerShell][How to install and configure Azure PowerShell].</span></span>

## <a name="restore-an-active-or-paused-database"></a><span data-ttu-id="4ca7a-119">Etkin ya da duraklatılmış bir veritabanını geri yükle</span><span class="sxs-lookup"><span data-stu-id="4ca7a-119">Restore an active or paused database</span></span>
<span data-ttu-id="4ca7a-120">Anlık görüntü kullanılmakta olan bir veritabanını geri yüklemek için [geri yükleme-AzureRmSqlDatabase] [ Restore-AzureRmSqlDatabase] PowerShell cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="4ca7a-120">To restore a database from a snapshot use the [Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase] PowerShell cmdlet.</span></span>

1. <span data-ttu-id="4ca7a-121">Windows PowerShell'i açın.</span><span class="sxs-lookup"><span data-stu-id="4ca7a-121">Open Windows PowerShell.</span></span>
2. <span data-ttu-id="4ca7a-122">Azure hesabınıza bağlanın ve hesabınızla ilişkili tüm abonelikleri listeler.</span><span class="sxs-lookup"><span data-stu-id="4ca7a-122">Connect to your Azure account and list all the subscriptions associated with your account.</span></span>
3. <span data-ttu-id="4ca7a-123">Geri yüklenecek veritabanını içeren aboneliği seçin.</span><span class="sxs-lookup"><span data-stu-id="4ca7a-123">Select the subscription that contains the database to be restored.</span></span>
4. <span data-ttu-id="4ca7a-124">Veritabanını geri yükleme noktaları listesi.</span><span class="sxs-lookup"><span data-stu-id="4ca7a-124">List the restore points for the database.</span></span>
5. <span data-ttu-id="4ca7a-125">RestorePointCreationDate kullanarak istenen geri yükleme noktası seçin.</span><span class="sxs-lookup"><span data-stu-id="4ca7a-125">Pick the desired restore point using the RestorePointCreationDate.</span></span>
6. <span data-ttu-id="4ca7a-126">Veritabanını geri yüklemek için istenen geri yükleme noktası.</span><span class="sxs-lookup"><span data-stu-id="4ca7a-126">Restore the database to the desired restore point.</span></span>
7. <span data-ttu-id="4ca7a-127">Geri yüklenen veritabanının çevrimiçi olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="4ca7a-127">Verify that the restored database is online.</span></span>

```Powershell

$SubscriptionName="<YourSubscriptionName>"
$ResourceGroupName="<YourResourceGroupName>"
$ServerName="<YourServerNameWithoutURLSuffixSeeNote>"  # Without database.windows.net
$DatabaseName="<YourDatabaseName>"
$NewDatabaseName="<YourDatabaseName>"

Login-AzureRmAccount
Get-AzureRmSubscription
Select-AzureRmSubscription -SubscriptionName $SubscriptionName

# List the last 10 database restore points
((Get-AzureRMSqlDatabaseRestorePoints -ResourceGroupName $ResourceGroupName -ServerName $ServerName -DatabaseName ($DatabaseName).RestorePointCreationDate)[-10 .. -1]

# Or list all restore points
Get-AzureRmSqlDatabaseRestorePoints -ResourceGroupName $ResourceGroupName -ServerName $ServerName -DatabaseName $DatabaseName

# Get the specific database to restore
$Database = Get-AzureRmSqlDatabase -ResourceGroupName $ResourceGroupName -ServerName $ServerName -DatabaseName $DatabaseName

# Pick desired restore point using RestorePointCreationDate
$PointInTime="<RestorePointCreationDate>"  

# Restore database from a restore point
$RestoredDatabase = Restore-AzureRmSqlDatabase –FromPointInTimeBackup –PointInTime $PointInTime -ResourceGroupName $Database.ResourceGroupName -ServerName $Database.$ServerName -TargetDatabaseName $NewDatabaseName –ResourceId $Database.ResourceID

# Verify the status of restored database
$RestoredDatabase.status

```

> [!NOTE]
> <span data-ttu-id="4ca7a-128">Geri yükleme tamamlandıktan sonra izleyerek, kurtarılan veritabanının yapılandırabilirsiniz [kurtarma işleminden sonra veritabanını yapılandırma][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="4ca7a-128">After the restore has completed, you can configure your recovered database by following [Configure your database after recovery][Configure your database after recovery].</span></span>
> 
> 

## <a name="restore-a-deleted-database"></a><span data-ttu-id="4ca7a-129">Silinen veritabanını geri yükleme</span><span class="sxs-lookup"><span data-stu-id="4ca7a-129">Restore a deleted database</span></span>
<span data-ttu-id="4ca7a-130">Silinen bir veritabanını geri yüklemek için kullanmak [geri yükleme-AzureRmSqlDatabase] [ Restore-AzureRmSqlDatabase] cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="4ca7a-130">To restore a deleted database, use the [Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase] cmdlet.</span></span>

1. <span data-ttu-id="4ca7a-131">Windows PowerShell'i açın.</span><span class="sxs-lookup"><span data-stu-id="4ca7a-131">Open Windows PowerShell.</span></span>
2. <span data-ttu-id="4ca7a-132">Azure hesabınıza bağlanın ve hesabınızla ilişkili tüm abonelikleri listeler.</span><span class="sxs-lookup"><span data-stu-id="4ca7a-132">Connect to your Azure account and list all the subscriptions associated with your account.</span></span>
3. <span data-ttu-id="4ca7a-133">Geri yüklenecek silinmiş veritabanını içeren aboneliği seçin.</span><span class="sxs-lookup"><span data-stu-id="4ca7a-133">Select the subscription that contains the deleted database to be restored.</span></span>
4. <span data-ttu-id="4ca7a-134">Belirli silinen bu veritabanını alın.</span><span class="sxs-lookup"><span data-stu-id="4ca7a-134">Get the specific deleted database.</span></span>
5. <span data-ttu-id="4ca7a-135">Silinen bir veritabanını geri yükleyin.</span><span class="sxs-lookup"><span data-stu-id="4ca7a-135">Restore the deleted database.</span></span>
6. <span data-ttu-id="4ca7a-136">Geri yüklenen veritabanının çevrimiçi olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="4ca7a-136">Verify that the restored database is online.</span></span>

```Powershell
$SubscriptionName="<YourSubscriptionName>"
$ResourceGroupName="<YourResourceGroupName>"
$ServerName="<YourServerNameWithoutURLSuffixSeeNote>"  # Without database.windows.net
$DatabaseName="<YourDatabaseName>"
$NewDatabaseName="<YourDatabaseName>"

Login-AzureRmAccount
Get-AzureRmSubscription
Select-AzureRmSubscription -SubscriptionName $SubscriptionName

# Get the deleted database to restore
$DeletedDatabase = Get-AzureRmSqlDeletedDatabaseBackup -ResourceGroupName $ResourceGroupName -ServerName $ServerName -DatabaseName $DatabaseName

# Restore deleted database
$RestoredDatabase = Restore-AzureRmSqlDatabase –FromDeletedDatabaseBackup –DeletionDate $DeletedDatabase.DeletionDate -ResourceGroupName $DeletedDatabase.ResourceGroupName -ServerName $DeletedDatabase.ServerName -TargetDatabaseName $NewDatabaseName –ResourceId $DeletedDatabase.ResourceID

# Verify the status of restored database
$RestoredDatabase.status
```

> [!NOTE]
> <span data-ttu-id="4ca7a-137">Geri yükleme tamamlandıktan sonra izleyerek, kurtarılan veritabanının yapılandırabilirsiniz [kurtarma işleminden sonra veritabanını yapılandırma][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="4ca7a-137">After the restore has completed, you can configure your recovered database by following [Configure your database after recovery][Configure your database after recovery].</span></span>
> 
> 

## <a name="restore-from-an-azure-geographical-region"></a><span data-ttu-id="4ca7a-138">Bir Azure coğrafi bölgesinden geri yükleme</span><span class="sxs-lookup"><span data-stu-id="4ca7a-138">Restore from an Azure geographical region</span></span>
<span data-ttu-id="4ca7a-139">Bir veritabanını kurtarmak için kullanmak [geri yükleme-AzureRmSqlDatabase] [ Restore-AzureRmSqlDatabase] cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="4ca7a-139">To recover a database, use the [Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase] cmdlet.</span></span>

1. <span data-ttu-id="4ca7a-140">Windows PowerShell'i açın.</span><span class="sxs-lookup"><span data-stu-id="4ca7a-140">Open Windows PowerShell.</span></span>
2. <span data-ttu-id="4ca7a-141">Azure hesabınıza bağlanın ve hesabınızla ilişkili tüm abonelikleri listeler.</span><span class="sxs-lookup"><span data-stu-id="4ca7a-141">Connect to your Azure account and list all the subscriptions associated with your account.</span></span>
3. <span data-ttu-id="4ca7a-142">Geri yüklenecek veritabanını içeren aboneliği seçin.</span><span class="sxs-lookup"><span data-stu-id="4ca7a-142">Select the subscription that contains the database to be restored.</span></span>
4. <span data-ttu-id="4ca7a-143">Kurtarmak istediğiniz veritabanı alın.</span><span class="sxs-lookup"><span data-stu-id="4ca7a-143">Get the database you want to recover.</span></span>
5. <span data-ttu-id="4ca7a-144">Veritabanı için kurtarma isteği oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4ca7a-144">Create the recovery request for the database.</span></span>
6. <span data-ttu-id="4ca7a-145">Coğrafi geri veritabanının durumunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="4ca7a-145">Verify the status of the geo-restored database.</span></span>

```Powershell
Login-AzureRmAccount
Get-AzureRmSubscription
Select-AzureRmSubscription -SubscriptionName "<Subscription_name>"

# Get the database you want to recover
$GeoBackup = Get-AzureRmSqlDatabaseGeoBackup -ResourceGroupName "<YourResourceGroupName>" -ServerName "<YourServerName>" -DatabaseName "<YourDatabaseName>"

# Recover database
$GeoRestoredDatabase = Restore-AzureRmSqlDatabase –FromGeoBackup -ResourceGroupName "<YourResourceGroupName>" -ServerName "<YourTargetServer>" -TargetDatabaseName "<NewDatabaseName>" –ResourceId $GeoBackup.ResourceID

# Verify that the geo-restored database is online
$GeoRestoredDatabase.status
```

> [!NOTE]
> <span data-ttu-id="4ca7a-146">Geri yükleme tamamlandıktan sonra veritabanını yapılandırmak için bkz: [kurtarma işleminden sonra veritabanını yapılandırma][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="4ca7a-146">To configure your database after the restore has completed, see [Configure your database after recovery][Configure your database after recovery].</span></span>
> 
> 

<span data-ttu-id="4ca7a-147">Kaynak veritabanı TDE etkinse kurtarılmış veritabanını TDE etkin olacaktır.</span><span class="sxs-lookup"><span data-stu-id="4ca7a-147">The recovered database will be TDE-enabled if the source database is TDE-enabled.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4ca7a-148">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4ca7a-148">Next steps</span></span>
<span data-ttu-id="4ca7a-149">Azure SQL veritabanı sürümlerini iş sürekliliği özellikleri hakkında bilgi edinmek için lütfen okuyun [Azure SQL Database iş sürekliliğine genel bakış][Azure SQL Database business continuity overview].</span><span class="sxs-lookup"><span data-stu-id="4ca7a-149">To learn about the business continuity features of Azure SQL Database editions, please read the [Azure SQL Database business continuity overview][Azure SQL Database business continuity overview].</span></span>

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
[Configure your database after recovery]: ../sql-database/sql-database-disaster-recovery.md#configure-your-database-after-recovery

<!--MSDN references-->
[Restore-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt693390.aspx

<!--Other Web references-->
[Azure Portal]: https://portal.azure.com/
[Microsoft Web Platform Installer]: https://aka.ms/webpi-azps
