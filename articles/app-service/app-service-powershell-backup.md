---
title: "aaaUse PowerShell tooback ayarlama ve uygulama hizmeti uygulamalar geri yükleme"
description: "Bilgi nasıl toouse PowerShell tooback ayarlama ve Azure App Service'te bir uygulama geri yükleme"
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
ms.openlocfilehash: 4042166f6c650841926f010056d6c80ab2de57e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-tooback-up-and-restore-app-service-apps"></a><span data-ttu-id="a88e6-103">PowerShell tooback kullanır ve App Service uygulamalarının geri yükleme</span><span class="sxs-lookup"><span data-stu-id="a88e6-103">Use PowerShell tooback up and restore App Service apps</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a88e6-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a88e6-104">PowerShell</span></span>](app-service-powershell-backup.md)
> * [<span data-ttu-id="a88e6-105">REST API</span><span class="sxs-lookup"><span data-stu-id="a88e6-105">REST API</span></span>](../app-service-web/websites-csm-backup.md)
> 
> 

<span data-ttu-id="a88e6-106">Bilgi nasıl toouse Azure PowerShell tooback ayarlama ve geri yükleme [App Service uygulamalarının](https://azure.microsoft.com/services/app-service/web/).</span><span class="sxs-lookup"><span data-stu-id="a88e6-106">Learn how toouse Azure PowerShell tooback up and restore [App Service apps](https://azure.microsoft.com/services/app-service/web/).</span></span> <span data-ttu-id="a88e6-107">Web uygulaması yedeklemeler, gereksinimleri ve kısıtlamaları dahil hakkında daha fazla bilgi için bkz: [Azure App Service'te bir web uygulaması yedekleme](../app-service-web/web-sites-backup.md).</span><span class="sxs-lookup"><span data-stu-id="a88e6-107">For more information about web app backups, including requirements and restrictions, see [Back up a web app in Azure App Service](../app-service-web/web-sites-backup.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a88e6-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="a88e6-108">Prerequisites</span></span>
<span data-ttu-id="a88e6-109">toouse PowerShell toomanage uygulama Yedeklemelerinizin aşağıdaki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="a88e6-109">toouse PowerShell toomanage your app backups, you need hello following:</span></span>

* <span data-ttu-id="a88e6-110">**Bir SAS URL'si** okuma ve yazma erişimi tooan Azure depolama kapsayıcısı sağlar.</span><span class="sxs-lookup"><span data-stu-id="a88e6-110">**A SAS URL** that allows read and write access tooan Azure Storage container.</span></span> <span data-ttu-id="a88e6-111">Bkz: [anlama hello SAS modelini](../storage/common/storage-dotnet-shared-access-signature-part-1.md) SAS URL'leri açıklaması için.</span><span class="sxs-lookup"><span data-stu-id="a88e6-111">See [Understanding hello SAS model](../storage/common/storage-dotnet-shared-access-signature-part-1.md) for an explanation of SAS URLs.</span></span> <span data-ttu-id="a88e6-112">Bkz: [Azure Storage ile Azure PowerShell'i kullanma](../storage/common/storage-powershell-guide-full.md) Azure PowerShell kullanarak depolama yönetme örnekler.</span><span class="sxs-lookup"><span data-stu-id="a88e6-112">See [Using Azure PowerShell with Azure Storage](../storage/common/storage-powershell-guide-full.md) for examples of managing Azure Storage using PowerShell.</span></span>
* <span data-ttu-id="a88e6-113">**Bir veritabanı bağlantı dizesi** yanı sıra, web uygulamanızın bir veritabanını tooback istiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="a88e6-113">**A database connection string** if you want tooback up a database along with your web app.</span></span>

### <a name="how-toogenerate-a-sas-url-toouse-with-hello-web-app-backup-cmdlets"></a><span data-ttu-id="a88e6-114">Nasıl toogenerate bir SAS URL'si toouse hello web uygulaması ile yedekleme cmdlet'leri</span><span class="sxs-lookup"><span data-stu-id="a88e6-114">How toogenerate a SAS URL toouse with hello web app backup cmdlets</span></span>
<span data-ttu-id="a88e6-115">Bir SAS URL'si PowerShell ile oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="a88e6-115">A SAS URL can be generated with PowerShell.</span></span> <span data-ttu-id="a88e6-116">Burada, nasıl toogenerate hello cmdlet ile birlikte kullanılan bir bu makalede ele alınan bir örnek verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="a88e6-116">Here is an example of how toogenerate one that can be used with hello cmdlets discussed in this article.</span></span>

        $storageAccountName = "<your storage account's name>"
        $storageAccountRg = "<your storage account's resource group>"

        # This returns an array of keys for your storage account. Be sure tooselect hello appropriate key. Here we select hello first key as a default.
        $storageAccountKey = Get-AzureRmStorageAccountKey -ResourceGroupName $storageAccountRg -Name $storageAccountName
        $context = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey[0].Value

        $blobContainerName = "<name of blob container for app backups>"
        $sasUrl = New-AzureStorageContainerSASToken -Name $blobContainerName -Permission rwdl -Context $context -ExpiryTime (Get-Date).AddMonths(1) -FullUri

## <a name="install-azure-powershell-132-or-greater"></a><span data-ttu-id="a88e6-117">Azure PowerShell 1.3.2 yüklemek veya daha büyük</span><span class="sxs-lookup"><span data-stu-id="a88e6-117">Install Azure PowerShell 1.3.2 or greater</span></span>
<span data-ttu-id="a88e6-118">Bkz: [Azure PowerShell kullanarak Azure Resource Manager ile](/powershell/azure/overview) yükleme ve Azure PowerShell kullanma hakkında yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="a88e6-118">See [Using Azure PowerShell with Azure Resource Manager](/powershell/azure/overview) for instructions on installing and using Azure PowerShell.</span></span>

## <a name="create-a-backup"></a><span data-ttu-id="a88e6-119">Bir yedekleme oluşturun</span><span class="sxs-lookup"><span data-stu-id="a88e6-119">Create a backup</span></span>
<span data-ttu-id="a88e6-120">Merhaba yeni AzureRmWebAppBackup cmdlet toocreate bir web uygulaması yedeğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="a88e6-120">Use hello New-AzureRmWebAppBackup cmdlet toocreate a backup of a web app.</span></span>

        $sasUrl = "<your SAS URL>"
        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"

        $backup = New-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -StorageAccountUrl $sasUrl

<span data-ttu-id="a88e6-121">Bu, otomatik olarak oluşturulan bir adla bir yedek oluşturur.</span><span class="sxs-lookup"><span data-stu-id="a88e6-121">This creates a backup with an automatically generated name.</span></span> <span data-ttu-id="a88e6-122">Yedekleme için bir ad tooprovide isterseniz hello YedekAdı isteğe bağlı parametresini kullanın.</span><span class="sxs-lookup"><span data-stu-id="a88e6-122">If you would like tooprovide a name for your backup, use hello BackupName optional parameter.</span></span>

        $backup = New-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -StorageAccountUrl $sasUrl -BackupName MyBackup

<span data-ttu-id="a88e6-123">tooinclude hello yedekleme, bir veritabanına ilk hello yeni AzureRmWebAppDatabaseBackupSetting cmdlet'ini kullanarak bir veritabanı yedekleme ayarı oluşturun ve sonra veritabanları parametresi hello yeni AzureRmWebAppBackup cmdlet, ayarı hello sağlayın.</span><span class="sxs-lookup"><span data-stu-id="a88e6-123">tooinclude a database in hello backup, first create a database backup setting using hello New-AzureRmWebAppDatabaseBackupSetting cmdlet, then supply that setting in hello Databases parameter of hello New-AzureRmWebAppBackup cmdlet.</span></span> <span data-ttu-id="a88e6-124">Merhaba veritabanları parametresi veritabanı ayarlarını, birden fazla veritabanını tooback sağlayan bir dizi kabul eder.</span><span class="sxs-lookup"><span data-stu-id="a88e6-124">hello Databases parameter accepts an array of database settings, allowing you tooback up more than one database.</span></span>

        $dbSetting1 = New-AzureRmWebAppDatabaseBackupSetting -Name DB1 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbSetting2 = New-AzureRmWebAppDatabaseBackupSetting -Name DB2 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbBackup = New-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -BackupName MyBackup -StorageAccountUrl $sasUrl -Databases $dbSetting1,$dbSetting2

## <a name="get-backups"></a><span data-ttu-id="a88e6-125">Yedeklemeleri Al</span><span class="sxs-lookup"><span data-stu-id="a88e6-125">Get backups</span></span>
<span data-ttu-id="a88e6-126">Merhaba Get-AzureRmWebAppBackupList cmdlet'i tüm yedeklemeler bir web uygulaması için bir dizi döndürür.</span><span class="sxs-lookup"><span data-stu-id="a88e6-126">hello Get-AzureRmWebAppBackupList cmdlet returns an array of all backups for a web app.</span></span> <span data-ttu-id="a88e6-127">Merhaba hello web uygulaması adını ve kaynak grubu sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="a88e6-127">You must supply hello name of hello web app and its resource group.</span></span>

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        $backups = Get-AzureRmWebAppBackupList -Name $appName -ResourceGroupName $resourceGroupName

<span data-ttu-id="a88e6-128">belirli bir yedekleme tooget hello Get-AzureRmWebAppBackup cmdlet'ini kullanın.</span><span class="sxs-lookup"><span data-stu-id="a88e6-128">tooget a specific backup, use hello Get-AzureRmWebAppBackup cmdlet.</span></span>

        $backup = Get-AzureRmWebAppBackup -Name $appName -ResourceGroupName $resourceGroupName -BackupId 10102

<span data-ttu-id="a88e6-129">Bir web uygulaması nesnesi, kolaylık sağlamak için hello Yedekleme Yönetimi cmdlet'leri hiçbirine de iletebildiğiniz.</span><span class="sxs-lookup"><span data-stu-id="a88e6-129">You can also pipe a web app object into any of hello backup management cmdlets for convenience.</span></span>

        $app = Get-AzureRmWebApp -Name ContosoApp -ResourceGroupName Default-Web-WestUS
        $backupList = $app | Get-AzureRmWebAppBackupList
        $backup = $app | Get-AzureRmWebAppBackup -BackupId 10102

## <a name="schedule-automatic-backups"></a><span data-ttu-id="a88e6-130">Otomatik yedeklemeler zamanlama</span><span class="sxs-lookup"><span data-stu-id="a88e6-130">Schedule automatic backups</span></span>
<span data-ttu-id="a88e6-131">Yedeklemeleri toohappen belirli aralıklarla otomatik olarak zamanlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a88e6-131">You can schedule backups toohappen automatically at a specified interval.</span></span> <span data-ttu-id="a88e6-132">tooconfigure bir yedekleme zamanlaması hello düzenleme AzureRmWebAppBackupConfiguration cmdlet'ini kullanın.</span><span class="sxs-lookup"><span data-stu-id="a88e6-132">tooconfigure a backup schedule, use hello Edit-AzureRmWebAppBackupConfiguration cmdlet.</span></span> <span data-ttu-id="a88e6-133">Bu cmdlet birkaç parametre alır:</span><span class="sxs-lookup"><span data-stu-id="a88e6-133">This cmdlet takes several parameters:</span></span>

* <span data-ttu-id="a88e6-134">**Ad** - hello hello web uygulamasının adı.</span><span class="sxs-lookup"><span data-stu-id="a88e6-134">**Name** - hello name of hello web app.</span></span>
* <span data-ttu-id="a88e6-135">**ResourceGroupName** - hello hello kaynak grubu içeren hello web uygulamasının adı.</span><span class="sxs-lookup"><span data-stu-id="a88e6-135">**ResourceGroupName** - hello name of hello resource group containing hello web app.</span></span>
* <span data-ttu-id="a88e6-136">**Yuva** - isteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="a88e6-136">**Slot** - Optional.</span></span> <span data-ttu-id="a88e6-137">Merhaba web uygulaması yuvası Hello adı.</span><span class="sxs-lookup"><span data-stu-id="a88e6-137">hello name of hello web app slot.</span></span>
* <span data-ttu-id="a88e6-138">**StorageAccountUrl** -toostore hello yedeklemeleri hello Azure depolama kapsayıcısının kullanılan SAS URL hello.</span><span class="sxs-lookup"><span data-stu-id="a88e6-138">**StorageAccountUrl** - hello SAS URL for hello Azure Storage container used toostore hello backups.</span></span>
* <span data-ttu-id="a88e6-139">**FrequencyInterval** -ne sıklıkta hello yedeklemeleri yapılmalıdır için sayısal bir değer.</span><span class="sxs-lookup"><span data-stu-id="a88e6-139">**FrequencyInterval** - Numeric value for how often hello backups should be made.</span></span> <span data-ttu-id="a88e6-140">Pozitif bir tamsayı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="a88e6-140">Must be a positive integer.</span></span>
* <span data-ttu-id="a88e6-141">**FrequencyUnit** -ne sıklıkta hello yedeklemeleri yapılmalıdır için zaman birimi.</span><span class="sxs-lookup"><span data-stu-id="a88e6-141">**FrequencyUnit** - Unit of time for how often hello backups should be made.</span></span> <span data-ttu-id="a88e6-142">Seçenekler şunlardır: saat ve günü.</span><span class="sxs-lookup"><span data-stu-id="a88e6-142">Options are Hour and Day.</span></span>
* <span data-ttu-id="a88e6-143">**RetentionPeriodInDays** - kaç gün hello otomatik yedeklemeler otomatik olarak silinmeden önce kaydedilmesi.</span><span class="sxs-lookup"><span data-stu-id="a88e6-143">**RetentionPeriodInDays** - How many days hello automatic backups should be saved before being automatically deleted.</span></span>
* <span data-ttu-id="a88e6-144">**StartTime** - isteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="a88e6-144">**StartTime** - Optional.</span></span> <span data-ttu-id="a88e6-145">Merhaba otomatik yedeklemeler ne zaman başlaması gereken başlangıç zamanı.</span><span class="sxs-lookup"><span data-stu-id="a88e6-145">hello time when hello automatic backups should begin.</span></span> <span data-ttu-id="a88e6-146">Bu null ise yedeklemeleri hemen başlayın.</span><span class="sxs-lookup"><span data-stu-id="a88e6-146">Backups begin immediately if this is null.</span></span> <span data-ttu-id="a88e6-147">Bir tarih saat olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="a88e6-147">Must be a DateTime.</span></span>
* <span data-ttu-id="a88e6-148">**Veritabanlarını** - isteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="a88e6-148">**Databases** - Optional.</span></span> <span data-ttu-id="a88e6-149">DatabaseBackupSettings dizisi hello veritabanları toobackup için.</span><span class="sxs-lookup"><span data-stu-id="a88e6-149">An array of DatabaseBackupSettings for hello databases toobackup.</span></span>
* <span data-ttu-id="a88e6-150">**KeepAtLeastOneBackup** - isteğe bağlı parametre geçti.</span><span class="sxs-lookup"><span data-stu-id="a88e6-150">**KeepAtLeastOneBackup** - Optional switched parameter.</span></span> <span data-ttu-id="a88e6-151">Bu bir yedekleme her zaman korunması gerektiğini varsa hello depolama hesabı, bağımsız olarak kaç yaşında olduğunu sağlayın.</span><span class="sxs-lookup"><span data-stu-id="a88e6-151">Supply this if one backup should always be kept in hello storage account, regardless of how old it is.</span></span>

<span data-ttu-id="a88e6-152">Aşağıdaki nasıl örneğidir toouse Bu cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="a88e6-152">Following is an example of how toouse this cmdlet.</span></span>

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        $slotName = "StagingSlot"
        $dbSetting1 = New-AzureRmWebAppDatabaseBackupSetting -Name DB1 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbSetting2 = New-AzureRmWebAppDatabaseBackupSetting -Name DB2 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        Edit-AzureRmWebAppBackupConfiguration -Name $appName -ResourceGroupName $resourceGroupName -Slot $slotName `
          -StorageAccountUrl "<your SAS URL>" -FrequencyInterval 6 -FrequencyUnit Hour -Databases $dbSetting1,$dbSetting2 `
          -KeepAtLeastOneBackup -StartTime (Get-Date).AddHours(1)

<span data-ttu-id="a88e6-153">tooget hello geçerli yedekleme zamanlamasını, hello Get-AzureRmWebAppBackupConfiguration cmdlet'ini kullanın.</span><span class="sxs-lookup"><span data-stu-id="a88e6-153">tooget hello current backup schedule, use hello Get-AzureRmWebAppBackupConfiguration cmdlet.</span></span> <span data-ttu-id="a88e6-154">Bu, önceden yapılandırılmış bir zamanlamayı değiştirmek için yararlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="a88e6-154">This can be useful for modifying a schedule that has already been configured.</span></span>

        $configuration = Get-AzureRmWebAppBackupConfiguration -Name $appName -ResourceGroupName $resourceGroupName

        # Modify hello configuration slightly
        $configuration.FrequencyInterval = 2
        $configuration.FrequencyUnit = "Day"

        # Apply hello new configuration by piping it into hello Edit-AzureRmWebAppBackupConfiguration cmdlet
        $configuration | Edit-AzureRmWebAppBackupConfiguration

## <a name="restore-a-web-app-from-a-backup"></a><span data-ttu-id="a88e6-155">Bir web uygulaması bir yedekten geri yükleyin</span><span class="sxs-lookup"><span data-stu-id="a88e6-155">Restore a web app from a backup</span></span>
<span data-ttu-id="a88e6-156">toorestore bir web uygulaması bir yedekten geri yükleme AzureRmWebAppBackup hello cmdlet'ini kullanın.</span><span class="sxs-lookup"><span data-stu-id="a88e6-156">toorestore a web app from a backup, use hello Restore-AzureRmWebAppBackup cmdlet.</span></span> <span data-ttu-id="a88e6-157">Merhaba en kolay yolu toouse Bu cmdlet toopipe hello Get-AzureRmWebAppBackup cmdlet'ini veya Get-AzureRmWebAppBackupList cmdlet'i alınan bir yedek nesnesinde ' dir.</span><span class="sxs-lookup"><span data-stu-id="a88e6-157">hello easiest way toouse this cmdlet is toopipe in a backup object retrieved from hello Get-AzureRmWebAppBackup cmdlet or Get-AzureRmWebAppBackupList cmdlet.</span></span>

<span data-ttu-id="a88e6-158">Bir yedekleme nesnesi oluşturduktan sonra hello geri yükleme AzureRmWebAppBackup cmdlet'e iletebildiğiniz.</span><span class="sxs-lookup"><span data-stu-id="a88e6-158">Once you have a backup object, you can pipe it into hello Restore-AzureRmWebAppBackup cmdlet.</span></span> <span data-ttu-id="a88e6-159">Merhaba üzerine yaz anahtar parametresi tooindicate toooverwrite hello içeriğini web uygulamanızı hello yedekleme Merhaba içeriğine düşündüğünüz belirtin.</span><span class="sxs-lookup"><span data-stu-id="a88e6-159">Specify hello Overwrite switch parameter tooindicate that you intend toooverwrite hello contents of your web app with hello contents of hello backup.</span></span> <span data-ttu-id="a88e6-160">Merhaba yedekleme veritabanları içeriyorsa, bu veritabanlarını da geri yüklenir.</span><span class="sxs-lookup"><span data-stu-id="a88e6-160">If hello backup contains databases, those databases are restored as well.</span></span>

        $backup | Restore-AzureRmWebAppBackup -Overwrite

<span data-ttu-id="a88e6-161">Aşağıda nasıl toouse hello geri yükleme AzureRmWebAppBackup tüm hello parametrelerini belirterek, bir örnek verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="a88e6-161">Following is an example of how toouse hello Restore-AzureRmWebAppBackup by specifying all hello parameters.</span></span>

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        $slotName = "StagingSlot"
        $blobName = "ContosoBackup.zip"
        $dbSetting1 = New-AzureRmWebAppDatabaseBackupSetting -Name DB1 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbSetting2 = New-AzureRmWebAppDatabaseBackupSetting -Name DB2 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        Restore-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -Slot $slotName -StorageAccountUrl "<your SAS URL>" -BlobName $blobName -Databases $dbSetting1,$dbSetting2 -Overwrite

## <a name="delete-a-backup"></a><span data-ttu-id="a88e6-162">Yedek Sil</span><span class="sxs-lookup"><span data-stu-id="a88e6-162">Delete a backup</span></span>
<span data-ttu-id="a88e6-163">toodelete bir yedekleme hello Kaldır AzureRmWebAppBackup cmdlet'ini kullanın.</span><span class="sxs-lookup"><span data-stu-id="a88e6-163">toodelete a backup, use hello Remove-AzureRmWebAppBackup cmdlet.</span></span> <span data-ttu-id="a88e6-164">Bu depolama hesabınızdan hello yedekleme kaldırır.</span><span class="sxs-lookup"><span data-stu-id="a88e6-164">This removes hello backup from your storage account.</span></span> <span data-ttu-id="a88e6-165">Uygulama adınız, kendi kaynak grubu belirtin ve hello Kimliğini hello toodelete istediğiniz yedekleme.</span><span class="sxs-lookup"><span data-stu-id="a88e6-165">Specify your app name, its resource group, and hello ID of hello backup you want toodelete.</span></span>

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        Remove-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -BackupId 10102

<span data-ttu-id="a88e6-166">Bir yedekleme nesnesi hello Kaldır AzureRmWebAppBackup cmdlet toodelete iletebildiğiniz onu.</span><span class="sxs-lookup"><span data-stu-id="a88e6-166">You can also pipe a backup object into hello Remove-AzureRmWebAppBackup cmdlet toodelete it.</span></span>

        $backup = Get-AzureRmWebAppBackup -Name $appName -ResourceGroupName $resourceGroupName -BackupId 10102
        $backup | Remove-AzureRmWebAppBackup -Overwrite
