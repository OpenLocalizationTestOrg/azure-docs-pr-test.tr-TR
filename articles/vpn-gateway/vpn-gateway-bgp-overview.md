---
title: Azure VPN Gateways ile BGP'ye aaaOverview | Microsoft Docs
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
ms.openlocfilehash: ced3f77ecd791c84fb72b96447e839be3bf94846
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-bgp-with-azure-vpn-gateways"></a><span data-ttu-id="2714d-103">Azure VPN Gateways ile BGP’ye genel bakış</span><span class="sxs-lookup"><span data-stu-id="2714d-103">Overview of BGP with Azure VPN Gateways</span></span>
<span data-ttu-id="2714d-104">Bu makale Azure VPN Gateways içindeki BGP (Sınır Ağ Geçidi Protokolü) desteğine genel bakış sağlar.</span><span class="sxs-lookup"><span data-stu-id="2714d-104">This article provides an overview of BGP (Border Gateway Protocol) support in Azure VPN Gateways.</span></span>

<span data-ttu-id="2714d-105">BGP hello Internet tooexchange Yönlendirme ve ulaşılabilirlik bilgilerini iki veya daha fazla ağ arasında yaygın olarak kullanılan hello standart yönlendirme protokolüdür.</span><span class="sxs-lookup"><span data-stu-id="2714d-105">BGP is hello standard routing protocol commonly used in hello Internet tooexchange routing and reachability information between two or more networks.</span></span> <span data-ttu-id="2714d-106">Ne zaman hello Azure sanal ağlar bağlamında kullanıldığında, BGP hello Azure VPN ağ geçitleri ve BGP eşleri olarak adlandırılan, şirket içi VPN cihazlarınızı etkinleştirir veya Komşuları olarak tooexchange "yolları", her iki ağ geçidini hello kullanılabilirliği ve ulaşılabilirliği olanlar için size bildirir Merhaba ağ geçitlerinden veya yönlendiricilerden söz konusu aracılığıyla toogo ekler.</span><span class="sxs-lookup"><span data-stu-id="2714d-106">When used in hello context of Azure Virtual Networks, BGP enables hello Azure VPN Gateways and your on-premises VPN devices, called BGP peers or neighbors, tooexchange "routes" that will inform both gateways on hello availability and reachability for those prefixes toogo through hello gateways or routers involved.</span></span> <span data-ttu-id="2714d-107">BGP, bir BGP eş tooall bir BGP ağ geçidinin öğrendiği yolları yayarak birden fazla ağ arasında geçiş yönlendirme de etkinleştirebilir diğer BGP eşleri.</span><span class="sxs-lookup"><span data-stu-id="2714d-107">BGP can also enable transit routing among multiple networks by propagating routes a BGP gateway learns from one BGP peer tooall other BGP peers.</span></span> 

## <a name="why-use-bgp"></a><span data-ttu-id="2714d-108">BGP neden kullanılır?</span><span class="sxs-lookup"><span data-stu-id="2714d-108">Why use BGP?</span></span>
<span data-ttu-id="2714d-109">BGP, Azure Yol Tabanlı VPN ağ geçitleri ile birlikte kullanabileceğiniz isteğe bağlı bir özelliktir.</span><span class="sxs-lookup"><span data-stu-id="2714d-109">BGP is an optional feature you can use with Azure Route-Based VPN gateways.</span></span> <span data-ttu-id="2714d-110">Merhaba özelliği etkinleştirmeden önce şirket içi VPN cihazlarınızı BGP desteklediğinden emin olmalısınız.</span><span class="sxs-lookup"><span data-stu-id="2714d-110">You should also make sure your on-premises VPN devices support BGP before you enable hello feature.</span></span> <span data-ttu-id="2714d-111">Toouse Azure VPN ağ geçitleri ve şirket içi VPN cihazlarınızı BGP olmadan devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2714d-111">You can continue toouse Azure VPN gateways and your on-premises VPN devices without BGP.</span></span> <span data-ttu-id="2714d-112">Statik yollar (BGP olmadan) kullanarak eşdeğer hello olan *karşılaştırması* dinamik BGP ile ağlarınız ve Azure arasında yönlendirme kullanarak.</span><span class="sxs-lookup"><span data-stu-id="2714d-112">It is hello equivalent of using static routes (without BGP) *vs.* using dynamic routing with BGP between your networks and Azure.</span></span>

