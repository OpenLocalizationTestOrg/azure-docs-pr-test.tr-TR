---
title: "Nasıl tooconfigure (eşleme) bir expressroute bağlantı hattı için yönlendirmeyi: Resource Manager: PowerShell: Azure | Microsoft Docs"
description: "Bu makalede, oluşturma ve sağlama hello özel, genel ve Microsoft bir expressroute bağlantı hattı eşlemesi hello adım adım anlatılmaktadır. Bu makalede ayrıca nasıl toocheck hello durumu, güncelleştirme veya bağlantı hattınız için eşlemeleri silme gösterilmektedir."
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 0a036d51-77ae-4fee-9ddb-35f040fbdcdf
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: eb3ddf5c05a086ac3e22c64417e51381ef465921
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-peering-for-an-expressroute-circuit-using-powershell"></a><span data-ttu-id="9ae37-104">Oluşturma ve PowerShell kullanarak bir ExpressRoute bağlantı hattı için eşlemesini değiştirme</span><span class="sxs-lookup"><span data-stu-id="9ae37-104">Create and modify peering for an ExpressRoute circuit using PowerShell</span></span>

<span data-ttu-id="9ae37-105">Bu makalede, PowerShell kullanarak hello Resource Manager dağıtım modelinde bir expressroute bağlantı hattı için yönlendirme yapılandırması oluşturma ve yönetme yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="9ae37-105">This article helps you create and manage routing configuration for an ExpressRoute circuit in hello Resource Manager deployment model using PowerShell.</span></span> <span data-ttu-id="9ae37-106">Ayrıca, hello durumu, güncelleştirme veya silme denetleyin ve bir expressroute bağlantı hattı için eşlemeler sağlamayı sonlandırın.</span><span class="sxs-lookup"><span data-stu-id="9ae37-106">You can also check hello status, update, or delete and deprovision peerings for an ExpressRoute circuit.</span></span> <span data-ttu-id="9ae37-107">Bağlantı hattınız ile toouse farklı yöntem toowork istiyorsanız, bir makale listesi aşağıdaki hello seçin:</span><span class="sxs-lookup"><span data-stu-id="9ae37-107">If you want toouse a different method toowork with your circuit, select an article from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="9ae37-108">Azure portal</span><span class="sxs-lookup"><span data-stu-id="9ae37-108">Azure portal</span></span>](expressroute-howto-routing-portal-resource-manager.md)
> * [<span data-ttu-id="9ae37-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9ae37-109">PowerShell</span></span>](expressroute-howto-routing-arm.md)
> * [<span data-ttu-id="9ae37-110">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="9ae37-110">Azure CLI</span></span>](howto-routing-cli.md)
> * [<span data-ttu-id="9ae37-111">Video - özel eşliği</span><span class="sxs-lookup"><span data-stu-id="9ae37-111">Video - Private peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-private-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="9ae37-112">Video - ortak eşleme</span><span class="sxs-lookup"><span data-stu-id="9ae37-112">Video - Public peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-public-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="9ae37-113">Video - Microsoft eşlemesi</span><span class="sxs-lookup"><span data-stu-id="9ae37-113">Video - Microsoft peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-microsoft-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="9ae37-114">PowerShell (klasik)</span><span class="sxs-lookup"><span data-stu-id="9ae37-114">PowerShell (classic)</span></span>](expressroute-howto-routing-classic.md)
> 

## <a name="configuration-prerequisites"></a><span data-ttu-id="9ae37-115">Yapılandırma önkoşulları</span><span class="sxs-lookup"><span data-stu-id="9ae37-115">Configuration prerequisites</span></span>

