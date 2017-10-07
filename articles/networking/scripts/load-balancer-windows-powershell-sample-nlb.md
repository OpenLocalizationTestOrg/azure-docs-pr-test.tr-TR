---
title: "PowerShell komut dosyası örneği - yüksek kullanılabilirlik için Yük Dengeleme trafik tooVMs aaaAzure | Microsoft Docs"
description: "Azure PowerShell Betiği örnek - yüksek kullanılabilirlik için Yük Dengeleme trafiği tooVMs"
services: load-balancer
documentationcenter: load-balancer
author: georgewallace
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: load-balancer
ms.devlang: powershell
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 05/16/2017
ms.author: gwallace
ms.openlocfilehash: 332c39e1aad071ca6f7ce420ccc1f423ef647d2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="load-balance-traffic-toovms-for-high-availability"></a>Bakiye trafiği tooVMs yüksek kullanılabilirlik için yük

Bu komut dosyası örneği gereken her şeyi oluşturur toorun birkaç Windows sanal makineleri yüksek oranda kullanılabilir yapılandırılmış ve yük dengeli yapılandırma. Çalışan hello betik sonra üç sanal makineler, birleştirilmiş tooan Azure kullanılabilirlik kümesi, sahip olur ve bir Azure yük dengeleyici üzerinden erişilebilir.

Gerekirse, Azure PowerShell hello yönerge kullanarak bulunan hello hello yükleyin [Azure PowerShell Kılavuzu](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/)ve ardından çalıştırın `Login-AzureRmAccount` toocreate Azure ile bir bağlantı.

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Örnek komut dosyası

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-nlb/create-vm-nlb.ps1 "Quick Create VM")]

## <a name="clean-up-deployment"></a>Dağıtımı temizleme 

Çalışma hello aşağıdaki tooremove hello kaynak grubu, VM ve tüm ilişkili kaynakları komutu.

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a>Komut dosyası açıklaması

Bu komut dosyası komutları toocreate bir kaynak grubu, sanal makine, kullanılabilirlik kümesi, yük dengeleyici ve tüm ilgili kaynaklar aşağıdaki hello kullanır. Her komut hello tablosundaki toocommand belirli belgeleri bağlar.

| Komut | Notlar |
|---|---|
| [Yeni-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) | Tüm kaynaklar depolandığı bir kaynak grubu oluşturur. |
| [AzureRmVirtualNetworkSubnetConfig yeni](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | Bir alt ağ yapılandırması oluşturur. Bu yapılandırma ile Merhaba sanal ağ oluşturma işleminde kullanılır. |
| [Yeni-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | Bir Azure sanal ağ ve alt ağ oluşturur. |
| [AzureRmPublicIpAddress yeni](/powershell/module/azurerm.network/new-azurermpublicipaddress)  | Bir ortak IP adresi statik bir IP adresi ve ilişkili bir DNS adı ile oluşturur. |
| [AzureRmLoadBalancer yeni](/powershell/module/azurerm.network/new-azurermloadbalancer)  | Bir Azure yük dengeleyici oluşturur. |
| [AzureRmLoadBalancerProbeConfig yeni](/powershell/module/azurerm.network/new-azurermloadbalancerprobeconfig) | Bir yük dengeleyici araştırması oluşturur. Yük Dengeleyici araştırmasını hello yük dengeleyici kümesindeki her bir VM kullanılan toomonitor değil. Tüm VM erişilemez hale gelirse, trafik yönlendirilmiş toohello VM değildir. |
| [AzureRmLoadBalancerRuleConfig yeni](/powershell/module/azurerm.network/new-azurermloadbalancerruleconfig) | Bir yük dengeleyici kuralı oluşturur. Bu örnekte, bağlantı noktası 80 için bir kural oluşturulur. HTTP trafiği hello yük dengeleyicide ulaştığında, yönlendirilmiş tooport 80 olur hello VM'ler hello yük dengeleyici kümesindeki biri. |
| [AzureRmLoadBalancerInboundNatRuleConfig yeni](/powershell/module/azurerm.network/new-azurermloadbalancerinboundnatruleconfig) | Yük Dengeleyici ağ adresi çevirisi (NAT) kuralı oluşturur.  NAT kuralları bir bağlantı noktasının hello yük dengeleyici tooa bir VM'de eşleyin. Bu örnekte, hello yük dengeleyici kümesindeki SSH trafiği tooeach VM için NAT kuralı oluşturulur.  |
| [AzureRmNetworkSecurityGroup yeni](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | Merhaba Internet ve hello sanal makine arasında bir güvenlik sınırı olan bir ağ güvenlik grubu (NSG) oluşturur. |
| [AzureRmNetworkSecurityRuleConfig yeni](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | Bir NSG kural tooallow oluşturur gelen trafiği. Bu örnekte, bağlantı noktası 22 SSH trafiği için açıldı. |
| [AzureRmNetworkInterface yeni](/powershell/module/azurerm.network/new-azurermnetworkinterface) | Bir sanal ağ kartı oluşturur ve toohello sanal ağ, alt ağ ve NSG ekler. |
| [AzureRmAvailabilitySet yeni](/powershell/module/azurerm.compute/new-azurermavailabilityset) | Bir kullanılabilirlik kümesi oluşturur. Kullanılabilirlik kümeleri, sağlayacak şekilde hello kümesinin tamamını değil hatası oluşursa, etkilenen hello sanal makineler arasında fiziksel kaynakları yayarak uygulama çalışma süresi emin olun. |
| [AzureRmVMConfig yeni](/powershell/module/azurerm.compute/new-azurermvmconfig) | Bir VM yapılandırması oluşturur. Bu yapılandırma VM adı, işletim sistemi ve yönetici kimlik bilgileri gibi bilgileri içerir. Merhaba yapılandırma VM oluşturma sırasında kullanılır. |
| [Yeni-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm)  | Merhaba sanal makine oluşturur ve toohello ağ kartı, sanal ağ, alt ağ ve NSG bağlanır. Bu komut ayrıca kullanılan hello sanal makine görüntü toobe belirtir ve yönetici kimlik bilgileri.  |
| [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | Tüm iç içe kaynaklar dahil olmak üzere bir kaynak grubu siler. |

## <a name="next-steps"></a>Sonraki adımlar

Hello Azure PowerShell hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](https://docs.microsoft.com/powershell/azure/overview).

Ek ağ PowerShell komut dosyası örnekleri hello bulunabilir [Azure ağ genel görünümü belgelerine](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).
