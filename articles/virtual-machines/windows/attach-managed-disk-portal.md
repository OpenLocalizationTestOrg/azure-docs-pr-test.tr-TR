---
title: "Bir Windows VM - Azure bir yönetilen veri diski Ekle | Microsoft Docs"
description: "Bir Windows VM Resource Manager dağıtım modelini kullanarak Azure portalında yeni yönetilen veri diski ekleme yapma."
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
ms.date: 05/09/2017
ms.author: cynthn
ms.openlocfilehash: f0cf88a06c5470ef173b22e7213419a6c8760723
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-attach-a-managed-data-disk-to-a-windows-vm-in-the-azure-portal"></a><span data-ttu-id="fd27f-103">Nasıl bir Windows VM Azure portalında bir yönetilen veri diski kullanıma açın</span><span class="sxs-lookup"><span data-stu-id="fd27f-103">How to attach a managed data disk to a Windows VM in the Azure portal</span></span>

<span data-ttu-id="fd27f-104">Bu makalede Azure portal ile Windows sanal makineleri yeni bir yönetilen veri diski ekleme gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="fd27f-104">This article shows you how to attach a new managed data disk to Windows virtual machines through the Azure portal.</span></span> <span data-ttu-id="fd27f-105">Bunu önce bu ipuçlarını gözden geçirin:</span><span class="sxs-lookup"><span data-stu-id="fd27f-105">Before you do this, review these tips:</span></span>

