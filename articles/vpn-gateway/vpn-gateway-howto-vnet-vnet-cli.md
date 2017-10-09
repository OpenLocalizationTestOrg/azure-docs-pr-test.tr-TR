---
title: "Sanal ağ tooanother VNet bağlanın: Azure CLI | Microsoft Docs"
description: "Bu makalede, Azure Resource Manager ve Azure CLI kullanarak sanal ağları birbirine bağlama konusu incelenmektedir."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 0683c664-9c03-40a4-b198-a6529bf1ce8b
ms.service: vpn-gateway
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/02/2017
ms.author: cherylmc
ms.openlocfilehash: 70113914bcae03c80f9ad133ff081d1cf37fc309
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-vnet-to-vnet-vpn-gateway-connection-using-azure-cli"></a><span data-ttu-id="977a4-103">Azure CLI kullanarak sanal ağlar arası VPN ağ geçidi bağlantısı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="977a4-103">Configure a VNet-to-VNet VPN gateway connection using Azure CLI</span></span>

<span data-ttu-id="977a4-104">Bu makale size nasıl gösterir toocreate sanal ağlar arasında bir VPN ağ geçidi bağlantısı.</span><span class="sxs-lookup"><span data-stu-id="977a4-104">This article shows you how toocreate a VPN gateway connection between virtual networks.</span></span> <span data-ttu-id="977a4-105">Merhaba sanal ağları olabilir hello aynı ya da farklı bölgelerde ve gelen aynı hello ya da farklı Aboneliklerde.</span><span class="sxs-lookup"><span data-stu-id="977a4-105">hello virtual networks can be in hello same or different regions, and from hello same or different subscriptions.</span></span> <span data-ttu-id="977a4-106">Bağlanan sanal ağlar farklı aboneliklerden hello abonelikleri ile ilişkili toobe gerekmediğinde aynı Active Directory Kiracı hello.</span><span class="sxs-lookup"><span data-stu-id="977a4-106">When connecting VNets from different subscriptions, hello subscriptions do not need toobe associated with hello same Active Directory tenant.</span></span> 

<span data-ttu-id="977a4-107">Bu makaledeki adımları Hello toohello Resource Manager dağıtım modeli uygulayın ve Azure CLI kullanın.</span><span class="sxs-lookup"><span data-stu-id="977a4-107">hello steps in this article apply toohello Resource Manager deployment model and use Azure CLI.</span></span> <span data-ttu-id="977a4-108">Liste aşağıdaki hello farklı bir seçeneği seçerek farklı dağıtım aracını veya dağıtım modelini kullanarak bu yapılandırma ayrıca oluşturabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="977a4-108">You can also create this configuration using a different deployment tool or deployment model by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="977a4-109">Azure portal</span><span class="sxs-lookup"><span data-stu-id="977a4-109">Azure portal</span></span>](vpn-gateway-howto-vnet-vnet-resource-manager-portal.md)
> * [<span data-ttu-id="977a4-110">PowerShell</span><span class="sxs-lookup"><span data-stu-id="977a4-110">PowerShell</span></span>](vpn-gateway-vnet-vnet-rm-ps.md)
> * [<span data-ttu-id="977a4-111">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="977a4-111">Azure CLI</span></span>](vpn-gateway-howto-vnet-vnet-cli.md)
> * [<span data-ttu-id="977a4-112">Azure portal (klasik)</span><span class="sxs-lookup"><span data-stu-id="977a4-112">Azure portal (classic)</span></span>](vpn-gateway-howto-vnet-vnet-portal-classic.md)
> * [<span data-ttu-id="977a4-113">Farklı dağıtım modellerini bağlama - Azure portalı</span><span class="sxs-lookup"><span data-stu-id="977a4-113">Connect different deployment models - Azure portal</span></span>](vpn-gateway-connect-different-deployment-models-portal.md)
> * [<span data-ttu-id="977a4-114">Farklı dağıtım modellerini bağlama - PowerShell</span><span class="sxs-lookup"><span data-stu-id="977a4-114">Connect different deployment models - PowerShell</span></span>](vpn-gateway-connect-different-deployment-models-powershell.md)
>
>

<span data-ttu-id="977a4-115">Sanal ağ tooanother sanal ağ (VNet-VNet) bağlanma benzer tooconnecting bir VNet tooan şirket içi site konumu değil.</span><span class="sxs-lookup"><span data-stu-id="977a4-115">Connecting a virtual network tooanother virtual network (VNet-to-VNet) is similar tooconnecting a VNet tooan on-premises site location.</span></span> <span data-ttu-id="977a4-116">Her iki bağlantı türü bir VPN ağ geçidi tooprovide IPSec/IKE kullanarak güvenli bir tünel kullanın.</span><span class="sxs-lookup"><span data-stu-id="977a4-116">Both connectivity types use a VPN gateway tooprovide a secure tunnel using IPsec/IKE.</span></span> <span data-ttu-id="977a4-117">Sanal ağlar hello varsa aynı bölgede VNet eşlemesi kullanarak bunları bağlanma tooconsider isteyebilir.</span><span class="sxs-lookup"><span data-stu-id="977a4-117">If your VNets are in hello same region, you may want tooconsider connecting them using VNet Peering.</span></span> <span data-ttu-id="977a4-118">VNet eşlemesi VPN ağ geçidini kullanmaz.</span><span class="sxs-lookup"><span data-stu-id="977a4-118">VNet peering does not use a VPN gateway.</span></span> <span data-ttu-id="977a4-119">Daha fazla bilgi için bkz. [VNet eşlemesi](../virtual-network/virtual-network-peering-overview.md).</span><span class="sxs-lookup"><span data-stu-id="977a4-119">For more information, see [VNet peering](../virtual-network/virtual-network-peering-overview.md).</span></span>

<span data-ttu-id="977a4-120">Hatta Sanal Ağdan Sanal Ağa iletişim çok siteli yapılandırmalarla bile birleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="977a4-120">VNet-to-VNet communication can be combined with multi-site configurations.</span></span> <span data-ttu-id="977a4-121">Hello Aşağıdaki diyagramda gösterildiği gibi arası sanal ağ bağlantısı ile şirket içi bağlantılar birleştiren ağ topolojileri kurabilmenize olanak sağlar:</span><span class="sxs-lookup"><span data-stu-id="977a4-121">This lets you establish network topologies that combine cross-premises connectivity with inter-virtual network connectivity, as shown in hello following diagram:</span></span>

![Bağlantılar hakkında](./media/vpn-gateway-howto-vnet-vnet-cli/aboutconnections.png)

### <span data-ttu-id="977a4-123"><a name="why"></a>Sanal ağları neden bağlamalıyız?</span><span class="sxs-lookup"><span data-stu-id="977a4-123"><a name="why"></a>Why connect virtual networks?</span></span>

<span data-ttu-id="977a4-124">Aşağıdaki nedenlerden Merhaba tooconnect sanal ağlar isteyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="977a4-124">You may want tooconnect virtual networks for hello following reasons:</span></span>

