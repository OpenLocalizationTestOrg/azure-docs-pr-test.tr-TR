---
title: "Şirket içi ağınızı bir Azure sanal ağına bağlama: Siteden Siteye VPN: Portal | Microsoft Docs"
description: "Şirket içi ağınız ile bir Azure sanal ağı arasında genel İnternet üzerinden bir IPSec bağlantısı oluşturma adımları. Bu adımlar portalı kullanarak Siteden Siteye şirket içi ve dışı karışık VPN Gateway bağlantısı oluşturmanıza yardımcı olur."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 827a4db7-7fa5-4eaf-b7e1-e1518c51c815
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/02/2017
ms.author: cherylmc
ms.openlocfilehash: 0dec0d3744f76a06313928197f3a5229290ba32b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-site-to-site-connection-in-the-azure-portal"></a><span data-ttu-id="9f183-104">Azure portalında Siteden Siteye bağlantı oluşturma</span><span class="sxs-lookup"><span data-stu-id="9f183-104">Create a Site-to-Site connection in the Azure portal</span></span>

<span data-ttu-id="9f183-105">Bu makalede, Azure portalını kullanarak şirket içi ağınızdan VNet’e Siteden Siteye VPN ağ geçidi bağlantısı oluşturma işlemi gösterilir.</span><span class="sxs-lookup"><span data-stu-id="9f183-105">This article shows you how to use the Azure portal to create a Site-to-Site VPN gateway connection from your on-premises network to the VNet.</span></span> <span data-ttu-id="9f183-106">Bu makaledeki adımlar Resource Manager dağıtım modeli için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="9f183-106">The steps in this article apply to the Resource Manager deployment model.</span></span> <span data-ttu-id="9f183-107">Ayrıca aşağıdaki listeden farklı bir seçenek belirtip farklı bir dağıtım aracı veya dağıtım modeli kullanarak da bu yapılandırmayı oluşturabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="9f183-107">You can also create this configuration using a different deployment tool or deployment model by selecting a different option from the following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="9f183-108">Azure portal</span><span class="sxs-lookup"><span data-stu-id="9f183-108">Azure portal</span></span>](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="9f183-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9f183-109">PowerShell</span></span>](vpn-gateway-create-site-to-site-rm-powershell.md)
> * [<span data-ttu-id="9f183-110">CLI</span><span class="sxs-lookup"><span data-stu-id="9f183-110">CLI</span></span>](vpn-gateway-howto-site-to-site-resource-manager-cli.md)
> * [<span data-ttu-id="9f183-111">Azure portal (klasik)</span><span class="sxs-lookup"><span data-stu-id="9f183-111">Azure portal (classic)</span></span>](vpn-gateway-howto-site-to-site-classic-portal.md)
> 
>

