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
# <a name="replicate-hyper-v-vms-tooazure-with-powershell-in-hello-classic-portal"></a><span data-ttu-id="75f47-103">PowerShell ile Hyper-V sanal makineleri tooAzure hello Klasik Portalı'nda çoğaltma</span><span class="sxs-lookup"><span data-stu-id="75f47-103">Replicate Hyper-V VMs tooAzure with PowerShell in hello classic portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="75f47-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="75f47-104">Azure Portal</span></span>](site-recovery-vmm-to-azure.md)
> * [<span data-ttu-id="75f47-105">PowerShell - Resource Manager</span><span class="sxs-lookup"><span data-stu-id="75f47-105">PowerShell - Resource Manager</span></span>](site-recovery-vmm-to-azure-powershell-resource-manager.md)
> * [<span data-ttu-id="75f47-106">Klasik Portal</span><span class="sxs-lookup"><span data-stu-id="75f47-106">Classic Portal</span></span>](site-recovery-vmm-to-azure-classic.md)
> * [<span data-ttu-id="75f47-107">PowerShell - Klasik</span><span class="sxs-lookup"><span data-stu-id="75f47-107">PowerShell - Classic</span></span>](site-recovery-deploy-with-powershell.md)
>
>

## <a name="overview"></a><span data-ttu-id="75f47-108">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="75f47-108">Overview</span></span>
<span data-ttu-id="75f47-109">Azure Site Recovery, çoğaltma, yük devretme ve kurtarma çeşitli dağıtım senaryolarında sanal makinelerin düzenleyerek tooyour iş sürekliliği ve olağanüstü durum kurtarma (BCDR) stratejinize katkı sağlar.</span><span class="sxs-lookup"><span data-stu-id="75f47-109">Azure Site Recovery contributes tooyour business continuity and disaster recovery (BCDR) strategy by orchestrating replication, failover and recovery of virtual machines in a number of deployment scenarios.</span></span> <span data-ttu-id="75f47-110">Dağıtım tam listesi için bkz: hello senaryoları [Azure Site Recovery genel bakış](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="75f47-110">For a full list of deployment scenarios see hello [Azure Site Recovery overview](site-recovery-overview.md).</span></span>

<span data-ttu-id="75f47-111">Bu makalede, Azure Site Recovery tooreplicate Hyper-V sanal makineleri System Center VMM Bulutları tooAzure depolama ayarlarken nasıl toouse PowerShell tooautomate ortak görevleri tooperform ihtiyacınız gösterir.</span><span class="sxs-lookup"><span data-stu-id="75f47-111">This article shows you how toouse PowerShell tooautomate common tasks you need tooperform when you set up Azure Site Recovery tooreplicate Hyper-V virtual machines in System Center VMM clouds tooAzure storage.</span></span>

<span data-ttu-id="75f47-112">Merhaba makale hello senaryo ve Site Recovery kasası yukarı tooset nasıl yüklemenize hello kaynak VMM sunucusunda Azure Site Recovery sağlayıcısı hello gösterir önkoşulları içerir, hello sunucu hello kasaya kaydetmek, bir Azure depolama hesabı ekleme, hello Azure yükleyin Kurtarma Hizmetleri aracısını Hyper-V konak sunucuları, uygulanan tooall korumalı sanal makineler olabilir ve bu sanal makineler için korumayı etkinleştir VMM Bulutları için koruma ayarlarını yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="75f47-112">hello article includes prerequisites for hello scenario, and shows you how tooset up a Site Recovery vault, install hello Azure Site Recovery Provider on hello source VMM server, register hello server in hello vault, add an Azure storage account, install hello Azure Recovery Services agent on Hyper-V host servers, configure protection settings for VMM clouds that will be applied tooall protected virtual machines, and then enable protection for those virtual machines.</span></span> <span data-ttu-id="75f47-113">Sınama hello yük devretme toomake tarafından her şeyin beklendiği gibi çalıştığından emin sonlandırın.</span><span class="sxs-lookup"><span data-stu-id="75f47-113">Finish up by testing hello failover toomake sure everything's working as expected.</span></span>

<span data-ttu-id="75f47-114">Bu senaryoyu oluşturan ayarlama sorunlarını alıyorsanız, üzerinde hello sorularınızı [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="75f47-114">If you run into problems setting up this scenario, post your questions on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

> [!NOTE]
> <span data-ttu-id="75f47-115">Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="75f47-115">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="75f47-116">Bu makalede, hello Klasik dağıtım modeli kullanarak yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="75f47-116">This article covers using hello Classic deployment model.</span></span>
>
>

## <a name="before-you-start"></a><span data-ttu-id="75f47-117">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="75f47-117">Before you start</span></span>
<span data-ttu-id="75f47-118">Bu Önkoşullar sağladığınızdan emin olun:</span><span class="sxs-lookup"><span data-stu-id="75f47-118">Make sure you have these prerequisites in place:</span></span>

### <a name="azure-prerequisites"></a><span data-ttu-id="75f47-119">Azure önkoşulları</span><span class="sxs-lookup"><span data-stu-id="75f47-119">Azure prerequisites</span></span>
* <span data-ttu-id="75f47-120">Bir [Microsoft Azure](https://azure.microsoft.com/) hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="75f47-120">You'll need a [Microsoft Azure](https://azure.microsoft.com/) account.</span></span> <span data-ttu-id="75f47-121">[Ücretsiz deneme sürümüyle](https://azure.microsoft.com/pricing/free-trial/) başlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="75f47-121">You can start with a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="75f47-122">Bir Azure depolama hesabı toostore çoğaltılmış verileri gerekir.</span><span class="sxs-lookup"><span data-stu-id="75f47-122">You'll need an Azure storage account toostore replicated data.</span></span> <span data-ttu-id="75f47-123">Merhaba hesabının coğrafi çoğaltmanın etkinleştirilmiş olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="75f47-123">hello account needs geo-replication enabled.</span></span> <span data-ttu-id="75f47-124">Merhaba hello Azure Site kurtarma kasasıyla aynı bölgede ve ile ilişkili olmalıdır hello aynı abonelik.</span><span class="sxs-lookup"><span data-stu-id="75f47-124">It should be in hello same region as hello Azure Site Recovery vault and be associated with hello same subscription.</span></span> <span data-ttu-id="75f47-125">[Azure storage hakkında daha fazla bilgi](../storage/common/storage-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="75f47-125">[Learn more about Azure storage](../storage/common/storage-introduction.md).</span></span>
* <span data-ttu-id="75f47-126">Toomake tooprotect istediğiniz sanal makineleri ile uyumlu olduğundan emin olmanız gerekir [Azure sanal makine önkoşulları](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span><span class="sxs-lookup"><span data-stu-id="75f47-126">You'll need toomake sure that virtual machines you want tooprotect comply with [Azure virtual machine prerequisites](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>

### <a name="vmm-prerequisites"></a><span data-ttu-id="75f47-127">VMM önkoşulları</span><span class="sxs-lookup"><span data-stu-id="75f47-127">VMM prerequisites</span></span>
* <span data-ttu-id="75f47-128">System Center 2012 R2 üzerinde çalışan VMM sunucusu gerekir.</span><span class="sxs-lookup"><span data-stu-id="75f47-128">You'll need  VMM server running on System Center 2012 R2.</span></span>
* <span data-ttu-id="75f47-129">Merhaba tooprotect istediğiniz VMM sunucusu üzerinde en az bir bulut gerekir.</span><span class="sxs-lookup"><span data-stu-id="75f47-129">You'll need at least one cloud on hello VMM server you want tooprotect.</span></span> <span data-ttu-id="75f47-130">Merhaba bulut içermelidir:</span><span class="sxs-lookup"><span data-stu-id="75f47-130">hello cloud should contain:</span></span>
  * <span data-ttu-id="75f47-131">Bir veya birden çok VMM ana bilgisayar grubu.</span><span class="sxs-lookup"><span data-stu-id="75f47-131">One or more VMM host groups.</span></span>
  * <span data-ttu-id="75f47-132">Bir veya daha fazla Hyper-V ana bilgisayar sunucuları veya kümeleri her konak grubundaki.</span><span class="sxs-lookup"><span data-stu-id="75f47-132">One or more Hyper-V host servers or clusters in each host group .</span></span>
  * <span data-ttu-id="75f47-133">Merhaba kaynak Hyper-V sunucu üzerindeki bir veya daha fazla sanal makineler.</span><span class="sxs-lookup"><span data-stu-id="75f47-133">One or more virtual machines on hello source Hyper-V server.</span></span>

### <a name="hyper-v-prerequisites"></a><span data-ttu-id="75f47-134">Hyper-V önkoşulları</span><span class="sxs-lookup"><span data-stu-id="75f47-134">Hyper-V prerequisites</span></span>
* <span data-ttu-id="75f47-135">Merhaba Hyper-V ana bilgisayar sunucuları en az çalıştırmalıdır **Windows Server 2012** Hyper-V rolüne sahip veya **Microsoft Hyper-V Server 2012** ve hello son güncelleştirmelerin yüklü olması.</span><span class="sxs-lookup"><span data-stu-id="75f47-135">hello host Hyper-V servers must be running at least **Windows Server 2012** with Hyper-V role or **Microsoft Hyper-V Server 2012** and have hello latest updates installed.</span></span>
* <span data-ttu-id="75f47-136">Hyper-V'yi bir kümede çalıştırıyorsanız statik IP adresi temelli bir kümeye sahip olmanız durumunda küme aracısının otomatik olarak oluşturulamayacağını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="75f47-136">If you're running Hyper-V in a cluster note that cluster broker isn't created automatically if you have a static IP address-based cluster.</span></span> <span data-ttu-id="75f47-137">El ile tooconfigure hello küme Aracısı gerekir.</span><span class="sxs-lookup"><span data-stu-id="75f47-137">You'll need tooconfigure hello cluster broker manually.</span></span> <span data-ttu-id="75f47-138">toodo Bu, Sunucu Yöneticisi'nde > Yük Devretme Kümesi Yöneticisi ' ni toohello kümesine bağlanın, tıklatın **rolü Yapılandır** seçip **Hyper-V çoğaltma aracısı** hello içinde **Select Role**hello Yüksek Kullanılabilirlik Sihirbazı'nın ekranı.</span><span class="sxs-lookup"><span data-stu-id="75f47-138">toodo this, in Server Manager > Failover Cluster Manager, connect toohello cluster, click **Configure Role** and select **Hyper-V Replica Broker** in hello **Select Role** screen of hello High Availability wizard.</span></span>
* <span data-ttu-id="75f47-139">Herhangi bir Hyper-V konak sunucusu veya küme toomanage koruma istediğiniz VMM Bulutu eklenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="75f47-139">Any Hyper-V host server or cluster for which you want toomanage protection must be included in a VMM cloud.</span></span>

### <a name="network-mapping-prerequisites"></a><span data-ttu-id="75f47-140">Ağ eşlemesi önkoşulları</span><span class="sxs-lookup"><span data-stu-id="75f47-140">Network mapping prerequisites</span></span>
<span data-ttu-id="75f47-141">Azure ağı eşlemesinde sanal makineleri korumaya zaman hello kaynak VMM sunucusunda VM ağları ve hedef Azure ağları tooenable hello aşağıdaki arasında eşler:</span><span class="sxs-lookup"><span data-stu-id="75f47-141">When you protect virtual machines in Azure network mapping maps between VM networks on hello source VMM server and target Azure networks tooenable hello following:</span></span>

* <span data-ttu-id="75f47-142">Merhaba üzerinde aynı yük devri tüm makineler ağ tooeach bulundukları hangi kurtarma planı yedeklemiş diğer bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="75f47-142">All machines which fail over on hello same network can connect tooeach other, irrespective of which recovery plan they are in.</span></span>
* <span data-ttu-id="75f47-143">Bir ağ geçidi Kurulum hello hedef Azure ağını üzerinde ise, sanal makineleri tooother şirket içi sanal makinelere bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="75f47-143">If a network gateway is setup on hello target Azure network, virtual machines can connect tooother on-premises virtual machines.</span></span>
* <span data-ttu-id="75f47-144">Hello aynı yük devri yalnızca sanal makineler eşleme, yapılandırmazsanız ağ kurtarma planı yük devretme tooAzure sonra diğer mümkün tooconnect tooeach olacaktır.</span><span class="sxs-lookup"><span data-stu-id="75f47-144">If you don’t configure network mapping only virtual machines that fail over in hello same recovery plan will be able tooconnect tooeach other after failover tooAzure.</span></span>

<span data-ttu-id="75f47-145">Toodeploy ağ eşlemesi istiyorsanız hello aşağıdakiler gerekir:</span><span class="sxs-lookup"><span data-stu-id="75f47-145">If you want toodeploy network mapping you'll need hello following:</span></span>

* <span data-ttu-id="75f47-146">Merhaba kaynak VMM sunucusunda tooprotect istediğiniz Hello sanal makineleri bağlı tooa VM ağı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="75f47-146">hello virtual machines you want tooprotect on hello source VMM server should be connected tooa VM network.</span></span> <span data-ttu-id="75f47-147">Bu ağ hello Bulutu ile ilişkili mantıksal ağ bağlantılı tooa olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="75f47-147">That network should be linked tooa logical network that is associated with hello cloud.</span></span>
* <span data-ttu-id="75f47-148">Bir Azure ağı toowhich çoğaltılan sanal makineler, yük devretme sonrasında bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="75f47-148">An Azure network toowhich replicated virtual machines can connect after failover.</span></span> <span data-ttu-id="75f47-149">Bu ağ hello yük devretme sırasında seçersiniz.</span><span class="sxs-lookup"><span data-stu-id="75f47-149">You'll select this network at hello time of failover.</span></span> <span data-ttu-id="75f47-150">Merhaba ağ hello olmalıdır, Azure Site Recovery abonelik aynı bölgede.</span><span class="sxs-lookup"><span data-stu-id="75f47-150">hello network should be in hello same region as your Azure Site Recovery subscription.</span></span>

### <a name="powershell-prerequisites"></a><span data-ttu-id="75f47-151">PowerShell önkoşulları</span><span class="sxs-lookup"><span data-stu-id="75f47-151">PowerShell prerequisites</span></span>
<span data-ttu-id="75f47-152">Azure PowerShell hazır toogo olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="75f47-152">Make sure you have Azure PowerShell ready toogo.</span></span> <span data-ttu-id="75f47-153">PowerShell zaten kullanıyorsanız, tooupgrade tooversion 0.8.10 gerekir ya da daha sonra.</span><span class="sxs-lookup"><span data-stu-id="75f47-153">If you are already using PowerShell, you'll need tooupgrade tooversion 0.8.10 or later.</span></span> <span data-ttu-id="75f47-154">PowerShell ayarlama hakkında daha fazla bilgi için bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="75f47-154">For information about setting up PowerShell, see [How tooinstall and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="75f47-155">Ayarlama ve PowerShell yapılandırılmış sonra tüm hello hizmeti için kullanılabilir cmdlet'leri hello görüntüleyebilirsiniz [burada](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="75f47-155">Once you have set up and configured PowerShell, you can view all of hello available cmdlets for hello service [here](/powershell/azure/overview).</span></span>

<span data-ttu-id="75f47-156">parametre değerleri, girişleri ve çıkışları genellikle Azure PowerShell'de işlenme gibi hello cmdlet'leri kullanmanıza yardımcı olabilecek ipuçları hakkında toolearn bkz [Azure cmdlet'leri ile çalışmaya başlama](/powershell/azure/get-started-azureps).</span><span class="sxs-lookup"><span data-stu-id="75f47-156">toolearn about tips that can help you use hello cmdlets, such as how parameter values, inputs, and outputs are typically handled in Azure PowerShell, see [Get Started with Azure Cmdlets](/powershell/azure/get-started-azureps).</span></span>

## <a name="step-1-set-hello-subscription"></a><span data-ttu-id="75f47-157">1. adım: hello abonelik ayarlama</span><span class="sxs-lookup"><span data-stu-id="75f47-157">Step 1: Set hello subscription</span></span>
<span data-ttu-id="75f47-158">PowerShell'de bu cmdlet'leri çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="75f47-158">In PowerShell, run these cmdlets:</span></span>

```
$UserName = "<user@live.com>"
$Password = "<password>"
$AzureSubscriptionName = "prod_sub1"

$SecurePassword = ConvertTo-SecureString -AsPlainText $Password -Force
$Cred = New-Object System.Management.Automation.PSCredential -ArgumentList $UserName, $securePassword
Add-AzureAccount -Credential $Cred;
$AzureSubscription = Select-AzureSubscription -SubscriptionName $AzureSubscriptionName

```

<span data-ttu-id="75f47-159">Merhaba "< >" Merhaba öğelerin size özgü bilgileri ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="75f47-159">Replace hello elements within hello "< >" with your specific information.</span></span>

## <a name="step-2-create-a-site-recovery-vault"></a><span data-ttu-id="75f47-160">2. adım: Site Recovery kasası oluşturma</span><span class="sxs-lookup"><span data-stu-id="75f47-160">Step 2: Create a Site Recovery vault</span></span>
<span data-ttu-id="75f47-161">PowerShell, belirli bilgilerinizle hello "< >" Merhaba öğeleri değiştirin ve bu komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="75f47-161">In PowerShell, replace hello elements within hello "< >" with your specific information, and run these commands:</span></span>

```

$VaultName = "<testvault123>"
$VaultGeo  = "<Southeast Asia>"
$OutputPathForSettingsFile = "<c:\>"

```


```
New-AzureSiteRecoveryVault -Location $VaultGeo -Name $VaultName;
$vault = Get-AzureSiteRecoveryVault -Name $VaultName;

```

## <a name="step-3-generate-a-vault-registration-key"></a><span data-ttu-id="75f47-162">3. adım: kasa kayıt anahtarı oluşturma</span><span class="sxs-lookup"><span data-stu-id="75f47-162">Step 3: Generate a vault registration key</span></span>
<span data-ttu-id="75f47-163">Merhaba kasada bir kayıt anahtarı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="75f47-163">Generate a registration key in hello vault.</span></span> <span data-ttu-id="75f47-164">Hello Azure Site Recovery Sağlayıcısı'nı indirin ve hello VMM sunucusuna yükledikten sonra bu anahtar tooregister hello VMM sunucusu hello kasasına kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="75f47-164">After you download hello Azure Site Recovery Provider and install it on hello VMM server, you'll use this key tooregister hello VMM server in hello vault.</span></span>

1. <span data-ttu-id="75f47-165">Merhaba kasası ayar dosyasını alın ve hello bağlamını ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="75f47-165">Get hello vault setting file and set hello context:</span></span>

   ```

   $VaultName = "<testvault123>"
   $VaultGeo  = "<Southeast Asia>"
   $OutputPathForSettingsFile = "<c:\>"

   $VaultSetingsFile = Get-AzureSiteRecoveryVaultSettingsFile -Location $VaultGeo -Name $VaultName -Path $OutputPathForSettingsFile;

   ```
2. <span data-ttu-id="75f47-166">Merhaba aşağıdaki komutları çalıştırarak Hello kasası bağlamını ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="75f47-166">Set hello vault context by running hello following commands:</span></span>

   ```

   $VaultSettingFilePath = $vaultSetingsFile.FilePath
   $VaultContext = Import-AzureSiteRecoveryVaultSettingsFile -Path $VaultSettingFilePath -ErrorAction Stop

   ```

## <a name="step-4-install-hello-azure-site-recovery-provider"></a><span data-ttu-id="75f47-167">Adım 4: hello Azure Site Recovery sağlayıcısı yükleme</span><span class="sxs-lookup"><span data-stu-id="75f47-167">Step 4: Install hello Azure Site Recovery Provider</span></span>
1. <span data-ttu-id="75f47-168">Merhaba VMM makinede hello aşağıdaki komutu çalıştırarak bir dizin oluşturun:</span><span class="sxs-lookup"><span data-stu-id="75f47-168">On hello VMM machine, create a directory by running hello following command:</span></span>

   ```

   pushd C:\ASR\

   ```
2. <span data-ttu-id="75f47-169">Merhaba aşağıdaki komutu çalıştırarak indirilen hello sağlayıcısını kullanarak hello dosyaları ayıklayın</span><span class="sxs-lookup"><span data-stu-id="75f47-169">Extract hello files using hello downloaded provider by running hello following command</span></span>

   ```

   AzureSiteRecoveryProvider.exe /x:. /q

   ```
3. <span data-ttu-id="75f47-170">Merhaba Sağlayıcı komutları aşağıdaki hello kullanarak yükleyin:</span><span class="sxs-lookup"><span data-stu-id="75f47-170">Install hello provider using hello following commands:</span></span>

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

   <span data-ttu-id="75f47-171">Merhaba yükleme toofinish bekleyin.</span><span class="sxs-lookup"><span data-stu-id="75f47-171">Wait for hello installation toofinish.</span></span>
4. <span data-ttu-id="75f47-172">Hello sunucu komutu aşağıdaki hello kullanarak hello kasasına kaydedin:</span><span class="sxs-lookup"><span data-stu-id="75f47-172">Register hello server in hello vault using hello following command:</span></span>

   ```

   $BinPath = $env:SystemDrive+"\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin"
   pushd $BinPath
   $encryptionFilePath = "C:\temp\"
   .\DRConfigurator.exe /r /Credentials $VaultSettingFilePath /vmmfriendlyname $env:COMPUTERNAME /dataencryptionenabled $encryptionFilePath /startvmmservice

   ```

## <a name="step-5-create-an-azure-storage-account"></a><span data-ttu-id="75f47-173">5. adım: Azure storage hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="75f47-173">Step 5: Create an Azure storage account</span></span>
<span data-ttu-id="75f47-174">Bir Azure depolama hesabınız yoksa, hello aşağıdaki komutu çalıştırarak bir coğrafi çoğaltmanın etkinleştirilmiş hesabı oluşturun:</span><span class="sxs-lookup"><span data-stu-id="75f47-174">If you don't have an Azure storage account, create a geo-replication enabled account by running hello following command:</span></span>

```

$StorageAccountName = "teststorageacc1"
$StorageAccountGeo  = "Southeast Asia"

New-AzureStorageAccount -StorageAccountName $StorageAccountName -Label $StorageAccountName -Location $StorageAccountGeo;

```

<span data-ttu-id="75f47-175">Merhaba depolama hesabı olması gerektiğini unutmayın hello hello Azure Site Recovery hizmeti ile aynı bölgeye ve ilişkilendirilmesi hello aynı abonelik.</span><span class="sxs-lookup"><span data-stu-id="75f47-175">Note that hello storage account must be in hello same region as hello Azure Site Recovery service, and be associated with hello same subscription.</span></span>

## <a name="step-6-install-hello-azure-recovery-services-agent"></a><span data-ttu-id="75f47-176">6. adım: hello Azure kurtarma Hizmetleri Aracısı yükleme</span><span class="sxs-lookup"><span data-stu-id="75f47-176">Step 6: Install hello Azure Recovery Services Agent</span></span>
<span data-ttu-id="75f47-177">Hello Azure portal hello VMM bulutlarında yer alan her Hyper-V ana bilgisayar sunucusunda yükleme hello Azure kurtarma Hizmetleri Aracısı'ndan tooprotect istiyor.</span><span class="sxs-lookup"><span data-stu-id="75f47-177">From hello Azure portal, install hello Azure Recovery Services agent on each Hyper-V host server located in hello VMM clouds you want tooprotect.</span></span>

<span data-ttu-id="75f47-178">Tüm VMM konaklarda komutu aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="75f47-178">Run hello following command on all VMM hosts:</span></span>

```

marsagentinstaller.exe /q /nu

```


## <a name="step-7-configure-cloud-protection-settings"></a><span data-ttu-id="75f47-179">7. adım: Bulut yapılandırma koruma ayarları</span><span class="sxs-lookup"><span data-stu-id="75f47-179">Step 7: Configure cloud protection settings</span></span>
1. <span data-ttu-id="75f47-180">Bulut koruma profili tooAzure hello aşağıdaki komutu çalıştırarak oluşturun:</span><span class="sxs-lookup"><span data-stu-id="75f47-180">Create a cloud protection profile tooAzure by running hello following command:</span></span>

   ```

   $ReplicationFrequencyInSeconds = "300";
   $ProfileResult = New-AzureSiteRecoveryProtectionProfileObject -ReplicationProvider HyperVReplica -RecoveryAzureSubscription $AzureSubscriptionName -RecoveryAzureStorageAccount $StorageAccountName -ReplicationFrequencyInSeconds     $ReplicationFrequencyInSeconds;

   ```
2. <span data-ttu-id="75f47-181">Koruma kapsayıcısı hello aşağıdaki komutları çalıştırarak alın:</span><span class="sxs-lookup"><span data-stu-id="75f47-181">Get a protection container by running hello following commands:</span></span>

   ```

   $PrimaryCloud = "testcloud"
   $protectionContainer = Get-AzureSiteRecoveryProtectionContainer -Name $PrimaryCloud;

   ```
3. <span data-ttu-id="75f47-182">Merhaba ilişkilendirme hello koruma kapsayıcısı ile Merhaba bulut Başlat:</span><span class="sxs-lookup"><span data-stu-id="75f47-182">Start hello association of hello protection container with hello cloud:</span></span>

   ```

   $associationJob = Start-AzureSiteRecoveryProtectionProfileAssociationJob -ProtectionProfile $profileResult -PrimaryProtectionContainer $protectionContainer;        

   ```
4. <span data-ttu-id="75f47-183">Merhaba işi tamamlandıktan sonra hello aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="75f47-183">After hello job has finished, run hello following command:</span></span>

        $job = Get-AzureSiteRecoveryJob -Id $associationJob.JobId;
        if($job -eq $null -or $job.StateDescription -ne "Completed")
        {
        $isJobLeftForProcessing = $true;
        }


1. <span data-ttu-id="75f47-184">Hello iş işlemeyi bitirdikten sonra hello aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="75f47-184">After hello job has finished processing, run hello following command:</span></span>

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



<span data-ttu-id="75f47-185">Merhaba işleminin toocheck hello tamamlanması izleyin hello adımlarda [etkinliğini izleme](#monitor).</span><span class="sxs-lookup"><span data-stu-id="75f47-185">toocheck hello completion of hello operation, follow hello steps in [Monitor Activity](#monitor).</span></span>

## <a name="step-8-configure-network-mapping"></a><span data-ttu-id="75f47-186">8. adım: ağ eşlemesini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="75f47-186">Step 8: Configure network mapping</span></span>
<span data-ttu-id="75f47-187">Başlamadan önce Ağ eşlemesi hello kaynak VMM sunucusundaki sanal makineleri bağlı tooa VM ağı olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="75f47-187">Before you begin network mapping verify that virtual machines on hello source VMM server are connected tooa VM network.</span></span> <span data-ttu-id="75f47-188">Ayrıca, bir veya daha fazla Azure sanal ağı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="75f47-188">In addition, create one or more Azure virtual networks.</span></span> <span data-ttu-id="75f47-189">Birden fazla VM ağı eşlenen tooa tek Azure ağ olabileceğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="75f47-189">Note that multiple VM networks can be mapped tooa single Azure network.</span></span>

<span data-ttu-id="75f47-190">Hello hedef ağın birden çok alt ağı varsa ve bu alt ağlardan biri olan hello adıyla aynı alt ağda hangi hello kaynak sanal makinenin bulunduğu sonra hello çoğaltma sanal makinesi yük devretme sonrasında bağlı toothat hedef alt olacaktır unutmayın.</span><span class="sxs-lookup"><span data-stu-id="75f47-190">Note that if hello target network has multiple subnets and one of those subnets has hello same name as subnet on which hello source virtual machine is located, then hello replica virtual machine will be connected toothat target subnet after failover.</span></span> <span data-ttu-id="75f47-191">Eşleşen bir ada sahip bir hedef alt ağa değilse hello sanal makineye bağlı toohello hello ağdaki ilk alt ağ olacaktır.</span><span class="sxs-lookup"><span data-stu-id="75f47-191">If there is not a target subnet with a matching name, hello virtual machine will be connected toohello first subnet in hello network.</span></span>

<span data-ttu-id="75f47-192">Merhaba ilk komut sunucuları için geçerli Azure Site Recovery kasası hello alır.</span><span class="sxs-lookup"><span data-stu-id="75f47-192">hello first command gets servers for hello current Azure Site Recovery vault.</span></span> <span data-ttu-id="75f47-193">Merhaba komut hello Microsoft Azure Site Recovery sunucuları hello $Servers dizi değişkeninde depolar.</span><span class="sxs-lookup"><span data-stu-id="75f47-193">hello command stores hello Microsoft Azure Site Recovery servers in hello $Servers array variable.</span></span>

    $Servers = Get-AzureSiteRecoveryServer


<span data-ttu-id="75f47-194">Merhaba ikinci komut hello site kurtarma ağ hello ilk sunucu için hello $Servers dizisini alır.</span><span class="sxs-lookup"><span data-stu-id="75f47-194">hello second command gets hello site recovery network for hello first server in hello $Servers array.</span></span> <span data-ttu-id="75f47-195">Merhaba komut hello ağları hello $Networks değişkeninde depolar.</span><span class="sxs-lookup"><span data-stu-id="75f47-195">hello command stores hello networks in hello $Networks variable.</span></span>

    $Networks = Get-AzureSiteRecoveryNetwork -Server $Servers[0]

<span data-ttu-id="75f47-196">Merhaba üçüncü komut hello Get-AzureSubscription cmdlet'ini kullanarak, Azure aboneliklerinize alır ve ardından bu değer hello $Subscriptions değişkeninde depolar.</span><span class="sxs-lookup"><span data-stu-id="75f47-196">hello third command gets your Azure subscriptions by using hello Get-AzureSubscription cmdlet, and then stores that value in hello $Subscriptions variable.</span></span>

    $Subscriptions = Get-AzureSubscription



<span data-ttu-id="75f47-197">Merhaba dördüncü komut hello $AzureVmNetworks değişkeninde hello Get-AzureVNetSite cmdlet'i ve bu değer'ı kullanarak Azure sanal ağlar alır.</span><span class="sxs-lookup"><span data-stu-id="75f47-197">hello fourth command gets Azure virtual networks by using hello Get-AzureVNetSite cmdlet, and then that value in hello $AzureVmNetworks variable.</span></span>

    $AzureVmNetworks = Get-AzureVNetSite



<span data-ttu-id="75f47-198">Merhaba son cmdlet'i hello birincil ağ ve hello Azure sanal makine ağı arasında bir eşleme oluşturur.</span><span class="sxs-lookup"><span data-stu-id="75f47-198">hello final cmdlet creates a mapping between hello primary network and hello Azure virtual machine network.</span></span> <span data-ttu-id="75f47-199">Merhaba cmdlet hello birincil ağ hello ilk öğesi $Networks belirtir.</span><span class="sxs-lookup"><span data-stu-id="75f47-199">hello cmdlet specifies hello primary network as hello first element of $Networks.</span></span> <span data-ttu-id="75f47-200">Merhaba cmdlet kimliğini kullanarak bir sanal makine ağına hello ilk öğesi $AzureVmNetworks belirtir</span><span class="sxs-lookup"><span data-stu-id="75f47-200">hello cmdlet specifies a virtual machine network as hello first element of $AzureVmNetworks by using its ID.</span></span> <span data-ttu-id="75f47-201">Azure abonelik kimliğinizi Hello komut içerir</span><span class="sxs-lookup"><span data-stu-id="75f47-201">hello command includes your Azure subscription ID.</span></span>

    New-AzureSiteRecoveryNetworkMapping -PrimaryNetwork $Networks[0] -AzureSubscriptionId $Subscriptions[0].SubscriptionId -AzureVMNetworkId $AzureVmNetworks[0].Id


## <a name="step-9-enable-protection-for-virtual-machines"></a><span data-ttu-id="75f47-202">9. adım: sanal makineler için korumayı etkinleştir</span><span class="sxs-lookup"><span data-stu-id="75f47-202">Step 9: Enable protection for virtual machines</span></span>
<span data-ttu-id="75f47-203">Sunucular, Bulutlar ve ağlar doğru şekilde yapılandırıldıktan sonra hello bulutta sanal makineler için korumayı etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="75f47-203">After servers, clouds, and networks are configured correctly, you can enable protection for virtual machines in hello cloud.</span></span> <span data-ttu-id="75f47-204">Merhaba aşağıdakileri göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="75f47-204">Note hello following:</span></span>

<span data-ttu-id="75f47-205">Sanal makineler karşılamalıdır [Azure sanal makine önkoşulları](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span><span class="sxs-lookup"><span data-stu-id="75f47-205">Virtual machines must meet [Azure virtual machine prerequisites](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>

<span data-ttu-id="75f47-206">tooenable koruma hello işletim sistemi ve işletim sistemi disk özellikleri hello sanal makine için ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="75f47-206">tooenable protection hello operating system and operating system disk properties must be set for hello virtual machine.</span></span> <span data-ttu-id="75f47-207">Bir sanal makine şablonu kullanarak VMM'de bir sanal makine oluşturduğunuzda hello özelliğini ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="75f47-207">When you create a virtual machine in VMM using a virtual machine template you can set hello property.</span></span> <span data-ttu-id="75f47-208">Bu özellikleri mevcut sanal makineler üzerinde hello ayarlayabilirsiniz **genel** ve **donanım yapılandırması** sekmeleri hello sanal makine özellikleri.</span><span class="sxs-lookup"><span data-stu-id="75f47-208">You can also set these properties for existing virtual machines on hello **General** and **Hardware Configuration** tabs of hello virtual machine properties.</span></span> <span data-ttu-id="75f47-209">Bu özellikleri VMM'de ayarlamazsanız mümkün tooconfigure olacak hello Azure Site Recovery portalında bunları.</span><span class="sxs-lookup"><span data-stu-id="75f47-209">If you don't set these properties in VMM you'll be able tooconfigure them in hello Azure Site Recovery portal.</span></span>

1. <span data-ttu-id="75f47-210">tooenable koruma, çalıştırma hello aşağıdaki tooget hello koruma kapsayıcısı komutu:</span><span class="sxs-lookup"><span data-stu-id="75f47-210">tooenable protection, run hello following command tooget hello protection container:</span></span>

     <span data-ttu-id="75f47-211">$ProtectionContainer = get-AzureSiteRecoveryProtectionContainer-ad $CloudName</span><span class="sxs-lookup"><span data-stu-id="75f47-211">$ProtectionContainer = Get-AzureSiteRecoveryProtectionContainer -Name $CloudName</span></span>
2. <span data-ttu-id="75f47-212">Merhaba koruma varlık (VM) hello aşağıdaki komutu çalıştırarak alın:</span><span class="sxs-lookup"><span data-stu-id="75f47-212">Get hello protection entity (VM) by running hello following command:</span></span>

        $protectionEntity = Get-AzureSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer



1. <span data-ttu-id="75f47-213">Merhaba DR hello VM için komutu aşağıdaki hello çalıştırarak etkinleştirin:</span><span class="sxs-lookup"><span data-stu-id="75f47-213">Enable hello DR for hello VM by running hello following command:</span></span>

        $jobResult = Set-AzureSiteRecoveryProtectionEntity -ProtectionEntity $protectionEntity     -Protection Enable -Force



## <a name="test-your-deployment"></a><span data-ttu-id="75f47-214">Dağıtımınızı test edin</span><span class="sxs-lookup"><span data-stu-id="75f47-214">Test your deployment</span></span>
<span data-ttu-id="75f47-215">tootest bir yük devretme sınaması için tek bir sanal makine çalıştırmak veya birden çok sanal makine içeren ve bir yük devretme testi hello için bir kurtarma planı oluşturun, dağıtımınızı planlayın.</span><span class="sxs-lookup"><span data-stu-id="75f47-215">tootest your deployment you can run a test failover for a single virtual machine, or create a recovery plan consisting of multiple virtual machines and run a test failover for hello plan.</span></span> <span data-ttu-id="75f47-216">Yük devretme testi, yük devretme işleminizi ve kurtarma mekanizmanızı yalıtılmış bir ortamda benzetimli olarak gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="75f47-216">Test failover simulates your failover and recovery mechanism in an isolated network.</span></span> <span data-ttu-id="75f47-217">Şunlara dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="75f47-217">Note that:</span></span>

* <span data-ttu-id="75f47-218">Hello yük devretme sonrasında Uzak Masaüstü'nü kullanarak azure'daki tooconnect toohello sanal makine istiyorsanız, Uzak Masaüstü Bağlantısı hello test yük devretmesi çalıştırmadan önce hello sanal makinesinde etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="75f47-218">If you want tooconnect toohello virtual machine in Azure using Remote Desktop after hello failover, enable Remote Desktop Connection on hello virtual machine before you run hello test failover.</span></span>
* <span data-ttu-id="75f47-219">Yük devretme sonrasında, Uzak Masaüstü kullanarak Azure'da bir ortak IP adresi tooconnect toohello sanal makine kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="75f47-219">After failover, you'll use a public IP address tooconnect toohello virtual machine in Azure using Remote Desktop.</span></span> <span data-ttu-id="75f47-220">Bu toodo istiyorsanız, bağlanan tooa sanal genel bir adres kullanarak makineden engelleyecek etki alanı ilkelerine sahip olmadığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="75f47-220">If you want toodo this, ensure you don't have any domain policies that prevent you from connecting tooa virtual machine using a public address.</span></span>

<span data-ttu-id="75f47-221">Merhaba işleminin toocheck hello tamamlanması izleyin hello adımlarda [etkinliğini izleme](#monitor).</span><span class="sxs-lookup"><span data-stu-id="75f47-221">toocheck hello completion of hello operation, follow hello steps in [Monitor Activity](#monitor).</span></span>

### <a name="create-a-recovery-plan"></a><span data-ttu-id="75f47-222">Kurtarma planı oluşturma</span><span class="sxs-lookup"><span data-stu-id="75f47-222">Create a recovery plan</span></span>
1. <span data-ttu-id="75f47-223">Merhaba veri aşağıdaki kullanarak kurtarma planınız için bir şablon olarak bir .xml dosyası oluşturun ve sonra "C:\RPTemplatePath.xml" kaydedin.</span><span class="sxs-lookup"><span data-stu-id="75f47-223">Create an .xml file as a template for your recovery plan using hello data below, and then save it as "C:\RPTemplatePath.xml".</span></span>
2. <span data-ttu-id="75f47-224">Merhaba RecoveryPlan düğüm kimliği, ad, PrimaryServerId ve SecondaryServerId değiştirin.</span><span class="sxs-lookup"><span data-stu-id="75f47-224">Change hello RecoveryPlan node Id, Name, PrimaryServerId, and SecondaryServerId.</span></span>
3. <span data-ttu-id="75f47-225">Merhaba ProtectionEntity düğümü PrimaryProtectionEntityId (vmm'den vmıd) değiştirin.</span><span class="sxs-lookup"><span data-stu-id="75f47-225">Change hello ProtectionEntity node PrimaryProtectionEntityId (vmid from VMM).</span></span>
4. <span data-ttu-id="75f47-226">Daha fazla VM'ler daha fazla ProtectionEntity düğüm ekleyerek ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="75f47-226">You can add more VMs by adding more ProtectionEntity nodes.</span></span>

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



1. <span data-ttu-id="75f47-227">Merhaba veri hello şablonunda doldurun:</span><span class="sxs-lookup"><span data-stu-id="75f47-227">Fill in hello data in hello template:</span></span>

        $TemplatePath = "C:\RPTemplatePath.xml";



1. <span data-ttu-id="75f47-228">Merhaba RecoveryPlan oluşturun:</span><span class="sxs-lookup"><span data-stu-id="75f47-228">Create hello RecoveryPlan:</span></span>

        $RPCreationJob = New-AzureSiteRecoveryRecoveryPlan -File $TemplatePath -WaitForCompletion;

### <a name="run-a-test-failover"></a><span data-ttu-id="75f47-229">Yük devretme testi çalıştırma</span><span class="sxs-lookup"><span data-stu-id="75f47-229">Run a test failover</span></span>
1. <span data-ttu-id="75f47-230">Merhaba aşağıdaki komutu çalıştırarak Hello RecoveryPlan nesnesini alın:</span><span class="sxs-lookup"><span data-stu-id="75f47-230">Get hello RecoveryPlan object by running hello following command:</span></span>

     <span data-ttu-id="75f47-231">$RPObject = get-AzureSiteRecoveryRecoveryPlan-ad $RPName;</span><span class="sxs-lookup"><span data-stu-id="75f47-231">$RPObject = Get-AzureSiteRecoveryRecoveryPlan -Name $RPName;</span></span>
2. <span data-ttu-id="75f47-232">Merhaba aşağıdaki komutu çalıştırarak Hello test yük devretme başlatın:</span><span class="sxs-lookup"><span data-stu-id="75f47-232">Start hello test failover by running hello following command:</span></span>

        $jobIDResult = Start-AzureSiteRecoveryTestFailoverJob -RecoveryPlan $RPObject -Direction PrimaryToRecovery;


## <span data-ttu-id="75f47-233"><a name=monitor></a>Etkinliğini izleme</span><span class="sxs-lookup"><span data-stu-id="75f47-233"><a name=monitor></a> Monitor Activity</span></span>
<span data-ttu-id="75f47-234">Aşağıdaki komutları toomonitor hello etkinlik hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="75f47-234">Use hello following commands toomonitor hello activity.</span></span> <span data-ttu-id="75f47-235">Merhaba işleme toofinish işleri arasında toowait gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="75f47-235">Note that you have toowait in between jobs for hello processing toofinish.</span></span>

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



## <a name="next-steps"></a><span data-ttu-id="75f47-236">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="75f47-236">Next steps</span></span>
<span data-ttu-id="75f47-237">[Daha fazla bilgi](/powershell/azure/overview) Azure Site Recovery PowerShell cmdlet'leri hakkında.</span><span class="sxs-lookup"><span data-stu-id="75f47-237">[Read more](/powershell/azure/overview) about Azure Site Recovery PowerShell cmdlets.</span></span> <span data-ttu-id="75f47-238"></a>.</span><span class="sxs-lookup"><span data-stu-id="75f47-238"></a>.</span></span>
