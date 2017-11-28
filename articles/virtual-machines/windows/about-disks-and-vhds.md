---
title: "Diskler ve Microsoft Azure Windows VM'ler için VHD'ler hakkında | Microsoft Docs"
description: "Diskleri ve VHD'ler için Windows Azure sanal makineleri temelleri hakkında bilgi edinin."
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 0142c64d-5e8c-4d62-aa6f-06d6261f485a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: robinsh
ms.openlocfilehash: c194ca0f31d077ffa998764b9d63b12dd596ac32
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="about-disks-and-vhds-for-azure-windows-vms"></a><span data-ttu-id="c0da8-103">Diskleri ve Azure Windows VM'ler için VHD'ler hakkında</span><span class="sxs-lookup"><span data-stu-id="c0da8-103">About disks and VHDs for Azure Windows VMs</span></span>
<span data-ttu-id="c0da8-104">Yalnızca başka bir bilgisayarda gibi azure'daki sanal makinelerde bir işletim sistemini, uygulamaları ve verileri depolamak için bir yer olarak diskleri kullanın.</span><span class="sxs-lookup"><span data-stu-id="c0da8-104">Just like any other computer, virtual machines in Azure use disks as a place to store an operating system, applications, and data.</span></span> <span data-ttu-id="c0da8-105">Tüm Azure sanal makineler en az iki disk – bir Windows işletim sistemi diski ve geçici bir diske sahip.</span><span class="sxs-lookup"><span data-stu-id="c0da8-105">All Azure virtual machines have at least two disks – a Windows operating system disk and a temporary disk.</span></span> <span data-ttu-id="c0da8-106">İşletim sistemi diski bir görüntüden oluşturulur ve hem işletim sistemi diski ve görüntünün sanal bir Azure depolama hesabında depolanan sabit diskler (VHD).</span><span class="sxs-lookup"><span data-stu-id="c0da8-106">The operating system disk is created from an image, and both the operating system disk and the image are virtual hard disks (VHDs) stored in an Azure storage account.</span></span> <span data-ttu-id="c0da8-107">Sanal makineler ayrıca VHD'ler olarak da depolanan bir veya daha fazla veri diski olabilir.</span><span class="sxs-lookup"><span data-stu-id="c0da8-107">Virtual machines also can have one or more data disks, that are also stored as VHDs.</span></span> 

<span data-ttu-id="c0da8-108">Bu makalede, biz diskler için farklı kullanımlar hakkında konuşun ve oluşturma ve kullanma disklerinin farklı türleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="c0da8-108">In this article, we will talk about the different uses for the disks, and then discuss the different types of disks you can create and use.</span></span> <span data-ttu-id="c0da8-109">Bu makalede ayrıca kullanılabilir [Linux sanal makineleri](about-disks-and-vhds.md).</span><span class="sxs-lookup"><span data-stu-id="c0da8-109">This article is also available for [Linux virtual machines](about-disks-and-vhds.md).</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="disks-used-by-vms"></a><span data-ttu-id="c0da8-110">VM'ler tarafından kullanılan diskler</span><span class="sxs-lookup"><span data-stu-id="c0da8-110">Disks used by VMs</span></span>

<span data-ttu-id="c0da8-111">Diskleri VM'ler tarafından nasıl kullanıldığı bir bakalım.</span><span class="sxs-lookup"><span data-stu-id="c0da8-111">Let's take a look at how the disks are used by the VMs.</span></span>

### <a name="operating-system-disk"></a><span data-ttu-id="c0da8-112">İşletim sistemi diski</span><span class="sxs-lookup"><span data-stu-id="c0da8-112">Operating system disk</span></span>
<span data-ttu-id="c0da8-113">Her bir sanal makinede bir ekli işletim sistemi diski var.</span><span class="sxs-lookup"><span data-stu-id="c0da8-113">Every virtual machine has one attached operating system disk.</span></span> <span data-ttu-id="c0da8-114">SATA sürücü olarak kayıtlı ve C: sürücüsündeki varsayılan olarak etiketli.</span><span class="sxs-lookup"><span data-stu-id="c0da8-114">It's registered as a SATA drive and labeled as the C: drive by default.</span></span> <span data-ttu-id="c0da8-115">Bu disk 2048 gigabayt (GB) en fazla kapasiteye sahiptir.</span><span class="sxs-lookup"><span data-stu-id="c0da8-115">This disk has a maximum capacity of 2048 gigabytes (GB).</span></span> 

