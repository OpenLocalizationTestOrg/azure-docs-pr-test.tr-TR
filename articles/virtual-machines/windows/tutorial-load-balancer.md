---
title: aaaHow tooload dengelemek azure'da Windows sanal makineler | Microsoft Docs
description: "Nasıl toouse hello Azure yük dengeleyici toocreate yüksek oranda kullanılabilir ve güvenli bir uygulama üç Windows VM'ler üzerindeki bilgi edinin"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 08/11/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: bfbd6a24e90a33e60d7d4f7b0c471af5d4e71f45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooload-balance-windows-virtual-machines-in-azure-toocreate-a-highly-available-application"></a>Nasıl tooload Bakiye Azure toocreate Windows sanal makinesi yüksek oranda kullanılabilir bir uygulama
Yük Dengeleme, birden çok sanal makine genelinde gelen istekleri yayarak daha yüksek düzeyde kullanılabilirlik sağlar. Bu öğreticide, trafiği dağıtmak ve yüksek kullanılabilirlik sağlamak hello farklı bileşenler hello Azure yük dengeleyici hakkında bilgi edinin. Aşağıdakileri nasıl yapacağınızı öğrenirsiniz:

> [!div class="checklist"]
> * Bir Azure yük dengeleyici oluşturma
> * Bir yük dengeleyici durum araştırması oluştur
> * Yük Dengeleyici trafiği kuralları oluşturma
> * Merhaba özel betik uzantısının toocreate temel IIS site kullanın
> * Sanal makineler oluşturmak ve tooa yük dengeleyici ekleme
> * Bir yük dengeleyici eylemde görüntüleyin
> * Ekleme ve sanal makineleri yük dengeleyiciden kaldırın

Bu öğretici hello Azure PowerShell modülü 3,6 veya sonraki bir sürümü gerektiriyor. Çalıştırma ` Get-Module -ListAvailable AzureRM` toofind hello sürümü. Tooupgrade gerekirse bkz [yükleme Azure PowerShell Modülü](/powershell/azure/install-azurerm-ps).


## <a name="azure-load-balancer-overview"></a>Azure yük dengeleyici genel bakış
Bir Azure yük dengeleyici gelen trafiği sağlıklı VM'ler arasında dağıtarak yüksek kullanılabilirlik sağlayan bir katman 4 (TCP, UDP) yük dengeleyicidir. Bir yük dengeleyici durum araştırması her VM üzerinde belirli bir bağlantı noktasını izler ve yalnızca trafik tooan dağıtır işletimsel VM.

Bir veya daha fazla ortak IP adreslerini içeren bir ön uç IP yapılandırmasını tanımlayın. Bu ön uç IP yapılandırmasını yük dengeleyici ve uygulamaları toobe hello Internet erişilebilir sağlar. 

Sanal makineler tooa yük dengeleyici, sanal ağ arabirim kartı (NIC) kullanarak bağlanın. toodistribute trafiği toohello VM'ler, bir arka uç adres havuzu hello sanal (NIC) bağlı toohello yük dengeleyici hello IP adreslerini içerir.

toocontrol hello akış trafiği belirli bağlantı noktalarını ve tooyour VM'ler eşleme protokolleri için yük dengeleyici kuralları tanımlayın.


## <a name="create-azure-load-balancer"></a>Azure yük dengeleyici oluşturma
Bu bölümde, nasıl oluşturma ve her bileşenin hello yük dengeleyicinin yapılandırma ayrıntıları. Yük Dengeleyici oluşturmadan önce bir kaynak grubuyla oluşturmanız [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup). Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu *myResourceGroupLoadBalancer* hello içinde *EastUS* konumu:

