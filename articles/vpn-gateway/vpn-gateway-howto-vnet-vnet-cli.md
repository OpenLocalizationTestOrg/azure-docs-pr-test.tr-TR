---
title: "Bir sanal ağı başka bir sanal ağa bağlama: Azure CLI | Microsoft Docs"
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
ms.openlocfilehash: ae42f661b39e8b6170fd415d758404fb33009ccc
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="configure-a-vnet-to-vnet-vpn-gateway-connection-using-azure-cli"></a><span data-ttu-id="5b5a2-103">Azure CLI kullanarak sanal ağlar arası VPN ağ geçidi bağlantısı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="5b5a2-103">Configure a VNet-to-VNet VPN gateway connection using Azure CLI</span></span>

<span data-ttu-id="5b5a2-104">Bu makalede, sanal ağlar arasında VPN ağ geçidi bağlantısının nasıl oluşturulduğu gösterilir.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-104">This article shows you how to create a VPN gateway connection between virtual networks.</span></span> <span data-ttu-id="5b5a2-105">Sanal ağlar aynı ya da farklı bölgelerde ve aynı ya da farklı aboneliklerde bulunuyor olabilirler.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-105">The virtual networks can be in the same or different regions, and from the same or different subscriptions.</span></span> <span data-ttu-id="5b5a2-106">Farklı aboneliklerden sanal ağları bağlarken aboneliklerin aynı Active Directory kiracısıyla ilişkilendirilmiş olması gerekmez.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-106">When connecting VNets from different subscriptions, the subscriptions do not need to be associated with the same Active Directory tenant.</span></span> 

