---
title: Windows Server VM aaaConnect tooa | Microsoft Docs
description: "Azure portal ve hello Resource Manager dağıtım modeli tooconnect ve Windows VM tooa kullanarak oturum aç nasıl hello öğrenin."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: ef62b02e-bf35-468d-b4c3-71b63fe7f409
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/01/2017
ms.author: cynthn
ms.openlocfilehash: dc397f435ef165ae5af09f1d037ad3d520bb7ac3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconnect-and-log-on-tooan-azure-virtual-machine-running-windows"></a><span data-ttu-id="72e3f-103">Nasıl Windows çalıştıran tooconnect ve oturum açma tooan Azure sanal makine</span><span class="sxs-lookup"><span data-stu-id="72e3f-103">How tooconnect and log on tooan Azure virtual machine running Windows</span></span>
<span data-ttu-id="72e3f-104">Merhaba kullanacağınız **Bağlan** hello Azure portal toostart bir Windows Masaüstü Uzak Masaüstü (RDP) oturumu düğmesini.</span><span class="sxs-lookup"><span data-stu-id="72e3f-104">You'll use hello **Connect** button in hello Azure portal toostart a Remote Desktop (RDP) session from a Windows desktop.</span></span> <span data-ttu-id="72e3f-105">Önce toohello sanal makineye bağlanın ve sonra oturum açın.</span><span class="sxs-lookup"><span data-stu-id="72e3f-105">First you connect toohello virtual machine, then you log on.</span></span>

<span data-ttu-id="72e3f-106">Tooconnect tooa Mac Windows VM'den çalışıyorsanız, Mac için RDP istemcisi gibi tooinstall gerek [Microsoft Uzak Masaüstü](https://itunes.apple.com/app/microsoft-remote-desktop/id715768417).</span><span class="sxs-lookup"><span data-stu-id="72e3f-106">If you are trying tooconnect tooa Windows VM from a Mac, you need tooinstall an RDP client for Mac like [Microsoft Remote Desktop](https://itunes.apple.com/app/microsoft-remote-desktop/id715768417).</span></span>

## <a name="connect-toohello-virtual-machine"></a><span data-ttu-id="72e3f-107">Toohello sanal makineye bağlanma</span><span class="sxs-lookup"><span data-stu-id="72e3f-107">Connect toohello virtual machine</span></span>
1. <span data-ttu-id="72e3f-108">Zaten yapmadıysanız, toohello içinde oturum [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="72e3f-108">If you haven't already done so, sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="72e3f-109">Merhaba Hub menüsünde **sanal makineleri**.</span><span class="sxs-lookup"><span data-stu-id="72e3f-109">On hello Hub menu, click **Virtual Machines**.</span></span>
3. <span data-ttu-id="72e3f-110">Merhaba sanal makine hello listeden seçin.</span><span class="sxs-lookup"><span data-stu-id="72e3f-110">Select hello virtual machine from hello list.</span></span>
4. <span data-ttu-id="72e3f-111">Merhaba sanal makine için Hello dikey penceresinde **Bağlan**.</span><span class="sxs-lookup"><span data-stu-id="72e3f-111">On hello blade for hello virtual machine, click **Connect**.</span></span>
   
    ![Hello Azure portal gösteren ekran görüntüsü nasıl tooconnect tooyour VM.](./media/connect-logon/connect.png)
   
   > [!TIP]
   > <span data-ttu-id="72e3f-113">Merhaba, **Bağlan** hello portalda düğmesine griyse ve aracılığıyla bağlı tooAzure olmayan bir [hızlı rota](../../expressroute/expressroute-introduction.md) veya [siteden siteye VPN](../../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md) bağlantısı toocreate gerekir ve RDP kullanmadan önce VM genel bir IP adresi atayın.</span><span class="sxs-lookup"><span data-stu-id="72e3f-113">If hello **Connect** button in hello portal is greyed out and you are not connected tooAzure via an [Express Route](../../expressroute/expressroute-introduction.md) or [Site-to-Site VPN](../../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md) connection, you need toocreate and assign your VM a public IP address before you can use RDP.</span></span> <span data-ttu-id="72e3f-114">[Azure’da genel IP adresleri](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) hakkında daha fazlasını okuyabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="72e3f-114">You can read more about [public IP addresses in Azure](../../virtual-network/virtual-network-ip-addresses-overview-arm.md).</span></span>
   > 
   > 

## <a name="log-on-toohello-virtual-machine"></a><span data-ttu-id="72e3f-115">Toohello sanal makinede oturum açın</span><span class="sxs-lookup"><span data-stu-id="72e3f-115">Log on toohello virtual machine</span></span>
[!INCLUDE [virtual-machines-log-on-win-server](../../../includes/virtual-machines-log-on-win-server.md)]

## <a name="next-steps"></a><span data-ttu-id="72e3f-116">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="72e3f-116">Next steps</span></span>
<span data-ttu-id="72e3f-117">Tooconnect çalıştığınızda sorun çalıştırırsanız, bkz: [sorun giderme Uzak Masaüstü bağlantıları](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="72e3f-117">If you run into trouble when you try tooconnect, see [Troubleshoot Remote Desktop connections](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="72e3f-118">Bu makale ortak sorunları tanılama ve çözme boyunca size yol gösterecektir.</span><span class="sxs-lookup"><span data-stu-id="72e3f-118">This article walks you through diagnosing and resolving common problems.</span></span>

