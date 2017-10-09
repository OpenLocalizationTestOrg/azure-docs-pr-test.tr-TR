---
title: aaaRestore Azure SQL Data Warehouse (PowerShell) | Microsoft Docs
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
ms.openlocfilehash: aa29a315080b1ed477cc6a051ce15a3202630cfa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="restore-an-azure-sql-data-warehouse-powershell"></a><span data-ttu-id="e1064-103">Bir Azure SQL veri ambarı (PowerShell) geri yükleme</span><span class="sxs-lookup"><span data-stu-id="e1064-103">Restore an Azure SQL Data Warehouse (PowerShell)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="e1064-104">[Genel bakış][Overview]</span><span class="sxs-lookup"><span data-stu-id="e1064-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="e1064-105">[Portal][Portal]</span><span class="sxs-lookup"><span data-stu-id="e1064-105">[Portal][Portal]</span></span>
> * <span data-ttu-id="e1064-106">[PowerShell][PowerShell]</span><span class="sxs-lookup"><span data-stu-id="e1064-106">[PowerShell][PowerShell]</span></span>
> * <span data-ttu-id="e1064-107">[REST][REST]</span><span class="sxs-lookup"><span data-stu-id="e1064-107">[REST][REST]</span></span>
> 
> 

<span data-ttu-id="e1064-108">Bu makalede nasıl toorestore bir Azure SQL Data Warehouse PowerShell kullanarak öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="e1064-108">In this article you will learn how toorestore an Azure SQL Data Warehouse using PowerShell.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="e1064-109">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="e1064-109">Before you begin</span></span>
<span data-ttu-id="e1064-110">**DTU kapasitenizi doğrulayın.**</span><span class="sxs-lookup"><span data-stu-id="e1064-110">**Verify your DTU capacity.**</span></span> <span data-ttu-id="e1064-111">Her SQL veri ambarı varsayılan DTU kota olan bir SQL server tarafından (örneğin myserver.database.windows.net) barındırılıyor.</span><span class="sxs-lookup"><span data-stu-id="e1064-111">Each SQL Data Warehouse is hosted by a SQL server (e.g. myserver.database.windows.net) which has a default DTU quota.</span></span>  <span data-ttu-id="e1064-112">SQL Data Warehouse geri yüklemeden önce SQL server'ınızdaki hello veritabanı geri yükleniyor için yeterince kalan DTU kota sahip o hello doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="e1064-112">Before you can restore a SQL Data Warehouse, verify that hello your SQL server has enough remaining DTU quota for hello database being restored.</span></span> <span data-ttu-id="e1064-113">toolearn nasıl toocalculate DTU gerekli veya toorequest daha fazla DTU bkz [DTU kota değişiklik isteği][Request a DTU quota change].</span><span class="sxs-lookup"><span data-stu-id="e1064-113">toolearn how toocalculate DTU needed or toorequest more DTU, see [Request a DTU quota change][Request a DTU quota change].</span></span>

### <a name="install-powershell"></a><span data-ttu-id="e1064-114">PowerShell yükleme</span><span class="sxs-lookup"><span data-stu-id="e1064-114">Install PowerShell</span></span>
<span data-ttu-id="e1064-115">Sipariş toouse SQL Data Warehouse ile Azure PowerShell, tooinstall Azure PowerShell sürüm 1.0 veya üzeri gerekir.</span><span class="sxs-lookup"><span data-stu-id="e1064-115">In order toouse Azure PowerShell with SQL Data Warehouse, you will need tooinstall Azure PowerShell version 1.0 or greater.</span></span>  <span data-ttu-id="e1064-116">Çalıştırarak sürümünüzü kontrol edebilirsiniz **Get-Module - listavailable birlikte-adı AzureRM**.</span><span class="sxs-lookup"><span data-stu-id="e1064-116">You can check your version by running **Get-Module -ListAvailable -Name AzureRM**.</span></span>  <span data-ttu-id="e1064-117">Merhaba en son sürümünü yüklenebilir [Microsoft Web Platformu yükleyicisi][Microsoft Web Platform Installer].</span><span class="sxs-lookup"><span data-stu-id="e1064-117">hello latest version can be installed from  [Microsoft Web Platform Installer][Microsoft Web Platform Installer].</span></span>  <span data-ttu-id="e1064-118">Merhaba en son sürümü yükleme hakkında daha fazla bilgi için bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma][How tooinstall and configure Azure PowerShell].</span><span class="sxs-lookup"><span data-stu-id="e1064-118">For more information on installing hello latest version, see [How tooinstall and configure Azure PowerShell][How tooinstall and configure Azure PowerShell].</span></span>

