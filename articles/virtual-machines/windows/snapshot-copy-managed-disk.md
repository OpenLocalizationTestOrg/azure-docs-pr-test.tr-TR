---
title: "bir yedekleme için bir Azure yönetilen diski kopyasını aaaCreate | Microsoft Docs"
description: "Azure yönetilen diski toouse geri yukarı veya sorun giderme disk için bir kopyasını toocreate nasıl sorunları hakkında bilgi edinin."
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
ms.openlocfilehash: 2f33dbbee624bcd813f3c7c3e3401072d0933714
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-copy-of-a-vhd-stored-as-an-azure-managed-disk-by-using-managed-snapshots"></a><span data-ttu-id="fee1e-103">Yönetilen bir Azure diski yönetilen anlık görüntülerini kullanarak tarafından depolanan VHD bir kopyasını oluşturun</span><span class="sxs-lookup"><span data-stu-id="fee1e-103">Create a copy of a VHD stored as an Azure Managed Disk by using Managed Snapshots</span></span>
<span data-ttu-id="fee1e-104">Yönetilen bir Disk Yedekleme için bir anlık görüntüsünü veya yönetilen bir Disk hello anlık görüntüden oluşturmak ve tooa test sanal makinesi tootroubleshoot ekleyin.</span><span class="sxs-lookup"><span data-stu-id="fee1e-104">Take a snapshot of a Managed Disk for backup or create a Managed Disk from hello snapshot and attach it tooa test virtual machine tootroubleshoot.</span></span> <span data-ttu-id="fee1e-105">Yönetilen bir anlık görüntü yönetilen bir VM Disk noktası zaman tam kopyasıdır.</span><span class="sxs-lookup"><span data-stu-id="fee1e-105">A Managed Snapshot is a full point-in-time copy of a VM Managed Disk.</span></span> <span data-ttu-id="fee1e-106">Bu, VHD salt okunur bir kopyasını oluşturur ve isteğe bağlı olarak varsayılan olarak, standart yönetilen Disk olarak depolar.</span><span class="sxs-lookup"><span data-stu-id="fee1e-106">It creates a read-only copy of your VHD and, by default, stores it as a Standard Managed Disk.</span></span> <span data-ttu-id="fee1e-107">Yönetilen diskler hakkında daha fazla bilgi için bkz: [Azure yönetilen diskleri genel bakış](managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="fee1e-107">For more information about Managed Disks, see [Azure Managed Disks overview](managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>

<span data-ttu-id="fee1e-108">Fiyatlandırma hakkında daha fazla bilgi için bkz: [Azure Storage fiyatlandırması](https://azure.microsoft.com/pricing/details/managed-disks/).</span><span class="sxs-lookup"><span data-stu-id="fee1e-108">For information about pricing, see [Azure Storage Pricing](https://azure.microsoft.com/pricing/details/managed-disks/).</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="fee1e-109">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="fee1e-109">Before you begin</span></span>
<span data-ttu-id="fee1e-110">PowerShell'i kullanırsanız, hello hello AzureRM.Compute PowerShell modülü en son sürümüne sahip olduğunuzdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="fee1e-110">If you use PowerShell, make sure that you have hello latest version of hello AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="fee1e-111">Çalıştırma hello komut tooinstall onu.</span><span class="sxs-lookup"><span data-stu-id="fee1e-111">Run hello following command tooinstall it.</span></span>

```
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
<span data-ttu-id="fee1e-112">Daha fazla bilgi için bkz: [Azure PowerShell sürüm](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="fee1e-112">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>

## <a name="copy-hello-vhd-with-a-snapshot"></a><span data-ttu-id="fee1e-113">Merhaba VHD anlık görüntüleri kopyalama</span><span class="sxs-lookup"><span data-stu-id="fee1e-113">Copy hello VHD with a snapshot</span></span>
<span data-ttu-id="fee1e-114">Hello Azure portal veya PowerShell tootake hello yönetilen Disk görüntüsünü kullanın.</span><span class="sxs-lookup"><span data-stu-id="fee1e-114">Use either hello Azure portal or PowerShell tootake a snapshot of hello Managed Disk.</span></span>

### <a name="use-azure-portal-tootake-a-snapshot"></a><span data-ttu-id="fee1e-115">Azure portal tootake bir anlık görüntü kullanın</span><span class="sxs-lookup"><span data-stu-id="fee1e-115">Use Azure portal tootake a snapshot</span></span> 

1. <span data-ttu-id="fee1e-116">İçinde toohello oturum [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="fee1e-116">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="fee1e-117">Merhaba üst sol başlayarak, tıklatın **yeni** arayın ve **anlık görüntü**.</span><span class="sxs-lookup"><span data-stu-id="fee1e-117">Starting in hello upper left, click **New** and search for **snapshot**.</span></span>
3. <span data-ttu-id="fee1e-118">Başlangıç anlık görüntü dikey penceresinde tıklayın **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="fee1e-118">In hello Snapshot blade, click **Create**.</span></span>
4. <span data-ttu-id="fee1e-119">Girin bir **adı** hello anlık görüntü için.</span><span class="sxs-lookup"><span data-stu-id="fee1e-119">Enter a **Name** for hello snapshot.</span></span>
5. <span data-ttu-id="fee1e-120">Var olan seçin [kaynak grubu](../../azure-resource-manager/resource-group-overview.md#resource-groups) veya yeni bir hello adını yazın.</span><span class="sxs-lookup"><span data-stu-id="fee1e-120">Select an existing [Resource group](../../azure-resource-manager/resource-group-overview.md#resource-groups) or type hello name for a new one.</span></span> 
6. <span data-ttu-id="fee1e-121">Azure veri merkezi konum seçin.</span><span class="sxs-lookup"><span data-stu-id="fee1e-121">Select an Azure datacenter Location.</span></span>  
7. <span data-ttu-id="fee1e-122">İçin **kaynak disk**, hello yönetilen Disk toosnapshot seçin.</span><span class="sxs-lookup"><span data-stu-id="fee1e-122">For **Source disk**, select hello Managed Disk toosnapshot.</span></span>
8. <span data-ttu-id="fee1e-123">Select hello **hesap türü** toouse toostore hello anlık görüntü.</span><span class="sxs-lookup"><span data-stu-id="fee1e-123">Select hello **Account type** toouse toostore hello snapshot.</span></span> <span data-ttu-id="fee1e-124">Öneririz **Standard_LRS** yüksek performanslı bir diskte depolanan gerekmedikçe.</span><span class="sxs-lookup"><span data-stu-id="fee1e-124">We recommend **Standard_LRS** unless you need it stored on a high performing disk.</span></span>
9. <span data-ttu-id="fee1e-125">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fee1e-125">Click **Create**.</span></span>

### <a name="use-powershell-tootake-a-snapshot"></a><span data-ttu-id="fee1e-126">PowerShell tootake bir anlık görüntü kullanın</span><span class="sxs-lookup"><span data-stu-id="fee1e-126">Use PowerShell tootake a snapshot</span></span>
<span data-ttu-id="fee1e-127">Hello aşağıdaki adımları nasıl tooget hello VHD disk kopyalanan toobe Göster, anlık görüntü yapılandırmaları hello oluşturmak ve hello yeni AzureRmSnapshot cmdlet'ini kullanarak hello disk bir anlık görüntüsünü<!--Add link toocmdlet when available-->.</span><span class="sxs-lookup"><span data-stu-id="fee1e-127">hello following steps show you how tooget hello VHD disk toobe copied, create hello snapshot configurations, and take a snapshot of hello disk by using hello New-AzureRmSnapshot cmdlet<!--Add link toocmdlet when available-->.</span></span> 

1. <span data-ttu-id="fee1e-128">Bazı parametreler ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="fee1e-128">Set some parameters.</span></span> 

 ```powershell
$resourceGroupName = 'myResourceGroup' 
$location = 'southeastasia' 
$dataDiskName = 'ContosoMD_datadisk1' 
$snapshotName = 'ContosoMD_datadisk1_snapshot1'  
```
  <span data-ttu-id="fee1e-129">Merhaba parametre değerlerini değiştirin:</span><span class="sxs-lookup"><span data-stu-id="fee1e-129">Replace hello parameter values:</span></span>
  -  <span data-ttu-id="fee1e-130">"contoso.com" Merhaba VM'in kaynak grubu ile.</span><span class="sxs-lookup"><span data-stu-id="fee1e-130">"myResourceGroup" with hello VM's resource group.</span></span>
  -  <span data-ttu-id="fee1e-131">"southeastasia" yönetilen depolanan anlık hello coğrafi konumu ile.</span><span class="sxs-lookup"><span data-stu-id="fee1e-131">"southeastasia" with hello geographic location where you want your Managed Snapshot stored.</span></span> <!---How do you look these up? -->
  -  <span data-ttu-id="fee1e-132">"ContosoMD_datadisk1" Merhaba adla hello VHD disk toocopy istiyor.</span><span class="sxs-lookup"><span data-stu-id="fee1e-132">"ContosoMD_datadisk1" with hello name of hello VHD disk that you want toocopy.</span></span>
  -  <span data-ttu-id="fee1e-133">"ContosoMD_datadisk1_snapshot1" Merhaba ile ad hello yeni bir anlık görüntü için toouse istiyor.</span><span class="sxs-lookup"><span data-stu-id="fee1e-133">"ContosoMD_datadisk1_snapshot1" with hello name you want toouse for hello new snapshot.</span></span>

2. <span data-ttu-id="fee1e-134">Kopyalanan hello VHD disk toobe alın.</span><span class="sxs-lookup"><span data-stu-id="fee1e-134">Get hello VHD disk toobe copied.</span></span>

 ```powershell
$disk = Get-AzureRmDisk -ResourceGroupName $resourceGroupName -DiskName $dataDiskName 
```
3. <span data-ttu-id="fee1e-135">Merhaba, anlık görüntü yapılandırmaları oluşturun.</span><span class="sxs-lookup"><span data-stu-id="fee1e-135">Create hello snapshot configurations.</span></span> 

 ```powershell
$snapshot =  New-AzureRmSnapshotConfig -SourceUri $disk.Id -CreateOption Copy -Location $location 
```
4. <span data-ttu-id="fee1e-136">Başlangıç anlık görüntü alın.</span><span class="sxs-lookup"><span data-stu-id="fee1e-136">Take hello snapshot.</span></span>

 ```powershell
New-AzureRmSnapshot -Snapshot $snapshot -SnapshotName $snapshotName -ResourceGroupName $resourceGroupName 
```
<span data-ttu-id="fee1e-137">Yönetilen bir Disk toouse hello anlık görüntü toocreate planlamak ve toobe yüksek performanslı gereken VM ekleme, hello parametresini kullanmanız `-AccountType Premium_LRS` hello yeni AzureRmSnapshot komutu.</span><span class="sxs-lookup"><span data-stu-id="fee1e-137">If you plan toouse hello snapshot toocreate a Managed Disk and attach it a VM that needs toobe high performing, use hello parameter `-AccountType Premium_LRS` with hello New-AzureRmSnapshot command.</span></span> <span data-ttu-id="fee1e-138">Merhaba parametre hello anlık görüntü oluşturur, böylece yönetilen bir Premium Disk depolanır.</span><span class="sxs-lookup"><span data-stu-id="fee1e-138">hello parameter creates hello snapshot so that it's stored as a Premium Managed Disk.</span></span> <span data-ttu-id="fee1e-139">Premium yönetilen diskleri standart daha pahalıdır.</span><span class="sxs-lookup"><span data-stu-id="fee1e-139">Premium Managed Disks are more expensive than Standard.</span></span> <span data-ttu-id="fee1e-140">Bu nedenle bu parametrenin kullanmadan önce Premium gerçekten ihtiyacınız emin olun.</span><span class="sxs-lookup"><span data-stu-id="fee1e-140">So be sure you really need Premium before using that parameter.</span></span>


