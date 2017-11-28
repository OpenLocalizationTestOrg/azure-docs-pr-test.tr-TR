---
title: aaaMigrate tooResource Manager PowerShell ile | Microsoft Docs
description: "Bu makalede hello platform desteklenen geçiş Iaas kaynakların sanal makineleri (VM'ler), sanal ağlar (Vnet'ler) ve depolama hesapları gibi Klasik tooAzure Resource Manager (ARM) Azure PowerShell komutlarını kullanarak anlatılmaktadır"
services: virtual-machines-windows
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 2b3dff9b-2e99-4556-acc5-d75ef234af9c
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: kasing
ms.openlocfilehash: b5b2987da292f1c241be71a354b0c2e1a96a07c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-iaas-resources-from-classic-tooazure-resource-manager-by-using-azure-powershell"></a><span data-ttu-id="2893a-103">Iaas kaynaklarına Klasik tooAzure Resource Manager Azure PowerShell kullanarak geçirme</span><span class="sxs-lookup"><span data-stu-id="2893a-103">Migrate IaaS resources from classic tooAzure Resource Manager by using Azure PowerShell</span></span>
<span data-ttu-id="2893a-104">Bu adımlar nasıl hello Klasik dağıtım modeli toohello Azure Resource Manager dağıtım modeli hizmet (Iaas) kaynaklardan olarak toomigrate altyapı toouse Azure PowerShell komutları gösterir.</span><span class="sxs-lookup"><span data-stu-id="2893a-104">These steps show you how toouse Azure PowerShell commands toomigrate infrastructure as a service (IaaS) resources from hello classic deployment model toohello Azure Resource Manager deployment model.</span></span>

<span data-ttu-id="2893a-105">İsterseniz, ayrıca kaynakları hello kullanarak geçirebileceğiniz [Azure komut satırı arabirimi (Azure CLI)](../linux/migration-classic-resource-manager-cli.md).</span><span class="sxs-lookup"><span data-stu-id="2893a-105">If you want, you can also migrate resources by using hello [Azure Command Line Interface (Azure CLI)](../linux/migration-classic-resource-manager-cli.md).</span></span>