```powershell
New-AzureRmResourceGroup `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS
```

### <a name="create-a-public-ip-address"></a>Genel IP adresi oluşturma
tooaccess uygulamanıza Internet Merhaba, hello yük dengeleyici için bir ortak IP adresi gerekir. Bir ortak IP adresiyle oluşturma [yeni AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress). Merhaba aşağıdaki örnekte oluşturur adlı ortak IP adresi *myPublicIP* hello içinde *myResourceGroupLoadBalancer* kaynak grubu:

```powershell
$publicIP = New-AzureRmPublicIpAddress `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS `
  -AllocationMethod Static `
  -Name myPublicIP
```

### <a name="create-a-load-balancer"></a>Yük dengeleyici oluşturma
Bir ön uç IP adresiyle oluşturma [yeni AzureRmLoadBalancerFrontendIpConfig](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig). Merhaba aşağıdaki örnekte oluşturur adlı bir ön uç IP adresi *myFrontEndPool*: 

```powershell
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig `
  -Name myFrontEndPool `
  -PublicIpAddress $publicIP
```

Olan bir arka uç adres havuzu oluşturma [yeni AzureRmLoadBalancerBackendAddressPoolConfig](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig). Merhaba aşağıdaki örnekte oluşturur adlı arka uç adres havuzu *myBackEndPool*:

```powershell
$backendPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name myBackEndPool
```

Şimdi, hello yük dengeleyici ile oluşturmak [yeni AzureRmLoadBalancer](/powershell/module/azurerm.network/new-azurermloadbalancer). Merhaba aşağıdaki örnek adlı bir yük dengeleyici oluşturur *myLoadBalancer* hello kullanarak *myPublicIP* adresi:

```powershell
$lb = New-AzureRmLoadBalancer `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Name myLoadBalancer `
  -Location EastUS `
  -FrontendIpConfiguration $frontendIP `
  -BackendAddressPool $backendPool
```

### <a name="create-a-health-probe"></a>Bir sistem durumu araştırması oluştur
tooallow hello yük dengeleyici toomonitor hello durumu, uygulamanızın bir sistem durumu araştırması kullanın. Merhaba durumu araştırması dinamik olarak ekler veya kendi yanıt toohealth denetimleri temel hello yük dengeleyici döndürme VM'ler kaldırır. Varsayılan olarak, bir VM hello yük dengeleyici dağıtımı 15 saniyelik aralıklarda iki ardışık hatadan sonra kaldırılır. Bir protokol veya belirli bir sistem onay sayfasında uygulamanız için temel bir sistem durumu araştırması oluşturun. 

Aşağıdaki örnek hello bir TCP araştırması oluşturur. Daha fazla hassas sistem durumu denetimlerinin özel HTTP araştırmalara de oluşturabilirsiniz. Özel bir HTTP araştırma kullanırken, hello sistem durumu onay sayfasında, aşağıdaki gibi oluşturmalısınız *healthcheck.aspx*. Merhaba araştırma döndürmelidir bir **HTTP 200 Tamam** hello yük dengeleyici tookeep hello ana döndürme yanıtı.

toocreate TCP durumu araştırması, kullandığınız [Ekle AzureRmLoadBalancerProbeConfig](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig). Merhaba aşağıdaki örnek adlı bir sistem durumu araştırması oluşturur *myHealthProbe* her VM izler:

```powershell
Add-AzureRmLoadBalancerProbeConfig `
  -Name myHealthProbe `
  -LoadBalancer $lb `
  -Protocol tcp `
  -Port 80 `
  -IntervalInSeconds 15 `
  -ProbeCount 2
```

Merhaba yük dengeleyici ile güncelleştirme [kümesi AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer):

```powershell
Set-AzureRmLoadBalancer -LoadBalancer $lb
```

### <a name="create-a-load-balancer-rule"></a>Yük Dengeleyici kuralı oluşturma
Yük Dengeleyici kuralı kullanılan toodefine olduğu dağıtılmış toohello VM'ler nasıl trafiğidir. Merhaba ön uç IP yapılandırmasını hello gelen trafiği ve hello arka uç IP havuzu tooreceive hello trafiği için hello gerekli kaynak ve hedef bağlantı noktası ile birlikte tanımlayın. toomake trafiği yalnızca sağlıklı VM'ler aldığınızdan emin, aynı zamanda hello sistem durumu araştırma toouse tanımlar.

