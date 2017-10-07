---
title: "Azure Ağ İzleyicisi sonraki atlama - Azure portal ile aaaFind sonraki atlama | Microsoft Docs"
description: "Bu makalede nasıl hangi hello sonraki atlama türü olan ve sonraki atlama kullanarak IP adresi hello Azure portalında bulabilirsiniz açıklayın"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 7b459dcf-4077-424e-a774-f7bfa34c5975
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: b64a2a5275c15aa8bdb10601de4ae1504a9ab551
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="find-out-what-hello-next-hop-type-is-using-hello-next-hop-capability-in-azure-network-watcher-using-hello-portal"></a>Hangi hello sonraki atlama türü hello sonraki atlama yetenek hello portalı kullanarak Azure Ağ İzleyicisi içinde kullandığını bulmak

> [!div class="op_single_selector"]
> - [Azure portal](network-watcher-check-next-hop-portal.md)
> - [PowerShell](network-watcher-check-next-hop-powershell.md)
> - [CLI 1.0](network-watcher-check-next-hop-cli-nodejs.md)
> - [CLI 2.0](network-watcher-check-next-hop-cli.md)
> - [Azure REST API'si](network-watcher-check-next-hop-rest.md)

Sonraki atlama bir özelliği olan Ağ İzleyicisi'hello yeteneği sağlar, hello sonraki atlama türü ve belirtilen bir sanal makineye dayalı IP adresi al ' dir. Bu özellik, bir sanal makine trafiğe bir ağ geçidi, internet veya sanal ağlar tooget tooits hedef geçiyorsa belirlemede yararlıdır.

## <a name="before-you-begin"></a>Başlamadan önce

Bu senaryo zaten izlediğiniz hello adımlarda varsayar [bir Ağ İzleyicisi oluşturma](network-watcher-create.md) toocreate bir Ağ İzleyicisi. Merhaba senaryo da geçerli bir sanal makine ile bir kaynak grubu kullanılan toobe var olduğunu varsayar.

## <a name="scenario"></a>Senaryo

Bu makalede ele alınan hello senaryo, bir kaynak için sonraki atlama toofind hello sonraki atlama türü ve IP adresini kullanır. Sonraki atlama, hakkında daha fazla toolearn ziyaret [sonraki atlama genel bakış](network-watcher-next-hop-overview.md).

Bu senaryoda, şunları yapacaksınız:

* Bir sanal makineden Hello sonraki atlama alın.

## <a name="get-next-hop"></a>Sonraki atlama Al

### <a name="step-1"></a>1. Adım

Tooyour Ağ İzleyicisi kaynak hello Azure portalına gidin.

### <a name="step-2"></a>2. Adım

Tıklatın **sonraki atlama** hello Gezinti bölmesinde, select hello sanal makine ve ağ arabirimi, hello kaynak ve hedef IP doldurun ve hello tıklatın **sonraki atlama** düğmesi.

> [!NOTE]
> Sonraki atlama hello VM kaynak toorun ayrılır gerektirir.

![sonraki atlama genel bakış][1]

### <a name="step-3"></a>3. Adım

Merhaba görev tamamlandıktan sonra hello sonuçları sağlanır. IP adresi ve cihaz hello sonraki atlama türü hello ise, görüntülenir. Merhaba aşağıdaki tabloda hello kullanılabilir döndürülen değer hello portalda görüntülenir.

**Sonraki atlama türü**

* Internet
* Değerinin VirtualAppliance
* VirtualNetworkGateway
* VnetLocal
* HyperNetGateway
* VnetPeering
* None

Özel rota kullanılan tooroute varsa bu trafiği hello kullanıcı tanımlı yönlendirme (UDR) de hello sonuçlarıyla gösterilir.

![sonraki atlama sonuçları Al][2]

## <a name="next-steps"></a>Sonraki adımlar

Bilgi nasıl tooreview ağ güvenlik grubu ayarlarınızı programlı olarak şu adresi ziyaret ederek [NSG Denetim Ağ İzleyicisi](network-watcher-nsg-auditing-powershell.md)

[1]: ./media/network-watcher-check-next-hop-portal/figure1.png
[2]: ./media/network-watcher-check-next-hop-portal/figure2.png














