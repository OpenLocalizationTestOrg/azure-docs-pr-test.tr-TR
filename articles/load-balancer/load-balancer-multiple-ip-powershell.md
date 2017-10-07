---
title: "birden çok IP yapılandırmaları Azure Dengeleme aaaLoad | Microsoft Docs"
description: "Birincil ve ikincil IP yapılandırmaları yükdengeleme"
services: load-balancer
documentationcenter: na
author: anavinahar
manager: narayan
editor: na
ms.assetid: 244907cd-b275-4494-aaf7-dcfc4d93edfe
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/16/2017
ms.author: annahar
ms.openlocfilehash: fe1cdb317350942ff759229491c2025e98dd24a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="load-balancing-on-multiple-ip-configurations-using-powershell"></a>PowerShell kullanarak birden fazla IP yapılandırması üzerinde yükdengeleme

> [!div class="op_single_selector"]
> * [Portal](load-balancer-multiple-ip.md)
> * [CLI](load-balancer-multiple-ip-cli.md)
> * [PowerShell](load-balancer-multiple-ip-powershell.md)

Bu makalede, nasıl bir ikincil ağ arabirimi (NIC) toouse Azure yük dengeleyici ile birden çok IP adresleri açıklanmaktadır. Bu senaryo için Windows, her birincil ve ikincil bir NIC ile çalışan iki VM sahibiz Her ikincil hello NIC'lerin iki IP yapılandırmaları vardır. Her VM Web siteleri contoso.com ve fabrikam.com barındırır. İlişkili tooone hello IP yapılandırmalarının hello ikincil NIC üzerinde her Web sitesi olan Azure yük dengeleyici tooexpose iki ön uç IP adresi, her bir Web sitesi, toodistribute trafiği toohello ilgili IP hello Web sitesinin yapılandırması için bir tane kullanırız. Bu senaryoda hem ön uçlar yanı sıra arasında her iki arka uç havuzu IP adreslerini hello aynı bağlantı noktası numarası kullanır.

![LB senaryo görüntüsü](./media/load-balancer-multiple-ip/lb-multi-ip.PNG)

## <a name="steps-tooload-balance-on-multiple-ip-configurations"></a>Adımları tooload bakiyesi birden fazla IP yapılandırması

Bu makalede açıklanan tooachieve hello senaryo Hello adımları izleyin:

1. Azure PowerShell'i yükleyin. Bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview) hello Azure PowerShell'in en son sürümünü yükleme, aboneliğinizi seçme ve tooyour hesabında imzalama hakkında bilgi.
2. Ayarları aşağıdaki hello kullanarak bir kaynak grubu oluşturun:

    ```powershell
    $location = "westcentralus".
    $myResourceGroup = "contosofabrikam"
    ```

    Daha fazla bilgi için bkz: 2. adım [bir kaynak grubu oluşturmak](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).

3. [Bir kullanılabilirlik kümesi oluşturmak](../virtual-machines/windows/tutorial-availability-sets.md?toc=%2fazure%2fload-balancer%2ftoc.json) toocontain Vm'leriniz. Bu senaryo için komutu aşağıdaki hello kullan:

    ```powershell
    New-AzureRmAvailabilitySet -ResourceGroupName "contosofabrikam" -Name "myAvailset" -Location "West Central US"
    ```

4. 5'te 3 adımları yönergeleri izleyin [bir Windows VM oluşturma](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json) makalesi tek bir NIC ile VM tooprepare hello oluşturma 6.1 adımı yürütme ve 6.2 adım yerine hello aşağıdakileri kullanın:

    ```powershell
    $availset = Get-AzureRmAvailabilitySet -ResourceGroupName "contosofabrikam" -Name "myAvailset"
    New-AzureRmVMConfig -VMName "VM1" -VMSize "Standard_DS1_v2" -AvailabilitySetId $availset.Id
    ```

    Daha sonra tamamlamak [bir Windows VM oluşturma](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json) 6,8 aracılığıyla 6.3 adımları.

5. Merhaba VM'ler, ikinci bir IP yapılandırması tooeach ekleyin. Merhaba yönergeleri izleyin [toovirtual makineleri birden çok IP adresi atamak](../virtual-network/virtual-network-multiple-ip-addresses-powershell.md#add) makalesi. Yapılandırma ayarları aşağıdaki hello kullan:

    ```powershell
    $NicName = "VM1-NIC2"
    $RgName = "contosofabrikam"
    $NicLocation = "West Central US"
    $IPConfigName4 = "VM1-ipconfig2"
    $Subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "mySubnet" -VirtualNetwork $myVnet
    ```

    Bu öğreticinin hello amaçla tooassociate hello ikincil IP yapılandırmaları olan ve genel IP'ler gerekmez. Hello komutu tooremove hello ortak IP ilişkilendirme bölümünü düzenleyin.

6. 4. adım, bu makalenin 6-VM2 için yeniden tamamlayın. Bunun yapılması emin tooreplace hello VM adı tooVM2 olabilir. Merhaba toocreate bir sanal ağ gerekmez Not ikinci VM. Kullanım durumunu temel alarak yeni bir alt ağ oluşturamaz veya olabilir.

