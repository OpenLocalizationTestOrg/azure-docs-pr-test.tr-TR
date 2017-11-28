---
title: "Bir Azure sanal ağı tooanother VNet bağlanın: PowerShell | Microsoft Docs"
description: "Bu makalede Azure Resource Manager ve PowerShell kullanarak sanal ağları birbirine bağlama konusu incelenmektedir."
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
ms.openlocfilehash: 2da30c76867cc3f71d040e63e0dd15d153e15c10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-vnet-to-vnet-vpn-gateway-connection-using-powershell"></a><span data-ttu-id="09d1b-103">PowerShell kullanarak sanal ağlar arası VPN ağ geçidi bağlantısı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="09d1b-103">Configure a VNet-to-VNet VPN gateway connection using PowerShell</span></span>

<span data-ttu-id="09d1b-104">Bu makale size nasıl gösterir toocreate sanal ağlar arasında bir VPN ağ geçidi bağlantısı.</span><span class="sxs-lookup"><span data-stu-id="09d1b-104">This article shows you how toocreate a VPN gateway connection between virtual networks.</span></span> <span data-ttu-id="09d1b-105">Merhaba sanal ağları olabilir hello aynı ya da farklı bölgelerde ve gelen aynı hello ya da farklı Aboneliklerde.</span><span class="sxs-lookup"><span data-stu-id="09d1b-105">hello virtual networks can be in hello same or different regions, and from hello same or different subscriptions.</span></span> <span data-ttu-id="09d1b-106">Bağlanan sanal ağlar farklı aboneliklerden hello abonelikleri ile ilişkili toobe gerekmediğinde aynı Active Directory Kiracı hello.</span><span class="sxs-lookup"><span data-stu-id="09d1b-106">When connecting VNets from different subscriptions, hello subscriptions do not need toobe associated with hello same Active Directory tenant.</span></span> 

<span data-ttu-id="09d1b-107">Bu makaledeki adımları Hello toohello Resource Manager dağıtım modeli uygulanır ve PowerShell kullanın.</span><span class="sxs-lookup"><span data-stu-id="09d1b-107">hello steps in this article apply toohello Resource Manager deployment model and use PowerShell.</span></span> <span data-ttu-id="09d1b-108">Liste aşağıdaki hello farklı bir seçeneği seçerek farklı dağıtım aracını veya dağıtım modelini kullanarak bu yapılandırma ayrıca oluşturabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="09d1b-108">You can also create this configuration using a different deployment tool or deployment model by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="09d1b-109">Azure portal</span><span class="sxs-lookup"><span data-stu-id="09d1b-109">Azure portal</span></span>](vpn-gateway-howto-vnet-vnet-resource-manager-portal.md)
> * [<span data-ttu-id="09d1b-110">PowerShell</span><span class="sxs-lookup"><span data-stu-id="09d1b-110">PowerShell</span></span>](vpn-gateway-vnet-vnet-rm-ps.md)
> * [<span data-ttu-id="09d1b-111">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="09d1b-111">Azure CLI</span></span>](vpn-gateway-howto-vnet-vnet-cli.md)
> * [<span data-ttu-id="09d1b-112">Azure portal (klasik)</span><span class="sxs-lookup"><span data-stu-id="09d1b-112">Azure portal (classic)</span></span>](vpn-gateway-howto-vnet-vnet-portal-classic.md)
> * [<span data-ttu-id="09d1b-113">Farklı dağıtım modellerini bağlama - Azure portalı</span><span class="sxs-lookup"><span data-stu-id="09d1b-113">Connect different deployment models - Azure portal</span></span>](vpn-gateway-connect-different-deployment-models-portal.md)
> * [<span data-ttu-id="09d1b-114">Farklı dağıtım modellerini bağlama - PowerShell</span><span class="sxs-lookup"><span data-stu-id="09d1b-114">Connect different deployment models - PowerShell</span></span>](vpn-gateway-connect-different-deployment-models-powershell.md)
>
>

<span data-ttu-id="09d1b-115">Sanal ağ tooanother sanal ağ (VNet-VNet) bağlanma benzer tooconnecting bir VNet tooan şirket içi site konumu değil.</span><span class="sxs-lookup"><span data-stu-id="09d1b-115">Connecting a virtual network tooanother virtual network (VNet-to-VNet) is similar tooconnecting a VNet tooan on-premises site location.</span></span> <span data-ttu-id="09d1b-116">Her iki bağlantı türü bir VPN ağ geçidi tooprovide IPSec/IKE kullanarak güvenli bir tünel kullanın.</span><span class="sxs-lookup"><span data-stu-id="09d1b-116">Both connectivity types use a VPN gateway tooprovide a secure tunnel using IPsec/IKE.</span></span> <span data-ttu-id="09d1b-117">Sanal ağlar hello varsa aynı bölgede VNet eşlemesi kullanarak bunları bağlanma tooconsider isteyebilir.</span><span class="sxs-lookup"><span data-stu-id="09d1b-117">If your VNets are in hello same region, you may want tooconsider connecting them using VNet Peering.</span></span> <span data-ttu-id="09d1b-118">VNet eşlemesi VPN ağ geçidini kullanmaz.</span><span class="sxs-lookup"><span data-stu-id="09d1b-118">VNet peering does not use a VPN gateway.</span></span> <span data-ttu-id="09d1b-119">Daha fazla bilgi için bkz. [VNet eşlemesi](../virtual-network/virtual-network-peering-overview.md).</span><span class="sxs-lookup"><span data-stu-id="09d1b-119">For more information, see [VNet peering](../virtual-network/virtual-network-peering-overview.md).</span></span>

<span data-ttu-id="09d1b-120">Hatta Sanal Ağdan Sanal Ağa iletişim çok siteli yapılandırmalarla bile birleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="09d1b-120">VNet-to-VNet communication can be combined with multi-site configurations.</span></span> <span data-ttu-id="09d1b-121">Hello Aşağıdaki diyagramda gösterildiği gibi arası sanal ağ bağlantısı ile şirket içi bağlantılar birleştiren ağ topolojileri kurabilmenize olanak sağlar:</span><span class="sxs-lookup"><span data-stu-id="09d1b-121">This lets you establish network topologies that combine cross-premises connectivity with inter-virtual network connectivity, as shown in hello following diagram:</span></span>

![Bağlantılar hakkında](./media/vpn-gateway-vnet-vnet-rm-ps/aboutconnections.png)

### <a name="why-connect-virtual-networks"></a><span data-ttu-id="09d1b-123">Sanal ağları neden bağlamalıyız?</span><span class="sxs-lookup"><span data-stu-id="09d1b-123">Why connect virtual networks?</span></span>

<span data-ttu-id="09d1b-124">Aşağıdaki nedenlerden Merhaba tooconnect sanal ağlar isteyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="09d1b-124">You may want tooconnect virtual networks for hello following reasons:</span></span>

* <span data-ttu-id="09d1b-125">**Çapraz bölge coğrafi artıklığı ve coğrafi-durum**</span><span class="sxs-lookup"><span data-stu-id="09d1b-125">**Cross region geo-redundancy and geo-presence**</span></span>

  * <span data-ttu-id="09d1b-126">Kendi coğrafi çoğaltma veya eşitlemenizi, güvenli bağlantıyla İnternet’te uç noktalara gitmeden ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="09d1b-126">You can set up your own geo-replication or synchronization with secure connectivity without going over Internet-facing endpoints.</span></span>
  * <span data-ttu-id="09d1b-127">Azure Traffic Manager ve Load Balancer ile birçok Azure bölgesinde coğrafi yedeklilik imkanıyla yüksek oranda kullanılabilir iş yükü oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="09d1b-127">With Azure Traffic Manager and Load Balancer, you can set up highly available workload with geo-redundancy across multiple Azure regions.</span></span> <span data-ttu-id="09d1b-128">Bir önemli SQL Always On kullanılabilirlik grupları: birden fazla Azure bölgesine yayılan ile yukarı tooset örnektir.</span><span class="sxs-lookup"><span data-stu-id="09d1b-128">One important example is tooset up SQL Always On with Availability Groups spreading across multiple Azure regions.</span></span>
