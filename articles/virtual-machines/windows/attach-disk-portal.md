---
title: "bir yönetilmeyen veri diski tooa Windows VM - Azure aaaAttach | Microsoft Docs"
description: "Nasıl tooattach yeni veya var olan yönetilmeyen veri diski tooa Windows VM Azure portal kullanarak hello Resource Manager dağıtım modeli hello."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3790fc59-7264-41df-b7a3-8d1226799885
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/09/2017
ms.author: cynthn
ms.openlocfilehash: 923a6663974143bf359970f9b0eb0d36cabcba9c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooattach-an-unmanaged-data-disk-tooa-windows-vm-in-hello-azure-portal"></a><span data-ttu-id="8b1c3-103">Nasıl tooattach yönetilmeyen bir veri diski hello Azure portal'ın Windows VM tooa</span><span class="sxs-lookup"><span data-stu-id="8b1c3-103">How tooattach an unmanaged data disk tooa Windows VM in hello Azure portal</span></span>

<span data-ttu-id="8b1c3-104">Bu makale size gösterir nasıl tooattach hem yeni hem de mevcut yönetilmeyen hello Azure portal aracılığıyla tooWindows sanal makineler diskler.</span><span class="sxs-lookup"><span data-stu-id="8b1c3-104">This article shows you how tooattach both new and existing unmanaged disks tooWindows virtual machines through hello Azure portal.</span></span> <span data-ttu-id="8b1c3-105">Ayrıca [PowerShell kullanarak bir veri diskini](./attach-disk-ps.md).</span><span class="sxs-lookup"><span data-stu-id="8b1c3-105">You can also [attach a data disk using PowerShell](./attach-disk-ps.md).</span></span> <span data-ttu-id="8b1c3-106">Bunu önce bu ipuçlarını gözden geçirin:</span><span class="sxs-lookup"><span data-stu-id="8b1c3-106">Before you do this, review these tips:</span></span>