<span data-ttu-id="2714d-113">BGP’nin çeşitli avantajları ve yeni özellikleri vardır:</span><span class="sxs-lookup"><span data-stu-id="2714d-113">There are several advantages and new capabilities with BGP:</span></span>

### <a name="support-automatic-and-flexible-prefix-updates"></a><span data-ttu-id="2714d-114">Otomatik ve esnek ön ek güncelleştirmelerini destekler</span><span class="sxs-lookup"><span data-stu-id="2714d-114">Support automatic and flexible prefix updates</span></span>
<span data-ttu-id="2714d-115">BGP ile yalnızca hello IPSec S2S VPN tüneli üzerinden toodeclare minimum önek tooa belirli BGP eşi gerekir.</span><span class="sxs-lookup"><span data-stu-id="2714d-115">With BGP, you only need toodeclare a minimum prefix tooa specific BGP peer over hello IPsec S2S VPN tunnel.</span></span> <span data-ttu-id="2714d-116">Ana bilgisayar önek olarak küçük olabilir (/ 32) hello şirket içi VPN cihazınızın BGP eş IP adresini.</span><span class="sxs-lookup"><span data-stu-id="2714d-116">It can be as small as a host prefix (/32) of hello BGP peer IP address of your on-premises VPN device.</span></span> <span data-ttu-id="2714d-117">Hangi ağ önekleri, Azure Virtual Network tooaccess tooadvertise tooAzure tooallow istediğiniz şirket içi kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2714d-117">You can control which on-premises network prefixes you want tooadvertise tooAzure tooallow your Azure Virtual Network tooaccess.</span></span>

<span data-ttu-id="2714d-118">Ayrıca, büyük özel bir IP adres alanı (örneğin, 10.0.0.0/8) gibi VNet adres ön bazıları içerebilir büyük ön ekler tanıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2714d-118">You can also advertise larger prefixes that may include some of your VNet address prefixes, such as a large private IP address space (for example, 10.0.0.0/8).</span></span> <span data-ttu-id="2714d-119">Hello öneklerini VNet ön herhangi biri ile aynı olamaz olsa unutmayın.</span><span class="sxs-lookup"><span data-stu-id="2714d-119">Note though hello prefixes cannot be identical with any one of your VNet prefixes.</span></span> <span data-ttu-id="2714d-120">Bu yollar aynı tooyour VNet ön reddedilir.</span><span class="sxs-lookup"><span data-stu-id="2714d-120">Those routes identical tooyour VNet prefixes will be rejected.</span></span>

### <a name="support-multiple-tunnels-between-a-vnet-and-an-on-premises-site-with-automatic-failover-based-on-bgp"></a><span data-ttu-id="2714d-121">Bir VNet ile şirket içi site arasında BGP’yi temel alan otomatik yük devretme ile birden fazla tüneli destekler</span><span class="sxs-lookup"><span data-stu-id="2714d-121">Support multiple tunnels between a VNet and an on-premises site with automatic failover based on BGP</span></span>
<span data-ttu-id="2714d-122">Birden fazla Azure VNet ile şirket içi VPN cihazlarınızı arasında hello bağlantı kurabilir aynı konumu.</span><span class="sxs-lookup"><span data-stu-id="2714d-122">You can establish multiple connections between your Azure VNet and your on-premises VPN devices in hello same location.</span></span> <span data-ttu-id="2714d-123">Bu özellik, bir aktif-aktif yapılandırma hello iki ağ arasında birden fazla tünel (yol) sağlar.</span><span class="sxs-lookup"><span data-stu-id="2714d-123">This capability provides multiple tunnels (paths) between hello two networks in an active-active configuration.</span></span> <span data-ttu-id="2714d-124">Merhaba tüneller birini bağlantısı kesilmişse hello karşılık gelen yollar BGP aracılığıyla geri çekilir ve hello trafiği toohello kalan tünellere otomatik olarak geçer.</span><span class="sxs-lookup"><span data-stu-id="2714d-124">If one of hello tunnels is disconnected, hello corresponding routes will be withdrawn via BGP and hello traffic automatically shifts toohello remaining tunnels.</span></span>

