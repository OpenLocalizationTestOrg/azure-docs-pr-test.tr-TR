---
title: "Şirket içi ağ tooan Azure sanal ağı bağlanın: siteden siteye VPN: portalı | Microsoft Docs"
description: "Şirket içi bir IPSec bağlantısı üzerinden tooan Azure sanal ağı ağ adımları toocreate genel Internet hello. Bu adımları hello portal kullanarak şirket içi siteden siteye VPN ağ geçidi bağlantı oluşturmanıza yardımcı olur."
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
ms.openlocfilehash: 6f0acbaf1bf016026cefade048a116e94686103d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-site-to-site-connection-in-hello-azure-portal"></a><span data-ttu-id="f152e-104">Hello Azure portalında bir siteden siteye bağlantı oluşturma</span><span class="sxs-lookup"><span data-stu-id="f152e-104">Create a Site-to-Site connection in hello Azure portal</span></span>

<span data-ttu-id="f152e-105">Bu makale size nasıl toouse hello Azure portal toocreate, şirket içi ağ toohello VNet bir siteden siteye VPN ağ geçidi bağlantısını gösterir.</span><span class="sxs-lookup"><span data-stu-id="f152e-105">This article shows you how toouse hello Azure portal toocreate a Site-to-Site VPN gateway connection from your on-premises network toohello VNet.</span></span> <span data-ttu-id="f152e-106">Bu makaledeki adımları Hello toohello Resource Manager dağıtım modeli uygulayın.</span><span class="sxs-lookup"><span data-stu-id="f152e-106">hello steps in this article apply toohello Resource Manager deployment model.</span></span> <span data-ttu-id="f152e-107">Liste aşağıdaki hello farklı bir seçeneği seçerek farklı dağıtım aracını veya dağıtım modelini kullanarak bu yapılandırma ayrıca oluşturabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f152e-107">You can also create this configuration using a different deployment tool or deployment model by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="f152e-108">Azure portal</span><span class="sxs-lookup"><span data-stu-id="f152e-108">Azure portal</span></span>](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="f152e-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f152e-109">PowerShell</span></span>](vpn-gateway-create-site-to-site-rm-powershell.md)
> * [<span data-ttu-id="f152e-110">CLI</span><span class="sxs-lookup"><span data-stu-id="f152e-110">CLI</span></span>](vpn-gateway-howto-site-to-site-resource-manager-cli.md)
> * [<span data-ttu-id="f152e-111">Azure portal (klasik)</span><span class="sxs-lookup"><span data-stu-id="f152e-111">Azure portal (classic)</span></span>](vpn-gateway-howto-site-to-site-classic-portal.md)
> 
>