* <span data-ttu-id="977a4-125">**Çapraz bölge coğrafi artıklığı ve coğrafi-durum**</span><span class="sxs-lookup"><span data-stu-id="977a4-125">**Cross region geo-redundancy and geo-presence**</span></span>

  * <span data-ttu-id="977a4-126">Kendi coğrafi çoğaltma veya eşitlemenizi, güvenli bağlantıyla İnternet’te uç noktalara gitmeden ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="977a4-126">You can set up your own geo-replication or synchronization with secure connectivity without going over Internet-facing endpoints.</span></span>
  * <span data-ttu-id="977a4-127">Azure Traffic Manager ve Load Balancer ile birçok Azure bölgesinde coğrafi yedeklilik imkanıyla yüksek oranda kullanılabilir iş yükü oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="977a4-127">With Azure Traffic Manager and Load Balancer, you can set up highly available workload with geo-redundancy across multiple Azure regions.</span></span> <span data-ttu-id="977a4-128">Bir önemli SQL Always On kullanılabilirlik grupları: birden fazla Azure bölgesine yayılan ile yukarı tooset örnektir.</span><span class="sxs-lookup"><span data-stu-id="977a4-128">One important example is tooset up SQL Always On with Availability Groups spreading across multiple Azure regions.</span></span>
* <span data-ttu-id="977a4-129">**Yalıtım veya yönetim sınır bölgesel çok katmanlı uygulamalar**</span><span class="sxs-lookup"><span data-stu-id="977a4-129">**Regional multi-tier applications with isolation or administrative boundary**</span></span>

  * <span data-ttu-id="977a4-130">İçinde hello aynı bölge tooisolation ya da yönetim gereksinimleri birbirlerine bağlı birden çok sanal ağ ile çok katmanlı uygulamalar ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="977a4-130">Within hello same region, you can set up multi-tier applications with multiple virtual networks connected together due tooisolation or administrative requirements.</span></span>

