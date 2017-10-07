---
title: "hello Azure PowerShell ile özel VM görüntüleri aaaCreate | Microsoft Docs"
description: "Öğretici - hello Azure PowerShell kullanarak özel bir VM görüntüsü oluşturun."
services: virtual-machines-windows
documentationcenter: virtual-machines
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/08/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 3a759fe1b7e7b72f531399b0f4a99e341713c6a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-image-of-an-azure-vm-using-powershell"></a>Özel bir Azure PowerShell kullanarak bir VM görüntüsü oluşturma

Özel resimler gibi Market görüntülerini olsa da, bunları kendiniz oluşturmanız. Özel resimler gibi uygulamalar, uygulama yapılandırmaları ve diğer işletim sistemi yapılandırmalarını önceden kullanılan toobootstrap yapılandırmaları olabilir. Bu öğreticide, kendi özel görüntünüzü bir Azure sanal makine oluşturun. Aşağıdakileri nasıl yapacağınızı öğrenirsiniz:

> [!div class="checklist"]
> * Sysprep ve VM'ler generalize
> * Özel görüntü oluşturma
> * Özel bir görüntüden bir VM oluşturma
> * Aboneliğinizdeki tüm hello görüntüler liste
> * Bir görüntü Sil

Bu öğretici hello Azure PowerShell modülü 3,6 veya sonraki bir sürümü gerektiriyor. Çalıştırma ` Get-Module -ListAvailable AzureRM` toofind hello sürümü. Tooupgrade gerekirse bkz [yükleme Azure PowerShell Modülü](/powershell/azure/install-azurerm-ps).

## <a name="before-you-begin"></a>Başlamadan önce

Merhaba adımları tootake mevcut bir VM'yi ve onu yeniden kullanılabilir özel bir görüntü, etkinleştirin toocreate yeni VM örnekleri nasıl kullanabileceğinizi ayrıntılı olarak açıklanmaktadır.

Bu öğreticide toocomplete hello örnek, mevcut bir sanal makine olması gerekir. Gerekirse, bu [komut dosyası örneği](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) sizin için bir tane oluşturabilirsiniz. Çalışma hello öğretici aracılığıyla değiştirdiğinizde hello kaynak grubu VM adları ve gerektiğinde.

## <a name="prepare-vm"></a>VM hazırlama

bir sanal makine görüntüsü toocreate genelleme hello ayırmasını kaldırma ve Azure'da genelleştirilmiş gibi VM hello kaynak işaretleme VM tarafından tooprepare hello VM gerekir.

### <a name="generalize-hello-windows-vm-using-sysprep"></a>Generalize Sysprep kullanarak Windows VM hello

