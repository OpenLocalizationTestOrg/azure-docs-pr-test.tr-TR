---
title: "Uzun vadeli yedekleme bekletme - Azure SQL veritabanı yapılandırma | Microsoft Docs"
description: "Nasıl toostore hello Azure kurtarma Hizmetleri kasası ve Azure kurtarma Hizmetleri kasası hello gelen toorestore yedeklemelerin otomatik öğrenin"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: aeb8c4c3-6ae2-45f7-b2c3-fa13e3752eed
ms.service: sql-database
ms.custom: business continuity
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/10/2017
ms.author: carlrab
ms.openlocfilehash: 603f4dd21cee4407d46f749655aba8f9ef3322c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-and-restore-from-azure-sql-database-long-term-backup-retention"></a>Yapılandırma ve Azure SQL veritabanı uzun vadeli yedekleme bekletme geri yükleme

Ve ardından Kurtarma kasası hello kullanarak yedeklemeler kullanarak bir veritabanı korunur hello Azure portal veya PowerShell hello Azure kurtarma Hizmetleri kasası toostore Azure SQL veritabanı yedeklemeleri yapılandırabilirsiniz.

## <a name="azure-portal"></a>Azure portalına

Merhaba, nasıl toouse hello Azure portal tooconfigure hello Azure kurtarma Hizmetleri kasası, yedeklemeler hello kasasına görüntülemek ve hello kasadan geri bölümleri göster aşağıdaki.

### <a name="configure-hello-vault-register-hello-server-and-select-databases"></a>Merhaba kasası yapılandırmak, hello sunucuyu kaydetmek ve veritabanlarını seçin

[Azure kurtarma Hizmetleri kasası otomatik tooretain yedeklemeleri yapılandırma](sql-database-long-term-retention.md) hizmet katmanı için hello saklama süresinden daha uzun bir süre. 

1. Açık hello **SQL Server** sunucunuz için sayfa.

   ![SQL server sayfası](./media/sql-database-get-started-portal/sql-server-blade.png)

2. **Uzun süreli yedek saklama**'ya tıklayın.

   ![uzun süreli yedek saklama bağlantısı](./media/sql-database-get-started-backup-recovery/long-term-backup-retention-link.png)

3. Merhaba üzerinde **uzun vadeli yedekleme bekletme** sayfasında sunucunuz için gözden geçirin ve hello Önizleme koşullarına (bunu - yapmış olduğunuz veya bu özellik artık Önizleme sürümünde olduğu sürece) kabul edin.

   ![Merhaba Önizleme koşullarını kabul edin](./media/sql-database-get-started-backup-recovery/accept-the-preview-terms.png)

4. tooconfigure uzun vadeli yedekleme bekletme, hello kılavuzunda bu veritabanını seçin ve ardından **yapılandırma** hello araç.

   ![uzun süreli yedek saklama için veritabanı seçme](./media/sql-database-get-started-backup-recovery/select-database-for-long-term-backup-retention.png)

5. Merhaba üzerinde **yapılandırma** sayfasında, **gerekli ayarları Yapılandır** altında **kurtarma hizmeti kasasının**.

   ![kasayı yapılandırma bağlantısı](./media/sql-database-get-started-backup-recovery/configure-vault-link.png)

6. Merhaba üzerinde **kurtarma Hizmetleri kasası** sayfasında, varsa mevcut bir kasayı seçin. Aksi takdirde, aboneliğiniz için bulunan hiçbir kurtarma Hizmetleri kasası, tooexit hello akış tıklatın ve bir kurtarma Hizmetleri kasası oluşturun.

   ![Kasa bağlantı oluşturma](./media/sql-database-get-started-backup-recovery/create-new-vault-link.png)

7. Merhaba üzerinde **kurtarma Hizmetleri kasaları** sayfasında, **Ekle**.

   ![Kasa bağlantısı ekleme](./media/sql-database-get-started-backup-recovery/add-new-vault-link.png)
   
8. Merhaba üzerinde **kurtarma Hizmetleri kasası** sayfasında, hello kurtarma Hizmetleri kasası için geçerli bir ad sağlayın.

   ![yeni kasa adı](./media/sql-database-get-started-backup-recovery/new-vault-name.png)

9. Abonelik ve kaynak grubu seçin ve sonra hello kasasının hello konumu seçin. İşiniz bittiğinde **Oluştur**'a tıklayın.

   ![Kasa oluşturma](./media/sql-database-get-started-backup-recovery/create-new-vault.png)

   > [!IMPORTANT]
   > Merhaba kasası bulunan, içinde hello hello Azure SQL mantıksal sunucusuna aynı bölgede ve kullanım aynı hello gerekir hello mantıksal sunucusu olarak kaynak grubu.
   >