<span data-ttu-id="f152e-112">Kullanılan tooconnect bir siteden siteye VPN gateway bağlantısı olan bir IPSec/IKE (Ikev1 veya Ikev2) VPN tüneli üzerinden tooan Azure sanal ağı şirket içi ağ.</span><span class="sxs-lookup"><span data-stu-id="f152e-112">A Site-to-Site VPN gateway connection is used tooconnect your on-premises network tooan Azure virtual network over an IPsec/IKE (IKEv1 or IKEv2) VPN tunnel.</span></span> <span data-ttu-id="f152e-113">Bağlantı bu tür bir VPN cihazı bulunan dışarıya dönük bir genel IP adresi atanmış tooit olan şirket içi gerektirir.</span><span class="sxs-lookup"><span data-stu-id="f152e-113">This type of connection requires a VPN device located on-premises that has an externally facing public IP address assigned tooit.</span></span> <span data-ttu-id="f152e-114">VPN ağ geçitleri hakkında daha fazla bilgi için bkz. [VPN ağ geçidi hakkında](vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="f152e-114">For more information about VPN gateways, see [About VPN gateway](vpn-gateway-about-vpngateways.md).</span></span>

![Siteden Siteye şirket içi ve dışı karışık VPN Gateway bağlantısı diyagramı](./media/vpn-gateway-howto-site-to-site-resource-manager-portal/site-to-site-diagram.png)

## <a name="before-you-begin"></a><span data-ttu-id="f152e-116">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="f152e-116">Before you begin</span></span>

<span data-ttu-id="f152e-117">Ölçüt yapılandırmanıza başlamadan önce aşağıdaki hello karşıladığınızı doğrulayın:</span><span class="sxs-lookup"><span data-stu-id="f152e-117">Verify that you have met hello following criteria before beginning your configuration:</span></span>

* <span data-ttu-id="f152e-118">Uyumlu bir VPN cihazı ve mümkün tooconfigure olan birisi olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="f152e-118">Make sure you have a compatible VPN device and someone who is able tooconfigure it.</span></span> <span data-ttu-id="f152e-119">Uyumlu VPN cihazları ve cihaz yapılandırması hakkında daha fazla bilgi için bkz.[VPN Cihazları Hakkında](vpn-gateway-about-vpn-devices.md).</span><span class="sxs-lookup"><span data-stu-id="f152e-119">For more information about compatible VPN devices and device configuration, see [About VPN Devices](vpn-gateway-about-vpn-devices.md).</span></span>
* <span data-ttu-id="f152e-120">VPN cihazınız için dışarıya dönük genel bir IPv4 adresi olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="f152e-120">Verify that you have an externally facing public IPv4 address for your VPN device.</span></span> <span data-ttu-id="f152e-121">Bu IP adresi bir NAT’nin arkasında olamaz.</span><span class="sxs-lookup"><span data-stu-id="f152e-121">This IP address cannot be located behind a NAT.</span></span>
* <span data-ttu-id="f152e-122">Bulunan hello IP adresi aralıklarıyla ilgili bilginiz yoksa, şirket içi ağ, bu ayrıntıları sizin için sağlayabilecek biriyle toocoordinate gerekir.</span><span class="sxs-lookup"><span data-stu-id="f152e-122">If you are unfamiliar with hello IP address ranges located in your on-premises network configuration, you need toocoordinate with someone who can provide those details for you.</span></span> <span data-ttu-id="f152e-123">Bu yapılandırma oluşturduğunuzda, Azure tooyour şirket içi konumu yönlendirilecek hello IP adresi aralığı önekleri belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="f152e-123">When you create this configuration, you must specify hello IP address range prefixes that Azure will route tooyour on-premises location.</span></span> <span data-ttu-id="f152e-124">Şirket içi ağınıza hello ağların hiçbiri diz tooconnect için istediğiniz hello sanal ağ alt ağı üzerinden olabilir.</span><span class="sxs-lookup"><span data-stu-id="f152e-124">None of hello subnets of your on-premises network can over lap with hello virtual network subnets that you want tooconnect to.</span></span> 

### <span data-ttu-id="f152e-125"><a name="values"></a>Örnek değerler</span><span class="sxs-lookup"><span data-stu-id="f152e-125"><a name="values"></a>Example values</span></span>

<span data-ttu-id="f152e-126">Bu makaledeki örneklerde Hello değerleri aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="f152e-126">hello examples in this article use hello following values.</span></span> <span data-ttu-id="f152e-127">Bu değerleri toocreate bir test ortamı kullanın veya toothem başvurun toobetter anlamak bu makaledeki hello örnekler.</span><span class="sxs-lookup"><span data-stu-id="f152e-127">You can use these values toocreate a test environment, or refer toothem toobetter understand hello examples in this article.</span></span>

* <span data-ttu-id="f152e-128">**VNet Name:** TestVNet1</span><span class="sxs-lookup"><span data-stu-id="f152e-128">**VNet Name:** TestVNet1</span></span>
* <span data-ttu-id="f152e-129">**Adres Alanı:**</span><span class="sxs-lookup"><span data-stu-id="f152e-129">**Address Space:**</span></span> 
  * <span data-ttu-id="f152e-130">10.11.0.0/16</span><span class="sxs-lookup"><span data-stu-id="f152e-130">10.11.0.0/16</span></span>
  * <span data-ttu-id="f152e-131">10.12.0.0/16 (bu alıştırma için isteğe bağlı)</span><span class="sxs-lookup"><span data-stu-id="f152e-131">10.12.0.0/16 (optional for this exercise)</span></span>
* <span data-ttu-id="f152e-132">**Alt ağlar:**</span><span class="sxs-lookup"><span data-stu-id="f152e-132">**Subnets:**</span></span>
  * <span data-ttu-id="f152e-133">FrontEnd: 10.11.0.0/24</span><span class="sxs-lookup"><span data-stu-id="f152e-133">FrontEnd: 10.11.0.0/24</span></span>
  * <span data-ttu-id="f152e-134">BackEnd: 10.12.0.0/24 (bu alıştırma için isteğe bağlı)</span><span class="sxs-lookup"><span data-stu-id="f152e-134">BackEnd: 10.12.0.0/24 (optional for this exercise)</span></span>
* <span data-ttu-id="f152e-135">**GatewaySubnet:** 10.11.255.0/27</span><span class="sxs-lookup"><span data-stu-id="f152e-135">**GatewaySubnet:** 10.11.255.0/27</span></span>
* <span data-ttu-id="f152e-136">**Kaynak Grubu:** TestRG1</span><span class="sxs-lookup"><span data-stu-id="f152e-136">**Resource Group:** TestRG1</span></span>
* <span data-ttu-id="f152e-137">**Konum:** Doğu ABD</span><span class="sxs-lookup"><span data-stu-id="f152e-137">**Location:** East US</span></span>
* <span data-ttu-id="f152e-138">**DNS Sunucusu:** İsteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="f152e-138">**DNS Server:** Optional.</span></span> <span data-ttu-id="f152e-139">Merhaba, DNS sunucunuzun IP adresi.</span><span class="sxs-lookup"><span data-stu-id="f152e-139">hello IP address of your DNS server.</span></span>
* <span data-ttu-id="f152e-140">**Sanal Ağ Geçidi Adı: VNet1GW**</span><span class="sxs-lookup"><span data-stu-id="f152e-140">**Virtual Network Gateway Name:** VNet1GW</span></span>
* <span data-ttu-id="f152e-141">**Genel IP:** VNet1GWIP</span><span class="sxs-lookup"><span data-stu-id="f152e-141">**Public IP:** VNet1GWIP</span></span>
* <span data-ttu-id="f152e-142">**VPN Türü:** Yol tabanlı</span><span class="sxs-lookup"><span data-stu-id="f152e-142">**VPN Type:** Route-based</span></span>
* <span data-ttu-id="f152e-143">**Bağlantı Türü:** Siteden siteye (IPsec)</span><span class="sxs-lookup"><span data-stu-id="f152e-143">**Connection Type:** Site-to-site (IPsec)</span></span>
* <span data-ttu-id="f152e-144">**Ağ Geçidi Türü:** VPN</span><span class="sxs-lookup"><span data-stu-id="f152e-144">**Gateway Type:** VPN</span></span>
* <span data-ttu-id="f152e-145">**Yerel Ağ Geçidi Adı:** Site2</span><span class="sxs-lookup"><span data-stu-id="f152e-145">**Local Network Gateway Name:** Site2</span></span>
* <span data-ttu-id="f152e-146">**Bağlantı Adı:** VNet1toSite2</span><span class="sxs-lookup"><span data-stu-id="f152e-146">**Connection Name:** VNet1toSite2</span></span>

## <span data-ttu-id="f152e-147"><a name="CreatVNet"></a>1. Sanal ağ oluşturma</span><span class="sxs-lookup"><span data-stu-id="f152e-147"><a name="CreatVNet"></a>1. Create a virtual network</span></span>

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-basic-vnet-s2s-rm-portal-include.md)]

