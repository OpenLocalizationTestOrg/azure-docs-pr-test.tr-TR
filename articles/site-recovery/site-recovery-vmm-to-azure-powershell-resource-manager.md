---
title: "PowerShell (Resource Manager) ve Azure Site Recovery kullanarak VMM bulutlarındaki aaaReplicate Hyper-V sanal makinelerini | Microsoft Docs"
description: "Azure Site Recovery ve PowerShell kullanarak VMM bulutlarındaki Hyper-V sanal makinelerini çoğaltma"
services: site-recovery
documentationcenter: 
author: Rajani-Janaki-Ram
manager: rochakm
editor: raynew
ms.assetid: 6ac509ad-5024-43d8-b621-d8fec019b9a9
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: rajanaki
ms.openlocfilehash: b0f641de4e10a600ead415ceb9bd488fb4d1659d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooazure-using-powershell-and-azure-resource-manager"></a>Hyper-V sanal makineleri PowerShell ve Azure Resource Manager kullanarak VMM Bulutları tooAzure Çoğalt
> [!div class="op_single_selector"]
> * [Azure Portal](site-recovery-vmm-to-azure.md)
> * [PowerShell - Resource Manager](site-recovery-vmm-to-azure-powershell-resource-manager.md)
> * [Klasik Portal](site-recovery-vmm-to-azure-classic.md)
> * [PowerShell - Klasik](site-recovery-deploy-with-powershell.md)
>
>

## <a name="overview"></a>Genel Bakış
Azure Site Recovery, çoğaltma, yük devretme ve kurtarma çeşitli dağıtım senaryolarında sanal makinelerin düzenleyerek tooyour iş sürekliliği ve olağanüstü durum kurtarma (BCDR) stratejinize katkı sağlar. Dağıtım tam listesi için bkz: hello senaryoları [Azure Site Recovery genel bakış](site-recovery-overview.md).

Bu makalede, Azure Site Recovery tooreplicate Hyper-V sanal makineleri System Center VMM Bulutları tooAzure depolama ayarlarken nasıl toouse PowerShell tooautomate ortak görevleri tooperform ihtiyacınız gösterir.

Merhaba makale hello senaryonun önkoşulları içerir ve gösterir

* Nasıl tooset bir kurtarma Hizmetleri kasası ayarlama
* Hello Azure Site Recovery sağlayıcısı hello kaynak VMM sunucusuna yükleyin
* Merhaba sunucu hello kasaya kaydetmek, bir Azure depolama hesabı ekleme
* Hyper-V ana bilgisayar sunucuları üzerinde Hello Azure kurtarma Hizmetleri aracısını yükleme
* Uygulanan tooall korumalı sanal makineleri olacak VMM Bulutları için koruma ayarlarını yapılandırın
* Bu sanal makineler için korumayı etkinleştirin.
* Merhaba yük devretme toomake her şeyin beklendiği gibi çalıştığından emin sınayın.

Bu senaryoyu oluşturan ayarlama sorunlarını alıyorsanız, üzerinde hello sorularınızı [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

> [!NOTE]
> Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../azure-resource-manager/resource-manager-deployment-model.md). Bu makalede, hello Resource Manager dağıtım modelini kullanarak yer almaktadır.
>
>

## <a name="before-you-start"></a>Başlamadan önce
Bu Önkoşullar sağladığınızdan emin olun:

