---
title: "aaaLegacy Azure sanal ağ geçidi SKU'ları | Microsoft Docs"
description: "Eski sanal ağ geçidi SKU'ları ağ."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/01/2017
ms.author: cherylmc
ms.openlocfilehash: 710417581423d2fbc62827cab7949f2e137c5996
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-virtual-network-gateway-skus-legacy-skus"></a><span data-ttu-id="8e7ac-103">Sanal ağ geçidi SKU'ları (eski SKU) ile çalışma</span><span class="sxs-lookup"><span data-stu-id="8e7ac-103">Working with virtual network gateway SKUs (legacy SKUs)</span></span>

<span data-ttu-id="8e7ac-104">Bu makale hello eski (eski) sanal ağ geçidi SKU'ları hakkında bilgi içerir.</span><span class="sxs-lookup"><span data-stu-id="8e7ac-104">This article contains information about hello legacy (old) virtual network gateway SKUs.</span></span> <span data-ttu-id="8e7ac-105">Merhaba eski SKU'ları önceden oluşturulmuş VPN ağ geçitleri için her iki dağıtım modeli hala çalışın.</span><span class="sxs-lookup"><span data-stu-id="8e7ac-105">hello legacy SKUs still work in both deployment models for VPN gateways that have already been created.</span></span> <span data-ttu-id="8e7ac-106">Klasik VPN ağ geçitleri devam toouse eski SKU'ları, varolan ağ geçitleri hem yeni bir ağ geçidi hello.</span><span class="sxs-lookup"><span data-stu-id="8e7ac-106">Classic VPN gateways continue toouse hello legacy SKUs, both for existing gateways, and for new gateways.</span></span> <span data-ttu-id="8e7ac-107">Yeni kaynak yöneticisi VPN ağ geçidi oluştururken, hello yeni ağ geçidi SKU'ları kullanın.</span><span class="sxs-lookup"><span data-stu-id="8e7ac-107">When creating new Resource Manager VPN gateways, use hello new gateway SKUs.</span></span> <span data-ttu-id="8e7ac-108">Yeni SKU hello hakkında bilgi için bkz: [VPN Gateway hakkında](vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="8e7ac-108">For information about hello new SKUs, see [About VPN Gateway](vpn-gateway-about-vpngateways.md).</span></span>

## <span data-ttu-id="8e7ac-109"><a name="gwsku"></a>Ağ Geçidi SKU'ları</span><span class="sxs-lookup"><span data-stu-id="8e7ac-109"><a name="gwsku"></a>Gateway SKUs</span></span>

[!INCLUDE [Legacy gateway SKUs](../../includes/vpn-gateway-gwsku-legacy-include.md)]

## <span data-ttu-id="8e7ac-110"><a name="agg"></a>SKU göre tahmini toplam verimlilik</span><span class="sxs-lookup"><span data-stu-id="8e7ac-110"><a name="agg"></a>Estimated aggregate throughput by SKU</span></span>

[!INCLUDE [Aggregated throughput by legacy SKU](../../includes/vpn-gateway-table-gwtype-legacy-aggtput-include.md)]

## <span data-ttu-id="8e7ac-111"><a name="config"></a>SKU ve VPN türü tarafından desteklenen yapılandırmalar</span><span class="sxs-lookup"><span data-stu-id="8e7ac-111"><a name="config"></a>Supported configurations by SKU and VPN type</span></span>

[!INCLUDE [Table requirements for old SKUs](../../includes/vpn-gateway-table-requirements-legacy-sku-include.md)]

## <span data-ttu-id="8e7ac-112"><a name="resize"></a>Bir ağ geçidi (ağ geçidi SKU'su değiştirme) yeniden boyutlandırma</span><span class="sxs-lookup"><span data-stu-id="8e7ac-112"><a name="resize"></a>Resize a gateway (change a gateway SKU)</span></span>

<span data-ttu-id="8e7ac-113">Ağ geçidi SKU'su hello içinde yeniden boyutlandırabilirsiniz aynı SKU ailesi.</span><span class="sxs-lookup"><span data-stu-id="8e7ac-113">You can resize a gateway SKU within hello same SKU family.</span></span> <span data-ttu-id="8e7ac-114">Örneğin, bir standart SKU varsa, tooa HighPerformance SKU yeniden boyutlandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8e7ac-114">For example, if you have a Standard SKU, you can resize tooa HighPerformance SKU.</span></span> <span data-ttu-id="8e7ac-115">VPN boyutlandırılamaz ağ geçitleri arasında eski SKU'ları hello ve hello yeni SKU ailesi.</span><span class="sxs-lookup"><span data-stu-id="8e7ac-115">You can't resize your VPN gateways between hello old SKUs and hello new SKU families.</span></span> <span data-ttu-id="8e7ac-116">Örneğin, bir standart SKU tooa VpnGw2 SKU gidemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="8e7ac-116">For example, you can't go from a Standard SKU tooa VpnGw2 SKU.</span></span> 

<span data-ttu-id="8e7ac-117">tooresize hello Klasik dağıtım modeli, komutu aşağıdaki kullanım hello için bir ağ geçidi SKU:</span><span class="sxs-lookup"><span data-stu-id="8e7ac-117">tooresize a gateway SKU for hello classic deployment model, use hello following command:</span></span>

```powershell
Resize-AzureVirtualNetworkGateway -GatewayId <Gateway ID> -GatewaySKU HighPerformance
```

<span data-ttu-id="8e7ac-118">tooresize hello Resource Manager dağıtım modeli için bir ağ geçidi SKU'su hello aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="8e7ac-118">tooresize a gateway SKU for hello Resource Manager deployment model, use hello following command:</span></span>

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg
Resize-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -GatewaySku HighPerformance
```

## <span data-ttu-id="8e7ac-119"><a name="migrate"></a>Toohello yeni ağ geçidi SKU'ları geçirme</span><span class="sxs-lookup"><span data-stu-id="8e7ac-119"><a name="migrate"></a>Migrate toohello new gateway SKUs</span></span>

<span data-ttu-id="8e7ac-120">Merhaba Resource Manager dağıtım modeliyle çalışıyorsanız, toohello yeni ağ geçidi SKU'ları geçirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8e7ac-120">If you are working with hello Resource Manager deployment model, you can migrate toohello new gateway SKUS.</span></span> <span data-ttu-id="8e7ac-121">Merhaba Klasik dağıtım modeliyle çalışıyorsanız, toohello geçiremezsiniz yeni SKU'ları ve bunun yerine toouse devam etmelisiniz eski SKU'ları hello.</span><span class="sxs-lookup"><span data-stu-id="8e7ac-121">If you are working with hello classic deployment model, you can't migrate toohello new SKUs and must instead continue toouse hello legacy SKUs.</span></span>

[!INCLUDE [Migrate SKU](../../includes/vpn-gateway-migrate-legacy-sku-include.md)]

## <a name="next-steps"></a><span data-ttu-id="8e7ac-122">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8e7ac-122">Next steps</span></span>

<span data-ttu-id="8e7ac-123">Merhaba yeni ağ geçidi SKU'ları hakkında daha fazla bilgi için bkz: [ağ geçidi SKU'ları](vpn-gateway-about-vpngateways.md#gwsku).</span><span class="sxs-lookup"><span data-stu-id="8e7ac-123">For more information about hello new Gateway SKUs, see [Gateway SKUs](vpn-gateway-about-vpngateways.md#gwsku).</span></span>

<span data-ttu-id="8e7ac-124">Yapılandırma ayarları hakkında daha fazla bilgi için bkz: [VPN Gateway hakkında yapılandırma ayarlarını](vpn-gateway-about-vpn-gateway-settings.md).</span><span class="sxs-lookup"><span data-stu-id="8e7ac-124">For more information about configuration settings, see [About VPN Gateway configuration settings](vpn-gateway-about-vpn-gateway-settings.md).</span></span>