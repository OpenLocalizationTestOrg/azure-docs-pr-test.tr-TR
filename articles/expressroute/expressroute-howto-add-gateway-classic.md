---
title: "PowerShell kullanarak ExpressRoute için bir VNet ağ geçidini yapılandırma: Klasik: Azure | Microsoft Docs"
description: "Klasik dağıtım için bir sanal ağ geçidi yapılandırmak için bir ExpressRoute yapılandırma PowerShell kullanarak VNet model."
documentationcenter: na
services: expressroute
author: charwen
manager: carmonm
editor: 
tags: azure-service-management
ms.assetid: 85ee0bc1-55be-4760-bfb4-34d9f2c96f30
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/21/2017
ms.author: charwen
ms.openlocfilehash: 6f37d4d9cba546b5416ab99040f5ef6dae273380
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-virtual-network-gateway-for-expressroute-using-powershell-classic"></a>Bir sanal ağ geçidi (Klasik) PowerShell kullanarak ExpressRoute için yapılandırma
> [!div class="op_single_selector"]
> * [Resource Manager - PowerShell](expressroute-howto-add-gateway-resource-manager.md)
> * [Klasik - PowerShell](expressroute-howto-add-gateway-classic.md)
> * [Video - Azure portalı](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-vpn-gateway-for-your-virtual-network)
> 
> 

Bu makale size yol gösterir hello adımları tooadd aracılığıyla yeniden boyutlandırma ve önceden var olan bir VNet için bir sanal ağ (VNet) ağ geçidi kaldırın. Merhaba bu yapılandırma için hello kullanılarak oluşturulan özellikle sanal ağlar için adımlardır **Klasik dağıtım modeli** ve, bir expressroute bağlantı yapılandırmasında kullanılabilir. 

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

**Azure dağıtım modelleri hakkında**

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="before-beginning"></a>Başlamadan önce
Bu yapılandırma için gerekli hello Azure PowerShell cmdlet'lerini yüklü olduğunu doğrulayın (1.0.2 veya üzeri). Merhaba cmdlet'leri yüklemediyseniz toodo gerekir hello yapılandırma adımlarına başlamadan önce bunu. Azure PowerShell'i yükleme hakkında daha fazla bilgi için bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview).

[!INCLUDE [expressroute-gateway-classic-ps](../../includes/expressroute-gateway-classic-ps-include.md)]

## <a name="next-steps"></a>Sonraki adımlar
Merhaba VNet ağ geçidini oluşturduktan sonra VNet tooan expressroute bağlantı hattı bağlayabilirsiniz. Bkz: [sanal ağ tooan expressroute bağlantı hattı bağlantı](expressroute-howto-linkvnet-classic.md).

