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
# <a name="how-tooconnect-and-log-on-tooan-azure-virtual-machine-running-windows"></a>Nasıl Windows çalıştıran tooconnect ve oturum açma tooan Azure sanal makine
Merhaba kullanacağınız **Bağlan** hello Azure portal toostart bir Windows Masaüstü Uzak Masaüstü (RDP) oturumu düğmesini. Önce toohello sanal makineye bağlanın ve sonra oturum açın.

Tooconnect tooa Mac Windows VM'den çalışıyorsanız, Mac için RDP istemcisi gibi tooinstall gerek [Microsoft Uzak Masaüstü](https://itunes.apple.com/app/microsoft-remote-desktop/id715768417).

## <a name="connect-toohello-virtual-machine"></a>Toohello sanal makineye bağlanma
1. Zaten yapmadıysanız, toohello içinde oturum [Azure portal](https://portal.azure.com/).
2. Merhaba Hub menüsünde **sanal makineleri**.
3. Merhaba sanal makine hello listeden seçin.
4. Merhaba sanal makine için Hello dikey penceresinde **Bağlan**.
   
    ![Hello Azure portal gösteren ekran görüntüsü nasıl tooconnect tooyour VM.](./media/connect-logon/connect.png)
   
   > [!TIP]
   > Merhaba, **Bağlan** hello portalda düğmesine griyse ve aracılığıyla bağlı tooAzure olmayan bir [hızlı rota](../../expressroute/expressroute-introduction.md) veya [siteden siteye VPN](../../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md) bağlantısı toocreate gerekir ve RDP kullanmadan önce VM genel bir IP adresi atayın. [Azure’da genel IP adresleri](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) hakkında daha fazlasını okuyabilirsiniz.
   > 
   > 

## <a name="log-on-toohello-virtual-machine"></a>Toohello sanal makinede oturum açın
[!INCLUDE [virtual-machines-log-on-win-server](../../../includes/virtual-machines-log-on-win-server.md)]

## <a name="next-steps"></a>Sonraki adımlar
Tooconnect çalıştığınızda sorun çalıştırırsanız, bkz: [sorun giderme Uzak Masaüstü bağlantıları](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Bu makale ortak sorunları tanılama ve çözme boyunca size yol gösterecektir.