<span data-ttu-id="5b5a2-107">Bu makaledeki adımlar Resource Manager dağıtım modeli için geçerlidir ve Azure CLI kullanılır.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-107">The steps in this article apply to the Resource Manager deployment model and use Azure CLI.</span></span> <span data-ttu-id="5b5a2-108">Ayrıca aşağıdaki listeden farklı bir seçenek belirtip farklı bir dağıtım aracı veya dağıtım modeli kullanarak da bu yapılandırmayı oluşturabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="5b5a2-108">You can also create this configuration using a different deployment tool or deployment model by selecting a different option from the following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="5b5a2-109">Azure portal</span><span class="sxs-lookup"><span data-stu-id="5b5a2-109">Azure portal</span></span>](vpn-gateway-howto-vnet-vnet-resource-manager-portal.md)
> * [<span data-ttu-id="5b5a2-110">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5b5a2-110">PowerShell</span></span>](vpn-gateway-vnet-vnet-rm-ps.md)
> * [<span data-ttu-id="5b5a2-111">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="5b5a2-111">Azure CLI</span></span>](vpn-gateway-howto-vnet-vnet-cli.md)
> * [<span data-ttu-id="5b5a2-112">Azure portal (klasik)</span><span class="sxs-lookup"><span data-stu-id="5b5a2-112">Azure portal (classic)</span></span>](vpn-gateway-howto-vnet-vnet-portal-classic.md)
> * [<span data-ttu-id="5b5a2-113">Farklı dağıtım modellerini bağlama - Azure portalı</span><span class="sxs-lookup"><span data-stu-id="5b5a2-113">Connect different deployment models - Azure portal</span></span>](vpn-gateway-connect-different-deployment-models-portal.md)
> * [<span data-ttu-id="5b5a2-114">Farklı dağıtım modellerini bağlama - PowerShell</span><span class="sxs-lookup"><span data-stu-id="5b5a2-114">Connect different deployment models - PowerShell</span></span>](vpn-gateway-connect-different-deployment-models-powershell.md)
>
>

<span data-ttu-id="5b5a2-115">Bir sanal ağı başka bir sanal ağa bağlamak (VNet'ten VNet'e), bir VNet'i şirket içi site konumuna bağlamakla aynıdır.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-115">Connecting a virtual network to another virtual network (VNet-to-VNet) is similar to connecting a VNet to an on-premises site location.</span></span> <span data-ttu-id="5b5a2-116">Her iki bağlantı türü de IPsec/IKE kullanarak güvenli bir tünel sunmak üzere bir VPN ağ geçidi kullanır.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-116">Both connectivity types use a VPN gateway to provide a secure tunnel using IPsec/IKE.</span></span> <span data-ttu-id="5b5a2-117">VNet’leriniz aynı bölgedeyse VNet Eşlemesi kullanarak bağlamayı düşünebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-117">If your VNets are in the same region, you may want to consider connecting them using VNet Peering.</span></span> <span data-ttu-id="5b5a2-118">VNet eşlemesi VPN ağ geçidini kullanmaz.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-118">VNet peering does not use a VPN gateway.</span></span> <span data-ttu-id="5b5a2-119">Daha fazla bilgi için bkz. [VNet eşlemesi](../virtual-network/virtual-network-peering-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5b5a2-119">For more information, see [VNet peering](../virtual-network/virtual-network-peering-overview.md).</span></span>

<span data-ttu-id="5b5a2-120">Hatta Sanal Ağdan Sanal Ağa iletişim çok siteli yapılandırmalarla bile birleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-120">VNet-to-VNet communication can be combined with multi-site configurations.</span></span> <span data-ttu-id="5b5a2-121">Bunun yapılması aşağıdaki diyagramda da görüldüğü gibi şirket içi ve şirket dışı bağlantıyla sanal ağ içi bağlantıyı birleştiren ağ topolojileri kurabilmenize olanak sağlar:</span><span class="sxs-lookup"><span data-stu-id="5b5a2-121">This lets you establish network topologies that combine cross-premises connectivity with inter-virtual network connectivity, as shown in the following diagram:</span></span>

![Bağlantılar hakkında](./media/vpn-gateway-howto-vnet-vnet-cli/aboutconnections.png)

### <span data-ttu-id="5b5a2-123"><a name="why"></a>Sanal ağları neden bağlamalıyız?</span><span class="sxs-lookup"><span data-stu-id="5b5a2-123"><a name="why"></a>Why connect virtual networks?</span></span>

<span data-ttu-id="5b5a2-124">Sanal ağları aşağıdaki sebeplerden dolayı bağlamak isteyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="5b5a2-124">You may want to connect virtual networks for the following reasons:</span></span>

* <span data-ttu-id="5b5a2-125">**Çapraz bölge coğrafi artıklığı ve coğrafi-durum**</span><span class="sxs-lookup"><span data-stu-id="5b5a2-125">**Cross region geo-redundancy and geo-presence**</span></span>

  * <span data-ttu-id="5b5a2-126">Kendi coğrafi çoğaltma veya eşitlemenizi, güvenli bağlantıyla İnternet’te uç noktalara gitmeden ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-126">You can set up your own geo-replication or synchronization with secure connectivity without going over Internet-facing endpoints.</span></span>
  * <span data-ttu-id="5b5a2-127">Azure Traffic Manager ve Load Balancer ile birçok Azure bölgesinde coğrafi yedeklilik imkanıyla yüksek oranda kullanılabilir iş yükü oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-127">With Azure Traffic Manager and Load Balancer, you can set up highly available workload with geo-redundancy across multiple Azure regions.</span></span> <span data-ttu-id="5b5a2-128">Buna önemli bir örnek olarak SQL Always On ile birden fazla Azure bölgesine yayılan Kullanılabilirlik Grupları’nı birlikte kurmak verilebilir.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-128">One important example is to set up SQL Always On with Availability Groups spreading across multiple Azure regions.</span></span>
* <span data-ttu-id="5b5a2-129">**Yalıtım veya yönetim sınır bölgesel çok katmanlı uygulamalar**</span><span class="sxs-lookup"><span data-stu-id="5b5a2-129">**Regional multi-tier applications with isolation or administrative boundary**</span></span>

  * <span data-ttu-id="5b5a2-130">Yalıtım ve yönetim gereksinimlerinden dolayı aynı bölge içinde birbirlerine bağlı birden fazla sanal ağ ile çok katmanlı uygulamalar kurabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-130">Within the same region, you can set up multi-tier applications with multiple virtual networks connected together due to isolation or administrative requirements.</span></span>

<span data-ttu-id="5b5a2-131">Sanal ağlar arası bağlantılar hakkında daha fazla bilgi için bu makalenin sonunda yer alan [Sanal ağlar arası bağlantılar hakkında SSS](#faq) bölümünü inceleyin.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-131">For more information about VNet-to-VNet connections, see the [VNet-to-VNet FAQ](#faq) at the end of this article.</span></span>

### <a name="which-set-of-steps-should-i-use"></a><span data-ttu-id="5b5a2-132">Hangi adımları tamamlamalıyım? </span><span class="sxs-lookup"><span data-stu-id="5b5a2-132">Which set of steps should I use?</span></span>

<span data-ttu-id="5b5a2-133">Bu makalede iki farklı adım kümesi görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-133">In this article, you see two different sets of steps.</span></span> <span data-ttu-id="5b5a2-134">Bir adım kümesi [Aynı abonelikte bulunan sanal ağlar](#samesub), diğer adım kümesi ise [Farklı aboneliklerde bulunan sanal ağlar](#difsub) içindir.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-134">One set of steps for [VNets that reside in the same subscription](#samesub), and another for [VNets that reside in different subscriptions](#difsub).</span></span>

## <span data-ttu-id="5b5a2-135"><a name="samesub"></a>Aynı abonelikte olan sanal ağları bağlanma</span><span class="sxs-lookup"><span data-stu-id="5b5a2-135"><a name="samesub"></a>Connect VNets that are in the same subscription</span></span>

![v2v diyagramı](./media/vpn-gateway-howto-vnet-vnet-cli/v2vrmps.png)

### <a name="before-you-begin"></a><span data-ttu-id="5b5a2-137">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="5b5a2-137">Before you begin</span></span>

<span data-ttu-id="5b5a2-138">Başlamadan önce, CLI komutlarının en son sürümünü (2.0 veya üzeri) yükleyin.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-138">Before beginning, install the latest version of the CLI commands (2.0 or later).</span></span> <span data-ttu-id="5b5a2-139">CLI komutlarını yükleme hakkında bilgi için bkz. [Azure CLI 2.0’ı yükleme](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="5b5a2-139">For information about installing the CLI commands, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span>

### <span data-ttu-id="5b5a2-140"><a name="Plan"></a>IP adresi aralıklarınızı planlama</span><span class="sxs-lookup"><span data-stu-id="5b5a2-140"><a name="Plan"></a>Plan your IP address ranges</span></span>

<span data-ttu-id="5b5a2-141">Aşağıdaki adımlarda kendi ağ geçidi alt ağları ve yapılandırmalarıyla birlikte iki sanal ağ oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-141">In the following steps, we create two virtual networks along with their respective gateway subnets and configurations.</span></span> <span data-ttu-id="5b5a2-142">Daha sonra iki sanal ağ arasında bir VPN bağlantısı oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-142">We then create a VPN connection between the two VNets.</span></span> <span data-ttu-id="5b5a2-143">Ağ yapılandırmanız için IP adres aralıklarını planlamanız önemlidir.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-143">It’s important to plan the IP address ranges for your network configuration.</span></span> <span data-ttu-id="5b5a2-144">Sanal ağ aralıklarınızın ya da yerel ağ aralıklarınızın hiçbir şekilde çakışmadığından emin olmalısınız.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-144">Keep in mind that you must make sure that none of your VNet ranges or local network ranges overlap in any way.</span></span> <span data-ttu-id="5b5a2-145">Bu örneklerde bir DNS sunucusu eklemiyoruz.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-145">In these examples, we do not include a DNS server.</span></span> <span data-ttu-id="5b5a2-146">Sanal ağlarınız için ad çözümlemesi istiyorsanız bkz. [Ad çözümlemesi](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span><span class="sxs-lookup"><span data-stu-id="5b5a2-146">If you want name resolution for your virtual networks, see [Name resolution](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span></span>

<span data-ttu-id="5b5a2-147">Örneklerde aşağıdaki değerler kullanılmaktadır:</span><span class="sxs-lookup"><span data-stu-id="5b5a2-147">We use the following values in the examples:</span></span>

<span data-ttu-id="5b5a2-148">**Değerler TestVNet1 için:**</span><span class="sxs-lookup"><span data-stu-id="5b5a2-148">**Values for TestVNet1:**</span></span>

* <span data-ttu-id="5b5a2-149">VNet Name: TestVNet1</span><span class="sxs-lookup"><span data-stu-id="5b5a2-149">VNet Name: TestVNet1</span></span>
* <span data-ttu-id="5b5a2-150">Resource Group: TestRG1</span><span class="sxs-lookup"><span data-stu-id="5b5a2-150">Resource Group: TestRG1</span></span>
* <span data-ttu-id="5b5a2-151">Location: East US</span><span class="sxs-lookup"><span data-stu-id="5b5a2-151">Location: East US</span></span>
* <span data-ttu-id="5b5a2-152">TestVNet1: 10.11.0.0/16 & 10.12.0.0/16</span><span class="sxs-lookup"><span data-stu-id="5b5a2-152">TestVNet1: 10.11.0.0/16 & 10.12.0.0/16</span></span>
* <span data-ttu-id="5b5a2-153">FrontEnd: 10.11.0.0/24</span><span class="sxs-lookup"><span data-stu-id="5b5a2-153">FrontEnd: 10.11.0.0/24</span></span>
* <span data-ttu-id="5b5a2-154">BackEnd: 10.12.0.0/24</span><span class="sxs-lookup"><span data-stu-id="5b5a2-154">BackEnd: 10.12.0.0/24</span></span>
* <span data-ttu-id="5b5a2-155">GatewaySubnet: 10.12.255.0/27</span><span class="sxs-lookup"><span data-stu-id="5b5a2-155">GatewaySubnet: 10.12.255.0/27</span></span>
* <span data-ttu-id="5b5a2-156">GatewayName: VNet1GW</span><span class="sxs-lookup"><span data-stu-id="5b5a2-156">GatewayName: VNet1GW</span></span>
* <span data-ttu-id="5b5a2-157">Public IP: VNet1GWIP</span><span class="sxs-lookup"><span data-stu-id="5b5a2-157">Public IP: VNet1GWIP</span></span>
* <span data-ttu-id="5b5a2-158">VPNType: RouteBased</span><span class="sxs-lookup"><span data-stu-id="5b5a2-158">VPNType: RouteBased</span></span>
* <span data-ttu-id="5b5a2-159">Connection(1to4): VNet1toVNet4</span><span class="sxs-lookup"><span data-stu-id="5b5a2-159">Connection(1to4): VNet1toVNet4</span></span>
* <span data-ttu-id="5b5a2-160">Connection(1to5): VNet1toVNet5</span><span class="sxs-lookup"><span data-stu-id="5b5a2-160">Connection(1to5): VNet1toVNet5</span></span>
* <span data-ttu-id="5b5a2-161">ConnectionType: VNet2VNet</span><span class="sxs-lookup"><span data-stu-id="5b5a2-161">ConnectionType: VNet2VNet</span></span>

<span data-ttu-id="5b5a2-162">**Değerler TestVNet4 için:**</span><span class="sxs-lookup"><span data-stu-id="5b5a2-162">**Values for TestVNet4:**</span></span>

* <span data-ttu-id="5b5a2-163">VNet Name: TestVNet4</span><span class="sxs-lookup"><span data-stu-id="5b5a2-163">VNet Name: TestVNet4</span></span>
* <span data-ttu-id="5b5a2-164">TestVNet2: 10.41.0.0/16 & 10.42.0.0/16</span><span class="sxs-lookup"><span data-stu-id="5b5a2-164">TestVNet2: 10.41.0.0/16 & 10.42.0.0/16</span></span>
* <span data-ttu-id="5b5a2-165">FrontEnd: 10.41.0.0/24</span><span class="sxs-lookup"><span data-stu-id="5b5a2-165">FrontEnd: 10.41.0.0/24</span></span>
* <span data-ttu-id="5b5a2-166">BackEnd: 10.42.0.0/24</span><span class="sxs-lookup"><span data-stu-id="5b5a2-166">BackEnd: 10.42.0.0/24</span></span>
* <span data-ttu-id="5b5a2-167">GatewaySubnet: 10.42.255.0/27</span><span class="sxs-lookup"><span data-stu-id="5b5a2-167">GatewaySubnet: 10.42.255.0/27</span></span>
* <span data-ttu-id="5b5a2-168">Resource Group: TestRG4</span><span class="sxs-lookup"><span data-stu-id="5b5a2-168">Resource Group: TestRG4</span></span>
* <span data-ttu-id="5b5a2-169">Location: West US</span><span class="sxs-lookup"><span data-stu-id="5b5a2-169">Location: West US</span></span>
* <span data-ttu-id="5b5a2-170">GatewayName: VNet4GW</span><span class="sxs-lookup"><span data-stu-id="5b5a2-170">GatewayName: VNet4GW</span></span>
* <span data-ttu-id="5b5a2-171">Public IP: VNet4GWIP</span><span class="sxs-lookup"><span data-stu-id="5b5a2-171">Public IP: VNet4GWIP</span></span>
* <span data-ttu-id="5b5a2-172">VPNType: RouteBased</span><span class="sxs-lookup"><span data-stu-id="5b5a2-172">VPNType: RouteBased</span></span>
* <span data-ttu-id="5b5a2-173">Connection: VNet4toVNet1</span><span class="sxs-lookup"><span data-stu-id="5b5a2-173">Connection: VNet4toVNet1</span></span>
* <span data-ttu-id="5b5a2-174">ConnectionType: VNet2VNet</span><span class="sxs-lookup"><span data-stu-id="5b5a2-174">ConnectionType: VNet2VNet</span></span>


### <span data-ttu-id="5b5a2-175"><a name="Connect"></a>1. Adım: Aboneliğinize bağlanma</span><span class="sxs-lookup"><span data-stu-id="5b5a2-175"><a name="Connect"></a>Step 1 - Connect to your subscription</span></span>

[!INCLUDE [CLI login](../../includes/vpn-gateway-cli-login-numbers-include.md)]

### <span data-ttu-id="5b5a2-176"><a name="TestVNet1"></a>Adım 2 - oluşturma ve TestVNet1 yapılandırma</span><span class="sxs-lookup"><span data-stu-id="5b5a2-176"><a name="TestVNet1"></a>Step 2 - Create and configure TestVNet1</span></span>

1. <span data-ttu-id="5b5a2-177">Bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-177">Create a resource group.</span></span>

  ```azurecli
  az group create -n TestRG1  -l eastus
  ```
2. <span data-ttu-id="5b5a2-178">TestVNet1’i ve TestVNet1’in alt ağlarını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-178">Create TestVNet1 and the subnets for TestVNet1.</span></span> <span data-ttu-id="5b5a2-179">Bu örnekte, TestVNet1 adlı bir sanal ağ ve FrontEnd adlı bir alt ağ oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-179">This example creates a virtual network named TestVNet1 and a subnet named FrontEnd.</span></span>

  ```azurecli
  az network vnet create -n TestVNet1 -g TestRG1 --address-prefix 10.11.0.0/16 -l eastus --subnet-name FrontEnd --subnet-prefix 10.11.0.0/24
  ```
3. <span data-ttu-id="5b5a2-180">Arka uç alt ağı için ek bir adres alanı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-180">Create an additional address space for the backend subnet.</span></span> <span data-ttu-id="5b5a2-181">Bu adımda hem daha önce oluşturduğumuz adres alanını hem de eklemek istediğimiz ek etki alanını belirttiğimize dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-181">Notice that in this step, we specify both the address space that we created earlier, and the additional address space that we want to add.</span></span> <span data-ttu-id="5b5a2-182">Bunun nedeni, [az network vnet update](https://docs.microsoft.com/cli/azure/network/vnet#update) komutunun önceki ayarların üzerine yazmasıdır.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-182">This is because the [az network vnet update](https://docs.microsoft.com/cli/azure/network/vnet#update) command overwrites the previous settings.</span></span> <span data-ttu-id="5b5a2-183">Bu komutu kullanırken tüm adres ön eklerini belirttiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-183">Make sure to specify all of the address prefixes when using this command.</span></span>

  ```azurecli
  az network vnet update -n TestVNet1 --address-prefixes 10.11.0.0/16 10.12.0.0/16 -g TestRG1
  ```
4. <span data-ttu-id="5b5a2-184">Arka uç alt ağını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-184">Create the backend subnet.</span></span>
  
  ```azurecli
  az network vnet subnet create --vnet-name TestVNet1 -n BackEnd -g TestRG1 --address-prefix 10.12.0.0/24 
  ```
5. <span data-ttu-id="5b5a2-185">Ağ geçidi alt ağını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-185">Create the gateway subnet.</span></span> <span data-ttu-id="5b5a2-186">Ağ geçidi alt ağının 'GatewaySubnet' olarak adlandırıldığına dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-186">Notice that the gateway subnet is named 'GatewaySubnet'.</span></span> <span data-ttu-id="5b5a2-187">Bu ad gereklidir.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-187">This name is required.</span></span> <span data-ttu-id="5b5a2-188">Bu örnekte ağ geçidi alt ağı bir /27 kullanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-188">In this example, the gateway subnet is using a /27.</span></span> <span data-ttu-id="5b5a2-189">/29 kadar küçük bir ağ geçidi alt ağı oluşturmak mümkün olsa da en az /28 veya /27’yi seçerek daha fazla adres içeren büyük bir alt ağ oluşturmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-189">While it is possible to create a gateway subnet as small as /29, we recommend that you create a larger subnet that includes more addresses by selecting at least /28 or /27.</span></span> <span data-ttu-id="5b5a2-190">Bu, gelecekte isteyebileceğiniz ek yapılandırmaları da içerecek yeteri kadar adres sağlayacaktır.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-190">This will allow for enough addresses to accommodate possible additional configurations that you may want in the future.</span></span>

  ```azurecli 
  az network vnet subnet create --vnet-name TestVNet1 -n GatewaySubnet -g TestRG1 --address-prefix 10.12.255.0/27
  ```
6. <span data-ttu-id="5b5a2-191">Sanal ağınız için oluşturacağınız ağ geçidine ayrılacak genel IP adresi isteyin.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-191">Request a public IP address to be allocated to the gateway you will create for your VNet.</span></span> <span data-ttu-id="5b5a2-192">AllocationMethod değerinin Dinamik olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-192">Notice that the AllocationMethod is Dynamic.</span></span> <span data-ttu-id="5b5a2-193">Kullanmak istediğiniz IP adresini belirtemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-193">You cannot specify the IP address that you want to use.</span></span> <span data-ttu-id="5b5a2-194">IP adresi, ağ geçidinize dinamik olarak ayrılır.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-194">It's dynamically allocated to your gateway.</span></span>

  ```azurecli
  az network public-ip create -n VNet1GWIP -g TestRG1 --allocation-method Dynamic
  ```
7. <span data-ttu-id="5b5a2-195">TestVNet1 için sanal ağ geçidini oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-195">Create the virtual network gateway for TestVNet1.</span></span> <span data-ttu-id="5b5a2-196">Sanal Ağdan Sanal Ağa yapılandırmaları, RouteBased bir VPNType gerektirir.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-196">VNet-to-VNet configurations require a RouteBased VpnType.</span></span> <span data-ttu-id="5b5a2-197">Bu komutu '--no-wait' parametresiyle çalıştırırsanız herhangi bir geri bildirim veya çıktı görmezsiniz.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-197">If you run this command using the '--no-wait' parameter, you don't see any feedback or output.</span></span> <span data-ttu-id="5b5a2-198">'--no-wait' parametresi, ağ geçidinin arka planda oluşturulmasına olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-198">The '--no-wait' parameter allows the gateway to create in the background.</span></span> <span data-ttu-id="5b5a2-199">VPN ağ geçidi oluşturma işleminin hemen tamamlandığı anlamına gelmez.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-199">It does not mean that the VPN gateway finishes creating immediately.</span></span> <span data-ttu-id="5b5a2-200">Bir ağ geçidinin oluşturulması, kullandığınız ağ geçidi SKU’suna bağlı olarak 45 dakika veya daha uzun sürebilir.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-200">Creating a gateway can often take 45 minutes or more, depending on the gateway SKU that you use.</span></span>

  ```azurecli
  az network vnet-gateway create -n VNet1GW -l eastus --public-ip-address VNet1GWIP -g TestRG1 --vnet TestVNet1 --gateway-type Vpn --sku VpnGw1 --vpn-type RouteBased --no-wait
  ```

### <span data-ttu-id="5b5a2-201"><a name="TestVNet4"></a>3. Adım - TestVNet4’ü oluşturma ve yapılandırma</span><span class="sxs-lookup"><span data-stu-id="5b5a2-201"><a name="TestVNet4"></a>Step 3 - Create and configure TestVNet4</span></span>

1. <span data-ttu-id="5b5a2-202">Bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-202">Create a resource group.</span></span>

  ```azurecli
  az group create -n TestRG4  -l westus
  ```
2. <span data-ttu-id="5b5a2-203">TestVNet4’ü oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-203">Create TestVNet4.</span></span>

  ```azurecli
  az network vnet create -n TestVNet4 -g TestRG4 --address-prefix 10.41.0.0/16 -l westus --subnet-name FrontEnd --subnet-prefix 10.41.0.0/24
  ```

3. <span data-ttu-id="5b5a2-204">TestVNet4 için ek alt ağlar oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-204">Create additional subnets for TestVNet4.</span></span>

  ```azurecli
  az network vnet update -n TestVNet4 --address-prefixes 10.41.0.0/16 10.42.0.0/16 -g TestRG4 
  az network vnet subnet create --vnet-name TestVNet4 -n BackEnd -g TestRG4 --address-prefix 10.42.0.0/24 
  ```
4. <span data-ttu-id="5b5a2-205">Ağ geçidi alt ağını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-205">Create the gateway subnet.</span></span>

  ```azurecli
   az network vnet subnet create --vnet-name TestVNet4 -n GatewaySubnet -g TestRG4 --address-prefix 10.42.255.0/27
  ```
5. <span data-ttu-id="5b5a2-206">Bir Genel IP adresi isteyin.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-206">Request a Public IP address.</span></span>

  ```azurecli
  az network public-ip create -n VNet4GWIP -g TestRG4 --allocation-method Dynamic
  ```
6. <span data-ttu-id="5b5a2-207">TestVNet4 sanal ağ geçidini oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-207">Create the TestVNet4 virtual network gateway.</span></span>

  ```azurecli
  az network vnet-gateway create -n VNet4GW -l westus --public-ip-address VNet4GWIP -g TestRG4 --vnet TestVNet4 --gateway-type Vpn --sku VpnGw1 --vpn-type RouteBased --no-wait
  ```

### <span data-ttu-id="5b5a2-208"><a name="createconnect"></a>4. Adım - Bağlantıları oluşturma</span><span class="sxs-lookup"><span data-stu-id="5b5a2-208"><a name="createconnect"></a>Step 4 - Create the connections</span></span>

<span data-ttu-id="5b5a2-209">Artık VPN ağ geçitleri olan iki sanal ağınız var.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-209">You now have two VNets with VPN gateways.</span></span> <span data-ttu-id="5b5a2-210">Bir sonraki adım, sanal ağın ağ geçitleri arasındaki VPN ağ geçidi bağlantılarını oluşturmaya yöneliktir.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-210">The next step is to create VPN gateway connections between the virtual network gateways.</span></span> <span data-ttu-id="5b5a2-211">Yukarıdaki örnekleri kullandıysanız, VNet ağ geçitleriniz farklı kaynak gruplarındadır.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-211">If you used the examples above, your VNet gateways are in different resource groups.</span></span> <span data-ttu-id="5b5a2-212">Ağ geçitleri farklı kaynak gruplarında olduğunda, bir bağlantı oluşturduğunuz sırada her ağ geçidinin kaynak kimliklerini tanımlamanız ve belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-212">When gateways are in different resource groups, you need to identify and specify the resource IDs for each gateway when making a connection.</span></span> <span data-ttu-id="5b5a2-213">VNet’leriniz aynı kaynak grubundaysa, kaynak kimliklerini belirtmeniz gerekmeyeceğinden [ikinci yönerge kümesini](#samerg) kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-213">If your VNets are in the same resource group, you can use the [second set of instructions](#samerg) because you don't need to specify the resource IDs.</span></span>

### <span data-ttu-id="5b5a2-214"><a name="diffrg"></a>Farklı kaynak gruplarında bulunan VNet’leri bağlamak için</span><span class="sxs-lookup"><span data-stu-id="5b5a2-214"><a name="diffrg"></a>To connect VNets that reside in different resource groups</span></span>

1. <span data-ttu-id="5b5a2-215">Aşağıdaki komutun çıktısından VNet1GW öğesinin Kaynak Kimliğini alın:</span><span class="sxs-lookup"><span data-stu-id="5b5a2-215">Get the Resource ID of VNet1GW from the output of the following command:</span></span>

  ```azurecli
  az network vnet-gateway show -n VNet1GW -g TestRG1
  ```

  <span data-ttu-id="5b5a2-216">Çıktıda "id:" satırını bulun.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-216">In the output, find the "id:" line.</span></span> <span data-ttu-id="5b5a2-217">Bir sonraki bölümde bağlantıyı oluşturmak için tırnak içindeki değerler gerekir.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-217">The values within the quotes are needed to create the connection in the next section.</span></span> <span data-ttu-id="5b5a2-218">Bağlantınızı oluştururken kolayca yapıştırabilmek için bu değerleri Notepad gibi bir metin düzenleyicisine kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-218">Copy these values to a text editor, such as Notepad, so that you can easily paste them when creating your connection.</span></span>

  <span data-ttu-id="5b5a2-219">Örnek çıktı:</span><span class="sxs-lookup"><span data-stu-id="5b5a2-219">Example output:</span></span>

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

  <span data-ttu-id="5b5a2-220">**"id":** ifadesinden sonra gelen tırnak içindeki değerleri kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-220">Copy the values after **"id":** within the quotes.</span></span>

  ```
  "id": "/subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW"
 ```

2. <span data-ttu-id="5b5a2-221">VNet4GW öğesinin Kaynak Kimliğini alın ve değerleri bir metin düzenleyicisine kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-221">Get the Resource ID of VNet4GW and copy the values to a text editor.</span></span>

  ```azurecli
  az network vnet-gateway show -n VNet4GW -g TestRG4
  ```

3. <span data-ttu-id="5b5a2-222">TestVNet1 - TestVNet4 bağlantısını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-222">Create the TestVNet1 to TestVNet4 connection.</span></span> <span data-ttu-id="5b5a2-223">Bu adımda TestVNet1 - TestVNet4 arasında bağlantı oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-223">In this step, you create the connection from TestVNet1 to TestVNet4.</span></span> <span data-ttu-id="5b5a2-224">Örneklerde sözü geçen bir paylaşılan anahtar vardır.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-224">There is a shared key referenced in the examples.</span></span> <span data-ttu-id="5b5a2-225">Paylaşılan anahtar için kendi değerlerinizi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-225">You can use your own values for the shared key.</span></span> <span data-ttu-id="5b5a2-226">Paylaşılan anahtarın her iki bağlantıyla da eşleşiyor olması önemlidir.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-226">The important thing is that the shared key must match for both connections.</span></span> <span data-ttu-id="5b5a2-227">Bağlantı oluşturma işleminin tamamlanması biraz zaman alır.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-227">Creating a connection takes a short while to complete.</span></span>

  ```azurecli
  az network vpn-connection create -n VNet1ToVNet4 -g TestRG1 --vnet-gateway1 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW -l eastus --shared-key "aabbcc" --vnet-gateway2 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG4/providers/Microsoft.Network/virtualNetworkGateways/VNet4GW 
  ```
4. <span data-ttu-id="5b5a2-228">TestVNet4 - TestVNet1 bağlantısı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-228">Create the TestVNet4 to TestVNet1 connection.</span></span> <span data-ttu-id="5b5a2-229">Bu adım, bağlantıyı TestVNet4’ten TestVNet1’e yönüne kuracak olmanız dışında yukarıdaki adımla aynıdır.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-229">This step is similar to the one above, except you are creating the connection from TestVNet4 to TestVNet1.</span></span> <span data-ttu-id="5b5a2-230">Paylaşılan anahtarların eşleştiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-230">Make sure the shared keys match.</span></span> <span data-ttu-id="5b5a2-231">Bağlantının kurulması birkaç dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-231">It takes a few minutes to establish the connection.</span></span>

  ```azurecli
  az network vpn-connection create -n VNet4ToVNet1 -g TestRG4 --vnet-gateway1 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG4/providers/Microsoft.Network/virtualNetworkGateways/VNet4GW -l westus --shared-key "aabbcc" --vnet-gateway2 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1G
  ```
5. <span data-ttu-id="5b5a2-232">Bağlantılarınızı doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-232">Verify your connections.</span></span> <span data-ttu-id="5b5a2-233">Bkz. [Bağlantınızı doğrulama](#verify).</span><span class="sxs-lookup"><span data-stu-id="5b5a2-233">See [Verify your connection](#verify).</span></span>

### <span data-ttu-id="5b5a2-234"><a name="samerg"></a>Aynı kaynak grubunda bulunan VNet’leri bağlamak için</span><span class="sxs-lookup"><span data-stu-id="5b5a2-234"><a name="samerg"></a>To connect VNets that reside in the same resource group</span></span>

1. <span data-ttu-id="5b5a2-235">TestVNet1 - TestVNet4 bağlantısını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-235">Create the TestVNet1 to TestVNet4 connection.</span></span> <span data-ttu-id="5b5a2-236">Bu adımda TestVNet1 - TestVNet4 arasında bağlantı oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-236">In this step, you create the connection from TestVNet1 to TestVNet4.</span></span> <span data-ttu-id="5b5a2-237">Örneklerdeki kaynak gruplarının aynı olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-237">Notice the resource groups are the same in the examples.</span></span> <span data-ttu-id="5b5a2-238">Örneklerde paylaşılan bir anahtardan söz edildiğini de göreceksiniz.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-238">You also see a shared key referenced in the examples.</span></span> <span data-ttu-id="5b5a2-239">Paylaşılan anahtar için kendi değerlerinizi kullanabilirsiniz, ancak her iki bağlantı için de paylaşılan anahtarın eşleşmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-239">You can use your own values for the shared key, however, the shared key must match for both connections.</span></span> <span data-ttu-id="5b5a2-240">Bağlantı oluşturma işleminin tamamlanması biraz zaman alır.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-240">Creating a connection takes a short while to complete.</span></span>

  ```azurecli
  az network vpn-connection create -n VNet1ToVNet4 -g TestRG1 --vnet-gateway1 VNet1GW -l eastus --shared-key "eeffgg" --vnet-gateway2 VNet4GW
  ```
2. <span data-ttu-id="5b5a2-241">TestVNet4 - TestVNet1 bağlantısı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-241">Create the TestVNet4 to TestVNet1 connection.</span></span> <span data-ttu-id="5b5a2-242">Bu adım, bağlantıyı TestVNet4’ten TestVNet1’e yönüne kuracak olmanız dışında yukarıdaki adımla aynıdır.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-242">This step is similar to the one above, except you are creating the connection from TestVNet4 to TestVNet1.</span></span> <span data-ttu-id="5b5a2-243">Paylaşılan anahtarların eşleştiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-243">Make sure the shared keys match.</span></span> <span data-ttu-id="5b5a2-244">Bağlantının kurulması birkaç dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-244">It takes a few minutes to establish the connection.</span></span>

  ```azurecli
  az network vpn-connection create -n VNet4ToVNet1 -g TestRG1 --vnet-gateway1 VNet4GW -l eastus --shared-key "eeffgg" --vnet-gateway2 VNet1GW
  ```
3. <span data-ttu-id="5b5a2-245">Bağlantılarınızı doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-245">Verify your connections.</span></span> <span data-ttu-id="5b5a2-246">Bkz. [Bağlantınızı doğrulama](#verify).</span><span class="sxs-lookup"><span data-stu-id="5b5a2-246">See [Verify your connection](#verify).</span></span>

## <span data-ttu-id="5b5a2-247"><a name="difsub"></a>Farklı aboneliklerdeki VNet'leri bağlama</span><span class="sxs-lookup"><span data-stu-id="5b5a2-247"><a name="difsub"></a>Connect VNets that are in different subscriptions</span></span>

![v2v diyagramı](./media/vpn-gateway-howto-vnet-vnet-cli/v2vdiffsub.png)

<span data-ttu-id="5b5a2-249">Bu senaryoda TestVNet1 ve TestVNet5 bağlanır.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-249">In this scenario, we connect TestVNet1 and TestVNet5.</span></span> <span data-ttu-id="5b5a2-250">VNet’ler farklı aboneliklerde yer alır.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-250">The VNets reside different subscriptions.</span></span> <span data-ttu-id="5b5a2-251">Aboneliklerin aynı Active Directory kiracısıyla ilişkilendirilmiş olması gerekmez.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-251">The subscriptions do not need to be associated with the same Active Directory tenant.</span></span> <span data-ttu-id="5b5a2-252">Bu yapılandırmanın adımları TestVNet1’i TestVNet5’e bağlamak için Sanal Ağdan Sanal Ağa bir bağlantı daha ekler.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-252">The steps for this configuration add an additional VNet-to-VNet connection in order to connect TestVNet1 to TestVNet5.</span></span>

### <span data-ttu-id="5b5a2-253"><a name="TestVNet1diff"></a>5. Adım - TestVNet1’i oluşturma ve yapılandırma</span><span class="sxs-lookup"><span data-stu-id="5b5a2-253"><a name="TestVNet1diff"></a>Step 5 - Create and configure TestVNet1</span></span>

<span data-ttu-id="5b5a2-254">Bu yönergeler, önceki bölümlerde yer alan adımların devamıdır.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-254">These instructions continue from the steps in the preceding sections.</span></span> <span data-ttu-id="5b5a2-255">TestVNet1 için TestVNet1 ve VPN ağ geçidini oluşturup yapılandırmak için [1. Adımı](#Connect) ve [2. Adımı](#TestVNet1) tamamlamalısınız. </span><span class="sxs-lookup"><span data-stu-id="5b5a2-255">You must complete [Step 1](#Connect) and [Step 2](#TestVNet1) to create and configure TestVNet1 and the VPN Gateway for TestVNet1.</span></span> <span data-ttu-id="5b5a2-256">Bu yapılandırma için önceki bölümdeki TestVNet4’ü oluşturmanız gerekmez, ancak oluşturursanız bu adımlarla çakışmaz.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-256">For this configuration, you are not required to create TestVNet4 from the previous section, although if you do create it, it will not conflict with these steps.</span></span> <span data-ttu-id="5b5a2-257">1. ve 2. Adımı tamamladıktan sonra 6. Adıma (aşağıda) geçin.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-257">Once you complete Step 1 and Step 2, continue with Step 6 (below).</span></span>

### <span data-ttu-id="5b5a2-258"><a name="verifyranges"></a>6. Adım - IP adresi aralıklarını doğrulama</span><span class="sxs-lookup"><span data-stu-id="5b5a2-258"><a name="verifyranges"></a>Step 6 - Verify the IP address ranges</span></span>

<span data-ttu-id="5b5a2-259">Ek bağlantılar oluşturulduğu sırada, yeni sanal ağın IP adresi alanının kendi Sanal Ağ aralıklarınız veya yerel ağ geçidi aralıkları ile çakışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-259">When creating additional connections, it's important to verify that the IP address space of the new virtual network does not overlap with any of your other VNet ranges or local network gateway ranges.</span></span> <span data-ttu-id="5b5a2-260">Bu alıştırmada TestVNet5 için aşağıdaki değerleri kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="5b5a2-260">For this exercise, you can use the following values for the TestVNet5:</span></span>

<span data-ttu-id="5b5a2-261">**Değerler TestVNet5 için:**</span><span class="sxs-lookup"><span data-stu-id="5b5a2-261">**Values for TestVNet5:**</span></span>

* <span data-ttu-id="5b5a2-262">VNet Name: TestVNet5</span><span class="sxs-lookup"><span data-stu-id="5b5a2-262">VNet Name: TestVNet5</span></span>
* <span data-ttu-id="5b5a2-263">Resource Group: TestRG5</span><span class="sxs-lookup"><span data-stu-id="5b5a2-263">Resource Group: TestRG5</span></span>
* <span data-ttu-id="5b5a2-264">Location: Japan East</span><span class="sxs-lookup"><span data-stu-id="5b5a2-264">Location: Japan East</span></span>
* <span data-ttu-id="5b5a2-265">TestVNet5: 10.51.0.0/16 & 10.52.0.0/16</span><span class="sxs-lookup"><span data-stu-id="5b5a2-265">TestVNet5: 10.51.0.0/16 & 10.52.0.0/16</span></span>
* <span data-ttu-id="5b5a2-266">FrontEnd: 10.51.0.0/24</span><span class="sxs-lookup"><span data-stu-id="5b5a2-266">FrontEnd: 10.51.0.0/24</span></span>
* <span data-ttu-id="5b5a2-267">BackEnd: 10.52.0.0/24</span><span class="sxs-lookup"><span data-stu-id="5b5a2-267">BackEnd: 10.52.0.0/24</span></span>
* <span data-ttu-id="5b5a2-268">GatewaySubnet: 10.52.255.0.0/27</span><span class="sxs-lookup"><span data-stu-id="5b5a2-268">GatewaySubnet: 10.52.255.0.0/27</span></span>
* <span data-ttu-id="5b5a2-269">GatewayName: VNet5GW</span><span class="sxs-lookup"><span data-stu-id="5b5a2-269">GatewayName: VNet5GW</span></span>
* <span data-ttu-id="5b5a2-270">Public IP: VNet5GWIP</span><span class="sxs-lookup"><span data-stu-id="5b5a2-270">Public IP: VNet5GWIP</span></span>
* <span data-ttu-id="5b5a2-271">VPNType: RouteBased</span><span class="sxs-lookup"><span data-stu-id="5b5a2-271">VPNType: RouteBased</span></span>
* <span data-ttu-id="5b5a2-272">Connection: VNet5toVNet1</span><span class="sxs-lookup"><span data-stu-id="5b5a2-272">Connection: VNet5toVNet1</span></span>
* <span data-ttu-id="5b5a2-273">ConnectionType: VNet2VNet</span><span class="sxs-lookup"><span data-stu-id="5b5a2-273">ConnectionType: VNet2VNet</span></span>

### <span data-ttu-id="5b5a2-274"><a name="TestVNet5"></a>7. Adım - TestVNet5’i oluşturma ve yapılandırma</span><span class="sxs-lookup"><span data-stu-id="5b5a2-274"><a name="TestVNet5"></a>Step 7 - Create and configure TestVNet5</span></span>

<span data-ttu-id="5b5a2-275">Bu adım, yeni abonelik (5. Abonelik) bağlamında tamamlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-275">This step must be done in the context of the new subscription, Subscription 5.</span></span> <span data-ttu-id="5b5a2-276">Bu kısım, aboneliğin sahibi olan farklı bir kuruluşun yöneticisi tarafından tamamlanabilir.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-276">This part may be performed by the administrator in a different organization that owns the subscription.</span></span> <span data-ttu-id="5b5a2-277">Abonelikler arasında geçiş yapmak için 'az account list --all' komutunu kullanarak hesabınızda kullanılabilen tüm abonelikleri listeleyin ve ardından 'az account set --subscription <subscriptionID>' komutuyla kullanmak istediğiniz aboneliğe geçin.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-277">To switch between subscriptions use 'az account list --all' to list the subscriptions available to your account, then use 'az account set --subscription <subscriptionID>' to switch to the subscription that you want to use.</span></span>

1. <span data-ttu-id="5b5a2-278">5. Aboneliğe bağlı olduğunuzdan emin olun ve bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-278">Make sure you are connected to Subscription 5, then create a resource group.</span></span>

  ```azurecli
  az group create -n TestRG5  -l japaneast
  ```
2. <span data-ttu-id="5b5a2-279">TestVNet5’i oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-279">Create TestVNet5.</span></span>

  ```azurecli
  az network vnet create -n TestVNet5 -g TestRG5 --address-prefix 10.51.0.0/16 -l japaneast --subnet-name FrontEnd --subnet-prefix 10.51.0.0/24
  ```

3. <span data-ttu-id="5b5a2-280">Alt ağlar ekleyin.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-280">Add subnets.</span></span>

  ```azurecli
  az network vnet update -n TestVNet5 --address-prefixes 10.51.0.0/16 10.52.0.0/16 -g TestRG5
  az network vnet subnet create --vnet-name TestVNet5 -n BackEnd -g TestRG5 --address-prefix 10.52.0.0/24
  ```

4. <span data-ttu-id="5b5a2-281">Ağ geçidi alt ağını ekleyin.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-281">Add the gateway subnet.</span></span>

  ```azurecli
  az network vnet subnet create --vnet-name TestVNet5 -n GatewaySubnet -g TestRG5 --address-prefix 10.52.255.0/27
  ```

5. <span data-ttu-id="5b5a2-282">Genel bir IP adresi isteyin.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-282">Request a public IP address.</span></span>

  ```azurecli
  az network public-ip create -n VNet5GWIP -g TestRG5 --allocation-method Dynamic
  ```
6. <span data-ttu-id="5b5a2-283">TestVNet5 ağ geçidini oluşturma</span><span class="sxs-lookup"><span data-stu-id="5b5a2-283">Create the TestVNet5 gateway</span></span>

  ```azurecli
  az network vnet-gateway create -n VNet5GW -l japaneast --public-ip-address VNet5GWIP -g TestRG5 --vnet TestVNet5 --gateway-type Vpn --sku VpnGw1 --vpn-type RouteBased --no-wait
  ```

### <span data-ttu-id="5b5a2-284"><a name="connections5"></a>8. Adım - Bağlantıları oluşturma</span><span class="sxs-lookup"><span data-stu-id="5b5a2-284"><a name="connections5"></a>Step 8 - Create the connections</span></span>

<span data-ttu-id="5b5a2-285">Bu örnekteki ağ geçitleri farklı aboneliklerde olduğundan, bu adımı **[1. Abonelik]** ve **[5. Abonelik]** olarak işaretlenen iki CLI oturumuna ayırdık.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-285">We split this step into two CLI sessions marked as **[Subscription 1]**, and **[Subscription 5]** because the gateways are in the different subscriptions.</span></span> <span data-ttu-id="5b5a2-286">Abonelikler arasında geçiş yapmak için 'az account list --all' komutunu kullanarak hesabınızda kullanılabilen tüm abonelikleri listeleyin ve ardından 'az account set --subscription <subscriptionID>' komutuyla kullanmak istediğiniz aboneliğe geçin.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-286">To switch between subscriptions use 'az account list --all' to list the subscriptions available to your account, then use 'az account set --subscription <subscriptionID>' to switch to the subscription that you want to use.</span></span>

1. <span data-ttu-id="5b5a2-287">**[1. Abonelik]** Oturum açın ve 1. Aboneliğe bağlanın.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-287">**[Subscription 1]** Log in and connect to Subscription 1.</span></span> <span data-ttu-id="5b5a2-288">Çıktıdan Ağ Geçidinin adını ve kimliğini almak için şu komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="5b5a2-288">Run the following command to get the name and ID of the Gateway from the output:</span></span>

  ```azurecli
  az network vnet-gateway show -n VNet1GW -g TestRG1
  ```

  <span data-ttu-id="5b5a2-289">"id:" çıktısını kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-289">Copy the output for "id:".</span></span> <span data-ttu-id="5b5a2-290">VNet ağ geçidinin (VNet1GW) kimliğini ve adını e-postayla veya başka bir yolla 5. Aboneliğin yöneticisine gönderin.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-290">Send the ID and the name of the VNet gateway (VNet1GW) to the administrator of Subscription 5 via email or another method.</span></span>

  <span data-ttu-id="5b5a2-291">Örnek çıktı:</span><span class="sxs-lookup"><span data-stu-id="5b5a2-291">Example output:</span></span>

  ```
  "id": "/subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW"
  ```

2. <span data-ttu-id="5b5a2-292">**[5. Abonelik]** Oturum açın ve 5. Aboneliğe bağlanın.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-292">**[Subscription 5]** Log in and connect to Subscription 5.</span></span> <span data-ttu-id="5b5a2-293">Çıktıdan Ağ Geçidinin adını ve kimliğini almak için şu komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="5b5a2-293">Run the following command to get the name and ID of the Gateway from the output:</span></span>

  ```azurecli
  az network vnet-gateway show -n VNet5GW -g TestRG5
  ```

  <span data-ttu-id="5b5a2-294">"id:" çıktısını kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-294">Copy the output for "id:".</span></span> <span data-ttu-id="5b5a2-295">VNet ağ geçidinin (VNet5GW) kimliğini ve adını e-postayla veya başka bir yolla 1. Aboneliğin yöneticisine gönderin.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-295">Send the ID and the name of the VNet gateway (VNet5GW) to the administrator of Subscription 1 via email or another method.</span></span>

3. <span data-ttu-id="5b5a2-296">**[1. Abonelik]** Bu adımda TestVNet1 ile TestVNet5 arasında bağlantı oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-296">**[Subscription 1]** In this step, you create the connection from TestVNet1 to TestVNet5.</span></span> <span data-ttu-id="5b5a2-297">Paylaşılan anahtar için kendi değerlerinizi kullanabilirsiniz, ancak her iki bağlantı için de paylaşılan anahtarın eşleşmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-297">You can use your own values for the shared key, however, the shared key must match for both connections.</span></span> <span data-ttu-id="5b5a2-298">Bir bağlantı oluşturmak çok zaman almaz.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-298">Creating a connection can take a short while to complete.</span></span> <span data-ttu-id="5b5a2-299">1 Abonelik’e bağlandığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-299">Make sure you connect to Subscription 1.</span></span>

  ```azurecli
  az network vpn-connection create -n VNet1ToVNet5 -g TestRG1 --vnet-gateway1 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW -l eastus --shared-key "eeffgg" --vnet-gateway2 /subscriptions/e7e33b39-fe28-4822-b65c-a4db8bbff7cb/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW
  ```

4. <span data-ttu-id="5b5a2-300">**[5. Abonelik]** Bu adım, bağlantıyı TestVNet5’ten TestVNet1’e doğru kuracak olmanızın dışında yukarıdaki adımla aynıdır.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-300">**[Subscription 5]** This step is similar to the one above, except you are creating the connection from TestVNet5 to TestVNet1.</span></span> <span data-ttu-id="5b5a2-301">Paylaşılan anahtarların eşleştiğinden ve 5. Aboneliğe bağlandığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-301">Make sure that the shared keys match and that you connect to Subscription 5.</span></span>

  ```azurecli
  az network vpn-connection create -n VNet5ToVNet1 -g TestRG5 --vnet-gateway1 /subscriptions/e7e33b39-fe28-4822-b65c-a4db8bbff7cb/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW -l japaneast --shared-key "eeffgg" --vnet-gateway2 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW
  ```

## <span data-ttu-id="5b5a2-302"><a name="verify"></a>Bağlantıları doğrulama</span><span class="sxs-lookup"><span data-stu-id="5b5a2-302"><a name="verify"></a>Verify the connections</span></span>
[!INCLUDE [vpn-gateway-no-nsg-include](../../includes/vpn-gateway-no-nsg-include.md)]

[!INCLUDE [verify connections v2v cli](../../includes/vpn-gateway-verify-connection-cli-rm-include.md)]

## <span data-ttu-id="5b5a2-303"><a name="faq"></a>Sanal ağlar arası bağlantılar hakkında SSS</span><span class="sxs-lookup"><span data-stu-id="5b5a2-303"><a name="faq"></a>VNet-to-VNet FAQ</span></span>
[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]

## <a name="next-steps"></a><span data-ttu-id="5b5a2-304">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5b5a2-304">Next steps</span></span>

* <span data-ttu-id="5b5a2-305">Bağlantınız tamamlandıktan sonra sanal ağlarınıza sanal makineler ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-305">Once your connection is complete, you can add virtual machines to your virtual networks.</span></span> <span data-ttu-id="5b5a2-306">Daha fazla bilgi edinmek için bkz. [Sanal Makineler ile ilgili belgeler](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span><span class="sxs-lookup"><span data-stu-id="5b5a2-306">For more information, see the [Virtual Machines documentation](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span></span>
* <span data-ttu-id="5b5a2-307">BGP hakkında bilgi edinmek için [BGP’ye Genel Bakış](vpn-gateway-bgp-overview.md) ve [BGP’yi yapılandırma](vpn-gateway-bgp-resource-manager-ps.md) makalelerine bakın.</span><span class="sxs-lookup"><span data-stu-id="5b5a2-307">For information about BGP, see the [BGP Overview](vpn-gateway-bgp-overview.md) and [How to configure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span></span>
