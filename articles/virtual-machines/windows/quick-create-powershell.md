---
title: "aaaAzure hızlı başlangıç - Windows VM PowerShell oluşturun | Microsoft Docs"
description: "Hızlı bir şekilde bir Windows sanal makineleri PowerShell ile toocreate öğrenin"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 5e92435bf7ee443a01c158fed91c356363e2f425
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-virtual-machine-with-powershell"></a>PowerShell ile Windows sanal makinesi oluşturma

Hello Azure PowerShell modülü kullanılan toocreate olan ve hello PowerShell komut satırından veya komut dosyalarında Azure kaynaklarını yönetin. PowerShell toocreate ve Windows Server 2016 çalıştıran Azure sanal makine kullanarak bu kılavuzu ayrıntıları. Dağıtım tamamlandıktan sonra biz toohello sunucusuna bağlanmak ve IIS yükleyin.  

Azure aboneliğiniz yoksa başlamadan önce [ücretsiz bir hesap](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) oluşturun.

Bu hızlı başlangıç hello Azure PowerShell modülü 3,6 veya sonraki bir sürümü gerektiriyor. Çalıştırma ` Get-Module -ListAvailable AzureRM` toofind hello sürümü. Tooinstall veya yükseltme gerekirse bkz [yükleme Azure PowerShell Modülü](/powershell/azure/install-azurerm-ps).

## <a name="log-in-tooazure"></a>İçinde tooAzure oturum

Tooyour hello Azure aboneliğiyle oturum `Login-AzureRmAccount` komut ve hello ekrandaki yönergeleri izleyin.

```powershell
Login-AzureRmAccount
```

## <a name="create-resource-group"></a>Kaynak grubu oluşturma

[New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) ile yeni bir Azure kaynak grubu oluşturun. Kaynak grubu, Azure kaynaklarının dağıtıldığı ve yönetildiği bir mantıksal kapsayıcıdır. 

```powershell
New-AzureRmResourceGroup -Name myResourceGroup -Location EastUS
```

## <a name="create-networking-resources"></a>Ağ kaynakları oluşturma

### <a name="create-a-virtual-network-subnet-and-a-public-ip-address"></a>Bir sanal ağ, alt ağ ve genel IP adresi oluşturun. 
Bu kaynaklar kullanılan tooprovide ağ bağlantısı toohello sanal makine olan ve toohello bağlamak Internet.

```powershell
# Create a subnet configuration
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name mySubnet -AddressPrefix 192.168.1.0/24

# Create a virtual network
$vnet = New-AzureRmVirtualNetwork -ResourceGroupName myResourceGroup -Location EastUS `
    -Name MYvNET -AddressPrefix 192.168.0.0/16 -Subnet $subnetConfig

# Create a public IP address and specify a DNS name
$pip = New-AzureRmPublicIpAddress -ResourceGroupName myResourceGroup -Location EastUS `
    -AllocationMethod Static -IdleTimeoutInMinutes 4 -Name "mypublicdns$(Get-Random)"
```

### <a name="create-a-network-security-group-and-a-network-security-group-rule"></a>Bir ağ güvenliği grubu ve bir ağ güvenliği grup kuralı oluşturun. 
Merhaba ağ güvenlik grubu gelen ve giden kuralları kullanarak hello sanal makine güvenliğini sağlar. Bu durumda, bağlantı noktası 3389 için gelen masaüstü bağlantılarına izin veren bir gelen kuralı oluşturulur. Ayrıca toocreate bir gelen kuralı gelen web trafiği sağlayan için bağlantı noktası 80, istiyoruz.

```powershell
# Create an inbound network security group rule for port 3389
$nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig -Name myNetworkSecurityGroupRuleRDP  -Protocol Tcp `
    -Direction Inbound -Priority 1000 -SourceAddressPrefix * -SourcePortRange * -DestinationAddressPrefix * `
    -DestinationPortRange 3389 -Access Allow

# Create an inbound network security group rule for port 80
$nsgRuleWeb = New-AzureRmNetworkSecurityRuleConfig -Name myNetworkSecurityGroupRuleWWW  -Protocol Tcp `
    -Direction Inbound -Priority 1001 -SourceAddressPrefix * -SourcePortRange * -DestinationAddressPrefix * `
    -DestinationPortRange 80 -Access Allow

# Create a network security group
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName myResourceGroup -Location EastUS `
    -Name myNetworkSecurityGroup -SecurityRules $nsgRuleRDP,$nsgRuleWeb
