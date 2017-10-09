---
title: aaaReplicate PowerShell (Azure Resource Manager) ile Hyper-V sanal makineleri VMM tooa ikincil sitedeki | Microsoft Docs
description: "Nasıl toodeploy Azure Site Recovery tooorchestrate çoğaltma, yük devretme ve kurtarma Hyper-V vm'lerinde VMM Bulutu tooa (Resource Manager) PowerShell kullanarak ikincil VMM sitesi açıklar"
services: site-recovery
documentationcenter: 
author: sujaytalasila
manager: rochakm
editor: raynew
ms.assetid: 9d38e9c3-217c-4e44-830c-575e9a4141f2
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: sutalasi
ms.openlocfilehash: a769dcc68d66c18b9dc47539071f4d0e0f1db70f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooa-secondary-vmm-site-using-powershell-resource-manager"></a>Hyper-V sanal makineleri (Resource Manager) PowerShell kullanarak VMM Bulutları tooa ikincil VMM sitesi Çoğalt
> [!div class="op_single_selector"]
> * [Azure Portal](site-recovery-vmm-to-vmm.md)
> * [Klasik Portal](site-recovery-vmm-to-vmm-classic.md)
> * [PowerShell - Resource Manager](site-recovery-vmm-to-vmm-powershell-resource-manager.md)
>
>

Site Recovery tooAzure Hoş Geldiniz! Tooreplicate içi System Center Virtual Machine Manager (VMM) Bulutlar tooa ikincil sitede yönetilen Hyper-V sanal makinelerin istiyorsanız, bu makaleyi kullanın.

Bu makalede, System Center VMM Bulutları tooSystem Center VMM bulutlarında ikincil sitede Azure Site Recovery tooreplicate Hyper-V sanal makineleri ayarladığınızda nasıl toouse PowerShell tooautomate ortak görevleri tooperform ihtiyacınız gösterir.

Merhaba makale hello senaryonun önkoşulları içerir ve gösterir

* Nasıl tooset bir kurtarma Hizmetleri kasası ayarlama
* Merhaba kaynak VMM sunucusunda ve hello hedef VMM sunucusunda Hello Azure Site Recovery sağlayıcısı yükleme
* Merhaba VMM sunucuları hello kasaya kaydetmek
* Merhaba VMM bulutu için çoğaltma ilkesini yapılandırın. hello İlkesi'nde Hello çoğaltma ayarları uygulanan tooall korumalı sanal makineler olacaktır
* Merhaba sanal makineler için korumayı etkinleştirin.
* VM'nin hello yük devretme testi ayrı ayrı veya bir kurtarmanın parçası olarak toomake her şeyin beklendiği gibi çalıştığından emin planlayın.
* Planlanmış veya planlanmamış bir yük devretme VM'lerin ayrı ayrı veya bir kurtarma planı toomake her şeyin beklendiği gibi çalıştığından emin bir parçası olarak gerçekleştirin.