* <span data-ttu-id="fd27f-106">Sanal makinenin boyutunu, iliştirebilirsiniz kaç tane veri diskleri denetler.</span><span class="sxs-lookup"><span data-stu-id="fd27f-106">The size of the virtual machine controls how many data disks you can attach.</span></span> <span data-ttu-id="fd27f-107">Ayrıntılar için bkz [sanal makineler için Boyutlar](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="fd27f-107">For details, see [Sizes for virtual machines](sizes.md).</span></span>
* <span data-ttu-id="fd27f-108">Yeni bir disk için bunu eklediğinizde Azure bunu oluşturduğundan ilk oluşturmanız gerekmez.</span><span class="sxs-lookup"><span data-stu-id="fd27f-108">For a new disk, you don't need to create it first because Azure creates it when you attach it.</span></span>

<span data-ttu-id="fd27f-109">Ayrıca [Powershell kullanarak bir veri diskini](attach-disk-ps.md).</span><span class="sxs-lookup"><span data-stu-id="fd27f-109">You can also [attach a data disk using Powershell](attach-disk-ps.md).</span></span>



## <a name="add-a-data-disk"></a><span data-ttu-id="fd27f-110">Bir veri diski Ekle</span><span class="sxs-lookup"><span data-stu-id="fd27f-110">Add a data disk</span></span>
1. <span data-ttu-id="fd27f-111">Soldaki menüde tıklatın **sanal makineleri**.</span><span class="sxs-lookup"><span data-stu-id="fd27f-111">In the menu on the left, click **Virtual Machines**.</span></span>
2. <span data-ttu-id="fd27f-112">Listeden sanal makineyi seçin.</span><span class="sxs-lookup"><span data-stu-id="fd27f-112">Select the virtual machine from the list.</span></span>
3. <span data-ttu-id="fd27f-113">Sanal makine dikey penceresinde **diskleri**.</span><span class="sxs-lookup"><span data-stu-id="fd27f-113">On the virtual machine blade, click **Disks**.</span></span>
   4. <span data-ttu-id="fd27f-114">Üzerinde **diskleri** dikey penceresinde tıklatın **+ Ekle veri diski**.</span><span class="sxs-lookup"><span data-stu-id="fd27f-114">On the **Disks** blade, click **+ Add data disk**.</span></span>
5. <span data-ttu-id="fd27f-115">Açılan yeni disk için seçin **boş oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="fd27f-115">In the drop-down for the new disk, select **Create empty**.</span></span>
6. <span data-ttu-id="fd27f-116">İçinde **oluşturma yönetilen disk** dikey penceresinde, disk için bir ad yazın ve diğer ayarları gerektiği gibi ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="fd27f-116">In the **Create managed disk** blade, type in a name for the disk and adjust the other settings as necessary.</span></span> <span data-ttu-id="fd27f-117">İşiniz bittiğinde tıklatın **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="fd27f-117">When you are done, click **Create**.</span></span>
7. <span data-ttu-id="fd27f-118">İçinde **diskleri** dikey penceresinde, VM için yeni disk yapılandırmasını kaydetmek için Kaydet'i tıklatın.</span><span class="sxs-lookup"><span data-stu-id="fd27f-118">In the **Disks** blade, click save to save the new disk configuration for the VM.</span></span>
6. <span data-ttu-id="fd27f-119">Azure disk oluşturur ve sanal makineye iliştirir sonra yeni disk sanal makinenin disk ayarları altında listelenen **veri diskleri**.</span><span class="sxs-lookup"><span data-stu-id="fd27f-119">After Azure creates the disk and attaches it to the virtual machine, the new disk is listed in the virtual machine's disk settings under **Data Disks**.</span></span>


## <a name="initialize-a-new-data-disk"></a><span data-ttu-id="fd27f-120">Yeni bir veri diski başlatın</span><span class="sxs-lookup"><span data-stu-id="fd27f-120">Initialize a new data disk</span></span>

1. <span data-ttu-id="fd27f-121">VM'ye bağlanın.</span><span class="sxs-lookup"><span data-stu-id="fd27f-121">Connect to the VM.</span></span>
1. <span data-ttu-id="fd27f-122">Başlat menüsünü türü ve VM içinde **diskmgmt.msc** ve isabet **Enter**.</span><span class="sxs-lookup"><span data-stu-id="fd27f-122">Click the start menu inside the VM and type **diskmgmt.msc** and hit **Enter**.</span></span> <span data-ttu-id="fd27f-123">Bu, Disk Yönetimi ek bileşenini başlatır.</span><span class="sxs-lookup"><span data-stu-id="fd27f-123">This will start the Disk Management snap-in.</span></span>
2. <span data-ttu-id="fd27f-124">Disk Yönetimi yeni ve başlatılmamış bir disk varsa ve diski başlatma penceresini kalkar algılar.</span><span class="sxs-lookup"><span data-stu-id="fd27f-124">Disk Management will recognize that you have a new, un-initialized disk and the Initialize Disk window will pop up.</span></span>
3. <span data-ttu-id="fd27f-125">Yeni disk seçildiğinden emin olun ve tıklayın **Tamam** başlatmak üzere.</span><span class="sxs-lookup"><span data-stu-id="fd27f-125">Make sure the new disk is selected and click **OK** to initialize it.</span></span>
4. <span data-ttu-id="fd27f-126">Yeni disk şimdi olarak görünür **ayrılmamış**.</span><span class="sxs-lookup"><span data-stu-id="fd27f-126">The new disk will now appear as **unallocated**.</span></span> <span data-ttu-id="fd27f-127">Herhangi bir yere sağ tıklatın ve disk **yeni basit birim**.</span><span class="sxs-lookup"><span data-stu-id="fd27f-127">Right-click anywhere on the disk and select **New simple volume**.</span></span> <span data-ttu-id="fd27f-128">**Yeni Basit Birim Sihirbazı** başlar.</span><span class="sxs-lookup"><span data-stu-id="fd27f-128">The **New Simple Volume Wizard** will start.</span></span>
5. <span data-ttu-id="fd27f-129">Seçim yapıldığında tüm varsayılanları, tutma Sihirbazı aracılığıyla gidin **son**.</span><span class="sxs-lookup"><span data-stu-id="fd27f-129">Go through the wizard, keeping all of the defaults, when you are done select **Finish**.</span></span>
6. <span data-ttu-id="fd27f-130">Disk Yönetimi'ni kapatın.</span><span class="sxs-lookup"><span data-stu-id="fd27f-130">Close Disk Management.</span></span>
7. <span data-ttu-id="fd27f-131">Kullanabilmeniz için önce yeni diski biçimlendirmek için gereken bir açılır pencere alırsınız.</span><span class="sxs-lookup"><span data-stu-id="fd27f-131">You will get a pop-up that you need to format the new disk before you can use it.</span></span> <span data-ttu-id="fd27f-132">Tıklatın **biçimi disk**.</span><span class="sxs-lookup"><span data-stu-id="fd27f-132">Click **Format disk**.</span></span>
8. <span data-ttu-id="fd27f-133">İçinde **biçimi yeni disk** iletişim ayarlarını kontrol edin ve ardından **Başlat**.</span><span class="sxs-lookup"><span data-stu-id="fd27f-133">In the **Format new disk** dialog, check the settings and then click **Start**.</span></span>
9. <span data-ttu-id="fd27f-134">Diskleri biçimlendirme tüm verileri silme, tıklatın bir uyarı alırsınız **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="fd27f-134">You will get a warning that formatting the disks will erase all of the data, click **OK**.</span></span>
10. <span data-ttu-id="fd27f-135">Biçimlendirme tamamlandığında tıklatın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="fd27f-135">When the format is complete, click **OK**.</span></span>

## <a name="use-trim-with-standard-storage"></a><span data-ttu-id="fd27f-136">Standart depolama ile kullanmak üzere KIRPMA</span><span class="sxs-lookup"><span data-stu-id="fd27f-136">Use TRIM with standard storage</span></span>

<span data-ttu-id="fd27f-137">Standart depolama (HDD) kullanırsanız, KIRPMA etkinleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="fd27f-137">If you use standard storage (HDD), you should enable TRIM.</span></span> <span data-ttu-id="fd27f-138">Yalnızca gerçekten kullandığınız depolama için faturalandırılır şekilde KIRPMA diskte kullanılmayan blokları atar.</span><span class="sxs-lookup"><span data-stu-id="fd27f-138">TRIM discards unused blocks on the disk so you are only billed for storage that you are actually using.</span></span> <span data-ttu-id="fd27f-139">Büyük dosyaları oluşturmak ve bunları silerseniz bu maliyetleri kaydedebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fd27f-139">This can save on costs if you create large files and then delete them.</span></span> 

<span data-ttu-id="fd27f-140">KIRPMA ayarını denetlemek için bu komutu çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fd27f-140">You can run this command to check the TRIM setting.</span></span> <span data-ttu-id="fd27f-141">Windows VM ve türü bir komut istemi açın:</span><span class="sxs-lookup"><span data-stu-id="fd27f-141">Open a command prompt on your Windows VM and type:</span></span>

```
fsutil behavior query DisableDeleteNotify
```

<span data-ttu-id="fd27f-142">Komut 0 döndürürse, KIRPMA doğru şekilde etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="fd27f-142">If the command returns 0, TRIM is enabled correctly.</span></span> <span data-ttu-id="fd27f-143">1 değeri döndürülürse, KIRPMA etkinleştirmek için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="fd27f-143">If it returns 1, run the following command to enable TRIM:</span></span>
```
fsutil behavior set DisableDeleteNotify 0
```

<span data-ttu-id="fd27f-144">Veri diskinizden sildikten sonra düzgün çalıştırarak temizleme KIRPMA işlemleri KIRPMA ile birleştirme sağlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="fd27f-144">After deleting data from your disk, you can ensure the TRIM operations flush properly by running defrag with TRIM:</span></span>

```
defrag.exe <volume:> -l
```

<span data-ttu-id="fd27f-145">Ayrıca, tüm birim birim biçimlendirme kırpılır emin olabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fd27f-145">You can also ensure the entire volume is trimmed by formatting the volume.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fd27f-146">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="fd27f-146">Next steps</span></span>
<span data-ttu-id="fd27f-147">Uygulama, D: kullanması gerekirse, verileri depolamak için sürücü, şunları yapabilirsiniz [Windows geçici disk sürücü harfini değiştirin](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fd27f-147">If you application needs to use the D: drive to store data, you can [change the drive letter of the Windows temporary disk](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>
