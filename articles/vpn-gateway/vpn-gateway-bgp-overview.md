---
title: "Azure VPN Gateways ile BGP'ye genel bakış | Microsoft Docs"
description: "Bu makale Azure VPN Gateways ile BGP’ye genel bakış sağlar."
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: 
ms.assetid: f8c3985c-c128-4f34-835c-0e88742bf36e
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/12/2017
ms.author: yushwang
ms.openlocfilehash: 60d8dd45ecbd4a075721c25acadb21d4e2fd5448
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="overview-of-bgp-with-azure-vpn-gateways"></a><span data-ttu-id="1ec78-103">Azure VPN Gateways ile BGP’ye genel bakış</span><span class="sxs-lookup"><span data-stu-id="1ec78-103">Overview of BGP with Azure VPN Gateways</span></span>
<span data-ttu-id="1ec78-104">Bu makale Azure VPN Gateways içindeki BGP (Sınır Ağ Geçidi Protokolü) desteğine genel bakış sağlar.</span><span class="sxs-lookup"><span data-stu-id="1ec78-104">This article provides an overview of BGP (Border Gateway Protocol) support in Azure VPN Gateways.</span></span>

<span data-ttu-id="1ec78-105">BGP iki veya daha fazla ağ arasında yönlendirme ve ulaşılabilirlik bilgilerini takas etmek üzere İnternet’te yaygın olarak kullanılan standart yönlendirme protokolüdür.</span><span class="sxs-lookup"><span data-stu-id="1ec78-105">BGP is the standard routing protocol commonly used in the Internet to exchange routing and reachability information between two or more networks.</span></span> <span data-ttu-id="1ec78-106">BGP, Azure Virtual Networks bağlamında kullanıldığında her iki ağ geçidini ön eklerin ilgili ağ geçitlerinden veya yönlendiricilerden geçmeye yönelik kullanılabilirliği ve ulaşılabilirliği konusunda bilgilendiren “yolları” değiştirmek amacıyla, Azure VPN Gateways’i ve BGP eşlikleri veya komşuları olarak adlandırılan şirket içi VPN cihazlarınızı etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="1ec78-106">When used in the context of Azure Virtual Networks, BGP enables the Azure VPN Gateways and your on-premises VPN devices, called BGP peers or neighbors, to exchange "routes" that will inform both gateways on the availability and reachability for those prefixes to go through the gateways or routers involved.</span></span> <span data-ttu-id="1ec78-107">BGP ayrıca bir BGP ağ geçidinin öğrendiği yolları bir BGP eşliğinden diğer tüm BGP eşliklerine yayarak birden fazla ağ arasında geçiş yönlendirmesi sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="1ec78-107">BGP can also enable transit routing among multiple networks by propagating routes a BGP gateway learns from one BGP peer to all other BGP peers.</span></span> 

## <a name="why-use-bgp"></a><span data-ttu-id="1ec78-108">BGP neden kullanılır?</span><span class="sxs-lookup"><span data-stu-id="1ec78-108">Why use BGP?</span></span>
<span data-ttu-id="1ec78-109">BGP, Azure Yol Tabanlı VPN ağ geçitleri ile birlikte kullanabileceğiniz isteğe bağlı bir özelliktir.</span><span class="sxs-lookup"><span data-stu-id="1ec78-109">BGP is an optional feature you can use with Azure Route-Based VPN gateways.</span></span> <span data-ttu-id="1ec78-110">Özelliği etkinleştirmeden önce şirket içi VPN cihazlarınızın da BGP’yi desteklediğinden emin olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="1ec78-110">You should also make sure your on-premises VPN devices support BGP before you enable the feature.</span></span> <span data-ttu-id="1ec78-111">Azure VPN ağ geçitlerini ve şirket içi VPN cihazlarınızı BGP olmadan kullanmaya devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1ec78-111">You can continue to use Azure VPN gateways and your on-premises VPN devices without BGP.</span></span> <span data-ttu-id="1ec78-112">BGP ile ağlarınız ve Azure arasında statik yollar kullanmaya (BGP olmadan) *karşılık* BGP ile dinamik yönlendirme kullanmanın eşdeğeridir.</span><span class="sxs-lookup"><span data-stu-id="1ec78-112">It is the equivalent of using static routes (without BGP) *vs.* using dynamic routing with BGP between your networks and Azure.</span></span>

<span data-ttu-id="1ec78-113">BGP’nin çeşitli avantajları ve yeni özellikleri vardır:</span><span class="sxs-lookup"><span data-stu-id="1ec78-113">There are several advantages and new capabilities with BGP:</span></span>

### <a name="support-automatic-and-flexible-prefix-updates"></a><span data-ttu-id="1ec78-114">Otomatik ve esnek ön ek güncelleştirmelerini destekler</span><span class="sxs-lookup"><span data-stu-id="1ec78-114">Support automatic and flexible prefix updates</span></span>
<span data-ttu-id="1ec78-115">BGP ile yalnızca belirli bir BGP eşliğine IPSec S2S VPN tüneli üzerinden en küçük ön eki bildirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="1ec78-115">With BGP, you only need to declare a minimum prefix to a specific BGP peer over the IPsec S2S VPN tunnel.</span></span> <span data-ttu-id="1ec78-116">Şirket içi VPN cihazınızın BGP eşliği IP adresinin ana bilgisayar ön eki (/32) kadar küçük olabilir.</span><span class="sxs-lookup"><span data-stu-id="1ec78-116">It can be as small as a host prefix (/32) of the BGP peer IP address of your on-premises VPN device.</span></span> <span data-ttu-id="1ec78-117">Azure Virtual Network’un erişmesine izin vermek üzere hangi şirket içi ağ ön eklerinin Azure’a tanıtılacağını denetleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1ec78-117">You can control which on-premises network prefixes you want to advertise to Azure to allow your Azure Virtual Network to access.</span></span>

