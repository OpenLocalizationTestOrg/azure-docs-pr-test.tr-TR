---
title: "Azure Ağ İzleyicisi sonraki atlama - Azure CLI 1.0 ile sonraki atlama aaaFind | Microsoft Docs"
description: "Bu makale, hangi hello sonraki atlama türü olduğunu ve IP adresini kullanarak sonraki atlama Azure CLI kullanarak nasıl bulabilirsiniz anlatmaktadır."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 0700c274-3e0d-4dca-acfa-3ceac8990613
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 54124c051021413695d70ba93c370605abc6ebbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="find-out-what-hello-next-hop-type-is-using-hello-next-hop-capability-in-azure-network-watcher-using-azure-cli-10"></a>Hangi hello sonraki atlama türü hello sonraki atlama yetenek Azure CLI 1.0 kullanarak Azure Ağ İzleyicisi içinde kullandığını bulmak

> [!div class="op_single_selector"]
> - [Azure portal](network-watcher-check-next-hop-portal.md)
> - [PowerShell](network-watcher-check-next-hop-powershell.md)
> - [CLI 1.0](network-watcher-check-next-hop-cli-nodejs.md)
> - [CLI 2.0](network-watcher-check-next-hop-cli.md)
> - [Azure REST API'si](network-watcher-check-next-hop-rest.md)

Sonraki atlama bir özelliği olan Ağ İzleyicisi'hello yeteneği sağlar, hello sonraki atlama türü ve belirtilen bir sanal makineye dayalı IP adresi al ' dir. Bu özellik, bir sanal makine trafiğe bir ağ geçidi, internet veya sanal ağlar tooget tooits hedef geçiyorsa belirlemede yararlıdır.

Bu makalede, platformlar arası Azure CLI 1.0, Windows, Mac ve Linux için kullanılabilir olduğu kullanır.

## <a name="before-you-begin"></a>Başlamadan önce

Bu senaryoda, hello Azure CLI toofind hello sonraki atlama türü ve IP adresini kullanır.

Bu senaryo zaten izlediğiniz hello adımlarda varsayar [bir Ağ İzleyicisi oluşturma](network-watcher-create.md) toocreate bir Ağ İzleyicisi. Merhaba senaryo da geçerli bir sanal makine ile bir kaynak grubu kullanılan toobe var olduğunu varsayar.

## <a name="scenario"></a>Senaryo

Bu makalede ele alınan hello senaryosu, sonraki atlama, bir özelliği olan Ağ İzleyicisi'hello sonraki atlama türü ve IP adresi için bir kaynak bulur kullanır. Sonraki atlama, hakkında daha fazla toolearn ziyaret [sonraki atlama genel bakış](network-watcher-next-hop-overview.md).


## <a name="get-next-hop"></a>Sonraki atlama Al

Merhaba diyoruz tooget hello sonraki atlama `azure netowrk watcher next-hop` cmdlet'i. Biz hello cmdlet hello Ağ İzleyicisi kaynak grubu, hello NetworkWatcher, sanal makine kimliği, kaynak IP adresi ve hedef IP adresi geçirin. Bu örnekte, başka bir sanal ağda tooa VM hello hedef IP adresi değil. Merhaba iki sanal ağ arasında bir sanal ağ geçidi yok. 

```azurecli
azure network watcher next-hop -g resourceGroupName -n networkWatcherName -t targetResourceId -a <source-ip> -d <destination-ip>
```

> [!NOTE]
Merhaba VM varsa birden çok NIC ve IP iletimini hello NIC'ler hiçbirinde etkinse, NIC parametre hello (-ı NIC-ID) belirtilmelidir. Aksi takdirde isteğe bağlıdır.

## <a name="review-results"></a>Sonuçları gözden geçirin

Tamamlandığında, hello sonuçları sağlanır. Merhaba sonraki atlama IP adresi bu kaynak hello türü yanı sıra döndürülür.

```
data:    Next Hop Ip Address             : 10.0.1.2
info:    network watcher next-hop command OK
```

Merhaba aşağıdaki listede hello şu anda kullanılabilir NextHopType değerleri gösterir:

**Sonraki atlama türü**

* Internet
* Değerinin VirtualAppliance
* VirtualNetworkGateway
* VnetLocal
* HyperNetGateway
* VnetPeering
* None

## <a name="next-steps"></a>Sonraki adımlar

Bilgi nasıl tooreview ağ güvenlik grubu ayarlarınızı programlı olarak şu adresi ziyaret ederek [NSG Denetim Ağ İzleyicisi](network-watcher-nsg-auditing-powershell.md)
