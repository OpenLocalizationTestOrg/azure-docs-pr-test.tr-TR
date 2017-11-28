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
ms.openlocfilehash: 195a38fa45f1c514a93980e777fb0d8238aa3f3f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-a-virtual-network-gateway-for-expressroute-using-powershell-classic"></a><span data-ttu-id="a14c6-103">Bir sanal ağ geçidi (Klasik) PowerShell kullanarak ExpressRoute için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="a14c6-103">Configure a virtual network gateway for ExpressRoute using PowerShell (classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a14c6-104">Resource Manager - PowerShell</span><span class="sxs-lookup"><span data-stu-id="a14c6-104">Resource Manager - PowerShell</span></span>](expressroute-howto-add-gateway-resource-manager.md)
> * [<span data-ttu-id="a14c6-105">Klasik - PowerShell</span><span class="sxs-lookup"><span data-stu-id="a14c6-105">Classic - PowerShell</span></span>](expressroute-howto-add-gateway-classic.md)
> * [<span data-ttu-id="a14c6-106">Video - Azure portalı</span><span class="sxs-lookup"><span data-stu-id="a14c6-106">Video - Azure Portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-vpn-gateway-for-your-virtual-network)
> 
> 

<span data-ttu-id="a14c6-107">Bu makalede eklemek, yeniden boyutlandırma ve önceden var olan bir VNet için bir sanal ağ (VNet) ağ geçidini kaldırmak için adımlarda size yol gösterecek.</span><span class="sxs-lookup"><span data-stu-id="a14c6-107">This article will walk you through the steps to add, resize, and remove a virtual network (VNet) gateway for a pre-existing VNet.</span></span> <span data-ttu-id="a14c6-108">Adımlardır kullanılarak oluşturulan özellikle sanal ağlar için bu yapılandırma için **Klasik dağıtım modeli** ve, bir expressroute bağlantı yapılandırmasında kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="a14c6-108">The steps for this configuration are specifically for VNets that were created using the **classic deployment model** and that will be be used in an ExpressRoute configuration.</span></span> 

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

<span data-ttu-id="a14c6-109">**Azure dağıtım modelleri hakkında**</span><span class="sxs-lookup"><span data-stu-id="a14c6-109">**About Azure deployment models**</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="before-beginning"></a><span data-ttu-id="a14c6-110">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="a14c6-110">Before beginning</span></span>
<span data-ttu-id="a14c6-111">Bu yapılandırma için gerekli Azure PowerShell cmdlet'lerini yüklü olduğunu doğrulayın (1.0.2 veya üzeri).</span><span class="sxs-lookup"><span data-stu-id="a14c6-111">Verify that you have installed the Azure PowerShell cmdlets needed for this configuration (1.0.2 or later).</span></span> <span data-ttu-id="a14c6-112">Cmdlet'leri yüklemediyseniz yapılandırma adımlarına başlamadan önce bunu yapmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="a14c6-112">If you haven't installed the cmdlets, you'll need to do so before beginning the configuration steps.</span></span> <span data-ttu-id="a14c6-113">Azure PowerShell'i yükleme hakkında daha fazla bilgi için bkz: [Azure PowerShell'i yükleme ve yapılandırma nasıl](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a14c6-113">For more information about installing Azure PowerShell, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

[!INCLUDE [expressroute-gateway-classic-ps](../../includes/expressroute-gateway-classic-ps-include.md)]

## <a name="next-steps"></a><span data-ttu-id="a14c6-114">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a14c6-114">Next steps</span></span>
<span data-ttu-id="a14c6-115">VNet ağ geçidini oluşturduktan sonra bir expressroute bağlantı hattı ağınıza bağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a14c6-115">After you have created the VNet gateway, you can link your VNet to an ExpressRoute circuit.</span></span> <span data-ttu-id="a14c6-116">Bkz: [bir expressroute bağlantı hattı için bir sanal ağ bağlantı](expressroute-howto-linkvnet-classic.md).</span><span class="sxs-lookup"><span data-stu-id="a14c6-116">See [Link a Virtual Network to an ExpressRoute circuit](expressroute-howto-linkvnet-classic.md).</span></span>

