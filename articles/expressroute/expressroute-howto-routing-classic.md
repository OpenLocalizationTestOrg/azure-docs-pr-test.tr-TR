---
title: "Nasıl tooconfigure (eşleme) bir expressroute bağlantı hattı için yönlendirmeyi: Azure: Klasik | Microsoft Docs"
description: "Bu makalede, oluşturma ve sağlama hello özel, genel ve Microsoft bir expressroute bağlantı hattı eşlemesi hello adım adım anlatılmaktadır. Bu makalede ayrıca nasıl toocheck hello durumu, güncelleştirme veya bağlantı hattınız için eşlemeleri silme gösterilmektedir."
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
ms.openlocfilehash: dc5bcc4b86c3bc965a88281b6c2a660f3bc58eb1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-peering-for-an-expressroute-circuit-classic"></a><span data-ttu-id="c9742-104">Oluşturma ve bir expressroute bağlantı hattı (Klasik) için eşleme değiştirme</span><span class="sxs-lookup"><span data-stu-id="c9742-104">Create and modify peering for an ExpressRoute circuit (classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c9742-105">Azure portal</span><span class="sxs-lookup"><span data-stu-id="c9742-105">Azure portal</span></span>](expressroute-howto-routing-portal-resource-manager.md)
> * [<span data-ttu-id="c9742-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c9742-106">PowerShell</span></span>](expressroute-howto-routing-arm.md)
> * [<span data-ttu-id="c9742-107">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="c9742-107">Azure CLI</span></span>](howto-routing-cli.md)
> * [<span data-ttu-id="c9742-108">Video - özel eşliği</span><span class="sxs-lookup"><span data-stu-id="c9742-108">Video - Private peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-private-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="c9742-109">Video - ortak eşleme</span><span class="sxs-lookup"><span data-stu-id="c9742-109">Video - Public peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-public-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="c9742-110">Video - Microsoft eşlemesi</span><span class="sxs-lookup"><span data-stu-id="c9742-110">Video - Microsoft peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-microsoft-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="c9742-111">PowerShell (klasik)</span><span class="sxs-lookup"><span data-stu-id="c9742-111">PowerShell (classic)</span></span>](expressroute-howto-routing-classic.md)
> 

<span data-ttu-id="c9742-112">Bu makalede hello adımları toocreate anlatılmaktadır ve PowerShell ve hello Klasik dağıtım modeli kullanarak bir expressroute için yönlendirme yapılandırması yönetin.</span><span class="sxs-lookup"><span data-stu-id="c9742-112">This article walks you through hello steps toocreate and manage routing configuration for an ExpressRoute circuit using PowerShell and hello classic deployment model.</span></span> <span data-ttu-id="c9742-113">Merhaba adımları de nasıl toocheck hello durumu, güncelleştirme veya silin ve bir expressroute bağlantı hattı için eşlemeler yetkisini kaldırma gösterilir.</span><span class="sxs-lookup"><span data-stu-id="c9742-113">hello steps below will also show you how toocheck hello status, update, or delete and deprovision peerings for an ExpressRoute circuit.</span></span>

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

<span data-ttu-id="c9742-114">**Azure dağıtım modelleri hakkında**</span><span class="sxs-lookup"><span data-stu-id="c9742-114">**About Azure deployment models**</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]