* <span data-ttu-id="2893a-106">Desteklenen geçiş senaryoları hakkında daha fazla bilgiler için bkz: [Klasik tooAzure Resource Manager Iaas kaynaklardan Platform desteklenen geçişini](migration-classic-resource-manager-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2893a-106">For background on supported migration scenarios, see [Platform-supported migration of IaaS resources from classic tooAzure Resource Manager](migration-classic-resource-manager-overview.md).</span></span>
* <span data-ttu-id="2893a-107">Ayrıntılı yönergeler ve bir geçiş kılavuz için bkz: [teknik ya ilişkin ayrıntılar platform desteklenen geçiş Klasik tooAzure Kaynak Yöneticisi'nden](migration-classic-resource-manager-deep-dive.md).</span><span class="sxs-lookup"><span data-stu-id="2893a-107">For detailed guidance and a migration walkthrough, see [Technical deep dive on platform-supported migration from classic tooAzure Resource Manager](migration-classic-resource-manager-deep-dive.md).</span></span>
* [<span data-ttu-id="2893a-108">En sık karşılaşılan geçiş hatalarını gözden geçirme</span><span class="sxs-lookup"><span data-stu-id="2893a-108">Review most common migration errors</span></span>](migration-classic-resource-manager-errors.md)

<br>
<span data-ttu-id="2893a-109">Adımları bir geçiş işlemi sırasında yürütülen toobe gereken bir akış çizelgesi tooidentify hello siparişi İşte</span><span class="sxs-lookup"><span data-stu-id="2893a-109">Here is a flowchart tooidentify hello order in which steps need toobe executed during a migration process</span></span>

![Merhaba geçiş adımlarını gösteren ekran görüntüsü](media/migration-classic-resource-manager/migration-flow.png)

## <a name="step-1-plan-for-migration"></a><span data-ttu-id="2893a-111">1. adım: geçişini planlama</span><span class="sxs-lookup"><span data-stu-id="2893a-111">Step 1: Plan for migration</span></span>
<span data-ttu-id="2893a-112">Klasik tooResource Yöneticisi geçirme Iaas kaynaklardan değerlendirirken öneririz birkaç en iyi uygulamalar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="2893a-112">Here are a few best practices that we recommend as you evaluate migrating IaaS resources from classic tooResource Manager:</span></span>

* <span data-ttu-id="2893a-113">Merhaba okuma [desteklenen ve desteklenmeyen özellikler ve yapılandırmalar](migration-classic-resource-manager-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2893a-113">Read through hello [supported and unsupported features and configurations](migration-classic-resource-manager-overview.md).</span></span> <span data-ttu-id="2893a-114">Desteklenmeyen yapılandırmaları veya özellikleri kullanan sanal makineler varsa, hello yapılandırma/özellik destek toobe duyurdu için beklemenizi öneririz.</span><span class="sxs-lookup"><span data-stu-id="2893a-114">If you have virtual machines that use unsupported configurations or features, we recommend that you wait for hello configuration/feature support toobe announced.</span></span> <span data-ttu-id="2893a-115">Alternatif olarak, gereksinimlerinize uygun değilse, bu özelliği kaldırmak veya yapılandırma tooenable geçişin dışına taşıyın.</span><span class="sxs-lookup"><span data-stu-id="2893a-115">Alternatively, if it suits your needs, remove that feature or move out of that configuration tooenable migration.</span></span>
* <span data-ttu-id="2893a-116">Bugün, altyapı ve uygulamalarınızı dağıtma komut otomatik değilse, geçiş için bu komut dosyalarını kullanarak toocreate benzer bir test Kurulum deneyin.</span><span class="sxs-lookup"><span data-stu-id="2893a-116">If you have automated scripts that deploy your infrastructure and applications today, try toocreate a similar test setup by using those scripts for migration.</span></span> <span data-ttu-id="2893a-117">Alternatif olarak, örnek ortamları hello Azure portal kullanarak ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2893a-117">Alternatively, you can set up sample environments by using hello Azure portal.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2893a-118">Uygulama ağ geçitleri, Klasik tooResource Yöneticisi geçiş için şu anda desteklenmemektedir.</span><span class="sxs-lookup"><span data-stu-id="2893a-118">Application Gateways are not currently supported for migration from classic tooResource Manager.</span></span> <span data-ttu-id="2893a-119">toomigrate bir uygulama ağ geçidi ile klasik sanal ağ hazırlama işlemi toomove hello ağ çalıştırmadan önce hello ağ geçidi kaldırın.</span><span class="sxs-lookup"><span data-stu-id="2893a-119">toomigrate a classic virtual network with an Application gateway, remove hello gateway before running a Prepare operation toomove hello network.</span></span> <span data-ttu-id="2893a-120">Merhaba ağ geçidi Azure Kaynak Yöneticisi'nde hello geçişi tamamlandıktan sonra yeniden bağlanın.</span><span class="sxs-lookup"><span data-stu-id="2893a-120">After you complete hello migration, reconnect hello gateway in Azure Resource Manager.</span></span>
>
><span data-ttu-id="2893a-121">ExpressRoute ağ geçidi başka bir Abonelikteki tooExpressRoute devreler bağlanma otomatik olarak geçirilemez.</span><span class="sxs-lookup"><span data-stu-id="2893a-121">ExpressRoute gateways connecting tooExpressRoute circuits in another subscription cannot be migrated automatically.</span></span> <span data-ttu-id="2893a-122">Böyle durumlarda, hello ExpressRoute ağ geçidi kaldırın, hello sanal ağını geçirin ve hello ağ geçidi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="2893a-122">In such cases, remove hello ExpressRoute gateway, migrate hello virtual network and recreate hello gateway.</span></span> <span data-ttu-id="2893a-123">Lütfen bakın [geçirmek ExpressRoute bağlantı hattına ve hello Klasik toohello Resource Manager dağıtım modeli sanal ağlardan ilişkili](../../expressroute/expressroute-migration-classic-resource-manager.md) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="2893a-123">Please see [Migrate ExpressRoute circuits and associated virtual networks from hello classic toohello Resource Manager deployment model](../../expressroute/expressroute-migration-classic-resource-manager.md) for more information.</span></span>
>
>

## <a name="step-2-install-hello-latest-version-of-azure-powershell"></a><span data-ttu-id="2893a-124">2. adım: hello Azure PowerShell'in en son sürümünü yükleme</span><span class="sxs-lookup"><span data-stu-id="2893a-124">Step 2: Install hello latest version of Azure PowerShell</span></span>
<span data-ttu-id="2893a-125">İki ana seçeneğiniz tooinstall Azure PowerShell vardır: [PowerShell Galerisi](https://www.powershellgallery.com/profiles/azure-sdk/) veya [Web Platformu Yükleyicisi (Webpı)](http://aka.ms/webpi-azps).</span><span class="sxs-lookup"><span data-stu-id="2893a-125">There are two main options tooinstall Azure PowerShell: [PowerShell Gallery](https://www.powershellgallery.com/profiles/azure-sdk/) or [Web Platform Installer (WebPI)](http://aka.ms/webpi-azps).</span></span> <span data-ttu-id="2893a-126">Webpı aylık güncelleştirmeleri alır.</span><span class="sxs-lookup"><span data-stu-id="2893a-126">WebPI receives monthly updates.</span></span> <span data-ttu-id="2893a-127">PowerShell Galerisi sürekli güncelleştirmeleri alır.</span><span class="sxs-lookup"><span data-stu-id="2893a-127">PowerShell Gallery receives updates on a continuous basis.</span></span> <span data-ttu-id="2893a-128">Bu makalede, Azure PowerShell sürüm 2.1.0 temel alır.</span><span class="sxs-lookup"><span data-stu-id="2893a-128">This article is based on Azure PowerShell version 2.1.0.</span></span>

<span data-ttu-id="2893a-129">Yükleme yönergeleri için bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="2893a-129">For installation instructions, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<br>

## <a name="step-3-ensure-that-you-are-an-administrator-for-hello-subscription-in-azure-portal"></a><span data-ttu-id="2893a-130">3. adım: Azure portalında hello abonelik için bir yönetici olduğundan emin olun</span><span class="sxs-lookup"><span data-stu-id="2893a-130">Step 3: Ensure that you are an administrator for hello subscription in Azure portal</span></span>
<span data-ttu-id="2893a-131">tooperform bu geçiş hello hello aboneliğinin ortak yönetici olarak eklenmelidir [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="2893a-131">tooperform this migration, you must be added as a co-administrator for hello subscription in hello [Azure portal](https://portal.azure.com).</span></span>

1. <span data-ttu-id="2893a-132">Merhaba içine oturum [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="2893a-132">Sign into hello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="2893a-133">Merhaba Hub menüsünde seçin **abonelik**.</span><span class="sxs-lookup"><span data-stu-id="2893a-133">On hello Hub menu, select **Subscription**.</span></span> <span data-ttu-id="2893a-134">Göremiyorsanız, seçin **daha fazla hizmet**.</span><span class="sxs-lookup"><span data-stu-id="2893a-134">If you don't see it, select **More services**.</span></span>
3. <span data-ttu-id="2893a-135">Merhaba uygun abonelik girişini bulun, sonra hello Ara **MY ROL** alan.</span><span class="sxs-lookup"><span data-stu-id="2893a-135">Find hello appropriate subscription entry, then look at hello **MY ROLE** field.</span></span> <span data-ttu-id="2893a-136">Bir ortak yönetici için hello değer olmalıdır _Hesap Yöneticisi_.</span><span class="sxs-lookup"><span data-stu-id="2893a-136">For a co-administrator, hello value should be _Account admin_.</span></span>

<span data-ttu-id="2893a-137">Ardından mümkün tooadd bir ortak yönetici değilse, bir Hizmet Yöneticisi veya ortak yönetici için hello abonelik tooget kendiniz eklenen başvurun.</span><span class="sxs-lookup"><span data-stu-id="2893a-137">If you are not able tooadd a co-administrator, then contact a service administrator or co-administrator for hello subscription tooget yourself added.</span></span>   

## <a name="step-4-set-your-subscription-and-sign-up-for-migration"></a><span data-ttu-id="2893a-138">4. adım: aboneliğinizi ayarlamak ve geçiş için kaydolun</span><span class="sxs-lookup"><span data-stu-id="2893a-138">Step 4: Set your subscription and sign up for migration</span></span>
<span data-ttu-id="2893a-139">İlk olarak, bir PowerShell istemi başlatın.</span><span class="sxs-lookup"><span data-stu-id="2893a-139">First, start a PowerShell prompt.</span></span> <span data-ttu-id="2893a-140">Geçiş için her iki Klasik için ortamınızı kurma tooset gerekir ve Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="2893a-140">For migration, you need tooset up your environment for both classic and Resource Manager.</span></span>

<span data-ttu-id="2893a-141">Merhaba Resource Manager modeli için tooyour hesabında oturum açın.</span><span class="sxs-lookup"><span data-stu-id="2893a-141">Sign in tooyour account for hello Resource Manager model.</span></span>

```powershell
    Login-AzureRmAccount
```

<span data-ttu-id="2893a-142">Kullanılabilir abonelikler Hello komutu aşağıdaki hello kullanarak alın:</span><span class="sxs-lookup"><span data-stu-id="2893a-142">Get hello available subscriptions by using hello following command:</span></span>

```powershell
    Get-AzureRMSubscription | Sort Name | Select Name
```

<span data-ttu-id="2893a-143">Azure aboneliğiniz için hello geçerli oturum ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="2893a-143">Set your Azure subscription for hello current session.</span></span> <span data-ttu-id="2893a-144">Bu örnek kümeleri hello varsayılan abonelik adı çok**My Azure aboneliği**.</span><span class="sxs-lookup"><span data-stu-id="2893a-144">This example sets hello default subscription name too**My Azure Subscription**.</span></span> <span data-ttu-id="2893a-145">Merhaba örnek abonelik adı kendinizinkilerle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="2893a-145">Replace hello example subscription name with your own.</span></span>

```powershell
    Select-AzureRmSubscription –SubscriptionName "My Azure Subscription"
```

> [!NOTE]
> <span data-ttu-id="2893a-146">Kayıt tek seferlik bir adımdır, ancak geçişi denemeden önce bir kez yapmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="2893a-146">Registration is a one-time step, but you must do it once before attempting migration.</span></span> <span data-ttu-id="2893a-147">Kayıt olmadan, hata iletisi aşağıdaki hello bakın:</span><span class="sxs-lookup"><span data-stu-id="2893a-147">Without registering, you see hello following error message:</span></span>
>
> <span data-ttu-id="2893a-148">*BadRequest: Abonelik geçiş için kayıtlı değil.*</span><span class="sxs-lookup"><span data-stu-id="2893a-148">*BadRequest : Subscription is not registered for migration.*</span></span>
>
>

<span data-ttu-id="2893a-149">Merhaba geçiş kaynak sağlayıcısı ile komutu aşağıdaki hello kullanarak kaydedin:</span><span class="sxs-lookup"><span data-stu-id="2893a-149">Register with hello migration resource provider by using hello following command:</span></span>

```powershell
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.ClassicInfrastructureMigrate
```

<span data-ttu-id="2893a-150">Merhaba kayıt toofinish için beş dakika bekleyin.</span><span class="sxs-lookup"><span data-stu-id="2893a-150">Please wait five minutes for hello registration toofinish.</span></span> <span data-ttu-id="2893a-151">Komutu aşağıdaki hello kullanarak hello hello onay durumunu denetleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="2893a-151">You can check hello status of hello approval by using hello following command:</span></span>

```powershell
    Get-AzureRmResourceProvider -ProviderNamespace Microsoft.ClassicInfrastructureMigrate
```

<span data-ttu-id="2893a-152">RegistrationState olduğundan emin olun `Registered` devam etmeden önce.</span><span class="sxs-lookup"><span data-stu-id="2893a-152">Make sure that RegistrationState is `Registered` before you proceed.</span></span>

<span data-ttu-id="2893a-153">Şimdi oturum açma tooyour hesabı hello Klasik modeli için.</span><span class="sxs-lookup"><span data-stu-id="2893a-153">Now sign in tooyour account for hello classic model.</span></span>

```powershell
    Add-AzureAccount
```

<span data-ttu-id="2893a-154">Kullanılabilir abonelikler Hello komutu aşağıdaki hello kullanarak alın:</span><span class="sxs-lookup"><span data-stu-id="2893a-154">Get hello available subscriptions by using hello following command:</span></span>

```powershell
    Get-AzureSubscription | Sort SubscriptionName | Select SubscriptionName
```

<span data-ttu-id="2893a-155">Azure aboneliğiniz için hello geçerli oturum ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="2893a-155">Set your Azure subscription for hello current session.</span></span> <span data-ttu-id="2893a-156">Bu örnek hello varsayılan abonelik çok ayarlar**My Azure aboneliği**.</span><span class="sxs-lookup"><span data-stu-id="2893a-156">This example sets hello default subscription too**My Azure Subscription**.</span></span> <span data-ttu-id="2893a-157">Merhaba örnek abonelik adı kendinizinkilerle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="2893a-157">Replace hello example subscription name with your own.</span></span>

```powershell
    Select-AzureSubscription –SubscriptionName "My Azure Subscription"
```

<br>

## <a name="step-5-make-sure-you-have-enough-azure-resource-manager-virtual-machine-cores-in-hello-azure-region-of-your-current-deployment-or-vnet"></a><span data-ttu-id="2893a-158">5. adım: hello geçerli dağıtım veya VNET Azure bölgesi yeterli Azure Resource Manager sanal makinesi çekirdeğe sahip olduğunuzdan emin olun</span><span class="sxs-lookup"><span data-stu-id="2893a-158">Step 5: Make sure you have enough Azure Resource Manager Virtual Machine cores in hello Azure region of your current deployment or VNET</span></span>
<span data-ttu-id="2893a-159">PowerShell komut toocheck hello geçerli Azure Kaynak Yöneticisi'nde sahip çekirdek sayısı aşağıdaki hello kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2893a-159">You can use hello following PowerShell command toocheck hello current number of cores you have in Azure Resource Manager.</span></span> <span data-ttu-id="2893a-160">toolearn çekirdek kotaları hakkında daha fazla bilgi görmek [sınırları ve hello Azure Resource Manager](../../azure-subscription-service-limits.md#limits-and-the-azure-resource-manager).</span><span class="sxs-lookup"><span data-stu-id="2893a-160">toolearn more about core quotas, see [Limits and hello Azure Resource Manager](../../azure-subscription-service-limits.md#limits-and-the-azure-resource-manager).</span></span>

<span data-ttu-id="2893a-161">Bu örnek hello hello kullanılabilirliğini denetler **Batı ABD** bölge.</span><span class="sxs-lookup"><span data-stu-id="2893a-161">This example checks hello availability in hello **West US** region.</span></span> <span data-ttu-id="2893a-162">Merhaba örnek bölge adı kendinizinkilerle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="2893a-162">Replace hello example region name with your own.</span></span>

```powershell
Get-AzureRmVMUsage -Location "West US"
```

## <a name="step-6-run-commands-toomigrate-your-iaas-resources"></a><span data-ttu-id="2893a-163">6. adım: Iaas kaynaklarınızı komutları toomigrate çalıştırma</span><span class="sxs-lookup"><span data-stu-id="2893a-163">Step 6: Run commands toomigrate your IaaS resources</span></span>
> [!NOTE]
> <span data-ttu-id="2893a-164">Burada açıklanan tüm hello ıdempotent işlemleridir.</span><span class="sxs-lookup"><span data-stu-id="2893a-164">All hello operations described here are idempotent.</span></span> <span data-ttu-id="2893a-165">Desteklenmeyen bir özellik veya bir yapılandırma hatası başka bir sorun varsa, hello yeniden deneme öneririz hazırlamak, iptal etmek veya yürütme işlemi.</span><span class="sxs-lookup"><span data-stu-id="2893a-165">If you have a problem other than an unsupported feature or a configuration error, we recommend that you retry hello prepare, abort, or commit operation.</span></span> <span data-ttu-id="2893a-166">Merhaba platform sonra hello eylemi yeniden dener.</span><span class="sxs-lookup"><span data-stu-id="2893a-166">hello platform then tries hello action again.</span></span>
>
>

## <a name="step-61-option-1---migrate-virtual-machines-in-a-cloud-service-not-in-a-virtual-network"></a><span data-ttu-id="2893a-167">6.1. adım: 1. seçenek - sanal makineler bir bulut hizmetinde (değil, sanal ağ için) geçirme</span><span class="sxs-lookup"><span data-stu-id="2893a-167">Step 6.1: Option 1 - Migrate virtual machines in a cloud service (not in a virtual network)</span></span>
<span data-ttu-id="2893a-168">Komutu aşağıdaki hello kullanarak bulut Hizmetleri ve çekme hello bulut hizmeti toomigrate istediğiniz Get hello listesi.</span><span class="sxs-lookup"><span data-stu-id="2893a-168">Get hello list of cloud services by using hello following command, and then pick hello cloud service that you want toomigrate.</span></span> <span data-ttu-id="2893a-169">Merhaba VM'ler hello bulut hizmetindeki bir sanal ağ veya web veya çalışan rolleri varsa, hello komutu bir hata iletisi döndürür.</span><span class="sxs-lookup"><span data-stu-id="2893a-169">If hello VMs in hello cloud service are in a virtual network or if they have web or worker roles, hello command returns an error message.</span></span>

```powershell
    Get-AzureService | ft Servicename
```

<span data-ttu-id="2893a-170">Merhaba dağıtım adı hello bulut hizmeti için alın.</span><span class="sxs-lookup"><span data-stu-id="2893a-170">Get hello deployment name for hello cloud service.</span></span> <span data-ttu-id="2893a-171">Bu örnekte, hello hizmet adı olan **Hizmetim**.</span><span class="sxs-lookup"><span data-stu-id="2893a-171">In this example, hello service name is **My Service**.</span></span> <span data-ttu-id="2893a-172">Merhaba örnek hizmet adı, kendi hizmet adı ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="2893a-172">Replace hello example service name with your own service name.</span></span>

```powershell
    $serviceName = "My Service"
    $deployment = Get-AzureDeployment -ServiceName $serviceName
    $deploymentName = $deployment.DeploymentName
```

<span data-ttu-id="2893a-173">Merhaba sanal makineleri hello bulut hizmetinde geçiş için hazırlayın.</span><span class="sxs-lookup"><span data-stu-id="2893a-173">Prepare hello virtual machines in hello cloud service for migration.</span></span> <span data-ttu-id="2893a-174">Gelen iki seçenekleri toochoose sahip.</span><span class="sxs-lookup"><span data-stu-id="2893a-174">You have two options toochoose from.</span></span>

* <span data-ttu-id="2893a-175">**Seçenek 1. Merhaba VM'ler tooa platform tarafından oluşturulan sanal ağını geçirin**</span><span class="sxs-lookup"><span data-stu-id="2893a-175">**Option 1. Migrate hello VMs tooa platform-created virtual network**</span></span>

    <span data-ttu-id="2893a-176">Merhaba aşağıdaki komutları kullanarak hello bulut hizmeti geçirirseniz ilk olarak, doğrulama:</span><span class="sxs-lookup"><span data-stu-id="2893a-176">First, validate if you can migrate hello cloud service using hello following commands:</span></span>

    ```powershell
    $validate = Move-AzureService -Validate -ServiceName $serviceName `
        -DeploymentName $deploymentName -CreateNewVirtualNetwork
    $validate.ValidationMessages
    ```

    <span data-ttu-id="2893a-177">Merhaba önceki komutu tüm uyarıları ve geçiş engelleme hataları görüntüler.</span><span class="sxs-lookup"><span data-stu-id="2893a-177">hello preceding command displays any warnings and errors that block migration.</span></span> <span data-ttu-id="2893a-178">Doğrulama başarılı olduğunda sonra toohello üzerinde taşıyabilirsiniz **Prepare** . adım:</span><span class="sxs-lookup"><span data-stu-id="2893a-178">If validation is successful, then you can move on toohello **Prepare** step:</span></span>

    ```powershell
    Move-AzureService -Prepare -ServiceName $serviceName `
        -DeploymentName $deploymentName -CreateNewVirtualNetwork
    ```
* <span data-ttu-id="2893a-179">**Seçenek 2. Mevcut sanal ağda hello Resource Manager dağıtım modeli tooan geçirme**</span><span class="sxs-lookup"><span data-stu-id="2893a-179">**Option 2. Migrate tooan existing virtual network in hello Resource Manager deployment model**</span></span>

    <span data-ttu-id="2893a-180">Bu örnek kümeleri hello kaynak grubu adı çok**myResourceGroup**, sanal ağ adı çok hello**myVirtualNetwork** ve alt ağ adı çok hello**mySubNet**.</span><span class="sxs-lookup"><span data-stu-id="2893a-180">This example sets hello resource group name too**myResourceGroup**, hello virtual network name too**myVirtualNetwork** and hello subnet name too**mySubNet**.</span></span> <span data-ttu-id="2893a-181">Merhaba adları hello örnekte kendi kaynaklarını hello adlarıyla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="2893a-181">Replace hello names in hello example with hello names of your own resources.</span></span>

    ```powershell
    $existingVnetRGName = "myResourceGroup"
    $vnetName = "myVirtualNetwork"
    $subnetName = "mySubNet"
    ```

    <span data-ttu-id="2893a-182">İlk olarak, komutu aşağıdaki hello kullanarak hello sanal ağ geçirirseniz doğrulama:</span><span class="sxs-lookup"><span data-stu-id="2893a-182">First, validate if you can migrate hello virtual network using hello following command:</span></span>

    ```powershell
    $validate = Move-AzureService -Validate -ServiceName $serviceName `
        -DeploymentName $deploymentName -UseExistingVirtualNetwork -VirtualNetworkResourceGroupName $existingVnetRGName -VirtualNetworkName $vnetName -SubnetName $subnetName
    $validate.ValidationMessages
    ```

    <span data-ttu-id="2893a-183">Merhaba önceki komutu tüm uyarıları ve geçiş engelleme hataları görüntüler.</span><span class="sxs-lookup"><span data-stu-id="2893a-183">hello preceding command displays any warnings and errors that block migration.</span></span> <span data-ttu-id="2893a-184">Doğrulama başarılı olursa, hazırlama adımı aşağıdaki hello ile devam edebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="2893a-184">If validation is successful, then you can proceed with hello following Prepare step:</span></span>

    ```powershell
        Move-AzureService -Prepare -ServiceName $serviceName -DeploymentName $deploymentName `
        -UseExistingVirtualNetwork -VirtualNetworkResourceGroupName $existingVnetRGName `
        -VirtualNetworkName $vnetName -SubnetName $subnetName
    ```

<span data-ttu-id="2893a-185">Merhaba Hazırlama işlemi seçenekleri önceki hello birini kullanarak başarılı olduktan sonra hello VM'ler hello geçiş durumu sorgu.</span><span class="sxs-lookup"><span data-stu-id="2893a-185">After hello Prepare operation succeeds with either of hello preceding options, query hello migration state of hello VMs.</span></span> <span data-ttu-id="2893a-186">Hello olduklarından emin olun `Prepared` durumu.</span><span class="sxs-lookup"><span data-stu-id="2893a-186">Ensure that they are in hello `Prepared` state.</span></span>

<span data-ttu-id="2893a-187">Bu örnek kümeleri hello VM adı çok**myVM**.</span><span class="sxs-lookup"><span data-stu-id="2893a-187">This example sets hello VM name too**myVM**.</span></span> <span data-ttu-id="2893a-188">Merhaba örnek adı kendi VM adıyla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="2893a-188">Replace hello example name with your own VM name.</span></span>

```powershell
    $vmName = "myVM"
    $vm = Get-AzureVM -ServiceName $serviceName -Name $vmName
    $vm.VM.MigrationState
```

<span data-ttu-id="2893a-189">PowerShell veya hello Azure portal kullanarak kaynakları hazırlanmış hello için başlangıç yapılandırmasını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="2893a-189">Check hello configuration for hello prepared resources by using either PowerShell or hello Azure portal.</span></span> <span data-ttu-id="2893a-190">Geçiş için hazır olmayan ve toogo geri toohello eski durum istiyorsanız hello aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="2893a-190">If you are not ready for migration and you want toogo back toohello old state, use hello following command:</span></span>

```powershell
    Move-AzureService -Abort -ServiceName $serviceName -DeploymentName $deploymentName
```

<span data-ttu-id="2893a-191">Merhaba hazırlanan yapılandırma iyi görünüyorsa, ilerlemek ve komut aşağıdaki hello kullanarak hello kaynakları Yürüt:</span><span class="sxs-lookup"><span data-stu-id="2893a-191">If hello prepared configuration looks good, you can move forward and commit hello resources by using hello following command:</span></span>

```powershell
    Move-AzureService -Commit -ServiceName $serviceName -DeploymentName $deploymentName
```

## <a name="step-61-option-2---migrate-virtual-machines-in-a-virtual-network"></a><span data-ttu-id="2893a-192">6.1. adım: 2. seçenek - bir sanal ağdaki sanal makineleri geçirme</span><span class="sxs-lookup"><span data-stu-id="2893a-192">Step 6.1: Option 2 - Migrate virtual machines in a virtual network</span></span>

<span data-ttu-id="2893a-193">toomigrate sanal makinelere sanal bir ağa hello sanal ağ geçirme.</span><span class="sxs-lookup"><span data-stu-id="2893a-193">toomigrate virtual machines in a virtual network, you migrate hello virtual network.</span></span> <span data-ttu-id="2893a-194">Merhaba sanal makineleri otomatik olarak hello sanal ağ ile geçirin.</span><span class="sxs-lookup"><span data-stu-id="2893a-194">hello virtual machines automatically migrate with hello virtual network.</span></span> <span data-ttu-id="2893a-195">Çekme hello sanal ağ toomigrate istiyor.</span><span class="sxs-lookup"><span data-stu-id="2893a-195">Pick hello virtual network that you want toomigrate.</span></span>
> [!NOTE]
> <span data-ttu-id="2893a-196">[Tek Klasik sanal makineyi geçirmek](migrate-single-classic-to-resource-manager.md) diskleri yönetilen hello sanal makinenin hello VHD (işletim sistemi ve veri) dosyalarını kullanarak yeni bir kaynak yöneticisi sanal makine oluşturarak.</span><span class="sxs-lookup"><span data-stu-id="2893a-196">[Migrate single classic virtual machine](migrate-single-classic-to-resource-manager.md) by creating a new Resource Manager virtual machine with Managed Disks using hello VHD (OS and data) files of hello virtual machine.</span></span>
<br>

> [!NOTE]
> <span data-ttu-id="2893a-197">Merhaba sanal ağ adı ne hello gösterilenden farklı olabilir yeni portalı.</span><span class="sxs-lookup"><span data-stu-id="2893a-197">hello virtual network name might be different from what is shown in hello new Portal.</span></span> <span data-ttu-id="2893a-198">Merhaba yeni Azure Portal görüntüler hello adıyla `[vnet-name]` ancak hello gerçek sanal ağ adı türü `Group [resource-group-name] [vnet-name]`.</span><span class="sxs-lookup"><span data-stu-id="2893a-198">hello new Azure Portal displays hello name as `[vnet-name]` but hello actual virtual network name is of type `Group [resource-group-name] [vnet-name]`.</span></span> <span data-ttu-id="2893a-199">Geçiş, arama hello gerçek sanal ağ adı hello komutunu kullanarak önce `Get-AzureVnetSite | Select -Property Name` veya hello görüntüleyin eski Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="2893a-199">Before migrating, lookup hello actual virtual network name using hello command `Get-AzureVnetSite | Select -Property Name` or view it in hello old Azure Portal.</span></span> 

<span data-ttu-id="2893a-200">Bu örnek kümeleri hello sanal ağ adı çok**myVnet**.</span><span class="sxs-lookup"><span data-stu-id="2893a-200">This example sets hello virtual network name too**myVnet**.</span></span> <span data-ttu-id="2893a-201">Merhaba örnek sanal ağ adı kendinizinkilerle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="2893a-201">Replace hello example virtual network name with your own.</span></span>

```powershell
    $vnetName = "myVnet"
```

> [!NOTE]
> <span data-ttu-id="2893a-202">Merhaba sanal ağ ile desteklenmeyen yapılandırmalar web veya çalışan rolleri ya da sanal makineleri içeriyorsa, bir doğrulama hata iletisi alırsınız.</span><span class="sxs-lookup"><span data-stu-id="2893a-202">If hello virtual network contains web or worker roles, or VMs with unsupported configurations, you get a validation error message.</span></span>
>
>

<span data-ttu-id="2893a-203">Komutu aşağıdaki hello kullanarak hello sanal ağ geçirebilirsiniz, ilk olarak, doğrulama:</span><span class="sxs-lookup"><span data-stu-id="2893a-203">First, validate if you can migrate hello virtual network by using hello following command:</span></span>

```powershell
    Move-AzureVirtualNetwork -Validate -VirtualNetworkName $vnetName
```

<span data-ttu-id="2893a-204">Merhaba önceki komutu tüm uyarıları ve geçiş engelleme hataları görüntüler.</span><span class="sxs-lookup"><span data-stu-id="2893a-204">hello preceding command displays any warnings and errors that block migration.</span></span> <span data-ttu-id="2893a-205">Doğrulama başarılı olursa, hazırlama adımı aşağıdaki hello ile devam edebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="2893a-205">If validation is successful, then you can proceed with hello following Prepare step:</span></span>

```powershell
    Move-AzureVirtualNetwork -Prepare -VirtualNetworkName $vnetName
```

<span data-ttu-id="2893a-206">Sanal makineler Azure PowerShell veya hello Azure portal kullanarak hazırlanmış hello için başlangıç yapılandırmasını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="2893a-206">Check hello configuration for hello prepared virtual machines by using either Azure PowerShell or hello Azure portal.</span></span> <span data-ttu-id="2893a-207">Geçiş için hazır olmayan ve toogo geri toohello eski durum istiyorsanız hello aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="2893a-207">If you are not ready for migration and you want toogo back toohello old state, use hello following command:</span></span>

```powershell
    Move-AzureVirtualNetwork -Abort -VirtualNetworkName $vnetName
```

<span data-ttu-id="2893a-208">Merhaba hazırlanan yapılandırma iyi görünüyorsa, ilerlemek ve komut aşağıdaki hello kullanarak hello kaynakları Yürüt:</span><span class="sxs-lookup"><span data-stu-id="2893a-208">If hello prepared configuration looks good, you can move forward and commit hello resources by using hello following command:</span></span>

```powershell
    Move-AzureVirtualNetwork -Commit -VirtualNetworkName $vnetName
```

## <a name="step-62-migrate-a-storage-account"></a><span data-ttu-id="2893a-209">Adım 6.2 geçirme bir depolama hesabı</span><span class="sxs-lookup"><span data-stu-id="2893a-209">Step 6.2 Migrate a storage account</span></span>
<span data-ttu-id="2893a-210">Merhaba sanal makinelerin geçirilmesine bitirdiğinizde hello depolama hesapları geçirme öneririz.</span><span class="sxs-lookup"><span data-stu-id="2893a-210">Once you're done migrating hello virtual machines, we recommend you migrate hello storage accounts.</span></span>

<span data-ttu-id="2893a-211">Merhaba depolama hesabı geçirmeden önce önkoşul denetimleri önceki gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="2893a-211">Before you migrate hello storage account, please perform preceding prerequisite checks:</span></span>

* <span data-ttu-id="2893a-212">**Klasik sanal makineleri, diskler hello depolama hesabında depolanır**</span><span class="sxs-lookup"><span data-stu-id="2893a-212">**Migrate classic virtual machines whose disks are stored in hello storage account**</span></span>

    <span data-ttu-id="2893a-213">Önceki komutu tüm hello Klasik VM diskleri RoleName ve DiskName özelliklerini hello depolama hesabında döndürür.</span><span class="sxs-lookup"><span data-stu-id="2893a-213">Preceding command returns RoleName and DiskName properties of all hello classic VM disks in hello storage account.</span></span> <span data-ttu-id="2893a-214">RoleName bir diskin eklendiği hello sanal makine toowhich hello adıdır.</span><span class="sxs-lookup"><span data-stu-id="2893a-214">RoleName is hello name of hello virtual machine toowhich a disk is attached.</span></span> <span data-ttu-id="2893a-215">Komut önceki diskleri sonra olun bu diskleri eklenir, sanal makineleri toowhich geçirmeden önce geçirilir döndürürse hello depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="2893a-215">If preceding command returns disks then ensure that virtual machines toowhich these disks are attached are migrated before migrating hello storage account.</span></span>
    ```powershell
     $storageAccountName = 'yourStorageAccountName'
      Get-AzureDisk | where-Object {$_.MediaLink.Host.Contains($storageAccountName)} | Select-Object -ExpandProperty AttachedTo -Property `
      DiskName | Format-List -Property RoleName, DiskName

    ```
* <span data-ttu-id="2893a-216">**Merhaba depolama hesabında depolanan eklenmemiş Klasik VM diskleri silme**</span><span class="sxs-lookup"><span data-stu-id="2893a-216">**Delete unattached classic VM disks stored in hello storage account**</span></span>

    <span data-ttu-id="2893a-217">Merhaba depolama Klasik eklenmemiş VM diskleri komutu kullanarak hesap bulun:</span><span class="sxs-lookup"><span data-stu-id="2893a-217">Find unattached classic VM disks in hello storage account using following command:</span></span>

    ```powershell
        $storageAccountName = 'yourStorageAccountName'
        Get-AzureDisk | where-Object {$_.MediaLink.Host.Contains($storageAccountName)} | Where-Object -Property AttachedTo -EQ $null | Format-List -Property DiskName  

    ```
    <span data-ttu-id="2893a-218">Komut döndürür diskleri ardından komutu kullanarak bu diskleri silerseniz:</span><span class="sxs-lookup"><span data-stu-id="2893a-218">If above command returns disks then delete these disks using following command:</span></span>

    ```powershell
       Remove-AzureDisk -DiskName 'yourDiskName'
    ```
* <span data-ttu-id="2893a-219">**Sil VM görüntüleri Hello depolama hesabında depolanan**</span><span class="sxs-lookup"><span data-stu-id="2893a-219">**Delete VM images stored in hello storage account**</span></span>

    <span data-ttu-id="2893a-220">Önceki komutu tüm hello VM görüntüleri hello depolama hesabında depolanan işletim sistemi diski ile döndürür.</span><span class="sxs-lookup"><span data-stu-id="2893a-220">Preceding command returns all hello VM images with OS disk stored in hello storage account.</span></span>
     ```powershell
        Get-AzureVmImage | Where-Object { $_.OSDiskConfiguration.MediaLink -ne $null -and $_.OSDiskConfiguration.MediaLink.Host.Contains($storageAccountName)`
                                } | Select-Object -Property ImageName, ImageLabel
     ```
     <span data-ttu-id="2893a-221">Komut önceki hello depolama hesabında depolanan veri diskleri içeren tüm hello VM görüntüleri döndürür.</span><span class="sxs-lookup"><span data-stu-id="2893a-221">Preceding command returns all hello VM images with data disks stored in hello storage account.</span></span>
     ```powershell

        Get-AzureVmImage | Where-Object {$_.DataDiskConfigurations -ne $null `
                                         -and ($_.DataDiskConfigurations | Where-Object {$_.MediaLink -ne $null -and $_.MediaLink.Host.Contains($storageAccountName)}).Count -gt 0 `
                                        } | Select-Object -Property ImageName, ImageLabel
     ```
    <span data-ttu-id="2893a-222">Önceki komutu kullandıktan komutları tarafından döndürülen tüm hello VM görüntüleri silin:</span><span class="sxs-lookup"><span data-stu-id="2893a-222">Delete all hello VM images returned by above commands using preceding command:</span></span>
    ```powershell
    Remove-AzureVMImage -ImageName 'yourImageName'
    ```

<span data-ttu-id="2893a-223">Her Depolama hesabı geçiş için komutu aşağıdaki hello kullanarak doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="2893a-223">Validate each storage account for migration by using hello following command.</span></span> <span data-ttu-id="2893a-224">Bu örnekte, hello depolama hesabı adı olan **myStorageAccount**.</span><span class="sxs-lookup"><span data-stu-id="2893a-224">In this example, hello storage account name is **myStorageAccount**.</span></span> <span data-ttu-id="2893a-225">Merhaba örnek adı hello kendi depolama hesabınızın adıyla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="2893a-225">Replace hello example name with hello name of your own storage account.</span></span>

```powershell
    $storageAccountName = "myStorageAccount"
    Move-AzureStorageAccount -Validate -StorageAccountName $storageAccountName
```

<span data-ttu-id="2893a-226">Geçiş için tooPrepare hello depolama hesabı sonraki adımdır</span><span class="sxs-lookup"><span data-stu-id="2893a-226">Next step is tooPrepare hello storage account for migration</span></span>

```powershell
    $storageAccountName = "myStorageAccount"
    Move-AzureStorageAccount -Prepare -StorageAccountName $storageAccountName
```

<span data-ttu-id="2893a-227">Depolama hesabı Azure PowerShell veya hello Azure portal kullanarak hazırlanmış hello için başlangıç yapılandırmasını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="2893a-227">Check hello configuration for hello prepared storage account by using either Azure PowerShell or hello Azure portal.</span></span> <span data-ttu-id="2893a-228">Geçiş için hazır olmayan ve toogo geri toohello eski durum istiyorsanız hello aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="2893a-228">If you are not ready for migration and you want toogo back toohello old state, use hello following command:</span></span>

```powershell
    Move-AzureStorageAccount -Abort -StorageAccountName $storageAccountName
```

<span data-ttu-id="2893a-229">Merhaba hazırlanan yapılandırma iyi görünüyorsa, ilerlemek ve komut aşağıdaki hello kullanarak hello kaynakları Yürüt:</span><span class="sxs-lookup"><span data-stu-id="2893a-229">If hello prepared configuration looks good, you can move forward and commit hello resources by using hello following command:</span></span>

```powershell
    Move-AzureStorageAccount -Commit -StorageAccountName $storageAccountName
```

## <a name="next-steps"></a><span data-ttu-id="2893a-230">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2893a-230">Next steps</span></span>
* [<span data-ttu-id="2893a-231">Klasik tooAzure Resource Manager Iaas kaynaklardan platform desteklenen geçişini genel bakış</span><span class="sxs-lookup"><span data-stu-id="2893a-231">Overview of platform-supported migration of IaaS resources from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="2893a-232">Teknik ya ilişkin ayrıntılar platform desteklenen geçiş Klasik tooAzure Kaynak Yöneticisi'nden</span><span class="sxs-lookup"><span data-stu-id="2893a-232">Technical deep dive on platform-supported migration from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-deep-dive.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="2893a-233">Iaas kaynaklardan Klasik tooAzure Kaynak Yöneticisi geçişini planlama</span><span class="sxs-lookup"><span data-stu-id="2893a-233">Planning for migration of IaaS resources from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-plan.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="2893a-234">CLI toomigrate Iaas kaynaklarına Klasik tooAzure Kaynak Yöneticisi'ni kullanın</span><span class="sxs-lookup"><span data-stu-id="2893a-234">Use CLI toomigrate IaaS resources from classic tooAzure Resource Manager</span></span>](../linux/migration-classic-resource-manager-cli.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="2893a-235">Iaas kaynaklardan Klasik tooAzure Kaynak Yöneticisi geçişini ile Yardım için topluluk araçları</span><span class="sxs-lookup"><span data-stu-id="2893a-235">Community tools for assisting with migration of IaaS resources from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-community-tools.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="2893a-236">En sık karşılaşılan geçiş hatalarını gözden geçirme</span><span class="sxs-lookup"><span data-stu-id="2893a-236">Review most common migration errors</span></span>](migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="2893a-237">Gözden geçirme hello en sık Klasik tooAzure Kaynak Yöneticisi geçirme Iaas kaynaklardan hakkında sorular</span><span class="sxs-lookup"><span data-stu-id="2893a-237">Review hello most frequently asked questions about migrating IaaS resources from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-faq.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