* <span data-ttu-id="8b1c3-107">Merhaba boyutunu hello sanal makine, iliştirebilirsiniz kaç tane veri diskleri denetler.</span><span class="sxs-lookup"><span data-stu-id="8b1c3-107">hello size of hello virtual machine controls how many data disks you can attach.</span></span> <span data-ttu-id="8b1c3-108">Ayrıntılar için bkz [sanal makineler için Boyutlar](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="8b1c3-108">For details, see [Sizes for virtual machines](sizes.md).</span></span>
* <span data-ttu-id="8b1c3-109">Premium depolama toouse, DS serisi veya GS serisi bir sanal makine gerekir.</span><span class="sxs-lookup"><span data-stu-id="8b1c3-109">toouse Premium storage, you need a DS-series or GS-series virtual machine.</span></span> <span data-ttu-id="8b1c3-110">Bu sanal makinelerle Premium ve standart depolama hesapları arasından diskleri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8b1c3-110">You can use disks from both Premium and Standard storage accounts with these virtual machines.</span></span> <span data-ttu-id="8b1c3-111">Premium depolama belirli bölgelerde kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="8b1c3-111">Premium storage is available in certain regions.</span></span> <span data-ttu-id="8b1c3-112">Ayrıntılar için bkz [Premium Storage: Azure sanal makine iş yükleri için yüksek performanslı depolama](../../storage/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8b1c3-112">For details, see [Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads](../../storage/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="8b1c3-113">Yeni bir disk için toocreate gerekmez, ilk bunu eklediğinizde Azure bunu oluşturduğundan.</span><span class="sxs-lookup"><span data-stu-id="8b1c3-113">For a new disk, you don't need toocreate it first because Azure creates it when you attach it.</span></span>


<span data-ttu-id="8b1c3-114">Ayrıca [Powershell kullanarak bir veri diskini](attach-disk-ps.md).</span><span class="sxs-lookup"><span data-stu-id="8b1c3-114">You can also [attach a data disk using Powershell](attach-disk-ps.md).</span></span>


## <a name="find-hello-virtual-machine"></a><span data-ttu-id="8b1c3-115">Merhaba sanal makine bulunamadı</span><span class="sxs-lookup"><span data-stu-id="8b1c3-115">Find hello virtual machine</span></span>
1. <span data-ttu-id="8b1c3-116">İçinde toohello oturum [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="8b1c3-116">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="8b1c3-117">Merhaba soldaki Hello menüde tıklatın **sanal makineleri**.</span><span class="sxs-lookup"><span data-stu-id="8b1c3-117">In hello menu on hello left, click **Virtual Machines**.</span></span>
3. <span data-ttu-id="8b1c3-118">Merhaba sanal makine hello listeden seçin.</span><span class="sxs-lookup"><span data-stu-id="8b1c3-118">Select hello virtual machine from hello list.</span></span>
4. <span data-ttu-id="8b1c3-119">Merhaba sanal makineleri dikey penceresinde tıklayın **diskleri**.</span><span class="sxs-lookup"><span data-stu-id="8b1c3-119">In hello Virtual machines blade, click **Disks**.</span></span>
   
<span data-ttu-id="8b1c3-120">Ya da eklemek için aşağıdaki yönergeleri tarafından devam bir [yeni disk](#option-1-attach-a-new-disk) veya bir [mevcut disk](#option-2-attach-an-existing-disk).</span><span class="sxs-lookup"><span data-stu-id="8b1c3-120">Continue by following instructions for attaching either a [new disk](#option-1-attach-a-new-disk) or an [existing disk](#option-2-attach-an-existing-disk).</span></span>

## <a name="option-1-attach-and-initialize-a-new-disk"></a><span data-ttu-id="8b1c3-121">Seçenek 1: Eklemek ve yeni bir disk başlatma</span><span class="sxs-lookup"><span data-stu-id="8b1c3-121">Option 1: Attach and initialize a new disk</span></span>
1. <span data-ttu-id="8b1c3-122">Merhaba üzerinde **diskleri** dikey penceresinde tıklatın **+ Ekle veri diski**.</span><span class="sxs-lookup"><span data-stu-id="8b1c3-122">On hello **Disks** blade, click **+ Add data disk**.</span></span>
2. <span data-ttu-id="8b1c3-123">Merhaba, **Attach yönetilen disk** dikey penceresinde hello disk için bir ad yazın **adı** ve ardından **yeni (boş disk)** içinde **kaynak türünü**.</span><span class="sxs-lookup"><span data-stu-id="8b1c3-123">In hello **Attach managed disk** blade, type a name for hello disk in **Name** and then select **New (empty disk)** in **Source type**.</span></span>
3. <span data-ttu-id="8b1c3-124">Altında **depolama kapsayıcısı**, hello tıklatın **Gözat** düğmesine tıklayın ve toohello depolama hesabı ve burada depolanan hello yeni VHD toobe ister ve ardından kapsayıcı Gözat **seçin**.</span><span class="sxs-lookup"><span data-stu-id="8b1c3-124">Under **Storage container**, click hello **Browse** button and browse toohello storage account and container where you would like hello new VHD toobe stored and then click **Select**.</span></span> 
  
   ![Disk ayarlarını gözden geçirin](./media/attach-disk-portal/attach-empty-unmanaged.png)
   
3. <span data-ttu-id="8b1c3-126">Merhaba veri diski hello ayarları ile işiniz bittiğinde tıklatın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="8b1c3-126">When you are done with hello settings for hello data disk, click **OK**.</span></span>
4. <span data-ttu-id="8b1c3-127">Merhaba edilene **diskleri** dikey penceresinde tıklatın **kaydetmek** tooadd hello disk toohello VM yapılandırması.</span><span class="sxs-lookup"><span data-stu-id="8b1c3-127">Back in hello **Disks** blade, click **Save** tooadd hello disk toohello VM configuration.</span></span>


### <a name="initialize-a-new-data-disk"></a><span data-ttu-id="8b1c3-128">Yeni bir veri diski başlatın</span><span class="sxs-lookup"><span data-stu-id="8b1c3-128">Initialize a new data disk</span></span>

1. <span data-ttu-id="8b1c3-129">Toohello sanal makineye bağlanın.</span><span class="sxs-lookup"><span data-stu-id="8b1c3-129">Connect toohello virtual machine.</span></span> <span data-ttu-id="8b1c3-130">Yönergeler için bkz: [nasıl Windows çalıştıran tooconnect ve oturum açma tooan Azure sanal makine](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8b1c3-130">For instructions, see [How tooconnect and log on tooan Azure virtual machine running Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
1. <span data-ttu-id="8b1c3-131">Merhaba tıklatın **Başlat** menüsünün hello VM ve türü içinde **diskmgmt.msc** ve isabet **Enter**.</span><span class="sxs-lookup"><span data-stu-id="8b1c3-131">Click hello **Start** menu inside hello VM and type **diskmgmt.msc** and hit **Enter**.</span></span> <span data-ttu-id="8b1c3-132">Bu, hello Disk Yönetimi ek bileşenini başlatır.</span><span class="sxs-lookup"><span data-stu-id="8b1c3-132">This starts hello Disk Management snap-in.</span></span>
2. <span data-ttu-id="8b1c3-133">Disk Yönetimi yeni ve başlatılmamış bir disk varsa ve hello diski başlatma penceresini kalkar tanır.</span><span class="sxs-lookup"><span data-stu-id="8b1c3-133">Disk Management recognizes that you have a new, uninitialized disk and hello Initialize Disk window will pop up.</span></span>
3. <span data-ttu-id="8b1c3-134">Merhaba yeni disk seçildiğinden emin olun ve tıklayın **Tamam** tooinitialize onu.</span><span class="sxs-lookup"><span data-stu-id="8b1c3-134">Make sure hello new disk is selected and click **OK** tooinitialize it.</span></span>
4. <span data-ttu-id="8b1c3-135">Merhaba yeni disk şimdi olarak görünür **ayrılmamış**.</span><span class="sxs-lookup"><span data-stu-id="8b1c3-135">hello new disk now appears as **unallocated**.</span></span> <span data-ttu-id="8b1c3-136">Merhaba disk üzerinde herhangi bir yere sağ tıklatıp **yeni basit birim**.</span><span class="sxs-lookup"><span data-stu-id="8b1c3-136">Right-click anywhere on hello disk and select **New simple volume**.</span></span> <span data-ttu-id="8b1c3-137">Merhaba **Yeni Basit Birim Sihirbazı** başlatır.</span><span class="sxs-lookup"><span data-stu-id="8b1c3-137">hello **New Simple Volume Wizard** starts.</span></span>
5. <span data-ttu-id="8b1c3-138">Seçim yapıldığında hello Varsayılanları tümünün tutma hello Sihirbazı aracılığıyla gidin **son**.</span><span class="sxs-lookup"><span data-stu-id="8b1c3-138">Go through hello wizard, keeping all of hello defaults, when you are done select **Finish**.</span></span>
6. <span data-ttu-id="8b1c3-139">Disk Yönetimi'ni kapatın.</span><span class="sxs-lookup"><span data-stu-id="8b1c3-139">Close Disk Management.</span></span>
7. <span data-ttu-id="8b1c3-140">Açılır pencere alma kullanabilmeniz için önce tooformat hello yeni bir disk gerekir.</span><span class="sxs-lookup"><span data-stu-id="8b1c3-140">You get a pop-up that you need tooformat hello new disk before you can use it.</span></span> <span data-ttu-id="8b1c3-141">Tıklatın **biçimi disk**.</span><span class="sxs-lookup"><span data-stu-id="8b1c3-141">Click **Format disk**.</span></span>
8. <span data-ttu-id="8b1c3-142">Merhaba, **biçimi yeni disk** iletişim, hello ayarlarını denetleyin ve ardından **Başlat**.</span><span class="sxs-lookup"><span data-stu-id="8b1c3-142">In hello **Format new disk** dialog, check hello settings and then click **Start**.</span></span>
9. <span data-ttu-id="8b1c3-143">Merhaba diskleri biçimlendirme hello verilerin tümünü siler, bir uyarı almak, tıklatın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="8b1c3-143">You get a warning that formatting hello disks erases all of hello data, click **OK**.</span></span>
10. <span data-ttu-id="8b1c3-144">Hello biçimi tamamlandığında tıklatın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="8b1c3-144">When hello format is complete, click **OK**.</span></span>


## <a name="option-2-attach-an-existing-disk"></a><span data-ttu-id="8b1c3-145">Seçenek 2: var olan bir diski kullanıma açın</span><span class="sxs-lookup"><span data-stu-id="8b1c3-145">Option 2: Attach an existing disk</span></span>
1. <span data-ttu-id="8b1c3-146">Merhaba üzerinde **diskleri** dikey penceresinde tıklatın **+ Ekle veri diski**.</span><span class="sxs-lookup"><span data-stu-id="8b1c3-146">On hello **Disks** blade, click **+ Add data disk**.</span></span>
2. <span data-ttu-id="8b1c3-147">Merhaba üzerinde **Attach yönetilmeyen disk** dikey penceresinde, **kaynak türünü** seçin **varolan blob**.</span><span class="sxs-lookup"><span data-stu-id="8b1c3-147">On hello **Attach unmanaged disk** blade, in **Source type** select **Existing blob**.</span></span>

    ![Disk ayarlarını gözden geçirin](./media/attach-disk-portal/attach-existing-unmanaged.png)

    3. <span data-ttu-id="8b1c3-149">Tıklatın **Gözat** toonavigate toohello depolama hesabı ve kapsayıcı hello varolan bir VHD'yi bulunduğu.</span><span class="sxs-lookup"><span data-stu-id="8b1c3-149">Click **Browse** toonavigate toohello storage account and container where hello existing VHD is located.</span></span> <span data-ttu-id="8b1c3-150">Tıklayın ve VHD hello ve ardından **seçin**.</span><span class="sxs-lookup"><span data-stu-id="8b1c3-150">Click and hello VHD and then click **Select**.</span></span>
4. <span data-ttu-id="8b1c3-151">Tıklatın **Tamam** hello içinde **Attach yönetilmeyen disk** dikey.</span><span class="sxs-lookup"><span data-stu-id="8b1c3-151">Click **OK** in hello **Attach unmanaged disk** blade.</span></span>
5. <span data-ttu-id="8b1c3-152">Merhaba, **diskleri** dikey penceresinde tıklatın **kaydetmek** hello VM için tooadd hello disk toohello yapılandırması.</span><span class="sxs-lookup"><span data-stu-id="8b1c3-152">In hello **Disks** blade, click **Save** tooadd hello disk toohello configuration for hello VM.</span></span>
   


## <a name="use-trim-with-standard-storage"></a><span data-ttu-id="8b1c3-153">Standart depolama ile kullanmak üzere KIRPMA</span><span class="sxs-lookup"><span data-stu-id="8b1c3-153">Use TRIM with standard storage</span></span>

<span data-ttu-id="8b1c3-154">Standart depolama (HDD) kullanırsanız, KIRPMA etkinleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="8b1c3-154">If you use standard storage (HDD), you should enable TRIM.</span></span> <span data-ttu-id="8b1c3-155">Yalnızca gerçekten kullandığınız depolama için faturalandırılır şekilde KIRPMA hello diskte kullanılmayan blokları atar.</span><span class="sxs-lookup"><span data-stu-id="8b1c3-155">TRIM discards unused blocks on hello disk so you are only billed for storage that you are actually using.</span></span> <span data-ttu-id="8b1c3-156">Büyük dosyaları oluşturmak ve bunları silerseniz bu maliyetleri kaydedebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8b1c3-156">This can save on costs if you create large files and then delete them.</span></span> 

<span data-ttu-id="8b1c3-157">Bu komut toocheck hello KIRPMA ayarı çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8b1c3-157">You can run this command toocheck hello TRIM setting.</span></span> <span data-ttu-id="8b1c3-158">Windows VM ve türü bir komut istemi açın:</span><span class="sxs-lookup"><span data-stu-id="8b1c3-158">Open a command prompt on your Windows VM and type:</span></span>

```
fsutil behavior query DisableDeleteNotify
```

<span data-ttu-id="8b1c3-159">Merhaba komut 0 döndürürse, KIRPMA doğru şekilde etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="8b1c3-159">If hello command returns 0, TRIM is enabled correctly.</span></span> <span data-ttu-id="8b1c3-160">1 değeri döndürülürse, komut tooenable KIRPMA aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="8b1c3-160">If it returns 1, run hello following command tooenable TRIM:</span></span>
```
fsutil behavior set DisableDeleteNotify 0
```

<span data-ttu-id="8b1c3-161">Veri diskinizden sildikten sonra hello KIRPMA işlemleri düzgün çalıştırarak temizleme KIRPMA ile birleştirme sağlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="8b1c3-161">After deleting data from your disk, you can ensure hello TRIM operations flush properly by running defrag with TRIM:</span></span>

```
defrag.exe <volume:> -l
```

<span data-ttu-id="8b1c3-162">Ayrıca, birimin tamamını hello hello birim biçimlendirme kırpılır emin olabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8b1c3-162">You can also ensure hello entire volume is trimmed by formatting hello volume.</span></span>


## <a name="next-steps"></a><span data-ttu-id="8b1c3-163">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8b1c3-163">Next steps</span></span>
<span data-ttu-id="8b1c3-164">Uygulama, toouse hello D: sürücü toostore veri gerekiyorsa, yapabilecekleriniz [hello Windows geçici disk hello sürücü harfini değiştirin](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8b1c3-164">If you application needs toouse hello D: drive toostore data, you can [change hello drive letter of hello Windows temporary disk](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

