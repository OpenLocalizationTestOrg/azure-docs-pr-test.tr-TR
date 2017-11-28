---
title: "Zorlamalı tünel Azure siteden siteye bağlantıları için yapılandırın: Resource Manager | Microsoft Docs"
description: "Nasıl tooredirect veya 'force' tüm Internet'e bağlı trafik geri tooyour konumu şirket içi."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: cbe58db8-b598-4c9f-ac88-62c865eb8721
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: cherylmc
ms.openlocfilehash: 6bc52c04ab0749a674c9863be5e4f9a9f7c98df4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-forced-tunneling-using-hello-azure-resource-manager-deployment-model"></a><span data-ttu-id="3f8fe-103">Zorlamalı tünel kullanarak yapılandırma hello Azure Resource Manager dağıtım modeli</span><span class="sxs-lookup"><span data-stu-id="3f8fe-103">Configure forced tunneling using hello Azure Resource Manager deployment model</span></span>

<span data-ttu-id="3f8fe-104">Yeniden yönlendirme veya "tüm Internet'e bağlı trafik geri tooyour şirket içi konumu denetleme ve denetim için bir siteden siteye VPN tüneli aracılığıyla zorla" sağlar tünel zorlandı.</span><span class="sxs-lookup"><span data-stu-id="3f8fe-104">Forced tunneling lets you redirect or "force" all Internet-bound traffic back tooyour on-premises location via a Site-to-Site VPN tunnel for inspection and auditing.</span></span> <span data-ttu-id="3f8fe-105">Bu, çoğu kurumsal BT için kritik güvenlik gereksinimdir ilkeleri.</span><span class="sxs-lookup"><span data-stu-id="3f8fe-105">This is a critical security requirement for most enterprise IT policies.</span></span> <span data-ttu-id="3f8fe-106">Zorlamalı tünel olmadan, Internet'e bağlı trafik, vm'lerden Azure her zaman Azure ağ altyapısından toohello Internet hello seçeneği tooallow olmadan doğrudan çıkışı, tooinspect veya denetim hello trafiğin geçeceğini.</span><span class="sxs-lookup"><span data-stu-id="3f8fe-106">Without forced tunneling, Internet-bound traffic from your VMs in Azure always traverses from Azure network infrastructure directly out toohello Internet, without hello option tooallow you tooinspect or audit hello traffic.</span></span> <span data-ttu-id="3f8fe-107">Yetkisiz Internet erişimine olası tooinformation açığa çıkmasına veya diğer tür güvenlik ihlallerini yol açabilir.</span><span class="sxs-lookup"><span data-stu-id="3f8fe-107">Unauthorized Internet access can potentially lead tooinformation disclosure or other types of security breaches.</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)] 

<span data-ttu-id="3f8fe-108">Bu makalede zorlamalı tünel hello Resource Manager dağıtım modeli kullanılarak oluşturulan sanal ağlar için nasıl yapılandıracağınız anlatılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="3f8fe-108">This article walks you through configuring forced tunneling for virtual networks created using hello Resource Manager deployment model.</span></span> <span data-ttu-id="3f8fe-109">Zorlamalı tünel, değil hello Portalı aracılığıyla PowerShell kullanarak yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="3f8fe-109">Forced tunneling can be configured by using PowerShell, not through hello portal.</span></span> <span data-ttu-id="3f8fe-110">Zorlanan hello Klasik dağıtım modeli için tünel tooconfigure istiyorsanız, Klasik makale açılır listeden aşağıdaki hello seçin:</span><span class="sxs-lookup"><span data-stu-id="3f8fe-110">If you want tooconfigure forced tunneling for hello classic deployment model, select classic article from hello following dropdown list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="3f8fe-111">PowerShell - Klasik</span><span class="sxs-lookup"><span data-stu-id="3f8fe-111">PowerShell - Classic</span></span>](vpn-gateway-about-forced-tunneling.md)
> * [<span data-ttu-id="3f8fe-112">PowerShell - Resource Manager</span><span class="sxs-lookup"><span data-stu-id="3f8fe-112">PowerShell - Resource Manager</span></span>](vpn-gateway-forced-tunneling-rm.md)
> 
> 

## <a name="about-forced-tunneling"></a><span data-ttu-id="3f8fe-113">Zorlanan tünel hakkında</span><span class="sxs-lookup"><span data-stu-id="3f8fe-113">About forced tunneling</span></span>

<span data-ttu-id="3f8fe-114">Aşağıdaki diyagramda hello nasıl zorlamalı tünel works gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="3f8fe-114">hello following diagram illustrates how forced tunneling works.</span></span> 

