---
title: "PowerShell ve Azure Resource Manager ile Hyper-V Vm'lerini çoğaltma | Microsoft Docs"
description: "Hyper-V sanal makineleri PowerShell ve Azure Resource Manager kullanarak Azure Site Recovery ile azure'a çoğaltma otomatikleştirin."
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
ms.openlocfilehash: dbd562b73b0caecd0feb993bd6fb796dddb0438c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="replicate-between-on-premises-hyper-v-virtual-machines-and-azure-by-using-powershell-and-azure-resource-manager"></a><span data-ttu-id="98163-103">PowerShell ve Azure Resource Manager kullanarak şirket içi Hyper-V sanal makineleri ve Azure arasında çoğaltma</span><span class="sxs-lookup"><span data-stu-id="98163-103">Replicate between on-premises Hyper-V virtual machines and Azure by using PowerShell and Azure Resource Manager</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="98163-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="98163-104">Azure Portal</span></span>](site-recovery-hyper-v-site-to-azure.md)
> * [<span data-ttu-id="98163-105">PowerShell - Resource Manager</span><span class="sxs-lookup"><span data-stu-id="98163-105">PowerShell - Resource Manager</span></span>](site-recovery-deploy-with-powershell-resource-manager.md)
> * [<span data-ttu-id="98163-106">Klasik Portal</span><span class="sxs-lookup"><span data-stu-id="98163-106">Classic Portal</span></span>](site-recovery-hyper-v-site-to-azure-classic.md)
>
>

