---
title: "aaaAbout diskleri ve Microsoft Azure Windows VM'ler için VHD'ler | Microsoft Docs"
description: "Diskleri ve sanal makineleri Azure VHD'ler için Windows hello temelleri hakkında bilgi edinin."
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
ms.openlocfilehash: 859e564dc74240bd7c70fec33255b8d071c4acf7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="about-disks-and-vhds-for-azure-windows-vms"></a><span data-ttu-id="4a7d6-103">Diskleri ve Azure Windows VM'ler için VHD'ler hakkında</span><span class="sxs-lookup"><span data-stu-id="4a7d6-103">About disks and VHDs for Azure Windows VMs</span></span>
<span data-ttu-id="4a7d6-104">Yalnızca başka bir bilgisayarda gibi azure'daki sanal makinelerde diskleri yer toostore bir işletim sistemi olarak, uygulamaları ve verileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="4a7d6-104">Just like any other computer, virtual machines in Azure use disks as a place toostore an operating system, applications, and data.</span></span> <span data-ttu-id="4a7d6-105">Tüm Azure sanal makineler en az iki disk – bir Windows işletim sistemi diski ve geçici bir diske sahip.</span><span class="sxs-lookup"><span data-stu-id="4a7d6-105">All Azure virtual machines have at least two disks – a Windows operating system disk and a temporary disk.</span></span> <span data-ttu-id="4a7d6-106">Merhaba işletim sistemi diski bir görüntüden oluşturulur ve hem hello işletim sistemi diski ve hello görüntü sabit bir Azure depolama hesabında depolanan sanal diskler (VHD).</span><span class="sxs-lookup"><span data-stu-id="4a7d6-106">hello operating system disk is created from an image, and both hello operating system disk and hello image are virtual hard disks (VHDs) stored in an Azure storage account.</span></span> <span data-ttu-id="4a7d6-107">Sanal makineler ayrıca VHD'ler olarak da depolanan bir veya daha fazla veri diski olabilir.</span><span class="sxs-lookup"><span data-stu-id="4a7d6-107">Virtual machines also can have one or more data disks, that are also stored as VHDs.</span></span> 

<span data-ttu-id="4a7d6-108">Bu makalede, biz hello hello diskler için farklı kullanımlar hakkında konuşun ve hello oluşturma ve kullanma disklerinin farklı türleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="4a7d6-108">In this article, we will talk about hello different uses for hello disks, and then discuss hello different types of disks you can create and use.</span></span> <span data-ttu-id="4a7d6-109">Bu makalede ayrıca kullanılabilir [Linux sanal makineleri](storage-about-disks-and-vhds-linux.md).</span><span class="sxs-lookup"><span data-stu-id="4a7d6-109">This article is also available for [Linux virtual machines](storage-about-disks-and-vhds-linux.md).</span></span>

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-both-include.md)]

## <a name="disks-used-by-vms"></a><span data-ttu-id="4a7d6-110">VM'ler tarafından kullanılan diskler</span><span class="sxs-lookup"><span data-stu-id="4a7d6-110">Disks used by VMs</span></span>

<span data-ttu-id="4a7d6-111">Merhaba diskleri hello VM'ler tarafından nasıl kullanıldığı bir bakalım.</span><span class="sxs-lookup"><span data-stu-id="4a7d6-111">Let's take a look at how hello disks are used by hello VMs.</span></span>

### <a name="operating-system-disk"></a><span data-ttu-id="4a7d6-112">İşletim sistemi diski</span><span class="sxs-lookup"><span data-stu-id="4a7d6-112">Operating system disk</span></span>
<span data-ttu-id="4a7d6-113">Her bir sanal makinede bir ekli işletim sistemi diski var.</span><span class="sxs-lookup"><span data-stu-id="4a7d6-113">Every virtual machine has one attached operating system disk.</span></span> <span data-ttu-id="4a7d6-114">SATA sürücü olarak kayıtlı ve hello C: sürücüsündeki varsayılan olarak etiketli.</span><span class="sxs-lookup"><span data-stu-id="4a7d6-114">It's registered as a SATA drive and labeled as hello C: drive by default.</span></span> <span data-ttu-id="4a7d6-115">Bu disk 2048 gigabayt (GB) en fazla kapasiteye sahiptir.</span><span class="sxs-lookup"><span data-stu-id="4a7d6-115">This disk has a maximum capacity of 2048 gigabytes (GB).</span></span> 

