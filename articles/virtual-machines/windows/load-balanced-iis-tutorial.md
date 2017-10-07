---
title: "aaaTutorial - yapı yüksek oranda kullanılabilir bir uygulamayı Azure vm'lerde | Microsoft Docs"
description: "Bilgi nasıl toocreate Azure yük dengeleyici ile üç Windows VM'ler arasında yüksek oranda kullanılabilir ve güvenli bir uygulama"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 03/30/2017
ms.author: davidmu
ms.openlocfilehash: f9eff96be4f3999651c4108f0334e4eaa1a39c0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-load-balanced-highly-available-application-on-windows-virtual-machines-in-azure"></a>Bir yük dengeli, azure'da Windows sanal makinelerde yüksek oranda kullanılabilir uygulama oluşturma

Bu öğreticide, esnek toomaintenance olayı yüksek oranda kullanılabilir bir uygulama oluşturun. Merhaba uygulaması bir yük dengeleyici, bir kullanılabilirlik kümesi ve üç Windows sanal makineleri (VM'ler) kullanır. Bu öğretici IIS yükler, kullanabilirsiniz ancak farklı uygulama framework kullanarak Bu öğretici toodeploy hello aynı yüksek kullanılabilirlik bileşenleri ve yönergeleri. 

## <a name="step-1---azure-prerequisites"></a>1. adım - Azure önkoşulları

toocomplete Bu öğretici, hello son yüklediğinizden emin olun [Azure PowerShell](/powershell/azure/overview) modülü.

İlk olarak, tooyour hello Login-AzureRmAccount komutu Azure aboneliğiyle oturum ve hello ekrandaki yönergeleri izleyin.

```powershell
Login-AzureRmAccount
```

Azure kaynak grubu, Azure kaynaklarının dağıtıldığı ve yönetildiği bir mantıksal kapsayıcıdır. Diğer Azure kaynaklarına oluşturabilmeniz için önce bir kaynak grubu ile toocreate gerekir [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup). Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu `myResourceGroup` hello içinde `westeurope` bölge: 

```powershell
New-AzureRmResourceGroup -ResourceGroupName myResourceGroup -Location westeurope
```

## <a name="step-2---create-availability-set"></a>2. adım - kullanılabilirlik kümesi oluştur

Sanal makineler arasında mantıksal hataya oluşturulabilir ve güncelleme etki alanları. Her mantıksal bir etki alanı donanım hello temel Azure veri merkezinde bir bölümünü temsil eder. İki veya daha fazla sanal makine oluşturduğunuzda, işlem ve depolama kaynaklarınızı bu etki alanları arasında dağıtılır. Donanım bileşeni bakım gerekiyorsa bu dağıtım, uygulamanızın hello kullanılabilirlik tutar. Kullanılabilirlik kümeleri, bu mantıksal arıza ve güncelleştirme etki alanları tanımlamanıza olanak sağlar.

Kullanılabilirlik kümesi oluştur [yeni AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset). Merhaba aşağıdaki örnekte oluşturur kullanılabilirlik adlandırılmış kümesi `myAvailabilitySet`:

```powershell
$availabilitySet = New-AzureRmAvailabilitySet `
  -ResourceGroupName myResourceGroup `
  -Name myAvailabilitySet `
  -Location westeurope `
  -Managed `
  -PlatformFaultDomainCount 3 `
  -PlatformUpdateDomainCount 2
```

## <a name="step-3---create-load-balancer"></a>3. adım - oluşturma yük dengeleyici

Bir Azure yük dengeleyici trafiği yük dengeleyici kuralları kullanarak tanımlanan VM'ler kümesi arasında dağıtır. Bir sistem durumu araştırması her VM üzerinde belirli bir bağlantı noktasını izler ve yalnızca trafik tooan dağıtır işletimsel VM.

### <a name="create-public-ip-address"></a>Ortak IP adresi oluştur

tooaccess uygulamanızı hello Internet üzerinde bir ortak IP adresi toohello yük dengeleyici atayın. Bir ortak IP adresiyle oluşturma [yeni AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress). Merhaba aşağıdaki örnekte oluşturur adlı ortak IP adresi `myPublicIP`:

```powershell
$pip = New-AzureRmPublicIpAddress `
  -ResourceGroupName myResourceGroup `
  -Location westeurope `
  -AllocationMethod Static `
  -Name myPublicIP
```

### <a name="create-load-balancer"></a>Yük Dengeleyici oluşturma

Bir ön uç IP adresiyle oluşturma [yeni AzureRmLoadBalancerFrontendIpConfig](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig). Merhaba aşağıdaki örnekte oluşturur adlı bir ön uç IP adresi `myFrontEndPool`: 

```powershell
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig -Name myFrontEndPool -PublicIpAddress $pip
```

Olan bir arka uç adres havuzu oluşturma [yeni AzureRmLoadBalancerBackendAddressPoolConfig](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig). Merhaba aşağıdaki örnekte oluşturur adlı arka uç adres havuzu `myBackEndPool`:

```powershell
$backendPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name myBackEndPool
```

Şimdi, hello yük dengeleyici ile oluşturmak [yeni AzureRmLoadBalancer](/powershell/module/azurerm.network/new-azurermloadbalancer). Merhaba aşağıdaki örnek adlı bir yük dengeleyici oluşturur `myLoadBalancer` hello kullanarak `myPublicIP` adresi:

```powershell
$lb = New-AzureRmLoadBalancer `
  -ResourceGroupName myResourceGroup `
  -Name myLoadBalancer `
  -Location westeurope `
  -FrontendIpConfiguration $frontendIP `
  -BackendAddressPool $backendPool
```

### <a name="create-health-probe"></a>Sistem durumu araştırması oluştur

tooallow hello yük dengeleyici toomonitor hello durumu, uygulamanızın bir sistem durumu araştırması kullanın. Merhaba durumu araştırması dinamik olarak ekler veya kendi yanıt toohealth denetimleri temel hello yük dengeleyici döndürme VM'ler kaldırır. Varsayılan olarak, bir VM hello yük dengeleyici dağıtımı 15 saniyelik aralıklarda iki ardışık hatadan sonra kaldırılır.

Bir sistem durumu araştırması ile oluşturma [Ekle AzureRmLoadBalancerProbeConfig](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig). Merhaba aşağıdaki örnek adlı bir sistem durumu araştırması oluşturur `myHealthProbe` her VM izler:

```powershell
Add-AzureRmLoadBalancerProbeConfig -Name myHealthProbe `
  -LoadBalancer $lb `
  -Protocol tcp `
  -Port 80 `
  -IntervalInSeconds 15 `
  -ProbeCount 2
```

### <a name="create-load-balancer-rule"></a>Yük Dengeleyici kuralı oluşturma

Yük Dengeleyici kuralı kullanılan toodefine olduğu dağıtılmış toohello VM'ler nasıl trafiğidir.

Yük Dengeleyici kuralı ile oluşturma [Ekle AzureRmLoadBalancerRuleConfig](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig). Merhaba aşağıdaki örnek adlı bir yük dengeleyici kuralı oluşturur `myLoadBalancerRule` ve bağlantı noktası üzerinde trafiği dengeler `80`:

```powershell
Add-AzureRmLoadBalancerRuleConfig -Name myLoadBalancerRule `
  -LoadBalancer $lb `
  -FrontendIpConfiguration $lb.FrontendIpConfigurations[0] `
  -BackendAddressPool $lb.BackendAddressPools[0] `
  -Protocol Tcp `
  -FrontendPort 80 `
  -BackendPort 80
```

Merhaba yük dengeleyici ile güncelleştirme [kümesi AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer):

```powershell
Set-AzureRmLoadBalancer -LoadBalancer $lb
```

## <a name="step-4---configure-networking"></a>4. adım - ağ yapılandırma

Her bir VM sanal ağ tooa bağlanan bir veya daha fazla sanal ağ arabirim kartları (NIC) sahiptir. Bu sanal ağ tanımlanmış erişim kurallarına göre toofilter trafiği güvenli hale getirilir.

### <a name="create-virtual-network"></a>Sanal ağ oluşturma

İlk olarak, bir alt ağ ile yapılandırma [yeni AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig). Merhaba aşağıdaki örnek adlı bir alt ağı oluşturur `mySubnet`:

```powershell
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name mySubnet -AddressPrefix 192.168.1.0/24
```

tooprovide ağ bağlantısı tooyour VM oluşturma bir sanal ağ ile [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork). Merhaba aşağıdaki örnek adlı bir sanal ağ oluşturur `myVnet` ile `mySubnet`:

```powershell
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myResourceGroup `
  -Location westeurope `
  -Name myVnet `
  -AddressPrefix 192.168.0.0/16 `
  -Subnet $subnetConfig
```

### <a name="configure-network-security"></a>Ağ güvenliği yapılandırma

Bir Azure [ağ güvenlik grubu](../../virtual-network/virtual-networks-nsg.md) (NSG) bir veya daha çok sanal makineler için gelen ve giden trafik denetler. Ağ güvenlik grubu kurallarının izin verin veya belirli bir bağlantı noktası veya bağlantı noktası aralığı ağ trafiği engelle. Önceden tanımlanmış bir kaynakta kaynaklanan trafiğin yalnızca bir sanal makineyle iletişim kurabilmesi için bu kurallar kaynak adres öneki de içerir.

tooallow trafiği tooreach uygulamanızı web, bir ağ güvenlik grubu kural oluştururken [yeni AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig). Merhaba aşağıdaki örnekte oluşturur adlı bir ağ güvenlik grubu kural `myNetworkSecurityGroupRule`:

```powershell
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
```

Bir ağ güvenlik grubu oluşturma [yeni AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup). Merhaba aşağıdaki örnekte oluşturur adlı bir NSG `myNetworkSecurityGroup`:

```powershell
$nsg = New-AzureRmNetworkSecurityGroup `
  -ResourceGroupName myResourceGroup `
  -Location westeurope `
  -Name myNetworkSecurityGroup `
  -SecurityRules $nsgRule
```

Merhaba ağ güvenlik grubu toohello olan bir alt ağ Ekle [kümesi AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig):

```powershell
Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet `
  -Name mySubnet `
  -NetworkSecurityGroup $nsg `
  -AddressPrefix 192.168.1.0/24
```

Güncelleştirme hello sanal ağ ile [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork):

```powershell
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```

### <a name="create-virtual-network-interface-cards"></a>Sanal ağ arabirim kartları oluşturma

Yük Dengeleyici işlevi hello sanal NIC kaynakla yerine gerçek VM hello. Merhaba sanal NIC bağlı toohello yük dengeleyicinin ve tooa VM bağlı.

Bir sanal NIC ile oluşturma [yeni AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface). Merhaba aşağıdaki örnek üç sanal NIC oluşturur. (Bir sanal NIC aşağıdaki hello uygulamanızda adımları için oluşturduğunuz her VM için):


```powershell
for ($i=1; $i -le 3; $i++)
{
   New-AzureRmNetworkInterface -ResourceGroupName myResourceGroup `
     -Name myNic$i `
     -Location westeurope `
     -Subnet $vnet.Subnets[0] `
     -LoadBalancerBackendAddressPool $lb.BackendAddressPools[0]
}

```

## <a name="step-5---create-virtual-machines"></a>5. adım - sanal makine oluşturma

Yerinde bileşenleri için temel alınan tüm hello ile uygulamanızı artık yüksek oranda kullanılabilir sanal makineleri toorun oluşturabilirsiniz. 

Merhaba kullanıcı adı ve parola ile Merhaba sanal makinede hello yönetici hesabı için gerekli alma [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):

```powershell
$cred = Get-Credential
```

Merhaba VM'ler ile oluşturmak [yeni AzureRmVMConfig](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/new-azurermvmconfig), [kümesi AzureRmVMOperatingSystem](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmoperatingsystem), [kümesi AzureRmVMSourceImage](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmsourceimage), [Set-AzureRmVMOSDisk](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmosdisk), [Ekleme AzureRmVMNetworkInterface](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/add-azurermvmnetworkinterface), ve [AzureRmVM yeni](/powershell/module/azurerm.compute/new-azurermvm). Aşağıdaki örnek hello üç VM'ler oluşturur:

```powershell
for ($i=1; $i -le 3; $i++)
{
   $vm = New-AzureRmVMConfig -VMName myVM$i -VMSize Standard_D1 -AvailabilitySetId $availabilitySet.Id
   $vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName myVM$i -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
   $vm = Set-AzureRmVMSourceImage -VM $vm -PublisherName MicrosoftWindowsServer -Offer WindowsServer -Skus 2016-Datacenter -Version latest
   $vm = Set-AzureRmVMOSDisk -VM $vm -Name myOsDisk$i -StorageAccountType StandardLRS -DiskSizeInGB 128 -CreateOption FromImage -Caching ReadWrite
   $nic = Get-AzureRmNetworkInterface -ResourceGroupName myResourceGroup -Name myNic$i
   $vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
   New-AzureRmVM -ResourceGroupName myResourceGroup -Location westeurope -VM $vm
}

```

Birkaç dakika toocreate alır ve tüm üç VM'ler yapılandırın. Merhaba uygulamayı her VM çalıştıran hello yük dengeleyici durum araştırması otomatik olarak algılar. Merhaba uygulama çalışmaya başladıktan sonra hello yük dengeleyici kuralı toodistribute trafiği başlatır.

### <a name="install-hello-app"></a>Merhaba uygulamasını yükleyin 

Azure sanal makinesi, uygulama yükleme ve yapılandırma hello işletim sistemi gibi kullanılan tooautomate sanal makine yapılandırma görevleri uzantılarıdır. Merhaba [Windows için özel betik uzantısı](./../virtual-machines-windows-extensions-customscript.md) kullanılan toorun hello sanal makinede bir PowerShell betiğidir. Merhaba komut dosyası Azure depolama alanında, erişilebilir tüm HTTP uç noktası depolanan veya hello özel betik uzantısı yapılandırmasında katıştırılmış. Merhaba özel betik uzantısı kullanırken hello Azure VM Aracısı hello betik yürütme yönetir.

Kullanım [kümesi AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) tooinstall hello özel betik uzantısı. Merhaba uzantısı çalışır `powershell Add-WindowsFeature Web-Server` tooinstall hello IIS Web sunucusu:

```powershell
for ($i=1; $i -le 3; $i++)
{
   Set-AzureRmVMExtension -ResourceGroupName myResourceGroup `
     -ExtensionName IIS `
     -VMName myVM$i `
     -Publisher Microsoft.Compute `
     -ExtensionType CustomScriptExtension `
     -TypeHandlerVersion 1.4 `
     -SettingString '{"commandToExecute":"powershell Add-WindowsFeature Web-Server"}' `
     -Location westeurope
}
```

### <a name="test-your-app"></a>Uygulamanızı test etme

Merhaba, yük dengeleyici ile genel IP adresi elde [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress). Merhaba aşağıdaki örnek alacağı için başlangıç IP adresi `myPublicIP` daha önce oluşturduğunuz:

```powershell
Get-AzureRmPublicIPAddress -ResourceGroupName myResourceGroup -Name myPublicIP | select IpAddress
```

Tooa web tarayıcısında Hello genel IP adresi girin. Yerinde Hello NSG kuralı ile Merhaba varsayılan IIS Web sitesi görüntülenir. 

![Varsayılan IIS sitesi](media/load-balanced-iis-tutorial/iis.png)

## <a name="step-6--management-tasks"></a>6. adım – yönetim görevleri

Merhaba işletim sistemi güncelleştirmelerini yükleme gibi uygulamanızı çalıştıran VM'ler tooperform bakım gerekebilir. toodeal trafiğinin artmasına tooyour uygulamayla ihtiyacınız olabilecek tooadd ilave VM'ler. Bu bölümde, nasıl gösterilir tooremove veya VM hello yük dengeleyiciden ekleyin. 

### <a name="remove-a-vm-from-hello-load-balancer"></a>Bir VM hello yük dengeleyiciden kaldırın

Bir VM hello ağ arabirim kartı hello LoadBalancerBackendAddressPools özelliği sıfırlayarak hello arka uç adres havuzundan kaldırın.

Merhaba ağ arabirimi kartı ile [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface):

```powershell
$nic = Get-AzureRmNetworkInterface -ResourceGroupName myResourceGroup -Name myNic2
``` 

Merhaba ağ arabirim kartı Hello LoadBalancerBackendAddressPools özelliğini çok Ayarla $null:

```powershell
$nic.Ipconfigurations[0].LoadBalancerBackendAddressPools=$null
```

Merhaba ağ arabirim kartı güncelleştirin:

```powershell
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

### <a name="add-a-vm-toohello-load-balancer"></a>Bir VM toohello yük dengeleyici ekleme

VM bakım yapmak veya tooexpand kapasitesine ihtiyacınız varsa, hello NIC VM toohello arka uç adres havuzu hello yük dengeleyici ekleme sonra.

Merhaba yük dengeleyici alın:

```powershell
$lb = Get-AzureRMLoadBalancer -ResourceGroupName myResourceGroup -Name myLoadBalancer 
```

Merhaba yük dengeleyici toohello ağ arabirim kartı Hello arka uç adres havuzu ekleyin:

```powershell
$nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$lb.BackendAddressPools[0]
```

Merhaba ağ arabirim kartı güncelleştirin:

```powershell
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

## <a name="next-steps"></a>Sonraki Adımlar

Örnekleri – [Azure sanal makine PowerShell örnek betikler](./../virtual-machines-windows-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
