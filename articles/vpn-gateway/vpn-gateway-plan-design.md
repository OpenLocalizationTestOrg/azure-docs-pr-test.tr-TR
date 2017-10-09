---
title: "Planlama ve tasarım şirket içi bağlantılar için: Azure VPN ağ geçidi | Microsoft Docs"
description: "VPN ağ geçidi planlama ve tasarım şirketler arası, karma ve VNet-VNet bağlantıları hakkında bilgi edinin"
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: d5aaab83-4e74-4484-8bf0-cc465811e757
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/27/2017
ms.author: cherylmc
ms.openlocfilehash: 3d4587ba31d163384212eca88a7e2c0ba8f3b21f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="planning-and-design-for-vpn-gateway"></a><span data-ttu-id="907be-103">VPN Gateway için planlama ve tasarım</span><span class="sxs-lookup"><span data-stu-id="907be-103">Planning and design for VPN Gateway</span></span>

<span data-ttu-id="907be-104">Planlama ve tasarlama şirketler arası ve VNet-VNet yapılandırmaları basit ya da ağ gereksinimlerinize bağlı olarak karmaşık olabilir.</span><span class="sxs-lookup"><span data-stu-id="907be-104">Planning and designing your cross-premises and VNet-to-VNet configurations can be either simple, or complicated, depending on your networking needs.</span></span> <span data-ttu-id="907be-105">Bu makalede temel planlama ve tasarım konuları anlatılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="907be-105">This article walks you through basic planning and design considerations.</span></span>

## <span data-ttu-id="907be-106"><a name="planning"></a>Planlama</span><span class="sxs-lookup"><span data-stu-id="907be-106"><a name="planning"></a>Planning</span></span>

### <span data-ttu-id="907be-107"><a name="compare"></a>Şirketler arası bağlantı seçenekleri</span><span class="sxs-lookup"><span data-stu-id="907be-107"><a name="compare"></a>Cross-premises connectivity options</span></span>

<span data-ttu-id="907be-108">Tooconnect istiyorsanız, şirket içi siteler güvenli bir şekilde tooa sanal ağ, bu nedenle üç farklı şekilde toodo gerekir: siteden siteye noktadan siteye ve ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="907be-108">If you want tooconnect your on-premises sites securely tooa virtual network, you have three different ways toodo so: Site-to-Site, Point-to-Site, and ExpressRoute.</span></span> <span data-ttu-id="907be-109">Kullanılabilir hello farklı şirket içi bağlantılar karşılaştırın.</span><span class="sxs-lookup"><span data-stu-id="907be-109">Compare hello different cross-premises connections that are available.</span></span> <span data-ttu-id="907be-110">Merhaba seçeneği gibi çeşitli etmenlere bağlı olabilir:</span><span class="sxs-lookup"><span data-stu-id="907be-110">hello option you choose can depend on various considerations, such as:</span></span>

* <span data-ttu-id="907be-111">Çözümünüz ne tür bir verimlilik gerektiriyor?</span><span class="sxs-lookup"><span data-stu-id="907be-111">What kind of throughput does your solution require?</span></span>
* <span data-ttu-id="907be-112">Merhaba toocommunicate istiyorsunuz genel Internet güvenli VPN aracılığıyla ya da özel bir bağlantı üzerinden mi?</span><span class="sxs-lookup"><span data-stu-id="907be-112">Do you want toocommunicate over hello public Internet via secure VPN, or over a private connection?</span></span>
* <span data-ttu-id="907be-113">Genel bir IP adresi kullanılabilir toouse var mı?</span><span class="sxs-lookup"><span data-stu-id="907be-113">Do you have a public IP address available toouse?</span></span>
* <span data-ttu-id="907be-114">Toouse bir VPN cihazı planlıyor musunuz?</span><span class="sxs-lookup"><span data-stu-id="907be-114">Are you planning toouse a VPN device?</span></span> <span data-ttu-id="907be-115">Bu uyumlu bir VPN cihazı mı?</span><span class="sxs-lookup"><span data-stu-id="907be-115">If so, is it compatible?</span></span>
* <span data-ttu-id="907be-116">Sadece bir kaç bilgisayarla mı bağlanıyorsunuz yoksa siteniz için kalıcı bir bağlantı istiyor musunuz?</span><span class="sxs-lookup"><span data-stu-id="907be-116">Are you connecting just a few computers, or do you want a persistent connection for your site?</span></span>
* <span data-ttu-id="907be-117">Ne tür bir VPN ağ geçidi gereklidir hello çözüm için toocreate istiyorsunuz?</span><span class="sxs-lookup"><span data-stu-id="907be-117">What type of VPN gateway is required for hello solution you want toocreate?</span></span>
* <span data-ttu-id="907be-118">Hangi ağ geçidi SKU'su kullanmalısınız?</span><span class="sxs-lookup"><span data-stu-id="907be-118">Which gateway SKU should you use?</span></span>