### <a name="temporary-disk"></a><span data-ttu-id="4a7d6-116">Geçici disk</span><span class="sxs-lookup"><span data-stu-id="4a7d6-116">Temporary disk</span></span>
<span data-ttu-id="4a7d6-117">Her VM geçici disk içerir.</span><span class="sxs-lookup"><span data-stu-id="4a7d6-117">Each VM contains a temporary disk.</span></span> <span data-ttu-id="4a7d6-118">Merhaba geçici disk uygulamalar ve işlemler için kısa vadeli depolama sağlar ve sayfa veya takas dosyaları gibi hedeflenen tooonly deposu veriler.</span><span class="sxs-lookup"><span data-stu-id="4a7d6-118">hello temporary disk provides short-term storage for applications and processes and is intended tooonly store data such as page or swap files.</span></span> <span data-ttu-id="4a7d6-119">Merhaba geçici disk üzerindeki verileri kaybolabilir sırasında bir [bakım olayı](../virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json#understand-vm-reboots---maintenance-vs-downtime) veya ne zaman, [VM yeniden](../virtual-machines/windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4a7d6-119">Data on hello temporary disk may be lost during a [maintenance event](../virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json#understand-vm-reboots---maintenance-vs-downtime) or when you [redeploy a VM](../virtual-machines/windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="4a7d6-120">Merhaba VM standart yeniden sırasında hello geçici sürücüdeki hello verilerin kalıcı.</span><span class="sxs-lookup"><span data-stu-id="4a7d6-120">During a standard reboot of hello VM, hello data on hello temporary drive should persist.</span></span>

<span data-ttu-id="4a7d6-121">Merhaba geçici disk varsayılan ve pagefile.sys depolamak için kullanılan tarafından hello D: sürücü etiketlenir.</span><span class="sxs-lookup"><span data-stu-id="4a7d6-121">hello temporary disk is labeled as hello D: drive by default and it used for storing pagefile.sys.</span></span> <span data-ttu-id="4a7d6-122">tooremap bu disk tooa farklı bir sürücü harfi bkz [değişiklik hello sürücü harfi hello Windows geçici disk](../virtual-machines/windows/change-drive-letter.md).</span><span class="sxs-lookup"><span data-stu-id="4a7d6-122">tooremap this disk tooa different drive letter, see [Change hello drive letter of hello Windows temporary disk](../virtual-machines/windows/change-drive-letter.md).</span></span> <span data-ttu-id="4a7d6-123">Merhaba hello geçici diskin boyutunu, hello hello sanal makine boyutuna göre değişir.</span><span class="sxs-lookup"><span data-stu-id="4a7d6-123">hello size of hello temporary disk varies, based on hello size of hello virtual machine.</span></span> <span data-ttu-id="4a7d6-124">Daha fazla bilgi için bkz: [boyutları için Windows sanal makineleri](../virtual-machines/windows/sizes.md).</span><span class="sxs-lookup"><span data-stu-id="4a7d6-124">For more information, see [Sizes for Windows virtual machines](../virtual-machines/windows/sizes.md).</span></span>

<span data-ttu-id="4a7d6-125">Azure hello geçici disk nasıl kullandığı hakkında daha fazla bilgi için bkz: [hello geçici sürücü Microsoft Azure sanal makineler üzerinde anlama](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)</span><span class="sxs-lookup"><span data-stu-id="4a7d6-125">For more information on how Azure uses hello temporary disk, see [Understanding hello temporary drive on Microsoft Azure Virtual Machines](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)</span></span>


### <a name="data-disk"></a><span data-ttu-id="4a7d6-126">Veri diski</span><span class="sxs-lookup"><span data-stu-id="4a7d6-126">Data disk</span></span>
<span data-ttu-id="4a7d6-127">Bir veri diski tookeep gereksinim duyduğunuz diğer veri mi ekli tooa sanal makine toostore uygulama verilerini bir VHD ' dir.</span><span class="sxs-lookup"><span data-stu-id="4a7d6-127">A data disk is a VHD that's attached tooa virtual machine toostore application data, or other data you need tookeep.</span></span> <span data-ttu-id="4a7d6-128">Veri diskleri SCSI sürücüsü olarak kaydedilir ve seçtiğiniz bir harf ile etiketlenir.</span><span class="sxs-lookup"><span data-stu-id="4a7d6-128">Data disks are registered as SCSI drives and are labeled with a letter that you choose.</span></span> <span data-ttu-id="4a7d6-129">Her veri diski maksimum 4095 GB kapasitesine sahiptir.</span><span class="sxs-lookup"><span data-stu-id="4a7d6-129">Each data disk has a maximum capacity of 4095 GB.</span></span> <span data-ttu-id="4a7d6-130">Merhaba hello sanal makine boyutunu belirler kullanabileceğiniz depolama tooit ve hello türü iliştirebilirsiniz kaç tane veri diskleri toohost hello diskler.</span><span class="sxs-lookup"><span data-stu-id="4a7d6-130">hello size of hello virtual machine determines how many data disks you can attach tooit and hello type of storage you can use toohost hello disks.</span></span>

> [!NOTE]
> <span data-ttu-id="4a7d6-131">Sanal makineler kapasiteleri hakkında daha fazla bilgi için bkz: [boyutları için Windows sanal makineleri](../virtual-machines/windows/sizes.md).</span><span class="sxs-lookup"><span data-stu-id="4a7d6-131">For more information about virtual machines capacities, see [Sizes for Windows virtual machines](../virtual-machines/windows/sizes.md).</span></span>
> 

<span data-ttu-id="4a7d6-132">Bir görüntüden sanal makine oluşturduğunuzda azure bir işletim sistemi diski oluşturur.</span><span class="sxs-lookup"><span data-stu-id="4a7d6-132">Azure creates an operating system disk when you create a virtual machine from an image.</span></span> <span data-ttu-id="4a7d6-133">Veri diskleri içeren bir görüntü kullanırsanız, hello sanal makine oluştururken Azure hello veri diskleri da oluşturur.</span><span class="sxs-lookup"><span data-stu-id="4a7d6-133">If you use an image that includes data disks, Azure also creates hello data disks when it creates hello virtual machine.</span></span> <span data-ttu-id="4a7d6-134">Aksi takdirde hello sanal makineyi oluşturduktan sonra veri diski ekleyin.</span><span class="sxs-lookup"><span data-stu-id="4a7d6-134">Otherwise, you add data disks after you create hello virtual machine.</span></span>

<span data-ttu-id="4a7d6-135">Veri diskleri tooa sanal makine olarak herhangi bir zamanda ekleyebilirsiniz **ekleme** disk toohello sanal makine hello.</span><span class="sxs-lookup"><span data-stu-id="4a7d6-135">You can add data disks tooa virtual machine at any time, by **attaching** hello disk toohello virtual machine.</span></span> <span data-ttu-id="4a7d6-136">Karşıya veya tooyour depolama hesabı kopyalanan ya da bir, Azure sizin için oluşturduğu bir VHD kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4a7d6-136">You can use a VHD that you've uploaded or copied tooyour storage account, or one that Azure creates for you.</span></span> <span data-ttu-id="4a7d6-137">Bir veri diski eklemeyi hala bağlıyken depolama biriminden silinemez şekilde 'kira' hello VHD üzerinde koyarak hello VHD dosyasını hello VM ile ilişkilendirir.</span><span class="sxs-lookup"><span data-stu-id="4a7d6-137">Attaching a data disk associates hello VHD file with hello VM by placing a 'lease' on hello VHD so it can't be deleted from storage while it's still attached.</span></span>


[!INCLUDE [storage-about-vhds-and-disks-windows-and-linux](../../includes/storage-about-vhds-and-disks-windows-and-linux.md)]

## <a name="one-last-recommendation-use-trim-with-unmanaged-standard-disks"></a><span data-ttu-id="4a7d6-138">Bir son öneri: kullanım yönetilmeyen standart disklerle KIRPMA</span><span class="sxs-lookup"><span data-stu-id="4a7d6-138">One last recommendation: Use TRIM with unmanaged standard disks</span></span> 

<span data-ttu-id="4a7d6-139">Yönetilmeyen standart disk (HDD) kullanırsanız, KIRPMA etkinleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="4a7d6-139">If you use unmanaged standard disks (HDD), you should enable TRIM.</span></span> <span data-ttu-id="4a7d6-140">Yalnızca gerçekten kullandığınız depolama için faturalandırılır şekilde KIRPMA hello diskte kullanılmayan blokları atar.</span><span class="sxs-lookup"><span data-stu-id="4a7d6-140">TRIM discards unused blocks on hello disk so you are only billed for storage that you are actually using.</span></span> <span data-ttu-id="4a7d6-141">Büyük dosyaları oluşturmak ve bunları silerseniz bu maliyetleri kaydedebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4a7d6-141">This can save on costs if you create large files and then delete them.</span></span> 

<span data-ttu-id="4a7d6-142">Bu komut toocheck hello KIRPMA ayarı çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4a7d6-142">You can run this command toocheck hello TRIM setting.</span></span> <span data-ttu-id="4a7d6-143">Windows VM ve türü bir komut istemi açın:</span><span class="sxs-lookup"><span data-stu-id="4a7d6-143">Open a command prompt on your Windows VM and type:</span></span>


```
fsutil behavior query DisableDeleteNotify
```

<span data-ttu-id="4a7d6-144">Merhaba komut 0 döndürürse, KIRPMA doğru şekilde etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="4a7d6-144">If hello command returns 0, TRIM is enabled correctly.</span></span> <span data-ttu-id="4a7d6-145">1 değeri döndürülürse, komut tooenable KIRPMA aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="4a7d6-145">If it returns 1, run hello following command tooenable TRIM:</span></span>

```
fsutil behavior set DisableDeleteNotify 0
```

> [!NOTE]
> <span data-ttu-id="4a7d6-146">Not: Windows Server 2012 ile kırpma desteği başlatır / Windows 8 ve yukarıda bkz bkz [yeni API apps toosend "KIRPMA ve eşlemesini" ipuçları toostorage medya sağlar](https://msdn.microsoft.com/windows/compatibility/new-api-allows-apps-to-send-trim-and-unmap-hints).</span><span class="sxs-lookup"><span data-stu-id="4a7d6-146">Note: Trim support starts with Windows Server 2012 / Windows 8 and above, see see [New API allows apps toosend "TRIM and Unmap" hints toostorage media](https://msdn.microsoft.com/windows/compatibility/new-api-allows-apps-to-send-trim-and-unmap-hints).</span></span>
> 

<!-- Might want toomatch next-steps from overview of managed disks -->
## <a name="next-steps"></a><span data-ttu-id="4a7d6-147">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4a7d6-147">Next steps</span></span>
* <span data-ttu-id="4a7d6-148">[Bir diski kullanıma açın](../virtual-machines/windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) tooadd, VM için ek depolama alanı.</span><span class="sxs-lookup"><span data-stu-id="4a7d6-148">[Attach a disk](../virtual-machines/windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) tooadd additional storage for your VM.</span></span>
* <span data-ttu-id="4a7d6-149">[Değişiklik hello sürücü harfi hello Windows geçici disk](../virtual-machines/windows/change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) uygulamanız için verileri hello D: sürücü kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4a7d6-149">[Change hello drive letter of hello Windows temporary disk](../virtual-machines/windows/change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) so your application can use hello D: drive for data.</span></span>

