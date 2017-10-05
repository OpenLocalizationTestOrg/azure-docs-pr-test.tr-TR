---
title: "Azure'da bir VHD'den yönetilen bir disk oluşturma | Microsoft Docs"
description: "Yönetilen bir disk Resource Manager dağıtım modelini kullanarak bir Azure depolama hesabında şu anda olan bir VHD'den oluşturun."
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
ms.openlocfilehash: c03ebf73f1090b595149daf2eb3e274b05822f4f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-managed-disks-from-unmanaged-disks-in-a-storage-account"></a><span data-ttu-id="58266-103">Bir depolama hesabı yönetilmeyen disklerden yönetilen diskleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="58266-103">Create managed disks from unmanaged disks in a storage account</span></span>

<span data-ttu-id="58266-104">Yönetilen bir disk, varolan bir veri diski veya bir Azure depolama hesabında şu anda olan işletim sistemi diski oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="58266-104">A managed disk can be created from an existing data disk or an OS disk that is currently in an Azure storage account.</span></span> <span data-ttu-id="58266-105">Ayrıca, bir VM için yeni bir veri diski olarak kullanılabilmesi için boş bir disk oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="58266-105">You can also create an empty disk that can be used as a new data disk for a VM.</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="58266-106">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="58266-106">Before you begin</span></span>
<span data-ttu-id="58266-107">PowerShell'i kullanırsanız, AzureRM.Compute PowerShell modülü en son sürümüne sahip olduğunuzdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="58266-107">If you use PowerShell, make sure that you have the latest version of the AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="58266-108">Yüklemek için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="58266-108">Run the following command to install it.</span></span>

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
<span data-ttu-id="58266-109">Daha fazla bilgi için bkz: [Azure PowerShell sürüm](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="58266-109">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


## <a name="create-a-managed-disk-from-a-vhd-in-an-azure-storage-account"></a><span data-ttu-id="58266-110">Bir Azure depolama hesabındaki bir VHD'den yönetilen bir disk oluşturma</span><span class="sxs-lookup"><span data-stu-id="58266-110">Create a managed disk from a VHD in an Azure storage account</span></span>

<span data-ttu-id="58266-111">Yönetilen disk olarak bir VHD'den disk oluştur ve parametreye atayın örnekte **$ disk 1** daha sonra kullanmak üzere.</span><span class="sxs-lookup"><span data-stu-id="58266-111">In the example we create a disk from a VHD as managed disk and assign it to the parameter **$disk1** to use later.</span></span> 

<span data-ttu-id="58266-112">Yönetilen disk içinde oluşturulacak **Batı ABD** konumda adlı bir kaynak grubu **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="58266-112">The managed disk will be created in the **West-US** location, in a resource group named **myResourceGroup**.</span></span> <span data-ttu-id="58266-113">Disk adında **myDisk** ve adlı bir VHD dosyasından oluşturulacak **myDisk.vhd** biz adlı bir depolama hesabı için daha önce karşıya **mystorageaccount**.</span><span class="sxs-lookup"><span data-stu-id="58266-113">The disk will be named **myDisk** and it will be created from a VHD file named **myDisk.vhd** we previously uploaded to a storage account named **mystorageaccount**.</span></span> <span data-ttu-id="58266-114">Yönetilen disk premium yerel olarak yedekli depolama (LRS) oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="58266-114">The managed disk will be created in premium locally-redundant storage (LRS).</span></span> <span data-ttu-id="58266-115">StandardLRS ve PremiumLRS olan tek **- AccountType** için kullanılabilir seçenekleri yönetilen diskler.</span><span class="sxs-lookup"><span data-stu-id="58266-115">StandardLRS and PremiumLRS are the only **-AccountType** options available for managed disks.</span></span> 

1.  <span data-ttu-id="58266-116">Bazı parametreler Ayarla</span><span class="sxs-lookup"><span data-stu-id="58266-116">Set some parameters</span></span>

    ```powershell
    $rgName = "myResourceGroup"
    $location = "West Central US"
    $diskName = "myDisk"
    $vhdUri = "https://mystorageaccount.blob.core.windows.net/vhds/myDisk.vhd"
    ```

2. <span data-ttu-id="58266-117">Veri diski oluşturun.</span><span class="sxs-lookup"><span data-stu-id="58266-117">Create the data disk.</span></span> 
    ```powershell
    $disk1 = New-AzureRmDisk -DiskName $diskName -Disk (New-AzureRmDiskConfig -AccountType PremiumLRS -Location $location -CreateOption Import -SourceUri $vhdUri) -ResourceGroupName $rgName
    ```
    
    

## <a name="create-an-empty-data-disk-as-a-managed-disk"></a><span data-ttu-id="58266-118">Boş veri diski yönetilen bir disk oluşturma</span><span class="sxs-lookup"><span data-stu-id="58266-118">Create an empty data disk as a managed disk</span></span>

<span data-ttu-id="58266-119">Boş veri diski yönetilen disk olarak oluşturun ve parametreye atayın örnekte **$dataDisk2** daha sonra kullanmak üzere.</span><span class="sxs-lookup"><span data-stu-id="58266-119">In the example we create an empty data disk as managed disk and assign it to the parameter **$dataDisk2** to use later.</span></span> <span data-ttu-id="58266-120">Boş veri diski başlatılmış VM'ye oturum açmayı ve diskmgmt.msc kullanarak olması gerekir veya [WinRM ve bir komut dosyası kullanarak uzaktan](attach-disk-ps.md#initialize-the-disk), çalışan bir VM bağlandıktan sonra.</span><span class="sxs-lookup"><span data-stu-id="58266-120">An empty data disk will need to be initialized logging in to the VM and using diskmgmt.msc or [remotely using WinRM and a script](attach-disk-ps.md#initialize-the-disk), once it is attached to a running VM.</span></span>

<span data-ttu-id="58266-121">Boş veri diski içinde oluşturulacak **Batı Orta ABD** konumda adlı bir kaynak grubu **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="58266-121">The empty data disk will be created in the **West Central US** location, in a resource group named **myResourceGroup**.</span></span> <span data-ttu-id="58266-122">Disk adında **myEmptyDataDisk**.</span><span class="sxs-lookup"><span data-stu-id="58266-122">The disk will be named **myEmptyDataDisk**.</span></span> <span data-ttu-id="58266-123">Premium yerel olarak yedekli depolama (LRS) boş disk oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="58266-123">The empty disk will be created in premium locally-redundant storage (LRS).</span></span> <span data-ttu-id="58266-124">StandardLRS ve PremiumLRS olan tek **- AccountType** için kullanılabilir seçenekleri yönetilen diskler.</span><span class="sxs-lookup"><span data-stu-id="58266-124">StandardLRS and PremiumLRS are the only **-AccountType** options available for managed disks.</span></span>

<span data-ttu-id="58266-125">Bu örnekte disk boyutu, 128 GB olmakla birlikte, VM üzerinde çalışan uygulamaların gereksinimlerini karşılayan bir boyut seçmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="58266-125">The disk size in this example is 128GB, but you should choose a size that meets the needs of any applications running on your VM.</span></span>

1.  <span data-ttu-id="58266-126">Bazı parametreler Ayarla</span><span class="sxs-lookup"><span data-stu-id="58266-126">Set some parameters</span></span>

    ```powershell
    $rgName = "myResourceGroup"
    $location = "West Central US"
    $dataDiskName = "myEmptyDataDisk"
    ```

2. <span data-ttu-id="58266-127">Veri diski oluşturun.</span><span class="sxs-lookup"><span data-stu-id="58266-127">Create the data disk.</span></span>
    ```powershell
    $dataDisk2 = New-AzureRmDisk -DiskName $dataDiskName -Disk (New-AzureRmDiskConfig -AccountType PremiumLRS -Location $location -CreateOption Empty -DiskSizeGB 128) -ResourceGroupName $rgName
    ```
    
## <a name="next-steps"></a><span data-ttu-id="58266-128">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="58266-128">Next Steps</span></span>   
- <span data-ttu-id="58266-129">Bir VM zaten varsa, [bir veri diskini](attach-disk-portal.md).</span><span class="sxs-lookup"><span data-stu-id="58266-129">If you already have a VM, you can [attach a data disk](attach-disk-portal.md).</span></span>
