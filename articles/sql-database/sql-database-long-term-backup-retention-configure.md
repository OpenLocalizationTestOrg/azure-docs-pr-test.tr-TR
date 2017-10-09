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
# <a name="configure-and-restore-from-azure-sql-database-long-term-backup-retention"></a><span data-ttu-id="40e1f-103">Yapılandırma ve Azure SQL veritabanı uzun vadeli yedekleme bekletme geri yükleme</span><span class="sxs-lookup"><span data-stu-id="40e1f-103">Configure and restore from Azure SQL Database long-term backup retention</span></span>

<span data-ttu-id="40e1f-104">Ve ardından Kurtarma kasası hello kullanarak yedeklemeler kullanarak bir veritabanı korunur hello Azure portal veya PowerShell hello Azure kurtarma Hizmetleri kasası toostore Azure SQL veritabanı yedeklemeleri yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="40e1f-104">You can configure hello Azure Recovery Services vault toostore Azure SQL database backups and then recover a database using backups retained in hello vault using hello Azure portal or PowerShell.</span></span>

## <a name="azure-portal"></a><span data-ttu-id="40e1f-105">Azure portalına</span><span class="sxs-lookup"><span data-stu-id="40e1f-105">Azure portal</span></span>

<span data-ttu-id="40e1f-106">Merhaba, nasıl toouse hello Azure portal tooconfigure hello Azure kurtarma Hizmetleri kasası, yedeklemeler hello kasasına görüntülemek ve hello kasadan geri bölümleri göster aşağıdaki.</span><span class="sxs-lookup"><span data-stu-id="40e1f-106">hello following sections show you how toouse hello Azure portal tooconfigure hello Azure Recovery Services vault, view backups in hello vault, and restore from hello vault.</span></span>

### <a name="configure-hello-vault-register-hello-server-and-select-databases"></a><span data-ttu-id="40e1f-107">Merhaba kasası yapılandırmak, hello sunucuyu kaydetmek ve veritabanlarını seçin</span><span class="sxs-lookup"><span data-stu-id="40e1f-107">Configure hello vault, register hello server, and select databases</span></span>

<span data-ttu-id="40e1f-108">[Azure kurtarma Hizmetleri kasası otomatik tooretain yedeklemeleri yapılandırma](sql-database-long-term-retention.md) hizmet katmanı için hello saklama süresinden daha uzun bir süre.</span><span class="sxs-lookup"><span data-stu-id="40e1f-108">You [configure an Azure Recovery Services vault tooretain automated backups](sql-database-long-term-retention.md) for a period longer than hello retention period for your service tier.</span></span> 

1. <span data-ttu-id="40e1f-109">Açık hello **SQL Server** sunucunuz için sayfa.</span><span class="sxs-lookup"><span data-stu-id="40e1f-109">Open hello **SQL Server** page for your server.</span></span>

   ![SQL server sayfası](./media/sql-database-get-started-portal/sql-server-blade.png)

2. <span data-ttu-id="40e1f-111">**Uzun süreli yedek saklama**'ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="40e1f-111">Click **Long-term backup retention**.</span></span>

   ![uzun süreli yedek saklama bağlantısı](./media/sql-database-get-started-backup-recovery/long-term-backup-retention-link.png)

3. <span data-ttu-id="40e1f-113">Merhaba üzerinde **uzun vadeli yedekleme bekletme** sayfasında sunucunuz için gözden geçirin ve hello Önizleme koşullarına (bunu - yapmış olduğunuz veya bu özellik artık Önizleme sürümünde olduğu sürece) kabul edin.</span><span class="sxs-lookup"><span data-stu-id="40e1f-113">On hello **Long-term backup retention** page for your server, review and accept hello preview terms (unless you have already done so - or this feature is no longer in preview).</span></span>

   ![Merhaba Önizleme koşullarını kabul edin](./media/sql-database-get-started-backup-recovery/accept-the-preview-terms.png)

4. <span data-ttu-id="40e1f-115">tooconfigure uzun vadeli yedekleme bekletme, hello kılavuzunda bu veritabanını seçin ve ardından **yapılandırma** hello araç.</span><span class="sxs-lookup"><span data-stu-id="40e1f-115">tooconfigure long-term backup retention, select that database in hello grid and then click **Configure** on hello toolbar.</span></span>

   ![uzun süreli yedek saklama için veritabanı seçme](./media/sql-database-get-started-backup-recovery/select-database-for-long-term-backup-retention.png)