<span data-ttu-id="977a4-131">VNet-VNet bağlantıları hakkında daha fazla bilgi için bkz: Merhaba [VNet-VNet ile ilgili SSS](#faq) hello bu makalenin sonunda.</span><span class="sxs-lookup"><span data-stu-id="977a4-131">For more information about VNet-to-VNet connections, see hello [VNet-to-VNet FAQ](#faq) at hello end of this article.</span></span>

### <a name="which-set-of-steps-should-i-use"></a><span data-ttu-id="977a4-132">Hangi adımları tamamlamalıyım? </span><span class="sxs-lookup"><span data-stu-id="977a4-132">Which set of steps should I use?</span></span>

<span data-ttu-id="977a4-133">Bu makalede iki farklı adım kümesi görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="977a4-133">In this article, you see two different sets of steps.</span></span> <span data-ttu-id="977a4-134">Adımlar için bir dizi [içinde bulunan sanal ağlar aynı abonelik hello](#samesub), diğeri [farklı Aboneliklerde bulunan sanal ağlar](#difsub).</span><span class="sxs-lookup"><span data-stu-id="977a4-134">One set of steps for [VNets that reside in hello same subscription](#samesub), and another for [VNets that reside in different subscriptions](#difsub).</span></span>

## <span data-ttu-id="977a4-135"><a name="samesub"></a>Hello olan sanal ağlara bağlantı aynı abonelik</span><span class="sxs-lookup"><span data-stu-id="977a4-135"><a name="samesub"></a>Connect VNets that are in hello same subscription</span></span>

![v2v diyagramı](./media/vpn-gateway-howto-vnet-vnet-cli/v2vrmps.png)

### <a name="before-you-begin"></a><span data-ttu-id="977a4-137">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="977a4-137">Before you begin</span></span>

<span data-ttu-id="977a4-138">Başlamadan önce hello hello CLI komutları (2.0 veya üstü) en son sürümünü yükleyin.</span><span class="sxs-lookup"><span data-stu-id="977a4-138">Before beginning, install hello latest version of hello CLI commands (2.0 or later).</span></span> <span data-ttu-id="977a4-139">Merhaba CLI komutları yükleme hakkında daha fazla bilgi için bkz: [Azure CLI 2.0 yükleme](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="977a4-139">For information about installing hello CLI commands, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span>

### <span data-ttu-id="977a4-140"><a name="Plan"></a>IP adresi aralıklarınızı planlama</span><span class="sxs-lookup"><span data-stu-id="977a4-140"><a name="Plan"></a>Plan your IP address ranges</span></span>

<span data-ttu-id="977a4-141">Aşağıdaki adımları hello, kullanıcıların kendi ağ geçidi alt ağları ve yapılandırmalarıyla birlikte iki sanal ağ oluşturun.</span><span class="sxs-lookup"><span data-stu-id="977a4-141">In hello following steps, we create two virtual networks along with their respective gateway subnets and configurations.</span></span> <span data-ttu-id="977a4-142">Ardından hello arasında bir VPN bağlantısı iki Vnet oluşturuyoruz.</span><span class="sxs-lookup"><span data-stu-id="977a4-142">We then create a VPN connection between hello two VNets.</span></span> <span data-ttu-id="977a4-143">Önemli tooplan başlangıç IP adresi aralıklarını ağ yapılandırmanızı olur.</span><span class="sxs-lookup"><span data-stu-id="977a4-143">It’s important tooplan hello IP address ranges for your network configuration.</span></span> <span data-ttu-id="977a4-144">Sanal ağ aralıklarınızın ya da yerel ağ aralıklarınızın hiçbir şekilde çakışmadığından emin olmalısınız.</span><span class="sxs-lookup"><span data-stu-id="977a4-144">Keep in mind that you must make sure that none of your VNet ranges or local network ranges overlap in any way.</span></span> <span data-ttu-id="977a4-145">Bu örneklerde bir DNS sunucusu eklemiyoruz.</span><span class="sxs-lookup"><span data-stu-id="977a4-145">In these examples, we do not include a DNS server.</span></span> <span data-ttu-id="977a4-146">Sanal ağlarınız için ad çözümlemesi istiyorsanız bkz. [Ad çözümlemesi](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span><span class="sxs-lookup"><span data-stu-id="977a4-146">If you want name resolution for your virtual networks, see [Name resolution](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span></span>

<span data-ttu-id="977a4-147">Merhaba örnekleri değerleri aşağıdaki hello kullanırız:</span><span class="sxs-lookup"><span data-stu-id="977a4-147">We use hello following values in hello examples:</span></span>

<span data-ttu-id="977a4-148">**Değerler TestVNet1 için:**</span><span class="sxs-lookup"><span data-stu-id="977a4-148">**Values for TestVNet1:**</span></span>

* <span data-ttu-id="977a4-149">VNet Name: TestVNet1</span><span class="sxs-lookup"><span data-stu-id="977a4-149">VNet Name: TestVNet1</span></span>
* <span data-ttu-id="977a4-150">Resource Group: TestRG1</span><span class="sxs-lookup"><span data-stu-id="977a4-150">Resource Group: TestRG1</span></span>
* <span data-ttu-id="977a4-151">Location: East US</span><span class="sxs-lookup"><span data-stu-id="977a4-151">Location: East US</span></span>
* <span data-ttu-id="977a4-152">TestVNet1: 10.11.0.0/16 & 10.12.0.0/16</span><span class="sxs-lookup"><span data-stu-id="977a4-152">TestVNet1: 10.11.0.0/16 & 10.12.0.0/16</span></span>
* <span data-ttu-id="977a4-153">FrontEnd: 10.11.0.0/24</span><span class="sxs-lookup"><span data-stu-id="977a4-153">FrontEnd: 10.11.0.0/24</span></span>
* <span data-ttu-id="977a4-154">BackEnd: 10.12.0.0/24</span><span class="sxs-lookup"><span data-stu-id="977a4-154">BackEnd: 10.12.0.0/24</span></span>
* <span data-ttu-id="977a4-155">GatewaySubnet: 10.12.255.0/27</span><span class="sxs-lookup"><span data-stu-id="977a4-155">GatewaySubnet: 10.12.255.0/27</span></span>
* <span data-ttu-id="977a4-156">GatewayName: VNet1GW</span><span class="sxs-lookup"><span data-stu-id="977a4-156">GatewayName: VNet1GW</span></span>
* <span data-ttu-id="977a4-157">Public IP: VNet1GWIP</span><span class="sxs-lookup"><span data-stu-id="977a4-157">Public IP: VNet1GWIP</span></span>
* <span data-ttu-id="977a4-158">VPNType: RouteBased</span><span class="sxs-lookup"><span data-stu-id="977a4-158">VPNType: RouteBased</span></span>
* <span data-ttu-id="977a4-159">Connection(1to4): VNet1toVNet4</span><span class="sxs-lookup"><span data-stu-id="977a4-159">Connection(1to4): VNet1toVNet4</span></span>
* <span data-ttu-id="977a4-160">Connection(1to5): VNet1toVNet5</span><span class="sxs-lookup"><span data-stu-id="977a4-160">Connection(1to5): VNet1toVNet5</span></span>
* <span data-ttu-id="977a4-161">ConnectionType: VNet2VNet</span><span class="sxs-lookup"><span data-stu-id="977a4-161">ConnectionType: VNet2VNet</span></span>

<span data-ttu-id="977a4-162">**Değerler TestVNet4 için:**</span><span class="sxs-lookup"><span data-stu-id="977a4-162">**Values for TestVNet4:**</span></span>

* <span data-ttu-id="977a4-163">VNet Name: TestVNet4</span><span class="sxs-lookup"><span data-stu-id="977a4-163">VNet Name: TestVNet4</span></span>
* <span data-ttu-id="977a4-164">TestVNet2: 10.41.0.0/16 & 10.42.0.0/16</span><span class="sxs-lookup"><span data-stu-id="977a4-164">TestVNet2: 10.41.0.0/16 & 10.42.0.0/16</span></span>
* <span data-ttu-id="977a4-165">FrontEnd: 10.41.0.0/24</span><span class="sxs-lookup"><span data-stu-id="977a4-165">FrontEnd: 10.41.0.0/24</span></span>
* <span data-ttu-id="977a4-166">BackEnd: 10.42.0.0/24</span><span class="sxs-lookup"><span data-stu-id="977a4-166">BackEnd: 10.42.0.0/24</span></span>
* <span data-ttu-id="977a4-167">GatewaySubnet: 10.42.255.0/27</span><span class="sxs-lookup"><span data-stu-id="977a4-167">GatewaySubnet: 10.42.255.0/27</span></span>
* <span data-ttu-id="977a4-168">Resource Group: TestRG4</span><span class="sxs-lookup"><span data-stu-id="977a4-168">Resource Group: TestRG4</span></span>
* <span data-ttu-id="977a4-169">Location: West US</span><span class="sxs-lookup"><span data-stu-id="977a4-169">Location: West US</span></span>
* <span data-ttu-id="977a4-170">GatewayName: VNet4GW</span><span class="sxs-lookup"><span data-stu-id="977a4-170">GatewayName: VNet4GW</span></span>
* <span data-ttu-id="977a4-171">Public IP: VNet4GWIP</span><span class="sxs-lookup"><span data-stu-id="977a4-171">Public IP: VNet4GWIP</span></span>
* <span data-ttu-id="977a4-172">VPNType: RouteBased</span><span class="sxs-lookup"><span data-stu-id="977a4-172">VPNType: RouteBased</span></span>
* <span data-ttu-id="977a4-173">Connection: VNet4toVNet1</span><span class="sxs-lookup"><span data-stu-id="977a4-173">Connection: VNet4toVNet1</span></span>
* <span data-ttu-id="977a4-174">ConnectionType: VNet2VNet</span><span class="sxs-lookup"><span data-stu-id="977a4-174">ConnectionType: VNet2VNet</span></span>


### <span data-ttu-id="977a4-175"><a name="Connect"></a>1. adım - tooyour. abonelik'e bağlanma</span><span class="sxs-lookup"><span data-stu-id="977a4-175"><a name="Connect"></a>Step 1 - Connect tooyour subscription</span></span>

[!INCLUDE [CLI login](../../includes/vpn-gateway-cli-login-numbers-include.md)]

### <span data-ttu-id="977a4-176"><a name="TestVNet1"></a>Adım 2 - oluşturma ve TestVNet1 yapılandırma</span><span class="sxs-lookup"><span data-stu-id="977a4-176"><a name="TestVNet1"></a>Step 2 - Create and configure TestVNet1</span></span>

1. <span data-ttu-id="977a4-177">Bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="977a4-177">Create a resource group.</span></span>

  ```azurecli
  az group create -n TestRG1  -l eastus
  ```
2. <span data-ttu-id="977a4-178">TestVNet1 için TestVNet1 ve hello alt ağlar oluşturun.</span><span class="sxs-lookup"><span data-stu-id="977a4-178">Create TestVNet1 and hello subnets for TestVNet1.</span></span> <span data-ttu-id="977a4-179">Bu örnekte, TestVNet1 adlı bir sanal ağ ve FrontEnd adlı bir alt ağ oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="977a4-179">This example creates a virtual network named TestVNet1 and a subnet named FrontEnd.</span></span>

  ```azurecli
  az network vnet create -n TestVNet1 -g TestRG1 --address-prefix 10.11.0.0/16 -l eastus --subnet-name FrontEnd --subnet-prefix 10.11.0.0/24
  ```
3. <span data-ttu-id="977a4-180">Merhaba arka uç alt ağ için ek adres alanı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="977a4-180">Create an additional address space for hello backend subnet.</span></span> <span data-ttu-id="977a4-181">Bu adımda, biz daha önce oluşturduğumuz iki hello adres alanını belirtin ve ek adres alanı tooadd istiyoruz Merhaba, dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="977a4-181">Notice that in this step, we specify both hello address space that we created earlier, and hello additional address space that we want tooadd.</span></span> <span data-ttu-id="977a4-182">Bunun nedeni, hello [az ağ vnet güncelleştirmesi](https://docs.microsoft.com/cli/azure/network/vnet#update) komutu hello önceki ayarların üzerine yazar.</span><span class="sxs-lookup"><span data-stu-id="977a4-182">This is because hello [az network vnet update](https://docs.microsoft.com/cli/azure/network/vnet#update) command overwrites hello previous settings.</span></span> <span data-ttu-id="977a4-183">Emin toospecify tüm hello adres öneklerinin bu komutunu kullanırken olun.</span><span class="sxs-lookup"><span data-stu-id="977a4-183">Make sure toospecify all of hello address prefixes when using this command.</span></span>

  ```azurecli
  az network vnet update -n TestVNet1 --address-prefixes 10.11.0.0/16 10.12.0.0/16 -g TestRG1
  ```
4. <span data-ttu-id="977a4-184">Merhaba arka uç alt ağ oluşturun.</span><span class="sxs-lookup"><span data-stu-id="977a4-184">Create hello backend subnet.</span></span>
  
  ```azurecli
  az network vnet subnet create --vnet-name TestVNet1 -n BackEnd -g TestRG1 --address-prefix 10.12.0.0/24 
  ```
5. <span data-ttu-id="977a4-185">Merhaba ağ geçidi alt ağı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="977a4-185">Create hello gateway subnet.</span></span> <span data-ttu-id="977a4-186">Bu hello ağ geçidi alt ağı 'GatewaySubnet' adlı dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="977a4-186">Notice that hello gateway subnet is named 'GatewaySubnet'.</span></span> <span data-ttu-id="977a4-187">Bu ad gereklidir.</span><span class="sxs-lookup"><span data-stu-id="977a4-187">This name is required.</span></span> <span data-ttu-id="977a4-188">Bu örnekte, hello ağ geçidi alt ağı/27 kullanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="977a4-188">In this example, hello gateway subnet is using a /27.</span></span> <span data-ttu-id="977a4-189">Olası toocreate ağ geçidi alt ağı /29 küçük olmakla birlikte, en az/28 veya /27 seçerek daha fazla adreslerini içeren daha büyük bir alt ağı oluşturmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="977a4-189">While it is possible toocreate a gateway subnet as small as /29, we recommend that you create a larger subnet that includes more addresses by selecting at least /28 or /27.</span></span> <span data-ttu-id="977a4-190">Bu, gelecekteki hello isteyebileceğiniz yeterli adresleri tooaccommodate olası ek yapılandırmalar için izin verir.</span><span class="sxs-lookup"><span data-stu-id="977a4-190">This will allow for enough addresses tooaccommodate possible additional configurations that you may want in hello future.</span></span>

  ```azurecli 
  az network vnet subnet create --vnet-name TestVNet1 -n GatewaySubnet -g TestRG1 --address-prefix 10.12.255.0/27
  ```
6. <span data-ttu-id="977a4-191">Ağınız için oluşturacağınız bir ortak IP adresi toobe ayrılmış toohello ağ geçidi isteği.</span><span class="sxs-lookup"><span data-stu-id="977a4-191">Request a public IP address toobe allocated toohello gateway you will create for your VNet.</span></span> <span data-ttu-id="977a4-192">Bu hello AllocationMethod dinamik olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="977a4-192">Notice that hello AllocationMethod is Dynamic.</span></span> <span data-ttu-id="977a4-193">Başlangıç IP adresi toouse istediğiniz belirtemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="977a4-193">You cannot specify hello IP address that you want toouse.</span></span> <span data-ttu-id="977a4-194">Dinamik olarak ayrılan tooyour geçididir.</span><span class="sxs-lookup"><span data-stu-id="977a4-194">It's dynamically allocated tooyour gateway.</span></span>

  ```azurecli
  az network public-ip create -n VNet1GWIP -g TestRG1 --allocation-method Dynamic
  ```
7. <span data-ttu-id="977a4-195">TestVNet1 için Hello sanal ağ geçidi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="977a4-195">Create hello virtual network gateway for TestVNet1.</span></span> <span data-ttu-id="977a4-196">Sanal Ağdan Sanal Ağa yapılandırmaları, RouteBased bir VPNType gerektirir.</span><span class="sxs-lookup"><span data-stu-id="977a4-196">VNet-to-VNet configurations require a RouteBased VpnType.</span></span> <span data-ttu-id="977a4-197">'Wait--yok-' parametresi hello kullanarak bu komutu çalıştırırsanız, herhangi bir geri bildirim veya çıkış görmüyorum.</span><span class="sxs-lookup"><span data-stu-id="977a4-197">If you run this command using hello '--no-wait' parameter, you don't see any feedback or output.</span></span> <span data-ttu-id="977a4-198">Merhaba 'wait--yok-' parametresi hello ağ geçidi toocreate hello arka planda izin verir.</span><span class="sxs-lookup"><span data-stu-id="977a4-198">hello '--no-wait' parameter allows hello gateway toocreate in hello background.</span></span> <span data-ttu-id="977a4-199">Bu hello VPN ağ geçidi hemen oluşturmayı tamamladığında anlamına gelmez.</span><span class="sxs-lookup"><span data-stu-id="977a4-199">It does not mean that hello VPN gateway finishes creating immediately.</span></span> <span data-ttu-id="977a4-200">Bir ağ geçidi oluşturma 45 dakika veya daha fazla hello ağ geçidi kullandığınız SKU bağlı olarak genellikle alabilir.</span><span class="sxs-lookup"><span data-stu-id="977a4-200">Creating a gateway can often take 45 minutes or more, depending on hello gateway SKU that you use.</span></span>

  ```azurecli
  az network vnet-gateway create -n VNet1GW -l eastus --public-ip-address VNet1GWIP -g TestRG1 --vnet TestVNet1 --gateway-type Vpn --sku VpnGw1 --vpn-type RouteBased --no-wait
  ```

### <span data-ttu-id="977a4-201"><a name="TestVNet4"></a>3. Adım - TestVNet4’ü oluşturma ve yapılandırma</span><span class="sxs-lookup"><span data-stu-id="977a4-201"><a name="TestVNet4"></a>Step 3 - Create and configure TestVNet4</span></span>

1. <span data-ttu-id="977a4-202">Bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="977a4-202">Create a resource group.</span></span>

  ```azurecli
  az group create -n TestRG4  -l westus
  ```
2. <span data-ttu-id="977a4-203">TestVNet4’ü oluşturun.</span><span class="sxs-lookup"><span data-stu-id="977a4-203">Create TestVNet4.</span></span>

  ```azurecli
  az network vnet create -n TestVNet4 -g TestRG4 --address-prefix 10.41.0.0/16 -l westus --subnet-name FrontEnd --subnet-prefix 10.41.0.0/24
  ```

3. <span data-ttu-id="977a4-204">TestVNet4 için ek alt ağlar oluşturun.</span><span class="sxs-lookup"><span data-stu-id="977a4-204">Create additional subnets for TestVNet4.</span></span>

  ```azurecli
  az network vnet update -n TestVNet4 --address-prefixes 10.41.0.0/16 10.42.0.0/16 -g TestRG4 
  az network vnet subnet create --vnet-name TestVNet4 -n BackEnd -g TestRG4 --address-prefix 10.42.0.0/24 
  ```
4. <span data-ttu-id="977a4-205">Merhaba ağ geçidi alt ağı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="977a4-205">Create hello gateway subnet.</span></span>

  ```azurecli
   az network vnet subnet create --vnet-name TestVNet4 -n GatewaySubnet -g TestRG4 --address-prefix 10.42.255.0/27
  ```
5. <span data-ttu-id="977a4-206">Bir Genel IP adresi isteyin.</span><span class="sxs-lookup"><span data-stu-id="977a4-206">Request a Public IP address.</span></span>

  ```azurecli
  az network public-ip create -n VNet4GWIP -g TestRG4 --allocation-method Dynamic
  ```
6. <span data-ttu-id="977a4-207">Merhaba TestVNet4 sanal ağ geçidi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="977a4-207">Create hello TestVNet4 virtual network gateway.</span></span>

  ```azurecli
  az network vnet-gateway create -n VNet4GW -l westus --public-ip-address VNet4GWIP -g TestRG4 --vnet TestVNet4 --gateway-type Vpn --sku VpnGw1 --vpn-type RouteBased --no-wait
  ```

### <span data-ttu-id="977a4-208"><a name="createconnect"></a>4. adım - hello bağlantıları oluşturma</span><span class="sxs-lookup"><span data-stu-id="977a4-208"><a name="createconnect"></a>Step 4 - Create hello connections</span></span>

<span data-ttu-id="977a4-209">Artık VPN ağ geçitleri olan iki sanal ağınız var.</span><span class="sxs-lookup"><span data-stu-id="977a4-209">You now have two VNets with VPN gateways.</span></span> <span data-ttu-id="977a4-210">Merhaba sonraki hello sanal ağ geçitleri arasında toocreate VPN ağ geçidi bağlantıları adımdır.</span><span class="sxs-lookup"><span data-stu-id="977a4-210">hello next step is toocreate VPN gateway connections between hello virtual network gateways.</span></span> <span data-ttu-id="977a4-211">Merhaba örnekler yukarıdaki kullandıysanız, VNet ağ geçitleri farklı kaynak gruplarında olduğunda.</span><span class="sxs-lookup"><span data-stu-id="977a4-211">If you used hello examples above, your VNet gateways are in different resource groups.</span></span> <span data-ttu-id="977a4-212">Ağ geçitleri farklı kaynak gruplarında olduğunda tooidentify gerekir ve her ağ geçidi için hello kaynak kimlikleri bağlantı kurarken belirtin.</span><span class="sxs-lookup"><span data-stu-id="977a4-212">When gateways are in different resource groups, you need tooidentify and specify hello resource IDs for each gateway when making a connection.</span></span> <span data-ttu-id="977a4-213">Sanal ağlar hello varsa aynı kaynak grubu, hello kullanabilirsiniz [yönergeleri ikinci kümesi](#samerg) toospecify hello kaynak kimlikleri gerektiğinden yok.</span><span class="sxs-lookup"><span data-stu-id="977a4-213">If your VNets are in hello same resource group, you can use hello [second set of instructions](#samerg) because you don't need toospecify hello resource IDs.</span></span>

### <span data-ttu-id="977a4-214"><a name="diffrg"></a>tooconnect farklı kaynak gruplarında bulunan sanal ağlar</span><span class="sxs-lookup"><span data-stu-id="977a4-214"><a name="diffrg"></a>tooconnect VNets that reside in different resource groups</span></span>

1. <span data-ttu-id="977a4-215">Merhaba, kaynak kimliği VNet1GW komutu aşağıdaki hello hello çıktısından alın:</span><span class="sxs-lookup"><span data-stu-id="977a4-215">Get hello Resource ID of VNet1GW from hello output of hello following command:</span></span>

  ```azurecli
  az network vnet-gateway show -n VNet1GW -g TestRG1
  ```

  <span data-ttu-id="977a4-216">Hello çıktısında hello Bul "kimliği:" satır.</span><span class="sxs-lookup"><span data-stu-id="977a4-216">In hello output, find hello "id:" line.</span></span> <span data-ttu-id="977a4-217">Merhaba hello tırnak işareti içinde gerekli toocreate hello bağlantı hello sonraki bölümde değerlerdir.</span><span class="sxs-lookup"><span data-stu-id="977a4-217">hello values within hello quotes are needed toocreate hello connection in hello next section.</span></span> <span data-ttu-id="977a4-218">Böylece, kolayca bunları bağlantınızı oluştururken yapıştırabilirsiniz bu değerleri tooa metin düzenleyici, Not Defteri gibi kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="977a4-218">Copy these values tooa text editor, such as Notepad, so that you can easily paste them when creating your connection.</span></span>

  <span data-ttu-id="977a4-219">Örnek çıktı:</span><span class="sxs-lookup"><span data-stu-id="977a4-219">Example output:</span></span>

  ```
  "activeActive": false, 
  "bgpSettings": { 
    "asn": 65515, 
    "bgpPeeringAddress": "10.12.255.30", 
    "peerWeight": 0 
   }, 
  "enableBgp": false, 
  "etag": "W/\"ecb42bc5-c176-44e1-802f-b0ce2962ac04\"", 
  "gatewayDefaultSite": null, 
  "gatewayType": "Vpn", 
  "id": "/subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW", 
  "ipConfigurations":
  ```

  <span data-ttu-id="977a4-220">Sonra Hello değerleri kopyalamak **"id":** hello tırnak işareti içinde.</span><span class="sxs-lookup"><span data-stu-id="977a4-220">Copy hello values after **"id":** within hello quotes.</span></span>

  ```
  "id": "/subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW"
 ```

2. <span data-ttu-id="977a4-221">Merhaba, kaynak kimliği VNet4GW ve kopyalama hello değerleri tooa metin düzenleyicisi alın.</span><span class="sxs-lookup"><span data-stu-id="977a4-221">Get hello Resource ID of VNet4GW and copy hello values tooa text editor.</span></span>

  ```azurecli
  az network vnet-gateway show -n VNet4GW -g TestRG4
  ```

3. <span data-ttu-id="977a4-222">Merhaba TestVNet1 tooTestVNet4 bağlantı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="977a4-222">Create hello TestVNet1 tooTestVNet4 connection.</span></span> <span data-ttu-id="977a4-223">Bu adımda TestVNet1 tooTestVNet4 hello bağlantı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="977a4-223">In this step, you create hello connection from TestVNet1 tooTestVNet4.</span></span> <span data-ttu-id="977a4-224">Merhaba örneklerde paylaşılan bir anahtarı yok.</span><span class="sxs-lookup"><span data-stu-id="977a4-224">There is a shared key referenced in hello examples.</span></span> <span data-ttu-id="977a4-225">Merhaba paylaşılan anahtar için kendi değerlerinizi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="977a4-225">You can use your own values for hello shared key.</span></span> <span data-ttu-id="977a4-226">Merhaba hello paylaşılan anahtara şeydir önemli hem bağlantılarında eşleşmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="977a4-226">hello important thing is that hello shared key must match for both connections.</span></span> <span data-ttu-id="977a4-227">Bağlantı oluşturma toocomplete sırasında kısa sürer.</span><span class="sxs-lookup"><span data-stu-id="977a4-227">Creating a connection takes a short while toocomplete.</span></span>

  ```azurecli
  az network vpn-connection create -n VNet1ToVNet4 -g TestRG1 --vnet-gateway1 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW -l eastus --shared-key "aabbcc" --vnet-gateway2 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG4/providers/Microsoft.Network/virtualNetworkGateways/VNet4GW 
  ```
4. <span data-ttu-id="977a4-228">Merhaba TestVNet4 tooTestVNet1 bağlantı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="977a4-228">Create hello TestVNet4 tooTestVNet1 connection.</span></span> <span data-ttu-id="977a4-229">TestVNet4 tooTestVNet1 hello bağlantı oluşturma dışında bu benzer toohello yukarıdaki bir adımdır.</span><span class="sxs-lookup"><span data-stu-id="977a4-229">This step is similar toohello one above, except you are creating hello connection from TestVNet4 tooTestVNet1.</span></span> <span data-ttu-id="977a4-230">Merhaba paylaşılan anahtarların eşleştiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="977a4-230">Make sure hello shared keys match.</span></span> <span data-ttu-id="977a4-231">Tooestablish hello bağlantı birkaç dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="977a4-231">It takes a few minutes tooestablish hello connection.</span></span>

  ```azurecli
  az network vpn-connection create -n VNet4ToVNet1 -g TestRG4 --vnet-gateway1 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG4/providers/Microsoft.Network/virtualNetworkGateways/VNet4GW -l westus --shared-key "aabbcc" --vnet-gateway2 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1G
  ```
5. <span data-ttu-id="977a4-232">Bağlantılarınızı doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="977a4-232">Verify your connections.</span></span> <span data-ttu-id="977a4-233">Bkz. [Bağlantınızı doğrulama](#verify).</span><span class="sxs-lookup"><span data-stu-id="977a4-233">See [Verify your connection](#verify).</span></span>

### <span data-ttu-id="977a4-234"><a name="samerg"></a>tooconnect hello aynı bulunan sanal ağlar kaynak grubu</span><span class="sxs-lookup"><span data-stu-id="977a4-234"><a name="samerg"></a>tooconnect VNets that reside in hello same resource group</span></span>

1. <span data-ttu-id="977a4-235">Merhaba TestVNet1 tooTestVNet4 bağlantı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="977a4-235">Create hello TestVNet1 tooTestVNet4 connection.</span></span> <span data-ttu-id="977a4-236">Bu adımda TestVNet1 tooTestVNet4 hello bağlantı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="977a4-236">In this step, you create hello connection from TestVNet1 tooTestVNet4.</span></span> <span data-ttu-id="977a4-237">Bildirim hello kaynak grupları olan hello hello örneklerde aynı.</span><span class="sxs-lookup"><span data-stu-id="977a4-237">Notice hello resource groups are hello same in hello examples.</span></span> <span data-ttu-id="977a4-238">Merhaba örneklerde paylaşılan bir anahtar de görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="977a4-238">You also see a shared key referenced in hello examples.</span></span> <span data-ttu-id="977a4-239">Merhaba paylaşılan anahtar için kendi değerlerinizi kullanabilirsiniz, ancak hello paylaşılan anahtar için her iki bağlantı eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="977a4-239">You can use your own values for hello shared key, however, hello shared key must match for both connections.</span></span> <span data-ttu-id="977a4-240">Bağlantı oluşturma toocomplete sırasında kısa sürer.</span><span class="sxs-lookup"><span data-stu-id="977a4-240">Creating a connection takes a short while toocomplete.</span></span>

  ```azurecli
  az network vpn-connection create -n VNet1ToVNet4 -g TestRG1 --vnet-gateway1 VNet1GW -l eastus --shared-key "eeffgg" --vnet-gateway2 VNet4GW
  ```
2. <span data-ttu-id="977a4-241">Merhaba TestVNet4 tooTestVNet1 bağlantı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="977a4-241">Create hello TestVNet4 tooTestVNet1 connection.</span></span> <span data-ttu-id="977a4-242">TestVNet4 tooTestVNet1 hello bağlantı oluşturma dışında bu benzer toohello yukarıdaki bir adımdır.</span><span class="sxs-lookup"><span data-stu-id="977a4-242">This step is similar toohello one above, except you are creating hello connection from TestVNet4 tooTestVNet1.</span></span> <span data-ttu-id="977a4-243">Merhaba paylaşılan anahtarların eşleştiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="977a4-243">Make sure hello shared keys match.</span></span> <span data-ttu-id="977a4-244">Tooestablish hello bağlantı birkaç dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="977a4-244">It takes a few minutes tooestablish hello connection.</span></span>

  ```azurecli
  az network vpn-connection create -n VNet4ToVNet1 -g TestRG1 --vnet-gateway1 VNet4GW -l eastus --shared-key "eeffgg" --vnet-gateway2 VNet1GW
  ```
3. <span data-ttu-id="977a4-245">Bağlantılarınızı doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="977a4-245">Verify your connections.</span></span> <span data-ttu-id="977a4-246">Bkz. [Bağlantınızı doğrulama](#verify).</span><span class="sxs-lookup"><span data-stu-id="977a4-246">See [Verify your connection](#verify).</span></span>

## <span data-ttu-id="977a4-247"><a name="difsub"></a>Farklı aboneliklerdeki VNet'leri bağlama</span><span class="sxs-lookup"><span data-stu-id="977a4-247"><a name="difsub"></a>Connect VNets that are in different subscriptions</span></span>

![v2v diyagramı](./media/vpn-gateway-howto-vnet-vnet-cli/v2vdiffsub.png)

<span data-ttu-id="977a4-249">Bu senaryoda TestVNet1 ve TestVNet5 bağlanır.</span><span class="sxs-lookup"><span data-stu-id="977a4-249">In this scenario, we connect TestVNet1 and TestVNet5.</span></span> <span data-ttu-id="977a4-250">Merhaba sanal ağlar farklı Aboneliklerde bulunur.</span><span class="sxs-lookup"><span data-stu-id="977a4-250">hello VNets reside different subscriptions.</span></span> <span data-ttu-id="977a4-251">Merhaba abonelikleri hello ile ilişkili toobe gerek yoktur aynı Active Directory kiracısı.</span><span class="sxs-lookup"><span data-stu-id="977a4-251">hello subscriptions do not need toobe associated with hello same Active Directory tenant.</span></span> <span data-ttu-id="977a4-252">Bu yapılandırma için Hello adımları sipariş tooconnect TestVNet1 tooTestVNet5 ek bir VNet-VNet bağlantı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="977a4-252">hello steps for this configuration add an additional VNet-to-VNet connection in order tooconnect TestVNet1 tooTestVNet5.</span></span>

### <span data-ttu-id="977a4-253"><a name="TestVNet1diff"></a>5. Adım - TestVNet1’i oluşturma ve yapılandırma</span><span class="sxs-lookup"><span data-stu-id="977a4-253"><a name="TestVNet1diff"></a>Step 5 - Create and configure TestVNet1</span></span>

<span data-ttu-id="977a4-254">Bu yönergeleri, önceki bölümlerde hello hello adımlardan devam edin.</span><span class="sxs-lookup"><span data-stu-id="977a4-254">These instructions continue from hello steps in hello preceding sections.</span></span> <span data-ttu-id="977a4-255">Tamamlamanız gereken [1. adım](#Connect) ve [2. adım](#TestVNet1) toocreate TestVNet1 yapılandırmak ve VPN ağ geçidi için TestVNet1 hello.</span><span class="sxs-lookup"><span data-stu-id="977a4-255">You must complete [Step 1](#Connect) and [Step 2](#TestVNet1) toocreate and configure TestVNet1 and hello VPN Gateway for TestVNet1.</span></span> <span data-ttu-id="977a4-256">Oluşturursanız, bu adımlara devam çakışmamasını rağmen bu yapılandırma için gerekli toocreate TestVNet4 hello önceki bölümden değildir.</span><span class="sxs-lookup"><span data-stu-id="977a4-256">For this configuration, you are not required toocreate TestVNet4 from hello previous section, although if you do create it, it will not conflict with these steps.</span></span> <span data-ttu-id="977a4-257">1. ve 2. Adımı tamamladıktan sonra 6. Adıma (aşağıda) geçin.</span><span class="sxs-lookup"><span data-stu-id="977a4-257">Once you complete Step 1 and Step 2, continue with Step 6 (below).</span></span>

### <span data-ttu-id="977a4-258"><a name="verifyranges"></a>6. adım - başlangıç IP adresi aralıklarını doğrulama</span><span class="sxs-lookup"><span data-stu-id="977a4-258"><a name="verifyranges"></a>Step 6 - Verify hello IP address ranges</span></span>

<span data-ttu-id="977a4-259">Ek bağlantılar oluştururken, başlangıç IP adresi alanı hello yeni sanal ağın hiçbirini diğer aralıklarınız veya yerel ağ geçidi aralıkları ile çakışmaması önemli tooverify bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="977a4-259">When creating additional connections, it's important tooverify that hello IP address space of hello new virtual network does not overlap with any of your other VNet ranges or local network gateway ranges.</span></span> <span data-ttu-id="977a4-260">Bu alıştırmada, hello TestVNet5 için değerler aşağıdaki hello kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="977a4-260">For this exercise, you can use hello following values for hello TestVNet5:</span></span>

<span data-ttu-id="977a4-261">**Değerler TestVNet5 için:**</span><span class="sxs-lookup"><span data-stu-id="977a4-261">**Values for TestVNet5:**</span></span>

* <span data-ttu-id="977a4-262">VNet Name: TestVNet5</span><span class="sxs-lookup"><span data-stu-id="977a4-262">VNet Name: TestVNet5</span></span>
* <span data-ttu-id="977a4-263">Resource Group: TestRG5</span><span class="sxs-lookup"><span data-stu-id="977a4-263">Resource Group: TestRG5</span></span>
* <span data-ttu-id="977a4-264">Location: Japan East</span><span class="sxs-lookup"><span data-stu-id="977a4-264">Location: Japan East</span></span>
* <span data-ttu-id="977a4-265">TestVNet5: 10.51.0.0/16 & 10.52.0.0/16</span><span class="sxs-lookup"><span data-stu-id="977a4-265">TestVNet5: 10.51.0.0/16 & 10.52.0.0/16</span></span>
* <span data-ttu-id="977a4-266">FrontEnd: 10.51.0.0/24</span><span class="sxs-lookup"><span data-stu-id="977a4-266">FrontEnd: 10.51.0.0/24</span></span>
* <span data-ttu-id="977a4-267">BackEnd: 10.52.0.0/24</span><span class="sxs-lookup"><span data-stu-id="977a4-267">BackEnd: 10.52.0.0/24</span></span>
* <span data-ttu-id="977a4-268">GatewaySubnet: 10.52.255.0.0/27</span><span class="sxs-lookup"><span data-stu-id="977a4-268">GatewaySubnet: 10.52.255.0.0/27</span></span>
* <span data-ttu-id="977a4-269">GatewayName: VNet5GW</span><span class="sxs-lookup"><span data-stu-id="977a4-269">GatewayName: VNet5GW</span></span>
* <span data-ttu-id="977a4-270">Public IP: VNet5GWIP</span><span class="sxs-lookup"><span data-stu-id="977a4-270">Public IP: VNet5GWIP</span></span>
* <span data-ttu-id="977a4-271">VPNType: RouteBased</span><span class="sxs-lookup"><span data-stu-id="977a4-271">VPNType: RouteBased</span></span>
* <span data-ttu-id="977a4-272">Connection: VNet5toVNet1</span><span class="sxs-lookup"><span data-stu-id="977a4-272">Connection: VNet5toVNet1</span></span>
* <span data-ttu-id="977a4-273">ConnectionType: VNet2VNet</span><span class="sxs-lookup"><span data-stu-id="977a4-273">ConnectionType: VNet2VNet</span></span>

### <span data-ttu-id="977a4-274"><a name="TestVNet5"></a>7. Adım - TestVNet5’i oluşturma ve yapılandırma</span><span class="sxs-lookup"><span data-stu-id="977a4-274"><a name="TestVNet5"></a>Step 7 - Create and configure TestVNet5</span></span>

<span data-ttu-id="977a4-275">Bu adım hello hello yeni abonelik, 5. abonelik bağlamında yapılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="977a4-275">This step must be done in hello context of hello new subscription, Subscription 5.</span></span> <span data-ttu-id="977a4-276">Bu bölümü hello aboneliğin sahibi olan farklı bir kuruluşta hello Yöneticisi tarafından gerçekleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="977a4-276">This part may be performed by hello administrator in a different organization that owns hello subscription.</span></span> <span data-ttu-id="977a4-277">Abonelikleri kullanımı arasındaki tooswitch ' az hesabı listesi--tüm ' toolist hello abonelikleri kullanılabilir tooyour hesabı sonra kullanın ' az hesabı kümesi--abonelik <subscriptionID>' toouse istediğiniz tooswitch toohello abonelik.</span><span class="sxs-lookup"><span data-stu-id="977a4-277">tooswitch between subscriptions use 'az account list --all' toolist hello subscriptions available tooyour account, then use 'az account set --subscription <subscriptionID>' tooswitch toohello subscription that you want toouse.</span></span>

1. <span data-ttu-id="977a4-278">Bağlı tooSubscription 5 olan, sonra bir kaynak grubu oluşturmak emin olun.</span><span class="sxs-lookup"><span data-stu-id="977a4-278">Make sure you are connected tooSubscription 5, then create a resource group.</span></span>

  ```azurecli
  az group create -n TestRG5  -l japaneast
  ```
2. <span data-ttu-id="977a4-279">TestVNet5’i oluşturun.</span><span class="sxs-lookup"><span data-stu-id="977a4-279">Create TestVNet5.</span></span>

  ```azurecli
  az network vnet create -n TestVNet5 -g TestRG5 --address-prefix 10.51.0.0/16 -l japaneast --subnet-name FrontEnd --subnet-prefix 10.51.0.0/24
  ```

3. <span data-ttu-id="977a4-280">Alt ağlar ekleyin.</span><span class="sxs-lookup"><span data-stu-id="977a4-280">Add subnets.</span></span>

  ```azurecli
  az network vnet update -n TestVNet5 --address-prefixes 10.51.0.0/16 10.52.0.0/16 -g TestRG5
  az network vnet subnet create --vnet-name TestVNet5 -n BackEnd -g TestRG5 --address-prefix 10.52.0.0/24
  ```

4. <span data-ttu-id="977a4-281">Merhaba ağ geçidi alt ağı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="977a4-281">Add hello gateway subnet.</span></span>

  ```azurecli
  az network vnet subnet create --vnet-name TestVNet5 -n GatewaySubnet -g TestRG5 --address-prefix 10.52.255.0/27
  ```

5. <span data-ttu-id="977a4-282">Genel bir IP adresi isteyin.</span><span class="sxs-lookup"><span data-stu-id="977a4-282">Request a public IP address.</span></span>

  ```azurecli
  az network public-ip create -n VNet5GWIP -g TestRG5 --allocation-method Dynamic
  ```
6. <span data-ttu-id="977a4-283">Merhaba TestVNet5 ağ geçidini oluşturma</span><span class="sxs-lookup"><span data-stu-id="977a4-283">Create hello TestVNet5 gateway</span></span>

  ```azurecli
  az network vnet-gateway create -n VNet5GW -l japaneast --public-ip-address VNet5GWIP -g TestRG5 --vnet TestVNet5 --gateway-type Vpn --sku VpnGw1 --vpn-type RouteBased --no-wait
  ```

### <span data-ttu-id="977a4-284"><a name="connections5"></a>8. adım - hello bağlantıları oluşturma</span><span class="sxs-lookup"><span data-stu-id="977a4-284"><a name="connections5"></a>Step 8 - Create hello connections</span></span>

<span data-ttu-id="977a4-285">Biz bu adımla olarak işaretlenmiş iki CLI oturumları bölme **[abonelik 1]**, ve **[5. abonelik]** hello ağ geçitleri hello farklı Aboneliklerde olduğundan.</span><span class="sxs-lookup"><span data-stu-id="977a4-285">We split this step into two CLI sessions marked as **[Subscription 1]**, and **[Subscription 5]** because hello gateways are in hello different subscriptions.</span></span> <span data-ttu-id="977a4-286">Abonelikleri kullanımı arasındaki tooswitch ' az hesabı listesi--tüm ' toolist hello abonelikleri kullanılabilir tooyour hesabı sonra kullanın ' az hesabı kümesi--abonelik <subscriptionID>' toouse istediğiniz tooswitch toohello abonelik.</span><span class="sxs-lookup"><span data-stu-id="977a4-286">tooswitch between subscriptions use 'az account list --all' toolist hello subscriptions available tooyour account, then use 'az account set --subscription <subscriptionID>' tooswitch toohello subscription that you want toouse.</span></span>

1. <span data-ttu-id="977a4-287">**[1. abonelik]**  Oturum açın ve tooSubscription 1 bağlanın.</span><span class="sxs-lookup"><span data-stu-id="977a4-287">**[Subscription 1]** Log in and connect tooSubscription 1.</span></span> <span data-ttu-id="977a4-288">Çalışma hello aşağıdaki tooget hello adını ve Kimliğini hello hello çıktısından ağ geçidi komutu:</span><span class="sxs-lookup"><span data-stu-id="977a4-288">Run hello following command tooget hello name and ID of hello Gateway from hello output:</span></span>

  ```azurecli
  az network vnet-gateway show -n VNet1GW -g TestRG1
  ```

  <span data-ttu-id="977a4-289">Merhaba çıktısını Kopyala "kimliği:".</span><span class="sxs-lookup"><span data-stu-id="977a4-289">Copy hello output for "id:".</span></span> <span data-ttu-id="977a4-290">Hello kimliği ve hello hello VNet ağ geçidi (VNet1GW) toohello yöneticinin adı 5. aboneliğin e-posta veya başka bir yöntemle gönderin.</span><span class="sxs-lookup"><span data-stu-id="977a4-290">Send hello ID and hello name of hello VNet gateway (VNet1GW) toohello administrator of Subscription 5 via email or another method.</span></span>

  <span data-ttu-id="977a4-291">Örnek çıktı:</span><span class="sxs-lookup"><span data-stu-id="977a4-291">Example output:</span></span>

  ```
  "id": "/subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW"
  ```

2. <span data-ttu-id="977a4-292">**[5. abonelik]**  Oturum açın ve tooSubscription 5 bağlanın.</span><span class="sxs-lookup"><span data-stu-id="977a4-292">**[Subscription 5]** Log in and connect tooSubscription 5.</span></span> <span data-ttu-id="977a4-293">Çalışma hello aşağıdaki tooget hello adını ve Kimliğini hello hello çıktısından ağ geçidi komutu:</span><span class="sxs-lookup"><span data-stu-id="977a4-293">Run hello following command tooget hello name and ID of hello Gateway from hello output:</span></span>

  ```azurecli
  az network vnet-gateway show -n VNet5GW -g TestRG5
  ```

  <span data-ttu-id="977a4-294">Merhaba çıktısını Kopyala "kimliği:".</span><span class="sxs-lookup"><span data-stu-id="977a4-294">Copy hello output for "id:".</span></span> <span data-ttu-id="977a4-295">Hello kimliği ve hello hello VNet ağ geçidi (vnet5gw'un) toohello yöneticisinin adını abonelik 1 e-posta veya başka bir yöntemle gönderin.</span><span class="sxs-lookup"><span data-stu-id="977a4-295">Send hello ID and hello name of hello VNet gateway (VNet5GW) toohello administrator of Subscription 1 via email or another method.</span></span>

3. <span data-ttu-id="977a4-296">**[1. abonelik]**  Bu adımda TestVNet1 tooTestVNet5 hello bağlantı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="977a4-296">**[Subscription 1]** In this step, you create hello connection from TestVNet1 tooTestVNet5.</span></span> <span data-ttu-id="977a4-297">Merhaba paylaşılan anahtar için kendi değerlerinizi kullanabilirsiniz, ancak hello paylaşılan anahtar için her iki bağlantı eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="977a4-297">You can use your own values for hello shared key, however, hello shared key must match for both connections.</span></span> <span data-ttu-id="977a4-298">Bağlantı oluşturma toocomplete sırasında kısa sürebilir.</span><span class="sxs-lookup"><span data-stu-id="977a4-298">Creating a connection can take a short while toocomplete.</span></span> <span data-ttu-id="977a4-299">TooSubscription 1 bağlandığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="977a4-299">Make sure you connect tooSubscription 1.</span></span>

  ```azurecli
  az network vpn-connection create -n VNet1ToVNet5 -g TestRG1 --vnet-gateway1 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW -l eastus --shared-key "eeffgg" --vnet-gateway2 /subscriptions/e7e33b39-fe28-4822-b65c-a4db8bbff7cb/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW
  ```

4. <span data-ttu-id="977a4-300">**[5. abonelik]**  TestVNet5 tooTestVNet1 hello bağlantı oluşturma dışında bu benzer toohello yukarıdaki bir adımdır.</span><span class="sxs-lookup"><span data-stu-id="977a4-300">**[Subscription 5]** This step is similar toohello one above, except you are creating hello connection from TestVNet5 tooTestVNet1.</span></span> <span data-ttu-id="977a4-301">Bu hello paylaşılan anahtarlar eşleşme ve tooSubscription 5 bağlanmak emin olun.</span><span class="sxs-lookup"><span data-stu-id="977a4-301">Make sure that hello shared keys match and that you connect tooSubscription 5.</span></span>

  ```azurecli
  az network vpn-connection create -n VNet5ToVNet1 -g TestRG5 --vnet-gateway1 /subscriptions/e7e33b39-fe28-4822-b65c-a4db8bbff7cb/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW -l japaneast --shared-key "eeffgg" --vnet-gateway2 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW
  ```

## <span data-ttu-id="977a4-302"><a name="verify"></a>Merhaba bağlantılarını doğrulama</span><span class="sxs-lookup"><span data-stu-id="977a4-302"><a name="verify"></a>Verify hello connections</span></span>
[!INCLUDE [vpn-gateway-no-nsg-include](../../includes/vpn-gateway-no-nsg-include.md)]

[!INCLUDE [verify connections v2v cli](../../includes/vpn-gateway-verify-connection-cli-rm-include.md)]

## <span data-ttu-id="977a4-303"><a name="faq"></a>Sanal ağlar arası bağlantılar hakkında SSS</span><span class="sxs-lookup"><span data-stu-id="977a4-303"><a name="faq"></a>VNet-to-VNet FAQ</span></span>
[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]

## <a name="next-steps"></a><span data-ttu-id="977a4-304">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="977a4-304">Next steps</span></span>

* <span data-ttu-id="977a4-305">Bağlantınız tamamlandıktan sonra sanal makineleri tooyour sanal ağları ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="977a4-305">Once your connection is complete, you can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="977a4-306">Daha fazla bilgi için bkz: Merhaba [Virtual Machines belgeleri](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span><span class="sxs-lookup"><span data-stu-id="977a4-306">For more information, see hello [Virtual Machines documentation](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span></span>
* <span data-ttu-id="977a4-307">BGP hakkında daha fazla bilgi için bkz: Merhaba [BGP genel bakış](vpn-gateway-bgp-overview.md) ve [nasıl tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span><span class="sxs-lookup"><span data-stu-id="977a4-307">For information about BGP, see hello [BGP Overview](vpn-gateway-bgp-overview.md) and [How tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span></span>
