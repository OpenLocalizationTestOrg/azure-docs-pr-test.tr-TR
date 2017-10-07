---
title: aaaReplicate Hyper-V sanal makineleri, PowerShell ve Azure Resource Manager | Microsoft Docs
description: "Hyper-V sanal makineleri tooAzure Hello çoğaltmasını PowerShell ve Azure Resource Manager kullanarak Azure Site Recovery ile otomatikleştirin."
services: site-recovery
documentationcenter: 
author: bsiva
manager: abhiag
editor: 
ms.assetid: 05e0d76e-c3f5-4845-8052-094019b6d102
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/31/2017
ms.author: bsiva
ms.openlocfilehash: 4fb15ce2e9ad54f1dd6f54ff769eb912aa4b0272
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-between-on-premises-hyper-v-virtual-machines-and-azure-by-using-powershell-and-azure-resource-manager"></a>PowerShell ve Azure Resource Manager kullanarak şirket içi Hyper-V sanal makineleri ve Azure arasında çoğaltma
> [!div class="op_single_selector"]
> * [Azure Portal](site-recovery-hyper-v-site-to-azure.md)
> * [PowerShell - Resource Manager](site-recovery-deploy-with-powershell-resource-manager.md)
> * [Klasik Portal](site-recovery-hyper-v-site-to-azure-classic.md)
>
>

## <a name="overview"></a>Genel Bakış
Azure Site Recovery, çoğaltma, yük devretme ve kurtarma çeşitli dağıtım senaryolarında sanal makinelerin düzenleyerek tooyour iş sürekliliği ve olağanüstü durum kurtarma stratejisi katkıda bulunur. Dağıtım senaryoları tam bir listesi için bkz: Merhaba [Azure Site Recovery genel bakış](site-recovery-overview.md).

Azure PowerShell cmdlet'leri toomanage Windows PowerShell üzerinden Azure sağlayan bir modüldür. İki tür modülü çalışabilir: Azure profili modülü veya hello Azure Resource Manager modülü hello.

Site Recovery PowerShell cmdlet, Azure PowerShell için Azure Resource Manager ile kullanılabilir korumak ve sunucularınızı Azure kurtarmak yardımcı olur.

Bu makalede nasıl toouse Windows PowerShell ile birlikte Azure Resource Manager, toodeploy Site Recovery tooconfigure ve sunucu koruması tooAzure düzenlemek. Bu makalede kullanılan hello örnek nasıl tooprotect, yük devri ve Azure Resource Manager ile Azure PowerShell kullanarak bir Hyper-V ana bilgisayar tooAzure sanal makinelerde kurtarmak gösterir.

> [!NOTE]
> Merhaba Site Recovery PowerShell cmdlet şu anda aşağıdaki tooconfigure hello sağlar: bir Sanal Makine Yöneticisi site tooanother, bir Sanal Makine Yöneticisi site tooAzure ve bir Hyper-V sitesi tooAzure.
>
>

Bu makalede toobe PowerShell Uzman toouse gerekmez, ancak toounderstand hello gibi temel kavramları modüller, cmdlet'ler ve oturumlar gerekir. Windows PowerShell hakkında daha fazla bilgi için bkz. [Windows PowerShell ile Çalışmaya Başlama](http://technet.microsoft.com/library/hh857337.aspx).

Ayrıca daha fazla hakkında bilgiyi [Azure PowerShell kullanarak Azure Resource Manager ile](../powershell-azure-resource-manager.md).

> [!NOTE]
> Merhaba bulut çözümü sağlayıcısı (CSP) programı parçası olan Microsoft iş ortaklarının yapılandırmak ve müşterilerin sunucuların korumasını yönetmek tootheir müşterilerin ilgili CSP aboneliklerin (Kiracı abonelikleri).
>
>

## <a name="before-you-start"></a>Başlamadan önce
Bu Önkoşullar sağladığınızdan emin olun:

