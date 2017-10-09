---
title: "aaaCreate VM kullanılabilirlik kümesi Azure'da | Microsoft Docs"
description: "Nasıl toocreate yönetilen bir kullanılabilirlik kümesi veya yönetilmeyen kullanılabilirlik Azure PowerShell kullanarak, sanal makineleriniz için ayarlamak veya portal hello Resource Manager dağıtım modelinde hello öğrenin."
keywords: "Kullanılabilirlik kümesi"
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: a3db8659-ace8-4e78-8b8c-1e75c04c042c
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: cynthn
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: eadcdfcd28bb2fa21a4647f207b390c33e022ef1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="increase-vm-availability-by-creating-an-azure-availability-set"></a><span data-ttu-id="0066d-104">Bir Azure kullanılabilirlik kümesi oluşturarak artış VM kullanılabilirliği</span><span class="sxs-lookup"><span data-stu-id="0066d-104">Increase VM availability by creating an Azure availability set</span></span> 
<span data-ttu-id="0066d-105">Kullanılabilirlik kümeleri artıklık tooyour uygulama sağlar.</span><span class="sxs-lookup"><span data-stu-id="0066d-105">Availability sets provide redundancy tooyour application.</span></span> <span data-ttu-id="0066d-106">Bir kullanılabilirlik kümesinde iki veya daha fazla sanal makineyi gruplandırmanız önerilir.</span><span class="sxs-lookup"><span data-stu-id="0066d-106">We recommend that you group two or more virtual machines in an availability set.</span></span> <span data-ttu-id="0066d-107">Bu yapılandırma ya da planlı veya plansız bir bakım olayı sırasında en az bir sanal makine kullanılabilir ve karşılayan hello %99,95 olmasını sağlar Azure SLA.</span><span class="sxs-lookup"><span data-stu-id="0066d-107">This configuration ensures that during either a planned or unplanned maintenance event, at least one virtual machine will be available and meet hello 99.95% Azure SLA.</span></span> <span data-ttu-id="0066d-108">Daha fazla bilgi için bkz: Merhaba [sanal makineler için SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/).</span><span class="sxs-lookup"><span data-stu-id="0066d-108">For more information, see hello [SLA for Virtual Machines](https://azure.microsoft.com/support/legal/sla/virtual-machines/).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0066d-109">Sanal makineleri oluşturulmalıdır hello aynı kaynak grubu hello kullanılabilirlik kümesi olarak.</span><span class="sxs-lookup"><span data-stu-id="0066d-109">VMs must be created in hello same resource group as hello availability set.</span></span>
> 

<span data-ttu-id="0066d-110">Bir kullanılabilirlik kümesi, VM toobe parçası istiyorsanız toocreate hello kullanılabilirlik gerekir ayarlamak ilk ya da yazarken, ilk VM hello kümesinde oluşturmakta olduğunuz.</span><span class="sxs-lookup"><span data-stu-id="0066d-110">If you want your VM toobe part of an availability set, you need toocreate hello availability set first or while you are creating your first VM in hello set.</span></span> <span data-ttu-id="0066d-111">VM diskleri yönetilen kullanıyorsanız, hello kullanılabilirlik kümesi yönetilen kullanılabilirlik kümesi oluşturulmuş olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="0066d-111">If your VM will be using Managed Disks, hello availability set must be created as a managed availability set.</span></span>

<span data-ttu-id="0066d-112">Oluşturma ve kullanılabilirlik kümelerini kullanma hakkında daha fazla bilgi için bkz: [hello sanal makinelerin kullanılabilirliğini yönetme](manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0066d-112">For more information about creating and using availability sets, see [Manage hello availability of virtual machines](manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="use-hello-portal-toocreate-an-availability-set-before-creating-your-vms"></a><span data-ttu-id="0066d-113">Merhaba portal toocreate kullanılabilirlik kümesi, sanal makineleri oluşturmadan önce kullanın</span><span class="sxs-lookup"><span data-stu-id="0066d-113">Use hello portal toocreate an availability set before creating your VMs</span></span>
1. <span data-ttu-id="0066d-114">Merhaba hub menüsünde tıklatın **Gözat** seçip **kullanılabilirlik kümeleri**.</span><span class="sxs-lookup"><span data-stu-id="0066d-114">In hello hub menu, click **Browse** and select **Availability sets**.</span></span>
2. <span data-ttu-id="0066d-115">Merhaba üzerinde **kullanılabilirlik kümeleri dikey**, tıklatın **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="0066d-115">On hello **Availability sets blade**, click **Add**.</span></span>
   
    ![Merhaba gösteren ekran görüntüsü yeni bir kullanılabilirlik kümesi oluşturmak için düğmesi ekleyin.](./media/create-availability-set/add-availability-set.png)
3. <span data-ttu-id="0066d-117">Merhaba üzerinde **kullanılabilirlik kümesi oluştur** dikey penceresinde, kümeniz için tam hello bilgileri.</span><span class="sxs-lookup"><span data-stu-id="0066d-117">On hello **Create availability set** blade, complete hello information for your set.</span></span>
   
    ![Ekran görüntüsü gösterildiği tooenter toocreate hello kullanılabilirlik gereksinim duyduğunuz bilgileri hello ayarlayın.](./media/create-availability-set/create-availability-set.png)
   
   * <span data-ttu-id="0066d-119">**Ad** -hello adı, sayı, harf, nokta, alt çizgi ve tire oluşan 1-80 karakter olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="0066d-119">**Name** - hello name should be 1-80 characters made up of numbers, letters, periods, underscores and dashes.</span></span> <span data-ttu-id="0066d-120">Merhaba ilk karakteri bir harf veya sayı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="0066d-120">hello first character must be a letter or number.</span></span> <span data-ttu-id="0066d-121">Merhaba son karakter bir harf, sayı veya alt çizgi olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="0066d-121">hello last character must be a letter, number or underscore.</span></span>
   * <span data-ttu-id="0066d-122">**Hata etki alanları** -hata etki alanlarını tanımlayın hello Grup sanal makinelerin, ortak bir güç kaynağı ve ağ anahtarını paylaşır.</span><span class="sxs-lookup"><span data-stu-id="0066d-122">**Fault domains** - fault domains define hello group of virtual machines that share a common power source and network switch.</span></span> <span data-ttu-id="0066d-123">Varsayılan olarak, hello VM'ler toothree hata etki alanları arasında ayrılır ve değiştirilen toobetween 1 ve 3 olabilir.</span><span class="sxs-lookup"><span data-stu-id="0066d-123">By default, hello VMs  are separated across up toothree fault domains and can be changed toobetween 1 and 3.</span></span>
   * <span data-ttu-id="0066d-124">**Güncelleme etki alanları** - beş güncelleştirme etki alanları, varsayılan olarak atanır ve bu toobetween 1 ve 20 ayarlanabilir.</span><span class="sxs-lookup"><span data-stu-id="0066d-124">**Update domains** -  five update domains are assigned by default and this can be set toobetween 1 and 20.</span></span> <span data-ttu-id="0066d-125">Güncelleme etki alanına belirtmek sanal makineler ve hello yeniden temel alınan fiziksel donanım grupları aynı anda.</span><span class="sxs-lookup"><span data-stu-id="0066d-125">Update domains indicate groups of virtual machines and underlying physical hardware that can be rebooted at hello same time.</span></span> <span data-ttu-id="0066d-126">Örneğin, beş güncelleştirme beşten fazla sanal makine bir tek kullanılabilirlik kümesi içinde hello altıncı sanal makine yapılandırıldığında etki alanları, yerleştirilir hello hello ilk sanal makineye aynı güncelleştirme etki hello seventh içinde belirtirseniz, aynı hello UD hello ikinci sanal makine vb. olarak.</span><span class="sxs-lookup"><span data-stu-id="0066d-126">For example, if we specify five update domains, when more than five virtual machines are configured within a single Availability Set, hello sixth virtual machine will be placed into hello same update domain as hello first virtual machine, hello seventh in hello same UD as hello second virtual machine, and so on.</span></span> <span data-ttu-id="0066d-127">Merhaba yeniden başlatmalar Hello sırasını sıralı değil, ancak aynı anda yalnızca tek bir güncelleştirme etki alanı yeniden başlatılacak.</span><span class="sxs-lookup"><span data-stu-id="0066d-127">hello order of hello reboots may not be sequential, but only one update domain will be rebooted at a time.</span></span>
   * <span data-ttu-id="0066d-128">**Abonelik** -birden fazla varsa hello abonelik toouse seçin.</span><span class="sxs-lookup"><span data-stu-id="0066d-128">**Subscription** - select hello subscription toouse if you have more than one.</span></span>
   * <span data-ttu-id="0066d-129">**Kaynak grubu** -hello okunu ve bir kaynak grubu hello seçerek varolan bir kaynak grubu açılan menüsünü seçin.</span><span class="sxs-lookup"><span data-stu-id="0066d-129">**Resource group** - select an existing resource group by clicking hello arrow and selecting a resource group from hello drop down.</span></span> <span data-ttu-id="0066d-130">Ayrıca, bir ad yazarak yeni bir kaynak grubu oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0066d-130">You can also create a new resource group by typing in a name.</span></span> <span data-ttu-id="0066d-131">Merhaba adı aşağıdaki karakterleri hello birini içerebilir: harf, sayı, nokta, tire, alt çizgi ve açma veya kapatma parantezi.</span><span class="sxs-lookup"><span data-stu-id="0066d-131">hello name can contain any of hello following characters: letters, numbers, periods, dashes, underscores and opening or closing parenthesis.</span></span> <span data-ttu-id="0066d-132">Merhaba ad bir nokta ile bitemez.</span><span class="sxs-lookup"><span data-stu-id="0066d-132">hello name cannot end in a period.</span></span> <span data-ttu-id="0066d-133">Merhaba VM'ler hello kullanılabilirlik grubundaki tümüne hello oluşturulan toobe ihtiyaç hello kullanılabilirlik kümesi ile aynı kaynak grubunda.</span><span class="sxs-lookup"><span data-stu-id="0066d-133">All of hello VMs in hello availability group need toobe created in hello same resource group as hello availability set.</span></span>
   * <span data-ttu-id="0066d-134">**Konum** -hello açılan listeden bir konum seçin.</span><span class="sxs-lookup"><span data-stu-id="0066d-134">**Location** - select a location from hello drop-down.</span></span>
   * <span data-ttu-id="0066d-135">**Yönetilen** - seçin *Evet* toocreate yönetilen kullanılabilirlik toouse yönetilen diskler için depolama kullanan sanal makineler ile ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="0066d-135">**Managed** - select *Yes* toocreate a managed availability set toouse with VMs that use Managed Disks for storage.</span></span> <span data-ttu-id="0066d-136">Seçin **Hayır** hello hello ayarlanır VM'ler bir depolama hesabında yönetilmeyen diskler kullanıyorsanız.</span><span class="sxs-lookup"><span data-stu-id="0066d-136">Select **No** if hello VMs that will be in hello set use unmanaged disks in a storage account.</span></span>
   
4. <span data-ttu-id="0066d-137">Merhaba bilgi girmeyi tamamladığınızda, tıklatın **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="0066d-137">When you are done entering hello information, click **Create**.</span></span> 

## <a name="use-hello-portal-toocreate-a-virtual-machine-and-an-availability-set-at-hello-same-time"></a><span data-ttu-id="0066d-138">Bir sanal makine ve bir kullanılabilirlik kümesi hello aynı hello portal toocreate kullanma zamanı</span><span class="sxs-lookup"><span data-stu-id="0066d-138">Use hello portal toocreate a virtual machine and an availability set at hello same time</span></span>
<span data-ttu-id="0066d-139">Merhaba portal kullanarak yeni bir VM oluşturuyorsanız, yeni bir kullanılabilirlik hello oluştururken Merhaba VM kümesi de oluşturabilirsiniz hello kümesindeki ilk VM.</span><span class="sxs-lookup"><span data-stu-id="0066d-139">If you are creating a new VM using hello portal, you can also create a new availability set for hello VM while you create hello first VM in hello set.</span></span> <span data-ttu-id="0066d-140">VM için toouse yönetilen diskleri seçerseniz, bir yönetilen kullanılabilirlik kümesi oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="0066d-140">If you choose toouse Managed Disks for your VM, a managed availability set will be created.</span></span>

![Yeni bir kullanılabilirlik hello VM oluştururken kümesi oluşturmak için başlangıç işlemini gösteren ekran görüntüsü.](./media/create-availability-set/new-vm-avail-set.png)

## <a name="add-a-new-vm-tooan-existing-availability-set-in-hello-portal"></a><span data-ttu-id="0066d-142">Merhaba Portalı'nda bir yeni VM tooan varolan kullanılabilirlik kümesi Ekle</span><span class="sxs-lookup"><span data-stu-id="0066d-142">Add a new VM tooan existing availability set in hello portal</span></span>
<span data-ttu-id="0066d-143">Hello kümesinde ait, içinde oluşturduğunuzdan emin olun, oluşturduğunuz her ek VM için aynı hello **kaynak grubu** ve ardından adım 3'te mevcut kullanılabilirlik seçin hello.</span><span class="sxs-lookup"><span data-stu-id="0066d-143">For each additional VM that you create that should belong in hello set, make sure that you create it in hello same **resource group** and then select hello existing availability set in Step 3.</span></span> 

![Tooselect varolan kullanılabilirlik toouse VM için nasıl ayarlanacağını gösteren ekran görüntüsü.](./media/create-availability-set/add-vm-to-set.png)

## <a name="use-powershell-toocreate-an-availability-set"></a><span data-ttu-id="0066d-145">PowerShell toocreate kullanılabilirlik kullanmak ayarlayın</span><span class="sxs-lookup"><span data-stu-id="0066d-145">Use PowerShell toocreate an availability set</span></span>
<span data-ttu-id="0066d-146">Bu örnek, kullanılabilirlik adlandırılmış kümesi oluşturur **myAvailabilitySet** hello içinde **myResourceGroup** hello kaynak grubunda **Batı ABD** konumu.</span><span class="sxs-lookup"><span data-stu-id="0066d-146">This example creates an availability set named **myAvailabilitySet** in hello **myResourceGroup** resource group in hello **West US** location.</span></span> <span data-ttu-id="0066d-147">Bu hello oluşturmadan önce bitti toobe gereken hello ayarlanır ilk VM.</span><span class="sxs-lookup"><span data-stu-id="0066d-147">This needs toobe done before you create hello first VM that will be in hello set.</span></span>

<span data-ttu-id="0066d-148">Başlamadan önce hello hello AzureRM.Compute PowerShell modülü en son sürümüne sahip olduğunuzdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="0066d-148">Before you begin, make sure that you have hello latest version of hello AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="0066d-149">Çalıştırma hello komut tooinstall onu.</span><span class="sxs-lookup"><span data-stu-id="0066d-149">Run hello following command tooinstall it.</span></span>

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
<span data-ttu-id="0066d-150">Daha fazla bilgi için bkz: [Azure PowerShell sürüm](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="0066d-150">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


<span data-ttu-id="0066d-151">Vm'leriniz için yönetilen diskler kullanıyorsanız yazın:</span><span class="sxs-lookup"><span data-stu-id="0066d-151">If you are using managed disks for your VMs, type:</span></span>

```powershell
    New-AzureRmAvailabilitySet -ResourceGroupName "myResourceGroup" '
    -Name "myAvailabilitySet" -Location "West US" -managed
```

<span data-ttu-id="0066d-152">Vm'leriniz için kendi depolama hesapları kullanıyorsanız yazın:</span><span class="sxs-lookup"><span data-stu-id="0066d-152">If you are using your own storage accounts for your VMs, type:</span></span>

```powershell
    New-AzureRmAvailabilitySet -ResourceGroupName "myResourceGroup" '
    -Name "myAvailabilitySet" -Location "West US" 
```

<span data-ttu-id="0066d-153">Daha fazla bilgi için bkz: [yeni AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span><span class="sxs-lookup"><span data-stu-id="0066d-153">For more information, see [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="0066d-154">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="0066d-154">Troubleshooting</span></span>
* <span data-ttu-id="0066d-155">Oluşturduğunuzda istediğiniz hello kullanılabilirlik kümesini hello portal hello aşağı açılan listesinde, yoksa bir VM, farklı bir kaynak grubu içinde oluşturduktan.</span><span class="sxs-lookup"><span data-stu-id="0066d-155">When you create a VM, if hello availability set you want isn't in hello drop-down list in hello portal you may have created it in a different resource group.</span></span> <span data-ttu-id="0066d-156">Merhaba kaynak grubu, kullanılabilirlik için ayarlayın, Git toohello hub menüsünde ve Gözat'ı tıklatın bilmiyorsanız > kullanılabilirlik kümeleri, kullanılabilirlik listesini ayarlar ve hangi kaynak grupları ait oldukları toosee.</span><span class="sxs-lookup"><span data-stu-id="0066d-156">If you don't know hello resource group for your availability set, go toohello hub menu and click Browse > Availability sets toosee a list of your availability sets and which resource groups they belong to.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0066d-157">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="0066d-157">Next steps</span></span>
<span data-ttu-id="0066d-158">Ek depolama alanı tooyour VM ek ekleyerek [veri diski](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0066d-158">Add additional storage tooyour VM by adding an additional [data disk](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

