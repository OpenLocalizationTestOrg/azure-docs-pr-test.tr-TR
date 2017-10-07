---
title: "Azure Ağ İzleyicisi sonraki atlama - PowerShell ile aaaFind sonraki atlama | Microsoft Docs"
description: "Bu makale, hangi hello sonraki atlama türü olduğunu ve IP adresini kullanarak sonraki atlama PowerShell kullanarak nasıl bulabilirsiniz anlatmaktadır."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 6a656c55-17bd-40f1-905d-90659087639c
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: fdb0b4a02d95fc45c103fe952fc1afa095414c18
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="find-out-what-hello-next-hop-type-is-using-hello-next-hop-capability-in-azure-network-watcher-using-powershell"></a>Hangi hello sonraki atlama türü hello sonraki atlama yetenek PowerShell kullanarak Azure Ağ İzleyicisi içinde kullandığını bulmak

> [!div class="op_single_selector"]
> - [Azure portal](network-watcher-check-next-hop-portal.md)
> - [PowerShell](network-watcher-check-next-hop-powershell.md)
> - [CLI 1.0](network-watcher-check-next-hop-cli-nodejs.md)
> - [CLI 2.0](network-watcher-check-next-hop-cli.md)
> - [Azure REST API'si](network-watcher-check-next-hop-rest.md)

Sonraki atlama bir özelliği olan Ağ İzleyicisi'hello yeteneği sağlar, hello sonraki atlama türü ve belirtilen bir sanal makineye dayalı IP adresi al ' dir. Bu özellik, bir sanal makine trafiğe bir ağ geçidi, internet veya sanal ağlar tooget tooits hedef geçiyorsa belirlemede yararlıdır.

## <a name="before-you-begin"></a>Başlamadan önce

Bu senaryoda, hello Azure portal toofind hello sonraki atlama türü ve IP adresini kullanır.

Bu senaryo zaten izlediğiniz hello adımlarda varsayar [bir Ağ İzleyicisi oluşturma](network-watcher-create.md) toocreate bir Ağ İzleyicisi. Merhaba senaryo da geçerli bir sanal makine ile bir kaynak grubu kullanılan toobe var olduğunu varsayar.

## <a name="scenario"></a>Senaryo

Bu makalede ele alınan hello senaryosu, sonraki atlama, bir özelliği olan Ağ İzleyicisi'hello sonraki atlama türü ve IP adresi için bir kaynak bulur kullanır. Sonraki atlama, hakkında daha fazla toolearn ziyaret [sonraki atlama genel bakış](network-watcher-next-hop-overview.md).

## <a name="retrieve-network-watcher"></a>Ağ İzleyicisi alma

Merhaba ilk adımı tooretrieve hello Ağ İzleyicisi örneğidir. Merhaba `$networkWatcher` değişkeni toohello sonraki atlama geçirilen cmdlet doğrulayın.

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName 
```

## <a name="get-a-virtual-machine"></a>Bir sanal makine Al

Sonraki atlama hello sonraki atlama ve hello sonraki atlamanın IP adresi hello bir sanal makineden döndürür. Bir sanal makine kimliği hello cmdlet'i için gereklidir. Merhaba sanal makine toouse hello Kimliğini biliyorsanız, bu adımı atlayabilirsiniz.

```powershell
$VM = Get-AzurermVM -ResourceGroupName "testrg" -Name "testvm1"
```

> [!NOTE]
> Sonraki atlama hello VM kaynak toorun ayrılır gerektirir.

## <a name="get-hello-network-interfaces"></a>Merhaba ağ arabirimlerini Al

Bu örnekte, bir sanal makinede hello NIC'ler alıyoruz hello sanal makinede bir NIC Hello IP adresi gereklidir. Başlangıç IP adresini biliyorsanız tootest istediğiniz hello sanal makinede, bu adımı atlayabilirsiniz.

```powershell
$Nics = Get-AzureRmNetworkInterface | Where {$_.Id -eq $vm.NetworkProfile.NetworkInterfaces.Id.ForEach({$_})}
```

## <a name="get-next-hop"></a>Sonraki atlama Al

Merhaba diyoruz artık `Get-AzureRmNetworkWatcherNextHop` cmdlet'i. Biz hello cmdlet hello Ağ İzleyicisi, sanal makine kimliği geçişi, kaynak IP adresi ve hedef IP adresi. Bu örnekte, başka bir sanal ağda tooa VM hello hedef IP adresi değil. Merhaba iki sanal ağ arasında bir sanal ağ geçidi yok.

```powershell
Get-AzureRmNetworkWatcherNextHop -NetworkWatcher $networkWatcher -TargetVirtualMachineId $VM.Id -SourceIPAddress $nics[0].IpConfigurations[0].PrivateIpAddress  -DestinationIPAddress 10.0.2.4 
```

## <a name="review-results"></a>Sonuçları gözden geçirin

Tamamlandığında, hello sonuçları sağlanır. Merhaba sonraki atlama IP adresi bu kaynak hello türü yanı sıra döndürülür. Bu senaryoda, hello hello sanal ağ geçidi genel IP adresi değil.

```
NextHopIpAddress NextHopType           RouteTableId 
---------------- -----------           ------------ 
13.78.238.92     VirtualNetworkGateway Gateway Route
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

















