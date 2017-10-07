---
title: "Azure Ağ İzleyicisi güvenlik grubu görünümü - Azure CLI 2.0 ile aaaAnalyze ağ güvenliği | Microsoft Docs"
description: "Bu makalede, Azure CLI 2.0 toouse tooanalyze sanal bir güvenlik grubu görünümü ile güvenliği nasıl makineleri anlatmaktadır."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: a986ff4f-7e0c-4994-95e1-4ac824986500
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 31a4cd628f54d7548f495251fd275f099e79a060
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-your-virtual-machine-security-with-security-group-view-using-azure-cli-20"></a>Güvenlik grubu Azure CLI 2.0 kullanarak görünümü ile sanal makine güvenliğinizi Çözümle

> [!div class="op_single_selector"]
> - [PowerShell](network-watcher-security-group-view-powershell.md)
> - [CLI 1.0](network-watcher-security-group-view-cli-nodejs.md)
> - [CLI 2.0](network-watcher-security-group-view-cli.md)
> - [REST API](network-watcher-security-group-view-rest.md)

Güvenlik grubu görünümü uygulanan tooa sanal makine yapılandırılmış ve etkili ağ güvenlik kuralları döndürür. Bu özellik kullanışlı tooaudit ve ağ güvenlik grupları tanılama ve bir VM tooensure trafiğinde yapılandırılmış kuralları yükleniyor doğru şekilde izin verilen veya reddedilen. Bu makalede, tooretrieve hello nasıl yapılandırılacağı ve Azure CLI kullanarak etkin güvenlik kuralları tooa sanal makine gösteriyoruz


Bu makalede bizim nesil CLI hello kaynak yönetimi dağıtım modeli için Azure CLI 2.0, Windows, Mac ve Linux için kullanılabilir olduğu kullanır.

Bu makaledeki adımları tooperform Merhaba, çok ihtiyacınız[hello Azure komut satırı arabirimi Mac, Linux ve Windows (Azure CLI) için yükleme](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).

## <a name="before-you-begin"></a>Başlamadan önce

Bu senaryo zaten izlediğiniz hello adımlarda varsayar [bir Ağ İzleyicisi oluşturma](network-watcher-create.md) toocreate bir Ağ İzleyicisi.

## <a name="scenario"></a>Senaryo

Bu makalede ele alınan hello senaryo yapılandırılmış hello ve belirli bir sanal makine için etkili güvenlik kurallarını alır.

## <a name="get-a-vm"></a>VM Al

Gerekli toorun hello bir sanal makinedir `vm list` cmdlet'i. Merhaba aşağıdaki komut bir kaynak grubunda hello sanal makineleri listeler:

```azurecli
az vm list -resource-group resourceGroupName
```

Merhaba sanal makine öğrendikten sonra hello kullanabilirsiniz `vm show` cmdlet tooget kendi kaynak kimliği:

```azurecli
az vm show -resource-group resourceGroupName -name virtualMachineName
```

## <a name="retrieve-security-group-view"></a>Güvenlik grubu görünümü alma

Merhaba sonraki tooretrieve hello güvenlik grubu Görünüm sonucu adımdır.

```azurecli
az network watcher show-security-group-view --resource-group resourceGroupName --vm vmName
```

## <a name="viewing-hello-results"></a>Merhaba sonuçları görüntüleme

Merhaba aşağıdaki kısaltılmış bir yanıt döndürdü hello sonuçlarının bir örnektir. Merhaba sonuçları tüm hello etkili ve uygulanan güvenlik kuralları hello sanal makineye gruplar halinde ayrıntılarıyla Göster **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, ve  **EffectiveSecurityRules**.

```json
{
  "networkInterfaces": [
    {
      "id": "/subscriptions/00000000-0000-0000-0000-0000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkInterfaces/{nicName}",
      "resourceGroup": "{resourceGroupName}",
      "securityRuleAssociations": {
        "defaultSecurityRules": [
          {
            "access": "Allow",
            "description": "Allow inbound traffic from all VMs in VNET",
            "destinationAddressPrefix": "VirtualNetwork",
            "destinationPortRange": "*",
            "direction": "Inbound",
            "etag": null,
            "id": "/subscriptions/00000000-0000-0000-0000-0000000000000/resourceGroups//providers/Microsoft.Network/networkSecurityGroups/{nsgName}/defaultSecurityRules/AllowVnetInBound",
            "name": "AllowVnetInBound",
            "priority": 65000,
            "protocol": "*",
            "provisioningState": "Succeeded",
            "resourceGroup": "",
            "sourceAddressPrefix": "VirtualNetwork",
            "sourcePortRange": "*"
          }...
        ],
        "effectiveSecurityRules": [
          {
            "access": "Deny",
            "destinationAddressPrefix": "*",
            "destinationPortRange": "0-65535",
            "direction": "Outbound",
            "expandedDestinationAddressPrefix": null,
            "expandedSourceAddressPrefix": null,
            "name": "DefaultOutboundDenyAll",
            "priority": 65500,
            "protocol": "All",
            "sourceAddressPrefix": "*",
            "sourcePortRange": "0-65535"
          },
          {
            "access": "Allow",
            "destinationAddressPrefix": "VirtualNetwork",
            "destinationPortRange": "0-65535",
            "direction": "Outbound",
            "expandedDestinationAddressPrefix": [
              "10.1.0.0/24",
              "168.63.129.16/32"
            ],
            "expandedSourceAddressPrefix": [
              "10.1.0.0/24",
              "168.63.129.16/32"
            ],
            "name": "DefaultRule_AllowVnetOutBound",
            "priority": 65000,
            "protocol": "All",
            "sourceAddressPrefix": "VirtualNetwork",
            "sourcePortRange": "0-65535"
          },...
        ],
        "networkInterfaceAssociation": {
          "id": "/subscriptions/00000000-0000-0000-0000-0000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkInterfaces/{nicName}",
          "resourceGroup": "{resourceGroupName}",
          "securityRules": [
            {
              "access": "Allow",
              "description": null,
              "destinationAddressPrefix": "*",
              "destinationPortRange": "3389",
              "direction": "Inbound",
              "etag": "W/\"efb606c1-2d54-475a-ab20-da3f80393577\"",
              "id": "/subscriptions/00000000-0000-0000-0000-0000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkSecurityGroups/{nsgName}/securityRules/default-allow-rdp",
              "name": "default-allow-rdp",
              "priority": 1000,
              "protocol": "TCP",
              "provisioningState": "Succeeded",
              "resourceGroup": "{resourceGroupName}",
              "sourceAddressPrefix": "*",
              "sourcePortRange": "*"
            }
          ]
        },
        "subnetAssociation": null
      }
    }
  ]
}
```

## <a name="next-steps"></a>Sonraki adımlar

Ziyaret [denetim ağ güvenlik grupları (NSG) Ağ İzleyicisi ile](network-watcher-nsg-auditing-powershell.md) toolearn nasıl tooautomate doğrulama ağ güvenlik grupları.

Şu adresi ziyaret ederek uygulanan tooyour ağ kaynaklarına olan hello güvenlik kuralları hakkında daha fazla bilgi [güvenlik grubu Görünümü'ne genel bakış](network-watcher-security-group-view-overview.md)
