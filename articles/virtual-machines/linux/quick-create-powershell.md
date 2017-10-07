---
title: "aaaAzure hızlı başlangıç - VM PowerShell oluşturun | Microsoft Docs"
description: "Hızlı bir şekilde Linux sanal makineleri PowerShell ile toocreate öğrenin"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: f05ea7fedafe4fda660dc6084ae57ebf9dced473
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-linux-virtual-machine-with-powershell"></a>PowerShell ile Linux sanal makinesi oluşturma

Hello Azure PowerShell modülü kullanılan toocreate olan ve hello PowerShell komut satırından veya komut dosyalarında Azure kaynaklarını yönetin. Ubuntu server çalıştıran bir sanal makine Hello Azure PowerShell modülü toodeploy kullanarak bu kılavuzu ayrıntıları. Merhaba sunucu dağıtıldığında, bir SSH bağlantısı oluşturulur ve bir NGINX Web sunucusu yüklenir.

Azure aboneliğiniz yoksa başlamadan önce [ücretsiz bir hesap](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) oluşturun.

Bu hızlı başlangıç hello Azure PowerShell modülü 3,6 veya sonraki bir sürümü gerektiriyor. Çalıştırma ` Get-Module -ListAvailable AzureRM` toofind hello sürümü. Tooinstall veya yükseltme gerekirse bkz [yükleme Azure PowerShell Modülü](/powershell/azure/install-azurerm-ps).

