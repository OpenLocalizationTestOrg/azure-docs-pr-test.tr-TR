---
title: "Sanal ağ tooan expressroute bağlantı hattı bağlantı: CLI: Azure | Microsoft Docs"
description: "Bu belge hello Resource Manager dağıtım modeli ve CLI kullanarak (Vnet'ler) tooExpressRoute devreler nasıl toolink sanal ağları genel bir bakış sağlar."
services: expressroute
documentationcenter: na
author: cherylmc
manager: timlit
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/25/2017
ms.author: anzaman,cherylmc
ms.openlocfilehash: 1251f016d9b94d3fee81de1df164cb085cbe9d78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-virtual-network-tooan-expressroute-circuit-using-cli"></a><span data-ttu-id="f32fb-103">CLI kullanarak bir sanal ağ tooan expressroute bağlantı hattı Bağlan</span><span class="sxs-lookup"><span data-stu-id="f32fb-103">Connect a virtual network tooan ExpressRoute circuit using CLI</span></span>

<span data-ttu-id="f32fb-104">Bu makale, CLI kullanarak sanal ağlar (Vnet'ler) tooAzure ExpressRoute devreleri bağlantı yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="f32fb-104">This article helps you link virtual networks (VNets) tooAzure ExpressRoute circuits using CLI.</span></span> <span data-ttu-id="f32fb-105">Azure CLI kullanarak toolink hello sanal ağlar hello Resource Manager dağıtım modeli kullanılarak oluşturulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="f32fb-105">toolink using Azure CLI, hello virtual networks must be created using hello Resource Manager deployment model.</span></span> <span data-ttu-id="f32fb-106">Hello ya da olabilir aynı abonelik ya da başka bir abonelik parçası.</span><span class="sxs-lookup"><span data-stu-id="f32fb-106">They can either be in hello same subscription, or part of another subscription.</span></span> <span data-ttu-id="f32fb-107">VNet tooan expressroute bağlantı hattı toouse farklı yöntem tooconnect istiyorsanız, bir makale listesi aşağıdaki hello seçebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f32fb-107">If you want toouse a different method tooconnect your VNet tooan ExpressRoute circuit, you can select an article from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="f32fb-108">Azure portal</span><span class="sxs-lookup"><span data-stu-id="f32fb-108">Azure portal</span></span>](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [<span data-ttu-id="f32fb-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f32fb-109">PowerShell</span></span>](expressroute-howto-linkvnet-arm.md)
> * [<span data-ttu-id="f32fb-110">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="f32fb-110">Azure CLI</span></span>](howto-linkvnet-cli.md)
> * [<span data-ttu-id="f32fb-111">Video - Azure portalı</span><span class="sxs-lookup"><span data-stu-id="f32fb-111">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [<span data-ttu-id="f32fb-112">PowerShell (klasik)</span><span class="sxs-lookup"><span data-stu-id="f32fb-112">PowerShell (classic)</span></span>](expressroute-howto-linkvnet-classic.md)
> 

## <a name="configuration-prerequisites"></a><span data-ttu-id="f32fb-113">Yapılandırma önkoşulları</span><span class="sxs-lookup"><span data-stu-id="f32fb-113">Configuration prerequisites</span></span>

* <span data-ttu-id="f32fb-114">Merhaba komut satırı arabirimi (CLI) en son sürümünü hello gerekir.</span><span class="sxs-lookup"><span data-stu-id="f32fb-114">You need hello latest version of hello command-line interface (CLI).</span></span> <span data-ttu-id="f32fb-115">Daha fazla bilgi için bkz: [Azure CLI 2.0 yükleme](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="f32fb-115">For more information, see [Install Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span></span>
* <span data-ttu-id="f32fb-116">Tooreview hello gereksinim [Önkoşullar](expressroute-prerequisites.md), [yönlendirme gereksinimleri](expressroute-routing.md), ve [iş akışları](expressroute-workflows.md) yapılandırmaya başlamadan önce.</span><span class="sxs-lookup"><span data-stu-id="f32fb-116">You need tooreview hello [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
* <span data-ttu-id="f32fb-117">Etkin bir ExpressRoute bağlantı hattınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="f32fb-117">You must have an active ExpressRoute circuit.</span></span> 
  * <span data-ttu-id="f32fb-118">Çok olarak Hello yönergeleri[bir expressroute bağlantı hattı oluşturma](howto-circuit-cli.md) ve bağlantı sağlayıcınız tarafından etkinleştirilmiş hello hattı sahip.</span><span class="sxs-lookup"><span data-stu-id="f32fb-118">Follow hello instructions too[create an ExpressRoute circuit](howto-circuit-cli.md) and have hello circuit enabled by your connectivity provider.</span></span> 
  * <span data-ttu-id="f32fb-119">Bağlantı hattınız için yapılandırılmış Azure özel eşleme olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="f32fb-119">Ensure that you have Azure private peering configured for your circuit.</span></span> <span data-ttu-id="f32fb-120">Merhaba bkz [yönlendirmeyi yapılandırma](howto-routing-cli.md) yönlendirme yönergeleri için makalenin.</span><span class="sxs-lookup"><span data-stu-id="f32fb-120">See hello [configure routing](howto-routing-cli.md) article for routing instructions.</span></span> 
  * <span data-ttu-id="f32fb-121">Azure özel eşleme yapılandırıldığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="f32fb-121">Ensure that Azure private peering is configured.</span></span> <span data-ttu-id="f32fb-122">uçtan uca bağlantı etkinleştirebilmeniz için yukarı ağınız ve Microsoft arasında hello BGP eşliği olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="f32fb-122">hello BGP peering between your network and Microsoft must be up so that you can enable end-to-end connectivity.</span></span>
  * <span data-ttu-id="f32fb-123">Bir sanal ağ ve oluşturulan ve tam olarak sağlanan bir sanal ağ geçidi olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="f32fb-123">Ensure that you have a virtual network and a virtual network gateway created and fully provisioned.</span></span> <span data-ttu-id="f32fb-124">Çok olarak Hello yönergeleri[ExpressRoute için bir sanal ağ geçidi yapılandırma](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli).</span><span class="sxs-lookup"><span data-stu-id="f32fb-124">Follow hello instructions too[Configure a virtual network gateway for ExpressRoute](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli).</span></span> <span data-ttu-id="f32fb-125">Emin toouse olması `--gateway-type ExpressRoute`.</span><span class="sxs-lookup"><span data-stu-id="f32fb-125">Be sure toouse `--gateway-type ExpressRoute`.</span></span>

* <span data-ttu-id="f32fb-126">Too10 sanal ağlar tooa standart expressroute bağlantı hattı bağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f32fb-126">You can link up too10 virtual networks tooa standard ExpressRoute circuit.</span></span> <span data-ttu-id="f32fb-127">Tüm sanal ağları hello olmalıdır standart bir expressroute bağlantı hattını kullanırken aynı coğrafi bölge.</span><span class="sxs-lookup"><span data-stu-id="f32fb-127">All virtual networks must be in hello same geopolitical region when using a standard ExpressRoute circuit.</span></span> 

* <span data-ttu-id="f32fb-128">Hello ExpressRoute premium eklentisi etkinleştirirseniz, bir sanal ağ dışında hello coğrafi bölge hello expressroute bağlantı hattı, bağlantı ya da çok sayıda sanal ağlar tooyour expressroute bağlantı hattı bağlanın.</span><span class="sxs-lookup"><span data-stu-id="f32fb-128">If you enable hello ExpressRoute premium add-on, you can link a virtual network outside of hello geopolitical region of hello ExpressRoute circuit, or connect a larger number of virtual networks tooyour ExpressRoute circuit.</span></span> <span data-ttu-id="f32fb-129">Merhaba hello premium eklentisi hakkında daha fazla bilgi için bkz: [SSS](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="f32fb-129">For more information about hello premium add-on, see hello [FAQ](expressroute-faqs.md).</span></span>

## <a name="connect-a-virtual-network-in-hello-same-subscription-tooa-circuit"></a><span data-ttu-id="f32fb-130">Merhaba sanal bir ağa bağlan aynı abonelik tooa hattı</span><span class="sxs-lookup"><span data-stu-id="f32fb-130">Connect a virtual network in hello same subscription tooa circuit</span></span>

<span data-ttu-id="f32fb-131">Merhaba örneği kullanarak bir sanal ağ geçidi tooan expressroute bağlantı hattı bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="f32fb-131">You can connect a virtual network gateway tooan ExpressRoute circuit by using hello example.</span></span> <span data-ttu-id="f32fb-132">Bu hello sanal ağ geçidi oluşturulur ve hello komutunu çalıştırmadan önce bağlama için hazır olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="f32fb-132">Make sure that hello virtual network gateway is created and is ready for linking before you run hello command.</span></span>

```azurecli
az network vpn-connection create --name ERConnection --resource-group ExpressRouteResourceGroup --vnet-gateway1 VNet1GW --express-route-circuit2 MyCircuit
```

## <a name="connect-a-virtual-network-in-a-different-subscription-tooa-circuit"></a><span data-ttu-id="f32fb-133">Farklı bir abonelik tooa hattı sanal bir ağa bağlan</span><span class="sxs-lookup"><span data-stu-id="f32fb-133">Connect a virtual network in a different subscription tooa circuit</span></span>

<span data-ttu-id="f32fb-134">Bir expressroute bağlantı hattı birden çok abonelik paylaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f32fb-134">You can share an ExpressRoute circuit across multiple subscriptions.</span></span> <span data-ttu-id="f32fb-135">Aşağıdaki Hello şekilde birden çok abonelik arasında basit bir ExpressRoute bağlantı hatları için nasıl paylaşım works'ün şematik gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="f32fb-135">hello figure below shows a simple schematic of how sharing works for ExpressRoute circuits across multiple subscriptions.</span></span>

<span data-ttu-id="f32fb-136">Her hello küçük bulutların hello büyük bulut içinde bir kuruluş içindeki toodifferent bölümler ait kullanılan toorepresent abonelikleri içindir.</span><span class="sxs-lookup"><span data-stu-id="f32fb-136">Each of hello smaller clouds within hello large cloud is used toorepresent subscriptions that belong toodifferent departments within an organization.</span></span> <span data-ttu-id="f32fb-137">Her hello kuruluşunuz içinde hello bölümlerin kendi aboneliği kullanabilirsiniz dağıtmak için kendi hizmetlerini--ancak tek bir ExpressRoute bağlantı hattı tooconnect geri tooyour şirket içi ağ paylaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f32fb-137">Each of hello departments within hello organization can use their own subscription for deploying their services--but they can share a single ExpressRoute circuit tooconnect back tooyour on-premises network.</span></span> <span data-ttu-id="f32fb-138">Tek bir bölüm (Bu örnekte: BT) hello expressroute bağlantı hattı sahip olabilir.</span><span class="sxs-lookup"><span data-stu-id="f32fb-138">A single department (in this example: IT) can own hello ExpressRoute circuit.</span></span> <span data-ttu-id="f32fb-139">Merhaba kuruluştaki diğer abonelikler hello expressroute bağlantı hattı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f32fb-139">Other subscriptions within hello organization can use hello ExpressRoute circuit.</span></span>

> [!NOTE]
> <span data-ttu-id="f32fb-140">Bağlantı ve bant genişliği ücretleri ayrılmış hello hattı için uygulanan toohello ExpressRoute bağlantı hattı sahip olacaktır.</span><span class="sxs-lookup"><span data-stu-id="f32fb-140">Connectivity and bandwidth charges for hello dedicated circuit will be applied toohello ExpressRoute Circuit Owner.</span></span> <span data-ttu-id="f32fb-141">Tüm sanal ağları hello paylaşmak aynı bant genişliği.</span><span class="sxs-lookup"><span data-stu-id="f32fb-141">All virtual networks share hello same bandwidth.</span></span>
> 
> 

![Çapraz abonelik bağlantısı](./media/expressroute-howto-linkvnet-classic/cross-subscription.png)

### <a name="administration---circuit-owners-and-circuit-users"></a><span data-ttu-id="f32fb-143">Yönetim - hattı sahipleri ve hattı kullanıcılar</span><span class="sxs-lookup"><span data-stu-id="f32fb-143">Administration - Circuit Owners and Circuit Users</span></span>

<span data-ttu-id="f32fb-144">Merhaba 'Devre sahibinden' hello ExpressRoute bağlantı hattı kaynak yetkili bir güç kullanıcısıdır.</span><span class="sxs-lookup"><span data-stu-id="f32fb-144">hello 'Circuit Owner' is an authorized Power User of hello ExpressRoute circuit resource.</span></span> <span data-ttu-id="f32fb-145">Merhaba devre sahibinden 'hattı kullanıcılar tarafından kullanılan yetkilerini oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f32fb-145">hello Circuit Owner can create authorizations that can be redeemed by 'Circuit Users'.</span></span> <span data-ttu-id="f32fb-146">Bağlantı hattı kullanıcılardır sahipleri sanal ağ içinde olmayan ağ geçitleri, expressroute bağlantı hattı hello gibi aynı abonelik hello.</span><span class="sxs-lookup"><span data-stu-id="f32fb-146">Circuit Users are owners of virtual network gateways that are not within hello same subscription as hello ExpressRoute circuit.</span></span> <span data-ttu-id="f32fb-147">Bağlantı hattı kullanıcıların yetkilerini (sanal ağ başına bir yetkilendirme) kullanmak.</span><span class="sxs-lookup"><span data-stu-id="f32fb-147">Circuit Users can redeem authorizations (one authorization per virtual network).</span></span>

<span data-ttu-id="f32fb-148">Merhaba devre sahibinden hello güç toomodify ve revoke yetkilerini herhangi bir zamanda sahiptir.</span><span class="sxs-lookup"><span data-stu-id="f32fb-148">hello Circuit Owner has hello power toomodify and revoke authorizations at any time.</span></span> <span data-ttu-id="f32fb-149">Bir yetkilendirme iptal edildiğinde, tüm bağlantı erişimini iptal edildi hello abonelikten silinir.</span><span class="sxs-lookup"><span data-stu-id="f32fb-149">When an authorization is revoked, all link connections are deleted from hello subscription whose access was revoked.</span></span>

### <a name="circuit-owner-operations"></a><span data-ttu-id="f32fb-150">Sahip işlem hattı</span><span class="sxs-lookup"><span data-stu-id="f32fb-150">Circuit Owner operations</span></span>

<span data-ttu-id="f32fb-151">**toocreate bir yetkilendirme**</span><span class="sxs-lookup"><span data-stu-id="f32fb-151">**toocreate an authorization**</span></span>

<span data-ttu-id="f32fb-152">Merhaba devre sahibinden oluşturur olabilir bir yetkilendirme anahtarı oluşturur bir yetkilendirme kendi sanal ağ ağ geçitleri toohello expressroute bağlantı hattı kullanıcı tooconnect tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="f32fb-152">hello Circuit Owner creates an authorization, which creates an authorization key that can be used by a Circuit User tooconnect their virtual network gateways toohello ExpressRoute circuit.</span></span> <span data-ttu-id="f32fb-153">Bir yetkilendirme yalnızca bir bağlantı için geçerli değil.</span><span class="sxs-lookup"><span data-stu-id="f32fb-153">An authorization is valid for only one connection.</span></span>

<span data-ttu-id="f32fb-154">örnekte gösterildiği nasıl aşağıdaki hello toocreate bir yetkilendirme:</span><span class="sxs-lookup"><span data-stu-id="f32fb-154">hello following example shows how toocreate an authorization:</span></span>

```azurecli
az network express-route auth create --circuit-name MyCircuit -g ExpressRouteResourceGroup -n MyAuthorization
```

<span data-ttu-id="f32fb-155">Merhaba yanıt hello yetkilendirme anahtar ve durum içerir:</span><span class="sxs-lookup"><span data-stu-id="f32fb-155">hello response contains hello authorization key and status:</span></span>

```azurecli
"authorizationKey": "0a7f3020-541f-4b4b-844a-5fb43472e3d7",
"authorizationUseStatus": "Available",
"etag": "W/\"010353d4-8955-4984-807a-585c21a22ae0\"",
"id": "/subscriptions/81ab786c-56eb-4a4d-bb5f-f60329772466/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit/authorizations/MyAuthorization1",
"name": "MyAuthorization1",
"provisioningState": "Succeeded",
"resourceGroup": "ExpressRouteResourceGroup"
```

<span data-ttu-id="f32fb-156">**tooreview yetkilerini**</span><span class="sxs-lookup"><span data-stu-id="f32fb-156">**tooreview authorizations**</span></span>

<span data-ttu-id="f32fb-157">Merhaba devre sahibinden aşağıdaki örneğine hello çalıştırarak belirli bir bağlantı hattı üzerinde verilen tüm yetkilerini gözden geçirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f32fb-157">hello Circuit Owner can review all authorizations that are issued on a particular circuit by running hello following example:</span></span>

```azurecli
az network express-route auth list --circuit-name MyCircuit -g ExpressRouteResourceGroup
```

<span data-ttu-id="f32fb-158">**tooadd yetkilerini**</span><span class="sxs-lookup"><span data-stu-id="f32fb-158">**tooadd authorizations**</span></span>

<span data-ttu-id="f32fb-159">Merhaba devre sahibinden yetkilerini aşağıdaki örneğine hello kullanarak ekleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f32fb-159">hello Circuit Owner can add authorizations by using hello following example:</span></span>

```azurecli
az network express-route auth create --circuit-name MyCircuit -g ExpressRouteResourceGroup -n MyAuthorization1
```

<span data-ttu-id="f32fb-160">**toodelete yetkilerini**</span><span class="sxs-lookup"><span data-stu-id="f32fb-160">**toodelete authorizations**</span></span>

<span data-ttu-id="f32fb-161">Merhaba devre sahibinden revoke/yetkilerini toohello kullanıcı aşağıdaki örneğine hello çalıştırarak silme:</span><span class="sxs-lookup"><span data-stu-id="f32fb-161">hello Circuit Owner can revoke/delete authorizations toohello user by running hello following example:</span></span>

```azurecli
az network express-route auth delete --circuit-name MyCircuit -g ExpressRouteResourceGroup -n MyAuthorization1
```

### <a name="circuit-user-operations"></a><span data-ttu-id="f32fb-162">Bağlantı hattı kullanıcı işlemleri</span><span class="sxs-lookup"><span data-stu-id="f32fb-162">Circuit User operations</span></span>

<span data-ttu-id="f32fb-163">Merhaba hattı kullanıcı hello eş kimliği ve hello devre sahibinden yetkilendirme anahtarından gerekir.</span><span class="sxs-lookup"><span data-stu-id="f32fb-163">hello Circuit User needs hello peer ID and an authorization key from hello Circuit Owner.</span></span> <span data-ttu-id="f32fb-164">Merhaba yetkilendirme anahtarının bir GUID değeridir.</span><span class="sxs-lookup"><span data-stu-id="f32fb-164">hello authorization key is a GUID.</span></span>

```azurecli
Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
```

<span data-ttu-id="f32fb-165">**tooredeem Bağlantı Yetkilendirme**</span><span class="sxs-lookup"><span data-stu-id="f32fb-165">**tooredeem a connection authorization**</span></span>

<span data-ttu-id="f32fb-166">Merhaba hattı kullanıcı örnek tooredeem aşağıdaki hello bağlantı yetkilendirme çalıştırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f32fb-166">hello Circuit User can run hello following example tooredeem a link authorization:</span></span>

```azurecli
az network vpn-connection create --name ERConnection --resource-group ExpressRouteResourceGroup --vnet-gateway1 VNet1GW --express-route-circuit2 MyCircuit --authorization-key "^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^"
```

<span data-ttu-id="f32fb-167">**toorelease Bağlantı Yetkilendirme**</span><span class="sxs-lookup"><span data-stu-id="f32fb-167">**toorelease a connection authorization**</span></span>

<span data-ttu-id="f32fb-168">Bir yetkilendirme hello ExpressRoute bağlantı hattı toohello sanal ağ bağlantıları hello bağlantı silerek serbest bırakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f32fb-168">You can release an authorization by deleting hello connection that links hello ExpressRoute circuit toohello virtual network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f32fb-169">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f32fb-169">Next steps</span></span>

<span data-ttu-id="f32fb-170">ExpressRoute hakkında daha fazla bilgi için bkz: Merhaba [ExpressRoute SSS](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="f32fb-170">For more information about ExpressRoute, see hello [ExpressRoute FAQ](expressroute-faqs.md).</span></span>
