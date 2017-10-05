---
title: "Şirket içi Azure bağlantıları için VPN ağ geçidi ayarları | Microsoft Docs"
description: "Azure sanal ağ geçitleri için VPN ağ geçidi ayarları hakkında bilgi edinin."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: ae665bc5-0089-45d0-a0d5-bc0ab4e79899
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/26/2017
ms.author: cherylmc
ms.openlocfilehash: 07aa6946b9c3994c5afc5c88837f23567b95d8a5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="about-vpn-gateway-configuration-settings"></a><span data-ttu-id="69f46-103">VPN ağ geçidi yapılandırma ayarları hakkında</span><span class="sxs-lookup"><span data-stu-id="69f46-103">About VPN Gateway configuration settings</span></span>

<span data-ttu-id="69f46-104">Bir VPN ağ geçidi, sanal ağınızı ve şirket içi konumunuz arasındaki şifrelenmiş trafik ortak bir bağlantı üzerinden gönderir sanal ağ geçidi türüdür.</span><span class="sxs-lookup"><span data-stu-id="69f46-104">A VPN gateway is a type of virtual network gateway that sends encrypted traffic between your virtual network and your on-premises location across a public connection.</span></span> <span data-ttu-id="69f46-105">Azure omurga üzerinden sanal ağlar arasında trafiği göndermek için bir VPN ağ geçidi'ni de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="69f46-105">You can also use a VPN gateway to send traffic between virtual networks across the Azure backbone.</span></span>