Yük Dengeleyici kuralı ile oluşturma [Ekle AzureRmLoadBalancerRuleConfig](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig). Merhaba aşağıdaki örnek adlı bir yük dengeleyici kuralı oluşturur *myLoadBalancerRule* ve bağlantı noktası üzerinde trafiği dengeler *80*:

```powershell
$probe = Get-AzureRmLoadBalancerProbeConfig -LoadBalancer $lb -Name myHealthProbe

Add-AzureRmLoadBalancerRuleConfig `
  -Name myLoadBalancerRule `
  -LoadBalancer $lb `
  -FrontendIpConfiguration $lb.FrontendIpConfigurations[0] `
  -BackendAddressPool $lb.BackendAddressPools[0] `
  -Protocol Tcp `
  -FrontendPort 80 `
  -BackendPort 80 `
  -Probe $probe
```

Merhaba yük dengeleyici ile güncelleştirme [kümesi AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer):

```powershell
Set-AzureRmLoadBalancer -LoadBalancer $lb
```


## <a name="configure-virtual-network"></a>Sanal ağ yapılandırma
Bazı sanal makineleri dağıtmak ve, dengeleyici sınayabilirsiniz önce sanal ağ kaynaklarına destekleme hello oluşturun. Sanal ağlar hakkında daha fazla bilgi için bkz: Merhaba [Azure Sanal Ağları Yönet](tutorial-virtual-network.md) Öğreticisi.

### <a name="create-network-resources"></a>Ağ kaynakları oluşturun
Bir sanal ağ ile oluşturma [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork). Merhaba aşağıdaki örnek adlı bir sanal ağ oluşturur *myVnet* ile *mySubnet*:

```powershell
# Create subnet config
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
  -Name mySubnet `
  -AddressPrefix 192.168.1.0/24

# Create hello virtual network
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS `
  -Name myVnet `
  -AddressPrefix 192.168.0.0/16 `
  -Subnet $subnetConfig
```

Ağ güvenlik grubu kural oluştururken [yeni AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig), bir ağ güvenlik grubu oluşturma [yeni AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup). Merhaba ağ güvenlik grubu toohello olan bir alt ağ Ekle [kümesi AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig) ve hello sanal ağ ile güncelleştirme [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork). 

Merhaba aşağıdaki örnekte oluşturur adlı bir ağ güvenlik grubu kural *myNetworkSecurityGroup* ve çok geçerlidir*mySubnet*:

```powershell
# Create security rule config
$nsgRule = New-AzureRmNetworkSecurityRuleConfig `
  -Name myNetworkSecurityGroupRule `
  -Protocol Tcp `
  -Direction Inbound `
  -Priority 1001 `
  -SourceAddressPrefix * `
  -SourcePortRange * `
  -DestinationAddressPrefix * `
  -DestinationPortRange 80 `
  -Access Allow

# Create hello network security group
$nsg = New-AzureRmNetworkSecurityGroup `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS `
  -Name myNetworkSecurityGroup `
  -SecurityRules $nsgRule

# Apply hello network security group tooa subnet
Set-AzureRmVirtualNetworkSubnetConfig `
  -VirtualNetwork $vnet `
  -Name mySubnet `
  -NetworkSecurityGroup $nsg `
  -AddressPrefix 192.168.1.0/24

# Update hello virtual network
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```

Sanal NIC ile oluşturulan [yeni AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface). Merhaba aşağıdaki örnek üç sanal NIC oluşturur. (Bir sanal NIC aşağıdaki hello uygulamanızda adımları için oluşturduğunuz her VM için). Ek sanal NIC ve sanal makineleri herhangi bir zamanda oluşturmak ve bunları toohello yük dengeleyici Ekle:

