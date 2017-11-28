---
title: "aaaAbout ExpressRoute sanal ağ geçitlerini | Microsoft Docs"
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
ms.openlocfilehash: 4daf4f96b4fadb00683d8e536e51734853008c50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="about-virtual-network-gateways-for-expressroute"></a><span data-ttu-id="ea0b1-103">ExpressRoute için sanal ağ geçitleri hakkında</span><span class="sxs-lookup"><span data-stu-id="ea0b1-103">About virtual network gateways for ExpressRoute</span></span>
<span data-ttu-id="ea0b1-104">Bir sanal ağ geçidi kullanılan Azure sanal ağlar ve şirket içi konumlara arasında ağ trafiğini toosend.</span><span class="sxs-lookup"><span data-stu-id="ea0b1-104">A virtual network gateway is used toosend network traffic between Azure virtual networks and on-premises locations.</span></span> <span data-ttu-id="ea0b1-105">ExpressRoute bağlantısı yapılandırdığınızda oluşturmak ve sanal ağ geçidi ve sanal ağ geçidi bağlantısı yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ea0b1-105">When you configure an ExpressRoute connection, you must create and configure a virtual network gateway and a virtual network gateway connection.</span></span>

<span data-ttu-id="ea0b1-106">Bir sanal ağ geçidi kaynağı oluştururken birkaç ayar belirtirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ea0b1-106">When you create a virtual network gateway, you specify several settings.</span></span> <span data-ttu-id="ea0b1-107">Gerekli hello ayarlarından birini hello ağ geçidi ExpressRoute veya siteden siteye VPN trafiği için kullanılıp kullanılmayacağını belirtir.</span><span class="sxs-lookup"><span data-stu-id="ea0b1-107">One of hello required settings specifies whether hello gateway will be used for ExpressRoute or Site-to-Site VPN traffic.</span></span> <span data-ttu-id="ea0b1-108">Merhaba Resource Manager dağıtım modelinde hello ayardır '-GatewayType'.</span><span class="sxs-lookup"><span data-stu-id="ea0b1-108">In hello Resource Manager deployment model, hello setting is '-GatewayType'.</span></span>

<span data-ttu-id="ea0b1-109">Ağ trafiği üzerinde özel bir bağlantı gönderildiğinde hello ağ geçidi türü 'ExpressRoute' kullanın.</span><span class="sxs-lookup"><span data-stu-id="ea0b1-109">When network traffic is sent on a private connection, you use hello gateway type 'ExpressRoute'.</span></span> <span data-ttu-id="ea0b1-110">Bu, başvurulan tooas bir ExpressRoute ağ geçidi de geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="ea0b1-110">This is also referred tooas an ExpressRoute gateway.</span></span> <span data-ttu-id="ea0b1-111">Ne zaman ağ trafiğini gönderilir arasında şifrelenmiş genel Internet Merhaba, hello ağ geçidi türü 'Vpn' kullanın.</span><span class="sxs-lookup"><span data-stu-id="ea0b1-111">When network traffic is sent encrypted across hello public Internet, you use hello gateway type 'Vpn'.</span></span> <span data-ttu-id="ea0b1-112">Başvurulan tooas bir VPN ağ geçidi budur.</span><span class="sxs-lookup"><span data-stu-id="ea0b1-112">This is referred tooas a VPN gateway.</span></span> <span data-ttu-id="ea0b1-113">Siteden Siteye, Noktadan Siteye ve Sanal Ağdan Sanal Ağa bağlantıların tümü VPN ağ geçidi kullanır.</span><span class="sxs-lookup"><span data-stu-id="ea0b1-113">Site-to-Site, Point-to-Site, and VNet-to-VNet connections all use a VPN gateway.</span></span>

<span data-ttu-id="ea0b1-114">Bir sanal ağın her ağ geçidi türü için yalnızca bir sanal ağ geçidi olabilir.</span><span class="sxs-lookup"><span data-stu-id="ea0b1-114">Each virtual network can have only one virtual network gateway per gateway type.</span></span> <span data-ttu-id="ea0b1-115">Örneğin, GatewayType Vpn kullanan bir sanal ağ geçidiniz ve GatewayType ExpressRoute kullanan bir sanal ağ geçidiniz olabilir.</span><span class="sxs-lookup"><span data-stu-id="ea0b1-115">For example, you can have one virtual network gateway that uses -GatewayType Vpn, and one that uses -GatewayType ExpressRoute.</span></span> <span data-ttu-id="ea0b1-116">Bu makalede hello ExpressRoute sanal ağ geçidinde odaklanır.</span><span class="sxs-lookup"><span data-stu-id="ea0b1-116">This article focuses on hello ExpressRoute virtual network gateway.</span></span>

## <span data-ttu-id="ea0b1-117"><a name="gwsku"></a>Ağ Geçidi SKU'ları</span><span class="sxs-lookup"><span data-stu-id="ea0b1-117"><a name="gwsku"></a>Gateway SKUs</span></span>
[!INCLUDE [expressroute-gwsku-include](../../includes/expressroute-gwsku-include.md)]

