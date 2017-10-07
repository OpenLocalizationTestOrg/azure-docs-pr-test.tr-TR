---
title: aaaAttach disk tooa Klasik Azure VM | Microsoft Docs
description: "Bir veri diski tooa Windows hello Klasik dağıtım modeliyle oluşturulan sanal makinenin ekleyin ve onu başlatın."
services: virtual-machines-windows, storage
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: be4e3e74-05bc-4527-969f-84f10a1d66a7
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 02/21/2017
ms.author: cynthn
ms.openlocfilehash: bfe1b0fa066277d28d3862a18da4b1023cb4452d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="attach-a-data-disk-tooa-windows-virtual-machine-created-with-hello-classic-deployment-model"></a><span data-ttu-id="32385-103">Bir veri diski tooa Windows hello Klasik dağıtım modeliyle oluşturulan sanal makinenin ekleme</span><span class="sxs-lookup"><span data-stu-id="32385-103">Attach a data disk tooa Windows virtual machine created with hello classic deployment model</span></span>
<!--
Refernce article:
    If you want toouse hello new portal, see [How tooattach a data disk tooa Windows VM in hello Azure portal](../../virtual-machines-windows-attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
-->

<span data-ttu-id="32385-104">Bu makalede tooattach yeni ve mevcut diskleri hello Klasik dağıtım modeli tooa Windows hello kullanarak sanal makine ile Azure portalına nasıl oluşturulacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="32385-104">This article shows you how tooattach new and existing disks created with hello Classic deployment model tooa Windows virtual machine using hello Azure portal.</span></span>

<span data-ttu-id="32385-105">Ayrıca [hello Azure portal'ın bir veri diski tooa Linux VM ekleme](../../linux/attach-disk-portal.md).</span><span class="sxs-lookup"><span data-stu-id="32385-105">You can also [attach a data disk tooa Linux VM in hello Azure portal](../../linux/attach-disk-portal.md).</span></span>

<span data-ttu-id="32385-106">Bir disk eklemeden önce bu ipuçlarını gözden geçirin:</span><span class="sxs-lookup"><span data-stu-id="32385-106">Before you attach a disk, review these tips:</span></span>

* <span data-ttu-id="32385-107">Merhaba boyutunu hello sanal makine, iliştirebilirsiniz kaç tane veri diskleri denetler.</span><span class="sxs-lookup"><span data-stu-id="32385-107">hello size of hello virtual machine controls how many data disks you can attach.</span></span> <span data-ttu-id="32385-108">Ayrıntılar için bkz [sanal makineler için Boyutlar](../../virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="32385-108">For details, see [Sizes for virtual machines](../../virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

* <span data-ttu-id="32385-109">Premium depolama toouse, DS serisi veya GS serisi bir sanal makine gerekir.</span><span class="sxs-lookup"><span data-stu-id="32385-109">toouse Premium storage, you need a DS-series or GS-series virtual machine.</span></span> <span data-ttu-id="32385-110">Bu sanal makinelerle Premium ve standart depolama hesapları arasından diskleri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="32385-110">You can use disks from both Premium and Standard storage accounts with these virtual machines.</span></span> <span data-ttu-id="32385-111">Premium depolama belirli bölgelerde kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="32385-111">Premium storage is available in certain regions.</span></span> <span data-ttu-id="32385-112">Ayrıntılar için bkz [Premium Storage: Azure sanal makine iş yükleri için yüksek performanslı depolama](../../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="32385-112">For details, see [Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads](../../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

* <span data-ttu-id="32385-113">Yeni bir disk için toocreate gerekmez, ilk bunu eklediğinizde Azure bunu oluşturduğundan.</span><span class="sxs-lookup"><span data-stu-id="32385-113">For a new disk, you don't need toocreate it first because Azure creates it when you attach it.</span></span>

<span data-ttu-id="32385-114">Ayrıca [Powershell kullanarak bir veri diskini](../../virtual-machines-windows-attach-disk-ps.md).</span><span class="sxs-lookup"><span data-stu-id="32385-114">You can also [attach a data disk using Powershell](../../virtual-machines-windows-attach-disk-ps.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="32385-115">Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="32385-115">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span>

## <a name="find-hello-virtual-machine"></a><span data-ttu-id="32385-116">Merhaba sanal makine bulunamadı</span><span class="sxs-lookup"><span data-stu-id="32385-116">Find hello virtual machine</span></span>
1. <span data-ttu-id="32385-117">İçinde toohello oturum [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="32385-117">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="32385-118">Sanal makineden hello Panoda listelenen hello Kaynak Seç hello.</span><span class="sxs-lookup"><span data-stu-id="32385-118">Select hello virtual machine from hello resource listed on hello dashboard.</span></span>
3. <span data-ttu-id="32385-119">Merhaba sol bölmede altında **ayarları**, tıklatın **diskleri**.</span><span class="sxs-lookup"><span data-stu-id="32385-119">In hello left pane under **Settings**, click **Disks**.</span></span>

    ![Disk Ayarları'nı açın](./media/attach-disk/virtualmachinedisks.png)

<span data-ttu-id="32385-121">Ya da eklemek için aşağıdaki yönergeleri tarafından devam bir [yeni disk](#option-1-attach-a-new-disk) veya bir [mevcut disk](#option-2-attach-an-existing-disk).</span><span class="sxs-lookup"><span data-stu-id="32385-121">Continue by following instructions for attaching either a [new disk](#option-1-attach-a-new-disk) or an [existing disk](#option-2-attach-an-existing-disk).</span></span>

## <a name="option-1-attach-and-initialize-a-new-disk"></a><span data-ttu-id="32385-122">Seçenek 1: Eklemek ve yeni bir disk başlatma</span><span class="sxs-lookup"><span data-stu-id="32385-122">Option 1: Attach and initialize a new disk</span></span>

1. <span data-ttu-id="32385-123">Merhaba üzerinde **diskleri** dikey penceresinde tıklatın **Attach yeni**.</span><span class="sxs-lookup"><span data-stu-id="32385-123">On hello **Disks** blade, click **Attach new**.</span></span>
2. <span data-ttu-id="32385-124">Merhaba varsayılan ayarları gözden geçirin, gerektiği gibi güncelleştirin ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="32385-124">Review hello default settings, update as necessary, and then click **OK**.</span></span>

   ![Disk ayarlarını gözden geçirin](./media/attach-disk/attach-new.png)

3. <span data-ttu-id="32385-126">Azure hello disk oluşturur ve toohello sanal makineye iliştirir sonra hello yeni disk hello sanal makinenin disk ayarları altında listelenen **veri diskleri**.</span><span class="sxs-lookup"><span data-stu-id="32385-126">After Azure creates hello disk and attaches it toohello virtual machine, hello new disk is listed in hello virtual machine's disk settings under **Data Disks**.</span></span>

### <a name="initialize-a-new-data-disk"></a><span data-ttu-id="32385-127">Yeni bir veri diski başlatın</span><span class="sxs-lookup"><span data-stu-id="32385-127">Initialize a new data disk</span></span>

1. <span data-ttu-id="32385-128">Toohello sanal makineye bağlanın.</span><span class="sxs-lookup"><span data-stu-id="32385-128">Connect toohello virtual machine.</span></span> <span data-ttu-id="32385-129">Yönergeler için bkz: [nasıl Windows çalıştıran tooconnect ve oturum açma tooan Azure sanal makine](../../virtual-machines-windows-connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="32385-129">For instructions, see [How tooconnect and log on tooan Azure virtual machine running Windows](../../virtual-machines-windows-connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
2. <span data-ttu-id="32385-130">Toohello sanal makinede oturum sonra açmak **Sunucu Yöneticisi'ni**.</span><span class="sxs-lookup"><span data-stu-id="32385-130">After you log on toohello virtual machine, open **Server Manager**.</span></span> <span data-ttu-id="32385-131">Merhaba sol bölmesinde seçin **dosya ve depolama hizmetleri**.</span><span class="sxs-lookup"><span data-stu-id="32385-131">In hello left pane, select **File and Storage Services**.</span></span>

    ![Sunucu Yöneticisi'ni açma](../media/attach-disk-portal/fileandstorageservices.png)

3. <span data-ttu-id="32385-133">Seçin **diskleri**.</span><span class="sxs-lookup"><span data-stu-id="32385-133">Select **Disks**.</span></span>
4. <span data-ttu-id="32385-134">Merhaba **diskleri** bölümü hello diskleri listeler.</span><span class="sxs-lookup"><span data-stu-id="32385-134">hello **Disks** section lists hello disks.</span></span> <span data-ttu-id="32385-135">Genellikle, bir sanal makine disk 0, 1 disk ve disk 2 ' var.</span><span class="sxs-lookup"><span data-stu-id="32385-135">Most often, a virtual machine has disk 0, disk 1, and disk 2.</span></span> <span data-ttu-id="32385-136">Disk 0 hello işletim sistemi diski, disk 1 hello geçici diski olduğundan ve disk 2 hello veri diski yeni toohello sanal makineye bağlı.</span><span class="sxs-lookup"><span data-stu-id="32385-136">Disk 0 is hello operating system disk, disk 1 is hello temporary disk, and disk 2 is hello data disk newly attached toohello virtual machine.</span></span> <span data-ttu-id="32385-137">Merhaba veri diski listeleri hello bölümü olarak **bilinmeyen**.</span><span class="sxs-lookup"><span data-stu-id="32385-137">hello data disk lists hello Partition as **Unknown**.</span></span>

 <span data-ttu-id="32385-138">Başlangıç diski sağ tıklatın ve seçin **başlatma**.</span><span class="sxs-lookup"><span data-stu-id="32385-138">Right-click hello disk and select **Initialize**.</span></span>

5. <span data-ttu-id="32385-139">Merhaba disk başlatıldığında tüm veriler silinecek bildirim.</span><span class="sxs-lookup"><span data-stu-id="32385-139">You're notified that all data will be erased when hello disk is initialized.</span></span> <span data-ttu-id="32385-140">Tıklatın **Evet** tooacknowledge hello uyarı ve başlatma hello disk.</span><span class="sxs-lookup"><span data-stu-id="32385-140">Click **Yes** tooacknowledge hello warning and initialize hello disk.</span></span> <span data-ttu-id="32385-141">Tamamlandıktan sonra hello bölüm olarak listelenmez. **GPT**.</span><span class="sxs-lookup"><span data-stu-id="32385-141">Once complete, hello partition will be listed as **GPT**.</span></span> <span data-ttu-id="32385-142">Başlangıç diski yeniden sağ tıklatın ve seçin **yeni birim**.</span><span class="sxs-lookup"><span data-stu-id="32385-142">Right-click hello disk again and select **New Volume**.</span></span>

6. <span data-ttu-id="32385-143">Merhaba varsayılan değerleri kullanarak hello Sihirbazı tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="32385-143">Complete hello wizard using hello default values.</span></span> <span data-ttu-id="32385-144">Merhaba Sihirbazı tamamlandığında, hello **birimleri** bölümü hello yeni birim listeler.</span><span class="sxs-lookup"><span data-stu-id="32385-144">When hello wizard is done, hello **Volumes** section lists hello new volume.</span></span> <span data-ttu-id="32385-145">Merhaba disk artık çevrimiçi olduğunu ve hazır toostore verilerdir.</span><span class="sxs-lookup"><span data-stu-id="32385-145">hello disk is now online and ready toostore data.</span></span>

    ![Birimi başarıyla başlatıldı](./media/attach-disk/newdiskafterinitialization.png)

## <a name="option-2-attach-an-existing-disk"></a><span data-ttu-id="32385-147">Seçenek 2: var olan bir diski kullanıma açın</span><span class="sxs-lookup"><span data-stu-id="32385-147">Option 2: Attach an existing disk</span></span>
1. <span data-ttu-id="32385-148">Merhaba üzerinde **diskleri** dikey penceresinde tıklatın **Attach varolan**.</span><span class="sxs-lookup"><span data-stu-id="32385-148">On hello **Disks** blade, click **Attach existing**.</span></span>
2. <span data-ttu-id="32385-149">Altında **varolan bir diski İlişti**, tıklatın **konumu**.</span><span class="sxs-lookup"><span data-stu-id="32385-149">Under **Attach existing disk**, click **Location**.</span></span>

   ![Varolan bir diski kullanıma açın](./media/attach-disk/attachexistingdisksettings.png)
3. <span data-ttu-id="32385-151">Altında **depolama hesapları**, hello hesabınızı ve hello .vhd dosyası tutan kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="32385-151">Under **Storage accounts**, select hello account and container that holds hello .vhd file.</span></span>

   ![VHD konumunu bulma](./media/attach-disk/existdiskstorageaccountandcontainer.png)

4. <span data-ttu-id="32385-153">Merhaba .vhd dosyasını seçin.</span><span class="sxs-lookup"><span data-stu-id="32385-153">Select hello .vhd file.</span></span>
5. <span data-ttu-id="32385-154">Altında **varolan bir diski İlişti**, seçtiğiniz hello dosya altında listelenen **VHD dosyasını**.</span><span class="sxs-lookup"><span data-stu-id="32385-154">Under **Attach existing disk**, hello file you just selected is listed under **VHD File**.</span></span> <span data-ttu-id="32385-155">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="32385-155">Click **OK**.</span></span>
6. <span data-ttu-id="32385-156">Disk toohello sanal makine Azure ekler hello sonra hello sanal makinenin disk ayarları altında listelenen **veri diskleri**.</span><span class="sxs-lookup"><span data-stu-id="32385-156">After Azure attaches hello disk toohello virtual machine, it's listed in hello virtual machine's disk settings under **Data Disks**.</span></span>

## <a name="use-trim-with-standard-storage"></a><span data-ttu-id="32385-157">Standart depolama ile kullanmak üzere KIRPMA</span><span class="sxs-lookup"><span data-stu-id="32385-157">Use TRIM with standard storage</span></span>

<span data-ttu-id="32385-158">Standart depolama (HDD) kullanırsanız, KIRPMA etkinleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="32385-158">If you use standard storage (HDD), you should enable TRIM.</span></span> <span data-ttu-id="32385-159">Yalnızca gerçekten kullandığınız depolama için faturalandırılır şekilde KIRPMA hello diskte kullanılmayan blokları atar.</span><span class="sxs-lookup"><span data-stu-id="32385-159">TRIM discards unused blocks on hello disk so you are only billed for storage that you are actually using.</span></span> <span data-ttu-id="32385-160">KIRPMA kullanarak büyük dosyaların silinmesi neden kullanılmayan blokları dahil, maliyetleri kaydedebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="32385-160">Using TRIM can save costs, including unused blocks that result from deleting large files.</span></span>

<span data-ttu-id="32385-161">Bu komut toocheck hello KIRPMA ayarı çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="32385-161">You can run this command toocheck hello TRIM setting.</span></span> <span data-ttu-id="32385-162">Windows VM ve türü bir komut istemi açın:</span><span class="sxs-lookup"><span data-stu-id="32385-162">Open a command prompt on your Windows VM and type:</span></span>

```
fsutil behavior query DisableDeleteNotify
```

<span data-ttu-id="32385-163">Merhaba komut 0 döndürürse, KIRPMA doğru şekilde etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="32385-163">If hello command returns 0, TRIM is enabled correctly.</span></span> <span data-ttu-id="32385-164">1 değeri döndürülürse, komut tooenable KIRPMA aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="32385-164">If it returns 1, run hello following command tooenable TRIM:</span></span>
```
fsutil behavior set DisableDeleteNotify 0
```

## <a name="next-steps"></a><span data-ttu-id="32385-165">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="32385-165">Next steps</span></span>
<span data-ttu-id="32385-166">Uygulamanızı toouse hello D: sürücü toostore veri gerekiyorsa, yapabilecekleriniz [hello Windows geçici disk hello sürücü harfini değiştirin](../../virtual-machines-windows-change-drive-letter.md).</span><span class="sxs-lookup"><span data-stu-id="32385-166">If your application needs toouse hello D: drive toostore data, you can [change hello drive letter of hello Windows temporary disk](../../virtual-machines-windows-change-drive-letter.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="32385-167">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="32385-167">Additional resources</span></span>
[<span data-ttu-id="32385-168">Diskleri ve sanal makineler için VHD'ler hakkında</span><span class="sxs-lookup"><span data-stu-id="32385-168">About disks and VHDs for virtual machines</span></span>](../../virtual-machines-linux-about-disks-vhds.md)