Son olarak, bir genel SSH anahtarı hello adla *id_rsa.pub* hello depolanan toobe gereken *.ssh* Windows kullanıcı profilinizin dizin. Azure için SSH anahtarları oluşturma hakkında ayrıntılı bilgi için bkz. [Azure için SSH anahtarları oluşturma](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="log-in-tooazure"></a>İçinde tooAzure oturum

Tooyour hello Azure aboneliğiyle oturum `Login-AzureRmAccount` komut ve hello ekrandaki yönergeleri izleyin.

```powershell
Login-AzureRmAccount
```

## <a name="create-resource-group"></a>Kaynak grubu oluşturma

[New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) ile yeni bir Azure kaynak grubu oluşturun. Kaynak grubu, Azure kaynaklarının dağıtıldığı ve yönetildiği bir mantıksal kapsayıcıdır. 

```powershell
New-AzureRmResourceGroup -Name myResourceGroup -Location eastus
```

## <a name="create-networking-resources"></a>Ağ kaynakları oluşturma

Bir sanal ağ, alt ağ ve genel IP adresi oluşturun. Bu kaynaklar kullanılan tooprovide ağ bağlantısı toohello sanal makine olan ve toohello bağlamak Internet.

```powershell
# Create a subnet configuration
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name mySubnet -AddressPrefix 192.168.1.0/24

# Create a virtual network
$vnet = New-AzureRmVirtualNetwork -ResourceGroupName myResourceGroup -Location eastus `
-Name MYvNET -AddressPrefix 192.168.0.0/16 -Subnet $subnetConfig

# Create a public IP address and specify a DNS name
$pip = New-AzureRmPublicIpAddress -ResourceGroupName myResourceGroup -Location eastus `
-AllocationMethod Static -IdleTimeoutInMinutes 4 -Name "mypublicdns$(Get-Random)"
```

Bir ağ güvenliği grubu ve bir ağ güvenliği grup kuralı oluşturun. Merhaba ağ güvenlik grubu gelen ve giden kuralları kullanarak hello sanal makine güvenliğini sağlar. Bu durumda, bağlantı noktası 22 için gelen SSH bağlantılarına izin veren bir gelen kuralı oluşturulur. Ayrıca toocreate bir gelen kuralı gelen web trafiği sağlayan için bağlantı noktası 80, istiyoruz.

```powershell
# Create an inbound network security group rule for port 22
$nsgRuleSSH = New-AzureRmNetworkSecurityRuleConfig -Name myNetworkSecurityGroupRuleSSH  -Protocol Tcp `
-Direction Inbound -Priority 1000 -SourceAddressPrefix * -SourcePortRange * -DestinationAddressPrefix * `
-DestinationPortRange 22 -Access Allow

# Create an inbound network security group rule for port 80
$nsgRuleWeb = New-AzureRmNetworkSecurityRuleConfig -Name myNetworkSecurityGroupRuleWWW  -Protocol Tcp `
-Direction Inbound -Priority 1001 -SourceAddressPrefix * -SourcePortRange * -DestinationAddressPrefix * `
-DestinationPortRange 80 -Access Allow

# Create a network security group
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName myResourceGroup -Location eastus `
-Name myNetworkSecurityGroup -SecurityRules $nsgRuleSSH,$nsgRuleWeb
```

Bir ağ kartı ile oluşturmak [yeni AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) hello sanal makine için. Merhaba ağ kartı hello sanal makine tooa alt ağ, ağ güvenlik grubu ve genel IP adresine bağlanır.

```powershell
# Create a virtual network card and associate with public IP address and NSG
$nic = New-AzureRmNetworkInterface -Name myNic -ResourceGroupName myResourceGroup -Location eastus `
-SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -NetworkSecurityGroupId $nsg.Id
```

## <a name="create-virtual-machine"></a>Sanal makine oluşturma

Sanal makine yapılandırması oluşturun. Bu yapılandırma, bir sanal makine görüntüsü, boyutu ve kimlik doğrulama yapılandırması gibi hello sanal makine dağıtımı sırasında kullanılan hello ayarlarını içerir.

```powershell
# Define a credential object
$securePassword = ConvertTo-SecureString ' ' -AsPlainText -Force
$cred = New-Object System.Management.Automation.PSCredential ("azureuser", $securePassword)

# Create a virtual machine configuration
$vmConfig = New-AzureRmVMConfig -VMName myVM -VMSize Standard_D1 | `
Set-AzureRmVMOperatingSystem -Linux -ComputerName myVM -Credential $cred -DisablePasswordAuthentication | `
Set-AzureRmVMSourceImage -PublisherName Canonical -Offer UbuntuServer -Skus 14.04.2-LTS -Version latest | `
Add-AzureRmVMNetworkInterface -Id $nic.Id

# Configure SSH Keys
$sshPublicKey = Get-Content "$env:USERPROFILE\.ssh\id_rsa.pub"
Add-AzureRmVMSshPublicKey -VM $vmconfig -KeyData $sshPublicKey -Path "/home/azureuser/.ssh/authorized_keys"
```

Merhaba sanal makineyle oluşturmak [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).

```powershell
New-AzureRmVM -ResourceGroupName myResourceGroup -Location eastus -VM $vmConfig
```

## <a name="connect-toovirtual-machine"></a>Toovirtual makineyi bağlayın

Merhaba dağıtım tamamlandıktan sonra bir SSH bağlantısı ile Merhaba sanal makine oluşturun.

Kullanım hello [Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) tooreturn hello genel IP adresi hello sanal makinenin komutu.

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName myResourceGroup | Select IpAddress
```

SSH yüklü bir sistemden tooconnect toohello sanal makine kullanılan hello şu komutu. Windows üzerinde çalışıyorsanız [Putty](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-ssh-from-windows?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#create-a-private-key-for-putty) kullanılan toocreate hello bağlantı olabilir. 

```bash 
ssh <Public IP Address>
```

İstendiğinde, hello oturum açma kullanıcı adı. *azureuser*. Bir parola SSH anahtarları oluşturma sırasında girilen, bu da tooenter gerekir.


## <a name="install-nginx"></a>NGINX yükleme

Kullanım hello aşağıdaki komut dosyası tooupdate paket kaynaklarını bash ve hello son NGINX paketini yükleyin. 

```bash 
#!/bin/bash

# update package source
apt-get -y update

# install NGINX
apt-get -y install nginx
```

## <a name="view-hello-ngix-welcome-page"></a>Merhaba NGIX Karşılama sayfasını görüntüle

Yüklü NGINX ve bağlantı noktası 80, VM'den hello Internet - üzerinde şimdi açık seçim tooview hello varsayılan NGINX Hoş Geldiniz sayfasını bir web tarayıcısı kullanabilirsiniz. Toovisit hello varsayılan sayfa belgelenen emin toouse hello genel IP adresi olabilir. 

![Varsayılan NGINX sitesi](./media/quick-create-cli/nginx.png) 

## <a name="clean-up-resources"></a>Kaynakları temizleme

Artık gerektiğinde Merhaba kullanabilirsiniz [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) tooremove hello kaynak grubu, VM ve tüm ilişkili kaynakları komutu.

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="next-steps"></a>Sonraki adımlar

Bu hızlı başlangıçta basit bir sanal makine ve bir ağ güvenlik grubu kuralı dağıtıp, bir web sunucusu yüklediniz. Azure sanal makinelerde hakkında daha fazla toolearn toohello öğretici Linux VM'ler için devam edin.

> [!div class="nextstepaction"]
> [Azure Linux sanal makine öğreticileri](./tutorial-manage-vm.md)