* A [Microsoft Azure](https://azure.microsoft.com/) hesabı. [Ücretsiz deneme sürümüyle](https://azure.microsoft.com/pricing/free-trial/) başlayabilirsiniz. Ayrıca, hakkında bilgi edinebilirsiniz [Azure Site Recovery Manager fiyatlandırma](https://azure.microsoft.com/pricing/details/site-recovery/).
* Azure PowerShell 1.0. Bu sürüm hakkında bilgi için ve nasıl tooinstall, bkz: [Azure PowerShell 1.0.](https://azure.microsoft.com/)
* Merhaba [AzureRM.SiteRecovery](https://www.powershellgallery.com/packages/AzureRM.SiteRecovery/) ve [AzureRM.RecoveryServices](https://www.powershellgallery.com/packages/AzureRM.RecoveryServices/) modüller. Merhaba en son sürümleri bu modüllerin hello alabilirsiniz [PowerShell Galerisi](https://www.powershellgallery.com/)

Bu makalede gösterilmektedir nasıl toouse Azure Powershell ile Azure Resource Manager tooconfigure ve koruma sunucularınızın yönetin. Bu makalede kullanılan hello örnek gösterir, nasıl tooprotect tooAzure bir Hyper-V ana bilgisayarında çalışan bir sanal makine. Önkoşullar aşağıdaki hello belirli toothis örnektir. Çeşitli Site kurtarma senaryoları, daha kapsamlı birtakım hello gereksinimleri için toothat senaryo ilgili toohello belgelerine başvurun.

* Windows Server 2012 R2 veya bir veya daha fazla sanal makine içeren Microsoft Hyper-V Server 2012 R2 çalıştıran bir Hyper-V ana bilgisayarı.
* Hyper-V sunucuları toohello Internet, doğrudan ya da bir proxy üzerinden bağlı.
* Merhaba tooprotect istediğiniz sanal makineleri karşılaması gerektiğini [sanal makine önkoşulları](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).

## <a name="step-1-sign-in-tooyour-azure-account"></a>1. adım: tooyour Azure hesabı ile oturum açın.
1. Bir PowerShell konsolu açın ve bu komutu toosign tooyour Azure hesabı çalıştırın. Merhaba cmdlet'i için hesap kimlik bilgilerinizi ister bir web sayfasını getirir.

        Login-AzureRmAccount

    Alternatif olarak, ayrıca hesabı kimlik bilgilerinizi parametresi toohello ekleyebilirsiniz `Login-AzureRmAccount` hello kullanarak cmdlet `-Credential` parametresi.

    Kiracı adına çalışma CSP ortağı varsa, hello müşteri kendi Tenantıd veya Kiracı birincil etki alanı adını kullanarak bir kiracı olarak belirtin.

        Login-AzureRmAccount -Tenant "fabrikam.com"
2. Hello hesabıyla toouse hello aboneliği ilişkilendirmeniz böylece bir hesap birden fazla abonelik olabilir.

        Select-AzureRmSubscription -SubscriptionName $SubscriptionName
3. Aboneliğinizin kayıtlı toouse olduğunu doğrulayın hello aşağıdaki komutları kullanarak kurtarma Hizmetleri ve Site kurtarma için Azure sağlayıcıları hello:

   * `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.RecoveryServices`
   * `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.SiteRecovery`

   Merhaba, aşağıdaki komutlardan birini hello çıktısında **RegistrationState** çok ayarlanır**kayıtlı**, tooStep 2 devam edebilirsiniz. Aksi durumda, aboneliğinizde hello eksik sağlayıcısı kaydetmeniz.

   tooregister Site kurtarma ve kurtarma Hizmetleri için Azure sağlayıcı Merhaba, hello aşağıdaki komutları çalıştırın:

       Register-AzureRmResourceProvider -ProviderNamespace Microsoft.SiteRecovery
       Register-AzureRmResourceProvider -ProviderNamespace Microsoft.RecoveryServices

   Merhaba aşağıdaki komutları kullanarak Hello sağlayıcıları başarıyla kaydedildiğini doğrulayın: `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.RecoveryServices` ve `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.SiteRecovery`.

## <a name="step-2-set-up-hello-recovery-services-vault"></a>2. adım: Hello ayarlama kurtarma Hizmetleri kasası
1. İçinde hello kasası oluşturma veya varolan bir kaynak grubunu kullanın bir Azure Resource Manager kaynak grubu oluşturun. Komutu aşağıdaki hello kullanarak yeni bir kaynak grubu oluşturabilirsiniz:

        New-AzureRmResourceGroup -Name $ResourceGroupName -Location $Geo  

    Merhaba $ResourceGroupName değişkeni hello hello kaynak grubu adını içeren burada toocreate istediğiniz ve hello $Geo değişkenini içeren hello Azure bölgesi hangi toocreate hello kaynak grubunda (örneğin, "Brezilya Güney").

    Kaynak grupları listesini hello kullanarak aboneliğinizde elde edebilirsiniz `Get-AzureRmResourceGroup` cmdlet'i.
2. Yeni bir Azure kurtarma Hizmetleri kasası gibi oluşturun:

        $vault = New-AzureRmRecoveryServicesVault -Name <string> -ResourceGroupName <string> -Location <string>

    Hello kullanarak mevcut kasalarının listesi alabilirsiniz `Get-AzureRmRecoveryServicesVault` cmdlet'i.

> [!NOTE]
> Site Recovery kasası hello Klasik portalında veya hello Azure Service Management PowerShell modülü kullanılarak oluşturulan tooperform işlemleri istiyorsanız hello kullanarak bu tür kasalarının listesi alabilirsiniz `Get-AzureRmSiteRecoveryVault` cmdlet'i. Tüm yeni işlemleri için yeni bir kurtarma Hizmetleri kasası oluşturmanız gerekir. daha önce oluşturduğunuz hello Site Recovery kasası desteklenir, ancak hello en son özelliklere sahip değilsiniz.
>
>

## <a name="step-3-set-hello-recovery-services-vault-context"></a>3. adım: hello kurtarma Hizmetleri kasası bağlam ayarlama
1. Merhaba aşağıdaki komutu çalıştırarak Hello kasası bağlamını ayarlayın:

       Set-AzureRmSiteRecoveryVaultSettings -ARSVault $vault

## <a name="step-4-create-a-hyper-v-site-and-generate-a-new-vault-registration-key-for-hello-site"></a>4. adım: bir Hyper-V sitesi oluşturun ve hello site için yeni bir kasa kayıt anahtarı oluşturun.
1. Yeni bir Hyper-V sitesi gibi oluşturun:

        $sitename = "MySite"                #Specify site friendly name
        New-AzureRmSiteRecoverySite -Name $sitename

    Bu cmdlet, bir Site kurtarma işi toocreate hello siteyi başlatır ve Site Recovery iş nesnesi döndürür. Merhaba iş toocomplete için bekleyin ve o hello işi başarıyla tamamlandı doğrulayın.

    Merhaba iş nesnesini almak ve böylelikle hello Get-AzureRmSiteRecoveryJob cmdlet'ini kullanarak hello hello işinin geçerli durumunu denetleyin.
2. Oluşturun ve aşağıdaki gibi hello site için bir kayıt anahtarını indirin:

        $SiteIdentifier = Get-AzureRmSiteRecoverySite -Name $sitename | Select -ExpandProperty SiteIdentifier
        Get-AzureRmRecoveryServicesVaultSettingsFile -Vault $vault -SiteIdentifier $SiteIdentifier -SiteFriendlyName $sitename -Path $Path

    Kopya hello anahtar toohello Hyper-V konak indirilir. Merhaba anahtar tooregister hello Hyper-V ana bilgisayar toohello sitesi gerekir.

## <a name="step-5-install-hello-azure-site-recovery-provider-and-azure-recovery-services-agent-on-your-hyper-v-host"></a>5. adım: hello Azure Site Recovery sağlayıcısı ve Azure kurtarma Hizmetleri Aracısı, Hyper-V konak üzerinde yükleyin
1. Hello yükleyiciyi hello hello Sağlayıcısı'ndan en son sürümü karşıdan [Microsoft](https://aka.ms/downloaddra).
2. Hyper-V ana bilgisayarınızda ve hello yükleme hello sonunda çalışma hello yükleyici toohello kayıt adımından devam edin.
3. İstendiğinde, site kayıt anahtarını ve hello Hyper-V ana bilgisayar toohello sitenin tam kayıt hello indirilen sağlayın.
4. Merhaba aşağıdaki komutu kullanarak bu hello Hyper-V ana kayıtlı toohello site olduğunu doğrulayın:

        $server =  Get-AzureRmSiteRecoveryServer -FriendlyName $server-friendlyname

## <a name="step-6-create-a-replication-policy-and-associate-it-with-hello-protection-container"></a>6. adım: bir çoğaltma ilkesi oluşturun ve hello koruma kapsayıcısı ile ilişkilendirin
1. Bir çoğaltma ilkesi şu şekilde oluşturun:

        $ReplicationFrequencyInSeconds = "300";        #options are 30,300,900
        $PolicyName = “replicapolicy”
        $Recoverypoints = 6                    #specify hello number of recovery points
        $storageaccountID = Get-AzureRmStorageAccount -Name "mystorea" -ResourceGroupName "MyRG" | Select -ExpandProperty Id

        $PolicyResult = New-AzureRmSiteRecoveryPolicy -Name $PolicyName -ReplicationProvider “HyperVReplicaAzure” -ReplicationFrequencyInSeconds $ReplicationFrequencyInSeconds  -RecoveryPoints $Recoverypoints -ApplicationConsistentSnapshotFrequencyInHours 1 -RecoveryAzureStorageAccountId $storageaccountID

    Onay hello hello çoğaltma ilkesi oluşturma başarılı iş tooensure döndürdü.

   > [!IMPORTANT]
   > Merhaba belirtilen depolama hesabı olması gerekir, Kurtarma Hizmetleri kasasıyla aynı Azure bölgesinde hello ve coğrafi çoğaltmanın etkinleştirilmiş olması gerekir.
   >
   > * Merhaba depolama hesabı Azure Storage (Klasik) türünde kurtarma belirtilmişse, hello Yük Devretmesini makineler kurtarmak hello makine tooAzure Iaas (Klasik) korumalı.
   > * Merhaba Kurtarma Depolama hesabı Azure Storage (Azure Resource Manager) türünü belirtilirse, hello Yük Devretmesini makineler kurtarmak hello makine tooAzure Iaas (Azure Resource Manager) korumalı.
   >
   >
2. Merhaba koruma kapsayıcısı karşılık gelen toohello site, aşağıdaki gibi alın:

        $protectionContainer = Get-AzureRmSiteRecoveryProtectionContainer
3. Merhaba koruma kapsayıcısı Hello ilişkilendirmesini hello çoğaltma ilkesi, aşağıda gösterildiği gibi başlatın:

     $Policy get-AzureRmSiteRecoveryPolicy - FriendlyName $PolicyName $associationJob = başlangıç AzureRmSiteRecoveryPolicyAssociationJob =-ilke $Policy - PrimaryProtectionContainer $protectionContainer

   Merhaba ilişkilendirme iş toocomplete için bekleyin ve başarıyla tamamlandığını doğrulayın.

## <a name="step-7-enable-protection-for-virtual-machines"></a>7. adım: sanal makineler için korumayı etkinleştir
1. Merhaba koruma varlık karşılık gelen toohello tooprotect, aşağıdaki gibi istediğiniz VM alın:

        $VMFriendlyName = "Fabrikam-app"                    #Name of hello VM
        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -ProtectionContainer $protectionContainer -FriendlyName $VMFriendlyName
2. Merhaba sanal makine, aşağıdaki gibi koruma başlatın:

        $Ostype = "Windows"                                 # "Windows" or "Linux"
        $DRjob = Set-AzureRmSiteRecoveryProtectionEntity -ProtectionEntity $protectionEntity -Policy $Policy -Protection Enable -RecoveryAzureStorageAccountId $storageaccountID  -OS $OStype -OSDiskName $protectionEntity.Disks[0].Name

   > [!IMPORTANT]
   > Merhaba belirtilen depolama hesabı olması gerekir, Kurtarma Hizmetleri kasasıyla aynı Azure bölgesinde hello ve coğrafi çoğaltmanın etkinleştirilmiş olması gerekir.
   >
   > * Merhaba depolama hesabı Azure Storage (Klasik) türünde kurtarma belirtilmişse, hello Yük Devretmesini makineler kurtarmak hello makine tooAzure Iaas (Klasik) korumalı.
   > * Merhaba Kurtarma Depolama hesabı Azure Storage (Azure Resource Manager) türünü belirtilirse, hello Yük Devretmesini makineler kurtarmak hello makine tooAzure Iaas (Azure Resource Manager) korumalı.
   >
   > Merhaba koruduğunuz VM birden fazla disk ekli tooit, hello kullanarak hello işletim sistemi diski belirtmek varsa *OSDiskName* parametresi.
   >
   >
3. Merhaba sanal makineleri tooreach için korumalı bir duruma hello ilk çoğaltma sonrasında bekleyin. Bu, çoğaltılmış verileri toobe hello miktarı gibi etkenlere bağlı olarak uzun sürebilir ve Yukarı Akış bant tooAzure hello. aşağıdaki gibi Hello iş durumu ve StateDescription hello korumalı bir duruma ulaşmadan VM güncelleştirilir.

        PS C:\> $DRjob = Get-AzureRmSiteRecoveryJob -Job $DRjob

        PS C:\> $DRjob | Select-Object -ExpandProperty State
        Succeeded

        PS C:\> $DRjob | Select-Object -ExpandProperty StateDescription
        Completed
4. Merhaba VM rol boyutu ve hello Azure ağ tooattach hello sanal makinenin ağ arabirimi kartları tooupon yük devretme gibi kurtarma özelliklerini güncelleştirir.

        PS C:\> $nw1 = Get-AzureRmVirtualNetwork -Name "FailoverNw" -ResourceGroupName "MyRG"

        PS C:\> $VMFriendlyName = "Fabrikam-App"

        PS C:\> $VM = Get-AzureRmSiteRecoveryVM -ProtectionContainer $protectionContainer -FriendlyName $VMFriendlyName

        PS C:\> $UpdateJob = Set-AzureRmSiteRecoveryVM -VirtualMachine $VM -PrimaryNic $VM.NicDetailsList[0].NicId -RecoveryNetworkId $nw1.Id -RecoveryNicSubnetName $nw1.Subnets[0].Name

        PS C:\> $UpdateJob = Get-AzureRmSiteRecoveryJob -Job $UpdateJob

        PS C:\> $UpdateJob

        Name             : b8a647e0-2cb9-40d1-84c4-d0169919e2c5
        ID               : /Subscriptions/a731825f-4bf2-4f81-a611-c331b272206e/resourceGroups/MyRG/providers/Microsoft.RecoveryServices/vault
                           s/MyVault/replicationJobs/b8a647e0-2cb9-40d1-84c4-d0169919e2c5
        Type             : Microsoft.RecoveryServices/vaults/replicationJobs
        JobType          : UpdateVmProperties
        DisplayName      : Update hello virtual machine
        ClientRequestId  : 805a22a3-be86-441c-9da8-f32685673112-2015-12-10 17:55:51Z-P
        State            : Succeeded
        StateDescription : Completed
        StartTime        : 10-12-2015 17:55:53 +00:00
        EndTime          : 10-12-2015 17:55:54 +00:00
        TargetObjectId   : 289682c6-c5e6-42dc-a1d2-5f9621f78ae6
        TargetObjectType : ProtectionEntity
        TargetObjectName : Fabrikam-App
        AllowedActions   : {Restart}
        Tasks            : {UpdateVmPropertiesTask}
        Errors           : {}



## <a name="step-8-run-a-test-failover"></a>8. adım: yük devretme testi çalıştırma
1. Bir test yük devretme işini çalıştırmak için şunları yapın:

        $nw = Get-AzureRmVirtualNetwork -Name "TestFailoverNw" -ResourceGroupName "MyRG" #Specify Azure vnet name and resource group

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -FriendlyName $VMFriendlyName -ProtectionContainer $protectionContainer

        $TFjob = Start-AzureRmSiteRecoveryTestFailoverJob -ProtectionEntity $protectionEntity -Direction PrimaryToRecovery -AzureVMNetworkId $nw.Id
2. Azure'da VM oluşturulan hello test doğrulayın. (Merhaba test yük devretme işini, Azure'da hello test VM oluşturduktan sonra askıya alındı. Merhaba iş hello işi sırasında oluşturulan hello artefacts hello sonraki adımda gösterildiği gibi temizleniyor tarafından tamamlar.)
3. Tam hello yük devretme, aşağıdaki gibi test edin:

        $TFjob = Resume-AzureRmSiteRecoveryJob -Job $TFjob

## <a name="next-steps"></a>Sonraki Adımlar
[Daha fazla bilgi](https://msdn.microsoft.com/library/azure/mt637930.aspx) Azure Site Recovery ile Azure Resource Manager PowerShell cmdlet'leri hakkında.
