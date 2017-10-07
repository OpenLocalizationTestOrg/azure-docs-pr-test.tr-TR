---
title: "Azure Ağ İzleyicisi IP akış ile aaaverify trafiği doğrulama - PowerShell | Microsoft Docs"
description: "Bu makalede nasıl bir sanal makineden trafiği tooor izin verilen veya PowerShell kullanarak reddedildi toocheck"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: e1dad757-8c5d-467f-812e-7cc751143207
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 924da1de1bd554e15816886f8e51d7f170f0e7ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-tooor-from-a-vm-with-ip-flow-verify-a-component-of-azure-network-watcher"></a>Trafik izin verilen ya da bir VM'den IP akış ile tooor reddedildi onay Azure Ağ İzleyicisi'nin bir bileşeni doğrulayın

> [!div class="op_single_selector"]
> - [Azure portal](network-watcher-check-ip-flow-verify-portal.md)
> - [PowerShell](network-watcher-check-ip-flow-verify-powershell.md)
> - [CLI 1.0](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [CLI 2.0](network-watcher-check-ip-flow-verify-cli.md)
> - [Azure REST API'si](network-watcher-check-ip-flow-verify-rest.md)


IP akış doğrulayın Ağ İzleyicisinin, trafiği bir sanal makineden tooor izin verilip verilmediğini tooverify sağlayan bir özelliktir. Bu senaryo kullanışlı tooget bir sanal makine tooan dış kaynak veya arka uç iletişim kurabilirsiniz, geçerli bir durumda olur. IP akış doğrulayın olabilir kullanılan tooverify ağ güvenlik grubu (NSG) kurallarınızı düzgün şekilde yapılandırılırsa ve NSG kuralları tarafından engellenen akışları sorun giderme. IP kullanan başka bir nedeni akış durumda engellenen istediğiniz tooensure trafiği engellenmiş düzgün şekilde NSG hello tarafından doğrulayın.

## <a name="before-you-begin"></a>Başlamadan önce

Bu senaryo zaten izlediğiniz hello adımlarda varsayar [bir Ağ İzleyicisi oluşturmak](network-watcher-create.md) toocreate bir Ağ İzleyicisi'ni veya mevcut bir Ağ İzleyicisi örneği. Merhaba senaryo da geçerli bir sanal makine ile bir kaynak grubu kullanılan toobe var olduğunu varsayar.

## <a name="scenario"></a>Senaryo

Bu senaryo kullanan IP akışını denetlemek için bir sanal makine tooa bilinen geçebildiğinden if tooverify Bing IP adresi. Merhaba trafik reddedilirse, bu trafiğin reddediyor hello güvenlik kuralı döndürür. IP akışı hakkında daha fazla doğrulama, toolearn ziyaret [IP akış doğrulayın genel bakış](network-watcher-ip-flow-verify-overview.md)

## <a name="retrieve-network-watcher"></a>Ağ İzleyicisi alma

Merhaba ilk adımı tooretrieve hello Ağ İzleyicisi örneğidir. Merhaba `$networkWatcher` değişkeni toohello IP geçirilen akış cmdlet doğrulayın.

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName 
```

## <a name="get-a-vm"></a>VM Al

IP akış testleri trafiği tooor bir sanal makine tooor uzaktan bir hedef üzerinde bir IP adresinden doğrulayın. Bir sanal makine kimliği hello cmdlet'i için gereklidir. Merhaba sanal makine toouse hello Kimliğini biliyorsanız, bu adımı atlayabilirsiniz.

```powershell
$VM = Get-AzurermVM -ResourceGroupName "testrg" -Name "testvm1"
```

## <a name="get-hello-nics"></a>Merhaba NIC alma

Bu örnekte, bir sanal makinede hello NIC'ler alıyoruz hello sanal makinede bir NIC Hello IP adresi gereklidir. Başlangıç IP adresini biliyorsanız tootest istediğiniz hello sanal makinede, bu adımı atlayabilirsiniz.

```powershell
$Nics = Get-AzureRmNetworkInterface | Where {$_.Id -eq $vm.NetworkProfile.NetworkInterfaces.Id.ForEach({$_})}
```

## <a name="run-ip-flow-verify"></a>Çalışma IP akış doğrulayın

Toorun hello cmdlet hello bilgi sahibiz, biz hello çalıştırmak `Test-AzureRmNetworkWatcherIPFlow` cmdlet tootest hello trafiği. Bu örnekte, hello ilk IP adresi hello ilk NIC üzerinde kullanıyoruz

```powershell
Test-AzureRmNetworkWatcherIPFlow -NetworkWatcher $networkWatcher -TargetVirtualMachineId $VM.Id `
-Direction Outbound -Protocol TCP `
-LocalIPAddress $nics[0].IpConfigurations[0].PrivateIpAddress -LocalPort 6895 -RemoteIPAddress 204.79.197.200 -RemotePort 80
```

> [!NOTE]
> IP akış doğrulayın gerektirir hello VM kaynak toorun ayrılır.

## <a name="review-results"></a>Sonuçları gözden geçirin

Çalıştırdıktan sonra `Test-AzureRmNetworkWatcherIPFlow` hello sonuçlarının döndürüldüğü, hello aşağıdaki adım önceki hello döndürülen hello sonuçları bir örnektir.

```
Access RuleName                                  
------ --------                                  
Allow  defaultSecurityRules/AllowInternetOutBound
```

## <a name="next-steps"></a>Sonraki adımlar

Trafik engelleniyor ve olmamalıdır, bkz: [ağ güvenlik grupları yönet](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tanımlanan hello ağ güvenlik grubu ve güvenlik kuralları aşağı tootrack.

[1]: ./media/network-watcher-check-ip-flow-verify-portal/figure1.png
[2]: ./media/network-watcher-check-ip-flow-verify-portal/figure2.png













