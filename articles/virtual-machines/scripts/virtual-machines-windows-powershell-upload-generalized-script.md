---
title: "genelleştirilmiş bir VHD tooAzure PowerShell komut dosyası örneği aaaUpload | Microsoft Docs"
description: "PowerShell komut dosyası tooupload genelleştirilmiş bir VHD tooAzure örnek ve hello resource manager dağıtım modeli ve yönetilen diskleri kullanarak yeni bir VM oluşturun."
services: virtual-machines-windows
documentationcenter: virtual-machines
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/18/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 72b4ff09eb7a6ba1604b9d5cbac51e60eded7545
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="sample-script-tooupload-a-vhd-tooazure-and-create-a-new-vm"></a>Örnek bir VHD tooAzure tooupload komut dosyasını hazırlamak ve yeni bir VM oluşturun

Bu komut dosyasını bir yerel .vhd dosyası genelleştirilmiş bir sanal makineden alır ve tooAzure yükler, yönetilen Disk görüntüsü oluşturur ve hello toocreate yeni bir VM kullanır.

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Örnek komut dosyası

```powershell
# Provide values for hello variables
$resourceGroup = 'myResourceGroup'
$location = 'EastUS'
$storageaccount = 'mystorageaccount'
$storageType = 'Standard_LRS'
$containername = 'mycontainer'
$localPath = 'C:\Users\Public\Documents\Hyper-V\VHDs\generalized.vhd'
$vmName = 'myVM'
$imageName = 'myImage'
$vhdName = 'myUploadedVhd.vhd'
$diskSizeGB = '128'
$subnetName = 'mySubnet'
$vnetName = 'myVnet'
$ipName = 'myPip'
$nicName = 'myNic'
$nsgName = 'myNsg'
$ruleName = 'myRdpRule'
$vmName = 'myVM'
$computerName = 'myComputerName'
$vmSize = 'Standard_DS1_v2'

# Get hello username and password toobe used for hello administrators account on hello VM. 
# This is used when connecting toohello VM using RDP.

$cred = Get-Credential

# Upload hello VHD
New-AzureRmResourceGroup -Name $resourceGroup -Location $location
New-AzureRmStorageAccount -ResourceGroupName $resourceGroup -Name $storageAccount -Location $location `
    -SkuName $storageType -Kind "Storage"
$urlOfUploadedImageVhd = ('https://' + $storageaccount + '.blob.core.windows.net/' + $containername + '/' + $vhdName)
Add-AzureRmVhd -ResourceGroupName $resourceGroup -Destination $urlOfUploadedImageVhd `
    -LocalFilePath $localPath

# Note: Uploading hello VHD may take awhile!

# Create a managed image from hello uploaded VHD 
$imageConfig = New-AzureRmImageConfig -Location $location
$imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsType Windows -OsState Generalized `
    -BlobUri $urlOfUploadedImageVhd
$image = New-AzureRmImage -ImageName $imageName -ResourceGroupName $resourceGroup -Image $imageConfig
 
# Create hello networking resources
$singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
$vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $resourceGroup -Location $location `
    -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
$pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $resourceGroup -Location $location `
    -AllocationMethod Dynamic
$nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $resourceGroup -Location $location `
    -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name $ruleName -Description 'Allow RDP' -Access Allow `
    -Protocol Tcp -Direction Inbound -Priority 110 -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $resourceGroup -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $resourceGroup -Name $vnetName

# Start building hello VM configuration
$vm = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize

# Set hello VM image as source image for hello new VM
$vm = Set-AzureRmVMSourceImage -VM $vm -Id $image.Id

# Finish hello VM configuration and add hello NIC.
$vm = Set-AzureRmVMOSDisk -VM $vm  -DiskSizeInGB $diskSizeGB -CreateOption FromImage -Caching ReadWrite
$vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName $computerName -Credential $cred `
    -ProvisionVMAgent -EnableAutoUpdate
$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id

# Create hello VM
New-AzureRmVM -VM $vm -ResourceGroupName $resourceGroup -Location $location

# Verify that hello VM was created
$vmList = Get-AzureRmVM -ResourceGroupName $resourceGroup
$vmList.Name


```


<!-- 
[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-iis/create-windows-vm-iis.ps1 "Create VM IIS")] -->

## <a name="clean-up-deployment"></a>Dağıtımı temizleme 

Çalışma hello aşağıdaki tooremove hello kaynak grubu, VM ve tüm ilişkili kaynakları komutu.

```powershell
Remove-AzureRmResourceGroup -Name $resourceGroup
```

## <a name="script-explanation"></a>Komut dosyası açıklaması

Bu komut dosyası komutları toocreate hello dağıtım aşağıdaki hello kullanır. Merhaba tablosundaki her öğesi toocommand belirli belgeleri bağlar.