<span data-ttu-id="9f183-112">Siteden Siteye VPN ağ geçidi bağlantısı, şirket içi ağınızı bir IPsec/IKE (IKEv1 veya IKEv2) tüneli üzerinden Azure sanal ağına bağlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="9f183-112">A Site-to-Site VPN gateway connection is used to connect your on-premises network to an Azure virtual network over an IPsec/IKE (IKEv1 or IKEv2) VPN tunnel.</span></span> <span data-ttu-id="9f183-113">Bu bağlantı türü için, şirket içinde yer alan ve kendisine atanmış dışarıya yönelik bir genel IP adresi atanmış olan bir VPN cihazı gerekir.</span><span class="sxs-lookup"><span data-stu-id="9f183-113">This type of connection requires a VPN device located on-premises that has an externally facing public IP address assigned to it.</span></span> <span data-ttu-id="9f183-114">VPN ağ geçitleri hakkında daha fazla bilgi için bkz. [VPN ağ geçidi hakkında](vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="9f183-114">For more information about VPN gateways, see [About VPN gateway](vpn-gateway-about-vpngateways.md).</span></span>

![Siteden Siteye şirket içi ve dışı karışık VPN Gateway bağlantısı diyagramı](./media/vpn-gateway-howto-site-to-site-resource-manager-portal/site-to-site-diagram.png)

## <a name="before-you-begin"></a><span data-ttu-id="9f183-116">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="9f183-116">Before you begin</span></span>

<span data-ttu-id="9f183-117">Yapılandırmanıza başlamadan önce aşağıdaki ölçütleri karşıladığınızı doğrulayın:</span><span class="sxs-lookup"><span data-stu-id="9f183-117">Verify that you have met the following criteria before beginning your configuration:</span></span>

* <span data-ttu-id="9f183-118">Uyumlu bir VPN cihazı ve bu cihazı yapılandırabilecek birinin bulunduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="9f183-118">Make sure you have a compatible VPN device and someone who is able to configure it.</span></span> <span data-ttu-id="9f183-119">Uyumlu VPN cihazları ve cihaz yapılandırması hakkında daha fazla bilgi için bkz.[VPN Cihazları Hakkında](vpn-gateway-about-vpn-devices.md).</span><span class="sxs-lookup"><span data-stu-id="9f183-119">For more information about compatible VPN devices and device configuration, see [About VPN Devices](vpn-gateway-about-vpn-devices.md).</span></span>
* <span data-ttu-id="9f183-120">VPN cihazınız için dışarıya dönük genel bir IPv4 adresi olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="9f183-120">Verify that you have an externally facing public IPv4 address for your VPN device.</span></span> <span data-ttu-id="9f183-121">Bu IP adresi bir NAT’nin arkasında olamaz.</span><span class="sxs-lookup"><span data-stu-id="9f183-121">This IP address cannot be located behind a NAT.</span></span>
* <span data-ttu-id="9f183-122">Şirket içi ağ yapılandırmanızda bulunan IP adresi aralıklarıyla ilgili fazla bilginiz yoksa size bu ayrıntıları sağlayabilecek biriyle çalışmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="9f183-122">If you are unfamiliar with the IP address ranges located in your on-premises network configuration, you need to coordinate with someone who can provide those details for you.</span></span> <span data-ttu-id="9f183-123">Bu yapılandırmayı oluşturduğunuzda, Azure’un şirket içi konumunuza yönlendireceği IP adres aralığı ön eklerini oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="9f183-123">When you create this configuration, you must specify the IP address range prefixes that Azure will route to your on-premises location.</span></span> <span data-ttu-id="9f183-124">Şirket içi ağınızın alt ağlarından hiçbiri, bağlanmak istediğiniz sanal ağ alt ağlarıyla çakışamaz.</span><span class="sxs-lookup"><span data-stu-id="9f183-124">None of the subnets of your on-premises network can over lap with the virtual network subnets that you want to connect to.</span></span> 

### <span data-ttu-id="9f183-125"><a name="values"></a>Örnek değerler</span><span class="sxs-lookup"><span data-stu-id="9f183-125"><a name="values"></a>Example values</span></span>

<span data-ttu-id="9f183-126">Bu makaledeki örneklerde aşağıdaki değerler kullanılır.</span><span class="sxs-lookup"><span data-stu-id="9f183-126">The examples in this article use the following values.</span></span> <span data-ttu-id="9f183-127">Bu değerleri kullanarak bir test ortamı oluşturabilir veya bu makaledeki örnekleri daha iyi anlamak için bunlara bakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9f183-127">You can use these values to create a test environment, or refer to them to better understand the examples in this article.</span></span>

* <span data-ttu-id="9f183-128">**VNet Name:** TestVNet1</span><span class="sxs-lookup"><span data-stu-id="9f183-128">**VNet Name:** TestVNet1</span></span>
* <span data-ttu-id="9f183-129">**Adres Alanı:**</span><span class="sxs-lookup"><span data-stu-id="9f183-129">**Address Space:**</span></span> 
  * <span data-ttu-id="9f183-130">10.11.0.0/16</span><span class="sxs-lookup"><span data-stu-id="9f183-130">10.11.0.0/16</span></span>
  * <span data-ttu-id="9f183-131">10.12.0.0/16 (bu alıştırma için isteğe bağlı)</span><span class="sxs-lookup"><span data-stu-id="9f183-131">10.12.0.0/16 (optional for this exercise)</span></span>
* <span data-ttu-id="9f183-132">**Alt ağlar:**</span><span class="sxs-lookup"><span data-stu-id="9f183-132">**Subnets:**</span></span>
  * <span data-ttu-id="9f183-133">FrontEnd: 10.11.0.0/24</span><span class="sxs-lookup"><span data-stu-id="9f183-133">FrontEnd: 10.11.0.0/24</span></span>
  * <span data-ttu-id="9f183-134">BackEnd: 10.12.0.0/24 (bu alıştırma için isteğe bağlı)</span><span class="sxs-lookup"><span data-stu-id="9f183-134">BackEnd: 10.12.0.0/24 (optional for this exercise)</span></span>
* <span data-ttu-id="9f183-135">**GatewaySubnet:** 10.11.255.0/27</span><span class="sxs-lookup"><span data-stu-id="9f183-135">**GatewaySubnet:** 10.11.255.0/27</span></span>
* <span data-ttu-id="9f183-136">**Kaynak Grubu:** TestRG1</span><span class="sxs-lookup"><span data-stu-id="9f183-136">**Resource Group:** TestRG1</span></span>
* <span data-ttu-id="9f183-137">**Konum:** Doğu ABD</span><span class="sxs-lookup"><span data-stu-id="9f183-137">**Location:** East US</span></span>
* <span data-ttu-id="9f183-138">**DNS Sunucusu:** İsteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="9f183-138">**DNS Server:** Optional.</span></span> <span data-ttu-id="9f183-139">DNS sunucunuzun IP adresidir.</span><span class="sxs-lookup"><span data-stu-id="9f183-139">The IP address of your DNS server.</span></span>
* <span data-ttu-id="9f183-140">**Sanal Ağ Geçidi Adı: VNet1GW**</span><span class="sxs-lookup"><span data-stu-id="9f183-140">**Virtual Network Gateway Name:** VNet1GW</span></span>
* <span data-ttu-id="9f183-141">**Genel IP:** VNet1GWIP</span><span class="sxs-lookup"><span data-stu-id="9f183-141">**Public IP:** VNet1GWIP</span></span>
* <span data-ttu-id="9f183-142">**VPN Türü:** Yol tabanlı</span><span class="sxs-lookup"><span data-stu-id="9f183-142">**VPN Type:** Route-based</span></span>
* <span data-ttu-id="9f183-143">**Bağlantı Türü:** Siteden siteye (IPsec)</span><span class="sxs-lookup"><span data-stu-id="9f183-143">**Connection Type:** Site-to-site (IPsec)</span></span>
* <span data-ttu-id="9f183-144">**Ağ Geçidi Türü:** VPN</span><span class="sxs-lookup"><span data-stu-id="9f183-144">**Gateway Type:** VPN</span></span>
* <span data-ttu-id="9f183-145">**Yerel Ağ Geçidi Adı:** Site2</span><span class="sxs-lookup"><span data-stu-id="9f183-145">**Local Network Gateway Name:** Site2</span></span>
* <span data-ttu-id="9f183-146">**Bağlantı Adı:** VNet1toSite2</span><span class="sxs-lookup"><span data-stu-id="9f183-146">**Connection Name:** VNet1toSite2</span></span>

## <span data-ttu-id="9f183-147"><a name="CreatVNet"></a>1. Sanal ağ oluşturma</span><span class="sxs-lookup"><span data-stu-id="9f183-147"><a name="CreatVNet"></a>1. Create a virtual network</span></span>

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-basic-vnet-s2s-rm-portal-include.md)]

