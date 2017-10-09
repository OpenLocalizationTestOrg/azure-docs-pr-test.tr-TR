---
title: aaaMigrating VM'ler tooAzure Premium depolama | Microsoft Docs
description: "Var olan sanal makineleri tooAzure Premium depolama geçirin. Premium Storage, Azure sanal makinelerde çalışan g/Ç kullanımı yoğun iş yükleri için yüksek performanslı, düşük gecikmeli disk desteği sağlar."
services: storage
documentationcenter: na
author: yuemlu
manager: tadb
editor: tysonn
ms.assetid: 272250b3-fd4e-41d2-8e34-fd8cc341ec87
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: yuemlu
ms.openlocfilehash: 19aaf2b7594e570f5a964baa00958a7a8eaae97b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="migrating-tooazure-premium-storage-unmanaged-disks"></a><span data-ttu-id="8396d-104">Geçirme tooAzure Premium Storage (yönetilmeyen diskler)</span><span class="sxs-lookup"><span data-stu-id="8396d-104">Migrating tooAzure Premium Storage (Unmanaged Disks)</span></span>

> [!NOTE]
> <span data-ttu-id="8396d-105">Bu makalede nasıl toomigrate yönetilmeyen standart diskler tooa kullanan VM kullanan bir VM'yi premium diskleri yönetilmeyen anlatılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="8396d-105">This article discusses how toomigrate a VM that uses unmanaged standard disks tooa VM that uses unmanaged premium disks.</span></span> <span data-ttu-id="8396d-106">Azure yönetilen diskleri yeni VM'ler için kullanın ve önceki yönetilmeyen diskleri toomanaged disklerinizi Dönüştür öneririz.</span><span class="sxs-lookup"><span data-stu-id="8396d-106">We recommend that you use Azure Managed Disks for new VMs, and that you convert your previous unmanaged disks toomanaged disks.</span></span> <span data-ttu-id="8396d-107">Zorunda kalmamak için yönetilen diskleri tanıtıcı hello temel alınan depolama hesapları.</span><span class="sxs-lookup"><span data-stu-id="8396d-107">Managed Disks handle hello underlying storage accounts so you don't have to.</span></span> <span data-ttu-id="8396d-108">Daha fazla bilgi için lütfen bkz bizim [yönetilen diskleri genel bakış](../../virtual-machines/windows/managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8396d-108">For more information, please see our [Managed Disks Overview](../../virtual-machines/windows/managed-disks-overview.md).</span></span>
>

<span data-ttu-id="8396d-109">Azure Premium depolama g/Ç kullanımı yoğun iş yükleri çalıştıran sanal makineler için yüksek performanslı, düşük gecikmeli disk desteği sunar.</span><span class="sxs-lookup"><span data-stu-id="8396d-109">Azure Premium Storage delivers high-performance, low-latency disk support for virtual machines running I/O-intensive workloads.</span></span> <span data-ttu-id="8396d-110">Uygulamanızın VM diskleri tooAzure Premium depolama geçirerek avantajı hello hızına ve bu disklerin performansını alabilir.</span><span class="sxs-lookup"><span data-stu-id="8396d-110">You can take advantage of hello speed and performance of these disks by migrating your application's VM disks tooAzure Premium Storage.</span></span>

<span data-ttu-id="8396d-111">Bu kılavuzun amacı Hello Azure Premium Storage daha iyi toohelp yeni kullanıcılar, geçerli sistem tooPremium depolama alanından sorunsuz bir geçiş toomake hazırlama ' dir.</span><span class="sxs-lookup"><span data-stu-id="8396d-111">hello purpose of this guide is toohelp new users of Azure Premium Storage better prepare toomake a smooth transition from their current system tooPremium Storage.</span></span> <span data-ttu-id="8396d-112">Merhaba Kılavuzu üç hello anahtar bileşenleri bu süreçte ele alır:</span><span class="sxs-lookup"><span data-stu-id="8396d-112">hello guide addresses three of hello key components in this process:</span></span>

