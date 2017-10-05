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
# <a name="use-powershell-to-back-up-and-restore-app-service-apps"></a>Ve App Service uygulamalarının geri yükleme için PowerShell kullanma
> [!div class="op_single_selector"]
> * [PowerShell](app-service-powershell-backup.md)
> * [REST API](../app-service-web/websites-csm-backup.md)
> 
> 

Yedekleme ve geri yükleme için Azure PowerShell kullanmayı öğrenin [App Service uygulamalarının](https://azure.microsoft.com/services/app-service/web/). Web uygulaması yedeklemeler, gereksinimleri ve kısıtlamaları dahil hakkında daha fazla bilgi için bkz: [Azure App Service'te bir web uygulaması yedekleme](../app-service-web/web-sites-backup.md).

## <a name="prerequisites"></a>Ön koşullar
Uygulama Yedeklemelerinizin yönetmek için PowerShell kullanmak için aşağıdakiler gerekir:

* **Bir SAS URL'si** okuma ve bir Azure Storage kapsayıcısına yazma erişimi sağlar. Bkz: [SAS modelini anlama](../storage/common/storage-dotnet-shared-access-signature-part-1.md) SAS URL'leri açıklaması için. Bkz: [Azure Storage ile Azure PowerShell'i kullanma](../storage/common/storage-powershell-guide-full.md) Azure PowerShell kullanarak depolama yönetme örnekler.
* **Bir veritabanı bağlantı dizesi** web uygulamanızı birlikte bir veritabanı yedeklemek istiyorsanız.

### <a name="how-to-generate-a-sas-url-to-use-with-the-web-app-backup-cmdlets"></a>Web uygulaması Yedekleme cmdlet ile birlikte kullanmak için bir SAS URL'si oluşturmak nasıl
Bir SAS URL'si PowerShell ile oluşturulabilir. Bu makalede açıklanan cmdlet'leri ile birlikte kullanılabilen bir oluşturmak nasıl bir örneği burada verilmiştir.

        $storageAccountName = "<your storage account's name>"
        $storageAccountRg = "<your storage account's resource group>"

        # This returns an array of keys for your storage account. Be sure to select the appropriate key. Here we select the first key as a default.
        $storageAccountKey = Get-AzureRmStorageAccountKey -ResourceGroupName $storageAccountRg -Name $storageAccountName
        $context = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey[0].Value

        $blobContainerName = "<name of blob container for app backups>"
        $sasUrl = New-AzureStorageContainerSASToken -Name $blobContainerName -Permission rwdl -Context $context -ExpiryTime (Get-Date).AddMonths(1) -FullUri

## <a name="install-azure-powershell-132-or-greater"></a>Azure PowerShell 1.3.2 yüklemek veya daha büyük
Bkz: [Azure PowerShell kullanarak Azure Resource Manager ile](/powershell/azure/overview) yükleme ve Azure PowerShell kullanma hakkında yönergeler için.

## <a name="create-a-backup"></a>Bir yedekleme oluşturun
Web uygulamasının bir yedekleme oluşturmak için New-AzureRmWebAppBackup cmdlet'ini kullanın.

        $sasUrl = "<your SAS URL>"
        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"

        $backup = New-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -StorageAccountUrl $sasUrl

Bu, otomatik olarak oluşturulan bir adla bir yedek oluşturur. Yedekleme için bir ad sağlamak istiyorsanız YedekAdı isteğe bağlı parametresini kullanın.

        $backup = New-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -StorageAccountUrl $sasUrl -BackupName MyBackup

Bir veritabanını yedeklemeye dahil edilecek ilk yeni AzureRmWebAppDatabaseBackupSetting cmdlet'ini kullanarak bir veritabanı yedekleme ayarı oluşturun ve sonra bu ayar yeni AzureRmWebAppBackup cmdlet'in veritabanları parametresinde sağlamak. Veritabanları parametresi veritabanı ayarlarını, birden fazla veritabanını yedeklemek sağlayan bir dizi kabul eder.

        $dbSetting1 = New-AzureRmWebAppDatabaseBackupSetting -Name DB1 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbSetting2 = New-AzureRmWebAppDatabaseBackupSetting -Name DB2 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbBackup = New-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -BackupName MyBackup -StorageAccountUrl $sasUrl -Databases $dbSetting1,$dbSetting2

## <a name="get-backups"></a>Yedeklemeleri Al
Get-AzureRmWebAppBackupList cmdlet'i tüm yedeklemeler bir web uygulaması için bir dizi döndürür. Web uygulaması ve kaynak grubu adı sağlamanız gerekir.

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        $backups = Get-AzureRmWebAppBackupList -Name $appName -ResourceGroupName $resourceGroupName

Belirli bir yedek almak için Get-AzureRmWebAppBackup cmdlet'ini kullanın.

        $backup = Get-AzureRmWebAppBackup -Name $appName -ResourceGroupName $resourceGroupName -BackupId 10102

Bir web uygulaması nesnesi, kolaylık sağlamak için Yedekleme Yönetimi cmdlet'leri hiçbirine de iletebildiğiniz.

        $app = Get-AzureRmWebApp -Name ContosoApp -ResourceGroupName Default-Web-WestUS
        $backupList = $app | Get-AzureRmWebAppBackupList
        $backup = $app | Get-AzureRmWebAppBackup -BackupId 10102

## <a name="schedule-automatic-backups"></a>Otomatik yedeklemeler zamanlama
Belirli aralıklarla otomatik olarak gerçekleştirilmesi için yedeklemeler zamanlayabilirsiniz. Yedekleme zamanlamasını yapılandırmak için düzenleme AzureRmWebAppBackupConfiguration cmdlet'ini kullanın. Bu cmdlet birkaç parametre alır:

* **Ad** -web uygulamasının adı.
* **ResourceGroupName** -web uygulamasını içeren kaynak grubunun adı.
* **Yuva** - isteğe bağlı. Web uygulaması yuvası adı.
* **StorageAccountUrl** -yedeklemelerini depolamak için kullanılan Azure depolama kapsayıcısı için SAS URL.
* **FrequencyInterval** -yedeklemelerin ne sıklıkta yapılmalıdır için sayısal bir değer. Pozitif bir tamsayı olmalıdır.
* **FrequencyUnit** -yedeklemelerin ne sıklıkta yapılmalıdır için zaman birimi. Seçenekler şunlardır: saat ve günü.
* **RetentionPeriodInDays** - kaç gün Otomatik yedeklemeleri otomatik olarak silinmeden önce kaydedilmesi.
* **StartTime** - isteğe bağlı. Otomatik yedekleme ne zaman başlaması gereken süre. Bu null ise yedeklemeleri hemen başlayın. Bir tarih saat olmalıdır.
* **Veritabanlarını** - isteğe bağlı. Veritabanlarını yedeklemek için DatabaseBackupSettings dizisi.
* **KeepAtLeastOneBackup** - isteğe bağlı parametre geçti. Bu, kaynağı bir yedekleme her zaman saklanması kaç yaşında olduğunu bağımsız olarak depolama hesabındaki.

Bu cmdlet'in nasıl kullanılacağı örneği verilmiştir.

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        $slotName = "StagingSlot"
        $dbSetting1 = New-AzureRmWebAppDatabaseBackupSetting -Name DB1 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbSetting2 = New-AzureRmWebAppDatabaseBackupSetting -Name DB2 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        Edit-AzureRmWebAppBackupConfiguration -Name $appName -ResourceGroupName $resourceGroupName -Slot $slotName `
          -StorageAccountUrl "<your SAS URL>" -FrequencyInterval 6 -FrequencyUnit Hour -Databases $dbSetting1,$dbSetting2 `
          -KeepAtLeastOneBackup -StartTime (Get-Date).AddHours(1)

Geçerli yedekleme zamanlamasını almak için Get-AzureRmWebAppBackupConfiguration cmdlet'ini kullanın. Bu, önceden yapılandırılmış bir zamanlamayı değiştirmek için yararlı olabilir.

        $configuration = Get-AzureRmWebAppBackupConfiguration -Name $appName -ResourceGroupName $resourceGroupName

        # Modify the configuration slightly
        $configuration.FrequencyInterval = 2
        $configuration.FrequencyUnit = "Day"

        # Apply the new configuration by piping it into the Edit-AzureRmWebAppBackupConfiguration cmdlet
        $configuration | Edit-AzureRmWebAppBackupConfiguration

## <a name="restore-a-web-app-from-a-backup"></a>Bir web uygulaması bir yedekten geri yükleyin
Bir web uygulaması bir yedekten geri yüklemek için geri yükleme-AzureRmWebAppBackup cmdlet'ini kullanın. Bu cmdlet kullanılarak en kolay yolu bir yedek nesnesinde kanal alınan Get-AzureRmWebAppBackup cmdlet veya Get-AzureRmWebAppBackupList cmdlet'i.

Bir yedekleme nesnesi olduktan sonra geri yükleme AzureRmWebAppBackup cmdlet'e iletebildiğiniz. Web uygulamanızın içeriğini yedekleme içeriğinin üzerine istediğinizi belirtmek için üzerine yazma anahtar parametresini belirtin. Veritabanlarını yedekleme içeriyorsa, bu veritabanlarını da geri yüklenir.

        $backup | Restore-AzureRmWebAppBackup -Overwrite

Aşağıdaki, tüm parametreleri belirterek geri yükleme AzureRmWebAppBackup kullanmayı örneğidir.

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        $slotName = "StagingSlot"
        $blobName = "ContosoBackup.zip"
        $dbSetting1 = New-AzureRmWebAppDatabaseBackupSetting -Name DB1 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbSetting2 = New-AzureRmWebAppDatabaseBackupSetting -Name DB2 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        Restore-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -Slot $slotName -StorageAccountUrl "<your SAS URL>" -BlobName $blobName -Databases $dbSetting1,$dbSetting2 -Overwrite

## <a name="delete-a-backup"></a>Yedek Sil
Bir yedekleme silmek için Remove-AzureRmWebAppBackup cmdlet'ini kullanın. Bu yedekleme depolama hesabınızdan siler. Uygulama adı, kaynak grubu ve silmek istediğiniz yedekleme Kimliğini belirtin.

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        Remove-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -BackupId 10102

Bir yedek nesnesini silmek için Remove-AzureRmWebAppBackup cmdlet'e de iletebildiğiniz.

        $backup = Get-AzureRmWebAppBackup -Name $appName -ResourceGroupName $resourceGroupName -BackupId 10102
        $backup | Remove-AzureRmWebAppBackup -Overwrite