## <span data-ttu-id="9f183-148"><a name="dns"></a>2. DNS sunucusu belirleme</span><span class="sxs-lookup"><span data-stu-id="9f183-148"><a name="dns"></a>2. Specify a DNS server</span></span>

<span data-ttu-id="9f183-149">Siteden Siteye bağlantı oluşturmak için DNS gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="9f183-149">DNS is not required to create a Site-to-Site connection.</span></span> <span data-ttu-id="9f183-150">Ancak, sanal ağınıza dağıtılmış olan kaynaklarınız için ad çözümleme istiyorsanız bir DNS sunucusu belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="9f183-150">However, if you want to have name resolution for resources that are deployed to your virtual network, you should specify a DNS server.</span></span> <span data-ttu-id="9f183-151">Bu ayar, bu sanal ağ için ad çözümlemede kullanmak istediğiniz DNS sunucusunu belirtmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="9f183-151">This setting lets you specify the DNS server that you want to use for name resolution for this virtual network.</span></span> <span data-ttu-id="9f183-152">Bir DNS sunucusu oluşturmaz.</span><span class="sxs-lookup"><span data-stu-id="9f183-152">It does not create a DNS server.</span></span> <span data-ttu-id="9f183-153">Ad çözümlemesi hakkında daha fazla bilgi için bkz. [VM'ler ve rol örnekleri için Ad Çözümlemesi](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span><span class="sxs-lookup"><span data-stu-id="9f183-153">For more information about name resolution, see [Name Resolution for VMs and role instances](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span></span>

[!INCLUDE [vpn-gateway-add-dns-rm-portal](../../includes/vpn-gateway-add-dns-rm-portal-include.md)]

## <span data-ttu-id="9f183-154"><a name="gatewaysubnet"></a>3. Ağ geçidi alt ağını oluşturma</span><span class="sxs-lookup"><span data-stu-id="9f183-154"><a name="gatewaysubnet"></a>3. Create the gateway subnet</span></span>

[!INCLUDE [vpn-gateway-aboutgwsubnet](../../includes/vpn-gateway-about-gwsubnet-include.md)]

[!INCLUDE [vpn-gateway-add-gwsubnet-rm-portal](../../includes/vpn-gateway-add-gwsubnet-s2s-rm-portal-include.md)]

## <span data-ttu-id="9f183-155"><a name="VNetGateway"></a>4. VPN ağ geçidini oluşturma</span><span class="sxs-lookup"><span data-stu-id="9f183-155"><a name="VNetGateway"></a>4. Create the VPN gateway</span></span>

[!INCLUDE [vpn-gateway-add-gw-s2s-rm-portal](../../includes/vpn-gateway-add-gw-s2s-rm-portal-include.md)]

## <span data-ttu-id="9f183-156"><a name="LocalNetworkGateway"></a>5. Yerel ağ geçidini oluşturma</span><span class="sxs-lookup"><span data-stu-id="9f183-156"><a name="LocalNetworkGateway"></a>5. Create the local network gateway</span></span>

<span data-ttu-id="9f183-157">Yerel ağ geçidi genellikle şirket içi konumunuz anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="9f183-157">The local network gateway typically refers to your on-premises location.</span></span> <span data-ttu-id="9f183-158">Siteye Azure’un başvuruda bulunmak için kullanabileceği bir ad verir, ardından bağlantı oluşturacağınız şirket içi VPN cihazının IP adresini belirtirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9f183-158">You give the site a name by which Azure can refer to it, then specify the IP address of the on-premises VPN device to which you will create a connection.</span></span> <span data-ttu-id="9f183-159">Ayrıca, VPN ağ geçidi üzerinden VPN cihazına yönlendirilecek IP adresi ön eklerini de belirtirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9f183-159">You also specify the IP address prefixes that will be routed through the VPN gateway to the VPN device.</span></span> <span data-ttu-id="9f183-160">Belirttiğiniz adres ön ekleri, şirket içi adresinizde yer alan ön eklerdir.</span><span class="sxs-lookup"><span data-stu-id="9f183-160">The address prefixes you specify are the prefixes located on your on-premises network.</span></span> <span data-ttu-id="9f183-161">Şirket içi ağınız değişirse veya VPN cihazının genel IP adresini değiştirmeniz gerekirse değerleri daha sonra kolayca güncelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9f183-161">If your on-premises network changes or you need to change the public IP address for the VPN device, you can easily update the values later.</span></span>

[!INCLUDE [Add local network gateway](../../includes/vpn-gateway-add-lng-s2s-rm-portal-include.md)]

## <span data-ttu-id="9f183-162"><a name="VPNDevice"></a>6. VPN cihazınızı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="9f183-162"><a name="VPNDevice"></a>6. Configure your VPN device</span></span>

<span data-ttu-id="9f183-163">Bir şirket içi ağı ile Siteden Siteye bağlantılar için VPN cihazı gerekir.</span><span class="sxs-lookup"><span data-stu-id="9f183-163">Site-to-Site connections to an on-premises network require a VPN device.</span></span> <span data-ttu-id="9f183-164">Bu adımda VPN cihazınızı yapılandıracaksınız.</span><span class="sxs-lookup"><span data-stu-id="9f183-164">In this step, you configure your VPN device.</span></span> <span data-ttu-id="9f183-165">VPN cihazınızı yapılandırırken şunlar gerekir:</span><span class="sxs-lookup"><span data-stu-id="9f183-165">When configuring your VPN device, you need the following:</span></span>

- <span data-ttu-id="9f183-166">Paylaşılan bir anahtar.</span><span class="sxs-lookup"><span data-stu-id="9f183-166">A shared key.</span></span> <span data-ttu-id="9f183-167">Siteden Siteye VPN bağlantınızı oluştururken belirttiğiniz paylaşılan anahtarın aynısıdır.</span><span class="sxs-lookup"><span data-stu-id="9f183-167">This is the same shared key that you specify when creating your Site-to-Site VPN connection.</span></span> <span data-ttu-id="9f183-168">Bu örneklerde temel bir paylaşılan anahtar kullanılır.</span><span class="sxs-lookup"><span data-stu-id="9f183-168">In our examples, we use a basic shared key.</span></span> <span data-ttu-id="9f183-169">Kullanmak için daha karmaşık bir anahtar oluşturmanız önerilir.</span><span class="sxs-lookup"><span data-stu-id="9f183-169">We recommend that you generate a more complex key to use.</span></span>
- <span data-ttu-id="9f183-170">Sanal ağ geçidinizin Genel IP adresi.</span><span class="sxs-lookup"><span data-stu-id="9f183-170">The Public IP address of your virtual network gateway.</span></span> <span data-ttu-id="9f183-171">Azure Portal, PowerShell veya CLI kullanarak genel IP adresini görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9f183-171">You can view the public IP address by using the Azure portal, PowerShell, or CLI.</span></span> <span data-ttu-id="9f183-172">Azure portalını kullanarak VPN ağ geçidinizin Genel IP adresini bulmak için **Sanal ağ geçitleri**’ne gidin ve ağ geçidinizin adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9f183-172">To find the Public IP address of your VPN gateway using the Azure portal, navigate to **Virtual network gateways**, then click the name of your gateway.</span></span>

[!INCLUDE [Configure a VPN device](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]

## <span data-ttu-id="9f183-173"><a name="CreateConnection"></a>7. VPN bağlantısını oluşturma</span><span class="sxs-lookup"><span data-stu-id="9f183-173"><a name="CreateConnection"></a>7. Create the VPN connection</span></span>

<span data-ttu-id="9f183-174">Sanal ağ geçidiniz ile şirket içi VPN cihazınız arasında Siteden Siteye VPN bağlantısı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9f183-174">Create the Site-to-Site VPN connection between your virtual network gateway and your on-premises VPN device.</span></span>

[!INCLUDE [Add connections](../../includes/vpn-gateway-add-site-to-site-connection-s2s-rm-portal-include.md)]

## <span data-ttu-id="9f183-175"><a name="VerifyConnection"></a>8. VPN bağlantısını doğrulama</span><span class="sxs-lookup"><span data-stu-id="9f183-175"><a name="VerifyConnection"></a>8. Verify the VPN connection</span></span>

[!INCLUDE [Verify - Azure portal](../../includes/vpn-gateway-verify-connection-portal-rm-include.md)]

## <span data-ttu-id="9f183-176"><a name="connectVM"></a>Sanal makineye bağlanma</span><span class="sxs-lookup"><span data-stu-id="9f183-176"><a name="connectVM"></a>To connect to a virtual machine</span></span>

[!INCLUDE [Connect to a VM](../../includes/vpn-gateway-connect-vm-s2s-include.md)]

## <span data-ttu-id="9f183-177"><a name="reset"></a>VPN ağ geçidini sıfırlama</span><span class="sxs-lookup"><span data-stu-id="9f183-177"><a name="reset"></a>How to reset a VPN gateway</span></span>

<span data-ttu-id="9f183-178">Bir veya daha fazla Siteden Siteye VPN tünelinde şirketler arası VPN bağlantısını kaybederseniz bir Azure VPN ağ geçidinin sıfırlanması yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="9f183-178">Resetting an Azure VPN gateway is helpful if you lose cross-premises VPN connectivity on one or more Site-to-Site VPN tunnels.</span></span> <span data-ttu-id="9f183-179">Bu durumda şirket içi VPN cihazlarınızın tümü düzgün çalışır, ancak Azure VPN ağ geçitleriyle IPsec tünelleri kuramaz.</span><span class="sxs-lookup"><span data-stu-id="9f183-179">In this situation, your on-premises VPN devices are all working correctly, but are not able to establish IPsec tunnels with the Azure VPN gateways.</span></span> <span data-ttu-id="9f183-180">Adımlar için bkz. [VPN ağ geçidini sıfırlama](vpn-gateway-resetgw-classic.md).</span><span class="sxs-lookup"><span data-stu-id="9f183-180">For steps, see [Reset a VPN gateway](vpn-gateway-resetgw-classic.md).</span></span>

## <span data-ttu-id="9f183-181"><a name="resize"></a>Ağ geçidi SKU’sunu değiştirme (ağ geçidini yeniden boyutlandırma)</span><span class="sxs-lookup"><span data-stu-id="9f183-181"><a name="resize"></a>How to change a gateway SKU (resize a gateway)</span></span>

<span data-ttu-id="9f183-182">Bir ağ geçidi SKU'sunu değiştirme adımları için bkz. [Ağ geçidi SKU'ları](vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span><span class="sxs-lookup"><span data-stu-id="9f183-182">For the steps to change a gateway SKU, see [Gateway SKUs](vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9f183-183">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9f183-183">Next steps</span></span>

* <span data-ttu-id="9f183-184">BGP hakkında bilgi edinmek için [BGP’ye Genel Bakış](vpn-gateway-bgp-overview.md) ve [BGP’yi yapılandırma](vpn-gateway-bgp-resource-manager-ps.md) makalelerine bakın.</span><span class="sxs-lookup"><span data-stu-id="9f183-184">For information about BGP, see the [BGP Overview](vpn-gateway-bgp-overview.md) and [How to configure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span></span>
* <span data-ttu-id="9f183-185">Zorlamalı Tünel Oluşturma hakkında bilgi için bkz. [Zorlamalı Tünel Oluşturma Hakkında](vpn-gateway-forced-tunneling-rm.md).</span><span class="sxs-lookup"><span data-stu-id="9f183-185">For information about Forced Tunneling, see [About Forced Tunneling](vpn-gateway-forced-tunneling-rm.md).</span></span>
* <span data-ttu-id="9f183-186">Yüksek Oranda Kullanılabilir Etkin-Etkin bağlantılar hakkında bilgi için bkz. [Yüksek Oranda Kullanılabilir Şirket İçi ve Dışı ile Sanal Ağdan Sanal Ağa Bağlantı](vpn-gateway-highlyavailable.md).</span><span class="sxs-lookup"><span data-stu-id="9f183-186">For information about Highly Available Active-Active connections, see [Highly Available cross-premises and VNet-to-VNet connectivity](vpn-gateway-highlyavailable.md).</span></span>
