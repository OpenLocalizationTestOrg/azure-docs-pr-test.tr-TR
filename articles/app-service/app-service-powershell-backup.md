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
# <a name="use-powershell-tooback-up-and-restore-app-service-apps"></a>PowerShell tooback kullanır ve App Service uygulamalarının geri yükleme
> [!div class="op_single_selector"]
> * [PowerShell](app-service-powershell-backup.md)
> * [REST API](../app-service-web/websites-csm-backup.md)
> 
> 

Bilgi nasıl toouse Azure PowerShell tooback ayarlama ve geri yükleme [App Service uygulamalarının](https://azure.microsoft.com/services/app-service/web/). Web uygulaması yedeklemeler, gereksinimleri ve kısıtlamaları dahil hakkında daha fazla bilgi için bkz: [Azure App Service'te bir web uygulaması yedekleme](../app-service-web/web-sites-backup.md).

## <a name="prerequisites"></a>Ön koşullar
toouse PowerShell toomanage uygulama Yedeklemelerinizin aşağıdaki hello gerekir:

* **Bir SAS URL'si** okuma ve yazma erişimi tooan Azure depolama kapsayıcısı sağlar. Bkz: [anlama hello SAS modelini](../storage/common/storage-dotnet-shared-access-signature-part-1.md) SAS URL'leri açıklaması için. Bkz: [Azure Storage ile Azure PowerShell'i kullanma](../storage/common/storage-powershell-guide-full.md) Azure PowerShell kullanarak depolama yönetme örnekler.
* **Bir veritabanı bağlantı dizesi** yanı sıra, web uygulamanızın bir veritabanını tooback istiyorsanız.

### <a name="how-toogenerate-a-sas-url-toouse-with-hello-web-app-backup-cmdlets"></a>Nasıl toogenerate bir SAS URL'si toouse hello web uygulaması ile yedekleme cmdlet'leri
Bir SAS URL'si PowerShell ile oluşturulabilir. Burada, nasıl toogenerate hello cmdlet ile birlikte kullanılan bir bu makalede ele alınan bir örnek verilmiştir.

        $storageAccountName = "<your storage account's name>"
        $storageAccountRg = "<your storage account's resource group>"

        # This returns an array of keys for your storage account. Be sure tooselect hello appropriate key. Here we select hello first key as a default.
        $storageAccountKey = Get-AzureRmStorageAccountKey -ResourceGroupName $storageAccountRg -Name $storageAccountName
        $context = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey[0].Value

        $blobContainerName = "<name of blob container for app backups>"
        $sasUrl = New-AzureStorageContainerSASToken -Name $blobContainerName -Permission rwdl -Context $context -ExpiryTime (Get-Date).AddMonths(1) -FullUri

## <a name="install-azure-powershell-132-or-greater"></a>Azure PowerShell 1.3.2 yüklemek veya daha büyük
Bkz: [Azure PowerShell kullanarak Azure Resource Manager ile](/powershell/azure/overview) yükleme ve Azure PowerShell kullanma hakkında yönergeler için.

## <a name="create-a-backup"></a>Bir yedekleme oluşturun
Merhaba yeni AzureRmWebAppBackup cmdlet toocreate bir web uygulaması yedeğini kullanın.

        $sasUrl = "<your SAS URL>"
        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"

        $backup = New-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -StorageAccountUrl $sasUrl

Bu, otomatik olarak oluşturulan bir adla bir yedek oluşturur. Yedekleme için bir ad tooprovide isterseniz hello YedekAdı isteğe bağlı parametresini kullanın.

        $backup = New-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -StorageAccountUrl $sasUrl -BackupName MyBackup

tooinclude hello yedekleme, bir veritabanına ilk hello yeni AzureRmWebAppDatabaseBackupSetting cmdlet'ini kullanarak bir veritabanı yedekleme ayarı oluşturun ve sonra veritabanları parametresi hello yeni AzureRmWebAppBackup cmdlet, ayarı hello sağlayın. Merhaba veritabanları parametresi veritabanı ayarlarını, birden fazla veritabanını tooback sağlayan bir dizi kabul eder.

        $dbSetting1 = New-AzureRmWebAppDatabaseBackupSetting -Name DB1 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbSetting2 = New-AzureRmWebAppDatabaseBackupSetting -Name DB2 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbBackup = New-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -BackupName MyBackup -StorageAccountUrl $sasUrl -Databases $dbSetting1,$dbSetting2

## <a name="get-backups"></a>Yedeklemeleri Al
Merhaba Get-AzureRmWebAppBackupList cmdlet'i tüm yedeklemeler bir web uygulaması için bir dizi döndürür. Merhaba hello web uygulaması adını ve kaynak grubu sağlamanız gerekir.

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        $backups = Get-AzureRmWebAppBackupList -Name $appName -ResourceGroupName $resourceGroupName

belirli bir yedekleme tooget hello Get-AzureRmWebAppBackup cmdlet'ini kullanın.

        $backup = Get-AzureRmWebAppBackup -Name $appName -ResourceGroupName $resourceGroupName -BackupId 10102

Bir web uygulaması nesnesi, kolaylık sağlamak için hello Yedekleme Yönetimi cmdlet'leri hiçbirine de iletebildiğiniz.

        $app = Get-AzureRmWebApp -Name ContosoApp -ResourceGroupName Default-Web-WestUS
        $backupList = $app | Get-AzureRmWebAppBackupList
        $backup = $app | Get-AzureRmWebAppBackup -BackupId 10102

## <a name="schedule-automatic-backups"></a>Otomatik yedeklemeler zamanlama
Yedeklemeleri toohappen belirli aralıklarla otomatik olarak zamanlayabilirsiniz. tooconfigure bir yedekleme zamanlaması hello düzenleme AzureRmWebAppBackupConfiguration cmdlet'ini kullanın. Bu cmdlet birkaç parametre alır:

* **Ad** - hello hello web uygulamasının adı.
* **ResourceGroupName** - hello hello kaynak grubu içeren hello web uygulamasının adı.
* **Yuva** - isteğe bağlı. Merhaba web uygulaması yuvası Hello adı.
* **StorageAccountUrl** -toostore hello yedeklemeleri hello Azure depolama kapsayıcısının kullanılan SAS URL hello.
* **FrequencyInterval** -ne sıklıkta hello yedeklemeleri yapılmalıdır için sayısal bir değer. Pozitif bir tamsayı olmalıdır.
* **FrequencyUnit** -ne sıklıkta hello yedeklemeleri yapılmalıdır için zaman birimi. Seçenekler şunlardır: saat ve günü.
* **RetentionPeriodInDays** - kaç gün hello otomatik yedeklemeler otomatik olarak silinmeden önce kaydedilmesi.
* **StartTime** - isteğe bağlı. Merhaba otomatik yedeklemeler ne zaman başlaması gereken başlangıç zamanı. Bu null ise yedeklemeleri hemen başlayın. Bir tarih saat olmalıdır.
* **Veritabanlarını** - isteğe bağlı. DatabaseBackupSettings dizisi hello veritabanları toobackup için.
* **KeepAtLeastOneBackup** - isteğe bağlı parametre geçti. Bu bir yedekleme her zaman korunması gerektiğini varsa hello depolama hesabı, bağımsız olarak kaç yaşında olduğunu sağlayın.

Aşağıdaki nasıl örneğidir toouse Bu cmdlet'i.

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        $slotName = "StagingSlot"
        $dbSetting1 = New-AzureRmWebAppDatabaseBackupSetting -Name DB1 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbSetting2 = New-AzureRmWebAppDatabaseBackupSetting -Name DB2 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        Edit-AzureRmWebAppBackupConfiguration -Name $appName -ResourceGroupName $resourceGroupName -Slot $slotName `
          -StorageAccountUrl "<your SAS URL>" -FrequencyInterval 6 -FrequencyUnit Hour -Databases $dbSetting1,$dbSetting2 `
          -KeepAtLeastOneBackup -StartTime (Get-Date).AddHours(1)

tooget hello geçerli yedekleme zamanlamasını, hello Get-AzureRmWebAppBackupConfiguration cmdlet'ini kullanın. Bu, önceden yapılandırılmış bir zamanlamayı değiştirmek için yararlı olabilir.

        $configuration = Get-AzureRmWebAppBackupConfiguration -Name $appName -ResourceGroupName $resourceGroupName

        # Modify hello configuration slightly
        $configuration.FrequencyInterval = 2
        $configuration.FrequencyUnit = "Day"

        # Apply hello new configuration by piping it into hello Edit-AzureRmWebAppBackupConfiguration cmdlet
        $configuration | Edit-AzureRmWebAppBackupConfiguration

## <a name="restore-a-web-app-from-a-backup"></a>Bir web uygulaması bir yedekten geri yükleyin
toorestore bir web uygulaması bir yedekten geri yükleme AzureRmWebAppBackup hello cmdlet'ini kullanın. Merhaba en kolay yolu toouse Bu cmdlet toopipe hello Get-AzureRmWebAppBackup cmdlet'ini veya Get-AzureRmWebAppBackupList cmdlet'i alınan bir yedek nesnesinde ' dir.

Bir yedekleme nesnesi oluşturduktan sonra hello geri yükleme AzureRmWebAppBackup cmdlet'e iletebildiğiniz. Merhaba üzerine yaz anahtar parametresi tooindicate toooverwrite hello içeriğini web uygulamanızı hello yedekleme Merhaba içeriğine düşündüğünüz belirtin. Merhaba yedekleme veritabanları içeriyorsa, bu veritabanlarını da geri yüklenir.

        $backup | Restore-AzureRmWebAppBackup -Overwrite

Aşağıda nasıl toouse hello geri yükleme AzureRmWebAppBackup tüm hello parametrelerini belirterek, bir örnek verilmiştir.

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        $slotName = "StagingSlot"
        $blobName = "ContosoBackup.zip"
        $dbSetting1 = New-AzureRmWebAppDatabaseBackupSetting -Name DB1 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbSetting2 = New-AzureRmWebAppDatabaseBackupSetting -Name DB2 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        Restore-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -Slot $slotName -StorageAccountUrl "<your SAS URL>" -BlobName $blobName -Databases $dbSetting1,$dbSetting2 -Overwrite

## <a name="delete-a-backup"></a>Yedek Sil
toodelete bir yedekleme hello Kaldır AzureRmWebAppBackup cmdlet'ini kullanın. Bu depolama hesabınızdan hello yedekleme kaldırır. Uygulama adınız, kendi kaynak grubu belirtin ve hello Kimliğini hello toodelete istediğiniz yedekleme.

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        Remove-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -BackupId 10102

Bir yedekleme nesnesi hello Kaldır AzureRmWebAppBackup cmdlet toodelete iletebildiğiniz onu.

        $backup = Get-AzureRmWebAppBackup -Name $appName -ResourceGroupName $resourceGroupName -BackupId 10102
        $backup | Remove-AzureRmWebAppBackup -Overwrite
