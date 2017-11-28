---
title: "Azure Premium Depolama'ya geçirme VM'ler | Microsoft Docs"
description: "Varolan Vm'lerinizi Azure Premium depolama alanına geçiş. Premium Storage, Azure sanal makinelerde çalışan g/Ç kullanımı yoğun iş yükleri için yüksek performanslı, düşük gecikmeli disk desteği sağlar."
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
ms.openlocfilehash: ca893f87b155a92c457e3bf6d9d39aaf86bf5fb3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="migrating-to-azure-premium-storage-unmanaged-disks"></a><span data-ttu-id="96e89-104">Azure Premium Storage (yönetilmeyen diskleri) geçirme</span><span class="sxs-lookup"><span data-stu-id="96e89-104">Migrating to Azure Premium Storage (Unmanaged Disks)</span></span>

> [!NOTE]
> <span data-ttu-id="96e89-105">Bu makalede, yönetilmeyen premium diskleri kullanan bir VM için yönetilmeyen standart diskler kullanan bir VM geçirme açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="96e89-105">This article discusses how to migrate a VM that uses unmanaged standard disks to a VM that uses unmanaged premium disks.</span></span> <span data-ttu-id="96e89-106">Azure yönetilen diskleri yeni VM'ler için kullanın ve önceki yönetilmeyen disklerinizi yönetilen Diske Dönüştür öneririz.</span><span class="sxs-lookup"><span data-stu-id="96e89-106">We recommend that you use Azure Managed Disks for new VMs, and that you convert your previous unmanaged disks to managed disks.</span></span> <span data-ttu-id="96e89-107">Diskleri tanıtıcı zorunda kalmamak için temel alınan depolama hesapları yönetilen.</span><span class="sxs-lookup"><span data-stu-id="96e89-107">Managed Disks handle the underlying storage accounts so you don't have to.</span></span> <span data-ttu-id="96e89-108">Daha fazla bilgi için lütfen bkz bizim [yönetilen diskleri genel bakış](../../virtual-machines/windows/managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="96e89-108">For more information, please see our [Managed Disks Overview](../../virtual-machines/windows/managed-disks-overview.md).</span></span>
>

<span data-ttu-id="96e89-109">Azure Premium depolama g/Ç kullanımı yoğun iş yükleri çalıştıran sanal makineler için yüksek performanslı, düşük gecikmeli disk desteği sunar.</span><span class="sxs-lookup"><span data-stu-id="96e89-109">Azure Premium Storage delivers high-performance, low-latency disk support for virtual machines running I/O-intensive workloads.</span></span> <span data-ttu-id="96e89-110">Uygulamanızın VM diskleri için Azure Premium Depolama'ya geçiş yaparak hızını avantajlarından ve bu disklerin performansını alabilir.</span><span class="sxs-lookup"><span data-stu-id="96e89-110">You can take advantage of the speed and performance of these disks by migrating your application's VM disks to Azure Premium Storage.</span></span>

<span data-ttu-id="96e89-111">Bu kılavuzun amacı, Premium depolama kendi geçerli sisteminden sorunsuz bir geçiş yapmak hazırlama yeni kullanıcılar Azure Premium Storage daha iyi yardımcı olmaktır.</span><span class="sxs-lookup"><span data-stu-id="96e89-111">The purpose of this guide is to help new users of Azure Premium Storage better prepare to make a smooth transition from their current system to Premium Storage.</span></span> <span data-ttu-id="96e89-112">Kılavuzu üç anahtar bileşenleri bu süreçte ele alır:</span><span class="sxs-lookup"><span data-stu-id="96e89-112">The guide addresses three of the key components in this process:</span></span>

* [<span data-ttu-id="96e89-113">Premium depolama geçişi planlama</span><span class="sxs-lookup"><span data-stu-id="96e89-113">Plan for the Migration to Premium Storage</span></span>](#plan-the-migration-to-premium-storage)
* [<span data-ttu-id="96e89-114">Hazırlama ve sanal sabit diskleri (VHD) Premium depolama alanına kopyalama</span><span class="sxs-lookup"><span data-stu-id="96e89-114">Prepare and Copy Virtual Hard Disks (VHDs) to Premium Storage</span></span>](#prepare-and-copy-virtual-hard-disks-VHDs-to-premium-storage)
* [<span data-ttu-id="96e89-115">Premium depolama kullanarak Azure sanal makine oluşturun</span><span class="sxs-lookup"><span data-stu-id="96e89-115">Create Azure Virtual Machine using Premium Storage</span></span>](#create-azure-virtual-machine-using-premium-storage)

<span data-ttu-id="96e89-116">Diğer platformlarından Azure Premium Storage Vm'leri geçirme veya var olan Azure VM'ler standart depolama biriminden Premium bir depolama alanına geçiş.</span><span class="sxs-lookup"><span data-stu-id="96e89-116">You can either migrate VMs from other platforms to Azure Premium Storage or migrate existing Azure VMs from Standard Storage to Premium Storage.</span></span> <span data-ttu-id="96e89-117">Bu kılavuz, her iki iki senaryo adımları kapsar.</span><span class="sxs-lookup"><span data-stu-id="96e89-117">This guide covers steps for both two scenarios.</span></span> <span data-ttu-id="96e89-118">Senaryonuza bağlı olarak ilgili bölümdeki belirtilen adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="96e89-118">Follow the steps specified in the relevant section depending on your scenario.</span></span>

> [!NOTE]
> <span data-ttu-id="96e89-119">Özelliklere genel bakış ve Premium depolama, Premium Storage fiyatlandırma bulabilirsiniz: [Azure sanal makine iş yükleri için yüksek performanslı depolama](storage-premium-storage.md).</span><span class="sxs-lookup"><span data-stu-id="96e89-119">You can find a feature overview and pricing of Premium Storage in Premium Storage: [High-Performance Storage for Azure Virtual Machine Workloads](storage-premium-storage.md).</span></span> <span data-ttu-id="96e89-120">Uygulamanız için en iyi performans için Azure Premium Depolama'ya yüksek IOPS gerektiren herhangi bir sanal makine disk geçirme öneririz.</span><span class="sxs-lookup"><span data-stu-id="96e89-120">We recommend migrating any virtual machine disk requiring high IOPS to Azure Premium Storage for the best performance for your application.</span></span> <span data-ttu-id="96e89-121">Diskinizin yüksek IOPS gerektirmiyorsa SSD yerine Sabit Disk sürücülerinin (HDD'ler) üzerinde sanal makine disk verilerini depolayan standart depolama tutarak maliyetleri sınırlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="96e89-121">If your disk does not require high IOPS, you can limit costs by maintaining it in Standard Storage, which stores virtual machine disk data on Hard Disk Drives (HDDs) instead of SSDs.</span></span>
>

<span data-ttu-id="96e89-122">Bütün geçiş işlemini tamamlama öncesinde ve sonrasında bu kılavuzda sağlanan adımları ek eylemler gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="96e89-122">Completing the migration process in its entirety may require additional actions both before and after the steps provided in this guide.</span></span> <span data-ttu-id="96e89-123">Sanal ağlar veya uç noktaların yapılandırma veya uygulamanızda miktar kapalı kalma süresi gerektirebilecek uygulamanın kendisinden kodda değişiklikler yaparak örnek olarak verilebilir.</span><span class="sxs-lookup"><span data-stu-id="96e89-123">Examples include configuring virtual networks or endpoints or making code changes within the application itself which may require some downtime in your application.</span></span> <span data-ttu-id="96e89-124">Bu eylemler her uygulama için benzersiz ve bunları birlikte tam geçiş Premium depolama alanına mümkün olduğunca sorunsuz yapmak için bu kılavuzda sağlanan adımları tamamlamanız.</span><span class="sxs-lookup"><span data-stu-id="96e89-124">These actions are unique to each application, and you should complete them along with the steps provided in this guide to make the full transition to Premium Storage as seamless as possible.</span></span>

## <span data-ttu-id="96e89-125"><a name="plan-the-migration-to-premium-storage"></a>Premium depolama geçişi planlama</span><span class="sxs-lookup"><span data-stu-id="96e89-125"><a name="plan-the-migration-to-premium-storage"></a>Plan for the migration to Premium Storage</span></span>
<span data-ttu-id="96e89-126">Bu bölümde, bu makaledeki geçiş adımları uygulamaya hazır olduğunu ve VM ve Disk türlerinde en iyi kararı vermenize yardımcı olur sağlar.</span><span class="sxs-lookup"><span data-stu-id="96e89-126">This section ensures that you are ready to follow the migration steps in this article, and helps you to make the best decision on VM and Disk types.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="96e89-127">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="96e89-127">Prerequisites</span></span>
* <span data-ttu-id="96e89-128">Bir Azure aboneliği gerekir.</span><span class="sxs-lookup"><span data-stu-id="96e89-128">You will need an Azure subscription.</span></span> <span data-ttu-id="96e89-129">Yoksa, bir aylık oluşturabilirsiniz [ücretsiz deneme sürümü](https://azure.microsoft.com/pricing/free-trial/) abonelik veya ziyaret [Azure fiyatlandırma](https://azure.microsoft.com/pricing/) daha fazla seçenek için.</span><span class="sxs-lookup"><span data-stu-id="96e89-129">If you don't have one, you can create a one-month [free trial](https://azure.microsoft.com/pricing/free-trial/) subscription or visit [Azure Pricing](https://azure.microsoft.com/pricing/) for more options.</span></span>
* <span data-ttu-id="96e89-130">PowerShell cmdlet'lerini çalıştırmak için Microsoft Azure PowerShell modülü gerekir.</span><span class="sxs-lookup"><span data-stu-id="96e89-130">To execute PowerShell cmdlets, you will need the Microsoft Azure PowerShell module.</span></span> <span data-ttu-id="96e89-131">Yükleme noktası ve yükleme yönergeleri için bkz. [Azure PowerShell’i yükleme ve yapılandırma](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="96e89-131">See [How to install and configure Azure PowerShell](/powershell/azure/overview) for the install point and installation instructions.</span></span>
* <span data-ttu-id="96e89-132">Azure Premium depolama üzerinde çalışan Vm'leri kullanmak planlama yaparken, Premium depolama yeteneğine sahip sanal makineleri kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="96e89-132">When you plan to use Azure VMs running on Premium Storage, you need to use the Premium Storage capable VMs.</span></span> <span data-ttu-id="96e89-133">Premium depolama yeteneğine sahip sanal makineleri ile standart ve Premium depolama diskleri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="96e89-133">You can use both Standard and Premium Storage disks with Premium Storage capable VMs.</span></span> <span data-ttu-id="96e89-134">Premium depolama diskleri gelecekte daha fazla VM türleriyle kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="96e89-134">Premium storage disks will be available with more VM types in the future.</span></span> <span data-ttu-id="96e89-135">Tüm kullanılabilir Azure VM disk türleri ve boyutları hakkında daha fazla bilgi için bkz: [sanal makineler için Boyutlar](../../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) ve [Cloud Services boyutları](../../cloud-services/cloud-services-sizes-specs.md).</span><span class="sxs-lookup"><span data-stu-id="96e89-135">For more information on all available Azure VM disk types and sizes, see [Sizes for virtual machines](../../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) and [Sizes for Cloud Services](../../cloud-services/cloud-services-sizes-specs.md).</span></span>

### <a name="considerations"></a><span data-ttu-id="96e89-136">Dikkat edilmesi gerekenler</span><span class="sxs-lookup"><span data-stu-id="96e89-136">Considerations</span></span>
<span data-ttu-id="96e89-137">Bir Azure VM uygulamalarınızı en fazla 256 TB depolama VM başına böylece birkaç Premium depolama diskleri ekleme destekler.</span><span class="sxs-lookup"><span data-stu-id="96e89-137">An Azure VM supports attaching several Premium Storage disks so that your applications can have up to 256 TB of storage per VM.</span></span> <span data-ttu-id="96e89-138">Premium depolama ile uygulamalarınızı, ikinci disk işleme VM başına okuma işlemleri için son derece düşük gecikme ile başına VM ve 2000 MB başına 80.000 IOPS (saniye başına girdi/çıktı işlemleri) elde edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="96e89-138">With Premium Storage, your applications can achieve 80,000 IOPS (input/output operations per second) per VM and 2000 MB per second disk throughput per VM with extremely low latencies for read operations.</span></span> <span data-ttu-id="96e89-139">VM'ler ve diskleri çeşitli seçeneğiniz vardır.</span><span class="sxs-lookup"><span data-stu-id="96e89-139">You have options in a variety of VMs and Disks.</span></span> <span data-ttu-id="96e89-140">Bu bölümde, iş yükünüzü uygun bir seçeneği bulmak için yardımcı olmaktır.</span><span class="sxs-lookup"><span data-stu-id="96e89-140">This section is to help you to find an option that best suits your workload.</span></span>

#### <a name="vm-sizes"></a><span data-ttu-id="96e89-141">VM boyutları</span><span class="sxs-lookup"><span data-stu-id="96e89-141">VM sizes</span></span>
<span data-ttu-id="96e89-142">Azure VM boyutu belirtimleri listelenen [sanal makineler için Boyutlar](../../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="96e89-142">The Azure VM size specifications are listed in [Sizes for virtual machines](../../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="96e89-143">Premium Storage ile birlikte çalışmak ve İş yükünüzün uygun en uygun VM boyutunu seçin sanal makineleri performans özelliklerini gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="96e89-143">Review the performance characteristics of virtual machines that work with Premium Storage and choose the most appropriate VM size that best suits your workload.</span></span> <span data-ttu-id="96e89-144">Yeterli bant genişliği kullanılabilir disk trafiği sürücü için de kendi VM'nizi bulunduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="96e89-144">Make sure that there is sufficient bandwidth available on your VM to drive the disk traffic.</span></span>

#### <a name="disk-sizes"></a><span data-ttu-id="96e89-145">Disk boyutları</span><span class="sxs-lookup"><span data-stu-id="96e89-145">Disk sizes</span></span>
<span data-ttu-id="96e89-146">VM ile kullanılan diskler beş tür vardır ve her belirli IOPS ve üretilen iş sahip sınırlar.</span><span class="sxs-lookup"><span data-stu-id="96e89-146">There are five types of disks that can be used with your VM and each has specific IOPs and throughput limits.</span></span> <span data-ttu-id="96e89-147">Bu sınırlar yoğun yükler ve kapasite, performans, ölçeklenebilirlik açısından, uygulamanızın gereksinimlerine, VM için disk türü seçme temel yaparken dikkate.</span><span class="sxs-lookup"><span data-stu-id="96e89-147">Take into consideration these limits when choosing the disk type for your VM based on the needs of your application in terms of capacity, performance, scalability, and peak loads.</span></span>

| <span data-ttu-id="96e89-148">Premium diskler türü</span><span class="sxs-lookup"><span data-stu-id="96e89-148">Premium Disks Type</span></span>  | <span data-ttu-id="96e89-149">P10</span><span class="sxs-lookup"><span data-stu-id="96e89-149">P10</span></span>   | <span data-ttu-id="96e89-150">P20</span><span class="sxs-lookup"><span data-stu-id="96e89-150">P20</span></span>   | <span data-ttu-id="96e89-151">P30</span><span class="sxs-lookup"><span data-stu-id="96e89-151">P30</span></span>            | <span data-ttu-id="96e89-152">P40</span><span class="sxs-lookup"><span data-stu-id="96e89-152">P40</span></span>            | <span data-ttu-id="96e89-153">P50</span><span class="sxs-lookup"><span data-stu-id="96e89-153">P50</span></span>            | 
|:-------------------:|:-----:|:-----:|:--------------:|:--------------:|:--------------:|
| <span data-ttu-id="96e89-154">Disk boyutu</span><span class="sxs-lookup"><span data-stu-id="96e89-154">Disk size</span></span>           | <span data-ttu-id="96e89-155">128 GB</span><span class="sxs-lookup"><span data-stu-id="96e89-155">128 GB</span></span>| <span data-ttu-id="96e89-156">512 GB</span><span class="sxs-lookup"><span data-stu-id="96e89-156">512 GB</span></span>| <span data-ttu-id="96e89-157">1024 GB (1 TB)</span><span class="sxs-lookup"><span data-stu-id="96e89-157">1024 GB (1 TB)</span></span> | <span data-ttu-id="96e89-158">2048 GB (2 TB)</span><span class="sxs-lookup"><span data-stu-id="96e89-158">2048 GB (2 TB)</span></span> | <span data-ttu-id="96e89-159">4095 GB (4 TB)</span><span class="sxs-lookup"><span data-stu-id="96e89-159">4095 GB (4 TB)</span></span> | 
| <span data-ttu-id="96e89-160">Disk başına IOPS</span><span class="sxs-lookup"><span data-stu-id="96e89-160">IOPS per disk</span></span>       | <span data-ttu-id="96e89-161">500</span><span class="sxs-lookup"><span data-stu-id="96e89-161">500</span></span>   | <span data-ttu-id="96e89-162">2300</span><span class="sxs-lookup"><span data-stu-id="96e89-162">2300</span></span>  | <span data-ttu-id="96e89-163">5000</span><span class="sxs-lookup"><span data-stu-id="96e89-163">5000</span></span>           | <span data-ttu-id="96e89-164">7500</span><span class="sxs-lookup"><span data-stu-id="96e89-164">7500</span></span>           | <span data-ttu-id="96e89-165">7500</span><span class="sxs-lookup"><span data-stu-id="96e89-165">7500</span></span>           | 
| <span data-ttu-id="96e89-166">Disk başına aktarım hızı</span><span class="sxs-lookup"><span data-stu-id="96e89-166">Throughput per disk</span></span> | <span data-ttu-id="96e89-167">Saniyede 100 MB</span><span class="sxs-lookup"><span data-stu-id="96e89-167">100 MB per second</span></span> | <span data-ttu-id="96e89-168">150 MB / saniye</span><span class="sxs-lookup"><span data-stu-id="96e89-168">150 MB per second</span></span> | <span data-ttu-id="96e89-169">200 MB / saniye</span><span class="sxs-lookup"><span data-stu-id="96e89-169">200 MB per second</span></span> | <span data-ttu-id="96e89-170">Saniye başına 250 MB</span><span class="sxs-lookup"><span data-stu-id="96e89-170">250 MB per second</span></span> | <span data-ttu-id="96e89-171">Saniye başına 250 MB</span><span class="sxs-lookup"><span data-stu-id="96e89-171">250 MB per second</span></span> |

<span data-ttu-id="96e89-172">İş yükünüz bağlı olarak, ek veri disklerinin VM için gerekli olup olmadığını belirleyin.</span><span class="sxs-lookup"><span data-stu-id="96e89-172">Depending on your workload, determine if additional data disks are necessary for your VM.</span></span> <span data-ttu-id="96e89-173">VM'nize birden çok kalıcı veri disk ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="96e89-173">You can attach several persistent data disks to your VM.</span></span> <span data-ttu-id="96e89-174">Gerekirse, kapasite ve birim performansını artırmak için bu disklere şeritler.</span><span class="sxs-lookup"><span data-stu-id="96e89-174">If needed, you can stripe across the disks to increase the capacity and performance of the volume.</span></span> <span data-ttu-id="96e89-175">(Disk şeritleme görmek [burada](storage-premium-storage-performance.md#disk-striping).) Premium depolama veri diskleri kullanarak şeritler varsa [depolama alanları][4], kullanılan her disk için bir sütun ile yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="96e89-175">(See what is Disk Striping [here](storage-premium-storage-performance.md#disk-striping).) If you stripe Premium Storage data disks using [Storage Spaces][4], you should configure it with one column for each disk that is used.</span></span> <span data-ttu-id="96e89-176">Aksi takdirde, disklerde şeritli birim genel performansını trafik düzensiz dağıtım nedeniyle beklenenden daha düşük olabilir.</span><span class="sxs-lookup"><span data-stu-id="96e89-176">Otherwise, the overall performance of the striped volume may be lower than expected due to uneven distribution of traffic across the disks.</span></span> <span data-ttu-id="96e89-177">Linux VM'ler için kullandığınız *mdadm* aynı elde etmek için yardımcı programı.</span><span class="sxs-lookup"><span data-stu-id="96e89-177">For Linux VMs you can use the *mdadm* utility to achieve the same.</span></span> <span data-ttu-id="96e89-178">Makalesine bakın [yapılandırma yazılım RAID Linux'ta](../../virtual-machines/linux/configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="96e89-178">See article [Configure Software RAID on Linux](../../virtual-machines/linux/configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for details.</span></span>

#### <a name="storage-account-scalability-targets"></a><span data-ttu-id="96e89-179">Depolama hesabımın ölçeklenebilirlik hedefleri</span><span class="sxs-lookup"><span data-stu-id="96e89-179">Storage account scalability targets</span></span>
<span data-ttu-id="96e89-180">Premium depolama hesapları sahip ek olarak aşağıdaki ölçeklenebilirlik hedefleri [Azure Storage ölçeklenebilirlik ve performans hedefleri](storage-scalability-targets.md).</span><span class="sxs-lookup"><span data-stu-id="96e89-180">Premium Storage accounts have the following scalability targets in addition to the [Azure Storage Scalability and Performance Targets](storage-scalability-targets.md).</span></span> <span data-ttu-id="96e89-181">Uygulamanızın gereksinimleri tek bir depolama hesabı ölçeklenebilirlik hedeflerini aşarsa, birden çok depolama hesabı kullanmak için uygulamanızı oluşturmak ve bu depolama hesaplarında verilerinizi bölüm.</span><span class="sxs-lookup"><span data-stu-id="96e89-181">If your application requirements exceed the scalability targets of a single storage account, build your application to use multiple storage accounts, and partition your data across those storage accounts.</span></span>

| <span data-ttu-id="96e89-182">Toplam hesabı kapasitesi</span><span class="sxs-lookup"><span data-stu-id="96e89-182">Total Account Capacity</span></span> | <span data-ttu-id="96e89-183">Yerel olarak yedekli depolama hesabı için toplam bant genişliği</span><span class="sxs-lookup"><span data-stu-id="96e89-183">Total Bandwidth for a Locally Redundant Storage Account</span></span> |
|:--- |:--- |
| <span data-ttu-id="96e89-184">Disk kapasitesi: 35TB</span><span class="sxs-lookup"><span data-stu-id="96e89-184">Disk capacity: 35TB</span></span><br /><span data-ttu-id="96e89-185">Kapasite anlık görüntü: 10 TB</span><span class="sxs-lookup"><span data-stu-id="96e89-185">Snapshot capacity: 10 TB</span></span> |<span data-ttu-id="96e89-186">Gelen + giden için saniye başına en fazla 50 Gigabit</span><span class="sxs-lookup"><span data-stu-id="96e89-186">Up to 50 gigabits per second for Inbound + Outbound</span></span> |

<span data-ttu-id="96e89-187">Premium depolama özellikleri hakkında daha fazla bilgi için kullanıma [ölçeklenebilirlik ve performans Premium depolama kullanırken hedefleri](storage-premium-storage.md#scalability-and-performance-targets).</span><span class="sxs-lookup"><span data-stu-id="96e89-187">For the more information on Premium Storage specifications, check out [Scalability and Performance Targets when using Premium Storage](storage-premium-storage.md#scalability-and-performance-targets).</span></span>

#### <a name="disk-caching-policy"></a><span data-ttu-id="96e89-188">Önbellek İlkesi disk</span><span class="sxs-lookup"><span data-stu-id="96e89-188">Disk caching policy</span></span>
<span data-ttu-id="96e89-189">Varsayılan olarak, ilke önbelleğe alma disktir *salt okunur* tüm Premium veri diskleri için ve *okuma-yazma* için Premium işletim sistemi diski VM'ye eklenmiş.</span><span class="sxs-lookup"><span data-stu-id="96e89-189">By default, disk caching policy is *Read-Only* for all the Premium data disks, and *Read-Write* for the Premium operating system disk attached to the VM.</span></span> <span data-ttu-id="96e89-190">Bu yapılandırma ayarının uygulamanızın IOs için en iyi performans elde etmek için önerilir.</span><span class="sxs-lookup"><span data-stu-id="96e89-190">This configuration setting is recommended to achieve the optimal performance for your application's IOs.</span></span> <span data-ttu-id="96e89-191">(SQL Server günlük dosyaları gibi) ağır yazma ya da salt yazılır veri diskleri için daha iyi uygulama performansı elde etmek için disk önbelleğe almayı devre dışı bırakın.</span><span class="sxs-lookup"><span data-stu-id="96e89-191">For write-heavy or write-only data disks (such as SQL Server log files), disable disk caching so that you can achieve better application performance.</span></span> <span data-ttu-id="96e89-192">Mevcut veri diskleri için önbellek ayarlarını kullanarak güncelleştirilebilir [Azure Portal](https://portal.azure.com) veya *- HostCaching* parametresinin *kümesi AzureDataDisk* cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="96e89-192">The cache settings for existing data disks can be updated using [Azure Portal](https://portal.azure.com) or the *-HostCaching* parameter of the *Set-AzureDataDisk* cmdlet.</span></span>

#### <a name="location"></a><span data-ttu-id="96e89-193">Konum</span><span class="sxs-lookup"><span data-stu-id="96e89-193">Location</span></span>
<span data-ttu-id="96e89-194">Azure Premium Storage kullanılabilir olduğu bir konum seçin.</span><span class="sxs-lookup"><span data-stu-id="96e89-194">Pick a location where Azure Premium Storage is available.</span></span> <span data-ttu-id="96e89-195">Bkz: [bölgeye göre Azure Hizmetleri](https://azure.microsoft.com/regions/#services) kullanılabilir konumları hakkında güncel bilgi.</span><span class="sxs-lookup"><span data-stu-id="96e89-195">See [Azure Services by Region](https://azure.microsoft.com/regions/#services) for up-to-date information on available locations.</span></span> <span data-ttu-id="96e89-196">Depoları ayrı bölge içinde olup olmadığını daha çok daha iyi performans için VM diskleri sağlayabilir depolama hesabı ile aynı bölgede yer alan VM'ler.</span><span class="sxs-lookup"><span data-stu-id="96e89-196">VMs located in the same region as the Storage account that stores the disks for the VM will give much better performance than if they are in separate regions.</span></span>

#### <a name="other-azure-vm-configuration-settings"></a><span data-ttu-id="96e89-197">Diğer Azure VM yapılandırma ayarları</span><span class="sxs-lookup"><span data-stu-id="96e89-197">Other Azure VM configuration settings</span></span>
<span data-ttu-id="96e89-198">Bir Azure VM oluştururken, belirli VM ayarlarını yapılandırmak için istenir.</span><span class="sxs-lookup"><span data-stu-id="96e89-198">When creating an Azure VM, you will be asked to configure certain VM settings.</span></span> <span data-ttu-id="96e89-199">Değiştirme veya başkalarının daha sonra ekleme sırasında birkaç ayarlar VM ömrü boyunca sabit unutmayın.</span><span class="sxs-lookup"><span data-stu-id="96e89-199">Remember, few settings are fixed for the lifetime of the VM, while you can modify or add others later.</span></span> <span data-ttu-id="96e89-200">Bu Azure VM yapılandırma ayarlarını gözden geçirin ve bunları uygun şekilde, iş yükü gereksinimlerinize uyacak şekilde yapılandırıldığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="96e89-200">Review these Azure VM configuration settings and make sure that these are configured appropriately to match your workload requirements.</span></span>

### <a name="optimization"></a><span data-ttu-id="96e89-201">İyileştirme</span><span class="sxs-lookup"><span data-stu-id="96e89-201">Optimization</span></span>
<span data-ttu-id="96e89-202">[Azure Premium Storage: Tasarım için yüksek performanslı](storage-premium-storage-performance.md) Azure Premium Storage kullanarak yüksek performanslı uygulamalar oluşturmak için yönergeler sağlar.</span><span class="sxs-lookup"><span data-stu-id="96e89-202">[Azure Premium Storage: Design for High Performance](storage-premium-storage-performance.md) provides guidelines for building high-performance applications using Azure Premium Storage.</span></span> <span data-ttu-id="96e89-203">Performansı en iyi yöntemler, uygulamanız tarafından kullanılan teknolojiler uygulanabilir birlikte yönergeleri takip edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="96e89-203">You can follow the guidelines combined with performance best practices applicable to technologies used by your application.</span></span>

## <span data-ttu-id="96e89-204"><a name="prepare-and-copy-virtual-hard-disks-VHDs-to-premium-storage"></a>Hazırlama ve sanal sabit diskleri (VHD) Premium depolama alanına kopyalama</span><span class="sxs-lookup"><span data-stu-id="96e89-204"><a name="prepare-and-copy-virtual-hard-disks-VHDs-to-premium-storage"></a>Prepare and copy virtual hard disks (VHDs) to Premium Storage</span></span>
<span data-ttu-id="96e89-205">Aşağıdaki bölümde, sanal makineden VHD'ler hazırlama ve VHD Azure depolama alanına kopyalama için yönergeler sağlar.</span><span class="sxs-lookup"><span data-stu-id="96e89-205">The following section provides guidelines for preparing VHDs from your VM and copying VHDs to Azure Storage.</span></span>

* [<span data-ttu-id="96e89-206">Senaryo 1: "ı mevcut Azure VM'ler Azure Premium depolama alanına geçirme."</span><span class="sxs-lookup"><span data-stu-id="96e89-206">Scenario 1: "I am migrating existing Azure VMs to Azure Premium Storage."</span></span>](#scenario1)
* [<span data-ttu-id="96e89-207">Senaryo 2: "ı VM'ler diğer platformlarından Azure Premium depolama alanına geçirme."</span><span class="sxs-lookup"><span data-stu-id="96e89-207">Scenario 2: "I am migrating VMs from other platforms to Azure Premium Storage."</span></span>](#scenario2)

### <a name="prerequisites"></a><span data-ttu-id="96e89-208">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="96e89-208">Prerequisites</span></span>
<span data-ttu-id="96e89-209">VHD'leri geçişe hazırlamak için ihtiyacınız vardır:</span><span class="sxs-lookup"><span data-stu-id="96e89-209">To prepare the VHDs for migration, you'll need:</span></span>

* <span data-ttu-id="96e89-210">Bir Azure aboneliği, bir depolama hesabı ve bir kapsayıcıda bu depolama hesabı, VHD kopyalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="96e89-210">An Azure subscription, a storage account, and a container in that storage account to which you can copy your VHD.</span></span> <span data-ttu-id="96e89-211">Hedef depolama hesabının bir standart veya Premium depolama hesabı ihtiyacınıza olabileceğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="96e89-211">Note that the destination storage account can be a Standard or Premium Storage account depending on your requirement.</span></span>
* <span data-ttu-id="96e89-212">Birden çok VM örnekleri ondan oluşturmayı planlıyorsanız, VHD'yi genelleştirmek için bir araç.</span><span class="sxs-lookup"><span data-stu-id="96e89-212">A tool to generalize the VHD if you plan to create multiple VM instances from it.</span></span> <span data-ttu-id="96e89-213">Örneğin, sysprep Windows ya da Sanal Küp Str sysprep Ubuntu için.</span><span class="sxs-lookup"><span data-stu-id="96e89-213">For example, sysprep for Windows or virt-sysprep for Ubuntu.</span></span>
* <span data-ttu-id="96e89-214">Depolama hesabına VHD dosyasını yüklemek için bir araç.</span><span class="sxs-lookup"><span data-stu-id="96e89-214">A tool to upload the VHD file to the Storage account.</span></span> <span data-ttu-id="96e89-215">Bkz: [AzCopy komut satırı yardımcı programı ile veri aktarma](storage-use-azcopy.md) veya bir [Azure storage Gezgini](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx).</span><span class="sxs-lookup"><span data-stu-id="96e89-215">See [Transfer data with the AzCopy Command-Line Utility](storage-use-azcopy.md) or use an [Azure storage explorer](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx).</span></span> <span data-ttu-id="96e89-216">Bu kılavuzda AzCopy aracını kullanarak, VHD kopyalama açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="96e89-216">This guide describes copying your VHD using the AzCopy tool.</span></span>

> [!NOTE]
> <span data-ttu-id="96e89-217">AzCopy, zaman uyumlu kopyası seçeneğiyle seçerseniz en iyi performans için bu araçlardan biri, hedef depolama hesabının aynı bölgede bir Azure VM çalıştırarak, VHD'yi kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="96e89-217">If you choose synchronous copy option with AzCopy, for optimal performance, copy your VHD by running one of these tools from an Azure VM that is in the same region as the destination storage account.</span></span> <span data-ttu-id="96e89-218">Bir VHD farklı bir bölgede bir Azure VM kopyalıyorsanız performansınızı daha yavaş olabilir.</span><span class="sxs-lookup"><span data-stu-id="96e89-218">If you are copying a VHD from an Azure VM in a different region, your performance may be slower.</span></span>
>
> <span data-ttu-id="96e89-219">Sınırlı bant genişliği üzerinde büyük miktarda veri kopyalama için göz önünde bulundurun [Blob depolama alanına veri aktarmak için Azure içeri/dışarı aktarma hizmeti kullanma](../storage-import-export-service.md); Bu, Azure veri merkezinde sabit disk sürücülerine sevkiyat tarafından veri aktarım olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="96e89-219">For copying a large amount of data over limited bandwidth, consider [using the Azure Import/Export service to transfer data to Blob Storage](../storage-import-export-service.md); this allows you to transfer your data by shipping hard disk drives to an Azure datacenter.</span></span> <span data-ttu-id="96e89-220">Yalnızca standart depolama hesabı için veri kopyalamak için Azure içeri/dışarı aktarma hizmetini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="96e89-220">You can use the Azure Import/Export service to copy data to a standard storage account only.</span></span> <span data-ttu-id="96e89-221">Standart depolama hesabınızdaki veriler olduktan sonra kullanabilirsiniz [kopyalama Blob API](https://msdn.microsoft.com/library/azure/dd894037.aspx) veya premium depolama hesabınıza verileri aktarmak için Azcopy'yi.</span><span class="sxs-lookup"><span data-stu-id="96e89-221">Once the data is in your standard storage account, you can use either the [Copy Blob API](https://msdn.microsoft.com/library/azure/dd894037.aspx) or AzCopy to transfer the data to your premium storage account.</span></span>
>
> <span data-ttu-id="96e89-222">Microsoft Azure yalnızca sabit boyutlu VHD dosyalarını desteklediğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="96e89-222">Note that Microsoft Azure only supports fixed size VHD files.</span></span> <span data-ttu-id="96e89-223">VHDX dosyaları veya dinamik VHD desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="96e89-223">VHDX files or dynamic VHDs are not supported.</span></span> <span data-ttu-id="96e89-224">Dinamik VHD varsa, bunu sabit boyutlu kullanarak dönüştürebilirsiniz [Convert-VHD](http://technet.microsoft.com/library/hh848454.aspx) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="96e89-224">If you have a dynamic VHD, you can convert it to fixed size using the [Convert-VHD](http://technet.microsoft.com/library/hh848454.aspx) cmdlet.</span></span>
>
>

### <span data-ttu-id="96e89-225"><a name="scenario1"></a>Senaryo 1: "ı mevcut Azure VM'ler Azure Premium depolama alanına geçirme."</span><span class="sxs-lookup"><span data-stu-id="96e89-225"><a name="scenario1"></a>Scenario 1: "I am migrating existing Azure VMs to Azure Premium Storage."</span></span>
<span data-ttu-id="96e89-226">Mevcut Azure sanal makineleri geçiriyorsanız ve VM'yi durdurun, VHD istediğiniz VHD türü başına hazırlayın ve VHD AzCopy veya PowerShell ile kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="96e89-226">If you are migrating existing Azure VMs, stop the VM, prepare VHDs per the type of VHD you want, and then copy the VHD with AzCopy or PowerShell.</span></span>

<span data-ttu-id="96e89-227">VM temiz bir duruma geçirmek için tamamen aşağı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="96e89-227">The VM needs to be completely down to migrate a clean state.</span></span> <span data-ttu-id="96e89-228">Geçiş tamamlanana kadar bir kapalı kalma süresi olacaktır.</span><span class="sxs-lookup"><span data-stu-id="96e89-228">There will be a downtime until the migration completes.</span></span>

#### <a name="step-1-prepare-vhds-for-migration"></a><span data-ttu-id="96e89-229">1. Adım</span><span class="sxs-lookup"><span data-stu-id="96e89-229">Step 1.</span></span> <span data-ttu-id="96e89-230">VHD'ler geçiş için hazırlama</span><span class="sxs-lookup"><span data-stu-id="96e89-230">Prepare VHDs for migration</span></span>
<span data-ttu-id="96e89-231">Premium depolama alanına var olan Azure sanal makineleri geçiriyorsanız, VHD olabilir:</span><span class="sxs-lookup"><span data-stu-id="96e89-231">If you are migrating existing Azure VMs to Premium Storage, your VHD may be:</span></span>

* <span data-ttu-id="96e89-232">Genelleştirilmiş işletim sistemi görüntüsü</span><span class="sxs-lookup"><span data-stu-id="96e89-232">A generalized operating system image</span></span>
* <span data-ttu-id="96e89-233">Benzersiz işletim sistemi diski</span><span class="sxs-lookup"><span data-stu-id="96e89-233">A unique operating system disk</span></span>
* <span data-ttu-id="96e89-234">Bir veri diski</span><span class="sxs-lookup"><span data-stu-id="96e89-234">A data disk</span></span>

<span data-ttu-id="96e89-235">Aşağıda Biz bu 3 senaryolar için VHD hazırlama yol.</span><span class="sxs-lookup"><span data-stu-id="96e89-235">Below we walk through these 3 scenarios for preparing your VHD.</span></span>

##### <a name="use-a-generalized-operating-system-vhd-to-create-multiple-vm-instances"></a><span data-ttu-id="96e89-236">Genelleştirilmiş bir işletim sistemi VHD birden çok VM örnekleri oluşturmak için kullanın</span><span class="sxs-lookup"><span data-stu-id="96e89-236">Use a generalized Operating System VHD to create multiple VM instances</span></span>
<span data-ttu-id="96e89-237">Birden çok genel Azure VM örnekleri oluşturmak için kullanılan bir VHD yüklüyorsanız, sysprep yardımcı programını kullanarak VHD generalize gerekir.</span><span class="sxs-lookup"><span data-stu-id="96e89-237">If you are uploading a VHD that will be used to create multiple generic Azure VM instances, you must first generalize VHD using a sysprep utility.</span></span> <span data-ttu-id="96e89-238">Bu, şirket içi bir VHD veya bulutta geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="96e89-238">This applies to a VHD that is on-premises or in the cloud.</span></span> <span data-ttu-id="96e89-239">Sysprep herhangi bir makineye özel bilgi VHD'den kaldırır.</span><span class="sxs-lookup"><span data-stu-id="96e89-239">Sysprep removes any machine-specific information from the VHD.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="96e89-240">Bir anlık görüntüsünü veya genelleme önce VM'yi yedekleme.</span><span class="sxs-lookup"><span data-stu-id="96e89-240">Take a snapshot or backup your VM before generalizing it.</span></span> <span data-ttu-id="96e89-241">Çalışan sysprep durdurun ve VM örneği serbest bırakma.</span><span class="sxs-lookup"><span data-stu-id="96e89-241">Running sysprep will stop and deallocate the VM instance.</span></span> <span data-ttu-id="96e89-242">Sysprep Windows işletim sistemi VHD için aşağıdaki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="96e89-242">Follow steps below to sysprep a Windows OS VHD.</span></span> <span data-ttu-id="96e89-243">Sysprep komutunu çalıştırarak, sanal makine kapatılamıyor gerektireceğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="96e89-243">Note that running the Sysprep command will require you to shut down the virtual machine.</span></span> <span data-ttu-id="96e89-244">Sysprep hakkında daha fazla bilgi için bkz: [Sysprep genel bakış](http://technet.microsoft.com/library/hh825209.aspx) veya [Sysprep Teknik Başvurusu](http://technet.microsoft.com/library/cc766049.aspx).</span><span class="sxs-lookup"><span data-stu-id="96e89-244">For more information about Sysprep, see [Sysprep Overview](http://technet.microsoft.com/library/hh825209.aspx) or [Sysprep Technical Reference](http://technet.microsoft.com/library/cc766049.aspx).</span></span>
>
>

1. <span data-ttu-id="96e89-245">Yönetici olarak bir komut istemi penceresi açın.</span><span class="sxs-lookup"><span data-stu-id="96e89-245">Open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="96e89-246">Sysprep açmak için aşağıdaki komutu girin:</span><span class="sxs-lookup"><span data-stu-id="96e89-246">Enter the following command to open Sysprep:</span></span>

    ```
    %windir%\system32\sysprep\sysprep.exe
    ```

3. <span data-ttu-id="96e89-247">Sistem Hazırlama aracı girin sistem Out-of-Box deneyimi (OOBE) seçin, Generalize onay kutusunu işaretleyin, **kapatma**ve ardından **Tamam**, aşağıdaki resimde gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="96e89-247">In the System Preparation Tool, select Enter System Out-of-Box Experience (OOBE), select the Generalize check box, select **Shutdown**, and then click **OK**, as shown in the image below.</span></span> <span data-ttu-id="96e89-248">Sysprep'i kullanarak işletim sistemini genelleştirir ve sistemi kapat.</span><span class="sxs-lookup"><span data-stu-id="96e89-248">Sysprep will generalize the operating system and shut down the system.</span></span>

    ![][1]

<span data-ttu-id="96e89-249">Bir Ubuntu VM için Sanal Küp Str sysprep aynı elde etmek için kullanın.</span><span class="sxs-lookup"><span data-stu-id="96e89-249">For an Ubuntu VM, use virt-sysprep to achieve the same.</span></span> <span data-ttu-id="96e89-250">Bkz: [Sanal Küp Str sysprep](http://manpages.ubuntu.com/manpages/precise/man1/virt-sysprep.1.html) daha fazla ayrıntı için.</span><span class="sxs-lookup"><span data-stu-id="96e89-250">See [virt-sysprep](http://manpages.ubuntu.com/manpages/precise/man1/virt-sysprep.1.html) for more details.</span></span> <span data-ttu-id="96e89-251">Ayrıca bazı açık kaynak bkz [sunucu Linux sağlama yazılım](http://www.cyberciti.biz/tips/server-provisioning-software.html) diğer Linux işletim sistemleri için.</span><span class="sxs-lookup"><span data-stu-id="96e89-251">See also some of the open source [Linux Server Provisioning software](http://www.cyberciti.biz/tips/server-provisioning-software.html) for other Linux operating systems.</span></span>

##### <a name="use-a-unique-operating-system-vhd-to-create-a-single-vm-instance"></a><span data-ttu-id="96e89-252">Tek bir VM örneği oluşturmak için benzersiz bir işletim sistemi VHD kullanın</span><span class="sxs-lookup"><span data-stu-id="96e89-252">Use a unique Operating System VHD to create a single VM instance</span></span>
<span data-ttu-id="96e89-253">Makine belirli veri gerektiren VM üzerinde çalışan bir uygulamanız varsa, VHD'yi generalize değil.</span><span class="sxs-lookup"><span data-stu-id="96e89-253">If you have an application running on the VM which requires the machine specific data, do not generalize the VHD.</span></span> <span data-ttu-id="96e89-254">Genelleştirilmiş olmayan bir VHD benzersiz bir Azure VM örneği oluşturmak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="96e89-254">A non-generalized VHD can be used to create a unique Azure VM instance.</span></span> <span data-ttu-id="96e89-255">VHD etki alanı denetleyicisi varsa, örneğin, sysprep yürütülürken, bir etki alanı denetleyicisi olarak etkisiz hale getirir.</span><span class="sxs-lookup"><span data-stu-id="96e89-255">For example, if you have Domain Controller on your VHD, executing sysprep will make it ineffective as a Domain Controller.</span></span> <span data-ttu-id="96e89-256">VM'nizi ve VHD genelleme önce sysprep çalışan etkisini çalışan uygulamaları gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="96e89-256">Review the applications running on your VM and the impact of running sysprep on them before generalizing the VHD.</span></span>

##### <a name="register-data-disk-vhd"></a><span data-ttu-id="96e89-257">Veri diski VHD kaydetme</span><span class="sxs-lookup"><span data-stu-id="96e89-257">Register data disk VHD</span></span>
<span data-ttu-id="96e89-258">Veri diskleri geçirilmesi Azure'da varsa, bu veri diskleri kullanan sanal makineleri kapatmak emin olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="96e89-258">If you have data disks in Azure to be migrated, you must make sure the VMs that use these data disks are shut down.</span></span>

<span data-ttu-id="96e89-259">VHD Azure Premium depolama alanına kopyalayın ve sağlanan veri diski olarak kaydetmek için aşağıda açıklanan adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="96e89-259">Follow the steps described below to copy VHD to Azure Premium Storage and register it as a provisioned data disk.</span></span>

#### <a name="step-2-create-the-destination-for-your-vhd"></a><span data-ttu-id="96e89-260">2. Adım</span><span class="sxs-lookup"><span data-stu-id="96e89-260">Step 2.</span></span> <span data-ttu-id="96e89-261">VHD için hedef oluşturma</span><span class="sxs-lookup"><span data-stu-id="96e89-261">Create the destination for your VHD</span></span>
<span data-ttu-id="96e89-262">Vhd'lerinizi korumak için bir depolama hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="96e89-262">Create a storage account for maintaining your VHDs.</span></span> <span data-ttu-id="96e89-263">Vhd'lerinizi depolanacağı planlarken aşağıdaki noktaları dikkate alın:</span><span class="sxs-lookup"><span data-stu-id="96e89-263">Consider the following points when planning where to store your VHDs:</span></span>

* <span data-ttu-id="96e89-264">Premium depolama hesabı hedef.</span><span class="sxs-lookup"><span data-stu-id="96e89-264">The target Premium storage account.</span></span>
* <span data-ttu-id="96e89-265">Depolama hesap konumu Premium depolama özellikli Azure Son aşamada oluşturacak VM'ler ile aynı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="96e89-265">The storage account location must be same as Premium Storage capable Azure VMs you will create in the final stage.</span></span> <span data-ttu-id="96e89-266">Yeni depolama hesabı ya da gereksinimlerinize göre aynı depolama hesabı kullanmak için plan kopyalamak.</span><span class="sxs-lookup"><span data-stu-id="96e89-266">You could copy to a new storage account, or plan to use the same storage account based on your needs.</span></span>
* <span data-ttu-id="96e89-267">Kopyalayın ve bir sonraki aşaması için hedef depolama hesabının depolama hesabı anahtarı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="96e89-267">Copy and save the storage account key of the destination storage account for the next stage.</span></span>

<span data-ttu-id="96e89-268">Veri diskleri için bir standart depolama hesabı (örneğin, için depolama alanına sahip diskler) bazı veri diskleri tutmak seçebilirsiniz, ancak, premium depolama kullanmak, üretim iş yükü için tüm verilerin taşınması önerilir.</span><span class="sxs-lookup"><span data-stu-id="96e89-268">For data disks, you can choose to keep some data disks in a standard storage account (for example, disks that have cooler storage), but we strongly recommend you moving all data for production workload to use premium storage.</span></span>

#### <span data-ttu-id="96e89-269"><a name="copy-vhd-with-azcopy-or-powershell"></a>3. adım.</span><span class="sxs-lookup"><span data-stu-id="96e89-269"><a name="copy-vhd-with-azcopy-or-powershell"></a>Step 3.</span></span> <span data-ttu-id="96e89-270">VHD AzCopy veya PowerShell ile kopyalama</span><span class="sxs-lookup"><span data-stu-id="96e89-270">Copy VHD with AzCopy or PowerShell</span></span>
<span data-ttu-id="96e89-271">Bu iki seçenekten biri işlemek için kapsayıcı yolu ve depolama hesabı anahtarınızı bulmak gerekir.</span><span class="sxs-lookup"><span data-stu-id="96e89-271">You will need to find your container path and storage account key to process either of these two options.</span></span> <span data-ttu-id="96e89-272">Kapsayıcı yolu ve depolama hesabı anahtarı bulunabilir **Azure Portal** > **depolama**.</span><span class="sxs-lookup"><span data-stu-id="96e89-272">Container path and storage account key can be found in **Azure Portal** > **Storage**.</span></span> <span data-ttu-id="96e89-273">Kapsayıcı URL "gibi https://myaccount.blob.core.windows.net/mycontainer/" olacaktır.</span><span class="sxs-lookup"><span data-stu-id="96e89-273">The container URL will be like "https://myaccount.blob.core.windows.net/mycontainer/".</span></span>

##### <a name="option-1-copy-a-vhd-with-azcopy-asynchronous-copy"></a><span data-ttu-id="96e89-274">Seçenek 1: bir VHD AzCopy (zaman uyumsuz kopya) ile kopyalama</span><span class="sxs-lookup"><span data-stu-id="96e89-274">Option 1: Copy a VHD with AzCopy (Asynchronous copy)</span></span>
<span data-ttu-id="96e89-275">AzCopy kullanarak, Internet üzerinden VHD kolayca karşıya yükleyebilir.</span><span class="sxs-lookup"><span data-stu-id="96e89-275">Using AzCopy, you can easily upload the VHD over the Internet.</span></span> <span data-ttu-id="96e89-276">VHD'leri boyutuna bağlı olarak, bu zaman alabilir.</span><span class="sxs-lookup"><span data-stu-id="96e89-276">Depending on the size of the VHDs, this may take time.</span></span> <span data-ttu-id="96e89-277">Bu seçenek kullanıldığında depolama hesabı giriş/çıkış sınırları denetlemek unutmayın.</span><span class="sxs-lookup"><span data-stu-id="96e89-277">Remember to check the storage account ingress/egress limits when using this option.</span></span> <span data-ttu-id="96e89-278">Bkz: [Azure Storage ölçeklenebilirlik ve performans hedefleri](storage-scalability-targets.md) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="96e89-278">See [Azure Storage Scalability and Performance Targets](storage-scalability-targets.md) for details.</span></span>

1. <span data-ttu-id="96e89-279">AzCopy buradan yükleyip: [en güncel AzCopy sürümünü](http://aka.ms/downloadazcopy)</span><span class="sxs-lookup"><span data-stu-id="96e89-279">Download and install AzCopy from here: [Latest version of AzCopy](http://aka.ms/downloadazcopy)</span></span>
2. <span data-ttu-id="96e89-280">Azure PowerShell'i açın ve AzCopy yüklü olduğu klasöre gidin.</span><span class="sxs-lookup"><span data-stu-id="96e89-280">Open Azure PowerShell and go to the folder where AzCopy is installed.</span></span>
3. <span data-ttu-id="96e89-281">"Kaynak" VHD dosyasına "Hedef" kopyalamak için aşağıdaki komutu kullanın.</span><span class="sxs-lookup"><span data-stu-id="96e89-281">Use the following command to copy the VHD file from "Source" to "Destination".</span></span>

    ```azcopy
    AzCopy /Source: <source> /SourceKey: <source-account-key> /Dest: <destination> /DestKey: <dest-account-key> /BlobType:page /Pattern: <file-name>
    ```

    <span data-ttu-id="96e89-282">Örnek:</span><span class="sxs-lookup"><span data-stu-id="96e89-282">Example:</span></span>

    ```azcopy
    AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /SourceKey:key1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /DestKey:key2 /Pattern:abc.vhd
    ```

    <span data-ttu-id="96e89-283">AzCopy komutta kullanılan parametreler açıklamalarını şunlardır:</span><span class="sxs-lookup"><span data-stu-id="96e89-283">Here are descriptions of the parameters used in the AzCopy command:</span></span>

   * <span data-ttu-id="96e89-284">**/ Kaynak:  *&lt;kaynak&gt;:***  klasör veya VHD'yi içeren depolama kapsayıcısı URL.</span><span class="sxs-lookup"><span data-stu-id="96e89-284">**/Source: *&lt;source&gt;:*** Location of the folder or storage container URL that contains the VHD.</span></span>
   * <span data-ttu-id="96e89-285">**/ SourceKey:  *&lt;kaynak hesap anahtarı&gt;:***  kaynağı depolama hesabının depolama hesabı anahtarı.</span><span class="sxs-lookup"><span data-stu-id="96e89-285">**/SourceKey: *&lt;source-account-key&gt;:*** Storage account key of the source storage account.</span></span>
   * <span data-ttu-id="96e89-286">**/ Taşınmaya:  *&lt;hedef&gt;:***  VHD'ye kopyalamak için depolama kapsayıcı URL'si.</span><span class="sxs-lookup"><span data-stu-id="96e89-286">**/Dest: *&lt;destination&gt;:*** Storage container URL to copy the VHD to.</span></span>
   * <span data-ttu-id="96e89-287">**/ DestKey:  *&lt;hedef hesap anahtarı&gt;:***  hedef depolama hesabının depolama hesabı anahtarı.</span><span class="sxs-lookup"><span data-stu-id="96e89-287">**/DestKey: *&lt;dest-account-key&gt;:*** Storage account key of the destination storage account.</span></span>
   * <span data-ttu-id="96e89-288">**/ Deseni:  *&lt;dosya adı&gt;:***  kopyalamak için VHD dosyasının adını belirtin.</span><span class="sxs-lookup"><span data-stu-id="96e89-288">**/Pattern: *&lt;file-name&gt;:*** Specify the file name of the VHD to copy.</span></span>

<span data-ttu-id="96e89-289">Aracı AzCopy kullanımıyla ilgili ayrıntılar için bkz: [AzCopy komut satırı yardımcı programı ile veri aktarma](storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="96e89-289">For details on using AzCopy tool, see [Transfer data with the AzCopy Command-Line Utility](storage-use-azcopy.md).</span></span>

##### <a name="option-2-copy-a-vhd-with-powershell-synchronized-copy"></a><span data-ttu-id="96e89-290">Seçenek 2: bir VHD PowerShell (Synchronızed kopya) ile kopyalama</span><span class="sxs-lookup"><span data-stu-id="96e89-290">Option 2: Copy a VHD with PowerShell (Synchronized copy)</span></span>
<span data-ttu-id="96e89-291">Ayrıca, başlangıç AzureStorageBlobCopy PowerShell cmdlet'ini kullanarak VHD dosyasını kopyalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="96e89-291">You can also copy the VHD file using the PowerShell cmdlet Start-AzureStorageBlobCopy.</span></span> <span data-ttu-id="96e89-292">Aşağıdaki komutu Azure PowerShell VHD kopyalamak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="96e89-292">Use the following command on Azure PowerShell to copy VHD.</span></span> <span data-ttu-id="96e89-293">Kaynak ve hedef depolama hesabınız karşılık gelen değerlerle <> değerleri değiştirin.</span><span class="sxs-lookup"><span data-stu-id="96e89-293">Replace the values in <> with corresponding values from your source and destination storage account.</span></span> <span data-ttu-id="96e89-294">Bu komutu kullanmak için hedef depolama hesabınız VHD adlı bir kapsayıcı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="96e89-294">To use this command, you must have a container called vhds in your destination storage account.</span></span> <span data-ttu-id="96e89-295">Kapsayıcı yoksa, bir komut çalıştırmadan önce oluşturun.</span><span class="sxs-lookup"><span data-stu-id="96e89-295">If the container doesn't exist, create one before running the command.</span></span>

```powershell
$sourceBlobUri = <source-vhd-uri>

$sourceContext = New-AzureStorageContext  –StorageAccountName <source-account> -StorageAccountKey <source-account-key>

$destinationContext = New-AzureStorageContext  –StorageAccountName <dest-account> -StorageAccountKey <dest-account-key>

Start-AzureStorageBlobCopy -srcUri $sourceBlobUri -SrcContext $sourceContext -DestContainer <dest-container> -DestBlob <dest-disk-name> -DestContext $destinationContext
```

<span data-ttu-id="96e89-296">Örnek:</span><span class="sxs-lookup"><span data-stu-id="96e89-296">Example:</span></span>

```powershell
C:\PS> $sourceBlobUri = "https://sourceaccount.blob.core.windows.net/vhds/myvhd.vhd"

C:\PS> $sourceContext = New-AzureStorageContext  –StorageAccountName "sourceaccount" -StorageAccountKey "J4zUI9T5b8gvHohkiRg"

C:\PS> $destinationContext = New-AzureStorageContext  –StorageAccountName "destaccount" -StorageAccountKey "XZTmqSGKUYFSh7zB5"

C:\PS> Start-AzureStorageBlobCopy -srcUri $sourceBlobUri -SrcContext $sourceContext -DestContainer "vhds" -DestBlob "myvhd.vhd" -DestContext $destinationContext
```

### <span data-ttu-id="96e89-297"><a name="scenario2"></a>Senaryo 2: "ı VM'ler diğer platformlarından Azure Premium depolama alanına geçirme."</span><span class="sxs-lookup"><span data-stu-id="96e89-297"><a name="scenario2"></a>Scenario 2: "I am migrating VMs from other platforms to Azure Premium Storage."</span></span>
<span data-ttu-id="96e89-298">VHD için Azure olmayan - Azure bulut depolama biriminden geçiriyorsanız, yerel bir dizine VHD ilk vermeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="96e89-298">If you are migrating VHD from non-Azure Cloud Storage to Azure, you must first export the VHD to a local directory.</span></span> <span data-ttu-id="96e89-299">VHD kullanışlı depolandığı bir yerel dizinin tam kaynak yoluna sahip ve AzCopy kullanarak Azure Storage'a yükler.</span><span class="sxs-lookup"><span data-stu-id="96e89-299">Have the complete source path of the local directory where VHD is stored handy, and then using AzCopy to upload it to Azure Storage.</span></span>

#### <a name="step-1-export-vhd-to-a-local-directory"></a><span data-ttu-id="96e89-300">1. Adım</span><span class="sxs-lookup"><span data-stu-id="96e89-300">Step 1.</span></span> <span data-ttu-id="96e89-301">VHD yerel bir dizine dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="96e89-301">Export VHD to a local directory</span></span>
##### <a name="copy-a-vhd-from-aws"></a><span data-ttu-id="96e89-302">Bir VHD'yi AWS kopyalayın</span><span class="sxs-lookup"><span data-stu-id="96e89-302">Copy a VHD from AWS</span></span>
1. <span data-ttu-id="96e89-303">AWS kullanıyorsanız, EC2 örneği bir Amazon S3 demetini VHD'yi verin.</span><span class="sxs-lookup"><span data-stu-id="96e89-303">If you are using AWS, export the EC2 instance to a VHD in an Amazon S3 bucket.</span></span> <span data-ttu-id="96e89-304">Amazon EC2 komut satırı arabirimi (CLI) aracını yükleyin ve EC2 örneği bir VHD dosyasına aktarmak için örnek verme Görev Oluştur komutu çalıştırmak Amazon EC2 örnekleri dışarı aktarma için Amazon belgelerinde açıklanan adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="96e89-304">Follow the steps described in the Amazon documentation for Exporting Amazon EC2 Instances to install the Amazon EC2 command-line interface (CLI) tool and run the create-instance-export-task command to export the EC2 instance to a VHD file.</span></span> <span data-ttu-id="96e89-305">Kullandığınızdan emin olun **VHD** DISK &#95; görüntü &#95; Çalıştırırken biçimi değişkeni **-örnek-export-görev oluştur** komutu.</span><span class="sxs-lookup"><span data-stu-id="96e89-305">Be sure to use **VHD** for the DISK&#95;IMAGE&#95;FORMAT variable when running the **create-instance-export-task** command.</span></span> <span data-ttu-id="96e89-306">Dışarı aktarılan VHD dosyasının bu işlem sırasında belirttiğiniz Amazon S3 demetini kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="96e89-306">The exported VHD file is saved in the Amazon S3 bucket you designate during that process.</span></span>

    ```
    aws ec2 create-instance-export-task --instance-id ID --target-environment TARGET_ENVIRONMENT \
      --export-to-s3-task DiskImageFormat=DISK_IMAGE_FORMAT,ContainerFormat=ova,S3Bucket=BUCKET,S3Prefix=PREFIX
    ```

2. <span data-ttu-id="96e89-307">VHD dosyasını S3 demetini indirin.</span><span class="sxs-lookup"><span data-stu-id="96e89-307">Download the VHD file from the S3 bucket.</span></span> <span data-ttu-id="96e89-308">VHD dosyasını seçip **Eylemler** > **karşıdan**.</span><span class="sxs-lookup"><span data-stu-id="96e89-308">Select the VHD file, then **Actions** > **Download**.</span></span>

    ![][3]

##### <a name="copy-a-vhd-from-other-non-azure-cloud"></a><span data-ttu-id="96e89-309">Bir VHD'yi diğer Azure olmayan buluttan kopyalayın</span><span class="sxs-lookup"><span data-stu-id="96e89-309">Copy a VHD from other non-Azure cloud</span></span>
<span data-ttu-id="96e89-310">VHD için Azure olmayan - Azure bulut depolama biriminden geçiriyorsanız, yerel bir dizine VHD ilk vermeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="96e89-310">If you are migrating VHD from non-Azure Cloud Storage to Azure, you must first export the VHD to a local directory.</span></span> <span data-ttu-id="96e89-311">VHD depolandığı bir yerel dizinin tam kaynak yolu kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="96e89-311">Copy the complete source path of the local directory where VHD is stored.</span></span>

##### <a name="copy-a-vhd-from-on-premises"></a><span data-ttu-id="96e89-312">Şirket içi bir VHD'yi kopyalayın</span><span class="sxs-lookup"><span data-stu-id="96e89-312">Copy a VHD from on-premises</span></span>
<span data-ttu-id="96e89-313">Bir şirket içi ortamından VHD geçiriyorsanız, VHD depolandığı tam kaynak yolu gerekir.</span><span class="sxs-lookup"><span data-stu-id="96e89-313">If you are migrating VHD from an on-premises environment, you will need the complete source path where VHD is stored.</span></span> <span data-ttu-id="96e89-314">Kaynak yolu, bir sunucu konumu veya dosya paylaşımı olabilir.</span><span class="sxs-lookup"><span data-stu-id="96e89-314">The source path could be a server location or file share.</span></span>

#### <a name="step-2-create-the-destination-for-your-vhd"></a><span data-ttu-id="96e89-315">2. Adım</span><span class="sxs-lookup"><span data-stu-id="96e89-315">Step 2.</span></span> <span data-ttu-id="96e89-316">VHD için hedef oluşturma</span><span class="sxs-lookup"><span data-stu-id="96e89-316">Create the destination for your VHD</span></span>
<span data-ttu-id="96e89-317">Vhd'lerinizi korumak için bir depolama hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="96e89-317">Create a storage account for maintaining your VHDs.</span></span> <span data-ttu-id="96e89-318">Vhd'lerinizi depolanacağı planlarken aşağıdaki noktaları dikkate alın:</span><span class="sxs-lookup"><span data-stu-id="96e89-318">Consider the following points when planning where to store your VHDs:</span></span>

* <span data-ttu-id="96e89-319">Hedef depolama hesabı, standart veya premium depolama uygulama ihtiyacınıza olabilir.</span><span class="sxs-lookup"><span data-stu-id="96e89-319">The target storage account could be standard or premium storage depending on your application requirement.</span></span>
* <span data-ttu-id="96e89-320">Depolama hesabı bölgesi Premium depolama özellikli Azure Son aşamada oluşturacak VM'ler ile aynı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="96e89-320">The storage account region must be same as Premium Storage capable Azure VMs you will create in the final stage.</span></span> <span data-ttu-id="96e89-321">Yeni depolama hesabı ya da gereksinimlerinize göre aynı depolama hesabı kullanmak için plan kopyalamak.</span><span class="sxs-lookup"><span data-stu-id="96e89-321">You could copy to a new storage account, or plan to use the same storage account based on your needs.</span></span>
* <span data-ttu-id="96e89-322">Kopyalayın ve bir sonraki aşaması için hedef depolama hesabının depolama hesabı anahtarı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="96e89-322">Copy and save the storage account key of the destination storage account for the next stage.</span></span>

<span data-ttu-id="96e89-323">Premium depolama kullanmak, üretim iş yükü için tüm veriler hareket öneririz.</span><span class="sxs-lookup"><span data-stu-id="96e89-323">We strongly recommend you moving all data for production workload to use premium storage.</span></span>

#### <a name="step-3-upload-the-vhd-to-azure-storage"></a><span data-ttu-id="96e89-324">3. Adım</span><span class="sxs-lookup"><span data-stu-id="96e89-324">Step 3.</span></span> <span data-ttu-id="96e89-325">Azure depolama alanına VHD yükleme</span><span class="sxs-lookup"><span data-stu-id="96e89-325">Upload the VHD to Azure Storage</span></span>
<span data-ttu-id="96e89-326">Yerel dizindeki, VHD sahip olduğunuza göre .vhd dosyası Azure depolama alanına yüklemek için AzCopy veya AzurePowerShell kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="96e89-326">Now that you have your VHD in the local directory, you can use AzCopy or AzurePowerShell to upload the .vhd file to Azure Storage.</span></span> <span data-ttu-id="96e89-327">Her iki seçenek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="96e89-327">Both options are provided here:</span></span>

##### <a name="option-1-using-azure-powershell-add-azurevhd-to-upload-the-vhd-file"></a><span data-ttu-id="96e89-328">Seçenek 1: .vhd dosyasını karşıya yüklemek için Azure PowerShell Ekle-AzureVhd kullanma</span><span class="sxs-lookup"><span data-stu-id="96e89-328">Option 1: Using Azure PowerShell Add-AzureVhd to upload the .vhd file</span></span>

```powershell
Add-AzureVhd [-Destination] <Uri> [-LocalFilePath] <FileInfo>
```

<span data-ttu-id="96e89-329">Örnek <Uri> olabilir ***"https://storagesample.blob.core.windows.net/mycontainer/blob1.vhd"***.</span><span class="sxs-lookup"><span data-stu-id="96e89-329">An example <Uri> might be ***"https://storagesample.blob.core.windows.net/mycontainer/blob1.vhd"***.</span></span> <span data-ttu-id="96e89-330">Örnek <FileInfo> olabilir ***"C:\path\to\upload.vhd"***.</span><span class="sxs-lookup"><span data-stu-id="96e89-330">An example <FileInfo> might be ***"C:\path\to\upload.vhd"***.</span></span>

##### <a name="option-2-using-azcopy-to-upload-the-vhd-file"></a><span data-ttu-id="96e89-331">Seçenek 2: .vhd dosyasını karşıya yüklemek için AzCopy kullanma</span><span class="sxs-lookup"><span data-stu-id="96e89-331">Option 2: Using AzCopy to upload the .vhd file</span></span>
<span data-ttu-id="96e89-332">AzCopy kullanarak, Internet üzerinden VHD kolayca karşıya yükleyebilir.</span><span class="sxs-lookup"><span data-stu-id="96e89-332">Using AzCopy, you can easily upload the VHD over the Internet.</span></span> <span data-ttu-id="96e89-333">VHD'leri boyutuna bağlı olarak, bu zaman alabilir.</span><span class="sxs-lookup"><span data-stu-id="96e89-333">Depending on the size of the VHDs, this may take time.</span></span> <span data-ttu-id="96e89-334">Bu seçenek kullanıldığında depolama hesabı giriş/çıkış sınırları denetlemek unutmayın.</span><span class="sxs-lookup"><span data-stu-id="96e89-334">Remember to check the storage account ingress/egress limits when using this option.</span></span> <span data-ttu-id="96e89-335">Bkz: [Azure Storage ölçeklenebilirlik ve performans hedefleri](storage-scalability-targets.md) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="96e89-335">See [Azure Storage Scalability and Performance Targets](storage-scalability-targets.md) for details.</span></span>

1. <span data-ttu-id="96e89-336">AzCopy buradan yükleyip: [en güncel AzCopy sürümünü](http://aka.ms/downloadazcopy)</span><span class="sxs-lookup"><span data-stu-id="96e89-336">Download and install AzCopy from here: [Latest version of AzCopy](http://aka.ms/downloadazcopy)</span></span>
2. <span data-ttu-id="96e89-337">Azure PowerShell'i açın ve AzCopy yüklü olduğu klasöre gidin.</span><span class="sxs-lookup"><span data-stu-id="96e89-337">Open Azure PowerShell and go to the folder where AzCopy is installed.</span></span>
3. <span data-ttu-id="96e89-338">"Kaynak" VHD dosyasına "Hedef" kopyalamak için aşağıdaki komutu kullanın.</span><span class="sxs-lookup"><span data-stu-id="96e89-338">Use the following command to copy the VHD file from "Source" to "Destination".</span></span>

    ```azcopy
    AzCopy /Source: <source> /SourceKey: <source-account-key> /Dest: <destination> /DestKey: <dest-account-key> /BlobType:page /Pattern: <file-name>
    ```

    <span data-ttu-id="96e89-339">Örnek:</span><span class="sxs-lookup"><span data-stu-id="96e89-339">Example:</span></span>

    ```azcopy
    AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /SourceKey:key1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /DestKey:key2 /BlobType:page /Pattern:abc.vhd
    ```

    <span data-ttu-id="96e89-340">AzCopy komutta kullanılan parametreler açıklamalarını şunlardır:</span><span class="sxs-lookup"><span data-stu-id="96e89-340">Here are descriptions of the parameters used in the AzCopy command:</span></span>

   * <span data-ttu-id="96e89-341">**/ Kaynak:  *&lt;kaynak&gt;:***  klasör veya VHD'yi içeren depolama kapsayıcısı URL.</span><span class="sxs-lookup"><span data-stu-id="96e89-341">**/Source: *&lt;source&gt;:*** Location of the folder or storage container URL that contains the VHD.</span></span>
   * <span data-ttu-id="96e89-342">**/ SourceKey:  *&lt;kaynak hesap anahtarı&gt;:***  kaynağı depolama hesabının depolama hesabı anahtarı.</span><span class="sxs-lookup"><span data-stu-id="96e89-342">**/SourceKey: *&lt;source-account-key&gt;:*** Storage account key of the source storage account.</span></span>
   * <span data-ttu-id="96e89-343">**/ Taşınmaya:  *&lt;hedef&gt;:***  VHD'ye kopyalamak için depolama kapsayıcı URL'si.</span><span class="sxs-lookup"><span data-stu-id="96e89-343">**/Dest: *&lt;destination&gt;:*** Storage container URL to copy the VHD to.</span></span>
   * <span data-ttu-id="96e89-344">**/ DestKey:  *&lt;hedef hesap anahtarı&gt;:***  hedef depolama hesabının depolama hesabı anahtarı.</span><span class="sxs-lookup"><span data-stu-id="96e89-344">**/DestKey: *&lt;dest-account-key&gt;:*** Storage account key of the destination storage account.</span></span>
   * <span data-ttu-id="96e89-345">**/ BlobType: sayfa:** hedef bir sayfa blob'u olduğunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="96e89-345">**/BlobType: page:** Specifies that the destination is a page blob.</span></span>
   * <span data-ttu-id="96e89-346">**/ Deseni:  *&lt;dosya adı&gt;:***  kopyalamak için VHD dosyasının adını belirtin.</span><span class="sxs-lookup"><span data-stu-id="96e89-346">**/Pattern: *&lt;file-name&gt;:*** Specify the file name of the VHD to copy.</span></span>

<span data-ttu-id="96e89-347">Aracı AzCopy kullanımıyla ilgili ayrıntılar için bkz: [AzCopy komut satırı yardımcı programı ile veri aktarma](storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="96e89-347">For details on using AzCopy tool, see [Transfer data with the AzCopy Command-Line Utility](storage-use-azcopy.md).</span></span>

##### <a name="other-options-for-uploading-a-vhd"></a><span data-ttu-id="96e89-348">Bir VHD karşıya yükleme için diğer seçenekleri</span><span class="sxs-lookup"><span data-stu-id="96e89-348">Other options for uploading a VHD</span></span>
<span data-ttu-id="96e89-349">Bir VHD depolama hesabınıza aşağıdaki anlamına gelir birini kullanarak da yükleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="96e89-349">You can also upload a VHD to your storage account using one of the following means:</span></span>

* [<span data-ttu-id="96e89-350">Azure depolama kopyalama Blob API</span><span class="sxs-lookup"><span data-stu-id="96e89-350">Azure Storage Copy Blob API</span></span>](https://msdn.microsoft.com/library/azure/dd894037.aspx)
* [<span data-ttu-id="96e89-351">Azure Depolama Gezgini karşıya BLOB'ları</span><span class="sxs-lookup"><span data-stu-id="96e89-351">Azure Storage Explorer Uploading Blobs</span></span>](https://azurestorageexplorer.codeplex.com/)
* [<span data-ttu-id="96e89-352">Depolama içeri/dışarı aktarma hizmeti REST API Başvurusu</span><span class="sxs-lookup"><span data-stu-id="96e89-352">Storage Import/Export Service REST API Reference</span></span>](https://msdn.microsoft.com/library/dn529096.aspx)

> [!NOTE]
> <span data-ttu-id="96e89-353">İçeri/dışarı aktarma hizmeti 7 günden daha uzun süre karşıya tahmini varsa kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="96e89-353">We recommend using Import/Export Service if estimated uploading time is longer than 7 days.</span></span> <span data-ttu-id="96e89-354">Kullanabileceğiniz [DataTransferSpeedCalculator](https://github.com/Azure-Samples/storage-dotnet-import-export-job-management/blob/master/DataTransferSpeedCalculator.html) veri boyutu ve aktarım birimi saati tahmin etmek için.</span><span class="sxs-lookup"><span data-stu-id="96e89-354">You can use [DataTransferSpeedCalculator](https://github.com/Azure-Samples/storage-dotnet-import-export-job-management/blob/master/DataTransferSpeedCalculator.html) to estimate the time from data size and transfer unit.</span></span>
>
> <span data-ttu-id="96e89-355">İçeri/dışarı aktarma, bir standart depolama hesabına kopyalamak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="96e89-355">Import/Export can be used to copy to a standard storage account.</span></span> <span data-ttu-id="96e89-356">Premium depolama hesabı AzCopy gibi bir araç kullanarak standart depolama biriminden kopyalamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="96e89-356">You will need to copy from standard storage to premium storage account using a tool like AzCopy.</span></span>
>
>

## <span data-ttu-id="96e89-357"><a name="create-azure-virtual-machine-using-premium-storage"></a>Azure Premium Storage kullanarak VM'ler oluşturma</span><span class="sxs-lookup"><span data-stu-id="96e89-357"><a name="create-azure-virtual-machine-using-premium-storage"></a>Create Azure VMs using Premium Storage</span></span>
<span data-ttu-id="96e89-358">VHD karşıya veya istenen depolama hesabına kopyalanır sonra VHD bir işletim sistemi görüntüsü veya işletim sistemi diski senaryonuza bağlı olarak kaydettirmek ve ondan VM örneği oluşturmak için bu bölümdeki yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="96e89-358">After the VHD is uploaded or copied to the desired storage account, follow the instructions in this section to register the VHD as an OS image, or OS disk depending on your scenario and then create a VM instance from it.</span></span> <span data-ttu-id="96e89-359">Oluşturulduktan sonra veri diski VHD VM'ye bağlı.</span><span class="sxs-lookup"><span data-stu-id="96e89-359">The data disk VHD can be attached to the VM once it is created.</span></span>
<span data-ttu-id="96e89-360">Örnek geçiş komut dosyası, bu bölümün sonunda sağlanır.</span><span class="sxs-lookup"><span data-stu-id="96e89-360">A sample migration script is provided at the end of this section.</span></span> <span data-ttu-id="96e89-361">Bu basit bir komut dosyası tüm senaryoları eşleşmiyor.</span><span class="sxs-lookup"><span data-stu-id="96e89-361">This simple script does not match all scenarios.</span></span> <span data-ttu-id="96e89-362">Kodun belirli senaryonuza ile eşleşecek şekilde güncelleştirmeniz gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="96e89-362">You may need to update the script to match with your specific scenario.</span></span> <span data-ttu-id="96e89-363">Bu komut dosyası senaryonuz için geçerli olup olmadığını görmek için aşağıya bakın: [bir örnek geçiş komut dosyası](#a-sample-migration-script).</span><span class="sxs-lookup"><span data-stu-id="96e89-363">To see if this script applies to your scenario, see below [A Sample Migration Script](#a-sample-migration-script).</span></span>

### <a name="checklist"></a><span data-ttu-id="96e89-364">Denetim listesi</span><span class="sxs-lookup"><span data-stu-id="96e89-364">Checklist</span></span>
1. <span data-ttu-id="96e89-365">Tüm kopyalama VHD diskleri olduğu tamamlanana kadar bekleyin.</span><span class="sxs-lookup"><span data-stu-id="96e89-365">Wait until all the VHD disks copying is complete.</span></span>
2. <span data-ttu-id="96e89-366">Premium depolama, geçiş yaptığınız bölgede kullanılabilir olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="96e89-366">Make sure Premium Storage is available in the region you are migrating to.</span></span>
3. <span data-ttu-id="96e89-367">Kullanacağınız yeni VM dizisi karar verin.</span><span class="sxs-lookup"><span data-stu-id="96e89-367">Decide the new VM series you will be using.</span></span> <span data-ttu-id="96e89-368">Premium depolama özelliğine sahip olmalıdır ve boyutu bölgede kullanılabilirliğine bağlı olarak ve gereksinimlerinize göre.</span><span class="sxs-lookup"><span data-stu-id="96e89-368">It should be a Premium Storage capable, and the size should be depending on the availability in the region and based on your needs.</span></span>
4. <span data-ttu-id="96e89-369">Kullanacağınız tam VM boyutu karar verin.</span><span class="sxs-lookup"><span data-stu-id="96e89-369">Decide the exact VM size you will use.</span></span> <span data-ttu-id="96e89-370">VM boyutu sahip veri diski sayısı desteklemek için büyük olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="96e89-370">VM size needs to be large enough to support the number of data disks you have.</span></span> <span data-ttu-id="96e89-371">Örneğin</span><span class="sxs-lookup"><span data-stu-id="96e89-371">E.g.</span></span> <span data-ttu-id="96e89-372">4 veri diski varsa, VM 2 veya daha fazla çekirdek olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="96e89-372">if you have 4 data disks, the VM must have 2 or more cores.</span></span> <span data-ttu-id="96e89-373">Ayrıca, işlemci gücü, bellek göz önünde bulundurun ve ağ bant genişliği gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="96e89-373">Also, consider processing power, memory and network bandwidth needs.</span></span>
5. <span data-ttu-id="96e89-374">Premium depolama hesabı hedef bölgede oluşturun.</span><span class="sxs-lookup"><span data-stu-id="96e89-374">Create a Premium Storage account in the target region.</span></span> <span data-ttu-id="96e89-375">Yeni VM için kullanacağı hesap budur.</span><span class="sxs-lookup"><span data-stu-id="96e89-375">This is the account you will use for the new VM.</span></span>
6. <span data-ttu-id="96e89-376">Kullanışlı, diskler ve karşılık gelen VHD BLOB'ları listesi dahil olmak üzere geçerli VM ayrıntıları vardır.</span><span class="sxs-lookup"><span data-stu-id="96e89-376">Have the current VM details handy, including the list of disks and corresponding VHD blobs.</span></span>

<span data-ttu-id="96e89-377">Uygulamanızı kapalı kalma süresi için hazırlayın.</span><span class="sxs-lookup"><span data-stu-id="96e89-377">Prepare your application for downtime.</span></span> <span data-ttu-id="96e89-378">Temiz bir geçiş yapmak için geçerli sistemdeki tüm işleme durdurmak zorunda.</span><span class="sxs-lookup"><span data-stu-id="96e89-378">To do a clean migration, you have to stop all the processing in the current system.</span></span> <span data-ttu-id="96e89-379">Ancak bundan sonra yeni platforma geçirebilirsiniz tutarlı durumuna alabilir.</span><span class="sxs-lookup"><span data-stu-id="96e89-379">Only then you can get it to consistent state which you can migrate to the new platform.</span></span> <span data-ttu-id="96e89-380">Kapalı kalma süresi geçirmek için diskleri veri miktarına bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="96e89-380">Downtime duration will depend on the amount of data in the disks to migrate.</span></span>

> [!NOTE]
> <span data-ttu-id="96e89-381">Özel bir VHD diskten bir Azure Kaynak Yöneticisi'ni VM oluşturuyorsanız, lütfen [bu şablonu](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd) Resource Manager mevcut diski kullanarak VM dağıtmak için.</span><span class="sxs-lookup"><span data-stu-id="96e89-381">If you are creating an Azure Resource Manager VM from a specialized VHD Disk, please refer to [this template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd) for deploying Resource Manager VM using existing disk.</span></span>
>
>

### <a name="register-your-vhd"></a><span data-ttu-id="96e89-382">VHD kaydetme</span><span class="sxs-lookup"><span data-stu-id="96e89-382">Register your VHD</span></span>
<span data-ttu-id="96e89-383">İşletim sistemi VHD'den bir VM oluşturun veya yeni bir sanal makineye bir veri diski eklemek için önce bunları kaydetmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="96e89-383">To create a VM from OS VHD or to attach a data disk to a new VM, you must first register them.</span></span> <span data-ttu-id="96e89-384">VHD'ler senaryo bağlı olarak aşağıdaki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="96e89-384">Follow steps below depending on your VHD's scenario.</span></span>

#### <a name="generalized-operating-system-vhd-to-create-multiple-azure-vm-instances"></a><span data-ttu-id="96e89-385">İşletim sistemi birden çok Azure VM örnekleri oluşturmak için VHD genelleştirilmiş</span><span class="sxs-lookup"><span data-stu-id="96e89-385">Generalized Operating System VHD to create multiple Azure VM instances</span></span>
<span data-ttu-id="96e89-386">Genelleştirilmiş işletim sistemi görüntüsü VHD depolama hesabına yüklendikten sonra olarak kaydettirmek bir **Azure VM görüntüsü** böylece bir veya daha fazla VM örnekleri oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="96e89-386">After generalized OS image VHD is uploaded to the storage account, register it as an **Azure VM Image** so that you can create one or more VM instances from it.</span></span> <span data-ttu-id="96e89-387">Bir Azure VM işletim sistemi görüntüsü olarak, VHD'yi kaydetmek için aşağıdaki PowerShell cmdlet'lerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="96e89-387">Use the following PowerShell cmdlets to register your VHD as an Azure VM OS image.</span></span> <span data-ttu-id="96e89-388">VHD için burada kopyalanmıştır tam kapsayıcı URL'sini sağlayın.</span><span class="sxs-lookup"><span data-stu-id="96e89-388">Provide the complete container URL where VHD was copied to.</span></span>

```powershell
Add-AzureVMImage -ImageName "OSImageName" -MediaLocation "https://storageaccount.blob.core.windows.net/vhdcontainer/osimage.vhd" -OS Windows
```

<span data-ttu-id="96e89-389">Kopyalayın ve bu yeni Azure VM görüntü adı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="96e89-389">Copy and save the name of this new Azure VM Image.</span></span> <span data-ttu-id="96e89-390">Yukarıdaki örnek *OSImageName*.</span><span class="sxs-lookup"><span data-stu-id="96e89-390">In the example above, it is *OSImageName*.</span></span>

#### <a name="unique-operating-system-vhd-to-create-a-single-azure-vm-instance"></a><span data-ttu-id="96e89-391">Tek bir Azure VM örneği oluşturmak için benzersiz işletim sistemi VHD</span><span class="sxs-lookup"><span data-stu-id="96e89-391">Unique Operating System VHD to create a single Azure VM instance</span></span>
<span data-ttu-id="96e89-392">Depolama hesabı için benzersiz OS VHD yüklendikten sonra olarak kaydettirmek bir **Azure işletim sistemi diski** böylece VM örneği oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="96e89-392">After the unique OS VHD is uploaded to the storage account, register it as an **Azure OS Disk** so that you can create a VM instance from it.</span></span> <span data-ttu-id="96e89-393">VHD Azure işletim sistemi diski kaydetmek için şu PowerShell cmdlet'lerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="96e89-393">Use these PowerShell cmdlets to register your VHD as an Azure OS Disk.</span></span> <span data-ttu-id="96e89-394">VHD için burada kopyalanmıştır tam kapsayıcı URL'sini sağlayın.</span><span class="sxs-lookup"><span data-stu-id="96e89-394">Provide the complete container URL where VHD was copied to.</span></span>

```powershell
Add-AzureDisk -DiskName "OSDisk" -MediaLocation "https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd" -Label "My OS Disk" -OS "Windows"
```

<span data-ttu-id="96e89-395">Kopyalayın ve bu yeni Azure işletim sistemi diski adı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="96e89-395">Copy and save the name of this new Azure OS Disk.</span></span> <span data-ttu-id="96e89-396">Yukarıdaki örnek *OSDisk*.</span><span class="sxs-lookup"><span data-stu-id="96e89-396">In the example above, it is *OSDisk*.</span></span>

#### <a name="data-disk-vhd-to-be-attached-to-new-azure-vm-instances"></a><span data-ttu-id="96e89-397">VHD yeni Azure VM örnekleri için eklenecek veri diski</span><span class="sxs-lookup"><span data-stu-id="96e89-397">Data disk VHD to be attached to new Azure VM instance(s)</span></span>
<span data-ttu-id="96e89-398">Veri diski VHD depolama hesabına yüklendikten sonra yeni DS serisi için DSv2 serisi veya GS serisi Azure VM örneği eklenebilecek böylece bir Azure veri diski olarak kaydedin.</span><span class="sxs-lookup"><span data-stu-id="96e89-398">After the data disk VHD is uploaded to storage account, register it as an Azure Data Disk so that it can be attached to your new DS Series, DSv2 series or GS Series Azure VM instance.</span></span>

<span data-ttu-id="96e89-399">Bir Azure veri diski olarak, VHD'yi kaydetmek için şu PowerShell cmdlet'lerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="96e89-399">Use these PowerShell cmdlets to register your VHD as an Azure Data Disk.</span></span> <span data-ttu-id="96e89-400">VHD için burada kopyalanmıştır tam kapsayıcı URL'sini sağlayın.</span><span class="sxs-lookup"><span data-stu-id="96e89-400">Provide the complete container URL where VHD was copied to.</span></span>

```powershell
Add-AzureDisk -DiskName "DataDisk" -MediaLocation "https://storageaccount.blob.core.windows.net/vhdcontainer/datadisk.vhd" -Label "My Data Disk"
```

<span data-ttu-id="96e89-401">Kopyalayın ve bu yeni Azure veri diski adını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="96e89-401">Copy and save the name of this new Azure Data Disk.</span></span> <span data-ttu-id="96e89-402">Yukarıdaki örnek *DataDisk*.</span><span class="sxs-lookup"><span data-stu-id="96e89-402">In the example above, it is *DataDisk*.</span></span>

### <a name="create-a-premium-storage-capable-vm"></a><span data-ttu-id="96e89-403">Premium depolama özelliğine sahip VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="96e89-403">Create a Premium Storage capable VM</span></span>
<span data-ttu-id="96e89-404">Bir kez işletim sistemi görüntüsü veya işletim sistemi diski kayıtlı, yeni DS serisi, DSv2 serisi veya GS serisi VM oluşturun.</span><span class="sxs-lookup"><span data-stu-id="96e89-404">Once the OS image or OS disk are registered, create a new DS-series, DSv2-series or GS-series VM.</span></span> <span data-ttu-id="96e89-405">İşletim sistemi görüntüsü veya kaydettiğiniz işletim sistemi disk adı kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="96e89-405">You will be using the operating system image or operating system disk name that you registered.</span></span> <span data-ttu-id="96e89-406">VM Premium depolama katmanını seçin.</span><span class="sxs-lookup"><span data-stu-id="96e89-406">Select the VM type from the Premium Storage tier.</span></span> <span data-ttu-id="96e89-407">Aşağıdaki örnekte kullanıyoruz *Standard_DS2* VM boyutu.</span><span class="sxs-lookup"><span data-stu-id="96e89-407">In example below, we are using the *Standard_DS2* VM size.</span></span>

> [!NOTE]
> <span data-ttu-id="96e89-408">Kapasite ve performans gereksinimlerini ve kullanılabilir Azure disk boyutlarını eşleştiğinden emin olmak için disk boyutu güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="96e89-408">Update the disk size to make sure it matches your capacity and performance requirements and the available Azure disk sizes.</span></span>
>
>

<span data-ttu-id="96e89-409">Yeni bir VM oluşturmak için aşağıdaki adım adım PowerShell cmdlet'leri izleyin.</span><span class="sxs-lookup"><span data-stu-id="96e89-409">Follow the step by step PowerShell cmdlets below to create the new VM.</span></span> <span data-ttu-id="96e89-410">İlk olarak, ortak parametreleri ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="96e89-410">First, set the common parameters:</span></span>

```powershell
$serviceName = "yourVM"
$location = "location-name" (e.g., West US)
$vmSize ="Standard_DS2"
$adminUser = "youradmin"
$adminPassword = "yourpassword"
$vmName ="yourVM"
$vmSize = "Standard_DS2"
```

<span data-ttu-id="96e89-411">İlk olarak, yeni VM'ler içinde barındıracak bir bulut hizmeti oluşturun.</span><span class="sxs-lookup"><span data-stu-id="96e89-411">First, create a cloud service in which you will be hosting your new VMs.</span></span>

```powershell
New-AzureService -ServiceName $serviceName -Location $location
```

<span data-ttu-id="96e89-412">Ardından, senaryonuza bağlı olarak işletim sistemi görüntüsü veya kaydettiğiniz işletim sistemi diski ' Azure VM örneği oluşturun.</span><span class="sxs-lookup"><span data-stu-id="96e89-412">Next, depending on your scenario, create the Azure VM instance from either the OS Image or OS Disk that you registered.</span></span>

#### <a name="generalized-operating-system-vhd-to-create-multiple-azure-vm-instances"></a><span data-ttu-id="96e89-413">İşletim sistemi birden çok Azure VM örnekleri oluşturmak için VHD genelleştirilmiş</span><span class="sxs-lookup"><span data-stu-id="96e89-413">Generalized Operating System VHD to create multiple Azure VM instances</span></span>
<span data-ttu-id="96e89-414">Kullanarak bir veya daha fazla yeni DS serisi Azure VM örnekleri oluşturmak **Azure işletim sistemi görüntüsü** , kayıtlı.</span><span class="sxs-lookup"><span data-stu-id="96e89-414">Create the one or more new DS Series Azure VM instances using the **Azure OS Image** that you registered.</span></span> <span data-ttu-id="96e89-415">Bu işletim sistemi görüntüsü adı, aşağıda gösterildiği gibi yeni bir VM oluştururken, VM yapılandırması belirtin.</span><span class="sxs-lookup"><span data-stu-id="96e89-415">Specify this OS Image name in the VM configuration when creating new VM as shown below.</span></span>

```powershell
$OSImage = Get-AzureVMImage –ImageName "OSImageName"

$vm = New-AzureVMConfig -Name $vmName –InstanceSize $vmSize -ImageName $OSImage.ImageName

Add-AzureProvisioningConfig -Windows –AdminUserName $adminUser -Password $adminPassword –VM $vm

New-AzureVM -ServiceName $serviceName -VM $vm
```

#### <a name="unique-operating-system-vhd-to-create-a-single-azure-vm-instance"></a><span data-ttu-id="96e89-416">Tek bir Azure VM örneği oluşturmak için benzersiz işletim sistemi VHD</span><span class="sxs-lookup"><span data-stu-id="96e89-416">Unique Operating System VHD to create a single Azure VM instance</span></span>
<span data-ttu-id="96e89-417">Kullanarak yeni bir DS serisi Azure VM örneği oluştur **Azure işletim sistemi diski** , kayıtlı.</span><span class="sxs-lookup"><span data-stu-id="96e89-417">Create a new DS series Azure VM instance using the **Azure OS Disk** that you registered.</span></span> <span data-ttu-id="96e89-418">Bu işletim sistemi diski adı VM Yapılandırması'nda yeni VM aşağıda gösterildiği gibi oluştururken belirtin.</span><span class="sxs-lookup"><span data-stu-id="96e89-418">Specify this OS Disk name in the VM configuration when creating the new VM as shown below.</span></span>

```powershell
$OSDisk = Get-AzureDisk –DiskName "OSDisk"

$vm = New-AzureVMConfig -Name $vmName -InstanceSize $vmSize -DiskName $OSDisk.DiskName

New-AzureVM -ServiceName $serviceName –VM $vm
```

<span data-ttu-id="96e89-419">Bulut hizmeti, bölge, depolama hesabı, kullanılabilirlik kümesi ve önbellek İlkesi gibi diğer Azure VM bilgileri belirtin.</span><span class="sxs-lookup"><span data-stu-id="96e89-419">Specify other Azure VM information, such as a cloud service, region, storage account, availability set, and caching policy.</span></span> <span data-ttu-id="96e89-420">Seçili bulut hizmetini, bölge ve depolama hesabı tüm aynı konumu bu disklerin temel VHD olarak olmalıdır VM örneği ilişkili işletim sistemi veya veri diski ile birlikte bulunan olması gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="96e89-420">Note that the VM instance must be co-located with associated operating system or data disks, so the selected cloud service, region and storage account must all be in the same location as the underlying VHDs of those disks.</span></span>

### <a name="attach-data-disk"></a><span data-ttu-id="96e89-421">Veri diski ekleme</span><span class="sxs-lookup"><span data-stu-id="96e89-421">Attach data disk</span></span>
<span data-ttu-id="96e89-422">Veri diski VHD'leri kaydettiyseniz, son olarak, bunları yeni Premium depolama özellikli Azure VM'e ekleyin.</span><span class="sxs-lookup"><span data-stu-id="96e89-422">Lastly, if you have registered data disk VHDs, attach them to the new Premium Storage capable Azure VM.</span></span>

<span data-ttu-id="96e89-423">Veri diski yeni VM'e ekleyin ve önbellek ilkesi belirtmek için PowerShell cmdlet'ini kullanın.</span><span class="sxs-lookup"><span data-stu-id="96e89-423">Use following PowerShell cmdlet to attach data disk to the new VM and specify the caching policy.</span></span> <span data-ttu-id="96e89-424">Aşağıdaki örnekte önbellek İlkesi ayarlamak *salt okunur*.</span><span class="sxs-lookup"><span data-stu-id="96e89-424">In example below the caching policy is set to *ReadOnly*.</span></span>

```powershell
$vm = Get-AzureVM -ServiceName $serviceName -Name $vmName

Add-AzureDataDisk -ImportFrom -DiskName "DataDisk" -LUN 0 –HostCaching ReadOnly –VM $vm

Update-AzureVM  -VM $vm
```

> [!NOTE]
> <span data-ttu-id="96e89-425">Ek adımlar olabilir, uygulama desteklemek için gerekli kapsanmayan bu kılavuzda.</span><span class="sxs-lookup"><span data-stu-id="96e89-425">There may be additional steps necessary to support your application that is not be covered by this guide.</span></span>
>
>

### <a name="checking-and-plan-backup"></a><span data-ttu-id="96e89-426">Denetleme ve yedekleme planlama</span><span class="sxs-lookup"><span data-stu-id="96e89-426">Checking and plan backup</span></span>
<span data-ttu-id="96e89-427">Yeni VM çalışır durumda sonra aynı oturum açma kimliğini kullanarak erişmek ve parola özgün VM ve bu her şeyin beklendiği gibi çalıştığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="96e89-427">Once the new VM is up and running, access it using the same login id and password is as the original VM, and verify that everything is working as expected.</span></span> <span data-ttu-id="96e89-428">Şeritli birimler dahil tüm ayarlar ve yeni VM mevcut olacaktır.</span><span class="sxs-lookup"><span data-stu-id="96e89-428">All the settings, including the striped volumes, would be present in the new VM.</span></span>

<span data-ttu-id="96e89-429">Yedekleme plana son adımdır ve yeni VM için bakım zamanlaması uygulamanın gereksinimlerine göre.</span><span class="sxs-lookup"><span data-stu-id="96e89-429">The last step is to plan backup and maintenance schedule for the new VM based on the application's needs.</span></span>

### <span data-ttu-id="96e89-430"><a name="a-sample-migration-script"></a>Örnek geçiş komut dosyası</span><span class="sxs-lookup"><span data-stu-id="96e89-430"><a name="a-sample-migration-script"></a>A sample migration script</span></span>
<span data-ttu-id="96e89-431">Geçirmek için birden çok VM varsa, automation PowerShell komut yardımcı olacaktır.</span><span class="sxs-lookup"><span data-stu-id="96e89-431">If you have multiple VMs to migrate, automation through PowerShell scripts will be helpful.</span></span> <span data-ttu-id="96e89-432">Bir VM geçişini otomatikleştiren bir örnek betiği aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="96e89-432">Following is a sample script that automates the migration of a VM.</span></span> <span data-ttu-id="96e89-433">Not yalnızca bir örnek komut dosyası aşağıda olan ve geçerli VM diskleri hakkında yapılan birkaç varsayımlar vardır.</span><span class="sxs-lookup"><span data-stu-id="96e89-433">Note that below script is only an example, and there are few assumptions made about the current VM disks.</span></span> <span data-ttu-id="96e89-434">Kodun belirli senaryonuza ile eşleşecek şekilde güncelleştirmeniz gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="96e89-434">You may need to update the script to match with your specific scenario.</span></span>

<span data-ttu-id="96e89-435">Varsayımlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="96e89-435">The assumptions are:</span></span>

* <span data-ttu-id="96e89-436">Klasik Azure sanal makineleri oluşturuyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="96e89-436">You are creating classic Azure VMs.</span></span>
* <span data-ttu-id="96e89-437">Kaynak işletim sistemi diski ve kaynak veri diskleri aynı depolama hesabı ve aynı kapsayıcı olan.</span><span class="sxs-lookup"><span data-stu-id="96e89-437">Your source OS Disks and source Data Disks are in same storage account and same container.</span></span> <span data-ttu-id="96e89-438">İşletim sistemi diskleri ve veri diskleri aynı yerde değilse, depolama hesapları ve kapsayıcıları VHD'ler kopyalamak için AzCopy ya da Azure PowerShell kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="96e89-438">If your OS Disks and Data Disks are not in the same place, you can use AzCopy or Azure PowerShell to copy VHDs over storage accounts and containers.</span></span> <span data-ttu-id="96e89-439">Önceki adıma bakın: [kopyalama VHD AzCopy veya PowerShell ile](#copy-vhd-with-azcopy-or-powershell).</span><span class="sxs-lookup"><span data-stu-id="96e89-439">Refer to the previous step: [Copy VHD with AzCopy or PowerShell](#copy-vhd-with-azcopy-or-powershell).</span></span> <span data-ttu-id="96e89-440">Senaryonuz karşılamak için bu komut dosyasını düzenleme başka bir seçenektir ancak daha kolay ve hızlı olduğundan AzCopy veya PowerShell kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="96e89-440">Editing this script to meet your scenario is another choice, but we recommend using AzCopy or PowerShell since it is easier and faster.</span></span>

<span data-ttu-id="96e89-441">Otomasyon betiğini aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="96e89-441">The automation script is provided below.</span></span> <span data-ttu-id="96e89-442">Metin bilgilerinizle değiştirin ve belirli senaryonuza ile eşleşmesi için komut dosyasını güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="96e89-442">Replace text with your information and update the script to match with your specific scenario.</span></span>

> [!NOTE]
> <span data-ttu-id="96e89-443">Varolan bir komut dosyasını kullanarak, kaynak VM ağ yapılandırması korumaz.</span><span class="sxs-lookup"><span data-stu-id="96e89-443">Using the existing script does not preserve the network configuration of your source VM.</span></span> <span data-ttu-id="96e89-444">Ağ ayarları re-config geçirilen Vm'leriniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="96e89-444">You will need to re-config the networking settings on your migrated VMs.</span></span>
>
>

```
    <#
    .Synopsis
    This script is provided as an EXAMPLE to show how to migrate a VM from a standard storage account to a premium storage account. You can customize it according to your specific requirements.

    .Description
    The script will copy the vhds (page blobs) of the source VM to the new storage account.
    And then it will create a new VM from these copied vhds based on the inputs that you specified for the new VM.
    You can modify the script to satisfy your specific requirement, but please be aware of the items specified
    in the Terms of Use section.

    .Terms of Use
    Copyright © 2015 Microsoft Corporation.  All rights reserved.

    THIS CODE AND ANY ASSOCIATED INFORMATION ARE PROVIDED "AS IS" WITHOUT WARRANTY OF ANY KIND,
    EITHER EXPRESSED OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE IMPLIED WARRANTIES OF MERCHANTABILITY
    AND/OR FITNESS FOR A PARTICULAR PURPOSE. THE ENTIRE RISK OF USE, INABILITY TO USE, OR
    RESULTS FROM THE USE OF THIS CODE REMAINS WITH THE USER.

    .Example (Save this script as Migrate-AzureVM.ps1)

    .\Migrate-AzureVM.ps1 -SourceServiceName CurrentServiceName -SourceVMName CurrentVMName –DestStorageAccount newpremiumstorageaccount -DestServiceName NewServiceName -DestVMName NewDSVMName -DestVMSize "Standard_DS2" –Location "Southeast Asia"

    .Link
    To find more information about how to set up Azure PowerShell, refer to the following links.
    http://azure.microsoft.com/documentation/articles/powershell-install-configure/
    http://azure.microsoft.com/documentation/articles/storage-powershell-guide-full/
    http://azure.microsoft.com/blog/2014/10/22/migrate-azure-virtual-machines-between-storage-accounts/

    #>

    Param(
    # the cloud service name of the VM.
    [Parameter(Mandatory = $true)]
    [string] $SourceServiceName,

    # The VM name to copy.
    [Parameter(Mandatory = $true)]
    [String] $SourceVMName,

    # The destination storage account name.
    [Parameter(Mandatory = $true)]
    [String] $DestStorageAccount,

    # The destination cloud service name
    [Parameter(Mandatory = $true)]
    [String] $DestServiceName,

    # the destination vm name
    [Parameter(Mandatory = $true)]
    [String] $DestVMName,

    # the destination vm size
    [Parameter(Mandatory = $true)]
    [String] $DestVMSize,

    # the location of destination VM.
    [Parameter(Mandatory = $true)]
    [string] $Location,

    # whether or not to copy the os disk, the default is only copy data disks
    [Parameter(Mandatory = $false)]
    [Bool] $DataDiskOnly = $true,

    # how frequently to report the copy status in sceconds
    [Parameter(Mandatory = $false)]
    [Int32] $CopyStatusReportInterval = 15,

    # the name suffix to add to new created disks to avoid conflict with source disk names
    [Parameter(Mandatory = $false)]
    [String]$DiskNameSuffix = "-prem"

    ) #end param

    #######################################################################
    #  Verify Azure PowerShell module and version
    #######################################################################

    #import the Azure PowerShell module
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


    #Check the Azure PowerShell module version
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
        Write-Host "[ERROR] - There is no valid Azure subscription found in PowerShell. Please refer to this article http://azure.microsoft.com/documentation/articles/powershell-install-configure/ to connect an Azure subscription. Exiting." -ForegroundColor Red
        Exit
    }


    #######################################################################
    #  Check if the VM is shut down
    #  Stopping the VM is a required step so that the file system is consistent when you do the copy operation.
    #  Azure does not support live migration at this time..
    #######################################################################

    if (($sourceVM = Get-AzureVM –ServiceName $SourceServiceName –Name $SourceVMName) -eq $null)
    {
        Write-Host "[ERROR] - The source VM doesn't exist in the current subscription. Exiting." -ForegroundColor Red
        Exit
    }

    # check if VM is shut down
    if ( $sourceVM.Status -notmatch "Stopped" )
    {
        Write-Host "[Warning] - Stopping the VM is a required step so that the file system is consistent when you do the copy operation. Azure does not support live migration at this time. If you'd like to create a VM from a generalized image, sys-prep the Virtual Machine before stopping it." -ForegroundColor Yellow
        $ContinueAnswer = Read-Host "`n`tDo you wish to stop $SourceVMName now? Input 'N' if you want to shut down the VM manually and come back later.(Y/N)"
        If ($ContinueAnswer -ne "Y") { Write-Host "`n Exiting." -ForegroundColor Red;Exit }
        $sourceVM | Stop-AzureVM

        # wait until the VM is shut down
        $VMStatus = (Get-AzureVM –ServiceName $SourceServiceName –Name $vmName).Status
        while ($VMStatus -notmatch "Stopped")
        {
            Write-Host "`n[Status] - Waiting VM $vmName to shut down" -ForegroundColor Green
            Sleep -Seconds 5
            $VMStatus = (Get-AzureVM –ServiceName $SourceServiceName –Name $vmName).Status
        }
    }

    # exporting the sourve vm to a configuration file, you can restore the original VM by importing this config file
    # see more information for Import-AzureVM
    $workingDir = (Get-Location).Path
    $vmConfigurationPath = $env:HOMEPATH + "\VM-" + $SourceVMName + ".xml"
    Write-Host "`n[WORKITEM] - Exporting VM configuration to $vmConfigurationPath" -ForegroundColor Yellow
    $exportRe = $sourceVM | Export-AzureVM -Path $vmConfigurationPath


    #######################################################################
    #  Copy the vhds of the source vm
    #  You can choose to copy all disks including os and data disks by specifying the
    #  parameter -DataDiskOnly to be $false. The default is to copy only data disk vhds
    #  and the new VM will boot from the original os disk.
    #######################################################################

    $sourceOSDisk = $sourceVM.VM.OSVirtualHardDisk
    $sourceDataDisks = $sourceVM.VM.DataVirtualHardDisks

    # Get source storage account information, not considering the data disks and os disks are in different accounts
    $sourceStorageAccountName = $sourceOSDisk.MediaLink.Host -split "\." | select -First 1
    $sourceStorageKey = (Get-AzureStorageKey -StorageAccountName $sourceStorageAccountName).Primary
    $sourceContext = New-AzureStorageContext –StorageAccountName $sourceStorageAccountName -StorageAccountKey $sourceStorageKey

    # Create destination context
    $destStorageKey = (Get-AzureStorageKey -StorageAccountName $DestStorageAccount).Primary
    $destContext = New-AzureStorageContext –StorageAccountName $DestStorageAccount -StorageAccountKey $destStorageKey

    # Create a container of vhds if it doesn't exist
    if ((Get-AzureStorageContainer -Context $destContext -Name vhds -ErrorAction SilentlyContinue) -eq $null)
    {
        Write-Host "`n[WORKITEM] - Creating a container vhds in the destination storage account." -ForegroundColor Yellow
        New-AzureStorageContainer -Context $destContext -Name vhds
    }


    $allDisksToCopy = $sourceDataDisks
    # check if need to copy os disk
    $sourceOSVHD = $sourceOSDisk.MediaLink.Segments[2]
    if ($DataDiskOnly)
    {
        # copy data disks only, this option requires deleting the source VM so that dest VM can boot
        # from the same vhd blob.
        $ContinueAnswer = Read-Host "`n`t[Warning] You chose to copy data disks only. Moving VM requires removing the original VM (the disks and backing vhd files will NOT be deleted) so that the new VM can boot from the same vhd. This is an irreversible action. Do you wish to proceed right now? (Y/N)"
        If ($ContinueAnswer -ne "Y") { Write-Host "`n Exiting." -ForegroundColor Red;Exit }
        $destOSVHD = Get-AzureStorageBlob -Blob $sourceOSVHD -Container vhds -Context $sourceContext
        Write-Host "`n[WORKITEM] - Removing the original VM (the vhd files are NOT deleted)." -ForegroundColor Yellow
        Remove-AzureVM -Name $SourceVMName -ServiceName $SourceServiceName

        Write-Host "`n[WORKITEM] - Waiting utill the OS disk is released by source VM. This may take up to several minutes."
        $diskAttachedTo = (Get-AzureDisk -DiskName $sourceOSDisk.DiskName).AttachedTo
        while ($diskAttachedTo -ne $null)
        {
            Start-Sleep -Seconds 10
            $diskAttachedTo = (Get-AzureDisk -DiskName $sourceOSDisk.DiskName).AttachedTo
        }

    }
    else
    {
        # copy the os disk vhd
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
        # update the media link to point to the target blob link
        $disk.MediaLink = $targetBlob.ICloudBlob.Uri.AbsoluteUri
    }

    # Wait until all vhd files are copied.
    $diskComplete = @()
    do
    {
        Write-Host "`n[WORKITEM] - Waiting for all disk copy to complete. Checking status every $CopyStatusReportInterval seconds." -ForegroundColor Yellow
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
    #  the new VM can be created from the copied disks or the original os disk.
    #  You can ddd your own logic here to satisfy your specific requirements of the vm.
    #######################################################################

    # Create a VM from the existing os disk
    if ($DataDiskOnly)
    {
        $vm = New-AzureVMConfig -Name $DestVMName -InstanceSize $DestVMSize -DiskName $sourceOSDisk.DiskName
    }
    else
    {
        $newOSDisk = Add-AzureDisk -OS $sourceOSDisk.OS -DiskName ($sourceOSDisk.DiskName + $DiskNameSuffix) -MediaLocation $destOSVHD.ICloudBlob.Uri.AbsoluteUri
        $vm = New-AzureVMConfig -Name $DestVMName -InstanceSize $DestVMSize -DiskName $newOSDisk.DiskName
    }
    # Attached the copied data disks to the new VM
    foreach ($dataDisk in $sourceDataDisks)
    {
        # add -DiskLabel $dataDisk.DiskLabel if there are labels for disks of the source vm
        $diskLabel = "drive" + $dataDisk.Lun
        $vm | Add-AzureDataDisk -ImportFrom -DiskLabel $diskLabel -LUN $dataDisk.Lun -MediaLocation $dataDisk.MediaLink
    }

    # Edit this if you want to add more custimization to the new VM
    # $vm | Add-AzureEndpoint -Protocol tcp -LocalPort 443 -PublicPort 443 -Name 'HTTPs'
    # $vm | Set-AzureSubnet "PubSubnet","PrivSubnet"

    New-AzureVM -ServiceName $DestServiceName -VMs $vm -Location $Location
```

#### <span data-ttu-id="96e89-445"><a name="optimization"></a>En iyi duruma getirme</span><span class="sxs-lookup"><span data-stu-id="96e89-445"><a name="optimization"></a>Optimization</span></span>
<span data-ttu-id="96e89-446">Geçerli VM yapılandırmanızı, özellikle de standart diskler ile çalışmak için özelleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="96e89-446">Your current VM configuration may be customized specifically to work well with Standard disks.</span></span> <span data-ttu-id="96e89-447">Örneğin, bir şeritli birim birçok diskleri kullanarak performansını artırmak için.</span><span class="sxs-lookup"><span data-stu-id="96e89-447">For instance, to increase the performance by using many disks in a striped volume.</span></span> <span data-ttu-id="96e89-448">Örneğin, 4 disk ayrı olarak Premium depolama kullanmak yerine, tek bir disk sağlayarak maliyeti en iyi duruma getirmek mümkün olabilir.</span><span class="sxs-lookup"><span data-stu-id="96e89-448">For example, instead of using 4 disks separately on Premium Storage, you may be able to optimize the cost by having a single disk.</span></span> <span data-ttu-id="96e89-449">En iyi duruma getirme bu gerek bir olay temelinde işlenmesi ve özel adımlar geçişten sonra gerektiren ister.</span><span class="sxs-lookup"><span data-stu-id="96e89-449">Optimizations like this need to be handled on a case by case basis and require custom steps after the migration.</span></span> <span data-ttu-id="96e89-450">Ayrıca, bu işlem veritabanları ve ayarları'nda tanımlanan disk düzeni kullanan uygulamalar için düzgün çalışmayabilir unutmayın.</span><span class="sxs-lookup"><span data-stu-id="96e89-450">Also, note that this process may not well work for databases and applications that depend on the disk layout defined in the setup.</span></span>

##### <a name="preparation"></a><span data-ttu-id="96e89-451">Hazırlama</span><span class="sxs-lookup"><span data-stu-id="96e89-451">Preparation</span></span>
1. <span data-ttu-id="96e89-452">Basit geçiş, önceki bölümde açıklandığı gibi tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="96e89-452">Complete the Simple Migration as described in the earlier section.</span></span> <span data-ttu-id="96e89-453">En iyi duruma getirme geçişten sonra yeni VM üzerinde gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="96e89-453">Optimizations will be performed on the new VM after the migration.</span></span>
2. <span data-ttu-id="96e89-454">İçin en iyi duruma getirilmiş yapılandırma yeni disk boyutları tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="96e89-454">Define the new disk sizes needed for the optimized configuration.</span></span>
3. <span data-ttu-id="96e89-455">Yeni disk belirtimlerine geçerli diskleri/birimlerin eşleme belirler.</span><span class="sxs-lookup"><span data-stu-id="96e89-455">Determine mapping of the current disks/volumes to the new disk specifications.</span></span>

##### <a name="execution-steps"></a><span data-ttu-id="96e89-456">Yürütme adımları</span><span class="sxs-lookup"><span data-stu-id="96e89-456">Execution steps</span></span>
1. <span data-ttu-id="96e89-457">Premium depolama VM üzerinde doğru boyutta yeni diskleri oluşturun.</span><span class="sxs-lookup"><span data-stu-id="96e89-457">Create the new disks with the right sizes on the Premium Storage VM.</span></span>
2. <span data-ttu-id="96e89-458">Oturum açma verileri kopyalamanız ve VM birime eşleştiren yeni diske geçerli birimden.</span><span class="sxs-lookup"><span data-stu-id="96e89-458">Login to the VM and copy the data from the current volume to the new disk that maps to that volume.</span></span> <span data-ttu-id="96e89-459">Yeni bir diske eşlemeniz geçerli birimler için bunu yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="96e89-459">Do this for all the current volumes that need to map to a new disk.</span></span>
3. <span data-ttu-id="96e89-460">Ardından, yeni disklere geçiş yapmak için uygulama ayarlarını değiştirin ve eski birimlerin ayırın.</span><span class="sxs-lookup"><span data-stu-id="96e89-460">Next, change the application settings to switch to the new disks, and detach the old volumes.</span></span>

<span data-ttu-id="96e89-461">Uygulama için daha iyi disk performansı ayarlamak için lütfen [uygulama performansı en iyi duruma getirme](storage-premium-storage-performance.md#optimizing-application-performance).</span><span class="sxs-lookup"><span data-stu-id="96e89-461">For tuning the application for better disk performance, please refer to [Optimizing Application Performance](storage-premium-storage-performance.md#optimizing-application-performance).</span></span>

### <a name="application-migrations"></a><span data-ttu-id="96e89-462">Uygulama geçişleri</span><span class="sxs-lookup"><span data-stu-id="96e89-462">Application migrations</span></span>
<span data-ttu-id="96e89-463">Veritabanları ve diğer karmaşık uygulamalar geçiş için uygulama sağlayıcısı tarafından tanımlanan özel adımlar gerektirebilir.</span><span class="sxs-lookup"><span data-stu-id="96e89-463">Databases and other complex applications may require special steps as defined by the application provider for the migration.</span></span> <span data-ttu-id="96e89-464">Lütfen ilgili uygulama belgelerine başvurun.</span><span class="sxs-lookup"><span data-stu-id="96e89-464">Please refer to respective application documentation.</span></span> <span data-ttu-id="96e89-465">Örneğin</span><span class="sxs-lookup"><span data-stu-id="96e89-465">E.g.</span></span> <span data-ttu-id="96e89-466">veritabanlarını yedekleme genellikle geçirilebilecek ve geri yükleme.</span><span class="sxs-lookup"><span data-stu-id="96e89-466">typically databases can be migrated through backup and restore.</span></span>

## <a name="next-steps"></a><span data-ttu-id="96e89-467">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="96e89-467">Next steps</span></span>
<span data-ttu-id="96e89-468">Sanal makineleri geçirmek için belirli senaryolar için aşağıdaki kaynaklara bakın:</span><span class="sxs-lookup"><span data-stu-id="96e89-468">See the following resources for specific scenarios for migrating virtual machines:</span></span>

* [<span data-ttu-id="96e89-469">Azure sanal makineleri depolama hesapları arasında geçiş</span><span class="sxs-lookup"><span data-stu-id="96e89-469">Migrate Azure Virtual Machines between Storage Accounts</span></span>](https://azure.microsoft.com/blog/2014/10/22/migrate-azure-virtual-machines-between-storage-accounts/)
* [<span data-ttu-id="96e89-470">Oluşturun ve Windows Server VHD Azure'a yükleyin.</span><span class="sxs-lookup"><span data-stu-id="96e89-470">Create and upload a Windows Server VHD to Azure.</span></span>](../../virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [<span data-ttu-id="96e89-471">Oluşturma ve Linux işletim sistemini içeren bir Sanal Sabit Disk karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="96e89-471">Creating and Uploading a Virtual Hard Disk that Contains the Linux Operating System</span></span>](../../virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="96e89-472">Geçirme sanal makinelerden Amazon AWS Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="96e89-472">Migrating Virtual Machines from Amazon AWS to Microsoft Azure</span></span>](http://channel9.msdn.com/Series/Migrating-Virtual-Machines-from-Amazon-AWS-to-Microsoft-Azure)

<span data-ttu-id="96e89-473">Ayrıca, Azure Storage ve Azure sanal makineler hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:</span><span class="sxs-lookup"><span data-stu-id="96e89-473">Also, see the following resources to learn more about Azure Storage and Azure Virtual Machines:</span></span>

* [<span data-ttu-id="96e89-474">Azure Depolama</span><span class="sxs-lookup"><span data-stu-id="96e89-474">Azure Storage</span></span>](https://azure.microsoft.com/documentation/services/storage/)
* [<span data-ttu-id="96e89-475">Azure sanal makineler</span><span class="sxs-lookup"><span data-stu-id="96e89-475">Azure Virtual Machines</span></span>](https://azure.microsoft.com/documentation/services/virtual-machines/)
* [<span data-ttu-id="96e89-476">Premium Depolama: Azure Sanal Makine İş Yükleri için Yüksek Performanslı Depolama</span><span class="sxs-lookup"><span data-stu-id="96e89-476">Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads</span></span>](storage-premium-storage.md)

[1]:./media/storage-migration-to-premium-storage/migration-to-premium-storage-1.png
[2]:./media/storage-migration-to-premium-storage/migration-to-premium-storage-1.png
[3]:./media/storage-migration-to-premium-storage/migration-to-premium-storage-3.png
[4]: http://technet.microsoft.com/library/hh831739.aspx
