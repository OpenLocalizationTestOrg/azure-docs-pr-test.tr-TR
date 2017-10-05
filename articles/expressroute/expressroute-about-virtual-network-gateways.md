---
title: "ExpressRoute sanal ağ geçitleri hakkında | Microsoft Docs"
description: "ExpressRoute için sanal ağ geçitleri hakkında bilgi edinin."
services: expressroute
documentationcenter: na
author: cherylmc
manager: carmonm
editor: 
tags: azure-resource-manager, azure-service-management
ms.assetid: 7e0d9658-bc00-45b0-848f-f7a6da648635
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/05/2017
ms.author: cherylmc
ms.openlocfilehash: a6363fa380d0bab05d7500141cc6019d1d3f68b8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="about-virtual-network-gateways-for-expressroute"></a><span data-ttu-id="34af2-103">ExpressRoute için sanal ağ geçitleri hakkında</span><span class="sxs-lookup"><span data-stu-id="34af2-103">About virtual network gateways for ExpressRoute</span></span>
<span data-ttu-id="34af2-104">Bir sanal ağ geçidi Azure sanal ağlar arasında ağ trafiğini göndermek için kullanılır ve şirket içi konumlara.</span><span class="sxs-lookup"><span data-stu-id="34af2-104">A virtual network gateway is used to send network traffic between Azure virtual networks and on-premises locations.</span></span> <span data-ttu-id="34af2-105">ExpressRoute bağlantısı yapılandırdığınızda oluşturmak ve sanal ağ geçidi ve sanal ağ geçidi bağlantısı yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="34af2-105">When you configure an ExpressRoute connection, you must create and configure a virtual network gateway and a virtual network gateway connection.</span></span>

<span data-ttu-id="34af2-106">Bir sanal ağ geçidi kaynağı oluştururken birkaç ayar belirtirsiniz.</span><span class="sxs-lookup"><span data-stu-id="34af2-106">When you create a virtual network gateway, you specify several settings.</span></span> <span data-ttu-id="34af2-107">Gerekli ayarları birini ağ geçidini ExpressRoute veya siteden siteye VPN trafiği için kullanılıp kullanılmayacağını belirtir.</span><span class="sxs-lookup"><span data-stu-id="34af2-107">One of the required settings specifies whether the gateway will be used for ExpressRoute or Site-to-Site VPN traffic.</span></span> <span data-ttu-id="34af2-108">Resource Manager dağıtım modelinde ayardır '-GatewayType'.</span><span class="sxs-lookup"><span data-stu-id="34af2-108">In the Resource Manager deployment model, the setting is '-GatewayType'.</span></span>

<span data-ttu-id="34af2-109">Ağ trafiği üzerinde özel bir bağlantı gönderilir, ağ geçidi türü 'ExpressRoute' kullanın.</span><span class="sxs-lookup"><span data-stu-id="34af2-109">When network traffic is sent on a private connection, you use the gateway type 'ExpressRoute'.</span></span> <span data-ttu-id="34af2-110">Bu seçenek ExpressRoute ağ geçidi olarak da adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="34af2-110">This is also referred to as an ExpressRoute gateway.</span></span> <span data-ttu-id="34af2-111">Ağ trafiği genel Internet üzerinden şifrelenmiş olarak gönderildiğinde 'Vpn' ağ geçidi türünü kullanın.</span><span class="sxs-lookup"><span data-stu-id="34af2-111">When network traffic is sent encrypted across the public Internet, you use the gateway type 'Vpn'.</span></span> <span data-ttu-id="34af2-112">Bu seçenek VPN ağ geçidi olarak adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="34af2-112">This is referred to as a VPN gateway.</span></span> <span data-ttu-id="34af2-113">Siteden Siteye, Noktadan Siteye ve Sanal Ağdan Sanal Ağa bağlantıların tümü VPN ağ geçidi kullanır.</span><span class="sxs-lookup"><span data-stu-id="34af2-113">Site-to-Site, Point-to-Site, and VNet-to-VNet connections all use a VPN gateway.</span></span>

<span data-ttu-id="34af2-114">Bir sanal ağın her ağ geçidi türü için yalnızca bir sanal ağ geçidi olabilir.</span><span class="sxs-lookup"><span data-stu-id="34af2-114">Each virtual network can have only one virtual network gateway per gateway type.</span></span> <span data-ttu-id="34af2-115">Örneğin, GatewayType Vpn kullanan bir sanal ağ geçidiniz ve GatewayType ExpressRoute kullanan bir sanal ağ geçidiniz olabilir.</span><span class="sxs-lookup"><span data-stu-id="34af2-115">For example, you can have one virtual network gateway that uses -GatewayType Vpn, and one that uses -GatewayType ExpressRoute.</span></span> <span data-ttu-id="34af2-116">Bu makalede ExpressRoute sanal ağ geçidinde odaklanır.</span><span class="sxs-lookup"><span data-stu-id="34af2-116">This article focuses on the ExpressRoute virtual network gateway.</span></span>

