---
title: "Azure Ağ İzleyicisi IP akış ile aaaVerify trafiği doğrulama - REST | Microsoft Docs"
description: "Bu makalede nasıl bir sanal makineden trafiği tooor izin verilen veya reddedilen varsa toocheck"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 3307a79f-03be-46a0-aaaf-b2079cb5f3b2
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 956db0d326db597c6c402a9e8d4a5522c47c02d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-with-ip-flow-verify-a-component-of-azure-network-watcher"></a>Trafik izin verilen ya da IP akışla reddedildi onay Azure Ağ İzleyicisi'nin bir bileşeni doğrulayın

> [!div class="op_single_selector"]
> - [Azure portal](network-watcher-check-ip-flow-verify-portal.md)
> - [PowerShell](network-watcher-check-ip-flow-verify-powershell.md)
> - [CLI 1.0](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [CLI 2.0](network-watcher-check-ip-flow-verify-cli.md)
> - [Azure REST API'si](network-watcher-check-ip-flow-verify-rest.md)


IP akış doğrulayın Ağ İzleyicisinin, trafiği bir sanal makineden tooor izin verilip verilmediğini tooverify sağlayan bir özelliktir. Merhaba doğrulama gelen veya giden trafiği için çalıştırılabilir. Bu senaryo kullanışlı tooget bir sanal makine tooan dış kaynak veya arka uç iletişim kurabilirsiniz, geçerli bir durumda olur. IP akış doğrulayın olabilir kullanılan tooverify ağ güvenlik grubu (NSG) kurallarınızı düzgün şekilde yapılandırılırsa ve NSG kuralları tarafından engellenen akışları sorun giderme. IP kullanan başka bir nedeni akış durumda engellenen istediğiniz tooensure trafiği engellenmiş düzgün şekilde NSG hello tarafından doğrulayın.

## <a name="before-you-begin"></a>Başlamadan önce

ARMclient PowerShell kullanarak kullanılan toocall hello REST API ' dir. ARMClient bulundu üzerinde adresindeki chocolatey [ARMClient Chocolatey üzerinde](https://chocolatey.org/packages/ARMClient)

Bu senaryo zaten izlediğiniz hello adımlarda varsayar [bir Ağ İzleyicisi oluşturma](network-watcher-create.md) toocreate bir Ağ İzleyicisi.

## <a name="scenario"></a>Senaryo

Bu senaryo IP akış doğrula tooverify kullanıyorsa bir sanal makine tooanother makine 443 numaralı bağlantı noktası iletişim kurabilirsiniz. Merhaba trafik reddedilirse, bu trafiğin reddediyor hello güvenlik kuralı döndürür. IP akış doğrulayın, hakkında daha fazla toolearn ziyaret [IP akış doğrulayın genel bakış](network-watcher-ip-flow-verify-overview.md)

Bu senaryoda:

* Bir sanal makine alma
* Çağrı IP akış doğrulayın
* Sonuçları doğrulayın

## <a name="log-in-with-armclient"></a>Oturum ARMClient oturum

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a>Bir sanal makine alma

Komut dosyası tooreturn aşağıdaki hello bir sanal makine çalıştırın. Merhaba aşağıdaki kodu değerleri hello değişkenleri gerekir:

* **Subscriptionıd** -abonelik kimliği toouse hello.
* **resourceGroupName** - hello sanal makine içeren bir kaynak grubu adı.

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "<resource group name>"

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

Merhaba gerekli bilgileri hello hello türü altında kimliğidir `Microsoft.Compute/virtualMachines`. Merhaba sonuçları benzer toohello kodu örneği aşağıdaki gibi olmalıdır:

```json
...,
        "networkProfile": {
          "networkInterfaces": [
            {
              "id": "/subscriptions/{00000000-0000-0000-0000-000000000000}/resourceGroups/ContosoExampleRG/providers/Microsoft
.Network/networkInterfaces/contosovm842"
            }
          ]
        },
        "provisioningState": "Succeeded"
      },
      "resources": [
        {
          "id": "/subscriptions/{00000000-0000-0000-0000-000000000000}/resourceGroups/ContosoExampleRG/providers/Microsoft.Com
pute/virtualMachines/ContosoVM/extensions/CustomScriptExtension"
        }
      ],
      "type": "Microsoft.Compute/virtualMachines",
      "location": "westcentralus",
      "id": "/subscriptions/{00000000-0000-0000-0000-000000000000}/resourceGroups/ContosoExampleRG/providers/Microsoft.Compute
/virtualMachines/ContosoVM",
      "name": "ContosoVM"
    }
  ]
}
```

## <a name="call-ip-flow-verify"></a>Çağrı IP akış doğrulayın

Merhaba aşağıdaki örnek belirtilen bir sanal makine için bir istek tooverify hello trafiği oluşturur. Merhaba trafiğine izin verilip verilmediğini veya hello trafiği reddedilirse Hello yanıtı döndürür. Trafik reddedilirse Ayrıca hangi kural bloklarını trafiği hello döndürür.

> [!NOTE]
> IP akış doğrulayın gerektirir hello VM kaynak ayrılır.

Merhaba betik hello kaynak kimliği, bir sanal makinenin ve hello sanal makinedeki ağ arabirim kartı gerektirir. Bu değerleri çıktı önceki hello tarafından sağlanır.

> [!Important]
> İçin tüm Ağ İzleyicisi REST çağrılarını hello hello tanılama eylemleri gerçekleştirdiğiniz hello kaynakları değil hello Ağ İzleyicisi örneği içeren bir URI'dir hello isteğindeki kaynak grubu adı hello.

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "<resource group name>"
$networkWatcherName = "<network watcher name>"
$vmName = "<vm name>"
$vmNICName = "<vm NIC name>"
$direction = "<direction of traffic>" # Examples are: Inbound or Outbound
$localIP = "<source IP>"
$localPort = "<source Port>"
$remoteIP = "<destination IP>"
$remotePort = "<destination Port>" # Examples are: 80, or 80-120
$protocol = "<UDP, TCP or *>"
$targetUri = "<uri of target resource>" # Example: /subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.compute/virtualMachine/${vmName}
$targetNic = "<uri of target nic resource>" # Example: /subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkInterfaces/${vmNICName}

$requestBody = @"
{
    'targetResourceId':  '$targetUri',
    'direction':  '$direction',
    'protocol':  '$protocol',
    'localPort':  '$localPort',
    'remotePort':  '$remotePort',
    'localIPAddress':  '$localIP',
    'remoteIPAddress':  '$remoteIP',
    'targetNICResourceId':  '$targetNic'
}
"@
        
armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/ipFlowVerify?api-version=2016-12-01" $requestBody -verbose
```

## <a name="understanding-hello-results"></a>Merhaba sonuçlarını anlama

geri alma hello yanıt hello trafiğine izin verilen veya reddedilen söyler. Merhaba yanıt bir hello örnekler aşağıdaki gibi görünür:

**İzin verilen**

```json
{
  "access": "Allow",
  "ruleName": "defaultSecurityRules/AllowInternetOutBound"
}
```

**Engellendi**

```json
{
  "access": "Deny",
  "ruleName": "defaultSecurityRules/DefaultInboundDenyAll"
}
```

## <a name="next-steps"></a>Sonraki adımlar

Trafik engelleniyor ve olmamalıdır, bkz: [ağ güvenlik grupları yönet](../virtual-network/virtual-network-manage-nsg-arm-portal.md) toolearn ağ güvenlik grupları hakkında daha fazla bilgi.