Bu senaryoyu oluşturan ayarlama sorunlarını alıyorsanız, üzerinde hello sorularınızı [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

> [!NOTE]
> Azure, kaynak oluşturmak ve bu kaynaklarla çalışmak için iki [dağıtım modeli](../azure-resource-manager/resource-manager-deployment-model.md) kullanır: Azure Resource Manager ve klasik model. Ayrıca Azure iki portala – hello Klasik dağıtım modelini destekleyen Klasik Azure portalı hello ve her iki dağıtım modeline de destek Azure portal hello sahiptir. Bu makalede, hello Resource Manager dağıtım modeli yer almaktadır.
>
>

## <a name="on-premises-prerequisites"></a>Şirket içi önkoşullar
İşte hello birincil gerekenler ve bu senaryo ikincil şirket içi siteler toodeploy:

| **Önkoşullar** | **Ayrıntılar** |
| --- | --- |
| **VMM** |Bir VMM sunucusunun hello birincil sitede ve hello ikincil sitedeki VMM sunucusu dağıtmak öneririz.<br/><br/> Ayrıca [tek bir VMM sunucusundaki Bulutlar arasında çoğaltma](site-recovery-vmm-to-vmm.md#prepare-for-single-server-deployment). toodo bu hello VMM sunucusunda yapılandırılmış en az iki bulut gerekir.<br/><br/> VMM sunucuları çalışıyor. en az hello en son güncelleştirmeleri içeren System Center 2012 SP1.<br/><br/> Her bir VMM sunucusunun tek sahip olmalı veya daha fazla bulut yapılandırılmış ve tüm Bulutlar hello Hyper-V Kapasite profili kümesine sahip olması gerekir. <br/><br/>Bulut bir veya daha fazla VMM ana bilgisayar grubu içermesi gerekir.<br/><br/>VMM bulutlarını ayarlama hakkında daha fazla bilgi [yapılandırma hello VMM bulut doku](https://msdn.microsoft.com/library/azure/dn469075.aspx#BKMK_Fabric), ve [izlenecek yol: System Center 2012 SP1 VMM içeren özel bulut oluşturma](http://blogs.technet.com/b/keithmayer/archive/2013/04/18/walkthrough-creating-private-clouds-with-system-center-2012-sp1-virtual-machine-manager-build-your-private-cloud-in-a-month.aspx).<br/><br/> VMM sunucuları Internet erişimine sahip olmalıdır. |
| **Hyper-V** |Hyper-V sunucuları çalışıyor olmalıdır en az Windows Server 2012 hello Hyper-V rolüne sahip ve hello son güncelleştirmelerin yüklü olması.<br/><br/> Bir Hyper-V sunucusunun bir veya daha fazla VM içermesi gerekir.<br/><br/>  Hyper-V ana bilgisayar sunucuları konak grupları hello birincil ve ikincil VMM bulutlarında yer.<br/><br/> Windows Server 2012 R2'de bir kümede Hyper-V çalıştırıyorsanız, yüklemelisiniz [2961977 güncelleştir](https://support.microsoft.com/kb/2961977)<br/><br/> Bir kümede küme aracısının Windows Server 2012 Not üzerinde Hyper-V çalıştırıyorsanız, bir statik IP adresi tabanlı kümeniz varsa otomatik olarak oluşturulmaz. El ile tooconfigure hello küme Aracısı gerekir. [Daha fazla bilgi edinin](http://social.technet.microsoft.com/wiki/contents/articles/18792.configure-replica-broker-role-cluster-to-cluster-replication.aspx). |
| **Sağlayıcı** |Site Recovery dağıtımı sırasında VMM sunucularına Azure Site Recovery sağlayıcısı hello yükleyin. Merhaba sağlayıcısı HTTPS 443 tooorchestrate çoğaltma Site Recovery ile iletişim kurar. Veri çoğaltma hello LAN üzerinden hello birincil ve ikincil Hyper-V sunucuları veya bir VPN bağlantısı arasında oluşur.<br/><br/> Merhaba hello VMM sunucusunda çalışan sağlayıcı toothese URL'leri erişimi gerektirir: *. hypervrecoverymanager.windowsazure.com; *. accesscontrol.windows.net; *. backup.windowsazure.com; *. blob.core.windows.net; *. store.core.windows.net.<br/><br/> Ayrıca hello VMM sunucuları toohello gelen güvenlik duvarı iletişimi izin [Azure veri merkezi IP aralıkları](https://www.microsoft.com/download/confirmation.aspx?id=41653) ve hello HTTPS (443) protokolüne izin verin. |

### <a name="network-mapping-prerequisites"></a>Ağ eşlemesi önkoşulları
Ağ eşlemesi eşlemeleri hello birincil ve ikincil VMM sunucuları için VMM VM ağlarında arasında:

* En iyi şekilde çoğaltılan VM'ler üzerinde ikincil Hyper-V konakları yük devretme sonrasında yerleştirin.
* Çoğaltma sanal makineleri tooappropriate VM ağları bağlayın.
* Ağ yapılandırmazsanız çoğaltma eşleme VM'ler bağlı tooany Ağ Yük devretme sonrasında olmayacaktır.
* Ağ tooset istiyorsanız Site kurtarması sırasında eşleme gerekenler dağıtım burada verilmiştir:

  * Merhaba kaynağı Hyper-V konak sunucusu üzerinde sanal makineleri bağlı tooa VMM VM ağ olduğundan emin olun. Bu ağ hello Bulutu ile ilişkili mantıksal ağ bağlantılı tooa olmalıdır.
  * Kurtarma için kullanacağınız hello ikincil bulut yapılandırılmış karşılık gelen VM ağı olduğundan emin olun. Bir VM ağı hello ikincil bulutla ilişkilendirilen mantıksal ağ bağlantılı tooa olmalıdır.

Merhaba makaleleri aşağıda VMM ağları yapılandırma hakkında daha fazla bilgi edinin

* [Nasıl tooconfigure vmm'de Mantıksal ağlar](http://go.microsoft.com/fwlink/p/?LinkId=386307)
* [Nasıl tooconfigure VM ağları ve ağ geçitlerini vmm'de](http://go.microsoft.com/fwlink/p/?LinkId=386308)

Ağ eşlemesinin nasıl çalıştığı hakkında [daha fazla bilgi edinin](site-recovery-vmm-to-vmm.md#prepare-for-network-mapping).

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
1. Zaten yoksa, bir Azure Resource Manager kaynak grubu oluşturun

        New-AzureRmResourceGroup -Name #ResourceGroupName -Location #location
2. Yeni bir kurtarma Hizmetleri kasası oluşturun ve ASR kasası nesne (daha sonra kullanılacak) bir değişkende oluşturulan hello kaydedin. Merhaba ASR kasası nesne post oluşturma hello Get-AzureRMRecoveryServicesVault cmdlet'ini kullanarak elde edebilirsiniz:-

        $vault = New-AzureRmRecoveryServicesVault -Name #vaultname -ResouceGroupName #ResourceGroupName -Location #location

## <a name="step-3-set-hello-recovery-services-vault-context"></a>3. adım: hello kurtarma Hizmetleri kasası bağlamını ayarlayın
1. Önceden oluşturulmuş bir kasa varsa, komut tooget hello kasası altındaki hello çalıştırın.

       $vault = Get-AzureRmRecoveryServicesVault -Name #vaultname
2. Hello aşağıdaki komutu çalıştırarak Hello kasası bağlamını ayarlayın.

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

## <a name="step-5-create-and-associate-a-replication-policy"></a>5. adım: Oluşturun ve bir çoğaltma ilkesi ilişkilendirin
1. Merhaba aşağıdaki komutu çalıştırarak bir 2012 R2 Hyper-V çoğaltma ilkesi oluşturun:

        $ReplicationFrequencyInSeconds = "300";        #options are 30,300,900
        $PolicyName = “replicapolicy”
        $RepProvider = HyperVReplica2012R2
        $Recoverypoints = 24                    #specify hello number of hours tooretain recovery pints
        $AppConsistentSnapshotFrequency = 4 #specify hello frequency (in hours) at which app consistent snapshots are taken
        $AuthMode = "Kerberos"  #options are "Kerberos" or "Certificate"
        $AuthPort = "8083"  #specify hello port number that will be used for replication traffic on Hyper-V hosts
        $InitialRepMethod = "Online" #options are "Online" or "Offline"

        $policyresult = New-AzureRmSiteRecoveryPolicy -Name $policyname -ReplicationProvider $RepProvider -ReplicationFrequencyInSeconds $Replicationfrequencyinseconds -RecoveryPoints $recoverypoints -ApplicationConsistentSnapshotFrequencyInHours $AppConsistentSnapshotFrequency -Authentication $AuthMode -ReplicationPort $AuthPort -ReplicationMethod $InitialRepMethod

    > [!NOTE]
    > Merhaba VMM bulut (Merhaba Hyper-V önkoşullarını belirtildiği gibi) Windows Server'ın farklı sürümlerini çalıştıran Hyper-V konakları içerebilir, ancak hello çoğaltma ilkedir belirli işletim sistemi sürümü. Farklı işletim sistemi sürümlerinde çalışan farklı ana bilgisayarınız varsa, her tür işletim sistemi sürümü için ayrı çoğaltma ilkeleri oluşturun. İçin örn: Windows sunucuları 2012 ve Windows Server 2012 R2'de üç çalışan beş ana bilgisayarınız varsa, iki oluşturmak çoğaltma ilkeleri – bir işletim sistemi sürümleri her tür.

1. Hello birincil koruma kapsayıcısı (birincil VMM Bulutu) ve kurtarma koruma kapsayıcısı (Kurtarma VMM bulut) hello aşağıdaki komutları çalıştırarak alın:

       $PrimaryCloud = "testprimarycloud"
       $primaryprotectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $PrimaryCloud;  

       $RecoveryCloud = "testrecoverycloud"
       $recoveryprotectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $RecoveryCloud;  
2. 1. adım kullanarak oluşturduğunuz hello İlkesi almak hello İlkesi hello kolay adı

       $policy = Get-AzureRmSiteRecoveryPolicy -FriendlyName $policyname
3. Merhaba koruma kapsayıcısı (VMM Bulutu) Hello ilişkilendirmesini hello çoğaltma ilkesiyle başlatın:

       $associationJob  = Start-AzureRmSiteRecoveryPolicyAssociationJob -Policy     $Policy -PrimaryProtectionContainer $primaryprotectionContainer -RecoveryProtectionContainer $recoveryprotectionContainer
4. Hello İlkesi ilişkilendirme iş toocomplete bekleyin. Merhaba iş PowerShell parçacığını aşağıdaki hello kullanarak tamamlandı kontrol edebilirsiniz.

       $job = Get-AzureRmSiteRecoveryJob -Job $associationJob

       if($job -eq $null -or $job.StateDescription -ne "Completed")
       {
         $isJobLeftForProcessing = $true;
       }

   Hello iş işlemeyi bitirdikten sonra hello aşağıdaki komutu çalıştırın:

       if($isJobLeftForProcessing)
       {
         Start-Sleep -Seconds 60
       }
       }While($isJobLeftForProcessing)

Merhaba işleminin toocheck hello tamamlanması izleyin hello adımlarda [etkinliğini izleme](#monitor).

## <a name="step-6-configure-network-mapping"></a>6. adım: ağ eşlemesini yapılandırma
1. Merhaba ilk komut sunucuları için geçerli Azure Site Recovery kasası hello alır. Merhaba komut hello Microsoft Azure Site Recovery sunucuları hello $Servers dizi değişkeninde depolar.

        $Servers = Get-AzureRmSiteRecoveryServer
2. Merhaba komutları aşağıda hello site kurtarma ağ hello kaynak VMM sunucusunu ve hello hedef VMM sunucusu için alın.

        $PrimaryNetworks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[0]        

        $RecoveryNetworks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[1]

    > [!NOTE]
    > Merhaba kaynak VMM sunucusunu olması hello birinci veya hello ikinci bir söz hello sunucuları dizi. Hello VMM sunucularının Hello adlarını denetleyin ve hello ağları uygun şekilde Al


1. Merhaba son cmdlet'i hello birincil ağ ve hello kurtarma ağ arasında bir eşleme oluşturur. Merhaba cmdlet hello birincil ağ kurtarma ağ $PrimaryNetworks ve hello $RecoveryNetworks hello ilk öğesi olarak hello ilk öğesi olarak belirtir.

        New-AzureRmSiteRecoveryNetworkMapping -PrimaryNetwork $PrimaryNetworks[0] -RecoveryNetwork $RecoveryNetworks[0]

## <a name="step-7-configure-storage-mapping"></a>7. adım: depolama eşlemesi yapılandırma
1. Merhaba komutu aşağıda depolama sınıflandırmaları $storageclassifications değişkeni içine hello listesini alır.

        $storageclassifications = Get-AzureRmSiteRecoveryStorageClassification
2. Merhaba komutları aşağıda hello kaynak sınıflandırma $SourceClassificaion değişkeni içine ve hedef sınıflandırma $TargetClassification değişkeni içine alın.

        $SourceClassificaion = $storageclassifications[0]

        $TargetClassification = $storageclassifications[1]

    > [!NOTE]
    > Merhaba kaynak ve hedef sınıflandırmaları hello dizisinde herhangi bir öğe olabilir. Kaynak ve hedef sınıflandırmaları $storageclassifications dizisindeki komutu toofigure hello dizini altındaki hello toohello çıktısını bakın.

    > Get-AzureRmSiteRecoveryStorageClassification | Select-Object - FriendlyName özelliği, kimliği | Tablo Biçimlendir


1. Aşağıdaki cmdlet'i Hello hello kaynak sınıflandırma ve hello Hedef Sınıflandırma arasında bir eşleme oluşturur.

        New-AzureRmSiteRecoveryStorageClassificationMapping -PrimaryStorageClassification $SourceClassificaion -RecoveryStorageClassification $TargetClassification

## <a name="step-8-enable-protection-for-virtual-machines"></a>8. Adım: Sanal makinelere yönelik korumayı etkinleştirme
Merhaba sunucular, Bulutlar ve ağlar doğru şekilde yapılandırıldıktan sonra hello bulutta sanal makineler için korumayı etkinleştirebilirsiniz.

1. tooenable koruma, çalıştırma hello aşağıdaki tooget hello koruma kapsayıcısı komutu:

          $PrimaryProtectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $PrimaryCloudName
2. Merhaba koruma varlık (VM) hello aşağıdaki komutu çalıştırarak alın:

           $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -friendlyName $VMName -ProtectionContainer $PrimaryProtectionContainer
3. Merhaba VM için çoğaltma hello aşağıdaki komutu çalıştırarak etkinleştirin:

          $jobResult = Set-AzureRmSiteRecoveryProtectionEntity -ProtectionEntity $protectionentity -Protection Enable -Policy $policy

## <a name="test-your-deployment"></a>Dağıtımınızı test edin
tootest bir yük devretme sınaması için tek bir sanal makine çalıştırmak veya birden çok sanal makine içeren ve bir yük devretme testi hello için bir kurtarma planı oluşturun, dağıtımınızı planlayın. Yük devretme testi, yük devretme işleminizi ve kurtarma mekanizmanızı yalıtılmış bir ortamda benzetimli olarak gerçekleştirir.

> [!NOTE]
> Azure Portalı'nda, uygulamanız için bir kurtarma planı oluşturabilirsiniz.
>
>

Merhaba işleminin toocheck hello tamamlanması izleyin hello adımlarda [etkinliğini izleme](#monitor).

### <a name="run-a-test-failover"></a>Yük devretme testi çalıştırma
1. Vm'leriniz için tootest yük devretme istediğiniz cmdlet'leri tooget hello VM ağ toowhich aşağıda Hello çalıştırın.

       $Servers = Get-AzureRmSiteRecoveryServer
       $RecoveryNetworks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[1]
2. VM bir sınama yük devretmesi hello aşağıdakileri yaparak gerçekleştirin:

       $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -FriendlyName $VMName -ProtectionContainer $PrimaryprotectionContainer

       $jobIDResult =  Start-AzureRmSiteRecoveryTestFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -VMNetwork $RecoveryNetworks[1]
3. Bir kurtarma planı bir sınama yük devretmesi hello aşağıdakileri yaparak gerçekleştirin:

       $recoveryplanname = "test-recovery-plan"

       $recoveryplan = Get-AzureRmSiteRecoveryRecoveryPlan -FriendlyName $recoveryplanname

       $jobIDResult =  Start-AzureRmSiteRecoveryTestFailoverJob -Direction PrimaryToRecovery -Recoveryplan $recoveryplan -VMNetwork $RecoveryNetworks[1]

### <a name="run-a-planned-failover"></a>Planlı yük devretmeyi çalıştırma
1. Merhaba aşağıdakileri yaparak bir VM planlanmış bir yük devretme gerçekleştirin:

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $PrimaryprotectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity
2. Merhaba aşağıdakileri yaparak bir kurtarma planı planlanan bir yük devretme gerçekleştirin:

        $recoveryplanname = "test-recovery-plan"

        $recoveryplan = Get-AzureRmSiteRecoveryRecoveryPlan -FriendlyName $recoveryplanname

        $jobIDResult =  Start-AzureRmSiteRecoveryPlannedFailoverJob -Direction PrimaryToRecovery -Recoveryplan $recoveryplan

### <a name="run-an-unplanned-failover"></a>Planlanmamış bir yük devretmeyi çalıştırma
1. Merhaba aşağıdakileri yaparak bir VM planlanmamış yük devretme gerçekleştirin:

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $PrimaryprotectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryUnPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity

2. hello aşağıdakileri yaparak bir kurtarma planı planlanmamış yük devretme gerçekleştirin:

        $recoveryplanname = "test-recovery-plan"

        $recoveryplan = Get-AzureRmSiteRecoveryRecoveryPlan -FriendlyName $recoveryplanname

        $jobIDResult =  Start-AzureRmSiteRecoveryUnPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity

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