![Zorlamalı Tünel Oluşturma](./media/vpn-gateway-forced-tunneling-rm/forced-tunnel.png)

<span data-ttu-id="3f8fe-116">Merhaba yukarıdaki örnekte, alt ağı değil zorlanır ön uç tünelli hello.</span><span class="sxs-lookup"><span data-stu-id="3f8fe-116">In hello example above, hello Frontend subnet is not forced tunneled.</span></span> <span data-ttu-id="3f8fe-117">Merhaba ön uç alt Hello iş yüklerini tooaccept devam et ve toocustomer isteklerini doğrudan Internet hello yanıt.</span><span class="sxs-lookup"><span data-stu-id="3f8fe-117">hello workloads in hello Frontend subnet can continue tooaccept and respond toocustomer requests from hello Internet directly.</span></span> <span data-ttu-id="3f8fe-118">Merhaba Orta katmanda ve arka uç alt zorlanır tünel.</span><span class="sxs-lookup"><span data-stu-id="3f8fe-118">hello Mid-tier and Backend subnets are forced tunneled.</span></span> <span data-ttu-id="3f8fe-119">Bu iki alt toohello Internet tüm giden bağlantılar zorlanmış ya da yeniden yönlendirilen geri tooan şirket içi site S2S VPN tünelleri hello biri aracılığıyla olacaktır.</span><span class="sxs-lookup"><span data-stu-id="3f8fe-119">Any outbound connections from these two subnets toohello Internet will be forced or redirected back tooan on-premises site via one of hello S2S VPN tunnels.</span></span>

<span data-ttu-id="3f8fe-120">Bu toorestrict sağlar ve Internet erişimi, sanal makinelerden inceleme veya çok katmanlı bir hizmet Mimarinizi gerekli tooenable devam ederken, azure'daki hizmetlere bulut.</span><span class="sxs-lookup"><span data-stu-id="3f8fe-120">This allows you toorestrict and inspect Internet access from your virtual machines or cloud services in Azure, while continuing tooenable your multi-tier service architecture required.</span></span> <span data-ttu-id="3f8fe-121">Sanal ağlarınıza hiçbir Internet'e iş yükleri varsa, zorlamalı tünel toohello tüm sanal ağların de uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3f8fe-121">If there are no Internet-facing workloads in your virtual networks, you also can apply forced tunneling toohello entire virtual networks.</span></span>

## <a name="requirements-and-considerations"></a><span data-ttu-id="3f8fe-122">Gereksinimleri ve konular</span><span class="sxs-lookup"><span data-stu-id="3f8fe-122">Requirements and considerations</span></span>

<span data-ttu-id="3f8fe-123">Zorlamalı tünel Azure'da sanal ağ kullanıcı tanımlı yollar yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="3f8fe-123">Forced tunneling in Azure is configured via virtual network user-defined routes.</span></span> <span data-ttu-id="3f8fe-124">Yeniden yönlendirme trafiği tooan site varsayılan yol toohello Azure VPN ağ geçidi olarak ifade edilir şirket içi.</span><span class="sxs-lookup"><span data-stu-id="3f8fe-124">Redirecting traffic tooan on-premises site is expressed as a Default Route toohello Azure VPN gateway.</span></span> <span data-ttu-id="3f8fe-125">Kullanıcı tanımlı Yönlendirme ve sanal ağlar hakkında daha fazla bilgi için bkz: [kullanıcı tanımlı yollar ve IP iletimini](../virtual-network/virtual-networks-udr-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3f8fe-125">For more information about user-defined routing and virtual networks, see [User-defined routes and IP forwarding](../virtual-network/virtual-networks-udr-overview.md).</span></span>

