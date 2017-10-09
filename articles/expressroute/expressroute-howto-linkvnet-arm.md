---
title: "Sanal ağ tooan expressroute bağlantı hattı bağlantı: PowerShell: Azure | Microsoft Docs"
description: "Bu belge nasıl hello Resource Manager dağıtım modeli ve PowerShell kullanarak sanal toolink (Vnet'ler) tooExpressRoute devreler ağları genel bir bakış sağlar."
services: expressroute
documentationcenter: na
author: ganesr
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: daacb6e5-705a-456f-9a03-c4fc3f8c1f7e
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/05/2017
ms.author: ganesr
ms.openlocfilehash: e75a9f6b42fa8e1a579e4f19882ec99b277b545f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-virtual-network-tooan-expressroute-circuit"></a><span data-ttu-id="30a83-103">Sanal ağ tooan expressroute bağlantı hattı Bağlan</span><span class="sxs-lookup"><span data-stu-id="30a83-103">Connect a virtual network tooan ExpressRoute circuit</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="30a83-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="30a83-104">Azure portal</span></span>](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [<span data-ttu-id="30a83-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="30a83-105">PowerShell</span></span>](expressroute-howto-linkvnet-arm.md)
> * [<span data-ttu-id="30a83-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="30a83-106">Azure CLI</span></span>](howto-linkvnet-cli.md)
> * [<span data-ttu-id="30a83-107">Video - Azure portalı</span><span class="sxs-lookup"><span data-stu-id="30a83-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [<span data-ttu-id="30a83-108">PowerShell (klasik)</span><span class="sxs-lookup"><span data-stu-id="30a83-108">PowerShell (classic)</span></span>](expressroute-howto-linkvnet-classic.md)
>

<span data-ttu-id="30a83-109">Bu makalede, hello Resource Manager dağıtım modeli ve PowerShell kullanarak sanal ağlar (Vnet'ler) tooAzure ExpressRoute bağlantı hatları bağlama yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="30a83-109">This article helps you link virtual networks (VNets) tooAzure ExpressRoute circuits by using hello Resource Manager deployment model and PowerShell.</span></span> <span data-ttu-id="30a83-110">Sanal ağlar hello olabilir ya da aynı abonelik veya başka bir abonelik parçası.</span><span class="sxs-lookup"><span data-stu-id="30a83-110">Virtual networks can either be in hello same subscription or part of another subscription.</span></span> <span data-ttu-id="30a83-111">Bu makalede ayrıca nasıl tooupdate bir sanal ağ bağlantı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="30a83-111">This article also shows you how tooupdate a virtual network link.</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="30a83-112">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="30a83-112">Before you begin</span></span>
* <span data-ttu-id="30a83-113">Merhaba hello Azure PowerShell modüllerinin en son sürümünü yükleyin.</span><span class="sxs-lookup"><span data-stu-id="30a83-113">Install hello latest version of hello Azure PowerShell modules.</span></span> <span data-ttu-id="30a83-114">Daha fazla bilgi için bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="30a83-114">For more information, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="30a83-115">Gözden geçirme hello [Önkoşullar](expressroute-prerequisites.md), [yönlendirme gereksinimleri](expressroute-routing.md), ve [iş akışları](expressroute-workflows.md) yapılandırmaya başlamadan önce.</span><span class="sxs-lookup"><span data-stu-id="30a83-115">Review hello [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
* <span data-ttu-id="30a83-116">Etkin bir ExpressRoute bağlantı hattınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="30a83-116">You must have an active ExpressRoute circuit.</span></span> 
  * <span data-ttu-id="30a83-117">Çok olarak Hello yönergeleri[bir expressroute bağlantı hattı oluşturma](expressroute-howto-circuit-arm.md) ve bağlantı sağlayıcınız tarafından etkinleştirilmiş hello hattı sahip.</span><span class="sxs-lookup"><span data-stu-id="30a83-117">Follow hello instructions too[create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have hello circuit enabled by your connectivity provider.</span></span> 
  * <span data-ttu-id="30a83-118">Bağlantı hattınız için yapılandırılmış Azure özel eşleme olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="30a83-118">Ensure that you have Azure private peering configured for your circuit.</span></span> <span data-ttu-id="30a83-119">Merhaba bkz [yönlendirmeyi yapılandırma](expressroute-howto-routing-arm.md) yönlendirme yönergeleri için makalenin.</span><span class="sxs-lookup"><span data-stu-id="30a83-119">See hello [configure routing](expressroute-howto-routing-arm.md) article for routing instructions.</span></span> 
  * <span data-ttu-id="30a83-120">Azure özel eşleme yapılandırılır ve uçtan uca bağlantı etkinleştirebilmeniz için ağınız ve Microsoft arasında hello BGP eşliği yukarı olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="30a83-120">Ensure that Azure private peering is configured and hello BGP peering between your network and Microsoft is up so that you can enable end-to-end connectivity.</span></span>
  * <span data-ttu-id="30a83-121">Bir sanal ağ ve oluşturulan ve tam olarak sağlanan bir sanal ağ geçidi olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="30a83-121">Ensure that you have a virtual network and a virtual network gateway created and fully provisioned.</span></span> <span data-ttu-id="30a83-122">Çok olarak Hello yönergeleri[ExpressRoute için bir sanal ağ geçidi oluşturmak](expressroute-howto-add-gateway-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="30a83-122">Follow hello instructions too[create a virtual network gateway for ExpressRoute](expressroute-howto-add-gateway-resource-manager.md).</span></span> <span data-ttu-id="30a83-123">ExpressRoute için bir sanal ağ geçidi hello GatewayType 'ExpressRoute' değil VPN kullanır.</span><span class="sxs-lookup"><span data-stu-id="30a83-123">A virtual network gateway for ExpressRoute uses hello GatewayType 'ExpressRoute', not VPN.</span></span>

* <span data-ttu-id="30a83-124">Too10 sanal ağlar tooa standart expressroute bağlantı hattı bağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="30a83-124">You can link up too10 virtual networks tooa standard ExpressRoute circuit.</span></span> <span data-ttu-id="30a83-125">Tüm sanal ağları hello olmalıdır standart bir expressroute bağlantı hattını kullanırken aynı coğrafi bölge.</span><span class="sxs-lookup"><span data-stu-id="30a83-125">All virtual networks must be in hello same geopolitical region when using a standard ExpressRoute circuit.</span></span> 

* <span data-ttu-id="30a83-126">Merhaba expressroute bağlantı hattı hello jeopolitik bölge dışında sanal ağlara bağlantı veya çok sayıda sanal ağlar tooyour expressroute bağlantı hattı hello ExpressRoute premium eklentisi etkinse bağlanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="30a83-126">You can link a virtual networks outside of hello geopolitical region of hello ExpressRoute circuit, or connect a larger number of virtual networks tooyour ExpressRoute circuit if you enabled hello ExpressRoute premium add-on.</span></span> <span data-ttu-id="30a83-127">Merhaba denetleyin [SSS](expressroute-faqs.md) hello premium eklentisi hakkında daha fazla ayrıntı için.</span><span class="sxs-lookup"><span data-stu-id="30a83-127">Check hello [FAQ](expressroute-faqs.md) for more details on hello premium add-on.</span></span>


## <a name="connect-a-virtual-network-in-hello-same-subscription-tooa-circuit"></a><span data-ttu-id="30a83-128">Merhaba sanal bir ağa bağlan aynı abonelik tooa hattı</span><span class="sxs-lookup"><span data-stu-id="30a83-128">Connect a virtual network in hello same subscription tooa circuit</span></span>
<span data-ttu-id="30a83-129">Bir sanal ağ geçidi tooan expressroute bağlantı hattı cmdlet'i aşağıdaki hello kullanarak bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="30a83-129">You can connect a virtual network gateway tooan ExpressRoute circuit by using hello following cmdlet.</span></span> <span data-ttu-id="30a83-130">Bu hello sanal ağ geçidi oluşturulur ve hello cmdlet'i çalıştırmadan önce bağlama için hazır olduğundan emin olun:</span><span class="sxs-lookup"><span data-stu-id="30a83-130">Make sure that hello virtual network gateway is created and is ready for linking before you run hello cmdlet:</span></span>

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$gw = Get-AzureRmVirtualNetworkGateway -Name "ExpressRouteGw" -ResourceGroupName "MyRG"
$connection = New-AzureRmVirtualNetworkGatewayConnection -Name "ERConnection" -ResourceGroupName "MyRG" -Location "East US" -VirtualNetworkGateway1 $gw -PeerId $circuit.Id -ConnectionType ExpressRoute
```

## <a name="connect-a-virtual-network-in-a-different-subscription-tooa-circuit"></a><span data-ttu-id="30a83-131">Farklı bir abonelik tooa hattı sanal bir ağa bağlan</span><span class="sxs-lookup"><span data-stu-id="30a83-131">Connect a virtual network in a different subscription tooa circuit</span></span>
<span data-ttu-id="30a83-132">Bir expressroute bağlantı hattı birden çok abonelik paylaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="30a83-132">You can share an ExpressRoute circuit across multiple subscriptions.</span></span> <span data-ttu-id="30a83-133">Aşağıdaki şekilde hello arasında birden çok abonelik basit bir ExpressRoute bağlantı hatları için nasıl paylaşım works'ün şematik gösterir.</span><span class="sxs-lookup"><span data-stu-id="30a83-133">hello following figure shows a simple schematic of how sharing works for ExpressRoute circuits across multiple subscriptions.</span></span>

<span data-ttu-id="30a83-134">Her hello küçük bulutların hello büyük bulut içinde bir kuruluş içindeki toodifferent bölümler ait kullanılan toorepresent abonelikleri içindir.</span><span class="sxs-lookup"><span data-stu-id="30a83-134">Each of hello smaller clouds within hello large cloud is used toorepresent subscriptions that belong toodifferent departments within an organization.</span></span> <span data-ttu-id="30a83-135">Her hello kuruluşunuz içinde hello bölümlerin kendi aboneliği kullanabilirsiniz dağıtmak için kendi hizmetlerini--ancak tek bir ExpressRoute bağlantı hattı tooconnect geri tooyour şirket içi ağ paylaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="30a83-135">Each of hello departments within hello organization can use their own subscription for deploying their services--but they can share a single ExpressRoute circuit tooconnect back tooyour on-premises network.</span></span> <span data-ttu-id="30a83-136">Tek bir bölüm (Bu örnekte: BT) hello expressroute bağlantı hattı sahip olabilir.</span><span class="sxs-lookup"><span data-stu-id="30a83-136">A single department (in this example: IT) can own hello ExpressRoute circuit.</span></span> <span data-ttu-id="30a83-137">Merhaba kuruluştaki diğer abonelikler hello expressroute bağlantı hattı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="30a83-137">Other subscriptions within hello organization can use hello ExpressRoute circuit.</span></span>

> [!NOTE]
> <span data-ttu-id="30a83-138">Bağlantı ve bant genişliği ücretleri hello expressroute bağlantı hattı için uygulanan toohello abonelik sahibi olur.</span><span class="sxs-lookup"><span data-stu-id="30a83-138">Connectivity and bandwidth charges for hello ExpressRoute circuit will be applied toohello subscription owner.</span></span> <span data-ttu-id="30a83-139">Tüm sanal ağları hello paylaşmak aynı bant genişliği.</span><span class="sxs-lookup"><span data-stu-id="30a83-139">All virtual networks share hello same bandwidth.</span></span>
> 
> 

![Çapraz abonelik bağlantısı](./media/expressroute-howto-linkvnet-classic/cross-subscription.png)


### <a name="administration---circuit-owners-and-circuit-users"></a><span data-ttu-id="30a83-141">Yönetim - hattı sahipleri ve hattı kullanıcılar</span><span class="sxs-lookup"><span data-stu-id="30a83-141">Administration - circuit owners and circuit users</span></span>

<span data-ttu-id="30a83-142">Merhaba 'devre sahibinden' hello ExpressRoute bağlantı hattı kaynak yetkili bir güç kullanıcısıdır.</span><span class="sxs-lookup"><span data-stu-id="30a83-142">hello 'circuit owner' is an authorized Power User of hello ExpressRoute circuit resource.</span></span> <span data-ttu-id="30a83-143">Merhaba devre sahibinden 'hattı kullanıcılar tarafından kullanılan yetkilerini oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="30a83-143">hello circuit owner can create authorizations that can be redeemed by 'circuit users'.</span></span> <span data-ttu-id="30a83-144">Bağlantı hattı kullanıcılardır sahipleri sanal ağ içinde olmayan ağ geçitleri, expressroute bağlantı hattı hello gibi aynı abonelik hello.</span><span class="sxs-lookup"><span data-stu-id="30a83-144">Circuit users are owners of virtual network gateways that are not within hello same subscription as hello ExpressRoute circuit.</span></span> <span data-ttu-id="30a83-145">Bağlantı hattı kullanıcıların yetkilerini (sanal ağ başına bir yetkilendirme) kullanmak.</span><span class="sxs-lookup"><span data-stu-id="30a83-145">Circuit users can redeem authorizations (one authorization per virtual network).</span></span>

<span data-ttu-id="30a83-146">Merhaba devre sahibinden hello güç toomodify ve revoke yetkilerini herhangi bir zamanda sahiptir.</span><span class="sxs-lookup"><span data-stu-id="30a83-146">hello circuit owner has hello power toomodify and revoke authorizations at any time.</span></span> <span data-ttu-id="30a83-147">Bir yetkilendirme sonuçlarına tüm bağlantı erişimini iptal edildi hello abonelikten silinmesini iptal ediliyor.</span><span class="sxs-lookup"><span data-stu-id="30a83-147">Revoking an authorization results in all link connections being deleted from hello subscription whose access was revoked.</span></span>

### <a name="circuit-owner-operations"></a><span data-ttu-id="30a83-148">Bağlantı hattı sahibi işlemleri</span><span class="sxs-lookup"><span data-stu-id="30a83-148">Circuit owner operations</span></span>

<span data-ttu-id="30a83-149">**toocreate bir yetkilendirme**</span><span class="sxs-lookup"><span data-stu-id="30a83-149">**toocreate an authorization**</span></span>

<span data-ttu-id="30a83-150">Merhaba devre sahibinden bir yetkilendirme oluşturur.</span><span class="sxs-lookup"><span data-stu-id="30a83-150">hello circuit owner creates an authorization.</span></span> <span data-ttu-id="30a83-151">Bu olabilir bir yetkilendirme anahtarı hello oluşturulmasında sonuçları kendi sanal ağ ağ geçitleri toohello expressroute bağlantı hattı kullanıcı tooconnect tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="30a83-151">This results in hello creation of an authorization key that can be used by a circuit user tooconnect their virtual network gateways toohello ExpressRoute circuit.</span></span> <span data-ttu-id="30a83-152">Bir yetkilendirme yalnızca bir bağlantı için geçerli değil.</span><span class="sxs-lookup"><span data-stu-id="30a83-152">An authorization is valid for only one connection.</span></span>

<span data-ttu-id="30a83-153">cmdlet kod parçacığında gösterildiği nasıl aşağıdaki hello toocreate bir yetkilendirme:</span><span class="sxs-lookup"><span data-stu-id="30a83-153">hello following cmdlet snippet shows how toocreate an authorization:</span></span>

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
Add-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit -Name "MyAuthorization1"
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $circuit

$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$auth1 = Get-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit -Name "MyAuthorization1"
```


<span data-ttu-id="30a83-154">Merhaba yanıt toothis hello yetkilendirme anahtar ve durum içerir:</span><span class="sxs-lookup"><span data-stu-id="30a83-154">hello response toothis will contain hello authorization key and status:</span></span>

    Name                   : MyAuthorization1
    Id                     : /subscriptions/&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&/resourceGroups/ERCrossSubTestRG/providers/Microsoft.Network/expressRouteCircuits/CrossSubTest/authorizations/MyAuthorization1
    Etag                   : &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&& 
    AuthorizationKey       : ####################################
    AuthorizationUseStatus : Available
    ProvisioningState      : Succeeded



<span data-ttu-id="30a83-155">**tooreview yetkilerini**</span><span class="sxs-lookup"><span data-stu-id="30a83-155">**tooreview authorizations**</span></span>

<span data-ttu-id="30a83-156">Merhaba devre sahibinden hello aşağıdaki cmdlet'i çalıştırarak belirli bir bağlantı hattı üzerinde verilen tüm yetkilerini gözden geçirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="30a83-156">hello circuit owner can review all authorizations that are issued on a particular circuit by running hello following cmdlet:</span></span>

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$authorizations = Get-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit
```

<span data-ttu-id="30a83-157">**tooadd yetkilerini**</span><span class="sxs-lookup"><span data-stu-id="30a83-157">**tooadd authorizations**</span></span>

<span data-ttu-id="30a83-158">Merhaba devre sahibinden yetkilerini cmdlet'i aşağıdaki hello kullanarak ekleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="30a83-158">hello circuit owner can add authorizations by using hello following cmdlet:</span></span>

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
Add-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit -Name "MyAuthorization2"
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $circuit

$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$authorizations = Get-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit
```

<span data-ttu-id="30a83-159">**toodelete yetkilerini**</span><span class="sxs-lookup"><span data-stu-id="30a83-159">**toodelete authorizations**</span></span>

<span data-ttu-id="30a83-160">Merhaba devre sahibinden revoke/yetkilerini toohello kullanıcı hello aşağıdaki cmdlet'i çalıştırarak silme:</span><span class="sxs-lookup"><span data-stu-id="30a83-160">hello circuit owner can revoke/delete authorizations toohello user by running hello following cmdlet:</span></span>

```powershell
Remove-AzureRmExpressRouteCircuitAuthorization -Name "MyAuthorization2" -ExpressRouteCircuit $circuit
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $circuit
```    

### <a name="circuit-user-operations"></a><span data-ttu-id="30a83-161">Bağlantı hattı kullanıcı işlemleri</span><span class="sxs-lookup"><span data-stu-id="30a83-161">Circuit user operations</span></span>

<span data-ttu-id="30a83-162">Merhaba hattı kullanıcı hello eş kimliği ve hello devre sahibinden yetkilendirme anahtarı gerekir.</span><span class="sxs-lookup"><span data-stu-id="30a83-162">hello circuit user needs hello peer ID and an authorization key from hello circuit owner.</span></span> <span data-ttu-id="30a83-163">Merhaba yetkilendirme anahtarının bir GUID değeridir.</span><span class="sxs-lookup"><span data-stu-id="30a83-163">hello authorization key is a GUID.</span></span>

<span data-ttu-id="30a83-164">Eş Kimliği komutu aşağıdaki hello denetlenebilir:</span><span class="sxs-lookup"><span data-stu-id="30a83-164">Peer ID can be checked from hello following command:</span></span>

```powershell
Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
```

<span data-ttu-id="30a83-165">**tooredeem Bağlantı Yetkilendirme**</span><span class="sxs-lookup"><span data-stu-id="30a83-165">**tooredeem a connection authorization**</span></span>

<span data-ttu-id="30a83-166">Merhaba hattı kullanıcı cmdlet tooredeem aşağıdaki hello bağlantı yetkilendirme çalıştırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="30a83-166">hello circuit user can run hello following cmdlet tooredeem a link authorization:</span></span>

```powershell
$id = "/subscriptions/********************************/resourceGroups/ERCrossSubTestRG/providers/Microsoft.Network/expressRouteCircuits/MyCircuit"    
$gw = Get-AzureRmVirtualNetworkGateway -Name "ExpressRouteGw" -ResourceGroupName "MyRG"
$connection = New-AzureRmVirtualNetworkGatewayConnection -Name "ERConnection" -ResourceGroupName "RemoteResourceGroup" -Location "East US" -VirtualNetworkGateway1 $gw -PeerId $id -ConnectionType ExpressRoute -AuthorizationKey "^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^"
```

<span data-ttu-id="30a83-167">**toorelease Bağlantı Yetkilendirme**</span><span class="sxs-lookup"><span data-stu-id="30a83-167">**toorelease a connection authorization**</span></span>

<span data-ttu-id="30a83-168">Bir yetkilendirme hello ExpressRoute bağlantı hattı toohello sanal ağ bağlantıları hello bağlantı silerek serbest bırakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="30a83-168">You can release an authorization by deleting hello connection that links hello ExpressRoute circuit toohello virtual network.</span></span>

## <a name="modify-a-virtual-network-connection"></a><span data-ttu-id="30a83-169">Sanal ağ bağlantısı değiştirme</span><span class="sxs-lookup"><span data-stu-id="30a83-169">Modify a virtual network connection</span></span>
<span data-ttu-id="30a83-170">Belirli bir sanal ağ bağlantısı özellikleri güncelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="30a83-170">You can update certain properties of a virtual network connection.</span></span> 

<span data-ttu-id="30a83-171">**tooupdate hello bağlantı ağırlığı**</span><span class="sxs-lookup"><span data-stu-id="30a83-171">**tooupdate hello connection weight**</span></span>

<span data-ttu-id="30a83-172">Sanal ağınıza bağlı toomultiple ExpressRoute bağlantı hatları olabilir.</span><span class="sxs-lookup"><span data-stu-id="30a83-172">Your virtual network can be connected toomultiple ExpressRoute circuits.</span></span> <span data-ttu-id="30a83-173">Birden fazla expressroute bağlantı hattı aynı önek hello alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="30a83-173">You may receive hello same prefix from more than one ExpressRoute circuit.</span></span> <span data-ttu-id="30a83-174">hangi bağlantı toosend trafiği için bu önek hedefleyen toochoose değiştirebilir *RoutingWeight* bağlantısı.</span><span class="sxs-lookup"><span data-stu-id="30a83-174">toochoose which connection toosend traffic destined for this prefix, you can change *RoutingWeight* of a connection.</span></span> <span data-ttu-id="30a83-175">Trafik, yüksek hello ile Merhaba bağlantıda gönderilecek *RoutingWeight*.</span><span class="sxs-lookup"><span data-stu-id="30a83-175">Traffic will be sent on hello connection with hello highest *RoutingWeight*.</span></span>

```powershell
$connection = Get-AzureRmVirtualNetworkGatewayConnection -Name "MyVirtualNetworkConnection" -ResourceGroupName "MyRG"
$connection.RoutingWeight = 100
Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection
```

<span data-ttu-id="30a83-176">Merhaba aralığını *RoutingWeight* 0 too32000 değil.</span><span class="sxs-lookup"><span data-stu-id="30a83-176">hello range of *RoutingWeight* is 0 too32000.</span></span> <span data-ttu-id="30a83-177">Merhaba varsayılan değer 0'dır.</span><span class="sxs-lookup"><span data-stu-id="30a83-177">hello default value is 0.</span></span>

## <a name="next-steps"></a><span data-ttu-id="30a83-178">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="30a83-178">Next steps</span></span>
<span data-ttu-id="30a83-179">ExpressRoute hakkında daha fazla bilgi için bkz: Merhaba [ExpressRoute SSS](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="30a83-179">For more information about ExpressRoute, see hello [ExpressRoute FAQ](expressroute-faqs.md).</span></span>
