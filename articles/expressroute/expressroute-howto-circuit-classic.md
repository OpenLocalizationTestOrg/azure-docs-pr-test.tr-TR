---
title: "Oluşturma ve bir expressroute bağlantı hattı değiştirme: PowerShell: Azure Klasik | Microsoft Docs"
description: "Bu makalede, oluşturma ve bir expressroute bağlantı hattı sağlama hello adım adım anlatılmaktadır. Bu makalede ayrıca, nasıl toocheck hello durumu, güncelleştirme veya silme ve hattınız yetkisini kaldırma gösterir."
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 0134d242-6459-4dec-a2f1-4657c3bc8b23
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/21/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: 9897c88776a2153ba22aa9ff328becb9f12b660b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-an-expressroute-circuit-using-powershell-classic"></a><span data-ttu-id="7e541-104">Oluşturma ve PowerShell (Klasik) kullanarak bir expressroute bağlantı hattı değiştirme</span><span class="sxs-lookup"><span data-stu-id="7e541-104">Create and modify an ExpressRoute circuit using PowerShell (classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7e541-105">Azure portal</span><span class="sxs-lookup"><span data-stu-id="7e541-105">Azure portal</span></span>](expressroute-howto-circuit-portal-resource-manager.md)
> * [<span data-ttu-id="7e541-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7e541-106">PowerShell</span></span>](expressroute-howto-circuit-arm.md)
> * [<span data-ttu-id="7e541-107">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="7e541-107">Azure CLI</span></span>](howto-circuit-cli.md)
> * [<span data-ttu-id="7e541-108">Video - Azure portalı</span><span class="sxs-lookup"><span data-stu-id="7e541-108">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [<span data-ttu-id="7e541-109">PowerShell (klasik)</span><span class="sxs-lookup"><span data-stu-id="7e541-109">PowerShell (classic)</span></span>](expressroute-howto-circuit-classic.md)
>

<span data-ttu-id="7e541-110">Bu makalede PowerShell cmdlet'leri ve hello Klasik dağıtım modeli kullanarak bir Azure expressroute bağlantı hattı hello adımları toocreate anlatılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="7e541-110">This article walks you through hello steps toocreate an Azure ExpressRoute circuit by using PowerShell cmdlets and hello classic deployment model.</span></span> <span data-ttu-id="7e541-111">Bu makalede ayrıca, nasıl toocheck hello durumu, güncelleştirme veya silme ve bir expressroute bağlantı hattı yetkisini kaldırma gösterir.</span><span class="sxs-lookup"><span data-stu-id="7e541-111">This article also shows you how toocheck hello status, update, or delete and deprovision an ExpressRoute circuit.</span></span>

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]


