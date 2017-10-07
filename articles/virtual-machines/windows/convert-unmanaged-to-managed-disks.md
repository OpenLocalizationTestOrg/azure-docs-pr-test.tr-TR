---
title: "aaaConvert yönetilmeyenden Windows sanal makine disklerini toomanaged diskler - Azure yönetilen disk | Microsoft Docs"
description: "Merhaba Resource Manager dağıtım modelinde PowerShell kullanarak nasıl tooconvert yönetilmeyen diskleri toomanaged Windows VM'den diskler"
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
ms.date: 06/23/2017
ms.author: cynthn
ms.openlocfilehash: e8ed8694b0e776d22df26261e2fc8340bfe5cafa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="convert-a-windows-virtual-machine-from-unmanaged-disks-toomanaged-disks"></a><span data-ttu-id="566d1-103">Windows sanal makine yönetilmeyen diskleri toomanaged disklerden Dönüştür</span><span class="sxs-lookup"><span data-stu-id="566d1-103">Convert a Windows virtual machine from unmanaged disks toomanaged disks</span></span>

<span data-ttu-id="566d1-104">Yönetilmeyen diskleri kullanan bir mevcut Windows sanal makineleri (VM'ler) varsa, hello aracılığıyla hello VM'ler yönetilen toouse diskler dönüştürülebilir [Azure yönetilen diskleri](managed-disks-overview.md) hizmet.</span><span class="sxs-lookup"><span data-stu-id="566d1-104">If you have existing Windows virtual machines (VMs) that use unmanaged disks, you can convert hello VMs toouse managed disks through hello [Azure Managed Disks](managed-disks-overview.md) service.</span></span> <span data-ttu-id="566d1-105">Bu işlem hello işletim sistemi disk ve tüm eklenen veri disklerini dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="566d1-105">This process converts both hello OS disk and any attached data disks.</span></span>

<span data-ttu-id="566d1-106">Bu makale size nasıl gösterir Azure PowerShell kullanarak sanal makineleri tooconvert.</span><span class="sxs-lookup"><span data-stu-id="566d1-106">This article shows you how tooconvert VMs by using Azure PowerShell.</span></span> <span data-ttu-id="566d1-107">Yükseltmek veya tooinstall gerekir, bkz: [yükleyin ve Azure PowerShell yapılandırma](/powershell/azure/install-azurerm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="566d1-107">If you need tooinstall or upgrade it, see [Install and configure Azure PowerShell](/powershell/azure/install-azurerm-ps.md).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="566d1-108">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="566d1-108">Before you begin</span></span>


* <span data-ttu-id="566d1-109">Gözden geçirme [planlama hello geçiş için tooManaged diskleri](on-prem-to-azure.md#plan-for-the-migration-to-managed-disks).</span><span class="sxs-lookup"><span data-stu-id="566d1-109">Review [Plan for hello migration tooManaged Disks](on-prem-to-azure.md#plan-for-the-migration-to-managed-disks).</span></span>

[!INCLUDE [virtual-machines-common-convert-disks-considerations](../../../includes/virtual-machines-common-convert-disks-considerations.md)]




## <a name="convert-single-instance-vms"></a><span data-ttu-id="566d1-110">Tek Örnekli VM'ler Dönüştür</span><span class="sxs-lookup"><span data-stu-id="566d1-110">Convert single-instance VMs</span></span>
<span data-ttu-id="566d1-111">Bu bölüm, nasıl tooconvert Tek Örnekli yönetilmeyenden Azure VM'ler toomanaged diskleri kapsar.</span><span class="sxs-lookup"><span data-stu-id="566d1-111">This section covers how tooconvert single-instance Azure VMs from unmanaged disks toomanaged disks.</span></span> <span data-ttu-id="566d1-112">(Bir kullanılabilirlik kümesine Vm'leriniz varsa hello sonraki bölüme bakın.)</span><span class="sxs-lookup"><span data-stu-id="566d1-112">(If your VMs are in an availability set, see hello next section.)</span></span> 

1. <span data-ttu-id="566d1-113">Hello kullanarak Hello VM serbest bırakma [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="566d1-113">Deallocate hello VM by using hello [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) cmdlet.</span></span> <span data-ttu-id="566d1-114">Merhaba aşağıdaki örnek kaldırır hello adlı VM `myVM` adlı hello kaynak grubunda `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="566d1-114">hello following example deallocates hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span> 

  ```powershell
  $rgName = "myResourceGroup"
  $vmName = "myVM"
  Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName -Force
  ```

2. <span data-ttu-id="566d1-115">Hello kullanarak Hello VM toomanaged diskleri dönüştürme [ConvertTo-AzureRmVMManagedDisk](/powershell/module/azurerm.compute/convertto-azurermvmmanageddisk) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="566d1-115">Convert hello VM toomanaged disks by using hello [ConvertTo-AzureRmVMManagedDisk](/powershell/module/azurerm.compute/convertto-azurermvmmanageddisk) cmdlet.</span></span> <span data-ttu-id="566d1-116">işlem dönüştürür aşağıdaki hello hello işletim sistemi diski ve veri diskleri dahil önceki VM hello:</span><span class="sxs-lookup"><span data-stu-id="566d1-116">hello following process converts hello previous VM, including hello OS disk and any data disks:</span></span>

  ```powershell
  ConvertTo-AzureRmVMManagedDisk -ResourceGroupName $rgName -VMName $vmName
  ```

3. <span data-ttu-id="566d1-117">Merhaba VM hello dönüştürme toomanaged diskleri sonra başlamayı [Start-AzureRmVM](/powershell/module/azurerm.compute/start-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="566d1-117">Start hello VM after hello conversion toomanaged disks by using [Start-AzureRmVM](/powershell/module/azurerm.compute/start-azurermvm).</span></span> <span data-ttu-id="566d1-118">Aşağıdaki örnek yeniden hello önceki VM hello:</span><span class="sxs-lookup"><span data-stu-id="566d1-118">hello following example restarts hello previous VM:</span></span>

  ```powershell
  Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName
  ```


## <a name="convert-vms-in-an-availability-set"></a><span data-ttu-id="566d1-119">Sanal makineleri bir kullanılabilirlik kümesine Dönüştür</span><span class="sxs-lookup"><span data-stu-id="566d1-119">Convert VMs in an availability set</span></span>

<span data-ttu-id="566d1-120">Tooconvert toomanaged disklerdir bir kullanılabilirlik kümesinde istediğiniz hello VM'ler, ilk tooconvert hello kullanılabilirlik kümesi tooa yönetilen ihtiyacınız varsa kullanılabilirlik kümesi.</span><span class="sxs-lookup"><span data-stu-id="566d1-120">If hello VMs that you want tooconvert toomanaged disks are in an availability set, you first need tooconvert hello availability set tooa managed availability set.</span></span>

1. <span data-ttu-id="566d1-121">Merhaba kullanılabilirlik Hello kullanarak kümesi Dönüştür [güncelleştirme AzureRmAvailabilitySet](/powershell/module/azurerm.compute/update-azurermavailabilityset) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="566d1-121">Convert hello availability set by using hello [Update-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/update-azurermavailabilityset) cmdlet.</span></span> <span data-ttu-id="566d1-122">Aşağıdaki güncelleştirmeler hello kullanılabilirlik adlandırılmış kümesi örneğine hello `myAvailabilitySet` adlı hello kaynak grubunda `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="566d1-122">hello following example updates hello availability set named `myAvailabilitySet` in hello resource group named `myResourceGroup`:</span></span>

  ```powershell
  $rgName = 'myResourceGroup'
  $avSetName = 'myAvailabilitySet'

  $avSet = Get-AzureRmAvailabilitySet -ResourceGroupName $rgName -Name $avSetName
  Update-AzureRmAvailabilitySet -AvailabilitySet $avSet -Sku Aligned 
  ```

  <span data-ttu-id="566d1-123">Yalnızca 2 yönetilen hata etki alanı kullanılabilirlik kümesi bulunduğu hello bölge vardır ancak hello numarası yönetilmeyen hata etki alanı 3, bu komutu bir hata benzer gösterir çok "Merhaba hata etki alanı sayısı 3 hello aralığı 1 too2 dönmesi gerekir belirtilirse."</span><span class="sxs-lookup"><span data-stu-id="566d1-123">If hello region where your availability set is located has only 2 managed fault domains but hello number of unmanaged fault domains is 3, this command shows an error similar too"hello specified fault domain count 3 must fall in hello range 1 too2."</span></span> <span data-ttu-id="566d1-124">hata, güncelleştirme hello hata etki alanı too2 ve güncelleştirme tooresolve hello `Sku` çok`Aligned` gibi:</span><span class="sxs-lookup"><span data-stu-id="566d1-124">tooresolve hello error, update hello fault domain too2 and update `Sku` too`Aligned` as follows:</span></span>

  ```powershell
  $avSet.PlatformFaultDomainCount = 2
  Update-AzureRmAvailabilitySet -AvailabilitySet $avSet -Sku Aligned
  ```

2. <span data-ttu-id="566d1-125">Deallocate ve hello VM'ler hello kullanılabilirlik kümesindeki dönüştürün.</span><span class="sxs-lookup"><span data-stu-id="566d1-125">Deallocate and convert hello VMs in hello availability set.</span></span> <span data-ttu-id="566d1-126">Merhaba aşağıdaki komut dosyası her VM hello kullanarak kaldırır [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) cmdlet'ini dönüştürür onu kullanarak [ConvertTo-AzureRmVMManagedDisk](/powershell/module/azurerm.compute/convertto-azurermvmmanageddisk)ve kullanarak yeniden [Start-AzureRmVM ](/powershell/module/azurerm.compute/start-azurermvm):</span><span class="sxs-lookup"><span data-stu-id="566d1-126">hello following script deallocates each VM by using hello [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) cmdlet, converts it by using [ConvertTo-AzureRmVMManagedDisk](/powershell/module/azurerm.compute/convertto-azurermvmmanageddisk), and restarts it by using [Start-AzureRmVM](/powershell/module/azurerm.compute/start-azurermvm):</span></span>

  ```powershell
  $avSet = Get-AzureRmAvailabilitySet -ResourceGroupName $rgName -Name $avSetName

  foreach($vmInfo in $avSet.VirtualMachinesReferences)
  {
     $vm = Get-AzureRmVM -ResourceGroupName $rgName | Where-Object {$_.Id -eq $vmInfo.id}
     Stop-AzureRmVM -ResourceGroupName $rgName -Name $vm.Name -Force
     ConvertTo-AzureRmVMManagedDisk -ResourceGroupName $rgName -VMName $vm.Name
     Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName
  }
  ```


## <a name="troubleshooting"></a><span data-ttu-id="566d1-127">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="566d1-127">Troubleshooting</span></span>

<span data-ttu-id="566d1-128">Dönüştürme sırasında bir hata varsa veya bir VM önceki dönüştürme sorunları nedeniyle başarısız bir durumda ise, hello çalıştırın `ConvertTo-AzureRmVMManagedDisk` cmdlet'ini yeniden.</span><span class="sxs-lookup"><span data-stu-id="566d1-128">If there is an error during conversion, or if a VM is in a failed state because of issues in a previous conversion, run hello `ConvertTo-AzureRmVMManagedDisk` cmdlet again.</span></span> <span data-ttu-id="566d1-129">Basit bir yeniden deneme genellikle hello durum kaldırır.</span><span class="sxs-lookup"><span data-stu-id="566d1-129">A simple retry usually unblocks hello situation.</span></span>


## <a name="next-steps"></a><span data-ttu-id="566d1-130">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="566d1-130">Next steps</span></span>

[<span data-ttu-id="566d1-131">Standart yönetilen disk toopremium Dönüştür</span><span class="sxs-lookup"><span data-stu-id="566d1-131">Convert standard managed disks toopremium</span></span>](convert-disk-storage.md)

<span data-ttu-id="566d1-132">Kullanarak bir VM salt okunur bir kopyasını alın [anlık görüntüleri](snapshot-copy-managed-disk.md).</span><span class="sxs-lookup"><span data-stu-id="566d1-132">Take a read-only copy of a VM by using [snapshots](snapshot-copy-managed-disk.md).</span></span>

