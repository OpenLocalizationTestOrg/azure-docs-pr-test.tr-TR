---
title: "VM bir veri diski D: sürücüyü hale | Microsoft Docs"
description: "Bir veri sürücüsü olarak D: sürücü kullanabilmesi için bir Windows VM sürücü harflerini değiştirmek açıklar."
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
ms.openlocfilehash: 7667175c01be2421bfc3badd83b1d8aaeb29bfde
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-d-drive-as-a-data-drive-on-a-windows-vm"></a><span data-ttu-id="d0770-103">Bir Windows VM üzerinde bir veri sürücüsü olarak kullanmak üzere D: sürücü</span><span class="sxs-lookup"><span data-stu-id="d0770-103">Use the D: drive as a data drive on a Windows VM</span></span>
<span data-ttu-id="d0770-104">Uygulamanızın veri depolamak için D sürücüsündeki kullanması gerekirse, farklı bir sürücü harfi için geçici disk kullanmak için bu yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="d0770-104">If your application needs to use the D drive to store data, follow these instructions to use a different drive letter for the temporary disk.</span></span> <span data-ttu-id="d0770-105">Hiçbir zaman tutmak için gereken verileri depolamak için geçici disk kullanın.</span><span class="sxs-lookup"><span data-stu-id="d0770-105">Never use the temporary disk to store data that you need to keep.</span></span>

<span data-ttu-id="d0770-106">Yeniden boyutlandırma varsa veya **Dur (Deallocate)** bir sanal makine, bu yeni bir hiper yönetici sanal makinenin yerleştirme tetikleyebilir.</span><span class="sxs-lookup"><span data-stu-id="d0770-106">If you resize or **Stop (Deallocate)** a virtual machine, this may trigger placement of the virtual machine to a new hypervisor.</span></span> <span data-ttu-id="d0770-107">Bir planlı veya plansız bir bakım olayı de bu yerleştirme tetikleyebilir.</span><span class="sxs-lookup"><span data-stu-id="d0770-107">A planned or unplanned maintenance event may also trigger this placement.</span></span> <span data-ttu-id="d0770-108">Bu senaryoda, geçici disk ilk kullanılabilir sürücü harfi atanır.</span><span class="sxs-lookup"><span data-stu-id="d0770-108">In this scenario, the temporary disk will be reassigned to the first available drive letter.</span></span> <span data-ttu-id="d0770-109">Özellikle D: sürücü gerektiren bir uygulama varsa, geçici olarak pagefile.sys taşıyın, yeni bir veri diskini ve harf D atayın ve ardından pagefile.sys geçici sürücü taşımak için şu adımları izlemesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="d0770-109">If you have an application that specifically requires the D: drive, you need to follow these steps to temporarily move the pagefile.sys, attach a new data disk and assign it the letter D and then move the pagefile.sys back to the temporary drive.</span></span> <span data-ttu-id="d0770-110">VM için farklı bir hiper taşınırsa tamamlandıktan sonra Azure geri D: olmayacaktır.</span><span class="sxs-lookup"><span data-stu-id="d0770-110">Once complete, Azure will not take back the D: if the VM moves to a different hypervisor.</span></span>

<span data-ttu-id="d0770-111">Azure geçici disk nasıl kullandığı hakkında daha fazla bilgi için bkz: [geçici sürücü Microsoft Azure sanal makineler üzerinde anlama](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)</span><span class="sxs-lookup"><span data-stu-id="d0770-111">For more information about how Azure uses the temporary disk, see [Understanding the temporary drive on Microsoft Azure Virtual Machines](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)</span></span>

## <a name="attach-the-data-disk"></a><span data-ttu-id="d0770-112">Veri diski Ekle</span><span class="sxs-lookup"><span data-stu-id="d0770-112">Attach the data disk</span></span>
<span data-ttu-id="d0770-113">İlk olarak, sanal makine veri diski eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="d0770-113">First, you'll need to attach the data disk to the virtual machine.</span></span> <span data-ttu-id="d0770-114">Portalı kullanarak bunu yapmak için bkz: [Azure portalında bir yönetilen veri diskini nasıl](attach-managed-disk-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d0770-114">To do this using the portal, see [How to attach a managed data disk in the Azure portal](attach-managed-disk-portal.md).</span></span>