10. Merhaba gerekli adımları tooreturn toohello Hello yeni kasası oluşturulduktan sonra yürütme **kurtarma Hizmetleri kasası** sayfası.

11. Merhaba üzerinde **kurtarma Hizmetleri kasası** sayfasında, hello kasaya tıklayın ve ardından **seçin**.

   ![var olan kasayı seçme](./media/sql-database-get-started-backup-recovery/select-existing-vault.png)

12. Merhaba üzerinde **yapılandırma** sayfasında, hello yeni bekletme ilkesi için geçerli bir ad, hello varsayılan bekletme ilkesi uygun şekilde değiştirin ve ardından **Tamam**.

   ![saklama ilkesi tanımlama](./media/sql-database-get-started-backup-recovery/define-retention-policy.png)

13. Merhaba üzerinde **uzun vadeli yedekleme bekletme** sayfasında veritabanınız için **kaydetmek** ve ardından **Tamam** tooapply hello seçili uzun vadeli yedekleme bekletme ilkesi tooall veritabanları.

   ![saklama ilkesi tanımlama](./media/sql-database-get-started-backup-recovery/save-retention-policy.png)

14. Tıklatın **kaydetmek** tooenable uzun vadeli yedekleme bekletme, yapılandırdığınız bu yeni ilke toohello Azure kurtarma Hizmetleri kasası kullanarak.

   ![saklama ilkesi tanımlama](./media/sql-database-get-started-backup-recovery/enable-long-term-retention.png)

> [!IMPORTANT]
> Bir kere yapılandırıldığında, yedekleme hello kasasına sonraki yedi gün içinde gösterilir. Bu öğretici hello kasasına yedeklemeleri görünmesini kadar devam etmeyin.
>

### <a name="view-backups-in-long-term-retention-using-azure-portal"></a>Azure portalını kullanarak uzun vadeli bekletme içinde yedekleri görüntüle

Veritabanı yedeklerinizi hakkındaki bilgileri görüntüleyin [uzun vadeli yedekleme bekletme](sql-database-long-term-retention.md). 

1. İçinde Azure portal Merhaba, Azure kurtarma Hizmetleri kasanız için veritabanı yedeklerinizi açın (çok Git**tüm kaynakları** ve aboneliğiniz için kaynakların hello listeden seçin) tooview hello veritabanı tarafından kullanılan depolama alanı miktarı Merhaba kasasında yedeklemeler.

   ![kurtarma hizmetleri kasasını ve yedekleri görüntüleme](./media/sql-database-get-started-backup-recovery/view-recovery-services-vault-with-data.png)

2. Açık hello **SQL veritabanı** veritabanınız için sayfa.

   ![Yeni örnek db sayfası](./media/sql-database-get-started-portal/new-sample-db-blade.png)

3. Merhaba araç çubuğundan, **geri**.

   ![geri yükleme araç çubuğu](./media/sql-database-get-started-backup-recovery/restore-toolbar.png)

4. Merhaba geri yükleme sayfasında, tıklatın **uzun vadeli**.

5. Azure kasası yedeklemeler altında tıklatın **bir yedeği seçin** tooview hello kullanılabilir veritabanı yedeklemeleri uzun vadeli yedekleme bekletme.

   ![kasadaki yedekler](./media/sql-database-get-started-backup-recovery/view-backups-in-vault.png)

### <a name="restore-a-database-from-a-backup-in-long-term-backup-retention-using-hello-azure-portal"></a>Uzun vadeli yedekleme bekletme hello Azure portal kullanarak, bir yedekten bir veritabanını geri yükleyin

Azure kurtarma Hizmetleri kasası hello içinde bir yedekten hello veritabanı tooa yeni veritabanını geri yükleyin.

1. Merhaba üzerinde **Azure kasası yedeklemeleri** sayfasında, hello yedekleme toorestore tıklayın ve ardından **seçin**.

   ![kasadaki bir yedeği seçme](./media/sql-database-get-started-backup-recovery/select-backup-in-vault.png)

2. Merhaba, **veritabanı adı** metin kutusunda, geri hello veritabanı hello adı sağlayın.

   ![yeni veritabanı adı](./media/sql-database-get-started-backup-recovery/new-database-name.png)

3. Tıklatın **Tamam** toorestore hello kasa toohello yeni veritabanı hello yedeklemeye veritabanınızdan.

4. Merhaba araç çubuğunda hello bildirim simgesine tooview hello hello geri yükleme işinin durumunu tıklatın.

   ![kasadan geri yükleme işi ilerleme durumu](./media/sql-database-get-started-backup-recovery/restore-job-progress-long-term.png)

5. Merhaba geri yükleme işi tamamlandığında hello açmak **SQL veritabanları** sayfa tooview yeni geri hello veritabanı.

   ![kasadan geri yüklenen veritabanı](./media/sql-database-get-started-backup-recovery/restored-database-from-vault.png)

