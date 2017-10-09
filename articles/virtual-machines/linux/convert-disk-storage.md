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
# <a name="convert-azure-managed-disks-storage-from-standard-toopremium-and-vice-versa"></a><span data-ttu-id="e6a5b-103">Azure Dönüştür yönetilen diskleri depolama standart toopremium ve tersi</span><span class="sxs-lookup"><span data-stu-id="e6a5b-103">Convert Azure managed disks storage from standard toopremium, and vice versa</span></span>

<span data-ttu-id="e6a5b-104">Yönetilen diskleri iki depolama seçenekleri sunar: [Premium](../../storage/storage-premium-storage.md) (SSD tabanlı) ve [standart](../../storage/storage-standard-storage.md) (HDD tabanlı).</span><span class="sxs-lookup"><span data-stu-id="e6a5b-104">Managed disks offers two storage options: [Premium](../../storage/storage-premium-storage.md) (SSD-based) and [Standard](../../storage/storage-standard-storage.md) (HDD-based).</span></span> <span data-ttu-id="e6a5b-105">Performans ihtiyaçlarınıza göre en düşük kapalı kalma süresi ile Merhaba iki seçenekten tooeasily anahtar sağlar.</span><span class="sxs-lookup"><span data-stu-id="e6a5b-105">It allows you tooeasily switch between hello two options with minimal downtime based on your performance needs.</span></span> <span data-ttu-id="e6a5b-106">Bu özellik, yönetilmeyen diskler için kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="e6a5b-106">This capability is not available for unmanaged disks.</span></span> <span data-ttu-id="e6a5b-107">Ancak kolayca [Dönüştür toomanaged diskleri](convert-unmanaged-to-managed-disks.md) hello iki seçenekten tooeasily anahtar.</span><span class="sxs-lookup"><span data-stu-id="e6a5b-107">But you can easily [convert toomanaged disks](convert-unmanaged-to-managed-disks.md) tooeasily switch between hello two options.</span></span>

<span data-ttu-id="e6a5b-108">Bu makalede, standart toopremium ve bunun tersi de Azure CLI kullanarak tooconvert diskleri nasıl yönetileceğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="e6a5b-108">This article shows you how tooconvert managed disks from standard toopremium, and vice versa by using Azure CLI.</span></span> <span data-ttu-id="e6a5b-109">Yükseltmek veya tooinstall gerekir, bkz: [Azure CLI 2.0 yükleme](/cli/azure/install-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="e6a5b-109">If you need tooinstall or upgrade it, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli.md).</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="e6a5b-110">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="e6a5b-110">Before you begin</span></span>

* <span data-ttu-id="e6a5b-111">Merhaba dönüştürme hello VM yeniden başlatılmasını gerektirir, bu nedenle, diskleri depolama hello geçiş önceden var olan bir bakım penceresi sırasında zamanlayın.</span><span class="sxs-lookup"><span data-stu-id="e6a5b-111">hello conversion requires a restart of hello VM, so schedule hello migration of your disks storage during a pre-existing maintenance window.</span></span> 
* <span data-ttu-id="e6a5b-112">Yönetilmeyen diskler, ilk kez kullanıyorsanız, [Dönüştür toomanaged diskleri](convert-unmanaged-to-managed-disks.md) toouse Bu makale tooswitch hello iki depolama seçenekleri arasında.</span><span class="sxs-lookup"><span data-stu-id="e6a5b-112">If you are using unmanaged disks, first [convert toomanaged disks](convert-unmanaged-to-managed-disks.md) toouse this article tooswitch between hello two storage options.</span></span> 


## <a name="convert-all-hello-managed-disks-of-a-vm-from-standard-toopremium-and-vice-versa"></a><span data-ttu-id="e6a5b-113">Tüm hello dönüştürme yönetilen VM diskleri standart toopremium ve tersi</span><span class="sxs-lookup"><span data-stu-id="e6a5b-113">Convert all hello managed disks of a VM from standard toopremium, and vice versa</span></span>

<span data-ttu-id="e6a5b-114">Aşağıdaki örneğine hello gösteriyoruz nasıl tooswitch tüm standart toopremium depolama biriminden bir VM diskleri hello.</span><span class="sxs-lookup"><span data-stu-id="e6a5b-114">In hello following example, we show how tooswitch all hello disks of a VM from standard toopremium storage.</span></span> <span data-ttu-id="e6a5b-115">toouse premium disklerin yönetilen, VM'yi kullanmalısınız bir [VM boyutu](sizes.md) premium storage destekler.</span><span class="sxs-lookup"><span data-stu-id="e6a5b-115">toouse premium managed disks, your VM must use a [VM size](sizes.md) that supports premium storage.</span></span> <span data-ttu-id="e6a5b-116">Bu örnek ayrıca premium depolama destekleyen tooa boyutu geçer.</span><span class="sxs-lookup"><span data-stu-id="e6a5b-116">This example also switches tooa size that supports premium storage.</span></span>

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
## <a name="convert-a-managed-disk-from-standard-toopremium-and-vice-versa"></a><span data-ttu-id="e6a5b-117">Yönetilen bir diske Dönüştür standart toopremium ve tersi</span><span class="sxs-lookup"><span data-stu-id="e6a5b-117">Convert a managed disk from standard toopremium, and vice versa</span></span>

<span data-ttu-id="e6a5b-118">Geliştirme ve test iş yükü için standart ve premium disklerin tooreduce toohave karışımını maliyetinizi isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e6a5b-118">For your dev/test workload, you may want toohave mixture of standard and premium disks tooreduce your cost.</span></span> <span data-ttu-id="e6a5b-119">Bu, daha iyi performans gerektiren hello disk toopremium depolama yükselterek gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e6a5b-119">You can accomplish it by upgrading toopremium storage, only hello disks that require better performance.</span></span> <span data-ttu-id="e6a5b-120">Aşağıdaki örneğine hello gösteriyoruz nasıl tooswitch bir VM tek bir disk standart toopremium depolama biriminden ve tersi.</span><span class="sxs-lookup"><span data-stu-id="e6a5b-120">In hello following example, we show how tooswitch a single disk of a VM from standard toopremium storage, and vice versa.</span></span> <span data-ttu-id="e6a5b-121">toouse premium disklerin yönetilen, VM'yi kullanmalısınız bir [VM boyutu](sizes.md) premium storage destekler.</span><span class="sxs-lookup"><span data-stu-id="e6a5b-121">toouse premium managed disks, your VM must use a [VM size](sizes.md) that supports premium storage.</span></span> <span data-ttu-id="e6a5b-122">Bu örnek ayrıca premium depolama destekleyen tooa boyutu geçer.</span><span class="sxs-lookup"><span data-stu-id="e6a5b-122">This example also switches tooa size that supports premium storage.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="e6a5b-123">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e6a5b-123">Next steps</span></span>

<span data-ttu-id="e6a5b-124">Kullanarak bir VM salt okunur bir kopyasını alın [anlık görüntüleri](snapshot-copy-managed-disk.md).</span><span class="sxs-lookup"><span data-stu-id="e6a5b-124">Take a read-only copy of a VM by using [snapshots](snapshot-copy-managed-disk.md).</span></span>