## <a name="temporarily-move-pagefilesys-to-c-drive"></a><span data-ttu-id="d0770-115">Geçici olarak pagefile.sys C sürücüye taşıyın</span><span class="sxs-lookup"><span data-stu-id="d0770-115">Temporarily move pagefile.sys to C drive</span></span>
1. <span data-ttu-id="d0770-116">Sanal makineye bağlanın.</span><span class="sxs-lookup"><span data-stu-id="d0770-116">Connect to the virtual machine.</span></span> 
2. <span data-ttu-id="d0770-117">Sağ **Başlat** menü ve select **sistem**.</span><span class="sxs-lookup"><span data-stu-id="d0770-117">Right-click the **Start** menu and select **System**.</span></span>
3. <span data-ttu-id="d0770-118">Sol menüde seçin **Gelişmiş Sistem ayarları**.</span><span class="sxs-lookup"><span data-stu-id="d0770-118">In the left-hand menu, select **Advanced system settings**.</span></span>
4. <span data-ttu-id="d0770-119">İçinde **performans** bölümünde, select **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="d0770-119">In the **Performance** section, select **Settings**.</span></span>
5. <span data-ttu-id="d0770-120">Seçin **Gelişmiş** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="d0770-120">Select the **Advanced** tab.</span></span>
6. <span data-ttu-id="d0770-121">İçinde **sanal bellek** bölümünde, select **değişiklik**.</span><span class="sxs-lookup"><span data-stu-id="d0770-121">In the **Virtual memory** section, select **Change**.</span></span>
7. <span data-ttu-id="d0770-122">Seçin **C** sürücü ve ardından **sistem yönetilen boyutu** ve ardından **ayarlamak**.</span><span class="sxs-lookup"><span data-stu-id="d0770-122">Select the **C** drive and then click **System managed size** and then click **Set**.</span></span>
8. <span data-ttu-id="d0770-123">Seçin **D** sürücü ve ardından **herhangi bir disk belleği dosyası** ve ardından **ayarlamak**.</span><span class="sxs-lookup"><span data-stu-id="d0770-123">Select the **D** drive and then click **No paging file** and then click **Set**.</span></span>
9. <span data-ttu-id="d0770-124">Uygula'yı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="d0770-124">Click Apply.</span></span> <span data-ttu-id="d0770-125">Bilgisayarın değişikliklerin etkili olması için yeniden başlatılması gerekiyor bir uyarı alırsınız.</span><span class="sxs-lookup"><span data-stu-id="d0770-125">You will get a warning that the computer needs to be restarted for the changes to take affect.</span></span>
10. <span data-ttu-id="d0770-126">Sanal makineyi yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="d0770-126">Restart the virtual machine.</span></span>

