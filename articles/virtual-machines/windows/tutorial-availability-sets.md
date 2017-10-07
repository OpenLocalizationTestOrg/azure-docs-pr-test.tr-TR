---
title: "aaaAvailability öğretici azure'da Windows sanal makineleri için ayarlar | Microsoft Docs"
description: "Merhaba kullanılabilirlik kümeleri için Windows azure'da VM hakkında bilgi edinin."
documentationcenter: 
services: virtual-machines-windows
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
ms.date: 05/08/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 853775c5f126dd815c1933f9d71d2274a75ea661
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-availability-sets"></a>Nasıl toouse kullanılabilirlik kümeleri

Bu öğreticide, nasıl tooincrease hello kullanılabilirliği ve güvenilirliği bir özelliği kullanarak azure'da sanal makine çözümlerinizi kullanılabilirlik kümeleri adlı öğreneceksiniz. Kullanılabilirlik kümeleri, Azure üzerinde dağıttığınız VM'lerin birden çok yalıtılmış donanım kümeler arasında dağıtılır, hello emin olun. Bunun yapılması Azure içinde bir donanım veya yazılım hatası olur, alt kümesini, VM'ler etkilenir ve çözümünüzün genel kullanılabilir ve işletimsel kullanmadan müşterilerinizin hello açısından kalacak sağlar. 

Bu öğreticide şunların nasıl yapıldığını öğreneceksiniz:

> [!div class="checklist"]
> * Kullanılabilirlik kümesi oluşturma
> * Bir kullanılabilirlik kümesine bir VM oluşturma
> * Kullanılabilir VM boyutları denetleyin

Bu öğretici hello Azure PowerShell modülü 3,6 veya sonraki bir sürümü gerektiriyor. Çalıştırma ` Get-Module -ListAvailable AzureRM` toofind hello sürümü. Tooupgrade gerekirse bkz [yükleme Azure PowerShell Modülü](/powershell/azure/install-azurerm-ps).

## <a name="availability-set-overview"></a>Kullanılabilirlik kümesi'ne genel bakış

Bir kullanılabilirlik kümesi kullanabileceğiniz bir mantıksal bir gruplandırma bir Azure veri merkezi içinde dağıtıldığında içine yerleştirin hello VM kaynakları birbirinden yalıtılmış Azure tooensure içinde bir özelliktir. Bu hello VM'ler arasında birden fazla fiziksel sunucu çalıştırmak bir kullanılabilirlik kümesi içinde yerleştirin Azure sağlar, işlem rafları, depolama birimi ve ağ anahtarları. Bu hello olay bir donanım ya da Azure yazılım hatası yalnızca bir alt kümesini, VM'ler etkilenir ve genel uygulamanız kalması ve toobe kullanılabilir tooyour müşteriler devam sağlar. Toobuild güvenilir bulut çözümleri istediğiniz kullanılabilirlik kümelerini kullanarak bir önemli özelliği tooleverage durumdur.

Şimdi burada 4 ön uç web sunucusu ve bir veritabanı ana bilgisayar 2 arka uç VM kullanmak bir tipik VM tabanlı çözümünü göz önünde bulundurun. Azure ile Vm'leriniz dağıtmadan önce toodefine iki kullanılabilirlik kümeleri istiyor: hello "web" katmanı ve bir kullanılabilirlik kümesi için hello "veritabanı" katmanı için bir kullanılabilirlik kümesi. Ardından, bir parametre toohello az vm komutu oluşturun ve Azure otomatik olarak o hello hello içinde oluşturduğunuz VM'ler sağlayacak şekilde ayarlayın hello kullanılabilirlik belirtebilirsiniz yeni bir VM oluştururken kümesi yalıtılmış birden çok fiziksel donanım kaynaklarına arasında. Bir Web sunucusu veya veritabanı sunucusu VM'ler üzerinde çalıştığı hello fiziksel donanım bir sorun varsa, o hello bilmeniz yani farklı donanıma olduğundan Web sunucusu ve veritabanı VM'ler diğer örneklerini düzgün çalışır durumda.

Azure içindeki güvenilir tabanlı VM çözümleri toodeploy istediğinizde kullanılabilirlik kümeleri her zaman kullanmalısınız.

## <a name="create-an-availability-set"></a>Kullanılabilirlik kümesi oluşturma

Kullanılabilirlik kümesi kullanarak oluşturabileceğiniz [yeni AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset). Bu örnekte, güncelleştirme ve hata etki alanları iki hello sayısı ayarlarız *2* hello kullanılabilirlik adlandırılmış kümesi için *myAvailabilitySet* hello içinde *myResourceGroupAvailability*kaynak grubu.

Bir kaynak grubu oluşturun.

```powershell
New-AzureRmResourceGroup -Name myResourceGroupAvailability -Location EastUS
```