> [!NOTE]
> Buradan, SQL Server Management Studio tooperform gerekli görevler gibi çok kullanılarak geri toohello veritabanı bağlanabilir[hello varolan bir veritabanını veya toodelete hello varolan geri hello veritabanı toocopy bit veri ayıklamak Veritabanı ve yeniden adlandırma geri hello veritabanı toohello var olan veritabanı adı](sql-database-recovery-using-backups.md#point-in-time-restore).
>

## <a name="powershell"></a>PowerShell

Aşağıdaki bölümlerde hello nasıl toouse PowerShell tooconfigure hello Azure kurtarma Hizmetleri kasası, yedeklemeler hello kasasına görüntüleyin ve hello kasadan geri gösterir.

### <a name="create-a-recovery-services-vault"></a>Kurtarma hizmetleri kasası oluşturma

Kullanım hello [yeni AzureRmRecoveryServicesVault](/powershell/module/azurerm.recoveryservices/new-azurermrecoveryservicesvault) toocreate bir kurtarma Hizmetleri kasası.

> [!IMPORTANT]
> Merhaba kasası bulunan, içinde hello hello Azure SQL mantıksal sunucusuna aynı bölgede ve kullanım aynı hello gerekir hello mantıksal sunucusu olarak kaynak grubu.

```PowerShell
# Create a recovery services vault

#$resourceGroupName = "{resource-group-name}"
#$serverName = "{server-name}"
$serverLocation = (Get-AzureRmSqlServer -ServerName $serverName -ResourceGroupName $resourceGroupName).Location
$recoveryServiceVaultName = "{new-vault-name}"

$vault = New-AzureRmRecoveryServicesVault -Name $recoveryServiceVaultName -ResourceGroupName $ResourceGroupName -Location $serverLocation 
Set-AzureRmRecoveryServicesBackupProperties -BackupStorageRedundancy LocallyRedundant -Vault $vault
```

### <a name="set-your-server-toouse-hello-recovery-vault-for-its-long-term-retention-backups"></a>Sunucu toouse hello kurtarma kasanızı, uzun vadeli bekletme yedeklemeleri için ayarlama

Kullanım hello [kümesi AzureRmSqlServerBackupLongTermRetentionVault](/powershell/module/azurerm.sql/set-azurermsqlserverbackuplongtermretentionvault) cmdlet tooassociate daha önce oluşturulmuş bir kurtarma Hizmetleri kasası ile belirli bir Azure SQL sunucusu.

```PowerShell
# Set your server toouse hello vault toofor long-term backup retention 

Set-AzureRmSqlServerBackupLongTermRetentionVault -ResourceGroupName $resourceGroupName -ServerName $serverName -ResourceId $vault.Id
```

### <a name="create-a-retention-policy"></a>Saklama ilkesi tanımlama

Bir bekletme ilkesi, bir veritabanı yedeği ne kadar süreyle tookeep belirlendiği ' dir. Kullanım hello [Get-AzureRmRecoveryServicesBackupRetentionPolicyObject](https://docs.microsoft.com/powershell/resourcemanager/azurerm.recoveryservices.backup/v2.3.0/get-azurermrecoveryservicesbackupretentionpolicyobject) cmdlet tooget hello varsayılan bekletme ilkesi toouse ilkeleri oluşturmak için hello şablon olarak. Bu şablonda hello saklama dönemi için 2 yıl ayarlanır. Ardından, hello çalıştırın [yeni AzureRmRecoveryServicesBackupProtectionPolicy](/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy) toofinally hello ilkesi oluşturun. 

> [!NOTE]
> Bazı cmdlet'leri çalıştırmadan önce hello kasası bağlamını ayarlayın gerektirir ([kümesi AzureRmRecoveryServicesVaultContext](/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)) birkaç ilgili parçacıkları Bu cmdlet görürsünüz. Hello İlkesi hello kasası parçası olduğundan hello bağlamını ayarlayın. Her kasa için birden çok bekletme ilkeleri oluşturun ve sonra istenen hello İlkesi toospecific veritabanları uygulayın. 


```PowerShell
# Retrieve hello default retention policy for hello AzureSQLDatabase workload type
$retentionPolicy = Get-AzureRmRecoveryServicesBackupRetentionPolicyObject -WorkloadType AzureSQLDatabase

# Set hello retention value tootwo years (you can set tooany time between 1 week and 10 years)
$retentionPolicy.RetentionDurationType = "Years"
$retentionPolicy.RetentionCount = 2
$retentionPolicyName = "my2YearRetentionPolicy"

# Set hello vault context toohello vault you are creating hello policy for
Set-AzureRmRecoveryServicesVaultContext -Vault $vault

# Create hello new policy
$policy = New-AzureRmRecoveryServicesBackupProtectionPolicy -name $retentionPolicyName -WorkloadType AzureSQLDatabase -retentionPolicy $retentionPolicy
$policy
```

### <a name="configure-a-database-toouse-hello-previously-defined-retention-policy"></a>Bir veritabanı toouse önceden tanımlanmış hello bekletme ilkesi yapılandırma

Kullanım hello [kümesi AzureRmSqlDatabaseBackupLongTermRetentionPolicy](/powershell/module/azurerm.sql/set-azurermsqldatabasebackuplongtermretentionpolicy) cmdlet tooapply hello yeni ilke tooa belirli veritabanı.

```PowerShell
# Enable long-term retention for a specific SQL database
$policyState = "enabled"
Set-AzureRmSqlDatabaseBackupLongTermRetentionPolicy -ResourceGroupName $resourceGroupName -ServerName $serverName -DatabaseName $databaseName -State $policyState -ResourceId $policy.Id
```

### <a name="view-backup-info-and-backups-in-long-term-retention"></a>Uzun süreli saklama kapsamındaki yedekleme bilgilerini ve yedekleri görüntüleme

Veritabanı yedeklerinizi hakkındaki bilgileri görüntüleyin [uzun vadeli yedekleme bekletme](sql-database-long-term-retention.md). 

Aşağıdaki cmdlet'leri tooview yedekleme bilgilerle hello kullan:

- [Get-AzureRmRecoveryServicesBackupContainer](/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupcontainer)
- [Get-AzureRmRecoveryServicesBackupItem](/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupitem)
- [Get-AzureRmRecoveryServicesBackupRecoveryPoint](/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackuprecoverypoint)

```PowerShell
#$resourceGroupName = "{resource-group-name}"
#$serverName = "{server-name}"
$databaseNeedingRestore = $databaseName

# Set hello vault context toohello vault we want toorestore from
#$vault = Get-AzureRmRecoveryServicesVault -ResourceGroupName $resourceGroupName
Set-AzureRmRecoveryServicesVaultContext -Vault $vault

# hello following commands find hello container associated with hello server 'myserver' under resource group 'myresourcegroup'
$container = Get-AzureRmRecoveryServicesBackupContainer -ContainerType AzureSQL -FriendlyName $vault.Name

# Get hello long-term retention metadata associated with a specific database
$item = Get-AzureRmRecoveryServicesBackupItem -Container $container -WorkloadType AzureSQLDatabase -Name $databaseNeedingRestore

# Get all available backups for hello previously indicated database
# Optionally, set hello -StartDate and -EndDate parameters tooreturn backups within a specific time period
$availableBackups = Get-AzureRmRecoveryServicesBackupRecoveryPoint -Item $item
$availableBackups
```

### <a name="restore-a-database-from-a-backup-in-long-term-backup-retention"></a>Bir veritabanını uzun süreli yedek saklama kapsamındaki bir yedekten geri yükleme

Uzun vadeli yedekleme bekletme geri kullanan hello [geri yükleme-AzureRmSqlDatabase](/powershell/module/azurerm.sql/restore-azurermsqldatabase) cmdlet'i.

```PowerShell
# Restore hello most recent backup: $availableBackups[0]
#$resourceGroupName = "{resource-group-name}"
#$serverName = "{server-name}"
$restoredDatabaseName = "{new-database-name}"
$edition = "Basic"
$performanceLevel = "Basic"

$restoredDb = Restore-AzureRmSqlDatabase -FromLongTermRetentionBackup -ResourceId $availableBackups[0].Id -ResourceGroupName $resourceGroupName `
 -ServerName $serverName -TargetDatabaseName $restoredDatabaseName -Edition $edition -ServiceObjectiveName $performanceLevel
$restoredDb
```


> [!NOTE]
> Buradan, SQL Server Management Studio tooperform gerekli görevleri kullanarak geri toohello veritabanı bağlanabilir, tooextract gibi biraz hello verilerden veritabanı toocopy hello varolan bir veritabanını veya toodelete hello varolan bir veritabanını yeniden adlandırma geri Merhaba geri yüklenen veritabanı toohello varolan bir veritabanı adı. Bkz: [geri yükleme noktası](sql-database-recovery-using-backups.md#point-in-time-restore).

## <a name="next-steps"></a>Sonraki adımlar

- toolearn hizmeti tarafından oluşturulan otomatik yedeklemeler hakkında bkz [otomatik yedekleme](sql-database-automated-backups.md)
- uzun vadeli yedekleme bekletme hakkında toolearn bakın [uzun vadeli yedekleme bekletme](sql-database-long-term-retention.md)
- toolearn, yedeklerden geri yükleme hakkında bkz [yedekten geri yükleme](sql-database-recovery-using-backups.md)
