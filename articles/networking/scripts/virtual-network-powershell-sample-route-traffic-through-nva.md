---
title: "aaaAzure PowerShell komut dosyası örneği - rota trafiği ağ sanal gereç aracılığıyla | Microsoft Docs"
description: "Azure PowerShell komut dosyası örneği - güvenlik duvarı ağ sanal gereç yoluyla trafiği yönlendirme."
services: virtual-network
documentationcenter: virtual-network
author: georgewallace
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: powershell
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 05/16/2017
ms.author: gwallace
ms.openlocfilehash: 3b999f3289d654c00d5becb973e2883896457d52
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="route-traffic-through-a-network-virtual-appliance"></a>Bir ağ sanal gereç yoluyla trafiği yönlendirme

Bu komut dosyası örneği ön uç ve arka uç alt ağları ile bir sanal ağ oluşturur. Ayrıca hello iki alt ağlar arasında etkin tooroute trafiğinin iletme IP ile VM oluşturur. Merhaba komut dosyasını çalıştırdıktan sonra bir güvenlik duvarı uygulaması toohello VM gibi ağ yazılım dağıtabilirsiniz.

Gerekirse, Azure PowerShell hello yönerge kullanarak bulunan hello hello yükleyin [Azure PowerShell Kılavuzu](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/)ve ardından çalıştırın `Login-AzureRmAccount` toocreate Azure ile bir bağlantı.

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Örnek komut dosyası


[!code-powershell[main](../../../powershell_scripts/virtual-network/route-traffic-through-nva/route-traffic-through-nva.ps1 "Route traffic through a network virtual appliance")]

## <a name="clean-up-deployment"></a>Dağıtımı temizleme 

Çalışma hello aşağıdaki tooremove hello kaynak grubu, VM ve tüm ilişkili kaynakları komutu.

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```
## <a name="script-explanation"></a>Komut dosyası açıklaması

Bu komut dosyası komutları toocreate aşağıdaki hello bir kaynak grubu, sanal ağ ve ağ güvenlik grupları kullanır. Her komut hello tablosundaki toocommand özgü belgeleri bağlar.

| Komut | Notlar |
|---|---|
| [Yeni-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup)  | Tüm kaynaklar depolandığı bir kaynak grubu oluşturur. |
| [Yeni-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | Bir Azure sanal ağı ve ön uç alt ağı oluşturur. |
| [AzureRmVirtualNetworkSubnetConfig yeni](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | Arka uç ve DMZ alt ağlar oluşturur. |
| [AzureRmPublicIpAddress yeni](/powershell/module/azurerm.network/new-azurermpublicipaddress) | Ortak IP adresi tooaccess hello VM Internet hello oluşturur. |
| [AzureRmNetworkInterface yeni](/powershell/module/azurerm.network/new-azurermnetworkinterface) | Bir sanal ağ arabirimi ve onu için IP iletimini etkinleştirme oluşturur. |
| [AzureRmNetworkSecurityGroup yeni](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | Bir ağ güvenlik grubu (NSG) oluşturur. |
| [AzureRmNetworkSecurityRuleConfig yeni](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | HTTP ve HTTPS bağlantı noktalarını toohello VM gelene izin ver NSG kuralları oluşturur. |
| [Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig)| Nsg'ler ilişkilendirilmiş bir hello ve rota toosubnets tabloları. |
| [AzureRmRouteTable yeni](/powershell/module/azurerm.network/new-azurermroutetable)| Tüm yollar için yol tablosu oluşturur. |
| [AzureRMRouteConfig yeni](/powershell/module/azurerm.network/new-azurermrouteconfig)| Yollar tooroute trafiği alt ağlar arasında ve hello Internet üzerinden hello VM oluşturur. |
| [Yeni-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) | Bir sanal makine oluşturur ve hello NIC tooit ekler. Bu komut ayrıca hello sanal makine görüntü toouse ve yönetici kimlik bilgilerini belirtir. |
| [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup)  | Bir kaynak grubu ve içerdiği tüm kaynakları siler. |

## <a name="next-steps"></a>Sonraki adımlar

Hello Azure PowerShell hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](https://docs.microsoft.com/powershell/azure/overview).

Ek ağ PowerShell komut dosyası örnekleri hello bulunabilir [Azure ağ genel görünümü belgelerine](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).