* <span data-ttu-id="9ae37-116">Hello Azure Resource Manager PowerShell cmdlet'lerinin en son sürümünü hello gerekir.</span><span class="sxs-lookup"><span data-stu-id="9ae37-116">You will need hello latest version of hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="9ae37-117">Daha fazla bilgi için bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="9ae37-117">For more information, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span> 
* <span data-ttu-id="9ae37-118">Merhaba gözden geçirdiğinizden emin olun [Önkoşullar](expressroute-prerequisites.md) hello sayfasında [yönlendirme gereksinimleri](expressroute-routing.md) sayfası ve hello [iş akışları](expressroute-workflows.md) yapılandırmaya başlamadan önce sayfasında.</span><span class="sxs-lookup"><span data-stu-id="9ae37-118">Make sure that you have reviewed hello [prerequisites](expressroute-prerequisites.md) page, hello [routing requirements](expressroute-routing.md) page, and hello [workflows](expressroute-workflows.md) page before you begin configuration.</span></span>
* <span data-ttu-id="9ae37-119">Etkin bir ExpressRoute bağlantı hattınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="9ae37-119">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="9ae37-120">Çok olarak Hello yönergeleri[bir expressroute bağlantı hattı oluşturma](expressroute-howto-circuit-arm.md) ve devam etmeden önce bağlantı sağlayıcınız tarafından etkinleştirilen hello hattı sahip.</span><span class="sxs-lookup"><span data-stu-id="9ae37-120">Follow hello instructions too[Create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have hello circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="9ae37-121">Merhaba expressroute bağlantı hattı, bu makaledeki toobe mümkün toorun hello cmdlet'leri için sağlanmış ve etkin durumda olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="9ae37-121">hello ExpressRoute circuit must be in a provisioned and enabled state for you toobe able toorun hello cmdlets in this article.</span></span>

<span data-ttu-id="9ae37-122">Bu yönergeler yalnızca Katman 2 bağlantı hizmetleri sunan hizmet sağlayıcıları ile oluşturulan toocircuits geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="9ae37-122">These instructions only apply toocircuits created with service providers offering Layer 2 connectivity services.</span></span> <span data-ttu-id="9ae37-123">Yönetilen sunan bir hizmet sağlayıcısı kullanıyorsanız, Katman 3 Hizmetleri (genellikle gibi bir IPVPN MPLS), bağlantı sağlayıcınız yapılandırmak ve yönetmek için yönlendirme.</span><span class="sxs-lookup"><span data-stu-id="9ae37-123">If you are using a service provider that offers managed Layer 3 services (typically an IPVPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9ae37-124">Biz hello Hizmet Yönetimi Portalı aracılığıyla hizmet sağlayıcılar tarafından yapılandırılan eşlemeleri şu anda tanıtmıyoruz.</span><span class="sxs-lookup"><span data-stu-id="9ae37-124">We currently do not advertise peerings configured by service providers through hello service management portal.</span></span> <span data-ttu-id="9ae37-125">Bu özelliği yakında etkinleştirmek için çalışıyoruz.</span><span class="sxs-lookup"><span data-stu-id="9ae37-125">We are working on enabling this capability soon.</span></span> <span data-ttu-id="9ae37-126">BGP eşlemelerini yapılandırmadan önce hizmet sağlayıcınıza başvurun.</span><span class="sxs-lookup"><span data-stu-id="9ae37-126">Check with your service provider before configuring BGP peerings.</span></span>
> 
> 

<span data-ttu-id="9ae37-127">Bir ExpressRoute bağlantı hattı için bir, iki veya üç eşlemenin tamamını (Azure özel, Azure ortak ve Microsoft) yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9ae37-127">You can configure one, two, or all three peerings (Azure private, Azure public and Microsoft) for an ExpressRoute circuit.</span></span> <span data-ttu-id="9ae37-128">Eşlemeleri seçtiğiniz herhangi bir sırayla yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9ae37-128">You can configure peerings in any order you choose.</span></span> <span data-ttu-id="9ae37-129">Bununla birlikte, her eşleme birer birer başlangıç yapılandırmasını tamamlayın emin olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="9ae37-129">However, you must make sure that you complete hello configuration of each peering one at a time.</span></span> 

## <a name="azure-private-peering"></a><span data-ttu-id="9ae37-130">Azure özel eşlemesi</span><span class="sxs-lookup"><span data-stu-id="9ae37-130">Azure private peering</span></span>

<span data-ttu-id="9ae37-131">Bu bölümde, oluşturma, alma, güncelleştirme ve hello bir expressroute bağlantı hattı için Azure özel eşleme yapılandırmasını silme yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="9ae37-131">This section helps you create, get, update, and delete hello Azure private peering configuration for an ExpressRoute circuit.</span></span>

### <a name="toocreate-azure-private-peering"></a><span data-ttu-id="9ae37-132">Azure özel eşleme toocreate</span><span class="sxs-lookup"><span data-stu-id="9ae37-132">toocreate Azure private peering</span></span>

1. <span data-ttu-id="9ae37-133">ExpressRoute için Hello PowerShell modülünü içeri aktarın.</span><span class="sxs-lookup"><span data-stu-id="9ae37-133">Import hello PowerShell module for ExpressRoute.</span></span>

  <span data-ttu-id="9ae37-134">Merhaba son PowerShell'i Yükleyiciden yüklemelisiniz [PowerShell Galerisi](http://www.powershellgallery.com/) ve hello ExpressRoute cmdlet'lerini kullanmaya sipariş toostart hello PowerShell oturumunda hello Azure Resource Manager modüllerini aktarın.</span><span class="sxs-lookup"><span data-stu-id="9ae37-134">You must install hello latest PowerShell installer from [PowerShell Gallery](http://www.powershellgallery.com/) and import hello Azure Resource Manager modules into hello PowerShell session in order toostart using hello ExpressRoute cmdlets.</span></span> <span data-ttu-id="9ae37-135">Yönetici olarak toorun PowerShell gerekir.</span><span class="sxs-lookup"><span data-stu-id="9ae37-135">You will need toorun PowerShell as an Administrator.</span></span>

  ```powershell
  Install-Module AzureRM
  Install-AzureRM
  ```

  <span data-ttu-id="9ae37-136">Tüm hello bilinen semantik sürüm aralığı içinde hello AzureRM.* modüllerini içeri aktarın.</span><span class="sxs-lookup"><span data-stu-id="9ae37-136">Import all of hello AzureRM.* modules within hello known semantic version range.</span></span>

  ```powershell
  Import-AzureRM
  ```

  <span data-ttu-id="9ae37-137">Ayrıca hello bilinen semantik sürüm aralığı içinde seçili bir modülü içeri aktarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9ae37-137">You can also just import a select module within hello known semantic version range.</span></span>

  ```powershell
  Import-Module AzureRM.Network 
  ```

  <span data-ttu-id="9ae37-138">Tooyour hesabında oturum açın.</span><span class="sxs-lookup"><span data-stu-id="9ae37-138">Sign in tooyour account.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

  <span data-ttu-id="9ae37-139">Toocreate expressroute bağlantı hattı hello aboneliği seçin.</span><span class="sxs-lookup"><span data-stu-id="9ae37-139">Select hello subscription you want toocreate ExpressRoute circuit.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
  ```
2. <span data-ttu-id="9ae37-140">ExpressRoute bağlantı hattı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9ae37-140">Create an ExpressRoute circuit.</span></span>

  <span data-ttu-id="9ae37-141">Merhaba yönergeleri toocreate izleyin bir [expressroute bağlantı hattı](expressroute-howto-circuit-arm.md) ve hello bağlantı sağlayıcı tarafından sağlanan sahip.</span><span class="sxs-lookup"><span data-stu-id="9ae37-141">Follow hello instructions toocreate an [ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have it provisioned by hello connectivity provider.</span></span>

  <span data-ttu-id="9ae37-142">Bağlantı sağlayıcınız yönetilen Katman 3 Hizmetleri sunuyorsa, bağlantı sağlayıcısı tooenable Azure sizin için eşlemeyi özel isteyebilir.</span><span class="sxs-lookup"><span data-stu-id="9ae37-142">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider tooenable Azure private peering for you.</span></span> <span data-ttu-id="9ae37-143">Bu durumda, hello sonraki bölümlerde listelenen toofollow yönergeleri gerekmez.</span><span class="sxs-lookup"><span data-stu-id="9ae37-143">In that case, you won't need toofollow instructions listed in hello next sections.</span></span> <span data-ttu-id="9ae37-144">Ancak, bağlantı sağlayıcınız yönlendirmeyi sizin için hattınızı oluşturduktan sonra yönetmiyorsa yapılandırmanızı hello sonraki adımları kullanarak devam edin.</span><span class="sxs-lookup"><span data-stu-id="9ae37-144">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using hello next steps.</span></span>
3. <span data-ttu-id="9ae37-145">Merhaba ExpressRoute bağlantı hattı toomake sağlanan ve ayrıca etkin olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="9ae37-145">Check hello ExpressRoute circuit toomake sure it is provisioned and also enabled.</span></span> <span data-ttu-id="9ae37-146">Aşağıdaki örnek hello kullan:</span><span class="sxs-lookup"><span data-stu-id="9ae37-146">Use hello following example:</span></span>

  ```powershell
  Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
  ```

  <span data-ttu-id="9ae37-147">Merhaba yanıt benzer toohello örneği aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="9ae37-147">hello response is similar toohello following example:</span></span>

  ```
  Name                             : ExpressRouteARMCircuit
  ResourceGroupName                : ExpressRouteResourceGroup
  Location                         : westus
  Id                               : /subscriptions/***************************/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/ExpressRouteARMCircuit
  Etag                             : W/"################################"
  ProvisioningState                : Succeeded
  Sku                              : {
                                       "Name": "Standard_MeteredData",
                                       "Tier": "Standard",
                                       "Family": "MeteredData"
                                     }
  CircuitProvisioningState         : Enabled
  ServiceProviderProvisioningState : Provisioned
  ServiceProviderNotes             : 
  ServiceProviderProperties        : {
                                       "ServiceProviderName": "Equinix",
                                       "PeeringLocation": "Silicon Valley",
                                       "BandwidthInMbps": 200
                                     }
  ServiceKey                       : **************************************
  Peerings                         : []
  ```
4. <span data-ttu-id="9ae37-148">Merhaba bağlantı hattı için Azure özel eşlemesini yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="9ae37-148">Configure Azure private peering for hello circuit.</span></span> <span data-ttu-id="9ae37-149">Merhaba sonraki adımlara devam etmeden önce aşağıdaki öğelerindeki hello sahip olduğunuzdan emin olun:</span><span class="sxs-lookup"><span data-stu-id="9ae37-149">Make sure that you have hello following items before you proceed with hello next steps:</span></span>

  * <span data-ttu-id="9ae37-150">Bir/30 alt ağı hello birincil bağlantı için.</span><span class="sxs-lookup"><span data-stu-id="9ae37-150">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="9ae37-151">Merhaba alt ağ, sanal ağlar için ayrılmış herhangi bir adres alanının parçası olmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="9ae37-151">hello subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="9ae37-152">Bir/30 alt ağı hello ikincil bağlantı için.</span><span class="sxs-lookup"><span data-stu-id="9ae37-152">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="9ae37-153">Merhaba alt ağ, sanal ağlar için ayrılmış herhangi bir adres alanının parçası olmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="9ae37-153">hello subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="9ae37-154">Geçerli bir VLAN kimliği tooestablish bu eşlemenin.</span><span class="sxs-lookup"><span data-stu-id="9ae37-154">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="9ae37-155">Hiçbir diğer eşliği emin hello devredeki aynı VLAN kimliğini kullanan hello</span><span class="sxs-lookup"><span data-stu-id="9ae37-155">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
  * <span data-ttu-id="9ae37-156">Eşleme için AS numarası.</span><span class="sxs-lookup"><span data-stu-id="9ae37-156">AS number for peering.</span></span> <span data-ttu-id="9ae37-157">2 bayt ve 4 bayt AS numaralarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9ae37-157">You can use both 2-byte and 4-byte AS numbers.</span></span> <span data-ttu-id="9ae37-158">Bu eşleme için özel bir AS numarası kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9ae37-158">You can use a private AS number for this peering.</span></span> <span data-ttu-id="9ae37-159">65515’i kullanmadığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="9ae37-159">Ensure that you are not using 65515.</span></span>
  * <span data-ttu-id="9ae37-160">**İsteğe bağlı -** toouse birini seçerseniz bir MD5 karma değeri.</span><span class="sxs-lookup"><span data-stu-id="9ae37-160">**Optional -** An MD5 hash if you choose toouse one.</span></span>

  <span data-ttu-id="9ae37-161">Aşağıdaki örnek tooconfigure Azure hattınız için eşlemesini özel hello kullan:</span><span class="sxs-lookup"><span data-stu-id="9ae37-161">Use hello following example tooconfigure Azure private peering for your circuit:</span></span>

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt -PeeringType AzurePrivatePeering -PeerASN 100 -PrimaryPeerAddressPrefix "10.0.0.0/30" -SecondaryPeerAddressPrefix "10.0.0.4/30" -VlanId 200

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

  <span data-ttu-id="9ae37-162">Bir MD5 karma değeri toouse seçerseniz, aşağıdaki örneğine hello kullan:</span><span class="sxs-lookup"><span data-stu-id="9ae37-162">If you choose toouse an MD5 hash, use hello following example:</span></span>

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt -PeeringType AzurePrivatePeering -PeerASN 100 -PrimaryPeerAddressPrefix "10.0.0.0/30" -SecondaryPeerAddressPrefix "10.0.0.4/30" -VlanId 200  -SharedKey "A1B2C3D4"
  ```

  > [!IMPORTANT]
  > <span data-ttu-id="9ae37-163">AS numaranızı müşteri ASN’si değil eşleme ASN’si olarak belirttiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="9ae37-163">Ensure that you specify your AS number as peering ASN, not customer ASN.</span></span>
  > 
  >

### <a name="tooview-azure-private-peering-details"></a><span data-ttu-id="9ae37-164">tooview Azure özel eşleme ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="9ae37-164">tooview Azure private peering details</span></span>

<span data-ttu-id="9ae37-165">Aşağıdaki örnek hello kullanarak yapılandırma ayrıntılarını alabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="9ae37-165">You can get configuration details by using hello following example:</span></span>

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -Circuit $ckt
```

### <a name="tooupdate-azure-private-peering-configuration"></a><span data-ttu-id="9ae37-166">Azure özel eşleme yapılandırmasını tooupdate</span><span class="sxs-lookup"><span data-stu-id="9ae37-166">tooupdate Azure private peering configuration</span></span>

<span data-ttu-id="9ae37-167">Aşağıdaki örneğine hello kullanarak hello yapılandırmasını herhangi bir bölümünü güncelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9ae37-167">You can update any part of hello configuration using hello following example.</span></span> <span data-ttu-id="9ae37-168">Bu örnekte, hello hello hattının VLAN kimliği 100 too500 güncelleştiriliyor.</span><span class="sxs-lookup"><span data-stu-id="9ae37-168">In this example, hello VLAN ID of hello circuit is being updated from 100 too500.</span></span>

```powershell
Set-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt -PeeringType AzurePrivatePeering -PeerASN 100 -PrimaryPeerAddressPrefix "10.0.0.0/30" -SecondaryPeerAddressPrefix "10.0.0.4/30" -VlanId 200

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="toodelete-azure-private-peering"></a><span data-ttu-id="9ae37-169">Azure özel eşleme toodelete</span><span class="sxs-lookup"><span data-stu-id="9ae37-169">toodelete Azure private peering</span></span>

<span data-ttu-id="9ae37-170">Aşağıdaki örnek hello çalıştırarak eşleme yapılandırmanızı kaldırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="9ae37-170">You can remove your peering configuration by running hello following example:</span></span>

> [!WARNING]
> <span data-ttu-id="9ae37-171">Bu örneği çalıştırmadan önce tüm sanal ağları expressroute bağlantı hattı hello bağlantısız olduğundan emin olmalısınız.</span><span class="sxs-lookup"><span data-stu-id="9ae37-171">You must ensure that all virtual networks are unlinked from hello ExpressRoute circuit before running this example.</span></span> 
> 
> 

```powershell
Remove-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <a name="azure-public-peering"></a><span data-ttu-id="9ae37-172">Azure ortak eşleme</span><span class="sxs-lookup"><span data-stu-id="9ae37-172">Azure public peering</span></span>

<span data-ttu-id="9ae37-173">Bu bölümde, oluşturma, alma, güncelleştirme ve hello bir expressroute bağlantı hattı için Azure ortak eşleme yapılandırmasını silme yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="9ae37-173">This section helps you create, get, update, and delete hello Azure public peering configuration for an ExpressRoute circuit.</span></span>

### <a name="toocreate-azure-public-peering"></a><span data-ttu-id="9ae37-174">Azure ortak eşleme toocreate</span><span class="sxs-lookup"><span data-stu-id="9ae37-174">toocreate Azure public peering</span></span>

1. <span data-ttu-id="9ae37-175">ExpressRoute için Hello PowerShell modülünü içeri aktarın.</span><span class="sxs-lookup"><span data-stu-id="9ae37-175">Import hello PowerShell module for ExpressRoute.</span></span>

  <span data-ttu-id="9ae37-176">Merhaba son PowerShell'i Yükleyiciden yüklemelisiniz [PowerShell Galerisi](http://www.powershellgallery.com/) ve hello ExpressRoute cmdlet'lerini kullanmaya sipariş toostart hello PowerShell oturumunda hello Azure Resource Manager modüllerini aktarın.</span><span class="sxs-lookup"><span data-stu-id="9ae37-176">You must install hello latest PowerShell installer from [PowerShell Gallery](http://www.powershellgallery.com/) and import hello Azure Resource Manager modules into hello PowerShell session in order toostart using hello ExpressRoute cmdlets.</span></span> <span data-ttu-id="9ae37-177">Yönetici olarak toorun PowerShell gerekir.</span><span class="sxs-lookup"><span data-stu-id="9ae37-177">You will need toorun PowerShell as an Administrator.</span></span>

  ```powershell
  Install-Module AzureRM

  Install-AzureRM
```

  <span data-ttu-id="9ae37-178">Tüm hello bilinen semantik sürüm aralığı içinde hello AzureRM.* modüllerini içeri aktarın.</span><span class="sxs-lookup"><span data-stu-id="9ae37-178">Import all of hello AzureRM.* modules within hello known semantic version range.</span></span>

  ```powershell
  Import-AzureRM
  ```

  <span data-ttu-id="9ae37-179">Ayrıca hello bilinen semantik sürüm aralığı içinde seçili bir modülü içeri aktarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9ae37-179">You can also just import a select module within hello known semantic version range.</span></span>

  ```powershell
  Import-Module AzureRM.Network
```

  <span data-ttu-id="9ae37-180">Tooyour hesabında oturum açın.</span><span class="sxs-lookup"><span data-stu-id="9ae37-180">Sign in tooyour account.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

  <span data-ttu-id="9ae37-181">Toocreate expressroute bağlantı hattı hello aboneliği seçin.</span><span class="sxs-lookup"><span data-stu-id="9ae37-181">Select hello subscription you want toocreate ExpressRoute circuit.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
  ```
2. <span data-ttu-id="9ae37-182">ExpressRoute bağlantı hattı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9ae37-182">Create an ExpressRoute circuit.</span></span>

  <span data-ttu-id="9ae37-183">Merhaba yönergeleri toocreate izleyin bir [expressroute bağlantı hattı](expressroute-howto-circuit-arm.md) ve hello bağlantı sağlayıcı tarafından sağlanan sahip.</span><span class="sxs-lookup"><span data-stu-id="9ae37-183">Follow hello instructions toocreate an [ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have it provisioned by hello connectivity provider.</span></span>

  <span data-ttu-id="9ae37-184">Bağlantı sağlayıcınız yönetilen Katman 3 Hizmetleri sunuyorsa, bağlantı sağlayıcısı tooenable Azure sizin için eşlemeyi özel isteyebilir.</span><span class="sxs-lookup"><span data-stu-id="9ae37-184">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider tooenable Azure private peering for you.</span></span> <span data-ttu-id="9ae37-185">Bu durumda, hello sonraki bölümlerde listelenen toofollow yönergeleri gerekmez.</span><span class="sxs-lookup"><span data-stu-id="9ae37-185">In that case, you won't need toofollow instructions listed in hello next sections.</span></span> <span data-ttu-id="9ae37-186">Ancak, bağlantı sağlayıcınız yönlendirmeyi sizin için hattınızı oluşturduktan sonra yönetmiyorsa yapılandırmanızı hello sonraki adımları kullanarak devam edin.</span><span class="sxs-lookup"><span data-stu-id="9ae37-186">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using hello next steps.</span></span>
3. <span data-ttu-id="9ae37-187">Sağlanan ve ayrıca etkin hello ExpressRoute bağlantı hattı tooensure denetleyin.</span><span class="sxs-lookup"><span data-stu-id="9ae37-187">Check hello ExpressRoute circuit tooensure it is provisioned and also enabled.</span></span> <span data-ttu-id="9ae37-188">Aşağıdaki örnek hello kullan:</span><span class="sxs-lookup"><span data-stu-id="9ae37-188">Use hello following example:</span></span>

  ```powershell
  Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
  ```

  <span data-ttu-id="9ae37-189">Merhaba yanıt benzer toohello örneği aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="9ae37-189">hello response is similar toohello following example:</span></span>

  ```
  Name                             : ExpressRouteARMCircuit
  ResourceGroupName                : ExpressRouteResourceGroup
  Location                         : westus
  Id                               : /subscriptions/***************************/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/ExpressRouteARMCircuit
  Etag                             : W/"################################"
  ProvisioningState                : Succeeded
  Sku                              : {
                                      "Name": "Standard_MeteredData",
                                       "Tier": "Standard",
                                       "Family": "MeteredData"
                                     }
  CircuitProvisioningState         : Enabled
  ServiceProviderProvisioningState : Provisioned
  ServiceProviderNotes             : 
  ServiceProviderProperties        : {
                                       "ServiceProviderName": "Equinix",
                                       "PeeringLocation": "Silicon Valley",
                                       "BandwidthInMbps": 200
                                     }
  ServiceKey                       : **************************************
  Peerings                         : []
  ```
4. <span data-ttu-id="9ae37-190">Merhaba bağlantı hattı için Azure ortak eşlemesini yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="9ae37-190">Configure Azure public peering for hello circuit.</span></span> <span data-ttu-id="9ae37-191">Devam etmeden önce aşağıdaki bilgilerle hello sahip olduğunuzdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="9ae37-191">Make sure that you have hello following information before you proceed further.</span></span>

  * <span data-ttu-id="9ae37-192">Bir/30 alt ağı hello birincil bağlantı için.</span><span class="sxs-lookup"><span data-stu-id="9ae37-192">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="9ae37-193">Bu geçerli bir ortak IPv4 öneki olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="9ae37-193">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="9ae37-194">Bir/30 alt ağı hello ikincil bağlantı için.</span><span class="sxs-lookup"><span data-stu-id="9ae37-194">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="9ae37-195">Bu geçerli bir ortak IPv4 öneki olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="9ae37-195">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="9ae37-196">Geçerli bir VLAN kimliği tooestablish bu eşlemenin.</span><span class="sxs-lookup"><span data-stu-id="9ae37-196">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="9ae37-197">Hiçbir diğer eşliği emin hello devredeki aynı VLAN kimliğini kullanan hello</span><span class="sxs-lookup"><span data-stu-id="9ae37-197">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
  * <span data-ttu-id="9ae37-198">Eşleme için AS numarası.</span><span class="sxs-lookup"><span data-stu-id="9ae37-198">AS number for peering.</span></span> <span data-ttu-id="9ae37-199">2 bayt ve 4 bayt AS numaralarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9ae37-199">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="9ae37-200">**İsteğe bağlı -** toouse birini seçerseniz bir MD5 karma değeri.</span><span class="sxs-lookup"><span data-stu-id="9ae37-200">**Optional -** An MD5 hash if you choose toouse one.</span></span>

  <span data-ttu-id="9ae37-201">Aşağıdaki örnek tooconfigure Azure hattınız için eşlemesini genel hello çalıştırın</span><span class="sxs-lookup"><span data-stu-id="9ae37-201">Run hello following example tooconfigure Azure public peering for your circuit</span></span>

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt -PeeringType AzurePublicPeering -PeerASN 100 -PrimaryPeerAddressPrefix "12.0.0.0/30" -SecondaryPeerAddressPrefix "12.0.0.4/30" -VlanId 100

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

  <span data-ttu-id="9ae37-202">Bir MD5 karma değeri toouse seçerseniz, aşağıdaki örneğine hello kullan:</span><span class="sxs-lookup"><span data-stu-id="9ae37-202">If you choose toouse an MD5 hash, use hello following example:</span></span>

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt -PeeringType AzurePublicPeering -PeerASN 100 -PrimaryPeerAddressPrefix "12.0.0.0/30" -SecondaryPeerAddressPrefix "12.0.0.4/30" -VlanId 100  -SharedKey "A1B2C3D4"

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

  > [!IMPORTANT]
  > <span data-ttu-id="9ae37-203">AS numaranızı müşteri ASN’si değil eşleme ASN’si olarak belirttiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="9ae37-203">Ensure that you specify your AS number as peering ASN, not customer ASN.</span></span>
  > 
  >

### <a name="tooview-azure-public-peering-details"></a><span data-ttu-id="9ae37-204">tooview Azure genel eşliği ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="9ae37-204">tooview Azure public peering details</span></span>

<span data-ttu-id="9ae37-205">Hello aşağıdaki cmdlet'i kullanarak yapılandırma ayrıntılarını alabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="9ae37-205">You can get configuration details using hello following cmdlet:</span></span>

```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

  Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -Circuit $ckt
  ```

### <a name="tooupdate-azure-public-peering-configuration"></a><span data-ttu-id="9ae37-206">Azure ortak eşleme yapılandırmasını tooupdate</span><span class="sxs-lookup"><span data-stu-id="9ae37-206">tooupdate Azure public peering configuration</span></span>

<span data-ttu-id="9ae37-207">Aşağıdaki örneğine hello kullanarak hello yapılandırmasını herhangi bir bölümünü güncelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9ae37-207">You can update any part of hello configuration using hello following example.</span></span> <span data-ttu-id="9ae37-208">Bu örnekte, hello hello hattının VLAN kimliği 200 too600 güncelleştiriliyor.</span><span class="sxs-lookup"><span data-stu-id="9ae37-208">In this example, hello VLAN ID of hello circuit is being updated from 200 too600.</span></span>

```powershell
Set-AzureRmExpressRouteCircuitPeeringConfig  -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt -PeeringType AzurePublicPeering -PeerASN 100 -PrimaryPeerAddressPrefix "123.0.0.0/30" -SecondaryPeerAddressPrefix "123.0.0.4/30" -VlanId 600

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="toodelete-azure-public-peering"></a><span data-ttu-id="9ae37-209">Azure ortak eşleme toodelete</span><span class="sxs-lookup"><span data-stu-id="9ae37-209">toodelete Azure public peering</span></span>

<span data-ttu-id="9ae37-210">Aşağıdaki örnek hello çalıştırarak eşleme yapılandırmanızı kaldırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="9ae37-210">You can remove your peering configuration by running hello following example:</span></span>

```powershell
Remove-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <a name="microsoft-peering"></a><span data-ttu-id="9ae37-211">Microsoft eşlemesi</span><span class="sxs-lookup"><span data-stu-id="9ae37-211">Microsoft peering</span></span>

<span data-ttu-id="9ae37-212">Bu bölümde, oluşturma, alma, güncelleştirme ve bir expressroute bağlantı hattı için Microsoft eşleme yapılandırmasını hello silme yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="9ae37-212">This section helps you create, get, update, and delete hello Microsoft peering configuration for an ExpressRoute circuit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9ae37-213">Önceki tooAugust 1 yapılandırılmış olan ExpressRoute bağlantı hatları Microsoft eşliği, yol filtreleri tanımlanmamış olsa bile 2017 hello Microsoft eşleme aracılığıyla tanıtılan tüm hizmet ön eklerin sahip olur.</span><span class="sxs-lookup"><span data-stu-id="9ae37-213">Microsoft peering of ExpressRoute circuits that were configured prior tooAugust 1, 2017 will have all service prefixes advertised through hello Microsoft peering, even if route filters are not defined.</span></span> <span data-ttu-id="9ae37-214">Ve 1 Ağustos 2017 sonrasında yapılandırılmış ExpressRoute bağlantı hatları, Microsoft eşlemesi sahip olmaz tüm ön eklerin rota filtre bağlanana kadar tanıtılan toohello hattı.</span><span class="sxs-lookup"><span data-stu-id="9ae37-214">Microsoft peering of ExpressRoute circuits that are configured on or after August 1, 2017 will not have any prefixes advertised until a route filter is attached toohello circuit.</span></span> <span data-ttu-id="9ae37-215">Daha fazla bilgi için bkz: [Microsoft eşliği için rota filtresini Yapılandır](how-to-routefilter-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="9ae37-215">For more information, see [Configure a route filter for Microsoft peering](how-to-routefilter-powershell.md).</span></span>
> 
> 

### <a name="toocreate-microsoft-peering"></a><span data-ttu-id="9ae37-216">toocreate Microsoft eşlemesi</span><span class="sxs-lookup"><span data-stu-id="9ae37-216">toocreate Microsoft peering</span></span>

1. <span data-ttu-id="9ae37-217">ExpressRoute için Hello PowerShell modülünü içeri aktarın.</span><span class="sxs-lookup"><span data-stu-id="9ae37-217">Import hello PowerShell module for ExpressRoute.</span></span>

  <span data-ttu-id="9ae37-218">Merhaba son PowerShell'i Yükleyiciden yüklemelisiniz [PowerShell Galerisi](http://www.powershellgallery.com/) ve hello ExpressRoute cmdlet'lerini kullanmaya sipariş toostart hello PowerShell oturumunda hello Azure Resource Manager modüllerini aktarın.</span><span class="sxs-lookup"><span data-stu-id="9ae37-218">You must install hello latest PowerShell installer from [PowerShell Gallery](http://www.powershellgallery.com/) and import hello Azure Resource Manager modules into hello PowerShell session in order toostart using hello ExpressRoute cmdlets.</span></span> <span data-ttu-id="9ae37-219">Yönetici olarak toorun PowerShell gerekir.</span><span class="sxs-lookup"><span data-stu-id="9ae37-219">You will need toorun PowerShell as an Administrator.</span></span>

  ```powershell
  Install-Module AzureRM

  Install-AzureRM
  ```

  <span data-ttu-id="9ae37-220">Tüm hello bilinen semantik sürüm aralığı içinde hello AzureRM.* modüllerini içeri aktarın.</span><span class="sxs-lookup"><span data-stu-id="9ae37-220">Import all of hello AzureRM.* modules within hello known semantic version range.</span></span>

  ```powershell
  Import-AzureRM
  ```

  <span data-ttu-id="9ae37-221">Ayrıca hello bilinen semantik sürüm aralığı içinde seçili bir modülü içeri aktarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9ae37-221">You can also just import a select module within hello known semantic version range.</span></span>

  ```powershell
  Import-Module AzureRM.Network
  ```

  <span data-ttu-id="9ae37-222">Tooyour hesabında oturum açın.</span><span class="sxs-lookup"><span data-stu-id="9ae37-222">Sign in tooyour account.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

  <span data-ttu-id="9ae37-223">Toocreate expressroute bağlantı hattı hello aboneliği seçin.</span><span class="sxs-lookup"><span data-stu-id="9ae37-223">Select hello subscription you want toocreate ExpressRoute circuit.</span></span>

  ```powershell
Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
  ```
2. <span data-ttu-id="9ae37-224">ExpressRoute bağlantı hattı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9ae37-224">Create an ExpressRoute circuit.</span></span>

  <span data-ttu-id="9ae37-225">Merhaba yönergeleri toocreate izleyin bir [expressroute bağlantı hattı](expressroute-howto-circuit-arm.md) ve hello bağlantı sağlayıcı tarafından sağlanan sahip.</span><span class="sxs-lookup"><span data-stu-id="9ae37-225">Follow hello instructions toocreate an [ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have it provisioned by hello connectivity provider.</span></span>

  <span data-ttu-id="9ae37-226">Bağlantı sağlayıcınız yönetilen Katman 3 Hizmetleri sunuyorsa, bağlantı sağlayıcısı tooenable Azure sizin için eşlemeyi özel isteyebilir.</span><span class="sxs-lookup"><span data-stu-id="9ae37-226">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider tooenable Azure private peering for you.</span></span> <span data-ttu-id="9ae37-227">Bu durumda, hello sonraki bölümlerde listelenen toofollow yönergeleri gerekmez.</span><span class="sxs-lookup"><span data-stu-id="9ae37-227">In that case, you won't need toofollow instructions listed in hello next sections.</span></span> <span data-ttu-id="9ae37-228">Ancak, bağlantı sağlayıcınız yönlendirmeyi sizin için hattınızı oluşturduktan sonra yönetmiyorsa yapılandırmanızı hello sonraki adımları kullanarak devam edin.</span><span class="sxs-lookup"><span data-stu-id="9ae37-228">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using hello next steps.</span></span>
3. <span data-ttu-id="9ae37-229">Merhaba ExpressRoute bağlantı hattı toomake sağlanan ve ayrıca etkin olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="9ae37-229">Check hello ExpressRoute circuit toomake sure it is provisioned and also enabled.</span></span> <span data-ttu-id="9ae37-230">Aşağıdaki örnek hello kullan:</span><span class="sxs-lookup"><span data-stu-id="9ae37-230">Use hello following example:</span></span>

  ```powershell
  Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
  ```

  <span data-ttu-id="9ae37-231">Merhaba yanıt benzer toohello örneği aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="9ae37-231">hello response is similar toohello following example:</span></span>

  ```
  Name                             : ExpressRouteARMCircuit
  ResourceGroupName                : ExpressRouteResourceGroup
  Location                         : westus
  Id                               : /subscriptions/***************************/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/ExpressRouteARMCircuit
  Etag                             : W/"################################"
  ProvisioningState                : Succeeded
  Sku                              : {
                                       "Name": "Standard_MeteredData",
                                       "Tier": "Standard",
                                       "Family": "MeteredData"
                                     }
  CircuitProvisioningState         : Enabled
  ServiceProviderProvisioningState : Provisioned
  ServiceProviderNotes             : 
  ServiceProviderProperties        : {
                                       "ServiceProviderName": "Equinix",
                                       "PeeringLocation": "Silicon Valley",
                                       "BandwidthInMbps": 200
                                     }
  ServiceKey                       : **************************************
  Peerings                         : []
  ```
4. <span data-ttu-id="9ae37-232">Microsoft Hello bağlantı hattı için eşlemesini yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="9ae37-232">Configure Microsoft peering for hello circuit.</span></span> <span data-ttu-id="9ae37-233">Devam etmeden önce bilgilerini aşağıdaki hello sahip olduğunuzdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="9ae37-233">Make sure that you have hello following information before you proceed.</span></span>

  * <span data-ttu-id="9ae37-234">Bir/30 alt ağı hello birincil bağlantı için.</span><span class="sxs-lookup"><span data-stu-id="9ae37-234">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="9ae37-235">Bu size ait ve bir RIR / IRR içinde kayıtlı bir geçerli ortak IPv4 ön eki olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="9ae37-235">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="9ae37-236">Bir/30 alt ağı hello ikincil bağlantı için.</span><span class="sxs-lookup"><span data-stu-id="9ae37-236">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="9ae37-237">Bu size ait ve bir RIR / IRR içinde kayıtlı bir geçerli ortak IPv4 ön eki olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="9ae37-237">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="9ae37-238">Geçerli bir VLAN kimliği tooestablish bu eşlemenin.</span><span class="sxs-lookup"><span data-stu-id="9ae37-238">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="9ae37-239">Hiçbir diğer eşliği emin hello devredeki aynı VLAN kimliğini kullanan hello</span><span class="sxs-lookup"><span data-stu-id="9ae37-239">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
  * <span data-ttu-id="9ae37-240">Eşleme için AS numarası.</span><span class="sxs-lookup"><span data-stu-id="9ae37-240">AS number for peering.</span></span> <span data-ttu-id="9ae37-241">2 bayt ve 4 bayt AS numaralarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9ae37-241">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="9ae37-242">Tanıtılan önekler: listesini sağlamanız gerekir tüm ön eklerin hello BGP oturumu üzerinden tooadvertise planlayın.</span><span class="sxs-lookup"><span data-stu-id="9ae37-242">Advertised prefixes: You must provide a list of all prefixes you plan tooadvertise over hello BGP session.</span></span> <span data-ttu-id="9ae37-243">Yalnızca ortak IP adresi ön ekleri kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="9ae37-243">Only public IP address prefixes are accepted.</span></span> <span data-ttu-id="9ae37-244">Toosend ön ek kümesi planlıyorsanız, virgülle ayrılmış bir liste gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9ae37-244">If you plan toosend a set of prefixes, you can send a comma-separated list.</span></span> <span data-ttu-id="9ae37-245">Bu ön eklerin bir RIR içinde kayıtlı tooyou olmalıdır / IRR.</span><span class="sxs-lookup"><span data-stu-id="9ae37-245">These prefixes must be registered tooyou in an RIR / IRR.</span></span>
  * <span data-ttu-id="9ae37-246">**İsteğe bağlı -** müşteri ASN'si: eşleme AS numarasına kayıtlı toohello olmayan önekler Tanıtıyorsanız, kayıtlı oldukları numara toowhich hello belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9ae37-246">**Optional -** Customer ASN: If you are advertising prefixes that are not registered toohello peering AS number, you can specify hello AS number toowhich they are registered.</span></span>
  * <span data-ttu-id="9ae37-247">Yönlendirme kayıt defteri adı: Merhaba RIR belirtebilirsiniz / hangi hello karşı AS numarası ve önekleri IRR kayıtlı.</span><span class="sxs-lookup"><span data-stu-id="9ae37-247">Routing Registry Name: You can specify hello RIR / IRR against which hello AS number and prefixes are registered.</span></span>
  * <span data-ttu-id="9ae37-248">**İsteğe bağlı -** toouse birini seçerseniz bir MD5 karma değeri.</span><span class="sxs-lookup"><span data-stu-id="9ae37-248">**Optional -** An MD5 hash if you choose toouse one.</span></span>

   <span data-ttu-id="9ae37-249">Aşağıdaki örnek tooconfigure hattınız için Microsoft eşlemesini hello kullan:</span><span class="sxs-lookup"><span data-stu-id="9ae37-249">Use hello following example tooconfigure Microsoft peering for your circuit:</span></span>

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt -PeeringType MicrosoftPeering -PeerASN 100 -PrimaryPeerAddressPrefix "123.0.0.0/30" -SecondaryPeerAddressPrefix "123.0.0.4/30" -VlanId 300 -MicrosoftConfigAdvertisedPublicPrefixes "123.1.0.0/24" -MicrosoftConfigCustomerAsn 23 -MicrosoftConfigRoutingRegistryName "ARIN"

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

### <a name="tooget-microsoft-peering-details"></a><span data-ttu-id="9ae37-250">tooget Microsoft eşleme ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="9ae37-250">tooget Microsoft peering details</span></span>

<span data-ttu-id="9ae37-251">Aşağıdaki örnek hello kullanarak yapılandırma ayrıntılarını alabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="9ae37-251">You can get configuration details using hello following example:</span></span>

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

Get-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt
```

### <a name="tooupdate-microsoft-peering-configuration"></a><span data-ttu-id="9ae37-252">tooupdate Microsoft eşleme yapılandırması</span><span class="sxs-lookup"><span data-stu-id="9ae37-252">tooupdate Microsoft peering configuration</span></span>

<span data-ttu-id="9ae37-253">Aşağıdaki örneğine hello kullanarak hello yapılandırmasını herhangi bir bölümünü güncelleştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="9ae37-253">You can update any part of hello configuration using hello following example:</span></span>

```powershell
Set-AzureRmExpressRouteCircuitPeeringConfig  -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt -PeeringType MicrosoftPeering -PeerASN 100 -PrimaryPeerAddressPrefix "123.0.0.0/30" -SecondaryPeerAddressPrefix "123.0.0.4/30" -VlanId 300 -MicrosoftConfigAdvertisedPublicPrefixes "124.1.0.0/24" -MicrosoftConfigCustomerAsn 23 -MicrosoftConfigRoutingRegistryName "ARIN"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="toodelete-microsoft-peering"></a><span data-ttu-id="9ae37-254">toodelete Microsoft eşlemesi</span><span class="sxs-lookup"><span data-stu-id="9ae37-254">toodelete Microsoft peering</span></span>

<span data-ttu-id="9ae37-255">Hello aşağıdaki cmdlet'i çalıştırarak eşleme yapılandırmanızı kaldırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="9ae37-255">You can remove your peering configuration by running hello following cmdlet:</span></span>

```powershell
Remove-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <a name="next-steps"></a><span data-ttu-id="9ae37-256">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9ae37-256">Next steps</span></span>

<span data-ttu-id="9ae37-257">Sonraki adım, [VNet tooan expressroute bağlantı hattı bağlantı](expressroute-howto-linkvnet-arm.md).</span><span class="sxs-lookup"><span data-stu-id="9ae37-257">Next step, [Link a VNet tooan ExpressRoute circuit](expressroute-howto-linkvnet-arm.md).</span></span>

* <span data-ttu-id="9ae37-258">ExpressRoute iş akışları hakkında daha fazla bilgi için bkz. [ExpressRoute iş akışları](expressroute-workflows.md).</span><span class="sxs-lookup"><span data-stu-id="9ae37-258">For more information about ExpressRoute workflows, see [ExpressRoute workflows](expressroute-workflows.md).</span></span>
* <span data-ttu-id="9ae37-259">Bağlantı hattı eşlemesi hakkında daha fazla bilgi için bkz. [ExpressRoute bağlantı hattı ve yönlendirme etki alanları](expressroute-circuit-peerings.md).</span><span class="sxs-lookup"><span data-stu-id="9ae37-259">For more information about circuit peering, see [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md).</span></span>
* <span data-ttu-id="9ae37-260">Sanal ağlarla çalışma hakkında daha fazla bilgi için bkz. [Sanal ağa genel bakış](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9ae37-260">For more information about working with virtual networks, see [Virtual network overview](../virtual-network/virtual-networks-overview.md).</span></span>