## <a name="restore-an-active-or-paused-database"></a><span data-ttu-id="e1064-119">Etkin ya da duraklatılmış bir veritabanını geri yükle</span><span class="sxs-lookup"><span data-stu-id="e1064-119">Restore an active or paused database</span></span>
<span data-ttu-id="e1064-120">toorestore bir anlık görüntü veritabanından kullanmak hello [geri yükleme-AzureRmSqlDatabase] [ Restore-AzureRmSqlDatabase] PowerShell cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="e1064-120">toorestore a database from a snapshot use hello [Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase] PowerShell cmdlet.</span></span>

1. <span data-ttu-id="e1064-121">Windows PowerShell'i açın.</span><span class="sxs-lookup"><span data-stu-id="e1064-121">Open Windows PowerShell.</span></span>
2. <span data-ttu-id="e1064-122">Azure hesabı tooyour bağlanın ve hesabınızla ilişkili tüm hello abonelik listesi.</span><span class="sxs-lookup"><span data-stu-id="e1064-122">Connect tooyour Azure account and list all hello subscriptions associated with your account.</span></span>
3. <span data-ttu-id="e1064-123">Merhaba veritabanı toobe geri içeren hello aboneliği seçin.</span><span class="sxs-lookup"><span data-stu-id="e1064-123">Select hello subscription that contains hello database toobe restored.</span></span>
4. <span data-ttu-id="e1064-124">Liste hello geri yükleme noktaları hello veritabanı için.</span><span class="sxs-lookup"><span data-stu-id="e1064-124">List hello restore points for hello database.</span></span>
5. <span data-ttu-id="e1064-125">Merhaba RestorePointCreationDate kullanarak istenen hello geri yükleme noktası seçin.</span><span class="sxs-lookup"><span data-stu-id="e1064-125">Pick hello desired restore point using hello RestorePointCreationDate.</span></span>
6. <span data-ttu-id="e1064-126">Merhaba veritabanı istenen toohello geri yükleme noktası geri yükleyin.</span><span class="sxs-lookup"><span data-stu-id="e1064-126">Restore hello database toohello desired restore point.</span></span>
7. <span data-ttu-id="e1064-127">Geri hello veritabanının çevrimiçi olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="e1064-127">Verify that hello restored database is online.</span></span>

```Powershell

$SubscriptionName="<YourSubscriptionName>"
$ResourceGroupName="<YourResourceGroupName>"
$ServerName="<YourServerNameWithoutURLSuffixSeeNote>"  # Without database.windows.net
$DatabaseName="<YourDatabaseName>"
$NewDatabaseName="<YourDatabaseName>"

Login-AzureRmAccount
Get-AzureRmSubscription
Select-AzureRmSubscription -SubscriptionName $SubscriptionName

# List hello last 10 database restore points
((Get-AzureRMSqlDatabaseRestorePoints -ResourceGroupName $ResourceGroupName -ServerName $ServerName -DatabaseName ($DatabaseName).RestorePointCreationDate)[-10 .. -1]

# Or list all restore points
Get-AzureRmSqlDatabaseRestorePoints -ResourceGroupName $ResourceGroupName -ServerName $ServerName -DatabaseName $DatabaseName

# Get hello specific database toorestore
$Database = Get-AzureRmSqlDatabase -ResourceGroupName $ResourceGroupName -ServerName $ServerName -DatabaseName $DatabaseName

# Pick desired restore point using RestorePointCreationDate
$PointInTime="<RestorePointCreationDate>"  

# Restore database from a restore point
$RestoredDatabase = Restore-AzureRmSqlDatabase –FromPointInTimeBackup –PointInTime $PointInTime -ResourceGroupName $Database.ResourceGroupName -ServerName $Database.$ServerName -TargetDatabaseName $NewDatabaseName –ResourceId $Database.ResourceID

# Verify hello status of restored database
$RestoredDatabase.status

```