* <span data-ttu-id="09d1b-129">**Yalıtım veya yönetim sınır bölgesel çok katmanlı uygulamalar**</span><span class="sxs-lookup"><span data-stu-id="09d1b-129">**Regional multi-tier applications with isolation or administrative boundary**</span></span>

  * <span data-ttu-id="09d1b-130">İçinde hello aynı bölge tooisolation ya da yönetim gereksinimleri birbirlerine bağlı birden çok sanal ağ ile çok katmanlı uygulamalar ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="09d1b-130">Within hello same region, you can set up multi-tier applications with multiple virtual networks connected together due tooisolation or administrative requirements.</span></span>

<span data-ttu-id="09d1b-131">VNet-VNet bağlantıları hakkında daha fazla bilgi için bkz: Merhaba [VNet-VNet ile ilgili SSS](#faq) hello bu makalenin sonunda.</span><span class="sxs-lookup"><span data-stu-id="09d1b-131">For more information about VNet-to-VNet connections, see hello [VNet-to-VNet FAQ](#faq) at hello end of this article.</span></span>

## <a name="which-set-of-steps-should-i-use"></a><span data-ttu-id="09d1b-132">Hangi adımları tamamlamalıyım? </span><span class="sxs-lookup"><span data-stu-id="09d1b-132">Which set of steps should I use?</span></span>

<span data-ttu-id="09d1b-133">Bu makalede iki farklı adım kümesi görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="09d1b-133">In this article, you see two different sets of steps.</span></span> <span data-ttu-id="09d1b-134">Adımlar için bir dizi [içinde bulunan sanal ağlar aynı abonelik hello](#samesub), diğeri [farklı Aboneliklerde bulunan sanal ağlar](#difsub).</span><span class="sxs-lookup"><span data-stu-id="09d1b-134">One set of steps for [VNets that reside in hello same subscription](#samesub), and another for [VNets that reside in different subscriptions](#difsub).</span></span> <span data-ttu-id="09d1b-135">Merhaba anahtar hello kümeleri arasında olup olmadığını oluşturabilir ve hello içindeki tüm sanal ağ ve ağ geçidi kaynaklarını yapılandırma farktır aynı PowerShell oturumunda.</span><span class="sxs-lookup"><span data-stu-id="09d1b-135">hello key difference between hello sets is whether you can create and configure all virtual network and gateway resources within hello same PowerShell session.</span></span>

<span data-ttu-id="09d1b-136">Merhaba bu makaledeki adımları hello her bölümün başında bildirilen değişkenlerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="09d1b-136">hello steps in this article use variables that are declared at hello beginning of each section.</span></span> <span data-ttu-id="09d1b-137">Varolan sanal ağlar ile çalışıyorsanız, kendi ortamınızdaki hello değişkenleri tooreflect hello ayarlarını değiştirin.</span><span class="sxs-lookup"><span data-stu-id="09d1b-137">If you already are working with existing VNets, modify hello variables tooreflect hello settings in your own environment.</span></span> <span data-ttu-id="09d1b-138">Sanal ağlarınız için ad çözümlemesi istiyorsanız bkz. [Ad çözümlemesi](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span><span class="sxs-lookup"><span data-stu-id="09d1b-138">If you want name resolution for your virtual networks, see [Name resolution](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span></span>

## <span data-ttu-id="09d1b-139"><a name="samesub"></a>Nasıl tooconnect sanal ağlar olan hello aynı abonelik</span><span class="sxs-lookup"><span data-stu-id="09d1b-139"><a name="samesub"></a>How tooconnect VNets that are in hello same subscription</span></span>

![v2v diyagramı](./media/vpn-gateway-vnet-vnet-rm-ps/v2vrmps.png)

### <a name="before-you-begin"></a><span data-ttu-id="09d1b-141">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="09d1b-141">Before you begin</span></span>

<span data-ttu-id="09d1b-142">Başlamadan önce tooinstall hello en son sürümünü hello Azure Resource Manager PowerShell cmdlet'leri, en az 4.0 veya sonraki sürümü gerekir.</span><span class="sxs-lookup"><span data-stu-id="09d1b-142">Before beginning, you need tooinstall hello latest version of hello Azure Resource Manager PowerShell cmdlets, at least 4.0 or later.</span></span> <span data-ttu-id="09d1b-143">Merhaba PowerShell cmdlet'lerini yükleme hakkında daha fazla bilgi için bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="09d1b-143">For more information about installing hello PowerShell cmdlets, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

### <span data-ttu-id="09d1b-144"><a name="Step1"></a>1. adım -, IP adres aralıklarını planlama</span><span class="sxs-lookup"><span data-stu-id="09d1b-144"><a name="Step1"></a>Step 1 - Plan your IP address ranges</span></span>

<span data-ttu-id="09d1b-145">Aşağıdaki adımları hello, kullanıcıların kendi ağ geçidi alt ağları ve yapılandırmalarıyla birlikte iki sanal ağ oluşturun.</span><span class="sxs-lookup"><span data-stu-id="09d1b-145">In hello following steps, we create two virtual networks along with their respective gateway subnets and configurations.</span></span> <span data-ttu-id="09d1b-146">Ardından hello arasında bir VPN bağlantısı iki Vnet oluşturuyoruz.</span><span class="sxs-lookup"><span data-stu-id="09d1b-146">We then create a VPN connection between hello two VNets.</span></span> <span data-ttu-id="09d1b-147">Önemli tooplan başlangıç IP adresi aralıklarını ağ yapılandırmanızı olur.</span><span class="sxs-lookup"><span data-stu-id="09d1b-147">It’s important tooplan hello IP address ranges for your network configuration.</span></span> <span data-ttu-id="09d1b-148">Sanal ağ aralıklarınızın ya da yerel ağ aralıklarınızın hiçbir şekilde çakışmadığından emin olmalısınız.</span><span class="sxs-lookup"><span data-stu-id="09d1b-148">Keep in mind that you must make sure that none of your VNet ranges or local network ranges overlap in any way.</span></span> <span data-ttu-id="09d1b-149">Bu örneklerde bir DNS sunucusu eklemiyoruz.</span><span class="sxs-lookup"><span data-stu-id="09d1b-149">In these examples, we do not include a DNS server.</span></span> <span data-ttu-id="09d1b-150">Sanal ağlarınız için ad çözümlemesi istiyorsanız bkz. [Ad çözümlemesi](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span><span class="sxs-lookup"><span data-stu-id="09d1b-150">If you want name resolution for your virtual networks, see [Name resolution](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span></span>

<span data-ttu-id="09d1b-151">Merhaba örnekleri değerleri aşağıdaki hello kullanırız:</span><span class="sxs-lookup"><span data-stu-id="09d1b-151">We use hello following values in hello examples:</span></span>

<span data-ttu-id="09d1b-152">**Değerler TestVNet1 için:**</span><span class="sxs-lookup"><span data-stu-id="09d1b-152">**Values for TestVNet1:**</span></span>

* <span data-ttu-id="09d1b-153">VNet Name: TestVNet1</span><span class="sxs-lookup"><span data-stu-id="09d1b-153">VNet Name: TestVNet1</span></span>
* <span data-ttu-id="09d1b-154">Resource Group: TestRG1</span><span class="sxs-lookup"><span data-stu-id="09d1b-154">Resource Group: TestRG1</span></span>
* <span data-ttu-id="09d1b-155">Location: East US</span><span class="sxs-lookup"><span data-stu-id="09d1b-155">Location: East US</span></span>
* <span data-ttu-id="09d1b-156">TestVNet1: 10.11.0.0/16 & 10.12.0.0/16</span><span class="sxs-lookup"><span data-stu-id="09d1b-156">TestVNet1: 10.11.0.0/16 & 10.12.0.0/16</span></span>
* <span data-ttu-id="09d1b-157">FrontEnd: 10.11.0.0/24</span><span class="sxs-lookup"><span data-stu-id="09d1b-157">FrontEnd: 10.11.0.0/24</span></span>
* <span data-ttu-id="09d1b-158">BackEnd: 10.12.0.0/24</span><span class="sxs-lookup"><span data-stu-id="09d1b-158">BackEnd: 10.12.0.0/24</span></span>
* <span data-ttu-id="09d1b-159">GatewaySubnet: 10.12.255.0/27</span><span class="sxs-lookup"><span data-stu-id="09d1b-159">GatewaySubnet: 10.12.255.0/27</span></span>
* <span data-ttu-id="09d1b-160">GatewayName: VNet1GW</span><span class="sxs-lookup"><span data-stu-id="09d1b-160">GatewayName: VNet1GW</span></span>
* <span data-ttu-id="09d1b-161">Public IP: VNet1GWIP</span><span class="sxs-lookup"><span data-stu-id="09d1b-161">Public IP: VNet1GWIP</span></span>
* <span data-ttu-id="09d1b-162">VPNType: RouteBased</span><span class="sxs-lookup"><span data-stu-id="09d1b-162">VPNType: RouteBased</span></span>
* <span data-ttu-id="09d1b-163">Connection(1to4): VNet1toVNet4</span><span class="sxs-lookup"><span data-stu-id="09d1b-163">Connection(1to4): VNet1toVNet4</span></span>
* <span data-ttu-id="09d1b-164">Connection(1to5): VNet1toVNet5</span><span class="sxs-lookup"><span data-stu-id="09d1b-164">Connection(1to5): VNet1toVNet5</span></span>
* <span data-ttu-id="09d1b-165">ConnectionType: VNet2VNet</span><span class="sxs-lookup"><span data-stu-id="09d1b-165">ConnectionType: VNet2VNet</span></span>

<span data-ttu-id="09d1b-166">**Değerler TestVNet4 için:**</span><span class="sxs-lookup"><span data-stu-id="09d1b-166">**Values for TestVNet4:**</span></span>

* <span data-ttu-id="09d1b-167">VNet Name: TestVNet4</span><span class="sxs-lookup"><span data-stu-id="09d1b-167">VNet Name: TestVNet4</span></span>
* <span data-ttu-id="09d1b-168">TestVNet2: 10.41.0.0/16 & 10.42.0.0/16</span><span class="sxs-lookup"><span data-stu-id="09d1b-168">TestVNet2: 10.41.0.0/16 & 10.42.0.0/16</span></span>
* <span data-ttu-id="09d1b-169">FrontEnd: 10.41.0.0/24</span><span class="sxs-lookup"><span data-stu-id="09d1b-169">FrontEnd: 10.41.0.0/24</span></span>
* <span data-ttu-id="09d1b-170">BackEnd: 10.42.0.0/24</span><span class="sxs-lookup"><span data-stu-id="09d1b-170">BackEnd: 10.42.0.0/24</span></span>
* <span data-ttu-id="09d1b-171">GatewaySubnet: 10.42.255.0/27</span><span class="sxs-lookup"><span data-stu-id="09d1b-171">GatewaySubnet: 10.42.255.0/27</span></span>
* <span data-ttu-id="09d1b-172">Resource Group: TestRG4</span><span class="sxs-lookup"><span data-stu-id="09d1b-172">Resource Group: TestRG4</span></span>
* <span data-ttu-id="09d1b-173">Location: West US</span><span class="sxs-lookup"><span data-stu-id="09d1b-173">Location: West US</span></span>
* <span data-ttu-id="09d1b-174">GatewayName: VNet4GW</span><span class="sxs-lookup"><span data-stu-id="09d1b-174">GatewayName: VNet4GW</span></span>
* <span data-ttu-id="09d1b-175">Public IP: VNet4GWIP</span><span class="sxs-lookup"><span data-stu-id="09d1b-175">Public IP: VNet4GWIP</span></span>
* <span data-ttu-id="09d1b-176">VPNType: RouteBased</span><span class="sxs-lookup"><span data-stu-id="09d1b-176">VPNType: RouteBased</span></span>
* <span data-ttu-id="09d1b-177">Connection: VNet4toVNet1</span><span class="sxs-lookup"><span data-stu-id="09d1b-177">Connection: VNet4toVNet1</span></span>
* <span data-ttu-id="09d1b-178">ConnectionType: VNet2VNet</span><span class="sxs-lookup"><span data-stu-id="09d1b-178">ConnectionType: VNet2VNet</span></span>


### <span data-ttu-id="09d1b-179"><a name="Step2"></a>Adım 2 - oluşturma ve TestVNet1 yapılandırma</span><span class="sxs-lookup"><span data-stu-id="09d1b-179"><a name="Step2"></a>Step 2 - Create and configure TestVNet1</span></span>

1. <span data-ttu-id="09d1b-180">Değişkenlerinizi bildirin.</span><span class="sxs-lookup"><span data-stu-id="09d1b-180">Declare your variables.</span></span> <span data-ttu-id="09d1b-181">Bu örnekte bu alıştırmada hello değerleri kullanarak hello değişkenler bildirilmektedir.</span><span class="sxs-lookup"><span data-stu-id="09d1b-181">This example declares hello variables using hello values for this exercise.</span></span> <span data-ttu-id="09d1b-182">Çoğu durumda, hello değerleri kendinizinkilerle değiştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="09d1b-182">In most cases, you should replace hello values with your own.</span></span> <span data-ttu-id="09d1b-183">Ancak, hello adımları toobecome yapılandırma bu tür tanıdık aracılığıyla çalıştırıyorsanız, bu değişkenleri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="09d1b-183">However, you can use these variables if you are running through hello steps toobecome familiar with this type of configuration.</span></span> <span data-ttu-id="09d1b-184">Gerekirse, hello değişkenleri değiştirin, sonra kopyalayın ve PowerShell konsolunuza yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="09d1b-184">Modify hello variables if needed, then copy and paste them into your PowerShell console.</span></span>

  ```powershell
  $Sub1 = "Replace_With_Your_Subcription_Name"
  $RG1 = "TestRG1"
  $Location1 = "East US"
  $VNetName1 = "TestVNet1"
  $FESubName1 = "FrontEnd"
  $BESubName1 = "Backend"
  $GWSubName1 = "GatewaySubnet"
  $VNetPrefix11 = "10.11.0.0/16"
  $VNetPrefix12 = "10.12.0.0/16"
  $FESubPrefix1 = "10.11.0.0/24"
  $BESubPrefix1 = "10.12.0.0/24"
  $GWSubPrefix1 = "10.12.255.0/27"
  $GWName1 = "VNet1GW"
  $GWIPName1 = "VNet1GWIP"
  $GWIPconfName1 = "gwipconf1"
  $Connection14 = "VNet1toVNet4"
  $Connection15 = "VNet1toVNet5"
  ```

2. <span data-ttu-id="09d1b-185">Tooyour hesabı bağlayın.</span><span class="sxs-lookup"><span data-stu-id="09d1b-185">Connect tooyour account.</span></span> <span data-ttu-id="09d1b-186">Bağlandığınız örnek toohelp aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="09d1b-186">Use hello following example toohelp you connect:</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

  <span data-ttu-id="09d1b-187">Merhaba hesabının Hello abonelikleri kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="09d1b-187">Check hello subscriptions for hello account.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```

  <span data-ttu-id="09d1b-188">Merhaba abonelik toouse istediğinizi belirtin.</span><span class="sxs-lookup"><span data-stu-id="09d1b-188">Specify hello subscription that you want toouse.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionName $Sub1
  ```
3. <span data-ttu-id="09d1b-189">Yeni bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="09d1b-189">Create a new resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name $RG1 -Location $Location1
  ```
4. <span data-ttu-id="09d1b-190">TestVNet1 için alt ağ yapılandırmaları Hello oluşturun.</span><span class="sxs-lookup"><span data-stu-id="09d1b-190">Create hello subnet configurations for TestVNet1.</span></span> <span data-ttu-id="09d1b-191">Bu örnekte TestVNet1 adlı bir sanal ağ ve üç alt ağ oluşturulmaktadır. Biri GatewaySubnet, biri FrontEnd, diğeri BackEnd’dir.</span><span class="sxs-lookup"><span data-stu-id="09d1b-191">This example creates a virtual network named TestVNet1 and three subnets, one called GatewaySubnet, one called FrontEnd, and one called Backend.</span></span> <span data-ttu-id="09d1b-192">Kendi değerlerinizi yerleştirirken ağ geçidi alt ağınızı özellikle GatewaySubnet olarak adlandırmanız önem taşır.</span><span class="sxs-lookup"><span data-stu-id="09d1b-192">When substituting values, it's important that you always name your gateway subnet specifically GatewaySubnet.</span></span> <span data-ttu-id="09d1b-193">Başka bir ad kullanırsanız ağ geçidi oluşturma işleminiz başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="09d1b-193">If you name it something else, your gateway creation fails.</span></span>

  <span data-ttu-id="09d1b-194">Merhaba aşağıdaki örnek daha önce belirlediğiniz hello değişkenleri kullanır.</span><span class="sxs-lookup"><span data-stu-id="09d1b-194">hello following example uses hello variables that you set earlier.</span></span> <span data-ttu-id="09d1b-195">Bu örnekte, hello ağ geçidi alt ağı/27 kullanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="09d1b-195">In this example, hello gateway subnet is using a /27.</span></span> <span data-ttu-id="09d1b-196">Olası toocreate ağ geçidi alt ağı /29 küçük olmakla birlikte, en az/28 veya /27 seçerek daha fazla adreslerini içeren daha büyük bir alt ağı oluşturmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="09d1b-196">While it is possible toocreate a gateway subnet as small as /29, we recommend that you create a larger subnet that includes more addresses by selecting at least /28 or /27.</span></span> <span data-ttu-id="09d1b-197">Bu, gelecekteki hello isteyebileceğiniz yeterli adresleri tooaccommodate olası ek yapılandırmalar için izin verir.</span><span class="sxs-lookup"><span data-stu-id="09d1b-197">This will allow for enough addresses tooaccommodate possible additional configurations that you may want in hello future.</span></span>

  ```powershell
  $fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1
  $besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
  $gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1
  ```
5. <span data-ttu-id="09d1b-198">TestVNet1’i oluşturun.</span><span class="sxs-lookup"><span data-stu-id="09d1b-198">Create TestVNet1.</span></span>

  ```powershell
  New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 `
  -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1
  ```
6. <span data-ttu-id="09d1b-199">Ağınız için oluşturacağınız bir ortak IP adresi toobe ayrılmış toohello ağ geçidi isteği.</span><span class="sxs-lookup"><span data-stu-id="09d1b-199">Request a public IP address toobe allocated toohello gateway you will create for your VNet.</span></span> <span data-ttu-id="09d1b-200">Bu hello AllocationMethod dinamik olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="09d1b-200">Notice that hello AllocationMethod is Dynamic.</span></span> <span data-ttu-id="09d1b-201">Başlangıç IP adresi toouse istediğiniz belirtemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="09d1b-201">You cannot specify hello IP address that you want toouse.</span></span> <span data-ttu-id="09d1b-202">Dinamik olarak ayrılan tooyour geçididir.</span><span class="sxs-lookup"><span data-stu-id="09d1b-202">It's dynamically allocated tooyour gateway.</span></span> 

  ```powershell
  $gwpip1 = New-AzureRmPublicIpAddress -Name $GWIPName1 -ResourceGroupName $RG1 `
  -Location $Location1 -AllocationMethod Dynamic
  ```
7. <span data-ttu-id="09d1b-203">Merhaba ağ geçidi yapılandırmasını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="09d1b-203">Create hello gateway configuration.</span></span> <span data-ttu-id="09d1b-204">Merhaba ağ geçidi yapılandırmasını hello alt ağı ve hello ortak IP adresi toouse tanımlar.</span><span class="sxs-lookup"><span data-stu-id="09d1b-204">hello gateway configuration defines hello subnet and hello public IP address toouse.</span></span> <span data-ttu-id="09d1b-205">Merhaba örnek toocreate, ağ geçidi yapılandırmasını kullanın.</span><span class="sxs-lookup"><span data-stu-id="09d1b-205">Use hello example toocreate your gateway configuration.</span></span>

  ```powershell
  $vnet1 = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
  $subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
  $gwipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName1 `
  -Subnet $subnet1 -PublicIpAddress $gwpip1
  ```
8. <span data-ttu-id="09d1b-206">TestVNet1 için Hello ağ geçidi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="09d1b-206">Create hello gateway for TestVNet1.</span></span> <span data-ttu-id="09d1b-207">Bu adımda TestVNet1'iniz için hello sanal ağ geçidi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="09d1b-207">In this step, you create hello virtual network gateway for your TestVNet1.</span></span> <span data-ttu-id="09d1b-208">Sanal Ağdan Sanal Ağa yapılandırmaları, RouteBased bir VPNType gerektirir.</span><span class="sxs-lookup"><span data-stu-id="09d1b-208">VNet-to-VNet configurations require a RouteBased VpnType.</span></span> <span data-ttu-id="09d1b-209">Bir ağ geçidi oluşturma 45 dakika veya daha fazla hello seçilen ağ geçidi SKU'su bağlı olarak genellikle alabilir.</span><span class="sxs-lookup"><span data-stu-id="09d1b-209">Creating a gateway can often take 45 minutes or more, depending on hello selected gateway SKU.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 `
  -Location $Location1 -IpConfigurations $gwipconf1 -GatewayType Vpn `
  -VpnType RouteBased -GatewaySku VpnGw1
  ```

### <a name="step-3---create-and-configure-testvnet4"></a><span data-ttu-id="09d1b-210">3. Adım - TestVNet4’ü oluşturma ve yapılandırma</span><span class="sxs-lookup"><span data-stu-id="09d1b-210">Step 3 - Create and configure TestVNet4</span></span>

<span data-ttu-id="09d1b-211">TestVNet1 yapılandırıldıktan sonra TestVNet4’ü oluşturun.</span><span class="sxs-lookup"><span data-stu-id="09d1b-211">Once you've configured TestVNet1, create TestVNet4.</span></span> <span data-ttu-id="09d1b-212">Aşağıda, hello değerleri gerektiğinde kendi dosyanızı değiştirerek hello adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="09d1b-212">Follow hello steps below, replacing hello values with your own when needed.</span></span> <span data-ttu-id="09d1b-213">Bu adım hello içinde aynı yapılabilir PowerShell oturumu olduğundan hello aynı abonelik.</span><span class="sxs-lookup"><span data-stu-id="09d1b-213">This step can be done within hello same PowerShell session because it is in hello same subscription.</span></span>

1. <span data-ttu-id="09d1b-214">Değişkenlerinizi bildirin.</span><span class="sxs-lookup"><span data-stu-id="09d1b-214">Declare your variables.</span></span> <span data-ttu-id="09d1b-215">Merhaba olanları hello değerlerle emin tooreplace olması yapılandırmanızın toouse istiyor.</span><span class="sxs-lookup"><span data-stu-id="09d1b-215">Be sure tooreplace hello values with hello ones that you want toouse for your configuration.</span></span>

  ```powershell
  $RG4 = "TestRG4"
  $Location4 = "West US"
  $VnetName4 = "TestVNet4"
  $FESubName4 = "FrontEnd"
  $BESubName4 = "Backend"
  $GWSubName4 = "GatewaySubnet"
  $VnetPrefix41 = "10.41.0.0/16"
  $VnetPrefix42 = "10.42.0.0/16"
  $FESubPrefix4 = "10.41.0.0/24"
  $BESubPrefix4 = "10.42.0.0/24"
  $GWSubPrefix4 = "10.42.255.0/27"
  $GWName4 = "VNet4GW"
  $GWIPName4 = "VNet4GWIP"
  $GWIPconfName4 = "gwipconf4"
  $Connection41 = "VNet4toVNet1"
  ```
2. <span data-ttu-id="09d1b-216">Yeni bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="09d1b-216">Create a new resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name $RG4 -Location $Location4
  ```
3. <span data-ttu-id="09d1b-217">Merhaba TestVNet4 için alt ağ yapılandırmaları oluşturun.</span><span class="sxs-lookup"><span data-stu-id="09d1b-217">Create hello subnet configurations for TestVNet4.</span></span>

  ```powershell
  $fesub4 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName4 -AddressPrefix $FESubPrefix4
  $besub4 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName4 -AddressPrefix $BESubPrefix4
  $gwsub4 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName4 -AddressPrefix $GWSubPrefix4
  ```
4. <span data-ttu-id="09d1b-218">TestVNet4’ü oluşturun.</span><span class="sxs-lookup"><span data-stu-id="09d1b-218">Create TestVNet4.</span></span>

  ```powershell
  New-AzureRmVirtualNetwork -Name $VnetName4 -ResourceGroupName $RG4 `
  -Location $Location4 -AddressPrefix $VnetPrefix41,$VnetPrefix42 -Subnet $fesub4,$besub4,$gwsub4
  ```
5. <span data-ttu-id="09d1b-219">Genel bir IP adresi isteyin.</span><span class="sxs-lookup"><span data-stu-id="09d1b-219">Request a public IP address.</span></span>

  ```powershell
  $gwpip4 = New-AzureRmPublicIpAddress -Name $GWIPName4 -ResourceGroupName $RG4 `
  -Location $Location4 -AllocationMethod Dynamic
  ```
6. <span data-ttu-id="09d1b-220">Merhaba ağ geçidi yapılandırmasını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="09d1b-220">Create hello gateway configuration.</span></span>

  ```powershell
  $vnet4 = Get-AzureRmVirtualNetwork -Name $VnetName4 -ResourceGroupName $RG4
  $subnet4 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet4
  $gwipconf4 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName4 -Subnet $subnet4 -PublicIpAddress $gwpip4
  ```
7. <span data-ttu-id="09d1b-221">Merhaba TestVNet4 ağ geçidi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="09d1b-221">Create hello TestVNet4 gateway.</span></span> <span data-ttu-id="09d1b-222">Bir ağ geçidi oluşturma 45 dakika veya daha fazla hello seçilen ağ geçidi SKU'su bağlı olarak genellikle alabilir.</span><span class="sxs-lookup"><span data-stu-id="09d1b-222">Creating a gateway can often take 45 minutes or more, depending on hello selected gateway SKU.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName4 -ResourceGroupName $RG4 `
  -Location $Location4 -IpConfigurations $gwipconf4 -GatewayType Vpn `
  -VpnType RouteBased -GatewaySku VpnGw1
  ```

### <a name="step-4---create-hello-connections"></a><span data-ttu-id="09d1b-223">4. adım - hello bağlantıları oluşturma</span><span class="sxs-lookup"><span data-stu-id="09d1b-223">Step 4 - Create hello connections</span></span>

1. <span data-ttu-id="09d1b-224">Her iki sanal ağ geçidini de alın.</span><span class="sxs-lookup"><span data-stu-id="09d1b-224">Get both virtual network gateways.</span></span> <span data-ttu-id="09d1b-225">Merhaba ağ geçitleri her ikisi de hello olduğunda aynı abonelik hello örnekte olduğu gibi hello Bu adımda tamamlayabilirsiniz aynı PowerShell oturumunda.</span><span class="sxs-lookup"><span data-stu-id="09d1b-225">If both of hello gateways are in hello same subscription, as they are in hello example, you can complete this step in hello same PowerShell session.</span></span>

  ```powershell
  $vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
  $vnet4gw = Get-AzureRmVirtualNetworkGateway -Name $GWName4 -ResourceGroupName $RG4
  ```
2. <span data-ttu-id="09d1b-226">Merhaba TestVNet1 tooTestVNet4 bağlantı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="09d1b-226">Create hello TestVNet1 tooTestVNet4 connection.</span></span> <span data-ttu-id="09d1b-227">Bu adımda TestVNet1 tooTestVNet4 hello bağlantı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="09d1b-227">In this step, you create hello connection from TestVNet1 tooTestVNet4.</span></span> <span data-ttu-id="09d1b-228">Merhaba örneklerde paylaşılan bir anahtar göreceksiniz.</span><span class="sxs-lookup"><span data-stu-id="09d1b-228">You'll see a shared key referenced in hello examples.</span></span> <span data-ttu-id="09d1b-229">Merhaba paylaşılan anahtar için kendi değerlerinizi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="09d1b-229">You can use your own values for hello shared key.</span></span> <span data-ttu-id="09d1b-230">Merhaba hello paylaşılan anahtara şeydir önemli hem bağlantılarında eşleşmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="09d1b-230">hello important thing is that hello shared key must match for both connections.</span></span> <span data-ttu-id="09d1b-231">Bağlantı oluşturma toocomplete sırasında kısa sürebilir.</span><span class="sxs-lookup"><span data-stu-id="09d1b-231">Creating a connection can take a short while toocomplete.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection14 -ResourceGroupName $RG1 `
  -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet4gw -Location $Location1 `
  -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```
3. <span data-ttu-id="09d1b-232">Merhaba TestVNet4 tooTestVNet1 bağlantı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="09d1b-232">Create hello TestVNet4 tooTestVNet1 connection.</span></span> <span data-ttu-id="09d1b-233">TestVNet4 tooTestVNet1 hello bağlantı oluşturma dışında bu benzer toohello yukarıdaki bir adımdır.</span><span class="sxs-lookup"><span data-stu-id="09d1b-233">This step is similar toohello one above, except you are creating hello connection from TestVNet4 tooTestVNet1.</span></span> <span data-ttu-id="09d1b-234">Merhaba paylaşılan anahtarların eşleştiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="09d1b-234">Make sure hello shared keys match.</span></span> <span data-ttu-id="09d1b-235">birkaç dakika sonra Hello bağlantı kurulur.</span><span class="sxs-lookup"><span data-stu-id="09d1b-235">hello connection will be established after a few minutes.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection41 -ResourceGroupName $RG4 `
  -VirtualNetworkGateway1 $vnet4gw -VirtualNetworkGateway2 $vnet1gw -Location $Location4 `
  -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```
4. <span data-ttu-id="09d1b-236">Bağlantınızı doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="09d1b-236">Verify your connection.</span></span> <span data-ttu-id="09d1b-237">Merhaba bölümüne bakın [nasıl tooverify bağlantınızı](#verify).</span><span class="sxs-lookup"><span data-stu-id="09d1b-237">See hello section [How tooverify your connection](#verify).</span></span>

## <span data-ttu-id="09d1b-238"><a name="difsub"></a>Nasıl farklı Aboneliklerde bulunuyor tooconnect sanal ağlar</span><span class="sxs-lookup"><span data-stu-id="09d1b-238"><a name="difsub"></a>How tooconnect VNets that are in different subscriptions</span></span>

![v2v diyagramı](./media/vpn-gateway-vnet-vnet-rm-ps/v2vdiffsub.png)

<span data-ttu-id="09d1b-240">Bu senaryoda TestVNet1 ve TestVNet5 bağlanır.</span><span class="sxs-lookup"><span data-stu-id="09d1b-240">In this scenario, we connect TestVNet1 and TestVNet5.</span></span> <span data-ttu-id="09d1b-241">TestVNet1 ve TestVNet5 farklı bir abonelikte bulunur.</span><span class="sxs-lookup"><span data-stu-id="09d1b-241">TestVNet1 and TestVNet5 reside in a different subscription.</span></span> <span data-ttu-id="09d1b-242">Merhaba abonelikleri hello ile ilişkili toobe gerek yoktur aynı Active Directory kiracısı.</span><span class="sxs-lookup"><span data-stu-id="09d1b-242">hello subscriptions do not need toobe associated with hello same Active Directory tenant.</span></span> <span data-ttu-id="09d1b-243">Merhaba bu adımları hello önceki kümesi arasındaki bazı hello yapılandırma adımlarını hello hello ikinci abonelik bağlamında ayrı bir PowerShell oturumunda gerçekleştirilen toobe gerektiğini farktır.</span><span class="sxs-lookup"><span data-stu-id="09d1b-243">hello difference between these steps and hello previous set is that some of hello configuration steps need toobe performed in a separate PowerShell session in hello context of hello second subscription.</span></span> <span data-ttu-id="09d1b-244">Özellikle zaman hello iki abonelikleri toodifferent kuruluşların ait.</span><span class="sxs-lookup"><span data-stu-id="09d1b-244">Especially when hello two subscriptions belong toodifferent organizations.</span></span>

### <a name="step-5---create-and-configure-testvnet1"></a><span data-ttu-id="09d1b-245">5. Adım - TestVNet1'i oluşturma ve yapılandırma</span><span class="sxs-lookup"><span data-stu-id="09d1b-245">Step 5 - Create and configure TestVNet1</span></span>

<span data-ttu-id="09d1b-246">Tamamlamanız gereken [1. adım](#Step1) ve [2. adım](#Step2) hello önceki gelen bölüm toocreate TestVNet1 yapılandırmak ve VPN ağ geçidi için TestVNet1 hello.</span><span class="sxs-lookup"><span data-stu-id="09d1b-246">You must complete [Step 1](#Step1) and [Step 2](#Step2) from hello previous section toocreate and configure TestVNet1 and hello VPN Gateway for TestVNet1.</span></span> <span data-ttu-id="09d1b-247">Oluşturursanız, bu adımlara devam çakışmamasını rağmen bu yapılandırma için gerekli toocreate TestVNet4 hello önceki bölümden değildir.</span><span class="sxs-lookup"><span data-stu-id="09d1b-247">For this configuration, you are not required toocreate TestVNet4 from hello previous section, although if you do create it, it will not conflict with these steps.</span></span> <span data-ttu-id="09d1b-248">Adım 1 ve 2. adım tamamlandığında, adım 6 toocreate TestVNet5 devam edin.</span><span class="sxs-lookup"><span data-stu-id="09d1b-248">Once you complete Step 1 and Step 2, continue with Step 6 toocreate TestVNet5.</span></span> 

### <a name="step-6---verify-hello-ip-address-ranges"></a><span data-ttu-id="09d1b-249">6. adım - başlangıç IP adresi aralıklarını doğrulama</span><span class="sxs-lookup"><span data-stu-id="09d1b-249">Step 6 - Verify hello IP address ranges</span></span>

<span data-ttu-id="09d1b-250">Önemli toomake hello IP adres alanı hello yeni sanal ağın TestVNet5 hiçbirini aralıklarınız veya yerel ağ geçidi aralıkları ile çakışmaması emin olur.</span><span class="sxs-lookup"><span data-stu-id="09d1b-250">It is important toomake sure that hello IP address space of hello new virtual network, TestVNet5, does not overlap with any of your VNet ranges or local network gateway ranges.</span></span> <span data-ttu-id="09d1b-251">Bu örnekte, hello sanal ağlar toodifferent kuruluşlara ait olabilir.</span><span class="sxs-lookup"><span data-stu-id="09d1b-251">In this example, hello virtual networks may belong toodifferent organizations.</span></span> <span data-ttu-id="09d1b-252">Bu alıştırmada, hello TestVNet5 için değerler aşağıdaki hello kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="09d1b-252">For this exercise, you can use hello following values for hello TestVNet5:</span></span>

<span data-ttu-id="09d1b-253">**Değerler TestVNet5 için:**</span><span class="sxs-lookup"><span data-stu-id="09d1b-253">**Values for TestVNet5:**</span></span>

* <span data-ttu-id="09d1b-254">VNet Name: TestVNet5</span><span class="sxs-lookup"><span data-stu-id="09d1b-254">VNet Name: TestVNet5</span></span>
* <span data-ttu-id="09d1b-255">Resource Group: TestRG5</span><span class="sxs-lookup"><span data-stu-id="09d1b-255">Resource Group: TestRG5</span></span>
* <span data-ttu-id="09d1b-256">Location: Japan East</span><span class="sxs-lookup"><span data-stu-id="09d1b-256">Location: Japan East</span></span>
* <span data-ttu-id="09d1b-257">TestVNet5: 10.51.0.0/16 & 10.52.0.0/16</span><span class="sxs-lookup"><span data-stu-id="09d1b-257">TestVNet5: 10.51.0.0/16 & 10.52.0.0/16</span></span>
* <span data-ttu-id="09d1b-258">FrontEnd: 10.51.0.0/24</span><span class="sxs-lookup"><span data-stu-id="09d1b-258">FrontEnd: 10.51.0.0/24</span></span>
* <span data-ttu-id="09d1b-259">BackEnd: 10.52.0.0/24</span><span class="sxs-lookup"><span data-stu-id="09d1b-259">BackEnd: 10.52.0.0/24</span></span>
* <span data-ttu-id="09d1b-260">GatewaySubnet: 10.52.255.0.0/27</span><span class="sxs-lookup"><span data-stu-id="09d1b-260">GatewaySubnet: 10.52.255.0.0/27</span></span>
* <span data-ttu-id="09d1b-261">GatewayName: VNet5GW</span><span class="sxs-lookup"><span data-stu-id="09d1b-261">GatewayName: VNet5GW</span></span>
* <span data-ttu-id="09d1b-262">Public IP: VNet5GWIP</span><span class="sxs-lookup"><span data-stu-id="09d1b-262">Public IP: VNet5GWIP</span></span>
* <span data-ttu-id="09d1b-263">VPNType: RouteBased</span><span class="sxs-lookup"><span data-stu-id="09d1b-263">VPNType: RouteBased</span></span>
* <span data-ttu-id="09d1b-264">Connection: VNet5toVNet1</span><span class="sxs-lookup"><span data-stu-id="09d1b-264">Connection: VNet5toVNet1</span></span>
* <span data-ttu-id="09d1b-265">ConnectionType: VNet2VNet</span><span class="sxs-lookup"><span data-stu-id="09d1b-265">ConnectionType: VNet2VNet</span></span>

### <a name="step-7---create-and-configure-testvnet5"></a><span data-ttu-id="09d1b-266">7. Adım - TestVNet5'i oluşturma ve yapılandırma</span><span class="sxs-lookup"><span data-stu-id="09d1b-266">Step 7 - Create and configure TestVNet5</span></span>

<span data-ttu-id="09d1b-267">Bu adım hello hello yeni abonelik bağlamında yapılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="09d1b-267">This step must be done in hello context of hello new subscription.</span></span> <span data-ttu-id="09d1b-268">Bu bölümü hello aboneliğin sahibi olan farklı bir kuruluşta hello Yöneticisi tarafından gerçekleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="09d1b-268">This part may be performed by hello administrator in a different organization that owns hello subscription.</span></span>

1. <span data-ttu-id="09d1b-269">Değişkenlerinizi bildirin.</span><span class="sxs-lookup"><span data-stu-id="09d1b-269">Declare your variables.</span></span> <span data-ttu-id="09d1b-270">Merhaba olanları hello değerlerle emin tooreplace olması yapılandırmanızın toouse istiyor.</span><span class="sxs-lookup"><span data-stu-id="09d1b-270">Be sure tooreplace hello values with hello ones that you want toouse for your configuration.</span></span>

  ```powershell
  $Sub5 = "Replace_With_the_New_Subcription_Name"
  $RG5 = "TestRG5"
  $Location5 = "Japan East"
  $VnetName5 = "TestVNet5"
  $FESubName5 = "FrontEnd"
  $BESubName5 = "Backend"
  $GWSubName5 = "GatewaySubnet"
  $VnetPrefix51 = "10.51.0.0/16"
  $VnetPrefix52 = "10.52.0.0/16"
  $FESubPrefix5 = "10.51.0.0/24"
  $BESubPrefix5 = "10.52.0.0/24"
  $GWSubPrefix5 = "10.52.255.0/27"
  $GWName5 = "VNet5GW"
  $GWIPName5 = "VNet5GWIP"
  $GWIPconfName5 = "gwipconf5"
  $Connection51 = "VNet5toVNet1"
  ```
2. <span data-ttu-id="09d1b-271">Toosubscription 5 bağlayın.</span><span class="sxs-lookup"><span data-stu-id="09d1b-271">Connect toosubscription 5.</span></span> <span data-ttu-id="09d1b-272">PowerShell Konsolunuzu açın ve tooyour hesap bağlanın.</span><span class="sxs-lookup"><span data-stu-id="09d1b-272">Open your PowerShell console and connect tooyour account.</span></span> <span data-ttu-id="09d1b-273">Bağlandığınız örnek toohelp aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="09d1b-273">Use hello following sample toohelp you connect:</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

  <span data-ttu-id="09d1b-274">Merhaba hesabının Hello abonelikleri kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="09d1b-274">Check hello subscriptions for hello account.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```

  <span data-ttu-id="09d1b-275">Merhaba abonelik toouse istediğinizi belirtin.</span><span class="sxs-lookup"><span data-stu-id="09d1b-275">Specify hello subscription that you want toouse.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionName $Sub5
  ```
3. <span data-ttu-id="09d1b-276">Yeni bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="09d1b-276">Create a new resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name $RG5 -Location $Location5
  ```
4. <span data-ttu-id="09d1b-277">Merhaba TestVNet5 için alt ağ yapılandırmaları oluşturun.</span><span class="sxs-lookup"><span data-stu-id="09d1b-277">Create hello subnet configurations for TestVNet5.</span></span>

  ```powershell
  $fesub5 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName5 -AddressPrefix $FESubPrefix5
  $besub5 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName5 -AddressPrefix $BESubPrefix5
  $gwsub5 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName5 -AddressPrefix $GWSubPrefix5
  ```
5. <span data-ttu-id="09d1b-278">TestVNet5’i oluşturun.</span><span class="sxs-lookup"><span data-stu-id="09d1b-278">Create TestVNet5.</span></span>

  ```powershell
  New-AzureRmVirtualNetwork -Name $VnetName5 -ResourceGroupName $RG5 -Location $Location5 `
  -AddressPrefix $VnetPrefix51,$VnetPrefix52 -Subnet $fesub5,$besub5,$gwsub5
  ```
6. <span data-ttu-id="09d1b-279">Genel bir IP adresi isteyin.</span><span class="sxs-lookup"><span data-stu-id="09d1b-279">Request a public IP address.</span></span>

  ```powershell
  $gwpip5 = New-AzureRmPublicIpAddress -Name $GWIPName5 -ResourceGroupName $RG5 `
  -Location $Location5 -AllocationMethod Dynamic
  ```
7. <span data-ttu-id="09d1b-280">Merhaba ağ geçidi yapılandırmasını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="09d1b-280">Create hello gateway configuration.</span></span>

  ```powershell
  $vnet5 = Get-AzureRmVirtualNetwork -Name $VnetName5 -ResourceGroupName $RG5
  $subnet5  = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet5
  $gwipconf5 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName5 -Subnet $subnet5 -PublicIpAddress $gwpip5
  ```
8. <span data-ttu-id="09d1b-281">Merhaba TestVNet5 ağ geçidi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="09d1b-281">Create hello TestVNet5 gateway.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName5 -ResourceGroupName $RG5 -Location $Location5 `
  -IpConfigurations $gwipconf5 -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1
  ```

### <a name="step-8---create-hello-connections"></a><span data-ttu-id="09d1b-282">8. adım - hello bağlantıları oluşturma</span><span class="sxs-lookup"><span data-stu-id="09d1b-282">Step 8 - Create hello connections</span></span>

<span data-ttu-id="09d1b-283">Merhaba ağ geçitleri hello farklı Aboneliklerde olduğundan bu örnekte, biz bu adımı iki PowerShell oturumuna [abonelik 1] ve [5. abonelik] bölme.</span><span class="sxs-lookup"><span data-stu-id="09d1b-283">In this example, because hello gateways are in hello different subscriptions, we've split this step into two PowerShell sessions marked as [Subscription 1] and [Subscription 5].</span></span>

1. <span data-ttu-id="09d1b-284">**[1. abonelik]**  Get hello sanal ağ geçidi için abonelik 1.</span><span class="sxs-lookup"><span data-stu-id="09d1b-284">**[Subscription 1]** Get hello virtual network gateway for Subscription 1.</span></span> <span data-ttu-id="09d1b-285">Oturum açın ve aşağıdaki örneğine hello çalıştırmadan önce tooSubscription 1 bağlanın:</span><span class="sxs-lookup"><span data-stu-id="09d1b-285">Log in and connect tooSubscription 1 before running hello following example:</span></span>

  ```powershell
  $vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
  ```

  <span data-ttu-id="09d1b-286">Öğeleri aşağıdaki hello Hello çıktısını kopyalayın ve 5. abonelik bu toohello yönetici e-posta veya başka bir yöntemle gönderin.</span><span class="sxs-lookup"><span data-stu-id="09d1b-286">Copy hello output of hello following elements and send these toohello administrator of Subscription 5 via email or another method.</span></span>

  ```powershell
  $vnet1gw.Name
  $vnet1gw.Id
  ```

  <span data-ttu-id="09d1b-287">Bu iki öğenin değerleri benzer toohello örnek çıktı şu olacaktır:</span><span class="sxs-lookup"><span data-stu-id="09d1b-287">These two elements will have values similar toohello following example output:</span></span>

  ```
  PS D:\> $vnet1gw.Name
  VNet1GW
  PS D:\> $vnet1gw.Id
  /subscriptions/b636ca99-6f88-4df4-a7c3-2f8dc4545509/resourceGroupsTestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW
  ```
2. <span data-ttu-id="09d1b-288">**[5. abonelik]**  Get hello sanal ağ geçidi 5. abonelik için.</span><span class="sxs-lookup"><span data-stu-id="09d1b-288">**[Subscription 5]** Get hello virtual network gateway for Subscription 5.</span></span> <span data-ttu-id="09d1b-289">Oturum açın ve aşağıdaki örneğine hello çalıştırmadan önce tooSubscription 5 bağlanın:</span><span class="sxs-lookup"><span data-stu-id="09d1b-289">Log in and connect tooSubscription 5 before running hello following example:</span></span>

  ```powershell
  $vnet5gw = Get-AzureRmVirtualNetworkGateway -Name $GWName5 -ResourceGroupName $RG5
  ```

  <span data-ttu-id="09d1b-290">Öğeleri aşağıdaki hello Hello çıktısını kopyalayın ve bu abonelik 1 toohello yönetici e-posta veya başka bir yöntem gönderin.</span><span class="sxs-lookup"><span data-stu-id="09d1b-290">Copy hello output of hello following elements and send these toohello administrator of Subscription 1 via email or another method.</span></span>

  ```powershell
  $vnet5gw.Name
  $vnet5gw.Id
  ```

  <span data-ttu-id="09d1b-291">Bu iki öğenin değerleri benzer toohello örnek çıktı şu olacaktır:</span><span class="sxs-lookup"><span data-stu-id="09d1b-291">These two elements will have values similar toohello following example output:</span></span>

  ```
  PS C:\> $vnet5gw.Name
  VNet5GW
  PS C:\> $vnet5gw.Id
  /subscriptions/66c8e4f1-ecd6-47ed-9de7-7e530de23994/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW
  ```
3. <span data-ttu-id="09d1b-292">**[1. abonelik]**  Hello TestVNet1 tooTestVNet5 bağlantı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="09d1b-292">**[Subscription 1]** Create hello TestVNet1 tooTestVNet5 connection.</span></span> <span data-ttu-id="09d1b-293">Bu adımda TestVNet1 tooTestVNet5 hello bağlantı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="09d1b-293">In this step, you create hello connection from TestVNet1 tooTestVNet5.</span></span> <span data-ttu-id="09d1b-294">Burada Hello fark, farklı bir abonelikte olduğundan bu $ vnet5gw'un doğrudan alınamıyor olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="09d1b-294">hello difference here is that $vnet5gw cannot be obtained directly because it is in a different subscription.</span></span> <span data-ttu-id="09d1b-295">1. abonelikten hello Yukarıdaki adımlarda iletilen hello değerlerle yeni bir PowerShell nesnesi toocreate gerekir.</span><span class="sxs-lookup"><span data-stu-id="09d1b-295">You will need toocreate a new PowerShell object with hello values communicated from Subscription 1 in hello steps above.</span></span> <span data-ttu-id="09d1b-296">Aşağıdaki Hello örneği kullanın.</span><span class="sxs-lookup"><span data-stu-id="09d1b-296">Use hello example below.</span></span> <span data-ttu-id="09d1b-297">Merhaba adı, kimliği ve paylaşılan anahtar kendi değerlerinizle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="09d1b-297">Replace hello Name, Id, and shared key with your own values.</span></span> <span data-ttu-id="09d1b-298">Merhaba hello paylaşılan anahtara şeydir önemli hem bağlantılarında eşleşmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="09d1b-298">hello important thing is that hello shared key must match for both connections.</span></span> <span data-ttu-id="09d1b-299">Bağlantı oluşturma toocomplete sırasında kısa sürebilir.</span><span class="sxs-lookup"><span data-stu-id="09d1b-299">Creating a connection can take a short while toocomplete.</span></span>

  <span data-ttu-id="09d1b-300">Aşağıdaki örnek hello çalıştırmadan önce tooSubscription 1 Bağlan:</span><span class="sxs-lookup"><span data-stu-id="09d1b-300">Connect tooSubscription 1 before running hello following example:</span></span>

  ```powershell
  $vnet5gw = New-Object Microsoft.Azure.Commands.Network.Models.PSVirtualNetworkGateway
  $vnet5gw.Name = "VNet5GW"
  $vnet5gw.Id   = "/subscriptions/66c8e4f1-ecd6-47ed-9de7-7e530de23994/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW"
  $Connection15 = "VNet1toVNet5"
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet5gw -Location $Location1 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```
4. <span data-ttu-id="09d1b-301">**[5. abonelik]**  Hello TestVNet5 tooTestVNet1 bağlantı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="09d1b-301">**[Subscription 5]** Create hello TestVNet5 tooTestVNet1 connection.</span></span> <span data-ttu-id="09d1b-302">Bu adım, TestVNet5 tooTestVNet1 hello bağlantı oluşturma dışında benzer toohello biri yukarıdaki aynıdır.</span><span class="sxs-lookup"><span data-stu-id="09d1b-302">This step is similar toohello one above, except you are creating hello connection from TestVNet5 tooTestVNet1.</span></span> <span data-ttu-id="09d1b-303">Merhaba, 1. abonelikten elde hello değerlere göre bir PowerShell nesnesi oluşturma aynı işlemi burada da geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="09d1b-303">hello same process of creating a PowerShell object based on hello values obtained from Subscription 1 applies here as well.</span></span> <span data-ttu-id="09d1b-304">Bu adımda, hello paylaşılan anahtarların eşleştiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="09d1b-304">In this step, be sure that hello shared keys match.</span></span>

  <span data-ttu-id="09d1b-305">Aşağıdaki örnek hello çalıştırmadan önce tooSubscription 5 Bağlan:</span><span class="sxs-lookup"><span data-stu-id="09d1b-305">Connect tooSubscription 5 before running hello following example:</span></span>

  ```powershell
  $vnet1gw = New-Object Microsoft.Azure.Commands.Network.Models.PSVirtualNetworkGateway
  $vnet1gw.Name = "VNet1GW"
  $vnet1gw.Id = "/subscriptions/b636ca99-6f88-4df4-a7c3-2f8dc4545509/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW "
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection51 -ResourceGroupName $RG5 -VirtualNetworkGateway1 $vnet5gw -VirtualNetworkGateway2 $vnet1gw -Location $Location5 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```

## <span data-ttu-id="09d1b-306"><a name="verify"></a>Nasıl tooverify bağlantı</span><span class="sxs-lookup"><span data-stu-id="09d1b-306"><a name="verify"></a>How tooverify a connection</span></span>

[!INCLUDE [vpn-gateway-no-nsg-include](../../includes/vpn-gateway-no-nsg-include.md)]

[!INCLUDE [verify connections powershell](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

## <span data-ttu-id="09d1b-307"><a name="faq"></a>Sanal ağlar arası bağlantılar hakkında SSS</span><span class="sxs-lookup"><span data-stu-id="09d1b-307"><a name="faq"></a>VNet-to-VNet FAQ</span></span>

[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]

## <a name="next-steps"></a><span data-ttu-id="09d1b-308">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="09d1b-308">Next steps</span></span>

* <span data-ttu-id="09d1b-309">Bağlantınız tamamlandıktan sonra sanal makineleri tooyour sanal ağları ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="09d1b-309">Once your connection is complete, you can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="09d1b-310">Merhaba bkz [Virtual Machines belgeleri](https://docs.microsoft.com/azure/#pivot=services&panel=Compute) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="09d1b-310">See hello [Virtual Machines documentation](https://docs.microsoft.com/azure/#pivot=services&panel=Compute) for more information.</span></span>
* <span data-ttu-id="09d1b-311">BGP hakkında daha fazla bilgi için bkz: Merhaba [BGP genel bakış](vpn-gateway-bgp-overview.md) ve [nasıl tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span><span class="sxs-lookup"><span data-stu-id="09d1b-311">For information about BGP, see hello [BGP Overview](vpn-gateway-bgp-overview.md) and [How tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span></span>