<span data-ttu-id="7e541-112">**Azure dağıtım modelleri hakkında**</span><span class="sxs-lookup"><span data-stu-id="7e541-112">**About Azure deployment models**</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="before-you-begin"></a><span data-ttu-id="7e541-113">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="7e541-113">Before you begin</span></span>
### <a name="step-1-review-hello-prerequisites-and-workflow-articles"></a><span data-ttu-id="7e541-114">1. Adım</span><span class="sxs-lookup"><span data-stu-id="7e541-114">Step 1.</span></span> <span data-ttu-id="7e541-115">Merhaba önkoşulları ve iş akışı makaleleri gözden geçirin</span><span class="sxs-lookup"><span data-stu-id="7e541-115">Review hello prerequisites and workflow articles</span></span>
<span data-ttu-id="7e541-116">Merhaba gözden geçirdiğinizden emin olun [Önkoşullar](expressroute-prerequisites.md) ve [iş akışları](expressroute-workflows.md) yapılandırmaya başlamadan önce.</span><span class="sxs-lookup"><span data-stu-id="7e541-116">Make sure that you have reviewed hello [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>  

### <a name="step-2-install-hello-latest-versions-of-hello-azure-service-management-sm-powershell-modules"></a><span data-ttu-id="7e541-117">2. Adım</span><span class="sxs-lookup"><span data-stu-id="7e541-117">Step 2.</span></span> <span data-ttu-id="7e541-118">Merhaba hello Azure Hizmet Yönetimi (SM) PowerShell modülleri en son sürümlerini yükleyin</span><span class="sxs-lookup"><span data-stu-id="7e541-118">Install hello latest versions of hello Azure Service Management (SM) PowerShell modules</span></span>
<span data-ttu-id="7e541-119">Merhaba yönergeleri izleyin [Azure PowerShell cmdlet'leri ile çalışmaya başlama](/powershell/azure/overview) nasıl hakkında adım adım yönergeler için tooconfigure bilgisayar toouse hello Azure PowerShell modüllerinizi.</span><span class="sxs-lookup"><span data-stu-id="7e541-119">Follow hello instructions in [Getting started with Azure PowerShell cmdlets](/powershell/azure/overview) for step-by-step guidance on how tooconfigure your computer toouse hello Azure PowerShell modules.</span></span>

### <a name="step-3-log-in-tooyour-azure-account-and-select-a-subscription"></a><span data-ttu-id="7e541-120">3. Adım</span><span class="sxs-lookup"><span data-stu-id="7e541-120">Step 3.</span></span> <span data-ttu-id="7e541-121">Tooyour Azure hesabı oturum ve bir abonelik seçin</span><span class="sxs-lookup"><span data-stu-id="7e541-121">Log in tooyour Azure account and select a subscription</span></span>
1. <span data-ttu-id="7e541-122">Yükseltilmiş haklarla PowerShell Konsolunuzu açın ve tooyour hesap bağlanın.</span><span class="sxs-lookup"><span data-stu-id="7e541-122">Open your PowerShell console with elevated rights and connect tooyour account.</span></span> <span data-ttu-id="7e541-123">Bağlandığınız örnek toohelp aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="7e541-123">Use hello following example toohelp you connect:</span></span>

        Login-AzureRmAccount

2. <span data-ttu-id="7e541-124">Merhaba hesabının Hello abonelikleri kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="7e541-124">Check hello subscriptions for hello account.</span></span>

        Get-AzureRmSubscription

3. <span data-ttu-id="7e541-125">Birden fazla aboneliğiniz varsa, toouse istediğiniz hello aboneliği seçin.</span><span class="sxs-lookup"><span data-stu-id="7e541-125">If you have more than one subscription, select hello subscription that you want toouse.</span></span>

        Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"

4. <span data-ttu-id="7e541-126">Ardından, aşağıdaki cmdlet'i tooadd hello Azure aboneliği tooPowerShell hello Klasik dağıtım modeli için kullanın.</span><span class="sxs-lookup"><span data-stu-id="7e541-126">Next, use hello following cmdlet tooadd your Azure subscription tooPowerShell for hello classic deployment model.</span></span>

        Add-AzureAccount

## <a name="create-and-provision-an-expressroute-circuit"></a><span data-ttu-id="7e541-127">Oluşturma ve bir expressroute bağlantı hattı sağlama</span><span class="sxs-lookup"><span data-stu-id="7e541-127">Create and provision an ExpressRoute circuit</span></span>
### <a name="step-1-import-hello-powershell-modules-for-expressroute"></a><span data-ttu-id="7e541-128">1. Adım</span><span class="sxs-lookup"><span data-stu-id="7e541-128">Step 1.</span></span> <span data-ttu-id="7e541-129">ExpressRoute için Hello PowerShell modülleri alın</span><span class="sxs-lookup"><span data-stu-id="7e541-129">Import hello PowerShell modules for ExpressRoute</span></span>
 <span data-ttu-id="7e541-130">Zaten yapmadıysanız, sipariş toostart hello ExpressRoute cmdlet'lerini kullanmaya hello PowerShell oturumunda hello Azure ve ExpressRoute modülleri almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="7e541-130">If you have not already done so, you must import hello Azure and ExpressRoute modules into hello PowerShell session in order toostart using hello ExpressRoute cmdlets.</span></span> <span data-ttu-id="7e541-131">Merhaba modülleri içe hello oldukları konumu tooon yerel bilgisayarınızda yüklü.</span><span class="sxs-lookup"><span data-stu-id="7e541-131">You import hello modules from hello location that they were installed tooon your local computer.</span></span> <span data-ttu-id="7e541-132">Tooinstall hello modülleri kullanılan Hello yöntemine bağlı olarak, başlangıç konumu aşağıdaki örnekte gösterildiği hello farklı olabilir.</span><span class="sxs-lookup"><span data-stu-id="7e541-132">Depending on hello method you used tooinstall hello modules, hello location may be different than hello following example shows.</span></span> <span data-ttu-id="7e541-133">Merhaba örneği gerekiyorsa değiştirin.</span><span class="sxs-lookup"><span data-stu-id="7e541-133">Modify hello example if necessary.</span></span>  

    Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
    Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'

### <a name="step-2-get-hello-list-of-supported-providers-locations-and-bandwidths"></a><span data-ttu-id="7e541-134">2. Adım</span><span class="sxs-lookup"><span data-stu-id="7e541-134">Step 2.</span></span> <span data-ttu-id="7e541-135">Desteklenen sağlayıcılar, konumları ve bant genişlikleri Hello listesini alma</span><span class="sxs-lookup"><span data-stu-id="7e541-135">Get hello list of supported providers, locations, and bandwidths</span></span>
<span data-ttu-id="7e541-136">Bir expressroute bağlantı hattı oluşturmadan önce desteklenen bağlantı sağlayıcıları, konumları ve bant genişliği seçenekleri hello listesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="7e541-136">Before you create an ExpressRoute circuit, you need hello list of supported connectivity providers, locations, and bandwidth options.</span></span>

<span data-ttu-id="7e541-137">PowerShell cmdlet hello `Get-AzureDedicatedCircuitServiceProvider` , sonraki adımlarda kullanacağınız bu bilgiler verir:</span><span class="sxs-lookup"><span data-stu-id="7e541-137">hello PowerShell cmdlet `Get-AzureDedicatedCircuitServiceProvider` returns this information, which you’ll use in later steps:</span></span>

    Get-AzureDedicatedCircuitServiceProvider

<span data-ttu-id="7e541-138">Bağlantı sağlayıcınız listelenip toosee kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="7e541-138">Check toosee if your connectivity provider is listed there.</span></span> <span data-ttu-id="7e541-139">Bir bağlantı hattı oluşturduğunuzda, daha sonra gerekir çünkü aşağıdaki bilgilerle hello not edin:</span><span class="sxs-lookup"><span data-stu-id="7e541-139">Make a note of hello following information because you'll need it later when you create a circuit:</span></span>

* <span data-ttu-id="7e541-140">Ad</span><span class="sxs-lookup"><span data-stu-id="7e541-140">Name</span></span>
* <span data-ttu-id="7e541-141">PeeringLocations</span><span class="sxs-lookup"><span data-stu-id="7e541-141">PeeringLocations</span></span>
* <span data-ttu-id="7e541-142">BandwidthsOffered</span><span class="sxs-lookup"><span data-stu-id="7e541-142">BandwidthsOffered</span></span>

<span data-ttu-id="7e541-143">Şimdi hazır toocreate bir expressroute bağlantı hattı olduğunuz.</span><span class="sxs-lookup"><span data-stu-id="7e541-143">You're now ready toocreate an ExpressRoute circuit.</span></span>         

### <a name="step-3-create-an-expressroute-circuit"></a><span data-ttu-id="7e541-144">3. Adım</span><span class="sxs-lookup"><span data-stu-id="7e541-144">Step 3.</span></span> <span data-ttu-id="7e541-145">ExpressRoute bağlantı hattı oluşturma</span><span class="sxs-lookup"><span data-stu-id="7e541-145">Create an ExpressRoute circuit</span></span>
<span data-ttu-id="7e541-146">Aşağıdaki örnek hello nasıl toocreate 200 MB/sn expressroute bağlantı hattı Silikon vadisi Equinix aracılığıyla gösterir.</span><span class="sxs-lookup"><span data-stu-id="7e541-146">hello following example shows how toocreate a 200-Mbps ExpressRoute circuit through Equinix in Silicon Valley.</span></span> <span data-ttu-id="7e541-147">Farklı bir sağlayıcı ve farklı ayarlar kullanıyorsanız, bu bilgileri isteğiniz yaptığınızda değiştirin.</span><span class="sxs-lookup"><span data-stu-id="7e541-147">If you're using a different provider and different settings, substitute that information when you make your request.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7e541-148">ExpressRoute bağlantı hattınız bir hizmet anahtarı verilen hello andan itibaren Fatura edilecek.</span><span class="sxs-lookup"><span data-stu-id="7e541-148">Your ExpressRoute circuit will be billed from hello moment a service key is issued.</span></span> <span data-ttu-id="7e541-149">Merhaba bağlantı sağlayıcı hazır tooprovision hello hattı olduğunda bu işlemi gerçekleştirmek emin olun.</span><span class="sxs-lookup"><span data-stu-id="7e541-149">Ensure that you perform this operation when hello connectivity provider is ready tooprovision hello circuit.</span></span>
> 
> 

<span data-ttu-id="7e541-150">Merhaba, yeni bir hizmet anahtarı için bir örnek isteği aşağıdadır:</span><span class="sxs-lookup"><span data-stu-id="7e541-150">hello following is an example request for a new service key:</span></span>

    $Bandwidth = 200
    $CircuitName = "MyTestCircuit"
    $ServiceProvider = "Equinix"
    $Location = "Silicon Valley"

    New-AzureDedicatedCircuit -CircuitName $CircuitName -ServiceProviderName $ServiceProvider -Bandwidth $Bandwidth -Location $Location -sku Standard -BillingType MeteredData

<span data-ttu-id="7e541-151">Ya da toocreate hello premium eklentisi ile bir expressroute bağlantı hattı istiyorsanız, aşağıdaki kullanım hello örneğine.</span><span class="sxs-lookup"><span data-stu-id="7e541-151">Or, if you want toocreate an ExpressRoute circuit with hello premium add-on, use hello following example.</span></span> <span data-ttu-id="7e541-152">Toohello başvuran [ExpressRoute SSS](expressroute-faqs.md) hello premium eklentisi hakkında daha fazla ayrıntı için.</span><span class="sxs-lookup"><span data-stu-id="7e541-152">Refer toohello [ExpressRoute FAQ](expressroute-faqs.md) for more details about hello premium add-on.</span></span>

    New-AzureDedicatedCircuit -CircuitName $CircuitName -ServiceProviderName $ServiceProvider -Bandwidth $Bandwidth -Location $Location -sku Premium - BillingType MeteredData


<span data-ttu-id="7e541-153">Merhaba yanıt hello hizmet anahtarı içerir.</span><span class="sxs-lookup"><span data-stu-id="7e541-153">hello response will contain hello service key.</span></span> <span data-ttu-id="7e541-154">Merhaba aşağıdakini çalıştırarak tüm hello parametrelerin ayrıntılı açıklamaları alabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="7e541-154">You can get detailed descriptions of all hello parameters by running hello following:</span></span>

    get-help new-azurededicatedcircuit -detailed

### <a name="step-4-list-all-hello-expressroute-circuits"></a><span data-ttu-id="7e541-155">4. Adım.</span><span class="sxs-lookup"><span data-stu-id="7e541-155">Step 4.</span></span> <span data-ttu-id="7e541-156">Tüm hello ExpressRoute bağlantı hatları listesi</span><span class="sxs-lookup"><span data-stu-id="7e541-156">List all hello ExpressRoute circuits</span></span>
<span data-ttu-id="7e541-157">Merhaba çalıştırabilirsiniz `Get-AzureDedicatedCircuit` tooget tüm listesini hello oluşturduğunuz ExpressRoute bağlantı hatları komutu:</span><span class="sxs-lookup"><span data-stu-id="7e541-157">You can run hello `Get-AzureDedicatedCircuit` command tooget a list of all hello ExpressRoute circuits that you created:</span></span>

    Get-AzureDedicatedCircuit

<span data-ttu-id="7e541-158">Merhaba yanıt aşağıdaki örneğine benzeri toohello olacaktır:</span><span class="sxs-lookup"><span data-stu-id="7e541-158">hello response will be something similar toohello following example:</span></span>

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : NotProvisioned
    Sku                              : Standard
    Status                           : Enabled

<span data-ttu-id="7e541-159">Hello kullanarak herhangi bir zamanda bu bilgiler alabilirsiniz `Get-AzureDedicatedCircuit` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="7e541-159">You can retrieve this information at any time by using hello `Get-AzureDedicatedCircuit` cmdlet.</span></span> <span data-ttu-id="7e541-160">Hiçbir parametre olmadan çağrı hello yapmadan tüm hello devreleri listeler.</span><span class="sxs-lookup"><span data-stu-id="7e541-160">Making hello call without any parameters lists all hello circuits.</span></span> <span data-ttu-id="7e541-161">Hizmet anahtarınız hello listelenmez *ServiceKey* alan.</span><span class="sxs-lookup"><span data-stu-id="7e541-161">Your service key will be listed in hello *ServiceKey* field.</span></span>

    Get-AzureDedicatedCircuit

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : NotProvisioned
    Sku                              : Standard
    Status                           : Enabled

<span data-ttu-id="7e541-162">Merhaba aşağıdakini çalıştırarak tüm hello parametrelerin ayrıntılı açıklamaları alabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="7e541-162">You can get detailed descriptions of all hello parameters by running hello following:</span></span>

    get-help get-azurededicatedcircuit -detailed

### <a name="step-5-send-hello-service-key-tooyour-connectivity-provider-for-provisioning"></a><span data-ttu-id="7e541-163">5. Adım.</span><span class="sxs-lookup"><span data-stu-id="7e541-163">Step 5.</span></span> <span data-ttu-id="7e541-164">Merhaba hizmet anahtar tooyour bağlantı sağlayıcı sağlamak için Gönder</span><span class="sxs-lookup"><span data-stu-id="7e541-164">Send hello service key tooyour connectivity provider for provisioning</span></span>
<span data-ttu-id="7e541-165">*ServiceProviderProvisioningState* hello hizmet sağlayıcı tarafında sağlama hello geçerli durumu hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="7e541-165">*ServiceProviderProvisioningState* provides information on hello current state of provisioning on hello service-provider side.</span></span> <span data-ttu-id="7e541-166">*Durum* Microsoft yan hello üzerinde hello durumunu sağlar.</span><span class="sxs-lookup"><span data-stu-id="7e541-166">*Status* provides hello state on hello Microsoft side.</span></span> <span data-ttu-id="7e541-167">Merhaba hattı durumları sağlama hakkında daha fazla bilgi için bkz: [iş akışları](expressroute-workflows.md#expressroute-circuit-provisioning-states) makalesi.</span><span class="sxs-lookup"><span data-stu-id="7e541-167">For more information about circuit provisioning states, see hello [Workflows](expressroute-workflows.md#expressroute-circuit-provisioning-states) article.</span></span>

<span data-ttu-id="7e541-168">Yeni bir expressroute bağlantı hattı oluşturduğunuzda, hello hattı durumu aşağıdaki hello olacaktır:</span><span class="sxs-lookup"><span data-stu-id="7e541-168">When you create a new ExpressRoute circuit, hello circuit will be in hello following state:</span></span>

    ServiceProviderProvisioningState : NotProvisioned
    Status                           : Enabled


<span data-ttu-id="7e541-169">Merhaba hattı hello bağlantı sağlayıcı için etkinleştirme işleminin hello olduğunda durumu aşağıdaki toohello geçer:</span><span class="sxs-lookup"><span data-stu-id="7e541-169">hello circuit will go toohello following state when hello connectivity provider is in hello process of enabling it for you:</span></span>

    ServiceProviderProvisioningState : Provisioning
    Status                           : Enabled

<span data-ttu-id="7e541-170">Bir expressroute bağlantı hattı, toobe mümkün toouse durumunu izleyen hello onu olması gerekir:</span><span class="sxs-lookup"><span data-stu-id="7e541-170">An ExpressRoute circuit must be in hello following state for you toobe able toouse it:</span></span>

    ServiceProviderProvisioningState : Provisioned
    Status                           : Enabled


### <a name="step-6-periodically-check-hello-status-and-hello-state-of-hello-circuit-key"></a><span data-ttu-id="7e541-171">6. Adım.</span><span class="sxs-lookup"><span data-stu-id="7e541-171">Step 6.</span></span> <span data-ttu-id="7e541-172">Merhaba durumunu ve hello hattı anahtar hello durumunu düzenli aralıklarla denetleyin</span><span class="sxs-lookup"><span data-stu-id="7e541-172">Periodically check hello status and hello state of hello circuit key</span></span>
<span data-ttu-id="7e541-173">Bu, sağlayıcınız hattınız etkin olduğunda bilmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="7e541-173">This lets you know when your provider has enabled your circuit.</span></span> <span data-ttu-id="7e541-174">Merhaba hattı yapılandırıldıktan sonra *ServiceProviderProvisioningState* olarak görüntülenir *hazırlandı* hello aşağıdaki örnekte gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="7e541-174">After hello circuit has been configured, *ServiceProviderProvisioningState* will display as *Provisioned* as shown in hello following example:</span></span>

    Get-AzureDedicatedCircuit

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

### <a name="step-7-create-your-routing-configuration"></a><span data-ttu-id="7e541-175">7. Adım.</span><span class="sxs-lookup"><span data-stu-id="7e541-175">Step 7.</span></span> <span data-ttu-id="7e541-176">Yönlendirme yapılandırması oluşturma</span><span class="sxs-lookup"><span data-stu-id="7e541-176">Create your routing configuration</span></span>
<span data-ttu-id="7e541-177">Toohello başvuran [expressroute bağlantı hattı yönlendirme yapılandırması (oluşturma ve hattı eşlemeler değiştirme)](expressroute-howto-routing-classic.md) makale adım adım yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="7e541-177">Refer toohello [ExpressRoute circuit routing configuration (create and modify circuit peerings)](expressroute-howto-routing-classic.md) article for step-by-step instructions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7e541-178">Bu yönergeler yalnızca Katman 2 bağlantı hizmetleri sunan hizmet sağlayıcıları ile oluşturulan toocircuits geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="7e541-178">These instructions only apply toocircuits that are created with service providers that offer layer 2 connectivity services.</span></span> <span data-ttu-id="7e541-179">Yönetilen sunan bir hizmet sağlayıcısı kullanıyorsanız, Katman 3 Hizmetleri (genellikle bir IP VPN, MPLS gibi), bağlantı sağlayıcınız yapılandırmak ve yönetmek için yönlendirme.</span><span class="sxs-lookup"><span data-stu-id="7e541-179">If you're using a service provider that offers managed layer 3 services (typically an IP VPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span>
> 
> 

### <a name="step-8-link-a-virtual-network-tooan-expressroute-circuit"></a><span data-ttu-id="7e541-180">8. adım.</span><span class="sxs-lookup"><span data-stu-id="7e541-180">Step 8.</span></span> <span data-ttu-id="7e541-181">Sanal ağ tooan expressroute bağlantı hattı bağlantı</span><span class="sxs-lookup"><span data-stu-id="7e541-181">Link a virtual network tooan ExpressRoute circuit</span></span>
<span data-ttu-id="7e541-182">Ardından, sanal ağ tooyour expressroute bağlantı hattı bağlayın.</span><span class="sxs-lookup"><span data-stu-id="7e541-182">Next, link a virtual network tooyour ExpressRoute circuit.</span></span> <span data-ttu-id="7e541-183">Çok başvuran[bağlama ExpressRoute bağlantı hattına toovirtual ağlar](expressroute-howto-linkvnet-classic.md) adım adım yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="7e541-183">Refer too[Linking ExpressRoute circuits toovirtual networks](expressroute-howto-linkvnet-classic.md) for step-by-step instructions.</span></span> <span data-ttu-id="7e541-184">ExpressRoute için hello Klasik dağıtım modeli kullanarak bir sanal ağ toocreate gerekirse bkz [ExpressRoute için bir sanal ağ oluşturma](expressroute-howto-vnet-portal-classic.md).</span><span class="sxs-lookup"><span data-stu-id="7e541-184">If you need toocreate a virtual network using hello classic deployment model for ExpressRoute, see [Create a virtual network for ExpressRoute](expressroute-howto-vnet-portal-classic.md).</span></span>

## <a name="getting-hello-status-of-an-expressroute-circuit"></a><span data-ttu-id="7e541-185">Bir expressroute bağlantı hattı Hello durumunu alma</span><span class="sxs-lookup"><span data-stu-id="7e541-185">Getting hello status of an ExpressRoute circuit</span></span>
<span data-ttu-id="7e541-186">Hello kullanarak herhangi bir zamanda bu bilgiler alabilirsiniz `Get-AzureCircuit` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="7e541-186">You can retrieve this information at any time by using hello `Get-AzureCircuit` cmdlet.</span></span> <span data-ttu-id="7e541-187">Hiçbir parametre olmadan çağrı hello yapmadan tüm hello devreleri listeler.</span><span class="sxs-lookup"><span data-stu-id="7e541-187">Making hello call without any parameters lists all hello circuits.</span></span>

    Get-AzureDedicatedCircuit

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

    Bandwidth                        : 1000
    CircuitName                      : MyAsiaCircuit
    Location                         : Singapore
    ServiceKey                       : #################################
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

<span data-ttu-id="7e541-188">Bir parametre toohello araması olarak hello hizmet anahtarını geçirerek belirli bir expressroute bağlantı hattı hakkında bilgi alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7e541-188">You can get information on a specific ExpressRoute circuit by passing hello service key as a parameter toohello call.</span></span>

    Get-AzureDedicatedCircuit -ServiceKey "*********************************"

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled


<span data-ttu-id="7e541-189">Aşağıdaki örnek hello çalıştırarak tüm hello parametrelerin ayrıntılı açıklamaları alabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="7e541-189">You can get detailed descriptions of all hello parameters by running hello following example:</span></span>

    get-help get-azurededicatedcircuit -detailed

## <a name="modifying-an-expressroute-circuit"></a><span data-ttu-id="7e541-190">Bir expressroute bağlantı hattı değiştirme</span><span class="sxs-lookup"><span data-stu-id="7e541-190">Modifying an ExpressRoute circuit</span></span>
<span data-ttu-id="7e541-191">Bağlantı etkilemeden belirli bir expressroute bağlantı hattı özelliklerini değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7e541-191">You can modify certain properties of an ExpressRoute circuit without impacting connectivity.</span></span>

<span data-ttu-id="7e541-192">Yapabileceğiniz kapalı kalma süresi ile aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="7e541-192">You can do hello following with no downtime:</span></span>

* <span data-ttu-id="7e541-193">Etkinleştirmek veya devre dışı bir expressroute bağlantı hattı için ExpressRoute premium eklentisi.</span><span class="sxs-lookup"><span data-stu-id="7e541-193">Enable or disable an ExpressRoute premium add-on for your ExpressRoute circuit.</span></span>
* <span data-ttu-id="7e541-194">Artış hello bant genişliği, expressroute bağlantı hattı var. kapasite kullanılabilir hello bağlantı noktasında sağlanır.</span><span class="sxs-lookup"><span data-stu-id="7e541-194">Increase hello bandwidth of your ExpressRoute circuit provided there is capacity available on hello port.</span></span> <span data-ttu-id="7e541-195">Önceki sürüme indirme bir bağlantı hattının bant genişliği hello Not desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="7e541-195">Note that downgrading hello bandwidth of a circuit is not supported.</span></span> 
* <span data-ttu-id="7e541-196">Ölçülen veri tooUnlimited veri planından ölçümü hello değiştirin.</span><span class="sxs-lookup"><span data-stu-id="7e541-196">Change hello metering plan from Metered Data tooUnlimited Data.</span></span> <span data-ttu-id="7e541-197">Bu değişen hello ölçüm planından veri desteklenmiyor sınırsız veri tooMetered unutmayın.</span><span class="sxs-lookup"><span data-stu-id="7e541-197">Note that changing hello metering plan from Unlimited Data tooMetered Data is not supported.</span></span>
* <span data-ttu-id="7e541-198">Etkinleştirme ve devre dışı *izin Klasik işlemleri*.</span><span class="sxs-lookup"><span data-stu-id="7e541-198">You can enable and disable *Allow Classic Operations*.</span></span>

<span data-ttu-id="7e541-199">Toohello başvuran [ExpressRoute SSS](expressroute-faqs.md) sınırlar ve sınırlamalar hakkında daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="7e541-199">Refer toohello [ExpressRoute FAQ](expressroute-faqs.md) for more information on limits and limitations.</span></span>

### <a name="tooenable-hello-expressroute-premium-add-on"></a><span data-ttu-id="7e541-200">tooenable hello ExpressRoute premium eklentisi</span><span class="sxs-lookup"><span data-stu-id="7e541-200">tooenable hello ExpressRoute premium add-on</span></span>
<span data-ttu-id="7e541-201">Merhaba aşağıdaki PowerShell cmdlet'ini kullanarak, varolan bağlantı hattınız için hello ExpressRoute premium eklentisi etkinleştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="7e541-201">You can enable hello ExpressRoute premium add-on for your existing circuit by using hello following PowerShell cmdlet:</span></span>

    Set-AzureDedicatedCircuitProperties -ServiceKey "*********************************" -Sku Premium

    Bandwidth                        : 1000
    CircuitName                      : TestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Premium
    Status                           : Enabled

<span data-ttu-id="7e541-202">Bağlantı hattınız şimdi hello ExpressRoute premium eklentisi özellikleri etkin olacaktır.</span><span class="sxs-lookup"><span data-stu-id="7e541-202">Your circuit will now have hello ExpressRoute premium add-on features enabled.</span></span> <span data-ttu-id="7e541-203">Biz hello komutu başarıyla çalıştırıldı hemen için hello premium eklenti özelliğini faturalama başlayacak unutmayın.</span><span class="sxs-lookup"><span data-stu-id="7e541-203">Note that we will start billing you for hello premium add-on capability as soon as hello command has successfully run.</span></span>

### <a name="toodisable-hello-expressroute-premium-add-on"></a><span data-ttu-id="7e541-204">toodisable hello ExpressRoute premium eklentisi</span><span class="sxs-lookup"><span data-stu-id="7e541-204">toodisable hello ExpressRoute premium add-on</span></span>
> [!IMPORTANT]
> <span data-ttu-id="7e541-205">Merhaba standart bağlantı hattı için izin daha büyük olan kaynaklar kullanıyorsanız, bu işlemi başarısız olabilir.</span><span class="sxs-lookup"><span data-stu-id="7e541-205">This operation can fail if you're using resources that are greater than what is permitted for hello standard circuit.</span></span>
> 
> 

#### <a name="considerations"></a><span data-ttu-id="7e541-206">Dikkat edilmesi gerekenler</span><span class="sxs-lookup"><span data-stu-id="7e541-206">Considerations</span></span>

* <span data-ttu-id="7e541-207">Premium toostandard düşürmek önce sanal ağlar bağlantılı toohello hattı hello sayısı 10'dan az olduğundan emin olmalısınız.</span><span class="sxs-lookup"><span data-stu-id="7e541-207">You must ensure that hello number of virtual networks linked toohello circuit is less than 10 before you downgrade from premium toostandard.</span></span> <span data-ttu-id="7e541-208">Bunu yapmazsanız, güncelleştirme isteği başarısız olur ve Faturalanan hello premium oranları olması.</span><span class="sxs-lookup"><span data-stu-id="7e541-208">If you don't do this, your update request will fail, and you'll be billed hello premium rates.</span></span>
* <span data-ttu-id="7e541-209">Tüm sanal ağları diğer coğrafi bölgelerde bağlantısını gerekir.</span><span class="sxs-lookup"><span data-stu-id="7e541-209">You must unlink all virtual networks in other geopolitical regions.</span></span> <span data-ttu-id="7e541-210">Bunu yapmazsanız, güncelleştirme isteği başarısız olur ve Faturalanan hello premium oranları olması.</span><span class="sxs-lookup"><span data-stu-id="7e541-210">If you don't do this, your update request will fail, and you'll be billed hello premium rates.</span></span>
* <span data-ttu-id="7e541-211">Yol tablosu özel eşleme için 4. 000'den az yolları olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="7e541-211">Your route table must be less than 4,000 routes for private peering.</span></span> <span data-ttu-id="7e541-212">Rota tablosu boyutunuz 4.000 yolları büyükse, hello BGP oturumu bırakacaktır ve 4.000 tanıtılan önekler hello sayısı gider kadar yeniden iler hale olmaz.</span><span class="sxs-lookup"><span data-stu-id="7e541-212">If your route table size is greater than 4,000 routes, hello BGP session will drop and won't be reenabled until hello number of advertised prefixes goes below 4,000.</span></span>

#### <a name="disable-hello-premium-add-on"></a><span data-ttu-id="7e541-213">Merhaba premium eklentisi devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="7e541-213">Disable hello premium add-on</span></span>
<span data-ttu-id="7e541-214">Merhaba aşağıdaki PowerShell cmdlet'ini kullanarak var olan bağlantı hattınız için hello ExpressRoute premium eklentisi devre dışı bırakabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="7e541-214">You can disable hello ExpressRoute premium add-on for your existing circuit by using hello following PowerShell cmdlet:</span></span>

    Set-AzureDedicatedCircuitProperties -ServiceKey "*********************************" -Sku Standard

    Bandwidth                        : 1000
    CircuitName                      : TestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled



### <a name="tooupdate-hello-expressroute-circuit-bandwidth"></a><span data-ttu-id="7e541-215">tooupdate hello ExpressRoute devresi bant genişliği</span><span class="sxs-lookup"><span data-stu-id="7e541-215">tooupdate hello ExpressRoute circuit bandwidth</span></span>
<span data-ttu-id="7e541-216">Merhaba denetleyin [ExpressRoute SSS](expressroute-faqs.md) desteklenen sağlayıcınız için bant seçenekleri.</span><span class="sxs-lookup"><span data-stu-id="7e541-216">Check hello [ExpressRoute FAQ](expressroute-faqs.md) for supported bandwidth options for your provider.</span></span> <span data-ttu-id="7e541-217">(Hattınız oluşturulduğu) hello fiziksel bağlantı noktası izin verdiği sürece, varolan bağlantı hattınız hello boyutundan büyük olan herhangi bir boyutta seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7e541-217">You can pick any size that is greater than hello size of your existing circuit as long as hello physical port (on which your circuit is created) allows.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7e541-218">Merhaba varolan bağlantı noktasında yetersiz kapasite ise toorecreate hello expressroute bağlantı hattı olabilir.</span><span class="sxs-lookup"><span data-stu-id="7e541-218">You may have toorecreate hello ExpressRoute circuit if there is inadequate capacity on hello existing port.</span></span> <span data-ttu-id="7e541-219">Varsa hiçbir ek kapasite kullanılabilir o konumda hello hattı yükseltemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="7e541-219">You cannot upgrade hello circuit if there is no additional capacity available at that location.</span></span>
>
> <span data-ttu-id="7e541-220">Bir expressroute bağlantı hattı kesintiye uğratmadan hello bant genişliği azaltma olamaz.</span><span class="sxs-lookup"><span data-stu-id="7e541-220">You cannot reduce hello bandwidth of an ExpressRoute circuit without disruption.</span></span> <span data-ttu-id="7e541-221">Bant genişliği eski sürüme düşürmeyi toodeprovision hello expressroute bağlantı hattı gerektirir ve yeni bir expressroute bağlantı hattı yeniden sağlayın.</span><span class="sxs-lookup"><span data-stu-id="7e541-221">Downgrading bandwidth requires you toodeprovision hello ExpressRoute circuit and then reprovision a new ExpressRoute circuit.</span></span>
> 
> 

#### <a name="resize-a-circuit"></a><span data-ttu-id="7e541-222">Bir bağlantı hattı yeniden boyutlandırma</span><span class="sxs-lookup"><span data-stu-id="7e541-222">Resize a circuit</span></span>

<span data-ttu-id="7e541-223">Gereksinim boyutu karar verdikten sonra komutu tooresize aşağıdaki hello hattınız kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="7e541-223">After you decide what size you need, you can use hello following command tooresize your circuit:</span></span>

    Set-AzureDedicatedCircuitProperties -ServiceKey ********************************* -Bandwidth 1000

    Bandwidth                        : 1000
    CircuitName                      : TestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

<span data-ttu-id="7e541-224">Bağlantı hattınız hello Microsoft tarafında boyutlandırılmış.</span><span class="sxs-lookup"><span data-stu-id="7e541-224">Your circuit will have been sized up on hello Microsoft side.</span></span> <span data-ttu-id="7e541-225">Bu değişiklik, bağlantı sağlayıcısı tooupdate yapılandırmalarını kendi yan toomatch başvurmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="7e541-225">You must contact your connectivity provider tooupdate configurations on their side toomatch this change.</span></span> <span data-ttu-id="7e541-226">Biz Merhaba faturalama başlayacak Not bant genişliği seçeneği bu noktasından güncelleştirdi.</span><span class="sxs-lookup"><span data-stu-id="7e541-226">Note that we will start billing you for hello updated bandwidth option from this point on.</span></span>

<span data-ttu-id="7e541-227">Merhaba hello hattı bant genişliğini artırma olduğunda aşağıdaki hata görürseniz, bu var. Varolan hattınız oluşturulduğu hello fiziksel bağlantı noktası hiçbir yeterli bant genişliği sol anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="7e541-227">If you see hello following error when increasing hello circuit bandwidth, it means there is no sufficient bandwidth left on hello physical port where your existing circuit is created.</span></span> <span data-ttu-id="7e541-228">Bu hattı toodelete sahip ve yeni bir hattı ihtiyacınız hello boyutunun oluşturma.</span><span class="sxs-lookup"><span data-stu-id="7e541-228">You have toodelete this circuit and create a new circuit of hello size you need.</span></span> 

    Set-AzureDedicatedCircuitProperties : InvalidOperation : Insufficient bandwidth available tooperform this circuit
    update operation
    At line:1 char:1
    + Set-AzureDedicatedCircuitProperties -ServiceKey ********************* ...
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
        + CategoryInfo          : CloseError: (:) [Set-AzureDedicatedCircuitProperties], CloudException
        + FullyQualifiedErrorId : Microsoft.WindowsAzure.Commands.ExpressRoute.SetAzureDedicatedCircuitPropertiesCommand


## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a><span data-ttu-id="7e541-229">Sağlamayı kaldırmayı ve bir expressroute bağlantı hattı silme</span><span class="sxs-lookup"><span data-stu-id="7e541-229">Deprovisioning and deleting an ExpressRoute circuit</span></span>

### <a name="considerations"></a><span data-ttu-id="7e541-230">Dikkat edilmesi gerekenler</span><span class="sxs-lookup"><span data-stu-id="7e541-230">Considerations</span></span>

* <span data-ttu-id="7e541-231">Tüm sanal ağlardan hello expressroute bağlantı hattı için bu işlemi toosucceed bağlantısını gerekir.</span><span class="sxs-lookup"><span data-stu-id="7e541-231">You must unlink all virtual networks from hello ExpressRoute circuit for this operation toosucceed.</span></span> <span data-ttu-id="7e541-232">Denetleme olan tüm sanal ağlarınız varsa toosee, bu işlem başarısız olursa toohello hattı bağlı.</span><span class="sxs-lookup"><span data-stu-id="7e541-232">Check toosee if you have any virtual networks that are linked toohello circuit if this operation fails.</span></span>
* <span data-ttu-id="7e541-233">Merhaba ExpressRoute bağlantı hattı Hizmet Sağlayıcısı sağlama durumu ise **sağlama** veya **hazırlandı** kendi tarafında hizmet sağlayıcısı toodeprovision hello hattınız ile çalışmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="7e541-233">If hello ExpressRoute circuit service provider provisioning state is **Provisioning** or **Provisioned** you must work with your service provider toodeprovision hello circuit on their side.</span></span> <span data-ttu-id="7e541-234">Biz tooreserve kaynakları devam edecek ve hello hizmet sağlayıcısı sağlamayı hello hattı tamamlandıktan ve bize bildiren kadar sizi faturalandırmak.</span><span class="sxs-lookup"><span data-stu-id="7e541-234">We will continue tooreserve resources and bill you until hello service provider completes deprovisioning hello circuit and notifies us.</span></span>
* <span data-ttu-id="7e541-235">Merhaba hizmet sağlayıcısı hello hattı sağlaması kaldırılıyor. sağlaması değilse (Merhaba Hizmet Sağlayıcısı sağlama durumu çok ayarlamak**sağlanmadı**) hello hattı sonra silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7e541-235">If hello service provider has deprovisioned hello circuit (hello service provider provisioning state is set too**Not provisioned**) you can then delete hello circuit.</span></span> <span data-ttu-id="7e541-236">Bu hello hattı için fatura durdurur.</span><span class="sxs-lookup"><span data-stu-id="7e541-236">This will stop billing for hello circuit.</span></span>

#### <a name="delete-a-circuit"></a><span data-ttu-id="7e541-237">Bir bağlantı hattı Sil</span><span class="sxs-lookup"><span data-stu-id="7e541-237">Delete a circuit</span></span>

<span data-ttu-id="7e541-238">Hello aşağıdaki komutu çalıştırarak, expressroute bağlantı hattı silebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="7e541-238">You can delete your ExpressRoute circuit by running hello following command:</span></span>

    Remove-AzureDedicatedCircuit -ServiceKey "*********************************"



## <a name="next-steps"></a><span data-ttu-id="7e541-239">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="7e541-239">Next steps</span></span>
<span data-ttu-id="7e541-240">Bağlantı hattınız oluşturduktan sonra aşağıdaki hello emin olun:</span><span class="sxs-lookup"><span data-stu-id="7e541-240">After you create your circuit, make sure that you do hello following:</span></span>

* [<span data-ttu-id="7e541-241">Oluşturma ve expressroute bağlantı hattı için yönlendirmeyi değiştirme</span><span class="sxs-lookup"><span data-stu-id="7e541-241">Create and modify routing for your ExpressRoute circuit</span></span>](expressroute-howto-routing-classic.md)
* [<span data-ttu-id="7e541-242">Sanal ağ tooyour expressroute bağlantı hattı bağlantı</span><span class="sxs-lookup"><span data-stu-id="7e541-242">Link your virtual network tooyour ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-classic.md)

