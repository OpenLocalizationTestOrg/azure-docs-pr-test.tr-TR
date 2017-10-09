---
title: "aaaConvert Azure yönetilen diskleri depolama standart toopremium ve tersi | Microsoft Docs"
description: "Nasıl tooconvert Azure diskleri depolama standart toopremium ve tersi, Azure CLI kullanarak yönetilen."
services: virtual-machines-linux
documentationcenter: 
author: ramankum
manager: kavithag
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: ramankum
ms.openlocfilehash: 261d77202f7fd381085c4e25211a5d0026f43b01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="convert-azure-managed-disks-storage-from-standard-toopremium-and-vice-versa"></a>Azure Dönüştür yönetilen diskleri depolama standart toopremium ve tersi

Yönetilen diskleri iki depolama seçenekleri sunar: [Premium](../../storage/storage-premium-storage.md) (SSD tabanlı) ve [standart](../../storage/storage-standard-storage.md) (HDD tabanlı). Performans ihtiyaçlarınıza göre en düşük kapalı kalma süresi ile Merhaba iki seçenekten tooeasily anahtar sağlar. Bu özellik, yönetilmeyen diskler için kullanılamaz. Ancak kolayca [Dönüştür toomanaged diskleri](convert-unmanaged-to-managed-disks.md) hello iki seçenekten tooeasily anahtar.

Bu makalede, standart toopremium ve bunun tersi de Azure CLI kullanarak tooconvert diskleri nasıl yönetileceğini gösterir. Yükseltmek veya tooinstall gerekir, bkz: [Azure CLI 2.0 yükleme](/cli/azure/install-azure-cli.md). 

## <a name="before-you-begin"></a>Başlamadan önce

* Merhaba dönüştürme hello VM yeniden başlatılmasını gerektirir, bu nedenle, diskleri depolama hello geçiş önceden var olan bir bakım penceresi sırasında zamanlayın. 
* Yönetilmeyen diskler, ilk kez kullanıyorsanız, [Dönüştür toomanaged diskleri](convert-unmanaged-to-managed-disks.md) toouse Bu makale tooswitch hello iki depolama seçenekleri arasında. 


## <a name="convert-all-hello-managed-disks-of-a-vm-from-standard-toopremium-and-vice-versa"></a>Tüm hello dönüştürme yönetilen VM diskleri standart toopremium ve tersi

Aşağıdaki örneğine hello gösteriyoruz nasıl tooswitch tüm standart toopremium depolama biriminden bir VM diskleri hello. toouse premium disklerin yönetilen, VM'yi kullanmalısınız bir [VM boyutu](sizes.md) premium storage destekler. Bu örnek ayrıca premium depolama destekleyen tooa boyutu geçer.

 ```azurecli

#resource group that contains hello virtual machine
rgName='yourResourceGroup'

#Name of hello virtual machine
vmName='yourVM'

#Premium capable size 
#Required only if converting from standard toopremium
size='Standard_DS2_v2'

#Choose between Standard_LRS and Premium_LRS based on your scenario
sku='Premium_LRS'

#Deallocate hello VM before changing hello size of hello VM
az vm deallocate --name $vmName --resource-group $rgName

#Change hello VM size tooa size that supports premium storage 
#Skip this step if converting storage from premium toostandard
az vm resize --resource-group $rgName --name $vmName --size $size

#Update hello sku of all hello data disks 
az vm show -n $vmName -g $rgName --query storageProfile.dataDisks[*].managedDisk -o tsv \
 | awk -v sku=$sku '{system("az disk update --sku "sku" --ids "$1)}'

#Update hello sku of hello OS disk
az vm show -n $vmName -g $rgName --query storageProfile.osDisk.managedDisk -o tsv \
| awk -v sku=$sku '{system("az disk update --sku "sku" --ids "$1)}'

az vm start --name $vmName --resource-group $rgName

```
## <a name="convert-a-managed-disk-from-standard-toopremium-and-vice-versa"></a>Yönetilen bir diske Dönüştür standart toopremium ve tersi

Geliştirme ve test iş yükü için standart ve premium disklerin tooreduce toohave karışımını maliyetinizi isteyebilirsiniz. Bu, daha iyi performans gerektiren hello disk toopremium depolama yükselterek gerçekleştirebilirsiniz. Aşağıdaki örneğine hello gösteriyoruz nasıl tooswitch bir VM tek bir disk standart toopremium depolama biriminden ve tersi. toouse premium disklerin yönetilen, VM'yi kullanmalısınız bir [VM boyutu](sizes.md) premium storage destekler. Bu örnek ayrıca premium depolama destekleyen tooa boyutu geçer.

 ```azurecli

#resource group that contains hello managed disk
rgName='yourResourceGroup'

#Name of your managed disk
diskName='yourManagedDiskName'

#Premium capable size 
#Required only if converting from standard toopremium
size='Standard_DS2_v2'

#Choose between Standard_LRS and Premium_LRS based on your scenario
sku='Premium_LRS'

#Get hello parent VM Id 
vmId=$(az disk show --name $diskName --resource-group $rgName --query managedBy --output tsv)

#Deallocate hello VM before changing hello size of hello VM
az vm deallocate --ids $vmId 

#Change hello VM size tooa size that supports premium storage 
#Skip this step if converting storage from premium toostandard
az vm resize --ids $vmId --size $size

# Update hello sku
az disk update --sku $sku --name $diskName --resource-group $rgName 

az vm start --ids $vmId 
```

## <a name="next-steps"></a>Sonraki adımlar

Kullanarak bir VM salt okunur bir kopyasını alın [anlık görüntüleri](snapshot-copy-managed-disk.md).

