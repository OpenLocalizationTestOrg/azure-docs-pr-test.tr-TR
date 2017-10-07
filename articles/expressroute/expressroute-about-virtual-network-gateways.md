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
# <a name="about-virtual-network-gateways-for-expressroute"></a>ExpressRoute için sanal ağ geçitleri hakkında
Bir sanal ağ geçidi kullanılan Azure sanal ağlar ve şirket içi konumlara arasında ağ trafiğini toosend. ExpressRoute bağlantısı yapılandırdığınızda oluşturmak ve sanal ağ geçidi ve sanal ağ geçidi bağlantısı yapılandırmanız gerekir.

Bir sanal ağ geçidi kaynağı oluştururken birkaç ayar belirtirsiniz. Gerekli hello ayarlarından birini hello ağ geçidi ExpressRoute veya siteden siteye VPN trafiği için kullanılıp kullanılmayacağını belirtir. Merhaba Resource Manager dağıtım modelinde hello ayardır '-GatewayType'.

Ağ trafiği üzerinde özel bir bağlantı gönderildiğinde hello ağ geçidi türü 'ExpressRoute' kullanın. Bu, başvurulan tooas bir ExpressRoute ağ geçidi de geçerlidir. Ne zaman ağ trafiğini gönderilir arasında şifrelenmiş genel Internet Merhaba, hello ağ geçidi türü 'Vpn' kullanın. Başvurulan tooas bir VPN ağ geçidi budur. Siteden Siteye, Noktadan Siteye ve Sanal Ağdan Sanal Ağa bağlantıların tümü VPN ağ geçidi kullanır.

Bir sanal ağın her ağ geçidi türü için yalnızca bir sanal ağ geçidi olabilir. Örneğin, GatewayType Vpn kullanan bir sanal ağ geçidiniz ve GatewayType ExpressRoute kullanan bir sanal ağ geçidiniz olabilir. Bu makalede hello ExpressRoute sanal ağ geçidinde odaklanır.

## <a name="gwsku"></a>Ağ Geçidi SKU'ları
[!INCLUDE [expressroute-gwsku-include](../../includes/expressroute-gwsku-include.md)]

Tooupgrade, ağ geçidi tooa daha güçlü istiyorsanız, ağ geçidi SKU'su, çoğu durumda, kullanabileceğiniz 'Boyutlandırma-AzureRmVirtualNetworkGateway' PowerShell cmdlet'ini hello. Bu yükseltme tooStandard ve HighPerformance SKU'ları için çalışır. Ancak, tooupgrade toohello UltraPerformance SKU, gerekir toorecreate hello ağ geçidi.

### <a name="aggthroughput"></a>Ağ geçidi SKU'su göre tahmini toplam verimlilik
Merhaba aşağıdaki tabloda hello ağ geçidi türleri ve tahmini toplam verimlilik hello gösterilmektedir. Bu tablo tooboth hello Resource Manager ve klasik dağıtım modellerine uygulanır.

[!INCLUDE [expressroute-table-aggthroughput](../../includes/expressroute-table-aggtput-include.md)]

> [!IMPORTANT]
> Uygulama işlemenizi hello uçtan uca gecikme gibi birden çok etkene bağlıdır ve trafik hello sayısı hello uygulama açılır akar. Hello numaraları hello tablo temsil hello üst sınırı Merhaba uygulaması theorectically için ideal bir ortamda elde edin. 
> 
>

## <a name="resources"></a>REST API ve PowerShell cmdlet'leri
Ek teknik kaynaklar ve REST API'leri ve PowerShell cmdlet'leri için sanal ağ geçidi yapılandırmaları kullanırken belirli sözdizimi gereksinimleri için sayfalar aşağıdaki hello bakın:

| **Klasik** | **Resource Manager** |
| --- | --- |
| [PowerShell](https://msdn.microsoft.com/library/mt270335.aspx) |[PowerShell](https://msdn.microsoft.com/library/mt163510.aspx) |
| [REST API](https://msdn.microsoft.com/library/jj154113.aspx) |[REST API](https://msdn.microsoft.com/library/mt163859.aspx) |

## <a name="next-steps"></a>Sonraki adımlar
Bkz: [ExpressRoute genel bakış](expressroute-introduction.md) kullanılabilir bağlantı yapılandırmaları hakkında daha fazla bilgi için. 