```powershell
for ($i=1; $i -le 3; $i++)
{
   New-AzureRmNetworkInterface `
     -ResourceGroupName myResourceGroupLoadBalancer `
     -Name myNic$i `
     -Location EastUS `
     -Subnet $vnet.Subnets[0] `
     -LoadBalancerBackendAddressPool $lb.BackendAddressPools[0]
}
```

## <a name="create-virtual-machines"></a>Sanal makineler oluşturma
tooimprove hello yüksek kullanılabilirlik, uygulamanızın bir kullanılabilirlik kümesine Vm'leriniz yerleştirin.

Kullanılabilirlik kümesi oluştur [yeni AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset). Merhaba aşağıdaki örnekte oluşturur kullanılabilirlik adlandırılmış kümesi *myAvailabilitySet*:

```powershell
$availabilitySet = New-AzureRmAvailabilitySet `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Name myAvailabilitySet `
  -Location EastUS `
  -Managed `
  -PlatformFaultDomainCount 3 `
  -PlatformUpdateDomainCount 2
```

Yönetici olan hello VM'ler için kullanıcı adı ve parola ayarlayın [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):

```powershell
$cred = Get-Credential
```

Merhaba VM'ler ile oluşturduğunuz artık [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm). Aşağıdaki örnek hello üç VM'ler oluşturur:

```powershell
for ($i=1; $i -le 3; $i++)
{
  $vm = New-AzureRmVMConfig `
    -VMName myVM$i `
    -VMSize Standard_D1 `
    -AvailabilitySetId $availabilitySet.Id
  $vm = Set-AzureRmVMOperatingSystem `
    -VM $vm `
    -Windows `
    -ComputerName myVM$i `
    -Credential $cred `
    -ProvisionVMAgent `
    -EnableAutoUpdate
  $vm = Set-AzureRmVMSourceImage `
    -VM $vm `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter `
    -Version latest
  $vm = Set-AzureRmVMOSDisk `
    -VM $vm `
    -Name myOsDisk$i `
    -DiskSizeInGB 128 `
    -CreateOption FromImage `
    -Caching ReadWrite
  $nic = Get-AzureRmNetworkInterface `
    -ResourceGroupName myResourceGroupLoadBalancer `
    -Name myNic$i
  $vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
  New-AzureRmVM `
    -ResourceGroupName myResourceGroupLoadBalancer `
    -Location EastUS `
    -VM $vm
}
```

Birkaç dakika toocreate alır ve tüm üç VM'ler yapılandırın.

### <a name="install-iis-with-custom-script-extension"></a>Özel betik uzantısı ile IIS yükleme
Önceki bir öğretici içinde [nasıl toocustomize Windows sanal makine](tutorial-automate-vm-deployment.md), nasıl özel betik uzantısı için Windows hello tooautomate VM özelleştirmesiyle öğrendiniz. Merhaba kullanabilirsiniz aynı tooinstall yaklaşmak ve IIS Vm'leriniz yapılandırın.

Kullanım [kümesi AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) tooinstall hello özel betik uzantısı. Merhaba uzantısı çalışır `powershell Add-WindowsFeature Web-Server` tooinstall hello IIS Web sunucusu ve ardından güncelleştirmeleri hello *Default.htm* sayfa tooshow hello hello VM konak adı:

```powershell
for ($i=1; $i -le 3; $i++)
{
   Set-AzureRmVMExtension `
     -ResourceGroupName myResourceGroupLoadBalancer `
     -ExtensionName IIS `
     -VMName myVM$i `
     -Publisher Microsoft.Compute `
     -ExtensionType CustomScriptExtension `
     -TypeHandlerVersion 1.4 `
     -SettingString '{"commandToExecute":"powershell Add-WindowsFeature Web-Server; powershell Add-Content -Path \"C:\\inetpub\\wwwroot\\Default.htm\" -Value $($env:computername)"}' `
     -Location EastUS
}
```

