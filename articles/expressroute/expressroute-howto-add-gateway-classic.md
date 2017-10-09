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
# <a name="configure-a-virtual-network-gateway-for-expressroute-using-powershell-classic"></a><span data-ttu-id="67a7c-103">Bir sanal ağ geçidi (Klasik) PowerShell kullanarak ExpressRoute için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="67a7c-103">Configure a virtual network gateway for ExpressRoute using PowerShell (classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="67a7c-104">Resource Manager - PowerShell</span><span class="sxs-lookup"><span data-stu-id="67a7c-104">Resource Manager - PowerShell</span></span>](expressroute-howto-add-gateway-resource-manager.md)
> * [<span data-ttu-id="67a7c-105">Klasik - PowerShell</span><span class="sxs-lookup"><span data-stu-id="67a7c-105">Classic - PowerShell</span></span>](expressroute-howto-add-gateway-classic.md)
> * [<span data-ttu-id="67a7c-106">Video - Azure portalı</span><span class="sxs-lookup"><span data-stu-id="67a7c-106">Video - Azure Portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-vpn-gateway-for-your-virtual-network)
> 
> 

<span data-ttu-id="67a7c-107">Bu makale size yol gösterir hello adımları tooadd aracılığıyla yeniden boyutlandırma ve önceden var olan bir VNet için bir sanal ağ (VNet) ağ geçidi kaldırın.</span><span class="sxs-lookup"><span data-stu-id="67a7c-107">This article will walk you through hello steps tooadd, resize, and remove a virtual network (VNet) gateway for a pre-existing VNet.</span></span> <span data-ttu-id="67a7c-108">Merhaba bu yapılandırma için hello kullanılarak oluşturulan özellikle sanal ağlar için adımlardır **Klasik dağıtım modeli** ve, bir expressroute bağlantı yapılandırmasında kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="67a7c-108">hello steps for this configuration are specifically for VNets that were created using hello **classic deployment model** and that will be be used in an ExpressRoute configuration.</span></span> 

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

<span data-ttu-id="67a7c-109">**Azure dağıtım modelleri hakkında**</span><span class="sxs-lookup"><span data-stu-id="67a7c-109">**About Azure deployment models**</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="before-beginning"></a><span data-ttu-id="67a7c-110">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="67a7c-110">Before beginning</span></span>
<span data-ttu-id="67a7c-111">Bu yapılandırma için gerekli hello Azure PowerShell cmdlet'lerini yüklü olduğunu doğrulayın (1.0.2 veya üzeri).</span><span class="sxs-lookup"><span data-stu-id="67a7c-111">Verify that you have installed hello Azure PowerShell cmdlets needed for this configuration (1.0.2 or later).</span></span> <span data-ttu-id="67a7c-112">Merhaba cmdlet'leri yüklemediyseniz toodo gerekir hello yapılandırma adımlarına başlamadan önce bunu.</span><span class="sxs-lookup"><span data-stu-id="67a7c-112">If you haven't installed hello cmdlets, you'll need toodo so before beginning hello configuration steps.</span></span> <span data-ttu-id="67a7c-113">Azure PowerShell'i yükleme hakkında daha fazla bilgi için bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="67a7c-113">For more information about installing Azure PowerShell, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

[!INCLUDE [expressroute-gateway-classic-ps](../../includes/expressroute-gateway-classic-ps-include.md)]

## <a name="next-steps"></a><span data-ttu-id="67a7c-114">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="67a7c-114">Next steps</span></span>
<span data-ttu-id="67a7c-115">Merhaba VNet ağ geçidini oluşturduktan sonra VNet tooan expressroute bağlantı hattı bağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="67a7c-115">After you have created hello VNet gateway, you can link your VNet tooan ExpressRoute circuit.</span></span> <span data-ttu-id="67a7c-116">Bkz: [sanal ağ tooan expressroute bağlantı hattı bağlantı](expressroute-howto-linkvnet-classic.md).</span><span class="sxs-lookup"><span data-stu-id="67a7c-116">See [Link a Virtual Network tooan ExpressRoute circuit](expressroute-howto-linkvnet-classic.md).</span></span>

