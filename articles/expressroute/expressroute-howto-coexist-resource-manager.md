---
title: "Bir arada var olabilen ExpressRoute ve Siteden Siteye VPN bağlantıları yapılandırma: Resource Manager: Azure | Microsoft Docs"
description: "Bu makalede Resource Manager modeli için bir arada var olabilen ExpressRoute ve bir Siteden Siteye VPN bağlantısını nasıl yapılandıracağınız anlatılmaktadır."
documentationcenter: na
services: expressroute
author: charwen
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: c7717b14-3da3-4a6d-b78e-a5020766bc2c
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/19/2017
ms.author: charwen,cherylmc
ms.openlocfilehash: efda9f89d95617c8c4e75af91b20631dc468d4db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-expressroute-and-site-to-site-coexisting-connections"></a><span data-ttu-id="45b3f-103">Birlikte bulunan ExpressRoute bağlantıları ile Siteden Siteye bağlantıları yapılandırma</span><span class="sxs-lookup"><span data-stu-id="45b3f-103">Configure ExpressRoute and Site-to-Site coexisting connections</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="45b3f-104">PowerShell - Resource Manager</span><span class="sxs-lookup"><span data-stu-id="45b3f-104">PowerShell - Resource Manager</span></span>](expressroute-howto-coexist-resource-manager.md)
> * [<span data-ttu-id="45b3f-105">PowerShell - Klasik</span><span class="sxs-lookup"><span data-stu-id="45b3f-105">PowerShell - Classic</span></span>](expressroute-howto-coexist-classic.md)
> 
> 