* <span data-ttu-id="3f8fe-126">Her sanal ağ alt yerleşik sistem yönlendirme tablosu vardır.</span><span class="sxs-lookup"><span data-stu-id="3f8fe-126">Each virtual network subnet has a built-in, system routing table.</span></span> <span data-ttu-id="3f8fe-127">Merhaba sistem yönlendirme tablosu aşağıdaki üç grup yolların hello sahiptir:</span><span class="sxs-lookup"><span data-stu-id="3f8fe-127">hello system routing table has hello following three groups of routes:</span></span>
  
  * <span data-ttu-id="3f8fe-128">**Yerel VNet yollar:** doğrudan toohello hedef VM'ler hello aynı sanal ağ.</span><span class="sxs-lookup"><span data-stu-id="3f8fe-128">**Local VNet routes:** Directly toohello destination VMs in hello same virtual network.</span></span>
  * <span data-ttu-id="3f8fe-129">**Şirket içi yollar:** toohello Azure VPN ağ geçidi.</span><span class="sxs-lookup"><span data-stu-id="3f8fe-129">**On-premises routes:** toohello Azure VPN gateway.</span></span>
  * <span data-ttu-id="3f8fe-130">**Varsayılan yol:** doğrudan toohello Internet.</span><span class="sxs-lookup"><span data-stu-id="3f8fe-130">**Default route:** Directly toohello Internet.</span></span> <span data-ttu-id="3f8fe-131">Merhaba önceki iki yolları tarafından kapsanmayan hedefleyen paketler toohello özel IP adresleri bırakılır.</span><span class="sxs-lookup"><span data-stu-id="3f8fe-131">Packets destined toohello private IP addresses not covered by hello previous two routes are dropped.</span></span>
