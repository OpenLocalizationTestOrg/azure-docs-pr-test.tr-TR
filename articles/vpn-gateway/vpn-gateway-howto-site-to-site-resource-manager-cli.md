---
title: "Şirket içi ağ tooan Azure sanal ağı bağlanın: siteden siteye VPN: CLI | Microsoft Docs"
description: "Şirket içi bir IPSec bağlantısı üzerinden tooan Azure sanal ağı ağ adımları toocreate genel Internet hello. Bu adımlar CLI kullanarak Siteden Siteye şirket içi ve dışı karışık VPN Gateway bağlantısı oluşturmanıza yardımcı olur."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/09/2017
ms.author: cherylmc
ms.openlocfilehash: c652cf2caf3928cdeb19d7dc329f6db101e5ed90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-with-a-site-to-site-vpn-connection-using-cli"></a><span data-ttu-id="eb55b-104">CLI kullanarak Siteden Siteye VPN bağlantısı olan bir sanal ağ oluşturma</span><span class="sxs-lookup"><span data-stu-id="eb55b-104">Create a virtual network with a Site-to-Site VPN connection using CLI</span></span>

<span data-ttu-id="eb55b-105">Bu makale size nasıl toouse hello Azure CLI toocreate, şirket içi ağ toohello VNet bir siteden siteye VPN ağ geçidi bağlantısını gösterir.</span><span class="sxs-lookup"><span data-stu-id="eb55b-105">This article shows you how toouse hello Azure CLI toocreate a Site-to-Site VPN gateway connection from your on-premises network toohello VNet.</span></span> <span data-ttu-id="eb55b-106">Bu makaledeki adımları Hello toohello Resource Manager dağıtım modeli uygulayın.</span><span class="sxs-lookup"><span data-stu-id="eb55b-106">hello steps in this article apply toohello Resource Manager deployment model.</span></span> <span data-ttu-id="eb55b-107">Liste aşağıdaki hello farklı bir seçeneği seçerek farklı dağıtım aracını veya dağıtım modelini kullanarak bu yapılandırma ayrıca oluşturabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="eb55b-107">You can also create this configuration using a different deployment tool or deployment model by selecting a different option from hello following list:</span></span><br>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="eb55b-108">Azure portal</span><span class="sxs-lookup"><span data-stu-id="eb55b-108">Azure portal</span></span>](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="eb55b-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="eb55b-109">PowerShell</span></span>](vpn-gateway-create-site-to-site-rm-powershell.md)
> * [<span data-ttu-id="eb55b-110">CLI</span><span class="sxs-lookup"><span data-stu-id="eb55b-110">CLI</span></span>](vpn-gateway-howto-site-to-site-resource-manager-cli.md)
> * [<span data-ttu-id="eb55b-111">Azure portal (klasik)</span><span class="sxs-lookup"><span data-stu-id="eb55b-111">Azure portal (classic)</span></span>](vpn-gateway-howto-site-to-site-classic-portal.md)
> 
>


![Siteden Siteye şirket içi ve dışı karışık VPN Gateway bağlantısı diyagramı](./media/vpn-gateway-howto-site-to-site-resource-manager-cli/site-to-site-diagram.png)

<span data-ttu-id="eb55b-113">Kullanılan tooconnect bir siteden siteye VPN gateway bağlantısı olan bir IPSec/IKE (Ikev1 veya Ikev2) VPN tüneli üzerinden tooan Azure sanal ağı şirket içi ağ.</span><span class="sxs-lookup"><span data-stu-id="eb55b-113">A Site-to-Site VPN gateway connection is used tooconnect your on-premises network tooan Azure virtual network over an IPsec/IKE (IKEv1 or IKEv2) VPN tunnel.</span></span> <span data-ttu-id="eb55b-114">Bağlantı bu tür bir VPN cihazı bulunan dışarıya dönük bir genel IP adresi atanmış tooit olan şirket içi gerektirir.</span><span class="sxs-lookup"><span data-stu-id="eb55b-114">This type of connection requires a VPN device located on-premises that has an externally facing public IP address assigned tooit.</span></span> <span data-ttu-id="eb55b-115">VPN ağ geçitleri hakkında daha fazla bilgi için bkz. [VPN ağ geçidi hakkında](vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="eb55b-115">For more information about VPN gateways, see [About VPN gateway](vpn-gateway-about-vpngateways.md).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="eb55b-116">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="eb55b-116">Before you begin</span></span>

<span data-ttu-id="eb55b-117">Ölçüt yapılandırmaya başlamadan önce aşağıdaki hello karşıladığınızı doğrulayın:</span><span class="sxs-lookup"><span data-stu-id="eb55b-117">Verify that you have met hello following criteria before beginning configuration:</span></span>

* <span data-ttu-id="eb55b-118">Uyumlu bir VPN cihazı ve mümkün tooconfigure olan birisi olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="eb55b-118">Make sure you have a compatible VPN device and someone who is able tooconfigure it.</span></span> <span data-ttu-id="eb55b-119">Uyumlu VPN cihazları ve cihaz yapılandırması hakkında daha fazla bilgi için bkz.[VPN Cihazları Hakkında](vpn-gateway-about-vpn-devices.md).</span><span class="sxs-lookup"><span data-stu-id="eb55b-119">For more information about compatible VPN devices and device configuration, see [About VPN Devices](vpn-gateway-about-vpn-devices.md).</span></span>
* <span data-ttu-id="eb55b-120">VPN cihazınız için dışarıya dönük genel bir IPv4 adresi olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="eb55b-120">Verify that you have an externally facing public IPv4 address for your VPN device.</span></span> <span data-ttu-id="eb55b-121">Bu IP adresi bir NAT’nin arkasında olamaz.</span><span class="sxs-lookup"><span data-stu-id="eb55b-121">This IP address cannot be located behind a NAT.</span></span>
* <span data-ttu-id="eb55b-122">Bulunan hello IP adresi aralıklarıyla ilgili bilginiz yoksa, şirket içi ağ, bu ayrıntıları sizin için sağlayabilecek biriyle toocoordinate gerekir.</span><span class="sxs-lookup"><span data-stu-id="eb55b-122">If you are unfamiliar with hello IP address ranges located in your on-premises network configuration, you need toocoordinate with someone who can provide those details for you.</span></span> <span data-ttu-id="eb55b-123">Bu yapılandırma oluşturduğunuzda, Azure tooyour şirket içi konumu yönlendirilecek hello IP adresi aralığı önekleri belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="eb55b-123">When you create this configuration, you must specify hello IP address range prefixes that Azure will route tooyour on-premises location.</span></span> <span data-ttu-id="eb55b-124">Şirket içi ağınıza hello ağların hiçbiri diz tooconnect için istediğiniz hello sanal ağ alt ağı üzerinden olabilir.</span><span class="sxs-lookup"><span data-stu-id="eb55b-124">None of hello subnets of your on-premises network can over lap with hello virtual network subnets that you want tooconnect to.</span></span>
* <span data-ttu-id="eb55b-125">Merhaba CLI komutları (2.0 veya üstü) en son sürümünü yüklediğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="eb55b-125">Verify that you have installed latest version of hello CLI commands (2.0 or later).</span></span> <span data-ttu-id="eb55b-126">Merhaba CLI komutları yükleme hakkında daha fazla bilgi için bkz: [Azure CLI 2.0 yükleme](/cli/azure/install-azure-cli) ve [Azure CLI 2.0 ile çalışmaya başlama](/cli/azure/get-started-with-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="eb55b-126">For information about installing hello CLI commands, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli) and [Get Started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli).</span></span>

### <span data-ttu-id="eb55b-127"><a name="example"></a>Örnek değerler</span><span class="sxs-lookup"><span data-stu-id="eb55b-127"><a name="example"></a>Example values</span></span>

<span data-ttu-id="eb55b-128">Aşağıdaki değerleri toocreate bir test ortamı hello kullanın veya toothese değerleri bkz toobetter anlamak bu makaledeki hello örnekler:</span><span class="sxs-lookup"><span data-stu-id="eb55b-128">You can use hello following values toocreate a test environment, or refer toothese values toobetter understand hello examples in this article:</span></span>

```
#Example values

VnetName                = TestVNet1 
ResourceGroup           = TestRG1 
Location                = eastus 
AddressSpace            = 10.11.0.0/16 
SubnetName              = Subnet1 
Subnet                  = 10.11.0.0/24 
GatewaySubnet           = 10.11.255.0/27 
LocalNetworkGatewayName = Site2 
LNG Public IP           = <VPN device IP address>
LocalAddrPrefix1        = 10.0.0.0/24
LocalAddrPrefix2        = 20.0.0.0/24   
GatewayName             = VNet1GW 
PublicIP                = VNet1GWIP 
VPNType                 = RouteBased 
GatewayType             = Vpn 
ConnectionName          = VNet1toSite2
```

## <span data-ttu-id="eb55b-129"><a name="Login"></a>1. Tooyour. abonelik'e bağlanma</span><span class="sxs-lookup"><span data-stu-id="eb55b-129"><a name="Login"></a>1. Connect tooyour subscription</span></span>

[!INCLUDE [CLI login](../../includes/vpn-gateway-cli-login-include.md)]

## <span data-ttu-id="eb55b-130"><a name="rg"></a>2. Kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="eb55b-130"><a name="rg"></a>2. Create a resource group</span></span>

<span data-ttu-id="eb55b-131">Merhaba aşağıdaki örnek hello 'eastus' konum ' TestRG1' adlı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="eb55b-131">hello following example creates a resource group named 'TestRG1' in hello 'eastus' location.</span></span> <span data-ttu-id="eb55b-132">Sanal ağınızı toocreate istediğiniz hello bölgede bir kaynak grubu zaten varsa, bunun yerine bir kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eb55b-132">If you already have a resource group in hello region that you want toocreate your VNet, you can use that one instead.</span></span>

```azurecli
az group create --name TestRG1 --location eastus
```

## <span data-ttu-id="eb55b-133"><a name="VNet"></a>3. Sanal ağ oluşturma</span><span class="sxs-lookup"><span data-stu-id="eb55b-133"><a name="VNet"></a>3. Create a virtual network</span></span>

<span data-ttu-id="eb55b-134">Bir sanal ağ zaten yoksa oluşturmak hello kullanarak [az ağ vnet oluşturma](/cli/azure/network/vnet#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="eb55b-134">If you don't already have a virtual network, create one using hello [az network vnet create](/cli/azure/network/vnet#create) command.</span></span> <span data-ttu-id="eb55b-135">Bir sanal ağ oluştururken, belirttiğiniz hello adres alanlarının, şirket içi ağınızda sahip hello adres alanları çakışmadığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="eb55b-135">When creating a virtual network, make sure that hello address spaces you specify don't overlap any of hello address spaces that you have on your on-premises network.</span></span>

<span data-ttu-id="eb55b-136">Merhaba aşağıdaki örnek 'TestVNet1' ve bir alt ağı, 'Subnet1' adlı bir sanal ağ oluşturur.</span><span class="sxs-lookup"><span data-stu-id="eb55b-136">hello following example creates a virtual network named 'TestVNet1' and a subnet, 'Subnet1'.</span></span>

```azurecli
az network vnet create --name TestVNet1 --resource-group TestRG1 --address-prefix 10.11.0.0/16 --location eastus --subnet-name Subnet1 --subnet-prefix 10.11.0.0/24
```

## <span data-ttu-id="eb55b-137">4. <a name="gwsub"></a>Merhaba ağ geçidi alt ağı oluşturun</span><span class="sxs-lookup"><span data-stu-id="eb55b-137">4. <a name="gwsub"></a>Create hello gateway subnet</span></span>

[!INCLUDE [vpn-gateway-no-nsg](../../includes/vpn-gateway-no-nsg-include.md)]

<span data-ttu-id="eb55b-138">Bu yapılandırma için, bir ağ geçidi alt ağına da ihtiyacınız olacaktır.</span><span class="sxs-lookup"><span data-stu-id="eb55b-138">For this configuration, you also need a gateway subnet.</span></span> <span data-ttu-id="eb55b-139">Merhaba sanal ağ geçidi hello VPN ağ geçidi Hizmetleri tarafından kullanılan hello IP adreslerini içeren bir ağ geçidi alt ağı kullanır.</span><span class="sxs-lookup"><span data-stu-id="eb55b-139">hello virtual network gateway uses a gateway subnet that contains hello IP addresses that are used by hello VPN gateway services.</span></span> <span data-ttu-id="eb55b-140">Ağ geçidi alt ağını oluşturduğunuzda, bu alt ağ 'GatewaySubnet' olarak adlandırılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="eb55b-140">When you create a gateway subnet, it must be named 'GatewaySubnet'.</span></span> <span data-ttu-id="eb55b-141">Başka bir ad kullanırsanız alt ağ oluşturulur ancak Azure bunu bir ağ geçidi alt ağı olarak değerlendirmez.</span><span class="sxs-lookup"><span data-stu-id="eb55b-141">If you name it something else, you create a subnet, but Azure won't treat it as a gateway subnet.</span></span>

<span data-ttu-id="eb55b-142">Merhaba, belirttiğiniz hello ağ geçidi alt ağı boyutunu toocreate istediğiniz hello VPN ağ geçidi yapılandırmasına bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="eb55b-142">hello size of hello gateway subnet that you specify depends on hello VPN gateway configuration that you want toocreate.</span></span> <span data-ttu-id="eb55b-143">Olası toocreate ağ geçidi alt ağı /29 küçük olmakla birlikte, / 27 veya /28 seçerek daha fazla adreslerini içeren daha büyük bir alt ağı oluşturmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="eb55b-143">While it is possible toocreate a gateway subnet as small as /29, we recommend that you create a larger subnet that includes more addresses by selecting /27 or /28.</span></span> <span data-ttu-id="eb55b-144">Daha büyük bir ağ geçidi alt ağı kullanmak yeterli IP adreslerini tooaccommodate olası gelecekteki yapılandırmaları için sağlar.</span><span class="sxs-lookup"><span data-stu-id="eb55b-144">Using a larger gateway subnet allows for enough IP addresses tooaccommodate possible future configurations.</span></span>

<span data-ttu-id="eb55b-145">Kullanım hello [az ağ sanal alt oluşturmak](/cli/azure/network/vnet/subnet#create) komutu toocreate hello ağ geçidi alt ağı.</span><span class="sxs-lookup"><span data-stu-id="eb55b-145">Use hello [az network vnet subnet create](/cli/azure/network/vnet/subnet#create) command toocreate hello gateway subnet.</span></span>

```azurecli
az network vnet subnet create --address-prefix 10.11.255.0/27 --name GatewaySubnet --resource-group TestRG1 --vnet-name TestVNet1
```

## <span data-ttu-id="eb55b-146"><a name="localnet"></a>5. Merhaba yerel ağ geçidi oluşturma</span><span class="sxs-lookup"><span data-stu-id="eb55b-146"><a name="localnet"></a>5. Create hello local network gateway</span></span>

<span data-ttu-id="eb55b-147">Merhaba yerel ağ geçidi genellikle tooyour içi konumunuz anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="eb55b-147">hello local network gateway typically refers tooyour on-premises location.</span></span> <span data-ttu-id="eb55b-148">Merhaba site olarak Azure tooit bakın, sonra kullanabilirsiniz hello IP adresi belirtin bir ad verin hello şirket içi VPN aygıtının toowhich bir bağlantı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="eb55b-148">You give hello site a name by which Azure can refer tooit, then specify hello IP address of hello on-premises VPN device toowhich you will create a connection.</span></span> <span data-ttu-id="eb55b-149">Ayrıca, hello VPN ağ geçidi toohello VPN cihazı yönlendirilecek hello IP adresi öneklerini belirtin.</span><span class="sxs-lookup"><span data-stu-id="eb55b-149">You also specify hello IP address prefixes that will be routed through hello VPN gateway toohello VPN device.</span></span> <span data-ttu-id="eb55b-150">Belirttiğiniz hello adres öneklerini hello öneklerini şirket içi ağınızda yer alan var.</span><span class="sxs-lookup"><span data-stu-id="eb55b-150">hello address prefixes you specify are hello prefixes located on your on-premises network.</span></span> <span data-ttu-id="eb55b-151">Şirket içi ağınıza değişirse hello öneklerini kolayca güncelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eb55b-151">If your on-premises network changes, you can easily update hello prefixes.</span></span>

<span data-ttu-id="eb55b-152">Hello aşağıdaki değerleri kullanın:</span><span class="sxs-lookup"><span data-stu-id="eb55b-152">Use hello following values:</span></span>

* <span data-ttu-id="eb55b-153">Merhaba *--ağ geçidi IP adresi* şirket içi VPN aygıtınızın hello IP adresidir.</span><span class="sxs-lookup"><span data-stu-id="eb55b-153">hello *--gateway-ip-address* is hello IP address of your on-premises VPN device.</span></span> <span data-ttu-id="eb55b-154">VPN cihazınız bir NAT’nin arkasında olamaz.</span><span class="sxs-lookup"><span data-stu-id="eb55b-154">Your VPN device cannot be located behind a NAT.</span></span>
* <span data-ttu-id="eb55b-155">Merhaba *--yerel adres öneklerini* şirket içi adres alanlarının olduğundan.</span><span class="sxs-lookup"><span data-stu-id="eb55b-155">hello *--local-address-prefixes* are your on-premises address spaces.</span></span>

<span data-ttu-id="eb55b-156">Kullanım hello [az ağ yerel-ağ geçidi oluşturmak](/cli/azure/network/local-gateway#create) komutu tooadd birden çok adres öneklerini sahip bir yerel ağ geçidi:</span><span class="sxs-lookup"><span data-stu-id="eb55b-156">Use hello [az network local-gateway create](/cli/azure/network/local-gateway#create) command tooadd a local network gateway with multiple address prefixes:</span></span>

```azurecli
az network local-gateway create --gateway-ip-address 23.99.221.164 --name Site2 --resource-group TestRG1 --local-address-prefixes 10.0.0.0/24 20.0.0.0/24
```

## <span data-ttu-id="eb55b-157"><a name="PublicIP"></a>6. Genel IP adresi isteme</span><span class="sxs-lookup"><span data-stu-id="eb55b-157"><a name="PublicIP"></a>6. Request a Public IP address</span></span>

<span data-ttu-id="eb55b-158">Bir VPN ağ geçidinin genel bir IP adresi olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="eb55b-158">A VPN gateway must have a Public IP address.</span></span> <span data-ttu-id="eb55b-159">Başlangıç IP adresi kaynağı ilk isteği ve ardından sanal ağ geçidinizi oluştururken tooit bakın.</span><span class="sxs-lookup"><span data-stu-id="eb55b-159">You first request hello IP address resource, and then refer tooit when creating your virtual network gateway.</span></span> <span data-ttu-id="eb55b-160">Başlangıç IP adresi toohello kaynak Hello VPN ağ geçidi oluşturulup dinamik olarak atanır.</span><span class="sxs-lookup"><span data-stu-id="eb55b-160">hello IP address is dynamically assigned toohello resource when hello VPN gateway is created.</span></span> <span data-ttu-id="eb55b-161">VPN Gateway hizmeti şu anda yalnızca *Dinamik* Genel IP adresi ayırmayı desteklemektedir.</span><span class="sxs-lookup"><span data-stu-id="eb55b-161">VPN Gateway currently only supports *Dynamic* Public IP address allocation.</span></span> <span data-ttu-id="eb55b-162">Statik bir Genel IP adresi ataması isteğinde bulunamazsınız.</span><span class="sxs-lookup"><span data-stu-id="eb55b-162">You cannot request a Static Public IP address assignment.</span></span> <span data-ttu-id="eb55b-163">Ancak, bu tooyour VPN ağ geçidi atandıktan sonra hello IP adresini değiştirse anlamına gelmez.</span><span class="sxs-lookup"><span data-stu-id="eb55b-163">However, this does not mean that hello IP address changes after it has been assigned tooyour VPN gateway.</span></span> <span data-ttu-id="eb55b-164">ağ geçidi Hello genel IP adresi değişiklikleri hello zaman hello yalnızca zaman silinmiş ve yeniden oluşturulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="eb55b-164">hello only time hello Public IP address changes is when hello gateway is deleted and re-created.</span></span> <span data-ttu-id="eb55b-165">VPN ağ geçidiniz üzerinde gerçekleştirilen yeniden boyutlandırma, sıfırlama veya diğer iç bakım/yükseltme işlemleri sırasında değişmez.</span><span class="sxs-lookup"><span data-stu-id="eb55b-165">It doesn't change across resizing, resetting, or other internal maintenance/upgrades of your VPN gateway.</span></span>

<span data-ttu-id="eb55b-166">Kullanım hello [az ağ genel IP oluşturun](/cli/azure/network/public-ip#create) komutu toorequest dinamik genel IP adresi.</span><span class="sxs-lookup"><span data-stu-id="eb55b-166">Use hello [az network public-ip create](/cli/azure/network/public-ip#create) command toorequest a Dynamic Public IP address.</span></span>

```azurecli
az network public-ip create --name VNet1GWIP --resource-group TestRG1 --allocation-method Dynamic
```

## <span data-ttu-id="eb55b-167"><a name="CreateGateway"></a>7. Merhaba VPN ağ geçidi oluşturma</span><span class="sxs-lookup"><span data-stu-id="eb55b-167"><a name="CreateGateway"></a>7. Create hello VPN gateway</span></span>

<span data-ttu-id="eb55b-168">Merhaba sanal ağ VPN ağ geçidi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="eb55b-168">Create hello virtual network VPN gateway.</span></span> <span data-ttu-id="eb55b-169">Bir VPN ağ geçidi oluşturma too45 dakika veya daha fazla toocomplete alabilir.</span><span class="sxs-lookup"><span data-stu-id="eb55b-169">Creating a VPN gateway can take up too45 minutes or more toocomplete.</span></span>

<span data-ttu-id="eb55b-170">Hello aşağıdaki değerleri kullanın:</span><span class="sxs-lookup"><span data-stu-id="eb55b-170">Use hello following values:</span></span>

* <span data-ttu-id="eb55b-171">Merhaba *--ağ geçidi türü* bir Site siteye için yapılandırmadır *Vpn*.</span><span class="sxs-lookup"><span data-stu-id="eb55b-171">hello *--gateway-type* for a Site-to-Site configuration is *Vpn*.</span></span> <span data-ttu-id="eb55b-172">Merhaba ağ geçidi türü her zaman, uygulamakta olduğunuz belirli toohello yapılandırmadır.</span><span class="sxs-lookup"><span data-stu-id="eb55b-172">hello gateway type is always specific toohello configuration that you are implementing.</span></span> <span data-ttu-id="eb55b-173">Daha fazla bilgi için bkz. [Ağ geçidi türleri](vpn-gateway-about-vpn-gateway-settings.md#gwtype).</span><span class="sxs-lookup"><span data-stu-id="eb55b-173">For more information, see [Gateway types](vpn-gateway-about-vpn-gateway-settings.md#gwtype).</span></span>
* <span data-ttu-id="eb55b-174">Merhaba *--vpn türü* olabilir *RouteBased* (bazı belgelerde dinamik ağ geçidi tooas denir) veya *PolicyBased* (tooas statik bir ağ geçidi bazı olarak adlandırılır belgeler).</span><span class="sxs-lookup"><span data-stu-id="eb55b-174">hello *--vpn-type* can be *RouteBased* (referred tooas a Dynamic Gateway in some documentation), or *PolicyBased* (referred tooas a Static Gateway in some documentation).</span></span> <span data-ttu-id="eb55b-175">Merhaba, bağlandığınız hello aygıtının belirli toorequirements ayardır.</span><span class="sxs-lookup"><span data-stu-id="eb55b-175">hello setting is specific toorequirements of hello device that you are connecting to.</span></span> <span data-ttu-id="eb55b-176">VPN ağ geçidi türleri hakkında daha fazla bilgi için bkz. [VPN Gateway yapılandırma ayarları hakkında](vpn-gateway-about-vpn-gateway-settings.md#vpntype).</span><span class="sxs-lookup"><span data-stu-id="eb55b-176">For more information about VPN gateway types, see [About VPN Gateway configuration settings](vpn-gateway-about-vpn-gateway-settings.md#vpntype).</span></span>
* <span data-ttu-id="eb55b-177">Merhaba ağ geçidi SKU'su toouse istediğinizi seçin.</span><span class="sxs-lookup"><span data-stu-id="eb55b-177">Select hello Gateway SKU that you want toouse.</span></span> <span data-ttu-id="eb55b-178">Bazı SKU’larda yapılandırma sınırlamaları vardır.</span><span class="sxs-lookup"><span data-stu-id="eb55b-178">There are configuration limitations for certain SKUs.</span></span> <span data-ttu-id="eb55b-179">Daha fazla bilgi için bkz. [Ağ geçidi SKU'ları](vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span><span class="sxs-lookup"><span data-stu-id="eb55b-179">For more information, see [Gateway SKUs](vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span></span>

<span data-ttu-id="eb55b-180">Hello kullanarak hello VPN ağ geçidi oluşturmak [az ağ sanal ağ geçidi oluşturma](/cli/azure/network/vnet-gateway#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="eb55b-180">Create hello VPN gateway using hello [az network vnet-gateway create](/cli/azure/network/vnet-gateway#create) command.</span></span> <span data-ttu-id="eb55b-181">'Wait--yok-' parametresi hello kullanarak bu komutu çalıştırırsanız, herhangi bir geri bildirim veya çıkış görmüyorum.</span><span class="sxs-lookup"><span data-stu-id="eb55b-181">If you run this command using hello '--no-wait' parameter, you don't see any feedback or output.</span></span> <span data-ttu-id="eb55b-182">Bu parametre hello ağ geçidi toocreate hello arka planda sağlar.</span><span class="sxs-lookup"><span data-stu-id="eb55b-182">This parameter allows hello gateway toocreate in hello background.</span></span> <span data-ttu-id="eb55b-183">Bir ağ geçidi toocreate yaklaşık 45 dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="eb55b-183">It takes around 45 minutes toocreate a gateway.</span></span>

```azurecli
az network vnet-gateway create --name VNet1GW --public-ip-address VNet1GWIP --resource-group TestRG1 --vnet TestVNet1 --gateway-type Vpn --vpn-type RouteBased --sku VpnGw1 --no-wait 
```

## <span data-ttu-id="eb55b-184"><a name="VPNDevice"></a>8. VPN cihazınızı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="eb55b-184"><a name="VPNDevice"></a>8. Configure your VPN device</span></span>

<span data-ttu-id="eb55b-185">Siteden siteye bağlantıları tooan şirket içi ağ bir VPN cihazı gerektirir.</span><span class="sxs-lookup"><span data-stu-id="eb55b-185">Site-to-Site connections tooan on-premises network require a VPN device.</span></span> <span data-ttu-id="eb55b-186">Bu adımda VPN cihazınızı yapılandıracaksınız.</span><span class="sxs-lookup"><span data-stu-id="eb55b-186">In this step, you configure your VPN device.</span></span> <span data-ttu-id="eb55b-187">VPN Cihazınızı yapılandırırken hello aşağıdaki gerekir:</span><span class="sxs-lookup"><span data-stu-id="eb55b-187">When configuring your VPN device, you need hello following:</span></span>

- <span data-ttu-id="eb55b-188">Paylaşılan bir anahtar.</span><span class="sxs-lookup"><span data-stu-id="eb55b-188">A shared key.</span></span> <span data-ttu-id="eb55b-189">Bu olduğu hello aynı paylaşılan siteden siteye VPN bağlantınızı oluştururken belirttiğiniz anahtarı.</span><span class="sxs-lookup"><span data-stu-id="eb55b-189">This is hello same shared key that you specify when creating your Site-to-Site VPN connection.</span></span> <span data-ttu-id="eb55b-190">Bu örneklerde temel bir paylaşılan anahtar kullanılır.</span><span class="sxs-lookup"><span data-stu-id="eb55b-190">In our examples, we use a basic shared key.</span></span> <span data-ttu-id="eb55b-191">Daha karmaşık bir anahtar toouse oluşturmak öneririz.</span><span class="sxs-lookup"><span data-stu-id="eb55b-191">We recommend that you generate a more complex key toouse.</span></span>
- <span data-ttu-id="eb55b-192">Merhaba sanal ağ geçidinizin genel IP adresi.</span><span class="sxs-lookup"><span data-stu-id="eb55b-192">hello Public IP address of your virtual network gateway.</span></span> <span data-ttu-id="eb55b-193">Hello Azure portal, PowerShell veya CLI kullanarak hello ortak IP adresini görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eb55b-193">You can view hello public IP address by using hello Azure portal, PowerShell, or CLI.</span></span> <span data-ttu-id="eb55b-194">sanal ağ geçidinizi kullanın hello toofind hello genel IP adresi [az ağ ortak IP listesi](/cli/azure/network/public-ip#list) komutu.</span><span class="sxs-lookup"><span data-stu-id="eb55b-194">toofind hello public IP address of your virtual network gateway, use hello [az network public-ip list](/cli/azure/network/public-ip#list) command.</span></span> <span data-ttu-id="eb55b-195">Kolay okuma için hello çıkış biçimlendirilmiş toodisplay hello genel IP'ler, tablo biçiminde listesidir.</span><span class="sxs-lookup"><span data-stu-id="eb55b-195">For easy reading, hello output is formatted toodisplay hello list of public IPs in table format.</span></span>

  ```azurecli
  az network public-ip list --resource-group TestRG1 --output table
  ```


[!INCLUDE [Configure VPN device](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]


## <span data-ttu-id="eb55b-196"><a name="CreateConnection"></a>9. Merhaba VPN bağlantısı oluşturun</span><span class="sxs-lookup"><span data-stu-id="eb55b-196"><a name="CreateConnection"></a>9. Create hello VPN connection</span></span>

<span data-ttu-id="eb55b-197">Sanal ağ geçidiniz ve şirket içi VPN aygıtınızın arasında Hello siteden siteye VPN bağlantısı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="eb55b-197">Create hello Site-to-Site VPN connection between your virtual network gateway and your on-premises VPN device.</span></span> <span data-ttu-id="eb55b-198">Yapılandırılmış hello eşleşmelidir ödeme özellikle dikkat toohello paylaşılan anahtar değeri, VPN cihazınız için anahtar değeri paylaşılan.</span><span class="sxs-lookup"><span data-stu-id="eb55b-198">Pay particular attention toohello shared key value, which must match hello configured shared key value for your VPN device.</span></span>

<span data-ttu-id="eb55b-199">Hello kullanarak hello bağlantısı oluşturma [az ağ vpn bağlantısı oluşturmak](/cli/azure/network/vpn-connection#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="eb55b-199">Create hello connection using hello [az network vpn-connection create](/cli/azure/network/vpn-connection#create) command.</span></span>

```azurecli
az network vpn-connection create --name VNet1toSite2 -resource-group TestRG1 --vnet-gateway1 VNet1GW -l eastus --shared-key abc123 --local-gateway2 Site2
```

<span data-ttu-id="eb55b-200">Kısa bir süre, hello bağlantı kurulur.</span><span class="sxs-lookup"><span data-stu-id="eb55b-200">After a short while, hello connection will be established.</span></span>

## <span data-ttu-id="eb55b-201"><a name="toverify"></a>10. Merhaba VPN bağlantısını doğrulama</span><span class="sxs-lookup"><span data-stu-id="eb55b-201"><a name="toverify"></a>10. Verify hello VPN connection</span></span>

[!INCLUDE [verify connection](../../includes/vpn-gateway-verify-connection-cli-rm-include.md)]

<span data-ttu-id="eb55b-202">Başka bir yöntem tooverify toouse istiyorsanız, bağlantınızı bkz [bir VPN ağ geçidi bağlantısını doğrulama](vpn-gateway-verify-connection-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="eb55b-202">If you want toouse another method tooverify your connection, see [Verify a VPN Gateway connection](vpn-gateway-verify-connection-resource-manager.md).</span></span>

## <span data-ttu-id="eb55b-203"><a name="connectVM"></a>tooconnect tooa sanal makine</span><span class="sxs-lookup"><span data-stu-id="eb55b-203"><a name="connectVM"></a>tooconnect tooa virtual machine</span></span>

[!INCLUDE [Connect tooa VM](../../includes/vpn-gateway-connect-vm-s2s-include.md)]

## <span data-ttu-id="eb55b-204"><a name="tasks"></a>Genel görevler</span><span class="sxs-lookup"><span data-stu-id="eb55b-204"><a name="tasks"></a>Common tasks</span></span>

<span data-ttu-id="eb55b-205">Bu bölüm, siteden siteye yapılandırmalarla çalışırken yararlı olan genel komutları içerir.</span><span class="sxs-lookup"><span data-stu-id="eb55b-205">This section contains common commands that are helpful when working with site-to-site configurations.</span></span> <span data-ttu-id="eb55b-206">Merhaba tam CLI ağ komutların listesi için bkz: [Azure CLI - ağ](/cli/azure/network).</span><span class="sxs-lookup"><span data-stu-id="eb55b-206">For hello full list of CLI networking commands, see [Azure CLI - Networking](/cli/azure/network).</span></span>

[!INCLUDE [local network gateway common tasks](../../includes/vpn-gateway-common-tasks-cli-include.md)]

## <a name="next-steps"></a><span data-ttu-id="eb55b-207">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="eb55b-207">Next steps</span></span>

* <span data-ttu-id="eb55b-208">Bağlantınız tamamlandıktan sonra sanal makineleri tooyour sanal ağları ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eb55b-208">Once your connection is complete, you can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="eb55b-209">Daha fazla bilgi için bkz. [Sanal Makineler](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span><span class="sxs-lookup"><span data-stu-id="eb55b-209">For more information, see [Virtual Machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span></span>
* <span data-ttu-id="eb55b-210">BGP hakkında daha fazla bilgi için bkz: Merhaba [BGP genel bakış](vpn-gateway-bgp-overview.md) ve [nasıl tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span><span class="sxs-lookup"><span data-stu-id="eb55b-210">For information about BGP, see hello [BGP Overview](vpn-gateway-bgp-overview.md) and [How tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span></span>
* <span data-ttu-id="eb55b-211">Zorlamalı Tünel Oluşturma hakkında bilgi için bkz. [Zorlamalı Tünel Oluşturma Hakkında](vpn-gateway-forced-tunneling-rm.md).</span><span class="sxs-lookup"><span data-stu-id="eb55b-211">For information about Forced Tunneling, see [About Forced Tunneling](vpn-gateway-forced-tunneling-rm.md).</span></span>
* <span data-ttu-id="eb55b-212">Yüksek Oranda Kullanılabilir Etkin-Etkin bağlantılar hakkında bilgi için bkz. [Yüksek Oranda Kullanılabilir Şirket İçi ve Dışı ile Sanal Ağdan Sanal Ağa Bağlantı](vpn-gateway-highlyavailable.md).</span><span class="sxs-lookup"><span data-stu-id="eb55b-212">For information about Highly Available Active-Active connections, see [Highly Available cross-premises and VNet-to-VNet connectivity](vpn-gateway-highlyavailable.md).</span></span>
* <span data-ttu-id="eb55b-213">Ağ Azure CLI komutlarının listesi için bkz. [Azure CLI](https://docs.microsoft.com/cli/azure/network).</span><span class="sxs-lookup"><span data-stu-id="eb55b-213">For a list of networking Azure CLI commands, see [Azure CLI](https://docs.microsoft.com/cli/azure/network).</span></span>