---
title: "Azure sanal ağlar ve Windows sanal makineleri | Microsoft Docs"
description: "Öğretici - Azure sanal ağlar ve Azure PowerShell ile Windows sanal makineleri yönetme"
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
ms.date: 05/02/2017
ms.author: davidmu
ms.custom: mvc
ms.openlocfilehash: c71c07f8ecd123a7e27848ba5043d46e315fcf03
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="manage-azure-virtual-networks-and-windows-virtual-machines-with-azure-powershell"></a>Azure sanal ağlar ve Azure PowerShell ile Windows sanal makineleri yönetme

Azure sanal makineler, iç ve dış ağ iletişimi için Azure ağ kullanın. Bu öğreticide, bir sanal ağda birden çok sanal makine (VM) oluşturabilir ve bunları arasında ağ bağlantısı yapılandırabilirsiniz. Aşağıdakileri nasıl yapacağınızı öğrenirsiniz:

> [!div class="checklist"]
> * Sanal ağ oluşturma
> * Sanal ağ alt ağları oluşturma
> * Ağ güvenlik gruplarıyla ağ trafiğini denetleme
> * Eylem trafik kurallarını görüntüle

Bu öğretici, Azure PowerShell modülü 3.6 veya sonraki bir sürümü gerektirir. Sürümü bulmak için ` Get-Module -ListAvailable AzureRM` komutunu çalıştırın. Yükseltme gerekiyorsa, bkz: [yükleme Azure PowerShell Modülü](/powershell/azure/install-azurerm-ps).

## <a name="create-vnet"></a>VNet oluşturma

Bir VNet kendi ağ bulutta gösterimidir. Bir VNet Azure bulutunun aboneliğinize adanmış mantıksal bir yalıtım ' dir. Bir sanal ağ içinde alt ağlar, bu alt ağlar ve bağlantıları VM'ler alt ağlara bağlantısı kurallarını bulun.

Diğer Azure kaynaklarına oluşturabilmeniz için önce bir kaynak grubu ile oluşturmanıza gerek [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup). Aşağıdaki örnek, bir kaynak grubu oluşturur *myRGNetwork* içinde *EastUS* konumu:

```powershell
New-AzureRmResourceGroup -ResourceGroupName myRGNetwork -Location EastUS
```

Bir alt ağ alt bir vnet'in kaynaktır ve adres alanları IP adresi öneklerini kullanarak bir CIDR bloğu içinde kesimleri yardımcı tanımlayın. NIC alt ağlara eklendi ve çeşitli iş yükleri için bağlantı sağlama VM'ler bağlı.

Bir alt ağ ile oluşturma [yeni AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig):

```powershell
$frontendSubnet = New-AzureRmVirtualNetworkSubnetConfig `
  -Name myFrontendSubnet `
  -AddressPrefix 10.0.0.0/24
```

Adlı VNET oluşturma *myVNet* kullanarak *myFrontendSubnet* ile [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork):

```powershell
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myVNet `
  -AddressPrefix 10.0.0.0/16 `
  -Subnet $frontendSubnet
```

## <a name="create-front-end-vm"></a>Ön uç VM oluşturma

Bir VM sanal ağ içinde iletişim kurmak bir sanal ağ arabirimi (NIC) gerekir. *MyFrontendVM* internet'ten erişilir, böylece bir ortak IP adresini de gerekir. 

Bir ortak IP adresiyle oluşturma [yeni AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress):

```powershell
$pip = New-AzureRmPublicIpAddress `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -AllocationMethod Static `
  -Name myPublicIPAddress
```

Bir NIC ile oluşturma [AzureRmNetworkInterface yeni](/powershell/module/azurerm.network/new-azurermnetworkinterface):


```powershell
$frontendNic = New-AzureRmNetworkInterface `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myFrontendNic `
  -SubnetId $vnet.Subnets[0].Id `
  -PublicIpAddressId $pip.Id