| Komut                                                                                                             | Notlar                                                                                                                                                                                |
|---------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [Yeni-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup)                           | Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.                                                                                                                          |
| [Yeni-AzureRmStorageAccount](/powershell/module/azurerm.resources/new-azurermstorageaccount)                         | Bir depolama hesabı oluşturur.                                                                                                                                                           |
| [Ekleme AzureRmVhd](/powershell/module/azurerm.resources/add-azurermvhd)                                               | Bir sanal sabit diskten bir şirket içi sanal makine tooa blob Azure bulut depolama hesabında karşıya yükleme.                                                                       |
| [AzureRmImageConfig yeni](/powershell/module/azurerm.resources/new-azurermimageconfig)                               | Yapılandırılabilir Resim nesnesi oluşturur.                                                                                                                                                 |
| [Set-AzureRmImageOsDisk](/powershell/module/azurerm.resources/set-azurermimageosdisk)                               | Merhaba işletim sistemi görüntüsü nesne üzerinde disk özelliklerini ayarlar.                                                                                                                        |
| [AzureRmImage yeni](/powershell/module/azurerm.resources/new-azurermimage)                                           | Yeni bir görüntü oluşturur.                                                                                                                                                                 |
| [AzureRmVirtualNetworkSubnetConfig yeni](/powershell/module/azurerm.resources/new-azurermvirtualnetworksubnetconfig) | Bir alt ağ yapılandırması oluşturur. Bu yapılandırma ile Merhaba sanal ağ oluşturma işleminde kullanılır.                                                                                |
| [Yeni-AzureRmVirtualNetwork](/powershell/module/azurerm.resources/new-azurermvirtualnetwork)                         | Sanal ağ oluşturur.                                                                                                                                                           |
| [AzureRmPublicIpAddress yeni](/powershell/module/azurerm.resources/new-azurermpublicipaddress)                       | Bir ortak IP adresi oluşturur.                                                                                                                                                         |
| [AzureRmNetworkInterface yeni](/powershell/module/azurerm.resources/new-azurermnetworkinterface)                     | Bir ağ arabirimi oluşturur.                                                                                                                                                         |
| [AzureRmNetworkSecurityRuleConfig yeni](/powershell/module/azurerm.resources/new-azurermnetworksecurityruleconfig)   | Bir ağ güvenlik grubu kural yapılandırması oluşturur. Merhaba NSG oluşturulduğunda bu kullanılan toocreate bir NSG kuralı yapılandırmadır.                                                       |
| [AzureRmNetworkSecurityGroup yeni](/powershell/module/azurerm.resources/new-azurermnetworksecuritygroup)             | Bir ağ güvenlik grubu oluşturur.                                                                                                                                                    |
| [Get-AzureRmVirtualNetwork](/powershell/module/azurerm.resources/get-azurermvirtualnetwork)                         | Bir sanal ağ, bir kaynak grubunda alır.                                                                                                                                          |
| [AzureRmVMConfig yeni](/powershell/module/azurerm.resources/new-azurermvmconfig)                                     | Bir VM yapılandırması oluşturur. Bu yapılandırma VM adı, işletim sistemi ve yönetici kimlik bilgileri gibi bilgileri içerir. Merhaba yapılandırma VM oluşturma sırasında kullanılır. |
| [Set-AzureRmVMSourceImage](/powershell/module/azurerm.resources/set-azurermvmsourceimage)                           | Bir sanal makine için bir görüntü belirtir.                                                                                                                                            |
| [Set-AzureRmVMOSDisk](/powershell/module/azurerm.resources/set-azurermvmosdisk)                                     | Merhaba işletim sistemi, bir sanal makineye disk özelliklerini ayarlar.                                                                                                                      |
| [Set-AzureRmVMOperatingSystem](/powershell/module/azurerm.resources/set-azurermvmoperatingsystem)                   | Merhaba işletim sistemi, bir sanal makineye disk özelliklerini ayarlar.                                                                                                                      |
| [Ekleme AzureRmVMNetworkInterface](/powershell/module/azurerm.resources/add-azurermvmnetworkinterface)                 | Bir ağ arabirimi tooa sanal makineye ekler.                                                                                                                                       |
| [Yeni-AzureRmVM](/powershell/module/azurerm.resources/new-azurermvm)                                                 | Bir sanal makine oluşturun.                                                                                                                                                            |
| [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup)                     | Bir kaynak grubu ve içerdiği tüm kaynaklar kaldırır.                                                                                                                         |

## <a name="next-steps"></a>Sonraki adımlar

Hello Azure PowerShell modülü hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](/powershell/azure/overview).

Ek sanal makine PowerShell komut dosyası örnekleri hello bulunabilir [Azure Windows VM belgelerine](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