5. <span data-ttu-id="40e1f-117">Merhaba üzerinde **yapılandırma** sayfasında, **gerekli ayarları Yapılandır** altında **kurtarma hizmeti kasasının**.</span><span class="sxs-lookup"><span data-stu-id="40e1f-117">On hello **Configure** page, click **Configure required settings** under **Recovery service vault**.</span></span>

   ![kasayı yapılandırma bağlantısı](./media/sql-database-get-started-backup-recovery/configure-vault-link.png)

6. <span data-ttu-id="40e1f-119">Merhaba üzerinde **kurtarma Hizmetleri kasası** sayfasında, varsa mevcut bir kasayı seçin.</span><span class="sxs-lookup"><span data-stu-id="40e1f-119">On hello **Recovery services vault** page, select an existing vault, if any.</span></span> <span data-ttu-id="40e1f-120">Aksi takdirde, aboneliğiniz için bulunan hiçbir kurtarma Hizmetleri kasası, tooexit hello akış tıklatın ve bir kurtarma Hizmetleri kasası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="40e1f-120">Otherwise, if no recovery services vault found for your subscription, click tooexit hello flow and create a recovery services vault.</span></span>

   ![Kasa bağlantı oluşturma](./media/sql-database-get-started-backup-recovery/create-new-vault-link.png)

7. <span data-ttu-id="40e1f-122">Merhaba üzerinde **kurtarma Hizmetleri kasaları** sayfasında, **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="40e1f-122">On hello **Recovery Services vaults** page, click **Add**.</span></span>

   ![Kasa bağlantısı ekleme](./media/sql-database-get-started-backup-recovery/add-new-vault-link.png)
   
8. <span data-ttu-id="40e1f-124">Merhaba üzerinde **kurtarma Hizmetleri kasası** sayfasında, hello kurtarma Hizmetleri kasası için geçerli bir ad sağlayın.</span><span class="sxs-lookup"><span data-stu-id="40e1f-124">On hello **Recovery Services vault** page, provide a valid name for hello Recovery Services vault.</span></span>

   ![yeni kasa adı](./media/sql-database-get-started-backup-recovery/new-vault-name.png)

9. <span data-ttu-id="40e1f-126">Abonelik ve kaynak grubu seçin ve sonra hello kasasının hello konumu seçin.</span><span class="sxs-lookup"><span data-stu-id="40e1f-126">Select your subscription and resource group, and then select hello location for hello vault.</span></span> <span data-ttu-id="40e1f-127">İşiniz bittiğinde **Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="40e1f-127">When done, click **Create**.</span></span>

   ![Kasa oluşturma](./media/sql-database-get-started-backup-recovery/create-new-vault.png)

   > [!IMPORTANT]
   > <span data-ttu-id="40e1f-129">Merhaba kasası bulunan, içinde hello hello Azure SQL mantıksal sunucusuna aynı bölgede ve kullanım aynı hello gerekir hello mantıksal sunucusu olarak kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="40e1f-129">hello vault must be located in hello same region as hello Azure SQL logical server, and must use hello same resource group as hello logical server.</span></span>
   >

10. <span data-ttu-id="40e1f-130">Merhaba gerekli adımları tooreturn toohello Hello yeni kasası oluşturulduktan sonra yürütme **kurtarma Hizmetleri kasası** sayfası.</span><span class="sxs-lookup"><span data-stu-id="40e1f-130">After hello new vault is created, execute hello necessary steps tooreturn toohello **Recovery services vault** page.</span></span>

11. <span data-ttu-id="40e1f-131">Merhaba üzerinde **kurtarma Hizmetleri kasası** sayfasında, hello kasaya tıklayın ve ardından **seçin**.</span><span class="sxs-lookup"><span data-stu-id="40e1f-131">On hello **Recovery services vault** page, click hello vault and then click **Select**.</span></span>

   ![var olan kasayı seçme](./media/sql-database-get-started-backup-recovery/select-existing-vault.png)

12. <span data-ttu-id="40e1f-133">Merhaba üzerinde **yapılandırma** sayfasında, hello yeni bekletme ilkesi için geçerli bir ad, hello varsayılan bekletme ilkesi uygun şekilde değiştirin ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="40e1f-133">On hello **Configure** page, provide a valid name for hello new retention policy, modify hello default retention policy as appropriate, and then click **OK**.</span></span>

   ![saklama ilkesi tanımlama](./media/sql-database-get-started-backup-recovery/define-retention-policy.png)