7. İki ortak IP adresi oluşturun ve bunları gösterildiği gibi hello uygun değişkenlerde saklayın:

    ```powershell
    $publicIP1 = New-AzureRmPublicIpAddress -Name PublicIp1 -ResourceGroupName contosofabrikam -Location 'West Central US' -AllocationMethod Dynamic -DomainNameLabel contoso
    $publicIP2 = New-AzureRmPublicIpAddress -Name PublicIp2 -ResourceGroupName contosofabrikam -Location 'West Central US' -AllocationMethod Dynamic -DomainNameLabel fabrikam

    $publicIP1 = Get-AzureRmPublicIpAddress -Name PublicIp1 -ResourceGroupName contosofabrikam
    $publicIP2 = Get-AzureRmPublicIpAddress -Name PublicIp2 -ResourceGroupName contosofabrikam
    ```

8. İki ön uç IP yapılandırması oluşturun:

    ```powershell
    $frontendIP1 = New-AzureRmLoadBalancerFrontendIpConfig -Name contosofe -PublicIpAddress $publicIP1
    $frontendIP2 = New-AzureRmLoadBalancerFrontendIpConfig -Name fabrikamfe -PublicIpAddress $publicIP2
    ```

9. Arka uç adres havuzu, bir araştırma ve Yük Dengeleme kuralları oluşturun:

    ```powershell
    $beaddresspool1 = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name contosopool
    $beaddresspool2 = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name fabrikampool

    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name HTTP -RequestPath 'index.html' -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2

    $lbrule1 = New-AzureRmLoadBalancerRuleConfig -Name HTTPc -FrontendIpConfiguration $frontendIP1 -BackendAddressPool $beaddresspool1 -Probe $healthprobe -Protocol Tcp -FrontendPort 80 -BackendPort 80
    $lbrule2 = New-AzureRmLoadBalancerRuleConfig -Name HTTPf -FrontendIpConfiguration $frontendIP2 -BackendAddressPool $beaddresspool2 -Probe $healthprobe -Protocol Tcp -FrontendPort 80 -BackendPort 80
    ```

10. Oluşturulan bu kaynakları oluşturduktan sonra yük dengeleyicisi oluşturun:

    ```powershell
    $mylb = New-AzureRmLoadBalancer -ResourceGroupName contosofabrikam -Name mylb -Location 'West Central US' -FrontendIpConfiguration $frontendIP1 -LoadBalancingRule $lbrule -BackendAddressPool $beAddressPool -Probe $healthProbe
    ```

11. Merhaba ikinci arka uç adres havuzu ve ön uç IP yapılandırması tooyour yeni oluşturulan yük dengeleyici ekleyin:

    ```powershell
    $mylb = Get-AzureRmLoadBalancer -Name "mylb" -ResourceGroupName $myResourceGroup | Add-AzureRmLoadBalancerBackendAddressPoolConfig -Name fabrikampool | Set-AzureRmLoadBalancer

    $mylb | Add-AzureRmLoadBalancerFrontendIpConfig -Name fabrikamfe -PublicIpAddress $publicIP2 | Set-AzureRmLoadBalancer
    
    Add-AzureRmLoadBalancerRuleConfig -Name HTTP -LoadBalancer $mylb -FrontendIpConfiguration $frontendIP2 -BackendAddressPool $beaddresspool2 -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 80 | Set-AzureRmLoadBalancer
    ```

12. Aşağıdaki Hello komutları hello NIC'ler alın ve her ikincil NIC toohello arka uç adres havuzu Merhaba, her iki IP yapılandırmalarını yük dengeleyici ekleyin:

    ```powershell
    $nic1 = Get-AzureRmNetworkInterface -Name "VM1-NIC2" -ResourceGroupName "MyResourcegroup";
    $nic2 = Get-AzureRmNetworkInterface -Name "VM2-NIC2" -ResourceGroupName "MyResourcegroup";

    $nic1.IpConfigurations[0].LoadBalancerBackendAddressPools.Add($mylb.BackendAddressPools[0]);
    $nic1.IpConfigurations[1].LoadBalancerBackendAddressPools.Add($mylb.BackendAddressPools[1]);
    $nic2.IpConfigurations[0].LoadBalancerBackendAddressPools.Add($mylb.BackendAddressPools[0]);
    $nic2.IpConfigurations[1].LoadBalancerBackendAddressPools.Add($mylb.BackendAddressPools[1]);

    $mylb = $mylb | Set-AzureRmLoadBalancer

    $nic1 | Set-AzureRmNetworkInterface
    $nic2 | Set-AzureRmNetworkInterface
    ```

13. Son olarak, DNS kaynak kayıtlarını toopoint toohello ilgili ön uç IP adresi hello yük dengeleyici için yapılandırmanız gerekir. Azure DNS'de etki alanlarınızı barındırabilir. Azure DNS yük dengeleyici ile kullanma hakkında daha fazla bilgi için bkz: [kullanarak Azure DNS diğer Azure hizmetleriyle](../dns/dns-for-azure-services.md).

## <a name="next-steps"></a>Sonraki adımlar
- Nasıl toocombine Yük Dengeleme Azure hizmetleri hakkında daha fazla bilgi [Azure'da Yük Dengeleme hizmetlerini kullanarak](../traffic-manager/traffic-manager-load-balancing-azure.md).
- Nasıl günlükleri farklı türlerde içinde Azure toomanage kullanın ve yük dengeleyici sorun giderme öğrenin [analytics Azure yük dengeleyici için oturum](../load-balancer/load-balancer-monitor-log.md).