```

Kullanıcı adı ayarlayabilir ve parola için yönetici hesabı ile VM üzerinde [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):

```powershell
$cred = Get-Credential
```

VM'lerin oluşturma [AzureRmVMConfig yeni](/powershell/module/azurerm.compute/new-azurermvmconfig), [kümesi AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem), [kümesi AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage), [kümesi AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk), [ekleme AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface), ve [AzureRmVM yeni](/powershell/module/azurerm.compute/new-azurermvm). 

```powershell
$frontendVM = New-AzureRmVMConfig `
    -VMName myFrontendVM `
    -VMSize Standard_D1
$frontendVM = Set-AzureRmVMOperatingSystem `
    -VM $frontendVM `
    -Windows `
    -ComputerName myFrontendVM `
    -Credential $cred `
    -ProvisionVMAgent `
    -EnableAutoUpdate
$frontendVM = Set-AzureRmVMSourceImage `
    -VM $frontendVM `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter `
    -Version latest
$frontendVM = Set-AzureRmVMOSDisk `
    -VM $frontendVM `
    -Name myFrontendOSDisk `
    -DiskSizeInGB 128 `
    -CreateOption FromImage `
    -Caching ReadWrite
$frontendVM = Add-AzureRmVMNetworkInterface `
    -VM $frontendVM `
    -Id $frontendNic.Id
New-AzureRmVM `
    -ResourceGroupName myRGNetwork `
    -Location EastUS `
    -VM $frontendVM
```

## <a name="install-web-server"></a>Web sunucusunu yükleme

IIS yükleyebilirsiniz *myFrontendVM* Uzak Masaüstü oturumu kullanarak. Genel IP adresi erişmek için VM'nin edinmeniz gerekir.

Genel IP adresi elde edebilirsiniz *myFrontendVM* ile [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress). Aşağıdaki örnek IP adresi alacağı *myPublicIPAddress* daha önce oluşturduğunuz:

```powershell
Get-AzureRmPublicIPAddress `
    -ResourceGroupName myRGNetwork `
    -Name myPublicIPAddress | select IpAddress
```

Sonraki adımlarda kullanabilmesi için bu IP adresini not edin.

İle Uzak Masaüstü oturumu oluşturmak için aşağıdaki komutu kullanın *myFrontendVM*. Değiştir  *<publicIPAddress>*  daha önce kaydettiğiniz adresine sahip. İstendiğinde VM oluşturduğunuz sırada kullanılan kimlik bilgilerini girin.

```
mstsc /v:<publicIpAddress>
``` 

Oturum olduğunuza *myFrontendVM*, IIS yüklemek ve web trafiğine izin vermek yerel güvenlik duvarı kuralı etkinleştirmek için tek satırlık bir PowerShell kullanabilirsiniz. Bir PowerShell istemi açın ve şu komutu çalıştırın:

