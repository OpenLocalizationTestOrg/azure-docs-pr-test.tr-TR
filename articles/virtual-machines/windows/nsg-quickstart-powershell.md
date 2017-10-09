---
title: "aaaOpen bağlantı noktalarını tooa Azure PowerShell kullanarak bir VM | Microsoft Docs"
description: "Bilgi nasıl tooopen bir bağlantı noktası / bir uç nokta tooyour Windows VM oluşturma hello Azure Kaynak Yöneticisi dağıtım modu ve Azure PowerShell kullanma"
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: cf45f7d8-451a-48ab-8419-730366d54f1e
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 08/21/2017
ms.author: iainfou
ms.openlocfilehash: c1817a0c447ae4ce7a1ce2a1fc6927bedf2dacb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooopen-ports-and-endpoints-tooa-vm-in-azure-using-powershell"></a>Nasıl tooopen bağlantı noktalarını ve uç noktaları tooa PowerShell kullanarak azure'da VM
[!INCLUDE [virtual-machines-common-nsg-quickstart](../../../includes/virtual-machines-common-nsg-quickstart.md)]

## <a name="quick-commands"></a>Hızlı komutlar
toocreate bir ağ güvenlik grubu ve ACL kurallarını ihtiyacınız [Azure PowerShell'in yüklü en son sürümünü hello](/powershell/azureps-cmdlets-docs). Ayrıca [hello Azure portal kullanarak aşağıdaki adımları gerçekleştirin](nsg-quickstart-portal.md).

Azure hesabı tooyour oturum:

```powershell
Login-AzureRmAccount
```

Hello aşağıdaki örneklerde, örnek parametre adları kendi değerlerinizle değiştirin. Örnek parametre adları dahil *myResourceGroup*, *myNetworkSecurityGroup*, ve *myVnet*.

Bir kural oluştururken [yeni AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig). Merhaba aşağıdaki örnek adlı bir kural oluşturur *myNetworkSecurityGroupRule* tooallow *tcp* bağlantı noktasında trafik *80*:

```powershell
$httprule = New-AzureRmNetworkSecurityRuleConfig `
    -Name "myNetworkSecurityGroupRule" `
    -Description "Allow HTTP" `
    -Access "Allow" `
    -Protocol "Tcp" `
    -Direction "Inbound" `
    -Priority "100" `
    -SourceAddressPrefix "Internet" `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 80
```

Ardından, ağ güvenlik grubu ile oluşturma [yeni AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) ve yeni oluşturduğunuz gibi Ata hello HTTP kural. Merhaba aşağıdaki örnekte oluşturur adlı bir ağ güvenlik grubu *myNetworkSecurityGroup*:

```powershell
$nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName "myResourceGroup" `
    -Location "EastUS" `
    -Name "myNetworkSecurityGroup" `
    -SecurityRules $httprule
```

Şimdi şimdi ağ güvenlik grubu tooa alt ağınızı atayın. Merhaba aşağıdaki örnek atar adlı varolan bir sanal ağ *myVnet* toohello değişkeni *$vnet* ile [Get-AzureRmVirtualNetwork](/powershell/module/azurerm.network/get-azurermvirtualnetwork):

```powershell
$vnet = Get-AzureRmVirtualNetwork `
    -ResourceGroupName "myResourceGroup" `
    -Name "myVnet"
```

Ağ güvenlik grubu, alt ağ ile ilişkilendirmek [kümesi AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig). Merhaba aşağıdaki örnek ilişkilendirir adlı hello alt *mySubnet* ağ güvenlik grubu ile:

```powershell
$subnetPrefix = $vnet.Subnets|?{$_.Name -eq 'mySubnet'}

Set-AzureRmVirtualNetworkSubnetConfig `
    -VirtualNetwork $vnet `
    -Name "mySubnet" `
    -AddressPrefix $subnetPrefix.AddressPrefix `
    -NetworkSecurityGroup $nsg
```

Son olarak, sanal ağınızla güncelleştirme [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork) sırada, değişiklikleri tootake efekti için:

```powershell
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```


## <a name="more-information-on-network-security-groups"></a>Ağ güvenlik grupları hakkında daha fazla bilgi
Burada hızlı komutları Hello tooget yukarı ve trafik boyunca tooyour VM ile çalışmaya izin verir. Ağ güvenlik grupları, birçok harika özellikler ve denetleme tooyour kaynaklara erişmek için ayrıntı düzeyi sağlar. Daha fazla bilgi edinebilirsiniz [bir ağ güvenlik grubu ve ACL oluşturma kuralları burada](tutorial-virtual-network.md#manage-internal-traffic).

Yüksek oranda kullanılabilir web uygulamaları için Azure yük dengeleyici arkasında Vm'leriniz yerleştirmeniz gerekir. Merhaba yük dengeleyici trafik filtreleme sağlar bir ağ güvenlik grubuyla trafiği tooVMs dağıtır. Daha fazla bilgi için bkz: [nasıl tooload Bakiye Linux sanal yüksek oranda kullanılabilir bir uygulama içinde Azure toocreate makineleri](tutorial-load-balancer.md).

## <a name="next-steps"></a>Sonraki adımlar
Bu örnekte, bir basit kural tooallow HTTP trafiği oluşturuldu. Aşağıdaki makaleleri hello ayrıntılı ortamları oluşturma hakkında bilgi bulabilirsiniz:

* [Azure Resource Manager'a genel bakış](../../azure-resource-manager/resource-group-overview.md)
* [Ağ Güvenlik Grubu (NSG) Nedir?](../../virtual-network/virtual-networks-nsg.md)
* [Yük Dengeleyiciler için Azure Resource Manager'a genel bakış](../../load-balancer/load-balancer-arm.md)