<span data-ttu-id="1ec78-118">Ayrıca, büyük özel bir IP adres alanı (örneğin, 10.0.0.0/8) gibi VNet adres ön bazıları içerebilir büyük ön ekler tanıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1ec78-118">You can also advertise larger prefixes that may include some of your VNet address prefixes, such as a large private IP address space (for example, 10.0.0.0/8).</span></span> <span data-ttu-id="1ec78-119">Ön ekler VNet ön herhangi biri ile aynı olamaz olsa unutmayın.</span><span class="sxs-lookup"><span data-stu-id="1ec78-119">Note though the prefixes cannot be identical with any one of your VNet prefixes.</span></span> <span data-ttu-id="1ec78-120">VNet ön eklerinizle aynı olan yollar reddedilir.</span><span class="sxs-lookup"><span data-stu-id="1ec78-120">Those routes identical to your VNet prefixes will be rejected.</span></span>

### <a name="support-multiple-tunnels-between-a-vnet-and-an-on-premises-site-with-automatic-failover-based-on-bgp"></a><span data-ttu-id="1ec78-121">Bir VNet ile şirket içi site arasında BGP’yi temel alan otomatik yük devretme ile birden fazla tüneli destekler</span><span class="sxs-lookup"><span data-stu-id="1ec78-121">Support multiple tunnels between a VNet and an on-premises site with automatic failover based on BGP</span></span>
<span data-ttu-id="1ec78-122">Azure VNet ile şirket içi VPN cihazlarınız arasında aynı konumda birden fazla bağlantı kurabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1ec78-122">You can establish multiple connections between your Azure VNet and your on-premises VPN devices in the same location.</span></span> <span data-ttu-id="1ec78-123">Bu özellik aktif-aktif bir yapılandırmadaki iki ağ arasında birden fazla tünel (yol) sağlar.</span><span class="sxs-lookup"><span data-stu-id="1ec78-123">This capability provides multiple tunnels (paths) between the two networks in an active-active configuration.</span></span> <span data-ttu-id="1ec78-124">Tünellerden birinin bağlantısı kesilirse karşılık gelen yollar BGP aracılığıyla geri çekilir ve trafik kalan tünellere otomatik olarak geçer.</span><span class="sxs-lookup"><span data-stu-id="1ec78-124">If one of the tunnels is disconnected, the corresponding routes will be withdrawn via BGP and the traffic automatically shifts to the remaining tunnels.</span></span>

<span data-ttu-id="1ec78-125">Aşağıdaki diyagramda yüksek oranda kullanılabilen bu kurulumun basit bir örneği gösterilmiştir:</span><span class="sxs-lookup"><span data-stu-id="1ec78-125">The following diagram shows a simple example of this highly available setup:</span></span>

![Birden fazla etkin yol](./media/vpn-gateway-bgp-overview/multiple-active-tunnels.png)

### <a name="support-transit-routing-between-your-on-premises-networks-and-multiple-azure-vnets"></a><span data-ttu-id="1ec78-127">Şirket içi ağlarınız ile birden fazla Azure VNet arasında geçiş yönlendirme desteği</span><span class="sxs-lookup"><span data-stu-id="1ec78-127">Support transit routing between your on-premises networks and multiple Azure VNets</span></span>
<span data-ttu-id="1ec78-128">BGP, doğrudan veya dolaylı olarak bağlı olmasına bakılmaksızın birden fazla ağ geçidinin farklı ağlardaki ön ekleri öğrenmesini ve yaymasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="1ec78-128">BGP enables multiple gateways to learn and propagate prefixes from different networks, whether they are directly or indirectly connected.</span></span> <span data-ttu-id="1ec78-129">Bu özellik şirket içi siteleriniz arasında veya birden fazla Azure Sanal Ağında Azure VPN ağ geçitleri ile geçiş yönlendirmesi sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="1ec78-129">This can enable transit routing with Azure VPN gateways between your on-premises sites or across multiple Azure Virtual Networks.</span></span>

<span data-ttu-id="1ec78-130">Aşağıdaki diyagramda Microsoft Networks içindeki Azure VPN ağ geçitleri üzerinden iki şirket içi ağ arasındaki trafiği geçebilen birden fazla yola sahip çoklu atlamalı bir topolojinin örneği gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="1ec78-130">The following diagram shows an example of a multi-hop topology with multiple paths that can transit traffic between the two on-premises networks through Azure VPN gateways within the Microsoft Networks:</span></span>

![Çoklu atlamalı geçiş](./media/vpn-gateway-bgp-overview/full-mesh-transit.png)

## <a name="bgp-faq"></a><span data-ttu-id="1ec78-132">BGP SSS</span><span class="sxs-lookup"><span data-stu-id="1ec78-132">BGP FAQ</span></span>
[!INCLUDE [vpn-gateway-bgp-faq-include](../../includes/vpn-gateway-bpg-faq-include.md)]

## <a name="next-steps"></a><span data-ttu-id="1ec78-133">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1ec78-133">Next steps</span></span>
<span data-ttu-id="1ec78-134">BGP’yi şirketler arası ve VNet’ten VNet’te bağlantılar için yapılandırma adımları için bkz. [Azure VPN ağ geçitlerinde BGP kullanmaya başlama](vpn-gateway-bgp-resource-manager-ps.md).</span><span class="sxs-lookup"><span data-stu-id="1ec78-134">See [Getting started with BGP on Azure VPN gateways](vpn-gateway-bgp-resource-manager-ps.md) for steps to configure BGP for your cross-premises and VNet-to-VNet connections.</span></span>