## <a name="change-the-drive-letters"></a><span data-ttu-id="d0770-127">Sürücü harflerini değiştirme</span><span class="sxs-lookup"><span data-stu-id="d0770-127">Change the drive letters</span></span>
1. <span data-ttu-id="d0770-128">VM yeniden başlatıldıktan sonra geri açın VM oturum açın.</span><span class="sxs-lookup"><span data-stu-id="d0770-128">Once the VM restarts, log back on to the VM.</span></span>
2. <span data-ttu-id="d0770-129">Tıklatın **Başlat** menü ve türü **diskmgmt.msc** ve Enter tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="d0770-129">Click the **Start** menu and type **diskmgmt.msc** and hit Enter.</span></span> <span data-ttu-id="d0770-130">Disk Yönetimi başlar.</span><span class="sxs-lookup"><span data-stu-id="d0770-130">Disk Management will start.</span></span>
3. <span data-ttu-id="d0770-131">Sağ **D**, geçici depolama sürücüsü ve select **değişiklik sürücü harfi ve yolları**.</span><span class="sxs-lookup"><span data-stu-id="d0770-131">Right-click on **D**, the Temporary Storage drive, and select **Change Drive Letter and Paths**.</span></span>
4. <span data-ttu-id="d0770-132">Sürücü harfi altında yeni bir sürücü gibi seçin **T** ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="d0770-132">Under Drive letter, select a new drive such as **T** and then click **OK**.</span></span> 
5. <span data-ttu-id="d0770-133">Üzerinde veri diski sağ tıklatın ve seçin **değişiklik sürücü harfi ve yolları**.</span><span class="sxs-lookup"><span data-stu-id="d0770-133">Right-click on the data disk, and select **Change Drive Letter and Paths**.</span></span>
6. <span data-ttu-id="d0770-134">Sürücü harfi altında seçin **D** ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="d0770-134">Under Drive letter, select drive **D** and then click **OK**.</span></span> 

## <a name="move-pagefilesys-back-to-the-temporary-storage-drive"></a><span data-ttu-id="d0770-135">Pagefile.sys geçici bir depolama sürücüsüne geri dönün</span><span class="sxs-lookup"><span data-stu-id="d0770-135">Move pagefile.sys back to the temporary storage drive</span></span>
1. <span data-ttu-id="d0770-136">Sağ **Başlat** menü ve select **sistem**</span><span class="sxs-lookup"><span data-stu-id="d0770-136">Right-click the **Start** menu and select **System**</span></span>
2. <span data-ttu-id="d0770-137">Sol menüde seçin **Gelişmiş Sistem ayarları**.</span><span class="sxs-lookup"><span data-stu-id="d0770-137">In the left-hand menu, select **Advanced system settings**.</span></span>
3. <span data-ttu-id="d0770-138">İçinde **performans** bölümünde, select **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="d0770-138">In the **Performance** section, select **Settings**.</span></span>
4. <span data-ttu-id="d0770-139">Seçin **Gelişmiş** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="d0770-139">Select the **Advanced** tab.</span></span>
5. <span data-ttu-id="d0770-140">İçinde **sanal bellek** bölümünde, select **değişiklik**.</span><span class="sxs-lookup"><span data-stu-id="d0770-140">In the **Virtual memory** section, select **Change**.</span></span>
6. <span data-ttu-id="d0770-141">İşletim sistemi sürücüsü **C** tıklatıp **herhangi bir disk belleği dosyası** ve ardından **ayarlamak**.</span><span class="sxs-lookup"><span data-stu-id="d0770-141">Select the OS drive **C** and click **No paging file** and then click **Set**.</span></span>
7. <span data-ttu-id="d0770-142">Geçici depolama sürücüsünü seçin **T** ve ardından **sistem yönetilen boyutu** ve ardından **ayarlamak**.</span><span class="sxs-lookup"><span data-stu-id="d0770-142">Select the temporary storage drive **T** and then click **System managed size** and then click **Set**.</span></span>
8. <span data-ttu-id="d0770-143">**Uygula**'ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d0770-143">Click **Apply**.</span></span> <span data-ttu-id="d0770-144">Bilgisayarın değişikliklerin etkili olması için yeniden başlatılması gerekiyor bir uyarı alırsınız.</span><span class="sxs-lookup"><span data-stu-id="d0770-144">You will get a warning that the computer needs to be restarted for the changes to take affect.</span></span>
9. <span data-ttu-id="d0770-145">Sanal makineyi yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="d0770-145">Restart the virtual machine.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d0770-146">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d0770-146">Next steps</span></span>
* <span data-ttu-id="d0770-147">Sanal makinenize tarafından kullanılabilir depolama alanı artırabilirsiniz [bir ek veri diski eklemeyi](attach-managed-disk-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d0770-147">You can increase the storage available to your virtual machine by [attaching a additional data disk](attach-managed-disk-portal.md).</span></span>