* <span data-ttu-id="3f8fe-132">Bu yordam, kullanıcı tanımlı yolları (UDR) toocreate yönlendirme tablosu tooadd varsayılan bir yol kullanır ve bu alt ağlardaki tünel zorunlu tablo tooyour sanal ağ alt ağı tooenable yönlendirme hello ilişkilendirin.</span><span class="sxs-lookup"><span data-stu-id="3f8fe-132">This procedure uses user-defined routes (UDR) toocreate a routing table tooadd a default route, and then associate hello routing table tooyour VNet subnet(s) tooenable forced tunneling on those subnets.</span></span>
* <span data-ttu-id="3f8fe-133">Zorlamalı tünel rota tabanlı VPN ağ geçidi sahip bir sanal ağ ile ilişkilendirilmiş olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="3f8fe-133">Forced tunneling must be associated with a VNet that has a route-based VPN gateway.</span></span> <span data-ttu-id="3f8fe-134">Tooset "varsayılan site" Merhaba şirket içi yerel siteleri bağlı toohello sanal ağ arasında gerekir.</span><span class="sxs-lookup"><span data-stu-id="3f8fe-134">You need tooset a "default site" among hello cross-premises local sites connected toohello virtual network.</span></span> <span data-ttu-id="3f8fe-135">Ayrıca, hello VPN cihazı trafiğini Seçici 0.0.0.0/0 kullanılarak yapılandırılmalıdır şirket içi.</span><span class="sxs-lookup"><span data-stu-id="3f8fe-135">Also, hello on-premises VPN device must be configured using 0.0.0.0/0 as traffic selectors.</span></span> 
* <span data-ttu-id="3f8fe-136">Zorlanan tünel ExpressRoute bu düzenek yapılandırılmamış, ancak bunun yerine, varsayılan rota hello ExpressRoute BGP üzerinden reklam tarafından etkinleştirilmiş eşliği oturumlarını.</span><span class="sxs-lookup"><span data-stu-id="3f8fe-136">ExpressRoute forced tunneling is not configured via this mechanism, but instead, is enabled by advertising a default route via hello ExpressRoute BGP peering sessions.</span></span> <span data-ttu-id="3f8fe-137">Daha fazla bilgi için bkz: Merhaba [ExpressRoute belgeleri](https://azure.microsoft.com/documentation/services/expressroute/).</span><span class="sxs-lookup"><span data-stu-id="3f8fe-137">For more information, see hello [ExpressRoute Documentation](https://azure.microsoft.com/documentation/services/expressroute/).</span></span>

## <a name="configuration-overview"></a><span data-ttu-id="3f8fe-138">Yapılandırmasına genel bakış</span><span class="sxs-lookup"><span data-stu-id="3f8fe-138">Configuration overview</span></span>

<span data-ttu-id="3f8fe-139">Aşağıdaki yordamı hello bir kaynak grubu ve bir sanal ağ oluşturmanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="3f8fe-139">hello following procedure helps you create a resource group and a VNet.</span></span> <span data-ttu-id="3f8fe-140">Sonra bir VPN ağ geçidi oluşturabilir ve zorlamalı tüneli yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="3f8fe-140">You'll then create a VPN gateway and configure forced tunneling.</span></span> <span data-ttu-id="3f8fe-141">Bu yordamda hello sanal ağ 'MultiTier-VNet' üç alt ağa sahip değil: 'Ön uç', 'Midtier' ve 'Backend' dört ile şirket içi bağlantılar: 'DefaultSiteHQ' ve üç dalları.</span><span class="sxs-lookup"><span data-stu-id="3f8fe-141">In this procedure, hello virtual network 'MultiTier-VNet' has three subnets: 'Frontend', 'Midtier', and 'Backend', with four cross-premises connections: 'DefaultSiteHQ', and three Branches.</span></span>

<span data-ttu-id="3f8fe-142">Merhaba varsayılan site bağlantısı için zorlanan tünel ve hello 'Midtier' ve 'Backend' alt ağlar toouse zorlanan tünel yapılandırırken hello 'DefaultSiteHQ' hello yordam adımları ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="3f8fe-142">hello procedure steps set hello 'DefaultSiteHQ' as hello default site connection for forced tunneling, and configure hello 'Midtier' and 'Backend' subnets toouse forced tunneling.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="3f8fe-143">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="3f8fe-143">Before you begin</span></span>

<span data-ttu-id="3f8fe-144">Merhaba hello Azure Resource Manager PowerShell cmdlet'lerinin en son sürümünü yükleyin.</span><span class="sxs-lookup"><span data-stu-id="3f8fe-144">Install hello latest version of hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="3f8fe-145">Bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview) hello PowerShell cmdlet'lerini yükleme hakkında daha fazla bilgi.</span><span class="sxs-lookup"><span data-stu-id="3f8fe-145">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for more information about installing hello PowerShell cmdlets.</span></span>

### <a name="toolog-in"></a><span data-ttu-id="3f8fe-146">içinde toolog</span><span class="sxs-lookup"><span data-stu-id="3f8fe-146">toolog in</span></span>

[!INCLUDE [toolog in](../../includes/vpn-gateway-ps-login-include.md)]

## <a name="configure-forced-tunneling"></a><span data-ttu-id="3f8fe-147">Zorlamalı tünel yapılandırma</span><span class="sxs-lookup"><span data-stu-id="3f8fe-147">Configure forced tunneling</span></span>

1. <span data-ttu-id="3f8fe-148">Bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="3f8fe-148">Create a resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name 'ForcedTunneling' -Location 'North Europe'
  ```
2. <span data-ttu-id="3f8fe-149">Bir sanal ağ oluşturun ve alt ağları belirtin.</span><span class="sxs-lookup"><span data-stu-id="3f8fe-149">Create a virtual network and specify subnets.</span></span>

  ```powershell 
  $s1 = New-AzureRmVirtualNetworkSubnetConfig -Name "Frontend" -AddressPrefix "10.1.0.0/24"
  $s2 = New-AzureRmVirtualNetworkSubnetConfig -Name "Midtier" -AddressPrefix "10.1.1.0/24"
  $s3 = New-AzureRmVirtualNetworkSubnetConfig -Name "Backend" -AddressPrefix "10.1.2.0/24"
  $s4 = New-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix "10.1.200.0/28"
  $vnet = New-AzureRmVirtualNetwork -Name "MultiTier-VNet" -Location "North Europe" -ResourceGroupName "ForcedTunneling" -AddressPrefix "10.1.0.0/16" -Subnet $s1,$s2,$s3,$s4
  ```
3. <span data-ttu-id="3f8fe-150">Merhaba, yerel ağ geçitleri oluşturun.</span><span class="sxs-lookup"><span data-stu-id="3f8fe-150">Create hello local network gateways.</span></span>

  ```powershell
  $lng1 = New-AzureRmLocalNetworkGateway -Name "DefaultSiteHQ" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.111" -AddressPrefix "192.168.1.0/24"
  $lng2 = New-AzureRmLocalNetworkGateway -Name "Branch1" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.112" -AddressPrefix "192.168.2.0/24"
  $lng3 = New-AzureRmLocalNetworkGateway -Name "Branch2" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.113" -AddressPrefix "192.168.3.0/24"
  $lng4 = New-AzureRmLocalNetworkGateway -Name "Branch3" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.114" -AddressPrefix "192.168.4.0/24"
  ```
4. <span data-ttu-id="3f8fe-151">Merhaba rota tablosu ve yol kuralı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="3f8fe-151">Create hello route table and route rule.</span></span>

  ```powershell
  New-AzureRmRouteTable –Name "MyRouteTable" -ResourceGroupName "ForcedTunneling" –Location "North Europe"
  $rt = Get-AzureRmRouteTable –Name "MyRouteTable" -ResourceGroupName "ForcedTunneling" 
  Add-AzureRmRouteConfig -Name "DefaultRoute" -AddressPrefix "0.0.0.0/0" -NextHopType VirtualNetworkGateway -RouteTable $rt
  Set-AzureRmRouteTable -RouteTable $rt
  ```
5. <span data-ttu-id="3f8fe-152">Merhaba rota tablosu toohello Midtier ve arka uç alt ağları ilişkilendirin.</span><span class="sxs-lookup"><span data-stu-id="3f8fe-152">Associate hello route table toohello Midtier and Backend subnets.</span></span>

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name "MultiTier-Vnet" -ResourceGroupName "ForcedTunneling"
  Set-AzureRmVirtualNetworkSubnetConfig -Name "MidTier" -VirtualNetwork $vnet -AddressPrefix "10.1.1.0/24" -RouteTable $rt
  Set-AzureRmVirtualNetworkSubnetConfig -Name "Backend" -VirtualNetwork $vnet -AddressPrefix "10.1.2.0/24" -RouteTable $rt
  Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
6. <span data-ttu-id="3f8fe-153">Merhaba ağ geçidi ile bir varsayılan sitesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="3f8fe-153">Create hello Gateway with a default site.</span></span> <span data-ttu-id="3f8fe-154">Oluşturma ve hello ağ geçidi yapılandırma olduğundan bu adımı bazı zaman toocomplete, bazen 45 dakika veya daha fazla sürer.</span><span class="sxs-lookup"><span data-stu-id="3f8fe-154">This step takes some time toocomplete, sometimes 45 minutes or more, because you are creating and configuring hello gateway.</span></span><br> <span data-ttu-id="3f8fe-155">Merhaba **- GatewayDefaultSite** olan hello zorunlu yönlendirme yapılandırması toowork verir cmdlet parametresi Merhaba, bu nedenle bu ayarı düzgün dikkatli tooconfigure alın.</span><span class="sxs-lookup"><span data-stu-id="3f8fe-155">hello **-GatewayDefaultSite** is hello cmdlet parameter that allows hello forced routing configuration toowork, so take care tooconfigure this setting properly.</span></span> <span data-ttu-id="3f8fe-156">Bu parametre, PowerShell 1.0 veya sonraki kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="3f8fe-156">This parameter is available in PowerShell 1.0 or later.</span></span>

  ```powershell
  $pip = New-AzureRmPublicIpAddress -Name "GatewayIP" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -AllocationMethod Dynamic
  $gwsubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  $ipconfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name "gwIpConfig" -SubnetId $gwsubnet.Id -PublicIpAddressId $pip.Id
  New-AzureRmVirtualNetworkGateway -Name "Gateway1" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -IpConfigurations $ipconfig -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1 -GatewayDefaultSite $lng1 -EnableBgp $false
  ```
7. <span data-ttu-id="3f8fe-157">Merhaba siteden siteye VPN bağlantıları kurun.</span><span class="sxs-lookup"><span data-stu-id="3f8fe-157">Establish hello Site-to-Site VPN connections.</span></span>

  ```powershell
  $gateway = Get-AzureRmVirtualNetworkGateway -Name "Gateway1" -ResourceGroupName "ForcedTunneling"
  $lng1 = Get-AzureRmLocalNetworkGateway -Name "DefaultSiteHQ" -ResourceGroupName "ForcedTunneling" 
  $lng2 = Get-AzureRmLocalNetworkGateway -Name "Branch1" -ResourceGroupName "ForcedTunneling" 
  $lng3 = Get-AzureRmLocalNetworkGateway -Name "Branch2" -ResourceGroupName "ForcedTunneling" 
  $lng4 = Get-AzureRmLocalNetworkGateway -Name "Branch3" -ResourceGroupName "ForcedTunneling" 
    
  New-AzureRmVirtualNetworkGatewayConnection -Name "Connection1" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -VirtualNetworkGateway1 $gateway -LocalNetworkGateway2 $lng1 -ConnectionType IPsec -SharedKey "preSharedKey"
  New-AzureRmVirtualNetworkGatewayConnection -Name "Connection2" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -VirtualNetworkGateway1 $gateway -LocalNetworkGateway2 $lng2 -ConnectionType IPsec -SharedKey "preSharedKey"
  New-AzureRmVirtualNetworkGatewayConnection -Name "Connection3" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -VirtualNetworkGateway1 $gateway -LocalNetworkGateway2 $lng3 -ConnectionType IPsec -SharedKey "preSharedKey"
  New-AzureRmVirtualNetworkGatewayConnection -Name "Connection4" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -VirtualNetworkGateway1 $gateway -LocalNetworkGateway2 $lng4 -ConnectionType IPsec -SharedKey "preSharedKey"
    
  Get-AzureRmVirtualNetworkGatewayConnection -Name "Connection1" -ResourceGroupName "ForcedTunneling"
  ```