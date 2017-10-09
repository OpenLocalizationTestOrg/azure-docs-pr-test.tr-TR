---
title: "yönetilen bir VM görüntüden Azure VM aaaCreate | Microsoft Docs"
description: "Merhaba Resource Manager dağıtım modelinde Azure PowerShell kullanarak genelleştirilmiş yönetilen VM görüntüsü Windows sanal makine oluşturun."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: cynthn
ms.openlocfilehash: 5036ef1533c144a9a328e94599b359e0166f337d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-from-a-managed-image"></a>Yönetilen bir görüntüden bir VM oluşturma

Azure yönetilen bir VM görüntüsünden birden çok VM oluşturabilirsiniz. Yönetilen bir VM görüntüsü hello bilgi gerekli toocreate hello işletim sistemi ve veri diskleri de dahil olmak üzere, bir VM içerir. Merhaba hello OS diskleri ve veri diskleri de dahil olmak üzere hello görüntüyü oluşturan, yönetilen diskleri olarak depolanan VHD. 


## <a name="prerequisites"></a>Ön koşullar

Toohave zaten gereksinim [yönetilen bir VM görüntüsü oluşturulan](capture-image-resource.md) oluşturmak için toouse hello yeni VM. 

Merhaba AzureRM.Compute ve AzureRM.Network PowerShell modülleri hello en son sürümüne sahip olduğunuzdan emin olun. PowerShell komut istemini yönetici olarak açın ve komut tooinstall aşağıdaki hello çalıştırın bunları.

```powershell
Install-Module AzureRM.Compute,AzureRM.Network
```
Daha fazla bilgi için bkz: [Azure PowerShell sürüm](/powershell/azure/overview).



## <a name="collect-information-about-hello-image"></a>Merhaba görüntü ile ilgili bilgileri toplama

İlk biz hello görüntü ile ilgili temel bilgileri toogather gerekir ve hello görüntüsü için bir değişken oluşturun. Bu örnek adında yönetilen bir VM görüntüsü kullanan **myImage** diğer bir deyişle içinde hello **myResourceGroup** hello kaynak grubunda **Batı Orta ABD** konumu. 

```powershell
$rgName = "myResourceGroup"
$location = "West Central US"
$imageName = "myImage"
$image = Get-AzureRMImage -ImageName $imageName -ResourceGroupName $rgName
```

## <a name="create-a-virtual-network"></a>Sanal ağ oluşturma
Merhaba vNet ve alt hello oluşturma [sanal ağ](../../virtual-network/virtual-networks-overview.md).

1. Merhaba alt ağ oluşturun. Bu örnek adlı bir alt ağı oluşturur **mySubnet** hello adres öneki ile **10.0.0.0/24**.  
   
    ```powershell
    $subnetName = "mySubnet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. Merhaba sanal ağ oluşturun. Bu örnek adlı bir sanal ağ oluşturur **myVnet** hello adres öneki ile **10.0.0.0/16**.  
   
    ```powershell
    $vnetName = "myVnet"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

## <a name="create-a-public-ip-address-and-network-interface"></a>Ortak IP adresi ve ağ arabirimi oluşturma

ihtiyacınız tooenable iletişimi hello sanal ağındaki hello sanal makineyle bir [genel IP adresi](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) ve ağ arabirimi.

1. Bir ortak IP adresi oluşturun. Bu örnek adlı ortak IP adresi oluşturur **myPip**. 
   
    ```powershell
    $ipName = "myPip"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. Merhaba NIC oluşturun Bu örnek, adlandırılmış bir NIC oluşturur **myNic**. 
   
    ```powershell
    $nicName = "myNic"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName -Location $location `
        -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

## <a name="create-hello-network-security-group-and-an-rdp-rule"></a>Merhaba ağ güvenlik grubu ve bir RDP kuralı oluşturma

toobe mümkün toolog tooyour içinde RDP kullanarak VM toohave 3389 numaralı bağlantı noktası üzerinde RDP erişimine izin veren bir ağ güvenlik kuralı (NSG) gerekir. 

Bu örnekte adlı bir NSG oluşturulur **myNsg** adlı kuralı içeren **myRdpRule** 3389 numaralı bağlantı noktası RDP trafiğine izin veren. Nsg'ler hakkında daha fazla bilgi için bkz: [bağlantı noktalarını tooa VM PowerShell kullanarak Azure içinde açma](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

```powershell
$nsgName = "myNsg"
$ruleName = "myRdpRule"
$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name $ruleName -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389

