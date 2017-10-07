---
title: "ExpressRoute için bir sanal ağ geçidi tooa VNet ekleyin: PowerShell: Azure | Microsoft Docs"
description: "Bu makalede Resource Manager Vnet'i ExpressRoute için önceden oluşturulmuş bir sanal ağ geçidi tooan eklerken size yol gösterilir."
documentationcenter: na
services: expressroute
author: charwen
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 63e0bd60-abad-4963-8e27-3aa973e0d968
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/17/2017
ms.author: charwen
ms.openlocfilehash: 8983430b426ad7c4af766294fa16427c5e9df5c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-virtual-network-gateway-for-expressroute-using-powershell"></a>PowerShell kullanarak ExpressRoute için sanal ağ geçidi yapılandırma
> [!div class="op_single_selector"]
> * [Resource Manager - Azure portalı](expressroute-howto-add-gateway-portal-resource-manager.md)
> * [Resource Manager - PowerShell](expressroute-howto-add-gateway-resource-manager.md)
> * [Klasik - PowerShell](expressroute-howto-add-gateway-classic.md)
> * [Video - Azure portalı](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-vpn-gateway-for-your-virtual-network)
> 
> 

Bu makalede hello adımları tooadd anlatılmaktadır, yeniden boyutlandırma ve önceden var olan bir VNet için bir sanal ağ (VNet) ağ geçidi kaldırın. Merhaba bu yapılandırma için özellikle bir expressroute bağlantı yapılandırmasında kullanılacak hello Resource Manager dağıtım modeli kullanılarak oluşturulan sanal ağlar için adımlardır. Sanal ağ geçitleri ve ExpressRoute ağ geçidi yapılandırma ayarları hakkında daha fazla bilgi için bkz: [ExpressRoute için sanal ağ geçitleri hakkında](expressroute-about-virtual-network-gateways.md). 


## <a name="before-beginning"></a>Başlamadan önce
Merhaba en son Azure PowerShell cmdlet'lerini yüklü olduğunu doğrulayın. Merhaba son cmdlet'leri yüklemediyseniz toodo gereksinim hello yapılandırma adımlarına başlamadan önce bunu. Daha fazla bilgi için bkz. [Azure PowerShell’i yükleme ve yapılandırma](/powershell/azure/overview).

[!INCLUDE [expressroute-gateway-rm-ps](../../includes/expressroute-gateway-rm-ps-include.md)]

## <a name="next-steps"></a>Sonraki adımlar
Merhaba VNet ağ geçidini oluşturduktan sonra VNet tooan expressroute bağlantı hattı bağlayabilirsiniz. Bkz: [sanal ağ tooan expressroute bağlantı hattı bağlantı](expressroute-howto-linkvnet-arm.md).

