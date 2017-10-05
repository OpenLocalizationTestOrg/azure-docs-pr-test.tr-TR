---
title: "Yönlendirme (bir ExpressRoute için eşliği) hattı yapılandırma: Azure: Klasik | Microsoft Docs"
description: "Bu makalede, bir ExpressRoute bağlantı hattı için özel, ortak ve Microsoft eşlemesinin nasıl oluşturulduğu ve sağlandığı adım adım anlatılmaktadır. Bu makalede ayrıca bağlantı hattınızın durumunu denetleme, bağlantı hattını güncelleştirme veya silme işlemlerinin nasıl yapıldığı da anlatılmaktadır."
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: a4bd39d2-373a-467a-8b06-36cfcc1027d2
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/21/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: 37713db70f3ae837edafc997b78b16b121d0a885
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="create-and-modify-peering-for-an-expressroute-circuit-classic"></a><span data-ttu-id="96d47-104">Oluşturma ve bir expressroute bağlantı hattı (Klasik) için eşleme değiştirme</span><span class="sxs-lookup"><span data-stu-id="96d47-104">Create and modify peering for an ExpressRoute circuit (classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="96d47-105">Azure portal</span><span class="sxs-lookup"><span data-stu-id="96d47-105">Azure portal</span></span>](expressroute-howto-routing-portal-resource-manager.md)
> * [<span data-ttu-id="96d47-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="96d47-106">PowerShell</span></span>](expressroute-howto-routing-arm.md)
> * [<span data-ttu-id="96d47-107">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="96d47-107">Azure CLI</span></span>](howto-routing-cli.md)
> * [<span data-ttu-id="96d47-108">Video - özel eşliği</span><span class="sxs-lookup"><span data-stu-id="96d47-108">Video - Private peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-private-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="96d47-109">Video - ortak eşleme</span><span class="sxs-lookup"><span data-stu-id="96d47-109">Video - Public peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-public-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="96d47-110">Video - Microsoft eşlemesi</span><span class="sxs-lookup"><span data-stu-id="96d47-110">Video - Microsoft peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-microsoft-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="96d47-111">PowerShell (klasik)</span><span class="sxs-lookup"><span data-stu-id="96d47-111">PowerShell (classic)</span></span>](expressroute-howto-routing-classic.md)
> 

<span data-ttu-id="96d47-112">Bu makalede, PowerShell ve klasik dağıtım modeli kullanarak bir expressroute için yönlendirme yapılandırması oluşturma ve yönetme için adım adım anlatılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="96d47-112">This article walks you through the steps to create and manage routing configuration for an ExpressRoute circuit using PowerShell and the classic deployment model.</span></span> <span data-ttu-id="96d47-113">Aşağıdaki adımlarda ayrıca bir ExpressRoute bağlantı hattının durumunu denetleme, güncelleştirme veya bağlantı hattını silme ve eşlemelerin sağlamasını kaldırma işlemleri de anlatılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="96d47-113">The steps below will also show you how to check the status, update, or delete and deprovision peerings for an ExpressRoute circuit.</span></span>

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

<span data-ttu-id="96d47-114">**Azure dağıtım modelleri hakkında**</span><span class="sxs-lookup"><span data-stu-id="96d47-114">**About Azure deployment models**</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]