<span data-ttu-id="ea0b1-118">Tooupgrade, ağ geçidi tooa daha güçlü istiyorsanız, ağ geçidi SKU'su, çoğu durumda, kullanabileceğiniz 'Boyutlandırma-AzureRmVirtualNetworkGateway' PowerShell cmdlet'ini hello.</span><span class="sxs-lookup"><span data-stu-id="ea0b1-118">If you want tooupgrade your gateway tooa more powerful gateway SKU, in most cases you can use hello 'Resize-AzureRmVirtualNetworkGateway' PowerShell cmdlet.</span></span> <span data-ttu-id="ea0b1-119">Bu yükseltme tooStandard ve HighPerformance SKU'ları için çalışır.</span><span class="sxs-lookup"><span data-stu-id="ea0b1-119">This will work for upgrades tooStandard and HighPerformance SKUs.</span></span> <span data-ttu-id="ea0b1-120">Ancak, tooupgrade toohello UltraPerformance SKU, gerekir toorecreate hello ağ geçidi.</span><span class="sxs-lookup"><span data-stu-id="ea0b1-120">However, tooupgrade toohello UltraPerformance SKU, you will need toorecreate hello gateway.</span></span>

### <span data-ttu-id="ea0b1-121"><a name="aggthroughput"></a>Ağ geçidi SKU'su göre tahmini toplam verimlilik</span><span class="sxs-lookup"><span data-stu-id="ea0b1-121"><a name="aggthroughput"></a>Estimated aggregate throughput by gateway SKU</span></span>
<span data-ttu-id="ea0b1-122">Merhaba aşağıdaki tabloda hello ağ geçidi türleri ve tahmini toplam verimlilik hello gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="ea0b1-122">hello following table shows hello gateway types and hello estimated aggregate throughput.</span></span> <span data-ttu-id="ea0b1-123">Bu tablo tooboth hello Resource Manager ve klasik dağıtım modellerine uygulanır.</span><span class="sxs-lookup"><span data-stu-id="ea0b1-123">This table applies tooboth hello Resource Manager and classic deployment models.</span></span>

[!INCLUDE [expressroute-table-aggthroughput](../../includes/expressroute-table-aggtput-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="ea0b1-124">Uygulama işlemenizi hello uçtan uca gecikme gibi birden çok etkene bağlıdır ve trafik hello sayısı hello uygulama açılır akar.</span><span class="sxs-lookup"><span data-stu-id="ea0b1-124">Application throughput depends on multiple factors, such as hello end-to-end latency, and hello number of traffic flows hello application opens.</span></span> <span data-ttu-id="ea0b1-125">Hello numaraları hello tablo temsil hello üst sınırı Merhaba uygulaması theorectically için ideal bir ortamda elde edin.</span><span class="sxs-lookup"><span data-stu-id="ea0b1-125">hello numbers in hello table represent hello upper limit that hello application can theorectically achieve in an ideal environment.</span></span> 
> 
>

## <span data-ttu-id="ea0b1-126"><a name="resources"></a>REST API ve PowerShell cmdlet'leri</span><span class="sxs-lookup"><span data-stu-id="ea0b1-126"><a name="resources"></a>REST APIs and PowerShell cmdlets</span></span>
<span data-ttu-id="ea0b1-127">Ek teknik kaynaklar ve REST API'leri ve PowerShell cmdlet'leri için sanal ağ geçidi yapılandırmaları kullanırken belirli sözdizimi gereksinimleri için sayfalar aşağıdaki hello bakın:</span><span class="sxs-lookup"><span data-stu-id="ea0b1-127">For additional technical resources and specific syntax requirements when using REST APIs and PowerShell cmdlets for virtual network gateway configurations, see hello following pages:</span></span>

| <span data-ttu-id="ea0b1-128">**Klasik**</span><span class="sxs-lookup"><span data-stu-id="ea0b1-128">**Classic**</span></span> | <span data-ttu-id="ea0b1-129">**Resource Manager**</span><span class="sxs-lookup"><span data-stu-id="ea0b1-129">**Resource Manager**</span></span> |
| --- | --- |
| [<span data-ttu-id="ea0b1-130">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ea0b1-130">PowerShell</span></span>](https://msdn.microsoft.com/library/mt270335.aspx) |[<span data-ttu-id="ea0b1-131">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ea0b1-131">PowerShell</span></span>](https://msdn.microsoft.com/library/mt163510.aspx) |
| [<span data-ttu-id="ea0b1-132">REST API</span><span class="sxs-lookup"><span data-stu-id="ea0b1-132">REST API</span></span>](https://msdn.microsoft.com/library/jj154113.aspx) |[<span data-ttu-id="ea0b1-133">REST API</span><span class="sxs-lookup"><span data-stu-id="ea0b1-133">REST API</span></span>](https://msdn.microsoft.com/library/mt163859.aspx) |

## <a name="next-steps"></a><span data-ttu-id="ea0b1-134">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ea0b1-134">Next steps</span></span>
<span data-ttu-id="ea0b1-135">Bkz: [ExpressRoute genel bakış](expressroute-introduction.md) kullanılabilir bağlantı yapılandırmaları hakkında daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="ea0b1-135">See [ExpressRoute Overview](expressroute-introduction.md) for more information about available connection configurations.</span></span> 

