---
title: "aaaAzure Windows sanal makineler ve sanal ağları | Microsoft Docs"
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
ms.openlocfilehash: ed77d9d5873e849fcb2aaf15e41899d7ad8c781a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-virtual-networks-and-windows-virtual-machines-with-azure-powershell"></a>Azure sanal ağlar ve Azure PowerShell ile Windows sanal makineleri yönetme

Azure sanal makineler, iç ve dış ağ iletişimi için Azure ağ kullanın. Bu öğreticide, bir sanal ağda birden çok sanal makine (VM) oluşturabilir ve bunları arasında ağ bağlantısı yapılandırabilirsiniz. Aşağıdakileri nasıl yapacağınızı öğrenirsiniz:

> [!div class="checklist"]
> * Sanal ağ oluşturma
> * Sanal ağ alt ağları oluşturma
> * Ağ güvenlik gruplarıyla ağ trafiğini denetleme
> * Eylem trafik kurallarını görüntüle

Bu öğretici hello Azure PowerShell modülü 3,6 veya sonraki bir sürümü gerektiriyor. Çalıştırma ` Get-Module -ListAvailable AzureRM` toofind hello sürümü. Tooupgrade gerekirse bkz [yükleme Azure PowerShell Modülü](/powershell/azure/install-azurerm-ps).

## <a name="create-vnet"></a>VNet oluşturma

Bir VNet kendi ağ hello bulutta gösterimidir. Bir VNet hello ayrılmış Azure bulut tooyour abonelik mantıksal yalıtımının ' dir. Bir sanal ağ içinde alt ağlar, bağlantı toothose alt ağları ve hello VM'ler toohello alt bağlantılarından kurallarını bulun.

Diğer Azure kaynaklarına oluşturabilmeniz için önce bir kaynak grubu ile toocreate gerekir [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup). Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu *myRGNetwork* hello içinde *EastUS* konumu:

```powershell
New-AzureRmResourceGroup -ResourceGroupName myRGNetwork -Location EastUS
```

Bir alt ağ alt bir vnet'in kaynaktır ve adres alanları IP adresi öneklerini kullanarak bir CIDR bloğu içinde kesimleri yardımcı tanımlayın. NIC toosubnets ve çeşitli iş yükleri için bağlantı sağlama bağlı tooVMs eklenebilir.

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

Bir sanal ağda VM toocommunicate için bir sanal ağ arabirimi (NIC) gerekir. Merhaba *myFrontendVM* hello erişilen Internet nedenle da genel bir IP adresi gerekir. 

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

Merhaba kullanıcı adı ve parola hello VM hello yönetici hesabı için gerekli olan [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):

```powershell
$cred = Get-Credential
```

Merhaba VM'ler ile oluşturmak [yeni AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig), [kümesi AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem), [kümesi AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage), [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk), [Ekleme AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface), ve [AzureRmVM yeni](/powershell/module/azurerm.compute/new-azurermvm). 

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

IIS yükleyebilirsiniz *myFrontendVM* Uzak Masaüstü oturumu kullanarak. Merhaba VM tooaccess tooget hello genel IP adresi gerekiyor.

Merhaba genel IP adresi elde edebilirsiniz *myFrontendVM* ile [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress). Merhaba aşağıdaki örnek alacağı için başlangıç IP adresi *myPublicIPAddress* daha önce oluşturduğunuz:

```powershell
Get-AzureRmPublicIPAddress `
    -ResourceGroupName myRGNetwork `
    -Name myPublicIPAddress | select IpAddress
```

Sonraki adımlarda kullanabilmesi için bu IP adresini not edin.

Kullanım hello aşağıdaki komut ile Uzak Masaüstü oturumu toocreate *myFrontendVM*. Değiştir  *<publicIPAddress>*  daha önce kaydettiğiniz hello adresine sahip. İstendiğinde, hello VM oluştururken kullanılan hello kimlik bilgilerini girin.

```
mstsc /v:<publicIpAddress>
``` 

Çok günlüğe olduğunuza*myFrontendVM*, tek satırlık bir PowerShell tooinstall IIS kullanın ve hello yerel güvenlik duvarı kuralı tooallow web trafiği etkinleştirin. PowerShell komut istemini açın ve hello aşağıdaki komutu çalıştırın:

Kullanım [Install-WindowsFeature](https://technet.microsoft.com/itpro/powershell/windows/servermanager/install-windowsfeature) hello IIS Web sunucusu yükler toorun hello özel betik uzantısı:

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

Artık hello ortak IP adresi toobrowse toohello VM toosee hello IIS sitesi kullanabilirsiniz.

![Varsayılan IIS sitesi](./media/tutorial-virtual-network/iis.png)

## <a name="manage-internal-traffic"></a>İç trafiği yönetmek

Bir ağ güvenlik grubu (NSG) izin veren veya reddeden ağ trafiğine bağlı tooresources tooa VNet güvenlik kurallarının bir listesini içerir. Nsg'ler ilişkili toosubnets olabilir veya tek tek NIC tooVMs bağlı. Açma veya kapatma erişim tooVMs bağlantı noktaları üzerinden yapılır NSG kurallarını kullanma. Oluşturduğunuzda *myFrontendVM*, gelen bağlantı noktası 3389 RDP bağlantı için otomatik olarak açılmışsa.

İç iletişim VM'lerin bir NSG kullanarak yapılandırılabilir. Bu bölümde, bilgi nasıl toocreate hello ek bir alt ağ ve bir NSG tooit tooallow bir bağlantıdan atayın *myFrontendVM* çok*myBackendVM* 1433 numaralı bağlantı noktasında. Merhaba alt toohello VM oluşturulduktan sonra atanır.

Çok iç trafiğini sınırlandırmak*myBackendVM* yalnızca gelen *myFrontendVM* hello arka uç alt ağı için bir NSG oluşturarak. Merhaba aşağıdaki örnek adlı bir NSG kuralı oluşturur *myBackendNSGRule* ile [yeni AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig):

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

Ekle *myBackEndSubnet* çok*myVNet* ile [Ekle AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/add-azurermvirtualnetworksubnetconfig):

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

bir SQL Server görüntüsü kullanarak arka uç VM Hello en kolay yolu toocreate hello var. Bu öğretici yalnızca hello VM hello veritabanı sunucusuyla oluşturur, ancak hello veritabanına erişme hakkında bilgi sağlamaz.

Oluşturma *myBackendNic*:

```powershell
$backendNic = New-AzureRmNetworkInterface `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myBackendNic `
  -SubnetId $vnet.Subnets[1].Id
```

Merhaba kullanıcı adı ve parola hello VM Get-Credential ile Merhaba yönetici hesabı için gerekli ayarlayın:

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

kullanılan hello görüntü SQL Server'ın yüklü, ancak bu öğreticide kullanılmaz. Dahil edilen tooshow olduğu, nasıl bir VM toohandle web trafiği ve toohandle veritabanı yönetimi VM yapılandırabilirsiniz.

## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide oluşturduğunuz ve Azure ağları ilgili toovirtual makineler olarak güvenli. 

> [!div class="checklist"]
> * Sanal ağ oluşturma
> * Sanal ağ alt ağları oluşturma
> * Ağ güvenlik gruplarıyla ağ trafiğini denetleme
> * Eylem trafik kurallarını görüntüle

Azure Yedekleme'yi kullanarak sanal makinelerde güvenli hale getirme verileri izleme hakkında toohello sonraki öğretici toolearn ilerleyin. .

> [!div class="nextstepaction"]
> [Azure'da Windows sanal makineleri yedekleyin](./tutorial-backup-vms.md)