13. <span data-ttu-id="40e1f-135">Merhaba üzerinde **uzun vadeli yedekleme bekletme** sayfasında veritabanınız için **kaydetmek** ve ardından **Tamam** tooapply hello seçili uzun vadeli yedekleme bekletme ilkesi tooall veritabanları.</span><span class="sxs-lookup"><span data-stu-id="40e1f-135">On hello **Long-term backup retention** page for your database, click **Save** and then click **OK** tooapply hello long-term backup retention policy tooall selected databases.</span></span>

   ![saklama ilkesi tanımlama](./media/sql-database-get-started-backup-recovery/save-retention-policy.png)

14. <span data-ttu-id="40e1f-137">Tıklatın **kaydetmek** tooenable uzun vadeli yedekleme bekletme, yapılandırdığınız bu yeni ilke toohello Azure kurtarma Hizmetleri kasası kullanarak.</span><span class="sxs-lookup"><span data-stu-id="40e1f-137">Click **Save** tooenable long-term backup retention using this new policy toohello Azure Recovery Services vault that you configured.</span></span>

   ![saklama ilkesi tanımlama](./media/sql-database-get-started-backup-recovery/enable-long-term-retention.png)

> [!IMPORTANT]
> <span data-ttu-id="40e1f-139">Bir kere yapılandırıldığında, yedekleme hello kasasına sonraki yedi gün içinde gösterilir.</span><span class="sxs-lookup"><span data-stu-id="40e1f-139">Once configured, backups show up in hello vault within next seven days.</span></span> <span data-ttu-id="40e1f-140">Bu öğretici hello kasasına yedeklemeleri görünmesini kadar devam etmeyin.</span><span class="sxs-lookup"><span data-stu-id="40e1f-140">Do not continue this tutorial until backups show up in hello vault.</span></span>
>

### <a name="view-backups-in-long-term-retention-using-azure-portal"></a><span data-ttu-id="40e1f-141">Azure portalını kullanarak uzun vadeli bekletme içinde yedekleri görüntüle</span><span class="sxs-lookup"><span data-stu-id="40e1f-141">View backups in long-term retention using Azure portal</span></span>

<span data-ttu-id="40e1f-142">Veritabanı yedeklerinizi hakkındaki bilgileri görüntüleyin [uzun vadeli yedekleme bekletme](sql-database-long-term-retention.md).</span><span class="sxs-lookup"><span data-stu-id="40e1f-142">View information about your database backups in [long-term backup retention](sql-database-long-term-retention.md).</span></span> 

1. <span data-ttu-id="40e1f-143">İçinde Azure portal Merhaba, Azure kurtarma Hizmetleri kasanız için veritabanı yedeklerinizi açın (çok Git**tüm kaynakları** ve aboneliğiniz için kaynakların hello listeden seçin) tooview hello veritabanı tarafından kullanılan depolama alanı miktarı Merhaba kasasında yedeklemeler.</span><span class="sxs-lookup"><span data-stu-id="40e1f-143">In hello Azure portal, open your Azure Recovery Services vault for your database backups (go too**All resources** and select it from hello list of resources for your subscription) tooview hello amount of storage used by your database backups in hello vault.</span></span>

   ![kurtarma hizmetleri kasasını ve yedekleri görüntüleme](./media/sql-database-get-started-backup-recovery/view-recovery-services-vault-with-data.png)

2. <span data-ttu-id="40e1f-145">Açık hello **SQL veritabanı** veritabanınız için sayfa.</span><span class="sxs-lookup"><span data-stu-id="40e1f-145">Open hello **SQL database** page for your database.</span></span>

   ![Yeni örnek db sayfası](./media/sql-database-get-started-portal/new-sample-db-blade.png)

3. <span data-ttu-id="40e1f-147">Merhaba araç çubuğundan, **geri**.</span><span class="sxs-lookup"><span data-stu-id="40e1f-147">On hello toolbar, click **Restore**.</span></span>

   ![geri yükleme araç çubuğu](./media/sql-database-get-started-backup-recovery/restore-toolbar.png)

