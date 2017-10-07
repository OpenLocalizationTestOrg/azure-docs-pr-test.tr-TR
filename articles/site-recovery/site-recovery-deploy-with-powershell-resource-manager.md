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
# <a name="replicate-between-on-premises-hyper-v-virtual-machines-and-azure-by-using-powershell-and-azure-resource-manager"></a><span data-ttu-id="e15b5-103">PowerShell ve Azure Resource Manager kullanarak şirket içi Hyper-V sanal makineleri ve Azure arasında çoğaltma</span><span class="sxs-lookup"><span data-stu-id="e15b5-103">Replicate between on-premises Hyper-V virtual machines and Azure by using PowerShell and Azure Resource Manager</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e15b5-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="e15b5-104">Azure Portal</span></span>](site-recovery-hyper-v-site-to-azure.md)
> * [<span data-ttu-id="e15b5-105">PowerShell - Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e15b5-105">PowerShell - Resource Manager</span></span>](site-recovery-deploy-with-powershell-resource-manager.md)
> * [<span data-ttu-id="e15b5-106">Klasik Portal</span><span class="sxs-lookup"><span data-stu-id="e15b5-106">Classic Portal</span></span>](site-recovery-hyper-v-site-to-azure-classic.md)
>
>

## <a name="overview"></a><span data-ttu-id="e15b5-107">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="e15b5-107">Overview</span></span>
<span data-ttu-id="e15b5-108">Azure Site Recovery, çoğaltma, yük devretme ve kurtarma çeşitli dağıtım senaryolarında sanal makinelerin düzenleyerek tooyour iş sürekliliği ve olağanüstü durum kurtarma stratejisi katkıda bulunur.</span><span class="sxs-lookup"><span data-stu-id="e15b5-108">Azure Site Recovery contributes tooyour business continuity and disaster recovery strategy by orchestrating replication, failover, and recovery of virtual machines in a number of deployment scenarios.</span></span> <span data-ttu-id="e15b5-109">Dağıtım senaryoları tam bir listesi için bkz: Merhaba [Azure Site Recovery genel bakış](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e15b5-109">For a full list of deployment scenarios, see hello [Azure Site Recovery overview](site-recovery-overview.md).</span></span>

<span data-ttu-id="e15b5-110">Azure PowerShell cmdlet'leri toomanage Windows PowerShell üzerinden Azure sağlayan bir modüldür.</span><span class="sxs-lookup"><span data-stu-id="e15b5-110">Azure PowerShell is a module that provides cmdlets toomanage Azure through Windows PowerShell.</span></span> <span data-ttu-id="e15b5-111">İki tür modülü çalışabilir: Azure profili modülü veya hello Azure Resource Manager modülü hello.</span><span class="sxs-lookup"><span data-stu-id="e15b5-111">It can work with two types of modules: hello Azure Profile module, or hello Azure Resource Manager module.</span></span>

<span data-ttu-id="e15b5-112">Site Recovery PowerShell cmdlet, Azure PowerShell için Azure Resource Manager ile kullanılabilir korumak ve sunucularınızı Azure kurtarmak yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="e15b5-112">Site Recovery PowerShell cmdlets, available with Azure PowerShell for Azure Resource Manager, help you protect and recover your servers in Azure.</span></span>

<span data-ttu-id="e15b5-113">Bu makalede nasıl toouse Windows PowerShell ile birlikte Azure Resource Manager, toodeploy Site Recovery tooconfigure ve sunucu koruması tooAzure düzenlemek.</span><span class="sxs-lookup"><span data-stu-id="e15b5-113">This article describes how toouse Windows PowerShell, together with Azure Resource Manager, toodeploy Site Recovery tooconfigure and orchestrate server protection tooAzure.</span></span> <span data-ttu-id="e15b5-114">Bu makalede kullanılan hello örnek nasıl tooprotect, yük devri ve Azure Resource Manager ile Azure PowerShell kullanarak bir Hyper-V ana bilgisayar tooAzure sanal makinelerde kurtarmak gösterir.</span><span class="sxs-lookup"><span data-stu-id="e15b5-114">hello example used in this article shows you how tooprotect, fail over, and recover virtual machines on a Hyper-V host tooAzure, by using Azure PowerShell with Azure Resource Manager.</span></span>

> [!NOTE]
> <span data-ttu-id="e15b5-115">Merhaba Site Recovery PowerShell cmdlet şu anda aşağıdaki tooconfigure hello sağlar: bir Sanal Makine Yöneticisi site tooanother, bir Sanal Makine Yöneticisi site tooAzure ve bir Hyper-V sitesi tooAzure.</span><span class="sxs-lookup"><span data-stu-id="e15b5-115">hello Site Recovery PowerShell cmdlets currently allow you tooconfigure hello following: one Virtual Machine Manager site tooanother, a Virtual Machine Manager site tooAzure, and a Hyper-V site tooAzure.</span></span>
>
>

<span data-ttu-id="e15b5-116">Bu makalede toobe PowerShell Uzman toouse gerekmez, ancak toounderstand hello gibi temel kavramları modüller, cmdlet'ler ve oturumlar gerekir.</span><span class="sxs-lookup"><span data-stu-id="e15b5-116">You don't need toobe a PowerShell expert toouse this article, but you do need toounderstand hello basic concepts, such as modules, cmdlets, and sessions.</span></span> <span data-ttu-id="e15b5-117">Windows PowerShell hakkında daha fazla bilgi için bkz. [Windows PowerShell ile Çalışmaya Başlama](http://technet.microsoft.com/library/hh857337.aspx).</span><span class="sxs-lookup"><span data-stu-id="e15b5-117">For more information about Windows PowerShell, see [Getting Started with Windows PowerShell](http://technet.microsoft.com/library/hh857337.aspx).</span></span>

<span data-ttu-id="e15b5-118">Ayrıca daha fazla hakkında bilgiyi [Azure PowerShell kullanarak Azure Resource Manager ile](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="e15b5-118">You can also read more about [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span>

> [!NOTE]
> <span data-ttu-id="e15b5-119">Merhaba bulut çözümü sağlayıcısı (CSP) programı parçası olan Microsoft iş ortaklarının yapılandırmak ve müşterilerin sunucuların korumasını yönetmek tootheir müşterilerin ilgili CSP aboneliklerin (Kiracı abonelikleri).</span><span class="sxs-lookup"><span data-stu-id="e15b5-119">Microsoft partners that are part of hello Cloud Solution Provider (CSP) program can configure and manage protection of their customers' servers tootheir customers' respective CSP subscriptions (tenant subscriptions).</span></span>
>
>

## <a name="before-you-start"></a><span data-ttu-id="e15b5-120">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="e15b5-120">Before you start</span></span>
<span data-ttu-id="e15b5-121">Bu Önkoşullar sağladığınızdan emin olun:</span><span class="sxs-lookup"><span data-stu-id="e15b5-121">Make sure you have these prerequisites in place:</span></span>

* <span data-ttu-id="e15b5-122">A [Microsoft Azure](https://azure.microsoft.com/) hesabı.</span><span class="sxs-lookup"><span data-stu-id="e15b5-122">A [Microsoft Azure](https://azure.microsoft.com/) account.</span></span> <span data-ttu-id="e15b5-123">[Ücretsiz deneme sürümüyle](https://azure.microsoft.com/pricing/free-trial/) başlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e15b5-123">You can start with a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> <span data-ttu-id="e15b5-124">Ayrıca, hakkında bilgi edinebilirsiniz [Azure Site Recovery Manager fiyatlandırma](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="e15b5-124">In addition, you can read about [Azure Site Recovery Manager pricing](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>
* <span data-ttu-id="e15b5-125">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="e15b5-125">Azure PowerShell 1.0.</span></span> <span data-ttu-id="e15b5-126">Bu sürüm hakkında bilgi için ve nasıl tooinstall, bkz: [Azure PowerShell 1.0.](https://azure.microsoft.com/)</span><span class="sxs-lookup"><span data-stu-id="e15b5-126">For information about this release and how tooinstall it, see [Azure PowerShell 1.0.](https://azure.microsoft.com/)</span></span>
* <span data-ttu-id="e15b5-127">Merhaba [AzureRM.SiteRecovery](https://www.powershellgallery.com/packages/AzureRM.SiteRecovery/) ve [AzureRM.RecoveryServices](https://www.powershellgallery.com/packages/AzureRM.RecoveryServices/) modüller.</span><span class="sxs-lookup"><span data-stu-id="e15b5-127">hello [AzureRM.SiteRecovery](https://www.powershellgallery.com/packages/AzureRM.SiteRecovery/) and [AzureRM.RecoveryServices](https://www.powershellgallery.com/packages/AzureRM.RecoveryServices/) modules.</span></span> <span data-ttu-id="e15b5-128">Merhaba en son sürümleri bu modüllerin hello alabilirsiniz [PowerShell Galerisi](https://www.powershellgallery.com/)</span><span class="sxs-lookup"><span data-stu-id="e15b5-128">You can get hello latest versions of these modules from hello [PowerShell gallery](https://www.powershellgallery.com/)</span></span>

<span data-ttu-id="e15b5-129">Bu makalede gösterilmektedir nasıl toouse Azure Powershell ile Azure Resource Manager tooconfigure ve koruma sunucularınızın yönetin.</span><span class="sxs-lookup"><span data-stu-id="e15b5-129">This article illustrates how toouse Azure Powershell with Azure Resource Manager tooconfigure and manage protection of your servers.</span></span> <span data-ttu-id="e15b5-130">Bu makalede kullanılan hello örnek gösterir, nasıl tooprotect tooAzure bir Hyper-V ana bilgisayarında çalışan bir sanal makine.</span><span class="sxs-lookup"><span data-stu-id="e15b5-130">hello example used in this article shows you how tooprotect a virtual machine, running on a Hyper-V host, tooAzure.</span></span> <span data-ttu-id="e15b5-131">Önkoşullar aşağıdaki hello belirli toothis örnektir.</span><span class="sxs-lookup"><span data-stu-id="e15b5-131">hello following prerequisites are specific toothis example.</span></span> <span data-ttu-id="e15b5-132">Çeşitli Site kurtarma senaryoları, daha kapsamlı birtakım hello gereksinimleri için toothat senaryo ilgili toohello belgelerine başvurun.</span><span class="sxs-lookup"><span data-stu-id="e15b5-132">For a more comprehensive set of requirements for hello various Site Recovery scenarios, refer toohello documentation pertaining toothat scenario.</span></span>

* <span data-ttu-id="e15b5-133">Windows Server 2012 R2 veya bir veya daha fazla sanal makine içeren Microsoft Hyper-V Server 2012 R2 çalıştıran bir Hyper-V ana bilgisayarı.</span><span class="sxs-lookup"><span data-stu-id="e15b5-133">A Hyper-V host running Windows Server 2012 R2 or Microsoft Hyper-V Server 2012 R2 containing one or more virtual machines.</span></span>
* <span data-ttu-id="e15b5-134">Hyper-V sunucuları toohello Internet, doğrudan ya da bir proxy üzerinden bağlı.</span><span class="sxs-lookup"><span data-stu-id="e15b5-134">Hyper-V servers connected toohello Internet, either directly or through a proxy.</span></span>
* <span data-ttu-id="e15b5-135">Merhaba tooprotect istediğiniz sanal makineleri karşılaması gerektiğini [sanal makine önkoşulları](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span><span class="sxs-lookup"><span data-stu-id="e15b5-135">hello virtual machines you want tooprotect should conform with [Virtual Machine prerequisites](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>

## <a name="step-1-sign-in-tooyour-azure-account"></a><span data-ttu-id="e15b5-136">1. adım: tooyour Azure hesabı ile oturum açın.</span><span class="sxs-lookup"><span data-stu-id="e15b5-136">Step 1: Sign in tooyour Azure account</span></span>
1. <span data-ttu-id="e15b5-137">Bir PowerShell konsolu açın ve bu komutu toosign tooyour Azure hesabı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="e15b5-137">Open a PowerShell console and run this command toosign in tooyour Azure account.</span></span> <span data-ttu-id="e15b5-138">Merhaba cmdlet'i için hesap kimlik bilgilerinizi ister bir web sayfasını getirir.</span><span class="sxs-lookup"><span data-stu-id="e15b5-138">hello cmdlet brings up a web page that will prompt you for your account credentials.</span></span>

        Login-AzureRmAccount

    <span data-ttu-id="e15b5-139">Alternatif olarak, ayrıca hesabı kimlik bilgilerinizi parametresi toohello ekleyebilirsiniz `Login-AzureRmAccount` hello kullanarak cmdlet `-Credential` parametresi.</span><span class="sxs-lookup"><span data-stu-id="e15b5-139">Alternately, you could also include your account credentials as a parameter toohello `Login-AzureRmAccount` cmdlet, by using hello `-Credential` parameter.</span></span>

    <span data-ttu-id="e15b5-140">Kiracı adına çalışma CSP ortağı varsa, hello müşteri kendi Tenantıd veya Kiracı birincil etki alanı adını kullanarak bir kiracı olarak belirtin.</span><span class="sxs-lookup"><span data-stu-id="e15b5-140">If you are CSP partner working on behalf of a tenant, specify hello customer as a tenant, by using their tenantID or tenant primary domain name.</span></span>

        Login-AzureRmAccount -Tenant "fabrikam.com"
2. <span data-ttu-id="e15b5-141">Hello hesabıyla toouse hello aboneliği ilişkilendirmeniz böylece bir hesap birden fazla abonelik olabilir.</span><span class="sxs-lookup"><span data-stu-id="e15b5-141">An account can have several subscriptions, so you should associate hello subscription you want toouse with hello account.</span></span>

        Select-AzureRmSubscription -SubscriptionName $SubscriptionName
3. <span data-ttu-id="e15b5-142">Aboneliğinizin kayıtlı toouse olduğunu doğrulayın hello aşağıdaki komutları kullanarak kurtarma Hizmetleri ve Site kurtarma için Azure sağlayıcıları hello:</span><span class="sxs-lookup"><span data-stu-id="e15b5-142">Verify that your subscription is registered toouse hello Azure providers for Recovery Services and Site Recovery, by using hello following commands:</span></span>

   * `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.RecoveryServices`
   * `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.SiteRecovery`

   <span data-ttu-id="e15b5-143">Merhaba, aşağıdaki komutlardan birini hello çıktısında **RegistrationState** çok ayarlanır**kayıtlı**, tooStep 2 devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e15b5-143">In hello output of these commands, if hello **RegistrationState** is set too**Registered**, you can proceed tooStep 2.</span></span> <span data-ttu-id="e15b5-144">Aksi durumda, aboneliğinizde hello eksik sağlayıcısı kaydetmeniz.</span><span class="sxs-lookup"><span data-stu-id="e15b5-144">If not, you should register hello missing provider in your subscription.</span></span>

   <span data-ttu-id="e15b5-145">tooregister Site kurtarma ve kurtarma Hizmetleri için Azure sağlayıcı Merhaba, hello aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="e15b5-145">tooregister hello Azure provider for Site Recovery and Recovery Services, run hello following commands:</span></span>

       Register-AzureRmResourceProvider -ProviderNamespace Microsoft.SiteRecovery
       Register-AzureRmResourceProvider -ProviderNamespace Microsoft.RecoveryServices

   <span data-ttu-id="e15b5-146">Merhaba aşağıdaki komutları kullanarak Hello sağlayıcıları başarıyla kaydedildiğini doğrulayın: `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.RecoveryServices` ve `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.SiteRecovery`.</span><span class="sxs-lookup"><span data-stu-id="e15b5-146">Verify that hello providers registered successfully by using hello following commands: `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.RecoveryServices` and `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.SiteRecovery`.</span></span>

## <a name="step-2-set-up-hello-recovery-services-vault"></a><span data-ttu-id="e15b5-147">2. adım: Hello ayarlama kurtarma Hizmetleri kasası</span><span class="sxs-lookup"><span data-stu-id="e15b5-147">Step 2: Set up hello Recovery Services vault</span></span>
1. <span data-ttu-id="e15b5-148">İçinde hello kasası oluşturma veya varolan bir kaynak grubunu kullanın bir Azure Resource Manager kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e15b5-148">Create an Azure Resource Manager resource group in which you'll create hello vault, or use an existing resource group.</span></span> <span data-ttu-id="e15b5-149">Komutu aşağıdaki hello kullanarak yeni bir kaynak grubu oluşturabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="e15b5-149">You can create a new resource group by using hello following command:</span></span>

        New-AzureRmResourceGroup -Name $ResourceGroupName -Location $Geo  

    <span data-ttu-id="e15b5-150">Merhaba $ResourceGroupName değişkeni hello hello kaynak grubu adını içeren burada toocreate istediğiniz ve hello $Geo değişkenini içeren hello Azure bölgesi hangi toocreate hello kaynak grubunda (örneğin, "Brezilya Güney").</span><span class="sxs-lookup"><span data-stu-id="e15b5-150">where hello $ResourceGroupName variable contains hello name of hello resource group you want toocreate, and hello $Geo variable contains hello Azure region in which toocreate hello resource group (for example, "Brazil South").</span></span>

    <span data-ttu-id="e15b5-151">Kaynak grupları listesini hello kullanarak aboneliğinizde elde edebilirsiniz `Get-AzureRmResourceGroup` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="e15b5-151">You can obtain a list of resource groups in your subscription by using hello `Get-AzureRmResourceGroup` cmdlet.</span></span>
2. <span data-ttu-id="e15b5-152">Yeni bir Azure kurtarma Hizmetleri kasası gibi oluşturun:</span><span class="sxs-lookup"><span data-stu-id="e15b5-152">Create a new Azure Recovery Services vault as follows:</span></span>

        $vault = New-AzureRmRecoveryServicesVault -Name <string> -ResourceGroupName <string> -Location <string>

    <span data-ttu-id="e15b5-153">Hello kullanarak mevcut kasalarının listesi alabilirsiniz `Get-AzureRmRecoveryServicesVault` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="e15b5-153">You can retrieve a list of existing vaults by using hello `Get-AzureRmRecoveryServicesVault` cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="e15b5-154">Site Recovery kasası hello Klasik portalında veya hello Azure Service Management PowerShell modülü kullanılarak oluşturulan tooperform işlemleri istiyorsanız hello kullanarak bu tür kasalarının listesi alabilirsiniz `Get-AzureRmSiteRecoveryVault` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="e15b5-154">If you wish tooperform operations on Site Recovery vaults created using hello classic portal or hello Azure Service Management PowerShell module, you can retrieve a list of such vaults by using hello `Get-AzureRmSiteRecoveryVault` cmdlet.</span></span> <span data-ttu-id="e15b5-155">Tüm yeni işlemleri için yeni bir kurtarma Hizmetleri kasası oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="e15b5-155">You should create a new Recovery Services vault for all new operations.</span></span> <span data-ttu-id="e15b5-156">daha önce oluşturduğunuz hello Site Recovery kasası desteklenir, ancak hello en son özelliklere sahip değilsiniz.</span><span class="sxs-lookup"><span data-stu-id="e15b5-156">hello Site Recovery vaults you've created earlier are supported, but don't have hello latest features.</span></span>
>
>

## <a name="step-3-set-hello-recovery-services-vault-context"></a><span data-ttu-id="e15b5-157">3. adım: hello kurtarma Hizmetleri kasası bağlam ayarlama</span><span class="sxs-lookup"><span data-stu-id="e15b5-157">Step 3: Set hello Recovery Services vault context</span></span>
1. <span data-ttu-id="e15b5-158">Merhaba aşağıdaki komutu çalıştırarak Hello kasası bağlamını ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="e15b5-158">Set hello vault context by running hello following command:</span></span>

       Set-AzureRmSiteRecoveryVaultSettings -ARSVault $vault

## <a name="step-4-create-a-hyper-v-site-and-generate-a-new-vault-registration-key-for-hello-site"></a><span data-ttu-id="e15b5-159">4. adım: bir Hyper-V sitesi oluşturun ve hello site için yeni bir kasa kayıt anahtarı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e15b5-159">Step 4: Create a Hyper-V site and generate a new vault registration key for hello site.</span></span>
1. <span data-ttu-id="e15b5-160">Yeni bir Hyper-V sitesi gibi oluşturun:</span><span class="sxs-lookup"><span data-stu-id="e15b5-160">Create a new Hyper-V site as follows:</span></span>

        $sitename = "MySite"                #Specify site friendly name
        New-AzureRmSiteRecoverySite -Name $sitename

    <span data-ttu-id="e15b5-161">Bu cmdlet, bir Site kurtarma işi toocreate hello siteyi başlatır ve Site Recovery iş nesnesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="e15b5-161">This cmdlet starts a Site Recovery job toocreate hello site, and returns a Site Recovery job object.</span></span> <span data-ttu-id="e15b5-162">Merhaba iş toocomplete için bekleyin ve o hello işi başarıyla tamamlandı doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="e15b5-162">Wait for hello job toocomplete and verify that hello job completed successfully.</span></span>

    <span data-ttu-id="e15b5-163">Merhaba iş nesnesini almak ve böylelikle hello Get-AzureRmSiteRecoveryJob cmdlet'ini kullanarak hello hello işinin geçerli durumunu denetleyin.</span><span class="sxs-lookup"><span data-stu-id="e15b5-163">You can retrieve hello job object, and thereby check hello current status of hello job, by using hello Get-AzureRmSiteRecoveryJob cmdlet.</span></span>
2. <span data-ttu-id="e15b5-164">Oluşturun ve aşağıdaki gibi hello site için bir kayıt anahtarını indirin:</span><span class="sxs-lookup"><span data-stu-id="e15b5-164">Generate and download a registration key for hello site, as follows:</span></span>

        $SiteIdentifier = Get-AzureRmSiteRecoverySite -Name $sitename | Select -ExpandProperty SiteIdentifier
        Get-AzureRmRecoveryServicesVaultSettingsFile -Vault $vault -SiteIdentifier $SiteIdentifier -SiteFriendlyName $sitename -Path $Path

    <span data-ttu-id="e15b5-165">Kopya hello anahtar toohello Hyper-V konak indirilir.</span><span class="sxs-lookup"><span data-stu-id="e15b5-165">Copy hello downloaded key toohello Hyper-V host.</span></span> <span data-ttu-id="e15b5-166">Merhaba anahtar tooregister hello Hyper-V ana bilgisayar toohello sitesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="e15b5-166">You need hello key tooregister hello Hyper-V host toohello site.</span></span>

## <a name="step-5-install-hello-azure-site-recovery-provider-and-azure-recovery-services-agent-on-your-hyper-v-host"></a><span data-ttu-id="e15b5-167">5. adım: hello Azure Site Recovery sağlayıcısı ve Azure kurtarma Hizmetleri Aracısı, Hyper-V konak üzerinde yükleyin</span><span class="sxs-lookup"><span data-stu-id="e15b5-167">Step 5: Install hello Azure Site Recovery provider and Azure Recovery Services Agent on your Hyper-V host</span></span>
1. <span data-ttu-id="e15b5-168">Hello yükleyiciyi hello hello Sağlayıcısı'ndan en son sürümü karşıdan [Microsoft](https://aka.ms/downloaddra).</span><span class="sxs-lookup"><span data-stu-id="e15b5-168">Download hello installer for hello latest version of hello provider from [Microsoft](https://aka.ms/downloaddra).</span></span>
2. <span data-ttu-id="e15b5-169">Hyper-V ana bilgisayarınızda ve hello yükleme hello sonunda çalışma hello yükleyici toohello kayıt adımından devam edin.</span><span class="sxs-lookup"><span data-stu-id="e15b5-169">Run hello installer on your Hyper-V host, and at hello end of hello installation continue toohello registration step.</span></span>
3. <span data-ttu-id="e15b5-170">İstendiğinde, site kayıt anahtarını ve hello Hyper-V ana bilgisayar toohello sitenin tam kayıt hello indirilen sağlayın.</span><span class="sxs-lookup"><span data-stu-id="e15b5-170">When prompted, provide hello downloaded site registration key, and complete registration of hello Hyper-V host toohello site.</span></span>
4. <span data-ttu-id="e15b5-171">Merhaba aşağıdaki komutu kullanarak bu hello Hyper-V ana kayıtlı toohello site olduğunu doğrulayın:</span><span class="sxs-lookup"><span data-stu-id="e15b5-171">Verify that hello Hyper-V host is registered toohello site by using hello following command:</span></span>

        $server =  Get-AzureRmSiteRecoveryServer -FriendlyName $server-friendlyname

## <a name="step-6-create-a-replication-policy-and-associate-it-with-hello-protection-container"></a><span data-ttu-id="e15b5-172">6. adım: bir çoğaltma ilkesi oluşturun ve hello koruma kapsayıcısı ile ilişkilendirin</span><span class="sxs-lookup"><span data-stu-id="e15b5-172">Step 6: Create a replication policy and associate it with hello protection container</span></span>
1. <span data-ttu-id="e15b5-173">Bir çoğaltma ilkesi şu şekilde oluşturun:</span><span class="sxs-lookup"><span data-stu-id="e15b5-173">Create a replication policy as follows:</span></span>

        $ReplicationFrequencyInSeconds = "300";        #options are 30,300,900
        $PolicyName = “replicapolicy”
        $Recoverypoints = 6                    #specify hello number of recovery points
        $storageaccountID = Get-AzureRmStorageAccount -Name "mystorea" -ResourceGroupName "MyRG" | Select -ExpandProperty Id

        $PolicyResult = New-AzureRmSiteRecoveryPolicy -Name $PolicyName -ReplicationProvider “HyperVReplicaAzure” -ReplicationFrequencyInSeconds $ReplicationFrequencyInSeconds  -RecoveryPoints $Recoverypoints -ApplicationConsistentSnapshotFrequencyInHours 1 -RecoveryAzureStorageAccountId $storageaccountID

    <span data-ttu-id="e15b5-174">Onay hello hello çoğaltma ilkesi oluşturma başarılı iş tooensure döndürdü.</span><span class="sxs-lookup"><span data-stu-id="e15b5-174">Check hello returned job tooensure that hello replication policy creation succeeds.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="e15b5-175">Merhaba belirtilen depolama hesabı olması gerekir, Kurtarma Hizmetleri kasasıyla aynı Azure bölgesinde hello ve coğrafi çoğaltmanın etkinleştirilmiş olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="e15b5-175">hello storage account specified should be in hello same Azure region as your Recovery Services vault, and should have geo-replication enabled.</span></span>
   >
   > * <span data-ttu-id="e15b5-176">Merhaba depolama hesabı Azure Storage (Klasik) türünde kurtarma belirtilmişse, hello Yük Devretmesini makineler kurtarmak hello makine tooAzure Iaas (Klasik) korumalı.</span><span class="sxs-lookup"><span data-stu-id="e15b5-176">If hello specified Recovery storage account is of type Azure Storage (Classic), failover of hello protected machines recover hello machine tooAzure IaaS (Classic).</span></span>
   > * <span data-ttu-id="e15b5-177">Merhaba Kurtarma Depolama hesabı Azure Storage (Azure Resource Manager) türünü belirtilirse, hello Yük Devretmesini makineler kurtarmak hello makine tooAzure Iaas (Azure Resource Manager) korumalı.</span><span class="sxs-lookup"><span data-stu-id="e15b5-177">If hello specified Recovery storage account is of type Azure Storage (Azure Resource Manager), failover of hello protected machines recover hello machine tooAzure IaaS (Azure Resource Manager).</span></span>
   >
   >
2. <span data-ttu-id="e15b5-178">Merhaba koruma kapsayıcısı karşılık gelen toohello site, aşağıdaki gibi alın:</span><span class="sxs-lookup"><span data-stu-id="e15b5-178">Get hello protection container corresponding toohello site, as follows:</span></span>

        $protectionContainer = Get-AzureRmSiteRecoveryProtectionContainer
3. <span data-ttu-id="e15b5-179">Merhaba koruma kapsayıcısı Hello ilişkilendirmesini hello çoğaltma ilkesi, aşağıda gösterildiği gibi başlatın:</span><span class="sxs-lookup"><span data-stu-id="e15b5-179">Start hello association of hello protection container with hello replication policy, as follows:</span></span>

     <span data-ttu-id="e15b5-180">$Policy get-AzureRmSiteRecoveryPolicy - FriendlyName $PolicyName $associationJob = başlangıç AzureRmSiteRecoveryPolicyAssociationJob =-ilke $Policy - PrimaryProtectionContainer $protectionContainer</span><span class="sxs-lookup"><span data-stu-id="e15b5-180">$Policy = Get-AzureRmSiteRecoveryPolicy -FriendlyName $PolicyName   $associationJob  = Start-AzureRmSiteRecoveryPolicyAssociationJob -Policy $Policy -PrimaryProtectionContainer $protectionContainer</span></span>

   <span data-ttu-id="e15b5-181">Merhaba ilişkilendirme iş toocomplete için bekleyin ve başarıyla tamamlandığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="e15b5-181">Wait for hello association job toocomplete, and ensure that it completed successfully.</span></span>

## <a name="step-7-enable-protection-for-virtual-machines"></a><span data-ttu-id="e15b5-182">7. adım: sanal makineler için korumayı etkinleştir</span><span class="sxs-lookup"><span data-stu-id="e15b5-182">Step 7: Enable protection for virtual machines</span></span>
1. <span data-ttu-id="e15b5-183">Merhaba koruma varlık karşılık gelen toohello tooprotect, aşağıdaki gibi istediğiniz VM alın:</span><span class="sxs-lookup"><span data-stu-id="e15b5-183">Get hello protection entity corresponding toohello VM you want tooprotect, as follows:</span></span>

        $VMFriendlyName = "Fabrikam-app"                    #Name of hello VM
        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -ProtectionContainer $protectionContainer -FriendlyName $VMFriendlyName
2. <span data-ttu-id="e15b5-184">Merhaba sanal makine, aşağıdaki gibi koruma başlatın:</span><span class="sxs-lookup"><span data-stu-id="e15b5-184">Start protecting hello virtual machine, as follows:</span></span>

        $Ostype = "Windows"                                 # "Windows" or "Linux"
        $DRjob = Set-AzureRmSiteRecoveryProtectionEntity -ProtectionEntity $protectionEntity -Policy $Policy -Protection Enable -RecoveryAzureStorageAccountId $storageaccountID  -OS $OStype -OSDiskName $protectionEntity.Disks[0].Name

   > [!IMPORTANT]
   > <span data-ttu-id="e15b5-185">Merhaba belirtilen depolama hesabı olması gerekir, Kurtarma Hizmetleri kasasıyla aynı Azure bölgesinde hello ve coğrafi çoğaltmanın etkinleştirilmiş olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="e15b5-185">hello storage account specified should be in hello same Azure region as your Recovery Services vault, and should have geo-replication enabled.</span></span>
   >
   > * <span data-ttu-id="e15b5-186">Merhaba depolama hesabı Azure Storage (Klasik) türünde kurtarma belirtilmişse, hello Yük Devretmesini makineler kurtarmak hello makine tooAzure Iaas (Klasik) korumalı.</span><span class="sxs-lookup"><span data-stu-id="e15b5-186">If hello specified Recovery storage account is of type Azure Storage (Classic), failover of hello protected machines recover hello machine tooAzure IaaS (Classic).</span></span>
   > * <span data-ttu-id="e15b5-187">Merhaba Kurtarma Depolama hesabı Azure Storage (Azure Resource Manager) türünü belirtilirse, hello Yük Devretmesini makineler kurtarmak hello makine tooAzure Iaas (Azure Resource Manager) korumalı.</span><span class="sxs-lookup"><span data-stu-id="e15b5-187">If hello specified Recovery storage account is of type Azure Storage (Azure Resource Manager), failover of hello protected machines recover hello machine tooAzure IaaS (Azure Resource Manager).</span></span>
   >
   > <span data-ttu-id="e15b5-188">Merhaba koruduğunuz VM birden fazla disk ekli tooit, hello kullanarak hello işletim sistemi diski belirtmek varsa *OSDiskName* parametresi.</span><span class="sxs-lookup"><span data-stu-id="e15b5-188">If hello VM you are protecting has more than one disk attached tooit, specify hello operating system disk by using hello *OSDiskName* parameter.</span></span>
   >
   >
3. <span data-ttu-id="e15b5-189">Merhaba sanal makineleri tooreach için korumalı bir duruma hello ilk çoğaltma sonrasında bekleyin.</span><span class="sxs-lookup"><span data-stu-id="e15b5-189">Wait for hello virtual machines tooreach a protected state after hello initial replication.</span></span> <span data-ttu-id="e15b5-190">Bu, çoğaltılmış verileri toobe hello miktarı gibi etkenlere bağlı olarak uzun sürebilir ve Yukarı Akış bant tooAzure hello.</span><span class="sxs-lookup"><span data-stu-id="e15b5-190">This can take a while, depending on factors such as hello amount of data toobe replicated and hello available upstream bandwidth tooAzure.</span></span> <span data-ttu-id="e15b5-191">aşağıdaki gibi Hello iş durumu ve StateDescription hello korumalı bir duruma ulaşmadan VM güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="e15b5-191">hello job State and StateDescription are updated as follows, upon hello VM reaching a protected state.</span></span>

        PS C:\> $DRjob = Get-AzureRmSiteRecoveryJob -Job $DRjob

        PS C:\> $DRjob | Select-Object -ExpandProperty State
        Succeeded

        PS C:\> $DRjob | Select-Object -ExpandProperty StateDescription
        Completed
4. <span data-ttu-id="e15b5-192">Merhaba VM rol boyutu ve hello Azure ağ tooattach hello sanal makinenin ağ arabirimi kartları tooupon yük devretme gibi kurtarma özelliklerini güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="e15b5-192">Update recovery properties, such as hello VM role size, and hello Azure network tooattach hello virtual machine's network interface cards tooupon failover.</span></span>

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



## <a name="step-8-run-a-test-failover"></a><span data-ttu-id="e15b5-193">8. adım: yük devretme testi çalıştırma</span><span class="sxs-lookup"><span data-stu-id="e15b5-193">Step 8: Run a test failover</span></span>
1. <span data-ttu-id="e15b5-194">Bir test yük devretme işini çalıştırmak için şunları yapın:</span><span class="sxs-lookup"><span data-stu-id="e15b5-194">Run a test failover job, as follows:</span></span>

        $nw = Get-AzureRmVirtualNetwork -Name "TestFailoverNw" -ResourceGroupName "MyRG" #Specify Azure vnet name and resource group

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -FriendlyName $VMFriendlyName -ProtectionContainer $protectionContainer

        $TFjob = Start-AzureRmSiteRecoveryTestFailoverJob -ProtectionEntity $protectionEntity -Direction PrimaryToRecovery -AzureVMNetworkId $nw.Id
2. <span data-ttu-id="e15b5-195">Azure'da VM oluşturulan hello test doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="e15b5-195">Verify that hello test VM is created in Azure.</span></span> <span data-ttu-id="e15b5-196">(Merhaba test yük devretme işini, Azure'da hello test VM oluşturduktan sonra askıya alındı.</span><span class="sxs-lookup"><span data-stu-id="e15b5-196">(hello test failover job is suspended, after creating hello test VM in Azure.</span></span> <span data-ttu-id="e15b5-197">Merhaba iş hello işi sırasında oluşturulan hello artefacts hello sonraki adımda gösterildiği gibi temizleniyor tarafından tamamlar.)</span><span class="sxs-lookup"><span data-stu-id="e15b5-197">hello job completes by cleaning up hello created artefacts upon resuming hello job, as illustrated in hello next step.)</span></span>
3. <span data-ttu-id="e15b5-198">Tam hello yük devretme, aşağıdaki gibi test edin:</span><span class="sxs-lookup"><span data-stu-id="e15b5-198">Complete hello test failover, as follows:</span></span>

        $TFjob = Resume-AzureRmSiteRecoveryJob -Job $TFjob

## <a name="next-steps"></a><span data-ttu-id="e15b5-199">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="e15b5-199">Next Steps</span></span>
<span data-ttu-id="e15b5-200">[Daha fazla bilgi](https://msdn.microsoft.com/library/azure/mt637930.aspx) Azure Site Recovery ile Azure Resource Manager PowerShell cmdlet'leri hakkında.</span><span class="sxs-lookup"><span data-stu-id="e15b5-200">[Read more](https://msdn.microsoft.com/library/azure/mt637930.aspx) about Azure Site Recovery with Azure Resource Manager PowerShell cmdlets.</span></span>
