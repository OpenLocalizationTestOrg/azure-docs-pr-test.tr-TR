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
# <a name="configure-a-virtual-network-gateway-for-expressroute-using-powershell"></a><span data-ttu-id="d0310-103">PowerShell kullanarak ExpressRoute için sanal ağ geçidi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="d0310-103">Configure a virtual network gateway for ExpressRoute using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d0310-104">Resource Manager - Azure portalı</span><span class="sxs-lookup"><span data-stu-id="d0310-104">Resource Manager - Azure portal</span></span>](expressroute-howto-add-gateway-portal-resource-manager.md)
> * [<span data-ttu-id="d0310-105">Resource Manager - PowerShell</span><span class="sxs-lookup"><span data-stu-id="d0310-105">Resource Manager - PowerShell</span></span>](expressroute-howto-add-gateway-resource-manager.md)
> * [<span data-ttu-id="d0310-106">Klasik - PowerShell</span><span class="sxs-lookup"><span data-stu-id="d0310-106">Classic - PowerShell</span></span>](expressroute-howto-add-gateway-classic.md)
> * [<span data-ttu-id="d0310-107">Video - Azure portalı</span><span class="sxs-lookup"><span data-stu-id="d0310-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-vpn-gateway-for-your-virtual-network)
> 
> 

<span data-ttu-id="d0310-108">Bu makalede hello adımları tooadd anlatılmaktadır, yeniden boyutlandırma ve önceden var olan bir VNet için bir sanal ağ (VNet) ağ geçidi kaldırın.</span><span class="sxs-lookup"><span data-stu-id="d0310-108">This article walks you through hello steps tooadd, resize, and remove a virtual network (VNet) gateway for a pre-existing VNet.</span></span> <span data-ttu-id="d0310-109">Merhaba bu yapılandırma için özellikle bir expressroute bağlantı yapılandırmasında kullanılacak hello Resource Manager dağıtım modeli kullanılarak oluşturulan sanal ağlar için adımlardır.</span><span class="sxs-lookup"><span data-stu-id="d0310-109">hello steps for this configuration are specifically for VNets that were created using hello Resource Manager deployment model that will be used in an ExpressRoute configuration.</span></span> <span data-ttu-id="d0310-110">Sanal ağ geçitleri ve ExpressRoute ağ geçidi yapılandırma ayarları hakkında daha fazla bilgi için bkz: [ExpressRoute için sanal ağ geçitleri hakkında](expressroute-about-virtual-network-gateways.md).</span><span class="sxs-lookup"><span data-stu-id="d0310-110">For more information about virtual network gateways and gateway configuration settings for ExpressRoute, see [About virtual network gateways for ExpressRoute](expressroute-about-virtual-network-gateways.md).</span></span> 


## <a name="before-beginning"></a><span data-ttu-id="d0310-111">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="d0310-111">Before beginning</span></span>
<span data-ttu-id="d0310-112">Merhaba en son Azure PowerShell cmdlet'lerini yüklü olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="d0310-112">Verify that you have installed hello latest Azure PowerShell cmdlets.</span></span> <span data-ttu-id="d0310-113">Merhaba son cmdlet'leri yüklemediyseniz toodo gereksinim hello yapılandırma adımlarına başlamadan önce bunu.</span><span class="sxs-lookup"><span data-stu-id="d0310-113">If you haven't installed hello latest cmdlets, you need toodo so before beginning hello configuration steps.</span></span> <span data-ttu-id="d0310-114">Daha fazla bilgi için bkz. [Azure PowerShell’i yükleme ve yapılandırma](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d0310-114">For more information, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

[!INCLUDE [expressroute-gateway-rm-ps](../../includes/expressroute-gateway-rm-ps-include.md)]

## <a name="next-steps"></a><span data-ttu-id="d0310-115">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d0310-115">Next steps</span></span>
<span data-ttu-id="d0310-116">Merhaba VNet ağ geçidini oluşturduktan sonra VNet tooan expressroute bağlantı hattı bağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d0310-116">After you have created hello VNet gateway, you can link your VNet tooan ExpressRoute circuit.</span></span> <span data-ttu-id="d0310-117">Bkz: [sanal ağ tooan expressroute bağlantı hattı bağlantı](expressroute-howto-linkvnet-arm.md).</span><span class="sxs-lookup"><span data-stu-id="d0310-117">See [Link a Virtual Network tooan ExpressRoute circuit](expressroute-howto-linkvnet-arm.md).</span></span>

