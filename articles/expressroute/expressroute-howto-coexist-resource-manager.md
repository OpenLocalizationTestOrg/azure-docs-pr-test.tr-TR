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
ms.openlocfilehash: b29147a37f9a90fc80e16b350ac9b91daac1d7f2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-expressroute-and-site-to-site-coexisting-connections"></a><span data-ttu-id="b2595-103">Birlikte bulunan ExpressRoute bağlantıları ile Siteden Siteye bağlantıları yapılandırma</span><span class="sxs-lookup"><span data-stu-id="b2595-103">Configure ExpressRoute and Site-to-Site coexisting connections</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b2595-104">PowerShell - Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b2595-104">PowerShell - Resource Manager</span></span>](expressroute-howto-coexist-resource-manager.md)
> * [<span data-ttu-id="b2595-105">PowerShell - Klasik</span><span class="sxs-lookup"><span data-stu-id="b2595-105">PowerShell - Classic</span></span>](expressroute-howto-coexist-classic.md)
> 
> 

<span data-ttu-id="b2595-106">Siteden Siteye VPN ve ExpressRoute eşzamanlı bağlantılarını yapılandırmanın çeşitli avantajları vardır.</span><span class="sxs-lookup"><span data-stu-id="b2595-106">Configuring Site-to-Site VPN and ExpressRoute coexisting connections has several advantages.</span></span> <span data-ttu-id="b2595-107">ExressRoute için güvenli bir yük devretme yolu olarak Siteden Siteye VPN yapılandırabilir veya ExpressRoute aracılığıyla bağlanmayan sitelere bağlanmak için Siteden Siteye VPN’ler kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b2595-107">You can configure a Site-to-Site VPN as a secure failover path for ExressRoute, or use Site-to-Site VPNs to connect to sites that are not connected through ExpressRoute.</span></span> <span data-ttu-id="b2595-108">Bu makalede iki senaryo için de yapılandırma adımları verilmektedir.</span><span class="sxs-lookup"><span data-stu-id="b2595-108">We cover the steps to configure both scenarios in this article.</span></span> <span data-ttu-id="b2595-109">Bu makale Resource Manager dağıtım modelleri için geçerlidir ve PowerShell kullanır.</span><span class="sxs-lookup"><span data-stu-id="b2595-109">This article applies to the Resource Manager deployment model and uses PowerShell.</span></span> <span data-ttu-id="b2595-110">Bu yapılandırma Azure portalında kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="b2595-110">This configuration is not available in the Azure portal.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b2595-111">Aşağıdaki yönergeleri izlemeden önce ExpressRoute bağlantı hatlarının önceden yapılandırılmış olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="b2595-111">ExpressRoute circuits must be pre-configured before you follow the instructions below.</span></span> <span data-ttu-id="b2595-112">Devam etmeden önce [ExpressRoute bağlantı hattı oluşturma](expressroute-howto-circuit-arm.md) ve [yönlendirmeyi yapılandırma](expressroute-howto-routing-arm.md) kılavuzlarını izlediğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="b2595-112">Make sure that you have followed the guides to [create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and [configure routing](expressroute-howto-routing-arm.md) before you proceed.</span></span>
> 
> 

## <a name="limits-and-limitations"></a><span data-ttu-id="b2595-113">Sınırlar ve sınırlamalar</span><span class="sxs-lookup"><span data-stu-id="b2595-113">Limits and limitations</span></span>
* <span data-ttu-id="b2595-114">**Geçiş yönlendirmesi desteklenmez.**</span><span class="sxs-lookup"><span data-stu-id="b2595-114">**Transit routing is not supported.**</span></span> <span data-ttu-id="b2595-115">Siteden Siteye VPN aracılığıyla bağlanan yerel ağınız ve ExpressRoute aracılığıyla bağlanan yerel ağınız arasında (Azure aracılığıyla) yönlendirme yapamazsınız.</span><span class="sxs-lookup"><span data-stu-id="b2595-115">You cannot route (via Azure) between your local network connected via Site-to-Site VPN and your local network connected via ExpressRoute.</span></span>
* <span data-ttu-id="b2595-116">**Temel SKU ağ geçidi desteklenmez.**</span><span class="sxs-lookup"><span data-stu-id="b2595-116">**Basic SKU gateway is not supported.**</span></span> <span data-ttu-id="b2595-117">Hem [ExpressRoute ağ geçidi](expressroute-about-virtual-network-gateways.md) hem de [VPN ağ geçidi](../vpn-gateway/vpn-gateway-about-vpngateways.md) için Temel SKU olmayan bir ağ geçidi kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="b2595-117">You must use a non-Basic SKU gateway for both the [ExpressRoute gateway](expressroute-about-virtual-network-gateways.md) and the [VPN gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span></span>
* <span data-ttu-id="b2595-118">**Yalnızca rota tabanlı VPN ağ geçidi desteklenir.**</span><span class="sxs-lookup"><span data-stu-id="b2595-118">**Only route-based VPN gateway is supported.**</span></span> <span data-ttu-id="b2595-119">Rota tabanlı [VPN Gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md) kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="b2595-119">You must use a route-based [VPN Gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span></span>
* <span data-ttu-id="b2595-120">**VPN ağ geçidiniz için statik rota yapılandırılmalıdır.**</span><span class="sxs-lookup"><span data-stu-id="b2595-120">**Static route should be configured for your VPN gateway.**</span></span> <span data-ttu-id="b2595-121">Yerel ağınız hem ExpressRoute hem de Siteden Siteye VPN’e bağlıysa Siteden Siteye VPN bağlantısını genel İnternet’e yönlendirebilmeniz için yerel ağınızda statik bir rotanın yapılandırılmış olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="b2595-121">If your local network is connected to both ExpressRoute and a Site-to-Site VPN, you must have a static route configured in your local network to route the Site-to-Site VPN connection to the public Internet.</span></span>
* <span data-ttu-id="b2595-122">**Öncelikle ExpressRoute ağ geçidinin yapılandırılıp bir devreye bağlanması gerekir.**</span><span class="sxs-lookup"><span data-stu-id="b2595-122">**ExpressRoute gateway must be configured first and linked to a circuit.**</span></span> <span data-ttu-id="b2595-123">Siteden Siteye VPN ağ geçidini ekleyebilmek için önce ExpressRoute ağ geçidini oluşturup bir devreye bağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="b2595-123">You must create the ExpressRoute gateway first and link it to a circuit before you add the Site-to-Site VPN gateway.</span></span>

## <a name="configuration-designs"></a><span data-ttu-id="b2595-124">Yapılandırma tasarımları</span><span class="sxs-lookup"><span data-stu-id="b2595-124">Configuration designs</span></span>
### <a name="configure-a-site-to-site-vpn-as-a-failover-path-for-expressroute"></a><span data-ttu-id="b2595-125">Siteden siteye VPN’i ExpressRoute için bir yük devretme yolu olarak yapılandırma</span><span class="sxs-lookup"><span data-stu-id="b2595-125">Configure a Site-to-Site VPN as a failover path for ExpressRoute</span></span>
<span data-ttu-id="b2595-126">Siteden siteye bir VPN bağlantısını ExpressRoute için yedek olarak yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b2595-126">You can configure a Site-to-Site VPN connection as a backup for ExpressRoute.</span></span> <span data-ttu-id="b2595-127">Bu yalnızca Azure özel eşleme yoluna bağlı sanal ağlar için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="b2595-127">This applies only to virtual networks linked to the Azure private peering path.</span></span> <span data-ttu-id="b2595-128">Azure ortak ve Microsoft eşlemeleri aracılığıyla erişilebilen hizmetler için VPN tabanlı yük devretme çözümü yoktur.</span><span class="sxs-lookup"><span data-stu-id="b2595-128">There is no VPN-based failover solution for services accessible through Azure public and Microsoft peerings.</span></span> <span data-ttu-id="b2595-129">ExpressRoute bağlantı hattı her zaman birincil bağlantıdır.</span><span class="sxs-lookup"><span data-stu-id="b2595-129">The ExpressRoute circuit is always the primary link.</span></span> <span data-ttu-id="b2595-130">Veriler yalnızca ExpressRoute bağlantı hattı başarısız olursa, Siteden Siteye VPN üzerinden akar.</span><span class="sxs-lookup"><span data-stu-id="b2595-130">Data flows through the Site-to-Site VPN path only if the ExpressRoute circuit fails.</span></span>

> [!NOTE]
> <span data-ttu-id="b2595-131">Her iki yol da aynı olduğunda ExpressRoute bağlantı hattı Siteden Siteye VPN’ye tercih edilse de Azure paketin hedefine yönelik yolu seçmek için en uzun ön ek eşleşmesini kullanır.</span><span class="sxs-lookup"><span data-stu-id="b2595-131">While ExpressRoute circuit is preferred over Site-to-Site VPN when both routes are the same, Azure will use the longest prefix match to choose the route towards the packet's destination.</span></span>
> 
> 

![Bir arada var olma](media/expressroute-howto-coexist-resource-manager/scenario1.jpg)

### <a name="configure-a-site-to-site-vpn-to-connect-to-sites-not-connected-through-expressroute"></a><span data-ttu-id="b2595-133">ExpressRoute aracılığıyla bağlanılmayan sitelere bağlanmak için Siteden Siteye VPN yapılandırma</span><span class="sxs-lookup"><span data-stu-id="b2595-133">Configure a Site-to-Site VPN to connect to sites not connected through ExpressRoute</span></span>
<span data-ttu-id="b2595-134">Ağınızı bazı sitelerin Azure’a Siteden Siteye VPN üzerinden doğrudan ve bazı sitelerin ExpressRoute üzerinden bağlanması için yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b2595-134">You can configure your network where some sites connect directly to Azure over Site-to-Site VPN, and some sites connect through ExpressRoute.</span></span> 

![Bir arada var olma](media/expressroute-howto-coexist-resource-manager/scenario2.jpg)

> [!NOTE]
> <span data-ttu-id="b2595-136">Sanal ağı, geçiş yönlendiricisi olarak yapılandıramazsınız.</span><span class="sxs-lookup"><span data-stu-id="b2595-136">You cannot configure a virtual network as a transit router.</span></span>
> 
> 

## <a name="selecting-the-steps-to-use"></a><span data-ttu-id="b2595-137">Kullanılacak adımları seçme</span><span class="sxs-lookup"><span data-stu-id="b2595-137">Selecting the steps to use</span></span>
<span data-ttu-id="b2595-138">Aralarından seçim yapabileceğiniz iki farklı yordam kümesi vardır.</span><span class="sxs-lookup"><span data-stu-id="b2595-138">There are two different sets of procedures to choose from.</span></span> <span data-ttu-id="b2595-139">Seçtiğiniz yapılandırma yordamı, bağlanmak istediğiniz mevcut bir sanal ağ olup olmadığına veya yeni bir sanal ağ oluşturmak isteyip istememenize bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="b2595-139">The configuration procedure that you select depends on whether you have an existing virtual network that you want to connect to, or you want to create a new virtual network.</span></span>

* <span data-ttu-id="b2595-140">Bir VNet’im yok ve bir tane oluşturmam gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="b2595-140">I don't have a VNet and need to create one.</span></span>
  
    <span data-ttu-id="b2595-141">Zaten bir sanal ağınız yoksa, bu yordam Resource Manager dağıtım modelini kullanarak yeni bir sanal ağ oluşturmak ve yeni ExpressRoute ve Siteden Siteye VPN bağlantıları oluşturmak için size yol gösterir.</span><span class="sxs-lookup"><span data-stu-id="b2595-141">If you don’t already have a virtual network, this procedure walks you through creating a new virtual network using Resource Manager deployment model and creating new ExpressRoute and Site-to-Site VPN connections.</span></span> <span data-ttu-id="b2595-142">Sanal ağı yapılandırmak için, [Yeni bir sanal ağ ve bir arada var olabilen bağlantılar oluşturmak için](#new) bölümündeki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="b2595-142">To configure a virtual network, follow the steps in [To create a new virtual network and coexisting connections](#new).</span></span>
* <span data-ttu-id="b2595-143">Zaten bir Resource Manager dağıtım modeli VNet’im var.</span><span class="sxs-lookup"><span data-stu-id="b2595-143">I already have a Resource Manager deployment model VNet.</span></span>
  
    <span data-ttu-id="b2595-144">Mevcut bir Siteden Siteye VPN bağlantısı veya ExpressRoute bağlantısına sahip bir sanal ağınız zaten olabilir.</span><span class="sxs-lookup"><span data-stu-id="b2595-144">You may already have a virtual network in place with an existing Site-to-Site VPN connection or ExpressRoute connection.</span></span> <span data-ttu-id="b2595-145">[Zaten olan bir VNet için aynı anda mevcut bağlantılar yapılandırma](#add) bölümü, ağ geçidini silme ve ardından yeni ExpressRoute ve Siteden Siteye VPN bağlantıları oluşturma işlemi boyunca size yol gösterir.</span><span class="sxs-lookup"><span data-stu-id="b2595-145">The [To configure coexisting connections for an already existing VNet](#add) section walks you through deleting the gateway, and then creating new ExpressRoute and Site-to-Site VPN connections.</span></span> <span data-ttu-id="b2595-146">Yeni bağlantılar oluşturulurken adımların belirli bir sırayla tamamlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="b2595-146">When creating the new connections, the steps must be completed in a specific order.</span></span> <span data-ttu-id="b2595-147">Ağ geçitleriniz ve bağlantılarınızı oluşturmak için diğer makalelerdeki yönergeleri kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="b2595-147">Don't use the instructions in other articles to create your gateways and connections.</span></span>
  
    <span data-ttu-id="b2595-148">Bu yordamda, bir arada var olabilen bağlantılar oluşturmak, ağ geçidinizi silmenizi ve ardından yeni ağ geçitlerini yapılandırmanızı gerektirir.</span><span class="sxs-lookup"><span data-stu-id="b2595-148">In this procedure, creating connections that can coexist requires you to delete your gateway, and then configure new gateways.</span></span> <span data-ttu-id="b2595-149">Ağ geçidinizi ve bağlantıları silip yeniden oluştururken şirket içi ve dışı bağlantılarınız için kapalı kalma süresi yaşarsınız ancak VM’leriniz veya hizmetlerinizi yeni bir sanal ağa geçirmeniz gerekmez.</span><span class="sxs-lookup"><span data-stu-id="b2595-149">You will have downtime for your cross-premises connections while you delete and recreate your gateway and connections, but you will not need to migrate any of your VMs or services to a new virtual network.</span></span> <span data-ttu-id="b2595-150">VM'leriniz ve hizmetleriniz bunu yapmak için yapılandırılmışsa, ağ geçidi yapılandırması sırasında yük dengeleyici üzerinden iletişim kurmaya devam eder.</span><span class="sxs-lookup"><span data-stu-id="b2595-150">Your VMs and services will still be able to communicate out through the load balancer while you configure your gateway if they are configured to do so.</span></span>

## <span data-ttu-id="b2595-151"><a name="new"></a>Yeni bir sanal ağ ve bir arada var olabilen bağlantılar oluşturmak için</span><span class="sxs-lookup"><span data-stu-id="b2595-151"><a name="new"></a>To create a new virtual network and coexisting connections</span></span>
<span data-ttu-id="b2595-152">Bu yordamda, bir VNet oluşturma ve bir arada var olabilen Siteden Siteye ve ExpressRoute bağlantıları oluşturma işlemleri adım adım açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="b2595-152">This procedure walks you through creating a VNet and Site-to-Site and ExpressRoute connections that will coexist.</span></span>

1. <span data-ttu-id="b2595-153">Azure PowerShell cmdlet’lerinin en son sürümünü yükleyin.</span><span class="sxs-lookup"><span data-stu-id="b2595-153">Install the latest version of the Azure PowerShell cmdlets.</span></span> <span data-ttu-id="b2595-154">Cmdlet'leri yükleme hakkında bilgi için bkz. [Azure PowerShell'i yükleme ve yapılandırma](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b2595-154">For information about installing the cmdlets, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="b2595-155">Bu yapılandırma için kullanacağınız cmdlet'ler tanıdıklarınızdan biraz farklı olabilir.</span><span class="sxs-lookup"><span data-stu-id="b2595-155">The cmdlets that you use for this configuration may be slightly different than what you might be familiar with.</span></span> <span data-ttu-id="b2595-156">Bu yönergelerde belirtilen cmdlet'leri kullandığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="b2595-156">Be sure to use the cmdlets specified in these instructions.</span></span>
2. <span data-ttu-id="b2595-157">Hesabınızda oturum açın ve ortamı ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="b2595-157">Log in to your account and set up the environment.</span></span>

  ```powershell
  login-AzureRmAccount
  Select-AzureRmSubscription -SubscriptionName 'yoursubscription'
  $location = "Central US"
  $resgrp = New-AzureRmResourceGroup -Name "ErVpnCoex" -Location $location
  $VNetASN = 65010
  ```
3. <span data-ttu-id="b2595-158">Ağ Geçidi Alt Ağı içeren bir sanal ağ oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b2595-158">Create a virtual network including Gateway Subnet.</span></span> <span data-ttu-id="b2595-159">Sanal ağ yapılandırması hakkında daha fazla bilgi için bkz. [Azure Virtual Network yapılandırma](../virtual-network/virtual-networks-create-vnet-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="b2595-159">For more information about the virtual network configuration, see [Azure Virtual Network configuration](../virtual-network/virtual-networks-create-vnet-arm-ps.md).</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="b2595-160">Ağ Geçidi Alt Ağı /27 veya daha kısa bir ön ek (örneğin /26 veya /25) olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b2595-160">The Gateway Subnet must be /27 or a shorter prefix (such as /26 or /25).</span></span>
   > 
   > 
   
    <span data-ttu-id="b2595-161">Yeni bir VNet oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b2595-161">Create a new VNet.</span></span>

  ```powershell
  $vnet = New-AzureRmVirtualNetwork -Name "CoexVnet" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -AddressPrefix "10.200.0.0/16"
  ```
   
    <span data-ttu-id="b2595-162">Alt ağlar ekleyin.</span><span class="sxs-lookup"><span data-stu-id="b2595-162">Add subnets.</span></span>

  ```powershell
  Add-AzureRmVirtualNetworkSubnetConfig -Name "App" -VirtualNetwork $vnet -AddressPrefix "10.200.1.0/24"
  Add-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet -AddressPrefix "10.200.255.0/24"
  ```
   
    <span data-ttu-id="b2595-163">VNet yapılandırmasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="b2595-163">Save the VNet configuration.</span></span>

  ```powershell
  $vnet = Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
4. <span data-ttu-id="b2595-164"><a name="gw"></a>ExpressRoute ağ geçidi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b2595-164"><a name="gw"></a>Create an ExpressRoute gateway.</span></span> <span data-ttu-id="b2595-165">ExpressRoute ağ geçidi yapılandırması hakkında daha fazla bilgi için bkz. [ExpressRoute ağ geçidi yapılandırması](expressroute-howto-add-gateway-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="b2595-165">For more information about the ExpressRoute gateway configuration, see [ExpressRoute gateway configuration](expressroute-howto-add-gateway-resource-manager.md).</span></span> <span data-ttu-id="b2595-166">GatewaySKU değeri *Standard*, *HighPerformance* veya *UltraPerformance* olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b2595-166">The GatewaySKU must be *Standard*, *HighPerformance*, or *UltraPerformance*.</span></span>

  ```powershell
  $gwSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  $gwIP = New-AzureRmPublicIpAddress -Name "ERGatewayIP" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -AllocationMethod Dynamic
  $gwConfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name "ERGatewayIpConfig" -SubnetId $gwSubnet.Id -PublicIpAddressId $gwIP.Id
  $gw = New-AzureRmVirtualNetworkGateway -Name "ERGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -IpConfigurations $gwConfig -GatewayType "ExpressRoute" -GatewaySku Standard
  ```
5. <span data-ttu-id="b2595-167">ExpressRoute ağ geçidini ExpressRoute bağlantı hattına bağlayın.</span><span class="sxs-lookup"><span data-stu-id="b2595-167">Link the ExpressRoute gateway to the ExpressRoute circuit.</span></span> <span data-ttu-id="b2595-168">Bu adım tamamlandıktan sonra, ExpressRoute aracılığıyla şirket içi ağınız ve Azure arasında bağlantı kurulur.</span><span class="sxs-lookup"><span data-stu-id="b2595-168">After this step has been completed, the connection between your on-premises network and Azure, through ExpressRoute, is established.</span></span> <span data-ttu-id="b2595-169">Bağlantı işlemi hakkında daha fazla bilgi için bkz.[VNets’i ExpressRoute’a bağlama](expressroute-howto-linkvnet-arm.md).</span><span class="sxs-lookup"><span data-stu-id="b2595-169">For more information about the link operation, see [Link VNets to ExpressRoute](expressroute-howto-linkvnet-arm.md).</span></span>

  ```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "YourCircuit" -ResourceGroupName "YourCircuitResourceGroup"
  New-AzureRmVirtualNetworkGatewayConnection -Name "ERConnection" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -VirtualNetworkGateway1 $gw -PeerId $ckt.Id -ConnectionType ExpressRoute
  ```
6. <span data-ttu-id="b2595-170"><a name="vpngw"></a>Ardından, Siteden Siteye VPN ağ geçidinizi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b2595-170"><a name="vpngw"></a>Next, create your Site-to-Site VPN gateway.</span></span> <span data-ttu-id="b2595-171">VPN ağ geçidi yapılandırması hakkında daha fazla bilgi için bkz. [Siteden Siteye bağlantı ile VNet yapılandırma](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="b2595-171">For more information about the VPN gateway configuration, see [Configure a VNet with a Site-to-Site connection](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md).</span></span> <span data-ttu-id="b2595-172">GatewaySKU değeri *Standard*, *HighPerformance* veya *UltraPerformance* olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b2595-172">The GatewaySKU must be *Standard*, *HighPerformance*, or *UltraPerformance*.</span></span> <span data-ttu-id="b2595-173">VpnType değeri *RouteBased* olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b2595-173">The VpnType must *RouteBased*.</span></span>

  ```powershell
  $gwSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  $gwIP = New-AzureRmPublicIpAddress -Name "VPNGatewayIP" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -AllocationMethod Dynamic
  $gwConfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name "VPNGatewayIpConfig" -SubnetId $gwSubnet.Id -PublicIpAddressId $gwIP.Id
  New-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -IpConfigurations $gwConfig -GatewayType "Vpn" -VpnType "RouteBased" -GatewaySku "Standard"
  ```
   
    <span data-ttu-id="b2595-174">Azure VPN ağ geçidi, BGP yönlendirme protokolünü destekler.</span><span class="sxs-lookup"><span data-stu-id="b2595-174">Azure VPN gateway supports BGP routing protocol.</span></span> <span data-ttu-id="b2595-175">Aşağıdaki komuta -Asn anahtarını ekleyerek söz konusu Sanal Ağ için ASN (AS Numarası) belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b2595-175">You can specify ASN (AS Number) for that Virtual Network by adding the -Asn switch in the following command.</span></span> <span data-ttu-id="b2595-176">Bu parametreyi belirtmediğinizde AS numarası varsayılan olarak 65515 şeklinde ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="b2595-176">Not specifying that parameter will default to AS number 65515.</span></span>

  ```powershell
  $azureVpn = New-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -IpConfigurations $gwConfig -GatewayType "Vpn" -VpnType "RouteBased" -GatewaySku "Standard" -Asn $VNetASN
  ```
   
    <span data-ttu-id="b2595-177">BGP eşleme IP’sini ve Azure’un VPN ağ geçidi için kullandığı AS numarasını $azureVpn.BgpSettings.BgpPeeringAddress ve $azureVpn.BgpSettings.Asn’de bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b2595-177">You can find the BGP peering IP and the AS number that Azure uses for the VPN gateway in $azureVpn.BgpSettings.BgpPeeringAddress and $azureVpn.BgpSettings.Asn.</span></span> <span data-ttu-id="b2595-178">Daha fazla bilgi için bkz. Azure VPN ağ geçidi için [BGP’yi yapılandırma](../vpn-gateway/vpn-gateway-bgp-resource-manager-ps.md).</span><span class="sxs-lookup"><span data-stu-id="b2595-178">For more information, see [Configure BGP](../vpn-gateway/vpn-gateway-bgp-resource-manager-ps.md) for Azure VPN gateway.</span></span>
7. <span data-ttu-id="b2595-179">Bir yerel site VPN ağ geçidi varlığı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b2595-179">Create a local site VPN gateway entity.</span></span> <span data-ttu-id="b2595-180">Bu komut, şirket içi VPN ağ geçidinizi yapılandırmaz.</span><span class="sxs-lookup"><span data-stu-id="b2595-180">This command doesn’t configure your on-premises VPN gateway.</span></span> <span data-ttu-id="b2595-181">Azure VPN ağ geçidinin bağlanabilmesi için ortak IP ve şirket içi adres alanı gibi yerel ağ geçidi ayarlarını paylaşmanıza olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="b2595-181">Rather, it allows you to provide the local gateway settings, such as the public IP and the on-premises address space, so that the Azure VPN gateway can connect to it.</span></span>
   
    <span data-ttu-id="b2595-182">Yerel VPN cihazınız yalnızca statik yönlendirmeyi destekliyorsa statik rotaları aşağıdaki şekilde yapılandırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="b2595-182">If your local VPN device only supports static routing, you can configure the static routes in the following way:</span></span>

  ```powershell
  $MyLocalNetworkAddress = @("10.100.0.0/16","10.101.0.0/16","10.102.0.0/16")
  $localVpn = New-AzureRmLocalNetworkGateway -Name "LocalVPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -GatewayIpAddress *<Public IP>* -AddressPrefix $MyLocalNetworkAddress
  ```
   
    <span data-ttu-id="b2595-183">Yerel VPN cihazınız BGP’yi destekliyorsa ve dinamik yönlendirmeyi etkinleştirmek istiyorsanız yerel VPN cihazınızın kullandığı BGP eşleme IP’sini ve AS numarasını bilmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="b2595-183">If your local VPN device supports the BGP and you want to enable dynamic routing, you need to know the BGP peering IP and the AS number that your local VPN device uses.</span></span>

  ```powershell
  $localVPNPublicIP = "<Public IP>"
  $localBGPPeeringIP = "<Private IP for the BGP session>"
  $localBGPASN = "<ASN>"
  $localAddressPrefix = $localBGPPeeringIP + "/32"
  $localVpn = New-AzureRmLocalNetworkGateway -Name "LocalVPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -GatewayIpAddress $localVPNPublicIP -AddressPrefix $localAddressPrefix -BgpPeeringAddress $localBGPPeeringIP -Asn $localBGPASN
  ```
8. <span data-ttu-id="b2595-184">Yerel VPN cihazınızı yeni Azure VPN ağ geçidine bağlanmak için yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="b2595-184">Configure your local VPN device to connect to the new Azure VPN gateway.</span></span> <span data-ttu-id="b2595-185">VPN cihazını yapılandırma hakkında daha fazla bilgi için bkz. [VPN Cihazı Yapılandırma](../vpn-gateway/vpn-gateway-about-vpn-devices.md).</span><span class="sxs-lookup"><span data-stu-id="b2595-185">For more information about VPN device configuration, see [VPN Device Configuration](../vpn-gateway/vpn-gateway-about-vpn-devices.md).</span></span>
9. <span data-ttu-id="b2595-186">Azure’da Siteden Siteye ağ geçidini yerel ağ geçidine bağlayın.</span><span class="sxs-lookup"><span data-stu-id="b2595-186">Link the Site-to-Site VPN gateway on Azure to the local gateway.</span></span>

  ```powershell
  $azureVpn = Get-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName
  New-AzureRmVirtualNetworkGatewayConnection -Name "VPNConnection" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -VirtualNetworkGateway1 $azureVpn -LocalNetworkGateway2 $localVpn -ConnectionType IPsec -SharedKey <yourkey>
  ```

## <span data-ttu-id="b2595-187"><a name="add"></a>Zaten mevcut bir VNet için bir arada var olabilen bağlantılar yapılandırma</span><span class="sxs-lookup"><span data-stu-id="b2595-187"><a name="add"></a>To configure coexisting connections for an already existing VNet</span></span>
<span data-ttu-id="b2595-188">Zaten bir sanal ağınız varsa, ağ geçidi alt ağ boyutunu kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="b2595-188">If you have an existing virtual network, check the gateway subnet size.</span></span> <span data-ttu-id="b2595-189">Ağ geçidi alt ağı /28 veya /29 ise, önce sanal ağ geçidi silmeniz ve ağ geçidi alt ağı boyutunu artırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="b2595-189">If the gateway subnet is /28 or /29, you must first delete the virtual network gateway and increase the gateway subnet size.</span></span> <span data-ttu-id="b2595-190">Bu bölümdeki adımlar bunu nasıl yapacağınızı gösterir.</span><span class="sxs-lookup"><span data-stu-id="b2595-190">The steps in this section show you how to do that.</span></span>

<span data-ttu-id="b2595-191">Ağ geçidi alt ağı /27 veya daha büyükse ve sanal ağ ExpressRoute üzerinden bağlanıyorsa, aşağıdaki adımları atlayarak önceki bölümdeki ["6. Adım - Siteden Siteye VPN ağ geçidi oluşturma"](#vpngw) bölümüne geçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b2595-191">If the gateway subnet is /27 or larger and the virtual network is connected via ExpressRoute, you can skip the steps below and proceed to ["Step 6 - Create a Site-to-Site VPN gateway"](#vpngw) in the previous section.</span></span> 

> [!NOTE]
> <span data-ttu-id="b2595-192">Mevcut ağ geçidini sildiğinizde, bu yapılandırma üzerinde çalışırken, yerel şirket sanal ağ bağlantısını kaybeder.</span><span class="sxs-lookup"><span data-stu-id="b2595-192">When you delete the existing gateway, your local premises will lose the connection to your virtual network while you are working on this configuration.</span></span> 
> 
> 

1. <span data-ttu-id="b2595-193">Azure PowerShell cmdlet’lerinin en yeni sürümünü yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="b2595-193">You'll need to install the latest version of the Azure PowerShell cmdlets.</span></span> <span data-ttu-id="b2595-194">Cmdlet'leri yükleme hakkında daha fazla bilgi için bkz. [Azure PowerShell'i yükleme ve yapılandırma](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b2595-194">For more information about installing cmdlets, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="b2595-195">Bu yapılandırma için kullanacağınız cmdlet'ler tanıdıklarınızdan biraz farklı olabilir.</span><span class="sxs-lookup"><span data-stu-id="b2595-195">The cmdlets that you use for this configuration may be slightly different than what you might be familiar with.</span></span> <span data-ttu-id="b2595-196">Bu yönergelerde belirtilen cmdlet'leri kullandığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="b2595-196">Be sure to use the cmdlets specified in these instructions.</span></span> 
2. <span data-ttu-id="b2595-197">Mevcut ExpressRoute veya Siteden Siteye VPN ağ geçidini silin.</span><span class="sxs-lookup"><span data-stu-id="b2595-197">Delete the existing ExpressRoute or Site-to-Site VPN gateway.</span></span>

  ```powershell 
  Remove-AzureRmVirtualNetworkGateway -Name <yourgatewayname> -ResourceGroupName <yourresourcegroup>
  ```
3. <span data-ttu-id="b2595-198">Ağ Geçidi Alt Ağını silin.</span><span class="sxs-lookup"><span data-stu-id="b2595-198">Delete Gateway Subnet.</span></span>

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name <yourvnetname> -ResourceGroupName <yourresourcegroup> Remove-AzureRmVirtualNetworkSubnetConfig -Name GatewaySubnet -VirtualNetwork $vnet
  ```
4. <span data-ttu-id="b2595-199">/27 veya daha büyük bir Ağ Geçidi Alt Ağı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="b2595-199">Add a Gateway Subnet that is /27 or larger.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="b2595-200">Sanal ağınızda ağ geçidi alt ağı boyutunu artırmak için yeterli IP adresi kalmadıysa, daha fazla IP adresi alanı eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="b2595-200">If you don't have enough IP addresses left in your virtual network to increase the gateway subnet size, you need to add more IP address space.</span></span>
   > 
   > 

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name <yourvnetname> -ResourceGroupName <yourresourcegroup>
  Add-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet -AddressPrefix "10.200.255.0/24"
  ```
   
    <span data-ttu-id="b2595-201">VNet yapılandırmasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="b2595-201">Save the VNet configuration.</span></span>

  ```powershell
  $vnet = Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
5. <span data-ttu-id="b2595-202">Bu noktada, hiçbir ağ geçidi olmayan bir VNet’e sahip olursunuz.</span><span class="sxs-lookup"><span data-stu-id="b2595-202">At this point, you have a VNet with no gateways.</span></span> <span data-ttu-id="b2595-203">Yeni ağ geçitleri oluşturmak ve bağlantılarınızı tamamlamak için, önceki adım kümesinde bulabileceğiniz [4. Adım - Bir ExpressRoute ağ geçidi oluşturma](#gw) bölümüyle devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b2595-203">To create new gateways and complete your connections, you can proceed with [Step 4 - Create an ExpressRoute gateway](#gw), found in the preceding set of steps.</span></span>

## <a name="to-add-point-to-site-configuration-to-the-vpn-gateway"></a><span data-ttu-id="b2595-204">VPN ağ geçidine noktadan siteye yapılandırması eklemek için</span><span class="sxs-lookup"><span data-stu-id="b2595-204">To add point-to-site configuration to the VPN gateway</span></span>
<span data-ttu-id="b2595-205">Bir arada var olan kurulumda VPN ağ geçidinize Noktadan Siteye yapılandırması eklemek için aşağıdaki adımları izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b2595-205">You can follow the steps below to add Point-to-Site configuration to your VPN gateway in a co-existence setup.</span></span>

1. <span data-ttu-id="b2595-206">VPN İstemcisi adres havuzunu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="b2595-206">Add VPN Client address pool.</span></span>

  ```powershell
  $azureVpn = Get-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName
  Set-AzureRmVirtualNetworkGatewayVpnClientConfig -VirtualNetworkGateway $azureVpn -VpnClientAddressPool "10.251.251.0/24"
  ```
2. <span data-ttu-id="b2595-207">VPN ağ geçidiniz için VPN kök sertifikasını Azure’a yükleyin.</span><span class="sxs-lookup"><span data-stu-id="b2595-207">Upload the VPN root certificate to Azure for your VPN gateway.</span></span> <span data-ttu-id="b2595-208">Bu örnekte, kök sertifikasının aşağıdaki PowerShell cmdlet’lerinin çalıştığı yerel makinede saklandığı varsayılır.</span><span class="sxs-lookup"><span data-stu-id="b2595-208">In this example, it's assumed that the root certificate is stored in the local machine where the following PowerShell cmdlets are run.</span></span>

  ```powershell
  $p2sCertFullName = "RootErVpnCoexP2S.cer" 
  $p2sCertMatchName = "RootErVpnCoexP2S" 
  $p2sCertToUpload=get-childitem Cert:\CurrentUser\My | Where-Object {$_.Subject -match $p2sCertMatchName} 
  if ($p2sCertToUpload.count -eq 1){write-host "cert found"} else {write-host "cert not found" exit} 
  $p2sCertData = [System.Convert]::ToBase64String($p2sCertToUpload.RawData) Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $p2sCertFullName -VirtualNetworkGatewayname $azureVpn.Name -ResourceGroupName $resgrp.ResourceGroupName -PublicCertData $p2sCertData
  ```

<span data-ttu-id="b2595-209">Noktadan Siteye VPN hakkında daha fazla bilgi içini bkz. [Noktadan Siteye bağlantı yapılandırma](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="b2595-209">For more information on Point-to-Site VPN, see [Configure a Point-to-Site connection](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b2595-210">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b2595-210">Next steps</span></span>
<span data-ttu-id="b2595-211">ExpressRoute hakkında daha fazla bilgi için, bkz. [ExpressRoute SSS](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="b2595-211">For more information about ExpressRoute, see the [ExpressRoute FAQ](expressroute-faqs.md).</span></span>
