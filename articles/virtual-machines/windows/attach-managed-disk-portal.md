---
title: "aaaAttach bir yönetilen veri diski tooa Windows VM - Azure | Microsoft Docs"
description: "Veri diski tooa tooattach yeni yönetilen nasıl hello Azure portal kullanarak Windows VM Resource Manager dağıtım modeli hello."
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
ms.openlocfilehash: bacc0589ad2d93e4d3d055c8f837f8db27291ead
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooattach-a-managed-data-disk-tooa-windows-vm-in-hello-azure-portal"></a><span data-ttu-id="fbebb-103">Nasıl tooattach yönetilen bir veri diski hello Azure portal'ın Windows VM tooa</span><span class="sxs-lookup"><span data-stu-id="fbebb-103">How tooattach a managed data disk tooa Windows VM in hello Azure portal</span></span>

<span data-ttu-id="fbebb-104">Bu makale size nasıl tooattach yeni yönetilen bir veri diski hello Azure portal ile tooWindows sanal makineleri gösterir.</span><span class="sxs-lookup"><span data-stu-id="fbebb-104">This article shows you how tooattach a new managed data disk tooWindows virtual machines through hello Azure portal.</span></span> <span data-ttu-id="fbebb-105">Bunu önce bu ipuçlarını gözden geçirin:</span><span class="sxs-lookup"><span data-stu-id="fbebb-105">Before you do this, review these tips:</span></span>