## <span data-ttu-id="34af2-117"><a name="gwsku"></a>Ağ Geçidi SKU'ları</span><span class="sxs-lookup"><span data-stu-id="34af2-117"><a name="gwsku"></a>Gateway SKUs</span></span>
[!INCLUDE [expressroute-gwsku-include](../../includes/expressroute-gwsku-include.md)]

<span data-ttu-id="34af2-118">Ağ geçidi uygulamanızı daha güçlü bir ağ geçidi SKU'su yükseltmek istiyorsanız, çoğu durumda, 'Yeniden boyutlandırma-AzureRmVirtualNetworkGateway' PowerShell cmdlet'ini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="34af2-118">If you want to upgrade your gateway to a more powerful gateway SKU, in most cases you can use the 'Resize-AzureRmVirtualNetworkGateway' PowerShell cmdlet.</span></span> <span data-ttu-id="34af2-119">Bu, standart ve HighPerformance SKU'ları yükseltmeleri için çalışır.</span><span class="sxs-lookup"><span data-stu-id="34af2-119">This will work for upgrades to Standard and HighPerformance SKUs.</span></span> <span data-ttu-id="34af2-120">Ancak, UltraPerformance SKU'ya yükseltmek için ağ geçidi yeniden oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="34af2-120">However, to upgrade to the UltraPerformance SKU, you will need to recreate the gateway.</span></span>

### <span data-ttu-id="34af2-121"><a name="aggthroughput"></a>Ağ geçidi SKU'su göre tahmini toplam verimlilik</span><span class="sxs-lookup"><span data-stu-id="34af2-121"><a name="aggthroughput"></a>Estimated aggregate throughput by gateway SKU</span></span>
<span data-ttu-id="34af2-122">Aşağıdaki tabloda ağ geçidi türleri ve tahmini toplam verimlilik gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="34af2-122">The following table shows the gateway types and the estimated aggregate throughput.</span></span> <span data-ttu-id="34af2-123">Bu tablo hem Resource Manager, hem de klasik dağıtım modellerine uygulanır.</span><span class="sxs-lookup"><span data-stu-id="34af2-123">This table applies to both the Resource Manager and classic deployment models.</span></span>

[!INCLUDE [expressroute-table-aggthroughput](../../includes/expressroute-table-aggtput-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="34af2-124">Uygulama işlemenizi uçtan uca gecikme süresi ve uygulama açılır trafik akışlarının sayısı gibi birden çok etkene bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="34af2-124">Application throughput depends on multiple factors, such as the end-to-end latency, and the number of traffic flows the application opens.</span></span> <span data-ttu-id="34af2-125">Tabloda yer alan numaralarını uygulama can theorectically elde ideal bir ortamda üst sınırı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="34af2-125">The numbers in the table represent the upper limit that the application can theorectically achieve in an ideal environment.</span></span> 
> 
>

## <span data-ttu-id="34af2-126"><a name="resources"></a>REST API ve PowerShell cmdlet'leri</span><span class="sxs-lookup"><span data-stu-id="34af2-126"><a name="resources"></a>REST APIs and PowerShell cmdlets</span></span>
<span data-ttu-id="34af2-127">Ek teknik kaynaklar ve REST API'leri ve PowerShell cmdlet'leri için sanal ağ geçidi yapılandırmaları kullanırken belirli sözdizimi gereksinimleri için aşağıdaki sayfalarına bakın:</span><span class="sxs-lookup"><span data-stu-id="34af2-127">For additional technical resources and specific syntax requirements when using REST APIs and PowerShell cmdlets for virtual network gateway configurations, see the following pages:</span></span>

| <span data-ttu-id="34af2-128">**Klasik**</span><span class="sxs-lookup"><span data-stu-id="34af2-128">**Classic**</span></span> | <span data-ttu-id="34af2-129">**Resource Manager**</span><span class="sxs-lookup"><span data-stu-id="34af2-129">**Resource Manager**</span></span> |
| --- | --- |
| [<span data-ttu-id="34af2-130">PowerShell</span><span class="sxs-lookup"><span data-stu-id="34af2-130">PowerShell</span></span>](https://msdn.microsoft.com/library/mt270335.aspx) |[<span data-ttu-id="34af2-131">PowerShell</span><span class="sxs-lookup"><span data-stu-id="34af2-131">PowerShell</span></span>](https://msdn.microsoft.com/library/mt163510.aspx) |
| [<span data-ttu-id="34af2-132">REST API</span><span class="sxs-lookup"><span data-stu-id="34af2-132">REST API</span></span>](https://msdn.microsoft.com/library/jj154113.aspx) |[<span data-ttu-id="34af2-133">REST API</span><span class="sxs-lookup"><span data-stu-id="34af2-133">REST API</span></span>](https://msdn.microsoft.com/library/mt163859.aspx) |

## <a name="next-steps"></a><span data-ttu-id="34af2-134">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="34af2-134">Next steps</span></span>
<span data-ttu-id="34af2-135">Bkz: [ExpressRoute genel bakış](expressroute-introduction.md) kullanılabilir bağlantı yapılandırmaları hakkında daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="34af2-135">See [ExpressRoute Overview](expressroute-introduction.md) for more information about available connection configurations.</span></span> 