## <a name="configuration-prerequisites"></a><span data-ttu-id="c9742-115">Yapılandırma önkoşulları</span><span class="sxs-lookup"><span data-stu-id="c9742-115">Configuration prerequisites</span></span>
* <span data-ttu-id="c9742-116">Hello Azure Hizmet Yönetimi (SM) PowerShell cmdlet'lerinin en son sürümünü hello gerekir.</span><span class="sxs-lookup"><span data-stu-id="c9742-116">You will need hello latest version of hello Azure Service Management (SM) PowerShell cmdlets.</span></span> <span data-ttu-id="c9742-117">Daha fazla bilgi için bkz: [Azure PowerShell cmdlet'leri ile çalışmaya başlama](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c9742-117">For more information, see [Getting started with Azure PowerShell cmdlets](/powershell/azure/overview).</span></span>  
* <span data-ttu-id="c9742-118">Merhaba gözden geçirdiğinizden emin olun [Önkoşullar](expressroute-prerequisites.md) hello sayfasında [yönlendirme gereksinimleri](expressroute-routing.md) sayfası ve hello [iş akışları](expressroute-workflows.md) yapılandırmaya başlamadan önce sayfasında.</span><span class="sxs-lookup"><span data-stu-id="c9742-118">Make sure that you have reviewed hello [prerequisites](expressroute-prerequisites.md) page, hello [routing requirements](expressroute-routing.md) page, and hello [workflows](expressroute-workflows.md) page before you begin configuration.</span></span>
* <span data-ttu-id="c9742-119">Etkin bir ExpressRoute bağlantı hattınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="c9742-119">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="c9742-120">Çok olarak Hello yönergeleri[bir expressroute bağlantı hattı oluşturma](expressroute-howto-circuit-classic.md) ve devam etmeden önce bağlantı sağlayıcınız tarafından etkinleştirilen hello hattı sahip.</span><span class="sxs-lookup"><span data-stu-id="c9742-120">Follow hello instructions too[create an ExpressRoute circuit](expressroute-howto-circuit-classic.md) and have hello circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="c9742-121">Merhaba expressroute bağlantı hattı, aşağıda açıklanan toobe mümkün toorun hello cmdlet'leri için sağlanmış ve etkin durumda olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="c9742-121">hello ExpressRoute circuit must be in a provisioned and enabled state for you toobe able toorun hello cmdlets described below.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c9742-122">Bu yönergeler yalnızca Katman 2 bağlantı hizmetleri sunan hizmet sağlayıcıları ile oluşturulan toocircuits geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="c9742-122">These instructions only apply toocircuits created with service providers offering Layer 2 connectivity services.</span></span> <span data-ttu-id="c9742-123">Yönetilen Katman 3 hizmetleri (genellikle MPLS gibi bir IPVPN) sunan bir hizmet sağlayıcısı kullanıyorsanız, bağlantı sağlayıcınız yönlendirmeyi sizin için yapılandırır ve yönetir.</span><span class="sxs-lookup"><span data-stu-id="c9742-123">If you are using a service provider offering managed Layer 3 services (typically an IPVPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span>
> 
> 

<span data-ttu-id="c9742-124">Bir ExpressRoute bağlantı hattı için bir, iki veya üç eşlemenin tamamını (Azure özel, Azure ortak ve Microsoft) yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c9742-124">You can configure one, two, or all three peerings (Azure private, Azure public and Microsoft) for an ExpressRoute circuit.</span></span> <span data-ttu-id="c9742-125">Eşlemeleri seçtiğiniz herhangi bir sırayla yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c9742-125">You can configure peerings in any order you choose.</span></span> <span data-ttu-id="c9742-126">Bununla birlikte, her eşleme birer birer başlangıç yapılandırmasını tamamlayın emin olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="c9742-126">However, you must make sure that you complete hello configuration of each peering one at a time.</span></span>


### <a name="log-in-tooyour-azure-account-and-select-a-subscription"></a><span data-ttu-id="c9742-127">Tooyour Azure hesabı oturum ve bir abonelik seçin</span><span class="sxs-lookup"><span data-stu-id="c9742-127">Log in tooyour Azure account and select a subscription</span></span>
1. <span data-ttu-id="c9742-128">Yükseltilmiş haklarla PowerShell Konsolunuzu açın ve tooyour hesap bağlanın.</span><span class="sxs-lookup"><span data-stu-id="c9742-128">Open your PowerShell console with elevated rights and connect tooyour account.</span></span> <span data-ttu-id="c9742-129">Bağlandığınız örnek toohelp aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="c9742-129">Use hello following example toohelp you connect:</span></span>

        Login-AzureRmAccount

2. <span data-ttu-id="c9742-130">Merhaba hesabının Hello abonelikleri kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="c9742-130">Check hello subscriptions for hello account.</span></span>

        Get-AzureRmSubscription

3. <span data-ttu-id="c9742-131">Birden fazla aboneliğiniz varsa, toouse istediğiniz hello aboneliği seçin.</span><span class="sxs-lookup"><span data-stu-id="c9742-131">If you have more than one subscription, select hello subscription that you want toouse.</span></span>

        Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"

4. <span data-ttu-id="c9742-132">Ardından, aşağıdaki cmdlet'i tooadd hello Azure aboneliği tooPowerShell hello Klasik dağıtım modeli için kullanın.</span><span class="sxs-lookup"><span data-stu-id="c9742-132">Next, use hello following cmdlet tooadd your Azure subscription tooPowerShell for hello classic deployment model.</span></span>

        Add-AzureAccount


## <a name="azure-private-peering"></a><span data-ttu-id="c9742-133">Azure özel eşlemesi</span><span class="sxs-lookup"><span data-stu-id="c9742-133">Azure private peering</span></span>
<span data-ttu-id="c9742-134">Bu bölümde nasıl toocreate, alma, güncelleştirme ve hello bir expressroute bağlantı hattı için Azure özel eşleme yapılandırmasını silme hakkında yönergeler sağlar.</span><span class="sxs-lookup"><span data-stu-id="c9742-134">This section provides instructions on how toocreate, get, update, and delete hello Azure private peering configuration for an ExpressRoute circuit.</span></span> 

### <a name="toocreate-azure-private-peering"></a><span data-ttu-id="c9742-135">Azure özel eşleme toocreate</span><span class="sxs-lookup"><span data-stu-id="c9742-135">toocreate Azure private peering</span></span>
1. <span data-ttu-id="c9742-136">**ExpressRoute için Hello PowerShell modülünü içeri aktarın.**</span><span class="sxs-lookup"><span data-stu-id="c9742-136">**Import hello PowerShell module for ExpressRoute.**</span></span>
   
    <span data-ttu-id="c9742-137">Merhaba ExpressRoute cmdlet'lerini kullanmaya sipariş toostart hello PowerShell oturumunda hello Azure ve ExpressRoute modülleri almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="c9742-137">You must import hello Azure and ExpressRoute modules into hello PowerShell session in order toostart using hello ExpressRoute cmdlets.</span></span> <span data-ttu-id="c9742-138">Çalışma hello aşağıdaki tooimport hello Azure ve ExpressRoute modülleri hello PowerShell oturumuna komutları.</span><span class="sxs-lookup"><span data-stu-id="c9742-138">Run hello following commands tooimport hello Azure and ExpressRoute modules into hello PowerShell session.</span></span>  
   
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
2. <span data-ttu-id="c9742-139">**Bir expressroute bağlantı hattı oluşturun.**</span><span class="sxs-lookup"><span data-stu-id="c9742-139">**Create an ExpressRoute circuit.**</span></span>
   
    <span data-ttu-id="c9742-140">Merhaba yönergeleri toocreate izleyin bir [expressroute bağlantı hattı](expressroute-howto-circuit-classic.md) ve hello bağlantı sağlayıcı tarafından sağlanan sahip.</span><span class="sxs-lookup"><span data-stu-id="c9742-140">Follow hello instructions toocreate an [ExpressRoute circuit](expressroute-howto-circuit-classic.md) and have it provisioned by hello connectivity provider.</span></span> <span data-ttu-id="c9742-141">Bağlantı sağlayıcınız yönetilen Katman 3 Hizmetleri sunuyorsa, bağlantı sağlayıcısı tooenable Azure sizin için eşlemeyi özel isteyebilir.</span><span class="sxs-lookup"><span data-stu-id="c9742-141">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider tooenable Azure private peering for you.</span></span> <span data-ttu-id="c9742-142">Bu durumda, hello sonraki bölümlerde listelenen toofollow yönergeleri gerekmez.</span><span class="sxs-lookup"><span data-stu-id="c9742-142">In that case, you won't need toofollow instructions listed in hello next sections.</span></span> <span data-ttu-id="c9742-143">Ancak, bağlantı sağlayıcınız yönlendirmeyi sizin için hattınızı oluşturduktan sonra yönetmiyorsa aşağıdaki hello yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="c9742-143">However, if your connectivity provider does not manage routing for you, after creating your circuit, follow hello instructions below.</span></span> 
3. <span data-ttu-id="c9742-144">**Merhaba ExpressRoute bağlantı hattı tooensure sağlandığından denetleyin.**</span><span class="sxs-lookup"><span data-stu-id="c9742-144">**Check hello ExpressRoute circuit tooensure it is provisioned.**</span></span>
   
    <span data-ttu-id="c9742-145">Merhaba expressroute bağlantı hattı sağlanan ve ayrıca etkinleştirilirse toosee işaretlemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="c9742-145">You must first check toosee if hello ExpressRoute circuit is Provisioned and also Enabled.</span></span> <span data-ttu-id="c9742-146">Merhaba örneğe bakın.</span><span class="sxs-lookup"><span data-stu-id="c9742-146">See hello example below.</span></span>
   
        PS C:\> Get-AzureDedicatedCircuit -ServiceKey "*********************************"
   
        Bandwidth                        : 200
        CircuitName                      : MyTestCircuit
        Location                         : Silicon Valley
        ServiceKey                       : *********************************
        ServiceProviderName              : equinix
        ServiceProviderProvisioningState : Provisioned
        Sku                              : Standard
        Status                           : Enabled
   
    <span data-ttu-id="c9742-147">Merhaba hattı hazırlandı ve etkin gösterdiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="c9742-147">Make sure that hello circuit shows as Provisioned and Enabled.</span></span> <span data-ttu-id="c9742-148">Seçili değilse, bağlantı sağlayıcısı tooget ile hattı gerekli toohello durum ve duruma çalışır.</span><span class="sxs-lookup"><span data-stu-id="c9742-148">If it doesn't, work with your connectivity provider tooget your circuit toohello required state and status.</span></span>
   
        ServiceProviderProvisioningState : Provisioned
        Status                           : Enabled
4. <span data-ttu-id="c9742-149">**Merhaba bağlantı hattı için Azure özel eşlemesini yapılandırın.**</span><span class="sxs-lookup"><span data-stu-id="c9742-149">**Configure Azure private peering for hello circuit.**</span></span>
   
    <span data-ttu-id="c9742-150">Merhaba sonraki adımlara devam etmeden önce aşağıdaki öğelerindeki hello sahip olduğunuzdan emin olun:</span><span class="sxs-lookup"><span data-stu-id="c9742-150">Make sure that you have hello following items before you proceed with hello next steps:</span></span>
   
   * <span data-ttu-id="c9742-151">Bir/30 alt ağı hello birincil bağlantı için.</span><span class="sxs-lookup"><span data-stu-id="c9742-151">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="c9742-152">Bu, sanal ağlar için ayrılmış herhangi bir adres alanının parçası olmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="c9742-152">This must not be part of any address space reserved for virtual networks.</span></span>
   * <span data-ttu-id="c9742-153">Bir/30 alt ağı hello ikincil bağlantı için.</span><span class="sxs-lookup"><span data-stu-id="c9742-153">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="c9742-154">Bu, sanal ağlar için ayrılmış herhangi bir adres alanının parçası olmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="c9742-154">This must not be part of any address space reserved for virtual networks.</span></span>
   * <span data-ttu-id="c9742-155">Geçerli bir VLAN kimliği tooestablish bu eşlemenin.</span><span class="sxs-lookup"><span data-stu-id="c9742-155">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="c9742-156">Hiçbir diğer eşliği emin hello devredeki aynı VLAN kimliğini kullanan hello</span><span class="sxs-lookup"><span data-stu-id="c9742-156">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
   * <span data-ttu-id="c9742-157">Eşleme için AS numarası.</span><span class="sxs-lookup"><span data-stu-id="c9742-157">AS number for peering.</span></span> <span data-ttu-id="c9742-158">2 bayt ve 4 bayt AS numaralarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c9742-158">You can use both 2-byte and 4-byte AS numbers.</span></span> <span data-ttu-id="c9742-159">Bu eşleme için özel bir AS numarası kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c9742-159">You can use a private AS number for this peering.</span></span> <span data-ttu-id="c9742-160">65515’i kullanmadığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="c9742-160">Ensure that you are not using 65515.</span></span>
   * <span data-ttu-id="c9742-161">Toouse birini seçerseniz bir MD5 karma değeri.</span><span class="sxs-lookup"><span data-stu-id="c9742-161">An MD5 hash if you choose toouse one.</span></span> <span data-ttu-id="c9742-162">**Bu isteğe bağlıdır**.</span><span class="sxs-lookup"><span data-stu-id="c9742-162">**This is optional**.</span></span>
     
    <span data-ttu-id="c9742-163">Bağlantı hattınız için Azure özel eşleme cmdlet tooconfigure aşağıdaki hello çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c9742-163">You can run hello following cmdlet tooconfigure Azure private peering for your circuit.</span></span>
     
        <span data-ttu-id="c9742-164">Yeni AzureBGPPeering - AccessType özel - ServiceKey "***" - PrimaryPeerSubnet "10.0.0.0/30" - SecondaryPeerSubnet "10.0.0.4/30" - PeerAsn 1234 - Vlanıd 100</span><span class="sxs-lookup"><span data-stu-id="c9742-164">New-AzureBGPPeering -AccessType Private -ServiceKey "*********************************" -PrimaryPeerSubnet "10.0.0.0/30" -SecondaryPeerSubnet "10.0.0.4/30" -PeerAsn 1234 -VlanId 100</span></span>
     
    <span data-ttu-id="c9742-165">Bir MD5 karma değeri toouse seçerseniz, aşağıdaki hello cmdlet'ini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c9742-165">You can use hello cmdlet below if you choose toouse an MD5 hash.</span></span>
     
        <span data-ttu-id="c9742-166">Yeni AzureBGPPeering - AccessType özel - ServiceKey "***" - PrimaryPeerSubnet "10.0.0.0/30" - SecondaryPeerSubnet "10.0.0.4/30" - PeerAsn 1234 - Vlanıd 100 - SharedKey "A1B2C3D4"</span><span class="sxs-lookup"><span data-stu-id="c9742-166">New-AzureBGPPeering -AccessType Private -ServiceKey "*********************************" -PrimaryPeerSubnet "10.0.0.0/30" -SecondaryPeerSubnet "10.0.0.4/30" -PeerAsn 1234 -VlanId 100 -SharedKey "A1B2C3D4"</span></span>
     
     > [!IMPORTANT]
     > <span data-ttu-id="c9742-167">AS numaranızı müşteri ASN’si değil eşleme ASN’si olarak belirttiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="c9742-167">Ensure that you specify your AS number as peering ASN, not customer ASN.</span></span>
     > 
     > 

### <a name="tooview-azure-private-peering-details"></a><span data-ttu-id="c9742-168">tooview Azure özel eşleme ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="c9742-168">tooview Azure private peering details</span></span>
<span data-ttu-id="c9742-169">Hello aşağıdaki cmdlet'i kullanarak yapılandırma ayrıntılarını alabilirsiniz</span><span class="sxs-lookup"><span data-stu-id="c9742-169">You can get configuration details using hello following cmdlet</span></span>

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


### <a name="tooupdate-azure-private-peering-configuration"></a><span data-ttu-id="c9742-170">Azure özel eşleme yapılandırmasını tooupdate</span><span class="sxs-lookup"><span data-stu-id="c9742-170">tooupdate Azure private peering configuration</span></span>
<span data-ttu-id="c9742-171">Cmdlet aşağıdaki hello kullanarak hello yapılandırmasını herhangi bir bölümünü güncelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c9742-171">You can update any part of hello configuration using hello following cmdlet.</span></span> <span data-ttu-id="c9742-172">Merhaba aşağıdaki örnekte, hello hello hattının VLAN kimliği 100 too500 güncelleştiriliyor.</span><span class="sxs-lookup"><span data-stu-id="c9742-172">In hello example below, hello VLAN ID of hello circuit is being updated from 100 too500.</span></span>

    Set-AzureBGPPeering -AccessType Private -ServiceKey "*********************************" -PrimaryPeerSubnet "10.0.0.0/30" -SecondaryPeerSubnet "10.0.0.4/30" -PeerAsn 1234 -VlanId 500 -SharedKey "A1B2C3D4"

### <a name="toodelete-azure-private-peering"></a><span data-ttu-id="c9742-173">Azure özel eşleme toodelete</span><span class="sxs-lookup"><span data-stu-id="c9742-173">toodelete Azure private peering</span></span>
<span data-ttu-id="c9742-174">Hello aşağıdaki cmdlet'i çalıştırarak eşleme yapılandırmanızı kaldırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c9742-174">You can remove your peering configuration by running hello following cmdlet.</span></span>

> [!WARNING]
> <span data-ttu-id="c9742-175">Bu cmdlet'i çalıştırmadan önce tüm sanal ağları expressroute bağlantı hattı hello bağlantısız olduğundan emin olmalısınız.</span><span class="sxs-lookup"><span data-stu-id="c9742-175">You must ensure that all virtual networks are unlinked from hello ExpressRoute circuit before running this cmdlet.</span></span> 
> 
> 

    Remove-AzureBGPPeering -AccessType Private -ServiceKey "*********************************"


## <a name="azure-public-peering"></a><span data-ttu-id="c9742-176">Azure ortak eşleme</span><span class="sxs-lookup"><span data-stu-id="c9742-176">Azure public peering</span></span>
<span data-ttu-id="c9742-177">Bu bölümde, nasıl toocreate, alma, güncelleştirme ve hello bir expressroute bağlantı hattı için Azure ortak eşleme yapılandırmasını silme hakkında yönergeler sağlar.</span><span class="sxs-lookup"><span data-stu-id="c9742-177">This section provides instructions on how toocreate, get, update and delete hello Azure public peering configuration for an ExpressRoute circuit.</span></span>

### <a name="toocreate-azure-public-peering"></a><span data-ttu-id="c9742-178">Azure ortak eşleme toocreate</span><span class="sxs-lookup"><span data-stu-id="c9742-178">toocreate Azure public peering</span></span>
1. <span data-ttu-id="c9742-179">**ExpressRoute için Hello PowerShell modülünü içeri aktarın.**</span><span class="sxs-lookup"><span data-stu-id="c9742-179">**Import hello PowerShell module for ExpressRoute.**</span></span>
   
    <span data-ttu-id="c9742-180">Merhaba ExpressRoute cmdlet'lerini kullanmaya sipariş toostart hello PowerShell oturumunda hello Azure ve ExpressRoute modülleri almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="c9742-180">You must import hello Azure and ExpressRoute modules into hello PowerShell session in order toostart using hello ExpressRoute cmdlets.</span></span> <span data-ttu-id="c9742-181">Çalışma hello aşağıdaki tooimport hello Azure ve ExpressRoute modülleri hello PowerShell oturumuna komutları.</span><span class="sxs-lookup"><span data-stu-id="c9742-181">Run hello following commands tooimport hello Azure and ExpressRoute modules into hello PowerShell session.</span></span> 
   
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
2. <span data-ttu-id="c9742-182">**ExpressRoute bağlantı hattı oluşturma**</span><span class="sxs-lookup"><span data-stu-id="c9742-182">**Create an ExpressRoute circuit**</span></span>
   
    <span data-ttu-id="c9742-183">Merhaba yönergeleri toocreate izleyin bir [expressroute bağlantı hattı](expressroute-howto-circuit-classic.md) ve hello bağlantı sağlayıcı tarafından sağlanan sahip.</span><span class="sxs-lookup"><span data-stu-id="c9742-183">Follow hello instructions toocreate an [ExpressRoute circuit](expressroute-howto-circuit-classic.md) and have it provisioned by hello connectivity provider.</span></span> <span data-ttu-id="c9742-184">Bağlantı sağlayıcınız yönetilen Katman 3 Hizmetleri sunuyorsa, bağlantı sağlayıcısı tooenable Azure sizin için eşlemeyi genel isteyebilir.</span><span class="sxs-lookup"><span data-stu-id="c9742-184">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider tooenable Azure public peering for you.</span></span> <span data-ttu-id="c9742-185">Bu durumda, hello sonraki bölümlerde listelenen toofollow yönergeleri gerekmez.</span><span class="sxs-lookup"><span data-stu-id="c9742-185">In that case, you won't need toofollow instructions listed in hello next sections.</span></span> <span data-ttu-id="c9742-186">Ancak, bağlantı sağlayıcınız yönlendirmeyi sizin için hattınızı oluşturduktan sonra yönetmiyorsa aşağıdaki hello yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="c9742-186">However, if your connectivity provider does not manage routing for you, after creating your circuit, follow hello instructions below.</span></span>
3. <span data-ttu-id="c9742-187">**ExpressRoute bağlantı hattı tooensure sağlandığından denetleyin**</span><span class="sxs-lookup"><span data-stu-id="c9742-187">**Check ExpressRoute circuit tooensure it is provisioned**</span></span>
   
    <span data-ttu-id="c9742-188">Merhaba expressroute bağlantı hattı sağlanan ve ayrıca etkinleştirilirse toosee işaretlemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="c9742-188">You must first check toosee if hello ExpressRoute circuit is Provisioned and also Enabled.</span></span> <span data-ttu-id="c9742-189">Merhaba örneğe bakın.</span><span class="sxs-lookup"><span data-stu-id="c9742-189">See hello example below.</span></span>
   
        PS C:\> Get-AzureDedicatedCircuit -ServiceKey "*********************************"
   
        Bandwidth                        : 200
        CircuitName                      : MyTestCircuit
        Location                         : Silicon Valley
        ServiceKey                       : *********************************
        ServiceProviderName              : equinix
        ServiceProviderProvisioningState : Provisioned
        Sku                              : Standard
        Status                           : Enabled
   
    <span data-ttu-id="c9742-190">Merhaba hattı hazırlandı ve etkin gösterdiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="c9742-190">Make sure that hello circuit shows as Provisioned and Enabled.</span></span> <span data-ttu-id="c9742-191">Seçili değilse, bağlantı sağlayıcısı tooget ile hattı gerekli toohello durum ve duruma çalışır.</span><span class="sxs-lookup"><span data-stu-id="c9742-191">If it doesn't, work with your connectivity provider tooget your circuit toohello required state and status.</span></span>
   
        ServiceProviderProvisioningState : Provisioned
        Status                           : Enabled
4. <span data-ttu-id="c9742-192">**Merhaba bağlantı hattı için Azure ortak eşlemesini yapılandırın**</span><span class="sxs-lookup"><span data-stu-id="c9742-192">**Configure Azure public peering for hello circuit**</span></span>
   
    <span data-ttu-id="c9742-193">Devam etmeden önce aşağıdaki bilgilerle hello olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="c9742-193">Ensure that you have hello following information before you proceed further.</span></span>
   
   * <span data-ttu-id="c9742-194">Bir/30 alt ağı hello birincil bağlantı için.</span><span class="sxs-lookup"><span data-stu-id="c9742-194">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="c9742-195">Bu geçerli bir ortak IPv4 öneki olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="c9742-195">This must be a valid public IPv4 prefix.</span></span>
   * <span data-ttu-id="c9742-196">Bir/30 alt ağı hello ikincil bağlantı için.</span><span class="sxs-lookup"><span data-stu-id="c9742-196">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="c9742-197">Bu geçerli bir ortak IPv4 öneki olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="c9742-197">This must be a valid public IPv4 prefix.</span></span>
   * <span data-ttu-id="c9742-198">Geçerli bir VLAN kimliği tooestablish bu eşlemenin.</span><span class="sxs-lookup"><span data-stu-id="c9742-198">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="c9742-199">Hiçbir diğer eşliği emin hello devredeki aynı VLAN kimliğini kullanan hello</span><span class="sxs-lookup"><span data-stu-id="c9742-199">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
   * <span data-ttu-id="c9742-200">Eşleme için AS numarası.</span><span class="sxs-lookup"><span data-stu-id="c9742-200">AS number for peering.</span></span> <span data-ttu-id="c9742-201">2 bayt ve 4 bayt AS numaralarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c9742-201">You can use both 2-byte and 4-byte AS numbers.</span></span>
   * <span data-ttu-id="c9742-202">Toouse birini seçerseniz bir MD5 karma değeri.</span><span class="sxs-lookup"><span data-stu-id="c9742-202">An MD5 hash if you choose toouse one.</span></span> <span data-ttu-id="c9742-203">**Bu isteğe bağlıdır**.</span><span class="sxs-lookup"><span data-stu-id="c9742-203">**This is optional**.</span></span>
     
    <span data-ttu-id="c9742-204">Bağlantı hattınız için Azure ortak eşleme cmdlet tooconfigure aşağıdaki hello çalıştırabilirsiniz</span><span class="sxs-lookup"><span data-stu-id="c9742-204">You can run hello following cmdlet tooconfigure Azure public peering for your circuit</span></span>
     
        <span data-ttu-id="c9742-205">Yeni AzureBGPPeering - AccessType ortak - ServiceKey "***" - PrimaryPeerSubnet "131.107.0.0/30" - SecondaryPeerSubnet "131.107.0.4/30" - PeerAsn 1234 - Vlanıd 200</span><span class="sxs-lookup"><span data-stu-id="c9742-205">New-AzureBGPPeering -AccessType Public -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -PeerAsn 1234 -VlanId 200</span></span>
     
    <span data-ttu-id="c9742-206">Bir MD5 karma değeri toouse seçerseniz hello cmdlet'i kullanabilirsiniz</span><span class="sxs-lookup"><span data-stu-id="c9742-206">You can use hello cmdlet below if you choose toouse an MD5 hash</span></span>
     
        <span data-ttu-id="c9742-207">Yeni AzureBGPPeering - AccessType ortak - ServiceKey "***" - PrimaryPeerSubnet "131.107.0.0/30" - SecondaryPeerSubnet "131.107.0.4/30" - PeerAsn 1234 - Vlanıd 200 - SharedKey "A1B2C3D4"</span><span class="sxs-lookup"><span data-stu-id="c9742-207">New-AzureBGPPeering -AccessType Public -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -PeerAsn 1234 -VlanId 200 -SharedKey "A1B2C3D4"</span></span>
     
     > [!IMPORTANT]
     > <span data-ttu-id="c9742-208">AS numaranızı müşteri ASN’si değil eşleme ASN’si olarak belirttiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="c9742-208">Ensure that you specify your AS number as peering ASN and not customer ASN.</span></span>
     > 
     > 

### <a name="tooview-azure-public-peering-details"></a><span data-ttu-id="c9742-209">tooview Azure genel eşliği ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="c9742-209">tooview Azure public peering details</span></span>
<span data-ttu-id="c9742-210">Hello aşağıdaki cmdlet'i kullanarak yapılandırma ayrıntılarını alabilirsiniz</span><span class="sxs-lookup"><span data-stu-id="c9742-210">You can get configuration details using hello following cmdlet</span></span>

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


### <a name="tooupdate-azure-public-peering-configuration"></a><span data-ttu-id="c9742-211">Azure ortak eşleme yapılandırmasını tooupdate</span><span class="sxs-lookup"><span data-stu-id="c9742-211">tooupdate Azure public peering configuration</span></span>
<span data-ttu-id="c9742-212">Cmdlet aşağıdaki hello kullanarak hello yapılandırmasını herhangi bir bölümünü güncelleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="c9742-212">You can update any part of hello configuration using hello following cmdlet</span></span>

    Set-AzureBGPPeering -AccessType Public -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -PeerAsn 1234 -VlanId 600 -SharedKey "A1B2C3D4"

<span data-ttu-id="c9742-213">Merhaba hello hattının VLAN kimliği 200 too600 örnek yukarıda hello içinde gelen güncelleştiriliyor.</span><span class="sxs-lookup"><span data-stu-id="c9742-213">hello VLAN ID of hello circuit is being updated from 200 too600 in hello above example.</span></span>

### <a name="toodelete-azure-public-peering"></a><span data-ttu-id="c9742-214">Azure ortak eşleme toodelete</span><span class="sxs-lookup"><span data-stu-id="c9742-214">toodelete Azure public peering</span></span>
<span data-ttu-id="c9742-215">Hello aşağıdaki cmdlet'i çalıştırarak eşleme yapılandırmanızı kaldırabilirsiniz</span><span class="sxs-lookup"><span data-stu-id="c9742-215">You can remove your peering configuration by running hello following cmdlet</span></span>

    Remove-AzureBGPPeering -AccessType Public -ServiceKey "*********************************"

## <a name="microsoft-peering"></a><span data-ttu-id="c9742-216">Microsoft eşlemesi</span><span class="sxs-lookup"><span data-stu-id="c9742-216">Microsoft peering</span></span>
<span data-ttu-id="c9742-217">Bu bölümde, nasıl toocreate, alma, güncelleştirme ve bir expressroute bağlantı hattı için Microsoft eşleme yapılandırmasını hello silme hakkında yönergeler sağlar.</span><span class="sxs-lookup"><span data-stu-id="c9742-217">This section provides instructions on how toocreate, get, update and delete hello Microsoft peering configuration for an ExpressRoute circuit.</span></span> 

### <a name="toocreate-microsoft-peering"></a><span data-ttu-id="c9742-218">toocreate Microsoft eşlemesi</span><span class="sxs-lookup"><span data-stu-id="c9742-218">toocreate Microsoft peering</span></span>
1. <span data-ttu-id="c9742-219">**ExpressRoute için Hello PowerShell modülünü içeri aktarın.**</span><span class="sxs-lookup"><span data-stu-id="c9742-219">**Import hello PowerShell module for ExpressRoute.**</span></span>
   
    <span data-ttu-id="c9742-220">Merhaba ExpressRoute cmdlet'lerini kullanmaya sipariş toostart hello PowerShell oturumunda hello Azure ve ExpressRoute modülleri almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="c9742-220">You must import hello Azure and ExpressRoute modules into hello PowerShell session in order toostart using hello ExpressRoute cmdlets.</span></span> <span data-ttu-id="c9742-221">Çalışma hello aşağıdaki tooimport hello Azure ve ExpressRoute modülleri hello PowerShell oturumuna komutları.</span><span class="sxs-lookup"><span data-stu-id="c9742-221">Run hello following commands tooimport hello Azure and ExpressRoute modules into hello PowerShell session.</span></span>  
   
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
2. <span data-ttu-id="c9742-222">**ExpressRoute bağlantı hattı oluşturma**</span><span class="sxs-lookup"><span data-stu-id="c9742-222">**Create an ExpressRoute circuit**</span></span>
   
    <span data-ttu-id="c9742-223">Merhaba yönergeleri toocreate izleyin bir [expressroute bağlantı hattı](expressroute-howto-circuit-classic.md) ve hello bağlantı sağlayıcı tarafından sağlanan sahip.</span><span class="sxs-lookup"><span data-stu-id="c9742-223">Follow hello instructions toocreate an [ExpressRoute circuit](expressroute-howto-circuit-classic.md) and have it provisioned by hello connectivity provider.</span></span> <span data-ttu-id="c9742-224">Bağlantı sağlayıcınız yönetilen Katman 3 Hizmetleri sunuyorsa, bağlantı sağlayıcısı tooenable Azure sizin için eşlemeyi özel isteyebilir.</span><span class="sxs-lookup"><span data-stu-id="c9742-224">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider tooenable Azure private peering for you.</span></span> <span data-ttu-id="c9742-225">Bu durumda, hello sonraki bölümlerde listelenen toofollow yönergeleri gerekmez.</span><span class="sxs-lookup"><span data-stu-id="c9742-225">In that case, you won't need toofollow instructions listed in hello next sections.</span></span> <span data-ttu-id="c9742-226">Ancak, bağlantı sağlayıcınız yönlendirmeyi sizin için hattınızı oluşturduktan sonra yönetmiyorsa aşağıdaki hello yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="c9742-226">However, if your connectivity provider does not manage routing for you, after creating your circuit, follow hello instructions below.</span></span>
3. <span data-ttu-id="c9742-227">**ExpressRoute bağlantı hattı tooensure sağlandığından denetleyin**</span><span class="sxs-lookup"><span data-stu-id="c9742-227">**Check ExpressRoute circuit tooensure it is provisioned**</span></span>
   
    <span data-ttu-id="c9742-228">Merhaba expressroute bağlantı hattı hazırlandı ve etkin durumda ise toosee işaretlemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="c9742-228">You must first check toosee if hello ExpressRoute circuit is in Provisioned and Enabled state.</span></span>
   
        PS C:\> Get-AzureDedicatedCircuit -ServiceKey "*********************************"
   
        Bandwidth                        : 200
        CircuitName                      : MyTestCircuit
        Location                         : Silicon Valley
        ServiceKey                       : *********************************
        ServiceProviderName              : equinix
        ServiceProviderProvisioningState : Provisioned
        Sku                              : Standard
        Status                           : Enabled
   
    <span data-ttu-id="c9742-229">Merhaba hattı hazırlandı ve etkin gösterdiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="c9742-229">Make sure that hello circuit shows as Provisioned and Enabled.</span></span> <span data-ttu-id="c9742-230">Seçili değilse, bağlantı sağlayıcısı tooget ile hattı gerekli toohello durum ve duruma çalışır.</span><span class="sxs-lookup"><span data-stu-id="c9742-230">If it doesn't, work with your connectivity provider tooget your circuit toohello required state and status.</span></span>
   
        ServiceProviderProvisioningState : Provisioned
        Status                           : Enabled
4. <span data-ttu-id="c9742-231">**Microsoft eşlemesini Hello bağlantı hattı için yapılandırın**</span><span class="sxs-lookup"><span data-stu-id="c9742-231">**Configure Microsoft peering for hello circuit**</span></span>
   
    <span data-ttu-id="c9742-232">Devam etmeden önce bilgilerini aşağıdaki hello sahip olduğunuzdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="c9742-232">Make sure that you have hello following information before you proceed.</span></span>
   
   * <span data-ttu-id="c9742-233">Bir/30 alt ağı hello birincil bağlantı için.</span><span class="sxs-lookup"><span data-stu-id="c9742-233">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="c9742-234">Bu size ait ve bir RIR / IRR içinde kayıtlı bir geçerli ortak IPv4 ön eki olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="c9742-234">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
   * <span data-ttu-id="c9742-235">Bir/30 alt ağı hello ikincil bağlantı için.</span><span class="sxs-lookup"><span data-stu-id="c9742-235">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="c9742-236">Bu size ait ve bir RIR / IRR içinde kayıtlı bir geçerli ortak IPv4 ön eki olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="c9742-236">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
   * <span data-ttu-id="c9742-237">Geçerli bir VLAN kimliği tooestablish bu eşlemenin.</span><span class="sxs-lookup"><span data-stu-id="c9742-237">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="c9742-238">Hiçbir diğer eşliği emin hello devredeki aynı VLAN kimliğini kullanan hello</span><span class="sxs-lookup"><span data-stu-id="c9742-238">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
   * <span data-ttu-id="c9742-239">Eşleme için AS numarası.</span><span class="sxs-lookup"><span data-stu-id="c9742-239">AS number for peering.</span></span> <span data-ttu-id="c9742-240">2 bayt ve 4 bayt AS numaralarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c9742-240">You can use both 2-byte and 4-byte AS numbers.</span></span>
   * <span data-ttu-id="c9742-241">Tanıtılan önekler: listesini sağlamanız gerekir tüm ön eklerin hello BGP oturumu üzerinden tooadvertise planlayın.</span><span class="sxs-lookup"><span data-stu-id="c9742-241">Advertised prefixes: You must provide a list of all prefixes you plan tooadvertise over hello BGP session.</span></span> <span data-ttu-id="c9742-242">Yalnızca ortak IP adresi ön ekleri kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="c9742-242">Only public IP address prefixes are accepted.</span></span> <span data-ttu-id="c9742-243">Toosend ön ek kümesi planlıyorsanız, virgülle ayrılmış bir liste gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c9742-243">You can send a comma separated list if you plan toosend a set of prefixes.</span></span> <span data-ttu-id="c9742-244">Bu ön eklerin bir RIR içinde kayıtlı tooyou olmalıdır / IRR.</span><span class="sxs-lookup"><span data-stu-id="c9742-244">These prefixes must be registered tooyou in an RIR / IRR.</span></span>
   * <span data-ttu-id="c9742-245">Müşteri ASN'si: eşleme AS numarasına kayıtlı toohello olmayan önekleri reklam, kayıtlı oldukları numara toowhich hello belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c9742-245">Customer ASN: If you are advertising prefixes that are not registered toohello peering AS number, you can specify hello AS number toowhich they are registered.</span></span> <span data-ttu-id="c9742-246">**Bu isteğe bağlıdır**.</span><span class="sxs-lookup"><span data-stu-id="c9742-246">**This is optional**.</span></span>
   * <span data-ttu-id="c9742-247">Yönlendirme kayıt defteri adı: Merhaba RIR belirtebilirsiniz / hangi hello karşı AS numarası ve önekleri IRR kayıtlı.</span><span class="sxs-lookup"><span data-stu-id="c9742-247">Routing Registry Name: You can specify hello RIR / IRR against which hello AS number and prefixes are registered.</span></span>
   * <span data-ttu-id="c9742-248">Toouse birini seçerseniz bir MD5 karma değeri.</span><span class="sxs-lookup"><span data-stu-id="c9742-248">An MD5 hash, if you choose toouse one.</span></span> <span data-ttu-id="c9742-249">**Bu isteğe bağlıdır.**</span><span class="sxs-lookup"><span data-stu-id="c9742-249">**This is optional.**</span></span>
     
    <span data-ttu-id="c9742-250">Bağlantı hattınız için cmdlet tooconfigure Microsoft pering aşağıdaki hello çalıştırabilirsiniz</span><span class="sxs-lookup"><span data-stu-id="c9742-250">You can run hello following cmdlet tooconfigure Microsoft pering for your circuit</span></span>
     
        <span data-ttu-id="c9742-251">Yeni AzureBGPPeering - AccessType Microsoft - ServiceKey "***" - PrimaryPeerSubnet "131.107.0.0/30" - SecondaryPeerSubnet "131.107.0.4/30" - Vlanıd 300 - PeerAsn 1234 - CustomerAsn 2245 - AdvertisedPublicPrefixes "123.0.0.0/30" - RoutingRegistryName "ARIN" - SharedKey "A1B2C3D4"</span><span class="sxs-lookup"><span data-stu-id="c9742-251">New-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -VlanId 300 -PeerAsn 1234 -CustomerAsn 2245 -AdvertisedPublicPrefixes "123.0.0.0/30" -RoutingRegistryName "ARIN" -SharedKey "A1B2C3D4"</span></span>

### <a name="tooview-microsoft-peering-details"></a><span data-ttu-id="c9742-252">tooview Microsoft eşleme ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="c9742-252">tooview Microsoft peering details</span></span>
<span data-ttu-id="c9742-253">Hello aşağıdaki cmdlet'i kullanarak yapılandırma ayrıntılarını alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c9742-253">You can get configuration details using hello following cmdlet.</span></span>

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


### <a name="tooupdate-microsoft-peering-configuration"></a><span data-ttu-id="c9742-254">tooupdate Microsoft eşleme yapılandırması</span><span class="sxs-lookup"><span data-stu-id="c9742-254">tooupdate Microsoft peering configuration</span></span>
<span data-ttu-id="c9742-255">Cmdlet aşağıdaki hello kullanarak hello yapılandırmasını herhangi bir bölümünü güncelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c9742-255">You can update any part of hello configuration using hello following cmdlet.</span></span>

    Set-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -VlanId 300 -PeerAsn 1234 -CustomerAsn 2245 -AdvertisedPublicPrefixes "123.0.0.0/30" -RoutingRegistryName "ARIN" -SharedKey "A1B2C3D4"

### <a name="toodelete-microsoft-peering"></a><span data-ttu-id="c9742-256">toodelete Microsoft eşlemesi</span><span class="sxs-lookup"><span data-stu-id="c9742-256">toodelete Microsoft peering</span></span>
<span data-ttu-id="c9742-257">Hello aşağıdaki cmdlet'i çalıştırarak eşleme yapılandırmanızı kaldırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c9742-257">You can remove your peering configuration by running hello following cmdlet.</span></span>

    Remove-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************"

## <a name="next-steps"></a><span data-ttu-id="c9742-258">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c9742-258">Next steps</span></span>
<span data-ttu-id="c9742-259">Ardından, [VNet tooan expressroute bağlantı hattı bağlantı](expressroute-howto-linkvnet-classic.md).</span><span class="sxs-lookup"><span data-stu-id="c9742-259">Next, [Link a VNet tooan ExpressRoute circuit](expressroute-howto-linkvnet-classic.md).</span></span>

* <span data-ttu-id="c9742-260">İş akışları hakkında daha fazla bilgi için bkz: [ExpressRoute iş akışları](expressroute-workflows.md).</span><span class="sxs-lookup"><span data-stu-id="c9742-260">For more information about workflows, see [ExpressRoute workflows](expressroute-workflows.md).</span></span>
* <span data-ttu-id="c9742-261">Bağlantı hattı eşlemesi hakkında daha fazla bilgi için bkz. [ExpressRoute bağlantı hattı ve yönlendirme etki alanları](expressroute-circuit-peerings.md).</span><span class="sxs-lookup"><span data-stu-id="c9742-261">For more information about circuit peering, see [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md).</span></span>

