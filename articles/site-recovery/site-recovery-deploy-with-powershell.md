---
title: "PowerShell ile klasik portalda Hyper-V Vm'lerini Azure'a çoğaltma | Microsoft Docs"
description: "Klasik portalda Site Recovery ve PowerShell kullanarak VMM bulutlarındaki Hyper-V sanal makinelerini çoğaltma otomatikleştirme"
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
ms.openlocfilehash: 581daaaa5cc0cf8be782f834c6bdb3f27ee413fb
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="replicate-hyper-v-vms-to-azure-with-powershell-in-the-classic-portal"></a><span data-ttu-id="c0e20-103">Klasik portalda Azure PowerShell ile Hyper-V Vm'lerini çoğaltma</span><span class="sxs-lookup"><span data-stu-id="c0e20-103">Replicate Hyper-V VMs to Azure with PowerShell in the classic portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c0e20-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="c0e20-104">Azure Portal</span></span>](site-recovery-vmm-to-azure.md)
> * [<span data-ttu-id="c0e20-105">PowerShell - Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c0e20-105">PowerShell - Resource Manager</span></span>](site-recovery-vmm-to-azure-powershell-resource-manager.md)
> * [<span data-ttu-id="c0e20-106">Klasik Portal</span><span class="sxs-lookup"><span data-stu-id="c0e20-106">Classic Portal</span></span>](site-recovery-vmm-to-azure-classic.md)
> * [<span data-ttu-id="c0e20-107">PowerShell - Klasik</span><span class="sxs-lookup"><span data-stu-id="c0e20-107">PowerShell - Classic</span></span>](site-recovery-deploy-with-powershell.md)
>
>

## <a name="overview"></a><span data-ttu-id="c0e20-108">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="c0e20-108">Overview</span></span>
<span data-ttu-id="c0e20-109">Azure Site Recovery, çoğaltma, yük devretme ve kurtarma çeşitli dağıtım senaryolarında sanal makinelerin düzenleyerek iş sürekliliği ve olağanüstü durum kurtarma (BCDR) stratejinize katkı sağlar.</span><span class="sxs-lookup"><span data-stu-id="c0e20-109">Azure Site Recovery contributes to your business continuity and disaster recovery (BCDR) strategy by orchestrating replication, failover and recovery of virtual machines in a number of deployment scenarios.</span></span> <span data-ttu-id="c0e20-110">Dağıtım tam listesi için bkz: senaryoları [Azure Site Recovery genel bakış](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c0e20-110">For a full list of deployment scenarios see the [Azure Site Recovery overview](site-recovery-overview.md).</span></span>

<span data-ttu-id="c0e20-111">Bu makalede Azure depolama alanına System Center VMM bulutlarındaki Hyper-V sanal makineleri çoğaltmak için Azure Site Recovery ayarladığınızda, yapmanız gereken ortak görevleri otomatik hale getirmek için PowerShell kullanmayı gösterir.</span><span class="sxs-lookup"><span data-stu-id="c0e20-111">This article shows you how to use PowerShell to automate common tasks you need to perform when you set up Azure Site Recovery to replicate Hyper-V virtual machines in System Center VMM clouds to Azure storage.</span></span>

<span data-ttu-id="c0e20-112">Makaleyi senaryonun önkoşulları içerir ve Site Recovery kasasını oluşturup, kaynak VMM sunucusunda Azure Site kurtarma Sağlayıcısı'nı yükleme, sunucuyu kasaya kaydetmek, bir Azure depolama hesabı ekleme hakkında yükleme Azure kurtarma gösterir Hizmetleri aracısını Hyper-V konak sunucuları üzerindeki tüm korumalı sanal makineler için uygulanır ve bu sanal makineler için korumayı etkinleştir VMM Bulutları için koruma ayarlarını yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="c0e20-112">The article includes prerequisites for the scenario, and shows you how to set up a Site Recovery vault, install the Azure Site Recovery Provider on the source VMM server, register the server in the vault, add an Azure storage account, install the Azure Recovery Services agent on Hyper-V host servers, configure protection settings for VMM clouds that will be applied to all protected virtual machines, and then enable protection for those virtual machines.</span></span> <span data-ttu-id="c0e20-113">Her şeyin istendiği gibi çalıştığından emin olmak için yük devretmeyi test ederek işlemi sonlandırın.</span><span class="sxs-lookup"><span data-stu-id="c0e20-113">Finish up by testing the failover to make sure everything's working as expected.</span></span>

<span data-ttu-id="c0e20-114">Bu senaryoyu oluşturan ayarlama sorunlarını alıyorsanız, üzerinde sorularınızı [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="c0e20-114">If you run into problems setting up this scenario, post your questions on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

> [!NOTE]
> <span data-ttu-id="c0e20-115">Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="c0e20-115">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="c0e20-116">Bu makalede, Klasik dağıtım modeli kullanarak yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="c0e20-116">This article covers using the Classic deployment model.</span></span>
>
>

## <a name="before-you-start"></a><span data-ttu-id="c0e20-117">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="c0e20-117">Before you start</span></span>
<span data-ttu-id="c0e20-118">Bu Önkoşullar sağladığınızdan emin olun:</span><span class="sxs-lookup"><span data-stu-id="c0e20-118">Make sure you have these prerequisites in place:</span></span>

### <a name="azure-prerequisites"></a><span data-ttu-id="c0e20-119">Azure önkoşulları</span><span class="sxs-lookup"><span data-stu-id="c0e20-119">Azure prerequisites</span></span>
* <span data-ttu-id="c0e20-120">Bir [Microsoft Azure](https://azure.microsoft.com/) hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="c0e20-120">You'll need a [Microsoft Azure](https://azure.microsoft.com/) account.</span></span> <span data-ttu-id="c0e20-121">[Ücretsiz deneme sürümüyle](https://azure.microsoft.com/pricing/free-trial/) başlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c0e20-121">You can start with a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="c0e20-122">Çoğaltılan verileri depolamak için bir Azure depolama hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="c0e20-122">You'll need an Azure storage account to store replicated data.</span></span> <span data-ttu-id="c0e20-123">Hesap coğrafi çoğaltmanın etkinleştirilmiş olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="c0e20-123">The account needs geo-replication enabled.</span></span> <span data-ttu-id="c0e20-124">Bu Azure Site Recovery kasasıyla aynı bölgede olması ve aynı abonelikle ilişkilendirilmiş olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="c0e20-124">It should be in the same region as the Azure Site Recovery vault and be associated with the same subscription.</span></span> <span data-ttu-id="c0e20-125">[Azure storage hakkında daha fazla bilgi](../storage/common/storage-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c0e20-125">[Learn more about Azure storage](../storage/common/storage-introduction.md).</span></span>
* <span data-ttu-id="c0e20-126">Korumak istediğiniz sanal makineleri ile uyumlu olduğundan emin olmak gerekir [Azure sanal makine önkoşulları](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span><span class="sxs-lookup"><span data-stu-id="c0e20-126">You'll need to make sure that virtual machines you want to protect comply with [Azure virtual machine prerequisites](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>

### <a name="vmm-prerequisites"></a><span data-ttu-id="c0e20-127">VMM önkoşulları</span><span class="sxs-lookup"><span data-stu-id="c0e20-127">VMM prerequisites</span></span>
* <span data-ttu-id="c0e20-128">System Center 2012 R2 üzerinde çalışan VMM sunucusu gerekir.</span><span class="sxs-lookup"><span data-stu-id="c0e20-128">You'll need  VMM server running on System Center 2012 R2.</span></span>
* <span data-ttu-id="c0e20-129">Korumak istediğiniz VMM sunucusunda en az bir bulut gerekir.</span><span class="sxs-lookup"><span data-stu-id="c0e20-129">You'll need at least one cloud on the VMM server you want to protect.</span></span> <span data-ttu-id="c0e20-130">Bulut içermelidir:</span><span class="sxs-lookup"><span data-stu-id="c0e20-130">The cloud should contain:</span></span>
  * <span data-ttu-id="c0e20-131">Bir veya birden çok VMM ana bilgisayar grubu.</span><span class="sxs-lookup"><span data-stu-id="c0e20-131">One or more VMM host groups.</span></span>
  * <span data-ttu-id="c0e20-132">Bir veya daha fazla Hyper-V ana bilgisayar sunucuları veya kümeleri her konak grubundaki.</span><span class="sxs-lookup"><span data-stu-id="c0e20-132">One or more Hyper-V host servers or clusters in each host group .</span></span>
  * <span data-ttu-id="c0e20-133">Kaynak Hyper-V sunucu üzerindeki bir veya daha fazla sanal makineler.</span><span class="sxs-lookup"><span data-stu-id="c0e20-133">One or more virtual machines on the source Hyper-V server.</span></span>

### <a name="hyper-v-prerequisites"></a><span data-ttu-id="c0e20-134">Hyper-V önkoşulları</span><span class="sxs-lookup"><span data-stu-id="c0e20-134">Hyper-V prerequisites</span></span>
* <span data-ttu-id="c0e20-135">Hyper-V ana bilgisayar sunucuları en az çalıştırmalıdır **Windows Server 2012** Hyper-V rolüne sahip veya **Microsoft Hyper-V Server 2012** ve en son güncelleştirmelerin yüklü olması.</span><span class="sxs-lookup"><span data-stu-id="c0e20-135">The host Hyper-V servers must be running at least **Windows Server 2012** with Hyper-V role or **Microsoft Hyper-V Server 2012** and have the latest updates installed.</span></span>
* <span data-ttu-id="c0e20-136">Hyper-V'yi bir kümede çalıştırıyorsanız statik IP adresi temelli bir kümeye sahip olmanız durumunda küme aracısının otomatik olarak oluşturulamayacağını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="c0e20-136">If you're running Hyper-V in a cluster note that cluster broker isn't created automatically if you have a static IP address-based cluster.</span></span> <span data-ttu-id="c0e20-137">Küme aracısını sizin yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="c0e20-137">You'll need to configure the cluster broker manually.</span></span> <span data-ttu-id="c0e20-138">Bu, Sunucu Yöneticisi'nde yapmak için > Yük Devretme Kümesi Yöneticisi ' ni kümeye bağlanın, tıklatın **rolü Yapılandır** seçip **Hyper-V çoğaltma aracısı** içinde **rolü Seç** Yüksek Kullanılabilirlik Sihirbazı'nın ekranı.</span><span class="sxs-lookup"><span data-stu-id="c0e20-138">To do this, in Server Manager > Failover Cluster Manager, connect to the cluster, click **Configure Role** and select **Hyper-V Replica Broker** in the **Select Role** screen of the High Availability wizard.</span></span>
* <span data-ttu-id="c0e20-139">Herhangi bir Hyper-V konak sunucusu veya küme koruma yönetmek istediğiniz bir VMM bulutunda eklenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="c0e20-139">Any Hyper-V host server or cluster for which you want to manage protection must be included in a VMM cloud.</span></span>

### <a name="network-mapping-prerequisites"></a><span data-ttu-id="c0e20-140">Ağ eşlemesi önkoşulları</span><span class="sxs-lookup"><span data-stu-id="c0e20-140">Network mapping prerequisites</span></span>
<span data-ttu-id="c0e20-141">Azure'da sanal makineleri koruduğunuzda, ağ eşlemesi kaynak VMM sunucusundaki VM ağlarını hedef Azure ağları ile eşleyerek şu işlemlere olanak sağlar:</span><span class="sxs-lookup"><span data-stu-id="c0e20-141">When you protect virtual machines in Azure network mapping maps between VM networks on the source VMM server and target Azure networks to enable the following:</span></span>

* <span data-ttu-id="c0e20-142">Aynı ağda yük devri tüm makineler birbirine, hangi kurtarma planında yer aldıklarına bulundukları bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="c0e20-142">All machines which fail over on the same network can connect to each other, irrespective of which recovery plan they are in.</span></span>
* <span data-ttu-id="c0e20-143">Bir ağ geçidi hedef Azure ağında ayarlanırsa sanal makineler diğer şirket içi sanal makinelere bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="c0e20-143">If a network gateway is setup on the target Azure network, virtual machines can connect to other on-premises virtual machines.</span></span>
* <span data-ttu-id="c0e20-144">Ağ eşlemesini yapılandırmazsanız yalnızca aynı kurtarma planında yük devreden sanal makineler, Azure'a yük devretme işleminin ardından birbirleriyle bağlantı kurabilir.</span><span class="sxs-lookup"><span data-stu-id="c0e20-144">If you don’t configure network mapping only virtual machines that fail over in the same recovery plan will be able to connect to each other after failover to Azure.</span></span>

<span data-ttu-id="c0e20-145">Ağ eşlemesi dağıtmak isterseniz şunlara ihtiyaç duyarsınız:</span><span class="sxs-lookup"><span data-stu-id="c0e20-145">If you want to deploy network mapping you'll need the following:</span></span>

* <span data-ttu-id="c0e20-146">Kaynak VMM sunucusunda korumak istediğinizde sanal makinelerin bir VM ağına bağlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="c0e20-146">The virtual machines you want to protect on the source VMM server should be connected to a VM network.</span></span> <span data-ttu-id="c0e20-147">Bu ağın, bulutla ilişkilendirilen mantıksal bir ağ ile bağlantılı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="c0e20-147">That network should be linked to a logical network that is associated with the cloud.</span></span>
* <span data-ttu-id="c0e20-148">Yük devretme işleminin ardından çoğaltılan sanal makinelerin bağlanabileceği bir Azure ağı.</span><span class="sxs-lookup"><span data-stu-id="c0e20-148">An Azure network to which replicated virtual machines can connect after failover.</span></span> <span data-ttu-id="c0e20-149">Bu ağı yük devretme sırasında seçersiniz.</span><span class="sxs-lookup"><span data-stu-id="c0e20-149">You'll select this network at the time of failover.</span></span> <span data-ttu-id="c0e20-150">Ağın Azure Site Recovery aboneliğinizle aynı bölgede olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="c0e20-150">The network should be in the same region as your Azure Site Recovery subscription.</span></span>

### <a name="powershell-prerequisites"></a><span data-ttu-id="c0e20-151">PowerShell önkoşulları</span><span class="sxs-lookup"><span data-stu-id="c0e20-151">PowerShell prerequisites</span></span>
<span data-ttu-id="c0e20-152">Azure PowerShell davranmaya hazır olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="c0e20-152">Make sure you have Azure PowerShell ready to go.</span></span> <span data-ttu-id="c0e20-153">PowerShell zaten kullanıyorsanız, 0.8.10 sürümüne yükseltme veya üstü gerekir.</span><span class="sxs-lookup"><span data-stu-id="c0e20-153">If you are already using PowerShell, you'll need to upgrade to version 0.8.10 or later.</span></span> <span data-ttu-id="c0e20-154">PowerShell ayarlama hakkında daha fazla bilgi için bkz: [Azure PowerShell'i yükleme ve yapılandırma nasıl](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="c0e20-154">For information about setting up PowerShell, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="c0e20-155">Ayarlama ve PowerShell yapılandırılmış sonra tüm kullanılabilir cmdlet'leri hizmeti görüntüleyebilirsiniz [burada](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c0e20-155">Once you have set up and configured PowerShell, you can view all of the available cmdlets for the service [here](/powershell/azure/overview).</span></span>

<span data-ttu-id="c0e20-156">Parametre değerleri, girişleri ve çıkışları genellikle Azure PowerShell'de işlenme gibi cmdlet'leri kullanın yardımcı olabilecek ipuçları hakkında bilgi edinmek için bkz [Azure cmdlet'leri ile çalışmaya başlama](/powershell/azure/get-started-azureps).</span><span class="sxs-lookup"><span data-stu-id="c0e20-156">To learn about tips that can help you use the cmdlets, such as how parameter values, inputs, and outputs are typically handled in Azure PowerShell, see [Get Started with Azure Cmdlets](/powershell/azure/get-started-azureps).</span></span>

## <a name="step-1-set-the-subscription"></a><span data-ttu-id="c0e20-157">1. adım: Abonelik ayarlama</span><span class="sxs-lookup"><span data-stu-id="c0e20-157">Step 1: Set the subscription</span></span>
<span data-ttu-id="c0e20-158">PowerShell'de bu cmdlet'leri çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="c0e20-158">In PowerShell, run these cmdlets:</span></span>

```
$UserName = "<user@live.com>"
$Password = "<password>"
$AzureSubscriptionName = "prod_sub1"

$SecurePassword = ConvertTo-SecureString -AsPlainText $Password -Force
$Cred = New-Object System.Management.Automation.PSCredential -ArgumentList $UserName, $securePassword
Add-AzureAccount -Credential $Cred;
$AzureSubscription = Select-AzureSubscription -SubscriptionName $AzureSubscriptionName

```

<span data-ttu-id="c0e20-159">"< >" İçinde öğelerin size özgü bilgileri ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="c0e20-159">Replace the elements within the "< >" with your specific information.</span></span>

## <a name="step-2-create-a-site-recovery-vault"></a><span data-ttu-id="c0e20-160">2. adım: Site Recovery kasası oluşturma</span><span class="sxs-lookup"><span data-stu-id="c0e20-160">Step 2: Create a Site Recovery vault</span></span>
<span data-ttu-id="c0e20-161">PowerShell, "< >" içinde öğelerin belirli bilgilerinizle değiştirin ve bu komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="c0e20-161">In PowerShell, replace the elements within the "< >" with your specific information, and run these commands:</span></span>

```

$VaultName = "<testvault123>"
$VaultGeo  = "<Southeast Asia>"
$OutputPathForSettingsFile = "<c:\>"

```


```
New-AzureSiteRecoveryVault -Location $VaultGeo -Name $VaultName;
$vault = Get-AzureSiteRecoveryVault -Name $VaultName;

```

## <a name="step-3-generate-a-vault-registration-key"></a><span data-ttu-id="c0e20-162">3. adım: kasa kayıt anahtarı oluşturma</span><span class="sxs-lookup"><span data-stu-id="c0e20-162">Step 3: Generate a vault registration key</span></span>
<span data-ttu-id="c0e20-163">Kasada bir kayıt anahtarı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c0e20-163">Generate a registration key in the vault.</span></span> <span data-ttu-id="c0e20-164">Azure Site Recovery Sağlayıcısı'nı indirdikten sonra VMM sunucusuna yükleyin, oluşturduğunuz anahtarı kasadaki VMM sunucusuna kaydolmak için kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="c0e20-164">After you download the Azure Site Recovery Provider and install it on the VMM server, you'll use this key to register the VMM server in the vault.</span></span>

1. <span data-ttu-id="c0e20-165">Kasa ayar dosyasını alın ve bağlamını ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="c0e20-165">Get the vault setting file and set the context:</span></span>

   ```

   $VaultName = "<testvault123>"
   $VaultGeo  = "<Southeast Asia>"
   $OutputPathForSettingsFile = "<c:\>"

   $VaultSetingsFile = Get-AzureSiteRecoveryVaultSettingsFile -Location $VaultGeo -Name $VaultName -Path $OutputPathForSettingsFile;

   ```
2. <span data-ttu-id="c0e20-166">Aşağıdaki komutları çalıştırarak kasası bağlamını ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="c0e20-166">Set the vault context by running the following commands:</span></span>

   ```

   $VaultSettingFilePath = $vaultSetingsFile.FilePath
   $VaultContext = Import-AzureSiteRecoveryVaultSettingsFile -Path $VaultSettingFilePath -ErrorAction Stop

   ```

## <a name="step-4-install-the-azure-site-recovery-provider"></a><span data-ttu-id="c0e20-167">4. adım: Azure Site kurtarma Sağlayıcısı'nı yükleme</span><span class="sxs-lookup"><span data-stu-id="c0e20-167">Step 4: Install the Azure Site Recovery Provider</span></span>
1. <span data-ttu-id="c0e20-168">VMM makinesinde aşağıdaki komutu çalıştırarak bir dizin oluşturun:</span><span class="sxs-lookup"><span data-stu-id="c0e20-168">On the VMM machine, create a directory by running the following command:</span></span>

   ```

   pushd C:\ASR\

   ```
2. <span data-ttu-id="c0e20-169">Aşağıdaki komutu çalıştırarak indirilen sağlayıcısını kullanarak dosyaları ayıklayın</span><span class="sxs-lookup"><span data-stu-id="c0e20-169">Extract the files using the downloaded provider by running the following command</span></span>

   ```

   AzureSiteRecoveryProvider.exe /x:. /q

   ```
3. <span data-ttu-id="c0e20-170">Aşağıdaki komutları kullanarak sağlayıcısını yükleyin:</span><span class="sxs-lookup"><span data-stu-id="c0e20-170">Install the provider using the following commands:</span></span>

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

   <span data-ttu-id="c0e20-171">Yüklemesinin tamamlanması için bekleyin.</span><span class="sxs-lookup"><span data-stu-id="c0e20-171">Wait for the installation to finish.</span></span>
4. <span data-ttu-id="c0e20-172">Sunucu aşağıdaki komutu kullanarak kasaya kaydedin:</span><span class="sxs-lookup"><span data-stu-id="c0e20-172">Register the server in the vault using the following command:</span></span>

   ```

   $BinPath = $env:SystemDrive+"\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin"
   pushd $BinPath
   $encryptionFilePath = "C:\temp\"
   .\DRConfigurator.exe /r /Credentials $VaultSettingFilePath /vmmfriendlyname $env:COMPUTERNAME /dataencryptionenabled $encryptionFilePath /startvmmservice

   ```

## <a name="step-5-create-an-azure-storage-account"></a><span data-ttu-id="c0e20-173">5. adım: Azure storage hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="c0e20-173">Step 5: Create an Azure storage account</span></span>
<span data-ttu-id="c0e20-174">Bir Azure depolama hesabınız yoksa, aşağıdaki komutu çalıştırarak bir coğrafi çoğaltmanın etkinleştirilmiş hesabı oluşturun:</span><span class="sxs-lookup"><span data-stu-id="c0e20-174">If you don't have an Azure storage account, create a geo-replication enabled account by running the following command:</span></span>

```

$StorageAccountName = "teststorageacc1"
$StorageAccountGeo  = "Southeast Asia"

New-AzureStorageAccount -StorageAccountName $StorageAccountName -Label $StorageAccountName -Location $StorageAccountGeo;

```

<span data-ttu-id="c0e20-175">Depolama hesabı gerekir Azure Site Recovery hizmeti ile aynı bölgede olması ve aynı abonelikle ilişkilendirilmiş olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="c0e20-175">Note that the storage account must be in the same region as the Azure Site Recovery service, and be associated with the same subscription.</span></span>

## <a name="step-6-install-the-azure-recovery-services-agent"></a><span data-ttu-id="c0e20-176">6. adım: Azure kurtarma Hizmetleri Aracısı yükleme</span><span class="sxs-lookup"><span data-stu-id="c0e20-176">Step 6: Install the Azure Recovery Services Agent</span></span>
<span data-ttu-id="c0e20-177">Azure portalından, korumak istediğiniz VMM bulutlarında yer alan her Hyper-V ana bilgisayar sunucusunda Azure kurtarma Hizmetleri Aracısı'nı yükleyin.</span><span class="sxs-lookup"><span data-stu-id="c0e20-177">From the Azure portal, install the Azure Recovery Services agent on each Hyper-V host server located in the VMM clouds you want to protect.</span></span>

<span data-ttu-id="c0e20-178">Tüm VMM ana bilgisayarlarda aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="c0e20-178">Run the following command on all VMM hosts:</span></span>

```

marsagentinstaller.exe /q /nu

```


## <a name="step-7-configure-cloud-protection-settings"></a><span data-ttu-id="c0e20-179">7. adım: Bulut yapılandırma koruma ayarları</span><span class="sxs-lookup"><span data-stu-id="c0e20-179">Step 7: Configure cloud protection settings</span></span>
1. <span data-ttu-id="c0e20-180">Azure bulut koruması profil, aşağıdaki komutu çalıştırarak oluşturun:</span><span class="sxs-lookup"><span data-stu-id="c0e20-180">Create a cloud protection profile to Azure by running the following command:</span></span>

   ```

   $ReplicationFrequencyInSeconds = "300";
   $ProfileResult = New-AzureSiteRecoveryProtectionProfileObject -ReplicationProvider HyperVReplica -RecoveryAzureSubscription $AzureSubscriptionName -RecoveryAzureStorageAccount $StorageAccountName -ReplicationFrequencyInSeconds     $ReplicationFrequencyInSeconds;

   ```
2. <span data-ttu-id="c0e20-181">Koruma kapsayıcısı aşağıdaki komutları çalıştırarak alın:</span><span class="sxs-lookup"><span data-stu-id="c0e20-181">Get a protection container by running the following commands:</span></span>

   ```

   $PrimaryCloud = "testcloud"
   $protectionContainer = Get-AzureSiteRecoveryProtectionContainer -Name $PrimaryCloud;

   ```
3. <span data-ttu-id="c0e20-182">Koruma kapsayıcısı ilişkisini bulutla başlatın:</span><span class="sxs-lookup"><span data-stu-id="c0e20-182">Start the association of the protection container with the cloud:</span></span>

   ```

   $associationJob = Start-AzureSiteRecoveryProtectionProfileAssociationJob -ProtectionProfile $profileResult -PrimaryProtectionContainer $protectionContainer;        

   ```
4. <span data-ttu-id="c0e20-183">İş tamamlandıktan sonra aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="c0e20-183">After the job has finished, run the following command:</span></span>

        $job = Get-AzureSiteRecoveryJob -Id $associationJob.JobId;
        if($job -eq $null -or $job.StateDescription -ne "Completed")
        {
        $isJobLeftForProcessing = $true;
        }


1. <span data-ttu-id="c0e20-184">İş işlemeyi bitirdikten sonra aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="c0e20-184">After the job has finished processing, run the following command:</span></span>

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



<span data-ttu-id="c0e20-185">İşlemin tamamlanması denetlemek için adımları [etkinliğini izleme](#monitor).</span><span class="sxs-lookup"><span data-stu-id="c0e20-185">To check the completion of the operation, follow the steps in [Monitor Activity](#monitor).</span></span>

## <a name="step-8-configure-network-mapping"></a><span data-ttu-id="c0e20-186">8. adım: ağ eşlemesini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="c0e20-186">Step 8: Configure network mapping</span></span>
<span data-ttu-id="c0e20-187">Ağ eşlemesine başlamadan önce kaynak VMM sunucusundaki sanal makinelerin bir VM ağına bağlı olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="c0e20-187">Before you begin network mapping verify that virtual machines on the source VMM server are connected to a VM network.</span></span> <span data-ttu-id="c0e20-188">Ayrıca, bir veya daha fazla Azure sanal ağı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c0e20-188">In addition, create one or more Azure virtual networks.</span></span> <span data-ttu-id="c0e20-189">Birden çok VM ağının tek bir Azure ağına eşlenebileceğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="c0e20-189">Note that multiple VM networks can be mapped to a single Azure network.</span></span>

<span data-ttu-id="c0e20-190">Hedef ağın birden çok alt ağı varsa ve bu alt ağlardan biri kaynak sanal makinenin bulunduğu alt ağ ile aynı adı taşıyorsa çoğaltılan sanal makinenin, yük devretme işleminin ardından hedef alt ağa bağlandığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="c0e20-190">Note that if the target network has multiple subnets and one of those subnets has the same name as subnet on which the source virtual machine is located, then the replica virtual machine will be connected to that target subnet after failover.</span></span> <span data-ttu-id="c0e20-191">Eşleşen bir ada sahip bir hedef alt ağa değilse, sanal makine ağdaki ilk alt ağa bağlanır.</span><span class="sxs-lookup"><span data-stu-id="c0e20-191">If there is not a target subnet with a matching name, the virtual machine will be connected to the first subnet in the network.</span></span>

<span data-ttu-id="c0e20-192">İlk komut sunucuları için geçerli Azure Site Recovery kasası alır.</span><span class="sxs-lookup"><span data-stu-id="c0e20-192">The first command gets servers for the current Azure Site Recovery vault.</span></span> <span data-ttu-id="c0e20-193">Komut Microsoft Azure Site Recovery sunucuları $Servers dizi değişkeninde depolar.</span><span class="sxs-lookup"><span data-stu-id="c0e20-193">The command stores the Microsoft Azure Site Recovery servers in the $Servers array variable.</span></span>

    $Servers = Get-AzureSiteRecoveryServer


<span data-ttu-id="c0e20-194">İkinci komut site kurtarma ağ $Servers dizinin ilk sunucusunu alır.</span><span class="sxs-lookup"><span data-stu-id="c0e20-194">The second command gets the site recovery network for the first server in the $Servers array.</span></span> <span data-ttu-id="c0e20-195">Komut ağları $Networks değişkeninde depolar.</span><span class="sxs-lookup"><span data-stu-id="c0e20-195">The command stores the networks in the $Networks variable.</span></span>

    $Networks = Get-AzureSiteRecoveryNetwork -Server $Servers[0]

<span data-ttu-id="c0e20-196">Üçüncü komut Get-AzureSubscription cmdlet'ini kullanarak, Azure aboneliklerinize alır ve ardından bu değer $Subscriptions değişkeninde depolar.</span><span class="sxs-lookup"><span data-stu-id="c0e20-196">The third command gets your Azure subscriptions by using the Get-AzureSubscription cmdlet, and then stores that value in the $Subscriptions variable.</span></span>

    $Subscriptions = Get-AzureSubscription



<span data-ttu-id="c0e20-197">Dördüncü komut $AzureVmNetworks değişkeninde Get-AzureVNetSite cmdlet'i ve bu değer'ı kullanarak Azure sanal ağlar alır.</span><span class="sxs-lookup"><span data-stu-id="c0e20-197">The fourth command gets Azure virtual networks by using the Get-AzureVNetSite cmdlet, and then that value in the $AzureVmNetworks variable.</span></span>

    $AzureVmNetworks = Get-AzureVNetSite



<span data-ttu-id="c0e20-198">Son cmdlet birincil ağ ve Azure sanal makine ağı arasında bir eşleme oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c0e20-198">The final cmdlet creates a mapping between the primary network and the Azure virtual machine network.</span></span> <span data-ttu-id="c0e20-199">Cmdlet $Networks ilk öğe birincil ağı belirtir.</span><span class="sxs-lookup"><span data-stu-id="c0e20-199">The cmdlet specifies the primary network as the first element of $Networks.</span></span> <span data-ttu-id="c0e20-200">Cmdlet'in kendi kimliğini kullanarak bir sanal makine ağ $AzureVmNetworks ilk öğe belirtir</span><span class="sxs-lookup"><span data-stu-id="c0e20-200">The cmdlet specifies a virtual machine network as the first element of $AzureVmNetworks by using its ID.</span></span> <span data-ttu-id="c0e20-201">Bu komut Azure abonelik kimliğinizi içerir</span><span class="sxs-lookup"><span data-stu-id="c0e20-201">The command includes your Azure subscription ID.</span></span>

    New-AzureSiteRecoveryNetworkMapping -PrimaryNetwork $Networks[0] -AzureSubscriptionId $Subscriptions[0].SubscriptionId -AzureVMNetworkId $AzureVmNetworks[0].Id


## <a name="step-9-enable-protection-for-virtual-machines"></a><span data-ttu-id="c0e20-202">9. adım: sanal makineler için korumayı etkinleştir</span><span class="sxs-lookup"><span data-stu-id="c0e20-202">Step 9: Enable protection for virtual machines</span></span>
<span data-ttu-id="c0e20-203">Sunucular, bulutlar ve ağlar doğru şekilde yapılandırıldıktan sonra buluttaki sanal makineler için korumayı etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c0e20-203">After servers, clouds, and networks are configured correctly, you can enable protection for virtual machines in the cloud.</span></span> <span data-ttu-id="c0e20-204">Şunlara dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="c0e20-204">Note the following:</span></span>

<span data-ttu-id="c0e20-205">Sanal makineler karşılamalıdır [Azure sanal makine önkoşulları](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span><span class="sxs-lookup"><span data-stu-id="c0e20-205">Virtual machines must meet [Azure virtual machine prerequisites](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>

<span data-ttu-id="c0e20-206">Korumayı etkinleştirmek için işletim sisteminin ve işletim sistemi diski özelliklerinin sanal makineye göre ayarlanmış olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="c0e20-206">To enable protection the operating system and operating system disk properties must be set for the virtual machine.</span></span> <span data-ttu-id="c0e20-207">Sana makine şablonu kullanarak VMM'de bir sanal makine oluşturduğunuzda özelliği de ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c0e20-207">When you create a virtual machine in VMM using a virtual machine template you can set the property.</span></span> <span data-ttu-id="c0e20-208">Ayrıca var olan sanal makineler için bu özellikleri, sanal makinenin **Genel** ve **Donanım Yapılandırması** sekmelerinde de ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c0e20-208">You can also set these properties for existing virtual machines on the **General** and **Hardware Configuration** tabs of the virtual machine properties.</span></span> <span data-ttu-id="c0e20-209">Özellikleri VMM'de ayarlamazsanız Azure Site Recovery portalından da yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c0e20-209">If you don't set these properties in VMM you'll be able to configure them in the Azure Site Recovery portal.</span></span>

1. <span data-ttu-id="c0e20-210">Korumayı etkinleştirmek için koruma kapsayıcısı almak için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="c0e20-210">To enable protection, run the following command to get the protection container:</span></span>

     <span data-ttu-id="c0e20-211">$ProtectionContainer = get-AzureSiteRecoveryProtectionContainer-ad $CloudName</span><span class="sxs-lookup"><span data-stu-id="c0e20-211">$ProtectionContainer = Get-AzureSiteRecoveryProtectionContainer -Name $CloudName</span></span>
2. <span data-ttu-id="c0e20-212">Korunan varlık (VM), aşağıdaki komutu çalıştırarak alın:</span><span class="sxs-lookup"><span data-stu-id="c0e20-212">Get the protection entity (VM) by running the following command:</span></span>

        $protectionEntity = Get-AzureSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer



1. <span data-ttu-id="c0e20-213">DR VM için aşağıdaki komutu çalıştırarak etkinleştirin:</span><span class="sxs-lookup"><span data-stu-id="c0e20-213">Enable the DR for the VM by running the following command:</span></span>

        $jobResult = Set-AzureSiteRecoveryProtectionEntity -ProtectionEntity $protectionEntity     -Protection Enable -Force



## <a name="test-your-deployment"></a><span data-ttu-id="c0e20-214">Dağıtımınızı test edin</span><span class="sxs-lookup"><span data-stu-id="c0e20-214">Test your deployment</span></span>
<span data-ttu-id="c0e20-215">Dağıtımınızı test etmek için bir yük devretme sınaması için tek bir sanal makine çalıştırmak veya birden çok sanal makine içeren bir kurtarma planı oluşturmak ve bir yük devretme sınaması için plan çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="c0e20-215">To test your deployment you can run a test failover for a single virtual machine, or create a recovery plan consisting of multiple virtual machines and run a test failover for the plan.</span></span> <span data-ttu-id="c0e20-216">Yük devretme testi, yük devretme işleminizi ve kurtarma mekanizmanızı yalıtılmış bir ortamda benzetimli olarak gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="c0e20-216">Test failover simulates your failover and recovery mechanism in an isolated network.</span></span> <span data-ttu-id="c0e20-217">Şunlara dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="c0e20-217">Note that:</span></span>

* <span data-ttu-id="c0e20-218">Yük devretmenin ardından Azure'daki sanal makineye Uzak Masaüstü kullanarak bağlanmak isterseniz yük devretme testini çalıştırmadan önceden sanal makinenizde Uzak Masaüstü Bağlantısı'nı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="c0e20-218">If you want to connect to the virtual machine in Azure using Remote Desktop after the failover, enable Remote Desktop Connection on the virtual machine before you run the test failover.</span></span>
* <span data-ttu-id="c0e20-219">Yük devretme sonrasında, Uzak Masaüstü'nü kullanarak azure'daki sanal makineye bağlanmak için bir ortak IP adresini kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="c0e20-219">After failover, you'll use a public IP address to connect to the virtual machine in Azure using Remote Desktop.</span></span> <span data-ttu-id="c0e20-220">Bu işlemi gerçekleştirmek isterseniz genel bir adres kullanarak sanal makineye bağlanmanızı engelleyecek etki alanı ilkelerine sahip olmadığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="c0e20-220">If you want to do this, ensure you don't have any domain policies that prevent you from connecting to a virtual machine using a public address.</span></span>

<span data-ttu-id="c0e20-221">İşlemin tamamlanması denetlemek için adımları [etkinliğini izleme](#monitor).</span><span class="sxs-lookup"><span data-stu-id="c0e20-221">To check the completion of the operation, follow the steps in [Monitor Activity](#monitor).</span></span>

### <a name="create-a-recovery-plan"></a><span data-ttu-id="c0e20-222">Kurtarma planı oluşturma</span><span class="sxs-lookup"><span data-stu-id="c0e20-222">Create a recovery plan</span></span>
1. <span data-ttu-id="c0e20-223">Verileri kullanarak kurtarma planınız için bir şablon olarak bir .xml dosyası oluşturun ve ardından "C:\RPTemplatePath.xml" kaydedin.</span><span class="sxs-lookup"><span data-stu-id="c0e20-223">Create an .xml file as a template for your recovery plan using the data below, and then save it as "C:\RPTemplatePath.xml".</span></span>
2. <span data-ttu-id="c0e20-224">RecoveryPlan düğüm kimliği, ad, PrimaryServerId ve SecondaryServerId değiştirin.</span><span class="sxs-lookup"><span data-stu-id="c0e20-224">Change the RecoveryPlan node Id, Name, PrimaryServerId, and SecondaryServerId.</span></span>
3. <span data-ttu-id="c0e20-225">ProtectionEntity düğüm PrimaryProtectionEntityId (vmm'den vmıd) değiştirin.</span><span class="sxs-lookup"><span data-stu-id="c0e20-225">Change the ProtectionEntity node PrimaryProtectionEntityId (vmid from VMM).</span></span>
4. <span data-ttu-id="c0e20-226">Daha fazla VM'ler daha fazla ProtectionEntity düğüm ekleyerek ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c0e20-226">You can add more VMs by adding more ProtectionEntity nodes.</span></span>

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



1. <span data-ttu-id="c0e20-227">Şablondaki veri doldurun:</span><span class="sxs-lookup"><span data-stu-id="c0e20-227">Fill in the data in the template:</span></span>

        $TemplatePath = "C:\RPTemplatePath.xml";



1. <span data-ttu-id="c0e20-228">RecoveryPlan oluşturun:</span><span class="sxs-lookup"><span data-stu-id="c0e20-228">Create the RecoveryPlan:</span></span>

        $RPCreationJob = New-AzureSiteRecoveryRecoveryPlan -File $TemplatePath -WaitForCompletion;

### <a name="run-a-test-failover"></a><span data-ttu-id="c0e20-229">Yük devretme testi çalıştırma</span><span class="sxs-lookup"><span data-stu-id="c0e20-229">Run a test failover</span></span>
1. <span data-ttu-id="c0e20-230">Aşağıdaki komutu çalıştırarak RecoveryPlan nesnesini alın:</span><span class="sxs-lookup"><span data-stu-id="c0e20-230">Get the RecoveryPlan object by running the following command:</span></span>

     <span data-ttu-id="c0e20-231">$RPObject = get-AzureSiteRecoveryRecoveryPlan-ad $RPName;</span><span class="sxs-lookup"><span data-stu-id="c0e20-231">$RPObject = Get-AzureSiteRecoveryRecoveryPlan -Name $RPName;</span></span>
2. <span data-ttu-id="c0e20-232">Aşağıdaki komutu çalıştırarak test yük devretme başlatın:</span><span class="sxs-lookup"><span data-stu-id="c0e20-232">Start the test failover by running the following command:</span></span>

        $jobIDResult = Start-AzureSiteRecoveryTestFailoverJob -RecoveryPlan $RPObject -Direction PrimaryToRecovery;


## <span data-ttu-id="c0e20-233"><a name=monitor></a>Etkinliğini izleme</span><span class="sxs-lookup"><span data-stu-id="c0e20-233"><a name=monitor></a> Monitor Activity</span></span>
<span data-ttu-id="c0e20-234">Etkinliğini izlemek için aşağıdaki komutları kullanın.</span><span class="sxs-lookup"><span data-stu-id="c0e20-234">Use the following commands to monitor the activity.</span></span> <span data-ttu-id="c0e20-235">Bitirmek işleme işleri arasında beklemek zorunda unutmayın.</span><span class="sxs-lookup"><span data-stu-id="c0e20-235">Note that you have to wait in between jobs for the processing to finish.</span></span>

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



## <a name="next-steps"></a><span data-ttu-id="c0e20-236">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c0e20-236">Next steps</span></span>
<span data-ttu-id="c0e20-237">[Daha fazla bilgi](/powershell/azure/overview) Azure Site Recovery PowerShell cmdlet'leri hakkında.</span><span class="sxs-lookup"><span data-stu-id="c0e20-237">[Read more](/powershell/azure/overview) about Azure Site Recovery PowerShell cmdlets.</span></span> <span data-ttu-id="c0e20-238"></a>.</span><span class="sxs-lookup"><span data-stu-id="c0e20-238"></a>.</span></span>