## <span data-ttu-id="f152e-148"><a name="dns"></a>2. DNS sunucusu belirleme</span><span class="sxs-lookup"><span data-stu-id="f152e-148"><a name="dns"></a>2. Specify a DNS server</span></span>

<span data-ttu-id="f152e-149">DNS gerekli toocreate bir Site siteye bağlantı değil.</span><span class="sxs-lookup"><span data-stu-id="f152e-149">DNS is not required toocreate a Site-to-Site connection.</span></span> <span data-ttu-id="f152e-150">Ancak, dağıtılan tooyour sanal ağ için kaynaklar toohave ad çözümlemesi istiyorsanız, bir DNS sunucusunu belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="f152e-150">However, if you want toohave name resolution for resources that are deployed tooyour virtual network, you should specify a DNS server.</span></span> <span data-ttu-id="f152e-151">Bu ayar hello DNS sunucusu, bu sanal ağ için ad çözümlemesi için toouse istediğinizi belirtmenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="f152e-151">This setting lets you specify hello DNS server that you want toouse for name resolution for this virtual network.</span></span> <span data-ttu-id="f152e-152">Bir DNS sunucusu oluşturmaz.</span><span class="sxs-lookup"><span data-stu-id="f152e-152">It does not create a DNS server.</span></span> <span data-ttu-id="f152e-153">Ad çözümlemesi hakkında daha fazla bilgi için bkz. [VM'ler ve rol örnekleri için Ad Çözümlemesi](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span><span class="sxs-lookup"><span data-stu-id="f152e-153">For more information about name resolution, see [Name Resolution for VMs and role instances](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span></span>

[!INCLUDE [vpn-gateway-add-dns-rm-portal](../../includes/vpn-gateway-add-dns-rm-portal-include.md)]

## <span data-ttu-id="f152e-154"><a name="gatewaysubnet"></a>3. Merhaba ağ geçidi alt ağı oluşturun</span><span class="sxs-lookup"><span data-stu-id="f152e-154"><a name="gatewaysubnet"></a>3. Create hello gateway subnet</span></span>

[!INCLUDE [vpn-gateway-aboutgwsubnet](../../includes/vpn-gateway-about-gwsubnet-include.md)]

[!INCLUDE [vpn-gateway-add-gwsubnet-rm-portal](../../includes/vpn-gateway-add-gwsubnet-s2s-rm-portal-include.md)]

## <span data-ttu-id="f152e-155"><a name="VNetGateway"></a>4. Merhaba VPN ağ geçidi oluşturma</span><span class="sxs-lookup"><span data-stu-id="f152e-155"><a name="VNetGateway"></a>4. Create hello VPN gateway</span></span>

[!INCLUDE [vpn-gateway-add-gw-s2s-rm-portal](../../includes/vpn-gateway-add-gw-s2s-rm-portal-include.md)]

## <span data-ttu-id="f152e-156"><a name="LocalNetworkGateway"></a>5. Merhaba yerel ağ geçidi oluşturma</span><span class="sxs-lookup"><span data-stu-id="f152e-156"><a name="LocalNetworkGateway"></a>5. Create hello local network gateway</span></span>

<span data-ttu-id="f152e-157">Merhaba yerel ağ geçidi genellikle tooyour içi konumunuz anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="f152e-157">hello local network gateway typically refers tooyour on-premises location.</span></span> <span data-ttu-id="f152e-158">Merhaba site olarak Azure tooit bakın, sonra kullanabilirsiniz hello IP adresi belirtin bir ad verin hello şirket içi VPN aygıtının toowhich bir bağlantı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="f152e-158">You give hello site a name by which Azure can refer tooit, then specify hello IP address of hello on-premises VPN device toowhich you will create a connection.</span></span> <span data-ttu-id="f152e-159">Ayrıca, hello VPN ağ geçidi toohello VPN cihazı yönlendirilecek hello IP adresi öneklerini belirtin.</span><span class="sxs-lookup"><span data-stu-id="f152e-159">You also specify hello IP address prefixes that will be routed through hello VPN gateway toohello VPN device.</span></span> <span data-ttu-id="f152e-160">Belirttiğiniz hello adres öneklerini hello öneklerini şirket içi ağınızda yer alan var.</span><span class="sxs-lookup"><span data-stu-id="f152e-160">hello address prefixes you specify are hello prefixes located on your on-premises network.</span></span> <span data-ttu-id="f152e-161">Şirket içi ağ değişikliklerinizi veya toochange hello genel IP adresi hello VPN cihazı için gerekiyorsa, hello değerleri daha sonra kolayca güncelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f152e-161">If your on-premises network changes or you need toochange hello public IP address for hello VPN device, you can easily update hello values later.</span></span>

[!INCLUDE [Add local network gateway](../../includes/vpn-gateway-add-lng-s2s-rm-portal-include.md)]

## <span data-ttu-id="f152e-162"><a name="VPNDevice"></a>6. VPN cihazınızı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="f152e-162"><a name="VPNDevice"></a>6. Configure your VPN device</span></span>

<span data-ttu-id="f152e-163">Siteden siteye bağlantıları tooan şirket içi ağ bir VPN cihazı gerektirir.</span><span class="sxs-lookup"><span data-stu-id="f152e-163">Site-to-Site connections tooan on-premises network require a VPN device.</span></span> <span data-ttu-id="f152e-164">Bu adımda VPN cihazınızı yapılandıracaksınız.</span><span class="sxs-lookup"><span data-stu-id="f152e-164">In this step, you configure your VPN device.</span></span> <span data-ttu-id="f152e-165">VPN Cihazınızı yapılandırırken hello aşağıdaki gerekir:</span><span class="sxs-lookup"><span data-stu-id="f152e-165">When configuring your VPN device, you need hello following:</span></span>

- <span data-ttu-id="f152e-166">Paylaşılan bir anahtar.</span><span class="sxs-lookup"><span data-stu-id="f152e-166">A shared key.</span></span> <span data-ttu-id="f152e-167">Bu olduğu hello aynı paylaşılan siteden siteye VPN bağlantınızı oluştururken belirttiğiniz anahtarı.</span><span class="sxs-lookup"><span data-stu-id="f152e-167">This is hello same shared key that you specify when creating your Site-to-Site VPN connection.</span></span> <span data-ttu-id="f152e-168">Bu örneklerde temel bir paylaşılan anahtar kullanılır.</span><span class="sxs-lookup"><span data-stu-id="f152e-168">In our examples, we use a basic shared key.</span></span> <span data-ttu-id="f152e-169">Daha karmaşık bir anahtar toouse oluşturmak öneririz.</span><span class="sxs-lookup"><span data-stu-id="f152e-169">We recommend that you generate a more complex key toouse.</span></span>
- <span data-ttu-id="f152e-170">Merhaba sanal ağ geçidinizin genel IP adresi.</span><span class="sxs-lookup"><span data-stu-id="f152e-170">hello Public IP address of your virtual network gateway.</span></span> <span data-ttu-id="f152e-171">Hello Azure portal, PowerShell veya CLI kullanarak hello ortak IP adresini görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f152e-171">You can view hello public IP address by using hello Azure portal, PowerShell, or CLI.</span></span> <span data-ttu-id="f152e-172">toofind hello hello Azure portal kullanarak VPN ağ geçidinizin genel IP adresi gidin çok**sanal ağ geçitleri**, ağ geçidiniz hello adını tıklatın.</span><span class="sxs-lookup"><span data-stu-id="f152e-172">toofind hello Public IP address of your VPN gateway using hello Azure portal, navigate too**Virtual network gateways**, then click hello name of your gateway.</span></span>

[!INCLUDE [Configure a VPN device](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]

## <span data-ttu-id="f152e-173"><a name="CreateConnection"></a>7. Merhaba VPN bağlantısı oluşturun</span><span class="sxs-lookup"><span data-stu-id="f152e-173"><a name="CreateConnection"></a>7. Create hello VPN connection</span></span>

<span data-ttu-id="f152e-174">Sanal ağ geçidiniz ve şirket içi VPN aygıtınızın arasında Hello siteden siteye VPN bağlantısı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f152e-174">Create hello Site-to-Site VPN connection between your virtual network gateway and your on-premises VPN device.</span></span>

[!INCLUDE [Add connections](../../includes/vpn-gateway-add-site-to-site-connection-s2s-rm-portal-include.md)]

## <span data-ttu-id="f152e-175"><a name="VerifyConnection"></a>8. Merhaba VPN bağlantısını doğrulama</span><span class="sxs-lookup"><span data-stu-id="f152e-175"><a name="VerifyConnection"></a>8. Verify hello VPN connection</span></span>

[!INCLUDE [Verify - Azure portal](../../includes/vpn-gateway-verify-connection-portal-rm-include.md)]

## <span data-ttu-id="f152e-176"><a name="connectVM"></a>tooconnect tooa sanal makine</span><span class="sxs-lookup"><span data-stu-id="f152e-176"><a name="connectVM"></a>tooconnect tooa virtual machine</span></span>

[!INCLUDE [Connect tooa VM](../../includes/vpn-gateway-connect-vm-s2s-include.md)]

## <span data-ttu-id="f152e-177"><a name="reset"></a>Nasıl tooreset bir VPN ağ geçidi</span><span class="sxs-lookup"><span data-stu-id="f152e-177"><a name="reset"></a>How tooreset a VPN gateway</span></span>

<span data-ttu-id="f152e-178">Bir veya daha fazla Siteden Siteye VPN tünelinde şirketler arası VPN bağlantısını kaybederseniz bir Azure VPN ağ geçidinin sıfırlanması yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="f152e-178">Resetting an Azure VPN gateway is helpful if you lose cross-premises VPN connectivity on one or more Site-to-Site VPN tunnels.</span></span> <span data-ttu-id="f152e-179">Bu durumda, şirket içi VPN cihazlarınızı tüm düzgün şekilde çalışıp çalışmadığını, ancak şu tooestablish hello Azure VPN ağ geçitleri ile IPSec tünelleri.</span><span class="sxs-lookup"><span data-stu-id="f152e-179">In this situation, your on-premises VPN devices are all working correctly, but are not able tooestablish IPsec tunnels with hello Azure VPN gateways.</span></span> <span data-ttu-id="f152e-180">Adımlar için bkz. [VPN ağ geçidini sıfırlama](vpn-gateway-resetgw-classic.md).</span><span class="sxs-lookup"><span data-stu-id="f152e-180">For steps, see [Reset a VPN gateway](vpn-gateway-resetgw-classic.md).</span></span>

## <span data-ttu-id="f152e-181"><a name="resize"></a>Nasıl toochange bir ağ geçidi SKU'su (boyutlandırma bir ağ geçidi)</span><span class="sxs-lookup"><span data-stu-id="f152e-181"><a name="resize"></a>How toochange a gateway SKU (resize a gateway)</span></span>

<span data-ttu-id="f152e-182">Merhaba, bir ağ geçidi SKU'su toochange adımları için bkz: [ağ geçidi SKU'ları](vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span><span class="sxs-lookup"><span data-stu-id="f152e-182">For hello steps toochange a gateway SKU, see [Gateway SKUs](vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f152e-183">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f152e-183">Next steps</span></span>

* <span data-ttu-id="f152e-184">BGP hakkında daha fazla bilgi için bkz: Merhaba [BGP genel bakış](vpn-gateway-bgp-overview.md) ve [nasıl tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span><span class="sxs-lookup"><span data-stu-id="f152e-184">For information about BGP, see hello [BGP Overview](vpn-gateway-bgp-overview.md) and [How tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span></span>
* <span data-ttu-id="f152e-185">Zorlamalı Tünel Oluşturma hakkında bilgi için bkz. [Zorlamalı Tünel Oluşturma Hakkında](vpn-gateway-forced-tunneling-rm.md).</span><span class="sxs-lookup"><span data-stu-id="f152e-185">For information about Forced Tunneling, see [About Forced Tunneling](vpn-gateway-forced-tunneling-rm.md).</span></span>
* <span data-ttu-id="f152e-186">Yüksek Oranda Kullanılabilir Etkin-Etkin bağlantılar hakkında bilgi için bkz. [Yüksek Oranda Kullanılabilir Şirket İçi ve Dışı ile Sanal Ağdan Sanal Ağa Bağlantı](vpn-gateway-highlyavailable.md).</span><span class="sxs-lookup"><span data-stu-id="f152e-186">For information about Highly Available Active-Active connections, see [Highly Available cross-premises and VNet-to-VNet connectivity](vpn-gateway-highlyavailable.md).</span></span>
