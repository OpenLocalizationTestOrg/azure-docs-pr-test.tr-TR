---
title: "PowerShell komut dosyası örneği - aaaAzure Yük Dengelemesi Azure PowerShell ile birden çok Web siteleri | Microsoft Docs"
description: "Azure PowerShell Betiği örnek - yük dengelemesi birden çok Web siteleri toohello aynı sanal makine"
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
ms.openlocfilehash: 316818964eb6928fe4163ef69eb7f05da2dc9636
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="load-balance-multiple-websites"></a>Yük Dengelemesi birden çok Web sitesi

Bu komut dosyası örneği iki sanal bir kullanılabilirlik kümesi üyesi olan makinelerle (VM) bir sanal ağ oluşturur. Bir yük dengeleyici iki ayrı trafiğini yönlendiren IP adresleri toohello iki VM'ler. Sonra çalışan hello komut dosyası, web sunucusu yazılım toohello VM'ler dağıtın ve her biri kendi IP adresiyle birden çok web sitesini barındırmak.

Gerekirse, Azure PowerShell hello yönerge kullanarak bulunan hello hello yükleyin [Azure PowerShell Kılavuzu](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/)ve ardından çalıştırın `Login-AzureRmAccount` toocreate Azure ile bir bağlantı.

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Örnek komut dosyası

[!code-powershell[main](../../../powershell_scripts/load-balancer/load-balance-multiple-web-sites-vm/load-balance-multiple-web-sites-vm.ps1  "Load balance multiple web sites")]

## <a name="clean-up-deployment"></a>Dağıtımı temizleme 

Çalışma hello aşağıdaki tooremove hello kaynak grubu, VM ve tüm ilişkili kaynakları komutu.

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a>Komut dosyası açıklaması

Bu komut dosyası toocreate bir kaynak grubu, sanal ağ, yük dengeleyici ve tüm ilişkili kaynakları komutları aşağıdaki hello kullanır. Her komut hello tablosundaki toocommand belirli belgeleri bağlar.

| Komut | Notlar |
|---|---|
| [Yeni-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) | Tüm kaynaklar depolandığı bir kaynak grubu oluşturur. |
| [AzureRmAvailabilitySet yeni](/powershell/module/azurerm.compute/new-azurermavailabilityset) | Bir Azure kullanılabilirlik kümesi tooprovide yüksek kullanılabilirlik oluşturur. |
| [AzureRmVirtualNetworkSubnetConfig yeni](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | Bir alt ağ yapılandırması oluşturur. Bu yapılandırma ile Merhaba sanal ağ oluşturma işleminde kullanılır. |
| [Yeni-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | Sanal ağ oluşturur. |
| [AzureRmPublicIpAddress yeni](/powershell/module/azurerm.network/new-azurermpublicipaddress) | Bir ortak IP adresi oluşturur. |
| [AzureRmLoadBalancerFrontendIpConfig yeni](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig) | Bir yük dengeleyici için bir ön uç IP yapılandırması oluşturur. |
| [AzureRmLoadBalancerBackendAddressPoolConfig yeni](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig) | Bir yük dengeleyici için arka uç adres havuzu yapılandırması oluşturur. |
| [AzureRmLoadBalancerProbeConfig yeni](/powershell/module/azurerm.network/new-azurermloadbalancerprobeconfig) | Bir NLB araştırması oluşturur. Bir NLB araştırması hello NLB kümesindeki her bir VM kullanılan toomonitor değil. Tüm VM erişilemez hale gelirse, trafik yönlendirilmiş toohello VM değildir. |
| [AzureRmLoadBalancerRuleConfig yeni](/powershell/module/azurerm.network/new-azurermloadbalancerruleconfig) | Bir NLB kuralı oluşturur. Bu örnekte, bağlantı noktası 80 için bir kural oluşturulur. HTTP trafiği NLB hello sırasında ulaştığında, yönlendirilmiş tooport 80 olur hello VM'ler hello NLB kümesindeki biri. |
| [AzureRmLoadBalancer yeni](/powershell/module/azurerm.network/new-azurermloadbalancer) | Bir yük dengeleyici oluşturur. |
| [AzureRmNetworkInterfaceIpConfig yeni](/powershell/module/azurerm.network/new-azurermnetworkinterfaceipconfig) | Bir sanal ağ arabirimi için gelişmiş özelliklerini tanımlar. |
| [AzureRmNetworkInterface yeni](/powershell/module/azurerm.network/new-azurermnetworkinterface) | Bir ağ arabirimi oluşturur. |
| [AzureRmVMConfig yeni](/powershell/module/azurerm.compute/new-azurermvmconfig) | Bir VM yapılandırması oluşturur. Bu yapılandırma VM adı, işletim sistemi ve yönetici kimlik bilgileri gibi bilgileri içerir. Merhaba yapılandırma VM oluşturma sırasında kullanılır. |
| [Yeni-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) | Bir sanal makine oluşturun. |
|[Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | Bir kaynak grubu ve içerdiği tüm kaynaklar kaldırır. |

## <a name="next-steps"></a>Sonraki adımlar

Hello Azure PowerShell hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](https://docs.microsoft.com/powershell/azure/overview).

Ek ağ PowerShell komut dosyası örnekleri hello bulunabilir [Azure ağ genel görünümü belgelerine](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).