### <span data-ttu-id="907be-119"><a name="planningtable"></a>Tablo planlama</span><span class="sxs-lookup"><span data-stu-id="907be-119"><a name="planningtable"></a>Planning table</span></span>

<span data-ttu-id="907be-120">Aşağıdaki tablonun hello hello çözümünüz için en iyi bağlantı seçeneğine karar vermenize yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="907be-120">hello following table can help you decide hello best connectivity option for your solution.</span></span>

[!INCLUDE [vpn-gateway-cross-premises](../../includes/vpn-gateway-cross-premises-include.md)]

### <span data-ttu-id="907be-121"><a name="gwsku"></a>Ağ Geçidi SKU'ları</span><span class="sxs-lookup"><span data-stu-id="907be-121"><a name="gwsku"></a>Gateway SKUs</span></span>

[!INCLUDE [vpn-gateway-table-gwtype-aggtput](../../includes/vpn-gateway-table-gwtype-aggtput-include.md)]

### <span data-ttu-id="907be-122"><a name="wf"></a>İş akışı</span><span class="sxs-lookup"><span data-stu-id="907be-122"><a name="wf"></a>Workflow</span></span>

<span data-ttu-id="907be-123">Merhaba aşağıdaki liste anahatları bulut bağlantı için genel iş akışı hello:</span><span class="sxs-lookup"><span data-stu-id="907be-123">hello following list outlines hello common workflow for cloud connectivity:</span></span>

1. <span data-ttu-id="907be-124">Tasarım ve tüm ağları için bağlantı topolojisi ve liste hello adres alanları planı tooconnect istiyor.</span><span class="sxs-lookup"><span data-stu-id="907be-124">Design and plan your connectivity topology and list hello address spaces for all networks you want tooconnect.</span></span>
2. <span data-ttu-id="907be-125">Bir Azure sanal ağı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="907be-125">Create an Azure virtual network.</span></span> 
3. <span data-ttu-id="907be-126">Merhaba sanal ağ için bir VPN ağ geçidi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="907be-126">Create a VPN gateway for hello virtual network.</span></span>
4. <span data-ttu-id="907be-127">Oluşturun ve bağlantıları tooon içi ağlarda veya diğer sanal (gerekirse) yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="907be-127">Create and configure connections tooon-premises networks or other virtual networks (as needed).</span></span>
5. <span data-ttu-id="907be-128">Oluşturun ve bir noktadan siteye bağlantı (gerektiğinde), Azure VPN ağ geçidi için yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="907be-128">Create and configure a Point-to-Site connection for your Azure VPN gateway (as needed).</span></span>

## <span data-ttu-id="907be-129"><a name="design"></a>Tasarım</span><span class="sxs-lookup"><span data-stu-id="907be-129"><a name="design"></a>Design</span></span>
### <span data-ttu-id="907be-130"><a name="topologies"></a>Bağlantı topolojileri</span><span class="sxs-lookup"><span data-stu-id="907be-130"><a name="topologies"></a>Connection topologies</span></span>