### <a name="azure-prerequisites"></a>Azure önkoşulları
* Bir [Microsoft Azure](https://azure.microsoft.com/) hesabınızın olması gerekir. Yoksa, başlayan bir [ücretsiz bir hesap](https://azure.microsoft.com/free). Ayrıca, hello hakkında bilgi edinebilirsiniz [Azure Site Recovery Manager fiyatlandırma](https://azure.microsoft.com/pricing/details/site-recovery/).
* Merhaba çoğaltma tooa CSP abonelik senaryo çalışıyorsanız, CSP aboneliğine sahip olmanız gerekir. Merhaba CSP programı hakkında daha fazla bilgi [nasıl hello CSP programında tooenroll](https://msdn.microsoft.com/library/partnercenter/mt156995.aspx).
* Bir Azure v2 (Resource Manager) depolama hesabı toostore çoğaltılmış verileri tooAzure gerekir. Merhaba hesabının coğrafi çoğaltmanın etkinleştirilmiş olması gerekir. Merhaba hello Azure Site Recovery hizmeti ile aynı bölgeye ve hello ile ilişkili olmalıdır aynı abonelik veya hello CSP abonelik. Azure depolama birimini kurma hakkında daha fazla toolearn bkz hello [giriş tooMicrosoft Azure Storage](../storage/common/storage-introduction.md) başvuru.
* Toomake tooprotect istediğiniz sanal makineleri hello ile uyumlu olduğundan emin olmanız gerekir [Azure sanal makine önkoşulları](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).

> [!NOTE]
> Şu anda yalnızca VM düzeyinde işlemleri Powershell aracılığıyla mümkündür. Kurtarma planı düzeyi işlemleri için destek yakında sunulacaktır.  Şimdilik, sınırlı tooperforming başarısız-belirlemez yalnızca 'VM korumalı' ayrıntı düzeyi ve düzeyinde bir kurtarma planı demektir.
>
>

### <a name="vmm-prerequisites"></a>VMM önkoşulları
* System Center 2012 R2 üzerinde çalışan VMM sunucusu gerekir.
* Sanal makineler içeren herhangi bir VMM sunucusuna tooprotect hello Azure Site Recovery sağlayıcısı çalıştırmalıdır istiyor. Bu hello Azure Site Recovery dağıtımı sırasında yüklenir.
* Merhaba tooprotect istediğiniz VMM sunucusu üzerinde en az bir bulut gerekir. Merhaba bulut içermelidir:
  * Bir veya birden çok VMM ana bilgisayar grubu.
  * Her ana bilgisayar grubunda bir veya daha fazla Hyper-V sunucusu ya da kümesi.
  * Merhaba kaynak Hyper-V sunucu üzerindeki bir veya daha fazla sanal makineler.
* VMM bulutlarını ayarlama hakkında daha fazla bilgi edinin:
  * Özel VMM bulutlarındaki hakkında daha fazla bilgiyi [System Center 2012 R2 VMM ile özel bulut yenilikler](http://go.microsoft.com/fwlink/?LinkId=324952) ve [VMM 2012 ve hello Bulutları](http://go.microsoft.com/fwlink/?LinkId=324956).
  * Hakkında bilgi edinin [yapılandırma hello VMM bulut yapı](https://msdn.microsoft.com/library/azure/dn469075.aspx#BKMK_Fabric)
  * Bulut doku öğelerinizi hazır olduktan sonra özel bulutta oluşturma hakkında bilgi edinin [VMM'de özel bulut oluşturma](http://go.microsoft.com/fwlink/p/?LinkId=324953) ve [izlenecek yol: System Center 2012 SP1 VMM içeren özel bulut oluşturma](http://go.microsoft.com/fwlink/p/?LinkId=324954).

### <a name="hyper-v-prerequisites"></a>Hyper-V önkoşulları
* Merhaba Hyper-V ana bilgisayar sunucuları en az çalıştırmalıdır **Windows Server 2012** Hyper-V rolüne sahip veya **Microsoft Hyper-V Server 2012** ve hello son güncelleştirmelerin yüklü olması.
* Hyper-V'yi bir kümede çalıştırıyorsanız statik IP adresi temelli bir kümeye sahip olmanız durumunda küme aracısının otomatik olarak oluşturulamayacağını unutmayın. El ile tooconfigure hello küme Aracısı gerekir. için
* Yönergeler için bkz [nasıl tooConfigure Hyper-V çoğaltma aracısı](http://blogs.technet.com/b/haroldwong/archive/2013/03/27/server-virtualization-series-hyper-v-replica-broker-explained-part-15-of-20-by-yung-chou.aspx).
* Herhangi bir Hyper-V konak sunucusu veya küme toomanage koruma istediğiniz VMM Bulutu eklenmesi gerekir.

### <a name="network-mapping-prerequisites"></a>Ağ eşlemesi önkoşulları
Azure sanal makineleri koruduğunuzda, hello ağ eşlemesi hello sanal makine ağları hello kaynak VMM sunucuda ve hedef Azure ağları tooenable hello aşağıdaki eşler:

* Merhaba üzerinde aynı yük devri tüm makineler ağ tooeach bulundukları hangi kurtarma planı yedeklemiş diğer bağlanabilir.
* Bir ağ geçidi Kurulum hello hedef Azure ağını üzerinde ise, sanal makineleri tooother şirket içi sanal makinelere bağlanabilir.
* Ağ eşlemesini yapılandırmazsanız, yalnızca sanal makineler, hello aynı yük devri hello kurtarma planı yük devretme tooAzure sonra diğer mümkün tooconnect tooeach olacaktır.

Toodeploy ağ eşlemesi istiyorsanız hello aşağıdakiler gerekir:

* Merhaba kaynak VMM sunucusunda tooprotect istediğiniz Hello sanal makineleri bağlı tooa VM ağı olmalıdır. Bu ağ hello Bulutu ile ilişkili mantıksal ağ bağlantılı tooa olmalıdır.
* Bir Azure ağı toowhich çoğaltılan sanal makineler, yük devretme bağlanabilir. Yük devretme hello aynı anda bu ağ seçersiniz. Merhaba ağ hello olmalıdır, Azure Site Recovery abonelik aynı bölgede.

Ağ eşlemesi hakkında daha fazla bilgi edinin

* [Nasıl tooconfigure vmm'de Mantıksal ağlar](http://go.microsoft.com/fwlink/p/?LinkId=386307)
* [Nasıl tooconfigure VM ağları ve ağ geçitlerini vmm'de](http://go.microsoft.com/fwlink/p/?LinkId=386308)
* [Nasıl Azure sanal ağları tooconfigure ve İzleyicisi](https://azure.microsoft.com/documentation/services/virtual-network/)

### <a name="powershell-prerequisites"></a>PowerShell önkoşulları
Azure PowerShell hazır toogo olduğundan emin olun. PowerShell zaten kullanıyorsanız, tooupgrade tooversion 0.8.10 gerekir ya da daha sonra. Merhaba PowerShell ayarlama hakkında daha fazla bilgi için bkz [Kılavuzu tooinstall ve Azure PowerShell yapılandırma](/powershell/azureps-cmdlets-docs). Ayarlama ve PowerShell yapılandırılmış sonra tüm hello hizmeti için kullanılabilir cmdlet'leri hello görüntüleyebilirsiniz [burada](/powershell/azure/overview).

parametre değerleri, girişleri ve çıkışları genellikle Azure PowerShell'de işlenme gibi hello cmdlet'leri kullanmanıza yardımcı olabilecek ipuçları hakkında toolearn bkz hello [tooget Azure cmdlet'leri ile Başlarken Kılavuzu](/powershell/azure/get-started-azureps).

## <a name="step-1-set-hello-subscription"></a>1. adım: hello abonelik ayarlama
1. Azure powershell, oturum açma tooyour Azure hesabı üzerinden: hello aşağıdaki cmdlet'leri kullanarak

        $UserName = "<user@live.com>"
        $Password = "<password>"
        $SecurePassword = ConvertTo-SecureString -AsPlainText $Password -Force
        $Cred = New-Object System.Management.Automation.PSCredential -ArgumentList $UserName, $SecurePassword
        Login-AzureRmAccount #-Credential $Cred
2. Aboneliklerinizi listesini alın. Bu da hello subscriptionIDs her hello abonelikler için listeler. Toocreate hello kurtarma Hizmetleri kasası istediğiniz hello aboneliğin Hello Subscriptionıd unutmayın

        Get-AzureRmSubscription
3. Hangi hello kurtarma Hizmetleri kasası hello abonelik kimliği söz tarafından oluşturulan toobe olan hello abonelik ayarlayın

        Set-AzureRmContext –SubscriptionID <subscriptionId>

## <a name="step-2-create-a-recovery-services-vault"></a>2. Adım: Bir Kurtarma Hizmetleri kasası oluşturma
1. Zaten yoksa, Azure Kaynak Yöneticisi'nde bir kaynak grubu oluştur

        New-AzureRmResourceGroup -Name #ResourceGroupName -Location #location
2. Yeni bir kurtarma Hizmetleri kasası oluşturun ve ASR kasası nesne (daha sonra kullanılacak) bir değişkende oluşturulan hello kaydedin. Merhaba ASR kasası nesne post oluşturma hello Get-AzureRMRecoveryServicesVault cmdlet'ini kullanarak elde edebilirsiniz:-

        $vault = New-AzureRmRecoveryServicesVault -Name #vaultname -ResouceGroupName #ResourceGroupName -Location #location

## <a name="step-3-set-hello-recovery-services-vault-context"></a>3. adım: hello kurtarma Hizmetleri kasası bağlamını ayarlayın

Hello aşağıdaki komutu çalıştırarak Hello kasası bağlamını ayarlayın.

       Set-AzureRmSiteRecoveryVaultSettings -ARSVault $vault

## <a name="step-4-install-hello-azure-site-recovery-provider"></a>Adım 4: hello Azure Site Recovery sağlayıcısı yükleme
1. Merhaba VMM makinede hello aşağıdaki komutu çalıştırarak bir dizin oluşturun:

       New-Item c:\ASR -type directory
2. Merhaba aşağıdaki komutu çalıştırarak indirilen hello sağlayıcısını kullanarak hello dosyaları ayıklayın

       pushd C:\ASR\
       .\AzureSiteRecoveryProvider.exe /x:. /q
3. Merhaba Sağlayıcı komutları aşağıdaki hello kullanarak yükleyin:

       .\SetupDr.exe /i
       $installationRegPath = "hklm:\software\Microsoft\Microsoft System Center Virtual Machine Manager Server\DRAdapter"
       do
       {
         $isNotInstalled = $true;
         if(Test-Path $installationRegPath)
         {
           $isNotInstalled = $false;
         }
       }While($isNotInstalled)

   Merhaba yükleme toofinish bekleyin.
4. Hello sunucu komutu aşağıdaki hello kullanarak hello kasasına kaydedin:

       $BinPath = $env:SystemDrive+"\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin"
       pushd $BinPath
       $encryptionFilePath = "C:\temp\".\DRConfigurator.exe /r /Credentials $VaultSettingFilePath /vmmfriendlyname $env:COMPUTERNAME /dataencryptionenabled $encryptionFilePath /startvmmservice

## <a name="step-5-create-an-azure-storage-account"></a>5. adım: Azure storage hesabı oluşturma

Bir Azure depolama hesabınız yoksa, bir coğrafi çoğaltmanın etkinleştirilmiş hesabı oluşturmak hello hello aynı coğrafi bölgede kasa hello aşağıdaki komutu çalıştırarak:

        $StorageAccountName = "teststorageacc1"    #StorageAccountname
        $StorageAccountGeo  = "Southeast Asia"     
        $ResourceGroupName =  “myRG”             #ResourceGroupName
        $RecoveryStorageAccount = New-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $StorageAccountName -Type “StandardGRS” -Location $StorageAccountGeo

Merhaba depolama hesabı olması gerektiğini unutmayın hello hello Azure Site Recovery hizmeti ile aynı bölgeye ve ilişkilendirilmesi hello aynı abonelik.

## <a name="step-6-install-hello-azure-recovery-services-agent"></a>6. adım: hello Azure kurtarma Hizmetleri Aracısı yükleme
1. Konumundaki Hello Azure kurtarma Hizmetleri Aracısı'nı indirme [http://aka.ms/latestmarsagent](http://aka.ms/latestmarsagent) ve hello VMM bulunan her Hyper-V konak sunucusu üzerinde Bulutlar yükleme tooprotect istiyor.
2. Tüm VMM konaklarda komutu aşağıdaki hello çalıştırın:

       marsagentinstaller.exe /q /nu

## <a name="step-7-configure-cloud-protection-settings"></a>7. adım: Bulut yapılandırma koruma ayarları
1. Bir çoğaltma ilkesi tooAzure hello aşağıdaki komutu çalıştırarak oluşturun:

        $ReplicationFrequencyInSeconds = "300";        #options are 30,300,900
        $PolicyName = “replicapolicy”
        $Recoverypoints = 6                    #specify hello number of recovery points

        $policryresult = New-AzureRmSiteRecoveryPolicy -Name $policyname -ReplicationProvider HyperVReplicaAzure -ReplicationFrequencyInSeconds $replicationfrequencyinseconds -RecoveryPoints $recoverypoints -ApplicationConsistentSnapshotFrequencyInHours 1 -RecoveryAzureStorageAccountId "/subscriptions/q1345667/resourceGroups/test/providers/Microsoft.Storage/storageAccounts/teststorageacc1"

1. Koruma kapsayıcısı hello aşağıdaki komutları çalıştırarak alın:

       $PrimaryCloud = "testcloud"
       $protectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $PrimaryCloud;  
2. Oluşturulan hello işlemini kullanarak ve hello kolay ilke adı söz hello ilkesi ayrıntıları tooa değişkeni alın:

       $policy = Get-AzureRmSiteRecoveryPolicy -FriendlyName $policyname
3. Merhaba koruma kapsayıcısı Hello ilişkilendirmesini hello çoğaltma ilkesiyle başlatın:

       $associationJob  = Start-AzureRmSiteRecoveryPolicyAssociationJob -Policy     $Policy -PrimaryProtectionContainer $protectionContainer  
4. Merhaba işi tamamlandıktan sonra hello aşağıdaki komutu çalıştırın:

       $job = Get-AzureRmSiteRecoveryJob -Job $associationJob

       if($job -eq $null -or $job.StateDescription -ne "Completed")
       {
         $isJobLeftForProcessing = $true;
       }
5. Hello iş işlemeyi bitirdikten sonra hello aşağıdaki komutu çalıştırın:

       if($isJobLeftForProcessing)
       {
         Start-Sleep -Seconds 60
       }
       }While($isJobLeftForProcessing)

Merhaba işleminin toocheck hello tamamlanması izleyin hello adımlarda [etkinliğini izleme](#monitor).

## <a name="step-8-configure-network-mapping"></a>8. adım: ağ eşlemesini yapılandırma
Başlamadan önce Ağ eşlemesi hello kaynak VMM sunucusundaki sanal makineleri bağlı tooa VM ağı olduğunu doğrulayın. Ayrıca, bir veya daha fazla Azure sanal ağı oluşturun.

Toocreate sanal bir ağ Azure Resource Manager ve PowerShell kullanılarak nasıl hakkında daha fazla bilgi [Azure Resource Manager ve PowerShell kullanarak siteden siteye VPN bağlantısı olan bir sanal ağ oluşturma](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)

Birden çok sanal makine ağları eşlenen tooa tek Azure ağ olabileceğini unutmayın. Hello hedef ağın birden çok alt ağı varsa ve bu alt ağlardan biri olan hello adıyla aynı alt ağda hangi hello kaynak sanal makinenin bulunduğu sonra hello çoğaltma sanal makinesi yük devretme bağlı toothat hedef alt olacaktır. Eşleşen ada sahip bir hedef alt ağ ise hello sanal makineye bağlı toohello hello ağdaki ilk alt ağ olacaktır.

1. Merhaba ilk komut sunucuları için geçerli Azure Site Recovery kasası hello alır. Merhaba komut hello Microsoft Azure Site Recovery sunucuları hello $Servers dizi değişkeninde depolar.

        $Servers = Get-AzureRmSiteRecoveryServer
2. Merhaba ikinci komut hello site kurtarma ağ hello ilk sunucu için hello $Servers dizisini alır. Merhaba komut hello ağları hello $Networks değişkeninde depolar.

        $Networks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[0]

1. Merhaba üçüncü komut hello $AzureVmNetworks değişkeninde Azure sanal ağlar ve bu değeri alır.

        $AzureVmNetworks =  Get-AzureRmVirtualNetwork
2. Merhaba son cmdlet'i hello birincil ağ ve hello Azure sanal makine ağı arasında bir eşleme oluşturur. Merhaba cmdlet hello birincil ağ hello ilk öğesi $Networks belirtir. Merhaba cmdlet'i bir sanal makine ağına hello ilk öğesi $AzureVmNetworks belirtir.

        New-AzureRmSiteRecoveryNetworkMapping -PrimaryNetwork $Networks[0] -AzureVMNetworkId $AzureVmNetworks[0]

## <a name="step-9-enable-protection-for-virtual-machines"></a>9. adım: sanal makineler için korumayı etkinleştir
Merhaba sunucular, Bulutlar ve ağlar doğru şekilde yapılandırıldıktan sonra hello bulutta sanal makineler için korumayı etkinleştirebilirsiniz.

 Merhaba aşağıdakileri göz önünde bulundurun:

* Sanal makineler Azure gereksinimleri karşılaması gerekir. Bu iade [Önkoşullar ve Destek](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) hello Planlama Kılavuzu'nda.
* tooenable koruma, hello işletim sistemi ve işletim sistemi disk özellikleri hello sanal makine için ayarlamanız gerekir. Bir sanal makine şablonu kullanarak VMM'de bir sanal makine oluşturduğunuzda hello özelliğini ayarlayabilirsiniz. Bu özellikleri mevcut sanal makineler üzerinde hello ayarlayabilirsiniz **genel** ve **donanım yapılandırması** sekmeleri hello sanal makine özellikleri. Bu özellikleri VMM'de ayarlamazsanız mümkün tooconfigure olacak hello Azure Site Recovery portalında bunları.

1. tooenable koruma, çalıştırma hello aşağıdaki tooget hello koruma kapsayıcısı komutu:

          $ProtectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $CloudName
2. Merhaba koruma varlık (VM) hello aşağıdaki komutu çalıştırarak alın:

           $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -friendlyName $VMName -ProtectionContainer $protectionContainer
3. Merhaba DR hello VM için komutu aşağıdaki hello çalıştırarak etkinleştirin:

          $jobResult = Set-AzureRmSiteRecoveryProtectionEntity -ProtectionEntity $protectionentity -Protection Enable –Force -Policy $policy -RecoveryAzureStorageAccountId  $storageID "/subscriptions/217653172865hcvkchgvd/resourceGroups/rajanirgps/providers/Microsoft.Storage/storageAccounts/teststorageacc1

## <a name="test-your-deployment"></a>Dağıtımınızı test edin
tootest bir test çalıştırabilirsiniz dağıtımınız tek bir sanal makine için yük devretme veya birden çok sanal makine içeren bir kurtarma planı oluşturun ve test yük devretme hello planı için çalıştırın. Test yük devretme, yük devretme ve kurtarma mekanizmanızı yalıtılmış bir ağda benzetimini yapar. Şunlara dikkat edin:

* Hello yük devretme Uzak Masaüstü'nü kullanarak azure'daki tooconnect toohello sanal makine istiyorsanız, Uzak Masaüstü Bağlantısı hello test yük devretmesi çalıştırmadan önce hello sanal makinesinde etkinleştirin.
* Yük devretme, Uzak Masaüstü kullanarak Azure'da bir ortak IP adresi tooconnect toohello sanal makine kullanacaksınız. Bu toodo istiyorsanız, bağlanan tooa sanal genel bir adres kullanarak makineden engelleyecek etki alanı ilkelerine sahip olmadığınızdan emin olun.

Merhaba işleminin toocheck hello tamamlanması izleyin hello adımlarda [etkinliğini izleme](#monitor).

### <a name="run-a-test-failover"></a>Yük devretme testi çalıştırma
- Merhaba aşağıdaki komutu çalıştırarak Hello test yük devretme başlatın:

       $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer

       $jobIDResult =  Start-AzureRmSiteRecoveryTestFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -AzureVMNetworkId <string>  

### <a name="run-a-planned-failover"></a>Planlı yük devretmeyi çalıştırma
- Başlangıç hello hello aşağıdaki komutu çalıştırarak planlanan yük devretme:

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -AzureVMNetworkId <string>  

### <a name="run-an-unplanned-failover"></a>Planlanmamış bir yük devretmeyi çalıştırma
- Başlat komutu aşağıdaki hello çalıştırarak planlanmamış yük devretme hello:

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryUnPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -AzureVMNetworkId <string>  

## <a name=monitor></a>Etkinliğini izleme
Aşağıdaki komutları toomonitor hello etkinlik hello kullanın. Merhaba işleme toofinish işleri arasında toowait gerektiğini unutmayın.

    Do
    {
        $job = Get-AzureSiteRecoveryJob -Id $associationJob.JobId;
        Write-Host "Job State:{0}, StateDescription:{1}" -f Job.State, $job.StateDescription;
        if($job -eq $null -or $job.StateDescription -ne "Completed")
        {
            $isJobLeftForProcessing = $true;
        }

    if($isJobLeftForProcessing)
        {
            Start-Sleep -Seconds 60
        }
    }While($isJobLeftForProcessing)



## <a name="next-steps"></a>Sonraki adımlar
[Daha fazla bilgi](/powershell/module/azurerm.recoveryservices.backup/#recovery) Azure Site Recovery ile Azure Resource Manager PowerShell cmdlet'leri hakkında.