## <a name="test-load-balancer"></a>Test yük dengeleyici
Merhaba, yük dengeleyici ile genel IP adresi elde [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress). Merhaba aşağıdaki örnek alacağı için başlangıç IP adresi *myPublicIP* daha önce oluşturduğunuz:

```powershell
Get-AzureRmPublicIPAddress `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Name myPublicIP | select IpAddress
```

Ardından tooa web tarayıcısında hello genel IP adresi girebilirsiniz. Merhaba Web sitesi gösterilir, hello VM hello hostname dahil olmak üzere bu hello yük dengeleyici trafiği tooas aşağıdaki örneğine hello içinde dağıtılmış:

![Çalışan IIS Web sitesi](./media/tutorial-load-balancer/running-iis-website.png)

toosee hello yük dengeleyici, uygulamanızı çalıştıran tüm üç VM'ler arasında trafiği dağıtmak, zorla web tarayıcınızı yenileme.


## <a name="add-and-remove-vms"></a>Sanal makineleri ekleyip
Merhaba işletim sistemi güncelleştirmelerini yükleme gibi uygulamanızı çalıştıran VM'ler tooperform bakım gerekebilir. toodeal trafiğinin artmasına tooyour uygulamayla ihtiyacınız olabilecek tooadd ilave VM'ler. Bu bölümde, nasıl gösterilir tooremove veya VM hello yük dengeleyiciden ekleyin.

### <a name="remove-a-vm-from-hello-load-balancer"></a>Bir VM hello yük dengeleyiciden kaldırın
Merhaba ağ arabirimi kartı ile [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface), ardından kümesi hello *LoadBalancerBackendAddressPools* özelliği hello sanal NIC çok*$null*. Son olarak, sanal NIC hello güncelleştirin:

```powershell
$nic = Get-AzureRmNetworkInterface `
    -ResourceGroupName myResourceGroupLoadBalancer `
    -Name myNic2
$nic.Ipconfigurations[0].LoadBalancerBackendAddressPools=$null
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

toosee hello yük dengeleyici iki kalan hello arasında trafiği dağıtmak uygulamanızı çalıştıran VM'ler, zorla web tarayıcınızı yenileme. Merhaba işletim sistemi güncelleştirmeleri yükleme veya VM yeniden başlatma gerçekleştirme gibi VM üzerinde bakım artık gerçekleştirebilirsiniz.

### <a name="add-a-vm-toohello-load-balancer"></a>Bir VM toohello yük dengeleyici ekleme
Sonra VM bakım yapmak veya tooexpand kapasitesine ihtiyacınız varsa, hello ayarlayın *LoadBalancerBackendAddressPools* hello sanal NIC toohello özelliğinin *BackendAddressPool* gelen [ Get-AzureRMLoadBalancer](/powershell/module/azurerm.network/get-azurermloadbalancer):

Merhaba yük dengeleyici alın:

```powershell
$lb = Get-AzureRMLoadBalancer `
    -ResourceGroupName myResourceGroupLoadBalancer `
    -Name myLoadBalancer 
$nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$lb.BackendAddressPools[0]
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide, bir yük dengeleyici oluşturulur ve sanal makineleri tooit bağlı. Şunları öğrendiniz:

> [!div class="checklist"]
> * Bir Azure yük dengeleyici oluşturma
> * Bir yük dengeleyici durum araştırması oluştur
> * Yük Dengeleyici trafiği kuralları oluşturma
> * Merhaba özel betik uzantısının toocreate temel IIS site kullanın
> * Sanal makineler oluşturmak ve tooa yük dengeleyici ekleme
> * Bir yük dengeleyici eylemde görüntüleyin
> * Ekleme ve sanal makineleri yük dengeleyiciden kaldırın

Toohello sonraki öğretici toolearn nasıl ilerlemek toomanage VM ağı.

> [!div class="nextstepaction"]
> [VM’leri ve sanal ağları yönetme](./tutorial-virtual-network.md)