4. <span data-ttu-id="40e1f-149">Merhaba geri yükleme sayfasında, tıklatın **uzun vadeli**.</span><span class="sxs-lookup"><span data-stu-id="40e1f-149">On hello Restore page, click **Long-term**.</span></span>

5. <span data-ttu-id="40e1f-150">Azure kasası yedeklemeler altında tıklatın **bir yedeği seçin** tooview hello kullanılabilir veritabanı yedeklemeleri uzun vadeli yedekleme bekletme.</span><span class="sxs-lookup"><span data-stu-id="40e1f-150">Under Azure vault backups, click **Select a backup** tooview hello available database backups in long-term backup retention.</span></span>

   ![kasadaki yedekler](./media/sql-database-get-started-backup-recovery/view-backups-in-vault.png)

### <a name="restore-a-database-from-a-backup-in-long-term-backup-retention-using-hello-azure-portal"></a><span data-ttu-id="40e1f-152">Uzun vadeli yedekleme bekletme hello Azure portal kullanarak, bir yedekten bir veritabanını geri yükleyin</span><span class="sxs-lookup"><span data-stu-id="40e1f-152">Restore a database from a backup in long-term backup retention using hello Azure portal</span></span>

<span data-ttu-id="40e1f-153">Azure kurtarma Hizmetleri kasası hello içinde bir yedekten hello veritabanı tooa yeni veritabanını geri yükleyin.</span><span class="sxs-lookup"><span data-stu-id="40e1f-153">You restore hello database tooa new database from a backup in hello Azure Recovery Services vault.</span></span>

1. <span data-ttu-id="40e1f-154">Merhaba üzerinde **Azure kasası yedeklemeleri** sayfasında, hello yedekleme toorestore tıklayın ve ardından **seçin**.</span><span class="sxs-lookup"><span data-stu-id="40e1f-154">On hello **Azure vault backups** page, click hello backup toorestore and then click **Select**.</span></span>

   ![kasadaki bir yedeği seçme](./media/sql-database-get-started-backup-recovery/select-backup-in-vault.png)

2. <span data-ttu-id="40e1f-156">Merhaba, **veritabanı adı** metin kutusunda, geri hello veritabanı hello adı sağlayın.</span><span class="sxs-lookup"><span data-stu-id="40e1f-156">In hello **Database name** text box, provide hello name for hello restored database.</span></span>

   ![yeni veritabanı adı](./media/sql-database-get-started-backup-recovery/new-database-name.png)

3. <span data-ttu-id="40e1f-158">Tıklatın **Tamam** toorestore hello kasa toohello yeni veritabanı hello yedeklemeye veritabanınızdan.</span><span class="sxs-lookup"><span data-stu-id="40e1f-158">Click **OK** toorestore your database from hello backup in hello vault toohello new database.</span></span>

4. <span data-ttu-id="40e1f-159">Merhaba araç çubuğunda hello bildirim simgesine tooview hello hello geri yükleme işinin durumunu tıklatın.</span><span class="sxs-lookup"><span data-stu-id="40e1f-159">On hello toolbar, click hello notification icon tooview hello status of hello restore job.</span></span>

   ![kasadan geri yükleme işi ilerleme durumu](./media/sql-database-get-started-backup-recovery/restore-job-progress-long-term.png)

5. <span data-ttu-id="40e1f-161">Merhaba geri yükleme işi tamamlandığında hello açmak **SQL veritabanları** sayfa tooview yeni geri hello veritabanı.</span><span class="sxs-lookup"><span data-stu-id="40e1f-161">When hello restore job is completed, open hello **SQL databases** page tooview hello newly restored database.</span></span>

   ![kasadan geri yüklenen veritabanı](./media/sql-database-get-started-backup-recovery/restored-database-from-vault.png)

