---
title: "Sanal makine ölçek aaaCreating ayarlar PowerShell cmdlet'lerini kullanarak | Microsoft Docs"
description: "Oluşturma ve İlk Azure sanal makine ölçek Azure PowerShell cmdlet'lerini kullanarak kümelerinizi yönetme kullanmaya başlama"
services: virtual-machines-windows
documentationcenter: 
author: danielsollondon
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 430d9d64-1f35-48f0-a4fd-9b69910ffa59
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/21/2017
ms.author: danielsollondon
ms.openlocfilehash: 7979be367d04c904b60d78849c1b751a52cc8caf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-virtual-machine-scale-sets-using-powershell-cmdlets"></a>PowerShell cmdlet'leri kullanılarak sanal makine ölçek kümeleri oluşturma
Bu makalede nasıl toocreate (VMSS) bir sanal makine ölçek kümesi örnek anlatılmaktadır. İlişkili ağ ve depolama ile üç düğümü ölçek kümesi oluşturur.

## <a name="first-steps"></a>İlk adımlar
Merhaba yüklü en son Azure PowerShell modülü vardır, toomake hello PowerShell cmdlet'leri sahip olduğunuzdan emin toomaintain gereken ve ölçek kümeleri oluşturma emin olun.
Toohello komut satırı araçları Git [burada](http://aka.ms/webpi-azps) hello en son kullanılabilir Azure modüller.

toofind VMSS ilgili cmdlet'leri, hello arama dizesi kullanın \*VMSS\*. Örneğin, _gcm *vmss*_

## <a name="creating-a-vmss"></a>Bir VMSS oluşturma
#### <a name="create-resource-group"></a>Kaynak Grubu oluşturma
```
$loc = 'westus';
$rgname = 'mynewrgwu';
  New-AzureRmResourceGroup -Name $rgname -Location $loc -Force;
```

### <a name="create-networking-vnet--subnet"></a>Ağ oluşturma (VNET / alt ağ)
#### <a name="subnet-specification"></a>Alt ağ belirtimi
```
$subnetName = 'websubnet'
  $subnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix "10.0.0.0/24";
```

#### <a name="vnet-specification"></a>VNET belirtimi
```
$vnet = New-AzureRmVirtualNetwork -Force -Name ('vnet' + $rgname) -ResourceGroupName $rgname -Location $loc -AddressPrefix "10.0.0.0/16" -Subnet $subnet;
$vnet = Get-AzureRmVirtualNetwork -Name ('vnet' + $rgname) -ResourceGroupName $rgname;

# In this case assume hello new subnet is hello only one
$subnetId = $vnet.Subnets[0].Id;
```

#### <a name="create-public-ip-resource-tooallow-external-access"></a>Genel IP kaynağı tooAllow dış erişim oluşturma
Bu yük dengeleyici ilişkili toohello olacaktır.

```
$pubip = New-AzureRmPublicIpAddress -Force -Name ('pubip' + $rgname) -ResourceGroupName $rgname -Location $loc -AllocationMethod Dynamic -DomainNameLabel ('pubip' + $rgname);
$pubip = Get-AzureRmPublicIpAddress -Name ('pubip' + $rgname) -ResourceGroupName $rgname;
```

#### <a name="create-load-balancer"></a>Yük Dengeleyici oluşturma
```
$frontendName = 'fe' + $rgname
$backendAddressPoolName = 'bepool' + $rgname
$probeName = 'vmssprobe' + $rgname
$inboundNatPoolName = 'innatpool' + $rgname
$lbruleName = 'lbrule' + $rgname
$lbName = 'vmsslb' + $rgname

# Bind Public IP tooLoad Balancer
$frontend = New-AzureRmLoadBalancerFrontendIpConfig -Name $frontendName -PublicIpAddress $pubip
```

#### <a name="configure-load-balancer"></a>Yük Dengeleyici yapılandırma
Arka uç adres havuzu yapılandırma oluşturabilir, bu hello ölçek kümesinde hello VM'ler hello NIC tarafından paylaşılır.

```
$backendAddressPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name $backendAddressPoolName
```

Yük dengeli sonda bağlantı noktası kümesi, uygulamanız için uygun şekilde hello ayarlarını değiştirin.

```
$probe = New-AzureRmLoadBalancerProbeConfig -Name $probeName -RequestPath healthcheck.aspx -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2
```

Doğrudan yönlendirilmiş bağlantı (yükü dengelenmiş) için bir gelen NAT havuzu oluşturma toohello VM'ler hello ölçeğinde yük dengeleyici hello ayarlayın. Bu RDP kullanarak toodemonstrate ve uygulamanızda gerekli değildir.

```
$frontendpoolrangestart = 3360
$frontendpoolrangeend = 3370
$backendvmport = 3389
$inboundNatPool = New-AzureRmLoadBalancerInboundNatPoolConfig -Name $inboundNatPoolName -FrontendIPConfigurationId `
$frontend.Id -Protocol Tcp -FrontendPortRangeStart $frontendpoolrangestart -FrontendPortRangeEnd $frontendpoolrangeend -BackendPort $backendvmport;
```

Merhaba yük dengeli kuralı gösterir yük önceki adımlardan hello ayarlarını kullanarak Dengeleme bağlantı noktası 80 isteklerini bu örnek oluşturun.

```
$protocol = 'Tcp'
$feLBPort = 80
$beLBPort = 80

$lbrule = New-AzureRmLoadBalancerRuleConfig -Name $lbruleName `
-FrontendIPConfiguration $frontend -BackendAddressPool $backendAddressPool `
-Probe $probe -Protocol $protocol -FrontendPort $feLBPort -BackendPort $beLBPort `
-IdleTimeoutInMinutes 15 -EnableFloatingIP -LoadDistribution SourceIP -Verbose;
```

Yük Dengeleyici yapılandırması ile oluşturun.

```
$actualLb = New-AzureRmLoadBalancer -Name $lbName -ResourceGroupName $rgname -Location $loc `
-FrontendIpConfiguration $frontend -BackendAddressPool $backendAddressPool `
-Probe $probe -LoadBalancingRule $lbrule -InboundNatPool $inboundNatPool -Verbose;
```

LB ayarlarını denetleyin, yük denetleyin dengeli bağlantı noktası yapılandırmaları, Not, görmezsiniz hello ölçek kümesindeki sanal makineleri hello kadar gelen NAT kuralları oluşturulur.

```
$expectedLb = Get-AzureRmLoadBalancer -Name $lbName -ResourceGroupName $rgname
```

##### <a name="configure-and-create-hello-scale-set"></a>Yapılandırma ve oluşturma hello ölçek kümesi
Not: Bu altyapı örnek nasıl tooset yukarı dağıtmak ve ölçek web trafiği hello ölçek kümesini ancak hello VM'ler burada belirtilen görüntüleri üzerinden yüklü hiçbir web Hizmetleri yok gösterir.

```
# specify scale set Name
$vmssName = 'vmss' + $rgname;

## specify VMSS specific details
$adminUsername = 'azadmin';
$adminPassword = "Password1234!";

$PublisherName = 'MicrosoftWindowsServer'
$Offer         = 'WindowsServer'
$Sku          = '2012-R2-Datacenter'
$Version       = 'latest'
$vmNamePrefix = 'winvmss'

###add an extension
$extname = 'BGInfo';
$publisher = 'Microsoft.Compute';
$exttype = 'BGInfo';
$extver = '2.1';
```

NIC tooLoad dengeleyici ve alt ağ bağlama

```
$ipCfg = New-AzureRmVmssIPConfig -Name 'nic' `
-LoadBalancerInboundNatPoolsId $actualLb.InboundNatPools[0].Id `
-LoadBalancerBackendAddressPoolsId $actualLb.BackendAddressPools[0].Id `
-SubnetId $subnetId;
```

Ölçeği oluşturmak set Config

```
# Specify number of nodes
$numberofnodes = 3

$vmss = New-AzureRmVmssConfig -Location $loc -SkuCapacity $numberofnodes -SkuName 'Standard_A2' -UpgradePolicyMode 'automatic' `
    | Add-AzureRmVmssNetworkInterfaceConfiguration -Name $subnetName -Primary $true -IPConfiguration $ipCfg `
    | Set-AzureRmVmssOSProfile -ComputerNamePrefix $vmNamePrefix -AdminUsername $adminUsername -AdminPassword $adminPassword `
    | Set-AzureRmVmssStorageProfile -OsDiskCreateOption 'FromImage' -OsDiskCaching 'None' `
    -ImageReferenceOffer $Offer -ImageReferenceSku $Sku -ImageReferenceVersion $Version `
    -ImageReferencePublisher $PublisherName `
    | Add-AzureRmVmssExtension -Name $extname -Publisher $publisher -Type $exttype -TypeHandlerVersion $extver -AutoUpgradeMinorVersion $true
```

Derleme ölçek kümesi yapılandırması

```
New-AzureRmVmss -ResourceGroupName $rgname -Name $vmssName -VirtualMachineScaleSet $vmss -Verbose;
```

Şimdi hello ölçek kümesini oluşturdunuz. Bağlantı toohello sınayabilirsiniz Bu örnekte, RDP kullanarak tek tek VM:

```
VM0 : pubipmynewrgwu.westus.cloudapp.azure.com:3360
VM1 : pubipmynewrgwu.westus.cloudapp.azure.com:3361
VM2 : pubipmynewrgwu.westus.cloudapp.azure.com:3362
```
