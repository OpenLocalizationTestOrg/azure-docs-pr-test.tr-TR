---
title: "Şirket içi ağ tooan Azure sanal ağı bağlanın: siteden siteye VPN: PowerShell | Microsoft Docs"
description: "Şirket içi bir IPSec bağlantısı üzerinden tooan Azure sanal ağı ağ adımları toocreate genel Internet hello. Bu adımlar PowerShell kullanarak Siteden Siteye şirket içi ve dışı karışık VPN Gateway bağlantısı oluşturmanıza yardımcı olur."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: fcc2fda5-4493-4c15-9436-84d35adbda8e
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/09/2017
ms.author: cherylmc
ms.openlocfilehash: cb8db1dab3a5488816a7f7e8e63908a4c02f55db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vnet-with-a-site-to-site-vpn-connection-using-powershell"></a><span data-ttu-id="c828b-104">PowerShell kullanarak Siteden Siteye VPN bağlantısı ile sanal ağ oluşturma</span><span class="sxs-lookup"><span data-stu-id="c828b-104">Create a VNet with a Site-to-Site VPN connection using PowerShell</span></span>

<span data-ttu-id="c828b-105">Bu makale size nasıl toouse PowerShell toocreate bir Site siteye VPN ağ geçidi bağlantısını şirket içi ağ toohello VNet gösterir.</span><span class="sxs-lookup"><span data-stu-id="c828b-105">This article shows you how toouse PowerShell toocreate a Site-to-Site VPN gateway connection from your on-premises network toohello VNet.</span></span> <span data-ttu-id="c828b-106">Bu makaledeki adımları Hello toohello Resource Manager dağıtım modeli uygulayın.</span><span class="sxs-lookup"><span data-stu-id="c828b-106">hello steps in this article apply toohello Resource Manager deployment model.</span></span> <span data-ttu-id="c828b-107">Liste aşağıdaki hello farklı bir seçeneği seçerek farklı dağıtım aracını veya dağıtım modelini kullanarak bu yapılandırma ayrıca oluşturabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="c828b-107">You can also create this configuration using a different deployment tool or deployment model by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="c828b-108">Azure portal</span><span class="sxs-lookup"><span data-stu-id="c828b-108">Azure portal</span></span>](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="c828b-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c828b-109">PowerShell</span></span>](vpn-gateway-create-site-to-site-rm-powershell.md)
> * [<span data-ttu-id="c828b-110">CLI</span><span class="sxs-lookup"><span data-stu-id="c828b-110">CLI</span></span>](vpn-gateway-howto-site-to-site-resource-manager-cli.md)
> * [<span data-ttu-id="c828b-111">Azure portal (klasik)</span><span class="sxs-lookup"><span data-stu-id="c828b-111">Azure portal (classic)</span></span>](vpn-gateway-howto-site-to-site-classic-portal.md)
> * [<span data-ttu-id="c828b-112">Klasik portal (klasik)</span><span class="sxs-lookup"><span data-stu-id="c828b-112">Classic portal (classic)</span></span>](vpn-gateway-site-to-site-create.md)
> 
>