* [<span data-ttu-id="8396d-113">Merhaba geçiş tooPremium depolama planlama</span><span class="sxs-lookup"><span data-stu-id="8396d-113">Plan for hello Migration tooPremium Storage</span></span>](#plan-the-migration-to-premium-storage)
* [<span data-ttu-id="8396d-114">Hazırlama ve kopyalama sanal sabit diskleri (VHD) tooPremium depolama</span><span class="sxs-lookup"><span data-stu-id="8396d-114">Prepare and Copy Virtual Hard Disks (VHDs) tooPremium Storage</span></span>](#prepare-and-copy-virtual-hard-disks-VHDs-to-premium-storage)
* [<span data-ttu-id="8396d-115">Premium depolama kullanarak Azure sanal makine oluşturun</span><span class="sxs-lookup"><span data-stu-id="8396d-115">Create Azure Virtual Machine using Premium Storage</span></span>](#create-azure-virtual-machine-using-premium-storage)

<span data-ttu-id="8396d-116">Diğer platformlar tooAzure Premium depolama Vm'leri geçirme veya var olan Azure Vm'leri standart depolama tooPremium depolama geçirme.</span><span class="sxs-lookup"><span data-stu-id="8396d-116">You can either migrate VMs from other platforms tooAzure Premium Storage or migrate existing Azure VMs from Standard Storage tooPremium Storage.</span></span> <span data-ttu-id="8396d-117">Bu kılavuz, her iki iki senaryo adımları kapsar.</span><span class="sxs-lookup"><span data-stu-id="8396d-117">This guide covers steps for both two scenarios.</span></span> <span data-ttu-id="8396d-118">Senaryonuza bağlı olarak ilgili hello bölümünde belirtilen hello adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="8396d-118">Follow hello steps specified in hello relevant section depending on your scenario.</span></span>

> [!NOTE]
> <span data-ttu-id="8396d-119">Özelliklere genel bakış ve Premium depolama, Premium Storage fiyatlandırma bulabilirsiniz: [Azure sanal makine iş yükleri için yüksek performanslı depolama](storage-premium-storage.md).</span><span class="sxs-lookup"><span data-stu-id="8396d-119">You can find a feature overview and pricing of Premium Storage in Premium Storage: [High-Performance Storage for Azure Virtual Machine Workloads](storage-premium-storage.md).</span></span> <span data-ttu-id="8396d-120">Merhaba, uygulamanız için en iyi performans için yüksek IOPS tooAzure Premium depolama gerektiren herhangi bir sanal makine disk geçirme öneririz.</span><span class="sxs-lookup"><span data-stu-id="8396d-120">We recommend migrating any virtual machine disk requiring high IOPS tooAzure Premium Storage for hello best performance for your application.</span></span> <span data-ttu-id="8396d-121">Diskinizin yüksek IOPS gerektirmiyorsa SSD yerine Sabit Disk sürücülerinin (HDD'ler) üzerinde sanal makine disk verilerini depolayan standart depolama tutarak maliyetleri sınırlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8396d-121">If your disk does not require high IOPS, you can limit costs by maintaining it in Standard Storage, which stores virtual machine disk data on Hard Disk Drives (HDDs) instead of SSDs.</span></span>
>

<span data-ttu-id="8396d-122">Okumalıdır Hello geçiş işlemini tamamlama öncesinde ve sonrasında bu kılavuzda sağlanan hello adımları ek eylemler gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="8396d-122">Completing hello migration process in its entirety may require additional actions both before and after hello steps provided in this guide.</span></span> <span data-ttu-id="8396d-123">Sanal ağlar veya uç noktaların yapılandırma veya uygulamadaki miktar kapalı kalma süresi, uygulamanızda gerektirebilecek hello kendisini kodda değişiklikler yaparak örnek olarak verilebilir.</span><span class="sxs-lookup"><span data-stu-id="8396d-123">Examples include configuring virtual networks or endpoints or making code changes within hello application itself which may require some downtime in your application.</span></span> <span data-ttu-id="8396d-124">Bu eylemler benzersiz tooeach uygulama olan ve bu kılavuzu toomake hello tam geçiş tooPremium depolama olarak sorunsuz sağlanan hello adımlarını tamamlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8396d-124">These actions are unique tooeach application, and you should complete them along with hello steps provided in this guide toomake hello full transition tooPremium Storage as seamless as possible.</span></span>

## <span data-ttu-id="8396d-125"><a name="plan-the-migration-to-premium-storage"></a>Merhaba geçiş tooPremium depolama planlama</span><span class="sxs-lookup"><span data-stu-id="8396d-125"><a name="plan-the-migration-to-premium-storage"></a>Plan for hello migration tooPremium Storage</span></span>
<span data-ttu-id="8396d-126">Bu bölümde, hazır toofollow hello geçiş bu makalede adımlardır ve toomake hello en iyi karar VM ve Disk türleri hakkında yardımcı sağlar.</span><span class="sxs-lookup"><span data-stu-id="8396d-126">This section ensures that you are ready toofollow hello migration steps in this article, and helps you toomake hello best decision on VM and Disk types.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="8396d-127">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="8396d-127">Prerequisites</span></span>
* <span data-ttu-id="8396d-128">Bir Azure aboneliği gerekir.</span><span class="sxs-lookup"><span data-stu-id="8396d-128">You will need an Azure subscription.</span></span> <span data-ttu-id="8396d-129">Yoksa, bir aylık oluşturabilirsiniz [ücretsiz deneme sürümü](https://azure.microsoft.com/pricing/free-trial/) abonelik veya ziyaret [Azure fiyatlandırma](https://azure.microsoft.com/pricing/) daha fazla seçenek için.</span><span class="sxs-lookup"><span data-stu-id="8396d-129">If you don't have one, you can create a one-month [free trial](https://azure.microsoft.com/pricing/free-trial/) subscription or visit [Azure Pricing](https://azure.microsoft.com/pricing/) for more options.</span></span>
* <span data-ttu-id="8396d-130">tooexecute PowerShell cmdlet'leri, hello Microsoft Azure PowerShell modülü gerekir.</span><span class="sxs-lookup"><span data-stu-id="8396d-130">tooexecute PowerShell cmdlets, you will need hello Microsoft Azure PowerShell module.</span></span> <span data-ttu-id="8396d-131">Bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview) noktası ve yükleme yönergeleri için hello yükleyin.</span><span class="sxs-lookup"><span data-stu-id="8396d-131">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for hello install point and installation instructions.</span></span>
* <span data-ttu-id="8396d-132">Toouse Azure Premium depolama üzerinde çalışan Vm'leri planlarken, toouse hello özellikli Premium Storage Vm'lerini gerekir.</span><span class="sxs-lookup"><span data-stu-id="8396d-132">When you plan toouse Azure VMs running on Premium Storage, you need toouse hello Premium Storage capable VMs.</span></span> <span data-ttu-id="8396d-133">Premium depolama yeteneğine sahip sanal makineleri ile standart ve Premium depolama diskleri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8396d-133">You can use both Standard and Premium Storage disks with Premium Storage capable VMs.</span></span> <span data-ttu-id="8396d-134">Premium depolama diskleri hello gelecekte daha fazla VM türleri ile kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="8396d-134">Premium storage disks will be available with more VM types in hello future.</span></span> <span data-ttu-id="8396d-135">Tüm kullanılabilir Azure VM disk türleri ve boyutları hakkında daha fazla bilgi için bkz: [sanal makineler için Boyutlar](../../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) ve [Cloud Services boyutları](../../cloud-services/cloud-services-sizes-specs.md).</span><span class="sxs-lookup"><span data-stu-id="8396d-135">For more information on all available Azure VM disk types and sizes, see [Sizes for virtual machines](../../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) and [Sizes for Cloud Services](../../cloud-services/cloud-services-sizes-specs.md).</span></span>

### <a name="considerations"></a><span data-ttu-id="8396d-136">Dikkat edilmesi gerekenler</span><span class="sxs-lookup"><span data-stu-id="8396d-136">Considerations</span></span>
<span data-ttu-id="8396d-137">Bir Azure VM uygulamalarınızı too256 TB depolama alanı VM başına yukarı böylece birkaç Premium depolama diskleri ekleme destekler.</span><span class="sxs-lookup"><span data-stu-id="8396d-137">An Azure VM supports attaching several Premium Storage disks so that your applications can have up too256 TB of storage per VM.</span></span> <span data-ttu-id="8396d-138">Premium depolama ile uygulamalarınızı, ikinci disk işleme VM başına okuma işlemleri için son derece düşük gecikme ile başına VM ve 2000 MB başına 80.000 IOPS (saniye başına girdi/çıktı işlemleri) elde edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8396d-138">With Premium Storage, your applications can achieve 80,000 IOPS (input/output operations per second) per VM and 2000 MB per second disk throughput per VM with extremely low latencies for read operations.</span></span> <span data-ttu-id="8396d-139">VM'ler ve diskleri çeşitli seçeneğiniz vardır.</span><span class="sxs-lookup"><span data-stu-id="8396d-139">You have options in a variety of VMs and Disks.</span></span> <span data-ttu-id="8396d-140">Bu bölümde toohelp olan İş yükünüzün uygun bir seçeneği toofind.</span><span class="sxs-lookup"><span data-stu-id="8396d-140">This section is toohelp you toofind an option that best suits your workload.</span></span>

#### <a name="vm-sizes"></a><span data-ttu-id="8396d-141">VM boyutları</span><span class="sxs-lookup"><span data-stu-id="8396d-141">VM sizes</span></span>
<span data-ttu-id="8396d-142">Hello Azure VM boyutu belirtimleri içinde listelenen [sanal makineler için Boyutlar](../../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8396d-142">hello Azure VM size specifications are listed in [Sizes for virtual machines](../../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="8396d-143">Premium Storage ile birlikte çalışmak ve işleminizi iş yükü en çok uyan hello en uygun VM boyutunu seçin sanal makineleri Hello performans özellikleri gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="8396d-143">Review hello performance characteristics of virtual machines that work with Premium Storage and choose hello most appropriate VM size that best suits your workload.</span></span> <span data-ttu-id="8396d-144">Yeterli bant genişliği kullanılabilir VM toodrive hello disk trafiğinde bulunduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="8396d-144">Make sure that there is sufficient bandwidth available on your VM toodrive hello disk traffic.</span></span>

#### <a name="disk-sizes"></a><span data-ttu-id="8396d-145">Disk boyutları</span><span class="sxs-lookup"><span data-stu-id="8396d-145">Disk sizes</span></span>
<span data-ttu-id="8396d-146">VM ile kullanılan diskler beş tür vardır ve her belirli IOPS ve üretilen iş sahip sınırlar.</span><span class="sxs-lookup"><span data-stu-id="8396d-146">There are five types of disks that can be used with your VM and each has specific IOPs and throughput limits.</span></span> <span data-ttu-id="8396d-147">Bu sınırlar yoğun yükler ve kapasite, performans, ölçeklenebilirlik açısından, uygulamanızın hello gereksinimlerine hello disk türü, VM için seçme temel yaparken dikkate.</span><span class="sxs-lookup"><span data-stu-id="8396d-147">Take into consideration these limits when choosing hello disk type for your VM based on hello needs of your application in terms of capacity, performance, scalability, and peak loads.</span></span>

| <span data-ttu-id="8396d-148">Premium diskler türü</span><span class="sxs-lookup"><span data-stu-id="8396d-148">Premium Disks Type</span></span>  | <span data-ttu-id="8396d-149">P10</span><span class="sxs-lookup"><span data-stu-id="8396d-149">P10</span></span>   | <span data-ttu-id="8396d-150">P20</span><span class="sxs-lookup"><span data-stu-id="8396d-150">P20</span></span>   | <span data-ttu-id="8396d-151">P30</span><span class="sxs-lookup"><span data-stu-id="8396d-151">P30</span></span>            | <span data-ttu-id="8396d-152">P40</span><span class="sxs-lookup"><span data-stu-id="8396d-152">P40</span></span>            | <span data-ttu-id="8396d-153">P50</span><span class="sxs-lookup"><span data-stu-id="8396d-153">P50</span></span>            | 
|:-------------------:|:-----:|:-----:|:--------------:|:--------------:|:--------------:|
| <span data-ttu-id="8396d-154">Disk boyutu</span><span class="sxs-lookup"><span data-stu-id="8396d-154">Disk size</span></span>           | <span data-ttu-id="8396d-155">128 GB</span><span class="sxs-lookup"><span data-stu-id="8396d-155">128 GB</span></span>| <span data-ttu-id="8396d-156">512 GB</span><span class="sxs-lookup"><span data-stu-id="8396d-156">512 GB</span></span>| <span data-ttu-id="8396d-157">1024 GB (1 TB)</span><span class="sxs-lookup"><span data-stu-id="8396d-157">1024 GB (1 TB)</span></span> | <span data-ttu-id="8396d-158">2048 GB (2 TB)</span><span class="sxs-lookup"><span data-stu-id="8396d-158">2048 GB (2 TB)</span></span> | <span data-ttu-id="8396d-159">4095 GB (4 TB)</span><span class="sxs-lookup"><span data-stu-id="8396d-159">4095 GB (4 TB)</span></span> | 
| <span data-ttu-id="8396d-160">Disk başına IOPS</span><span class="sxs-lookup"><span data-stu-id="8396d-160">IOPS per disk</span></span>       | <span data-ttu-id="8396d-161">500</span><span class="sxs-lookup"><span data-stu-id="8396d-161">500</span></span>   | <span data-ttu-id="8396d-162">2300</span><span class="sxs-lookup"><span data-stu-id="8396d-162">2300</span></span>  | <span data-ttu-id="8396d-163">5000</span><span class="sxs-lookup"><span data-stu-id="8396d-163">5000</span></span>           | <span data-ttu-id="8396d-164">7500</span><span class="sxs-lookup"><span data-stu-id="8396d-164">7500</span></span>           | <span data-ttu-id="8396d-165">7500</span><span class="sxs-lookup"><span data-stu-id="8396d-165">7500</span></span>           | 
| <span data-ttu-id="8396d-166">Disk başına aktarım hızı</span><span class="sxs-lookup"><span data-stu-id="8396d-166">Throughput per disk</span></span> | <span data-ttu-id="8396d-167">Saniyede 100 MB</span><span class="sxs-lookup"><span data-stu-id="8396d-167">100 MB per second</span></span> | <span data-ttu-id="8396d-168">150 MB / saniye</span><span class="sxs-lookup"><span data-stu-id="8396d-168">150 MB per second</span></span> | <span data-ttu-id="8396d-169">200 MB / saniye</span><span class="sxs-lookup"><span data-stu-id="8396d-169">200 MB per second</span></span> | <span data-ttu-id="8396d-170">Saniye başına 250 MB</span><span class="sxs-lookup"><span data-stu-id="8396d-170">250 MB per second</span></span> | <span data-ttu-id="8396d-171">Saniye başına 250 MB</span><span class="sxs-lookup"><span data-stu-id="8396d-171">250 MB per second</span></span> |

<span data-ttu-id="8396d-172">İş yükünüz bağlı olarak, ek veri disklerinin VM için gerekli olup olmadığını belirleyin.</span><span class="sxs-lookup"><span data-stu-id="8396d-172">Depending on your workload, determine if additional data disks are necessary for your VM.</span></span> <span data-ttu-id="8396d-173">Birkaç kalıcı veri diskleri tooyour VM ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8396d-173">You can attach several persistent data disks tooyour VM.</span></span> <span data-ttu-id="8396d-174">Gerekirse, hello diskleri tooincrease hello kapasite ve performans hello birimin arasında şeritler.</span><span class="sxs-lookup"><span data-stu-id="8396d-174">If needed, you can stripe across hello disks tooincrease hello capacity and performance of hello volume.</span></span> <span data-ttu-id="8396d-175">(Disk şeritleme görmek [burada](storage-premium-storage-performance.md#disk-striping).) Premium depolama veri diskleri kullanarak şeritler varsa [depolama alanları][4], kullanılan her disk için bir sütun ile yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="8396d-175">(See what is Disk Striping [here](storage-premium-storage-performance.md#disk-striping).) If you stripe Premium Storage data disks using [Storage Spaces][4], you should configure it with one column for each disk that is used.</span></span> <span data-ttu-id="8396d-176">Aksi takdirde, hello genel hello şeritli birim performansını trafiği toouneven dağıtım hello disklerde beklenenden daha düşük olabilir.</span><span class="sxs-lookup"><span data-stu-id="8396d-176">Otherwise, hello overall performance of hello striped volume may be lower than expected due toouneven distribution of traffic across hello disks.</span></span> <span data-ttu-id="8396d-177">Linux VM'ler için hello kullanabilirsiniz *mdadm* yardımcı programı tooachieve hello aynı.</span><span class="sxs-lookup"><span data-stu-id="8396d-177">For Linux VMs you can use hello *mdadm* utility tooachieve hello same.</span></span> <span data-ttu-id="8396d-178">Makalesine bakın [yapılandırma yazılım RAID Linux'ta](../../virtual-machines/linux/configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="8396d-178">See article [Configure Software RAID on Linux](../../virtual-machines/linux/configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for details.</span></span>

#### <a name="storage-account-scalability-targets"></a><span data-ttu-id="8396d-179">Depolama hesabımın ölçeklenebilirlik hedefleri</span><span class="sxs-lookup"><span data-stu-id="8396d-179">Storage account scalability targets</span></span>
<span data-ttu-id="8396d-180">Premium depolama hesapları ekleme toohello ölçeklenebilirlik hedeflerini izleyerek hello sahip [Azure Storage ölçeklenebilirlik ve performans hedefleri](storage-scalability-targets.md).</span><span class="sxs-lookup"><span data-stu-id="8396d-180">Premium Storage accounts have hello following scalability targets in addition toohello [Azure Storage Scalability and Performance Targets](storage-scalability-targets.md).</span></span> <span data-ttu-id="8396d-181">Uygulamanızın gereksinimleri tek bir depolama hesabına hello ölçeklenebilirlik hedefleri aşarsa, uygulama toouse birden çok depolama hesabı oluşturun ve bu depolama hesaplarında verilerinizi bölüm.</span><span class="sxs-lookup"><span data-stu-id="8396d-181">If your application requirements exceed hello scalability targets of a single storage account, build your application toouse multiple storage accounts, and partition your data across those storage accounts.</span></span>

| <span data-ttu-id="8396d-182">Toplam hesabı kapasitesi</span><span class="sxs-lookup"><span data-stu-id="8396d-182">Total Account Capacity</span></span> | <span data-ttu-id="8396d-183">Yerel olarak yedekli depolama hesabı için toplam bant genişliği</span><span class="sxs-lookup"><span data-stu-id="8396d-183">Total Bandwidth for a Locally Redundant Storage Account</span></span> |
|:--- |:--- |
| <span data-ttu-id="8396d-184">Disk kapasitesi: 35TB</span><span class="sxs-lookup"><span data-stu-id="8396d-184">Disk capacity: 35TB</span></span><br /><span data-ttu-id="8396d-185">Kapasite anlık görüntü: 10 TB</span><span class="sxs-lookup"><span data-stu-id="8396d-185">Snapshot capacity: 10 TB</span></span> |<span data-ttu-id="8396d-186">Gelen + giden için saniye başına too50 Gigabit</span><span class="sxs-lookup"><span data-stu-id="8396d-186">Up too50 gigabits per second for Inbound + Outbound</span></span> |

<span data-ttu-id="8396d-187">Merhaba Premium depolama özellikleri hakkında daha fazla bilgi için kullanıma [ölçeklenebilirlik ve performans Premium depolama kullanırken hedefleri](storage-premium-storage.md#scalability-and-performance-targets).</span><span class="sxs-lookup"><span data-stu-id="8396d-187">For hello more information on Premium Storage specifications, check out [Scalability and Performance Targets when using Premium Storage](storage-premium-storage.md#scalability-and-performance-targets).</span></span>

#### <a name="disk-caching-policy"></a><span data-ttu-id="8396d-188">Önbellek İlkesi disk</span><span class="sxs-lookup"><span data-stu-id="8396d-188">Disk caching policy</span></span>
<span data-ttu-id="8396d-189">Varsayılan olarak, ilke önbelleğe alma disktir *salt okunur* tüm Premium diskleri hello için ve *okuma-yazma* hello Premium işletim sistemi diski için toohello VM bağlı.</span><span class="sxs-lookup"><span data-stu-id="8396d-189">By default, disk caching policy is *Read-Only* for all hello Premium data disks, and *Read-Write* for hello Premium operating system disk attached toohello VM.</span></span> <span data-ttu-id="8396d-190">Bu yapılandırma ayarının tooachieve hello en iyi performans için uygulamanızın IOs önerilir.</span><span class="sxs-lookup"><span data-stu-id="8396d-190">This configuration setting is recommended tooachieve hello optimal performance for your application's IOs.</span></span> <span data-ttu-id="8396d-191">(SQL Server günlük dosyaları gibi) ağır yazma ya da salt yazılır veri diskleri için daha iyi uygulama performansı elde etmek için disk önbelleğe almayı devre dışı bırakın.</span><span class="sxs-lookup"><span data-stu-id="8396d-191">For write-heavy or write-only data disks (such as SQL Server log files), disable disk caching so that you can achieve better application performance.</span></span> <span data-ttu-id="8396d-192">mevcut veri diskleri için Hello önbellek ayarlarını kullanarak güncelleştirilebilir [Azure Portal](https://portal.azure.com) veya hello *- HostCaching* hello parametresinin *kümesi AzureDataDisk* cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="8396d-192">hello cache settings for existing data disks can be updated using [Azure Portal](https://portal.azure.com) or hello *-HostCaching* parameter of hello *Set-AzureDataDisk* cmdlet.</span></span>

#### <a name="location"></a><span data-ttu-id="8396d-193">Konum</span><span class="sxs-lookup"><span data-stu-id="8396d-193">Location</span></span>
<span data-ttu-id="8396d-194">Azure Premium Storage kullanılabilir olduğu bir konum seçin.</span><span class="sxs-lookup"><span data-stu-id="8396d-194">Pick a location where Azure Premium Storage is available.</span></span> <span data-ttu-id="8396d-195">Bkz: [bölgeye göre Azure Hizmetleri](https://azure.microsoft.com/regions/#services) kullanılabilir konumları hakkında güncel bilgi.</span><span class="sxs-lookup"><span data-stu-id="8396d-195">See [Azure Services by Region](https://azure.microsoft.com/regions/#services) for up-to-date information on available locations.</span></span> <span data-ttu-id="8396d-196">Sanal makineleri bulunan hello aynı depolama hesabı hello VM ayrı bölge içinde olup olmadığını daha çok daha iyi performans sağlayacaktır için depoları diskleri hello hello gibi bölge.</span><span class="sxs-lookup"><span data-stu-id="8396d-196">VMs located in hello same region as hello Storage account that stores hello disks for hello VM will give much better performance than if they are in separate regions.</span></span>

#### <a name="other-azure-vm-configuration-settings"></a><span data-ttu-id="8396d-197">Diğer Azure VM yapılandırma ayarları</span><span class="sxs-lookup"><span data-stu-id="8396d-197">Other Azure VM configuration settings</span></span>
<span data-ttu-id="8396d-198">Bir Azure VM oluşturulurken olacaktır belirli VM ayarları tooconfigure istedi.</span><span class="sxs-lookup"><span data-stu-id="8396d-198">When creating an Azure VM, you will be asked tooconfigure certain VM settings.</span></span> <span data-ttu-id="8396d-199">Değiştirme veya başkalarının daha sonra ekleme sırasında birkaç ayarlar hello VM hello ömrü boyunca sabit unutmayın.</span><span class="sxs-lookup"><span data-stu-id="8396d-199">Remember, few settings are fixed for hello lifetime of hello VM, while you can modify or add others later.</span></span> <span data-ttu-id="8396d-200">Bu Azure VM yapılandırma ayarlarını gözden geçirin ve bu olduğundan emin olun toomatch, iş yükü gereksinimlerinize uygun şekilde yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="8396d-200">Review these Azure VM configuration settings and make sure that these are configured appropriately toomatch your workload requirements.</span></span>

### <a name="optimization"></a><span data-ttu-id="8396d-201">İyileştirme</span><span class="sxs-lookup"><span data-stu-id="8396d-201">Optimization</span></span>
<span data-ttu-id="8396d-202">[Azure Premium Storage: Tasarım için yüksek performanslı](storage-premium-storage-performance.md) Azure Premium Storage kullanarak yüksek performanslı uygulamalar oluşturmak için yönergeler sağlar.</span><span class="sxs-lookup"><span data-stu-id="8396d-202">[Azure Premium Storage: Design for High Performance](storage-premium-storage-performance.md) provides guidelines for building high-performance applications using Azure Premium Storage.</span></span> <span data-ttu-id="8396d-203">Uygulamanız tarafından kullanılan performansı en iyi uygulamalar uygulanabilir tootechnologies birlikte hello yönergeleri takip edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8396d-203">You can follow hello guidelines combined with performance best practices applicable tootechnologies used by your application.</span></span>

## <span data-ttu-id="8396d-204"><a name="prepare-and-copy-virtual-hard-disks-VHDs-to-premium-storage"></a>Hazırlama ve sanal sabit diskleri (VHD) tooPremium depolama kopyalayın</span><span class="sxs-lookup"><span data-stu-id="8396d-204"><a name="prepare-and-copy-virtual-hard-disks-VHDs-to-premium-storage"></a>Prepare and copy virtual hard disks (VHDs) tooPremium Storage</span></span>
<span data-ttu-id="8396d-205">bölümden hello VHD'ler, sanal makineden hazırlama ve VHD tooAzure depolama kopyalama için yönergeler sağlar.</span><span class="sxs-lookup"><span data-stu-id="8396d-205">hello following section provides guidelines for preparing VHDs from your VM and copying VHDs tooAzure Storage.</span></span>

* [<span data-ttu-id="8396d-206">Senaryo 1: "ı mevcut Azure VM'ler tooAzure Premium depolama geçirme."</span><span class="sxs-lookup"><span data-stu-id="8396d-206">Scenario 1: "I am migrating existing Azure VMs tooAzure Premium Storage."</span></span>](#scenario1)
* [<span data-ttu-id="8396d-207">Senaryo 2: "ı VM'ler diğer platformlar tooAzure Premium depolama geçirme."</span><span class="sxs-lookup"><span data-stu-id="8396d-207">Scenario 2: "I am migrating VMs from other platforms tooAzure Premium Storage."</span></span>](#scenario2)

### <a name="prerequisites"></a><span data-ttu-id="8396d-208">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="8396d-208">Prerequisites</span></span>
<span data-ttu-id="8396d-209">tooprepare hello VHD'ler geçiş için ihtiyacınız vardır:</span><span class="sxs-lookup"><span data-stu-id="8396d-209">tooprepare hello VHDs for migration, you'll need:</span></span>

* <span data-ttu-id="8396d-210">Bir Azure aboneliği, bir depolama hesabı ve kapsayıcı, depolama, VHD kopyalayabilirsiniz toowhich hesap.</span><span class="sxs-lookup"><span data-stu-id="8396d-210">An Azure subscription, a storage account, and a container in that storage account toowhich you can copy your VHD.</span></span> <span data-ttu-id="8396d-211">Merhaba hedef depolama hesabının bir standart veya Premium depolama hesabı ihtiyacınıza olabileceğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="8396d-211">Note that hello destination storage account can be a Standard or Premium Storage account depending on your requirement.</span></span>
* <span data-ttu-id="8396d-212">Bir aracı toogeneralize hello dışarı birden çok VM örnekleri toocreate düşünüyorsanız, VHD.</span><span class="sxs-lookup"><span data-stu-id="8396d-212">A tool toogeneralize hello VHD if you plan toocreate multiple VM instances from it.</span></span> <span data-ttu-id="8396d-213">Örneğin, sysprep Windows ya da Sanal Küp Str sysprep Ubuntu için.</span><span class="sxs-lookup"><span data-stu-id="8396d-213">For example, sysprep for Windows or virt-sysprep for Ubuntu.</span></span>
* <span data-ttu-id="8396d-214">Bir aracı tooupload hello VHD dosyası toohello depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="8396d-214">A tool tooupload hello VHD file toohello Storage account.</span></span> <span data-ttu-id="8396d-215">Bkz: [hello AzCopy komut satırı yardımcı programı ile veri aktarma](storage-use-azcopy.md) veya bir [Azure storage Gezgini](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx).</span><span class="sxs-lookup"><span data-stu-id="8396d-215">See [Transfer data with hello AzCopy Command-Line Utility](storage-use-azcopy.md) or use an [Azure storage explorer](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx).</span></span> <span data-ttu-id="8396d-216">Bu kılavuzda hello AzCopy aracını kullanarak, VHD kopyalama açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="8396d-216">This guide describes copying your VHD using hello AzCopy tool.</span></span>

> [!NOTE]
> <span data-ttu-id="8396d-217">AzCopy, en iyi performans için zaman uyumlu kopyası seçeneğiyle seçerseniz, VHD'yi Bu araçlardan birini hello olan bir Azure VM çalıştırarak kopyalayın hello hedef depolama hesabının aynı bölgede.</span><span class="sxs-lookup"><span data-stu-id="8396d-217">If you choose synchronous copy option with AzCopy, for optimal performance, copy your VHD by running one of these tools from an Azure VM that is in hello same region as hello destination storage account.</span></span> <span data-ttu-id="8396d-218">Bir VHD farklı bir bölgede bir Azure VM kopyalıyorsanız performansınızı daha yavaş olabilir.</span><span class="sxs-lookup"><span data-stu-id="8396d-218">If you are copying a VHD from an Azure VM in a different region, your performance may be slower.</span></span>
>
> <span data-ttu-id="8396d-219">Sınırlı bant genişliği üzerinde büyük miktarda veri kopyalama için göz önünde bulundurun [hello Azure içeri/dışarı aktarma hizmeti tootransfer veri tooBlob depolama kullanarak](../storage-import-export-service.md); tootransfer bu sayede verilerinizi sevkiyat sabit disk tarafından tooan Azure sürücüler Veri Merkezi.</span><span class="sxs-lookup"><span data-stu-id="8396d-219">For copying a large amount of data over limited bandwidth, consider [using hello Azure Import/Export service tootransfer data tooBlob Storage](../storage-import-export-service.md); this allows you tootransfer your data by shipping hard disk drives tooan Azure datacenter.</span></span> <span data-ttu-id="8396d-220">Hello Azure içeri/dışarı aktarma hizmeti toocopy veri tooa standart depolama hesabı yalnızca kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8396d-220">You can use hello Azure Import/Export service toocopy data tooa standard storage account only.</span></span> <span data-ttu-id="8396d-221">Standart depolama hesabınızdaki Hello veri olduktan sonra her iki hello kullanabilirsiniz [kopyalama Blob API](https://msdn.microsoft.com/library/azure/dd894037.aspx) veya AzCopy tootransfer hello veri tooyour premium depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="8396d-221">Once hello data is in your standard storage account, you can use either hello [Copy Blob API](https://msdn.microsoft.com/library/azure/dd894037.aspx) or AzCopy tootransfer hello data tooyour premium storage account.</span></span>
>
> <span data-ttu-id="8396d-222">Microsoft Azure yalnızca sabit boyutlu VHD dosyalarını desteklediğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="8396d-222">Note that Microsoft Azure only supports fixed size VHD files.</span></span> <span data-ttu-id="8396d-223">VHDX dosyaları veya dinamik VHD desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="8396d-223">VHDX files or dynamic VHDs are not supported.</span></span> <span data-ttu-id="8396d-224">Dinamik VHD varsa, hello kullanarak toofixed boyutunu dönüştürebilirsiniz [Convert-VHD](http://technet.microsoft.com/library/hh848454.aspx) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="8396d-224">If you have a dynamic VHD, you can convert it toofixed size using hello [Convert-VHD](http://technet.microsoft.com/library/hh848454.aspx) cmdlet.</span></span>
>
>

### <span data-ttu-id="8396d-225"><a name="scenario1"></a>Senaryo 1: "ı mevcut Azure VM'ler tooAzure Premium depolama geçirme."</span><span class="sxs-lookup"><span data-stu-id="8396d-225"><a name="scenario1"></a>Scenario 1: "I am migrating existing Azure VMs tooAzure Premium Storage."</span></span>
<span data-ttu-id="8396d-226">Azure VM'ler, Dur hello VM, varolan geçiriyorsanız istediğiniz VHD hello türü başına VHD'ler hazırlamak ve hello VHD AzCopy veya PowerShell ile kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="8396d-226">If you are migrating existing Azure VMs, stop hello VM, prepare VHDs per hello type of VHD you want, and then copy hello VHD with AzCopy or PowerShell.</span></span>

<span data-ttu-id="8396d-227">Merhaba VM tamamen toomigrate temiz bir duruma aşağı toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="8396d-227">hello VM needs toobe completely down toomigrate a clean state.</span></span> <span data-ttu-id="8396d-228">Merhaba Geçiş tamamlanana kadar bir kapalı kalma süresi olacaktır.</span><span class="sxs-lookup"><span data-stu-id="8396d-228">There will be a downtime until hello migration completes.</span></span>

#### <a name="step-1-prepare-vhds-for-migration"></a><span data-ttu-id="8396d-229">1. Adım</span><span class="sxs-lookup"><span data-stu-id="8396d-229">Step 1.</span></span> <span data-ttu-id="8396d-230">VHD'ler geçiş için hazırlama</span><span class="sxs-lookup"><span data-stu-id="8396d-230">Prepare VHDs for migration</span></span>
<span data-ttu-id="8396d-231">Var olan Azure Vm'leri tooPremium depolama geçiriyorsanız, VHD olabilir:</span><span class="sxs-lookup"><span data-stu-id="8396d-231">If you are migrating existing Azure VMs tooPremium Storage, your VHD may be:</span></span>

* <span data-ttu-id="8396d-232">Genelleştirilmiş işletim sistemi görüntüsü</span><span class="sxs-lookup"><span data-stu-id="8396d-232">A generalized operating system image</span></span>
* <span data-ttu-id="8396d-233">Benzersiz işletim sistemi diski</span><span class="sxs-lookup"><span data-stu-id="8396d-233">A unique operating system disk</span></span>
* <span data-ttu-id="8396d-234">Bir veri diski</span><span class="sxs-lookup"><span data-stu-id="8396d-234">A data disk</span></span>

<span data-ttu-id="8396d-235">Aşağıda Biz bu 3 senaryolar için VHD hazırlama yol.</span><span class="sxs-lookup"><span data-stu-id="8396d-235">Below we walk through these 3 scenarios for preparing your VHD.</span></span>

##### <a name="use-a-generalized-operating-system-vhd-toocreate-multiple-vm-instances"></a><span data-ttu-id="8396d-236">Birden çok VM örnekleri genelleştirilmiş bir işletim sistemi VHD toocreate kullanın</span><span class="sxs-lookup"><span data-stu-id="8396d-236">Use a generalized Operating System VHD toocreate multiple VM instances</span></span>
<span data-ttu-id="8396d-237">Birden çok genel Azure VM örnekleri kullanılan toocreate olacak VHD yüklüyorsanız, sysprep yardımcı programını kullanarak VHD generalize gerekir.</span><span class="sxs-lookup"><span data-stu-id="8396d-237">If you are uploading a VHD that will be used toocreate multiple generic Azure VM instances, you must first generalize VHD using a sysprep utility.</span></span> <span data-ttu-id="8396d-238">Bu tooa şirket içi VHD uygulanır veya hello bulutta.</span><span class="sxs-lookup"><span data-stu-id="8396d-238">This applies tooa VHD that is on-premises or in hello cloud.</span></span> <span data-ttu-id="8396d-239">Sysprep VHD hello tüm makine özgü bilgileri kaldırır.</span><span class="sxs-lookup"><span data-stu-id="8396d-239">Sysprep removes any machine-specific information from hello VHD.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8396d-240">Bir anlık görüntüsünü veya genelleme önce VM'yi yedekleme.</span><span class="sxs-lookup"><span data-stu-id="8396d-240">Take a snapshot or backup your VM before generalizing it.</span></span> <span data-ttu-id="8396d-241">Çalışan sysprep durdurun ve hello VM örneğine serbest bırakma.</span><span class="sxs-lookup"><span data-stu-id="8396d-241">Running sysprep will stop and deallocate hello VM instance.</span></span> <span data-ttu-id="8396d-242">Windows işletim sistemi VHD toosysprep adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="8396d-242">Follow steps below toosysprep a Windows OS VHD.</span></span> <span data-ttu-id="8396d-243">Hello Sysprep komutunu çalıştırarak tooshut hello sanal makine kapalı gerektirir olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="8396d-243">Note that running hello Sysprep command will require you tooshut down hello virtual machine.</span></span> <span data-ttu-id="8396d-244">Sysprep hakkında daha fazla bilgi için bkz: [Sysprep genel bakış](http://technet.microsoft.com/library/hh825209.aspx) veya [Sysprep Teknik Başvurusu](http://technet.microsoft.com/library/cc766049.aspx).</span><span class="sxs-lookup"><span data-stu-id="8396d-244">For more information about Sysprep, see [Sysprep Overview](http://technet.microsoft.com/library/hh825209.aspx) or [Sysprep Technical Reference](http://technet.microsoft.com/library/cc766049.aspx).</span></span>
>
>

1. <span data-ttu-id="8396d-245">Yönetici olarak bir komut istemi penceresi açın.</span><span class="sxs-lookup"><span data-stu-id="8396d-245">Open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="8396d-246">Komut tooopen Sysprep aşağıdaki hello girin:</span><span class="sxs-lookup"><span data-stu-id="8396d-246">Enter hello following command tooopen Sysprep:</span></span>

    ```
    %windir%\system32\sysprep\sysprep.exe
    ```

3. <span data-ttu-id="8396d-247">Hello Sistem Hazırlama aracı, select girin sistem Out-of-Box deneyimi (OOBE) select hello Generalize onay kutusunu seçin **kapatma**ve ardından **Tamam**hello resimde gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="8396d-247">In hello System Preparation Tool, select Enter System Out-of-Box Experience (OOBE), select hello Generalize check box, select **Shutdown**, and then click **OK**, as shown in hello image below.</span></span> <span data-ttu-id="8396d-248">Sysprep hello işletim sistemini genelleştirir ve hello Sistemi kapat.</span><span class="sxs-lookup"><span data-stu-id="8396d-248">Sysprep will generalize hello operating system and shut down hello system.</span></span>

    ![][1]

<span data-ttu-id="8396d-249">Bir Ubuntu VM için kullanım Sanal Küp Str sysprep tooachieve hello aynı.</span><span class="sxs-lookup"><span data-stu-id="8396d-249">For an Ubuntu VM, use virt-sysprep tooachieve hello same.</span></span> <span data-ttu-id="8396d-250">Bkz: [Sanal Küp Str sysprep](http://manpages.ubuntu.com/manpages/precise/man1/virt-sysprep.1.html) daha fazla ayrıntı için.</span><span class="sxs-lookup"><span data-stu-id="8396d-250">See [virt-sysprep](http://manpages.ubuntu.com/manpages/precise/man1/virt-sysprep.1.html) for more details.</span></span> <span data-ttu-id="8396d-251">Ayrıca bazı hello açık kaynak bkz [sunucu Linux sağlama yazılım](http://www.cyberciti.biz/tips/server-provisioning-software.html) diğer Linux işletim sistemleri için.</span><span class="sxs-lookup"><span data-stu-id="8396d-251">See also some of hello open source [Linux Server Provisioning software](http://www.cyberciti.biz/tips/server-provisioning-software.html) for other Linux operating systems.</span></span>

##### <a name="use-a-unique-operating-system-vhd-toocreate-a-single-vm-instance"></a><span data-ttu-id="8396d-252">Benzersiz bir işletim sistemi VHD toocreate tek bir VM örneği kullanın</span><span class="sxs-lookup"><span data-stu-id="8396d-252">Use a unique Operating System VHD toocreate a single VM instance</span></span>
<span data-ttu-id="8396d-253">Merhaba hello makine belirli veri gerektiren VM üzerinde çalışan bir uygulamanız varsa, hello VHD generalize değil.</span><span class="sxs-lookup"><span data-stu-id="8396d-253">If you have an application running on hello VM which requires hello machine specific data, do not generalize hello VHD.</span></span> <span data-ttu-id="8396d-254">Genelleştirilmiş olmayan bir VHD kullanılan toocreate benzersiz bir Azure VM örneği olabilir.</span><span class="sxs-lookup"><span data-stu-id="8396d-254">A non-generalized VHD can be used toocreate a unique Azure VM instance.</span></span> <span data-ttu-id="8396d-255">VHD etki alanı denetleyicisi varsa, örneğin, sysprep yürütülürken, bir etki alanı denetleyicisi olarak etkisiz hale getirir.</span><span class="sxs-lookup"><span data-stu-id="8396d-255">For example, if you have Domain Controller on your VHD, executing sysprep will make it ineffective as a Domain Controller.</span></span> <span data-ttu-id="8396d-256">Sysprep hello VHD genelleme önce bunlar üzerinde çalışan VM ve hello etkisi çalışan hello uygulamaları gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="8396d-256">Review hello applications running on your VM and hello impact of running sysprep on them before generalizing hello VHD.</span></span>

##### <a name="register-data-disk-vhd"></a><span data-ttu-id="8396d-257">Veri diski VHD kaydetme</span><span class="sxs-lookup"><span data-stu-id="8396d-257">Register data disk VHD</span></span>
<span data-ttu-id="8396d-258">Varsa Azure toobe'ndeki veri disklerinin geçişi, diskleri kapatma bu verileri kullanmak emin hello VM'ler yapmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="8396d-258">If you have data disks in Azure toobe migrated, you must make sure hello VMs that use these data disks are shut down.</span></span>

<span data-ttu-id="8396d-259">Premium depolama toocopy VHD tooAzure açıklanan başlangıç adımları izleyin ve sağlanan veri diski olarak kaydedin.</span><span class="sxs-lookup"><span data-stu-id="8396d-259">Follow hello steps described below toocopy VHD tooAzure Premium Storage and register it as a provisioned data disk.</span></span>

#### <a name="step-2-create-hello-destination-for-your-vhd"></a><span data-ttu-id="8396d-260">2. Adım</span><span class="sxs-lookup"><span data-stu-id="8396d-260">Step 2.</span></span> <span data-ttu-id="8396d-261">Merhaba hedef, VHD için oluşturma</span><span class="sxs-lookup"><span data-stu-id="8396d-261">Create hello destination for your VHD</span></span>
<span data-ttu-id="8396d-262">Vhd'lerinizi korumak için bir depolama hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8396d-262">Create a storage account for maintaining your VHDs.</span></span> <span data-ttu-id="8396d-263">Merhaba where planlarken aşağıdaki noktaları göz önünde bulundurun toostore Vhd'lerinizi:</span><span class="sxs-lookup"><span data-stu-id="8396d-263">Consider hello following points when planning where toostore your VHDs:</span></span>

* <span data-ttu-id="8396d-264">Merhaba hedef Premium depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="8396d-264">hello target Premium storage account.</span></span>
* <span data-ttu-id="8396d-265">Merhaba depolama hesap konumu Premium depolama özellikli Azure hello Son aşamada oluşturacak VM'ler ile aynı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="8396d-265">hello storage account location must be same as Premium Storage capable Azure VMs you will create in hello final stage.</span></span> <span data-ttu-id="8396d-266">Tooa yeni depolama hesabı ya da aynı depolama hesabındaki gereksinimlerinize göre plan toouse hello kopyalamak.</span><span class="sxs-lookup"><span data-stu-id="8396d-266">You could copy tooa new storage account, or plan toouse hello same storage account based on your needs.</span></span>
* <span data-ttu-id="8396d-267">Kopyalayın ve hello depolama hesabı anahtarı hello hedef depolama hesabının hello sonraki aşaması için kaydedin.</span><span class="sxs-lookup"><span data-stu-id="8396d-267">Copy and save hello storage account key of hello destination storage account for hello next stage.</span></span>

<span data-ttu-id="8396d-268">Veri diskleri için bir standart depolama hesabı (örneğin, için depolama alanına sahip diskler) bazı veri diskleri tookeep seçebilirsiniz, ancak, üretim iş yükü toouse premium depolama için tüm verilerin taşınması önerilir.</span><span class="sxs-lookup"><span data-stu-id="8396d-268">For data disks, you can choose tookeep some data disks in a standard storage account (for example, disks that have cooler storage), but we strongly recommend you moving all data for production workload toouse premium storage.</span></span>

#### <span data-ttu-id="8396d-269"><a name="copy-vhd-with-azcopy-or-powershell"></a>3. adım.</span><span class="sxs-lookup"><span data-stu-id="8396d-269"><a name="copy-vhd-with-azcopy-or-powershell"></a>Step 3.</span></span> <span data-ttu-id="8396d-270">VHD AzCopy veya PowerShell ile kopyalama</span><span class="sxs-lookup"><span data-stu-id="8396d-270">Copy VHD with AzCopy or PowerShell</span></span>
<span data-ttu-id="8396d-271">Kapsayıcı yolu ve bu iki seçenekten biri anahtar tooprocess hesap depolama toofind gerekir.</span><span class="sxs-lookup"><span data-stu-id="8396d-271">You will need toofind your container path and storage account key tooprocess either of these two options.</span></span> <span data-ttu-id="8396d-272">Kapsayıcı yolu ve depolama hesabı anahtarı bulunabilir **Azure Portal** > **depolama**.</span><span class="sxs-lookup"><span data-stu-id="8396d-272">Container path and storage account key can be found in **Azure Portal** > **Storage**.</span></span> <span data-ttu-id="8396d-273">Merhaba kapsayıcı URL "gibi https://myaccount.blob.core.windows.net/mycontainer/" olacaktır.</span><span class="sxs-lookup"><span data-stu-id="8396d-273">hello container URL will be like "https://myaccount.blob.core.windows.net/mycontainer/".</span></span>

##### <a name="option-1-copy-a-vhd-with-azcopy-asynchronous-copy"></a><span data-ttu-id="8396d-274">Seçenek 1: bir VHD AzCopy (zaman uyumsuz kopya) ile kopyalama</span><span class="sxs-lookup"><span data-stu-id="8396d-274">Option 1: Copy a VHD with AzCopy (Asynchronous copy)</span></span>
<span data-ttu-id="8396d-275">AzCopy kullanarak hello VHD hello Internet üzerinden kolayca karşıya yükleyebilir.</span><span class="sxs-lookup"><span data-stu-id="8396d-275">Using AzCopy, you can easily upload hello VHD over hello Internet.</span></span> <span data-ttu-id="8396d-276">Merhaba VHD'ler Hello boyutuna bağlı olarak, bu zaman alabilir.</span><span class="sxs-lookup"><span data-stu-id="8396d-276">Depending on hello size of hello VHDs, this may take time.</span></span> <span data-ttu-id="8396d-277">Bu seçenek kullanıldığında toocheck hello depolama hesabı giriş/çıkış sınırları unutmayın.</span><span class="sxs-lookup"><span data-stu-id="8396d-277">Remember toocheck hello storage account ingress/egress limits when using this option.</span></span> <span data-ttu-id="8396d-278">Bkz: [Azure Storage ölçeklenebilirlik ve performans hedefleri](storage-scalability-targets.md) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="8396d-278">See [Azure Storage Scalability and Performance Targets](storage-scalability-targets.md) for details.</span></span>

1. <span data-ttu-id="8396d-279">AzCopy buradan yükleyip: [en güncel AzCopy sürümünü](http://aka.ms/downloadazcopy)</span><span class="sxs-lookup"><span data-stu-id="8396d-279">Download and install AzCopy from here: [Latest version of AzCopy](http://aka.ms/downloadazcopy)</span></span>
2. <span data-ttu-id="8396d-280">Azure PowerShell ve AzCopy yüklendiği gidin toohello klasörünü açın.</span><span class="sxs-lookup"><span data-stu-id="8396d-280">Open Azure PowerShell and go toohello folder where AzCopy is installed.</span></span>
3. <span data-ttu-id="8396d-281">Kullanım hello şu komutu toocopy hello VHD "Kaynak" dosyasından çok "Hedef".</span><span class="sxs-lookup"><span data-stu-id="8396d-281">Use hello following command toocopy hello VHD file from "Source" too"Destination".</span></span>

    ```azcopy
    AzCopy /Source: <source> /SourceKey: <source-account-key> /Dest: <destination> /DestKey: <dest-account-key> /BlobType:page /Pattern: <file-name>
    ```

    <span data-ttu-id="8396d-282">Örnek:</span><span class="sxs-lookup"><span data-stu-id="8396d-282">Example:</span></span>

    ```azcopy
    AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /SourceKey:key1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /DestKey:key2 /Pattern:abc.vhd
    ```

    <span data-ttu-id="8396d-283">Açıklamaları hello AzCopy komut kullanılan hello Parametreler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="8396d-283">Here are descriptions of hello parameters used in hello AzCopy command:</span></span>

   * <span data-ttu-id="8396d-284">**/ Kaynak:  *&lt;kaynak&gt;:***  hello klasör veya hello VHD'yi içeren depolama kapsayıcısı URL konumu.</span><span class="sxs-lookup"><span data-stu-id="8396d-284">**/Source: *&lt;source&gt;:*** Location of hello folder or storage container URL that contains hello VHD.</span></span>
   * <span data-ttu-id="8396d-285">**/ SourceKey:  *&lt;kaynak hesap anahtarı&gt;:***  hello kaynak depolama hesabının depolama hesabı anahtarı.</span><span class="sxs-lookup"><span data-stu-id="8396d-285">**/SourceKey: *&lt;source-account-key&gt;:*** Storage account key of hello source storage account.</span></span>
   * <span data-ttu-id="8396d-286">**/ Taşınmaya:  *&lt;hedef&gt;:***  depolama kapsayıcısı URL toocopy hello VHD'ye.</span><span class="sxs-lookup"><span data-stu-id="8396d-286">**/Dest: *&lt;destination&gt;:*** Storage container URL toocopy hello VHD to.</span></span>
   * <span data-ttu-id="8396d-287">**/ DestKey:  *&lt;hedef hesap anahtarı&gt;:***  hello hedef depolama hesabının depolama hesabı anahtarı.</span><span class="sxs-lookup"><span data-stu-id="8396d-287">**/DestKey: *&lt;dest-account-key&gt;:*** Storage account key of hello destination storage account.</span></span>
   * <span data-ttu-id="8396d-288">**/ Deseni:  *&lt;dosya adı&gt;:***  hello VHD toocopy hello dosya adı belirtin.</span><span class="sxs-lookup"><span data-stu-id="8396d-288">**/Pattern: *&lt;file-name&gt;:*** Specify hello file name of hello VHD toocopy.</span></span>

<span data-ttu-id="8396d-289">Aracı AzCopy kullanımıyla ilgili ayrıntılar için bkz: [hello AzCopy komut satırı yardımcı programı ile veri aktarma](storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="8396d-289">For details on using AzCopy tool, see [Transfer data with hello AzCopy Command-Line Utility](storage-use-azcopy.md).</span></span>

##### <a name="option-2-copy-a-vhd-with-powershell-synchronized-copy"></a><span data-ttu-id="8396d-290">Seçenek 2: bir VHD PowerShell (Synchronızed kopya) ile kopyalama</span><span class="sxs-lookup"><span data-stu-id="8396d-290">Option 2: Copy a VHD with PowerShell (Synchronized copy)</span></span>
<span data-ttu-id="8396d-291">Ayrıca, başlangıç AzureStorageBlobCopy hello PowerShell cmdlet'ini kullanarak hello VHD dosyasını kopyalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8396d-291">You can also copy hello VHD file using hello PowerShell cmdlet Start-AzureStorageBlobCopy.</span></span> <span data-ttu-id="8396d-292">Azure PowerShell toocopy VHD komutu aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="8396d-292">Use hello following command on Azure PowerShell toocopy VHD.</span></span> <span data-ttu-id="8396d-293">Kaynak ve hedef depolama hesabınız karşılık gelen değerlerle <> Hello değerleri değiştirin.</span><span class="sxs-lookup"><span data-stu-id="8396d-293">Replace hello values in <> with corresponding values from your source and destination storage account.</span></span> <span data-ttu-id="8396d-294">toouse bu komut, hedef depolama hesabınız VHD adlı bir kapsayıcıya sahip olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8396d-294">toouse this command, you must have a container called vhds in your destination storage account.</span></span> <span data-ttu-id="8396d-295">Merhaba kapsayıcı yoksa, hello komutu çalıştırmadan önce oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8396d-295">If hello container doesn't exist, create one before running hello command.</span></span>

```powershell
$sourceBlobUri = <source-vhd-uri>

$sourceContext = New-AzureStorageContext  –StorageAccountName <source-account> -StorageAccountKey <source-account-key>

$destinationContext = New-AzureStorageContext  –StorageAccountName <dest-account> -StorageAccountKey <dest-account-key>

Start-AzureStorageBlobCopy -srcUri $sourceBlobUri -SrcContext $sourceContext -DestContainer <dest-container> -DestBlob <dest-disk-name> -DestContext $destinationContext
```

<span data-ttu-id="8396d-296">Örnek:</span><span class="sxs-lookup"><span data-stu-id="8396d-296">Example:</span></span>

```powershell
C:\PS> $sourceBlobUri = "https://sourceaccount.blob.core.windows.net/vhds/myvhd.vhd"

C:\PS> $sourceContext = New-AzureStorageContext  –StorageAccountName "sourceaccount" -StorageAccountKey "J4zUI9T5b8gvHohkiRg"

C:\PS> $destinationContext = New-AzureStorageContext  –StorageAccountName "destaccount" -StorageAccountKey "XZTmqSGKUYFSh7zB5"

C:\PS> Start-AzureStorageBlobCopy -srcUri $sourceBlobUri -SrcContext $sourceContext -DestContainer "vhds" -DestBlob "myvhd.vhd" -DestContext $destinationContext
```

### <span data-ttu-id="8396d-297"><a name="scenario2"></a>Senaryo 2: "ı VM'ler diğer platformlar tooAzure Premium depolama geçirme."</span><span class="sxs-lookup"><span data-stu-id="8396d-297"><a name="scenario2"></a>Scenario 2: "I am migrating VMs from other platforms tooAzure Premium Storage."</span></span>
<span data-ttu-id="8396d-298">Azure bulut depolama tooAzure VHD geçiriyorsanız, hello VHD tooa yerel dizin dışarı aktarmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="8396d-298">If you are migrating VHD from non-Azure Cloud Storage tooAzure, you must first export hello VHD tooa local directory.</span></span> <span data-ttu-id="8396d-299">VHD depolandığı kullanışlı hello yerel dizin Hello tam kaynak yolu varsa ve AzCopy tooupload kullanarak onu tooAzure depolama.</span><span class="sxs-lookup"><span data-stu-id="8396d-299">Have hello complete source path of hello local directory where VHD is stored handy, and then using AzCopy tooupload it tooAzure Storage.</span></span>

#### <a name="step-1-export-vhd-tooa-local-directory"></a><span data-ttu-id="8396d-300">1. Adım</span><span class="sxs-lookup"><span data-stu-id="8396d-300">Step 1.</span></span> <span data-ttu-id="8396d-301">VHD tooa yerel dizin dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="8396d-301">Export VHD tooa local directory</span></span>
##### <a name="copy-a-vhd-from-aws"></a><span data-ttu-id="8396d-302">Bir VHD'yi AWS kopyalayın</span><span class="sxs-lookup"><span data-stu-id="8396d-302">Copy a VHD from AWS</span></span>
1. <span data-ttu-id="8396d-303">AWS kullanıyorsanız, hello EC2 örneği tooa bir Amazon S3 demetini VHD'yi verin.</span><span class="sxs-lookup"><span data-stu-id="8396d-303">If you are using AWS, export hello EC2 instance tooa VHD in an Amazon S3 bucket.</span></span> <span data-ttu-id="8396d-304">Hello dışarı aktarma Amazon EC2 örnekleri tooinstall hello Amazon EC2 komut satırı arabirimi (CLI) aracı Amazon belgelerine açıklanan başlangıç adımları izleyin ve hello-örnek-export-Görev Oluştur komutu tooexport hello EC2 örneği tooa VHD dosyasını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="8396d-304">Follow hello steps described in hello Amazon documentation for Exporting Amazon EC2 Instances tooinstall hello Amazon EC2 command-line interface (CLI) tool and run hello create-instance-export-task command tooexport hello EC2 instance tooa VHD file.</span></span> <span data-ttu-id="8396d-305">Emin toouse olması **VHD** hello DISK &#95; görüntü &#95; Merhaba çalıştırırken biçimi değişkeni **-örnek-export-görev oluştur** komutu.</span><span class="sxs-lookup"><span data-stu-id="8396d-305">Be sure toouse **VHD** for hello DISK&#95;IMAGE&#95;FORMAT variable when running hello **create-instance-export-task** command.</span></span> <span data-ttu-id="8396d-306">Merhaba dışarı aktarılan VHD dosyasının bu işlem sırasında belirttiğiniz hello Amazon S3 demetini kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="8396d-306">hello exported VHD file is saved in hello Amazon S3 bucket you designate during that process.</span></span>

    ```
    aws ec2 create-instance-export-task --instance-id ID --target-environment TARGET_ENVIRONMENT \
      --export-to-s3-task DiskImageFormat=DISK_IMAGE_FORMAT,ContainerFormat=ova,S3Bucket=BUCKET,S3Prefix=PREFIX
    ```

2. <span data-ttu-id="8396d-307">Merhaba S3 demetini Hello VHD dosyasını indirin.</span><span class="sxs-lookup"><span data-stu-id="8396d-307">Download hello VHD file from hello S3 bucket.</span></span> <span data-ttu-id="8396d-308">Select hello VHD dosyasını, ardından **Eylemler** > **karşıdan**.</span><span class="sxs-lookup"><span data-stu-id="8396d-308">Select hello VHD file, then **Actions** > **Download**.</span></span>

    ![][3]

##### <a name="copy-a-vhd-from-other-non-azure-cloud"></a><span data-ttu-id="8396d-309">Bir VHD'yi diğer Azure olmayan buluttan kopyalayın</span><span class="sxs-lookup"><span data-stu-id="8396d-309">Copy a VHD from other non-Azure cloud</span></span>
<span data-ttu-id="8396d-310">Azure bulut depolama tooAzure VHD geçiriyorsanız, hello VHD tooa yerel dizin dışarı aktarmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="8396d-310">If you are migrating VHD from non-Azure Cloud Storage tooAzure, you must first export hello VHD tooa local directory.</span></span> <span data-ttu-id="8396d-311">Hello tam kaynak yolu VHD depolandığı hello yerel dizine kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="8396d-311">Copy hello complete source path of hello local directory where VHD is stored.</span></span>

##### <a name="copy-a-vhd-from-on-premises"></a><span data-ttu-id="8396d-312">Şirket içi bir VHD'yi kopyalayın</span><span class="sxs-lookup"><span data-stu-id="8396d-312">Copy a VHD from on-premises</span></span>
<span data-ttu-id="8396d-313">Bir şirket içi ortamından VHD geçiriyorsanız, VHD depolandığı hello tam kaynak yolu gerekir.</span><span class="sxs-lookup"><span data-stu-id="8396d-313">If you are migrating VHD from an on-premises environment, you will need hello complete source path where VHD is stored.</span></span> <span data-ttu-id="8396d-314">Merhaba kaynak yolu, bir sunucu konumu veya dosya paylaşımı olabilir.</span><span class="sxs-lookup"><span data-stu-id="8396d-314">hello source path could be a server location or file share.</span></span>

#### <a name="step-2-create-hello-destination-for-your-vhd"></a><span data-ttu-id="8396d-315">2. Adım</span><span class="sxs-lookup"><span data-stu-id="8396d-315">Step 2.</span></span> <span data-ttu-id="8396d-316">Merhaba hedef, VHD için oluşturma</span><span class="sxs-lookup"><span data-stu-id="8396d-316">Create hello destination for your VHD</span></span>
<span data-ttu-id="8396d-317">Vhd'lerinizi korumak için bir depolama hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8396d-317">Create a storage account for maintaining your VHDs.</span></span> <span data-ttu-id="8396d-318">Merhaba where planlarken aşağıdaki noktaları göz önünde bulundurun toostore Vhd'lerinizi:</span><span class="sxs-lookup"><span data-stu-id="8396d-318">Consider hello following points when planning where toostore your VHDs:</span></span>

* <span data-ttu-id="8396d-319">Merhaba hedef depolama hesabı, standart veya premium depolama uygulama ihtiyacınıza olabilir.</span><span class="sxs-lookup"><span data-stu-id="8396d-319">hello target storage account could be standard or premium storage depending on your application requirement.</span></span>
* <span data-ttu-id="8396d-320">Merhaba depolama hesabı bölgesi Premium depolama özellikli Azure hello Son aşamada oluşturacak VM'ler ile aynı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="8396d-320">hello storage account region must be same as Premium Storage capable Azure VMs you will create in hello final stage.</span></span> <span data-ttu-id="8396d-321">Tooa yeni depolama hesabı ya da aynı depolama hesabındaki gereksinimlerinize göre plan toouse hello kopyalamak.</span><span class="sxs-lookup"><span data-stu-id="8396d-321">You could copy tooa new storage account, or plan toouse hello same storage account based on your needs.</span></span>
* <span data-ttu-id="8396d-322">Kopyalayın ve hello depolama hesabı anahtarı hello hedef depolama hesabının hello sonraki aşaması için kaydedin.</span><span class="sxs-lookup"><span data-stu-id="8396d-322">Copy and save hello storage account key of hello destination storage account for hello next stage.</span></span>

<span data-ttu-id="8396d-323">Üretim iş yükü toouse premium depolama için tüm veriler hareket öneririz.</span><span class="sxs-lookup"><span data-stu-id="8396d-323">We strongly recommend you moving all data for production workload toouse premium storage.</span></span>

#### <a name="step-3-upload-hello-vhd-tooazure-storage"></a><span data-ttu-id="8396d-324">3. Adım</span><span class="sxs-lookup"><span data-stu-id="8396d-324">Step 3.</span></span> <span data-ttu-id="8396d-325">Merhaba VHD tooAzure depolama karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="8396d-325">Upload hello VHD tooAzure Storage</span></span>
<span data-ttu-id="8396d-326">VHD hello yerel bir dizine sahip olduğunuza göre AzCopy veya AzurePowerShell tooupload hello .vhd dosyası tooAzure depolama kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8396d-326">Now that you have your VHD in hello local directory, you can use AzCopy or AzurePowerShell tooupload hello .vhd file tooAzure Storage.</span></span> <span data-ttu-id="8396d-327">Her iki seçenek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="8396d-327">Both options are provided here:</span></span>

##### <a name="option-1-using-azure-powershell-add-azurevhd-tooupload-hello-vhd-file"></a><span data-ttu-id="8396d-328">Seçenek 1: Azure PowerShell Ekle-AzureVhd tooupload hello .vhd dosyası kullanma</span><span class="sxs-lookup"><span data-stu-id="8396d-328">Option 1: Using Azure PowerShell Add-AzureVhd tooupload hello .vhd file</span></span>

```powershell
Add-AzureVhd [-Destination] <Uri> [-LocalFilePath] <FileInfo>
```

<span data-ttu-id="8396d-329">Örnek <Uri> olabilir ***"https://storagesample.blob.core.windows.net/mycontainer/blob1.vhd"***.</span><span class="sxs-lookup"><span data-stu-id="8396d-329">An example <Uri> might be ***"https://storagesample.blob.core.windows.net/mycontainer/blob1.vhd"***.</span></span> <span data-ttu-id="8396d-330">Örnek <FileInfo> olabilir ***"C:\path\to\upload.vhd"***.</span><span class="sxs-lookup"><span data-stu-id="8396d-330">An example <FileInfo> might be ***"C:\path\to\upload.vhd"***.</span></span>

##### <a name="option-2-using-azcopy-tooupload-hello-vhd-file"></a><span data-ttu-id="8396d-331">Seçenek 2: AzCopy tooupload hello .vhd dosyası kullanma</span><span class="sxs-lookup"><span data-stu-id="8396d-331">Option 2: Using AzCopy tooupload hello .vhd file</span></span>
<span data-ttu-id="8396d-332">AzCopy kullanarak hello VHD hello Internet üzerinden kolayca karşıya yükleyebilir.</span><span class="sxs-lookup"><span data-stu-id="8396d-332">Using AzCopy, you can easily upload hello VHD over hello Internet.</span></span> <span data-ttu-id="8396d-333">Merhaba VHD'ler Hello boyutuna bağlı olarak, bu zaman alabilir.</span><span class="sxs-lookup"><span data-stu-id="8396d-333">Depending on hello size of hello VHDs, this may take time.</span></span> <span data-ttu-id="8396d-334">Bu seçenek kullanıldığında toocheck hello depolama hesabı giriş/çıkış sınırları unutmayın.</span><span class="sxs-lookup"><span data-stu-id="8396d-334">Remember toocheck hello storage account ingress/egress limits when using this option.</span></span> <span data-ttu-id="8396d-335">Bkz: [Azure Storage ölçeklenebilirlik ve performans hedefleri](storage-scalability-targets.md) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="8396d-335">See [Azure Storage Scalability and Performance Targets](storage-scalability-targets.md) for details.</span></span>

1. <span data-ttu-id="8396d-336">AzCopy buradan yükleyip: [en güncel AzCopy sürümünü](http://aka.ms/downloadazcopy)</span><span class="sxs-lookup"><span data-stu-id="8396d-336">Download and install AzCopy from here: [Latest version of AzCopy](http://aka.ms/downloadazcopy)</span></span>
2. <span data-ttu-id="8396d-337">Azure PowerShell ve AzCopy yüklendiği gidin toohello klasörünü açın.</span><span class="sxs-lookup"><span data-stu-id="8396d-337">Open Azure PowerShell and go toohello folder where AzCopy is installed.</span></span>
3. <span data-ttu-id="8396d-338">Kullanım hello şu komutu toocopy hello VHD "Kaynak" dosyasından çok "Hedef".</span><span class="sxs-lookup"><span data-stu-id="8396d-338">Use hello following command toocopy hello VHD file from "Source" too"Destination".</span></span>

    ```azcopy
    AzCopy /Source: <source> /SourceKey: <source-account-key> /Dest: <destination> /DestKey: <dest-account-key> /BlobType:page /Pattern: <file-name>
    ```

    <span data-ttu-id="8396d-339">Örnek:</span><span class="sxs-lookup"><span data-stu-id="8396d-339">Example:</span></span>

    ```azcopy
    AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /SourceKey:key1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /DestKey:key2 /BlobType:page /Pattern:abc.vhd
    ```

    <span data-ttu-id="8396d-340">Açıklamaları hello AzCopy komut kullanılan hello Parametreler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="8396d-340">Here are descriptions of hello parameters used in hello AzCopy command:</span></span>

   * <span data-ttu-id="8396d-341">**/ Kaynak:  *&lt;kaynak&gt;:***  hello klasör veya hello VHD'yi içeren depolama kapsayıcısı URL konumu.</span><span class="sxs-lookup"><span data-stu-id="8396d-341">**/Source: *&lt;source&gt;:*** Location of hello folder or storage container URL that contains hello VHD.</span></span>
   * <span data-ttu-id="8396d-342">**/ SourceKey:  *&lt;kaynak hesap anahtarı&gt;:***  hello kaynak depolama hesabının depolama hesabı anahtarı.</span><span class="sxs-lookup"><span data-stu-id="8396d-342">**/SourceKey: *&lt;source-account-key&gt;:*** Storage account key of hello source storage account.</span></span>
   * <span data-ttu-id="8396d-343">**/ Taşınmaya:  *&lt;hedef&gt;:***  depolama kapsayıcısı URL toocopy hello VHD'ye.</span><span class="sxs-lookup"><span data-stu-id="8396d-343">**/Dest: *&lt;destination&gt;:*** Storage container URL toocopy hello VHD to.</span></span>
   * <span data-ttu-id="8396d-344">**/ DestKey:  *&lt;hedef hesap anahtarı&gt;:***  hello hedef depolama hesabının depolama hesabı anahtarı.</span><span class="sxs-lookup"><span data-stu-id="8396d-344">**/DestKey: *&lt;dest-account-key&gt;:*** Storage account key of hello destination storage account.</span></span>
   * <span data-ttu-id="8396d-345">**/ BlobType: sayfa:** bu hello hedef bir sayfa blob'u olduğunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="8396d-345">**/BlobType: page:** Specifies that hello destination is a page blob.</span></span>
   * <span data-ttu-id="8396d-346">**/ Deseni:  *&lt;dosya adı&gt;:***  hello VHD toocopy hello dosya adı belirtin.</span><span class="sxs-lookup"><span data-stu-id="8396d-346">**/Pattern: *&lt;file-name&gt;:*** Specify hello file name of hello VHD toocopy.</span></span>

<span data-ttu-id="8396d-347">Aracı AzCopy kullanımıyla ilgili ayrıntılar için bkz: [hello AzCopy komut satırı yardımcı programı ile veri aktarma](storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="8396d-347">For details on using AzCopy tool, see [Transfer data with hello AzCopy Command-Line Utility](storage-use-azcopy.md).</span></span>

##### <a name="other-options-for-uploading-a-vhd"></a><span data-ttu-id="8396d-348">Bir VHD karşıya yükleme için diğer seçenekleri</span><span class="sxs-lookup"><span data-stu-id="8396d-348">Other options for uploading a VHD</span></span>
<span data-ttu-id="8396d-349">Yol aşağıdaki hello birini kullanarak bir VHD'yi tooyour depolama hesabı da yükleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="8396d-349">You can also upload a VHD tooyour storage account using one of hello following means:</span></span>

* [<span data-ttu-id="8396d-350">Azure depolama kopyalama Blob API</span><span class="sxs-lookup"><span data-stu-id="8396d-350">Azure Storage Copy Blob API</span></span>](https://msdn.microsoft.com/library/azure/dd894037.aspx)
* [<span data-ttu-id="8396d-351">Azure Depolama Gezgini karşıya BLOB'ları</span><span class="sxs-lookup"><span data-stu-id="8396d-351">Azure Storage Explorer Uploading Blobs</span></span>](https://azurestorageexplorer.codeplex.com/)
* [<span data-ttu-id="8396d-352">Depolama içeri/dışarı aktarma hizmeti REST API Başvurusu</span><span class="sxs-lookup"><span data-stu-id="8396d-352">Storage Import/Export Service REST API Reference</span></span>](https://msdn.microsoft.com/library/dn529096.aspx)

> [!NOTE]
> <span data-ttu-id="8396d-353">İçeri/dışarı aktarma hizmeti 7 günden daha uzun süre karşıya tahmini varsa kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="8396d-353">We recommend using Import/Export Service if estimated uploading time is longer than 7 days.</span></span> <span data-ttu-id="8396d-354">Kullanabileceğiniz [DataTransferSpeedCalculator](https://github.com/Azure-Samples/storage-dotnet-import-export-job-management/blob/master/DataTransferSpeedCalculator.html) veri boyutu ve aktarım birimi tooestimate başlangıç saati.</span><span class="sxs-lookup"><span data-stu-id="8396d-354">You can use [DataTransferSpeedCalculator](https://github.com/Azure-Samples/storage-dotnet-import-export-job-management/blob/master/DataTransferSpeedCalculator.html) tooestimate hello time from data size and transfer unit.</span></span>
>
> <span data-ttu-id="8396d-355">İçeri/dışarı aktarma olabilir toocopy tooa standart depolama hesabı kullanılır.</span><span class="sxs-lookup"><span data-stu-id="8396d-355">Import/Export can be used toocopy tooa standard storage account.</span></span> <span data-ttu-id="8396d-356">AzCopy gibi bir araç kullanarak standart depolama toopremium depolama hesabından toocopy gerekir.</span><span class="sxs-lookup"><span data-stu-id="8396d-356">You will need toocopy from standard storage toopremium storage account using a tool like AzCopy.</span></span>
>
>

## <span data-ttu-id="8396d-357"><a name="create-azure-virtual-machine-using-premium-storage"></a>Azure Premium Storage kullanarak VM'ler oluşturma</span><span class="sxs-lookup"><span data-stu-id="8396d-357"><a name="create-azure-virtual-machine-using-premium-storage"></a>Create Azure VMs using Premium Storage</span></span>
<span data-ttu-id="8396d-358">Karşıya yüklenen ya da kopyalanmış toohello istenen depolama hesabı Hello VHD olduktan sonra bir işletim sistemi görüntüsü veya işletim sistemi diski senaryonuza bağlı olarak bu bölüm tooregister hello VHD hello yönergeleri izleyin ve ardından VM örneği ondan oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8396d-358">After hello VHD is uploaded or copied toohello desired storage account, follow hello instructions in this section tooregister hello VHD as an OS image, or OS disk depending on your scenario and then create a VM instance from it.</span></span> <span data-ttu-id="8396d-359">bir kez oluşturulduğunda hello veri diski ekli toohello VM VHD olabilir.</span><span class="sxs-lookup"><span data-stu-id="8396d-359">hello data disk VHD can be attached toohello VM once it is created.</span></span>
<span data-ttu-id="8396d-360">Örnek geçiş dosyası hello bu bölümün sonunda sağlanır.</span><span class="sxs-lookup"><span data-stu-id="8396d-360">A sample migration script is provided at hello end of this section.</span></span> <span data-ttu-id="8396d-361">Bu basit bir komut dosyası tüm senaryoları eşleşmiyor.</span><span class="sxs-lookup"><span data-stu-id="8396d-361">This simple script does not match all scenarios.</span></span> <span data-ttu-id="8396d-362">Belirli senaryonuza tooupdate hello betik toomatch gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="8396d-362">You may need tooupdate hello script toomatch with your specific scenario.</span></span> <span data-ttu-id="8396d-363">Bu komut dosyası tooyour senaryo geçerliyse toosee bkz aşağıda [bir örnek geçiş komut dosyası](#a-sample-migration-script).</span><span class="sxs-lookup"><span data-stu-id="8396d-363">toosee if this script applies tooyour scenario, see below [A Sample Migration Script](#a-sample-migration-script).</span></span>

### <a name="checklist"></a><span data-ttu-id="8396d-364">Denetim listesi</span><span class="sxs-lookup"><span data-stu-id="8396d-364">Checklist</span></span>
1. <span data-ttu-id="8396d-365">Tüm hello VHD diskleri kopyalama beklemeniz tamamlanır.</span><span class="sxs-lookup"><span data-stu-id="8396d-365">Wait until all hello VHD disks copying is complete.</span></span>
2. <span data-ttu-id="8396d-366">Premium depolama, için geçirdiğiniz hello bölgede kullanılabilir olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="8396d-366">Make sure Premium Storage is available in hello region you are migrating to.</span></span>
3. <span data-ttu-id="8396d-367">Merhaba, kullanarak yeni VM dizisi karar verin.</span><span class="sxs-lookup"><span data-stu-id="8396d-367">Decide hello new VM series you will be using.</span></span> <span data-ttu-id="8396d-368">Premium depolama özelliğine sahip olmalıdır ve başlangıç boyutu hello bölgede hello kullanılabilirliğine bağlı olarak ve gereksinimlerinize göre olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8396d-368">It should be a Premium Storage capable, and hello size should be depending on hello availability in hello region and based on your needs.</span></span>
4. <span data-ttu-id="8396d-369">Kullanacağınız hello tam VM boyutu karar verin.</span><span class="sxs-lookup"><span data-stu-id="8396d-369">Decide hello exact VM size you will use.</span></span> <span data-ttu-id="8396d-370">VM boyutu toobe büyüklükte toosupport hello sahip veri diski sayısı gerekir.</span><span class="sxs-lookup"><span data-stu-id="8396d-370">VM size needs toobe large enough toosupport hello number of data disks you have.</span></span> <span data-ttu-id="8396d-371">Örneğin</span><span class="sxs-lookup"><span data-stu-id="8396d-371">E.g.</span></span> <span data-ttu-id="8396d-372">4 veri diski varsa, hello VM 2 veya daha fazla çekirdek olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="8396d-372">if you have 4 data disks, hello VM must have 2 or more cores.</span></span> <span data-ttu-id="8396d-373">Ayrıca, işlemci gücü, bellek göz önünde bulundurun ve ağ bant genişliği gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="8396d-373">Also, consider processing power, memory and network bandwidth needs.</span></span>
5. <span data-ttu-id="8396d-374">Premium depolama hesabı hello hedef bölgede oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8396d-374">Create a Premium Storage account in hello target region.</span></span> <span data-ttu-id="8396d-375">Bu hello için kullanacağınız hello hesabıdır yeni VM.</span><span class="sxs-lookup"><span data-stu-id="8396d-375">This is hello account you will use for hello new VM.</span></span>
6. <span data-ttu-id="8396d-376">Merhaba geçerli VM ayrıntıları hello disklerin listesini ve karşılık gelen VHD BLOB'ları da dahil olmak üzere kullanışlı vardır.</span><span class="sxs-lookup"><span data-stu-id="8396d-376">Have hello current VM details handy, including hello list of disks and corresponding VHD blobs.</span></span>

<span data-ttu-id="8396d-377">Uygulamanızı kapalı kalma süresi için hazırlayın.</span><span class="sxs-lookup"><span data-stu-id="8396d-377">Prepare your application for downtime.</span></span> <span data-ttu-id="8396d-378">toodo temiz bir geçiş, toostop hello geçerli sistemi tüm hello işleme sahip.</span><span class="sxs-lookup"><span data-stu-id="8396d-378">toodo a clean migration, you have toostop all hello processing in hello current system.</span></span> <span data-ttu-id="8396d-379">Ancak bundan sonra geçirebileceğiniz tooconsistent durumu alabilirsiniz toohello yeni platformu.</span><span class="sxs-lookup"><span data-stu-id="8396d-379">Only then you can get it tooconsistent state which you can migrate toohello new platform.</span></span> <span data-ttu-id="8396d-380">Kapalı kalma süresi hello hello diskleri toomigrate veri miktarına bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="8396d-380">Downtime duration will depend on hello amount of data in hello disks toomigrate.</span></span>

> [!NOTE]
> <span data-ttu-id="8396d-381">Lütfen özel bir VHD diskten bir Azure Kaynak Yöneticisi'ni VM oluşturuyorsanız, çok başvurun[bu şablonu](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd) Resource Manager mevcut diski kullanarak VM dağıtmak için.</span><span class="sxs-lookup"><span data-stu-id="8396d-381">If you are creating an Azure Resource Manager VM from a specialized VHD Disk, please refer too[this template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd) for deploying Resource Manager VM using existing disk.</span></span>
>
>

### <a name="register-your-vhd"></a><span data-ttu-id="8396d-382">VHD kaydetme</span><span class="sxs-lookup"><span data-stu-id="8396d-382">Register your VHD</span></span>
<span data-ttu-id="8396d-383">işletim sistemi VHD veya tooattach bir veri diski tooa VM'den toocreate yeni VM, ilk kaydetmeniz gerekir bunları.</span><span class="sxs-lookup"><span data-stu-id="8396d-383">toocreate a VM from OS VHD or tooattach a data disk tooa new VM, you must first register them.</span></span> <span data-ttu-id="8396d-384">VHD'ler senaryo bağlı olarak aşağıdaki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="8396d-384">Follow steps below depending on your VHD's scenario.</span></span>

#### <a name="generalized-operating-system-vhd-toocreate-multiple-azure-vm-instances"></a><span data-ttu-id="8396d-385">İşletim sistemi VHD toocreate birden çok Azure VM örnekleri genelleştirilmiş</span><span class="sxs-lookup"><span data-stu-id="8396d-385">Generalized Operating System VHD toocreate multiple Azure VM instances</span></span>
<span data-ttu-id="8396d-386">VHD'nin olduğundan genelleştirilmiş işletim sistemi görüntüsü toohello depolama hesabı karşıya sonra olarak kaydetmek bir **Azure VM görüntüsü** böylece bir veya daha fazla VM örnekleri oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8396d-386">After generalized OS image VHD is uploaded toohello storage account, register it as an **Azure VM Image** so that you can create one or more VM instances from it.</span></span> <span data-ttu-id="8396d-387">PowerShell cmdlet'leri tooregister aşağıdaki Merhaba, VHD bir Azure VM işletim sistemi görüntüsü olarak kullanın.</span><span class="sxs-lookup"><span data-stu-id="8396d-387">Use hello following PowerShell cmdlets tooregister your VHD as an Azure VM OS image.</span></span> <span data-ttu-id="8396d-388">VHD için burada kopyalanmıştır hello tam kapsayıcı URL'sini belirtin.</span><span class="sxs-lookup"><span data-stu-id="8396d-388">Provide hello complete container URL where VHD was copied to.</span></span>

```powershell
Add-AzureVMImage -ImageName "OSImageName" -MediaLocation "https://storageaccount.blob.core.windows.net/vhdcontainer/osimage.vhd" -OS Windows
```

<span data-ttu-id="8396d-389">Kopyalayın ve bu yeni Azure VM görüntüsü hello adını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="8396d-389">Copy and save hello name of this new Azure VM Image.</span></span> <span data-ttu-id="8396d-390">Yukarıdaki Hello örnek içinde *OSImageName*.</span><span class="sxs-lookup"><span data-stu-id="8396d-390">In hello example above, it is *OSImageName*.</span></span>

#### <a name="unique-operating-system-vhd-toocreate-a-single-azure-vm-instance"></a><span data-ttu-id="8396d-391">Benzersiz işletim sistemi VHD toocreate tek bir Azure VM örneği</span><span class="sxs-lookup"><span data-stu-id="8396d-391">Unique Operating System VHD toocreate a single Azure VM instance</span></span>
<span data-ttu-id="8396d-392">Hello sonra benzersiz OS VHD karşıya yüklenen toohello depolama olduğu hesap, olarak kaydeder bir **Azure işletim sistemi diski** böylece VM örneği oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8396d-392">After hello unique OS VHD is uploaded toohello storage account, register it as an **Azure OS Disk** so that you can create a VM instance from it.</span></span> <span data-ttu-id="8396d-393">Bu PowerShell cmdlet'leri tooregister, VHD Azure işletim sistemi diski kullanın.</span><span class="sxs-lookup"><span data-stu-id="8396d-393">Use these PowerShell cmdlets tooregister your VHD as an Azure OS Disk.</span></span> <span data-ttu-id="8396d-394">VHD için burada kopyalanmıştır hello tam kapsayıcı URL'sini belirtin.</span><span class="sxs-lookup"><span data-stu-id="8396d-394">Provide hello complete container URL where VHD was copied to.</span></span>

```powershell
Add-AzureDisk -DiskName "OSDisk" -MediaLocation "https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd" -Label "My OS Disk" -OS "Windows"
```

<span data-ttu-id="8396d-395">Kopyalayın ve bu yeni Azure işletim sistemi diski hello adını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="8396d-395">Copy and save hello name of this new Azure OS Disk.</span></span> <span data-ttu-id="8396d-396">Yukarıdaki Hello örnek içinde *OSDisk*.</span><span class="sxs-lookup"><span data-stu-id="8396d-396">In hello example above, it is *OSDisk*.</span></span>

#### <a name="data-disk-vhd-toobe-attached-toonew-azure-vm-instances"></a><span data-ttu-id="8396d-397">Veri diski VHD toobe toonew Azure VM örnekleri bağlı</span><span class="sxs-lookup"><span data-stu-id="8396d-397">Data disk VHD toobe attached toonew Azure VM instance(s)</span></span>
<span data-ttu-id="8396d-398">Merhaba veri disk VHD karşıya toostorage hesabı sonra ekli tooyour olması için bir Azure veri diski olarak kaydetmek yeni DS serisi, DSv2 serisi veya GS serisi Azure VM örneği.</span><span class="sxs-lookup"><span data-stu-id="8396d-398">After hello data disk VHD is uploaded toostorage account, register it as an Azure Data Disk so that it can be attached tooyour new DS Series, DSv2 series or GS Series Azure VM instance.</span></span>

<span data-ttu-id="8396d-399">Bu PowerShell cmdlet'leri tooregister, VHD bir Azure veri diski kullanın.</span><span class="sxs-lookup"><span data-stu-id="8396d-399">Use these PowerShell cmdlets tooregister your VHD as an Azure Data Disk.</span></span> <span data-ttu-id="8396d-400">VHD için burada kopyalanmıştır hello tam kapsayıcı URL'sini belirtin.</span><span class="sxs-lookup"><span data-stu-id="8396d-400">Provide hello complete container URL where VHD was copied to.</span></span>

```powershell
Add-AzureDisk -DiskName "DataDisk" -MediaLocation "https://storageaccount.blob.core.windows.net/vhdcontainer/datadisk.vhd" -Label "My Data Disk"
```

<span data-ttu-id="8396d-401">Kopyalayın ve bu yeni Azure veri diski hello adını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="8396d-401">Copy and save hello name of this new Azure Data Disk.</span></span> <span data-ttu-id="8396d-402">Yukarıdaki Hello örnek içinde *DataDisk*.</span><span class="sxs-lookup"><span data-stu-id="8396d-402">In hello example above, it is *DataDisk*.</span></span>

### <a name="create-a-premium-storage-capable-vm"></a><span data-ttu-id="8396d-403">Premium depolama özelliğine sahip VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="8396d-403">Create a Premium Storage capable VM</span></span>
<span data-ttu-id="8396d-404">İşletim sistemi görüntüsü kez hello veya işletim sistemi diski kayıtlı, yeni DS serisi, DSv2 serisi veya GS serisi VM oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8396d-404">Once hello OS image or OS disk are registered, create a new DS-series, DSv2-series or GS-series VM.</span></span> <span data-ttu-id="8396d-405">Merhaba işletim sistemi görüntüsü veya kaydettiğiniz işletim sistemi disk adı kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="8396d-405">You will be using hello operating system image or operating system disk name that you registered.</span></span> <span data-ttu-id="8396d-406">Merhaba VM türü hello Premium depolama katmanını seçin.</span><span class="sxs-lookup"><span data-stu-id="8396d-406">Select hello VM type from hello Premium Storage tier.</span></span> <span data-ttu-id="8396d-407">Aşağıdaki örnekte hello kullanıyoruz *Standard_DS2* VM boyutu.</span><span class="sxs-lookup"><span data-stu-id="8396d-407">In example below, we are using hello *Standard_DS2* VM size.</span></span>

> [!NOTE]
> <span data-ttu-id="8396d-408">Merhaba disk boyutu toomake kapasite ve performans gereksinimlerini ve hello kullanılabilir Azure disk boyutlarını eşleştiğinden emin güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="8396d-408">Update hello disk size toomake sure it matches your capacity and performance requirements and hello available Azure disk sizes.</span></span>
>
>

<span data-ttu-id="8396d-409">İzleme hello adım adım PowerShell cmdlet'leri toocreate altındaki Yeni VM hello.</span><span class="sxs-lookup"><span data-stu-id="8396d-409">Follow hello step by step PowerShell cmdlets below toocreate hello new VM.</span></span> <span data-ttu-id="8396d-410">İlk olarak, hello ortak parametreleri ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="8396d-410">First, set hello common parameters:</span></span>

```powershell
$serviceName = "yourVM"
$location = "location-name" (e.g., West US)
$vmSize ="Standard_DS2"
$adminUser = "youradmin"
$adminPassword = "yourpassword"
$vmName ="yourVM"
$vmSize = "Standard_DS2"
```

<span data-ttu-id="8396d-411">İlk olarak, yeni VM'ler içinde barındıracak bir bulut hizmeti oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8396d-411">First, create a cloud service in which you will be hosting your new VMs.</span></span>

```powershell
New-AzureService -ServiceName $serviceName -Location $location
```

<span data-ttu-id="8396d-412">Ardından, senaryonuza bağlı olarak ya da hello işletim sistemi görüntüsü veya işletim sistemi diski, kaydettiğiniz hello Azure VM örneği oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8396d-412">Next, depending on your scenario, create hello Azure VM instance from either hello OS Image or OS Disk that you registered.</span></span>

#### <a name="generalized-operating-system-vhd-toocreate-multiple-azure-vm-instances"></a><span data-ttu-id="8396d-413">İşletim sistemi VHD toocreate birden çok Azure VM örnekleri genelleştirilmiş</span><span class="sxs-lookup"><span data-stu-id="8396d-413">Generalized Operating System VHD toocreate multiple Azure VM instances</span></span>
<span data-ttu-id="8396d-414">Merhaba hello kullanarak bir veya daha fazla yeni DS serisi Azure VM örnekleri oluşturmak **Azure işletim sistemi görüntüsü** , kayıtlı.</span><span class="sxs-lookup"><span data-stu-id="8396d-414">Create hello one or more new DS Series Azure VM instances using hello **Azure OS Image** that you registered.</span></span> <span data-ttu-id="8396d-415">Bu işletim sistemi görüntüsü adı, aşağıda gösterildiği gibi yeni VM oluşturulurken hello VM yapılandırması belirtin.</span><span class="sxs-lookup"><span data-stu-id="8396d-415">Specify this OS Image name in hello VM configuration when creating new VM as shown below.</span></span>

```powershell
$OSImage = Get-AzureVMImage –ImageName "OSImageName"

$vm = New-AzureVMConfig -Name $vmName –InstanceSize $vmSize -ImageName $OSImage.ImageName

Add-AzureProvisioningConfig -Windows –AdminUserName $adminUser -Password $adminPassword –VM $vm

New-AzureVM -ServiceName $serviceName -VM $vm
```

#### <a name="unique-operating-system-vhd-toocreate-a-single-azure-vm-instance"></a><span data-ttu-id="8396d-416">Benzersiz işletim sistemi VHD toocreate tek bir Azure VM örneği</span><span class="sxs-lookup"><span data-stu-id="8396d-416">Unique Operating System VHD toocreate a single Azure VM instance</span></span>
<span data-ttu-id="8396d-417">Hello kullanarak yeni DS serisi Azure VM örneği oluşturma **Azure işletim sistemi diski** , kayıtlı.</span><span class="sxs-lookup"><span data-stu-id="8396d-417">Create a new DS series Azure VM instance using hello **Azure OS Disk** that you registered.</span></span> <span data-ttu-id="8396d-418">Oluşturma Merhaba, yeni VM aşağıda gösterildiği gibi hello VM yapılandırması bu işletim sistemi Disk adı belirtin.</span><span class="sxs-lookup"><span data-stu-id="8396d-418">Specify this OS Disk name in hello VM configuration when creating hello new VM as shown below.</span></span>

```powershell
$OSDisk = Get-AzureDisk –DiskName "OSDisk"

$vm = New-AzureVMConfig -Name $vmName -InstanceSize $vmSize -DiskName $OSDisk.DiskName

New-AzureVM -ServiceName $serviceName –VM $vm
```

<span data-ttu-id="8396d-419">Bulut hizmeti, bölge, depolama hesabı, kullanılabilirlik kümesi ve önbellek İlkesi gibi diğer Azure VM bilgileri belirtin.</span><span class="sxs-lookup"><span data-stu-id="8396d-419">Specify other Azure VM information, such as a cloud service, region, storage account, availability set, and caching policy.</span></span> <span data-ttu-id="8396d-420">Merhaba VM örneği ilişkili işletim sistemiyle birlikte bulunan veya seçili hello bulut hizmeti, bölge ve depolama hesabı tüm olması gerekir böylece veri diskleri, bu disklerin VHD'ler temel hello aynı konumda hello unutmayın.</span><span class="sxs-lookup"><span data-stu-id="8396d-420">Note that hello VM instance must be co-located with associated operating system or data disks, so hello selected cloud service, region and storage account must all be in hello same location as hello underlying VHDs of those disks.</span></span>

### <a name="attach-data-disk"></a><span data-ttu-id="8396d-421">Veri diski ekleme</span><span class="sxs-lookup"><span data-stu-id="8396d-421">Attach data disk</span></span>
<span data-ttu-id="8396d-422">Son olarak, kayıtlı durumunda veri VHD'ler disk, toohello ekleme yeni Premium depolama özellikli Azure VM.</span><span class="sxs-lookup"><span data-stu-id="8396d-422">Lastly, if you have registered data disk VHDs, attach them toohello new Premium Storage capable Azure VM.</span></span>

<span data-ttu-id="8396d-423">PowerShell cmdlet'ini tooattach veri diski toohello kullanmak yeni VM ve ilke önbelleğe alma hello belirtin.</span><span class="sxs-lookup"><span data-stu-id="8396d-423">Use following PowerShell cmdlet tooattach data disk toohello new VM and specify hello caching policy.</span></span> <span data-ttu-id="8396d-424">Merhaba aşağıdaki örnekte ilke önbelleğe alma çok kümesindeki*salt okunur*.</span><span class="sxs-lookup"><span data-stu-id="8396d-424">In example below hello caching policy is set too*ReadOnly*.</span></span>

```powershell
$vm = Get-AzureVM -ServiceName $serviceName -Name $vmName

Add-AzureDataDisk -ImportFrom -DiskName "DataDisk" -LUN 0 –HostCaching ReadOnly –VM $vm

Update-AzureVM  -VM $vm
```

> [!NOTE]
> <span data-ttu-id="8396d-425">Ek adımlar gerekli toosupport olabilir, uygulama değil Bu kılavuz kapsamında.</span><span class="sxs-lookup"><span data-stu-id="8396d-425">There may be additional steps necessary toosupport your application that is not be covered by this guide.</span></span>
>
>

### <a name="checking-and-plan-backup"></a><span data-ttu-id="8396d-426">Denetleme ve yedekleme planlama</span><span class="sxs-lookup"><span data-stu-id="8396d-426">Checking and plan backup</span></span>
<span data-ttu-id="8396d-427">Bir kez yeni VM çalışıyor hello ve çalışan, aynı oturum açma kimliği ve parola kullanarak hello erişim özgün VM hello aynıdır ve her şeyin beklendiği gibi çalıştığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="8396d-427">Once hello new VM is up and running, access it using hello same login id and password is as hello original VM, and verify that everything is working as expected.</span></span> <span data-ttu-id="8396d-428">Merhaba şeritli birimler dahil tüm hello ayarları de mevcut olacaktır yeni VM hello.</span><span class="sxs-lookup"><span data-stu-id="8396d-428">All hello settings, including hello striped volumes, would be present in hello new VM.</span></span>

<span data-ttu-id="8396d-429">Merhaba son adımı tooplan yedekleme ve bakım zamanlaması yeni VM hello uygulamanın gereksinimlerine göre hello için değildir.</span><span class="sxs-lookup"><span data-stu-id="8396d-429">hello last step is tooplan backup and maintenance schedule for hello new VM based on hello application's needs.</span></span>

### <span data-ttu-id="8396d-430"><a name="a-sample-migration-script"></a>Örnek geçiş komut dosyası</span><span class="sxs-lookup"><span data-stu-id="8396d-430"><a name="a-sample-migration-script"></a>A sample migration script</span></span>
<span data-ttu-id="8396d-431">Birden çok sanal makineleri toomigrate varsa, automation PowerShell komut yardımcı olacaktır.</span><span class="sxs-lookup"><span data-stu-id="8396d-431">If you have multiple VMs toomigrate, automation through PowerShell scripts will be helpful.</span></span> <span data-ttu-id="8396d-432">Bir VM hello geçişini otomatikleştiren bir örnek betiği aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="8396d-432">Following is a sample script that automates hello migration of a VM.</span></span> <span data-ttu-id="8396d-433">Not, aşağıdaki komut dosyası yalnızca bir örnektir ve hello geçerli VM diskleri hakkında yapılan birkaç varsayımlar vardır.</span><span class="sxs-lookup"><span data-stu-id="8396d-433">Note that below script is only an example, and there are few assumptions made about hello current VM disks.</span></span> <span data-ttu-id="8396d-434">Belirli senaryonuza tooupdate hello betik toomatch gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="8396d-434">You may need tooupdate hello script toomatch with your specific scenario.</span></span>

<span data-ttu-id="8396d-435">Merhaba varsayımlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="8396d-435">hello assumptions are:</span></span>

* <span data-ttu-id="8396d-436">Klasik Azure sanal makineleri oluşturuyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="8396d-436">You are creating classic Azure VMs.</span></span>
* <span data-ttu-id="8396d-437">Kaynak işletim sistemi diski ve kaynak veri diskleri aynı depolama hesabı ve aynı kapsayıcı olan.</span><span class="sxs-lookup"><span data-stu-id="8396d-437">Your source OS Disks and source Data Disks are in same storage account and same container.</span></span> <span data-ttu-id="8396d-438">İşletim sistemi diskleri ve veri diskleri içinde değilse aynı hello yerleştirin, AzCopy ya da Azure PowerShell toocopy VHD'ler depolama hesapları ve kapsayıcıları üzerinden kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8396d-438">If your OS Disks and Data Disks are not in hello same place, you can use AzCopy or Azure PowerShell toocopy VHDs over storage accounts and containers.</span></span> <span data-ttu-id="8396d-439">Toohello önceki adıma bakın: [kopyalama VHD AzCopy veya PowerShell ile](#copy-vhd-with-azcopy-or-powershell).</span><span class="sxs-lookup"><span data-stu-id="8396d-439">Refer toohello previous step: [Copy VHD with AzCopy or PowerShell](#copy-vhd-with-azcopy-or-powershell).</span></span> <span data-ttu-id="8396d-440">Bu komut dosyası toomeet düzenleme senaryonuz başka bir seçenektir ancak daha kolay ve hızlı olduğundan AzCopy veya PowerShell kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="8396d-440">Editing this script toomeet your scenario is another choice, but we recommend using AzCopy or PowerShell since it is easier and faster.</span></span>

<span data-ttu-id="8396d-441">Merhaba Otomasyon betiğini aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="8396d-441">hello automation script is provided below.</span></span> <span data-ttu-id="8396d-442">Metin bilgilerinizle değiştirin ve belirli senaryonuza hello betik toomatch güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="8396d-442">Replace text with your information and update hello script toomatch with your specific scenario.</span></span>

> [!NOTE]
> <span data-ttu-id="8396d-443">Merhaba varolan komut dosyasını kullanarak hello ağ yapılandırması kaynağınızın VM korumaz.</span><span class="sxs-lookup"><span data-stu-id="8396d-443">Using hello existing script does not preserve hello network configuration of your source VM.</span></span> <span data-ttu-id="8396d-444">Geçirilen Vm'leriniz toore-config hello ağ ayarları gerekir.</span><span class="sxs-lookup"><span data-stu-id="8396d-444">You will need toore-config hello networking settings on your migrated VMs.</span></span>
>
>

```
    <#
    .Synopsis
    This script is provided as an EXAMPLE tooshow how toomigrate a VM from a standard storage account tooa premium storage account. You can customize it according tooyour specific requirements.

    .Description
    hello script will copy hello vhds (page blobs) of hello source VM toohello new storage account.
    And then it will create a new VM from these copied vhds based on hello inputs that you specified for hello new VM.
    You can modify hello script toosatisfy your specific requirement, but please be aware of hello items specified
    in hello Terms of Use section.

    .Terms of Use
    Copyright © 2015 Microsoft Corporation.  All rights reserved.

    THIS CODE AND ANY ASSOCIATED INFORMATION ARE PROVIDED "AS IS" WITHOUT WARRANTY OF ANY KIND,
    EITHER EXPRESSED OR IMPLIED, INCLUDING BUT NOT LIMITED toohello IMPLIED WARRANTIES OF MERCHANTABILITY
    AND/OR FITNESS FOR A PARTICULAR PURPOSE. hello ENTIRE RISK OF USE, INABILITY tooUSE, OR
    RESULTS FROM hello USE OF THIS CODE REMAINS WITH hello USER.

    .Example (Save this script as Migrate-AzureVM.ps1)

    .\Migrate-AzureVM.ps1 -SourceServiceName CurrentServiceName -SourceVMName CurrentVMName –DestStorageAccount newpremiumstorageaccount -DestServiceName NewServiceName -DestVMName NewDSVMName -DestVMSize "Standard_DS2" –Location "Southeast Asia"

    .Link
    toofind more information about how tooset up Azure PowerShell, refer toohello following links.
    http://azure.microsoft.com/documentation/articles/powershell-install-configure/
    http://azure.microsoft.com/documentation/articles/storage-powershell-guide-full/
    http://azure.microsoft.com/blog/2014/10/22/migrate-azure-virtual-machines-between-storage-accounts/

    #>

    Param(
    # hello cloud service name of hello VM.
    [Parameter(Mandatory = $true)]
    [string] $SourceServiceName,

    # hello VM name toocopy.
    [Parameter(Mandatory = $true)]
    [String] $SourceVMName,

    # hello destination storage account name.
    [Parameter(Mandatory = $true)]
    [String] $DestStorageAccount,

    # hello destination cloud service name
    [Parameter(Mandatory = $true)]
    [String] $DestServiceName,

    # hello destination vm name
    [Parameter(Mandatory = $true)]
    [String] $DestVMName,

    # hello destination vm size
    [Parameter(Mandatory = $true)]
    [String] $DestVMSize,

    # hello location of destination VM.
    [Parameter(Mandatory = $true)]
    [string] $Location,

    # whether or not toocopy hello os disk, hello default is only copy data disks
    [Parameter(Mandatory = $false)]
    [Bool] $DataDiskOnly = $true,

    # how frequently tooreport hello copy status in sceconds
    [Parameter(Mandatory = $false)]
    [Int32] $CopyStatusReportInterval = 15,

    # hello name suffix tooadd toonew created disks tooavoid conflict with source disk names
    [Parameter(Mandatory = $false)]
    [String]$DiskNameSuffix = "-prem"

    ) #end param

    #######################################################################
    #  Verify Azure PowerShell module and version
    #######################################################################

    #import hello Azure PowerShell module
    Write-Host "`n[WORKITEM] - Importing Azure PowerShell module" -ForegroundColor Yellow
    $azureModule = Import-Module Azure -PassThru

    if ($azureModule -ne $null)
    {
        Write-Host "`tSuccess" -ForegroundColor Green
    }
    else
    {
        #show module not found interaction and bail out
        Write-Host "[ERROR] - PowerShell module not found. Exiting." -ForegroundColor Red
        Exit
    }


    #Check hello Azure PowerShell module version
    Write-Host "`n[WORKITEM] - Checking Azure PowerShell module verion" -ForegroundColor Yellow
    If ($azureModule.Version -ge (New-Object System.Version -ArgumentList "0.8.14"))
    {
        Write-Host "`tSuccess" -ForegroundColor Green
    }
    Else
    {
        Write-Host "[ERROR] - Azure PowerShell module must be version 0.8.14 or higher. Exiting." -ForegroundColor Red
        Exit
    }

    #Check if there is an azure subscription set up in PowerShell
    Write-Host "`n[WORKITEM] - Checking Azure Subscription" -ForegroundColor Yellow
    $currentSubs = Get-AzureSubscription -Current
    if ($currentSubs -ne $null)
    {
        Write-Host "`tSuccess" -ForegroundColor Green
        Write-Host "`tYour current azure subscription in PowerShell is $($currentSubs.SubscriptionName)." -ForegroundColor Green
    }
    else
    {
        Write-Host "[ERROR] - There is no valid Azure subscription found in PowerShell. Please refer toothis article http://azure.microsoft.com/documentation/articles/powershell-install-configure/ tooconnect an Azure subscription. Exiting." -ForegroundColor Red
        Exit
    }


    #######################################################################
    #  Check if hello VM is shut down
    #  Stopping hello VM is a required step so that hello file system is consistent when you do hello copy operation.
    #  Azure does not support live migration at this time..
    #######################################################################

    if (($sourceVM = Get-AzureVM –ServiceName $SourceServiceName –Name $SourceVMName) -eq $null)
    {
        Write-Host "[ERROR] - hello source VM doesn't exist in hello current subscription. Exiting." -ForegroundColor Red
        Exit
    }

    # check if VM is shut down
    if ( $sourceVM.Status -notmatch "Stopped" )
    {
        Write-Host "[Warning] - Stopping hello VM is a required step so that hello file system is consistent when you do hello copy operation. Azure does not support live migration at this time. If you'd like toocreate a VM from a generalized image, sys-prep hello Virtual Machine before stopping it." -ForegroundColor Yellow
        $ContinueAnswer = Read-Host "`n`tDo you wish toostop $SourceVMName now? Input 'N' if you want tooshut down hello VM manually and come back later.(Y/N)"
        If ($ContinueAnswer -ne "Y") { Write-Host "`n Exiting." -ForegroundColor Red;Exit }
        $sourceVM | Stop-AzureVM

        # wait until hello VM is shut down
        $VMStatus = (Get-AzureVM –ServiceName $SourceServiceName –Name $vmName).Status
        while ($VMStatus -notmatch "Stopped")
        {
            Write-Host "`n[Status] - Waiting VM $vmName tooshut down" -ForegroundColor Green
            Sleep -Seconds 5
            $VMStatus = (Get-AzureVM –ServiceName $SourceServiceName –Name $vmName).Status
        }
    }

    # exporting hello sourve vm tooa configuration file, you can restore hello original VM by importing this config file
    # see more information for Import-AzureVM
    $workingDir = (Get-Location).Path
    $vmConfigurationPath = $env:HOMEPATH + "\VM-" + $SourceVMName + ".xml"
    Write-Host "`n[WORKITEM] - Exporting VM configuration too$vmConfigurationPath" -ForegroundColor Yellow
    $exportRe = $sourceVM | Export-AzureVM -Path $vmConfigurationPath


    #######################################################################
    #  Copy hello vhds of hello source vm
    #  You can choose toocopy all disks including os and data disks by specifying the
    #  parameter -DataDiskOnly toobe $false. hello default is toocopy only data disk vhds
    #  and hello new VM will boot from hello original os disk.
    #######################################################################

    $sourceOSDisk = $sourceVM.VM.OSVirtualHardDisk
    $sourceDataDisks = $sourceVM.VM.DataVirtualHardDisks

    # Get source storage account information, not considering hello data disks and os disks are in different accounts
    $sourceStorageAccountName = $sourceOSDisk.MediaLink.Host -split "\." | select -First 1
    $sourceStorageKey = (Get-AzureStorageKey -StorageAccountName $sourceStorageAccountName).Primary
    $sourceContext = New-AzureStorageContext –StorageAccountName $sourceStorageAccountName -StorageAccountKey $sourceStorageKey

    # Create destination context
    $destStorageKey = (Get-AzureStorageKey -StorageAccountName $DestStorageAccount).Primary
    $destContext = New-AzureStorageContext –StorageAccountName $DestStorageAccount -StorageAccountKey $destStorageKey

    # Create a container of vhds if it doesn't exist
    if ((Get-AzureStorageContainer -Context $destContext -Name vhds -ErrorAction SilentlyContinue) -eq $null)
    {
        Write-Host "`n[WORKITEM] - Creating a container vhds in hello destination storage account." -ForegroundColor Yellow
        New-AzureStorageContainer -Context $destContext -Name vhds
    }


    $allDisksToCopy = $sourceDataDisks
    # check if need toocopy os disk
    $sourceOSVHD = $sourceOSDisk.MediaLink.Segments[2]
    if ($DataDiskOnly)
    {
        # copy data disks only, this option requires deleting hello source VM so that dest VM can boot
        # from hello same vhd blob.
        $ContinueAnswer = Read-Host "`n`t[Warning] You chose toocopy data disks only. Moving VM requires removing hello original VM (hello disks and backing vhd files will NOT be deleted) so that hello new VM can boot from hello same vhd. This is an irreversible action. Do you wish tooproceed right now? (Y/N)"
        If ($ContinueAnswer -ne "Y") { Write-Host "`n Exiting." -ForegroundColor Red;Exit }
        $destOSVHD = Get-AzureStorageBlob -Blob $sourceOSVHD -Container vhds -Context $sourceContext
        Write-Host "`n[WORKITEM] - Removing hello original VM (hello vhd files are NOT deleted)." -ForegroundColor Yellow
        Remove-AzureVM -Name $SourceVMName -ServiceName $SourceServiceName

        Write-Host "`n[WORKITEM] - Waiting utill hello OS disk is released by source VM. This may take up tooseveral minutes."
        $diskAttachedTo = (Get-AzureDisk -DiskName $sourceOSDisk.DiskName).AttachedTo
        while ($diskAttachedTo -ne $null)
        {
            Start-Sleep -Seconds 10
            $diskAttachedTo = (Get-AzureDisk -DiskName $sourceOSDisk.DiskName).AttachedTo
        }

    }
    else
    {
        # copy hello os disk vhd
        Write-Host "`n[WORKITEM] - Starting copying os disk $($disk.DiskName) at $(get-date)." -ForegroundColor Yellow
        $allDisksToCopy += @($sourceOSDisk)
        $targetBlob = Start-AzureStorageBlobCopy -SrcContainer vhds -SrcBlob $sourceOSVHD -DestContainer vhds -DestBlob $sourceOSVHD -Context $sourceContext -DestContext $destContext -Force
        $destOSVHD = $targetBlob
    }


    # Copy all data disk vhds
    # Start all async copy requests in parallel.
    foreach($disk in $sourceDataDisks)
    {
        $blobName = $disk.MediaLink.Segments[2]
        # copy all data disks
        Write-Host "`n[WORKITEM] - Starting copying data disk $($disk.DiskName) at $(get-date)." -ForegroundColor Yellow
        $targetBlob = Start-AzureStorageBlobCopy -SrcContainer vhds -SrcBlob $blobName -DestContainer vhds -DestBlob $blobName -Context $sourceContext -DestContext $destContext -Force
        # update hello media link toopoint toohello target blob link
        $disk.MediaLink = $targetBlob.ICloudBlob.Uri.AbsoluteUri
    }

    # Wait until all vhd files are copied.
    $diskComplete = @()
    do
    {
        Write-Host "`n[WORKITEM] - Waiting for all disk copy toocomplete. Checking status every $CopyStatusReportInterval seconds." -ForegroundColor Yellow
        # check status every 30 seconds
        Sleep -Seconds $CopyStatusReportInterval
        foreach ( $disk in $allDisksToCopy)
        {
            if ($diskComplete -contains $disk)
            {
                Continue
            }
            $blobName = $disk.MediaLink.Segments[2]
            $copyState = Get-AzureStorageBlobCopyState -Blob $blobName -Container vhds -Context $destContext
            if ($copyState.Status -eq "Success")
            {
                Write-Host "`n[Status] - Success for disk copy $($disk.DiskName) at $($copyState.CompletionTime)" -ForegroundColor Green
                $diskComplete += $disk
            }
            else
            {
                if ($copyState.TotalBytes -gt 0)
                {
                    $percent = ($copyState.BytesCopied / $copyState.TotalBytes) * 100
                    Write-Host "`n[Status] - $('{0:N2}' -f $percent)% Complete for disk copy $($disk.DiskName)" -ForegroundColor Green
                }
            }
        }
    }
    while($diskComplete.Count -lt $allDisksToCopy.Count)

    #######################################################################
    #  Create a new vm
    #  hello new VM can be created from hello copied disks or hello original os disk.
    #  You can ddd your own logic here toosatisfy your specific requirements of hello vm.
    #######################################################################

    # Create a VM from hello existing os disk
    if ($DataDiskOnly)
    {
        $vm = New-AzureVMConfig -Name $DestVMName -InstanceSize $DestVMSize -DiskName $sourceOSDisk.DiskName
    }
    else
    {
        $newOSDisk = Add-AzureDisk -OS $sourceOSDisk.OS -DiskName ($sourceOSDisk.DiskName + $DiskNameSuffix) -MediaLocation $destOSVHD.ICloudBlob.Uri.AbsoluteUri
        $vm = New-AzureVMConfig -Name $DestVMName -InstanceSize $DestVMSize -DiskName $newOSDisk.DiskName
    }
    # Attached hello copied data disks toohello new VM
    foreach ($dataDisk in $sourceDataDisks)
    {
        # add -DiskLabel $dataDisk.DiskLabel if there are labels for disks of hello source vm
        $diskLabel = "drive" + $dataDisk.Lun
        $vm | Add-AzureDataDisk -ImportFrom -DiskLabel $diskLabel -LUN $dataDisk.Lun -MediaLocation $dataDisk.MediaLink
    }

    # Edit this if you want tooadd more custimization toohello new VM
    # $vm | Add-AzureEndpoint -Protocol tcp -LocalPort 443 -PublicPort 443 -Name 'HTTPs'
    # $vm | Set-AzureSubnet "PubSubnet","PrivSubnet"

    New-AzureVM -ServiceName $DestServiceName -VMs $vm -Location $Location
```

#### <span data-ttu-id="8396d-445"><a name="optimization"></a>En iyi duruma getirme</span><span class="sxs-lookup"><span data-stu-id="8396d-445"><a name="optimization"></a>Optimization</span></span>
<span data-ttu-id="8396d-446">Geçerli VM yapılandırmanızı özelleştirilebilir özellikle toowork standart diskler ile iyi.</span><span class="sxs-lookup"><span data-stu-id="8396d-446">Your current VM configuration may be customized specifically toowork well with Standard disks.</span></span> <span data-ttu-id="8396d-447">Şeritli birim içinde birçok diskleri kullanarak örneği için tooincrease hello performans.</span><span class="sxs-lookup"><span data-stu-id="8396d-447">For instance, tooincrease hello performance by using many disks in a striped volume.</span></span> <span data-ttu-id="8396d-448">Örneğin, 4 disk ayrı olarak Premium depolama kullanmak yerine, mümkün toooptimize hello maliyet tek bir disk sağlayarak olabilir.</span><span class="sxs-lookup"><span data-stu-id="8396d-448">For example, instead of using 4 disks separately on Premium Storage, you may be able toooptimize hello cost by having a single disk.</span></span> <span data-ttu-id="8396d-449">En iyi duruma getirme, bir olay temelinde işlenen bu gereksinimi toobe ister ve hello geçişten sonra özel adımlar gerektirir.</span><span class="sxs-lookup"><span data-stu-id="8396d-449">Optimizations like this need toobe handled on a case by case basis and require custom steps after hello migration.</span></span> <span data-ttu-id="8396d-450">Ayrıca, bu işlem veritabanları ve hello Ayarları'nda tanımlanan hello disk düzeni kullanan uygulamalar için düzgün çalışmayabilir unutmayın.</span><span class="sxs-lookup"><span data-stu-id="8396d-450">Also, note that this process may not well work for databases and applications that depend on hello disk layout defined in hello setup.</span></span>

##### <a name="preparation"></a><span data-ttu-id="8396d-451">Hazırlama</span><span class="sxs-lookup"><span data-stu-id="8396d-451">Preparation</span></span>
1. <span data-ttu-id="8396d-452">Tam hello basit hello açıklandığı gibi geçiş bölümüne.</span><span class="sxs-lookup"><span data-stu-id="8396d-452">Complete hello Simple Migration as described in hello earlier section.</span></span> <span data-ttu-id="8396d-453">En iyi duruma getirme hello üzerinde gerçekleştirilecek hello geçişten sonra yeni VM.</span><span class="sxs-lookup"><span data-stu-id="8396d-453">Optimizations will be performed on hello new VM after hello migration.</span></span>
2. <span data-ttu-id="8396d-454">En iyi duruma getirilmiş hello için gerekli hello yeni disk boyutları tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="8396d-454">Define hello new disk sizes needed for hello optimized configuration.</span></span>
3. <span data-ttu-id="8396d-455">Merhaba geçerli diskleri/birimler toohello yeni disk belirtimleri eşlenmesini belirler.</span><span class="sxs-lookup"><span data-stu-id="8396d-455">Determine mapping of hello current disks/volumes toohello new disk specifications.</span></span>

##### <a name="execution-steps"></a><span data-ttu-id="8396d-456">Yürütme adımları</span><span class="sxs-lookup"><span data-stu-id="8396d-456">Execution steps</span></span>
1. <span data-ttu-id="8396d-457">Merhaba hello doğru boyutta hello Premium Storage VM'si üzerinde yeni diskleri oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8396d-457">Create hello new disks with hello right sizes on hello Premium Storage VM.</span></span>
2. <span data-ttu-id="8396d-458">Oturum açma toohello VM ve kopyalama hello verileri diskten toothat birimi eşler hello geçerli birim toohello yeni.</span><span class="sxs-lookup"><span data-stu-id="8396d-458">Login toohello VM and copy hello data from hello current volume toohello new disk that maps toothat volume.</span></span> <span data-ttu-id="8396d-459">Toomap tooa yeni disk gereken tüm hello geçerli birimleri için bunu.</span><span class="sxs-lookup"><span data-stu-id="8396d-459">Do this for all hello current volumes that need toomap tooa new disk.</span></span>
3. <span data-ttu-id="8396d-460">Ardından, hello uygulama ayarları tooswitch toohello yeni diskleri değiştirme ve hello eski birimlerin ayırma.</span><span class="sxs-lookup"><span data-stu-id="8396d-460">Next, change hello application settings tooswitch toohello new disks, and detach hello old volumes.</span></span>

<span data-ttu-id="8396d-461">Merhaba uygulama daha iyi disk performans ayarlaması için çok başvurun[uygulama performansı en iyi duruma getirme](storage-premium-storage-performance.md#optimizing-application-performance).</span><span class="sxs-lookup"><span data-stu-id="8396d-461">For tuning hello application for better disk performance, please refer too[Optimizing Application Performance](storage-premium-storage-performance.md#optimizing-application-performance).</span></span>

### <a name="application-migrations"></a><span data-ttu-id="8396d-462">Uygulama geçişleri</span><span class="sxs-lookup"><span data-stu-id="8396d-462">Application migrations</span></span>
<span data-ttu-id="8396d-463">Veritabanları ve diğer karmaşık uygulamalar hello geçiş hello uygulama sağlayıcısı tarafından tanımlanan özel adımlar gerektirebilir.</span><span class="sxs-lookup"><span data-stu-id="8396d-463">Databases and other complex applications may require special steps as defined by hello application provider for hello migration.</span></span> <span data-ttu-id="8396d-464">Lütfen toorespective uygulama belgelerine bakın.</span><span class="sxs-lookup"><span data-stu-id="8396d-464">Please refer toorespective application documentation.</span></span> <span data-ttu-id="8396d-465">Örneğin</span><span class="sxs-lookup"><span data-stu-id="8396d-465">E.g.</span></span> <span data-ttu-id="8396d-466">veritabanlarını yedekleme genellikle geçirilebilecek ve geri yükleme.</span><span class="sxs-lookup"><span data-stu-id="8396d-466">typically databases can be migrated through backup and restore.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8396d-467">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8396d-467">Next steps</span></span>
<span data-ttu-id="8396d-468">Sanal makineleri geçirmek için belirli senaryolar için kaynaklar aşağıdaki hello bakın:</span><span class="sxs-lookup"><span data-stu-id="8396d-468">See hello following resources for specific scenarios for migrating virtual machines:</span></span>

* [<span data-ttu-id="8396d-469">Azure sanal makineleri depolama hesapları arasında geçiş</span><span class="sxs-lookup"><span data-stu-id="8396d-469">Migrate Azure Virtual Machines between Storage Accounts</span></span>](https://azure.microsoft.com/blog/2014/10/22/migrate-azure-virtual-machines-between-storage-accounts/)
* [<span data-ttu-id="8396d-470">Oluşturun ve Windows Server VHD tooAzure yükleyin.</span><span class="sxs-lookup"><span data-stu-id="8396d-470">Create and upload a Windows Server VHD tooAzure.</span></span>](../../virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [<span data-ttu-id="8396d-471">Oluşturma ve bir Sanal Sabit Disk, Linux işletim sistemi içerir hello karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="8396d-471">Creating and Uploading a Virtual Hard Disk that Contains hello Linux Operating System</span></span>](../../virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="8396d-472">Amazon AWS tooMicrosoft Azure sanal makinelerden geçirme</span><span class="sxs-lookup"><span data-stu-id="8396d-472">Migrating Virtual Machines from Amazon AWS tooMicrosoft Azure</span></span>](http://channel9.msdn.com/Series/Migrating-Virtual-Machines-from-Amazon-AWS-to-Microsoft-Azure)

<span data-ttu-id="8396d-473">Ayrıca, Azure Storage ve Azure sanal makineler hakkında daha fazla kaynak toolearn aşağıdaki hello bakın:</span><span class="sxs-lookup"><span data-stu-id="8396d-473">Also, see hello following resources toolearn more about Azure Storage and Azure Virtual Machines:</span></span>

* [<span data-ttu-id="8396d-474">Azure Depolama</span><span class="sxs-lookup"><span data-stu-id="8396d-474">Azure Storage</span></span>](https://azure.microsoft.com/documentation/services/storage/)
* [<span data-ttu-id="8396d-475">Azure sanal makineler</span><span class="sxs-lookup"><span data-stu-id="8396d-475">Azure Virtual Machines</span></span>](https://azure.microsoft.com/documentation/services/virtual-machines/)
* [<span data-ttu-id="8396d-476">Premium Depolama: Azure Sanal Makine İş Yükleri için Yüksek Performanslı Depolama</span><span class="sxs-lookup"><span data-stu-id="8396d-476">Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads</span></span>](storage-premium-storage.md)

[1]:./media/storage-migration-to-premium-storage/migration-to-premium-storage-1.png
[2]:./media/storage-migration-to-premium-storage/migration-to-premium-storage-1.png
[3]:./media/storage-migration-to-premium-storage/migration-to-premium-storage-3.png
[4]: http://technet.microsoft.com/library/hh831739.aspx
