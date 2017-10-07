---
title: "VM bir veri diski D: sürücü hello olun | Microsoft Docs"
description: "Bir veri sürücüsü olarak hello D: sürücü kullanabilmesi için bir Windows VM nasıl toochange sürücü harfleri açıklar."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 0867a931-0055-4e31-8403-9b38a3eeb904
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/31/2017
ms.author: cynthn
ms.openlocfilehash: 43939da1a890ac4049266487951e3889aa0ed9d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-d-drive-as-a-data-drive-on-a-windows-vm"></a><span data-ttu-id="ff5f6-103">Bir Windows VM üzerinde bir veri sürücüsü olarak Hello D: sürücü kullanın</span><span class="sxs-lookup"><span data-stu-id="ff5f6-103">Use hello D: drive as a data drive on a Windows VM</span></span>
<span data-ttu-id="ff5f6-104">Uygulamanızı toouse hello D sürücü toostore veri gerekiyorsa, bu yönergeler toouse hello geçici disk için farklı bir sürücü harfi izleyin.</span><span class="sxs-lookup"><span data-stu-id="ff5f6-104">If your application needs toouse hello D drive toostore data, follow these instructions toouse a different drive letter for hello temporary disk.</span></span> <span data-ttu-id="ff5f6-105">Hiçbir zaman tookeep gereksinim hello geçici disk toostore verileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="ff5f6-105">Never use hello temporary disk toostore data that you need tookeep.</span></span>

<span data-ttu-id="ff5f6-106">Yeniden boyutlandırma varsa veya **Dur (Deallocate)** bir sanal makine, bu hello sanal makine tooa yeni hiper yerleşimini tetikleyebilir.</span><span class="sxs-lookup"><span data-stu-id="ff5f6-106">If you resize or **Stop (Deallocate)** a virtual machine, this may trigger placement of hello virtual machine tooa new hypervisor.</span></span> <span data-ttu-id="ff5f6-107">Bir planlı veya plansız bir bakım olayı de bu yerleştirme tetikleyebilir.</span><span class="sxs-lookup"><span data-stu-id="ff5f6-107">A planned or unplanned maintenance event may also trigger this placement.</span></span> <span data-ttu-id="ff5f6-108">Bu senaryoda, hello geçici disk yeniden atanan toohello ilk kullanılabilir sürücü harfini olacaktır.</span><span class="sxs-lookup"><span data-stu-id="ff5f6-108">In this scenario, hello temporary disk will be reassigned toohello first available drive letter.</span></span> <span data-ttu-id="ff5f6-109">Özellikle hello D: sürücü gerektiren bir uygulama varsa, bu yeni bir veri diski ekleyin ve hello Harf D atamak adımları tootemporarily taşıma hello pagefile.sys ve ardından toohello geçici sürücü geri taşıma hello pagefile.sys toofollow gerekir.</span><span class="sxs-lookup"><span data-stu-id="ff5f6-109">If you have an application that specifically requires hello D: drive, you need toofollow these steps tootemporarily move hello pagefile.sys, attach a new data disk and assign it hello letter D and then move hello pagefile.sys back toohello temporary drive.</span></span> <span data-ttu-id="ff5f6-110">Merhaba VM tooa farklı hiper yönetici taşınırsa tamamlandıktan sonra Azure geri hello D: olmayacaktır.</span><span class="sxs-lookup"><span data-stu-id="ff5f6-110">Once complete, Azure will not take back hello D: if hello VM moves tooa different hypervisor.</span></span>

<span data-ttu-id="ff5f6-111">Azure hello geçici disk nasıl kullandığı hakkında daha fazla bilgi için bkz: [hello geçici sürücü Microsoft Azure sanal makineler üzerinde anlama](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)</span><span class="sxs-lookup"><span data-stu-id="ff5f6-111">For more information about how Azure uses hello temporary disk, see [Understanding hello temporary drive on Microsoft Azure Virtual Machines](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)</span></span>

