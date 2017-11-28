---
title: "Şirket içi Azure bağlantıları için ağ geçidi ayarlarını aaaVPN | Microsoft Docs"
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
ms.openlocfilehash: 01229d99fa37e30e00aa00f939f488d631b5593c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="about-vpn-gateway-configuration-settings"></a><span data-ttu-id="81072-103">VPN ağ geçidi yapılandırma ayarları hakkında</span><span class="sxs-lookup"><span data-stu-id="81072-103">About VPN Gateway configuration settings</span></span>

<span data-ttu-id="81072-104">Bir VPN ağ geçidi, sanal ağınızı ve şirket içi konumunuz arasındaki şifrelenmiş trafik ortak bir bağlantı üzerinden gönderir sanal ağ geçidi türüdür.</span><span class="sxs-lookup"><span data-stu-id="81072-104">A VPN gateway is a type of virtual network gateway that sends encrypted traffic between your virtual network and your on-premises location across a public connection.</span></span> <span data-ttu-id="81072-105">Hello Azure omurga üzerinden sanal ağlar arasında bir VPN ağ geçidi toosend trafiği de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="81072-105">You can also use a VPN gateway toosend traffic between virtual networks across hello Azure backbone.</span></span>

<span data-ttu-id="81072-106">Bir VPN gateway bağlantısı her biri yapılandırılabilir ayarları içeren hello yapılandırmasına göre birden fazla kaynak kullanır.</span><span class="sxs-lookup"><span data-stu-id="81072-106">A VPN gateway connection relies on hello configuration of multiple resources, each of which contains configurable settings.</span></span> <span data-ttu-id="81072-107">Bu makalede Hello bölümlerde hello kaynakları ve Resource Manager dağıtım modelinde oluşturulmuş bir sanal ağ için tooa VPN ağ geçidi ile ilgili ayarları açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="81072-107">hello sections in this article discuss hello resources and settings that relate tooa VPN gateway for a virtual network created in Resource Manager deployment model.</span></span> <span data-ttu-id="81072-108">Merhaba her bağlantı çözümünüz için açıklamaları ve topoloji diyagramları bulabilirsiniz [VPN Gateway hakkında](vpn-gateway-about-vpngateways.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="81072-108">You can find descriptions and topology diagrams for each connection solution in hello [About VPN Gateway](vpn-gateway-about-vpngateways.md) article.</span></span>

## <span data-ttu-id="81072-109"><a name="gwtype"></a>Ağ geçidi türleri</span><span class="sxs-lookup"><span data-stu-id="81072-109"><a name="gwtype"></a>Gateway types</span></span>

<span data-ttu-id="81072-110">Her sanal ağ, yalnızca bir sanal ağ geçidi her tür olabilir.</span><span class="sxs-lookup"><span data-stu-id="81072-110">Each virtual network can only have one virtual network gateway of each type.</span></span> <span data-ttu-id="81072-111">Bir sanal ağ geçidi oluştururken, hello ağ geçidi türü yapılandırmanız için doğru olduğundan emin olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="81072-111">When you are creating a virtual network gateway, you must make sure that hello gateway type is correct for your configuration.</span></span>

<span data-ttu-id="81072-112">-GatewayType için Hello kullanılabilir değerler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="81072-112">hello available values for -GatewayType are:</span></span>

* <span data-ttu-id="81072-113">VPN</span><span class="sxs-lookup"><span data-stu-id="81072-113">Vpn</span></span>
* <span data-ttu-id="81072-114">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="81072-114">ExpressRoute</span></span>

<span data-ttu-id="81072-115">Bir VPN ağ geçidi hello gerektirir `-GatewayType` *Vpn*.</span><span class="sxs-lookup"><span data-stu-id="81072-115">A VPN gateway requires hello `-GatewayType` *Vpn*.</span></span>

<span data-ttu-id="81072-116">Örnek:</span><span class="sxs-lookup"><span data-stu-id="81072-116">Example:</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg `
-Location 'West US' -IpConfigurations $gwipconfig -GatewayType Vpn `
-VpnType RouteBased
```

## <span data-ttu-id="81072-117"><a name="gwsku"></a>Ağ Geçidi SKU'ları</span><span class="sxs-lookup"><span data-stu-id="81072-117"><a name="gwsku"></a>Gateway SKUs</span></span>

[!INCLUDE [vpn-gateway-gwsku-include](../../includes/vpn-gateway-gwsku-include.md)]

### <a name="configure-hello-gateway-sku"></a><span data-ttu-id="81072-118">Merhaba ağ geçidi SKU'su yapılandırın</span><span class="sxs-lookup"><span data-stu-id="81072-118">Configure hello gateway SKU</span></span>

#### <a name="azure-portal"></a><span data-ttu-id="81072-119">Azure portalına</span><span class="sxs-lookup"><span data-stu-id="81072-119">Azure portal</span></span>

<span data-ttu-id="81072-120">Hello Azure portal toocreate bir Resource Manager sanal ağ geçidi kullanırsanız, hello açılan listeyi kullanarak hello ağ geçidi SKU'su seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="81072-120">If you use hello Azure portal toocreate a Resource Manager virtual network gateway, you can select hello gateway SKU by using hello dropdown.</span></span> <span data-ttu-id="81072-121">ile sunulan başlangıç seçenekleri toohello ağ geçidi türü ve seçtiğiniz VPN türü karşılık gelir.</span><span class="sxs-lookup"><span data-stu-id="81072-121">hello options you are presented with correspond toohello Gateway type and VPN type that you select.</span></span>

#### <a name="powershell"></a><span data-ttu-id="81072-122">PowerShell</span><span class="sxs-lookup"><span data-stu-id="81072-122">PowerShell</span></span>

<span data-ttu-id="81072-123">Merhaba aşağıdaki PowerShell örnek belirtir hello `-GatewaySku` VpnGw1 olarak.</span><span class="sxs-lookup"><span data-stu-id="81072-123">hello following PowerShell example specifies hello `-GatewaySku` as VpnGw1.</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg `
-Location 'West US' -IpConfigurations $gwipconfig -GatewaySku VpnGw1 `
-GatewayType Vpn -VpnType RouteBased
```

#### <span data-ttu-id="81072-124"><a name="resize"></a>Değişiklik (boyutlandırma) bir ağ geçidi SKU'su</span><span class="sxs-lookup"><span data-stu-id="81072-124"><a name="resize"></a>Change (resize) a gateway SKU</span></span>

<span data-ttu-id="81072-125">Ağ geçidi SKU'su tooa tooupgrade istiyorsanız, daha güçlü SKU hello kullanabileceğiniz `Resize-AzureRmVirtualNetworkGateway` PowerShell cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="81072-125">If you want tooupgrade your gateway SKU tooa more powerful SKU, you can use hello `Resize-AzureRmVirtualNetworkGateway` PowerShell cmdlet.</span></span> <span data-ttu-id="81072-126">Ayrıca bu cmdlet kullanılarak hello ağ geçidi SKU boyutunu düşürmek.</span><span class="sxs-lookup"><span data-stu-id="81072-126">You can also downgrade hello gateway SKU size using this cmdlet.</span></span>

<span data-ttu-id="81072-127">Aşağıdaki PowerShell örneğine hello olan ağ geçidi SKU'su tooVpnGw2 yeniden boyutlandırılabilir gösterir.</span><span class="sxs-lookup"><span data-stu-id="81072-127">hello following PowerShell example shows a gateway SKU being resized tooVpnGw2.</span></span>

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg
Resize-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -GatewaySku VpnGw2
```

## <span data-ttu-id="81072-128"><a name="connectiontype"></a>Bağlantı türleri</span><span class="sxs-lookup"><span data-stu-id="81072-128"><a name="connectiontype"></a>Connection types</span></span>

<span data-ttu-id="81072-129">Merhaba Resource Manager dağıtım modelinde, her yapılandırma belirli sanal ağ geçidi bağlantı türü gerektirir.</span><span class="sxs-lookup"><span data-stu-id="81072-129">In hello Resource Manager deployment model, each configuration requires a specific virtual network gateway connection type.</span></span> <span data-ttu-id="81072-130">Merhaba kullanılabilir Resource Manager PowerShell değerleri `-ConnectionType` şunlardır:</span><span class="sxs-lookup"><span data-stu-id="81072-130">hello available Resource Manager PowerShell values for `-ConnectionType` are:</span></span>

* <span data-ttu-id="81072-131">IPsec</span><span class="sxs-lookup"><span data-stu-id="81072-131">IPsec</span></span>
* <span data-ttu-id="81072-132">Vnet2Vnet</span><span class="sxs-lookup"><span data-stu-id="81072-132">Vnet2Vnet</span></span>
* <span data-ttu-id="81072-133">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="81072-133">ExpressRoute</span></span>
* <span data-ttu-id="81072-134">VPNClient</span><span class="sxs-lookup"><span data-stu-id="81072-134">VPNClient</span></span>

<span data-ttu-id="81072-135">Aşağıdaki PowerShell örneğine hello hello bağlantı türü gerektiren bir S2S bağlantı oluşturuyoruz *IPSec*.</span><span class="sxs-lookup"><span data-stu-id="81072-135">In hello following PowerShell example, we create a S2S connection that requires hello connection type *IPsec*.</span></span>

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name localtovon -ResourceGroupName testrg `
-Location 'West US' -VirtualNetworkGateway1 $gateway1 -LocalNetworkGateway2 $local `
-ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
```

## <span data-ttu-id="81072-136"><a name="vpntype"></a>VPN türleri</span><span class="sxs-lookup"><span data-stu-id="81072-136"><a name="vpntype"></a>VPN types</span></span>

<span data-ttu-id="81072-137">Merhaba sanal ağ geçidi için VPN ağ geçidi yapılandırması oluşturduğunuzda, bir VPN türü belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="81072-137">When you create hello virtual network gateway for a VPN gateway configuration, you must specify a VPN type.</span></span> <span data-ttu-id="81072-138">Merhaba seçtiğiniz VPN türü toocreate istediğiniz hello bağlantı topolojiye bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="81072-138">hello VPN type that you choose depends on hello connection topology that you want toocreate.</span></span> <span data-ttu-id="81072-139">Örneğin, P2S bağlantısı RouteBased VPN türü gerektirir.</span><span class="sxs-lookup"><span data-stu-id="81072-139">For example, a P2S connection requires a RouteBased VPN type.</span></span> <span data-ttu-id="81072-140">Bir VPN türü ayrıca kullanmakta olduğunuz hello donanımına bağlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="81072-140">A VPN type can also depend on hello hardware that you are using.</span></span> <span data-ttu-id="81072-141">S2S yapılandırmaları bir VPN cihazı gerektirir.</span><span class="sxs-lookup"><span data-stu-id="81072-141">S2S configurations require a VPN device.</span></span> <span data-ttu-id="81072-142">Bazı VPN cihazlarının yalnızca belirli bir VPN türü destekler.</span><span class="sxs-lookup"><span data-stu-id="81072-142">Some VPN devices only support a certain VPN type.</span></span>

<span data-ttu-id="81072-143">Merhaba seçtiğiniz VPN türü toocreate istediğiniz hello çözüm için tüm hello bağlantı gereksinimleri karşılaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="81072-143">hello VPN type you select must satisfy all hello connection requirements for hello solution you want toocreate.</span></span> <span data-ttu-id="81072-144">Örneğin, toocreate istiyorsanız bir S2S VPN gateway bağlantısı ve P2S VPN ağ geçidi bağlantısı için Merhaba aynı sanal ağ, VPN türü kullanırsınız *RouteBased* çünkü P2S RouteBased VPN türü gerektirir.</span><span class="sxs-lookup"><span data-stu-id="81072-144">For example, if you want toocreate a S2S VPN gateway connection and a P2S VPN gateway connection for hello same virtual network, you would use VPN type *RouteBased* because P2S requires a RouteBased VPN type.</span></span> <span data-ttu-id="81072-145">Ayrıca, VPN cihazınızın RouteBased VPN bağlantısı desteklenen tooverify gerekir.</span><span class="sxs-lookup"><span data-stu-id="81072-145">You would also need tooverify that your VPN device supported a RouteBased VPN connection.</span></span> 

<span data-ttu-id="81072-146">Bir sanal ağ geçidi oluşturulduktan sonra hello VPN türü değiştirilemez.</span><span class="sxs-lookup"><span data-stu-id="81072-146">Once a virtual network gateway has been created, you can't change hello VPN type.</span></span> <span data-ttu-id="81072-147">Sanal ağ geçidi hello ve yeni bir tane oluşturun toodelete sahip.</span><span class="sxs-lookup"><span data-stu-id="81072-147">You have toodelete hello virtual network gateway and create a new one.</span></span> <span data-ttu-id="81072-148">İki VPN türü vardır:</span><span class="sxs-lookup"><span data-stu-id="81072-148">There are two VPN types:</span></span>

[!INCLUDE [vpn-gateway-vpntype](../../includes/vpn-gateway-vpntype-include.md)]

<span data-ttu-id="81072-149">Merhaba aşağıdaki PowerShell örnek belirtir hello `-VpnType` olarak *RouteBased*.</span><span class="sxs-lookup"><span data-stu-id="81072-149">hello following PowerShell example specifies hello `-VpnType` as *RouteBased*.</span></span> <span data-ttu-id="81072-150">Bir ağ geçidi oluştururken, o hello emin olmalısınız - VpnType öğesinin yapılandırmanız için doğru.</span><span class="sxs-lookup"><span data-stu-id="81072-150">When you are creating a gateway, you must make sure that hello -VpnType is correct for your configuration.</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg `
-Location 'West US' -IpConfigurations $gwipconfig `
-GatewayType Vpn -VpnType RouteBased
```

## <span data-ttu-id="81072-151"><a name="requirements"></a>Ağ geçidi gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="81072-151"><a name="requirements"></a>Gateway requirements</span></span>

[!INCLUDE [vpn-gateway-table-requirements](../../includes/vpn-gateway-table-requirements-include.md)]

## <span data-ttu-id="81072-152"><a name="gwsub"></a>Ağ geçidi alt ağı</span><span class="sxs-lookup"><span data-stu-id="81072-152"><a name="gwsub"></a>Gateway subnet</span></span>

<span data-ttu-id="81072-153">Bir VPN ağ geçidi oluşturmadan önce bir ağ geçidi alt ağı oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="81072-153">Before you create a VPN gateway, you must create a gateway subnet.</span></span> <span data-ttu-id="81072-154">Hello ağ geçidi alt ağı bu hello sanal ağ geçidi VMs hello IP adreslerini içeren ve Hizmetleri kullanın.</span><span class="sxs-lookup"><span data-stu-id="81072-154">hello gateway subnet contains hello IP addresses that hello virtual network gateway VMs and services use.</span></span> <span data-ttu-id="81072-155">Sanal ağ geçidinizi oluşturduğunuzda, ağ geçidi VMs dağıtılan toohello ağ geçidi alt ağı olan ve gerekli hello VPN ağ geçidi ayarları ile yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="81072-155">When you create your virtual network gateway, gateway VMs are deployed toohello gateway subnet and configured with hello required VPN gateway settings.</span></span> <span data-ttu-id="81072-156">Hiçbir zaman başka herhangi bir şey (örneğin, ek VM'ler) toohello ağ geçidi alt ağı dağıtmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="81072-156">You must never deploy anything else (for example, additional VMs) toohello gateway subnet.</span></span> <span data-ttu-id="81072-157">Merhaba ağ geçidi alt ağı 'GatewaySubnet' toowork düzgün olarak adlandırılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="81072-157">hello gateway subnet must be named 'GatewaySubnet' toowork properly.</span></span> <span data-ttu-id="81072-158">Merhaba ağ geçidi alt ağına 'GatewaySubnet' sağlar adlandırma Azure bilmeniz bu hello alt toodeploy hello sanal ağ ağ geçidi sanal makineleri ve Hizmetleri için.</span><span class="sxs-lookup"><span data-stu-id="81072-158">Naming hello gateway subnet 'GatewaySubnet' lets Azure know that this is hello subnet toodeploy hello virtual network gateway VMs and services to.</span></span>

<span data-ttu-id="81072-159">Merhaba ağ geçidi alt ağı oluşturduğunuzda, alt ağ hello IP adreslerinin sayısı hello içerdiğini belirtin.</span><span class="sxs-lookup"><span data-stu-id="81072-159">When you create hello gateway subnet, you specify hello number of IP addresses that hello subnet contains.</span></span> <span data-ttu-id="81072-160">hello ağ geçidi alt ağı Hello IP adresleri ayrılmış toohello ağ geçidi sanal makineleri ve ağ geçidi hizmetleri verilebilir.</span><span class="sxs-lookup"><span data-stu-id="81072-160">hello IP addresses in hello gateway subnet are allocated toohello gateway VMs and gateway services.</span></span> <span data-ttu-id="81072-161">Bazı yapılandırmalar diğerlerinden daha fazla IP adresi gerektirir.</span><span class="sxs-lookup"><span data-stu-id="81072-161">Some configurations require more IP addresses than others.</span></span> <span data-ttu-id="81072-162">Merhaba yönergeler toocreate istediğiniz ve toocreate istediğiniz bu hello ağ geçidi alt ağı bu gereksinimleri karşıladığını doğrulayın hello yapılandırması için bakın.</span><span class="sxs-lookup"><span data-stu-id="81072-162">Look at hello instructions for hello configuration that you want toocreate and verify that hello gateway subnet you want toocreate meets those requirements.</span></span> <span data-ttu-id="81072-163">Ayrıca, ağ geçidi alt ağı yeterli IP adreslerini tooaccommodate olası gelecekteki ek yapılandırmalar içerdiğinden emin toomake isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="81072-163">Additionally, you may want toomake sure your gateway subnet contains enough IP addresses tooaccommodate possible future additional configurations.</span></span> <span data-ttu-id="81072-164">Bir ağ geçidi alt ağı/29 kadar küçük oluşturabilirsiniz, ancak 28 ya da daha büyük bir ağ geçidi alt ağı oluşturmanızı öneririz (/ 28, / 27, /26 vs.).</span><span class="sxs-lookup"><span data-stu-id="81072-164">While you can create a gateway subnet as small as /29, we recommend that you create a gateway subnet of /28 or larger (/28, /27, /26 etc.).</span></span> <span data-ttu-id="81072-165">Merhaba gelecekteki işlevselliğini eklerseniz bu şekilde, olmaz tootear, ağ geçidine sahip sonra silin ve hello ağ geçidi alt ağı tooallow daha fazla IP adresi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="81072-165">That way, if you add functionality in hello future, you won't have tootear your gateway, then delete and recreate hello gateway subnet tooallow for more IP addresses.</span></span>

<span data-ttu-id="81072-166">Merhaba aşağıdaki Resource Manager PowerShell örnek GatewaySubnet adlı bir ağ geçidi alt ağı gösterir.</span><span class="sxs-lookup"><span data-stu-id="81072-166">hello following Resource Manager PowerShell example shows a gateway subnet named GatewaySubnet.</span></span> <span data-ttu-id="81072-167">Şu anda mevcut çoğu yapılandırma için yeterli IP adresine izin veren bir/27 hello CIDR gösteriminde belirtir görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="81072-167">You can see hello CIDR notation specifies a /27, which allows for enough IP addresses for most configurations that currently exist.</span></span>

```powershell
Add-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -AddressPrefix 10.0.3.0/27
```

[!INCLUDE [vpn-gateway-no-nsg](../../includes/vpn-gateway-no-nsg-include.md)]

## <span data-ttu-id="81072-168"><a name="lng"></a>Yerel ağ geçitleri</span><span class="sxs-lookup"><span data-stu-id="81072-168"><a name="lng"></a>Local network gateways</span></span>

<span data-ttu-id="81072-169">Bir VPN ağ geçidi yapılandırması oluştururken hello yerel ağ geçidi genellikle şirket içi konumunuzu temsil eder.</span><span class="sxs-lookup"><span data-stu-id="81072-169">When creating a VPN gateway configuration, hello local network gateway often represents your on-premises location.</span></span> <span data-ttu-id="81072-170">Merhaba Klasik dağıtım modelinde hello yerel ağ geçidi başvurulan tooas bir yerel Site oluştu.</span><span class="sxs-lookup"><span data-stu-id="81072-170">In hello classic deployment model, hello local network gateway was referred tooas a Local Site.</span></span> 

<span data-ttu-id="81072-171">Merhaba yerel ağ geçidi bir ad verin, hello şirket içi VPN cihazının genel IP adresi hello ve hello şirket içi konumunda yer hello adres öneklerini belirtirsiniz.</span><span class="sxs-lookup"><span data-stu-id="81072-171">You give hello local network gateway a name, hello public IP address of hello on-premises VPN device, and specify hello address prefixes that are located on hello on-premises location.</span></span> <span data-ttu-id="81072-172">Azure ağ trafiği için hello hedef adres öneklerine bakar, yerel ağ geçidiniz için belirttiğiniz hello yapılandırma bakar ve paketleri buna uygun şekilde yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="81072-172">Azure looks at hello destination address prefixes for network traffic, consults hello configuration that you have specified for your local network gateway, and routes packets accordingly.</span></span> <span data-ttu-id="81072-173">Ayrıca, VPN ağ geçidi bağlantısı kullanma VNet-VNet yapılandırmaları için yerel ağ geçitleri de belirtin.</span><span class="sxs-lookup"><span data-stu-id="81072-173">You also specify local network gateways for VNet-to-VNet configurations that use a VPN gateway connection.</span></span>

<span data-ttu-id="81072-174">Aşağıdaki PowerShell örneğine hello yeni bir yerel ağ geçidi oluşturur:</span><span class="sxs-lookup"><span data-stu-id="81072-174">hello following PowerShell example creates a new local network gateway:</span></span>

```powershell
New-AzureRmLocalNetworkGateway -Name LocalSite -ResourceGroupName testrg `
-Location 'West US' -GatewayIpAddress '23.99.221.164' -AddressPrefix '10.5.51.0/24'
```

<span data-ttu-id="81072-175">Bazen toomodify hello yerel ağ geçidi ayarlarını gerekir.</span><span class="sxs-lookup"><span data-stu-id="81072-175">Sometimes you need toomodify hello local network gateway settings.</span></span> <span data-ttu-id="81072-176">Örneğin, eklediğinizde veya hello adres aralığını değiştirmek veya hello VPN cihazının IP adresi hello değişip değişmediğini.</span><span class="sxs-lookup"><span data-stu-id="81072-176">For example, when you add or modify hello address range, or if hello IP address of hello VPN device changes.</span></span> <span data-ttu-id="81072-177">Klasik bir VNet için hello yerel ağlar sayfasında hello Klasik portalda bu ayarları değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="81072-177">For a classic VNet, you can change these settings in hello classic portal on hello Local Networks page.</span></span> <span data-ttu-id="81072-178">Kaynak Yöneticisi için bkz: [PowerShell kullanarak yerel ağ geçidi ayarlarını değiştirmek](vpn-gateway-modify-local-network-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="81072-178">For Resource Manager, see [Modify local network gateway settings using PowerShell](vpn-gateway-modify-local-network-gateway.md).</span></span>

## <span data-ttu-id="81072-179"><a name="resources"></a>REST API ve PowerShell cmdlet'leri</span><span class="sxs-lookup"><span data-stu-id="81072-179"><a name="resources"></a>REST APIs and PowerShell cmdlets</span></span>

<span data-ttu-id="81072-180">Ek teknik kaynaklar ve REST API'leri, PowerShell cmdlet'lerini veya Azure CLI için VPN ağ geçidi yapılandırmaları kullanırken belirli sözdizimi gereksinimleri için sayfalar aşağıdaki hello bakın:</span><span class="sxs-lookup"><span data-stu-id="81072-180">For additional technical resources and specific syntax requirements when using REST APIs, PowerShell cmdlets, or Azure CLI for VPN Gateway configurations, see hello following pages:</span></span>

| <span data-ttu-id="81072-181">**Klasik**</span><span class="sxs-lookup"><span data-stu-id="81072-181">**Classic**</span></span> | <span data-ttu-id="81072-182">**Resource Manager**</span><span class="sxs-lookup"><span data-stu-id="81072-182">**Resource Manager**</span></span> |
| --- | --- |
| [<span data-ttu-id="81072-183">PowerShell</span><span class="sxs-lookup"><span data-stu-id="81072-183">PowerShell</span></span>](/powershell/module/azure#networking) |[<span data-ttu-id="81072-184">PowerShell</span><span class="sxs-lookup"><span data-stu-id="81072-184">PowerShell</span></span>](/powershell/module/azurerm.network#vpn) |
| [<span data-ttu-id="81072-185">REST API</span><span class="sxs-lookup"><span data-stu-id="81072-185">REST API</span></span>](https://msdn.microsoft.com/library/jj154113) |[<span data-ttu-id="81072-186">REST API</span><span class="sxs-lookup"><span data-stu-id="81072-186">REST API</span></span>](/rest/api/network/virtualnetworkgateways) |
| <span data-ttu-id="81072-187">Desteklenmiyor</span><span class="sxs-lookup"><span data-stu-id="81072-187">Not supported</span></span> | [<span data-ttu-id="81072-188">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="81072-188">Azure CLI</span></span>](/cli/azure/network/vnet-gateway)|

## <a name="next-steps"></a><span data-ttu-id="81072-189">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="81072-189">Next steps</span></span>

<span data-ttu-id="81072-190">Bir bağlantı yapılandırmaları hakkında daha fazla bilgi için bkz: [VPN Gateway hakkında](vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="81072-190">For more information about available connection configurations, see [About VPN Gateway](vpn-gateway-about-vpngateways.md).</span></span>