### <a name="temporary-disk"></a><span data-ttu-id="c0da8-116">Geçici disk</span><span class="sxs-lookup"><span data-stu-id="c0da8-116">Temporary disk</span></span>
<span data-ttu-id="c0da8-117">Her VM geçici disk içerir.</span><span class="sxs-lookup"><span data-stu-id="c0da8-117">Each VM contains a temporary disk.</span></span> <span data-ttu-id="c0da8-118">Geçici disk uygulamalar ve işlemler için kısa vadeli depolama sağlar ve yalnızca sayfa veya takas dosyaları gibi verileri depolamak için kullanılması amaçlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="c0da8-118">The temporary disk provides short-term storage for applications and processes and is intended to only store data such as page or swap files.</span></span> <span data-ttu-id="c0da8-119">Geçici disk üzerindeki verileri kaybolabilir sırasında bir [bakım olayı](manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json#understand-vm-reboots---maintenance-vs-downtime) veya ne zaman, [VM yeniden](redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c0da8-119">Data on the temporary disk may be lost during a [maintenance event](manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json#understand-vm-reboots---maintenance-vs-downtime) or when you [redeploy a VM](redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="c0da8-120">Sırasında standart yeniden başlatma VM geçici sürücüdeki verilerin kalıcı olması.</span><span class="sxs-lookup"><span data-stu-id="c0da8-120">During a standard reboot of the VM, the data on the temporary drive should persist.</span></span>

<span data-ttu-id="c0da8-121">Geçici disk varsayılan ve pagefile.sys depolamak için kullanılan tarafından D: sürücü olarak etiketlenir.</span><span class="sxs-lookup"><span data-stu-id="c0da8-121">The temporary disk is labeled as the D: drive by default and it used for storing pagefile.sys.</span></span> <span data-ttu-id="c0da8-122">Farklı bir sürücü harfi için bu diski yeniden eşlemek için bkz: [Windows geçici disk sürücü harfini değiştirin](change-drive-letter.md).</span><span class="sxs-lookup"><span data-stu-id="c0da8-122">To remap this disk to a different drive letter, see [Change the drive letter of the Windows temporary disk](change-drive-letter.md).</span></span> <span data-ttu-id="c0da8-123">Geçici diskin boyutunu, sanal makine boyutuna göre değişir.</span><span class="sxs-lookup"><span data-stu-id="c0da8-123">The size of the temporary disk varies, based on the size of the virtual machine.</span></span> <span data-ttu-id="c0da8-124">Daha fazla bilgi için bkz: [boyutları için Windows sanal makineleri](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="c0da8-124">For more information, see [Sizes for Windows virtual machines](sizes.md).</span></span>

<span data-ttu-id="c0da8-125">Azure geçici disk nasıl kullandığı hakkında daha fazla bilgi için bkz: [geçici sürücü Microsoft Azure sanal makineler üzerinde anlama](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)</span><span class="sxs-lookup"><span data-stu-id="c0da8-125">For more information on how Azure uses the temporary disk, see [Understanding the temporary drive on Microsoft Azure Virtual Machines](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)</span></span>


### <a name="data-disk"></a><span data-ttu-id="c0da8-126">Veri diski</span><span class="sxs-lookup"><span data-stu-id="c0da8-126">Data disk</span></span>
<span data-ttu-id="c0da8-127">Uygulama verileri veya tutmak için gereksinim duyduğunuz diğer veri depolamak için bir sanal makineye bağlı VHD veri disktir.</span><span class="sxs-lookup"><span data-stu-id="c0da8-127">A data disk is a VHD that's attached to a virtual machine to store application data, or other data you need to keep.</span></span> <span data-ttu-id="c0da8-128">Veri diskleri SCSI sürücüsü olarak kaydedilir ve seçtiğiniz bir harf ile etiketlenir.</span><span class="sxs-lookup"><span data-stu-id="c0da8-128">Data disks are registered as SCSI drives and are labeled with a letter that you choose.</span></span> <span data-ttu-id="c0da8-129">Her veri diski maksimum 4095 GB kapasitesine sahiptir.</span><span class="sxs-lookup"><span data-stu-id="c0da8-129">Each data disk has a maximum capacity of 4095 GB.</span></span> <span data-ttu-id="c0da8-130">Kaç tane veri diskleri ve depolama türü için iliştirebilirsiniz diskleri barındırmak için kullanabileceğiniz sanal makine boyutunu belirler.</span><span class="sxs-lookup"><span data-stu-id="c0da8-130">The size of the virtual machine determines how many data disks you can attach to it and the type of storage you can use to host the disks.</span></span>

> [!NOTE]
> <span data-ttu-id="c0da8-131">Sanal makineler kapasiteleri hakkında daha fazla bilgi için bkz: [boyutları için Windows sanal makineleri](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="c0da8-131">For more information about virtual machines capacities, see [Sizes for Windows virtual machines](sizes.md).</span></span>
> 

<span data-ttu-id="c0da8-132">Bir görüntüden sanal makine oluşturduğunuzda azure bir işletim sistemi diski oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c0da8-132">Azure creates an operating system disk when you create a virtual machine from an image.</span></span> <span data-ttu-id="c0da8-133">Veri diskleri içeren bir görüntü kullanırsanız, sanal makine oluştururken Azure ayrıca veri diskleri oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c0da8-133">If you use an image that includes data disks, Azure also creates the data disks when it creates the virtual machine.</span></span> <span data-ttu-id="c0da8-134">Aksi halde, sanal makineyi oluşturduktan sonra veri diski ekleyin.</span><span class="sxs-lookup"><span data-stu-id="c0da8-134">Otherwise, you add data disks after you create the virtual machine.</span></span>

<span data-ttu-id="c0da8-135">Veri diski bir sanal makine için herhangi bir zamanda göre ekleyebileceğiniz **ekleme** sanal makineye disk.</span><span class="sxs-lookup"><span data-stu-id="c0da8-135">You can add data disks to a virtual machine at any time, by **attaching** the disk to the virtual machine.</span></span> <span data-ttu-id="c0da8-136">Karşıya veya depolama hesabınız veya bir Azure sizin için oluşturduğu kopyalanan VHD kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c0da8-136">You can use a VHD that you've uploaded or copied to your storage account, or one that Azure creates for you.</span></span> <span data-ttu-id="c0da8-137">Bir veri diski eklemeyi hala bağlıyken depolama biriminden silinemez şekilde VHD 'kira' koyarak VHD dosyasını VM ile ilişkilendirir.</span><span class="sxs-lookup"><span data-stu-id="c0da8-137">Attaching a data disk associates the VHD file with the VM by placing a 'lease' on the VHD so it can't be deleted from storage while it's still attached.</span></span>


[!INCLUDE [storage-about-vhds-and-disks-windows-and-linux](../../../includes/storage-about-vhds-and-disks-windows-and-linux.md)]

## <a name="one-last-recommendation-use-trim-with-unmanaged-standard-disks"></a><span data-ttu-id="c0da8-138">Bir son öneri: kullanım yönetilmeyen standart disklerle KIRPMA</span><span class="sxs-lookup"><span data-stu-id="c0da8-138">One last recommendation: Use TRIM with unmanaged standard disks</span></span> 

<span data-ttu-id="c0da8-139">Yönetilmeyen standart disk (HDD) kullanırsanız, KIRPMA etkinleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="c0da8-139">If you use unmanaged standard disks (HDD), you should enable TRIM.</span></span> <span data-ttu-id="c0da8-140">Yalnızca gerçekten kullandığınız depolama için faturalandırılır şekilde KIRPMA diskte kullanılmayan blokları atar.</span><span class="sxs-lookup"><span data-stu-id="c0da8-140">TRIM discards unused blocks on the disk so you are only billed for storage that you are actually using.</span></span> <span data-ttu-id="c0da8-141">Büyük dosyaları oluşturmak ve bunları silerseniz bu maliyetleri kaydedebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c0da8-141">This can save on costs if you create large files and then delete them.</span></span> 

<span data-ttu-id="c0da8-142">KIRPMA ayarını denetlemek için bu komutu çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c0da8-142">You can run this command to check the TRIM setting.</span></span> <span data-ttu-id="c0da8-143">Windows VM ve türü bir komut istemi açın:</span><span class="sxs-lookup"><span data-stu-id="c0da8-143">Open a command prompt on your Windows VM and type:</span></span>


```
fsutil behavior query DisableDeleteNotify
```

<span data-ttu-id="c0da8-144">Komut 0 döndürürse, KIRPMA doğru şekilde etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="c0da8-144">If the command returns 0, TRIM is enabled correctly.</span></span> <span data-ttu-id="c0da8-145">1 değeri döndürülürse, KIRPMA etkinleştirmek için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="c0da8-145">If it returns 1, run the following command to enable TRIM:</span></span>

```
fsutil behavior set DisableDeleteNotify 0
```

> [!NOTE]
> <span data-ttu-id="c0da8-146">Not: Windows Server 2012 ile kırpma desteği başlatır / Windows 8 ve yukarıda bkz bkz [yeni API sağlar "KIRPMA ve eşlemesini" ipuçları depolama ortamına göndermek uygulamalar](https://msdn.microsoft.com/windows/compatibility/new-api-allows-apps-to-send-trim-and-unmap-hints).</span><span class="sxs-lookup"><span data-stu-id="c0da8-146">Note: Trim support starts with Windows Server 2012 / Windows 8 and above, see see [New API allows apps to send "TRIM and Unmap" hints to storage media](https://msdn.microsoft.com/windows/compatibility/new-api-allows-apps-to-send-trim-and-unmap-hints).</span></span>
> 

<!-- Might want to match next-steps from overview of managed disks -->
## <a name="next-steps"></a><span data-ttu-id="c0da8-147">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c0da8-147">Next steps</span></span>
* <span data-ttu-id="c0da8-148">[Bir diski kullanıma açın](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) VM için ek depolama alanı eklemek için.</span><span class="sxs-lookup"><span data-stu-id="c0da8-148">[Attach a disk](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) to add additional storage for your VM.</span></span>
* <span data-ttu-id="c0da8-149">[Windows geçici disk sürücü harfini değiştirin](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) uygulamanız için verileri D: sürücü kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c0da8-149">[Change the drive letter of the Windows temporary disk](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) so your application can use the D: drive for data.</span></span>