Kullanım [Install-WindowsFeature](https://technet.microsoft.com/itpro/powershell/windows/servermanager/install-windowsfeature) IIS Web sunucusu yükler özel betik uzantısı çalıştırmak için:

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

Şimdi IIS sitesi görmek için VM göz atmak için genel IP adresini kullanabilirsiniz.

![Varsayılan IIS sitesi](./media/tutorial-virtual-network/iis.png)

## <a name="manage-internal-traffic"></a>İç trafiği yönetmek

Bir ağ güvenlik grubu (NSG) izin veren veya reddeden bir sanal ağa bağlı kaynaklar için ağ trafiği güvenlik kurallarının bir listesini içerir. Nsg'ler alt ağları veya VM'ler için bağlı tekil NIC'lerle ilişkili olabilir. Açma veya kapatma Vm'lere erişim bağlantı noktaları üzerinden yapılır NSG kurallarını kullanma. Oluşturduğunuzda *myFrontendVM*, gelen bağlantı noktası 3389 RDP bağlantı için otomatik olarak açılmışsa.

İç iletişim VM'lerin bir NSG kullanarak yapılandırılabilir. Bu bölümde, ağdaki ek bir alt ağ oluşturun ve bir NSG bir bağlantıdan izin verecek şekilde atamak öğrenin *myFrontendVM* için *myBackendVM* 1433 numaralı bağlantı noktasında. Alt ağ VM oluşturulduktan sonra atanır.

İç trafiği sınırlayabilirsiniz *myBackendVM* yalnızca gelen *myFrontendVM* arka uç alt ağı için bir NSG oluşturarak. Aşağıdaki örnek, adlandırılmış bir NSG kuralı oluşturur *myBackendNSGRule* ile [yeni AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig):

```powershell
$nsgBackendRule = New-AzureRmNetworkSecurityRuleConfig `
  -Name myBackendNSGRule `
  -Protocol Tcp `
  -Direction Inbound `
  -Priority 100 `
  -SourceAddressPrefix 10.0.0.0/24 `
  -SourcePortRange * `
  -DestinationAddressPrefix * `
  -DestinationPortRange 1433 `
  -Access Allow
```

Adlı ağ güvenlik grubu Ekle *myBackendNSG* ile [yeni AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup):

```powershell
$nsgBackend = New-AzureRmNetworkSecurityGroup `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myBackendNSG `
  -SecurityRules $nsgBackendRule
```
## <a name="add-back-end-subnet"></a>Arka uç alt ağ Ekle

Ekle *myBackEndSubnet* için *myVNet* ile [Ekle AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/add-azurermvirtualnetworksubnetconfig):

```powershell
Add-AzureRmVirtualNetworkSubnetConfig `
  -Name myBackendSubnet `
  -VirtualNetwork $vnet `
  -AddressPrefix 10.0.1.0/24 `
  -NetworkSecurityGroup $nsgBackend
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
$vnet = Get-AzureRmVirtualNetwork `
  -ResourceGroupName myRGNetwork `
  -Name myVNet
```

## <a name="create-back-end-vm"></a>Arka uç VM oluşturma

Arka uç VM oluşturmak için en kolay yolu, bir SQL Server görüntüsü kullanmaktır. Bu öğretici yalnızca VM veritabanı sunucusuyla oluşturur, ancak veritabanı erişme hakkında bilgi sağlamaz.

Oluşturma *myBackendNic*:

```powershell
$backendNic = New-AzureRmNetworkInterface `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myBackendNic `
  -SubnetId $vnet.Subnets[1].Id
```

Kullanıcı adı ve parola Get-Credential ile VM üzerinde yönetici hesabı için gerekli ayarlayın:

```powershell
$cred = Get-Credential
```

Oluşturma *myBackendVM*:

```powershell
$backendVM = New-AzureRmVMConfig `
  -VMName myBackendVM `
  -VMSize Standard_D1
$backendVM = Set-AzureRmVMOperatingSystem `
  -VM $backendVM `
  -Windows `
  -ComputerName myBackendVM `
  -Credential $cred `
  -ProvisionVMAgent `
  -EnableAutoUpdate
$backendVM = Set-AzureRmVMSourceImage `
  -VM $backendVM `
  -PublisherName MicrosoftSQLServer `
  -Offer SQL2016SP1-WS2016 `
  -Skus Enterprise `
  -Version latest
$backendVM = Set-AzureRmVMOSDisk `
  -VM $backendVM `
  -Name myBackendOSDisk `
  -DiskSizeInGB 128 `
  -CreateOption FromImage `
  -Caching ReadWrite
$backendVM = Add-AzureRmVMNetworkInterface `
  -VM $backendVM `
  -Id $backendNic.Id
New-AzureRmVM `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -VM $backendVM
```

Kullanılan görüntü SQL Server'ın yüklü, ancak bu öğreticide kullanılmaz. Web trafiğini işlemek için bir VM ve veritabanı yönetimi işlemek için bir VM nasıl yapılandırabileceğiniz göstermek için dahil edilir.

## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide oluşturduğunuz ve Azure ağları sanal makinelerle ilgili olarak güvenli. 

> [!div class="checklist"]
> * Sanal ağ oluşturma
> * Sanal ağ alt ağları oluşturma
> * Ağ güvenlik gruplarıyla ağ trafiğini denetleme
> * Eylem trafik kurallarını görüntüle

Azure Yedekleme'yi kullanarak sanal makinelerde güvenli hale getirme verileri izleme hakkında bilgi edinmek için sonraki öğretici ilerleyin. .

> [!div class="nextstepaction"]
> [Azure'da Windows sanal makineleri yedekleyin](./tutorial-backup-vms.md)
