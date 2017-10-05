---
title: "Ve App Service uygulamalarının geri yükleme için PowerShell kullanma"
description: "Yedekleme ve geri yükleme Azure App Service'te bir uygulama için PowerShell kullanma hakkında bilgi edinin"
services: app-service
documentationcenter: 
author: NKing92
manager: erikre
editor: 
ms.assetid: 7ea8661e-aefb-4823-9626-6bff980cdebf
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2016
ms.author: nicking
ms.openlocfilehash: 34a7e1d025c301ca056753d964bb3c5f4f1a62d8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="use-powershell-to-back-up-and-restore-app-service-apps"></a><span data-ttu-id="633e6-103">Ve App Service uygulamalarının geri yükleme için PowerShell kullanma</span><span class="sxs-lookup"><span data-stu-id="633e6-103">Use PowerShell to back up and restore App Service apps</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="633e6-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="633e6-104">PowerShell</span></span>](app-service-powershell-backup.md)
> * [<span data-ttu-id="633e6-105">REST API</span><span class="sxs-lookup"><span data-stu-id="633e6-105">REST API</span></span>](../app-service-web/websites-csm-backup.md)
> 
> 

<span data-ttu-id="633e6-106">Yedekleme ve geri yükleme için Azure PowerShell kullanmayı öğrenin [App Service uygulamalarının](https://azure.microsoft.com/services/app-service/web/).</span><span class="sxs-lookup"><span data-stu-id="633e6-106">Learn how to use Azure PowerShell to back up and restore [App Service apps](https://azure.microsoft.com/services/app-service/web/).</span></span> <span data-ttu-id="633e6-107">Web uygulaması yedeklemeler, gereksinimleri ve kısıtlamaları dahil hakkında daha fazla bilgi için bkz: [Azure App Service'te bir web uygulaması yedekleme](../app-service-web/web-sites-backup.md).</span><span class="sxs-lookup"><span data-stu-id="633e6-107">For more information about web app backups, including requirements and restrictions, see [Back up a web app in Azure App Service](../app-service-web/web-sites-backup.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="633e6-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="633e6-108">Prerequisites</span></span>
<span data-ttu-id="633e6-109">Uygulama Yedeklemelerinizin yönetmek için PowerShell kullanmak için aşağıdakiler gerekir:</span><span class="sxs-lookup"><span data-stu-id="633e6-109">To use PowerShell to manage your app backups, you need the following:</span></span>

* <span data-ttu-id="633e6-110">**Bir SAS URL'si** okuma ve bir Azure Storage kapsayıcısına yazma erişimi sağlar.</span><span class="sxs-lookup"><span data-stu-id="633e6-110">**A SAS URL** that allows read and write access to an Azure Storage container.</span></span> <span data-ttu-id="633e6-111">Bkz: [SAS modelini anlama](../storage/common/storage-dotnet-shared-access-signature-part-1.md) SAS URL'leri açıklaması için.</span><span class="sxs-lookup"><span data-stu-id="633e6-111">See [Understanding the SAS model](../storage/common/storage-dotnet-shared-access-signature-part-1.md) for an explanation of SAS URLs.</span></span> <span data-ttu-id="633e6-112">Bkz: [Azure Storage ile Azure PowerShell'i kullanma](../storage/common/storage-powershell-guide-full.md) Azure PowerShell kullanarak depolama yönetme örnekler.</span><span class="sxs-lookup"><span data-stu-id="633e6-112">See [Using Azure PowerShell with Azure Storage](../storage/common/storage-powershell-guide-full.md) for examples of managing Azure Storage using PowerShell.</span></span>
* <span data-ttu-id="633e6-113">**Bir veritabanı bağlantı dizesi** web uygulamanızı birlikte bir veritabanı yedeklemek istiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="633e6-113">**A database connection string** if you want to back up a database along with your web app.</span></span>

### <a name="how-to-generate-a-sas-url-to-use-with-the-web-app-backup-cmdlets"></a><span data-ttu-id="633e6-114">Web uygulaması Yedekleme cmdlet ile birlikte kullanmak için bir SAS URL'si oluşturmak nasıl</span><span class="sxs-lookup"><span data-stu-id="633e6-114">How to generate a SAS URL to use with the web app backup cmdlets</span></span>
<span data-ttu-id="633e6-115">Bir SAS URL'si PowerShell ile oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="633e6-115">A SAS URL can be generated with PowerShell.</span></span> <span data-ttu-id="633e6-116">Bu makalede açıklanan cmdlet'leri ile birlikte kullanılabilen bir oluşturmak nasıl bir örneği burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="633e6-116">Here is an example of how to generate one that can be used with the cmdlets discussed in this article.</span></span>

        $storageAccountName = "<your storage account's name>"
        $storageAccountRg = "<your storage account's resource group>"

        # This returns an array of keys for your storage account. Be sure to select the appropriate key. Here we select the first key as a default.
        $storageAccountKey = Get-AzureRmStorageAccountKey -ResourceGroupName $storageAccountRg -Name $storageAccountName
        $context = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey[0].Value

        $blobContainerName = "<name of blob container for app backups>"
        $sasUrl = New-AzureStorageContainerSASToken -Name $blobContainerName -Permission rwdl -Context $context -ExpiryTime (Get-Date).AddMonths(1) -FullUri

## <a name="install-azure-powershell-132-or-greater"></a><span data-ttu-id="633e6-117">Azure PowerShell 1.3.2 yüklemek veya daha büyük</span><span class="sxs-lookup"><span data-stu-id="633e6-117">Install Azure PowerShell 1.3.2 or greater</span></span>
<span data-ttu-id="633e6-118">Bkz: [Azure PowerShell kullanarak Azure Resource Manager ile](/powershell/azure/overview) yükleme ve Azure PowerShell kullanma hakkında yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="633e6-118">See [Using Azure PowerShell with Azure Resource Manager](/powershell/azure/overview) for instructions on installing and using Azure PowerShell.</span></span>

## <a name="create-a-backup"></a><span data-ttu-id="633e6-119">Bir yedekleme oluşturun</span><span class="sxs-lookup"><span data-stu-id="633e6-119">Create a backup</span></span>
<span data-ttu-id="633e6-120">Web uygulamasının bir yedekleme oluşturmak için New-AzureRmWebAppBackup cmdlet'ini kullanın.</span><span class="sxs-lookup"><span data-stu-id="633e6-120">Use the New-AzureRmWebAppBackup cmdlet to create a backup of a web app.</span></span>

        $sasUrl = "<your SAS URL>"
        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"

        $backup = New-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -StorageAccountUrl $sasUrl

<span data-ttu-id="633e6-121">Bu, otomatik olarak oluşturulan bir adla bir yedek oluşturur.</span><span class="sxs-lookup"><span data-stu-id="633e6-121">This creates a backup with an automatically generated name.</span></span> <span data-ttu-id="633e6-122">Yedekleme için bir ad sağlamak istiyorsanız YedekAdı isteğe bağlı parametresini kullanın.</span><span class="sxs-lookup"><span data-stu-id="633e6-122">If you would like to provide a name for your backup, use the BackupName optional parameter.</span></span>

        $backup = New-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -StorageAccountUrl $sasUrl -BackupName MyBackup

<span data-ttu-id="633e6-123">Bir veritabanını yedeklemeye dahil edilecek ilk yeni AzureRmWebAppDatabaseBackupSetting cmdlet'ini kullanarak bir veritabanı yedekleme ayarı oluşturun ve sonra bu ayar yeni AzureRmWebAppBackup cmdlet'in veritabanları parametresinde sağlamak.</span><span class="sxs-lookup"><span data-stu-id="633e6-123">To include a database in the backup, first create a database backup setting using the New-AzureRmWebAppDatabaseBackupSetting cmdlet, then supply that setting in the Databases parameter of the New-AzureRmWebAppBackup cmdlet.</span></span> <span data-ttu-id="633e6-124">Veritabanları parametresi veritabanı ayarlarını, birden fazla veritabanını yedeklemek sağlayan bir dizi kabul eder.</span><span class="sxs-lookup"><span data-stu-id="633e6-124">The Databases parameter accepts an array of database settings, allowing you to back up more than one database.</span></span>

        $dbSetting1 = New-AzureRmWebAppDatabaseBackupSetting -Name DB1 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbSetting2 = New-AzureRmWebAppDatabaseBackupSetting -Name DB2 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbBackup = New-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -BackupName MyBackup -StorageAccountUrl $sasUrl -Databases $dbSetting1,$dbSetting2

## <a name="get-backups"></a><span data-ttu-id="633e6-125">Yedeklemeleri Al</span><span class="sxs-lookup"><span data-stu-id="633e6-125">Get backups</span></span>
<span data-ttu-id="633e6-126">Get-AzureRmWebAppBackupList cmdlet'i tüm yedeklemeler bir web uygulaması için bir dizi döndürür.</span><span class="sxs-lookup"><span data-stu-id="633e6-126">The Get-AzureRmWebAppBackupList cmdlet returns an array of all backups for a web app.</span></span> <span data-ttu-id="633e6-127">Web uygulaması ve kaynak grubu adı sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="633e6-127">You must supply the name of the web app and its resource group.</span></span>

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        $backups = Get-AzureRmWebAppBackupList -Name $appName -ResourceGroupName $resourceGroupName

<span data-ttu-id="633e6-128">Belirli bir yedek almak için Get-AzureRmWebAppBackup cmdlet'ini kullanın.</span><span class="sxs-lookup"><span data-stu-id="633e6-128">To get a specific backup, use the Get-AzureRmWebAppBackup cmdlet.</span></span>

        $backup = Get-AzureRmWebAppBackup -Name $appName -ResourceGroupName $resourceGroupName -BackupId 10102

<span data-ttu-id="633e6-129">Bir web uygulaması nesnesi, kolaylık sağlamak için Yedekleme Yönetimi cmdlet'leri hiçbirine de iletebildiğiniz.</span><span class="sxs-lookup"><span data-stu-id="633e6-129">You can also pipe a web app object into any of the backup management cmdlets for convenience.</span></span>

        $app = Get-AzureRmWebApp -Name ContosoApp -ResourceGroupName Default-Web-WestUS
        $backupList = $app | Get-AzureRmWebAppBackupList
        $backup = $app | Get-AzureRmWebAppBackup -BackupId 10102

## <a name="schedule-automatic-backups"></a><span data-ttu-id="633e6-130">Otomatik yedeklemeler zamanlama</span><span class="sxs-lookup"><span data-stu-id="633e6-130">Schedule automatic backups</span></span>
<span data-ttu-id="633e6-131">Belirli aralıklarla otomatik olarak gerçekleştirilmesi için yedeklemeler zamanlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="633e6-131">You can schedule backups to happen automatically at a specified interval.</span></span> <span data-ttu-id="633e6-132">Yedekleme zamanlamasını yapılandırmak için düzenleme AzureRmWebAppBackupConfiguration cmdlet'ini kullanın.</span><span class="sxs-lookup"><span data-stu-id="633e6-132">To configure a backup schedule, use the Edit-AzureRmWebAppBackupConfiguration cmdlet.</span></span> <span data-ttu-id="633e6-133">Bu cmdlet birkaç parametre alır:</span><span class="sxs-lookup"><span data-stu-id="633e6-133">This cmdlet takes several parameters:</span></span>

* <span data-ttu-id="633e6-134">**Ad** -web uygulamasının adı.</span><span class="sxs-lookup"><span data-stu-id="633e6-134">**Name** - The name of the web app.</span></span>
* <span data-ttu-id="633e6-135">**ResourceGroupName** -web uygulamasını içeren kaynak grubunun adı.</span><span class="sxs-lookup"><span data-stu-id="633e6-135">**ResourceGroupName** - The name of the resource group containing the web app.</span></span>
* <span data-ttu-id="633e6-136">**Yuva** - isteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="633e6-136">**Slot** - Optional.</span></span> <span data-ttu-id="633e6-137">Web uygulaması yuvası adı.</span><span class="sxs-lookup"><span data-stu-id="633e6-137">The name of the web app slot.</span></span>
* <span data-ttu-id="633e6-138">**StorageAccountUrl** -yedeklemelerini depolamak için kullanılan Azure depolama kapsayıcısı için SAS URL.</span><span class="sxs-lookup"><span data-stu-id="633e6-138">**StorageAccountUrl** - The SAS URL for the Azure Storage container used to store the backups.</span></span>
* <span data-ttu-id="633e6-139">**FrequencyInterval** -yedeklemelerin ne sıklıkta yapılmalıdır için sayısal bir değer.</span><span class="sxs-lookup"><span data-stu-id="633e6-139">**FrequencyInterval** - Numeric value for how often the backups should be made.</span></span> <span data-ttu-id="633e6-140">Pozitif bir tamsayı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="633e6-140">Must be a positive integer.</span></span>
* <span data-ttu-id="633e6-141">**FrequencyUnit** -yedeklemelerin ne sıklıkta yapılmalıdır için zaman birimi.</span><span class="sxs-lookup"><span data-stu-id="633e6-141">**FrequencyUnit** - Unit of time for how often the backups should be made.</span></span> <span data-ttu-id="633e6-142">Seçenekler şunlardır: saat ve günü.</span><span class="sxs-lookup"><span data-stu-id="633e6-142">Options are Hour and Day.</span></span>
* <span data-ttu-id="633e6-143">**RetentionPeriodInDays** - kaç gün Otomatik yedeklemeleri otomatik olarak silinmeden önce kaydedilmesi.</span><span class="sxs-lookup"><span data-stu-id="633e6-143">**RetentionPeriodInDays** - How many days the automatic backups should be saved before being automatically deleted.</span></span>
* <span data-ttu-id="633e6-144">**StartTime** - isteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="633e6-144">**StartTime** - Optional.</span></span> <span data-ttu-id="633e6-145">Otomatik yedekleme ne zaman başlaması gereken süre.</span><span class="sxs-lookup"><span data-stu-id="633e6-145">The time when the automatic backups should begin.</span></span> <span data-ttu-id="633e6-146">Bu null ise yedeklemeleri hemen başlayın.</span><span class="sxs-lookup"><span data-stu-id="633e6-146">Backups begin immediately if this is null.</span></span> <span data-ttu-id="633e6-147">Bir tarih saat olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="633e6-147">Must be a DateTime.</span></span>
* <span data-ttu-id="633e6-148">**Veritabanlarını** - isteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="633e6-148">**Databases** - Optional.</span></span> <span data-ttu-id="633e6-149">Veritabanlarını yedeklemek için DatabaseBackupSettings dizisi.</span><span class="sxs-lookup"><span data-stu-id="633e6-149">An array of DatabaseBackupSettings for the databases to backup.</span></span>
* <span data-ttu-id="633e6-150">**KeepAtLeastOneBackup** - isteğe bağlı parametre geçti.</span><span class="sxs-lookup"><span data-stu-id="633e6-150">**KeepAtLeastOneBackup** - Optional switched parameter.</span></span> <span data-ttu-id="633e6-151">Bu, kaynağı bir yedekleme her zaman saklanması kaç yaşında olduğunu bağımsız olarak depolama hesabındaki.</span><span class="sxs-lookup"><span data-stu-id="633e6-151">Supply this if one backup should always be kept in the storage account, regardless of how old it is.</span></span>

<span data-ttu-id="633e6-152">Bu cmdlet'in nasıl kullanılacağı örneği verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="633e6-152">Following is an example of how to use this cmdlet.</span></span>

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        $slotName = "StagingSlot"
        $dbSetting1 = New-AzureRmWebAppDatabaseBackupSetting -Name DB1 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbSetting2 = New-AzureRmWebAppDatabaseBackupSetting -Name DB2 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        Edit-AzureRmWebAppBackupConfiguration -Name $appName -ResourceGroupName $resourceGroupName -Slot $slotName `
          -StorageAccountUrl "<your SAS URL>" -FrequencyInterval 6 -FrequencyUnit Hour -Databases $dbSetting1,$dbSetting2 `
          -KeepAtLeastOneBackup -StartTime (Get-Date).AddHours(1)

<span data-ttu-id="633e6-153">Geçerli yedekleme zamanlamasını almak için Get-AzureRmWebAppBackupConfiguration cmdlet'ini kullanın.</span><span class="sxs-lookup"><span data-stu-id="633e6-153">To get the current backup schedule, use the Get-AzureRmWebAppBackupConfiguration cmdlet.</span></span> <span data-ttu-id="633e6-154">Bu, önceden yapılandırılmış bir zamanlamayı değiştirmek için yararlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="633e6-154">This can be useful for modifying a schedule that has already been configured.</span></span>

        $configuration = Get-AzureRmWebAppBackupConfiguration -Name $appName -ResourceGroupName $resourceGroupName

        # Modify the configuration slightly
        $configuration.FrequencyInterval = 2
        $configuration.FrequencyUnit = "Day"

        # Apply the new configuration by piping it into the Edit-AzureRmWebAppBackupConfiguration cmdlet
        $configuration | Edit-AzureRmWebAppBackupConfiguration

## <a name="restore-a-web-app-from-a-backup"></a><span data-ttu-id="633e6-155">Bir web uygulaması bir yedekten geri yükleyin</span><span class="sxs-lookup"><span data-stu-id="633e6-155">Restore a web app from a backup</span></span>
<span data-ttu-id="633e6-156">Bir web uygulaması bir yedekten geri yüklemek için geri yükleme-AzureRmWebAppBackup cmdlet'ini kullanın.</span><span class="sxs-lookup"><span data-stu-id="633e6-156">To restore a web app from a backup, use the Restore-AzureRmWebAppBackup cmdlet.</span></span> <span data-ttu-id="633e6-157">Bu cmdlet kullanılarak en kolay yolu bir yedek nesnesinde kanal alınan Get-AzureRmWebAppBackup cmdlet veya Get-AzureRmWebAppBackupList cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="633e6-157">The easiest way to use this cmdlet is to pipe in a backup object retrieved from the Get-AzureRmWebAppBackup cmdlet or Get-AzureRmWebAppBackupList cmdlet.</span></span>

<span data-ttu-id="633e6-158">Bir yedekleme nesnesi olduktan sonra geri yükleme AzureRmWebAppBackup cmdlet'e iletebildiğiniz.</span><span class="sxs-lookup"><span data-stu-id="633e6-158">Once you have a backup object, you can pipe it into the Restore-AzureRmWebAppBackup cmdlet.</span></span> <span data-ttu-id="633e6-159">Web uygulamanızın içeriğini yedekleme içeriğinin üzerine istediğinizi belirtmek için üzerine yazma anahtar parametresini belirtin.</span><span class="sxs-lookup"><span data-stu-id="633e6-159">Specify the Overwrite switch parameter to indicate that you intend to overwrite the contents of your web app with the contents of the backup.</span></span> <span data-ttu-id="633e6-160">Veritabanlarını yedekleme içeriyorsa, bu veritabanlarını da geri yüklenir.</span><span class="sxs-lookup"><span data-stu-id="633e6-160">If the backup contains databases, those databases are restored as well.</span></span>

        $backup | Restore-AzureRmWebAppBackup -Overwrite

<span data-ttu-id="633e6-161">Aşağıdaki, tüm parametreleri belirterek geri yükleme AzureRmWebAppBackup kullanmayı örneğidir.</span><span class="sxs-lookup"><span data-stu-id="633e6-161">Following is an example of how to use the Restore-AzureRmWebAppBackup by specifying all the parameters.</span></span>

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        $slotName = "StagingSlot"
        $blobName = "ContosoBackup.zip"
        $dbSetting1 = New-AzureRmWebAppDatabaseBackupSetting -Name DB1 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbSetting2 = New-AzureRmWebAppDatabaseBackupSetting -Name DB2 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        Restore-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -Slot $slotName -StorageAccountUrl "<your SAS URL>" -BlobName $blobName -Databases $dbSetting1,$dbSetting2 -Overwrite

## <a name="delete-a-backup"></a><span data-ttu-id="633e6-162">Yedek Sil</span><span class="sxs-lookup"><span data-stu-id="633e6-162">Delete a backup</span></span>
<span data-ttu-id="633e6-163">Bir yedekleme silmek için Remove-AzureRmWebAppBackup cmdlet'ini kullanın.</span><span class="sxs-lookup"><span data-stu-id="633e6-163">To delete a backup, use the Remove-AzureRmWebAppBackup cmdlet.</span></span> <span data-ttu-id="633e6-164">Bu yedekleme depolama hesabınızdan siler.</span><span class="sxs-lookup"><span data-stu-id="633e6-164">This removes the backup from your storage account.</span></span> <span data-ttu-id="633e6-165">Uygulama adı, kaynak grubu ve silmek istediğiniz yedekleme Kimliğini belirtin.</span><span class="sxs-lookup"><span data-stu-id="633e6-165">Specify your app name, its resource group, and the ID of the backup you want to delete.</span></span>

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        Remove-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -BackupId 10102

<span data-ttu-id="633e6-166">Bir yedek nesnesini silmek için Remove-AzureRmWebAppBackup cmdlet'e de iletebildiğiniz.</span><span class="sxs-lookup"><span data-stu-id="633e6-166">You can also pipe a backup object into the Remove-AzureRmWebAppBackup cmdlet to delete it.</span></span>

        $backup = Get-AzureRmWebAppBackup -Name $appName -ResourceGroupName $resourceGroupName -BackupId 10102
        $backup | Remove-AzureRmWebAppBackup -Overwrite
