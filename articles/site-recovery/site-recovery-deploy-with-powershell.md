---
title: "PowerShell ile Merhaba Klasik portalında aaaReplicate Hyper-V sanal makineleri tooAzure | Microsoft Docs"
description: "Merhaba çoğaltma hello Klasik portalında Site Recovery ve PowerShell kullanarak VMM bulutlarındaki Hyper-V sanal makinelerin otomatik hale getirme"
services: site-recovery
documentationcenter: 
author: bsiva
manager: abhiag
editor: tysonn
ms.assetid: 9011f567-e0b4-4306-951a-b30da19f5db6
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/31/2017
ms.author: bsiva
ms.openlocfilehash: d6847b46ac227209e6890de4ab603b23f827360f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-vms-tooazure-with-powershell-in-hello-classic-portal"></a>PowerShell ile Hyper-V sanal makineleri tooAzure hello Klasik Portalı'nda çoğaltma
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

Merhaba makale hello senaryo ve Site Recovery kasası yukarı tooset nasıl yüklemenize hello kaynak VMM sunucusunda Azure Site Recovery sağlayıcısı hello gösterir önkoşulları içerir, hello sunucu hello kasaya kaydetmek, bir Azure depolama hesabı ekleme, hello Azure yükleyin Kurtarma Hizmetleri aracısını Hyper-V konak sunucuları, uygulanan tooall korumalı sanal makineler olabilir ve bu sanal makineler için korumayı etkinleştir VMM Bulutları için koruma ayarlarını yapılandırın. Sınama hello yük devretme toomake tarafından her şeyin beklendiği gibi çalıştığından emin sonlandırın.

Bu senaryoyu oluşturan ayarlama sorunlarını alıyorsanız, üzerinde hello sorularınızı [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

> [!NOTE]
> Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../azure-resource-manager/resource-manager-deployment-model.md). Bu makalede, hello Klasik dağıtım modeli kullanarak yer almaktadır.
>
>

## <a name="before-you-start"></a>Başlamadan önce
Bu Önkoşullar sağladığınızdan emin olun:

### <a name="azure-prerequisites"></a>Azure önkoşulları
* Bir [Microsoft Azure](https://azure.microsoft.com/) hesabınızın olması gerekir. [Ücretsiz deneme sürümüyle](https://azure.microsoft.com/pricing/free-trial/) başlayabilirsiniz.
* Bir Azure depolama hesabı toostore çoğaltılmış verileri gerekir. Merhaba hesabının coğrafi çoğaltmanın etkinleştirilmiş olması gerekir. Merhaba hello Azure Site kurtarma kasasıyla aynı bölgede ve ile ilişkili olmalıdır hello aynı abonelik. [Azure storage hakkında daha fazla bilgi](../storage/common/storage-introduction.md).
* Toomake tooprotect istediğiniz sanal makineleri ile uyumlu olduğundan emin olmanız gerekir [Azure sanal makine önkoşulları](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).

### <a name="vmm-prerequisites"></a>VMM önkoşulları
* System Center 2012 R2 üzerinde çalışan VMM sunucusu gerekir.
* Merhaba tooprotect istediğiniz VMM sunucusu üzerinde en az bir bulut gerekir. Merhaba bulut içermelidir:
  * Bir veya birden çok VMM ana bilgisayar grubu.
  * Bir veya daha fazla Hyper-V ana bilgisayar sunucuları veya kümeleri her konak grubundaki.
  * Merhaba kaynak Hyper-V sunucu üzerindeki bir veya daha fazla sanal makineler.

### <a name="hyper-v-prerequisites"></a>Hyper-V önkoşulları
* Merhaba Hyper-V ana bilgisayar sunucuları en az çalıştırmalıdır **Windows Server 2012** Hyper-V rolüne sahip veya **Microsoft Hyper-V Server 2012** ve hello son güncelleştirmelerin yüklü olması.
* Hyper-V'yi bir kümede çalıştırıyorsanız statik IP adresi temelli bir kümeye sahip olmanız durumunda küme aracısının otomatik olarak oluşturulamayacağını unutmayın. El ile tooconfigure hello küme Aracısı gerekir. toodo Bu, Sunucu Yöneticisi'nde > Yük Devretme Kümesi Yöneticisi ' ni toohello kümesine bağlanın, tıklatın **rolü Yapılandır** seçip **Hyper-V çoğaltma aracısı** hello içinde **Select Role**hello Yüksek Kullanılabilirlik Sihirbazı'nın ekranı.
* Herhangi bir Hyper-V konak sunucusu veya küme toomanage koruma istediğiniz VMM Bulutu eklenmesi gerekir.

### <a name="network-mapping-prerequisites"></a>Ağ eşlemesi önkoşulları
Azure ağı eşlemesinde sanal makineleri korumaya zaman hello kaynak VMM sunucusunda VM ağları ve hedef Azure ağları tooenable hello aşağıdaki arasında eşler:

* Merhaba üzerinde aynı yük devri tüm makineler ağ tooeach bulundukları hangi kurtarma planı yedeklemiş diğer bağlanabilir.
* Bir ağ geçidi Kurulum hello hedef Azure ağını üzerinde ise, sanal makineleri tooother şirket içi sanal makinelere bağlanabilir.
* Hello aynı yük devri yalnızca sanal makineler eşleme, yapılandırmazsanız ağ kurtarma planı yük devretme tooAzure sonra diğer mümkün tooconnect tooeach olacaktır.

Toodeploy ağ eşlemesi istiyorsanız hello aşağıdakiler gerekir:

* Merhaba kaynak VMM sunucusunda tooprotect istediğiniz Hello sanal makineleri bağlı tooa VM ağı olmalıdır. Bu ağ hello Bulutu ile ilişkili mantıksal ağ bağlantılı tooa olmalıdır.
* Bir Azure ağı toowhich çoğaltılan sanal makineler, yük devretme sonrasında bağlanabilir. Bu ağ hello yük devretme sırasında seçersiniz. Merhaba ağ hello olmalıdır, Azure Site Recovery abonelik aynı bölgede.

### <a name="powershell-prerequisites"></a>PowerShell önkoşulları
Azure PowerShell hazır toogo olduğundan emin olun. PowerShell zaten kullanıyorsanız, tooupgrade tooversion 0.8.10 gerekir ya da daha sonra. PowerShell ayarlama hakkında daha fazla bilgi için bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azureps-cmdlets-docs). Ayarlama ve PowerShell yapılandırılmış sonra tüm hello hizmeti için kullanılabilir cmdlet'leri hello görüntüleyebilirsiniz [burada](/powershell/azure/overview).