* <span data-ttu-id="fbebb-106">Merhaba boyutunu hello sanal makine, iliştirebilirsiniz kaç tane veri diskleri denetler.</span><span class="sxs-lookup"><span data-stu-id="fbebb-106">hello size of hello virtual machine controls how many data disks you can attach.</span></span> <span data-ttu-id="fbebb-107">Ayrıntılar için bkz [sanal makineler için Boyutlar](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="fbebb-107">For details, see [Sizes for virtual machines](sizes.md).</span></span>
* <span data-ttu-id="fbebb-108">Yeni bir disk için toocreate gerekmez, ilk bunu eklediğinizde Azure bunu oluşturduğundan.</span><span class="sxs-lookup"><span data-stu-id="fbebb-108">For a new disk, you don't need toocreate it first because Azure creates it when you attach it.</span></span>

<span data-ttu-id="fbebb-109">Ayrıca [Powershell kullanarak bir veri diskini](attach-disk-ps.md).</span><span class="sxs-lookup"><span data-stu-id="fbebb-109">You can also [attach a data disk using Powershell](attach-disk-ps.md).</span></span>



## <a name="add-a-data-disk"></a><span data-ttu-id="fbebb-110">Bir veri diski Ekle</span><span class="sxs-lookup"><span data-stu-id="fbebb-110">Add a data disk</span></span>
1. <span data-ttu-id="fbebb-111">Merhaba soldaki Hello menüde tıklatın **sanal makineleri**.</span><span class="sxs-lookup"><span data-stu-id="fbebb-111">In hello menu on hello left, click **Virtual Machines**.</span></span>
2. <span data-ttu-id="fbebb-112">Merhaba sanal makine hello listeden seçin.</span><span class="sxs-lookup"><span data-stu-id="fbebb-112">Select hello virtual machine from hello list.</span></span>
3. <span data-ttu-id="fbebb-113">Merhaba sanal makine dikey penceresinde **diskleri**.</span><span class="sxs-lookup"><span data-stu-id="fbebb-113">On hello virtual machine blade, click **Disks**.</span></span>
   4. <span data-ttu-id="fbebb-114">Merhaba üzerinde **diskleri** dikey penceresinde tıklatın **+ Ekle veri diski**.</span><span class="sxs-lookup"><span data-stu-id="fbebb-114">On hello **Disks** blade, click **+ Add data disk**.</span></span>
5. <span data-ttu-id="fbebb-115">Hello açılan hello yeni disk için seçin **boş oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="fbebb-115">In hello drop-down for hello new disk, select **Create empty**.</span></span>
6. <span data-ttu-id="fbebb-116">Merhaba, **oluşturma yönetilen disk** dikey penceresinde hello disk için bir ad yazın ve Ayarla diğer ayarları gerektiği gibi hello.</span><span class="sxs-lookup"><span data-stu-id="fbebb-116">In hello **Create managed disk** blade, type in a name for hello disk and adjust hello other settings as necessary.</span></span> <span data-ttu-id="fbebb-117">İşiniz bittiğinde tıklatın **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="fbebb-117">When you are done, click **Create**.</span></span>
7. <span data-ttu-id="fbebb-118">Merhaba, **diskleri** dikey penceresinde, toosave hello hello VM için yeni disk yapılandırması Kaydet.</span><span class="sxs-lookup"><span data-stu-id="fbebb-118">In hello **Disks** blade, click save toosave hello new disk configuration for hello VM.</span></span>
6. <span data-ttu-id="fbebb-119">Azure hello disk oluşturur ve toohello sanal makineye iliştirir sonra hello yeni disk hello sanal makinenin disk ayarları altında listelenen **veri diskleri**.</span><span class="sxs-lookup"><span data-stu-id="fbebb-119">After Azure creates hello disk and attaches it toohello virtual machine, hello new disk is listed in hello virtual machine's disk settings under **Data Disks**.</span></span>


## <a name="initialize-a-new-data-disk"></a><span data-ttu-id="fbebb-120">Yeni bir veri diski başlatın</span><span class="sxs-lookup"><span data-stu-id="fbebb-120">Initialize a new data disk</span></span>

1. <span data-ttu-id="fbebb-121">Toohello VM bağlayın.</span><span class="sxs-lookup"><span data-stu-id="fbebb-121">Connect toohello VM.</span></span>
1. <span data-ttu-id="fbebb-122">Merhaba VM içinde Hello Başlat menüsünde ve türünü tıklatın **diskmgmt.msc** ve isabet **Enter**.</span><span class="sxs-lookup"><span data-stu-id="fbebb-122">Click hello start menu inside hello VM and type **diskmgmt.msc** and hit **Enter**.</span></span> <span data-ttu-id="fbebb-123">Bu, hello Disk Yönetimi ek bileşenini başlatır.</span><span class="sxs-lookup"><span data-stu-id="fbebb-123">This will start hello Disk Management snap-in.</span></span>
2. <span data-ttu-id="fbebb-124">Disk Yönetimi yeni ve başlatılmamış bir disk varsa ve hello diski başlatma penceresini kalkar algılar.</span><span class="sxs-lookup"><span data-stu-id="fbebb-124">Disk Management will recognize that you have a new, un-initialized disk and hello Initialize Disk window will pop up.</span></span>
3. <span data-ttu-id="fbebb-125">Merhaba yeni disk seçildiğinden emin olun ve tıklayın **Tamam** tooinitialize onu.</span><span class="sxs-lookup"><span data-stu-id="fbebb-125">Make sure hello new disk is selected and click **OK** tooinitialize it.</span></span>
4. <span data-ttu-id="fbebb-126">Merhaba yeni bir disk olarak artık görünür **ayrılmamış**.</span><span class="sxs-lookup"><span data-stu-id="fbebb-126">hello new disk will now appear as **unallocated**.</span></span> <span data-ttu-id="fbebb-127">Merhaba disk üzerinde herhangi bir yere sağ tıklatıp **yeni basit birim**.</span><span class="sxs-lookup"><span data-stu-id="fbebb-127">Right-click anywhere on hello disk and select **New simple volume**.</span></span> <span data-ttu-id="fbebb-128">Merhaba **Yeni Basit Birim Sihirbazı** başlar.</span><span class="sxs-lookup"><span data-stu-id="fbebb-128">hello **New Simple Volume Wizard** will start.</span></span>
5. <span data-ttu-id="fbebb-129">Seçim yapıldığında hello Varsayılanları tümünün tutma hello Sihirbazı aracılığıyla gidin **son**.</span><span class="sxs-lookup"><span data-stu-id="fbebb-129">Go through hello wizard, keeping all of hello defaults, when you are done select **Finish**.</span></span>
6. <span data-ttu-id="fbebb-130">Disk Yönetimi'ni kapatın.</span><span class="sxs-lookup"><span data-stu-id="fbebb-130">Close Disk Management.</span></span>
7. <span data-ttu-id="fbebb-131">Açılır pencere, alırsınız, kullanmadan önce tooformat hello yeni bir disk gerekir.</span><span class="sxs-lookup"><span data-stu-id="fbebb-131">You will get a pop-up that you need tooformat hello new disk before you can use it.</span></span> <span data-ttu-id="fbebb-132">Tıklatın **biçimi disk**.</span><span class="sxs-lookup"><span data-stu-id="fbebb-132">Click **Format disk**.</span></span>
8. <span data-ttu-id="fbebb-133">Merhaba, **biçimi yeni disk** iletişim, hello ayarlarını denetleyin ve ardından **Başlat**.</span><span class="sxs-lookup"><span data-stu-id="fbebb-133">In hello **Format new disk** dialog, check hello settings and then click **Start**.</span></span>
9. <span data-ttu-id="fbebb-134">Merhaba diskleri biçimlendirme hello verilerin tümünü siler, bir uyarı alırsınız tıklatın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="fbebb-134">You will get a warning that formatting hello disks will erase all of hello data, click **OK**.</span></span>
10. <span data-ttu-id="fbebb-135">Hello biçimi tamamlandığında tıklatın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="fbebb-135">When hello format is complete, click **OK**.</span></span>

## <a name="use-trim-with-standard-storage"></a><span data-ttu-id="fbebb-136">Standart depolama ile kullanmak üzere KIRPMA</span><span class="sxs-lookup"><span data-stu-id="fbebb-136">Use TRIM with standard storage</span></span>

<span data-ttu-id="fbebb-137">Standart depolama (HDD) kullanırsanız, KIRPMA etkinleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="fbebb-137">If you use standard storage (HDD), you should enable TRIM.</span></span> <span data-ttu-id="fbebb-138">Yalnızca gerçekten kullandığınız depolama için faturalandırılır şekilde KIRPMA hello diskte kullanılmayan blokları atar.</span><span class="sxs-lookup"><span data-stu-id="fbebb-138">TRIM discards unused blocks on hello disk so you are only billed for storage that you are actually using.</span></span> <span data-ttu-id="fbebb-139">Büyük dosyaları oluşturmak ve bunları silerseniz bu maliyetleri kaydedebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fbebb-139">This can save on costs if you create large files and then delete them.</span></span> 

<span data-ttu-id="fbebb-140">Bu komut toocheck hello KIRPMA ayarı çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fbebb-140">You can run this command toocheck hello TRIM setting.</span></span> <span data-ttu-id="fbebb-141">Windows VM ve türü bir komut istemi açın:</span><span class="sxs-lookup"><span data-stu-id="fbebb-141">Open a command prompt on your Windows VM and type:</span></span>

```
fsutil behavior query DisableDeleteNotify
```

<span data-ttu-id="fbebb-142">Merhaba komut 0 döndürürse, KIRPMA doğru şekilde etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="fbebb-142">If hello command returns 0, TRIM is enabled correctly.</span></span> <span data-ttu-id="fbebb-143">1 değeri döndürülürse, komut tooenable KIRPMA aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="fbebb-143">If it returns 1, run hello following command tooenable TRIM:</span></span>
```
fsutil behavior set DisableDeleteNotify 0
```

<span data-ttu-id="fbebb-144">Veri diskinizden sildikten sonra hello KIRPMA işlemleri düzgün çalıştırarak temizleme KIRPMA ile birleştirme sağlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="fbebb-144">After deleting data from your disk, you can ensure hello TRIM operations flush properly by running defrag with TRIM:</span></span>

```
defrag.exe <volume:> -l
```

<span data-ttu-id="fbebb-145">Ayrıca, birimin tamamını hello hello birim biçimlendirme kırpılır emin olabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fbebb-145">You can also ensure hello entire volume is trimmed by formatting hello volume.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fbebb-146">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="fbebb-146">Next steps</span></span>
<span data-ttu-id="fbebb-147">Uygulama, toouse hello D: sürücü toostore veri gerekiyorsa, yapabilecekleriniz [hello Windows geçici disk hello sürücü harfini değiştirin](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fbebb-147">If you application needs toouse hello D: drive toostore data, you can [change hello drive letter of hello Windows temporary disk](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>