<span data-ttu-id="69f46-106">Bir VPN gateway bağlantısı her biri yapılandırılabilir ayarları içeren yapılandırmasına göre birden fazla kaynağı kullanır.</span><span class="sxs-lookup"><span data-stu-id="69f46-106">A VPN gateway connection relies on the configuration of multiple resources, each of which contains configurable settings.</span></span> <span data-ttu-id="69f46-107">Bu makalede bölümlerde kaynakları ve Resource Manager dağıtım modelinde oluşturulmuş bir sanal ağ için bir VPN ağ geçidi ile ilgili ayarları açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="69f46-107">The sections in this article discuss the resources and settings that relate to a VPN gateway for a virtual network created in Resource Manager deployment model.</span></span> <span data-ttu-id="69f46-108">Her bağlantı çözümünüz için açıklamaları ve topoloji diyagramları bulabilirsiniz [VPN Gateway hakkında](vpn-gateway-about-vpngateways.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="69f46-108">You can find descriptions and topology diagrams for each connection solution in the [About VPN Gateway](vpn-gateway-about-vpngateways.md) article.</span></span>

## <span data-ttu-id="69f46-109"><a name="gwtype"></a>Ağ geçidi türleri</span><span class="sxs-lookup"><span data-stu-id="69f46-109"><a name="gwtype"></a>Gateway types</span></span>

<span data-ttu-id="69f46-110">Her sanal ağ, yalnızca bir sanal ağ geçidi her tür olabilir.</span><span class="sxs-lookup"><span data-stu-id="69f46-110">Each virtual network can only have one virtual network gateway of each type.</span></span> <span data-ttu-id="69f46-111">Bir sanal ağ geçidi oluştururken, ağ geçidi türü yapılandırmanız için doğru olduğundan emin olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="69f46-111">When you are creating a virtual network gateway, you must make sure that the gateway type is correct for your configuration.</span></span>

<span data-ttu-id="69f46-112">-GatewayType kullanılabilir değerler:</span><span class="sxs-lookup"><span data-stu-id="69f46-112">The available values for -GatewayType are:</span></span>

* <span data-ttu-id="69f46-113">VPN</span><span class="sxs-lookup"><span data-stu-id="69f46-113">Vpn</span></span>
* <span data-ttu-id="69f46-114">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="69f46-114">ExpressRoute</span></span>

<span data-ttu-id="69f46-115">Bir VPN ağ geçidi gerektirir `-GatewayType` *Vpn*.</span><span class="sxs-lookup"><span data-stu-id="69f46-115">A VPN gateway requires the `-GatewayType` *Vpn*.</span></span>

<span data-ttu-id="69f46-116">Örnek:</span><span class="sxs-lookup"><span data-stu-id="69f46-116">Example:</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg `
-Location 'West US' -IpConfigurations $gwipconfig -GatewayType Vpn `
-VpnType RouteBased
```

## <span data-ttu-id="69f46-117"><a name="gwsku"></a>Ağ Geçidi SKU'ları</span><span class="sxs-lookup"><span data-stu-id="69f46-117"><a name="gwsku"></a>Gateway SKUs</span></span>

[!INCLUDE [vpn-gateway-gwsku-include](../../includes/vpn-gateway-gwsku-include.md)]

### <a name="configure-the-gateway-sku"></a><span data-ttu-id="69f46-118">Ağ geçidi SKU'su yapılandırın</span><span class="sxs-lookup"><span data-stu-id="69f46-118">Configure the gateway SKU</span></span>

#### <a name="azure-portal"></a><span data-ttu-id="69f46-119">Azure portalına</span><span class="sxs-lookup"><span data-stu-id="69f46-119">Azure portal</span></span>

<span data-ttu-id="69f46-120">Bir Resource Manager sanal ağ geçidi oluşturmak için Azure portalını kullanıyorsanız, açılan listeyi kullanarak ağ geçidi SKU'su seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="69f46-120">If you use the Azure portal to create a Resource Manager virtual network gateway, you can select the gateway SKU by using the dropdown.</span></span> <span data-ttu-id="69f46-121">İle sunulan seçenekler, seçtiğiniz VPN türü ve ağ geçidi türü için karşılık gelir.</span><span class="sxs-lookup"><span data-stu-id="69f46-121">The options you are presented with correspond to the Gateway type and VPN type that you select.</span></span>

#### <a name="powershell"></a><span data-ttu-id="69f46-122">PowerShell</span><span class="sxs-lookup"><span data-stu-id="69f46-122">PowerShell</span></span>

<span data-ttu-id="69f46-123">Aşağıdaki PowerShell örnek belirtir `-GatewaySku` VpnGw1 olarak.</span><span class="sxs-lookup"><span data-stu-id="69f46-123">The following PowerShell example specifies the `-GatewaySku` as VpnGw1.</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg `
-Location 'West US' -IpConfigurations $gwipconfig -GatewaySku VpnGw1 `
-GatewayType Vpn -VpnType RouteBased
```

#### <span data-ttu-id="69f46-124"><a name="resize"></a>Değişiklik (boyutlandırma) bir ağ geçidi SKU'su</span><span class="sxs-lookup"><span data-stu-id="69f46-124"><a name="resize"></a>Change (resize) a gateway SKU</span></span>

<span data-ttu-id="69f46-125">Daha güçlü bir SKU, ağ geçidi SKU'su yükseltmek istiyorsanız, kullanabileceğiniz `Resize-AzureRmVirtualNetworkGateway` PowerShell cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="69f46-125">If you want to upgrade your gateway SKU to a more powerful SKU, you can use the `Resize-AzureRmVirtualNetworkGateway` PowerShell cmdlet.</span></span> <span data-ttu-id="69f46-126">Ayrıca ağ geçidi Bu cmdlet'i kullanarak SKU boyutunu düşürmek.</span><span class="sxs-lookup"><span data-stu-id="69f46-126">You can also downgrade the gateway SKU size using this cmdlet.</span></span>

<span data-ttu-id="69f46-127">Aşağıdaki PowerShell örnek bir ağ geçidi için VpnGw2 yeniden boyutlandırılan SKU gösterir.</span><span class="sxs-lookup"><span data-stu-id="69f46-127">The following PowerShell example shows a gateway SKU being resized to VpnGw2.</span></span>

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg
Resize-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -GatewaySku VpnGw2
```

## <span data-ttu-id="69f46-128"><a name="connectiontype"></a>Bağlantı türleri</span><span class="sxs-lookup"><span data-stu-id="69f46-128"><a name="connectiontype"></a>Connection types</span></span>

<span data-ttu-id="69f46-129">Resource Manager dağıtım modelinde, her yapılandırma belirli sanal ağ geçidi bağlantı türü gerektirir.</span><span class="sxs-lookup"><span data-stu-id="69f46-129">In the Resource Manager deployment model, each configuration requires a specific virtual network gateway connection type.</span></span> <span data-ttu-id="69f46-130">`-ConnectionType` için kullanılabilir Resource Manager PowerShell değerleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="69f46-130">The available Resource Manager PowerShell values for `-ConnectionType` are:</span></span>

* <span data-ttu-id="69f46-131">IPsec</span><span class="sxs-lookup"><span data-stu-id="69f46-131">IPsec</span></span>
* <span data-ttu-id="69f46-132">Vnet2Vnet</span><span class="sxs-lookup"><span data-stu-id="69f46-132">Vnet2Vnet</span></span>
* <span data-ttu-id="69f46-133">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="69f46-133">ExpressRoute</span></span>
* <span data-ttu-id="69f46-134">VPNClient</span><span class="sxs-lookup"><span data-stu-id="69f46-134">VPNClient</span></span>

<span data-ttu-id="69f46-135">Aşağıdaki PowerShell örnekte, bağlantı türü gerektiren bir S2S bağlantı oluşturuyoruz *IPSec*.</span><span class="sxs-lookup"><span data-stu-id="69f46-135">In the following PowerShell example, we create a S2S connection that requires the connection type *IPsec*.</span></span>

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name localtovon -ResourceGroupName testrg `
-Location 'West US' -VirtualNetworkGateway1 $gateway1 -LocalNetworkGateway2 $local `
-ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
```

## <span data-ttu-id="69f46-136"><a name="vpntype"></a>VPN türleri</span><span class="sxs-lookup"><span data-stu-id="69f46-136"><a name="vpntype"></a>VPN types</span></span>

<span data-ttu-id="69f46-137">VPN ağ geçidi yapılandırması için sanal ağ geçidi oluşturduğunuzda, bir VPN türü belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="69f46-137">When you create the virtual network gateway for a VPN gateway configuration, you must specify a VPN type.</span></span> <span data-ttu-id="69f46-138">Seçtiğiniz VPN türü oluşturmak istediğiniz bağlantı topolojisine bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="69f46-138">The VPN type that you choose depends on the connection topology that you want to create.</span></span> <span data-ttu-id="69f46-139">Örneğin, P2S bağlantısı RouteBased VPN türü gerektirir.</span><span class="sxs-lookup"><span data-stu-id="69f46-139">For example, a P2S connection requires a RouteBased VPN type.</span></span> <span data-ttu-id="69f46-140">Bir VPN türü ayrıca kullandığınız donanımda bağlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="69f46-140">A VPN type can also depend on the hardware that you are using.</span></span> <span data-ttu-id="69f46-141">S2S yapılandırmaları bir VPN cihazı gerektirir.</span><span class="sxs-lookup"><span data-stu-id="69f46-141">S2S configurations require a VPN device.</span></span> <span data-ttu-id="69f46-142">Bazı VPN cihazlarının yalnızca belirli bir VPN türü destekler.</span><span class="sxs-lookup"><span data-stu-id="69f46-142">Some VPN devices only support a certain VPN type.</span></span>

<span data-ttu-id="69f46-143">Seçtiğiniz VPN türü oluşturmak istediğiniz tüm bağlantı çözümünün gereksinimlerini karşılaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="69f46-143">The VPN type you select must satisfy all the connection requirements for the solution you want to create.</span></span> <span data-ttu-id="69f46-144">Örneğin, bir S2S VPN gateway bağlantısı ve P2S VPN ağ geçidi bağlantısı aynı sanal ağ oluşturmak istiyorsanız, VPN türü kullanırsınız *RouteBased* çünkü P2S RouteBased VPN türü gerektirir.</span><span class="sxs-lookup"><span data-stu-id="69f46-144">For example, if you want to create a S2S VPN gateway connection and a P2S VPN gateway connection for the same virtual network, you would use VPN type *RouteBased* because P2S requires a RouteBased VPN type.</span></span> <span data-ttu-id="69f46-145">VPN Cihazınızı RouteBased VPN bağlantısı desteklenen doğrulamak gerekir.</span><span class="sxs-lookup"><span data-stu-id="69f46-145">You would also need to verify that your VPN device supported a RouteBased VPN connection.</span></span> 

<span data-ttu-id="69f46-146">Bir sanal ağ geçidi oluşturulduktan sonra VPN türünü değiştiremezsiniz.</span><span class="sxs-lookup"><span data-stu-id="69f46-146">Once a virtual network gateway has been created, you can't change the VPN type.</span></span> <span data-ttu-id="69f46-147">Sanal ağ geçidini silin ve yeni bir tane oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="69f46-147">You have to delete the virtual network gateway and create a new one.</span></span> <span data-ttu-id="69f46-148">İki VPN türü vardır:</span><span class="sxs-lookup"><span data-stu-id="69f46-148">There are two VPN types:</span></span>

[!INCLUDE [vpn-gateway-vpntype](../../includes/vpn-gateway-vpntype-include.md)]

<span data-ttu-id="69f46-149">Aşağıdaki PowerShell örnek belirtir `-VpnType` olarak *RouteBased*.</span><span class="sxs-lookup"><span data-stu-id="69f46-149">The following PowerShell example specifies the `-VpnType` as *RouteBased*.</span></span> <span data-ttu-id="69f46-150">Bir ağ geçidi oluştururken, -VpnType öğesinin yapılandırmanız için doğru olduğundan emin olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="69f46-150">When you are creating a gateway, you must make sure that the -VpnType is correct for your configuration.</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg `
-Location 'West US' -IpConfigurations $gwipconfig `
-GatewayType Vpn -VpnType RouteBased
```

## <span data-ttu-id="69f46-151"><a name="requirements"></a>Ağ geçidi gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="69f46-151"><a name="requirements"></a>Gateway requirements</span></span>

[!INCLUDE [vpn-gateway-table-requirements](../../includes/vpn-gateway-table-requirements-include.md)]

## <span data-ttu-id="69f46-152"><a name="gwsub"></a>Ağ geçidi alt ağı</span><span class="sxs-lookup"><span data-stu-id="69f46-152"><a name="gwsub"></a>Gateway subnet</span></span>

<span data-ttu-id="69f46-153">Bir VPN ağ geçidi oluşturmadan önce bir ağ geçidi alt ağı oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="69f46-153">Before you create a VPN gateway, you must create a gateway subnet.</span></span> <span data-ttu-id="69f46-154">Ağ geçidi alt ağı sanal ağ geçidi sanal makineleri ve hizmetleri kullanan IP adreslerini içerir.</span><span class="sxs-lookup"><span data-stu-id="69f46-154">The gateway subnet contains the IP addresses that the virtual network gateway VMs and services use.</span></span> <span data-ttu-id="69f46-155">Sanal ağ geçidinizi oluşturduğunuzda, ağ geçidi VM ağ geçidi alt ağına dağıtılan ve gerekli VPN ağ geçidi ayarlarıyla yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="69f46-155">When you create your virtual network gateway, gateway VMs are deployed to the gateway subnet and configured with the required VPN gateway settings.</span></span> <span data-ttu-id="69f46-156">Hiçbir zaman başka bir şey (örneğin, ek VM'ler) ağ geçidi alt ağına dağıtmalısınız.</span><span class="sxs-lookup"><span data-stu-id="69f46-156">You must never deploy anything else (for example, additional VMs) to the gateway subnet.</span></span> <span data-ttu-id="69f46-157">Ağ geçidi alt ağı 'GatewaySubnet' adlı gerekir düzgün çalışması için.</span><span class="sxs-lookup"><span data-stu-id="69f46-157">The gateway subnet must be named 'GatewaySubnet' to work properly.</span></span> <span data-ttu-id="69f46-158">Ağ geçidi alt ağı 'GatewaySubnet' adlandırma, bu sanal ağ geçidi sanal makineleri ve Hizmetleri dağıtmak için alt olduğunu biliyor Azure olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="69f46-158">Naming the gateway subnet 'GatewaySubnet' lets Azure know that this is the subnet to deploy the virtual network gateway VMs and services to.</span></span>

<span data-ttu-id="69f46-159">Ağ geçidi alt ağı oluştururken, alt ağın içerdiği IP adresi sayısını belirtirsiniz.</span><span class="sxs-lookup"><span data-stu-id="69f46-159">When you create the gateway subnet, you specify the number of IP addresses that the subnet contains.</span></span> <span data-ttu-id="69f46-160">Ağ geçidi alt ağdaki IP adresleri ağ geçidi sanal makineleri ve ağ geçidi Hizmetleri ayrılır.</span><span class="sxs-lookup"><span data-stu-id="69f46-160">The IP addresses in the gateway subnet are allocated to the gateway VMs and gateway services.</span></span> <span data-ttu-id="69f46-161">Bazı yapılandırmalar diğerlerinden daha fazla IP adresi gerektirir.</span><span class="sxs-lookup"><span data-stu-id="69f46-161">Some configurations require more IP addresses than others.</span></span> <span data-ttu-id="69f46-162">Oluşturma ve oluşturmak istediğiniz ağ geçidi alt ağı bu gereksinimleri karşıladığını doğrulamak istediğiniz yapılandırma yönergelerini bakın.</span><span class="sxs-lookup"><span data-stu-id="69f46-162">Look at the instructions for the configuration that you want to create and verify that the gateway subnet you want to create meets those requirements.</span></span> <span data-ttu-id="69f46-163">Ayrıca, ağ geçidi alt ağınızı gelecekteki olası ek yapılandırmalar karşılamak için yeterli IP adreslerini içerdiğinden emin olmak isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="69f46-163">Additionally, you may want to make sure your gateway subnet contains enough IP addresses to accommodate possible future additional configurations.</span></span> <span data-ttu-id="69f46-164">Bir ağ geçidi alt ağı/29 kadar küçük oluşturabilirsiniz, ancak 28 ya da daha büyük bir ağ geçidi alt ağı oluşturmanızı öneririz (/ 28, / 27, /26 vs.).</span><span class="sxs-lookup"><span data-stu-id="69f46-164">While you can create a gateway subnet as small as /29, we recommend that you create a gateway subnet of /28 or larger (/28, /27, /26 etc.).</span></span> <span data-ttu-id="69f46-165">İşlevselliği gelecekte eklerseniz, bu şekilde, ağ geçidiniz, kesmeden sonra silip için daha fazla IP adresine izin vermek için ağ geçidi alt ağı gerekmez.</span><span class="sxs-lookup"><span data-stu-id="69f46-165">That way, if you add functionality in the future, you won't have to tear your gateway, then delete and recreate the gateway subnet to allow for more IP addresses.</span></span>

<span data-ttu-id="69f46-166">Aşağıdaki Resource Manager PowerShell örnek GatewaySubnet adlı bir ağ geçidi alt ağı gösterir.</span><span class="sxs-lookup"><span data-stu-id="69f46-166">The following Resource Manager PowerShell example shows a gateway subnet named GatewaySubnet.</span></span> <span data-ttu-id="69f46-167">Şu anda mevcut çoğu yapılandırma için yeterli IP adresine izin veren bir/27 CIDR gösteriminde belirtir görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="69f46-167">You can see the CIDR notation specifies a /27, which allows for enough IP addresses for most configurations that currently exist.</span></span>

```powershell
Add-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -AddressPrefix 10.0.3.0/27
```

[!INCLUDE [vpn-gateway-no-nsg](../../includes/vpn-gateway-no-nsg-include.md)]

## <span data-ttu-id="69f46-168"><a name="lng"></a>Yerel ağ geçitleri</span><span class="sxs-lookup"><span data-stu-id="69f46-168"><a name="lng"></a>Local network gateways</span></span>

<span data-ttu-id="69f46-169">Bir VPN ağ geçidi yapılandırması oluştururken, yerel ağ geçidi genellikle şirket içi konumunuzu temsil eder.</span><span class="sxs-lookup"><span data-stu-id="69f46-169">When creating a VPN gateway configuration, the local network gateway often represents your on-premises location.</span></span> <span data-ttu-id="69f46-170">Klasik dağıtım modelinde, yerel ağ geçidi için Yerel Site olara ifade edilir.</span><span class="sxs-lookup"><span data-stu-id="69f46-170">In the classic deployment model, the local network gateway was referred to as a Local Site.</span></span> 

<span data-ttu-id="69f46-171">Yerel ağ geçidi, şirket içi VPN cihazının genel IP adresi olmak üzere bir ad verin ve şirket içi konumunda yer alan adres öneklerini belirtirsiniz.</span><span class="sxs-lookup"><span data-stu-id="69f46-171">You give the local network gateway a name, the public IP address of the on-premises VPN device, and specify the address prefixes that are located on the on-premises location.</span></span> <span data-ttu-id="69f46-172">Azure ağ trafiği için hedef adres öneklerine bakar, yerel ağ geçidiniz için belirttiğiniz yapılandırma bakar ve paketleri buna uygun şekilde yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="69f46-172">Azure looks at the destination address prefixes for network traffic, consults the configuration that you have specified for your local network gateway, and routes packets accordingly.</span></span> <span data-ttu-id="69f46-173">Ayrıca, VPN ağ geçidi bağlantısı kullanma VNet-VNet yapılandırmaları için yerel ağ geçitleri de belirtin.</span><span class="sxs-lookup"><span data-stu-id="69f46-173">You also specify local network gateways for VNet-to-VNet configurations that use a VPN gateway connection.</span></span>

<span data-ttu-id="69f46-174">Aşağıdaki PowerShell örnek yeni bir yerel ağ geçidi oluşturur:</span><span class="sxs-lookup"><span data-stu-id="69f46-174">The following PowerShell example creates a new local network gateway:</span></span>

```powershell
New-AzureRmLocalNetworkGateway -Name LocalSite -ResourceGroupName testrg `
-Location 'West US' -GatewayIpAddress '23.99.221.164' -AddressPrefix '10.5.51.0/24'
```

<span data-ttu-id="69f46-175">Bazen yerel ağ geçidi ayarlarını değiştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="69f46-175">Sometimes you need to modify the local network gateway settings.</span></span> <span data-ttu-id="69f46-176">Örneğin, eklediğinizde veya adres aralığını değiştirmek veya VPN cihazının IP adresi değişip değişmediğini.</span><span class="sxs-lookup"><span data-stu-id="69f46-176">For example, when you add or modify the address range, or if the IP address of the VPN device changes.</span></span> <span data-ttu-id="69f46-177">Klasik bir VNet için yerel ağlar sayfasında Klasik portalda bu ayarları değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="69f46-177">For a classic VNet, you can change these settings in the classic portal on the Local Networks page.</span></span> <span data-ttu-id="69f46-178">Kaynak Yöneticisi için bkz: [PowerShell kullanarak yerel ağ geçidi ayarlarını değiştirmek](vpn-gateway-modify-local-network-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="69f46-178">For Resource Manager, see [Modify local network gateway settings using PowerShell](vpn-gateway-modify-local-network-gateway.md).</span></span>

## <span data-ttu-id="69f46-179"><a name="resources"></a>REST API ve PowerShell cmdlet'leri</span><span class="sxs-lookup"><span data-stu-id="69f46-179"><a name="resources"></a>REST APIs and PowerShell cmdlets</span></span>

<span data-ttu-id="69f46-180">Ek teknik kaynaklar ve REST API'leri, PowerShell cmdlet'lerini veya Azure CLI için VPN ağ geçidi yapılandırmaları kullanırken belirli sözdizimi gereksinimleri için aşağıdaki sayfalarına bakın:</span><span class="sxs-lookup"><span data-stu-id="69f46-180">For additional technical resources and specific syntax requirements when using REST APIs, PowerShell cmdlets, or Azure CLI for VPN Gateway configurations, see the following pages:</span></span>

| <span data-ttu-id="69f46-181">**Klasik**</span><span class="sxs-lookup"><span data-stu-id="69f46-181">**Classic**</span></span> | <span data-ttu-id="69f46-182">**Resource Manager**</span><span class="sxs-lookup"><span data-stu-id="69f46-182">**Resource Manager**</span></span> |
| --- | --- |
| [<span data-ttu-id="69f46-183">PowerShell</span><span class="sxs-lookup"><span data-stu-id="69f46-183">PowerShell</span></span>](/powershell/module/azure#networking) |[<span data-ttu-id="69f46-184">PowerShell</span><span class="sxs-lookup"><span data-stu-id="69f46-184">PowerShell</span></span>](/powershell/module/azurerm.network#vpn) |
| [<span data-ttu-id="69f46-185">REST API</span><span class="sxs-lookup"><span data-stu-id="69f46-185">REST API</span></span>](https://msdn.microsoft.com/library/jj154113) |[<span data-ttu-id="69f46-186">REST API</span><span class="sxs-lookup"><span data-stu-id="69f46-186">REST API</span></span>](/rest/api/network/virtualnetworkgateways) |
| <span data-ttu-id="69f46-187">Desteklenmiyor</span><span class="sxs-lookup"><span data-stu-id="69f46-187">Not supported</span></span> | [<span data-ttu-id="69f46-188">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="69f46-188">Azure CLI</span></span>](/cli/azure/network/vnet-gateway)|

## <a name="next-steps"></a><span data-ttu-id="69f46-189">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="69f46-189">Next steps</span></span>

<span data-ttu-id="69f46-190">Bir bağlantı yapılandırmaları hakkında daha fazla bilgi için bkz: [VPN Gateway hakkında](vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="69f46-190">For more information about available connection configurations, see [About VPN Gateway](vpn-gateway-about-vpngateways.md).</span></span>