parametre değerleri, girişleri ve çıkışları genellikle Azure PowerShell'de işlenme gibi hello cmdlet'leri kullanmanıza yardımcı olabilecek ipuçları hakkında toolearn bkz [Azure cmdlet'leri ile çalışmaya başlama](/powershell/azure/get-started-azureps).

## <a name="step-1-set-hello-subscription"></a>1. adım: hello abonelik ayarlama
PowerShell'de bu cmdlet'leri çalıştırın:

```
$UserName = "<user@live.com>"
$Password = "<password>"
$AzureSubscriptionName = "prod_sub1"

$SecurePassword = ConvertTo-SecureString -AsPlainText $Password -Force
$Cred = New-Object System.Management.Automation.PSCredential -ArgumentList $UserName, $securePassword
Add-AzureAccount -Credential $Cred;
$AzureSubscription = Select-AzureSubscription -SubscriptionName $AzureSubscriptionName

```

Merhaba "< >" Merhaba öğelerin size özgü bilgileri ile değiştirin.

## <a name="step-2-create-a-site-recovery-vault"></a>2. adım: Site Recovery kasası oluşturma
PowerShell, belirli bilgilerinizle hello "< >" Merhaba öğeleri değiştirin ve bu komutları çalıştırın:

```

$VaultName = "<testvault123>"
$VaultGeo  = "<Southeast Asia>"
$OutputPathForSettingsFile = "<c:\>"

```


```
New-AzureSiteRecoveryVault -Location $VaultGeo -Name $VaultName;
$vault = Get-AzureSiteRecoveryVault -Name $VaultName;

```

## <a name="step-3-generate-a-vault-registration-key"></a>3. adım: kasa kayıt anahtarı oluşturma
Merhaba kasada bir kayıt anahtarı oluşturun. Hello Azure Site Recovery Sağlayıcısı'nı indirin ve hello VMM sunucusuna yükledikten sonra bu anahtar tooregister hello VMM sunucusu hello kasasına kullanacaksınız.

1. Merhaba kasası ayar dosyasını alın ve hello bağlamını ayarlayın:

   ```

   $VaultName = "<testvault123>"
   $VaultGeo  = "<Southeast Asia>"
   $OutputPathForSettingsFile = "<c:\>"

   $VaultSetingsFile = Get-AzureSiteRecoveryVaultSettingsFile -Location $VaultGeo -Name $VaultName -Path $OutputPathForSettingsFile;

   ```
2. Merhaba aşağıdaki komutları çalıştırarak Hello kasası bağlamını ayarlayın:

   ```

   $VaultSettingFilePath = $vaultSetingsFile.FilePath
   $VaultContext = Import-AzureSiteRecoveryVaultSettingsFile -Path $VaultSettingFilePath -ErrorAction Stop

   ```

## <a name="step-4-install-hello-azure-site-recovery-provider"></a>Adım 4: hello Azure Site Recovery sağlayıcısı yükleme
1. Merhaba VMM makinede hello aşağıdaki komutu çalıştırarak bir dizin oluşturun:

   ```

   pushd C:\ASR\

   ```
2. Merhaba aşağıdaki komutu çalıştırarak indirilen hello sağlayıcısını kullanarak hello dosyaları ayıklayın

   ```

   AzureSiteRecoveryProvider.exe /x:. /q

   ```
3. Merhaba Sağlayıcı komutları aşağıdaki hello kullanarak yükleyin:

   ```

   .\SetupDr.exe /i

   ```

   ```

   $installationRegPath = "hklm:\software\Microsoft\Microsoft System Center Virtual Machine Manager Server\DRAdapter"
   do
   {
     $isNotInstalled = $true;
     if(Test-Path $installationRegPath)
     {
         $isNotInstalled = $false;
     }
   }While($isNotInstalled)

   ```

   Merhaba yükleme toofinish bekleyin.
4. Hello sunucu komutu aşağıdaki hello kullanarak hello kasasına kaydedin:

   ```

   $BinPath = $env:SystemDrive+"\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin"
   pushd $BinPath
   $encryptionFilePath = "C:\temp\"
   .\DRConfigurator.exe /r /Credentials $VaultSettingFilePath /vmmfriendlyname $env:COMPUTERNAME /dataencryptionenabled $encryptionFilePath /startvmmservice

   ```

## <a name="step-5-create-an-azure-storage-account"></a>5. adım: Azure storage hesabı oluşturma
Bir Azure depolama hesabınız yoksa, hello aşağıdaki komutu çalıştırarak bir coğrafi çoğaltmanın etkinleştirilmiş hesabı oluşturun:

```

$StorageAccountName = "teststorageacc1"
$StorageAccountGeo  = "Southeast Asia"

New-AzureStorageAccount -StorageAccountName $StorageAccountName -Label $StorageAccountName -Location $StorageAccountGeo;

```

Merhaba depolama hesabı olması gerektiğini unutmayın hello hello Azure Site Recovery hizmeti ile aynı bölgeye ve ilişkilendirilmesi hello aynı abonelik.

## <a name="step-6-install-hello-azure-recovery-services-agent"></a>6. adım: hello Azure kurtarma Hizmetleri Aracısı yükleme
Hello Azure portal hello VMM bulutlarında yer alan her Hyper-V ana bilgisayar sunucusunda yükleme hello Azure kurtarma Hizmetleri Aracısı'ndan tooprotect istiyor.

Tüm VMM konaklarda komutu aşağıdaki hello çalıştırın:

```

marsagentinstaller.exe /q /nu

```


## <a name="step-7-configure-cloud-protection-settings"></a>7. adım: Bulut yapılandırma koruma ayarları
1. Bulut koruma profili tooAzure hello aşağıdaki komutu çalıştırarak oluşturun:

   ```

   $ReplicationFrequencyInSeconds = "300";
   $ProfileResult = New-AzureSiteRecoveryProtectionProfileObject -ReplicationProvider HyperVReplica -RecoveryAzureSubscription $AzureSubscriptionName -RecoveryAzureStorageAccount $StorageAccountName -ReplicationFrequencyInSeconds     $ReplicationFrequencyInSeconds;

   ```
2. Koruma kapsayıcısı hello aşağıdaki komutları çalıştırarak alın:

   ```

   $PrimaryCloud = "testcloud"
   $protectionContainer = Get-AzureSiteRecoveryProtectionContainer -Name $PrimaryCloud;

   ```
3. Merhaba ilişkilendirme hello koruma kapsayıcısı ile Merhaba bulut Başlat:

   ```

   $associationJob = Start-AzureSiteRecoveryProtectionProfileAssociationJob -ProtectionProfile $profileResult -PrimaryProtectionContainer $protectionContainer;        

   ```
4. Merhaba işi tamamlandıktan sonra hello aşağıdaki komutu çalıştırın:

        $job = Get-AzureSiteRecoveryJob -Id $associationJob.JobId;
        if($job -eq $null -or $job.StateDescription -ne "Completed")
        {
        $isJobLeftForProcessing = $true;
        }


1. Hello iş işlemeyi bitirdikten sonra hello aşağıdaki komutu çalıştırın:

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



Merhaba işleminin toocheck hello tamamlanması izleyin hello adımlarda [etkinliğini izleme](#monitor).

## <a name="step-8-configure-network-mapping"></a>8. adım: ağ eşlemesini yapılandırma
Başlamadan önce Ağ eşlemesi hello kaynak VMM sunucusundaki sanal makineleri bağlı tooa VM ağı olduğunu doğrulayın. Ayrıca, bir veya daha fazla Azure sanal ağı oluşturun. Birden fazla VM ağı eşlenen tooa tek Azure ağ olabileceğini unutmayın.

Hello hedef ağın birden çok alt ağı varsa ve bu alt ağlardan biri olan hello adıyla aynı alt ağda hangi hello kaynak sanal makinenin bulunduğu sonra hello çoğaltma sanal makinesi yük devretme sonrasında bağlı toothat hedef alt olacaktır unutmayın. Eşleşen bir ada sahip bir hedef alt ağa değilse hello sanal makineye bağlı toohello hello ağdaki ilk alt ağ olacaktır.

Merhaba ilk komut sunucuları için geçerli Azure Site Recovery kasası hello alır. Merhaba komut hello Microsoft Azure Site Recovery sunucuları hello $Servers dizi değişkeninde depolar.

    $Servers = Get-AzureSiteRecoveryServer


Merhaba ikinci komut hello site kurtarma ağ hello ilk sunucu için hello $Servers dizisini alır. Merhaba komut hello ağları hello $Networks değişkeninde depolar.

    $Networks = Get-AzureSiteRecoveryNetwork -Server $Servers[0]

Merhaba üçüncü komut hello Get-AzureSubscription cmdlet'ini kullanarak, Azure aboneliklerinize alır ve ardından bu değer hello $Subscriptions değişkeninde depolar.

    $Subscriptions = Get-AzureSubscription



Merhaba dördüncü komut hello $AzureVmNetworks değişkeninde hello Get-AzureVNetSite cmdlet'i ve bu değer'ı kullanarak Azure sanal ağlar alır.

    $AzureVmNetworks = Get-AzureVNetSite



Merhaba son cmdlet'i hello birincil ağ ve hello Azure sanal makine ağı arasında bir eşleme oluşturur. Merhaba cmdlet hello birincil ağ hello ilk öğesi $Networks belirtir. Merhaba cmdlet kimliğini kullanarak bir sanal makine ağına hello ilk öğesi $AzureVmNetworks belirtir Azure abonelik kimliğinizi Hello komut içerir

    New-AzureSiteRecoveryNetworkMapping -PrimaryNetwork $Networks[0] -AzureSubscriptionId $Subscriptions[0].SubscriptionId -AzureVMNetworkId $AzureVmNetworks[0].Id


## <a name="step-9-enable-protection-for-virtual-machines"></a>9. adım: sanal makineler için korumayı etkinleştir
Sunucular, Bulutlar ve ağlar doğru şekilde yapılandırıldıktan sonra hello bulutta sanal makineler için korumayı etkinleştirebilirsiniz. Merhaba aşağıdakileri göz önünde bulundurun:

Sanal makineler karşılamalıdır [Azure sanal makine önkoşulları](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).

tooenable koruma hello işletim sistemi ve işletim sistemi disk özellikleri hello sanal makine için ayarlamanız gerekir. Bir sanal makine şablonu kullanarak VMM'de bir sanal makine oluşturduğunuzda hello özelliğini ayarlayabilirsiniz. Bu özellikleri mevcut sanal makineler üzerinde hello ayarlayabilirsiniz **genel** ve **donanım yapılandırması** sekmeleri hello sanal makine özellikleri. Bu özellikleri VMM'de ayarlamazsanız mümkün tooconfigure olacak hello Azure Site Recovery portalında bunları.

1. tooenable koruma, çalıştırma hello aşağıdaki tooget hello koruma kapsayıcısı komutu:

     $ProtectionContainer = get-AzureSiteRecoveryProtectionContainer-ad $CloudName
2. Merhaba koruma varlık (VM) hello aşağıdaki komutu çalıştırarak alın:

        $protectionEntity = Get-AzureSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer



1. Merhaba DR hello VM için komutu aşağıdaki hello çalıştırarak etkinleştirin:

        $jobResult = Set-AzureSiteRecoveryProtectionEntity -ProtectionEntity $protectionEntity     -Protection Enable -Force



## <a name="test-your-deployment"></a>Dağıtımınızı test edin
tootest bir yük devretme sınaması için tek bir sanal makine çalıştırmak veya birden çok sanal makine içeren ve bir yük devretme testi hello için bir kurtarma planı oluşturun, dağıtımınızı planlayın. Yük devretme testi, yük devretme işleminizi ve kurtarma mekanizmanızı yalıtılmış bir ortamda benzetimli olarak gerçekleştirir. Şunlara dikkat edin:

* Hello yük devretme sonrasında Uzak Masaüstü'nü kullanarak azure'daki tooconnect toohello sanal makine istiyorsanız, Uzak Masaüstü Bağlantısı hello test yük devretmesi çalıştırmadan önce hello sanal makinesinde etkinleştirin.
* Yük devretme sonrasında, Uzak Masaüstü kullanarak Azure'da bir ortak IP adresi tooconnect toohello sanal makine kullanacaksınız. Bu toodo istiyorsanız, bağlanan tooa sanal genel bir adres kullanarak makineden engelleyecek etki alanı ilkelerine sahip olmadığınızdan emin olun.

Merhaba işleminin toocheck hello tamamlanması izleyin hello adımlarda [etkinliğini izleme](#monitor).

### <a name="create-a-recovery-plan"></a>Kurtarma planı oluşturma
1. Merhaba veri aşağıdaki kullanarak kurtarma planınız için bir şablon olarak bir .xml dosyası oluşturun ve sonra "C:\RPTemplatePath.xml" kaydedin.
2. Merhaba RecoveryPlan düğüm kimliği, ad, PrimaryServerId ve SecondaryServerId değiştirin.
3. Merhaba ProtectionEntity düğümü PrimaryProtectionEntityId (vmm'den vmıd) değiştirin.
4. Daha fazla VM'ler daha fazla ProtectionEntity düğüm ekleyerek ekleyebilirsiniz.

        <#
        <?xml version="1.0" encoding="utf-16"?>
        <RecoveryPlan Id="d0323b26-5be2-471b-addc-0a8742796610" Name="rp-test"     PrimaryServerId="9350a530-d5af-435b-9f2b-b941b5d9fcd5"     SecondaryServerId="21a9403c-6ec1-44f2-b744-b4e50b792387" Description=""     Version="V2014_07">
          <Actions />
          <ActionGroups>
            <ShutdownAllActionGroup Id="ShutdownAllActionGroup">
              <PreActionSequence />
              <PostActionSequence />
            </ShutdownAllActionGroup>
            <FailoverAllActionGroup Id="FailoverAllActionGroup">
              <PreActionSequence />
              <PostActionSequence />
            </FailoverAllActionGroup>
            <BootActionGroup Id="DefaultActionGroup">
              <PreActionSequence />
              <PostActionSequence />
              <ProtectionEntity PrimaryProtectionEntityId="d4c8ce92-a613-4c63-9b03-    cf163cc36ef8" />
            </BootActionGroup>
          </ActionGroups>
          <ActionGroupSequence>
            <ActionGroup Id="ShutdownAllActionGroup" ActionId="ShutdownAllActionGroup"     Before="FailoverAllActionGroup" />
            <ActionGroup Id="FailoverAllActionGroup" ActionId="FailoverAllActionGroup"     After="ShutdownAllActionGroup" Before="DefaultActionGroup" />
            <ActionGroup Id="DefaultActionGroup" ActionId="DefaultActionGroup" After="FailoverAllActionGroup"/>
          </ActionGroupSequence>
        </RecoveryPlan>
        #>



1. Merhaba veri hello şablonunda doldurun:

        $TemplatePath = "C:\RPTemplatePath.xml";



1. Merhaba RecoveryPlan oluşturun:

        $RPCreationJob = New-AzureSiteRecoveryRecoveryPlan -File $TemplatePath -WaitForCompletion;

### <a name="run-a-test-failover"></a>Yük devretme testi çalıştırma
1. Merhaba aşağıdaki komutu çalıştırarak Hello RecoveryPlan nesnesini alın:

     $RPObject = get-AzureSiteRecoveryRecoveryPlan-ad $RPName;
2. Merhaba aşağıdaki komutu çalıştırarak Hello test yük devretme başlatın:

        $jobIDResult = Start-AzureSiteRecoveryTestFailoverJob -RecoveryPlan $RPObject -Direction PrimaryToRecovery;


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
[Daha fazla bilgi](/powershell/azure/overview) Azure Site Recovery PowerShell cmdlet'leri hakkında. </a>.
