---
title: "Yönetilen bir Azure diski geri için bir kopyasını oluştur | Microsoft Docs"
description: "Yedekleme için kullanılacak bir Azure yönetilen Disk veya disk sorunlarını giderme bir kopyasını oluşturmayı öğrenin."
documentationcenter: 
author: cwatson-cat
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 15eb778e-fc07-45ef-bdc8-9090193a6d20
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 2/9/2017
ms.author: cwatson
ms.openlocfilehash: a7527b12f4f0d2b45713a0c0109d81ff51293fd8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-copy-of-a-vhd-stored-as-an-azure-managed-disk-by-using-managed-snapshots"></a><span data-ttu-id="ce7ae-103">Yönetilen bir Azure diski yönetilen anlık görüntülerini kullanarak tarafından depolanan VHD bir kopyasını oluşturun</span><span class="sxs-lookup"><span data-stu-id="ce7ae-103">Create a copy of a VHD stored as an Azure Managed Disk by using Managed Snapshots</span></span>
<span data-ttu-id="ce7ae-104">Yönetilen bir Disk Yedekleme için bir anlık görüntüsünü veya yönetilen bir Disk anlık görüntüden oluşturabilir ve sorun giderme için test sanal makineye Ekle.</span><span class="sxs-lookup"><span data-stu-id="ce7ae-104">Take a snapshot of a Managed Disk for backup or create a Managed Disk from the snapshot and attach it to a test virtual machine to troubleshoot.</span></span> <span data-ttu-id="ce7ae-105">Yönetilen bir anlık görüntü yönetilen bir VM Disk noktası zaman tam kopyasıdır.</span><span class="sxs-lookup"><span data-stu-id="ce7ae-105">A Managed Snapshot is a full point-in-time copy of a VM Managed Disk.</span></span> <span data-ttu-id="ce7ae-106">Bu, VHD salt okunur bir kopyasını oluşturur ve isteğe bağlı olarak varsayılan olarak, standart yönetilen Disk olarak depolar.</span><span class="sxs-lookup"><span data-stu-id="ce7ae-106">It creates a read-only copy of your VHD and, by default, stores it as a Standard Managed Disk.</span></span> <span data-ttu-id="ce7ae-107">Yönetilen diskler hakkında daha fazla bilgi için bkz: [Azure yönetilen diskleri genel bakış](managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="ce7ae-107">For more information about Managed Disks, see [Azure Managed Disks overview](managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>

<span data-ttu-id="ce7ae-108">Fiyatlandırma hakkında daha fazla bilgi için bkz: [Azure Storage fiyatlandırması](https://azure.microsoft.com/pricing/details/managed-disks/).</span><span class="sxs-lookup"><span data-stu-id="ce7ae-108">For information about pricing, see [Azure Storage Pricing](https://azure.microsoft.com/pricing/details/managed-disks/).</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="ce7ae-109">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="ce7ae-109">Before you begin</span></span>
<span data-ttu-id="ce7ae-110">PowerShell'i kullanırsanız, AzureRM.Compute PowerShell modülü en son sürümüne sahip olduğunuzdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="ce7ae-110">If you use PowerShell, make sure that you have the latest version of the AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="ce7ae-111">Yüklemek için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="ce7ae-111">Run the following command to install it.</span></span>

```
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
<span data-ttu-id="ce7ae-112">Daha fazla bilgi için bkz: [Azure PowerShell sürüm](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ce7ae-112">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>

## <a name="copy-the-vhd-with-a-snapshot"></a><span data-ttu-id="ce7ae-113">VHD bir anlık görüntü ile kopyalama</span><span class="sxs-lookup"><span data-stu-id="ce7ae-113">Copy the VHD with a snapshot</span></span>
<span data-ttu-id="ce7ae-114">Yönetilen diskin anlık görüntüsünü almak için Azure portal veya PowerShell kullanın.</span><span class="sxs-lookup"><span data-stu-id="ce7ae-114">Use either the Azure portal or PowerShell to take a snapshot of the Managed Disk.</span></span>

### <a name="use-azure-portal-to-take-a-snapshot"></a><span data-ttu-id="ce7ae-115">Bir anlık görüntüsünü için Azure portalını kullanma</span><span class="sxs-lookup"><span data-stu-id="ce7ae-115">Use Azure portal to take a snapshot</span></span> 

1. <span data-ttu-id="ce7ae-116">[Azure Portal](https://portal.azure.com) oturum açın.</span><span class="sxs-lookup"><span data-stu-id="ce7ae-116">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="ce7ae-117">Sol üst başlayarak, tıklatın **yeni** arayın ve **anlık görüntü**.</span><span class="sxs-lookup"><span data-stu-id="ce7ae-117">Starting in the upper left, click **New** and search for **snapshot**.</span></span>
3. <span data-ttu-id="ce7ae-118">Anlık görüntü dikey penceresinde tıklayın **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="ce7ae-118">In the Snapshot blade, click **Create**.</span></span>
4. <span data-ttu-id="ce7ae-119">Girin bir **adı** anlık görüntü için.</span><span class="sxs-lookup"><span data-stu-id="ce7ae-119">Enter a **Name** for the snapshot.</span></span>
5. <span data-ttu-id="ce7ae-120">Varolan [Kaynak grubunu](../../azure-resource-manager/resource-group-overview.md#resource-groups) seçin veya yenisi için adı yazın.</span><span class="sxs-lookup"><span data-stu-id="ce7ae-120">Select an existing [Resource group](../../azure-resource-manager/resource-group-overview.md#resource-groups) or type the name for a new one.</span></span> 
6. <span data-ttu-id="ce7ae-121">Azure veri merkezi konum seçin.</span><span class="sxs-lookup"><span data-stu-id="ce7ae-121">Select an Azure datacenter Location.</span></span>  
7. <span data-ttu-id="ce7ae-122">İçin **kaynak disk**, anlık görüntü için yönetilen diski seçin.</span><span class="sxs-lookup"><span data-stu-id="ce7ae-122">For **Source disk**, select the Managed Disk to snapshot.</span></span>
8. <span data-ttu-id="ce7ae-123">Seçin **hesap türü** anlık görüntü deposu için kullanılacak.</span><span class="sxs-lookup"><span data-stu-id="ce7ae-123">Select the **Account type** to use to store the snapshot.</span></span> <span data-ttu-id="ce7ae-124">Öneririz **Standard_LRS** yüksek performanslı bir diskte depolanan gerekmedikçe.</span><span class="sxs-lookup"><span data-stu-id="ce7ae-124">We recommend **Standard_LRS** unless you need it stored on a high performing disk.</span></span>
9. <span data-ttu-id="ce7ae-125">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ce7ae-125">Click **Create**.</span></span>

### <a name="use-powershell-to-take-a-snapshot"></a><span data-ttu-id="ce7ae-126">Bir anlık görüntüsünü için PowerShell kullanma</span><span class="sxs-lookup"><span data-stu-id="ce7ae-126">Use PowerShell to take a snapshot</span></span>
<span data-ttu-id="ce7ae-127">Aşağıdaki adımlar VHD diskin kopyalanması, anlık görüntü yapılandırmaları oluşturmak ve yeni AzureRmSnapshot cmdlet'ini kullanarak bir disk anlık görüntüsünü alma gösterir<!--Add link to cmdlet when available-->.</span><span class="sxs-lookup"><span data-stu-id="ce7ae-127">The following steps show you how to get the VHD disk to be copied, create the snapshot configurations, and take a snapshot of the disk by using the New-AzureRmSnapshot cmdlet<!--Add link to cmdlet when available-->.</span></span> 

1. <span data-ttu-id="ce7ae-128">Bazı parametreler ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="ce7ae-128">Set some parameters.</span></span> 

 ```powershell
$resourceGroupName = 'myResourceGroup' 
$location = 'southeastasia' 
$dataDiskName = 'ContosoMD_datadisk1' 
$snapshotName = 'ContosoMD_datadisk1_snapshot1'  
```
  <span data-ttu-id="ce7ae-129">Parametre değerleri değiştirin:</span><span class="sxs-lookup"><span data-stu-id="ce7ae-129">Replace the parameter values:</span></span>
  -  <span data-ttu-id="ce7ae-130">VM kaynak grubuyla "contoso.com".</span><span class="sxs-lookup"><span data-stu-id="ce7ae-130">"myResourceGroup" with the VM's resource group.</span></span>
  -  <span data-ttu-id="ce7ae-131">"southeastasia" yönetilen depolanan anlık coğrafi konumu ile.</span><span class="sxs-lookup"><span data-stu-id="ce7ae-131">"southeastasia" with the geographic location where you want your Managed Snapshot stored.</span></span> <!---How do you look these up? -->
  -  <span data-ttu-id="ce7ae-132">Kopyalamak istediğiniz VHD disk adı "ContosoMD_datadisk1".</span><span class="sxs-lookup"><span data-stu-id="ce7ae-132">"ContosoMD_datadisk1" with the name of the VHD disk that you want to copy.</span></span>
  -  <span data-ttu-id="ce7ae-133">Yeni anlık görüntü için kullanmak istediğiniz adla "ContosoMD_datadisk1_snapshot1".</span><span class="sxs-lookup"><span data-stu-id="ce7ae-133">"ContosoMD_datadisk1_snapshot1" with the name you want to use for the new snapshot.</span></span>

2. <span data-ttu-id="ce7ae-134">Kopyalanacak VHD disk alın.</span><span class="sxs-lookup"><span data-stu-id="ce7ae-134">Get the VHD disk to be copied.</span></span>

 ```powershell
$disk = Get-AzureRmDisk -ResourceGroupName $resourceGroupName -DiskName $dataDiskName 
```
3. <span data-ttu-id="ce7ae-135">Anlık görüntü yapılandırmaları oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ce7ae-135">Create the snapshot configurations.</span></span> 

 ```powershell
$snapshot =  New-AzureRmSnapshotConfig -SourceUri $disk.Id -CreateOption Copy -Location $location 
```
4. <span data-ttu-id="ce7ae-136">Anlık görüntü alın.</span><span class="sxs-lookup"><span data-stu-id="ce7ae-136">Take the snapshot.</span></span>

 ```powershell
New-AzureRmSnapshot -Snapshot $snapshot -SnapshotName $snapshotName -ResourceGroupName $resourceGroupName 
```
<span data-ttu-id="ce7ae-137">Yönetilen bir Disk oluşturmak ve yüksek performanslı olması gereken bir VM eklemek için anlık görüntü kullanmayı planlıyorsanız, parametresini kullanın `-AccountType Premium_LRS` yeni AzureRmSnapshot komutu.</span><span class="sxs-lookup"><span data-stu-id="ce7ae-137">If you plan to use the snapshot to create a Managed Disk and attach it a VM that needs to be high performing, use the parameter `-AccountType Premium_LRS` with the New-AzureRmSnapshot command.</span></span> <span data-ttu-id="ce7ae-138">Parametre anlık görüntü oluşturur, böylece yönetilen bir Premium Disk depolanır.</span><span class="sxs-lookup"><span data-stu-id="ce7ae-138">The parameter creates the snapshot so that it's stored as a Premium Managed Disk.</span></span> <span data-ttu-id="ce7ae-139">Premium yönetilen diskleri standart daha pahalıdır.</span><span class="sxs-lookup"><span data-stu-id="ce7ae-139">Premium Managed Disks are more expensive than Standard.</span></span> <span data-ttu-id="ce7ae-140">Bu nedenle bu parametrenin kullanmadan önce Premium gerçekten ihtiyacınız emin olun.</span><span class="sxs-lookup"><span data-stu-id="ce7ae-140">So be sure you really need Premium before using that parameter.</span></span>


