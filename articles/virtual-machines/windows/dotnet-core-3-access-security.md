---
title: "aaaAccess Azure Şablonları Windows VM'ler için güvenlik ve | Microsoft Docs"
description: "Azure sanal makinesi DotNet çekirdek Öğreticisi"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: e671fc45-5e4d-40fd-aac5-290892713cc0
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 4b8227ae745b3b0a22d136e98d18479f8b1504c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="access-and-security-in-azure-resource-manager-templates-for-windows-vms"></a>Azure Resource Manager Şablonları Windows VM'ler için güvenlik ve erişim

Barındırılan uygulamalarını Azure büyük olasılıkla toobe erişmeniz içinde hello internet veya VPN / Azure ile hızlı Rota bağlantısı. Merhaba müzik deposu uygulama örnekle hello web sitesi üzerinde kullanılabilir hale Internet bir ortak IP adresi ile Merhaba. Oluşturulan erişimle bağlantıları toohello uygulama ve erişim toohello sanal makine kaynakları kendilerini güvenli hale getirilmelidir. Bu erişim güvenliği bir ağ güvenlik grubu ile sağlanır. 

Bu belge hello müzik deposu uygulama hello örnek Azure Resource Manager şablonunda güvenliği nasıl ayrıntıları verilmektedir. Tüm bağımlılıkları ve benzersiz yapılandırmaları vurgulanır. Merhaba en iyi deneyim için önceden hello çözüm tooyour Azure aboneliği ve hello Azure Resource Manager şablonu ile birlikte çalışma örneği dağıtın. Merhaba tam şablon burada – bulunabilir [müzik deposu dağıtım Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).

## <a name="public-ip-address"></a>Genel IP adresi
tooprovide genel erişim tooan Azure kaynak, bir ortak IP adresi kaynağı kullanılabilir. Genel IP adresi statik veya dinamik IP adresi ile yapılandırılabilir. Bir dinamik adres kullanılır ve hello sanal makine durdurulmuş ve serbest, hello adresleri kaldırılır. Merhaba makine yeniden başlatıldığında, farklı bir ortak IP adresi atanmış. tooprevent bir IP adresini değiştirmesini, ayrılmış bir IP adresi kullanılabilir. 

Bir ortak IP adresi tooan Azure Resource Manager şablonu hello Visual Studio ekleme yeni kaynak Sihirbazı kullanılarak eklenebilir veya bir şablona geçerli JSON ekleyerek. 

Bu bağlantıyı toosee hello JSON örnek hello Resource Manager şablonu içinde– izleyin [genel IP adresi](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L110).

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/publicIPAddresses",
  "name": "[variables('publicIpAddressName')]",
  "location": "[resourceGroup().location]",
  "dependsOn": [],
  "tags": {
    "displayName": "public-ip"
  },
  "properties": {
    "publicIPAllocationMethod": "Dynamic",
    "dnsSettings": {
      "domainNameLabel": "[parameters('publicipaddressDnsName')]"
    }
  }
}
```

Bir ortak IP adresi, bir sanal ağ bağdaştırıcısı veya bir yük dengeleyici ile ilişkili olabilir. Merhaba müzik deposu Web sitesi birden fazla sanal makine genelinde dengelendiği olduğundan bu örnekte, ekli toohello yük dengeleyici hello genel IP adresi değildir.

Bu bağlantıyı toosee hello JSON örnek hello Resource Manager şablonu içinde– izleyin [yük dengeleyici genel IP adresi ilişkilendirmesini](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L211).

```json
"frontendIPConfigurations": [
  {
    "properties": {
      "publicIPAddress": {
        "id": "[resourceId('Microsoft.Network/publicIPAddresses', variables('publicIpAddressName'))]"
      }
    },
    "name": "LoadBalancerFrontend"
  }
]
```

Merhaba ortak IP adresi olarak hello Azure portal görülür. Merhaba genel IP adresi ilişkili tooa yük dengeleyicisi ve sanal makine olduğuna dikkat edin. Ağ Yük Dengeleyici hello sonraki bu seri belgede ayrıntılı olarak belirtilir.

![Genel IP adresi](./media/dotnet-core-3-access-security/pubip-win.png)

Azure ortak IP adresleri hakkında daha fazla bilgi için bkz: [azure'daki IP adresleri](../../virtual-network/virtual-network-ip-addresses-overview-arm.md).

## <a name="network-security-group"></a>Ağ güvenlik grubu
Erişim kurulan tooAzure kaynakları silindikten sonra bu erişim sınırlandırılmalıdır. Azure sanal makineler için bir ağ güvenlik grubu kullanılarak güvenli erişim elde edilir. Merhaba müzik deposu uygulama örneği ile tüm erişim toohello sanal makine http erişimi için bağlantı noktası 80 ve RDP erişim 3389 numaralı bağlantı noktası üzerinden dışında sınırlıdır. Bir ağ güvenlik grubu tooan Azure Resource Manager şablonu hello Visual Studio ekleme yeni kaynak Sihirbazı kullanılarak eklenebilir veya bir şablona geçerli JSON ekleyerek.

Bu bağlantıyı toosee hello JSON örnek hello Resource Manager şablonu içinde– izleyin [ağ güvenlik grubu](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L57).

```json
{
  "apiVersion": "2016-03-30",
  "type": "Microsoft.Network/networkSecurityGroups",
  "name": "[variables('networkSecurityGroup')]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "network-security-group"
  },
  "properties": {
    "securityRules": [
      {
        "name": "http",
        "properties": {
          "description": "http endpoint",
          "protocol": "Tcp",
          "sourcePortRange": "*",
          "destinationPortRange": "80",
          "sourceAddressPrefix": "*",
          "destinationAddressPrefix": "*",
          "access": "Allow",
          "priority": 100,
          "direction": "Inbound"
        }
      },
      ........<truncated> 
    ]
  }
},
```

Bu örnekte, hello ağ güvenlik grubu hello sanal ağ kaynak bildirilen hello alt ağ nesnesini ilişkilendirmek ' dir. 

Bu bağlantıyı toosee hello JSON örnek hello Resource Manager şablonu içinde– izleyin [sanal ağ ile ağ güvenlik grubu ilişkilendirmesini](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L143).

```json
"subnets": [
  {
    "name": "[variables('subnetName')]",
    "properties": {
      "addressPrefix": "10.0.0.0/24",
      "networkSecurityGroup": {
        "id": "[resourceId('Microsoft.Network/networkSecurityGroups', variables('networkSecurityGroup'))]"
      }
    }
  }
]
```

İşte hangi hello ağ güvenlik grubu gibi hello Azure portalında görünür. Bir NSG'yi bir alt ağ veya ağ arabirimi ile ilişkilendirmek dikkat edin. Bu durumda, hello NSG ilişkili tooa alt değil. Bu yapılandırmada, hello gelen kuralları tooall bağlı sanal makineleri toohello alt uygulayın.

![Ağ güvenlik grubu](./media/dotnet-core-3-access-security/nsg-win.png)

Ağ güvenlik grupları hakkında ayrıntılı bilgi için bkz: [bir ağ güvenlik grubu nedir](https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/).

## <a name="next-step"></a>Sonraki adım
<hr>

[3. adım - kullanılabilirliğini ve ölçeğini Azure Resource Manager şablonlarındaki](dotnet-core-4-availability-scale.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