$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
```


## <a name="create-a-variable-for-hello-virtual-network"></a>Merhaba sanal ağ için bir değişken oluşturma

Tamamlanan hello sanal ağ için bir değişken oluşturun. 

```powershell
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName

```

## <a name="get-hello-credentials-for-hello-vm"></a>Merhaba VM Hello kimlik bilgilerini alma

Merhaba aşağıdaki cmdlet'i yeni bir kullanıcı adı ve parola toouse hello yerel yönetici hesabı olarak hello VM uzaktan erişmek için gireceğiniz bir pencere açılır. 

```powershell
$cred = Get-Credential
```

## <a name="set-variables-for-hello-vm-name-computer-name-and-hello-size-of-hello-vm"></a>Merhaba VM kümesi değişkenleri adı, bilgisayar adı ve hello hello VM boyutu

1. Merhaba VM adı ve bilgisayar adı için değişkenler oluşturun. Bu örnek hello VM adı olarak ayarlar **myVM** ve hello bilgisayar adı olarak **Bilgisayarım**.

    ```powershell
    $vmName = "myVM"
    $computerName = "myComputer"
    ```
2. Merhaba hello sanal makine boyutunu ayarlayın. Bu örnekte **Standard_DS1_v2** VM boyuta sahip. Merhaba bkz [VM boyutları](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-sizes/) daha fazla bilgi için.

    ```powershell
    $vmSize = "Standard_DS1_v2"
    ```

3. Merhaba VM adını ve boyutunu toohello VM yapılandırmasına ekleyin.

```powershell
$vm = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize
```

## <a name="set-hello-vm-image-as-source-image-for-hello-new-vm"></a>Set hello VM görüntüsü hello için kaynak görüntüsü olarak yeni VM

Yönetilen hello VM görüntüsü Hello Kimliğini kullanarak hello kaynak görüntüsü ayarlayın.

```powershell
$vm = Set-AzureRmVMSourceImage -VM $vm -Id $image.Id
```

## <a name="set-hello-os-configuration-and-add-hello-nic"></a>Merhaba işletim sistemi yapılandırması ayarlayın ve hello NIC ekleyin

Merhaba depolama türü (PremiumLRS veya StandardLRS) ve hello işletim sistemi diski hello boyutunu girin. Bu örnek hello hesap türü çok ayarlar**PremiumLRS**, disk boyutu çok hello**128 GB** ve disk çok önbelleğe alma**ReadWrite**.

```powershell
$vm = Set-AzureRmVMOSDisk -VM $vm  -StorageAccountType PremiumLRS -DiskSizeInGB 128 `
-CreateOption FromImage -Caching ReadWrite

$vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName $computerName `
-Credential $cred -ProvisionVMAgent -EnableAutoUpdate

$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

## <a name="create-hello-vm"></a>Merhaba VM oluşturma

Oluşturma biz yerleşik ve hello depolanan hello Yapılandırması'nı kullanarak yeni Vm hello **$vm** değişkeni.

```powershell
New-AzureRmVM -VM $vm -ResourceGroupName $rgName -Location $location
```

## <a name="verify-that-hello-vm-was-created"></a>VM oluşturulduğu bu hello doğrulayın
Tamamlandığında, yeni VM hello oluşturulan hello görmelisiniz [Azure portal](https://portal.azure.com) altında **Gözat** > **sanal makineleri**, veya hello aşağıdakileri kullanarak PowerShell komutları:

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a>Sonraki adımlar
Yeni sanal makinenizi Azure PowerShell ile toomanage bkz [oluşturma ve hello Azure PowerShell modülü ile Windows sanal makineleri yönetme](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