<span data-ttu-id="45b3f-106">Siteden Siteye VPN ve ExpressRoute eşzamanlı bağlantılarını yapılandırmanın çeşitli avantajları vardır.</span><span class="sxs-lookup"><span data-stu-id="45b3f-106">Configuring Site-to-Site VPN and ExpressRoute coexisting connections has several advantages.</span></span> <span data-ttu-id="45b3f-107">ExressRoute için güvenli bir yük devretme yolu olarak siteden siteye VPN yapılandırmak veya ExpressRoute aracılığıyla bağlanmayan siteden siteye VPN tooconnect toosites kullanın.</span><span class="sxs-lookup"><span data-stu-id="45b3f-107">You can configure a Site-to-Site VPN as a secure failover path for ExressRoute, or use Site-to-Site VPNs tooconnect toosites that are not connected through ExpressRoute.</span></span> <span data-ttu-id="45b3f-108">Biz bu makalede her iki senaryoyu hello adımları tooconfigure kapsar.</span><span class="sxs-lookup"><span data-stu-id="45b3f-108">We cover hello steps tooconfigure both scenarios in this article.</span></span> <span data-ttu-id="45b3f-109">Bu makalede toohello Resource Manager dağıtım modeli uygular ve PowerShell kullanır.</span><span class="sxs-lookup"><span data-stu-id="45b3f-109">This article applies toohello Resource Manager deployment model and uses PowerShell.</span></span> <span data-ttu-id="45b3f-110">Bu yapılandırma hello Azure portalında kullanılabilir değil.</span><span class="sxs-lookup"><span data-stu-id="45b3f-110">This configuration is not available in hello Azure portal.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="45b3f-111">Aşağıdaki hello yönergeleri izlemeden önce ExpressRoute bağlantı hatlarının önceden yapılandırılmış olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="45b3f-111">ExpressRoute circuits must be pre-configured before you follow hello instructions below.</span></span> <span data-ttu-id="45b3f-112">Merhaba kılavuzları çok izlediğinizden emin olun[bir expressroute bağlantı hattı oluşturma](expressroute-howto-circuit-arm.md) ve [yönlendirmeyi yapılandırma](expressroute-howto-routing-arm.md) devam etmeden önce.</span><span class="sxs-lookup"><span data-stu-id="45b3f-112">Make sure that you have followed hello guides too[create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and [configure routing](expressroute-howto-routing-arm.md) before you proceed.</span></span>
> 
> 

## <a name="limits-and-limitations"></a><span data-ttu-id="45b3f-113">Sınırlar ve sınırlamalar</span><span class="sxs-lookup"><span data-stu-id="45b3f-113">Limits and limitations</span></span>
* <span data-ttu-id="45b3f-114">**Geçiş yönlendirmesi desteklenmez.**</span><span class="sxs-lookup"><span data-stu-id="45b3f-114">**Transit routing is not supported.**</span></span> <span data-ttu-id="45b3f-115">Siteden Siteye VPN aracılığıyla bağlanan yerel ağınız ve ExpressRoute aracılığıyla bağlanan yerel ağınız arasında (Azure aracılığıyla) yönlendirme yapamazsınız.</span><span class="sxs-lookup"><span data-stu-id="45b3f-115">You cannot route (via Azure) between your local network connected via Site-to-Site VPN and your local network connected via ExpressRoute.</span></span>
* <span data-ttu-id="45b3f-116">**Temel SKU ağ geçidi desteklenmez.**</span><span class="sxs-lookup"><span data-stu-id="45b3f-116">**Basic SKU gateway is not supported.**</span></span> <span data-ttu-id="45b3f-117">Temel SKU olmayan ağ geçidi için her iki hello kullanmalısınız [ExpressRoute ağ geçidi](expressroute-about-virtual-network-gateways.md) ve hello [VPN ağ geçidi](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="45b3f-117">You must use a non-Basic SKU gateway for both hello [ExpressRoute gateway](expressroute-about-virtual-network-gateways.md) and hello [VPN gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span></span>
* <span data-ttu-id="45b3f-118">**Yalnızca rota tabanlı VPN ağ geçidi desteklenir.**</span><span class="sxs-lookup"><span data-stu-id="45b3f-118">**Only route-based VPN gateway is supported.**</span></span> <span data-ttu-id="45b3f-119">Rota tabanlı [VPN Gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md) kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="45b3f-119">You must use a route-based [VPN Gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span></span>
* <span data-ttu-id="45b3f-120">**VPN ağ geçidiniz için statik rota yapılandırılmalıdır.**</span><span class="sxs-lookup"><span data-stu-id="45b3f-120">**Static route should be configured for your VPN gateway.**</span></span> <span data-ttu-id="45b3f-121">Yerel ağınıza bağlı tooboth ExpressRoute ve bir Site siteye VPN, bir statik yol, yerel ağ tooroute hello siteden siteye VPN bağlantısı toohello yapılandırılmış olması gerekiyor, ortak Internet.</span><span class="sxs-lookup"><span data-stu-id="45b3f-121">If your local network is connected tooboth ExpressRoute and a Site-to-Site VPN, you must have a static route configured in your local network tooroute hello Site-to-Site VPN connection toohello public Internet.</span></span>
* <span data-ttu-id="45b3f-122">**ExpressRoute ağ geçidi önce yapılandırılmalıdır ve tooa hattı bağlanır.**</span><span class="sxs-lookup"><span data-stu-id="45b3f-122">**ExpressRoute gateway must be configured first and linked tooa circuit.**</span></span> <span data-ttu-id="45b3f-123">Merhaba ExpressRoute ağ geçidi ilk oluşturmak ve hello siteden siteye VPN ağ geçidi eklemeden önce tooa hattı bağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="45b3f-123">You must create hello ExpressRoute gateway first and link it tooa circuit before you add hello Site-to-Site VPN gateway.</span></span>

## <a name="configuration-designs"></a><span data-ttu-id="45b3f-124">Yapılandırma tasarımları</span><span class="sxs-lookup"><span data-stu-id="45b3f-124">Configuration designs</span></span>
### <a name="configure-a-site-to-site-vpn-as-a-failover-path-for-expressroute"></a><span data-ttu-id="45b3f-125">Siteden siteye VPN’i ExpressRoute için bir yük devretme yolu olarak yapılandırma</span><span class="sxs-lookup"><span data-stu-id="45b3f-125">Configure a Site-to-Site VPN as a failover path for ExpressRoute</span></span>
<span data-ttu-id="45b3f-126">Siteden siteye bir VPN bağlantısını ExpressRoute için yedek olarak yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="45b3f-126">You can configure a Site-to-Site VPN connection as a backup for ExpressRoute.</span></span> <span data-ttu-id="45b3f-127">Bu, yalnızca toovirtual ağlar bağlantılı toohello Azure özel eşleme yoluna geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="45b3f-127">This applies only toovirtual networks linked toohello Azure private peering path.</span></span> <span data-ttu-id="45b3f-128">Azure ortak ve Microsoft eşlemeleri aracılığıyla erişilebilen hizmetler için VPN tabanlı yük devretme çözümü yoktur.</span><span class="sxs-lookup"><span data-stu-id="45b3f-128">There is no VPN-based failover solution for services accessible through Azure public and Microsoft peerings.</span></span> <span data-ttu-id="45b3f-129">Merhaba expressroute bağlantı hattı her zaman hello birincil bağlantıdır.</span><span class="sxs-lookup"><span data-stu-id="45b3f-129">hello ExpressRoute circuit is always hello primary link.</span></span> <span data-ttu-id="45b3f-130">Yalnızca hello expressroute bağlantı hattı başarısız olursa veriler hello siteden siteye VPN yolu üzerinden akar.</span><span class="sxs-lookup"><span data-stu-id="45b3f-130">Data flows through hello Site-to-Site VPN path only if hello ExpressRoute circuit fails.</span></span>

> [!NOTE]
> <span data-ttu-id="45b3f-131">Zaman aynı olan iki yollar hello expressroute bağlantı hattı siteden siteye VPN üzerinden tercih edilen olmakla birlikte, Azure doğru hello paketin hedef hello uzun önek eşleştirme toochoose hello rota kullanır.</span><span class="sxs-lookup"><span data-stu-id="45b3f-131">While ExpressRoute circuit is preferred over Site-to-Site VPN when both routes are hello same, Azure will use hello longest prefix match toochoose hello route towards hello packet's destination.</span></span>
> 
> 

![Bir arada var olma](media/expressroute-howto-coexist-resource-manager/scenario1.jpg)

### <a name="configure-a-site-to-site-vpn-tooconnect-toosites-not-connected-through-expressroute"></a><span data-ttu-id="45b3f-133">ExpressRoute aracılığıyla bağlanılmayan bir siteden siteye VPN tooconnect toosites yapılandırın</span><span class="sxs-lookup"><span data-stu-id="45b3f-133">Configure a Site-to-Site VPN tooconnect toosites not connected through ExpressRoute</span></span>
<span data-ttu-id="45b3f-134">Burada bazı siteler tooAzure siteden siteye VPN üzerinden doğrudan bağlanın ve bazı sitelerin ExpressRoute üzerinden bağlanması ağınız yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="45b3f-134">You can configure your network where some sites connect directly tooAzure over Site-to-Site VPN, and some sites connect through ExpressRoute.</span></span> 

![Bir arada var olma](media/expressroute-howto-coexist-resource-manager/scenario2.jpg)

> [!NOTE]
> <span data-ttu-id="45b3f-136">Sanal ağı, geçiş yönlendiricisi olarak yapılandıramazsınız.</span><span class="sxs-lookup"><span data-stu-id="45b3f-136">You cannot configure a virtual network as a transit router.</span></span>
> 
> 

## <a name="selecting-hello-steps-toouse"></a><span data-ttu-id="45b3f-137">Merhaba adımları toouse seçme</span><span class="sxs-lookup"><span data-stu-id="45b3f-137">Selecting hello steps toouse</span></span>
<span data-ttu-id="45b3f-138">Yordamlar toochoose iki farklı kümesi vardır.</span><span class="sxs-lookup"><span data-stu-id="45b3f-138">There are two different sets of procedures toochoose from.</span></span> <span data-ttu-id="45b3f-139">Seçtiğiniz hello yapılandırma yordamı için tooconnect istediğiniz veya yeni bir sanal ağ toocreate istediğiniz var olan bir sanal ağ olup olmadığına bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="45b3f-139">hello configuration procedure that you select depends on whether you have an existing virtual network that you want tooconnect to, or you want toocreate a new virtual network.</span></span>

* <span data-ttu-id="45b3f-140">I yoksa bir VNet ve toocreate biri gerekir.</span><span class="sxs-lookup"><span data-stu-id="45b3f-140">I don't have a VNet and need toocreate one.</span></span>
  
    <span data-ttu-id="45b3f-141">Zaten bir sanal ağınız yoksa, bu yordam Resource Manager dağıtım modelini kullanarak yeni bir sanal ağ oluşturmak ve yeni ExpressRoute ve Siteden Siteye VPN bağlantıları oluşturmak için size yol gösterir.</span><span class="sxs-lookup"><span data-stu-id="45b3f-141">If you don’t already have a virtual network, this procedure walks you through creating a new virtual network using Resource Manager deployment model and creating new ExpressRoute and Site-to-Site VPN connections.</span></span> <span data-ttu-id="45b3f-142">tooconfigure bir sanal ağ içinde hello adımları izleyin [toocreate yeni bir sanal ağ ve bir arada var olabilen bağlantılar](#new).</span><span class="sxs-lookup"><span data-stu-id="45b3f-142">tooconfigure a virtual network, follow hello steps in [toocreate a new virtual network and coexisting connections](#new).</span></span>
* <span data-ttu-id="45b3f-143">Zaten bir Resource Manager dağıtım modeli VNet’im var.</span><span class="sxs-lookup"><span data-stu-id="45b3f-143">I already have a Resource Manager deployment model VNet.</span></span>
  
    <span data-ttu-id="45b3f-144">Mevcut bir Siteden Siteye VPN bağlantısı veya ExpressRoute bağlantısına sahip bir sanal ağınız zaten olabilir.</span><span class="sxs-lookup"><span data-stu-id="45b3f-144">You may already have a virtual network in place with an existing Site-to-Site VPN connection or ExpressRoute connection.</span></span> <span data-ttu-id="45b3f-145">Merhaba [tooconfigure arada var olabilen bağlantılar zaten olan bir VNet için](#add) bölüm hello ağ geçidini silme ve ardından yeni ExpressRoute ve siteden siteye VPN bağlantıları oluşturma size yol gösterir.</span><span class="sxs-lookup"><span data-stu-id="45b3f-145">hello [tooconfigure coexisting connections for an already existing VNet](#add) section walks you through deleting hello gateway, and then creating new ExpressRoute and Site-to-Site VPN connections.</span></span> <span data-ttu-id="45b3f-146">Merhaba adımları Hello yeni bağlantıları oluştururken, belirli bir sırada tamamlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="45b3f-146">When creating hello new connections, hello steps must be completed in a specific order.</span></span> <span data-ttu-id="45b3f-147">Diğer makaleler toocreate Hello yönergeleri, ağ geçitleri ve bağlantıları kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="45b3f-147">Don't use hello instructions in other articles toocreate your gateways and connections.</span></span>
  
    <span data-ttu-id="45b3f-148">Bu yordam, bir arada var olabilen bağlantılar oluşturmak, ağ geçidi, toodelete gerektirir ve yeni ağ geçitlerini yapılandırmak.</span><span class="sxs-lookup"><span data-stu-id="45b3f-148">In this procedure, creating connections that can coexist requires you toodelete your gateway, and then configure new gateways.</span></span> <span data-ttu-id="45b3f-149">Şirket içi bağlantılarınız için kapalı kalma süresi silin ve ağ geçidiniz ve bağlantıları oluşturun, ancak toomigrate gerekmez herhangi biri sanal makineleri veya hizmetleri tooa yeni sanal ağınız olacaktır.</span><span class="sxs-lookup"><span data-stu-id="45b3f-149">You will have downtime for your cross-premises connections while you delete and recreate your gateway and connections, but you will not need toomigrate any of your VMs or services tooa new virtual network.</span></span> <span data-ttu-id="45b3f-150">Yapılandırılmış toodo şekilde olmaları durumunda, ağ geçidi yapılandırması sırasında VM'ler ve hizmetler hello yük dengeleyici üzerinden kullanıma mümkün toocommunicate olmaya devam eder.</span><span class="sxs-lookup"><span data-stu-id="45b3f-150">Your VMs and services will still be able toocommunicate out through hello load balancer while you configure your gateway if they are configured toodo so.</span></span>

## <span data-ttu-id="45b3f-151"><a name="new"></a>toocreate yeni bir sanal ağ ve arada var olabilen bağlantılar</span><span class="sxs-lookup"><span data-stu-id="45b3f-151"><a name="new"></a>toocreate a new virtual network and coexisting connections</span></span>
<span data-ttu-id="45b3f-152">Bu yordamda, bir VNet oluşturma ve bir arada var olabilen Siteden Siteye ve ExpressRoute bağlantıları oluşturma işlemleri adım adım açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="45b3f-152">This procedure walks you through creating a VNet and Site-to-Site and ExpressRoute connections that will coexist.</span></span>

1. <span data-ttu-id="45b3f-153">Merhaba hello Azure PowerShell cmdlet'lerinin en son sürümünü yükleyin.</span><span class="sxs-lookup"><span data-stu-id="45b3f-153">Install hello latest version of hello Azure PowerShell cmdlets.</span></span> <span data-ttu-id="45b3f-154">Merhaba cmdlet'lerini yükleme hakkında daha fazla bilgi için bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="45b3f-154">For information about installing hello cmdlets, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="45b3f-155">Bu yapılandırma için kullandığınız hello cmdlet'leri ne tanımanız değerinden biraz farklı olabilir.</span><span class="sxs-lookup"><span data-stu-id="45b3f-155">hello cmdlets that you use for this configuration may be slightly different than what you might be familiar with.</span></span> <span data-ttu-id="45b3f-156">Bu yönergelerde emin toouse hello cmdlet'leri belirtilmiş.</span><span class="sxs-lookup"><span data-stu-id="45b3f-156">Be sure toouse hello cmdlets specified in these instructions.</span></span>
2. <span data-ttu-id="45b3f-157">Tooyour hesabında oturum ve hello ortamını ayarlama.</span><span class="sxs-lookup"><span data-stu-id="45b3f-157">Log in tooyour account and set up hello environment.</span></span>

  ```powershell
  login-AzureRmAccount
  Select-AzureRmSubscription -SubscriptionName 'yoursubscription'
  $location = "Central US"
  $resgrp = New-AzureRmResourceGroup -Name "ErVpnCoex" -Location $location
  $VNetASN = 65010
  ```
3. <span data-ttu-id="45b3f-158">Ağ Geçidi Alt Ağı içeren bir sanal ağ oluşturun.</span><span class="sxs-lookup"><span data-stu-id="45b3f-158">Create a virtual network including Gateway Subnet.</span></span> <span data-ttu-id="45b3f-159">Merhaba sanal ağ yapılandırması hakkında daha fazla bilgi için bkz: [Azure sanal ağ yapılandırması](../virtual-network/virtual-networks-create-vnet-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="45b3f-159">For more information about hello virtual network configuration, see [Azure Virtual Network configuration](../virtual-network/virtual-networks-create-vnet-arm-ps.md).</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="45b3f-160">Merhaba ağ geçidi alt ağı/27 veya daha kısa bir önek (örneğin, /26 veya/25) olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="45b3f-160">hello Gateway Subnet must be /27 or a shorter prefix (such as /26 or /25).</span></span>
   > 
   > 
   
    <span data-ttu-id="45b3f-161">Yeni bir VNet oluşturun.</span><span class="sxs-lookup"><span data-stu-id="45b3f-161">Create a new VNet.</span></span>

  ```powershell
  $vnet = New-AzureRmVirtualNetwork -Name "CoexVnet" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -AddressPrefix "10.200.0.0/16"
  ```
   
    <span data-ttu-id="45b3f-162">Alt ağlar ekleyin.</span><span class="sxs-lookup"><span data-stu-id="45b3f-162">Add subnets.</span></span>

  ```powershell
  Add-AzureRmVirtualNetworkSubnetConfig -Name "App" -VirtualNetwork $vnet -AddressPrefix "10.200.1.0/24"
  Add-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet -AddressPrefix "10.200.255.0/24"
  ```
   
    <span data-ttu-id="45b3f-163">Merhaba VNet yapılandırmasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="45b3f-163">Save hello VNet configuration.</span></span>

  ```powershell
  $vnet = Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
4. <span data-ttu-id="45b3f-164"><a name="gw"></a>ExpressRoute ağ geçidi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="45b3f-164"><a name="gw"></a>Create an ExpressRoute gateway.</span></span> <span data-ttu-id="45b3f-165">Merhaba ExpressRoute ağ geçidi yapılandırması hakkında daha fazla bilgi için bkz: [ExpressRoute ağ geçidi Yapılandırması](expressroute-howto-add-gateway-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="45b3f-165">For more information about hello ExpressRoute gateway configuration, see [ExpressRoute gateway configuration](expressroute-howto-add-gateway-resource-manager.md).</span></span> <span data-ttu-id="45b3f-166">Merhaba gatewaysku *standart*, *HighPerformance*, veya *UltraPerformance*.</span><span class="sxs-lookup"><span data-stu-id="45b3f-166">hello GatewaySKU must be *Standard*, *HighPerformance*, or *UltraPerformance*.</span></span>

  ```powershell
  $gwSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  $gwIP = New-AzureRmPublicIpAddress -Name "ERGatewayIP" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -AllocationMethod Dynamic
  $gwConfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name "ERGatewayIpConfig" -SubnetId $gwSubnet.Id -PublicIpAddressId $gwIP.Id
  $gw = New-AzureRmVirtualNetworkGateway -Name "ERGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -IpConfigurations $gwConfig -GatewayType "ExpressRoute" -GatewaySku Standard
  ```
5. <span data-ttu-id="45b3f-167">Merhaba ExpressRoute ağ geçidi toohello expressroute bağlantı hattı bağlayın.</span><span class="sxs-lookup"><span data-stu-id="45b3f-167">Link hello ExpressRoute gateway toohello ExpressRoute circuit.</span></span> <span data-ttu-id="45b3f-168">Bu adımı tamamladıktan sonra şirket içi ağınız ve ExpressRoute aracılığıyla Azure arasında hello bağlantı kurulur.</span><span class="sxs-lookup"><span data-stu-id="45b3f-168">After this step has been completed, hello connection between your on-premises network and Azure, through ExpressRoute, is established.</span></span> <span data-ttu-id="45b3f-169">Merhaba bağlantı işlemi hakkında daha fazla bilgi için bkz: [Vnets'i tooExpressRoute](expressroute-howto-linkvnet-arm.md).</span><span class="sxs-lookup"><span data-stu-id="45b3f-169">For more information about hello link operation, see [Link VNets tooExpressRoute](expressroute-howto-linkvnet-arm.md).</span></span>

  ```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "YourCircuit" -ResourceGroupName "YourCircuitResourceGroup"
  New-AzureRmVirtualNetworkGatewayConnection -Name "ERConnection" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -VirtualNetworkGateway1 $gw -PeerId $ckt.Id -ConnectionType ExpressRoute
  ```
6. <span data-ttu-id="45b3f-170"><a name="vpngw"></a>Ardından, Siteden Siteye VPN ağ geçidinizi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="45b3f-170"><a name="vpngw"></a>Next, create your Site-to-Site VPN gateway.</span></span> <span data-ttu-id="45b3f-171">Merhaba VPN ağ geçidi yapılandırması hakkında daha fazla bilgi için bkz: [bir VNet ile siteden siteye bağlantı yapılandırma](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="45b3f-171">For more information about hello VPN gateway configuration, see [Configure a VNet with a Site-to-Site connection](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md).</span></span> <span data-ttu-id="45b3f-172">Merhaba gatewaysku *standart*, *HighPerformance*, veya *UltraPerformance*.</span><span class="sxs-lookup"><span data-stu-id="45b3f-172">hello GatewaySKU must be *Standard*, *HighPerformance*, or *UltraPerformance*.</span></span> <span data-ttu-id="45b3f-173">Merhaba VpnType gerekir *RouteBased*.</span><span class="sxs-lookup"><span data-stu-id="45b3f-173">hello VpnType must *RouteBased*.</span></span>

  ```powershell
  $gwSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  $gwIP = New-AzureRmPublicIpAddress -Name "VPNGatewayIP" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -AllocationMethod Dynamic
  $gwConfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name "VPNGatewayIpConfig" -SubnetId $gwSubnet.Id -PublicIpAddressId $gwIP.Id
  New-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -IpConfigurations $gwConfig -GatewayType "Vpn" -VpnType "RouteBased" -GatewaySku "Standard"
  ```
   
    <span data-ttu-id="45b3f-174">Azure VPN ağ geçidi, BGP yönlendirme protokolünü destekler.</span><span class="sxs-lookup"><span data-stu-id="45b3f-174">Azure VPN gateway supports BGP routing protocol.</span></span> <span data-ttu-id="45b3f-175">Bu sanal ağ için komutu aşağıdaki hello hello - Asn anahtarını ekleyerek, ASN (AS numarası) belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="45b3f-175">You can specify ASN (AS Number) for that Virtual Network by adding hello -Asn switch in hello following command.</span></span> <span data-ttu-id="45b3f-176">Bu parametre belirtmeden varsayılan tooAS 65515 numarası.</span><span class="sxs-lookup"><span data-stu-id="45b3f-176">Not specifying that parameter will default tooAS number 65515.</span></span>

  ```powershell
  $azureVpn = New-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -IpConfigurations $gwConfig -GatewayType "Vpn" -VpnType "RouteBased" -GatewaySku "Standard" -Asn $VNetASN
  ```
   
    <span data-ttu-id="45b3f-177">BGP eşliği IP hello ve hello Azure $azureVpn.BgpSettings.BgpPeeringAddress ve $azureVpn.BgpSettings.Asn hello VPN ağ geçidi için kullandığı bir sayı olarak bulabilir.</span><span class="sxs-lookup"><span data-stu-id="45b3f-177">You can find hello BGP peering IP and hello AS number that Azure uses for hello VPN gateway in $azureVpn.BgpSettings.BgpPeeringAddress and $azureVpn.BgpSettings.Asn.</span></span> <span data-ttu-id="45b3f-178">Daha fazla bilgi için bkz. Azure VPN ağ geçidi için [BGP’yi yapılandırma](../vpn-gateway/vpn-gateway-bgp-resource-manager-ps.md).</span><span class="sxs-lookup"><span data-stu-id="45b3f-178">For more information, see [Configure BGP](../vpn-gateway/vpn-gateway-bgp-resource-manager-ps.md) for Azure VPN gateway.</span></span>
7. <span data-ttu-id="45b3f-179">Bir yerel site VPN ağ geçidi varlığı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="45b3f-179">Create a local site VPN gateway entity.</span></span> <span data-ttu-id="45b3f-180">Bu komut, şirket içi VPN ağ geçidinizi yapılandırmaz.</span><span class="sxs-lookup"><span data-stu-id="45b3f-180">This command doesn’t configure your on-premises VPN gateway.</span></span> <span data-ttu-id="45b3f-181">Bunun yerine, hello genel IP gibi tooprovide hello yerel ağ geçidi ayarları sağlar ve hello Azure VPN ağ geçidi tooit bağlanabilmesi hello şirket içi adres alanı.</span><span class="sxs-lookup"><span data-stu-id="45b3f-181">Rather, it allows you tooprovide hello local gateway settings, such as hello public IP and hello on-premises address space, so that hello Azure VPN gateway can connect tooit.</span></span>
   
    <span data-ttu-id="45b3f-182">Yerel VPN Cihazınızı yalnızca statik yönlendirmeyi destekliyorsa, aşağıdaki şekilde hello hello statik yollar yapılandırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="45b3f-182">If your local VPN device only supports static routing, you can configure hello static routes in hello following way:</span></span>

  ```powershell
  $MyLocalNetworkAddress = @("10.100.0.0/16","10.101.0.0/16","10.102.0.0/16")
  $localVpn = New-AzureRmLocalNetworkGateway -Name "LocalVPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -GatewayIpAddress *<Public IP>* -AddressPrefix $MyLocalNetworkAddress
  ```
   
    <span data-ttu-id="45b3f-183">Yerel VPN Cihazınızı hello BGP destekler ve tooenable dinamik yönlendirme istiyorsanız tooknow hello BGP gereken IP ve yerel VPN numarası gibi hello eşliği aygıt kullanır.</span><span class="sxs-lookup"><span data-stu-id="45b3f-183">If your local VPN device supports hello BGP and you want tooenable dynamic routing, you need tooknow hello BGP peering IP and hello AS number that your local VPN device uses.</span></span>

  ```powershell
  $localVPNPublicIP = "<Public IP>"
  $localBGPPeeringIP = "<Private IP for hello BGP session>"
  $localBGPASN = "<ASN>"
  $localAddressPrefix = $localBGPPeeringIP + "/32"
  $localVpn = New-AzureRmLocalNetworkGateway -Name "LocalVPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -GatewayIpAddress $localVPNPublicIP -AddressPrefix $localAddressPrefix -BgpPeeringAddress $localBGPPeeringIP -Asn $localBGPASN
  ```
8. <span data-ttu-id="45b3f-184">Yerel VPN cihaz tooconnect toohello yeni Azure VPN ağ geçidinizi yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="45b3f-184">Configure your local VPN device tooconnect toohello new Azure VPN gateway.</span></span> <span data-ttu-id="45b3f-185">VPN cihazını yapılandırma hakkında daha fazla bilgi için bkz. [VPN Cihazı Yapılandırma](../vpn-gateway/vpn-gateway-about-vpn-devices.md).</span><span class="sxs-lookup"><span data-stu-id="45b3f-185">For more information about VPN device configuration, see [VPN Device Configuration](../vpn-gateway/vpn-gateway-about-vpn-devices.md).</span></span>
9. <span data-ttu-id="45b3f-186">Bağlantı hello siteden siteye VPN ağ geçidinde Azure toohello yerel ağ geçidi.</span><span class="sxs-lookup"><span data-stu-id="45b3f-186">Link hello Site-to-Site VPN gateway on Azure toohello local gateway.</span></span>

  ```powershell
  $azureVpn = Get-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName
  New-AzureRmVirtualNetworkGatewayConnection -Name "VPNConnection" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -VirtualNetworkGateway1 $azureVpn -LocalNetworkGateway2 $localVpn -ConnectionType IPsec -SharedKey <yourkey>
  ```

## <span data-ttu-id="45b3f-187"><a name="add"></a>zaten olan bir VNet için tooconfigure arada var olabilen bağlantılar</span><span class="sxs-lookup"><span data-stu-id="45b3f-187"><a name="add"></a>tooconfigure coexisting connections for an already existing VNet</span></span>
<span data-ttu-id="45b3f-188">Varolan bir sanal ağınız varsa, hello ağ geçidi alt ağ boyutunu kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="45b3f-188">If you have an existing virtual network, check hello gateway subnet size.</span></span> <span data-ttu-id="45b3f-189">Merhaba ağ geçidi alt ağı /28 veya/29 ise, öncelikle hello sanal ağ geçidini silmek ve hello ağ geçidi alt ağ boyutunu artırın.</span><span class="sxs-lookup"><span data-stu-id="45b3f-189">If hello gateway subnet is /28 or /29, you must first delete hello virtual network gateway and increase hello gateway subnet size.</span></span> <span data-ttu-id="45b3f-190">Merhaba bu bölümdeki adımları şunları nasıl yapacağınızı toodo.</span><span class="sxs-lookup"><span data-stu-id="45b3f-190">hello steps in this section show you how toodo that.</span></span>

<span data-ttu-id="45b3f-191">Merhaba ağ geçidi alt ağı /27 ise veya daha büyük ve hello sanal ağ ExpressRoute üzerinden bağlı olduğundan, hello adımları atlayın ve çok devam["6. adım - siteden siteye VPN ağ geçidi oluşturma"](#vpngw) hello önceki bölümdeki.</span><span class="sxs-lookup"><span data-stu-id="45b3f-191">If hello gateway subnet is /27 or larger and hello virtual network is connected via ExpressRoute, you can skip hello steps below and proceed too["Step 6 - Create a Site-to-Site VPN gateway"](#vpngw) in hello previous section.</span></span> 

> [!NOTE]
> <span data-ttu-id="45b3f-192">Merhaba mevcut ağ geçidini sildiğinizde, bu yapılandırma üzerinde çalışırken, yerel şirket hello bağlantı tooyour sanal ağ kaybedersiniz.</span><span class="sxs-lookup"><span data-stu-id="45b3f-192">When you delete hello existing gateway, your local premises will lose hello connection tooyour virtual network while you are working on this configuration.</span></span> 
> 
> 

1. <span data-ttu-id="45b3f-193">Tooinstall hello en son sürümünü hello Azure PowerShell cmdlet'lerini gerekir.</span><span class="sxs-lookup"><span data-stu-id="45b3f-193">You'll need tooinstall hello latest version of hello Azure PowerShell cmdlets.</span></span> <span data-ttu-id="45b3f-194">Cmdlet'lerini yükleme hakkında daha fazla bilgi için bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="45b3f-194">For more information about installing cmdlets, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="45b3f-195">Bu yapılandırma için kullandığınız hello cmdlet'leri ne tanımanız değerinden biraz farklı olabilir.</span><span class="sxs-lookup"><span data-stu-id="45b3f-195">hello cmdlets that you use for this configuration may be slightly different than what you might be familiar with.</span></span> <span data-ttu-id="45b3f-196">Bu yönergelerde emin toouse hello cmdlet'leri belirtilmiş.</span><span class="sxs-lookup"><span data-stu-id="45b3f-196">Be sure toouse hello cmdlets specified in these instructions.</span></span> 
2. <span data-ttu-id="45b3f-197">Merhaba mevcut ExpressRoute veya siteden siteye VPN ağ geçidini silin.</span><span class="sxs-lookup"><span data-stu-id="45b3f-197">Delete hello existing ExpressRoute or Site-to-Site VPN gateway.</span></span>

  ```powershell 
  Remove-AzureRmVirtualNetworkGateway -Name <yourgatewayname> -ResourceGroupName <yourresourcegroup>
  ```
3. <span data-ttu-id="45b3f-198">Ağ Geçidi Alt Ağını silin.</span><span class="sxs-lookup"><span data-stu-id="45b3f-198">Delete Gateway Subnet.</span></span>

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name <yourvnetname> -ResourceGroupName <yourresourcegroup> Remove-AzureRmVirtualNetworkSubnetConfig -Name GatewaySubnet -VirtualNetwork $vnet
  ```
4. <span data-ttu-id="45b3f-199">/27 veya daha büyük bir Ağ Geçidi Alt Ağı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="45b3f-199">Add a Gateway Subnet that is /27 or larger.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="45b3f-200">Yeterli IP adresi, sanal ağ tooincrease hello ağ geçidi alt ağı boyutuna sahip değilseniz, daha fazla IP adresi alanı tooadd gerekir.</span><span class="sxs-lookup"><span data-stu-id="45b3f-200">If you don't have enough IP addresses left in your virtual network tooincrease hello gateway subnet size, you need tooadd more IP address space.</span></span>
   > 
   > 

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name <yourvnetname> -ResourceGroupName <yourresourcegroup>
  Add-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet -AddressPrefix "10.200.255.0/24"
  ```
   
    <span data-ttu-id="45b3f-201">Merhaba VNet yapılandırmasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="45b3f-201">Save hello VNet configuration.</span></span>

  ```powershell
  $vnet = Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
5. <span data-ttu-id="45b3f-202">Bu noktada, hiçbir ağ geçidi olmayan bir VNet’e sahip olursunuz.</span><span class="sxs-lookup"><span data-stu-id="45b3f-202">At this point, you have a VNet with no gateways.</span></span> <span data-ttu-id="45b3f-203">toocreate yeni ağ geçitleri ve bağlantılarınızı tamamlamak, devam edebilmeniz [4. adım - bir ExpressRoute ağ geçidi oluşturma](#gw), önceki adımları kümesini hello bulunan.</span><span class="sxs-lookup"><span data-stu-id="45b3f-203">toocreate new gateways and complete your connections, you can proceed with [Step 4 - Create an ExpressRoute gateway](#gw), found in hello preceding set of steps.</span></span>

## <a name="tooadd-point-to-site-configuration-toohello-vpn-gateway"></a><span data-ttu-id="45b3f-204">tooadd noktadan siteye yapılandırması toohello VPN ağ geçidi</span><span class="sxs-lookup"><span data-stu-id="45b3f-204">tooadd point-to-site configuration toohello VPN gateway</span></span>
<span data-ttu-id="45b3f-205">Bir arada var olan kurulumda tooadd noktadan siteye yapılandırması tooyour VPN ağ geçidi hello adımları izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="45b3f-205">You can follow hello steps below tooadd Point-to-Site configuration tooyour VPN gateway in a co-existence setup.</span></span>

1. <span data-ttu-id="45b3f-206">VPN İstemcisi adres havuzunu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="45b3f-206">Add VPN Client address pool.</span></span>

  ```powershell
  $azureVpn = Get-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName
  Set-AzureRmVirtualNetworkGatewayVpnClientConfig -VirtualNetworkGateway $azureVpn -VpnClientAddressPool "10.251.251.0/24"
  ```
2. <span data-ttu-id="45b3f-207">Merhaba VPN kök sertifika tooAzure VPN ağ geçidinizi için karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="45b3f-207">Upload hello VPN root certificate tooAzure for your VPN gateway.</span></span> <span data-ttu-id="45b3f-208">Bu örnekte, bu hello kök sertifikası PowerShell cmdlet'lerini aşağıdaki hello çalıştırdığı hello yerel makinede saklandığı varsayılır.</span><span class="sxs-lookup"><span data-stu-id="45b3f-208">In this example, it's assumed that hello root certificate is stored in hello local machine where hello following PowerShell cmdlets are run.</span></span>

  ```powershell
  $p2sCertFullName = "RootErVpnCoexP2S.cer" 
  $p2sCertMatchName = "RootErVpnCoexP2S" 
  $p2sCertToUpload=get-childitem Cert:\CurrentUser\My | Where-Object {$_.Subject -match $p2sCertMatchName} 
  if ($p2sCertToUpload.count -eq 1){write-host "cert found"} else {write-host "cert not found" exit} 
  $p2sCertData = [System.Convert]::ToBase64String($p2sCertToUpload.RawData) Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $p2sCertFullName -VirtualNetworkGatewayname $azureVpn.Name -ResourceGroupName $resgrp.ResourceGroupName -PublicCertData $p2sCertData
  ```

<span data-ttu-id="45b3f-209">Noktadan Siteye VPN hakkında daha fazla bilgi içini bkz. [Noktadan Siteye bağlantı yapılandırma](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="45b3f-209">For more information on Point-to-Site VPN, see [Configure a Point-to-Site connection](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="45b3f-210">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="45b3f-210">Next steps</span></span>
<span data-ttu-id="45b3f-211">ExpressRoute hakkında daha fazla bilgi için bkz: Merhaba [ExpressRoute SSS](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="45b3f-211">For more information about ExpressRoute, see hello [ExpressRoute FAQ](expressroute-faqs.md).</span></span>
