---
title: "Sanal ağ tooan expressroute bağlantı hattı bağlantı: PowerShell: Klasik: Azure | Microsoft Docs"
description: "Bu belge nasıl hello Klasik dağıtım modeli ve PowerShell kullanarak sanal toolink (Vnet'ler) tooExpressRoute devreler ağları genel bir bakış sağlar."
services: expressroute
documentationcenter: na
author: ganesr
manager: carmonm
editor: 
tags: azure-service-management
ms.assetid: 9b53fd72-9b6b-4844-80b9-4e1d54fd0c17
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/28/2017
ms.author: ganesr
ms.openlocfilehash: 6b8a01dcd4bbb9618ec3dd438cf0107538fb2a7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-virtual-network-tooan-expressroute-circuit-using-powershell-classic"></a><span data-ttu-id="08492-103">PowerShell (Klasik) kullanarak bir sanal ağ tooan expressroute bağlantı hattı Bağlan</span><span class="sxs-lookup"><span data-stu-id="08492-103">Connect a virtual network tooan ExpressRoute circuit using PowerShell (classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="08492-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="08492-104">Azure portal</span></span>](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [<span data-ttu-id="08492-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="08492-105">PowerShell</span></span>](expressroute-howto-linkvnet-arm.md)
> * [<span data-ttu-id="08492-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="08492-106">Azure CLI</span></span>](howto-linkvnet-cli.md)
> * [<span data-ttu-id="08492-107">Video - Azure portalı</span><span class="sxs-lookup"><span data-stu-id="08492-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [<span data-ttu-id="08492-108">PowerShell (klasik)</span><span class="sxs-lookup"><span data-stu-id="08492-108">PowerShell (classic)</span></span>](expressroute-howto-linkvnet-classic.md)
>

<span data-ttu-id="08492-109">Bu makalede hello Klasik dağıtım modeli ve PowerShell kullanarak sanal ağlar (Vnet'ler) tooAzure ExpressRoute bağlantı hatları bağlama yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="08492-109">This article will help you link virtual networks (VNets) tooAzure ExpressRoute circuits by using hello classic deployment model and PowerShell.</span></span> <span data-ttu-id="08492-110">Sanal ağlar ya da içinde olabileceği hello aynı abonelik veya başka bir abonelik parçası olabilir.</span><span class="sxs-lookup"><span data-stu-id="08492-110">Virtual networks can either be in hello same subscription or can be part of another subscription.</span></span>

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

<span data-ttu-id="08492-111">**Azure dağıtım modelleri hakkında**</span><span class="sxs-lookup"><span data-stu-id="08492-111">**About Azure deployment models**</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="configuration-prerequisites"></a><span data-ttu-id="08492-112">Yapılandırma önkoşulları</span><span class="sxs-lookup"><span data-stu-id="08492-112">Configuration prerequisites</span></span>
1. <span data-ttu-id="08492-113">Hello Azure PowerShell modüllerinin en son sürümünü hello gerekir.</span><span class="sxs-lookup"><span data-stu-id="08492-113">You need hello latest version of hello Azure PowerShell modules.</span></span> <span data-ttu-id="08492-114">Merhaba PowerShell bölümünü hello hello son PowerShell modülleri indirebilirsiniz [Azure indirmeler sayfası](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="08492-114">You can download hello latest PowerShell modules from hello PowerShell section of hello [Azure Downloads page](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="08492-115">Merhaba yönergeleri izleyin [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview) nasıl hakkında adım adım yönergeler için tooconfigure bilgisayar toouse hello Azure PowerShell modüllerinizi.</span><span class="sxs-lookup"><span data-stu-id="08492-115">Follow hello instructions in [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for step-by-step guidance on how tooconfigure your computer toouse hello Azure PowerShell modules.</span></span>
2. <span data-ttu-id="08492-116">Tooreview hello gereksinim [Önkoşullar](expressroute-prerequisites.md), [yönlendirme gereksinimleri](expressroute-routing.md), ve [iş akışları](expressroute-workflows.md) yapılandırmaya başlamadan önce.</span><span class="sxs-lookup"><span data-stu-id="08492-116">You need tooreview hello [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
3. <span data-ttu-id="08492-117">Etkin bir ExpressRoute bağlantı hattınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="08492-117">You must have an active ExpressRoute circuit.</span></span>
   * <span data-ttu-id="08492-118">Çok olarak Hello yönergeleri[bir expressroute bağlantı hattı oluşturma](expressroute-howto-circuit-classic.md) ve bağlantı sağlayıcınız hello hattı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="08492-118">Follow hello instructions too[create an ExpressRoute circuit](expressroute-howto-circuit-classic.md) and have your connectivity provider enable hello circuit.</span></span>
   * <span data-ttu-id="08492-119">Bağlantı hattınız için yapılandırılmış Azure özel eşleme olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="08492-119">Ensure that you have Azure private peering configured for your circuit.</span></span> <span data-ttu-id="08492-120">Merhaba bkz [yönlendirmeyi yapılandırma](expressroute-howto-routing-classic.md) yönlendirme yönergeleri için makalenin.</span><span class="sxs-lookup"><span data-stu-id="08492-120">See hello [Configure routing](expressroute-howto-routing-classic.md) article for routing instructions.</span></span>
   * <span data-ttu-id="08492-121">Azure özel eşleme yapılandırılır ve uçtan uca bağlantı etkinleştirebilmeniz için ağınız ve Microsoft arasında hello BGP eşliği yukarı olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="08492-121">Ensure that Azure private peering is configured and hello BGP peering between your network and Microsoft is up so that you can enable end-to-end connectivity.</span></span>
   * <span data-ttu-id="08492-122">Bir sanal ağ ve oluşturulan ve tam olarak sağlanan bir sanal ağ geçidi olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="08492-122">You must have a virtual network and a virtual network gateway created and fully provisioned.</span></span> <span data-ttu-id="08492-123">Çok olarak Hello yönergeleri[sanal ağ ExpressRoute için yapılandırma](expressroute-howto-vnet-portal-classic.md).</span><span class="sxs-lookup"><span data-stu-id="08492-123">Follow hello instructions too[configure a virtual network for ExpressRoute](expressroute-howto-vnet-portal-classic.md).</span></span>

<span data-ttu-id="08492-124">Too10 sanal ağlar tooan expressroute bağlantı hattı bağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="08492-124">You can link up too10 virtual networks tooan ExpressRoute circuit.</span></span> <span data-ttu-id="08492-125">Tüm sanal ağları hello olmalıdır aynı coğrafi bölge.</span><span class="sxs-lookup"><span data-stu-id="08492-125">All virtual networks must be in hello same geopolitical region.</span></span> <span data-ttu-id="08492-126">Çok sayıda sanal ağlar tooyour expressroute bağlantı hattı bağlantı veya diğer coğrafi bölgelerde hello ExpressRoute premium eklentisi etkinse olan sanal ağlara bağlantı.</span><span class="sxs-lookup"><span data-stu-id="08492-126">You can link a larger number of virtual networks tooyour ExpressRoute circuit, or link virtual networks that are in other geopolitical regions if you enabled hello ExpressRoute premium add-on.</span></span> <span data-ttu-id="08492-127">Merhaba denetleyin [SSS](expressroute-faqs.md) hello premium eklentisi hakkında daha fazla ayrıntı için.</span><span class="sxs-lookup"><span data-stu-id="08492-127">Check hello [FAQ](expressroute-faqs.md) for more details on hello premium add-on.</span></span>

## <a name="connect-a-virtual-network-in-hello-same-subscription-tooa-circuit"></a><span data-ttu-id="08492-128">Merhaba sanal bir ağa bağlan aynı abonelik tooa hattı</span><span class="sxs-lookup"><span data-stu-id="08492-128">Connect a virtual network in hello same subscription tooa circuit</span></span>
<span data-ttu-id="08492-129">Cmdlet aşağıdaki hello kullanarak bir sanal ağ tooan expressroute bağlantı hattı bağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="08492-129">You can link a virtual network tooan ExpressRoute circuit by using hello following cmdlet.</span></span> <span data-ttu-id="08492-130">Bu hello sanal ağ geçidi oluşturulur ve hello cmdlet'i çalıştırmadan önce bağlama için hazır olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="08492-130">Make sure that hello virtual network gateway is created and is ready for linking before you run hello cmdlet.</span></span>

    New-AzureDedicatedCircuitLink -ServiceKey "*****************************" -VNetName "MyVNet"
    Provisioned

## <a name="connect-a-virtual-network-in-a-different-subscription-tooa-circuit"></a><span data-ttu-id="08492-131">Farklı bir abonelik tooa hattı sanal bir ağa bağlan</span><span class="sxs-lookup"><span data-stu-id="08492-131">Connect a virtual network in a different subscription tooa circuit</span></span>
<span data-ttu-id="08492-132">Bir expressroute bağlantı hattı birden çok abonelik paylaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="08492-132">You can share an ExpressRoute circuit across multiple subscriptions.</span></span> <span data-ttu-id="08492-133">Aşağıdaki şekilde hello arasında birden çok abonelik basit bir ExpressRoute bağlantı hatları için nasıl paylaşım works'ün şematik gösterir.</span><span class="sxs-lookup"><span data-stu-id="08492-133">hello following figure shows a simple schematic of how sharing works for ExpressRoute circuits across multiple subscriptions.</span></span>

<span data-ttu-id="08492-134">Her hello küçük bulutların hello büyük bulut içinde bir kuruluş içindeki toodifferent bölümler ait kullanılan toorepresent abonelikleri içindir.</span><span class="sxs-lookup"><span data-stu-id="08492-134">Each of hello smaller clouds within hello large cloud is used toorepresent subscriptions that belong toodifferent departments within an organization.</span></span> <span data-ttu-id="08492-135">Kendi Hizmetleri--ancak hello Departmanlar dağıtma tek bir ExpressRoute bağlantı hattı tooconnect geri tooyour şirket içi ağ paylaşımı için her hello kuruluşunuz içinde hello bölümlerin kendi aboneliği kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="08492-135">Each of hello departments within hello organization can use their own subscription for deploying their services--but hello departments can share a single ExpressRoute circuit tooconnect back tooyour on-premises network.</span></span> <span data-ttu-id="08492-136">Tek bir bölüm (Bu örnekte: BT) hello expressroute bağlantı hattı sahip olabilir.</span><span class="sxs-lookup"><span data-stu-id="08492-136">A single department (in this example: IT) can own hello ExpressRoute circuit.</span></span> <span data-ttu-id="08492-137">Merhaba kuruluştaki diğer abonelikler hello expressroute bağlantı hattı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="08492-137">Other subscriptions within hello organization can use hello ExpressRoute circuit.</span></span>

> [!NOTE]
> <span data-ttu-id="08492-138">Bağlantı ve bant genişliği ücretleri ayrılmış hello hattı için uygulanan toohello ExpressRoute bağlantı hattı sahip olacaktır.</span><span class="sxs-lookup"><span data-stu-id="08492-138">Connectivity and bandwidth charges for hello dedicated circuit will be applied toohello ExpressRoute circuit owner.</span></span> <span data-ttu-id="08492-139">Tüm sanal ağları hello paylaşmak aynı bant genişliği.</span><span class="sxs-lookup"><span data-stu-id="08492-139">All virtual networks share hello same bandwidth.</span></span>
> 
> 

![Çapraz abonelik bağlantısı](./media/expressroute-howto-linkvnet-classic/cross-subscription.png)

### <a name="administration"></a><span data-ttu-id="08492-141">Yönetim</span><span class="sxs-lookup"><span data-stu-id="08492-141">Administration</span></span>
<span data-ttu-id="08492-142">Merhaba *devre sahibinden* hello ExpressRoute bağlantı hattı oluşturulur hello abonelik hello yönetici/Abonelikteki olduğu.</span><span class="sxs-lookup"><span data-stu-id="08492-142">hello *circuit owner* is hello administrator/coadministrator of hello subscription in which hello ExpressRoute circuit is created.</span></span> <span data-ttu-id="08492-143">Merhaba devre sahibinden Yöneticiler/coadministrators diğer abonelikler, başvurulan tooas yetkilendirebilir *hattı kullanıcılar*, toouse hello oldukları hattı ayrılmış.</span><span class="sxs-lookup"><span data-stu-id="08492-143">hello circuit owner can authorize administrators/coadministrators of other subscriptions, referred tooas *circuit users*, toouse hello dedicated circuit that they own.</span></span> <span data-ttu-id="08492-144">Yetkileri sonra yetkili toouse hello kuruluşun ExpressRoute bağlantı hattı can hattı kullanıcılar kendi abonelik toohello expressroute bağlantı hattı hello sanal ağa bağlayın.</span><span class="sxs-lookup"><span data-stu-id="08492-144">Circuit users who are authorized toouse hello organization's ExpressRoute circuit can link hello virtual network in their subscription toohello ExpressRoute circuit after they are authorized.</span></span>

<span data-ttu-id="08492-145">Merhaba devre sahibinden hello güç toomodify ve revoke yetkilerini herhangi bir zamanda sahiptir.</span><span class="sxs-lookup"><span data-stu-id="08492-145">hello circuit owner has hello power toomodify and revoke authorizations at any time.</span></span> <span data-ttu-id="08492-146">Bir yetkilendirme iptal erişimini iptal edildi hello abonelikten silinen tüm bağlantılar neden olur.</span><span class="sxs-lookup"><span data-stu-id="08492-146">Revoking an authorization will result in all links being deleted from hello subscription whose access was revoked.</span></span>

### <a name="circuit-owner-operations"></a><span data-ttu-id="08492-147">Bağlantı hattı sahibi işlemleri</span><span class="sxs-lookup"><span data-stu-id="08492-147">Circuit owner operations</span></span>

<span data-ttu-id="08492-148">**Bir yetkilendirme oluşturma**</span><span class="sxs-lookup"><span data-stu-id="08492-148">**Creating an authorization**</span></span>

<span data-ttu-id="08492-149">Merhaba devre sahibinden yetkilendirir hello Yöneticiler diğer abonelikler toouse hello belirtilen hattı.</span><span class="sxs-lookup"><span data-stu-id="08492-149">hello circuit owner authorizes hello administrators of other subscriptions toouse hello specified circuit.</span></span> <span data-ttu-id="08492-150">Aşağıdaki örneğine hello hello yöneticisinin hello devrenin (Contoso BT) başka bir abonelik (geliştirme, Test) toolink tootwo sanal ağlar toohello hattı yukarı hello Yöneticisi sağlar.</span><span class="sxs-lookup"><span data-stu-id="08492-150">In hello following example, hello administrator of hello circuit (Contoso IT) enables hello administrator of another subscription (Dev-Test) toolink up tootwo virtual networks toohello circuit.</span></span> <span data-ttu-id="08492-151">Merhaba Contoso BT yöneticisinin bu hello geliştirme, Test Microsoft kimliği belirtilerek sağlar.</span><span class="sxs-lookup"><span data-stu-id="08492-151">hello Contoso IT administrator enables this by specifying hello Dev-Test Microsoft ID.</span></span> <span data-ttu-id="08492-152">e-posta toohello Microsoft kimliği belirtildi. Hello cmdlet göndermez</span><span class="sxs-lookup"><span data-stu-id="08492-152">hello cmdlet doesn't send email toohello specified Microsoft ID.</span></span> <span data-ttu-id="08492-153">Merhaba devre sahibinden gereken tooexplicitly yetkilendirme hello diğer abonelik sahibi tamamlandığında hello bildirin.</span><span class="sxs-lookup"><span data-stu-id="08492-153">hello circuit owner needs tooexplicitly notify hello other subscription owner that hello authorization is complete.</span></span>

    New-AzureDedicatedCircuitLinkAuthorization -ServiceKey "**************************" -Description "Dev-Test Links" -Limit 2 -MicrosoftIds 'devtest@contoso.com'

    Description         : Dev-Test Links
    Limit               : 2
    LinkAuthorizationId : **********************************
    MicrosoftIds        : devtest@contoso.com
    Used                : 0

<span data-ttu-id="08492-154">**Yetkilerini gözden geçirme**</span><span class="sxs-lookup"><span data-stu-id="08492-154">**Reviewing authorizations**</span></span>

<span data-ttu-id="08492-155">Merhaba devre sahibinden hello aşağıdaki cmdlet'i çalıştırarak belirli bir bağlantı hattı üzerinde verilen tüm yetkilerini gözden geçirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="08492-155">hello circuit owner can review all authorizations that are issued on a particular circuit by running hello following cmdlet:</span></span>

    Get-AzureDedicatedCircuitLinkAuthorization -ServiceKey: "**************************"

    Description         : EngineeringTeam
    Limit               : 3
    LinkAuthorizationId : ####################################
    MicrosoftIds        : engadmin@contoso.com
    Used                : 1

    Description         : MarketingTeam
    Limit               : 1
    LinkAuthorizationId : @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
    MicrosoftIds        : marketingadmin@contoso.com
    Used                : 0

    Description         : Dev-Test Links
    Limit               : 2
    LinkAuthorizationId : &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&
    MicrosoftIds        : salesadmin@contoso.com
    Used                : 2


<span data-ttu-id="08492-156">**Yetkilerini güncelleştiriliyor**</span><span class="sxs-lookup"><span data-stu-id="08492-156">**Updating authorizations**</span></span>

<span data-ttu-id="08492-157">Merhaba devre sahibinden yetkilerini cmdlet'i aşağıdaki hello kullanarak değiştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="08492-157">hello circuit owner can modify authorizations by using hello following cmdlet:</span></span>

    Set-AzureDedicatedCircuitLinkAuthorization -ServiceKey "**************************" -AuthorizationId "&&&&&&&&&&&&&&&&&&&&&&&&&&&&"-Limit 5

    Description         : Dev-Test Links
    Limit               : 5
    LinkAuthorizationId : &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&
    MicrosoftIds        : devtest@contoso.com
    Used                : 0


<span data-ttu-id="08492-158">**Yetkilerini silme**</span><span class="sxs-lookup"><span data-stu-id="08492-158">**Deleting authorizations**</span></span>

<span data-ttu-id="08492-159">Merhaba devre sahibinden revoke/yetkilerini toohello kullanıcı hello aşağıdaki cmdlet'i çalıştırarak silme:</span><span class="sxs-lookup"><span data-stu-id="08492-159">hello circuit owner can revoke/delete authorizations toohello user by running hello following cmdlet:</span></span>

    Remove-AzureDedicatedCircuitLinkAuthorization -ServiceKey "*****************************" -AuthorizationId "###############################"


### <a name="circuit-user-operations"></a><span data-ttu-id="08492-160">Bağlantı hattı kullanıcı işlemleri</span><span class="sxs-lookup"><span data-stu-id="08492-160">Circuit user operations</span></span>

<span data-ttu-id="08492-161">**Yetkilerini gözden geçirme**</span><span class="sxs-lookup"><span data-stu-id="08492-161">**Reviewing authorizations**</span></span>

<span data-ttu-id="08492-162">Hello hattı kullanıcı yetkilerini cmdlet'i aşağıdaki hello kullanarak gözden geçirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="08492-162">hello circuit user can review authorizations by using hello following cmdlet:</span></span>

    Get-AzureAuthorizedDedicatedCircuit

    Bandwidth                        : 200
    CircuitName                      : ContosoIT
    Location                         : Washington DC
    MaximumAllowedLinks              : 2
    ServiceKey                       : &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Status                           : Enabled
    UsedLinks                        : 0

<span data-ttu-id="08492-163">**Bağlantı yetkilerini itibaren**</span><span class="sxs-lookup"><span data-stu-id="08492-163">**Redeeming link authorizations**</span></span>

<span data-ttu-id="08492-164">Merhaba hattı kullanıcı cmdlet tooredeem aşağıdaki hello bağlantı yetkilendirme çalıştırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="08492-164">hello circuit user can run hello following cmdlet tooredeem a link authorization:</span></span>

    New-AzureDedicatedCircuitLink –servicekey "&&&&&&&&&&&&&&&&&&&&&&&&&&" –VnetName 'SalesVNET1'

    State VnetName
    ----- --------
    Provisioned SalesVNET1

<span data-ttu-id="08492-165">Yeni bağlantılı hello abonelik hello sanal ağ için bu komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="08492-165">Run this command in hello newly linked subscription for hello virtual network:</span></span>

    New-AzureDedicatedCircuitLink -ServiceKey "*****************************" -VNetName "MyVNet"

## <a name="next-steps"></a><span data-ttu-id="08492-166">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="08492-166">Next steps</span></span>
<span data-ttu-id="08492-167">ExpressRoute hakkında daha fazla bilgi için bkz: Merhaba [ExpressRoute SSS](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="08492-167">For more information about ExpressRoute, see hello [ExpressRoute FAQ](expressroute-faqs.md).</span></span>

