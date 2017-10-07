---
title: "aaaCreate Azure VHD'yi yönetilen bir diskten | Microsoft Docs"
description: "Yönetilen bir disk hello Resource Manager dağıtım modelini kullanarak bir Azure depolama hesabında şu anda olan bir VHD'den oluşturun."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 02/05/2017
ms.author: cynthn
ms.openlocfilehash: 77adaac5419186ff85039fe2c4752f021aa5e448
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-managed-disks-from-unmanaged-disks-in-a-storage-account"></a><span data-ttu-id="fd600-103">Bir depolama hesabı yönetilmeyen disklerden yönetilen diskleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="fd600-103">Create managed disks from unmanaged disks in a storage account</span></span>

<span data-ttu-id="fd600-104">Yönetilen bir disk, varolan bir veri diski veya bir Azure depolama hesabında şu anda olan işletim sistemi diski oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="fd600-104">A managed disk can be created from an existing data disk or an OS disk that is currently in an Azure storage account.</span></span> <span data-ttu-id="fd600-105">Ayrıca, bir VM için yeni bir veri diski olarak kullanılabilmesi için boş bir disk oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fd600-105">You can also create an empty disk that can be used as a new data disk for a VM.</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="fd600-106">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="fd600-106">Before you begin</span></span>
<span data-ttu-id="fd600-107">PowerShell'i kullanırsanız, hello hello AzureRM.Compute PowerShell modülü en son sürümüne sahip olduğunuzdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="fd600-107">If you use PowerShell, make sure that you have hello latest version of hello AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="fd600-108">Çalıştırma hello komut tooinstall onu.</span><span class="sxs-lookup"><span data-stu-id="fd600-108">Run hello following command tooinstall it.</span></span>

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
<span data-ttu-id="fd600-109">Daha fazla bilgi için bkz: [Azure PowerShell sürüm](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="fd600-109">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


## <a name="create-a-managed-disk-from-a-vhd-in-an-azure-storage-account"></a><span data-ttu-id="fd600-110">Bir Azure depolama hesabındaki bir VHD'den yönetilen bir disk oluşturma</span><span class="sxs-lookup"><span data-stu-id="fd600-110">Create a managed disk from a VHD in an Azure storage account</span></span>

<span data-ttu-id="fd600-111">Yönetilen disk olarak bir VHD'den disk oluştur ve toohello parametresi atamak hello örnekte **$ disk 1** toouse daha sonra.</span><span class="sxs-lookup"><span data-stu-id="fd600-111">In hello example we create a disk from a VHD as managed disk and assign it toohello parameter **$disk1** toouse later.</span></span> 

<span data-ttu-id="fd600-112">Merhaba yönetilen disk hello oluşturulacak **Batı ABD** konumda adlı bir kaynak grubu **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="fd600-112">hello managed disk will be created in hello **West-US** location, in a resource group named **myResourceGroup**.</span></span> <span data-ttu-id="fd600-113">Merhaba disk adlı **myDisk** ve adlı bir VHD dosyasından oluşturulacak **myDisk.vhd** biz adlı tooa depolama hesabı daha önce karşıya **mystorageaccount**.</span><span class="sxs-lookup"><span data-stu-id="fd600-113">hello disk will be named **myDisk** and it will be created from a VHD file named **myDisk.vhd** we previously uploaded tooa storage account named **mystorageaccount**.</span></span> <span data-ttu-id="fd600-114">Merhaba yönetilen disk premium yerel olarak yedekli depolama (LRS) oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="fd600-114">hello managed disk will be created in premium locally-redundant storage (LRS).</span></span> <span data-ttu-id="fd600-115">StandardLRS ve PremiumLRS olan hello yalnızca **- AccountType** için kullanılabilir seçenekleri yönetilen diskler.</span><span class="sxs-lookup"><span data-stu-id="fd600-115">StandardLRS and PremiumLRS are hello only **-AccountType** options available for managed disks.</span></span> 

1.  <span data-ttu-id="fd600-116">Bazı parametreler Ayarla</span><span class="sxs-lookup"><span data-stu-id="fd600-116">Set some parameters</span></span>

    ```powershell
    $rgName = "myResourceGroup"
    $location = "West Central US"
    $diskName = "myDisk"
    $vhdUri = "https://mystorageaccount.blob.core.windows.net/vhds/myDisk.vhd"
    ```

2. <span data-ttu-id="fd600-117">Merhaba veri diski oluşturun.</span><span class="sxs-lookup"><span data-stu-id="fd600-117">Create hello data disk.</span></span> 
    ```powershell
    $disk1 = New-AzureRmDisk -DiskName $diskName -Disk (New-AzureRmDiskConfig -AccountType PremiumLRS -Location $location -CreateOption Import -SourceUri $vhdUri) -ResourceGroupName $rgName
    ```
    
    

## <a name="create-an-empty-data-disk-as-a-managed-disk"></a><span data-ttu-id="fd600-118">Boş veri diski yönetilen bir disk oluşturma</span><span class="sxs-lookup"><span data-stu-id="fd600-118">Create an empty data disk as a managed disk</span></span>

<span data-ttu-id="fd600-119">Boş veri diski yönetilen disk olarak oluşturun ve toohello parametresi atamak hello örnekte **$dataDisk2** toouse daha sonra.</span><span class="sxs-lookup"><span data-stu-id="fd600-119">In hello example we create an empty data disk as managed disk and assign it toohello parameter **$dataDisk2** toouse later.</span></span> <span data-ttu-id="fd600-120">Boş veri diskini toohello VM günlüğe kaydetme ve diskmgmt.msc kullanarak başlatılmış toobe gerekir veya [WinRM ve bir komut dosyası kullanarak uzaktan](attach-disk-ps.md#initialize-the-disk), VM çalıştıran ekli tooa olduğunda.</span><span class="sxs-lookup"><span data-stu-id="fd600-120">An empty data disk will need toobe initialized logging in toohello VM and using diskmgmt.msc or [remotely using WinRM and a script](attach-disk-ps.md#initialize-the-disk), once it is attached tooa running VM.</span></span>

<span data-ttu-id="fd600-121">Merhaba boş veri diski hello oluşturulacak **Batı Orta ABD** konumda adlı bir kaynak grubu **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="fd600-121">hello empty data disk will be created in hello **West Central US** location, in a resource group named **myResourceGroup**.</span></span> <span data-ttu-id="fd600-122">Merhaba disk adlı **myEmptyDataDisk**.</span><span class="sxs-lookup"><span data-stu-id="fd600-122">hello disk will be named **myEmptyDataDisk**.</span></span> <span data-ttu-id="fd600-123">Merhaba boş disk premium yerel olarak yedekli depolama (LRS) oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="fd600-123">hello empty disk will be created in premium locally-redundant storage (LRS).</span></span> <span data-ttu-id="fd600-124">StandardLRS ve PremiumLRS olan hello yalnızca **- AccountType** için kullanılabilir seçenekleri yönetilen diskler.</span><span class="sxs-lookup"><span data-stu-id="fd600-124">StandardLRS and PremiumLRS are hello only **-AccountType** options available for managed disks.</span></span>

<span data-ttu-id="fd600-125">Bu örnekte Hello disk boyutu, 128 GB olmakla birlikte, VM'de çalışan herhangi bir uygulama, hello gereksinimlerini karşılayan bir boyut seçmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="fd600-125">hello disk size in this example is 128GB, but you should choose a size that meets hello needs of any applications running on your VM.</span></span>

1.  <span data-ttu-id="fd600-126">Bazı parametreler Ayarla</span><span class="sxs-lookup"><span data-stu-id="fd600-126">Set some parameters</span></span>

    ```powershell
    $rgName = "myResourceGroup"
    $location = "West Central US"
    $dataDiskName = "myEmptyDataDisk"
    ```

2. <span data-ttu-id="fd600-127">Merhaba veri diski oluşturun.</span><span class="sxs-lookup"><span data-stu-id="fd600-127">Create hello data disk.</span></span>
    ```powershell
    $dataDisk2 = New-AzureRmDisk -DiskName $dataDiskName -Disk (New-AzureRmDiskConfig -AccountType PremiumLRS -Location $location -CreateOption Empty -DiskSizeGB 128) -ResourceGroupName $rgName
    ```
    
## <a name="next-steps"></a><span data-ttu-id="fd600-128">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="fd600-128">Next Steps</span></span>   
- <span data-ttu-id="fd600-129">Bir VM zaten varsa, [bir veri diskini](attach-disk-portal.md).</span><span class="sxs-lookup"><span data-stu-id="fd600-129">If you already have a VM, you can [attach a data disk](attach-disk-portal.md).</span></span>
