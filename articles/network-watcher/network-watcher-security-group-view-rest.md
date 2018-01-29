---
title: "Azure Ağ İzleyicisi güvenlik grubu görünümü - REST API'si ile ağ güvenliği çözümleme | Microsoft Docs"
description: "Bu makalede PowerShell güvenlik grubu görünümü ile sanal makineleri güvenliği çözümlemek için nasıl kullanılacağını anlatmaktadır."
services: network-watcher
documentationcenter: na
author: jimdial
manager: timlt
editor: 
ms.assetid: a2f418fe-f5d2-43ed-8dc3-df0ed2a4d4ac
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: jdial
ms.openlocfilehash: 0eec45630fe3467db26620787038f6dd5a05cc72
ms.sourcegitcommit: b5c6197f997aa6858f420302d375896360dd7ceb
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/21/2017
---
# <a name="analyze-your-virtual-machine-security-with-security-group-view-using-rest-api"></a>Güvenlik grubu REST API kullanarak görünümü ile sanal makine güvenliğinizi Çözümle

> [!div class="op_single_selector"]
> - [PowerShell](network-watcher-security-group-view-powershell.md)
> - [CLI 1.0](network-watcher-security-group-view-cli-nodejs.md)
> - [CLI 2.0](network-watcher-security-group-view-cli.md)
> - [REST API](network-watcher-security-group-view-rest.md)

Güvenlik grubu görünümü bir sanal makineye uygulanan yapılandırılmış ve etkili ağ güvenlik kuralları döndürür. Bu denetim ve ağ güvenlik grupları ve trafik yükleniyor emin olmak için bir VM üzerinde yapılandırılmış kurallarını tanılamak yararlı bir yetenektir doğru şekilde izin verilen veya reddedilen. Bu makalede, sizi, REST API kullanarak bir sanal makine için etkili ve uygulanan güvenlik kuralları nasıl alınacağını gösterir

## <a name="before-you-begin"></a>Başlamadan önce

Bu senaryoda, bir sanal makine için güvenlik grubu görünümü almak için Ağ İzleyicisi Rest API çağrısı. ARMclient PowerShell kullanarak REST API'sini çağırmak için kullanılır. ARMClient bulundu üzerinde adresindeki chocolatey [ARMClient Chocolatey üzerinde](https://chocolatey.org/packages/ARMClient)

Bu senaryo zaten izlediğiniz adımlarda varsayar [bir Ağ İzleyicisi oluşturma](network-watcher-create.md) bir Ağ İzleyicisi oluşturmak için. Senaryo da geçerli bir sanal makine ile bir kaynak grubu kullanılacak var olduğunu varsayar.

## <a name="scenario"></a>Senaryo

Bu makalede ele alınan senaryo, belirli bir sanal makine için etkili ve uygulanan güvenlik kurallarını alır.

## <a name="log-in-with-armclient"></a>Oturum ARMClient oturum

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a>Bir sanal makine alma

Aşağıdaki kod, sanal machineThe döndürmek için aşağıdaki betiği çalıştırın değişkenleri gerekir:

- **Subscriptionıd** -abonelik kimliği ile aynı zamanda alınabilir **Get-AzureRMSubscription** cmdlet'i.
- **resourceGroupName** -sanal makine içeren bir kaynak grubu adı.

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = '<resource group name>'

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

Gerekli bilgileri **kimliği** türü'nün altında `Microsoft.Compute/virtualMachines` aşağıdaki örnekte görüldüğü gibi yanıt:

```json
...,
        "networkProfile": {
          "networkInterfaces": [
            {
              "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft
.Network/networkInterfaces/{nicName}"
            }
          ]
        },
        "provisioningState": "Succeeded"
      },
      "resources": [
        {
          "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Com
pute/virtualMachines/{vmName}/extensions/CustomScriptExtension"
        }
      ],
      "type": "Microsoft.Compute/virtualMachines",
      "location": "westcentralus",
      "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute
/virtualMachines/{vmName}",
      "name": "{vmName}"
    }
  ]
}
```

## <a name="get-security-group-view-for-virtual-machine"></a>Sanal makine için güvenlik grubu görünümü Al

Aşağıdaki örnek, hedeflenen bir sanal makinenin güvenlik grubu görünümü ister. Bu örnek sonuçlarından kurallara ve yapılandırma değişikliklerini aramak için oluşturulma tarafından tanımlanan güvenlik karşılaştırmak için kullanılabilir.

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "<resource group name>"
$networkWatcherName = "<network watcher name>"
$targetUri = "<uri of target resource>" # Example: /subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.compute/virtualMachine/$vmName

$requestBody = @"
{
    'targetResourceId': '${targetUri}'

}
"@
armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/securityGroupView?api-version=2016-12-01" $requestBody -verbose
```

## <a name="view-the-response"></a>Yanıtı görüntüleyin

Aşağıdaki örnek, önceki komuttan döndürülen yanıt ' dir. Gruplar halinde ayrılmış sanal makine üzerinde etkili ve uygulanan güvenlik kuralları sonuçları göster **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, ve **EffectiveSecurityRules**.

```json

{
  "networkInterfaces": [
    {
      "securityRuleAssociations": {
        "networkInterfaceAssociation": {
          "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkInterfaces/{nicName}",
          "securityRules": [
            {
              "name": "default-allow-rdp",
              "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkSecurityGroups/{nsgName}/securityRules/default-allow-rdp",
              "etag": "W/\"d4c411d4-0d62-49dc-8092-3d4b57825740\"",
              "properties": {
                "provisioningState": "Succeeded",
                "protocol": "TCP",
                "sourcePortRange": "*",
                "destinationPortRange": "3389",
                "sourceAddressPrefix": "*",
                "destinationAddressPrefix": "*",
                "access": "Allow",
                "priority": 1000,
                "direction": "Inbound"
              }
            }
          ]
        },
        "defaultSecurityRules": [
          {
            "name": "AllowVnetInBound",
            "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkSecurityGroups/{nsgName}/defaultSecurityRules/",
            "properties": {
              "provisioningState": "Succeeded",
              "description": "Allow inbound traffic from all VMs in VNET",
              "protocol": "*",
              "sourcePortRange": "*",
              "destinationPortRange": "*",
              "sourceAddressPrefix": "VirtualNetwork",
              "destinationAddressPrefix": "VirtualNetwork",
              "access": "Allow",
              "priority": 65000,
              "direction": "Inbound"
            }
          },
          ...
        ],
        "effectiveSecurityRules": [
          {
            "name": "DefaultOutboundDenyAll",
            "protocol": "All",
            "sourcePortRange": "0-65535",
            "destinationPortRange": "0-65535",
            "sourceAddressPrefix": "*",
            "destinationAddressPrefix": "*",
            "access": "Deny",
            "priority": 65500,
            "direction": "Outbound"
          },
          ...
        ]
      }
    }
  ]
}
```

## <a name="next-steps"></a>Sonraki adımlar

Ziyaret [denetim ağ güvenlik grupları (NSG) Ağ İzleyicisi ile](network-watcher-security-group-view-powershell.md) ağ güvenlik grupları doğrulanması otomatikleştirmek öğrenmek için.


