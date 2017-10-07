---
title: aaaCustomize Azure Windows VM | Microsoft Docs
description: "Toouse nasıl hello özel betik uzantısı ve anahtar kasası toocustomize azure'da Windows VM öğrenin"
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
ms.openlocfilehash: c03b2bb6d70875134c63ea2fe4c2e2c1777c2188
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocustomize-a-windows-virtual-machine-in-azure"></a>Nasıl toocustomize azure'da Windows sanal makine
hızlı ve tutarlı bir şekilde, tür Otomasyon tooconfigure sanal makineleri (VM'ler) genellikle istenen. Ortak bir yaklaşım toocustomize Windows VM toouse olan [için özel betik uzantısı Windows](extensions-customscript.md). Bu öğreticide şunların nasıl yapıldığını öğrenirsiniz:

> [!div class="checklist"]
> * Merhaba özel betik uzantısının tooinstall IIS kullanın
> * Merhaba özel betik uzantısı kullanan bir VM oluşturma
> * Merhaba uzantısı uygulandıktan sonra çalışan bir IIS sitesi görüntüleyin

Bu öğretici hello Azure PowerShell modülü 3,6 veya sonraki bir sürümü gerektiriyor. Çalıştırma ` Get-Module -ListAvailable AzureRM` toofind hello sürümü. Tooupgrade gerekirse bkz [yükleme Azure PowerShell Modülü](/powershell/azure/install-azurerm-ps).


## <a name="custom-script-extension-overview"></a>Özel betik uzantısı genel bakış
Merhaba özel betik uzantısının indirir ve Azure Vm'lerinde komut dosyaları çalıştırılır. Bu dağıtım yapılandırmaları, yazılım yükleme veya başka bir yapılandırma için yararlı bir uzantısıdır / yönetim görevi. Komut dosyaları Azure depolama veya GitHub indirilen veya toohello çalışma zamanı uzantısı Azure portalında sağlanan.

Merhaba özel betik uzantısı Azure Resource Manager şablonları ile tümleşir ve hello Azure CLI, PowerShell, Azure portal veya hello Azure sanal makine REST API'sini kullanarak da çalıştırılabilir.

Merhaba özel betik uzantısı, Windows ve Linux VM'ler ile kullanabilirsiniz.


## <a name="create-virtual-machine"></a>Sanal makine oluşturma
Bir VM oluşturmadan önce bir kaynak grubuyla oluşturmanız [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup). Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu *myResourceGroupAutomate* hello içinde *EastUS* konumu:

```powershell
New-AzureRmResourceGroup -ResourceGroupName myResourceGroupAutomate -Location EastUS
```

Yönetici olan hello VM'ler için kullanıcı adı ve parola ayarlayın [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):

```powershell
$cred = Get-Credential
```

Oluşturabileceğiniz artık VM ile Merhaba [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm). Merhaba aşağıdaki örnek gerekli hello sanal ağ bileşenleri hello işletim sistemi yapılandırması ve ardından adlı bir VM oluşturur *myVM*:

```powershell
# Create a subnet configuration
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -AddressPrefix 192.168.1.0/24

# Create a virtual network
$vnet = New-AzureRmVirtualNetwork `
    -ResourceGroupName myResourceGroupAutomate `
    -Location EastUS `
    -Name myVnet `
    -AddressPrefix 192.168.0.0/16 `
    -Subnet $subnetConfig

# Create a public IP address and specify a DNS name
$publicIP = New-AzureRmPublicIpAddress `
    -ResourceGroupName myResourceGroupAutomate `
    -Location EastUS `
    -AllocationMethod Static `
    -IdleTimeoutInMinutes 4 `
    -Name "myPublicIP"

# Create an inbound network security group rule for port 3389
$nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig `
    -Name myNetworkSecurityGroupRuleRDP  `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 1000 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 3389 `
    -Access Allow

# Create an inbound network security group rule for port 80
$nsgRuleWeb = New-AzureRmNetworkSecurityRuleConfig `
    -Name myNetworkSecurityGroupRuleWWW  `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 1001 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 80 `
    -Access Allow

# Create a network security group
$nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName myResourceGroupAutomate `
    -Location EastUS `
    -Name myNetworkSecurityGroup `
    -SecurityRules $nsgRuleRDP,$nsgRuleWeb

# Create a virtual network card and associate with public IP address and NSG
$nic = New-AzureRmNetworkInterface `
    -Name myNic `
    -ResourceGroupName myResourceGroupAutomate `
    -Location EastUS `
    -SubnetId $vnet.Subnets[0].Id `
    -PublicIpAddressId $publicIP.Id `
    -NetworkSecurityGroupId $nsg.Id

# Create a virtual machine configuration
$vmConfig = New-AzureRmVMConfig -VMName myVM -VMSize Standard_DS2 | `
Set-AzureRmVMOperatingSystem -Windows -ComputerName myVM -Credential $cred | `
Set-AzureRmVMSourceImage -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer -Skus 2016-Datacenter -Version latest | `
Add-AzureRmVMNetworkInterface -Id $nic.Id

New-AzureRmVM -ResourceGroupName myResourceGroupAutomate -Location EastUS -VM $vmConfig
```

Merhaba kaynaklar ve oluşturulan VM toobe için birkaç dakika sürer.


## <a name="automate-iis-install"></a>IIS yükleme otomatikleştirme
Kullanım [kümesi AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) tooinstall hello özel betik uzantısı. Merhaba uzantısı çalışır `powershell Add-WindowsFeature Web-Server` tooinstall hello IIS Web sunucusu ve ardından güncelleştirmeleri hello *Default.htm* sayfa tooshow hello hello VM konak adı:

```powershell
Set-AzureRmVMExtension -ResourceGroupName myResourceGroupAutomate `
    -ExtensionName IIS `
    -VMName myVM `
    -Publisher Microsoft.Compute `
    -ExtensionType CustomScriptExtension `
    -TypeHandlerVersion 1.4 `
    -SettingString '{"commandToExecute":"powershell Add-WindowsFeature Web-Server; powershell Add-Content -Path \"C:\\inetpub\\wwwroot\\Default.htm\" -Value $($env:computername)"}' `
    -Location EastUS
```


## <a name="test-web-site"></a>Sınama web sitesi
Merhaba, yük dengeleyici ile genel IP adresi elde [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress). Merhaba aşağıdaki örnek alacağı için başlangıç IP adresi *myPublicIP* daha önce oluşturduğunuz:

```powershell
Get-AzureRmPublicIPAddress `
    -ResourceGroupName myResourceGroupAutomate `
    -Name myPublicIP | select IpAddress
```

Ardından tooa web tarayıcısında hello genel IP adresi girebilirsiniz. Merhaba Web sitesi gösterilir, hello VM hello hostname dahil olmak üzere bu hello yük dengeleyici trafiği tooas aşağıdaki örneğine hello içinde dağıtılmış:

![Çalışan IIS Web sitesi](./media/tutorial-automate-vm-deployment/running-iis-website.png)


## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide, bir VM'ye IIS yüklemeniz hello otomatik. Size nasıl öğrenilen için:

> [!div class="checklist"]
> * Merhaba özel betik uzantısının tooinstall IIS kullanın
> * Merhaba özel betik uzantısı kullanan bir VM oluşturma
> * Merhaba uzantısı uygulandıktan sonra çalışan bir IIS sitesi görüntüleyin

Toohello sonraki öğretici toolearn nasıl ilerlemek toocreate özel VM görüntüler.

> [!div class="nextstepaction"]
> [Özel VM görüntüleri oluşturma](./tutorial-custom-images.md)