<span data-ttu-id="c828b-113">Kullanılan tooconnect bir siteden siteye VPN gateway bağlantısı olan bir IPSec/IKE (Ikev1 veya Ikev2) VPN tüneli üzerinden tooan Azure sanal ağı şirket içi ağ.</span><span class="sxs-lookup"><span data-stu-id="c828b-113">A Site-to-Site VPN gateway connection is used tooconnect your on-premises network tooan Azure virtual network over an IPsec/IKE (IKEv1 or IKEv2) VPN tunnel.</span></span> <span data-ttu-id="c828b-114">Bağlantı bu tür bir VPN cihazı bulunan dışarıya dönük bir genel IP adresi atanmış tooit olan şirket içi gerektirir.</span><span class="sxs-lookup"><span data-stu-id="c828b-114">This type of connection requires a VPN device located on-premises that has an externally facing public IP address assigned tooit.</span></span> <span data-ttu-id="c828b-115">VPN ağ geçitleri hakkında daha fazla bilgi için bkz. [VPN ağ geçidi hakkında](vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="c828b-115">For more information about VPN gateways, see [About VPN gateway](vpn-gateway-about-vpngateways.md).</span></span>

![Siteden Siteye şirket içi ve dışı karışık VPN Gateway bağlantısı diyagramı](./media/vpn-gateway-create-site-to-site-rm-powershell/site-to-site-diagram.png)

## <span data-ttu-id="c828b-117"><a name="before"></a>Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="c828b-117"><a name="before"></a>Before you begin</span></span>

<span data-ttu-id="c828b-118">Ölçüt yapılandırmanıza başlamadan önce aşağıdaki hello karşıladığınızı doğrulayın:</span><span class="sxs-lookup"><span data-stu-id="c828b-118">Verify that you have met hello following criteria before beginning your configuration:</span></span>

* <span data-ttu-id="c828b-119">Uyumlu bir VPN cihazı ve mümkün tooconfigure olan birisi olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="c828b-119">Make sure you have a compatible VPN device and someone who is able tooconfigure it.</span></span> <span data-ttu-id="c828b-120">Uyumlu VPN cihazları ve cihaz yapılandırması hakkında daha fazla bilgi için bkz.[VPN Cihazları Hakkında](vpn-gateway-about-vpn-devices.md).</span><span class="sxs-lookup"><span data-stu-id="c828b-120">For more information about compatible VPN devices and device configuration, see [About VPN Devices](vpn-gateway-about-vpn-devices.md).</span></span>
* <span data-ttu-id="c828b-121">VPN cihazınız için dışarıya dönük genel bir IPv4 adresi olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="c828b-121">Verify that you have an externally facing public IPv4 address for your VPN device.</span></span> <span data-ttu-id="c828b-122">Bu IP adresi bir NAT’nin arkasında olamaz.</span><span class="sxs-lookup"><span data-stu-id="c828b-122">This IP address cannot be located behind a NAT.</span></span>
* <span data-ttu-id="c828b-123">Bulunan hello IP adresi aralıklarıyla ilgili bilginiz yoksa, şirket içi ağ, bu ayrıntıları sizin için sağlayabilecek biriyle toocoordinate gerekir.</span><span class="sxs-lookup"><span data-stu-id="c828b-123">If you are unfamiliar with hello IP address ranges located in your on-premises network configuration, you need toocoordinate with someone who can provide those details for you.</span></span> <span data-ttu-id="c828b-124">Bu yapılandırma oluşturduğunuzda, Azure tooyour şirket içi konumu yönlendirilecek hello IP adresi aralığı önekleri belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="c828b-124">When you create this configuration, you must specify hello IP address range prefixes that Azure will route tooyour on-premises location.</span></span> <span data-ttu-id="c828b-125">Şirket içi ağınıza hello ağların hiçbiri diz tooconnect için istediğiniz hello sanal ağ alt ağı üzerinden olabilir.</span><span class="sxs-lookup"><span data-stu-id="c828b-125">None of hello subnets of your on-premises network can over lap with hello virtual network subnets that you want tooconnect to.</span></span>
* <span data-ttu-id="c828b-126">Merhaba hello Azure Resource Manager PowerShell cmdlet'lerinin en son sürümünü yükleyin.</span><span class="sxs-lookup"><span data-stu-id="c828b-126">Install hello latest version of hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="c828b-127">PowerShell cmdlet'leri sık sık güncelleştirilir ve genellikle, PowerShell cmdlet'leri tooget hello son özellik işlevinin tooupdate gerekir.</span><span class="sxs-lookup"><span data-stu-id="c828b-127">PowerShell cmdlets are updated frequently and you will typically need tooupdate your PowerShell cmdlets tooget hello latest feature functionality.</span></span> <span data-ttu-id="c828b-128">PowerShell cmdlet'leri güncelleştirmezseniz belirtilen hello değerleri başarısız olabilir.</span><span class="sxs-lookup"><span data-stu-id="c828b-128">If you don't update your PowerShell cmdlets, hello values specified may fail.</span></span> <span data-ttu-id="c828b-129">Bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview) karşıdan yükleme ve PowerShell cmdlet'leri hakkında daha fazla bilgi.</span><span class="sxs-lookup"><span data-stu-id="c828b-129">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for more information about downloading and installing PowerShell cmdlets.</span></span>

### <span data-ttu-id="c828b-130"><a name="example"></a>Örnek değerler</span><span class="sxs-lookup"><span data-stu-id="c828b-130"><a name="example"></a>Example values</span></span>

<span data-ttu-id="c828b-131">Bu makaledeki örneklerde Hello değerleri aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="c828b-131">hello examples in this article use hello following values.</span></span> <span data-ttu-id="c828b-132">Bu değerleri toocreate bir test ortamı kullanın veya toothem başvurun toobetter anlamak bu makaledeki hello örnekler.</span><span class="sxs-lookup"><span data-stu-id="c828b-132">You can use these values toocreate a test environment, or refer toothem toobetter understand hello examples in this article.</span></span>

```
#Example values

VnetName                = TestVNet1
ResourceGroup           = TestRG1
Location                = East US 
AddressSpace            = 10.11.0.0/16 
SubnetName              = Subnet1 
Subnet                  = 10.11.1.0/28 
GatewaySubnet           = 10.11.0.0/27
LocalNetworkGatewayName = Site2
LNG Public IP           = <VPN device IP address> 
Local Address Prefixes  = 10.0.0.0/24, 20.0.0.0/24
Gateway Name            = VNet1GW
PublicIP                = VNet1GWIP
Gateway IP Config       = gwipconfig1 
VPNType                 = RouteBased 
GatewayType             = Vpn 
ConnectionName          = VNet1toSite2

```


## <span data-ttu-id="c828b-133"><a name="Login"></a>1. Tooyour. abonelik'e bağlanma</span><span class="sxs-lookup"><span data-stu-id="c828b-133"><a name="Login"></a>1. Connect tooyour subscription</span></span>

[!INCLUDE [PowerShell login](../../includes/vpn-gateway-ps-login-include.md)]

## <span data-ttu-id="c828b-134"><a name="VNet"></a>2. Sanal ağ ve ağ geçidi alt ağı oluşturma</span><span class="sxs-lookup"><span data-stu-id="c828b-134"><a name="VNet"></a>2. Create a virtual network and a gateway subnet</span></span>

<span data-ttu-id="c828b-135">Sanal ağınız yoksa bir sanal ağ oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c828b-135">If you don't already have a virtual network, create one.</span></span> <span data-ttu-id="c828b-136">Bir sanal ağ oluştururken, belirttiğiniz hello adres alanlarının, şirket içi ağınızda sahip hello adres alanları çakışmadığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="c828b-136">When creating a virtual network, make sure that hello address spaces you specify don't overlap any of hello address spaces that you have on your on-premises network.</span></span>

[!INCLUDE [About gateway subnets](../../includes/vpn-gateway-about-gwsubnet-include.md)]

[!INCLUDE [No NSG warning](../../includes/vpn-gateway-no-nsg-include.md)]

### <span data-ttu-id="c828b-137"><a name="vnet"></a>toocreate sanal ağ ve bir ağ geçidi alt ağı</span><span class="sxs-lookup"><span data-stu-id="c828b-137"><a name="vnet"></a>toocreate a virtual network and a gateway subnet</span></span>

<span data-ttu-id="c828b-138">Bu örnekte, sanal ağ ve ağ geçidi alt ağı oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="c828b-138">This example creates a virtual network and a gateway subnet.</span></span> <span data-ttu-id="c828b-139">Tooadd görmek için bir ağ geçidi alt ağı gereken sanal ağ zaten varsa [tooadd önceden oluşturulmuş bir ağ geçidi alt ağı tooa sanal ağ](#gatewaysubnet).</span><span class="sxs-lookup"><span data-stu-id="c828b-139">If you already have a virtual network that you need tooadd a gateway subnet to, see [tooadd a gateway subnet tooa virtual network you have already created](#gatewaysubnet).</span></span>

<span data-ttu-id="c828b-140">Kaynak grubu oluşturun:</span><span class="sxs-lookup"><span data-stu-id="c828b-140">Create a resource group:</span></span>

```powershell
New-AzureRmResourceGroup -Name TestRG1 -Location 'East US'
```

<span data-ttu-id="c828b-141">Sanal ağınızı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c828b-141">Create your virtual network.</span></span>

1. <span data-ttu-id="c828b-142">Merhaba değişkenleri ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="c828b-142">Set hello variables.</span></span>

  ```powershell
  $subnet1 = New-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -AddressPrefix 10.11.0.0/27
  $subnet2 = New-AzureRmVirtualNetworkSubnetConfig -Name 'Subnet1' -AddressPrefix 10.11.1.0/28
  ```
2. <span data-ttu-id="c828b-143">Merhaba VNet oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c828b-143">Create hello VNet.</span></span>

  ```powershell
  New-AzureRmVirtualNetwork -Name TestVNet1 -ResourceGroupName TestRG1 `
  -Location 'East US' -AddressPrefix 10.11.0.0/16 -Subnet $subnet1, $subnet2
  ```

### <span data-ttu-id="c828b-144"><a name="gatewaysubnet"></a>tooadd önceden oluşturduğunuz bir ağ geçidi alt ağı tooa sanal ağ</span><span class="sxs-lookup"><span data-stu-id="c828b-144"><a name="gatewaysubnet"></a>tooadd a gateway subnet tooa virtual network you have already created</span></span>

1. <span data-ttu-id="c828b-145">Merhaba değişkenleri ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="c828b-145">Set hello variables.</span></span>

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG1 -Name TestVet1
  ```
2. <span data-ttu-id="c828b-146">Merhaba ağ geçidi alt ağı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c828b-146">Create hello gateway subnet.</span></span>

  ```powershell
  Add-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -AddressPrefix 10.11.0.0/27 -VirtualNetwork $vnet
  ```
3. <span data-ttu-id="c828b-147">Merhaba yapılandırmasını ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="c828b-147">Set hello configuration.</span></span>

  ```powershell
  Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```

## <span data-ttu-id="c828b-148">3. <a name="localnet"></a>Merhaba yerel ağ geçidi oluşturma</span><span class="sxs-lookup"><span data-stu-id="c828b-148">3. <a name="localnet"></a>Create hello local network gateway</span></span>

<span data-ttu-id="c828b-149">Merhaba yerel ağ geçidi genellikle tooyour içi konumunuz anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="c828b-149">hello local network gateway typically refers tooyour on-premises location.</span></span> <span data-ttu-id="c828b-150">Merhaba site olarak Azure tooit bakın, sonra kullanabilirsiniz hello IP adresi belirtin bir ad verin hello şirket içi VPN aygıtının toowhich bir bağlantı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c828b-150">You give hello site a name by which Azure can refer tooit, then specify hello IP address of hello on-premises VPN device toowhich you will create a connection.</span></span> <span data-ttu-id="c828b-151">Ayrıca, hello VPN ağ geçidi toohello VPN cihazı yönlendirilecek hello IP adresi öneklerini belirtin.</span><span class="sxs-lookup"><span data-stu-id="c828b-151">You also specify hello IP address prefixes that will be routed through hello VPN gateway toohello VPN device.</span></span> <span data-ttu-id="c828b-152">Belirttiğiniz hello adres öneklerini hello öneklerini şirket içi ağınızda yer alan var.</span><span class="sxs-lookup"><span data-stu-id="c828b-152">hello address prefixes you specify are hello prefixes located on your on-premises network.</span></span> <span data-ttu-id="c828b-153">Şirket içi ağınıza değişirse hello öneklerini kolayca güncelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c828b-153">If your on-premises network changes, you can easily update hello prefixes.</span></span>

<span data-ttu-id="c828b-154">Hello aşağıdaki değerleri kullanın:</span><span class="sxs-lookup"><span data-stu-id="c828b-154">Use hello following values:</span></span>

* <span data-ttu-id="c828b-155">Merhaba *Gatewayıpaddress* şirket içi VPN aygıtınızın hello IP adresidir.</span><span class="sxs-lookup"><span data-stu-id="c828b-155">hello *GatewayIPAddress* is hello IP address of your on-premises VPN device.</span></span> <span data-ttu-id="c828b-156">VPN cihazınız bir NAT’nin arkasında olamaz.</span><span class="sxs-lookup"><span data-stu-id="c828b-156">Your VPN device cannot be located behind a NAT.</span></span>
* <span data-ttu-id="c828b-157">Merhaba *AddressPrefix* şirket içi adres alanınızdır.</span><span class="sxs-lookup"><span data-stu-id="c828b-157">hello *AddressPrefix* is your on-premises address space.</span></span>

<span data-ttu-id="c828b-158">tooadd tek adres ön ekine sahip bir yerel ağ geçidi:</span><span class="sxs-lookup"><span data-stu-id="c828b-158">tooadd a local network gateway with a single address prefix:</span></span>

  ```powershell
  New-AzureRmLocalNetworkGateway -Name Site2 -ResourceGroupName TestRG1 `
  -Location 'East US' -GatewayIpAddress '23.99.221.164' -AddressPrefix '10.0.0.0/24'
  ```

<span data-ttu-id="c828b-159">tooadd birden çok adres öneklerini sahip bir yerel ağ geçidi:</span><span class="sxs-lookup"><span data-stu-id="c828b-159">tooadd a local network gateway with multiple address prefixes:</span></span>

  ```powershell
  New-AzureRmLocalNetworkGateway -Name Site2 -ResourceGroupName TestRG1 `
  -Location 'East US' -GatewayIpAddress '23.99.221.164' -AddressPrefix @('10.0.0.0/24','20.0.0.0/24')
  ```

<span data-ttu-id="c828b-160">yerel ağ geçidinizin IP adresi öneklerini toomodify:</span><span class="sxs-lookup"><span data-stu-id="c828b-160">toomodify IP address prefixes for your local network gateway:</span></span><br>
<span data-ttu-id="c828b-161">Bazen yerel ağ geçidi ön ekleriniz değişir.</span><span class="sxs-lookup"><span data-stu-id="c828b-161">Sometimes your local network gateway prefixes change.</span></span> <span data-ttu-id="c828b-162">Merhaba adımlar önekleri olup, bir VPN ağ geçidi bağlantısı oluşturup oluşturmadığınıza bağlıdır IP adresiniz toomodify uygulayın.</span><span class="sxs-lookup"><span data-stu-id="c828b-162">hello steps you take toomodify your IP address prefixes depend on whether you have created a VPN gateway connection.</span></span> <span data-ttu-id="c828b-163">Merhaba bkz [bir yerel ağ geçidi değiştirme IP adresi ön eklerini](#modify) bu makalenin.</span><span class="sxs-lookup"><span data-stu-id="c828b-163">See hello [Modify IP address prefixes for a local network gateway](#modify) section of this article.</span></span>

## <span data-ttu-id="c828b-164"><a name="PublicIP"></a>4. Genel IP adresi isteme</span><span class="sxs-lookup"><span data-stu-id="c828b-164"><a name="PublicIP"></a>4. Request a Public IP address</span></span>

<span data-ttu-id="c828b-165">Bir VPN ağ geçidinin genel bir IP adresi olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="c828b-165">A VPN gateway must have a Public IP address.</span></span> <span data-ttu-id="c828b-166">Başlangıç IP adresi kaynağı ilk isteği ve ardından sanal ağ geçidinizi oluştururken tooit bakın.</span><span class="sxs-lookup"><span data-stu-id="c828b-166">You first request hello IP address resource, and then refer tooit when creating your virtual network gateway.</span></span> <span data-ttu-id="c828b-167">Başlangıç IP adresi toohello kaynak Hello VPN ağ geçidi oluşturulup dinamik olarak atanır.</span><span class="sxs-lookup"><span data-stu-id="c828b-167">hello IP address is dynamically assigned toohello resource when hello VPN gateway is created.</span></span> <span data-ttu-id="c828b-168">VPN Gateway hizmeti şu anda yalnızca *Dinamik* Genel IP adresi ayırmayı desteklemektedir.</span><span class="sxs-lookup"><span data-stu-id="c828b-168">VPN Gateway currently only supports *Dynamic* Public IP address allocation.</span></span> <span data-ttu-id="c828b-169">Statik bir Genel IP adresi ataması isteğinde bulunamazsınız.</span><span class="sxs-lookup"><span data-stu-id="c828b-169">You cannot request a Static Public IP address assignment.</span></span> <span data-ttu-id="c828b-170">Ancak, bu tooyour VPN ağ geçidi atandıktan sonra hello IP adresini değiştirse anlamına gelmez.</span><span class="sxs-lookup"><span data-stu-id="c828b-170">However, this does not mean that hello IP address changes after it has been assigned tooyour VPN gateway.</span></span> <span data-ttu-id="c828b-171">ağ geçidi Hello genel IP adresi değişiklikleri hello zaman hello yalnızca zaman silinmiş ve yeniden oluşturulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="c828b-171">hello only time hello Public IP address changes is when hello gateway is deleted and re-created.</span></span> <span data-ttu-id="c828b-172">VPN ağ geçidiniz üzerinde gerçekleştirilen yeniden boyutlandırma, sıfırlama veya diğer iç bakım/yükseltme işlemleri sırasında değişmez.</span><span class="sxs-lookup"><span data-stu-id="c828b-172">It doesn't change across resizing, resetting, or other internal maintenance/upgrades of your VPN gateway.</span></span>

<span data-ttu-id="c828b-173">Tooyour sanal ağ VPN ağ geçidi atanmış bir genel IP adresi isteyin.</span><span class="sxs-lookup"><span data-stu-id="c828b-173">Request a Public IP address that will be assigned tooyour virtual network VPN gateway.</span></span>

```powershell
$gwpip= New-AzureRmPublicIpAddress -Name gwpip -ResourceGroupName TestRG1 -Location 'East US' -AllocationMethod Dynamic
```

## <span data-ttu-id="c828b-174"><a name="GatewayIPConfig"></a>5. Merhaba ağ geçidi IP adresleme yapılandırmasını oluşturma</span><span class="sxs-lookup"><span data-stu-id="c828b-174"><a name="GatewayIPConfig"></a>5. Create hello gateway IP addressing configuration</span></span>

<span data-ttu-id="c828b-175">Merhaba ağ geçidi yapılandırmasını hello alt ağı ve hello ortak IP adresi toouse tanımlar.</span><span class="sxs-lookup"><span data-stu-id="c828b-175">hello gateway configuration defines hello subnet and hello public IP address toouse.</span></span> <span data-ttu-id="c828b-176">Aşağıdaki örnek toocreate hello ağ geçidi yapılandırmanızı kullanın:</span><span class="sxs-lookup"><span data-stu-id="c828b-176">Use hello following example toocreate your gateway configuration:</span></span>

```powershell
$vnet = Get-AzureRmVirtualNetwork -Name TestVNet1 -ResourceGroupName TestRG1
$subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -VirtualNetwork $vnet
$gwipconfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name gwipconfig1 -SubnetId $subnet.Id -PublicIpAddressId $gwpip.Id
```

## <span data-ttu-id="c828b-177"><a name="CreateGateway"></a>6. Merhaba VPN ağ geçidi oluşturma</span><span class="sxs-lookup"><span data-stu-id="c828b-177"><a name="CreateGateway"></a>6. Create hello VPN gateway</span></span>

<span data-ttu-id="c828b-178">Merhaba sanal ağ VPN ağ geçidi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c828b-178">Create hello virtual network VPN gateway.</span></span> <span data-ttu-id="c828b-179">Bir VPN ağ geçidi oluşturma too45 dakika veya daha fazla toocomplete alabilir.</span><span class="sxs-lookup"><span data-stu-id="c828b-179">Creating a VPN gateway can take up too45 minutes or more toocomplete.</span></span>

<span data-ttu-id="c828b-180">Hello aşağıdaki değerleri kullanın:</span><span class="sxs-lookup"><span data-stu-id="c828b-180">Use hello following values:</span></span>

* <span data-ttu-id="c828b-181">Merhaba *- GatewayType* bir Site siteye için yapılandırmadır *Vpn*.</span><span class="sxs-lookup"><span data-stu-id="c828b-181">hello *-GatewayType* for a Site-to-Site configuration is *Vpn*.</span></span> <span data-ttu-id="c828b-182">Merhaba ağ geçidi türü her zaman, uygulamakta olduğunuz belirli toohello yapılandırmadır.</span><span class="sxs-lookup"><span data-stu-id="c828b-182">hello gateway type is always specific toohello configuration that you are implementing.</span></span> <span data-ttu-id="c828b-183">Örneğin, başka ağ geçidi yapılandırmalarında -GatewayType değerinin ExpressRoute olması gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="c828b-183">For example, other gateway configurations may require -GatewayType ExpressRoute.</span></span>
* <span data-ttu-id="c828b-184">Merhaba *- VpnType* olabilir *RouteBased* (bazı belgelerde dinamik ağ geçidi tooas denir) veya *PolicyBased* (bazı belgelerde statik ağ geçidi tooas adlandırılır ).</span><span class="sxs-lookup"><span data-stu-id="c828b-184">hello *-VpnType* can be *RouteBased* (referred tooas a Dynamic Gateway in some documentation), or *PolicyBased* (referred tooas a Static Gateway in some documentation).</span></span> <span data-ttu-id="c828b-185">VPN ağ geçidi türleri hakkında daha fazla bilgi için bkz. [VPN Gateway Hakkında](vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="c828b-185">For more information about VPN gateway types, see [About VPN Gateway](vpn-gateway-about-vpngateways.md).</span></span>
* <span data-ttu-id="c828b-186">Merhaba ağ geçidi SKU'su toouse istediğinizi seçin.</span><span class="sxs-lookup"><span data-stu-id="c828b-186">Select hello Gateway SKU that you want toouse.</span></span> <span data-ttu-id="c828b-187">Bazı SKU’larda yapılandırma sınırlamaları vardır.</span><span class="sxs-lookup"><span data-stu-id="c828b-187">There are configuration limitations for certain SKUs.</span></span> <span data-ttu-id="c828b-188">Daha fazla bilgi için bkz. [Ağ geçidi SKU'ları](vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span><span class="sxs-lookup"><span data-stu-id="c828b-188">For more information, see [Gateway SKUs](vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span></span> <span data-ttu-id="c828b-189">Hello ilgili hello VPN ağ geçidi oluştururken bir hata alırsanız - GatewaySku, doğrulayın hello PowerShell cmdlet'lerinin en yeni sürümünü hello yüklü.</span><span class="sxs-lookup"><span data-stu-id="c828b-189">If you get an error when creating hello VPN gateway regarding hello -GatewaySku, verify that you have installed hello latest version of hello PowerShell cmdlets.</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name VNet1GW -ResourceGroupName TestRG1 `
-Location 'East US' -IpConfigurations $gwipconfig -GatewayType Vpn `
-VpnType RouteBased -GatewaySku VpnGw1
```

## <span data-ttu-id="c828b-190"><a name="ConfigureVPNDevice"></a>7. VPN cihazınızı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="c828b-190"><a name="ConfigureVPNDevice"></a>7. Configure your VPN device</span></span>

<span data-ttu-id="c828b-191">Siteden siteye bağlantıları tooan şirket içi ağ bir VPN cihazı gerektirir.</span><span class="sxs-lookup"><span data-stu-id="c828b-191">Site-to-Site connections tooan on-premises network require a VPN device.</span></span> <span data-ttu-id="c828b-192">Bu adımda VPN cihazınızı yapılandıracaksınız.</span><span class="sxs-lookup"><span data-stu-id="c828b-192">In this step, you configure your VPN device.</span></span> <span data-ttu-id="c828b-193">VPN Cihazınızı yapılandırırken hello aşağıdaki gerekir:</span><span class="sxs-lookup"><span data-stu-id="c828b-193">When configuring your VPN device, you need hello following:</span></span>

- <span data-ttu-id="c828b-194">Paylaşılan bir anahtar.</span><span class="sxs-lookup"><span data-stu-id="c828b-194">A shared key.</span></span> <span data-ttu-id="c828b-195">Bu olduğu hello aynı paylaşılan siteden siteye VPN bağlantınızı oluştururken belirttiğiniz anahtarı.</span><span class="sxs-lookup"><span data-stu-id="c828b-195">This is hello same shared key that you specify when creating your Site-to-Site VPN connection.</span></span> <span data-ttu-id="c828b-196">Bu örneklerde temel bir paylaşılan anahtar kullanılır.</span><span class="sxs-lookup"><span data-stu-id="c828b-196">In our examples, we use a basic shared key.</span></span> <span data-ttu-id="c828b-197">Daha karmaşık bir anahtar toouse oluşturmak öneririz.</span><span class="sxs-lookup"><span data-stu-id="c828b-197">We recommend that you generate a more complex key toouse.</span></span>
- <span data-ttu-id="c828b-198">Merhaba sanal ağ geçidinizin genel IP adresi.</span><span class="sxs-lookup"><span data-stu-id="c828b-198">hello Public IP address of your virtual network gateway.</span></span> <span data-ttu-id="c828b-199">Hello Azure portal, PowerShell veya CLI kullanarak hello ortak IP adresini görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c828b-199">You can view hello public IP address by using hello Azure portal, PowerShell, or CLI.</span></span> <span data-ttu-id="c828b-200">toofind hello PowerShell, aşağıdaki örneğine kullanım hello kullanarak sanal ağ geçidinizin genel IP adresi:</span><span class="sxs-lookup"><span data-stu-id="c828b-200">toofind hello Public IP address of your virtual network gateway using PowerShell, use hello following example:</span></span>

  ```powershell
  Get-AzureRmPublicIpAddress -Name GW1PublicIP -ResourceGroupName TestRG1
  ```

[!INCLUDE [Configure VPN device](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]


## <span data-ttu-id="c828b-201"><a name="CreateConnection"></a>8. Merhaba VPN bağlantısı oluşturun</span><span class="sxs-lookup"><span data-stu-id="c828b-201"><a name="CreateConnection"></a>8. Create hello VPN connection</span></span>

<span data-ttu-id="c828b-202">Ardından, sanal ağ geçidiniz ile VPN cihazınız arasındaki hello siteden siteye VPN bağlantısı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c828b-202">Next, create hello Site-to-Site VPN connection between your virtual network gateway and your VPN device.</span></span> <span data-ttu-id="c828b-203">Emin tooreplace hello değerleri kendi değerlerinizle olabilir.</span><span class="sxs-lookup"><span data-stu-id="c828b-203">Be sure tooreplace hello values with your own.</span></span> <span data-ttu-id="c828b-204">Merhaba paylaşılan anahtar, VPN cihazınızın yapılandırması için kullanılan hello değerle eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="c828b-204">hello shared key must match hello value you used for your VPN device configuration.</span></span> <span data-ttu-id="c828b-205">Bu hello fark '-ConnectionType' siteden siteye için *IPSec*.</span><span class="sxs-lookup"><span data-stu-id="c828b-205">Notice that hello '-ConnectionType' for Site-to-Site is *IPsec*.</span></span>

1. <span data-ttu-id="c828b-206">Merhaba değişkenleri ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="c828b-206">Set hello variables.</span></span>
  ```powershell
  $gateway1 = Get-AzureRmVirtualNetworkGateway -Name VNet1GW -ResourceGroupName TestRG1
  $local = Get-AzureRmLocalNetworkGateway -Name Site2 -ResourceGroupName TestRG1
  ```

2. <span data-ttu-id="c828b-207">Merhaba bağlantı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c828b-207">Create hello connection.</span></span>
  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name VNet1toSite2 -ResourceGroupName TestRG1 `
  -Location 'East US' -VirtualNetworkGateway1 $gateway1 -LocalNetworkGateway2 $local `
  -ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
  ```

<span data-ttu-id="c828b-208">Kısa bir süre, hello bağlantı kurulur.</span><span class="sxs-lookup"><span data-stu-id="c828b-208">After a short while, hello connection will be established.</span></span>

## <span data-ttu-id="c828b-209"><a name="toverify"></a>9. Merhaba VPN bağlantısını doğrulama</span><span class="sxs-lookup"><span data-stu-id="c828b-209"><a name="toverify"></a>9. Verify hello VPN connection</span></span>

<span data-ttu-id="c828b-210">VPN bağlantınızı birkaç farklı şekilde tooverify vardır.</span><span class="sxs-lookup"><span data-stu-id="c828b-210">There are a few different ways tooverify your VPN connection.</span></span>

[!INCLUDE [Verify connection](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

## <span data-ttu-id="c828b-211"><a name="connectVM"></a>tooconnect tooa sanal makine</span><span class="sxs-lookup"><span data-stu-id="c828b-211"><a name="connectVM"></a>tooconnect tooa virtual machine</span></span>

[!INCLUDE [Connect tooa VM](../../includes/vpn-gateway-connect-vm-s2s-include.md)]


## <span data-ttu-id="c828b-212"><a name="modify"></a>Yerel bir ağ geçidinin IP adresi ön eklerini değiştirme</span><span class="sxs-lookup"><span data-stu-id="c828b-212"><a name="modify"></a>Modify IP address prefixes for a local network gateway</span></span>

<span data-ttu-id="c828b-213">Tooyour şirket içi konumunuz yönlendirilmiş istediğiniz başlangıç IP adresi öneklerini değiştirirseniz, hello yerel ağ geçidi değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c828b-213">If hello IP address prefixes that you want routed tooyour on-premises location change, you can modify hello local network gateway.</span></span> <span data-ttu-id="c828b-214">İki ayrı yönerge grubu sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="c828b-214">Two sets of instructions are provided.</span></span> <span data-ttu-id="c828b-215">Seçtiğiniz hello yönergeleri olup, zaten, ağ geçidi bağlantısı oluşturup oluşturmadığınıza bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="c828b-215">hello instructions you choose depend on whether you have already created your gateway connection.</span></span>

[!INCLUDE [Modify prefixes](../../includes/vpn-gateway-modify-ip-prefix-rm-include.md)]

## <span data-ttu-id="c828b-216"><a name="modifygwipaddress"></a>Bir yerel ağ geçidi Hello ağ geçidi IP adresini değiştirme</span><span class="sxs-lookup"><span data-stu-id="c828b-216"><a name="modifygwipaddress"></a>Modify hello gateway IP address for a local network gateway</span></span>

[!INCLUDE [Modify gateway IP address](../../includes/vpn-gateway-modify-lng-gateway-ip-rm-include.md)]

## <a name="next-steps"></a><span data-ttu-id="c828b-217">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c828b-217">Next steps</span></span>

*  <span data-ttu-id="c828b-218">Bağlantınız tamamlandıktan sonra sanal makineleri tooyour sanal ağları ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c828b-218">Once your connection is complete, you can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="c828b-219">Daha fazla bilgi için bkz. [Sanal Makineler](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span><span class="sxs-lookup"><span data-stu-id="c828b-219">For more information, see [Virtual Machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span></span>
* <span data-ttu-id="c828b-220">BGP hakkında daha fazla bilgi için bkz: Merhaba [BGP genel bakış](vpn-gateway-bgp-overview.md) ve [nasıl tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span><span class="sxs-lookup"><span data-stu-id="c828b-220">For information about BGP, see hello [BGP Overview](vpn-gateway-bgp-overview.md) and [How tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span></span>