Sysprep tüm kişisel hesap bilgilerinize, başka şeylerin kaldırır ve bir görüntü olarak kullanılan hello makine toobe hazırlar. Sysprep hakkında daha fazla ayrıntı için bkz: [nasıl tooUse Sysprep: Giriş](http://technet.microsoft.com/library/bb457073.aspx).


1. Toohello sanal makineye bağlanın.
2. Merhaba komut istemi penceresi bir yönetici olarak açın. Merhaba dizini çok değiştirmek*%windir%\system32\sysprep*ve ardından çalıştırın *sysprep.exe*.
3. Merhaba, **Sistem Hazırlama aracı** iletişim kutusunda *girin sistem Out-of-Box deneyimi (OOBE)*ve bu hello emin olun *Generalize* onay kutusu seçilidir.
4. İçinde **kapatma seçenekleri**seçin *kapatma* ve ardından **Tamam**.
5. Sysprep tamamlandığında hello sanal makineyi kapatır. **Merhaba VM yeniden başlatma**.

### <a name="deallocate-and-mark-hello-vm-as-generalized"></a>Deallocate ve hello VM genelleştirilmiş olarak işaretleyin

görüntüyü toocreate hello VM serbest ve Azure'da genelleştirilmiş olarak işaretlenen toobe gerekir.

VM deallocated hello kullanarak [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm).

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroupImages -Name myVM -Force
```

Hello sanal makinenin başlangıç durumu çok Ayarla`-Generalized` kullanarak [Set-AzureRmVm](/powershell/module/azurerm.compute/set-azurermvm). 
   
```powershell
Set-AzureRmVM -ResourceGroupName myResourceGroupImages -Name myVM -Generalized
```


## <a name="create-hello-image"></a>Merhaba görüntü oluşturma

Merhaba VM görüntüsünü kullanarak oluşturabileceğiniz artık [yeni AzureRmImageConfig](/powershell/module/azurerm.compute/new-azurermimageconfig) ve [yeni AzureRmImage](/powershell/module/azurerm.compute/new-azurermimage). Merhaba aşağıdaki örnekte oluşturur adlı bir resim *myImage* adlı bir VM'den *myVM*.

Merhaba sanal makine alın. 

```powershell
$vm = Get-AzureRmVM -Name myVM -ResourceGroupName myResourceGroupImages
```

Merhaba görüntü yapılandırmasını oluşturun.

```powershell
$image = New-AzureRmImageConfig -Location EastUS -SourceVirtualMachineId $vm.ID 
```

Merhaba görüntü oluşturma.

```powershell
New-AzureRmImage -Image $image -ImageName myImage -ResourceGroupName myResourceGroupImages
``` 

 
## <a name="create-vms-from-hello-image"></a>Sanal makineleri hello görüntüden oluşturma

Bir görüntü sahip olduğunuza göre bir veya daha fazla yeni VM'ler hello görüntüsünü oluşturabilirsiniz. Özel bir görüntüden bir VM oluşturma çok benzer toocreating bir Market görüntüsü kullanarak bir VM'i bağlıdır. Market görüntüsünü kullandığınızda, tooinformation hello görüntü, görüntü sağlayıcısı, teklif, SKU ve sürümü hakkında sahip. Özel bir görüntü ile tooprovide hello hello özel görüntü kaynak Kimliğini yeterlidir. 

Bir değişken oluşturuyoruz komut dosyası izleyen hello *$image* hello özel görüntü kullanma hakkında bilgi toostore [Get-AzureRmImage](/powershell/module/azurerm.compute/get-azurermimage) ve ardından kullanırız [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage)ve hello kullanarak hello kimliği belirtin *$image* değişken yeni oluşturduğumuz. 

Merhaba betiği oluşturur adlı bir VM'den *myVMfromImage* bizim Özel görüntüden yeni bir kaynak grubu adında *myResourceGroupFromImage* hello içinde *Batı ABD* konumu.


```powershell
$cred = Get-Credential -Message "Enter a username and password for hello virtual machine."

New-AzureRmResourceGroup -Name myResourceGroupFromImage -Location EastUS

$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -AddressPrefix 192.168.1.0/24

$vnet = New-AzureRmVirtualNetwork `
    -ResourceGroupName myResourceGroupFromImage `
    -Location EastUS `
    -Name MYvNET `
    -AddressPrefix 192.168.0.0/16 `
    -Subnet $subnetConfig

$pip = New-AzureRmPublicIpAddress `
    -ResourceGroupName myResourceGroupFromImage `
    -Location EastUS `
    -Name "mypublicdns$(Get-Random)" `
    -AllocationMethod Static `
    -IdleTimeoutInMinutes 4

  $nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig `
    -Name myNetworkSecurityGroupRuleRDP `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 1000 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 3389 `
    -Access Allow

  $nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName myResourceGroupFromImage `
    -Location EastUS `
    -Name myNetworkSecurityGroup `
    -SecurityRules $nsgRuleRDP

$nic = New-AzureRmNetworkInterface `
    -Name myNic `
    -ResourceGroupName myResourceGroupFromImage `
    -Location EastUS `
    -SubnetId $vnet.Subnets[0].Id `
    -PublicIpAddressId $pip.Id `
    -NetworkSecurityGroupId $nsg.Id

$vmConfig = New-AzureRmVMConfig `
    -VMName myVMfromImage `
    -VMSize Standard_D1 | Set-AzureRmVMOperatingSystem -Windows `
        -ComputerName myComputer `
        -Credential $cred 

# Here is where we create a variable toostore information about hello image 
$image = Get-AzureRmImage `
    -ImageName myImage `
    -ResourceGroupName myResourceGroupImages

# Here is where we specify that we want toocreate hello VM from and image and provide hello image ID
$vmConfig = Set-AzureRmVMSourceImage -VM $vmConfig -Id $image.Id

$vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic.Id

New-AzureRmVM `
    -ResourceGroupName myResourceGroupFromImage `
    -Location EastUS `
    -VM $vmConfig
```

## <a name="image-management"></a>Görüntü Yönetimi 

İşte bazı örnekler ortak yönetim görüntü görevlerinin nasıl ve ne toocomplete bunları PowerShell kullanarak.

Tüm görüntüleri ada göre listeler.

```powershell
$images = Find-AzureRMResource -ResourceType Microsoft.Compute/images 
$images.name
```

Görüntüyü silin. Bu örnek siler hello adlı görüntü *myOldImage* hello gelen *myResourceGroup*.

```powershell
Remove-AzureRmImage `
    -ImageName myOldImage `
    -ResourceGroupName myResourceGroup
```

## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide, özel bir VM görüntüsü oluşturuldu. Şunları öğrendiniz:

> [!div class="checklist"]
> * Sysprep ve VM'ler generalize
> * Özel görüntü oluşturma
> * Özel bir görüntüden bir VM oluşturma
> * Aboneliğinizdeki tüm hello görüntüler liste
> * Bir görüntü Sil

Toohello sonraki öğretici toolearn nasıl yüksek oranda kullanılabilir sanal makineler hakkında ilerleyin.

> [!div class="nextstepaction"]
> [Yüksek oranda kullanılabilir VM’ler oluşturma](tutorial-availability-sets.md)