## <a name="overview"></a><span data-ttu-id="98163-107">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="98163-107">Overview</span></span>
<span data-ttu-id="98163-108">Azure Site Recovery, çoğaltma, yük devretme ve kurtarma çeşitli dağıtım senaryolarında sanal makinelerin düzenleyerek iş sürekliliği ve olağanüstü durum kurtarma stratejinize katkıda bulunur.</span><span class="sxs-lookup"><span data-stu-id="98163-108">Azure Site Recovery contributes to your business continuity and disaster recovery strategy by orchestrating replication, failover, and recovery of virtual machines in a number of deployment scenarios.</span></span> <span data-ttu-id="98163-109">Dağıtım senaryoları tam bir listesi için bkz: [Azure Site Recovery genel bakış](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="98163-109">For a full list of deployment scenarios, see the [Azure Site Recovery overview](site-recovery-overview.md).</span></span>

<span data-ttu-id="98163-110">Azure PowerShell cmdlet'leri Azure Windows PowerShell üzerinden yönetmenizi sağlayan bir modüldür.</span><span class="sxs-lookup"><span data-stu-id="98163-110">Azure PowerShell is a module that provides cmdlets to manage Azure through Windows PowerShell.</span></span> <span data-ttu-id="98163-111">İki tür modülü çalışabilir: Azure profili modülü veya Azure Resource Manager modülü.</span><span class="sxs-lookup"><span data-stu-id="98163-111">It can work with two types of modules: the Azure Profile module, or the Azure Resource Manager module.</span></span>

<span data-ttu-id="98163-112">Site Recovery PowerShell cmdlet, Azure PowerShell için Azure Resource Manager ile kullanılabilir korumak ve sunucularınızı Azure kurtarmak yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="98163-112">Site Recovery PowerShell cmdlets, available with Azure PowerShell for Azure Resource Manager, help you protect and recover your servers in Azure.</span></span>

<span data-ttu-id="98163-113">Bu makalede, yapılandırmak ve sunucusu Azure koruması için düzenlemek için Site Recovery dağıtmak için Windows PowerShell, Azure Resource Manager ile birlikte kullanmak açıklar.</span><span class="sxs-lookup"><span data-stu-id="98163-113">This article describes how to use Windows PowerShell, together with Azure Resource Manager, to deploy Site Recovery to configure and orchestrate server protection to Azure.</span></span> <span data-ttu-id="98163-114">Bu makalede kullanılan örnek koruma, yük devri ve Azure Resource Manager ile Azure PowerShell'i kullanarak azure'a, Hyper-V konağı üzerinde sanal makineleri kurtarma gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="98163-114">The example used in this article shows you how to protect, fail over, and recover virtual machines on a Hyper-V host to Azure, by using Azure PowerShell with Azure Resource Manager.</span></span>

> [!NOTE]
> <span data-ttu-id="98163-115">Site Recovery PowerShell cmdlet şu anda aşağıdaki yapılandırmanıza olanak tanır: başka bir sanal makine yöneticisi sitesine, bir Azure Sanal Makine Yöneticisi siteye ve Azure Hyper-V sitesi.</span><span class="sxs-lookup"><span data-stu-id="98163-115">The Site Recovery PowerShell cmdlets currently allow you to configure the following: one Virtual Machine Manager site to another, a Virtual Machine Manager site to Azure, and a Hyper-V site to Azure.</span></span>
>
>

<span data-ttu-id="98163-116">Bu makalede kullanmak için uzman PowerShell olması gerekmez, ancak modüller, cmdlet'ler ve oturumlar gibi temel kavramları anlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="98163-116">You don't need to be a PowerShell expert to use this article, but you do need to understand the basic concepts, such as modules, cmdlets, and sessions.</span></span> <span data-ttu-id="98163-117">Windows PowerShell hakkında daha fazla bilgi için bkz. [Windows PowerShell ile Çalışmaya Başlama](http://technet.microsoft.com/library/hh857337.aspx).</span><span class="sxs-lookup"><span data-stu-id="98163-117">For more information about Windows PowerShell, see [Getting Started with Windows PowerShell](http://technet.microsoft.com/library/hh857337.aspx).</span></span>

<span data-ttu-id="98163-118">Ayrıca daha fazla hakkında bilgiyi [Azure PowerShell kullanarak Azure Resource Manager ile](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="98163-118">You can also read more about [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span>

> [!NOTE]
> <span data-ttu-id="98163-119">Bulut çözümü sağlayıcısı (CSP) programın parçası olan Microsoft iş ortaklarının yapılandırın ve müşterilerin ilgili CSP aboneliklere (Kiracı abonelikleri) müşterilerin sunucuların korumasını yönetin.</span><span class="sxs-lookup"><span data-stu-id="98163-119">Microsoft partners that are part of the Cloud Solution Provider (CSP) program can configure and manage protection of their customers' servers to their customers' respective CSP subscriptions (tenant subscriptions).</span></span>
>
>

## <a name="before-you-start"></a><span data-ttu-id="98163-120">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="98163-120">Before you start</span></span>
<span data-ttu-id="98163-121">Bu Önkoşullar sağladığınızdan emin olun:</span><span class="sxs-lookup"><span data-stu-id="98163-121">Make sure you have these prerequisites in place:</span></span>

* <span data-ttu-id="98163-122">A [Microsoft Azure](https://azure.microsoft.com/) hesabı.</span><span class="sxs-lookup"><span data-stu-id="98163-122">A [Microsoft Azure](https://azure.microsoft.com/) account.</span></span> <span data-ttu-id="98163-123">[Ücretsiz deneme sürümüyle](https://azure.microsoft.com/pricing/free-trial/) başlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="98163-123">You can start with a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> <span data-ttu-id="98163-124">Ayrıca, hakkında bilgi edinebilirsiniz [Azure Site Recovery Manager fiyatlandırma](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="98163-124">In addition, you can read about [Azure Site Recovery Manager pricing](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>
* <span data-ttu-id="98163-125">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="98163-125">Azure PowerShell 1.0.</span></span> <span data-ttu-id="98163-126">Bu sürüm ve nasıl yükleneceği hakkında daha fazla bilgi için bkz: [Azure PowerShell 1.0.](https://azure.microsoft.com/)</span><span class="sxs-lookup"><span data-stu-id="98163-126">For information about this release and how to install it, see [Azure PowerShell 1.0.](https://azure.microsoft.com/)</span></span>
* <span data-ttu-id="98163-127">[AzureRM.SiteRecovery](https://www.powershellgallery.com/packages/AzureRM.SiteRecovery/) ve [AzureRM.RecoveryServices](https://www.powershellgallery.com/packages/AzureRM.RecoveryServices/) modüller.</span><span class="sxs-lookup"><span data-stu-id="98163-127">The [AzureRM.SiteRecovery](https://www.powershellgallery.com/packages/AzureRM.SiteRecovery/) and [AzureRM.RecoveryServices](https://www.powershellgallery.com/packages/AzureRM.RecoveryServices/) modules.</span></span> <span data-ttu-id="98163-128">Bu modüllerden en son sürümlerini alabilirsiniz [PowerShell Galerisi](https://www.powershellgallery.com/)</span><span class="sxs-lookup"><span data-stu-id="98163-128">You can get the latest versions of these modules from the [PowerShell gallery](https://www.powershellgallery.com/)</span></span>

<span data-ttu-id="98163-129">Bu makalede Azure PowerShell'i Azure Resource Manager ile yapılandırmak ve koruma sunucularınızın yönetmek için nasıl kullanılacağı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="98163-129">This article illustrates how to use Azure Powershell with Azure Resource Manager to configure and manage protection of your servers.</span></span> <span data-ttu-id="98163-130">Bu makalede kullanılan örnek Azure bir Hyper-V ana bilgisayarda çalışan bir sanal makine Koru gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="98163-130">The example used in this article shows you how to protect a virtual machine, running on a Hyper-V host, to Azure.</span></span> <span data-ttu-id="98163-131">Bu örnek için aşağıdaki önkoşullar özgüdür.</span><span class="sxs-lookup"><span data-stu-id="98163-131">The following prerequisites are specific to this example.</span></span> <span data-ttu-id="98163-132">Daha kapsamlı birtakım çeşitli Site kurtarma senaryoları için gereksinimleri için bu senaryo ile ilgili belgelere başvurun.</span><span class="sxs-lookup"><span data-stu-id="98163-132">For a more comprehensive set of requirements for the various Site Recovery scenarios, refer to the documentation pertaining to that scenario.</span></span>

* <span data-ttu-id="98163-133">Windows Server 2012 R2 veya bir veya daha fazla sanal makine içeren Microsoft Hyper-V Server 2012 R2 çalıştıran bir Hyper-V ana bilgisayarı.</span><span class="sxs-lookup"><span data-stu-id="98163-133">A Hyper-V host running Windows Server 2012 R2 or Microsoft Hyper-V Server 2012 R2 containing one or more virtual machines.</span></span>
* <span data-ttu-id="98163-134">Hyper-V sunucularının, doğrudan ya da bir proxy sunucu üzerinden Internet'e bağlı.</span><span class="sxs-lookup"><span data-stu-id="98163-134">Hyper-V servers connected to the Internet, either directly or through a proxy.</span></span>
* <span data-ttu-id="98163-135">Korumak istediğiniz sanal makineleri karşılaması gerektiğini [sanal makine önkoşulları](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span><span class="sxs-lookup"><span data-stu-id="98163-135">The virtual machines you want to protect should conform with [Virtual Machine prerequisites](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>

## <a name="step-1-sign-in-to-your-azure-account"></a><span data-ttu-id="98163-136">1. adım: Azure hesabınızda oturum açın</span><span class="sxs-lookup"><span data-stu-id="98163-136">Step 1: Sign in to your Azure account</span></span>
1. <span data-ttu-id="98163-137">Bir PowerShell konsolu açın ve Azure hesabınızda oturum açmak için bu komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="98163-137">Open a PowerShell console and run this command to sign in to your Azure account.</span></span> <span data-ttu-id="98163-138">Cmdlet için hesap kimlik bilgilerinizi ister bir web sayfasını getirir.</span><span class="sxs-lookup"><span data-stu-id="98163-138">The cmdlet brings up a web page that will prompt you for your account credentials.</span></span>

        Login-AzureRmAccount

    <span data-ttu-id="98163-139">Alternatif olarak, ayrıca, hesap kimlik bilgilerini bir parametre olarak ekleyebilirsiniz `Login-AzureRmAccount` cmdlet'ini kullanarak `-Credential` parametresi.</span><span class="sxs-lookup"><span data-stu-id="98163-139">Alternately, you could also include your account credentials as a parameter to the `Login-AzureRmAccount` cmdlet, by using the `-Credential` parameter.</span></span>

    <span data-ttu-id="98163-140">Kiracı adına çalışma CSP ortağı varsa, müşteri, Tenantıd veya Kiracı birincil etki alanı adlarını kullanarak bir kiracı olarak belirtin.</span><span class="sxs-lookup"><span data-stu-id="98163-140">If you are CSP partner working on behalf of a tenant, specify the customer as a tenant, by using their tenantID or tenant primary domain name.</span></span>

        Login-AzureRmAccount -Tenant "fabrikam.com"
2. <span data-ttu-id="98163-141">Hesap ile kullanmak istediğiniz aboneliği ilişkilendirmeniz böylece bir hesap birden fazla abonelik olabilir.</span><span class="sxs-lookup"><span data-stu-id="98163-141">An account can have several subscriptions, so you should associate the subscription you want to use with the account.</span></span>

        Select-AzureRmSubscription -SubscriptionName $SubscriptionName
3. <span data-ttu-id="98163-142">Aboneliğinizi aşağıdaki komutları kullanarak Azure sağlayıcıları kurtarma Hizmetleri ve Site kurtarma için kullanmak üzere kayıtlı olduğunu doğrulayın:</span><span class="sxs-lookup"><span data-stu-id="98163-142">Verify that your subscription is registered to use the Azure providers for Recovery Services and Site Recovery, by using the following commands:</span></span>

   * `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.RecoveryServices`
   * `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.SiteRecovery`

   <span data-ttu-id="98163-143">Bu komutların çıktısı, varsa **RegistrationState** ayarlanır **kayıtlı**, adım 2'ye devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="98163-143">In the output of these commands, if the **RegistrationState** is set to **Registered**, you can proceed to Step 2.</span></span> <span data-ttu-id="98163-144">Aksi durumda, aboneliğinizde eksik sağlayıcısı kaydetmeniz.</span><span class="sxs-lookup"><span data-stu-id="98163-144">If not, you should register the missing provider in your subscription.</span></span>

   <span data-ttu-id="98163-145">Site kurtarma ve kurtarma Hizmetleri için Azure sağlayıcısını kaydetmek için aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="98163-145">To register the Azure provider for Site Recovery and Recovery Services, run the following commands:</span></span>

       Register-AzureRmResourceProvider -ProviderNamespace Microsoft.SiteRecovery
       Register-AzureRmResourceProvider -ProviderNamespace Microsoft.RecoveryServices

   <span data-ttu-id="98163-146">Aşağıdaki komutları kullanarak sağlayıcıları başarıyla kaydedildiğini doğrulayın: `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.RecoveryServices` ve `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.SiteRecovery`.</span><span class="sxs-lookup"><span data-stu-id="98163-146">Verify that the providers registered successfully by using the following commands: `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.RecoveryServices` and `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.SiteRecovery`.</span></span>

## <a name="step-2-set-up-the-recovery-services-vault"></a><span data-ttu-id="98163-147">2. adım: Kurtarma Hizmetleri kasası ayarlama</span><span class="sxs-lookup"><span data-stu-id="98163-147">Step 2: Set up the Recovery Services vault</span></span>
1. <span data-ttu-id="98163-148">İçinde kasası oluşturma veya varolan bir kaynak grubunu kullanın bir Azure Resource Manager kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="98163-148">Create an Azure Resource Manager resource group in which you'll create the vault, or use an existing resource group.</span></span> <span data-ttu-id="98163-149">Aşağıdaki komutu kullanarak yeni bir kaynak grubu oluşturabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="98163-149">You can create a new resource group by using the following command:</span></span>

        New-AzureRmResourceGroup -Name $ResourceGroupName -Location $Geo  

    <span data-ttu-id="98163-150">Burada $ResourceGroupName değişkeni oluşturmak istediğiniz kaynak grubunun adını içerir ve $Geo değişkeni (örneğin, "Brezilya Güney") kaynak grubunun oluşturulacağı Azure bölgesi içerir.</span><span class="sxs-lookup"><span data-stu-id="98163-150">where the $ResourceGroupName variable contains the name of the resource group you want to create, and the $Geo variable contains the Azure region in which to create the resource group (for example, "Brazil South").</span></span>

    <span data-ttu-id="98163-151">Kaynak gruplarının bir listesini kullanarak aboneliğinizde elde edebilirsiniz `Get-AzureRmResourceGroup` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="98163-151">You can obtain a list of resource groups in your subscription by using the `Get-AzureRmResourceGroup` cmdlet.</span></span>
2. <span data-ttu-id="98163-152">Yeni bir Azure kurtarma Hizmetleri kasası gibi oluşturun:</span><span class="sxs-lookup"><span data-stu-id="98163-152">Create a new Azure Recovery Services vault as follows:</span></span>

        $vault = New-AzureRmRecoveryServicesVault -Name <string> -ResourceGroupName <string> -Location <string>

    <span data-ttu-id="98163-153">Kullanarak mevcut kasalarının listesi alabilirsiniz `Get-AzureRmRecoveryServicesVault` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="98163-153">You can retrieve a list of existing vaults by using the `Get-AzureRmRecoveryServicesVault` cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="98163-154">Klasik Portalı'nı veya Azure Service Management PowerShell modülü kullanılarak oluşturulan Site Recovery kasası işlemleri gerçekleştirmek isterseniz, kullanarak bu tür kasalarının listesi alabilirsiniz `Get-AzureRmSiteRecoveryVault` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="98163-154">If you wish to perform operations on Site Recovery vaults created using the classic portal or the Azure Service Management PowerShell module, you can retrieve a list of such vaults by using the `Get-AzureRmSiteRecoveryVault` cmdlet.</span></span> <span data-ttu-id="98163-155">Tüm yeni işlemleri için yeni bir kurtarma Hizmetleri kasası oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="98163-155">You should create a new Recovery Services vault for all new operations.</span></span> <span data-ttu-id="98163-156">Daha önce oluşturduğunuz Site Recovery kasası desteklenir, ancak en son özelliklere sahip değilsiniz.</span><span class="sxs-lookup"><span data-stu-id="98163-156">The Site Recovery vaults you've created earlier are supported, but don't have the latest features.</span></span>
>
>

## <a name="step-3-set-the-recovery-services-vault-context"></a><span data-ttu-id="98163-157">3. adım: Kurtarma Hizmetleri kasası bağlamını ayarlayın</span><span class="sxs-lookup"><span data-stu-id="98163-157">Step 3: Set the Recovery Services vault context</span></span>
1. <span data-ttu-id="98163-158">Aşağıdaki komutu çalıştırarak kasası bağlamını ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="98163-158">Set the vault context by running the following command:</span></span>

       Set-AzureRmSiteRecoveryVaultSettings -ARSVault $vault

## <a name="step-4-create-a-hyper-v-site-and-generate-a-new-vault-registration-key-for-the-site"></a><span data-ttu-id="98163-159">4. adım: bir Hyper-V sitesi oluşturun ve site için yeni bir kasa kayıt anahtarı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="98163-159">Step 4: Create a Hyper-V site and generate a new vault registration key for the site.</span></span>
1. <span data-ttu-id="98163-160">Yeni bir Hyper-V sitesi gibi oluşturun:</span><span class="sxs-lookup"><span data-stu-id="98163-160">Create a new Hyper-V site as follows:</span></span>

        $sitename = "MySite"                #Specify site friendly name
        New-AzureRmSiteRecoverySite -Name $sitename

    <span data-ttu-id="98163-161">Bu cmdlet siteyi oluşturmak için bir Site kurtarma işini başlatır ve Site Recovery iş nesnesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="98163-161">This cmdlet starts a Site Recovery job to create the site, and returns a Site Recovery job object.</span></span> <span data-ttu-id="98163-162">İşi tamamlamak ve doğrulamak iş başarıyla tamamlandı bekleyin.</span><span class="sxs-lookup"><span data-stu-id="98163-162">Wait for the job to complete and verify that the job completed successfully.</span></span>

    <span data-ttu-id="98163-163">İş nesnesini almak ve böylelikle Get-AzureRmSiteRecoveryJob cmdlet'ini kullanarak işinin geçerli durumunu denetleyin.</span><span class="sxs-lookup"><span data-stu-id="98163-163">You can retrieve the job object, and thereby check the current status of the job, by using the Get-AzureRmSiteRecoveryJob cmdlet.</span></span>
2. <span data-ttu-id="98163-164">Oluştur ve site için bir kayıt anahtarı aşağıdaki gibi indirin:</span><span class="sxs-lookup"><span data-stu-id="98163-164">Generate and download a registration key for the site, as follows:</span></span>

        $SiteIdentifier = Get-AzureRmSiteRecoverySite -Name $sitename | Select -ExpandProperty SiteIdentifier
        Get-AzureRmRecoveryServicesVaultSettingsFile -Vault $vault -SiteIdentifier $SiteIdentifier -SiteFriendlyName $sitename -Path $Path

    <span data-ttu-id="98163-165">İndirilen anahtarı Hyper-V ana bilgisayara kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="98163-165">Copy the downloaded key to the Hyper-V host.</span></span> <span data-ttu-id="98163-166">Hyper-V ana siteye kaydetmek için anahtarını gerekir.</span><span class="sxs-lookup"><span data-stu-id="98163-166">You need the key to register the Hyper-V host to the site.</span></span>

## <a name="step-5-install-the-azure-site-recovery-provider-and-azure-recovery-services-agent-on-your-hyper-v-host"></a><span data-ttu-id="98163-167">5. adım: Azure Site Recovery sağlayıcısı ve Azure kurtarma Hizmetleri Aracısı, Hyper-V konak üzerinde yükleyin</span><span class="sxs-lookup"><span data-stu-id="98163-167">Step 5: Install the Azure Site Recovery provider and Azure Recovery Services Agent on your Hyper-V host</span></span>
1. <span data-ttu-id="98163-168">Yükleyici Sağlayıcısı'ndan en son sürümü karşıdan [Microsoft](https://aka.ms/downloaddra).</span><span class="sxs-lookup"><span data-stu-id="98163-168">Download the installer for the latest version of the provider from [Microsoft](https://aka.ms/downloaddra).</span></span>
2. <span data-ttu-id="98163-169">Çalışma yükleyici, Hyper-V ana bilgisayarında ve yükleme işleminin sonunda kayıt adıma devam edin.</span><span class="sxs-lookup"><span data-stu-id="98163-169">Run the installer on your Hyper-V host, and at the end of the installation continue to the registration step.</span></span>
3. <span data-ttu-id="98163-170">İstendiğinde, indirilen site kayıt anahtarını ve Hyper-V ana siteye tam kayıt sağlayın.</span><span class="sxs-lookup"><span data-stu-id="98163-170">When prompted, provide the downloaded site registration key, and complete registration of the Hyper-V host to the site.</span></span>
4. <span data-ttu-id="98163-171">Aşağıdaki komutu kullanarak Hyper-V ana siteye kayıtlı olduğunu doğrulayın:</span><span class="sxs-lookup"><span data-stu-id="98163-171">Verify that the Hyper-V host is registered to the site by using the following command:</span></span>

        $server =  Get-AzureRmSiteRecoveryServer -FriendlyName $server-friendlyname

## <a name="step-6-create-a-replication-policy-and-associate-it-with-the-protection-container"></a><span data-ttu-id="98163-172">6. adım: bir çoğaltma ilkesi oluşturun ve koruma kapsayıcısı ile ilişkilendirin</span><span class="sxs-lookup"><span data-stu-id="98163-172">Step 6: Create a replication policy and associate it with the protection container</span></span>
1. <span data-ttu-id="98163-173">Bir çoğaltma ilkesi şu şekilde oluşturun:</span><span class="sxs-lookup"><span data-stu-id="98163-173">Create a replication policy as follows:</span></span>

        $ReplicationFrequencyInSeconds = "300";        #options are 30,300,900
        $PolicyName = “replicapolicy”
        $Recoverypoints = 6                    #specify the number of recovery points
        $storageaccountID = Get-AzureRmStorageAccount -Name "mystorea" -ResourceGroupName "MyRG" | Select -ExpandProperty Id

        $PolicyResult = New-AzureRmSiteRecoveryPolicy -Name $PolicyName -ReplicationProvider “HyperVReplicaAzure” -ReplicationFrequencyInSeconds $ReplicationFrequencyInSeconds  -RecoveryPoints $Recoverypoints -ApplicationConsistentSnapshotFrequencyInHours 1 -RecoveryAzureStorageAccountId $storageaccountID

    <span data-ttu-id="98163-174">Çoğaltma İlkesi oluşturma başarılı olduğundan emin olmak için döndürülen işini denetleyin.</span><span class="sxs-lookup"><span data-stu-id="98163-174">Check the returned job to ensure that the replication policy creation succeeds.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="98163-175">Belirtilen depolama hesabı, Kurtarma Hizmetleri kasasıyla aynı Azure bölgesinde olmalıdır ve coğrafi çoğaltmanın etkinleştirilmiş olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="98163-175">The storage account specified should be in the same Azure region as your Recovery Services vault, and should have geo-replication enabled.</span></span>
   >
   > * <span data-ttu-id="98163-176">Belirtilen Kurtarma Depolama hesabı türü Azure Storage (Klasik) ise, korunan makinelerin yük devretme Azure Iaas (Klasik) makineye kurtarın.</span><span class="sxs-lookup"><span data-stu-id="98163-176">If the specified Recovery storage account is of type Azure Storage (Classic), failover of the protected machines recover the machine to Azure IaaS (Classic).</span></span>
   > * <span data-ttu-id="98163-177">Belirtilen Kurtarma Depolama hesabı türü Azure Storage (Azure Resource Manager) ise, korunan makinelerin yük devretme Azure Iaas (Azure Resource Manager) makineye kurtarın.</span><span class="sxs-lookup"><span data-stu-id="98163-177">If the specified Recovery storage account is of type Azure Storage (Azure Resource Manager), failover of the protected machines recover the machine to Azure IaaS (Azure Resource Manager).</span></span>
   >
   >
2. <span data-ttu-id="98163-178">Siteye gibi karşılık gelen koruma kapsayıcısı alın:</span><span class="sxs-lookup"><span data-stu-id="98163-178">Get the protection container corresponding to the site, as follows:</span></span>

        $protectionContainer = Get-AzureRmSiteRecoveryProtectionContainer
3. <span data-ttu-id="98163-179">Koruma kapsayıcısı ilişkisini çoğaltma ilkesi, aşağıda gösterildiği gibi başlatın:</span><span class="sxs-lookup"><span data-stu-id="98163-179">Start the association of the protection container with the replication policy, as follows:</span></span>

     <span data-ttu-id="98163-180">$Policy get-AzureRmSiteRecoveryPolicy - FriendlyName $PolicyName $associationJob = başlangıç AzureRmSiteRecoveryPolicyAssociationJob =-ilke $Policy - PrimaryProtectionContainer $protectionContainer</span><span class="sxs-lookup"><span data-stu-id="98163-180">$Policy = Get-AzureRmSiteRecoveryPolicy -FriendlyName $PolicyName   $associationJob  = Start-AzureRmSiteRecoveryPolicyAssociationJob -Policy $Policy -PrimaryProtectionContainer $protectionContainer</span></span>

   <span data-ttu-id="98163-181">İlişkilendirme işi tamamlanmasını bekleyin ve başarıyla tamamlandığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="98163-181">Wait for the association job to complete, and ensure that it completed successfully.</span></span>

## <a name="step-7-enable-protection-for-virtual-machines"></a><span data-ttu-id="98163-182">7. adım: sanal makineler için korumayı etkinleştir</span><span class="sxs-lookup"><span data-stu-id="98163-182">Step 7: Enable protection for virtual machines</span></span>
1. <span data-ttu-id="98163-183">Aşağıdaki gibi korumak istediğiniz VM karşılık gelen koruma varlık alın:</span><span class="sxs-lookup"><span data-stu-id="98163-183">Get the protection entity corresponding to the VM you want to protect, as follows:</span></span>

        $VMFriendlyName = "Fabrikam-app"                    #Name of the VM
        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -ProtectionContainer $protectionContainer -FriendlyName $VMFriendlyName
2. <span data-ttu-id="98163-184">Sanal makine aşağıdaki gibi koruma başlatın:</span><span class="sxs-lookup"><span data-stu-id="98163-184">Start protecting the virtual machine, as follows:</span></span>

        $Ostype = "Windows"                                 # "Windows" or "Linux"
        $DRjob = Set-AzureRmSiteRecoveryProtectionEntity -ProtectionEntity $protectionEntity -Policy $Policy -Protection Enable -RecoveryAzureStorageAccountId $storageaccountID  -OS $OStype -OSDiskName $protectionEntity.Disks[0].Name

   > [!IMPORTANT]
   > <span data-ttu-id="98163-185">Belirtilen depolama hesabı, Kurtarma Hizmetleri kasasıyla aynı Azure bölgesinde olmalıdır ve coğrafi çoğaltmanın etkinleştirilmiş olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="98163-185">The storage account specified should be in the same Azure region as your Recovery Services vault, and should have geo-replication enabled.</span></span>
   >
   > * <span data-ttu-id="98163-186">Belirtilen Kurtarma Depolama hesabı türü Azure Storage (Klasik) ise, korunan makinelerin yük devretme Azure Iaas (Klasik) makineye kurtarın.</span><span class="sxs-lookup"><span data-stu-id="98163-186">If the specified Recovery storage account is of type Azure Storage (Classic), failover of the protected machines recover the machine to Azure IaaS (Classic).</span></span>
   > * <span data-ttu-id="98163-187">Belirtilen Kurtarma Depolama hesabı türü Azure Storage (Azure Resource Manager) ise, korunan makinelerin yük devretme Azure Iaas (Azure Resource Manager) makineye kurtarın.</span><span class="sxs-lookup"><span data-stu-id="98163-187">If the specified Recovery storage account is of type Azure Storage (Azure Resource Manager), failover of the protected machines recover the machine to Azure IaaS (Azure Resource Manager).</span></span>
   >
   > <span data-ttu-id="98163-188">Koruduğunuz VM ekli birden çok disk varsa, işletim sistemi diski kullanarak belirtin *OSDiskName* parametresi.</span><span class="sxs-lookup"><span data-stu-id="98163-188">If the VM you are protecting has more than one disk attached to it, specify the operating system disk by using the *OSDiskName* parameter.</span></span>
   >
   >
3. <span data-ttu-id="98163-189">Sanal makinelerin ilk çoğaltma sonrasında bir korumalı durumuna ulaşmasını bekleyin.</span><span class="sxs-lookup"><span data-stu-id="98163-189">Wait for the virtual machines to reach a protected state after the initial replication.</span></span> <span data-ttu-id="98163-190">Bu çoğaltılacak veri miktarını ve Azure Yukarı Akış bant gibi etkenlere bağlı olarak biraz zaman alabilir.</span><span class="sxs-lookup"><span data-stu-id="98163-190">This can take a while, depending on factors such as the amount of data to be replicated and the available upstream bandwidth to Azure.</span></span> <span data-ttu-id="98163-191">Aşağıdaki gibi StateDescription ve iş durumu korumalı duruma ulaşmadan VM güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="98163-191">The job State and StateDescription are updated as follows, upon the VM reaching a protected state.</span></span>

        PS C:\> $DRjob = Get-AzureRmSiteRecoveryJob -Job $DRjob

        PS C:\> $DRjob | Select-Object -ExpandProperty State
        Succeeded

        PS C:\> $DRjob | Select-Object -ExpandProperty StateDescription
        Completed
4. <span data-ttu-id="98163-192">VM rol boyutu ve Itanium tabanlı sistemler için sanal makinenin ağ arabirimi kartları için yük devretme sırasında eklemek için Azure ağ gibi kurtarma özelliklerini güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="98163-192">Update recovery properties, such as the VM role size, and the Azure network to attach the virtual machine's network interface cards to upon failover.</span></span>

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
        DisplayName      : Update the virtual machine
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



## <a name="step-8-run-a-test-failover"></a><span data-ttu-id="98163-193">8. adım: yük devretme testi çalıştırma</span><span class="sxs-lookup"><span data-stu-id="98163-193">Step 8: Run a test failover</span></span>
1. <span data-ttu-id="98163-194">Bir test yük devretme işini çalıştırmak için şunları yapın:</span><span class="sxs-lookup"><span data-stu-id="98163-194">Run a test failover job, as follows:</span></span>

        $nw = Get-AzureRmVirtualNetwork -Name "TestFailoverNw" -ResourceGroupName "MyRG" #Specify Azure vnet name and resource group

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -FriendlyName $VMFriendlyName -ProtectionContainer $protectionContainer

        $TFjob = Start-AzureRmSiteRecoveryTestFailoverJob -ProtectionEntity $protectionEntity -Direction PrimaryToRecovery -AzureVMNetworkId $nw.Id
2. <span data-ttu-id="98163-195">Test Azure'da VM oluşturulduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="98163-195">Verify that the test VM is created in Azure.</span></span> <span data-ttu-id="98163-196">(Test yük devretme işini, Azure'da VM test oluşturduktan sonra askıya alındı.</span><span class="sxs-lookup"><span data-stu-id="98163-196">(The test failover job is suspended, after creating the test VM in Azure.</span></span> <span data-ttu-id="98163-197">İş işi yeniden başlatma sırasında oluşturulan artefacts sonraki adımda gösterildiği gibi temizleniyor tarafından tamamlar.)</span><span class="sxs-lookup"><span data-stu-id="98163-197">The job completes by cleaning up the created artefacts upon resuming the job, as illustrated in the next step.)</span></span>
3. <span data-ttu-id="98163-198">Yük devretme testi, aşağıdaki gibi tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="98163-198">Complete the test failover, as follows:</span></span>

        $TFjob = Resume-AzureRmSiteRecoveryJob -Job $TFjob

## <a name="next-steps"></a><span data-ttu-id="98163-199">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="98163-199">Next Steps</span></span>
<span data-ttu-id="98163-200">[Daha fazla bilgi](https://msdn.microsoft.com/library/azure/mt637930.aspx) Azure Site Recovery ile Azure Resource Manager PowerShell cmdlet'leri hakkında.</span><span class="sxs-lookup"><span data-stu-id="98163-200">[Read more](https://msdn.microsoft.com/library/azure/mt637930.aspx) about Azure Site Recovery with Azure Resource Manager PowerShell cmdlets.</span></span>