```powershell
New-AzureRmAvailabilitySet `
   -Location EastUS `
   -Name myAvailabilitySet `
   -ResourceGroupName myResourceGroupAvailability `
   -Managed `
   -PlatformFaultDomainCount 2 `
   -PlatformUpdateDomainCount 2
```

## <a name="create-vms-inside-an-availability-set"></a>VM'ler içinde bir kullanılabilirlik kümesi oluştur

Sanal makineleri hello kullanılabilirlik kümesi toomake hello donanım üzerinde doğru şekilde dağıtıldığından emin içinde oluşturulan toobe gerekir. Var olan VM tooan kullanılabilirlik kümesi oluşturulduktan sonra eklenemez. 

bir konumda Hello donanım toomultiple güncelleştirme etki alanları ve hata etki alanları ayrılmıştır. Bir **güncelleştirme etki alanı** VM'ler ve hello yeniden temel alınan fiziksel donanım oluşan bir gruptur aynı anda. İçinde sanal makineleri aynı hello **hata etki alanı** ortak bir güç kaynağı ve ağ anahtarı yanı sıra genel depolama paylaşın. 

Yapılandırma kullanarak bir VM oluştururken [yeni AzureRMVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig) hello kullanılarak ayarlanan hello kullanılabilirliği belirtmek `-AvailabilitySetId` hello kullanılabilirlik kümesinin parametresi toospecify hello kimliği.

İle 2 VM oluşturma [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) hello kullanılabilirlik kümesinde.

```powershell
$availabilitySet = Get-AzureRmAvailabilitySet `
    -ResourceGroupName myResourceGroupAvailability `
    -Name myAvailabilitySet

$cred = Get-Credential -Message "Enter a username and password for hello virtual machine."

$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -AddressPrefix 192.168.1.0/24
$vnet = New-AzureRmVirtualNetwork `
    -ResourceGroupName myResourceGroupAvailability `
    -Location EastUS `
    -Name MYvNET `
    -AddressPrefix 192.168.0.0/16 `
    -Subnet $subnetConfig

for ($i=1; $i -le 2; $i++)
{
   $pip = New-AzureRmPublicIpAddress `
        -ResourceGroupName myResourceGroupAvailability `
        -Location EastUS `
        -Name "mypublicdns$(Get-Random)" `
        -AllocationMethod Static `
        -IdleTimeoutInMinutes 4

   $nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig `
        -Name myNetworkSecurityGroupRuleRDP$i `
        -Protocol Tcp `
        -Direction Inbound `
        -Priority 1000 `
        -SourceAddressPrefix * `
        -SourcePortRange * `
        -DestinationAddressPrefix * `
        -DestinationPortRange 3389 `
        -Access Allow

   $nsg = New-AzureRmNetworkSecurityGroup `
        -ResourceGroupName myResourceGroupAvailability `
        -Location EastUS `
        -Name myNetworkSecurityGroup$i `
        -SecurityRules $nsgRuleRDP

   $nic = New-AzureRmNetworkInterface `
        -Name myNic$i `
        -ResourceGroupName myResourceGroupAvailability `
        -Location EastUS `
        -SubnetId $vnet.Subnets[0].Id `
        -PublicIpAddressId $pip.Id `
        -NetworkSecurityGroupId $nsg.Id

   # Here is where we specify hello availability set
   $vm = New-AzureRmVMConfig `
        -VMName myVM$i `
        -VMSize Standard_D1 `
        -AvailabilitySetId $availabilitySet.Id

   $vm = Set-AzureRmVMOperatingSystem `
        -VM $vm `
        -Windows -ComputerName myVM$i `   
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
   $vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
   New-AzureRmVM `
        -ResourceGroupName myResourceGroupAvailability `
        -Location EastUS `
        -VM $vm
}

```

Birkaç dakika toocreate alır ve her iki VM yapılandırın. Tamamlandığında, temel alınan donanım hello arasında dağıtılmış 2 sanal makine sahip olur. 

## <a name="check-for-available-vm-sizes"></a>Kullanılabilir VM boyutları denetle 

Daha fazla sanal makineleri toohello kullanılabilirlik kümesi daha sonra ekleyebilirsiniz, ancak hangi VM boyutları hello donanımda kullanılabilir tooknow gerekir. Kullanım [Get-AzureRMVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) tüm hello kullanılabilir boyutları hello donanımda hello kullanılabilirlik kümesi için küme toolist.

```powershell
Get-AzureRmVMSize `
   -AvailabilitySetName myAvailabilitySet `
   -ResourceGroupName myResourceGroupAvailability  
```

## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide, şunların nasıl yapıldığını öğrendiniz:

> [!div class="checklist"]
> * Kullanılabilirlik kümesi oluşturma
> * Bir kullanılabilirlik kümesine bir VM oluşturma
> * Kullanılabilir VM boyutları denetleyin

Sanal makine ölçek kümeleri hakkında toohello sonraki öğretici toolearn ilerleyin.

> [!div class="nextstepaction"]
> [VM ölçek kümesi oluşturma](tutorial-create-vmss.md)