<span data-ttu-id="2714d-125">Aşağıdaki diyagramda hello bu yüksek oranda kullanılabilir kurulumun basit bir örneği gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="2714d-125">hello following diagram shows a simple example of this highly available setup:</span></span>

![Birden fazla etkin yol](./media/vpn-gateway-bgp-overview/multiple-active-tunnels.png)

### <a name="support-transit-routing-between-your-on-premises-networks-and-multiple-azure-vnets"></a><span data-ttu-id="2714d-127">Şirket içi ağlarınız ile birden fazla Azure VNet arasında geçiş yönlendirme desteği</span><span class="sxs-lookup"><span data-stu-id="2714d-127">Support transit routing between your on-premises networks and multiple Azure VNets</span></span>
<span data-ttu-id="2714d-128">BGP birden çok ağ geçitleri toolearn sağlar ve doğrudan veya dolaylı olarak bağlı olmasına bakılmaksızın farklı ağlardaki ön ekleri yayar.</span><span class="sxs-lookup"><span data-stu-id="2714d-128">BGP enables multiple gateways toolearn and propagate prefixes from different networks, whether they are directly or indirectly connected.</span></span> <span data-ttu-id="2714d-129">Bu özellik şirket içi siteleriniz arasında veya birden fazla Azure Sanal Ağında Azure VPN ağ geçitleri ile geçiş yönlendirmesi sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="2714d-129">This can enable transit routing with Azure VPN gateways between your on-premises sites or across multiple Azure Virtual Networks.</span></span>

<span data-ttu-id="2714d-130">Merhaba Aşağıdaki diyagramda hello hello Microsoft Networks içindeki Azure VPN ağ geçitleri üzerinden iki şirket içi ağlar arasındaki trafiği geçebilen birden fazla yol ile çoklu atlamalı bir topolojinin örneği gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="2714d-130">hello following diagram shows an example of a multi-hop topology with multiple paths that can transit traffic between hello two on-premises networks through Azure VPN gateways within hello Microsoft Networks:</span></span>

![Çoklu atlamalı geçiş](./media/vpn-gateway-bgp-overview/full-mesh-transit.png)

## <a name="bgp-faq"></a><span data-ttu-id="2714d-132">BGP SSS</span><span class="sxs-lookup"><span data-stu-id="2714d-132">BGP FAQ</span></span>
[!INCLUDE [vpn-gateway-bgp-faq-include](../../includes/vpn-gateway-bpg-faq-include.md)]

## <a name="next-steps"></a><span data-ttu-id="2714d-133">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2714d-133">Next steps</span></span>
<span data-ttu-id="2714d-134">Bkz: [Azure VPN ağ geçitlerinde BGP ile çalışmaya başlama](vpn-gateway-bgp-resource-manager-ps.md) şirketler arası ve VNet-VNet bağlantıları için adımları tooconfigure BGP için.</span><span class="sxs-lookup"><span data-stu-id="2714d-134">See [Getting started with BGP on Azure VPN gateways](vpn-gateway-bgp-resource-manager-ps.md) for steps tooconfigure BGP for your cross-premises and VNet-to-VNet connections.</span></span>