<span data-ttu-id="907be-131">Başlangıç hello hello diyagramlarda bakarak [VPN Gateway hakkında](vpn-gateway-about-vpngateways.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="907be-131">Start by looking at hello diagrams in hello [About VPN Gateway](vpn-gateway-about-vpngateways.md) article.</span></span> <span data-ttu-id="907be-132">Merhaba makale temel diyagramları, hello dağıtım modellerinde her topoloji ve yapılandırmanızı toodeploy kullanabileceğiniz hello kullanılabilir dağıtım araçları içerir.</span><span class="sxs-lookup"><span data-stu-id="907be-132">hello article contains basic diagrams, hello deployment models for each topology, and hello available deployment tools you can use toodeploy your configuration.</span></span>

### <span data-ttu-id="907be-133"><a name="designbasics"></a>Tasarım temelleri</span><span class="sxs-lookup"><span data-stu-id="907be-133"><a name="designbasics"></a>Design basics</span></span>

<span data-ttu-id="907be-134">Aşağıdaki bölümlerde hello hello VPN ağ geçidi temelleri tartışın.</span><span class="sxs-lookup"><span data-stu-id="907be-134">hello following sections discuss hello VPN gateway basics.</span></span> 

#### <span data-ttu-id="907be-135"><a name="servicelimits"></a>Ağ Hizmetleri sınırları</span><span class="sxs-lookup"><span data-stu-id="907be-135"><a name="servicelimits"></a>Networking services limits</span></span>

<span data-ttu-id="907be-136">Merhaba tabloları tooview arasında kaydırma [Ağ Hizmetleri sınırları](../azure-subscription-service-limits.md#networking-limits).</span><span class="sxs-lookup"><span data-stu-id="907be-136">Scroll through hello tables tooview [networking services limits](../azure-subscription-service-limits.md#networking-limits).</span></span> <span data-ttu-id="907be-137">listelenen hello sınırları tasarımınızı etkileyebilir.</span><span class="sxs-lookup"><span data-stu-id="907be-137">hello limits listed may impact your design.</span></span>

#### <span data-ttu-id="907be-138"><a name="subnets"></a>Alt ağlar hakkında</span><span class="sxs-lookup"><span data-stu-id="907be-138"><a name="subnets"></a>About subnets</span></span>

<span data-ttu-id="907be-139">Bağlantıları oluştururken, alt ağ aralıklarını dikkate almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="907be-139">When you are creating connections, you must consider your subnet ranges.</span></span> <span data-ttu-id="907be-140">Alt ağ adres aralıklarını çakışan sahip olamaz.</span><span class="sxs-lookup"><span data-stu-id="907be-140">You cannot have overlapping subnet address ranges.</span></span> <span data-ttu-id="907be-141">Çakışan bir alt ağla hello başka bir konuma hello aynı adres alanı içeren bir sanal ağ veya şirket içi konumunu içeren durumdur.</span><span class="sxs-lookup"><span data-stu-id="907be-141">An overlapping subnet is when one virtual network or on-premises location contains hello same address space that hello other location contains.</span></span> <span data-ttu-id="907be-142">Bu, ağ mühendisleri, yerel şirket içi ağlar toocarve, toouse için bir aralığı çıkışı için Azure IP için gereken alanı/alt adresleme anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="907be-142">This means that you need your network engineers for your local on-premises networks toocarve out a range for you toouse for your Azure IP addressing space/subnets.</span></span> <span data-ttu-id="907be-143">Merhaba yerel şirket içi ağda kullanılmayan adres alanı gerekir.</span><span class="sxs-lookup"><span data-stu-id="907be-143">You need address space that is not being used on hello local on-premises network.</span></span>

<span data-ttu-id="907be-144">VNet-VNet bağlantıları ile çalışırken çakışan alt ağlarınız önleme da önemlidir.</span><span class="sxs-lookup"><span data-stu-id="907be-144">Avoiding overlapping subnets is also important when you are working with VNet-to-VNet connections.</span></span> <span data-ttu-id="907be-145">Alt ağlarınızın çakışmayan bir IP adresi hello gönderme ve hedef sanal ağlar bulunuyorsa, VNet-VNet bağlantı başarısız.</span><span class="sxs-lookup"><span data-stu-id="907be-145">If your subnets overlap and an IP address exists in both hello sending and destination VNets, VNet-to-VNet connections fail.</span></span> <span data-ttu-id="907be-146">Merhaba hedef adres VNet gönderme hello parçası olduğundan azure diğer Vnet'in hello veri toohello yönlendiremezsiniz.</span><span class="sxs-lookup"><span data-stu-id="907be-146">Azure can't route hello data toohello other VNet because hello destination address is part of hello sending VNet.</span></span>

<span data-ttu-id="907be-147">VPN ağ geçitleri bir ağ geçidi alt ağı olarak adlandırılan belirli bir alt gerektirir.</span><span class="sxs-lookup"><span data-stu-id="907be-147">VPN Gateways require a specific subnet called a gateway subnet.</span></span> <span data-ttu-id="907be-148">Tüm ağ geçidi alt ağları GatewaySubnet toowork düzgün olarak adlandırılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="907be-148">All gateway subnets must be named GatewaySubnet toowork properly.</span></span> <span data-ttu-id="907be-149">Mutlaka değil tooname farklı bir ağ geçidi alt ağınızı adlandırın ve Vm'leri veya herhangi bir şey başka toohello ağ geçidi alt ağı dağıtmazsınız.</span><span class="sxs-lookup"><span data-stu-id="907be-149">Be sure not tooname your gateway subnet a different name, and don't deploy VMs or anything else toohello gateway subnet.</span></span> <span data-ttu-id="907be-150">Bkz: [ağ geçidi alt ağları](vpn-gateway-about-vpn-gateway-settings.md#gwsub).</span><span class="sxs-lookup"><span data-stu-id="907be-150">See [Gateway Subnets](vpn-gateway-about-vpn-gateway-settings.md#gwsub).</span></span>

#### <span data-ttu-id="907be-151"><a name="local"></a>Yerel ağ geçitleri hakkında</span><span class="sxs-lookup"><span data-stu-id="907be-151"><a name="local"></a>About local network gateways</span></span>

<span data-ttu-id="907be-152">Merhaba yerel ağ geçidi genellikle tooyour içi konumunuz anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="907be-152">hello local network gateway typically refers tooyour on-premises location.</span></span> <span data-ttu-id="907be-153">Merhaba Klasik dağıtım modelinde, başvurulan tooas bir yerel ağ Site hello yerel ağ geçididir.</span><span class="sxs-lookup"><span data-stu-id="907be-153">In hello classic deployment model, hello local network gateway is referred tooas a Local Network Site.</span></span> <span data-ttu-id="907be-154">Bir yerel ağ geçidi yapılandırdığınızda hello hello şirket içi VPN cihazının genel IP adresini belirtin bir ad verin ve hello şirket içi konumdaysa hello adres öneklerini belirtirsiniz.</span><span class="sxs-lookup"><span data-stu-id="907be-154">When you configure a local network gateway, you give it a name, specify hello public IP address of hello on-premises VPN device, and specify hello address prefixes that are in hello on-premises location.</span></span> <span data-ttu-id="907be-155">Azure ağ trafiği için hello hedef adres öneklerine bakar, hello yerel ağ geçidi için belirttiğiniz hello yapılandırma bakar ve paketleri buna uygun şekilde yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="907be-155">Azure looks at hello destination address prefixes for network traffic, consults hello configuration that you have specified for hello local network gateway, and routes packets accordingly.</span></span> <span data-ttu-id="907be-156">Merhaba adres öneklerini gerektiği gibi değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="907be-156">You can modify hello address prefixes as needed.</span></span> <span data-ttu-id="907be-157">Daha fazla bilgi için bkz: [yerel ağ geçitleri](vpn-gateway-about-vpn-gateway-settings.md#lng).</span><span class="sxs-lookup"><span data-stu-id="907be-157">For more information, see [Local network gateways](vpn-gateway-about-vpn-gateway-settings.md#lng).</span></span>

#### <span data-ttu-id="907be-158"><a name="gwtype"></a>Ağ geçidi türleri hakkında</span><span class="sxs-lookup"><span data-stu-id="907be-158"><a name="gwtype"></a>About gateway types</span></span>

<span data-ttu-id="907be-159">Topolojiniz için Hello doğru ağ geçidi türünü seçme önemlidir.</span><span class="sxs-lookup"><span data-stu-id="907be-159">Selecting hello correct gateway type for your topology is critical.</span></span> <span data-ttu-id="907be-160">Merhaba yanlış tür seçerseniz, ağ geçidi düzgün çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="907be-160">If you select hello wrong type, your gateway won't work properly.</span></span> <span data-ttu-id="907be-161">Merhaba ağ geçidinin nasıl bağlanır ve hello Resource Manager dağıtım modeli için gereken Yapılandırma ayarıdır Hello ağ geçidi türünü belirtir.</span><span class="sxs-lookup"><span data-stu-id="907be-161">hello gateway type specifies how hello gateway itself connects and is a required configuration setting for hello Resource Manager deployment model.</span></span>

<span data-ttu-id="907be-162">Merhaba ağ geçidi türleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="907be-162">hello gateway types are:</span></span>

* <span data-ttu-id="907be-163">VPN</span><span class="sxs-lookup"><span data-stu-id="907be-163">Vpn</span></span>
* <span data-ttu-id="907be-164">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="907be-164">ExpressRoute</span></span>

#### <span data-ttu-id="907be-165"><a name="connectiontype"></a>Bağlantı türleri hakkında</span><span class="sxs-lookup"><span data-stu-id="907be-165"><a name="connectiontype"></a>About connection types</span></span>

<span data-ttu-id="907be-166">Her bağlantı belirli bir bağlantı türü gerektirir.</span><span class="sxs-lookup"><span data-stu-id="907be-166">Each configuration requires a specific connection type.</span></span> <span data-ttu-id="907be-167">Merhaba bağlantı türleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="907be-167">hello connection types are:</span></span>

* <span data-ttu-id="907be-168">IPsec</span><span class="sxs-lookup"><span data-stu-id="907be-168">IPsec</span></span>
* <span data-ttu-id="907be-169">Vnet2Vnet</span><span class="sxs-lookup"><span data-stu-id="907be-169">Vnet2Vnet</span></span>
* <span data-ttu-id="907be-170">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="907be-170">ExpressRoute</span></span>
* <span data-ttu-id="907be-171">VPNClient</span><span class="sxs-lookup"><span data-stu-id="907be-171">VPNClient</span></span>

#### <span data-ttu-id="907be-172"><a name="vpntype"></a>VPN türleri hakkında</span><span class="sxs-lookup"><span data-stu-id="907be-172"><a name="vpntype"></a>About VPN types</span></span>

<span data-ttu-id="907be-173">Her yapılandırma özel bir VPN türü gerektirir.</span><span class="sxs-lookup"><span data-stu-id="907be-173">Each configuration requires a specific VPN type.</span></span> <span data-ttu-id="907be-174">Bir siteden siteye bağlantı ve noktadan siteye bağlantı toohello oluşturma gibi iki yapılandırmayı birleştiriyorsanız aynı sanal ağı, her iki bağlantı gereksinimini de karşılayan bir VPN türü kullanmalısınız.</span><span class="sxs-lookup"><span data-stu-id="907be-174">If you are combining two configurations, such as creating a Site-to-Site connection and a Point-to-Site connection toohello same VNet, you must use a VPN type that satisfies both connection requirements.</span></span>

[!INCLUDE [vpn-gateway-vpntype](../../includes/vpn-gateway-vpntype-include.md)]

<span data-ttu-id="907be-175">tooeach bağlantı yapılandırması eşlemeleri gibi hello aşağıdaki tablolarda hello VPN türü gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="907be-175">hello following tables show hello VPN type as it maps tooeach connection configuration.</span></span> <span data-ttu-id="907be-176">Emin hello toocreate istediğiniz ağ geçidi eşleşmeleri hello yapılandırmanız için VPN türü olun.</span><span class="sxs-lookup"><span data-stu-id="907be-176">Make sure hello VPN type for your gateway matches hello configuration that you want toocreate.</span></span> 

[!INCLUDE [vpn-gateway-table-vpntype](../../includes/vpn-gateway-table-vpntype-include.md)]

### <span data-ttu-id="907be-177"><a name="devices"></a>Siteden siteye bağlantıları için VPN cihazları</span><span class="sxs-lookup"><span data-stu-id="907be-177"><a name="devices"></a>VPN devices for Site-to-Site connections</span></span>

<span data-ttu-id="907be-178">dağıtım modeli, bağımsız olarak tooconfigure bir Site siteye bağlantı aşağıdaki öğeleri hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="907be-178">tooconfigure a Site-to-Site connection, regardless of deployment model, you need hello following items:</span></span>

* <span data-ttu-id="907be-179">Azure VPN ağ geçitleri ile uyumlu bir VPN cihazı</span><span class="sxs-lookup"><span data-stu-id="907be-179">A VPN device that is compatible with Azure VPN gateways</span></span>
* <span data-ttu-id="907be-180">Bir genel kullanıma yönelik IPv4 IP adresi bir NAT'nin arkasında değildir</span><span class="sxs-lookup"><span data-stu-id="907be-180">A public-facing IPv4 IP address that is not behind a NAT</span></span>

<span data-ttu-id="907be-181">VPN Cihazınızı yapılandırmak toohave deneyimi ihtiyacınız veya birisi bu can sahip hello cihaz yapılandırdığınız.</span><span class="sxs-lookup"><span data-stu-id="907be-181">You need toohave experience configuring your VPN device, or have someone that can configure hello device for you.</span></span>

[!INCLUDE [vpn-gateway-configure-vpn-device-rm](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]

### <span data-ttu-id="907be-182"><a name="forcedtunnel"></a>Zorlamalı tünel yönlendirme göz önünde bulundurun</span><span class="sxs-lookup"><span data-stu-id="907be-182"><a name="forcedtunnel"></a>Consider forced tunnel routing</span></span>

<span data-ttu-id="907be-183">Çoğu yapılandırmada zorlamalı tünel yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="907be-183">For most configurations, you can configure forced tunneling.</span></span> <span data-ttu-id="907be-184">Yeniden yönlendirme veya "tüm Internet'e bağlı trafik geri tooyour şirket içi konumu denetleme ve denetim için bir siteden siteye VPN tüneli aracılığıyla zorla" sağlar tünel zorlandı.</span><span class="sxs-lookup"><span data-stu-id="907be-184">Forced tunneling lets you redirect or "force" all Internet-bound traffic back tooyour on-premises location via a Site-to-Site VPN tunnel for inspection and auditing.</span></span> <span data-ttu-id="907be-185">Bu, çoğu kurumsal BT için kritik güvenlik gereksinimdir ilkeleri.</span><span class="sxs-lookup"><span data-stu-id="907be-185">This is a critical security requirement for most enterprise IT policies.</span></span> 

<span data-ttu-id="907be-186">Zorlamalı tünel olmadan, Internet'e bağlı trafik, vm'lerden azure'da her zaman toohello Internet hello seçeneği tooallow olmadan çıkışı doğrudan Azure ağ altyapısından, tooinspect ya da Denetim hello trafik dizinlere.</span><span class="sxs-lookup"><span data-stu-id="907be-186">Without forced tunneling, Internet-bound traffic from your VMs in Azure will always traverse from Azure network infrastructure directly out toohello Internet, without hello option tooallow you tooinspect or audit hello traffic.</span></span> <span data-ttu-id="907be-187">Yetkisiz Internet erişimine olası tooinformation açığa çıkmasına veya diğer tür güvenlik ihlallerini yol açabilir.</span><span class="sxs-lookup"><span data-stu-id="907be-187">Unauthorized Internet access can potentially lead tooinformation disclosure or other types of security breaches.</span></span>

<span data-ttu-id="907be-188">Zorlamalı Tünel bağlantısı her iki dağıtım modeli ve farklı araçlar kullanılarak yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="907be-188">A forced tunneling connection can be configured in both deployment models and by using different tools.</span></span> <span data-ttu-id="907be-189">Daha fazla bilgi için bkz: [zorlamalı tüneli yapılandırma](vpn-gateway-forced-tunneling-rm.md).</span><span class="sxs-lookup"><span data-stu-id="907be-189">For more information, see [Configure forced tunneling](vpn-gateway-forced-tunneling-rm.md).</span></span>

<span data-ttu-id="907be-190">**Zorlamalı tünel diyagramı**</span><span class="sxs-lookup"><span data-stu-id="907be-190">**Forced tunneling diagram**</span></span>

![Azure VPN ağ geçidi zorlamalı tünel diyagramı](./media/vpn-gateway-plan-design/forced-tunneling-diagram.png)

## <a name="next-steps"></a><span data-ttu-id="907be-192">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="907be-192">Next steps</span></span>

<span data-ttu-id="907be-193">Merhaba bkz [VPN Gateway SSS](vpn-gateway-vpn-faq.md) ve [VPN Gateway hakkında](vpn-gateway-about-vpngateways.md) makaleler için daha fazla bilgi toohelp, tasarımınız ile.</span><span class="sxs-lookup"><span data-stu-id="907be-193">See hello [VPN Gateway FAQ](vpn-gateway-vpn-faq.md) and [About VPN Gateway](vpn-gateway-about-vpngateways.md) articles for more information toohelp you with your design.</span></span>

<span data-ttu-id="907be-194">Belirli ağ geçidi ayarları hakkında daha fazla bilgi için bkz: [hakkında VPN ağ geçidi ayarlarını](vpn-gateway-about-vpn-gateway-settings.md).</span><span class="sxs-lookup"><span data-stu-id="907be-194">For more information about specific gateway settings, see [About VPN Gateway Settings](vpn-gateway-about-vpn-gateway-settings.md).</span></span>