## <a name="configuration-prerequisites"></a><span data-ttu-id="96d47-115">Yapılandırma önkoşulları</span><span class="sxs-lookup"><span data-stu-id="96d47-115">Configuration prerequisites</span></span>
* <span data-ttu-id="96d47-116">Azure Hizmet Yönetimi (SM) PowerShell cmdlet'lerinin en yeni sürümünü gerekir.</span><span class="sxs-lookup"><span data-stu-id="96d47-116">You will need the latest version of the Azure Service Management (SM) PowerShell cmdlets.</span></span> <span data-ttu-id="96d47-117">Daha fazla bilgi için bkz: [Azure PowerShell cmdlet'leri ile çalışmaya başlama](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="96d47-117">For more information, see [Getting started with Azure PowerShell cmdlets](/powershell/azure/overview).</span></span>  
* <span data-ttu-id="96d47-118">Yapılandırmaya başlamadan önce [önkoşullar](expressroute-prerequisites.md) sayfasını, [yönlendirme gereksinimleri](expressroute-routing.md) sayfasını ve [iş akışları](expressroute-workflows.md) sayfasını gözden geçirdiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="96d47-118">Make sure that you have reviewed the [prerequisites](expressroute-prerequisites.md) page, the [routing requirements](expressroute-routing.md) page, and the [workflows](expressroute-workflows.md) page before you begin configuration.</span></span>
* <span data-ttu-id="96d47-119">Etkin bir ExpressRoute bağlantı hattınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="96d47-119">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="96d47-120">Yönergeleri izleyerek [bir expressroute bağlantı hattı oluşturma](expressroute-howto-circuit-classic.md) ve devam etmeden önce bağlantı sağlayıcınız tarafından etkinleştirilen hattı sahip.</span><span class="sxs-lookup"><span data-stu-id="96d47-120">Follow the instructions to [create an ExpressRoute circuit](expressroute-howto-circuit-classic.md) and have the circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="96d47-121">Aşağıda açıklanan cmdlet’leri çalıştırmanız için ExpressRoute bağlantı hattının sağlanmış ve etkin durumda olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="96d47-121">The ExpressRoute circuit must be in a provisioned and enabled state for you to be able to run the cmdlets described below.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="96d47-122">Bu yönergeler yalnızca Katman 2 bağlantı hizmetleri sunan hizmet sağlayıcıları ile oluşturulan bağlantı hatları için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="96d47-122">These instructions only apply to circuits created with service providers offering Layer 2 connectivity services.</span></span> <span data-ttu-id="96d47-123">Yönetilen Katman 3 hizmetleri (genellikle MPLS gibi bir IPVPN) sunan bir hizmet sağlayıcısı kullanıyorsanız, bağlantı sağlayıcınız yönlendirmeyi sizin için yapılandırır ve yönetir.</span><span class="sxs-lookup"><span data-stu-id="96d47-123">If you are using a service provider offering managed Layer 3 services (typically an IPVPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span>
> 
> 

<span data-ttu-id="96d47-124">Bir ExpressRoute bağlantı hattı için bir, iki veya üç eşlemenin tamamını (Azure özel, Azure ortak ve Microsoft) yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="96d47-124">You can configure one, two, or all three peerings (Azure private, Azure public and Microsoft) for an ExpressRoute circuit.</span></span> <span data-ttu-id="96d47-125">Eşlemeleri seçtiğiniz herhangi bir sırayla yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="96d47-125">You can configure peerings in any order you choose.</span></span> <span data-ttu-id="96d47-126">Ancak, her eşlemenin yapılandırmasını birer birer tamamladığınızdan emin olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="96d47-126">However, you must make sure that you complete the configuration of each peering one at a time.</span></span>


### <a name="log-in-to-your-azure-account-and-select-a-subscription"></a><span data-ttu-id="96d47-127">Azure hesabınızda oturum açın ve bir abonelik seçin</span><span class="sxs-lookup"><span data-stu-id="96d47-127">Log in to your Azure account and select a subscription</span></span>
1. <span data-ttu-id="96d47-128">PowerShell konsolunuzu yükseltilmiş haklarla açın ve hesabınıza bağlanın.</span><span class="sxs-lookup"><span data-stu-id="96d47-128">Open your PowerShell console with elevated rights and connect to your account.</span></span> <span data-ttu-id="96d47-129">Bağlanmanıza yardımcı olması için aşağıdaki örneği kullanın:</span><span class="sxs-lookup"><span data-stu-id="96d47-129">Use the following example to help you connect:</span></span>

        Login-AzureRmAccount

2. <span data-ttu-id="96d47-130">Hesapla ilişkili abonelikleri kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="96d47-130">Check the subscriptions for the account.</span></span>

        Get-AzureRmSubscription

3. <span data-ttu-id="96d47-131">Birden fazla aboneliğiniz varsa, kullanmak istediğiniz aboneliği seçin.</span><span class="sxs-lookup"><span data-stu-id="96d47-131">If you have more than one subscription, select the subscription that you want to use.</span></span>

        Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"

4. <span data-ttu-id="96d47-132">Ardından, Klasik dağıtım modeli için PowerShell için Azure aboneliğinize eklemek için aşağıdaki cmdlet'i kullanın.</span><span class="sxs-lookup"><span data-stu-id="96d47-132">Next, use the following cmdlet to add your Azure subscription to PowerShell for the classic deployment model.</span></span>

        Add-AzureAccount


## <a name="azure-private-peering"></a><span data-ttu-id="96d47-133">Azure özel eşlemesi</span><span class="sxs-lookup"><span data-stu-id="96d47-133">Azure private peering</span></span>
<span data-ttu-id="96d47-134">Bu bölümde bir ExpressRoute bağlantı hattı için Azure özel eşleme yapılandırmasını oluşturma, alma, güncelleştirme ve silme hakkında yönergeler açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="96d47-134">This section provides instructions on how to create, get, update, and delete the Azure private peering configuration for an ExpressRoute circuit.</span></span> 

### <a name="to-create-azure-private-peering"></a><span data-ttu-id="96d47-135">Azure özel eşlemesi oluşturmak için</span><span class="sxs-lookup"><span data-stu-id="96d47-135">To create Azure private peering</span></span>
1. <span data-ttu-id="96d47-136">**ExpressRoute için PowerShell modülünü içeri aktarın.**</span><span class="sxs-lookup"><span data-stu-id="96d47-136">**Import the PowerShell module for ExpressRoute.**</span></span>
   
    <span data-ttu-id="96d47-137">ExpressRoute cmdlet'lerini kullanmaya başlamak için PowerShell oturumuna Azure ve ExpressRoute modülleri içeri aktarmalısınız.</span><span class="sxs-lookup"><span data-stu-id="96d47-137">You must import the Azure and ExpressRoute modules into the PowerShell session in order to start using the ExpressRoute cmdlets.</span></span> <span data-ttu-id="96d47-138">Azure ve ExpressRoute modüllerini PowerShell oturumuna içeri aktarmak için aşağıdaki komutları çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="96d47-138">Run the following commands to import the Azure and ExpressRoute modules into the PowerShell session.</span></span>  
   
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
2. <span data-ttu-id="96d47-139">**Bir expressroute bağlantı hattı oluşturun.**</span><span class="sxs-lookup"><span data-stu-id="96d47-139">**Create an ExpressRoute circuit.**</span></span>
   
    <span data-ttu-id="96d47-140">Bir [ExpressRoute bağlantı hattı](expressroute-howto-circuit-classic.md) oluşturmak için yönergeleri izleyin ve bağlantı sağlayıcısından bağlantı hattını sağlamasını isteyin.</span><span class="sxs-lookup"><span data-stu-id="96d47-140">Follow the instructions to create an [ExpressRoute circuit](expressroute-howto-circuit-classic.md) and have it provisioned by the connectivity provider.</span></span> <span data-ttu-id="96d47-141">Bağlantı sağlayıcınız yönetilen Katman 3 hizmetleri sunuyorsa, bağlantı sağlayıcınızdan sizin için Azure özel eşlemeyi etkinleştirmesini isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="96d47-141">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider to enable Azure private peering for you.</span></span> <span data-ttu-id="96d47-142">Bu durumda, sonraki bölümlerde listelenen yönergeleri izlemeniz gerekmez.</span><span class="sxs-lookup"><span data-stu-id="96d47-142">In that case, you won't need to follow instructions listed in the next sections.</span></span> <span data-ttu-id="96d47-143">Ancak, bağlantı sağlayıcınız yönlendirmeyi sizin için yönetmiyorsa, bağlantı hattınızı oluşturduktan sonra aşağıdaki yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="96d47-143">However, if your connectivity provider does not manage routing for you, after creating your circuit, follow the instructions below.</span></span> 
3. <span data-ttu-id="96d47-144">**Expressroute bağlantı hattının sağlandığından emin olmak için kontrol edin.**</span><span class="sxs-lookup"><span data-stu-id="96d47-144">**Check the ExpressRoute circuit to ensure it is provisioned.**</span></span>
   
    <span data-ttu-id="96d47-145">Önce ExpressRoute ağ geçidinin Sağlandığından ve Etkin durumda olduğundan emin olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="96d47-145">You must first check to see if the ExpressRoute circuit is Provisioned and also Enabled.</span></span> <span data-ttu-id="96d47-146">Aşağıdaki örneğe bakın.</span><span class="sxs-lookup"><span data-stu-id="96d47-146">See the example below.</span></span>
   
        PS C:\> Get-AzureDedicatedCircuit -ServiceKey "*********************************"
   
        Bandwidth                        : 200
        CircuitName                      : MyTestCircuit
        Location                         : Silicon Valley
        ServiceKey                       : *********************************
        ServiceProviderName              : equinix
        ServiceProviderProvisioningState : Provisioned
        Sku                              : Standard
        Status                           : Enabled
   
    <span data-ttu-id="96d47-147">Bağlantı hattı hazırlandı ve etkin gösterdiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="96d47-147">Make sure that the circuit shows as Provisioned and Enabled.</span></span> <span data-ttu-id="96d47-148">Seçili değilse, bağlantı hattınız gerekli durumu ve durumunu almak için bağlantı sağlayıcınız ile çalışır.</span><span class="sxs-lookup"><span data-stu-id="96d47-148">If it doesn't, work with your connectivity provider to get your circuit to the required state and status.</span></span>
   
        ServiceProviderProvisioningState : Provisioned
        Status                           : Enabled
4. <span data-ttu-id="96d47-149">**Bağlantı hattı için Azure özel eşlemesini yapılandırın.**</span><span class="sxs-lookup"><span data-stu-id="96d47-149">**Configure Azure private peering for the circuit.**</span></span>
   
    <span data-ttu-id="96d47-150">Sonraki adımlara devam etmeden önce aşağıdaki öğelerin bulunduğundan emin olun:</span><span class="sxs-lookup"><span data-stu-id="96d47-150">Make sure that you have the following items before you proceed with the next steps:</span></span>
   
   * <span data-ttu-id="96d47-151">Birincil bağlantı için bir /30 alt ağı.</span><span class="sxs-lookup"><span data-stu-id="96d47-151">A /30 subnet for the primary link.</span></span> <span data-ttu-id="96d47-152">Bu, sanal ağlar için ayrılmış herhangi bir adres alanının parçası olmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="96d47-152">This must not be part of any address space reserved for virtual networks.</span></span>
   * <span data-ttu-id="96d47-153">İkincil bağlantı için bir /30 alt ağı.</span><span class="sxs-lookup"><span data-stu-id="96d47-153">A /30 subnet for the secondary link.</span></span> <span data-ttu-id="96d47-154">Bu, sanal ağlar için ayrılmış herhangi bir adres alanının parçası olmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="96d47-154">This must not be part of any address space reserved for virtual networks.</span></span>
   * <span data-ttu-id="96d47-155">Bu eşlemenin kurulacağı geçerli bir VLAN kimliği.</span><span class="sxs-lookup"><span data-stu-id="96d47-155">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="96d47-156">Bağlantı hattındaki başka bir eşlemenin aynı VLAN kimliğini kullanmadığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="96d47-156">Ensure that no other peering in the circuit uses the same VLAN ID.</span></span>
   * <span data-ttu-id="96d47-157">Eşleme için AS numarası.</span><span class="sxs-lookup"><span data-stu-id="96d47-157">AS number for peering.</span></span> <span data-ttu-id="96d47-158">2 bayt ve 4 bayt AS numaralarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="96d47-158">You can use both 2-byte and 4-byte AS numbers.</span></span> <span data-ttu-id="96d47-159">Bu eşleme için özel bir AS numarası kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="96d47-159">You can use a private AS number for this peering.</span></span> <span data-ttu-id="96d47-160">65515’i kullanmadığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="96d47-160">Ensure that you are not using 65515.</span></span>
   * <span data-ttu-id="96d47-161">Kullanmayı seçerseniz bir MD5 karma değeri.</span><span class="sxs-lookup"><span data-stu-id="96d47-161">An MD5 hash if you choose to use one.</span></span> <span data-ttu-id="96d47-162">**Bu isteğe bağlıdır**.</span><span class="sxs-lookup"><span data-stu-id="96d47-162">**This is optional**.</span></span>
     
    <span data-ttu-id="96d47-163">Bağlantı hattınız için Azure özel eşlemesini yapılandırmak üzere aşağıdaki cmdlet’i çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="96d47-163">You can run the following cmdlet to configure Azure private peering for your circuit.</span></span>
     
        <span data-ttu-id="96d47-164">Yeni AzureBGPPeering - AccessType özel - ServiceKey "***" - PrimaryPeerSubnet "10.0.0.0/30" - SecondaryPeerSubnet "10.0.0.4/30" - PeerAsn 1234 - Vlanıd 100</span><span class="sxs-lookup"><span data-stu-id="96d47-164">New-AzureBGPPeering -AccessType Private -ServiceKey "*********************************" -PrimaryPeerSubnet "10.0.0.0/30" -SecondaryPeerSubnet "10.0.0.4/30" -PeerAsn 1234 -VlanId 100</span></span>
     
    <span data-ttu-id="96d47-165">Bir MD5 karma değeri kullanmayı seçerseniz, aşağıdaki cmdlet'i kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="96d47-165">You can use the cmdlet below if you choose to use an MD5 hash.</span></span>
     
        <span data-ttu-id="96d47-166">Yeni AzureBGPPeering - AccessType özel - ServiceKey "***" - PrimaryPeerSubnet "10.0.0.0/30" - SecondaryPeerSubnet "10.0.0.4/30" - PeerAsn 1234 - Vlanıd 100 - SharedKey "A1B2C3D4"</span><span class="sxs-lookup"><span data-stu-id="96d47-166">New-AzureBGPPeering -AccessType Private -ServiceKey "*********************************" -PrimaryPeerSubnet "10.0.0.0/30" -SecondaryPeerSubnet "10.0.0.4/30" -PeerAsn 1234 -VlanId 100 -SharedKey "A1B2C3D4"</span></span>
     
     > [!IMPORTANT]
     > <span data-ttu-id="96d47-167">AS numaranızı müşteri ASN’si değil eşleme ASN’si olarak belirttiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="96d47-167">Ensure that you specify your AS number as peering ASN, not customer ASN.</span></span>
     > 
     > 

### <a name="to-view-azure-private-peering-details"></a><span data-ttu-id="96d47-168">Azure özel eşleme ayrıntılarını görüntülemek için</span><span class="sxs-lookup"><span data-stu-id="96d47-168">To view Azure private peering details</span></span>
<span data-ttu-id="96d47-169">Aşağıdaki cmdlet'i kullanarak yapılandırma ayrıntılarını alabilirsiniz</span><span class="sxs-lookup"><span data-stu-id="96d47-169">You can get configuration details using the following cmdlet</span></span>

    Get-AzureBGPPeering -AccessType Private -ServiceKey "*********************************"

    AdvertisedPublicPrefixes       : 
    AdvertisedPublicPrefixesState  : Configured
    AzureAsn                       : 12076
    CustomerAutonomousSystemNumber : 
    PeerAsn                        : 1234
    PrimaryAzurePort               : 
    PrimaryPeerSubnet              : 10.0.0.0/30
    RoutingRegistryName            : 
    SecondaryAzurePort             : 
    SecondaryPeerSubnet            : 10.0.0.4/30
    State                          : Enabled
    VlanId                         : 100


### <a name="to-update-azure-private-peering-configuration"></a><span data-ttu-id="96d47-170">Azure özel eşleme yapılandırmasını güncelleştirmek için</span><span class="sxs-lookup"><span data-stu-id="96d47-170">To update Azure private peering configuration</span></span>
<span data-ttu-id="96d47-171">Aşağıdaki cmdlet'i kullanarak yapılandırmanın herhangi bir bölümünü güncelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="96d47-171">You can update any part of the configuration using the following cmdlet.</span></span> <span data-ttu-id="96d47-172">Aşağıdaki örnekte, bağlantı hattının VLAN kimliği 100'den 500’e güncelleştiriliyor.</span><span class="sxs-lookup"><span data-stu-id="96d47-172">In the example below, the VLAN ID of the circuit is being updated from 100 to 500.</span></span>

    Set-AzureBGPPeering -AccessType Private -ServiceKey "*********************************" -PrimaryPeerSubnet "10.0.0.0/30" -SecondaryPeerSubnet "10.0.0.4/30" -PeerAsn 1234 -VlanId 500 -SharedKey "A1B2C3D4"

### <a name="to-delete-azure-private-peering"></a><span data-ttu-id="96d47-173">Azure özel eşlemesini silmek için</span><span class="sxs-lookup"><span data-stu-id="96d47-173">To delete Azure private peering</span></span>
<span data-ttu-id="96d47-174">Aşağıdaki cmdlet'i çalıştırarak eşleme yapılandırmanızı kaldırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="96d47-174">You can remove your peering configuration by running the following cmdlet.</span></span>

> [!WARNING]
> <span data-ttu-id="96d47-175">Bu cmdlet'i çalıştırmadan önce ExpressRoute bağlantı hattından tüm sanal ağların bağlantısının kaldırıldığından emin olmalısınız.</span><span class="sxs-lookup"><span data-stu-id="96d47-175">You must ensure that all virtual networks are unlinked from the ExpressRoute circuit before running this cmdlet.</span></span> 
> 
> 

    Remove-AzureBGPPeering -AccessType Private -ServiceKey "*********************************"


## <a name="azure-public-peering"></a><span data-ttu-id="96d47-176">Azure ortak eşleme</span><span class="sxs-lookup"><span data-stu-id="96d47-176">Azure public peering</span></span>
<span data-ttu-id="96d47-177">Bu bölümde bir ExpressRoute bağlantı hattı için Azure ortak eşleme yapılandırmasını oluşturma, alma, güncelleştirme ve silme hakkında yönergeler açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="96d47-177">This section provides instructions on how to create, get, update and delete the Azure public peering configuration for an ExpressRoute circuit.</span></span>

### <a name="to-create-azure-public-peering"></a><span data-ttu-id="96d47-178">Azure ortak eşlemesi oluşturmak için</span><span class="sxs-lookup"><span data-stu-id="96d47-178">To create Azure public peering</span></span>
1. <span data-ttu-id="96d47-179">**ExpressRoute için PowerShell modülünü içeri aktarın.**</span><span class="sxs-lookup"><span data-stu-id="96d47-179">**Import the PowerShell module for ExpressRoute.**</span></span>
   
    <span data-ttu-id="96d47-180">ExpressRoute cmdlet'lerini kullanmaya başlamak için PowerShell oturumuna Azure ve ExpressRoute modülleri içeri aktarmalısınız.</span><span class="sxs-lookup"><span data-stu-id="96d47-180">You must import the Azure and ExpressRoute modules into the PowerShell session in order to start using the ExpressRoute cmdlets.</span></span> <span data-ttu-id="96d47-181">Azure ve ExpressRoute modüllerini PowerShell oturumuna içeri aktarmak için aşağıdaki komutları çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="96d47-181">Run the following commands to import the Azure and ExpressRoute modules into the PowerShell session.</span></span> 
   
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
2. <span data-ttu-id="96d47-182">**ExpressRoute bağlantı hattı oluşturma**</span><span class="sxs-lookup"><span data-stu-id="96d47-182">**Create an ExpressRoute circuit**</span></span>
   
    <span data-ttu-id="96d47-183">Bir [ExpressRoute bağlantı hattı](expressroute-howto-circuit-classic.md) oluşturmak için yönergeleri izleyin ve bağlantı sağlayıcısından bağlantı hattını sağlamasını isteyin.</span><span class="sxs-lookup"><span data-stu-id="96d47-183">Follow the instructions to create an [ExpressRoute circuit](expressroute-howto-circuit-classic.md) and have it provisioned by the connectivity provider.</span></span> <span data-ttu-id="96d47-184">Bağlantı sağlayıcınız yönetilen Katman 3 hizmetleri sunuyorsa, bağlantı sağlayıcınızdan sizin için Azure ortak eşlemeyi etkinleştirmesini isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="96d47-184">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider to enable Azure public peering for you.</span></span> <span data-ttu-id="96d47-185">Bu durumda, sonraki bölümlerde listelenen yönergeleri izlemeniz gerekmez.</span><span class="sxs-lookup"><span data-stu-id="96d47-185">In that case, you won't need to follow instructions listed in the next sections.</span></span> <span data-ttu-id="96d47-186">Ancak, bağlantı sağlayıcınız yönlendirmeyi sizin için yönetmiyorsa, bağlantı hattınızı oluşturduktan sonra aşağıdaki yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="96d47-186">However, if your connectivity provider does not manage routing for you, after creating your circuit, follow the instructions below.</span></span>
3. <span data-ttu-id="96d47-187">**Expressroute bağlantı hattının sağlandığından emin olmak için kontrol edin**</span><span class="sxs-lookup"><span data-stu-id="96d47-187">**Check ExpressRoute circuit to ensure it is provisioned**</span></span>
   
    <span data-ttu-id="96d47-188">Önce ExpressRoute ağ geçidinin Sağlandığından ve Etkin durumda olduğundan emin olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="96d47-188">You must first check to see if the ExpressRoute circuit is Provisioned and also Enabled.</span></span> <span data-ttu-id="96d47-189">Aşağıdaki örneğe bakın.</span><span class="sxs-lookup"><span data-stu-id="96d47-189">See the example below.</span></span>
   
        PS C:\> Get-AzureDedicatedCircuit -ServiceKey "*********************************"
   
        Bandwidth                        : 200
        CircuitName                      : MyTestCircuit
        Location                         : Silicon Valley
        ServiceKey                       : *********************************
        ServiceProviderName              : equinix
        ServiceProviderProvisioningState : Provisioned
        Sku                              : Standard
        Status                           : Enabled
   
    <span data-ttu-id="96d47-190">Bağlantı hattı hazırlandı ve etkin gösterdiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="96d47-190">Make sure that the circuit shows as Provisioned and Enabled.</span></span> <span data-ttu-id="96d47-191">Seçili değilse, bağlantı hattınız gerekli durumu ve durumunu almak için bağlantı sağlayıcınız ile çalışır.</span><span class="sxs-lookup"><span data-stu-id="96d47-191">If it doesn't, work with your connectivity provider to get your circuit to the required state and status.</span></span>
   
        ServiceProviderProvisioningState : Provisioned
        Status                           : Enabled
4. <span data-ttu-id="96d47-192">**Bağlantı hattı için Azure ortak eşlemesini yapılandırın**</span><span class="sxs-lookup"><span data-stu-id="96d47-192">**Configure Azure public peering for the circuit**</span></span>
   
    <span data-ttu-id="96d47-193">Devam etmeden önce aşağıdaki bilgilere sahip olduğunuzdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="96d47-193">Ensure that you have the following information before you proceed further.</span></span>
   
   * <span data-ttu-id="96d47-194">Birincil bağlantı için bir /30 alt ağı.</span><span class="sxs-lookup"><span data-stu-id="96d47-194">A /30 subnet for the primary link.</span></span> <span data-ttu-id="96d47-195">Bu geçerli bir ortak IPv4 öneki olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="96d47-195">This must be a valid public IPv4 prefix.</span></span>
   * <span data-ttu-id="96d47-196">İkincil bağlantı için bir /30 alt ağı.</span><span class="sxs-lookup"><span data-stu-id="96d47-196">A /30 subnet for the secondary link.</span></span> <span data-ttu-id="96d47-197">Bu geçerli bir ortak IPv4 öneki olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="96d47-197">This must be a valid public IPv4 prefix.</span></span>
   * <span data-ttu-id="96d47-198">Bu eşlemenin kurulacak geçerli bir VLAN kimliği.</span><span class="sxs-lookup"><span data-stu-id="96d47-198">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="96d47-199">Bağlantı hattındaki başka bir eşlemenin aynı VLAN kimliğini kullanmadığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="96d47-199">Ensure that no other peering in the circuit uses the same VLAN ID.</span></span>
   * <span data-ttu-id="96d47-200">Eşleme için AS numarası.</span><span class="sxs-lookup"><span data-stu-id="96d47-200">AS number for peering.</span></span> <span data-ttu-id="96d47-201">2 bayt ve 4 bayt AS numaralarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="96d47-201">You can use both 2-byte and 4-byte AS numbers.</span></span>
   * <span data-ttu-id="96d47-202">Kullanmayı seçerseniz bir MD5 karma değeri.</span><span class="sxs-lookup"><span data-stu-id="96d47-202">An MD5 hash if you choose to use one.</span></span> <span data-ttu-id="96d47-203">**Bu isteğe bağlıdır**.</span><span class="sxs-lookup"><span data-stu-id="96d47-203">**This is optional**.</span></span>
     
    <span data-ttu-id="96d47-204">Bağlantı hattınız için Azure özel eşlemesini yapılandırmak üzere aşağıdaki cmdlet’i çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="96d47-204">You can run the following cmdlet to configure Azure public peering for your circuit</span></span>
     
        <span data-ttu-id="96d47-205">Yeni AzureBGPPeering - AccessType ortak - ServiceKey "***" - PrimaryPeerSubnet "131.107.0.0/30" - SecondaryPeerSubnet "131.107.0.4/30" - PeerAsn 1234 - Vlanıd 200</span><span class="sxs-lookup"><span data-stu-id="96d47-205">New-AzureBGPPeering -AccessType Public -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -PeerAsn 1234 -VlanId 200</span></span>
     
    <span data-ttu-id="96d47-206">Bir MD5 karma değeri kullanmayı seçerseniz, aşağıdaki cmdlet'i kullanabilirsiniz</span><span class="sxs-lookup"><span data-stu-id="96d47-206">You can use the cmdlet below if you choose to use an MD5 hash</span></span>
     
        <span data-ttu-id="96d47-207">Yeni AzureBGPPeering - AccessType ortak - ServiceKey "***" - PrimaryPeerSubnet "131.107.0.0/30" - SecondaryPeerSubnet "131.107.0.4/30" - PeerAsn 1234 - Vlanıd 200 - SharedKey "A1B2C3D4"</span><span class="sxs-lookup"><span data-stu-id="96d47-207">New-AzureBGPPeering -AccessType Public -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -PeerAsn 1234 -VlanId 200 -SharedKey "A1B2C3D4"</span></span>
     
     > [!IMPORTANT]
     > <span data-ttu-id="96d47-208">AS numaranızı müşteri ASN’si değil eşleme ASN’si olarak belirttiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="96d47-208">Ensure that you specify your AS number as peering ASN and not customer ASN.</span></span>
     > 
     > 

### <a name="to-view-azure-public-peering-details"></a><span data-ttu-id="96d47-209">Azure ortak eşleme ayrıntılarını görüntülemek için</span><span class="sxs-lookup"><span data-stu-id="96d47-209">To view Azure public peering details</span></span>
<span data-ttu-id="96d47-210">Aşağıdaki cmdlet'i kullanarak yapılandırma ayrıntılarını alabilirsiniz</span><span class="sxs-lookup"><span data-stu-id="96d47-210">You can get configuration details using the following cmdlet</span></span>

    Get-AzureBGPPeering -AccessType Public -ServiceKey "*********************************"

    AdvertisedPublicPrefixes       : 
    AdvertisedPublicPrefixesState  : Configured
    AzureAsn                       : 12076
    CustomerAutonomousSystemNumber : 
    PeerAsn                        : 1234
    PrimaryAzurePort               : 
    PrimaryPeerSubnet              : 131.107.0.0/30
    RoutingRegistryName            : 
    SecondaryAzurePort             : 
    SecondaryPeerSubnet            : 131.107.0.4/30
    State                          : Enabled
    VlanId                         : 200


### <a name="to-update-azure-public-peering-configuration"></a><span data-ttu-id="96d47-211">Azure ortak eşleme yapılandırmasını güncelleştirmek için</span><span class="sxs-lookup"><span data-stu-id="96d47-211">To update Azure public peering configuration</span></span>
<span data-ttu-id="96d47-212">Aşağıdaki cmdlet'i kullanarak yapılandırmanın herhangi bir bölümünü güncelleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="96d47-212">You can update any part of the configuration using the following cmdlet</span></span>

    Set-AzureBGPPeering -AccessType Public -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -PeerAsn 1234 -VlanId 600 -SharedKey "A1B2C3D4"

<span data-ttu-id="96d47-213">Yukarıdaki örnekte, bağlantı hattının VLAN kimliği 200'den 600’e güncelleştiriliyor.</span><span class="sxs-lookup"><span data-stu-id="96d47-213">The VLAN ID of the circuit is being updated from 200 to 600 in the above example.</span></span>

### <a name="to-delete-azure-public-peering"></a><span data-ttu-id="96d47-214">Azure ortak eşlemesini silmek için</span><span class="sxs-lookup"><span data-stu-id="96d47-214">To delete Azure public peering</span></span>
<span data-ttu-id="96d47-215">Aşağıdaki cmdlet'i çalıştırarak eşleme yapılandırmanızı kaldırabilirsiniz</span><span class="sxs-lookup"><span data-stu-id="96d47-215">You can remove your peering configuration by running the following cmdlet</span></span>

    Remove-AzureBGPPeering -AccessType Public -ServiceKey "*********************************"

## <a name="microsoft-peering"></a><span data-ttu-id="96d47-216">Microsoft eşlemesi</span><span class="sxs-lookup"><span data-stu-id="96d47-216">Microsoft peering</span></span>
<span data-ttu-id="96d47-217">Bu bölümde bir ExpressRoute bağlantı hattı için Microsoft eşleme yapılandırmasını oluşturma, alma, güncelleştirme ve silme hakkında yönergeler açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="96d47-217">This section provides instructions on how to create, get, update and delete the Microsoft peering configuration for an ExpressRoute circuit.</span></span> 

### <a name="to-create-microsoft-peering"></a><span data-ttu-id="96d47-218">Microsoft eşlemesi oluşturmak için</span><span class="sxs-lookup"><span data-stu-id="96d47-218">To create Microsoft peering</span></span>
1. <span data-ttu-id="96d47-219">**ExpressRoute için PowerShell modülünü içeri aktarın.**</span><span class="sxs-lookup"><span data-stu-id="96d47-219">**Import the PowerShell module for ExpressRoute.**</span></span>
   
    <span data-ttu-id="96d47-220">ExpressRoute cmdlet'lerini kullanmaya başlamak için PowerShell oturumuna Azure ve ExpressRoute modülleri içeri aktarmalısınız.</span><span class="sxs-lookup"><span data-stu-id="96d47-220">You must import the Azure and ExpressRoute modules into the PowerShell session in order to start using the ExpressRoute cmdlets.</span></span> <span data-ttu-id="96d47-221">Azure ve ExpressRoute modüllerini PowerShell oturumuna içeri aktarmak için aşağıdaki komutları çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="96d47-221">Run the following commands to import the Azure and ExpressRoute modules into the PowerShell session.</span></span>  
   
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
2. <span data-ttu-id="96d47-222">**ExpressRoute bağlantı hattı oluşturma**</span><span class="sxs-lookup"><span data-stu-id="96d47-222">**Create an ExpressRoute circuit**</span></span>
   
    <span data-ttu-id="96d47-223">Bir [ExpressRoute bağlantı hattı](expressroute-howto-circuit-classic.md) oluşturmak için yönergeleri izleyin ve bağlantı sağlayıcısından bağlantı hattını sağlamasını isteyin.</span><span class="sxs-lookup"><span data-stu-id="96d47-223">Follow the instructions to create an [ExpressRoute circuit](expressroute-howto-circuit-classic.md) and have it provisioned by the connectivity provider.</span></span> <span data-ttu-id="96d47-224">Bağlantı sağlayıcınız yönetilen Katman 3 hizmetleri sunuyorsa, bağlantı sağlayıcınızdan sizin için Azure özel eşlemeyi etkinleştirmesini isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="96d47-224">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider to enable Azure private peering for you.</span></span> <span data-ttu-id="96d47-225">Bu durumda, sonraki bölümlerde listelenen yönergeleri izlemeniz gerekmez.</span><span class="sxs-lookup"><span data-stu-id="96d47-225">In that case, you won't need to follow instructions listed in the next sections.</span></span> <span data-ttu-id="96d47-226">Ancak, bağlantı sağlayıcınız yönlendirmeyi sizin için yönetmiyorsa, bağlantı hattınızı oluşturduktan sonra aşağıdaki yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="96d47-226">However, if your connectivity provider does not manage routing for you, after creating your circuit, follow the instructions below.</span></span>
3. <span data-ttu-id="96d47-227">**Expressroute bağlantı hattının sağlandığından emin olmak için kontrol edin**</span><span class="sxs-lookup"><span data-stu-id="96d47-227">**Check ExpressRoute circuit to ensure it is provisioned**</span></span>
   
    <span data-ttu-id="96d47-228">Expressroute bağlantı hattı hazırlandı ve etkin durumda olup olmadığını görmek için ilk olarak işaretlemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="96d47-228">You must first check to see if the ExpressRoute circuit is in Provisioned and Enabled state.</span></span>
   
        PS C:\> Get-AzureDedicatedCircuit -ServiceKey "*********************************"
   
        Bandwidth                        : 200
        CircuitName                      : MyTestCircuit
        Location                         : Silicon Valley
        ServiceKey                       : *********************************
        ServiceProviderName              : equinix
        ServiceProviderProvisioningState : Provisioned
        Sku                              : Standard
        Status                           : Enabled
   
    <span data-ttu-id="96d47-229">Bağlantı hattı hazırlandı ve etkin gösterdiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="96d47-229">Make sure that the circuit shows as Provisioned and Enabled.</span></span> <span data-ttu-id="96d47-230">Seçili değilse, bağlantı hattınız gerekli durumu ve durumunu almak için bağlantı sağlayıcınız ile çalışır.</span><span class="sxs-lookup"><span data-stu-id="96d47-230">If it doesn't, work with your connectivity provider to get your circuit to the required state and status.</span></span>
   
        ServiceProviderProvisioningState : Provisioned
        Status                           : Enabled
4. <span data-ttu-id="96d47-231">**Microsoft bağlantı hattı için eşlemesini yapılandırın**</span><span class="sxs-lookup"><span data-stu-id="96d47-231">**Configure Microsoft peering for the circuit**</span></span>
   
    <span data-ttu-id="96d47-232">Devam etmeden önce aşağıdaki bilgilere sahip olduğunuzdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="96d47-232">Make sure that you have the following information before you proceed.</span></span>
   
   * <span data-ttu-id="96d47-233">Birincil bağlantı için bir /30 alt ağı.</span><span class="sxs-lookup"><span data-stu-id="96d47-233">A /30 subnet for the primary link.</span></span> <span data-ttu-id="96d47-234">Bu size ait ve bir RIR / IRR içinde kayıtlı bir geçerli ortak IPv4 ön eki olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="96d47-234">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
   * <span data-ttu-id="96d47-235">İkincil bağlantı için bir /30 alt ağı.</span><span class="sxs-lookup"><span data-stu-id="96d47-235">A /30 subnet for the secondary link.</span></span> <span data-ttu-id="96d47-236">Bu size ait ve bir RIR / IRR içinde kayıtlı bir geçerli ortak IPv4 ön eki olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="96d47-236">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
   * <span data-ttu-id="96d47-237">Bu eşlemenin kurulacağı geçerli bir VLAN kimliği.</span><span class="sxs-lookup"><span data-stu-id="96d47-237">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="96d47-238">Bağlantı hattındaki başka bir eşlemenin aynı VLAN kimliğini kullanmadığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="96d47-238">Ensure that no other peering in the circuit uses the same VLAN ID.</span></span>
   * <span data-ttu-id="96d47-239">Eşleme için AS numarası.</span><span class="sxs-lookup"><span data-stu-id="96d47-239">AS number for peering.</span></span> <span data-ttu-id="96d47-240">2 bayt ve 4 bayt AS numaralarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="96d47-240">You can use both 2-byte and 4-byte AS numbers.</span></span>
   * <span data-ttu-id="96d47-241">Tanıtılan önekler: BGP oturumunda tanıtmayı planladığınız tüm öneklerin bir listesini sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="96d47-241">Advertised prefixes: You must provide a list of all prefixes you plan to advertise over the BGP session.</span></span> <span data-ttu-id="96d47-242">Yalnızca genel IP adresi önekleri kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="96d47-242">Only public IP address prefixes are accepted.</span></span> <span data-ttu-id="96d47-243">Bir ön ek kümesi göndermeyi planlıyorsanız, virgülle ayrılmış bir liste gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="96d47-243">You can send a comma separated list if you plan to send a set of prefixes.</span></span> <span data-ttu-id="96d47-244">Bu önekler size bir RIR / IRR içinde kaydedilmiş olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="96d47-244">These prefixes must be registered to you in an RIR / IRR.</span></span>
   * <span data-ttu-id="96d47-245">Müşteri ASN’si: Eşleme AS numarasına kayıtlı olmayan önekler tanıtıyorsanız, kayıtlı oldukları AS numarasını belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="96d47-245">Customer ASN: If you are advertising prefixes that are not registered to the peering AS number, you can specify the AS number to which they are registered.</span></span> <span data-ttu-id="96d47-246">**Bu isteğe bağlıdır**.</span><span class="sxs-lookup"><span data-stu-id="96d47-246">**This is optional**.</span></span>
   * <span data-ttu-id="96d47-247">Yönlendirme Kayıt Defteri Adı: AS numarası ve öneklerinin kaydedildiği RIR / IRR’yi belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="96d47-247">Routing Registry Name: You can specify the RIR / IRR against which the AS number and prefixes are registered.</span></span>
   * <span data-ttu-id="96d47-248">Kullanmayı seçerseniz bir MD5 karma değeri.</span><span class="sxs-lookup"><span data-stu-id="96d47-248">An MD5 hash, if you choose to use one.</span></span> <span data-ttu-id="96d47-249">**Bu isteğe bağlıdır.**</span><span class="sxs-lookup"><span data-stu-id="96d47-249">**This is optional.**</span></span>
     
    <span data-ttu-id="96d47-250">Bağlantı hattınız için Microsoft pering yapılandırmak için aşağıdaki cmdlet'i çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="96d47-250">You can run the following cmdlet to configure Microsoft pering for your circuit</span></span>
     
        <span data-ttu-id="96d47-251">Yeni AzureBGPPeering - AccessType Microsoft - ServiceKey "***" - PrimaryPeerSubnet "131.107.0.0/30" - SecondaryPeerSubnet "131.107.0.4/30" - Vlanıd 300 - PeerAsn 1234 - CustomerAsn 2245 - AdvertisedPublicPrefixes "123.0.0.0/30" - RoutingRegistryName "ARIN" - SharedKey "A1B2C3D4"</span><span class="sxs-lookup"><span data-stu-id="96d47-251">New-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -VlanId 300 -PeerAsn 1234 -CustomerAsn 2245 -AdvertisedPublicPrefixes "123.0.0.0/30" -RoutingRegistryName "ARIN" -SharedKey "A1B2C3D4"</span></span>

### <a name="to-view-microsoft-peering-details"></a><span data-ttu-id="96d47-252">Microsoft eşleme ayrıntılarını görüntülemek için</span><span class="sxs-lookup"><span data-stu-id="96d47-252">To view Microsoft peering details</span></span>
<span data-ttu-id="96d47-253">Aşağıdaki cmdlet'i kullanarak yapılandırma ayrıntılarını alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="96d47-253">You can get configuration details using the following cmdlet.</span></span>

    Get-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************"

    AdvertisedPublicPrefixes       : 123.0.0.0/30
    AdvertisedPublicPrefixesState  : Configured
    AzureAsn                       : 12076
    CustomerAutonomousSystemNumber : 2245
    PeerAsn                        : 1234
    PrimaryAzurePort               : 
    PrimaryPeerSubnet              : 10.0.0.0/30
    RoutingRegistryName            : ARIN
    SecondaryAzurePort             : 
    SecondaryPeerSubnet            : 10.0.0.4/30
    State                          : Enabled
    VlanId                         : 300


### <a name="to-update-microsoft-peering-configuration"></a><span data-ttu-id="96d47-254">Microsoft eşlemesi yapılandırmasını güncelleştirmek için</span><span class="sxs-lookup"><span data-stu-id="96d47-254">To update Microsoft peering configuration</span></span>
<span data-ttu-id="96d47-255">Aşağıdaki cmdlet'i kullanarak yapılandırmanın herhangi bir bölümünü güncelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="96d47-255">You can update any part of the configuration using the following cmdlet.</span></span>

    Set-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -VlanId 300 -PeerAsn 1234 -CustomerAsn 2245 -AdvertisedPublicPrefixes "123.0.0.0/30" -RoutingRegistryName "ARIN" -SharedKey "A1B2C3D4"

### <a name="to-delete-microsoft-peering"></a><span data-ttu-id="96d47-256">Microsoft eşlemesini silmek için</span><span class="sxs-lookup"><span data-stu-id="96d47-256">To delete Microsoft peering</span></span>
<span data-ttu-id="96d47-257">Aşağıdaki cmdlet'i çalıştırarak eşleme yapılandırmanızı kaldırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="96d47-257">You can remove your peering configuration by running the following cmdlet.</span></span>

    Remove-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************"

## <a name="next-steps"></a><span data-ttu-id="96d47-258">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="96d47-258">Next steps</span></span>
<span data-ttu-id="96d47-259">Ardından, [expressroute bağlantı hattına bir VNet bağlama](expressroute-howto-linkvnet-classic.md).</span><span class="sxs-lookup"><span data-stu-id="96d47-259">Next, [Link a VNet to an ExpressRoute circuit](expressroute-howto-linkvnet-classic.md).</span></span>

* <span data-ttu-id="96d47-260">İş akışları hakkında daha fazla bilgi için bkz: [ExpressRoute iş akışları](expressroute-workflows.md).</span><span class="sxs-lookup"><span data-stu-id="96d47-260">For more information about workflows, see [ExpressRoute workflows](expressroute-workflows.md).</span></span>
* <span data-ttu-id="96d47-261">Bağlantı hattı eşlemesi hakkında daha fazla bilgi için bkz. [ExpressRoute bağlantı hattı ve yönlendirme etki alanları](expressroute-circuit-peerings.md).</span><span class="sxs-lookup"><span data-stu-id="96d47-261">For more information about circuit peering, see [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md).</span></span>

