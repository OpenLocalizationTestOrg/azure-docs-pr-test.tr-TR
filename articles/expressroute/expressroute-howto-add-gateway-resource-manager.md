---
title: "ExpressRoute için bir sanal ağa bir sanal ağ geçidi eklemek: PowerShell: Azure | Microsoft Docs"
description: "Bu makalede önceden oluşturulmuş bir Resource Manager Vnet'i ExpressRoute için sanal ağ geçidine eklerken size yol gösterilir."
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
ms.openlocfilehash: 3aeddd03e0be548933775164ae790ba208fc13ae
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-a-virtual-network-gateway-for-expressroute-using-powershell"></a><span data-ttu-id="095bc-103">PowerShell kullanarak ExpressRoute için sanal ağ geçidi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="095bc-103">Configure a virtual network gateway for ExpressRoute using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="095bc-104">Resource Manager - Azure portalı</span><span class="sxs-lookup"><span data-stu-id="095bc-104">Resource Manager - Azure portal</span></span>](expressroute-howto-add-gateway-portal-resource-manager.md)
> * [<span data-ttu-id="095bc-105">Resource Manager - PowerShell</span><span class="sxs-lookup"><span data-stu-id="095bc-105">Resource Manager - PowerShell</span></span>](expressroute-howto-add-gateway-resource-manager.md)
> * [<span data-ttu-id="095bc-106">Klasik - PowerShell</span><span class="sxs-lookup"><span data-stu-id="095bc-106">Classic - PowerShell</span></span>](expressroute-howto-add-gateway-classic.md)
> * [<span data-ttu-id="095bc-107">Video - Azure portalı</span><span class="sxs-lookup"><span data-stu-id="095bc-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-vpn-gateway-for-your-virtual-network)
> 
> 

<span data-ttu-id="095bc-108">Bu makalede, eklemek, yeniden boyutlandırma ve önceden var olan bir VNet için bir sanal ağ (VNet) ağ geçidini kaldırmak için adım adım anlatılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="095bc-108">This article walks you through the steps to add, resize, and remove a virtual network (VNet) gateway for a pre-existing VNet.</span></span> <span data-ttu-id="095bc-109">Bu yapılandırma için özellikle bir expressroute bağlantı yapılandırmasında kullanılacak Resource Manager dağıtım modeli kullanılarak oluşturulan sanal ağlar için adımlardır.</span><span class="sxs-lookup"><span data-stu-id="095bc-109">The steps for this configuration are specifically for VNets that were created using the Resource Manager deployment model that will be used in an ExpressRoute configuration.</span></span> <span data-ttu-id="095bc-110">Sanal ağ geçitleri ve ExpressRoute ağ geçidi yapılandırma ayarları hakkında daha fazla bilgi için bkz: [ExpressRoute için sanal ağ geçitleri hakkında](expressroute-about-virtual-network-gateways.md).</span><span class="sxs-lookup"><span data-stu-id="095bc-110">For more information about virtual network gateways and gateway configuration settings for ExpressRoute, see [About virtual network gateways for ExpressRoute](expressroute-about-virtual-network-gateways.md).</span></span> 


## <a name="before-beginning"></a><span data-ttu-id="095bc-111">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="095bc-111">Before beginning</span></span>
<span data-ttu-id="095bc-112">En son Azure PowerShell cmdlet'lerini yüklü olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="095bc-112">Verify that you have installed the latest Azure PowerShell cmdlets.</span></span> <span data-ttu-id="095bc-113">En son cmdlet'leri yüklemediyseniz yapılandırma adımlarına başlamadan önce bunu yapmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="095bc-113">If you haven't installed the latest cmdlets, you need to do so before beginning the configuration steps.</span></span> <span data-ttu-id="095bc-114">Daha fazla bilgi için bkz. [Azure PowerShell’i yükleme ve yapılandırma](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="095bc-114">For more information, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

[!INCLUDE [expressroute-gateway-rm-ps](../../includes/expressroute-gateway-rm-ps-include.md)]

## <a name="next-steps"></a><span data-ttu-id="095bc-115">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="095bc-115">Next steps</span></span>
<span data-ttu-id="095bc-116">VNet ağ geçidini oluşturduktan sonra bir expressroute bağlantı hattı ağınıza bağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="095bc-116">After you have created the VNet gateway, you can link your VNet to an ExpressRoute circuit.</span></span> <span data-ttu-id="095bc-117">Bkz: [bir expressroute bağlantı hattı için bir sanal ağ bağlantı](expressroute-howto-linkvnet-arm.md).</span><span class="sxs-lookup"><span data-stu-id="095bc-117">See [Link a Virtual Network to an ExpressRoute circuit](expressroute-howto-linkvnet-arm.md).</span></span>