## <a name="attach-hello-data-disk"></a><span data-ttu-id="ff5f6-112">Merhaba veri diski Ekle</span><span class="sxs-lookup"><span data-stu-id="ff5f6-112">Attach hello data disk</span></span>
<span data-ttu-id="ff5f6-113">İlk olarak, tooattach hello veri diski toohello sanal makine gerekir.</span><span class="sxs-lookup"><span data-stu-id="ff5f6-113">First, you'll need tooattach hello data disk toohello virtual machine.</span></span> <span data-ttu-id="ff5f6-114">toodo bu hello portal'ı kullanarak, bkz: [nasıl tooattach yönetilen bir veri diski hello Azure portal](attach-managed-disk-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ff5f6-114">toodo this using hello portal, see [How tooattach a managed data disk in hello Azure portal](attach-managed-disk-portal.md).</span></span>

## <a name="temporarily-move-pagefilesys-tooc-drive"></a><span data-ttu-id="ff5f6-115">Geçici olarak pagefile.sys tooC sürücüye taşıyın</span><span class="sxs-lookup"><span data-stu-id="ff5f6-115">Temporarily move pagefile.sys tooC drive</span></span>
1. <span data-ttu-id="ff5f6-116">Toohello sanal makineye bağlanın.</span><span class="sxs-lookup"><span data-stu-id="ff5f6-116">Connect toohello virtual machine.</span></span> 
2. <span data-ttu-id="ff5f6-117">Sağ hello **Başlat** menü ve select **sistem**.</span><span class="sxs-lookup"><span data-stu-id="ff5f6-117">Right-click hello **Start** menu and select **System**.</span></span>
3. <span data-ttu-id="ff5f6-118">Merhaba sol menüde seçin **Gelişmiş Sistem ayarları**.</span><span class="sxs-lookup"><span data-stu-id="ff5f6-118">In hello left-hand menu, select **Advanced system settings**.</span></span>
4. <span data-ttu-id="ff5f6-119">Merhaba, **performans** bölümünde, select **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="ff5f6-119">In hello **Performance** section, select **Settings**.</span></span>
5. <span data-ttu-id="ff5f6-120">Select hello **Gelişmiş** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="ff5f6-120">Select hello **Advanced** tab.</span></span>
6. <span data-ttu-id="ff5f6-121">Merhaba, **sanal bellek** bölümünde, select **değişiklik**.</span><span class="sxs-lookup"><span data-stu-id="ff5f6-121">In hello **Virtual memory** section, select **Change**.</span></span>
7. <span data-ttu-id="ff5f6-122">Select hello **C** sürücü ve ardından **sistem yönetilen boyutu** ve ardından **ayarlamak**.</span><span class="sxs-lookup"><span data-stu-id="ff5f6-122">Select hello **C** drive and then click **System managed size** and then click **Set**.</span></span>
8. <span data-ttu-id="ff5f6-123">Select hello **D** sürücü ve ardından **herhangi bir disk belleği dosyası** ve ardından **ayarlamak**.</span><span class="sxs-lookup"><span data-stu-id="ff5f6-123">Select hello **D** drive and then click **No paging file** and then click **Set**.</span></span>
9. <span data-ttu-id="ff5f6-124">Uygula'yı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="ff5f6-124">Click Apply.</span></span> <span data-ttu-id="ff5f6-125">Bu hello bilgisayarın hello değişiklikleri tootake etkileyen için yeniden toobe gerekiyor bir uyarı alırsınız.</span><span class="sxs-lookup"><span data-stu-id="ff5f6-125">You will get a warning that hello computer needs toobe restarted for hello changes tootake affect.</span></span>
10. <span data-ttu-id="ff5f6-126">Merhaba sanal makineyi yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="ff5f6-126">Restart hello virtual machine.</span></span>

## <a name="change-hello-drive-letters"></a><span data-ttu-id="ff5f6-127">Merhaba sürücü harflerini Değiştir</span><span class="sxs-lookup"><span data-stu-id="ff5f6-127">Change hello drive letters</span></span>
1. <span data-ttu-id="ff5f6-128">Bir kez hello VM yeniden başlatma geri toohello üzerinde VM oturum.</span><span class="sxs-lookup"><span data-stu-id="ff5f6-128">Once hello VM restarts, log back on toohello VM.</span></span>
2. <span data-ttu-id="ff5f6-129">Merhaba tıklatın **Başlat** menü ve türü **diskmgmt.msc** ve Enter tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="ff5f6-129">Click hello **Start** menu and type **diskmgmt.msc** and hit Enter.</span></span> <span data-ttu-id="ff5f6-130">Disk Yönetimi başlar.</span><span class="sxs-lookup"><span data-stu-id="ff5f6-130">Disk Management will start.</span></span>
3. <span data-ttu-id="ff5f6-131">Sağ **D**hello geçici depolama sürücüsü ve seçin **değişiklik sürücü harfi ve yolları**.</span><span class="sxs-lookup"><span data-stu-id="ff5f6-131">Right-click on **D**, hello Temporary Storage drive, and select **Change Drive Letter and Paths**.</span></span>
4. <span data-ttu-id="ff5f6-132">Sürücü harfi altında yeni bir sürücü gibi seçin **T** ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="ff5f6-132">Under Drive letter, select a new drive such as **T** and then click **OK**.</span></span> 
5. <span data-ttu-id="ff5f6-133">Merhaba veri disk üzerinde sağ tıklatın ve seçin **değişiklik sürücü harfi ve yolları**.</span><span class="sxs-lookup"><span data-stu-id="ff5f6-133">Right-click on hello data disk, and select **Change Drive Letter and Paths**.</span></span>
6. <span data-ttu-id="ff5f6-134">Sürücü harfi altında seçin **D** ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="ff5f6-134">Under Drive letter, select drive **D** and then click **OK**.</span></span> 

## <a name="move-pagefilesys-back-toohello-temporary-storage-drive"></a><span data-ttu-id="ff5f6-135">Pagefile.sys geri toohello geçici depolama sürücüsü taşıma</span><span class="sxs-lookup"><span data-stu-id="ff5f6-135">Move pagefile.sys back toohello temporary storage drive</span></span>
1. <span data-ttu-id="ff5f6-136">Sağ hello **Başlat** menü ve select **sistem**</span><span class="sxs-lookup"><span data-stu-id="ff5f6-136">Right-click hello **Start** menu and select **System**</span></span>
2. <span data-ttu-id="ff5f6-137">Merhaba sol menüde seçin **Gelişmiş Sistem ayarları**.</span><span class="sxs-lookup"><span data-stu-id="ff5f6-137">In hello left-hand menu, select **Advanced system settings**.</span></span>
3. <span data-ttu-id="ff5f6-138">Merhaba, **performans** bölümünde, select **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="ff5f6-138">In hello **Performance** section, select **Settings**.</span></span>
4. <span data-ttu-id="ff5f6-139">Select hello **Gelişmiş** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="ff5f6-139">Select hello **Advanced** tab.</span></span>
5. <span data-ttu-id="ff5f6-140">Merhaba, **sanal bellek** bölümünde, select **değişiklik**.</span><span class="sxs-lookup"><span data-stu-id="ff5f6-140">In hello **Virtual memory** section, select **Change**.</span></span>
6. <span data-ttu-id="ff5f6-141">Merhaba işletim sistemi sürücüsünü seçin **C** tıklatıp **herhangi bir disk belleği dosyası** ve ardından **ayarlamak**.</span><span class="sxs-lookup"><span data-stu-id="ff5f6-141">Select hello OS drive **C** and click **No paging file** and then click **Set**.</span></span>
7. <span data-ttu-id="ff5f6-142">Merhaba geçici depolama sürücüsünü seçin **T** ve ardından **sistem yönetilen boyutu** ve ardından **ayarlamak**.</span><span class="sxs-lookup"><span data-stu-id="ff5f6-142">Select hello temporary storage drive **T** and then click **System managed size** and then click **Set**.</span></span>
8. <span data-ttu-id="ff5f6-143">**Uygula**'ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ff5f6-143">Click **Apply**.</span></span> <span data-ttu-id="ff5f6-144">Bu hello bilgisayarın hello değişiklikleri tootake etkileyen için yeniden toobe gerekiyor bir uyarı alırsınız.</span><span class="sxs-lookup"><span data-stu-id="ff5f6-144">You will get a warning that hello computer needs toobe restarted for hello changes tootake affect.</span></span>
9. <span data-ttu-id="ff5f6-145">Merhaba sanal makineyi yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="ff5f6-145">Restart hello virtual machine.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ff5f6-146">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ff5f6-146">Next steps</span></span>
* <span data-ttu-id="ff5f6-147">Merhaba depolama kullanılabilir tooyour sanal makine tarafından artırabilirsiniz [bir ek veri diski eklemeyi](attach-managed-disk-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ff5f6-147">You can increase hello storage available tooyour virtual machine by [attaching a additional data disk](attach-managed-disk-portal.md).</span></span>