> [!NOTE]
> <span data-ttu-id="e1064-128">Merhaba geri yükleme tamamlandıktan sonra izleyerek, kurtarılan veritabanının yapılandırabilirsiniz [kurtarma işleminden sonra veritabanını yapılandırma][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="e1064-128">After hello restore has completed, you can configure your recovered database by following [Configure your database after recovery][Configure your database after recovery].</span></span>
> 
> 

## <a name="restore-a-deleted-database"></a><span data-ttu-id="e1064-129">Silinen veritabanını geri yükleme</span><span class="sxs-lookup"><span data-stu-id="e1064-129">Restore a deleted database</span></span>
<span data-ttu-id="e1064-130">toorestore silinen bir veritabanını kullanın hello [geri yükleme-AzureRmSqlDatabase] [ Restore-AzureRmSqlDatabase] cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="e1064-130">toorestore a deleted database, use hello [Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase] cmdlet.</span></span>

1. <span data-ttu-id="e1064-131">Windows PowerShell'i açın.</span><span class="sxs-lookup"><span data-stu-id="e1064-131">Open Windows PowerShell.</span></span>
2. <span data-ttu-id="e1064-132">Azure hesabı tooyour bağlanın ve hesabınızla ilişkili tüm hello abonelik listesi.</span><span class="sxs-lookup"><span data-stu-id="e1064-132">Connect tooyour Azure account and list all hello subscriptions associated with your account.</span></span>
3. <span data-ttu-id="e1064-133">Silinen hello veritabanı toobe geri içeren hello aboneliği seçin.</span><span class="sxs-lookup"><span data-stu-id="e1064-133">Select hello subscription that contains hello deleted database toobe restored.</span></span>
4. <span data-ttu-id="e1064-134">Merhaba belirli silinmiş veritabanı alın.</span><span class="sxs-lookup"><span data-stu-id="e1064-134">Get hello specific deleted database.</span></span>
5. <span data-ttu-id="e1064-135">Merhaba silinen veritabanını geri yükleyin.</span><span class="sxs-lookup"><span data-stu-id="e1064-135">Restore hello deleted database.</span></span>
6. <span data-ttu-id="e1064-136">Geri hello veritabanının çevrimiçi olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="e1064-136">Verify that hello restored database is online.</span></span>

```Powershell
$SubscriptionName="<YourSubscriptionName>"
$ResourceGroupName="<YourResourceGroupName>"
$ServerName="<YourServerNameWithoutURLSuffixSeeNote>"  # Without database.windows.net
$DatabaseName="<YourDatabaseName>"
$NewDatabaseName="<YourDatabaseName>"

Login-AzureRmAccount
Get-AzureRmSubscription
Select-AzureRmSubscription -SubscriptionName $SubscriptionName

# Get hello deleted database toorestore
$DeletedDatabase = Get-AzureRmSqlDeletedDatabaseBackup -ResourceGroupName $ResourceGroupName -ServerName $ServerName -DatabaseName $DatabaseName

# Restore deleted database
$RestoredDatabase = Restore-AzureRmSqlDatabase –FromDeletedDatabaseBackup –DeletionDate $DeletedDatabase.DeletionDate -ResourceGroupName $DeletedDatabase.ResourceGroupName -ServerName $DeletedDatabase.ServerName -TargetDatabaseName $NewDatabaseName –ResourceId $DeletedDatabase.ResourceID

# Verify hello status of restored database
$RestoredDatabase.status
```

> [!NOTE]
> <span data-ttu-id="e1064-137">Merhaba geri yükleme tamamlandıktan sonra izleyerek, kurtarılan veritabanının yapılandırabilirsiniz [kurtarma işleminden sonra veritabanını yapılandırma][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="e1064-137">After hello restore has completed, you can configure your recovered database by following [Configure your database after recovery][Configure your database after recovery].</span></span>
> 
> 

## <a name="restore-from-an-azure-geographical-region"></a><span data-ttu-id="e1064-138">Bir Azure coğrafi bölgesinden geri yükleme</span><span class="sxs-lookup"><span data-stu-id="e1064-138">Restore from an Azure geographical region</span></span>
<span data-ttu-id="e1064-139">toorecover bir veritabanını kullanın hello [geri yükleme-AzureRmSqlDatabase] [ Restore-AzureRmSqlDatabase] cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="e1064-139">toorecover a database, use hello [Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase] cmdlet.</span></span>

1. <span data-ttu-id="e1064-140">Windows PowerShell'i açın.</span><span class="sxs-lookup"><span data-stu-id="e1064-140">Open Windows PowerShell.</span></span>
2. <span data-ttu-id="e1064-141">Azure hesabı tooyour bağlanın ve hesabınızla ilişkili tüm hello abonelik listesi.</span><span class="sxs-lookup"><span data-stu-id="e1064-141">Connect tooyour Azure account and list all hello subscriptions associated with your account.</span></span>
3. <span data-ttu-id="e1064-142">Merhaba veritabanı toobe geri içeren hello aboneliği seçin.</span><span class="sxs-lookup"><span data-stu-id="e1064-142">Select hello subscription that contains hello database toobe restored.</span></span>
4. <span data-ttu-id="e1064-143">İstediğiniz hello veritabanı toorecover alın.</span><span class="sxs-lookup"><span data-stu-id="e1064-143">Get hello database you want toorecover.</span></span>
5. <span data-ttu-id="e1064-144">Merhaba kurtarma isteği hello veritabanı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e1064-144">Create hello recovery request for hello database.</span></span>
6. <span data-ttu-id="e1064-145">Merhaba coğrafi geri yüklenen veritabanı Hello durumunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="e1064-145">Verify hello status of hello geo-restored database.</span></span>

```Powershell
Login-AzureRmAccount
Get-AzureRmSubscription
Select-AzureRmSubscription -SubscriptionName "<Subscription_name>"

# Get hello database you want toorecover
$GeoBackup = Get-AzureRmSqlDatabaseGeoBackup -ResourceGroupName "<YourResourceGroupName>" -ServerName "<YourServerName>" -DatabaseName "<YourDatabaseName>"

# Recover database
$GeoRestoredDatabase = Restore-AzureRmSqlDatabase –FromGeoBackup -ResourceGroupName "<YourResourceGroupName>" -ServerName "<YourTargetServer>" -TargetDatabaseName "<NewDatabaseName>" –ResourceId $GeoBackup.ResourceID

# Verify that hello geo-restored database is online
$GeoRestoredDatabase.status
```

> [!NOTE]
> <span data-ttu-id="e1064-146">Merhaba geri yükleme tamamlandıktan sonra veritabanınızı tooconfigure bkz [kurtarma işleminden sonra veritabanını yapılandırma][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="e1064-146">tooconfigure your database after hello restore has completed, see [Configure your database after recovery][Configure your database after recovery].</span></span>
> 
> 

<span data-ttu-id="e1064-147">Merhaba kaynak veritabanı TDE etkinse hello kurtarılan veritabanı TDE etkin olacaktır.</span><span class="sxs-lookup"><span data-stu-id="e1064-147">hello recovered database will be TDE-enabled if hello source database is TDE-enabled.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e1064-148">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e1064-148">Next steps</span></span>
<span data-ttu-id="e1064-149">Azure SQL veritabanı sürümlerini hello iş sürekliliği özellikleri hakkında toolearn hello okuyun [Azure SQL Database iş sürekliliğine genel bakış][Azure SQL Database business continuity overview].</span><span class="sxs-lookup"><span data-stu-id="e1064-149">toolearn about hello business continuity features of Azure SQL Database editions, please read hello [Azure SQL Database business continuity overview][Azure SQL Database business continuity overview].</span></span>

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
[Configure your database after recovery]: ../sql-database/sql-database-disaster-recovery.md#configure-your-database-after-recovery

<!--MSDN references-->
[Restore-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt693390.aspx

<!--Other Web references-->
[Azure Portal]: https://portal.azure.com/
[Microsoft Web Platform Installer]: https://aka.ms/webpi-azps