> [!NOTE]
> <span data-ttu-id="40e1f-163">Buradan, SQL Server Management Studio tooperform gerekli görevler gibi çok kullanılarak geri toohello veritabanı bağlanabilir[hello varolan bir veritabanını veya toodelete hello varolan geri hello veritabanı toocopy bit veri ayıklamak Veritabanı ve yeniden adlandırma geri hello veritabanı toohello var olan veritabanı adı](sql-database-recovery-using-backups.md#point-in-time-restore).</span><span class="sxs-lookup"><span data-stu-id="40e1f-163">From here, you can connect toohello restored database using SQL Server Management Studio tooperform needed tasks, such as too[extract a bit of data from hello restored database toocopy into hello existing database or toodelete hello existing database and rename hello restored database toohello existing database name](sql-database-recovery-using-backups.md#point-in-time-restore).</span></span>
>

## <a name="powershell"></a><span data-ttu-id="40e1f-164">PowerShell</span><span class="sxs-lookup"><span data-stu-id="40e1f-164">PowerShell</span></span>

<span data-ttu-id="40e1f-165">Aşağıdaki bölümlerde hello nasıl toouse PowerShell tooconfigure hello Azure kurtarma Hizmetleri kasası, yedeklemeler hello kasasına görüntüleyin ve hello kasadan geri gösterir.</span><span class="sxs-lookup"><span data-stu-id="40e1f-165">hello following sections show you how toouse PowerShell tooconfigure hello Azure Recovery Services vault, view backups in hello vault, and restore from hello vault.</span></span>

### <a name="create-a-recovery-services-vault"></a><span data-ttu-id="40e1f-166">Kurtarma hizmetleri kasası oluşturma</span><span class="sxs-lookup"><span data-stu-id="40e1f-166">Create a recovery services vault</span></span>

<span data-ttu-id="40e1f-167">Kullanım hello [yeni AzureRmRecoveryServicesVault](/powershell/module/azurerm.recoveryservices/new-azurermrecoveryservicesvault) toocreate bir kurtarma Hizmetleri kasası.</span><span class="sxs-lookup"><span data-stu-id="40e1f-167">Use hello [New-AzureRmRecoveryServicesVault](/powershell/module/azurerm.recoveryservices/new-azurermrecoveryservicesvault) toocreate a recovery services vault.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="40e1f-168">Merhaba kasası bulunan, içinde hello hello Azure SQL mantıksal sunucusuna aynı bölgede ve kullanım aynı hello gerekir hello mantıksal sunucusu olarak kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="40e1f-168">hello vault must be located in hello same region as hello Azure SQL logical server, and must use hello same resource group as hello logical server.</span></span>

```PowerShell
# Create a recovery services vault

#$resourceGroupName = "{resource-group-name}"
#$serverName = "{server-name}"
$serverLocation = (Get-AzureRmSqlServer -ServerName $serverName -ResourceGroupName $resourceGroupName).Location
$recoveryServiceVaultName = "{new-vault-name}"

$vault = New-AzureRmRecoveryServicesVault -Name $recoveryServiceVaultName -ResourceGroupName $ResourceGroupName -Location $serverLocation 
Set-AzureRmRecoveryServicesBackupProperties -BackupStorageRedundancy LocallyRedundant -Vault $vault
```

### <a name="set-your-server-toouse-hello-recovery-vault-for-its-long-term-retention-backups"></a><span data-ttu-id="40e1f-169">Sunucu toouse hello kurtarma kasanızı, uzun vadeli bekletme yedeklemeleri için ayarlama</span><span class="sxs-lookup"><span data-stu-id="40e1f-169">Set your server toouse hello recovery vault for its long-term retention backups</span></span>

<span data-ttu-id="40e1f-170">Kullanım hello [kümesi AzureRmSqlServerBackupLongTermRetentionVault](/powershell/module/azurerm.sql/set-azurermsqlserverbackuplongtermretentionvault) cmdlet tooassociate daha önce oluşturulmuş bir kurtarma Hizmetleri kasası ile belirli bir Azure SQL sunucusu.</span><span class="sxs-lookup"><span data-stu-id="40e1f-170">Use hello [Set-AzureRmSqlServerBackupLongTermRetentionVault](/powershell/module/azurerm.sql/set-azurermsqlserverbackuplongtermretentionvault) cmdlet tooassociate a previously created recovery services vault with a specific Azure SQL server.</span></span>

```PowerShell
# Set your server toouse hello vault toofor long-term backup retention 

Set-AzureRmSqlServerBackupLongTermRetentionVault -ResourceGroupName $resourceGroupName -ServerName $serverName -ResourceId $vault.Id
```

### <a name="create-a-retention-policy"></a><span data-ttu-id="40e1f-171">Saklama ilkesi tanımlama</span><span class="sxs-lookup"><span data-stu-id="40e1f-171">Create a retention policy</span></span>

<span data-ttu-id="40e1f-172">Bir bekletme ilkesi, bir veritabanı yedeği ne kadar süreyle tookeep belirlendiği ' dir.</span><span class="sxs-lookup"><span data-stu-id="40e1f-172">A retention policy is where you set how long tookeep a database backup.</span></span> <span data-ttu-id="40e1f-173">Kullanım hello [Get-AzureRmRecoveryServicesBackupRetentionPolicyObject](https://docs.microsoft.com/powershell/resourcemanager/azurerm.recoveryservices.backup/v2.3.0/get-azurermrecoveryservicesbackupretentionpolicyobject) cmdlet tooget hello varsayılan bekletme ilkesi toouse ilkeleri oluşturmak için hello şablon olarak.</span><span class="sxs-lookup"><span data-stu-id="40e1f-173">Use hello [Get-AzureRmRecoveryServicesBackupRetentionPolicyObject](https://docs.microsoft.com/powershell/resourcemanager/azurerm.recoveryservices.backup/v2.3.0/get-azurermrecoveryservicesbackupretentionpolicyobject) cmdlet tooget hello default retention policy toouse as hello template for creating policies.</span></span> <span data-ttu-id="40e1f-174">Bu şablonda hello saklama dönemi için 2 yıl ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="40e1f-174">In this template, hello retention period is set for 2 years.</span></span> <span data-ttu-id="40e1f-175">Ardından, hello çalıştırın [yeni AzureRmRecoveryServicesBackupProtectionPolicy](/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy) toofinally hello ilkesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="40e1f-175">Next, run hello [New-AzureRmRecoveryServicesBackupProtectionPolicy](/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy) toofinally create hello policy.</span></span> 

> [!NOTE]
> <span data-ttu-id="40e1f-176">Bazı cmdlet'leri çalıştırmadan önce hello kasası bağlamını ayarlayın gerektirir ([kümesi AzureRmRecoveryServicesVaultContext](/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)) birkaç ilgili parçacıkları Bu cmdlet görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="40e1f-176">Some cmdlets require that you set hello vault context before running ([Set-AzureRmRecoveryServicesVaultContext](/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)) so you see this cmdlet in a few related snippets.</span></span> <span data-ttu-id="40e1f-177">Hello İlkesi hello kasası parçası olduğundan hello bağlamını ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="40e1f-177">You set hello context because hello policy is part of hello vault.</span></span> <span data-ttu-id="40e1f-178">Her kasa için birden çok bekletme ilkeleri oluşturun ve sonra istenen hello İlkesi toospecific veritabanları uygulayın.</span><span class="sxs-lookup"><span data-stu-id="40e1f-178">You can create multiple retention policies for each vault and then apply hello desired policy toospecific databases.</span></span> 


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

### <a name="configure-a-database-toouse-hello-previously-defined-retention-policy"></a><span data-ttu-id="40e1f-179">Bir veritabanı toouse önceden tanımlanmış hello bekletme ilkesi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="40e1f-179">Configure a database toouse hello previously defined retention policy</span></span>

<span data-ttu-id="40e1f-180">Kullanım hello [kümesi AzureRmSqlDatabaseBackupLongTermRetentionPolicy](/powershell/module/azurerm.sql/set-azurermsqldatabasebackuplongtermretentionpolicy) cmdlet tooapply hello yeni ilke tooa belirli veritabanı.</span><span class="sxs-lookup"><span data-stu-id="40e1f-180">Use hello [Set-AzureRmSqlDatabaseBackupLongTermRetentionPolicy](/powershell/module/azurerm.sql/set-azurermsqldatabasebackuplongtermretentionpolicy) cmdlet tooapply hello new policy tooa specific database.</span></span>

```PowerShell
# Enable long-term retention for a specific SQL database
$policyState = "enabled"
Set-AzureRmSqlDatabaseBackupLongTermRetentionPolicy -ResourceGroupName $resourceGroupName -ServerName $serverName -DatabaseName $databaseName -State $policyState -ResourceId $policy.Id
```

### <a name="view-backup-info-and-backups-in-long-term-retention"></a><span data-ttu-id="40e1f-181">Uzun süreli saklama kapsamındaki yedekleme bilgilerini ve yedekleri görüntüleme</span><span class="sxs-lookup"><span data-stu-id="40e1f-181">View backup info, and backups in long-term retention</span></span>

<span data-ttu-id="40e1f-182">Veritabanı yedeklerinizi hakkındaki bilgileri görüntüleyin [uzun vadeli yedekleme bekletme](sql-database-long-term-retention.md).</span><span class="sxs-lookup"><span data-stu-id="40e1f-182">View information about your database backups in [long-term backup retention](sql-database-long-term-retention.md).</span></span> 

<span data-ttu-id="40e1f-183">Aşağıdaki cmdlet'leri tooview yedekleme bilgilerle hello kullan:</span><span class="sxs-lookup"><span data-stu-id="40e1f-183">Use hello following cmdlets tooview backup information:</span></span>

- [<span data-ttu-id="40e1f-184">Get-AzureRmRecoveryServicesBackupContainer</span><span class="sxs-lookup"><span data-stu-id="40e1f-184">Get-AzureRmRecoveryServicesBackupContainer</span></span>](/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupcontainer)
- [<span data-ttu-id="40e1f-185">Get-AzureRmRecoveryServicesBackupItem</span><span class="sxs-lookup"><span data-stu-id="40e1f-185">Get-AzureRmRecoveryServicesBackupItem</span></span>](/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupitem)
- [<span data-ttu-id="40e1f-186">Get-AzureRmRecoveryServicesBackupRecoveryPoint</span><span class="sxs-lookup"><span data-stu-id="40e1f-186">Get-AzureRmRecoveryServicesBackupRecoveryPoint</span></span>](/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackuprecoverypoint)

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

### <a name="restore-a-database-from-a-backup-in-long-term-backup-retention"></a><span data-ttu-id="40e1f-187">Bir veritabanını uzun süreli yedek saklama kapsamındaki bir yedekten geri yükleme</span><span class="sxs-lookup"><span data-stu-id="40e1f-187">Restore a database from a backup in long-term backup retention</span></span>

<span data-ttu-id="40e1f-188">Uzun vadeli yedekleme bekletme geri kullanan hello [geri yükleme-AzureRmSqlDatabase](/powershell/module/azurerm.sql/restore-azurermsqldatabase) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="40e1f-188">Restoring from long-term backup retention uses hello [Restore-AzureRmSqlDatabase](/powershell/module/azurerm.sql/restore-azurermsqldatabase) cmdlet.</span></span>

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
> <span data-ttu-id="40e1f-189">Buradan, SQL Server Management Studio tooperform gerekli görevleri kullanarak geri toohello veritabanı bağlanabilir, tooextract gibi biraz hello verilerden veritabanı toocopy hello varolan bir veritabanını veya toodelete hello varolan bir veritabanını yeniden adlandırma geri Merhaba geri yüklenen veritabanı toohello varolan bir veritabanı adı.</span><span class="sxs-lookup"><span data-stu-id="40e1f-189">From here, you can connect toohello restored database using SQL Server Management Studio tooperform needed tasks, such as tooextract a bit of data from hello restored database toocopy into hello existing database or toodelete hello existing database and rename hello restored database toohello existing database name.</span></span> <span data-ttu-id="40e1f-190">Bkz: [geri yükleme noktası](sql-database-recovery-using-backups.md#point-in-time-restore).</span><span class="sxs-lookup"><span data-stu-id="40e1f-190">See [point in time restore](sql-database-recovery-using-backups.md#point-in-time-restore).</span></span>

## <a name="next-steps"></a><span data-ttu-id="40e1f-191">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="40e1f-191">Next steps</span></span>

- <span data-ttu-id="40e1f-192">toolearn hizmeti tarafından oluşturulan otomatik yedeklemeler hakkında bkz [otomatik yedekleme](sql-database-automated-backups.md)</span><span class="sxs-lookup"><span data-stu-id="40e1f-192">toolearn about service-generated automatic backups, see [automatic backups](sql-database-automated-backups.md)</span></span>
- <span data-ttu-id="40e1f-193">uzun vadeli yedekleme bekletme hakkında toolearn bakın [uzun vadeli yedekleme bekletme](sql-database-long-term-retention.md)</span><span class="sxs-lookup"><span data-stu-id="40e1f-193">toolearn about long-term backup retention, see [long-term backup retention](sql-database-long-term-retention.md)</span></span>
- <span data-ttu-id="40e1f-194">toolearn, yedeklerden geri yükleme hakkında bkz [yedekten geri yükleme](sql-database-recovery-using-backups.md)</span><span class="sxs-lookup"><span data-stu-id="40e1f-194">toolearn about restoring from backups, see [restore from backup](sql-database-recovery-using-backups.md)</span></span>
