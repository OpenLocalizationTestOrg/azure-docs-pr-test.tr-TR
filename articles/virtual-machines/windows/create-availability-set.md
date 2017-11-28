---
title: "Azure üzerinde ayarlanmış bir VM kullanılabilirlik oluştur | Microsoft Docs"
description: "Yönetilen kullanılabilirlik kümesi veya yönetilmeyen kullanılabilirlik Azure PowerShell veya portal Resource Manager dağıtım modelinde kullanarak, sanal makineleriniz kümesi oluşturmayı öğrenin."
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
ms.openlocfilehash: e813ade8e105169f21138ed8a8eafda1ff39f42e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="increase-vm-availability-by-creating-an-azure-availability-set"></a><span data-ttu-id="eec2c-104">Bir Azure kullanılabilirlik kümesi oluşturarak artış VM kullanılabilirliği</span><span class="sxs-lookup"><span data-stu-id="eec2c-104">Increase VM availability by creating an Azure availability set</span></span> 
<span data-ttu-id="eec2c-105">Kullanılabilirlik kümeleri, uygulamanız için artıklık sağlar.</span><span class="sxs-lookup"><span data-stu-id="eec2c-105">Availability sets provide redundancy to your application.</span></span> <span data-ttu-id="eec2c-106">Bir kullanılabilirlik kümesinde iki veya daha fazla sanal makineyi gruplandırmanız önerilir.</span><span class="sxs-lookup"><span data-stu-id="eec2c-106">We recommend that you group two or more virtual machines in an availability set.</span></span> <span data-ttu-id="eec2c-107">Bu yapılandırma ya da planlı veya plansız bir bakım olayı sırasında en az bir sanal makinenin kullanılabilir durumda olmasını ve %99,95 karşıladığından emin sağlar Azure SLA.</span><span class="sxs-lookup"><span data-stu-id="eec2c-107">This configuration ensures that during either a planned or unplanned maintenance event, at least one virtual machine will be available and meet the 99.95% Azure SLA.</span></span> <span data-ttu-id="eec2c-108">Daha fazla bilgi için bkz. [Sanal Makineler için SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/).</span><span class="sxs-lookup"><span data-stu-id="eec2c-108">For more information, see the [SLA for Virtual Machines](https://azure.microsoft.com/support/legal/sla/virtual-machines/).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="eec2c-109">Sanal makineleri kullanılabilirlik kümesi ile aynı kaynak grubunda oluşturulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="eec2c-109">VMs must be created in the same resource group as the availability set.</span></span>
> 

<span data-ttu-id="eec2c-110">Bir kullanılabilirlik kümesinin parçası olarak, VM istiyorsanız, önce ayarlamanız kullanılabilirlik oluşturmanız gerekir veya kümesindeki ilk VM oluştururken.</span><span class="sxs-lookup"><span data-stu-id="eec2c-110">If you want your VM to be part of an availability set, you need to create the availability set first or while you are creating your first VM in the set.</span></span> <span data-ttu-id="eec2c-111">VM diskleri yönetilen kullanıyorsanız, kullanılabilirlik kümesi yönetilen kullanılabilirlik kümesi oluşturulmuş olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="eec2c-111">If your VM will be using Managed Disks, the availability set must be created as a managed availability set.</span></span>

<span data-ttu-id="eec2c-112">Oluşturma ve kullanılabilirlik kümelerini kullanma hakkında daha fazla bilgi için bkz: [sanal makinelerin kullanılabilirliğini yönetme](manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="eec2c-112">For more information about creating and using availability sets, see [Manage the availability of virtual machines](manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="use-the-portal-to-create-an-availability-set-before-creating-your-vms"></a><span data-ttu-id="eec2c-113">Kullanılabilirlik kümesi, sanal makineleri oluşturmadan önce oluşturmak üzere portalı kullanın</span><span class="sxs-lookup"><span data-stu-id="eec2c-113">Use the portal to create an availability set before creating your VMs</span></span>
1. <span data-ttu-id="eec2c-114">Hub menüsünde tıklatın **Gözat** seçip **kullanılabilirlik kümeleri**.</span><span class="sxs-lookup"><span data-stu-id="eec2c-114">In the hub menu, click **Browse** and select **Availability sets**.</span></span>
2. <span data-ttu-id="eec2c-115">Üzerinde **kullanılabilirlik kümeleri dikey**, tıklatın **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="eec2c-115">On the **Availability sets blade**, click **Add**.</span></span>
   
    ![Yeni kullanılabilirlik oluşturmak için Ekle düğmesini gösteren ekran görüntüsü ayarlayın.](./media/create-availability-set/add-availability-set.png)
3. <span data-ttu-id="eec2c-117">Üzerinde **kullanılabilirlik kümesi oluştur** dikey penceresinde, kümeniz için bilgileri tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="eec2c-117">On the **Create availability set** blade, complete the information for your set.</span></span>
   
    ![Kullanılabilirlik kümesi oluşturmak için girmenize gerek bilgileri gösteren ekran görüntüsü.](./media/create-availability-set/create-availability-set.png)
   
   * <span data-ttu-id="eec2c-119">**Ad** -ad rakam, harf, nokta, alt çizgi ve tire oluşan 1-80 karakterden uzun olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="eec2c-119">**Name** - the name should be 1-80 characters made up of numbers, letters, periods, underscores and dashes.</span></span> <span data-ttu-id="eec2c-120">İlk karakteri bir harf veya sayı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="eec2c-120">The first character must be a letter or number.</span></span> <span data-ttu-id="eec2c-121">Son karakter bir harf, sayı veya alt çizgi olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="eec2c-121">The last character must be a letter, number or underscore.</span></span>
   * <span data-ttu-id="eec2c-122">**Hata etki alanları** -hata etki alanlarını tanımlayın ortak bir güç kaynağı ve ağ anahtarı paylaşmak sanal makineler grubudur.</span><span class="sxs-lookup"><span data-stu-id="eec2c-122">**Fault domains** - fault domains define the group of virtual machines that share a common power source and network switch.</span></span> <span data-ttu-id="eec2c-123">Varsayılan olarak, sanal makineleri en çok üç hata etki alanlarında ayrılır ve 1 ile 3 arasında değiştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="eec2c-123">By default, the VMs  are separated across up to three fault domains and can be changed to between 1 and 3.</span></span>
   * <span data-ttu-id="eec2c-124">**Güncelleme etki alanları** - beş güncelleştirme etki alanları, varsayılan olarak atanır ve bu 1 ve 20 arasında ayarlanabilir.</span><span class="sxs-lookup"><span data-stu-id="eec2c-124">**Update domains** -  five update domains are assigned by default and this can be set to between 1 and 20.</span></span> <span data-ttu-id="eec2c-125">Güncelleme etki alanına sanal makineler ve aynı anda yeniden temel alınan fiziksel donanım grupları belirtin.</span><span class="sxs-lookup"><span data-stu-id="eec2c-125">Update domains indicate groups of virtual machines and underlying physical hardware that can be rebooted at the same time.</span></span> <span data-ttu-id="eec2c-126">Örneğin, beşten fazla sanal makine kullanılabilirlik tek bir kümesi içinde yapılandırıldığında beş güncelleme etki alanları, belirtirseniz, altıncı sanal makine ilk sanal makineye aynı UD ikinci sanal makine olarak yedinci aynı güncelleştirme etki yerleştirilir ve benzeri.</span><span class="sxs-lookup"><span data-stu-id="eec2c-126">For example, if we specify five update domains, when more than five virtual machines are configured within a single Availability Set, the sixth virtual machine will be placed into the same update domain as the first virtual machine, the seventh in the same UD as the second virtual machine, and so on.</span></span> <span data-ttu-id="eec2c-127">Yeniden başlatma sırasını sıralı değil, ancak aynı anda yalnızca tek bir güncelleştirme etki alanı yeniden başlatılacak.</span><span class="sxs-lookup"><span data-stu-id="eec2c-127">The order of the reboots may not be sequential, but only one update domain will be rebooted at a time.</span></span>
   * <span data-ttu-id="eec2c-128">**Abonelik** -birden fazla varsa, kullanılacak aboneliği seçin.</span><span class="sxs-lookup"><span data-stu-id="eec2c-128">**Subscription** - select the subscription to use if you have more than one.</span></span>
   * <span data-ttu-id="eec2c-129">**Kaynak grubu** -oka tıklayarak ve aşağı açılan listeden bir kaynak grubu seçerek varolan bir kaynak grubu seçin.</span><span class="sxs-lookup"><span data-stu-id="eec2c-129">**Resource group** - select an existing resource group by clicking the arrow and selecting a resource group from the drop down.</span></span> <span data-ttu-id="eec2c-130">Ayrıca, bir ad yazarak yeni bir kaynak grubu oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eec2c-130">You can also create a new resource group by typing in a name.</span></span> <span data-ttu-id="eec2c-131">Ad aşağıdaki karakterlerden herhangi birini içerebilir: harf, sayı, nokta, tire, alt çizgi ve açma veya kapatma parantezi.</span><span class="sxs-lookup"><span data-stu-id="eec2c-131">The name can contain any of the following characters: letters, numbers, periods, dashes, underscores and opening or closing parenthesis.</span></span> <span data-ttu-id="eec2c-132">Ad bir nokta ile bitemez.</span><span class="sxs-lookup"><span data-stu-id="eec2c-132">The name cannot end in a period.</span></span> <span data-ttu-id="eec2c-133">Tüm sanal makineleri kullanılabilirlik grubundaki kullanılabilirlik kümesi ile aynı kaynak grubunda oluşturulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="eec2c-133">All of the VMs in the availability group need to be created in the same resource group as the availability set.</span></span>
   * <span data-ttu-id="eec2c-134">**Konum** -açılan listeden bir konum seçin.</span><span class="sxs-lookup"><span data-stu-id="eec2c-134">**Location** - select a location from the drop-down.</span></span>
   * <span data-ttu-id="eec2c-135">**Yönetilen** - seçin *Evet* yönetilen diskler için depolama kullanan sanal makineler ile kullanmak üzere ayarlanmış yönetilen bir kullanılabilirlik oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="eec2c-135">**Managed** - select *Yes* to create a managed availability set to use with VMs that use Managed Disks for storage.</span></span> <span data-ttu-id="eec2c-136">Seçin **Hayır** kümesinde olacak VM'ler yönetilmeyen diskler bir depolama hesabı kullanıyorsanız.</span><span class="sxs-lookup"><span data-stu-id="eec2c-136">Select **No** if the VMs that will be in the set use unmanaged disks in a storage account.</span></span>
   
4. <span data-ttu-id="eec2c-137">İşiniz bittiğinde bilgileri girerek, tıklatın **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="eec2c-137">When you are done entering the information, click **Create**.</span></span> 

## <a name="use-the-portal-to-create-a-virtual-machine-and-an-availability-set-at-the-same-time"></a><span data-ttu-id="eec2c-138">Bir sanal makine ve kullanılabilirlik aynı anda kümesi oluşturmak üzere portalı kullanın</span><span class="sxs-lookup"><span data-stu-id="eec2c-138">Use the portal to create a virtual machine and an availability set at the same time</span></span>
<span data-ttu-id="eec2c-139">Portalı'nı kullanarak yeni bir VM oluşturuyorsanız, yeni bir kullanılabilirlik kümesinde ilk VM oluştururken VM için kümesi de oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eec2c-139">If you are creating a new VM using the portal, you can also create a new availability set for the VM while you create the first VM in the set.</span></span> <span data-ttu-id="eec2c-140">VM için yönetilen diskleri kullanmayı seçerseniz, bir yönetilen kullanılabilirlik kümesi oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="eec2c-140">If you choose to use Managed Disks for your VM, a managed availability set will be created.</span></span>

![Yeni bir kullanılabilirlik VM oluştururken kümesi oluşturmayı gösteren ekran görüntüsü.](./media/create-availability-set/new-vm-avail-set.png)

## <a name="add-a-new-vm-to-an-existing-availability-set-in-the-portal"></a><span data-ttu-id="eec2c-142">Var olan kullanılabilirlik kümesi Portalı'nda yeni bir VM ekleme</span><span class="sxs-lookup"><span data-stu-id="eec2c-142">Add a new VM to an existing availability set in the portal</span></span>
<span data-ttu-id="eec2c-143">Kümeye ait olan, oluşturduğunuz her ek VM için onu aynı oluşturduğunuzdan emin olun **kaynak grubu** ve var olan kullanılabilirlik adım 3'te kümesini seçin.</span><span class="sxs-lookup"><span data-stu-id="eec2c-143">For each additional VM that you create that should belong in the set, make sure that you create it in the same **resource group** and then select the existing availability set in Step 3.</span></span> 

![VM için kullanmak üzere bir var olan kullanılabilirlik kümesi seçme gösteren ekran görüntüsü.](./media/create-availability-set/add-vm-to-set.png)

## <a name="use-powershell-to-create-an-availability-set"></a><span data-ttu-id="eec2c-145">Bir kullanılabilirlik kümesi oluşturmak için PowerShell kullanın</span><span class="sxs-lookup"><span data-stu-id="eec2c-145">Use PowerShell to create an availability set</span></span>
<span data-ttu-id="eec2c-146">Bu örnek, kullanılabilirlik adlandırılmış kümesi oluşturur **myAvailabilitySet** içinde **myResourceGroup** kaynak grubunda **Batı ABD** konumu.</span><span class="sxs-lookup"><span data-stu-id="eec2c-146">This example creates an availability set named **myAvailabilitySet** in the **myResourceGroup** resource group in the **West US** location.</span></span> <span data-ttu-id="eec2c-147">Bu kümede yer alacak ilk VM oluşturmadan önce yapılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="eec2c-147">This needs to be done before you create the first VM that will be in the set.</span></span>

<span data-ttu-id="eec2c-148">Başlamadan önce AzureRM.Compute PowerShell modülü en son sürümüne sahip olduğunuzdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="eec2c-148">Before you begin, make sure that you have the latest version of the AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="eec2c-149">Yüklemek için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="eec2c-149">Run the following command to install it.</span></span>

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
<span data-ttu-id="eec2c-150">Daha fazla bilgi için bkz: [Azure PowerShell sürüm](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="eec2c-150">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


<span data-ttu-id="eec2c-151">Vm'leriniz için yönetilen diskler kullanıyorsanız yazın:</span><span class="sxs-lookup"><span data-stu-id="eec2c-151">If you are using managed disks for your VMs, type:</span></span>

```powershell
    New-AzureRmAvailabilitySet -ResourceGroupName "myResourceGroup" '
    -Name "myAvailabilitySet" -Location "West US" -managed
```

<span data-ttu-id="eec2c-152">Vm'leriniz için kendi depolama hesapları kullanıyorsanız yazın:</span><span class="sxs-lookup"><span data-stu-id="eec2c-152">If you are using your own storage accounts for your VMs, type:</span></span>

```powershell
    New-AzureRmAvailabilitySet -ResourceGroupName "myResourceGroup" '
    -Name "myAvailabilitySet" -Location "West US" 
```

<span data-ttu-id="eec2c-153">Daha fazla bilgi için bkz: [yeni AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span><span class="sxs-lookup"><span data-stu-id="eec2c-153">For more information, see [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="eec2c-154">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="eec2c-154">Troubleshooting</span></span>
* <span data-ttu-id="eec2c-155">Portal aşağı açılan listesinde, istediğiniz kullanılabilirlik kümesi değilse, bir VM oluştururken farklı kaynak grubunda oluşturduğunuz.</span><span class="sxs-lookup"><span data-stu-id="eec2c-155">When you create a VM, if the availability set you want isn't in the drop-down list in the portal you may have created it in a different resource group.</span></span> <span data-ttu-id="eec2c-156">Kaynak grubu, kullanılabilirlik için ayarlayın, hub menüsüne gidin ve Gözat'ı bilmiyorsanız > kullanılabilirlik kümeleri, kullanılabilirlik kümeleri ve hangi listesini görmek için kaynak gruplarını ait oldukları.</span><span class="sxs-lookup"><span data-stu-id="eec2c-156">If you don't know the resource group for your availability set, go to the hub menu and click Browse > Availability sets to see a list of your availability sets and which resource groups they belong to.</span></span>

## <a name="next-steps"></a><span data-ttu-id="eec2c-157">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="eec2c-157">Next steps</span></span>
<span data-ttu-id="eec2c-158">Ek depolama alanı, VM için ek bir ekleyerek [veri diski](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="eec2c-158">Add additional storage to your VM by adding an additional [data disk](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

