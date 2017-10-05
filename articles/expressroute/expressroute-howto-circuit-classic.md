---
title: "Oluşturma ve bir expressroute bağlantı hattı değiştirme: PowerShell: Azure Klasik | Microsoft Docs"
description: "Bu makalede, oluşturma ve bir expressroute bağlantı hattı sağlama için adım adım anlatılmaktadır. Bu makalede ayrıca durumu, güncelleştirme veya silme denetleyin ve hattınız yetkisini kaldırma kullanmayı gösterir."
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
ms.openlocfilehash: 3b12bbb21ebf6a0160227c4a281c420cf192d6f7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="create-and-modify-an-expressroute-circuit-using-powershell-classic"></a><span data-ttu-id="65b21-104">Oluşturma ve PowerShell (Klasik) kullanarak bir expressroute bağlantı hattı değiştirme</span><span class="sxs-lookup"><span data-stu-id="65b21-104">Create and modify an ExpressRoute circuit using PowerShell (classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="65b21-105">Azure portal</span><span class="sxs-lookup"><span data-stu-id="65b21-105">Azure portal</span></span>](expressroute-howto-circuit-portal-resource-manager.md)
> * [<span data-ttu-id="65b21-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="65b21-106">PowerShell</span></span>](expressroute-howto-circuit-arm.md)
> * [<span data-ttu-id="65b21-107">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="65b21-107">Azure CLI</span></span>](howto-circuit-cli.md)
> * [<span data-ttu-id="65b21-108">Video - Azure portalı</span><span class="sxs-lookup"><span data-stu-id="65b21-108">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [<span data-ttu-id="65b21-109">PowerShell (klasik)</span><span class="sxs-lookup"><span data-stu-id="65b21-109">PowerShell (classic)</span></span>](expressroute-howto-circuit-classic.md)
>

<span data-ttu-id="65b21-110">Bu makalede, PowerShell cmdlet'leri ve klasik dağıtım modeli kullanarak bir Azure expressroute bağlantı hattı oluşturmak için adım adım anlatılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="65b21-110">This article walks you through the steps to create an Azure ExpressRoute circuit by using PowerShell cmdlets and the classic deployment model.</span></span> <span data-ttu-id="65b21-111">Bu makalede ayrıca durumu, güncelleştirme veya silme denetleyin ve bir expressroute bağlantı hattı yetkisini kaldırma kullanmayı gösterir.</span><span class="sxs-lookup"><span data-stu-id="65b21-111">This article also shows you how to check the status, update, or delete and deprovision an ExpressRoute circuit.</span></span>

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]


<span data-ttu-id="65b21-112">**Azure dağıtım modelleri hakkında**</span><span class="sxs-lookup"><span data-stu-id="65b21-112">**About Azure deployment models**</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="before-you-begin"></a><span data-ttu-id="65b21-113">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="65b21-113">Before you begin</span></span>
### <a name="step-1-review-the-prerequisites-and-workflow-articles"></a><span data-ttu-id="65b21-114">1. Adım</span><span class="sxs-lookup"><span data-stu-id="65b21-114">Step 1.</span></span> <span data-ttu-id="65b21-115">Önkoşulları ve iş akışı makaleleri gözden geçirin</span><span class="sxs-lookup"><span data-stu-id="65b21-115">Review the prerequisites and workflow articles</span></span>
<span data-ttu-id="65b21-116">Gözden geçirdiğinizden emin olun [Önkoşullar](expressroute-prerequisites.md) ve [iş akışları](expressroute-workflows.md) yapılandırmaya başlamadan önce.</span><span class="sxs-lookup"><span data-stu-id="65b21-116">Make sure that you have reviewed the [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>  

### <a name="step-2-install-the-latest-versions-of-the-azure-service-management-sm-powershell-modules"></a><span data-ttu-id="65b21-117">2. Adım</span><span class="sxs-lookup"><span data-stu-id="65b21-117">Step 2.</span></span> <span data-ttu-id="65b21-118">Azure Hizmet Yönetimi (SM) PowerShell modülleri en son sürümlerini yükleyin</span><span class="sxs-lookup"><span data-stu-id="65b21-118">Install the latest versions of the Azure Service Management (SM) PowerShell modules</span></span>
<span data-ttu-id="65b21-119">' Ndaki yönergeleri izleyin [Azure PowerShell cmdlet'leri ile çalışmaya başlama](/powershell/azure/overview) bilgisayarınızı Azure PowerShell modülleri kullanacak şekilde yapılandırma hakkında adım adım yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="65b21-119">Follow the instructions in [Getting started with Azure PowerShell cmdlets](/powershell/azure/overview) for step-by-step guidance on how to configure your computer to use the Azure PowerShell modules.</span></span>

### <a name="step-3-log-in-to-your-azure-account-and-select-a-subscription"></a><span data-ttu-id="65b21-120">3. Adım</span><span class="sxs-lookup"><span data-stu-id="65b21-120">Step 3.</span></span> <span data-ttu-id="65b21-121">Azure hesabınızda oturum açın ve bir abonelik seçin</span><span class="sxs-lookup"><span data-stu-id="65b21-121">Log in to your Azure account and select a subscription</span></span>
1. <span data-ttu-id="65b21-122">PowerShell konsolunuzu yükseltilmiş haklarla açın ve hesabınıza bağlanın.</span><span class="sxs-lookup"><span data-stu-id="65b21-122">Open your PowerShell console with elevated rights and connect to your account.</span></span> <span data-ttu-id="65b21-123">Bağlanmanıza yardımcı olması için aşağıdaki örneği kullanın:</span><span class="sxs-lookup"><span data-stu-id="65b21-123">Use the following example to help you connect:</span></span>

        Login-AzureRmAccount

2. <span data-ttu-id="65b21-124">Hesapla ilişkili abonelikleri kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="65b21-124">Check the subscriptions for the account.</span></span>

        Get-AzureRmSubscription

3. <span data-ttu-id="65b21-125">Birden fazla aboneliğiniz varsa, kullanmak istediğiniz aboneliği seçin.</span><span class="sxs-lookup"><span data-stu-id="65b21-125">If you have more than one subscription, select the subscription that you want to use.</span></span>

        Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"

4. <span data-ttu-id="65b21-126">Ardından, Klasik dağıtım modeli için PowerShell için Azure aboneliğinize eklemek için aşağıdaki cmdlet'i kullanın.</span><span class="sxs-lookup"><span data-stu-id="65b21-126">Next, use the following cmdlet to add your Azure subscription to PowerShell for the classic deployment model.</span></span>

        Add-AzureAccount

## <a name="create-and-provision-an-expressroute-circuit"></a><span data-ttu-id="65b21-127">Oluşturma ve bir expressroute bağlantı hattı sağlama</span><span class="sxs-lookup"><span data-stu-id="65b21-127">Create and provision an ExpressRoute circuit</span></span>
### <a name="step-1-import-the-powershell-modules-for-expressroute"></a><span data-ttu-id="65b21-128">1. Adım</span><span class="sxs-lookup"><span data-stu-id="65b21-128">Step 1.</span></span> <span data-ttu-id="65b21-129">ExpressRoute için PowerShell modülleri alın</span><span class="sxs-lookup"><span data-stu-id="65b21-129">Import the PowerShell modules for ExpressRoute</span></span>
 <span data-ttu-id="65b21-130">Zaten yapmadıysanız, Azure ve ExpressRoute modüllerini PowerShell oturumuna ExpressRoute cmdlet'lerini kullanmaya başlamak için içeri aktarmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="65b21-130">If you have not already done so, you must import the Azure and ExpressRoute modules into the PowerShell session in order to start using the ExpressRoute cmdlets.</span></span> <span data-ttu-id="65b21-131">Yerel bilgisayarınızda yüklü olan bir konumdan modülleri içeri aktarın.</span><span class="sxs-lookup"><span data-stu-id="65b21-131">You import the modules from the location that they were installed to on your local computer.</span></span> <span data-ttu-id="65b21-132">Konumun modüllerini yüklemek için kullanılan yönteme bağlı olarak aşağıdaki örnekte gösterildiği farklı olabilir.</span><span class="sxs-lookup"><span data-stu-id="65b21-132">Depending on the method you used to install the modules, the location may be different than the following example shows.</span></span> <span data-ttu-id="65b21-133">Örnek gerekiyorsa değiştirin.</span><span class="sxs-lookup"><span data-stu-id="65b21-133">Modify the example if necessary.</span></span>  

    Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
    Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'

### <a name="step-2-get-the-list-of-supported-providers-locations-and-bandwidths"></a><span data-ttu-id="65b21-134">2. Adım</span><span class="sxs-lookup"><span data-stu-id="65b21-134">Step 2.</span></span> <span data-ttu-id="65b21-135">Desteklenen sağlayıcılar, konumları ve bant genişlikleri listesini alma</span><span class="sxs-lookup"><span data-stu-id="65b21-135">Get the list of supported providers, locations, and bandwidths</span></span>
<span data-ttu-id="65b21-136">Bir expressroute bağlantı hattı oluşturmadan önce desteklenen bağlantı sağlayıcıları, konumları ve bant seçeneklerini listesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="65b21-136">Before you create an ExpressRoute circuit, you need the list of supported connectivity providers, locations, and bandwidth options.</span></span>

<span data-ttu-id="65b21-137">PowerShell cmdlet `Get-AzureDedicatedCircuitServiceProvider` , sonraki adımlarda kullanacağınız bu bilgiler verir:</span><span class="sxs-lookup"><span data-stu-id="65b21-137">The PowerShell cmdlet `Get-AzureDedicatedCircuitServiceProvider` returns this information, which you’ll use in later steps:</span></span>

    Get-AzureDedicatedCircuitServiceProvider

<span data-ttu-id="65b21-138">Bağlantı sağlayıcınız listelenip listelenmediğini denetleyin.</span><span class="sxs-lookup"><span data-stu-id="65b21-138">Check to see if your connectivity provider is listed there.</span></span> <span data-ttu-id="65b21-139">Bir bağlantı hattı oluşturduğunuzda, daha sonra gerekir çünkü aşağıdaki bilgileri not edin:</span><span class="sxs-lookup"><span data-stu-id="65b21-139">Make a note of the following information because you'll need it later when you create a circuit:</span></span>

* <span data-ttu-id="65b21-140">Ad</span><span class="sxs-lookup"><span data-stu-id="65b21-140">Name</span></span>
* <span data-ttu-id="65b21-141">PeeringLocations</span><span class="sxs-lookup"><span data-stu-id="65b21-141">PeeringLocations</span></span>
* <span data-ttu-id="65b21-142">BandwidthsOffered</span><span class="sxs-lookup"><span data-stu-id="65b21-142">BandwidthsOffered</span></span>

<span data-ttu-id="65b21-143">Artık bir expressroute bağlantı hattı oluşturmak hazırsınız.</span><span class="sxs-lookup"><span data-stu-id="65b21-143">You're now ready to create an ExpressRoute circuit.</span></span>         

### <a name="step-3-create-an-expressroute-circuit"></a><span data-ttu-id="65b21-144">3. Adım</span><span class="sxs-lookup"><span data-stu-id="65b21-144">Step 3.</span></span> <span data-ttu-id="65b21-145">ExpressRoute bağlantı hattı oluşturma</span><span class="sxs-lookup"><span data-stu-id="65b21-145">Create an ExpressRoute circuit</span></span>
<span data-ttu-id="65b21-146">Aşağıdaki örnek 200 MB/sn expressroute bağlantı hattı üzerinden Equinix Silikon Vadisi'nde oluşturulacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="65b21-146">The following example shows how to create a 200-Mbps ExpressRoute circuit through Equinix in Silicon Valley.</span></span> <span data-ttu-id="65b21-147">Farklı bir sağlayıcı ve farklı ayarlar kullanıyorsanız, bu bilgileri isteğiniz yaptığınızda değiştirin.</span><span class="sxs-lookup"><span data-stu-id="65b21-147">If you're using a different provider and different settings, substitute that information when you make your request.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="65b21-148">ExpressRoute bağlantı hattınız bir hizmet anahtarı verilen andan itibaren Fatura edilecek.</span><span class="sxs-lookup"><span data-stu-id="65b21-148">Your ExpressRoute circuit will be billed from the moment a service key is issued.</span></span> <span data-ttu-id="65b21-149">Bağlantı sağlayıcı bağlantı hattı sağlamak hazır olduğunda bu işlemi gerçekleştirmek emin olun.</span><span class="sxs-lookup"><span data-stu-id="65b21-149">Ensure that you perform this operation when the connectivity provider is ready to provision the circuit.</span></span>
> 
> 

<span data-ttu-id="65b21-150">Yeni bir hizmet anahtarı için bir örnek isteği verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="65b21-150">The following is an example request for a new service key:</span></span>

    $Bandwidth = 200
    $CircuitName = "MyTestCircuit"
    $ServiceProvider = "Equinix"
    $Location = "Silicon Valley"

    New-AzureDedicatedCircuit -CircuitName $CircuitName -ServiceProviderName $ServiceProvider -Bandwidth $Bandwidth -Location $Location -sku Standard -BillingType MeteredData

<span data-ttu-id="65b21-151">Veya, bir expressroute premium eklentisi ile oluşturmak istiyorsanız, aşağıdaki örneği kullanın.</span><span class="sxs-lookup"><span data-stu-id="65b21-151">Or, if you want to create an ExpressRoute circuit with the premium add-on, use the following example.</span></span> <span data-ttu-id="65b21-152">Başvurmak [ExpressRoute SSS](expressroute-faqs.md) premium eklentisi hakkında daha fazla ayrıntı için.</span><span class="sxs-lookup"><span data-stu-id="65b21-152">Refer to the [ExpressRoute FAQ](expressroute-faqs.md) for more details about the premium add-on.</span></span>

    New-AzureDedicatedCircuit -CircuitName $CircuitName -ServiceProviderName $ServiceProvider -Bandwidth $Bandwidth -Location $Location -sku Premium - BillingType MeteredData


<span data-ttu-id="65b21-153">Yanıt hizmet anahtarını içerir.</span><span class="sxs-lookup"><span data-stu-id="65b21-153">The response will contain the service key.</span></span> <span data-ttu-id="65b21-154">Aşağıdaki komutu çalıştırarak tüm parametrelerin ayrıntılı açıklamaları alabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="65b21-154">You can get detailed descriptions of all the parameters by running the following:</span></span>

    get-help new-azurededicatedcircuit -detailed

### <a name="step-4-list-all-the-expressroute-circuits"></a><span data-ttu-id="65b21-155">4. Adım.</span><span class="sxs-lookup"><span data-stu-id="65b21-155">Step 4.</span></span> <span data-ttu-id="65b21-156">Tüm ExpressRoute bağlantı hatları listesi</span><span class="sxs-lookup"><span data-stu-id="65b21-156">List all the ExpressRoute circuits</span></span>
<span data-ttu-id="65b21-157">Çalıştırabilirsiniz `Get-AzureDedicatedCircuit` oluşturduğunuz tüm expressroute bağlantı hatları listesini almak için komutu:</span><span class="sxs-lookup"><span data-stu-id="65b21-157">You can run the `Get-AzureDedicatedCircuit` command to get a list of all the ExpressRoute circuits that you created:</span></span>

    Get-AzureDedicatedCircuit

<span data-ttu-id="65b21-158">Yanıt aşağıdaki örneğe benzer bir şey olacaktır:</span><span class="sxs-lookup"><span data-stu-id="65b21-158">The response will be something similar to the following example:</span></span>

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : NotProvisioned
    Sku                              : Standard
    Status                           : Enabled

<span data-ttu-id="65b21-159">Herhangi bir zamanda bu bilgileri kullanarak alabilirsiniz `Get-AzureDedicatedCircuit` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="65b21-159">You can retrieve this information at any time by using the `Get-AzureDedicatedCircuit` cmdlet.</span></span> <span data-ttu-id="65b21-160">Hiçbir parametre olmadan çağrıyı yapan tüm devreler listeler.</span><span class="sxs-lookup"><span data-stu-id="65b21-160">Making the call without any parameters lists all the circuits.</span></span> <span data-ttu-id="65b21-161">Hizmet anahtarınız listelenen *ServiceKey* alan.</span><span class="sxs-lookup"><span data-stu-id="65b21-161">Your service key will be listed in the *ServiceKey* field.</span></span>

    Get-AzureDedicatedCircuit

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : NotProvisioned
    Sku                              : Standard
    Status                           : Enabled

<span data-ttu-id="65b21-162">Aşağıdaki komutu çalıştırarak tüm parametrelerin ayrıntılı açıklamaları alabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="65b21-162">You can get detailed descriptions of all the parameters by running the following:</span></span>

    get-help get-azurededicatedcircuit -detailed

### <a name="step-5-send-the-service-key-to-your-connectivity-provider-for-provisioning"></a><span data-ttu-id="65b21-163">5. Adım.</span><span class="sxs-lookup"><span data-stu-id="65b21-163">Step 5.</span></span> <span data-ttu-id="65b21-164">Hizmet anahtarı sağlamak için bağlantı sağlayıcınızı Gönder</span><span class="sxs-lookup"><span data-stu-id="65b21-164">Send the service key to your connectivity provider for provisioning</span></span>
<span data-ttu-id="65b21-165">*ServiceProviderProvisioningState* hizmet sağlayıcı tarafında sağlama geçerli durumu hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="65b21-165">*ServiceProviderProvisioningState* provides information on the current state of provisioning on the service-provider side.</span></span> <span data-ttu-id="65b21-166">*Durum* Microsoft tarafında durumunu sağlar.</span><span class="sxs-lookup"><span data-stu-id="65b21-166">*Status* provides the state on the Microsoft side.</span></span> <span data-ttu-id="65b21-167">Bağlantı hattı durumları sağlama hakkında daha fazla bilgi için bkz: [iş akışları](expressroute-workflows.md#expressroute-circuit-provisioning-states) makalesi.</span><span class="sxs-lookup"><span data-stu-id="65b21-167">For more information about circuit provisioning states, see the [Workflows](expressroute-workflows.md#expressroute-circuit-provisioning-states) article.</span></span>

<span data-ttu-id="65b21-168">Yeni bir expressroute bağlantı hattı oluşturduğunuzda, bağlantı hattı şu durumda olacaktır:</span><span class="sxs-lookup"><span data-stu-id="65b21-168">When you create a new ExpressRoute circuit, the circuit will be in the following state:</span></span>

    ServiceProviderProvisioningState : NotProvisioned
    Status                           : Enabled


<span data-ttu-id="65b21-169">Bağlantı sağlayıcı onu sizin için etkinleştirme sürecinde olduğunda bağlantı hattı aşağıdaki durumuna gidin:</span><span class="sxs-lookup"><span data-stu-id="65b21-169">The circuit will go to the following state when the connectivity provider is in the process of enabling it for you:</span></span>

    ServiceProviderProvisioningState : Provisioning
    Status                           : Enabled

<span data-ttu-id="65b21-170">Bir expressroute bağlantı hattı, onu kullanabilmek aşağıdaki durumda olması gerekir:</span><span class="sxs-lookup"><span data-stu-id="65b21-170">An ExpressRoute circuit must be in the following state for you to be able to use it:</span></span>

    ServiceProviderProvisioningState : Provisioned
    Status                           : Enabled


### <a name="step-6-periodically-check-the-status-and-the-state-of-the-circuit-key"></a><span data-ttu-id="65b21-171">6. Adım.</span><span class="sxs-lookup"><span data-stu-id="65b21-171">Step 6.</span></span> <span data-ttu-id="65b21-172">Durum ve hattı anahtar durumunu düzenli aralıklarla denetleyin</span><span class="sxs-lookup"><span data-stu-id="65b21-172">Periodically check the status and the state of the circuit key</span></span>
<span data-ttu-id="65b21-173">Bu, sağlayıcınız hattınız etkin olduğunda bilmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="65b21-173">This lets you know when your provider has enabled your circuit.</span></span> <span data-ttu-id="65b21-174">Bağlantı hattı yapılandırıldıktan sonra *ServiceProviderProvisioningState* olarak görüntülenir *hazırlandı* aşağıdaki örnekte gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="65b21-174">After the circuit has been configured, *ServiceProviderProvisioningState* will display as *Provisioned* as shown in the following example:</span></span>

    Get-AzureDedicatedCircuit

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

### <a name="step-7-create-your-routing-configuration"></a><span data-ttu-id="65b21-175">7. Adım.</span><span class="sxs-lookup"><span data-stu-id="65b21-175">Step 7.</span></span> <span data-ttu-id="65b21-176">Yönlendirme yapılandırması oluşturma</span><span class="sxs-lookup"><span data-stu-id="65b21-176">Create your routing configuration</span></span>
<span data-ttu-id="65b21-177">Başvurmak [expressroute bağlantı hattı yönlendirme yapılandırması (oluşturma ve hattı eşlemeler değiştirme)](expressroute-howto-routing-classic.md) makale adım adım yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="65b21-177">Refer to the [ExpressRoute circuit routing configuration (create and modify circuit peerings)](expressroute-howto-routing-classic.md) article for step-by-step instructions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="65b21-178">Bu yönergeler yalnızca Katman 2 bağlantı hizmetleri sunan hizmet sağlayıcıları ile oluşturulan bağlantı hatları için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="65b21-178">These instructions only apply to circuits that are created with service providers that offer layer 2 connectivity services.</span></span> <span data-ttu-id="65b21-179">Yönetilen sunan bir hizmet sağlayıcısı kullanıyorsanız, Katman 3 Hizmetleri (genellikle bir IP VPN, MPLS gibi), bağlantı sağlayıcınız yapılandırmak ve yönetmek için yönlendirme.</span><span class="sxs-lookup"><span data-stu-id="65b21-179">If you're using a service provider that offers managed layer 3 services (typically an IP VPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span>
> 
> 

### <a name="step-8-link-a-virtual-network-to-an-expressroute-circuit"></a><span data-ttu-id="65b21-180">8. adım.</span><span class="sxs-lookup"><span data-stu-id="65b21-180">Step 8.</span></span> <span data-ttu-id="65b21-181">ExpressRoute bağlantı hattına bir sanal ağı bağlama</span><span class="sxs-lookup"><span data-stu-id="65b21-181">Link a virtual network to an ExpressRoute circuit</span></span>
<span data-ttu-id="65b21-182">Ardından, bir sanal ağ, expressroute bağlantı hattına bağlayın.</span><span class="sxs-lookup"><span data-stu-id="65b21-182">Next, link a virtual network to your ExpressRoute circuit.</span></span> <span data-ttu-id="65b21-183">Başvurmak [sanal ağlara bağlama ExpressRoute bağlantı hatları](expressroute-howto-linkvnet-classic.md) adım adım yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="65b21-183">Refer to [Linking ExpressRoute circuits to virtual networks](expressroute-howto-linkvnet-classic.md) for step-by-step instructions.</span></span> <span data-ttu-id="65b21-184">ExpressRoute için Klasik dağıtım modeli kullanarak bir sanal ağ oluşturma gerekiyorsa bkz [ExpressRoute için bir sanal ağ oluşturma](expressroute-howto-vnet-portal-classic.md).</span><span class="sxs-lookup"><span data-stu-id="65b21-184">If you need to create a virtual network using the classic deployment model for ExpressRoute, see [Create a virtual network for ExpressRoute](expressroute-howto-vnet-portal-classic.md).</span></span>

## <a name="getting-the-status-of-an-expressroute-circuit"></a><span data-ttu-id="65b21-185">Bir expressroute bağlantı hattı durumunu alma</span><span class="sxs-lookup"><span data-stu-id="65b21-185">Getting the status of an ExpressRoute circuit</span></span>
<span data-ttu-id="65b21-186">Herhangi bir zamanda bu bilgileri kullanarak alabilirsiniz `Get-AzureCircuit` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="65b21-186">You can retrieve this information at any time by using the `Get-AzureCircuit` cmdlet.</span></span> <span data-ttu-id="65b21-187">Hiçbir parametre olmadan çağrıyı yapan tüm devreler listeler.</span><span class="sxs-lookup"><span data-stu-id="65b21-187">Making the call without any parameters lists all the circuits.</span></span>

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

<span data-ttu-id="65b21-188">Çağrısına parametre olarak hizmet anahtarını geçirerek belirli bir expressroute bağlantı hattı hakkında bilgi alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="65b21-188">You can get information on a specific ExpressRoute circuit by passing the service key as a parameter to the call.</span></span>

    Get-AzureDedicatedCircuit -ServiceKey "*********************************"

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled


<span data-ttu-id="65b21-189">Aşağıdaki örnek çalıştırarak tüm parametrelerin ayrıntılı açıklamaları alabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="65b21-189">You can get detailed descriptions of all the parameters by running the following example:</span></span>

    get-help get-azurededicatedcircuit -detailed

## <a name="modifying-an-expressroute-circuit"></a><span data-ttu-id="65b21-190">Bir expressroute bağlantı hattı değiştirme</span><span class="sxs-lookup"><span data-stu-id="65b21-190">Modifying an ExpressRoute circuit</span></span>
<span data-ttu-id="65b21-191">Bağlantı etkilemeden belirli bir expressroute bağlantı hattı özelliklerini değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="65b21-191">You can modify certain properties of an ExpressRoute circuit without impacting connectivity.</span></span>

<span data-ttu-id="65b21-192">Kapalı kalma süresi olmadan aşağıdakileri yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="65b21-192">You can do the following with no downtime:</span></span>

* <span data-ttu-id="65b21-193">Etkinleştirmek veya devre dışı bir expressroute bağlantı hattı için ExpressRoute premium eklentisi.</span><span class="sxs-lookup"><span data-stu-id="65b21-193">Enable or disable an ExpressRoute premium add-on for your ExpressRoute circuit.</span></span>
* <span data-ttu-id="65b21-194">Sağlanmış kapasite kullanılabilir bağlantı noktası, expressroute bağlantı hattı bant genişliğini artırır.</span><span class="sxs-lookup"><span data-stu-id="65b21-194">Increase the bandwidth of your ExpressRoute circuit provided there is capacity available on the port.</span></span> <span data-ttu-id="65b21-195">Bir bağlantı hattının bant genişliğini eski sürüme düşürmeyi desteklenmediğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="65b21-195">Note that downgrading the bandwidth of a circuit is not supported.</span></span> 
* <span data-ttu-id="65b21-196">Ölçüm plan sınırsız veri ölçülen verilerden değiştirin.</span><span class="sxs-lookup"><span data-stu-id="65b21-196">Change the metering plan from Metered Data to Unlimited Data.</span></span> <span data-ttu-id="65b21-197">Ölçülen veri sınırsız verilerden ölçüm planı değiştirmek desteklenmez unutmayın.</span><span class="sxs-lookup"><span data-stu-id="65b21-197">Note that changing the metering plan from Unlimited Data to Metered Data is not supported.</span></span>
* <span data-ttu-id="65b21-198">Etkinleştirme ve devre dışı *izin Klasik işlemleri*.</span><span class="sxs-lookup"><span data-stu-id="65b21-198">You can enable and disable *Allow Classic Operations*.</span></span>

<span data-ttu-id="65b21-199">Başvurmak [ExpressRoute SSS](expressroute-faqs.md) sınırlar ve sınırlamalar hakkında daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="65b21-199">Refer to the [ExpressRoute FAQ](expressroute-faqs.md) for more information on limits and limitations.</span></span>

### <a name="to-enable-the-expressroute-premium-add-on"></a><span data-ttu-id="65b21-200">ExpressRoute premium eklentisi etkinleştirmek için</span><span class="sxs-lookup"><span data-stu-id="65b21-200">To enable the ExpressRoute premium add-on</span></span>
<span data-ttu-id="65b21-201">Aşağıdaki PowerShell cmdlet'ini kullanarak, varolan bağlantı hattınız için ExpressRoute premium eklentisi etkinleştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="65b21-201">You can enable the ExpressRoute premium add-on for your existing circuit by using the following PowerShell cmdlet:</span></span>

    Set-AzureDedicatedCircuitProperties -ServiceKey "*********************************" -Sku Premium

    Bandwidth                        : 1000
    CircuitName                      : TestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Premium
    Status                           : Enabled

<span data-ttu-id="65b21-202">Bağlantı hattınız şimdi etkin ExpressRoute premium eklentisi özellikleri sahip olur.</span><span class="sxs-lookup"><span data-stu-id="65b21-202">Your circuit will now have the ExpressRoute premium add-on features enabled.</span></span> <span data-ttu-id="65b21-203">Biz komutu başarıyla çalıştırıldı hemen premium eklenti özellik faturalama başlayacak unutmayın.</span><span class="sxs-lookup"><span data-stu-id="65b21-203">Note that we will start billing you for the premium add-on capability as soon as the command has successfully run.</span></span>

### <a name="to-disable-the-expressroute-premium-add-on"></a><span data-ttu-id="65b21-204">ExpressRoute premium eklentisi devre dışı bırakmak için</span><span class="sxs-lookup"><span data-stu-id="65b21-204">To disable the ExpressRoute premium add-on</span></span>
> [!IMPORTANT]
> <span data-ttu-id="65b21-205">Standart bağlantı hattı için izin daha büyük olan kaynaklar kullanıyorsanız, bu işlemi başarısız olabilir.</span><span class="sxs-lookup"><span data-stu-id="65b21-205">This operation can fail if you're using resources that are greater than what is permitted for the standard circuit.</span></span>
> 
> 

#### <a name="considerations"></a><span data-ttu-id="65b21-206">Dikkat edilmesi gerekenler</span><span class="sxs-lookup"><span data-stu-id="65b21-206">Considerations</span></span>

* <span data-ttu-id="65b21-207">Standart Premium'dan düşürmek önce devresine bağlı sanal ağlar sayısı 10'dan az olduğundan emin olmalısınız.</span><span class="sxs-lookup"><span data-stu-id="65b21-207">You must ensure that the number of virtual networks linked to the circuit is less than 10 before you downgrade from premium to standard.</span></span> <span data-ttu-id="65b21-208">Bunu yapmazsanız, güncelleştirme isteği başarısız olur ve olması, premium oranları faturalandırılır.</span><span class="sxs-lookup"><span data-stu-id="65b21-208">If you don't do this, your update request will fail, and you'll be billed the premium rates.</span></span>
* <span data-ttu-id="65b21-209">Tüm sanal ağları diğer coğrafi bölgelerde bağlantısını gerekir.</span><span class="sxs-lookup"><span data-stu-id="65b21-209">You must unlink all virtual networks in other geopolitical regions.</span></span> <span data-ttu-id="65b21-210">Bunu yapmazsanız, güncelleştirme isteği başarısız olur ve olması, premium oranları faturalandırılır.</span><span class="sxs-lookup"><span data-stu-id="65b21-210">If you don't do this, your update request will fail, and you'll be billed the premium rates.</span></span>
* <span data-ttu-id="65b21-211">Yol tablosu özel eşleme için 4. 000'den az yolları olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="65b21-211">Your route table must be less than 4,000 routes for private peering.</span></span> <span data-ttu-id="65b21-212">Rota tablosu boyutunuz 4.000 yolları büyükse, BGP oturumu bırakacaktır ve 4.000 tanıtılan ön ek sayısı gider kadar yeniden iler hale olmaz.</span><span class="sxs-lookup"><span data-stu-id="65b21-212">If your route table size is greater than 4,000 routes, the BGP session will drop and won't be reenabled until the number of advertised prefixes goes below 4,000.</span></span>

#### <a name="disable-the-premium-add-on"></a><span data-ttu-id="65b21-213">Premium eklentisi devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="65b21-213">Disable the premium add-on</span></span>
<span data-ttu-id="65b21-214">Aşağıdaki PowerShell cmdlet'ini kullanarak var olan bağlantı hattınız için ExpressRoute premium eklentisi devre dışı bırakabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="65b21-214">You can disable the ExpressRoute premium add-on for your existing circuit by using the following PowerShell cmdlet:</span></span>

    Set-AzureDedicatedCircuitProperties -ServiceKey "*********************************" -Sku Standard

    Bandwidth                        : 1000
    CircuitName                      : TestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled



### <a name="to-update-the-expressroute-circuit-bandwidth"></a><span data-ttu-id="65b21-215">ExpressRoute bağlantı hattı bant genişliğini güncelleştirmek için</span><span class="sxs-lookup"><span data-stu-id="65b21-215">To update the ExpressRoute circuit bandwidth</span></span>
<span data-ttu-id="65b21-216">Denetleme [ExpressRoute SSS](expressroute-faqs.md) desteklenen sağlayıcınız için bant seçenekleri.</span><span class="sxs-lookup"><span data-stu-id="65b21-216">Check the [ExpressRoute FAQ](expressroute-faqs.md) for supported bandwidth options for your provider.</span></span> <span data-ttu-id="65b21-217">Sunucudaki fiziksel bağlantı noktası (hattınız oluşturulduğu) izin verdiği sürece, varolan bağlantı hattınız boyutundan büyük herhangi bir boyutta seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="65b21-217">You can pick any size that is greater than the size of your existing circuit as long as the physical port (on which your circuit is created) allows.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="65b21-218">Varolan bir bağlantı üzerinde yetersiz kapasite ise expressroute bağlantı hattı yeniden başlatmanız gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="65b21-218">You may have to recreate the ExpressRoute circuit if there is inadequate capacity on the existing port.</span></span> <span data-ttu-id="65b21-219">Varsa hiçbir ek kapasite kullanılabilir o konumda bağlantı hattı yükseltemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="65b21-219">You cannot upgrade the circuit if there is no additional capacity available at that location.</span></span>
>
> <span data-ttu-id="65b21-220">Bir expressroute bağlantı hattı kesintiye uğratmadan bant indiremezsiniz.</span><span class="sxs-lookup"><span data-stu-id="65b21-220">You cannot reduce the bandwidth of an ExpressRoute circuit without disruption.</span></span> <span data-ttu-id="65b21-221">Bant genişliği eski sürüme düşürmeyi expressroute bağlantı hattı yetkisini kaldırma ve yeni bir expressroute bağlantı hattı yeniden hazırlayana gerektirir.</span><span class="sxs-lookup"><span data-stu-id="65b21-221">Downgrading bandwidth requires you to deprovision the ExpressRoute circuit and then reprovision a new ExpressRoute circuit.</span></span>
> 
> 

#### <a name="resize-a-circuit"></a><span data-ttu-id="65b21-222">Bir bağlantı hattı yeniden boyutlandırma</span><span class="sxs-lookup"><span data-stu-id="65b21-222">Resize a circuit</span></span>

<span data-ttu-id="65b21-223">Gereksinim boyutu karar verdikten sonra bağlantı hattınız yeniden boyutlandırmak için aşağıdaki komutu kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="65b21-223">After you decide what size you need, you can use the following command to resize your circuit:</span></span>

    Set-AzureDedicatedCircuitProperties -ServiceKey ********************************* -Bandwidth 1000

    Bandwidth                        : 1000
    CircuitName                      : TestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

<span data-ttu-id="65b21-224">Bağlantı hattınız Microsoft tarafında boyutlandırılmış.</span><span class="sxs-lookup"><span data-stu-id="65b21-224">Your circuit will have been sized up on the Microsoft side.</span></span> <span data-ttu-id="65b21-225">Bu değişiklik eşleşecek şekilde kendi tarafında yapılandırmalar güncelleştirileceğini bağlantı sağlayıcınız başvurmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="65b21-225">You must contact your connectivity provider to update configurations on their side to match this change.</span></span> <span data-ttu-id="65b21-226">Biz üzerinde bu noktasından güncelleştirilmiş bant seçeneği için faturalama başlayacak unutmayın.</span><span class="sxs-lookup"><span data-stu-id="65b21-226">Note that we will start billing you for the updated bandwidth option from this point on.</span></span>

<span data-ttu-id="65b21-227">Bağlantı hattı bant genişliğini artırma olduğunda aşağıdaki hata görürseniz, bu var. Varolan hattınız oluşturulduğu fiziksel bağlantı noktası üzerinde hiçbir yeterli bant genişliği sol anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="65b21-227">If you see the following error when increasing the circuit bandwidth, it means there is no sufficient bandwidth left on the physical port where your existing circuit is created.</span></span> <span data-ttu-id="65b21-228">Bağlantı hattı silin ve yeni bir bağlantı hattı gereksinim boyutu oluşturmak zorunda.</span><span class="sxs-lookup"><span data-stu-id="65b21-228">You have to delete this circuit and create a new circuit of the size you need.</span></span> 

    Set-AzureDedicatedCircuitProperties : InvalidOperation : Insufficient bandwidth available to perform this circuit
    update operation
    At line:1 char:1
    + Set-AzureDedicatedCircuitProperties -ServiceKey ********************* ...
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
        + CategoryInfo          : CloseError: (:) [Set-AzureDedicatedCircuitProperties], CloudException
        + FullyQualifiedErrorId : Microsoft.WindowsAzure.Commands.ExpressRoute.SetAzureDedicatedCircuitPropertiesCommand


## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a><span data-ttu-id="65b21-229">Sağlamayı kaldırmayı ve bir expressroute bağlantı hattı silme</span><span class="sxs-lookup"><span data-stu-id="65b21-229">Deprovisioning and deleting an ExpressRoute circuit</span></span>

### <a name="considerations"></a><span data-ttu-id="65b21-230">Dikkat edilmesi gerekenler</span><span class="sxs-lookup"><span data-stu-id="65b21-230">Considerations</span></span>

* <span data-ttu-id="65b21-231">Expressroute bağlantı hattı başarılı olması bu işlem için tüm sanal ağlardan bağlantısını gerekir.</span><span class="sxs-lookup"><span data-stu-id="65b21-231">You must unlink all virtual networks from the ExpressRoute circuit for this operation to succeed.</span></span> <span data-ttu-id="65b21-232">Bu işlem başarısız olursa, devresine bağlı sanal ağlar olup olmadığını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="65b21-232">Check to see if you have any virtual networks that are linked to the circuit if this operation fails.</span></span>
* <span data-ttu-id="65b21-233">Sağlama durumu ExpressRoute bağlantı hattı hizmet sağlayıcı ise **sağlama** veya **hazırlandı** kendi tarafında hattı yetkisini kaldırma için hizmet sağlayıcınıza birlikte çalışmalısınız.</span><span class="sxs-lookup"><span data-stu-id="65b21-233">If the ExpressRoute circuit service provider provisioning state is **Provisioning** or **Provisioned** you must work with your service provider to deprovision the circuit on their side.</span></span> <span data-ttu-id="65b21-234">Kaynakları ayırabilir ve hizmet sağlayıcısı devre sağlama kaldırma işlemi tamamlandıktan ve bize bildiren kadar sizi faturalandırmak devam eder.</span><span class="sxs-lookup"><span data-stu-id="65b21-234">We will continue to reserve resources and bill you until the service provider completes deprovisioning the circuit and notifies us.</span></span>
* <span data-ttu-id="65b21-235">Hizmet sağlayıcısı hattı sağlaması kaldırılıyor. sağlaması değilse (sağlama durumu hizmet sağlayıcısı kümesine **sağlanmadı**), ardından bağlantı hattı silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="65b21-235">If the service provider has deprovisioned the circuit (the service provider provisioning state is set to **Not provisioned**) you can then delete the circuit.</span></span> <span data-ttu-id="65b21-236">Bu bağlantı hattı için fatura durdurur.</span><span class="sxs-lookup"><span data-stu-id="65b21-236">This will stop billing for the circuit.</span></span>

#### <a name="delete-a-circuit"></a><span data-ttu-id="65b21-237">Bir bağlantı hattı Sil</span><span class="sxs-lookup"><span data-stu-id="65b21-237">Delete a circuit</span></span>

<span data-ttu-id="65b21-238">Aşağıdaki komutu çalıştırarak, expressroute bağlantı hattı silebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="65b21-238">You can delete your ExpressRoute circuit by running the following command:</span></span>

    Remove-AzureDedicatedCircuit -ServiceKey "*********************************"



## <a name="next-steps"></a><span data-ttu-id="65b21-239">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="65b21-239">Next steps</span></span>
<span data-ttu-id="65b21-240">Bağlantı hattınız oluşturduktan sonra aşağıdakileri yaptığınızdan emin olun:</span><span class="sxs-lookup"><span data-stu-id="65b21-240">After you create your circuit, make sure that you do the following:</span></span>

* [<span data-ttu-id="65b21-241">Oluşturma ve expressroute bağlantı hattı için yönlendirmeyi değiştirme</span><span class="sxs-lookup"><span data-stu-id="65b21-241">Create and modify routing for your ExpressRoute circuit</span></span>](expressroute-howto-routing-classic.md)
* [<span data-ttu-id="65b21-242">Sanal ağ, ExpressRoute devresine bağlama</span><span class="sxs-lookup"><span data-stu-id="65b21-242">Link your virtual network to your ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-classic.md)