```

### <a name="create-a-network-card-for-hello-virtual-machine"></a>Merhaba sanal makine için bir ağ kartı oluşturun. 
Bir ağ kartı ile oluşturmak [yeni AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) hello sanal makine için. Merhaba ağ kartı hello sanal makine tooa alt ağ, ağ güvenlik grubu ve genel IP adresine bağlanır.

```powershell
# Create a virtual network card and associate with public IP address and NSG
$nic = New-AzureRmNetworkInterface -Name myNic -ResourceGroupName myResourceGroup -Location EastUS `
    -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -NetworkSecurityGroupId $nsg.Id
```

## <a name="create-virtual-machine"></a>Sanal makine oluşturma

Sanal makine yapılandırması oluşturun. Bu yapılandırma, bir sanal makine görüntüsü, boyutu ve kimlik doğrulama yapılandırması gibi hello sanal makine dağıtımı sırasında kullanılan hello ayarlarını içerir. Bu adımı çalıştırırken kimlik bilgileri istenir. Girdiğiniz hello değerleri hello kullanıcı adı ve parola hello sanal makine için olarak yapılandırılır.

```powershell
# Define a credential object
$cred = Get-Credential

# Create a virtual machine configuration
$vmConfig = New-AzureRmVMConfig -VMName myVM -VMSize Standard_DS2 | `
    Set-AzureRmVMOperatingSystem -Windows -ComputerName myVM -Credential $cred | `
    Set-AzureRmVMSourceImage -PublisherName MicrosoftWindowsServer -Offer WindowsServer `
    -Skus 2016-Datacenter -Version latest | Add-AzureRmVMNetworkInterface -Id $nic.Id
```

Merhaba sanal makineyle oluşturmak [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).

```powershell
New-AzureRmVM -ResourceGroupName myResourceGroup -Location EastUS -VM $vmConfig
```

## <a name="connect-toovirtual-machine"></a>Toovirtual makineyi bağlayın

Merhaba dağıtım tamamlandıktan sonra bir Uzak Masaüstü Bağlantısı ile Merhaba sanal makine oluşturun.

Kullanım hello [Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) tooreturn hello genel IP adresi hello sanal makinenin komutu. Tarayıcı tootest web bağlantınızı bir sonraki adımda ile tooit bağlanabilmesi için bu IP adresini not alın.

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName myResourceGroup | Select IpAddress
```

Kullanım hello aşağıdaki hello sanal makineyle Uzak Masaüstü oturumu toocreate komutu. Başlangıç IP adresi ile hello yerine *Publicıpaddress* sanal makinenizin. İstendiğinde, hello sanal makine oluşturulurken kullanılan hello kimlik bilgilerini girin.

```bash 
mstsc /v:<publicIpAddress>
```

## <a name="install-iis-via-powershell"></a>PowerShell kullanarak IIS yükleme

Toohello Azure VM'de oturum, tek satırlık bir PowerShell tooinstall IIS kullanın ve hello yerel güvenlik duvarı kuralı tooallow web trafiği etkinleştirin. PowerShell komut istemini açın ve hello aşağıdaki komutu çalıştırın:

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

## <a name="view-hello-iis-welcome-page"></a>Görünüm hello IIS Karşılama sayfası

IIS yüklü ve bağlantı noktası 80, VM'den hello Internet üzerinde şimdi açık ile seçim tooview hello varsayılan IIS Karşılama sayfasını bir web tarayıcısı kullanabilirsiniz. Emin toouse hello olması *Publicıpaddress* toovisit hello varsayılan sayfa belgelenmiştir. 

![Varsayılan IIS sitesi](./media/quick-create-powershell/default-iis-website.png) 

## <a name="clean-up-resources"></a>Kaynakları temizleme

Artık gerektiğinde Merhaba kullanabilirsiniz [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) tooremove hello kaynak grubu, VM ve tüm ilişkili kaynakları komutu.

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="next-steps"></a>Sonraki adımlar

Bu hızlı başlangıçta basit bir sanal makine ve bir ağ güvenlik grubu kuralı dağıtıp, bir web sunucusu yüklediniz. Azure sanal makinelerde hakkında daha fazla toolearn toohello öğretici Windows VM'ler için devam edin.

> [!div class="nextstepaction"]
> [Azure Windows sanal makine öğreticileri](./tutorial-manage-vm.md)
