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
# <a name="working-with-virtual-network-gateway-skus-legacy-skus"></a>Sanal ağ geçidi SKU'ları (eski SKU) ile çalışma

Bu makale hello eski (eski) sanal ağ geçidi SKU'ları hakkında bilgi içerir. Merhaba eski SKU'ları önceden oluşturulmuş VPN ağ geçitleri için her iki dağıtım modeli hala çalışın. Klasik VPN ağ geçitleri devam toouse eski SKU'ları, varolan ağ geçitleri hem yeni bir ağ geçidi hello. Yeni kaynak yöneticisi VPN ağ geçidi oluştururken, hello yeni ağ geçidi SKU'ları kullanın. Yeni SKU hello hakkında bilgi için bkz: [VPN Gateway hakkında](vpn-gateway-about-vpngateways.md).

## <a name="gwsku"></a>Ağ Geçidi SKU'ları

[!INCLUDE [Legacy gateway SKUs](../../includes/vpn-gateway-gwsku-legacy-include.md)]

## <a name="agg"></a>SKU göre tahmini toplam verimlilik

[!INCLUDE [Aggregated throughput by legacy SKU](../../includes/vpn-gateway-table-gwtype-legacy-aggtput-include.md)]

## <a name="config"></a>SKU ve VPN türü tarafından desteklenen yapılandırmalar

[!INCLUDE [Table requirements for old SKUs](../../includes/vpn-gateway-table-requirements-legacy-sku-include.md)]

## <a name="resize"></a>Bir ağ geçidi (ağ geçidi SKU'su değiştirme) yeniden boyutlandırma

Ağ geçidi SKU'su hello içinde yeniden boyutlandırabilirsiniz aynı SKU ailesi. Örneğin, bir standart SKU varsa, tooa HighPerformance SKU yeniden boyutlandırabilirsiniz. VPN boyutlandırılamaz ağ geçitleri arasında eski SKU'ları hello ve hello yeni SKU ailesi. Örneğin, bir standart SKU tooa VpnGw2 SKU gidemezsiniz. 

tooresize hello Klasik dağıtım modeli, komutu aşağıdaki kullanım hello için bir ağ geçidi SKU:

```powershell
Resize-AzureVirtualNetworkGateway -GatewayId <Gateway ID> -GatewaySKU HighPerformance
```

tooresize hello Resource Manager dağıtım modeli için bir ağ geçidi SKU'su hello aşağıdaki komutu kullanın:

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg
Resize-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -GatewaySku HighPerformance
```

## <a name="migrate"></a>Toohello yeni ağ geçidi SKU'ları geçirme

Merhaba Resource Manager dağıtım modeliyle çalışıyorsanız, toohello yeni ağ geçidi SKU'ları geçirebilirsiniz. Merhaba Klasik dağıtım modeliyle çalışıyorsanız, toohello geçiremezsiniz yeni SKU'ları ve bunun yerine toouse devam etmelisiniz eski SKU'ları hello.

[!INCLUDE [Migrate SKU](../../includes/vpn-gateway-migrate-legacy-sku-include.md)]

## <a name="next-steps"></a>Sonraki adımlar

Merhaba yeni ağ geçidi SKU'ları hakkında daha fazla bilgi için bkz: [ağ geçidi SKU'ları](vpn-gateway-about-vpngateways.md#gwsku).

Yapılandırma ayarları hakkında daha fazla bilgi için bkz: [VPN Gateway hakkında yapılandırma ayarlarını](vpn-gateway-about-vpn-gateway-settings.md).