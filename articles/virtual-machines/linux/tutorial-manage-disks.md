---
title: "Azure CLI ile Azure diskleri yönetme | Microsoft Docs"
description: "Öğretici - Azure CLI ile Azure diskleri yönetme"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: d77dd2b44dca8cee6fa2e93e79cda76c80ccfe1a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-azure-disks-with-the-azure-cli"></a><span data-ttu-id="6f289-103">Azure CLI ile Azure diskleri yönetme</span><span class="sxs-lookup"><span data-stu-id="6f289-103">Manage Azure disks with the Azure CLI</span></span>

<span data-ttu-id="6f289-104">Azure sanal makineleri diskleri sanal makineleri işletim sistemi, uygulamaları ve verileri depolamak için kullanır.</span><span class="sxs-lookup"><span data-stu-id="6f289-104">Azure virtual machines use disks to store the VMs operating system, applications, and data.</span></span> <span data-ttu-id="6f289-105">Bir VM oluşturulurken bir disk boyutu ve beklenen iş yükü için uygun yapılandırma seçmek önemlidir.</span><span class="sxs-lookup"><span data-stu-id="6f289-105">When creating a VM it is important to choose a disk size and configuration appropriate to the expected workload.</span></span> <span data-ttu-id="6f289-106">Bu öğretici, dağıtma ve VM diskleri yönetme kapsar.</span><span class="sxs-lookup"><span data-stu-id="6f289-106">This tutorial covers deploying and managing VM disks.</span></span> <span data-ttu-id="6f289-107">Hakkında bilgi edinin:</span><span class="sxs-lookup"><span data-stu-id="6f289-107">You learn about:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6f289-108">İşletim sistemi ve geçici disklerle</span><span class="sxs-lookup"><span data-stu-id="6f289-108">OS disks and temporary disks</span></span>
> * <span data-ttu-id="6f289-109">Veri diskleri</span><span class="sxs-lookup"><span data-stu-id="6f289-109">Data disks</span></span>
> * <span data-ttu-id="6f289-110">Standart ve Premium diskleri</span><span class="sxs-lookup"><span data-stu-id="6f289-110">Standard and Premium disks</span></span>
> * <span data-ttu-id="6f289-111">Disk performansı</span><span class="sxs-lookup"><span data-stu-id="6f289-111">Disk performance</span></span>
> * <span data-ttu-id="6f289-112">Ekleme ve veri diskleri hazırlama</span><span class="sxs-lookup"><span data-stu-id="6f289-112">Attaching and preparing data disks</span></span>
> * <span data-ttu-id="6f289-113">Diskleri yeniden boyutlandırma</span><span class="sxs-lookup"><span data-stu-id="6f289-113">Resizing disks</span></span>
> * <span data-ttu-id="6f289-114">Disk anlık görüntüler</span><span class="sxs-lookup"><span data-stu-id="6f289-114">Disk snapshots</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="6f289-115">Yüklemek ve CLI yerel olarak kullanmak seçerseniz, Bu öğretici, Azure CLI Sürüm 2.0.4 çalıştırmasını gerektirir veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="6f289-115">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="6f289-116">Sürümü bulmak için `az --version` komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="6f289-116">Run `az --version` to find the version.</span></span> <span data-ttu-id="6f289-117">Yüklemeniz veya yükseltmeniz gerekirse, bkz. [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="6f289-117">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="default-azure-disks"></a><span data-ttu-id="6f289-118">Azure diskleri varsayılan</span><span class="sxs-lookup"><span data-stu-id="6f289-118">Default Azure disks</span></span>

<span data-ttu-id="6f289-119">Bir Azure sanal makine oluşturulduğunda, iki disk otomatik olarak sanal makineye bağlanmış.</span><span class="sxs-lookup"><span data-stu-id="6f289-119">When an Azure virtual machine is created, two disks are automatically attached to the virtual machine.</span></span> 

<span data-ttu-id="6f289-120">**İşletim sistemi diski** -işletim sistemi disklerinde en fazla 1 terabayttan küçük boyuta sahip ve VM'ler işletim sistemi barındırır.</span><span class="sxs-lookup"><span data-stu-id="6f289-120">**Operating system disk** - Operating system disks can be sized up to 1 terabyte, and hosts the VMs operating system.</span></span> <span data-ttu-id="6f289-121">İşletim sistemi diski etiketli */dev/sda* varsayılan olarak.</span><span class="sxs-lookup"><span data-stu-id="6f289-121">The OS disk is labeled */dev/sda* by default.</span></span> <span data-ttu-id="6f289-122">İşletim sistemi disk yapılandırması önbelleğe alma disk işletim sistemi performans için optimize edilmiştir.</span><span class="sxs-lookup"><span data-stu-id="6f289-122">The disk caching configuration of the OS disk is optimized for OS performance.</span></span> <span data-ttu-id="6f289-123">Bu yapılandırma, işletim sistemi diski nedeniyle **vermemelisiniz** konak uygulamalar veya veri.</span><span class="sxs-lookup"><span data-stu-id="6f289-123">Because of this configuration, the OS disk **should not** host applications or data.</span></span> <span data-ttu-id="6f289-124">Uygulamalar ve veriler için bu makalenin sonraki bölümlerinde ayrıntılı veri diskleri kullanın.</span><span class="sxs-lookup"><span data-stu-id="6f289-124">For applications and data, use data disks, which are detailed later in this article.</span></span> 

<span data-ttu-id="6f289-125">**Geçici disk** -geçici diskleri VM ile aynı Azure konakta bulunan bir katı hal sürücüsü kullanın.</span><span class="sxs-lookup"><span data-stu-id="6f289-125">**Temporary disk** - Temporary disks use a solid-state drive that is located on the same Azure host as the VM.</span></span> <span data-ttu-id="6f289-126">Temp disklerinin yüksek oranda kullanıcı durumda ve geçici veri işleme gibi işlemler için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="6f289-126">Temp disks are highly performant and may be used for operations such as temporary data processing.</span></span> <span data-ttu-id="6f289-127">Ancak, VM yeni bir ana bilgisayara taşındığında, geçici bir diskte depolanan tüm verileri kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="6f289-127">However, if the VM is moved to a new host, any data stored on a temporary disk is removed.</span></span> <span data-ttu-id="6f289-128">Geçici disk boyutunu VM boyutu tarafından belirlenir.</span><span class="sxs-lookup"><span data-stu-id="6f289-128">The size of the temporary disk is determined by the VM size.</span></span> <span data-ttu-id="6f289-129">Geçici diskleri etiketli */dev/sdb* ve mountpoint, */mnt*.</span><span class="sxs-lookup"><span data-stu-id="6f289-129">Temporary disks are labeled */dev/sdb* and have a mountpoint of */mnt*.</span></span>

### <a name="temporary-disk-sizes"></a><span data-ttu-id="6f289-130">Geçici disk boyutları</span><span class="sxs-lookup"><span data-stu-id="6f289-130">Temporary disk sizes</span></span>

| <span data-ttu-id="6f289-131">Tür</span><span class="sxs-lookup"><span data-stu-id="6f289-131">Type</span></span> | <span data-ttu-id="6f289-132">VM boyutu</span><span class="sxs-lookup"><span data-stu-id="6f289-132">VM Size</span></span> | <span data-ttu-id="6f289-133">En büyük geçici disk boyutu (GB)</span><span class="sxs-lookup"><span data-stu-id="6f289-133">Max temp disk size (GB)</span></span> |
|----|----|----|
| [<span data-ttu-id="6f289-134">Genel amaçlı</span><span class="sxs-lookup"><span data-stu-id="6f289-134">General purpose</span></span>](sizes-general.md) | <span data-ttu-id="6f289-135">A ve D serisi</span><span class="sxs-lookup"><span data-stu-id="6f289-135">A and D series</span></span> | <span data-ttu-id="6f289-136">800</span><span class="sxs-lookup"><span data-stu-id="6f289-136">800</span></span> |
| [<span data-ttu-id="6f289-137">İşlem için iyileştirilmiş</span><span class="sxs-lookup"><span data-stu-id="6f289-137">Compute optimized</span></span>](sizes-compute.md) | <span data-ttu-id="6f289-138">F serisi</span><span class="sxs-lookup"><span data-stu-id="6f289-138">F series</span></span> | <span data-ttu-id="6f289-139">800</span><span class="sxs-lookup"><span data-stu-id="6f289-139">800</span></span> |
| [<span data-ttu-id="6f289-140">Bellek için iyileştirilmiş</span><span class="sxs-lookup"><span data-stu-id="6f289-140">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md) | <span data-ttu-id="6f289-141">D ve G serisi</span><span class="sxs-lookup"><span data-stu-id="6f289-141">D and G series</span></span> | <span data-ttu-id="6f289-142">6144</span><span class="sxs-lookup"><span data-stu-id="6f289-142">6144</span></span> |
| [<span data-ttu-id="6f289-143">Depolama için iyileştirilmiş</span><span class="sxs-lookup"><span data-stu-id="6f289-143">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md) | <span data-ttu-id="6f289-144">L serisi</span><span class="sxs-lookup"><span data-stu-id="6f289-144">L series</span></span> | <span data-ttu-id="6f289-145">5630</span><span class="sxs-lookup"><span data-stu-id="6f289-145">5630</span></span> |
| [<span data-ttu-id="6f289-146">GPU</span><span class="sxs-lookup"><span data-stu-id="6f289-146">GPU</span></span>](sizes-gpu.md) | <span data-ttu-id="6f289-147">N serisi</span><span class="sxs-lookup"><span data-stu-id="6f289-147">N series</span></span> | <span data-ttu-id="6f289-148">1440</span><span class="sxs-lookup"><span data-stu-id="6f289-148">1440</span></span> |
| [<span data-ttu-id="6f289-149">Yüksek performans</span><span class="sxs-lookup"><span data-stu-id="6f289-149">High performance</span></span>](sizes-hpc.md) | <span data-ttu-id="6f289-150">A ve H serisi</span><span class="sxs-lookup"><span data-stu-id="6f289-150">A and H series</span></span> | <span data-ttu-id="6f289-151">2000</span><span class="sxs-lookup"><span data-stu-id="6f289-151">2000</span></span> |

## <a name="azure-data-disks"></a><span data-ttu-id="6f289-152">Azure veri diski</span><span class="sxs-lookup"><span data-stu-id="6f289-152">Azure data disks</span></span>

<span data-ttu-id="6f289-153">Uygulama yükleme ve verilerini depolamak için ek veri disklerinin eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="6f289-153">Additional data disks can be added for installing applications and storing data.</span></span> <span data-ttu-id="6f289-154">Veri diskleri sağlam ve esnek veri depolama burada istenen herhangi bir durumda kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="6f289-154">Data disks should be used in any situation where durable and responsive data storage is desired.</span></span> <span data-ttu-id="6f289-155">Her veri diski 1 terabayttan küçük maksimum kapasitesine sahiptir.</span><span class="sxs-lookup"><span data-stu-id="6f289-155">Each data disk has a maximum capacity of 1 terabyte.</span></span> <span data-ttu-id="6f289-156">Kaç tane veri diskleri için bir VM eklenebilecek sanal makine boyutunu belirler.</span><span class="sxs-lookup"><span data-stu-id="6f289-156">The size of the virtual machine determines how many data disks can be attached to a VM.</span></span> <span data-ttu-id="6f289-157">Her VM çekirdek için iki veri diskleri eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="6f289-157">For each VM core, two data disks can be attached.</span></span> 

### <a name="max-data-disks-per-vm"></a><span data-ttu-id="6f289-158">VM başına en fazla veri diski</span><span class="sxs-lookup"><span data-stu-id="6f289-158">Max data disks per VM</span></span>

| <span data-ttu-id="6f289-159">Tür</span><span class="sxs-lookup"><span data-stu-id="6f289-159">Type</span></span> | <span data-ttu-id="6f289-160">VM boyutu</span><span class="sxs-lookup"><span data-stu-id="6f289-160">VM Size</span></span> | <span data-ttu-id="6f289-161">VM başına en fazla veri diski</span><span class="sxs-lookup"><span data-stu-id="6f289-161">Max data disks per VM</span></span> |
|----|----|----|
| [<span data-ttu-id="6f289-162">Genel amaçlı</span><span class="sxs-lookup"><span data-stu-id="6f289-162">General purpose</span></span>](sizes-general.md) | <span data-ttu-id="6f289-163">A ve D serisi</span><span class="sxs-lookup"><span data-stu-id="6f289-163">A and D series</span></span> | <span data-ttu-id="6f289-164">32</span><span class="sxs-lookup"><span data-stu-id="6f289-164">32</span></span> |
| [<span data-ttu-id="6f289-165">İşlem için iyileştirilmiş</span><span class="sxs-lookup"><span data-stu-id="6f289-165">Compute optimized</span></span>](sizes-compute.md) | <span data-ttu-id="6f289-166">F serisi</span><span class="sxs-lookup"><span data-stu-id="6f289-166">F series</span></span> | <span data-ttu-id="6f289-167">32</span><span class="sxs-lookup"><span data-stu-id="6f289-167">32</span></span> |
| [<span data-ttu-id="6f289-168">Bellek için iyileştirilmiş</span><span class="sxs-lookup"><span data-stu-id="6f289-168">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md) | <span data-ttu-id="6f289-169">D ve G serisi</span><span class="sxs-lookup"><span data-stu-id="6f289-169">D and G series</span></span> | <span data-ttu-id="6f289-170">64</span><span class="sxs-lookup"><span data-stu-id="6f289-170">64</span></span> |
| [<span data-ttu-id="6f289-171">Depolama için iyileştirilmiş</span><span class="sxs-lookup"><span data-stu-id="6f289-171">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md) | <span data-ttu-id="6f289-172">L serisi</span><span class="sxs-lookup"><span data-stu-id="6f289-172">L series</span></span> | <span data-ttu-id="6f289-173">64</span><span class="sxs-lookup"><span data-stu-id="6f289-173">64</span></span> |
| [<span data-ttu-id="6f289-174">GPU</span><span class="sxs-lookup"><span data-stu-id="6f289-174">GPU</span></span>](sizes-gpu.md) | <span data-ttu-id="6f289-175">N serisi</span><span class="sxs-lookup"><span data-stu-id="6f289-175">N series</span></span> | <span data-ttu-id="6f289-176">48</span><span class="sxs-lookup"><span data-stu-id="6f289-176">48</span></span> |
| [<span data-ttu-id="6f289-177">Yüksek performans</span><span class="sxs-lookup"><span data-stu-id="6f289-177">High performance</span></span>](sizes-hpc.md) | <span data-ttu-id="6f289-178">A ve H serisi</span><span class="sxs-lookup"><span data-stu-id="6f289-178">A and H series</span></span> | <span data-ttu-id="6f289-179">32</span><span class="sxs-lookup"><span data-stu-id="6f289-179">32</span></span> |

## <a name="vm-disk-types"></a><span data-ttu-id="6f289-180">VM disk türleri</span><span class="sxs-lookup"><span data-stu-id="6f289-180">VM disk types</span></span>

<span data-ttu-id="6f289-181">Azure disk iki tür sağlar.</span><span class="sxs-lookup"><span data-stu-id="6f289-181">Azure provides two types of disk.</span></span>

### <a name="standard-disk"></a><span data-ttu-id="6f289-182">Standart disk</span><span class="sxs-lookup"><span data-stu-id="6f289-182">Standard disk</span></span>

<span data-ttu-id="6f289-183">Standart Depolama, HDD’ler ile desteklenir ve yüksek performans sunarken uygun maliyetli depolama sağlar.</span><span class="sxs-lookup"><span data-stu-id="6f289-183">Standard Storage is backed by HDDs, and delivers cost-effective storage while still being performant.</span></span> <span data-ttu-id="6f289-184">Standart diskler için uygun maliyetli geliştirme idealdir ve iş yükü test.</span><span class="sxs-lookup"><span data-stu-id="6f289-184">Standard disks are ideal for a cost effective dev and test workload.</span></span>

### <a name="premium-disk"></a><span data-ttu-id="6f289-185">Premium disk</span><span class="sxs-lookup"><span data-stu-id="6f289-185">Premium disk</span></span>

<span data-ttu-id="6f289-186">Premium diskler, SSD tabanlı yüksek performanslı, düşük gecikme süreli disk tarafından desteklenir.</span><span class="sxs-lookup"><span data-stu-id="6f289-186">Premium disks are backed by SSD-based high-performance, low-latency disk.</span></span> <span data-ttu-id="6f289-187">Üretim iş yükü çalıştıran VM'ler için mükemmel.</span><span class="sxs-lookup"><span data-stu-id="6f289-187">Perfect for VMs running production workload.</span></span> <span data-ttu-id="6f289-188">Premium depolama destekleyen DS serisi, DSv2 serisi, GS serisi ve FS-serisi VM'ler.</span><span class="sxs-lookup"><span data-stu-id="6f289-188">Premium Storage supports DS-series, DSv2-series, GS-series, and FS-series VMs.</span></span> <span data-ttu-id="6f289-189">Üç tür (P10, P20, P30) Premium diskleri gelir, disk türü disk boyutunu belirler.</span><span class="sxs-lookup"><span data-stu-id="6f289-189">Premium disks come in three types (P10, P20, P30), the size of the disk determines the disk type.</span></span> <span data-ttu-id="6f289-190">Disk boyutu değeri seçerken, sonraki türü yuvarlanır.</span><span class="sxs-lookup"><span data-stu-id="6f289-190">When selecting, a disk size the value is rounded up to the next type.</span></span> <span data-ttu-id="6f289-191">Örneğin, disk boyutu 128 GB daha az ise, disk türünü P10 ' dir.</span><span class="sxs-lookup"><span data-stu-id="6f289-191">For example, if the disk size is less than 128 GB, the disk type is P10.</span></span> <span data-ttu-id="6f289-192">Disk boyutu 129 GB ile 512 GB arasında ise, bir P20 boyutudur.</span><span class="sxs-lookup"><span data-stu-id="6f289-192">If the disk size is between 129 GB and 512 GB, the size is a P20.</span></span> <span data-ttu-id="6f289-193">Hiçbir şey 512 GB'den, bir P30 boyutudur.</span><span class="sxs-lookup"><span data-stu-id="6f289-193">Anything over 512 GB, the size is a P30.</span></span>

### <a name="premium-disk-performance"></a><span data-ttu-id="6f289-194">Premium disk performansı</span><span class="sxs-lookup"><span data-stu-id="6f289-194">Premium disk performance</span></span>

|<span data-ttu-id="6f289-195">Premium depolama disk türü</span><span class="sxs-lookup"><span data-stu-id="6f289-195">Premium storage disk type</span></span> | <span data-ttu-id="6f289-196">P10</span><span class="sxs-lookup"><span data-stu-id="6f289-196">P10</span></span> | <span data-ttu-id="6f289-197">P20</span><span class="sxs-lookup"><span data-stu-id="6f289-197">P20</span></span> | <span data-ttu-id="6f289-198">P30</span><span class="sxs-lookup"><span data-stu-id="6f289-198">P30</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6f289-199">Disk boyutu (yukarı yuvarlar)</span><span class="sxs-lookup"><span data-stu-id="6f289-199">Disk size (round up)</span></span> | <span data-ttu-id="6f289-200">128 GB</span><span class="sxs-lookup"><span data-stu-id="6f289-200">128 GB</span></span> | <span data-ttu-id="6f289-201">512 GB</span><span class="sxs-lookup"><span data-stu-id="6f289-201">512 GB</span></span> | <span data-ttu-id="6f289-202">1.024 GB (1 TB)</span><span class="sxs-lookup"><span data-stu-id="6f289-202">1,024 GB (1 TB)</span></span> |
| <span data-ttu-id="6f289-203">Disk başına en fazla IOPS</span><span class="sxs-lookup"><span data-stu-id="6f289-203">Max IOPS per disk</span></span> | <span data-ttu-id="6f289-204">500</span><span class="sxs-lookup"><span data-stu-id="6f289-204">500</span></span> | <span data-ttu-id="6f289-205">2,300</span><span class="sxs-lookup"><span data-stu-id="6f289-205">2,300</span></span> | <span data-ttu-id="6f289-206">5,000</span><span class="sxs-lookup"><span data-stu-id="6f289-206">5,000</span></span> |
<span data-ttu-id="6f289-207">Disk başına aktarım hızı</span><span class="sxs-lookup"><span data-stu-id="6f289-207">Throughput per disk</span></span> | <span data-ttu-id="6f289-208">100 MB/s</span><span class="sxs-lookup"><span data-stu-id="6f289-208">100 MB/s</span></span> | <span data-ttu-id="6f289-209">150 MB/s</span><span class="sxs-lookup"><span data-stu-id="6f289-209">150 MB/s</span></span> | <span data-ttu-id="6f289-210">200 MB/sn</span><span class="sxs-lookup"><span data-stu-id="6f289-210">200 MB/s</span></span> |

<span data-ttu-id="6f289-211">Yukarıdaki tabloda, disk başına maksimum IOPS tanımlanmaktadır olsa da, daha yüksek düzeyde performans birden çok veri diskleri bölümlemesine tarafından elde edilebilir.</span><span class="sxs-lookup"><span data-stu-id="6f289-211">While the above table identifies max IOPS per disk, a higher level of performance can be achieved by striping multiple data disks.</span></span> <span data-ttu-id="6f289-212">Örneğin, bir Standard_GS5 VM en 80.000 IOPS elde edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6f289-212">For instance, a Standard_GS5 VM can achieve a maximum of 80,000 IOPS.</span></span> <span data-ttu-id="6f289-213">VM başına maksimum IOPS hakkında ayrıntılı bilgi için bkz: [Linux VM boyutları](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="6f289-213">For detailed information on max IOPS per VM, see [Linux VM sizes](sizes.md).</span></span>

## <a name="create-and-attach-disks"></a><span data-ttu-id="6f289-214">Oluşturma ve diskleri ekleme</span><span class="sxs-lookup"><span data-stu-id="6f289-214">Create and attach disks</span></span>

<span data-ttu-id="6f289-215">Veri diskleri oluşturulur ve VM oluşturma zamanında veya mevcut bir VM'yi bağlı.</span><span class="sxs-lookup"><span data-stu-id="6f289-215">Data disks can be created and attached at VM creation time or to an existing VM.</span></span>

### <a name="attach-disk-at-vm-creation"></a><span data-ttu-id="6f289-216">VM oluşturulurken diski kullanıma açın</span><span class="sxs-lookup"><span data-stu-id="6f289-216">Attach disk at VM creation</span></span>

<span data-ttu-id="6f289-217">[az group create](https://docs.microsoft.com/cli/azure/group#create) komutuyla bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="6f289-217">Create a resource group with the [az group create](https://docs.microsoft.com/cli/azure/group#create) command.</span></span> 

```azurecli-interactive 
az group create --name myResourceGroupDisk --location eastus
```

<span data-ttu-id="6f289-218">Kullanarak bir VM oluşturun [az vm oluşturma]( /cli/azure/vm#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="6f289-218">Create a VM using the [az vm create]( /cli/azure/vm#create) command.</span></span> <span data-ttu-id="6f289-219">`--datadisk-sizes-gb` Bağımsız değişkeni bir ek disk oluşturulabilir ve sanal makineye bağlı olduğunu belirtmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="6f289-219">The `--datadisk-sizes-gb` argument is used to specify that an additional disk should be created and attached to the virtual machine.</span></span> <span data-ttu-id="6f289-220">Oluşturma ve birden fazla disk eklemek için disk boyutu değerleri boşlukla ayrılmış bir listesini kullanın.</span><span class="sxs-lookup"><span data-stu-id="6f289-220">To create and attach more than one disk, use a space-delimited list of disk size values.</span></span> <span data-ttu-id="6f289-221">Aşağıdaki örnekte, iki veri disklerinde, her iki 128 GB VM oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="6f289-221">In the following example, a VM is created with two data disks, both 128 GB.</span></span> <span data-ttu-id="6f289-222">128 GB disk boyutu olduğundan, bu diskleri hem de disk başına en fazla 500 IOPS sağlar P10s olarak yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="6f289-222">Because the disk sizes are 128 GB, these disks are both configured as P10s, which provide maximum 500 IOPS per disk.</span></span>

```azurecli-interactive 
az vm create \
  --resource-group myResourceGroupDisk \
  --name myVM \
  --image UbuntuLTS \
  --size Standard_DS2_v2 \
  --data-disk-sizes-gb 128 128 \
  --generate-ssh-keys
```

### <a name="attach-disk-to-existing-vm"></a><span data-ttu-id="6f289-223">Var olan VM disk ekleme</span><span class="sxs-lookup"><span data-stu-id="6f289-223">Attach disk to existing VM</span></span>

<span data-ttu-id="6f289-224">Oluşturabilir ve varolan bir sanal makineye yeni bir disk eklemek için kullanın [az vm diskini](/cli/azure/vm/disk#attach) komutu.</span><span class="sxs-lookup"><span data-stu-id="6f289-224">To create and attach a new disk to an existing virtual machine, use the [az vm disk attach](/cli/azure/vm/disk#attach) command.</span></span> <span data-ttu-id="6f289-225">Aşağıdaki örnek, bir premium disk boyutu, 128 gigabayt oluşturur ve son adımda oluşturulan VM ekler.</span><span class="sxs-lookup"><span data-stu-id="6f289-225">The following example creates a premium disk, 128 gigabytes in size, and attaches it to the VM created in the last step.</span></span>

```azurecli-interactive 
az vm disk attach --vm-name myVM --resource-group myResourceGroupDisk --disk myDataDisk --size-gb 128 --sku Premium_LRS --new 
```

## <a name="prepare-data-disks"></a><span data-ttu-id="6f289-226">Veri diskleri hazırlama</span><span class="sxs-lookup"><span data-stu-id="6f289-226">Prepare data disks</span></span>

<span data-ttu-id="6f289-227">Bir disk sanal makineye bağlandıktan sonra işletim sistemi diski kullanacak şekilde yapılandırılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="6f289-227">Once a disk has been attached to the virtual machine, the operating system needs to be configured to use the disk.</span></span> <span data-ttu-id="6f289-228">Aşağıdaki örnek, el ile bir disk nasıl yapılandırılacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="6f289-228">The following example shows how to manually configure a disk.</span></span> <span data-ttu-id="6f289-229">Bu işlem ayrıca içinde ele bulut-init, kullanarak otomatik olarak yapılabilir bir [sonraki öğretici](./tutorial-automate-vm-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="6f289-229">This process can also be automated using cloud-init, which is covered in a [later tutorial](./tutorial-automate-vm-deployment.md).</span></span>

### <a name="manual-configuration"></a><span data-ttu-id="6f289-230">El ile yapılandırma</span><span class="sxs-lookup"><span data-stu-id="6f289-230">Manual configuration</span></span>

<span data-ttu-id="6f289-231">Sanal makine ile bir SSH bağlantısı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="6f289-231">Create an SSH connection with the virtual machine.</span></span> <span data-ttu-id="6f289-232">Örnek IP adresinin, sanal makine genel IP ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="6f289-232">Replace the example IP address with the public IP of the virtual machine.</span></span>

```azurecli-interactive 
ssh 52.174.34.95
```

<span data-ttu-id="6f289-233">Diskle bölüm `fdisk`.</span><span class="sxs-lookup"><span data-stu-id="6f289-233">Partition the disk with `fdisk`.</span></span>

```bash
(echo n; echo p; echo 1; echo ; echo ; echo w) | sudo fdisk /dev/sdc
```

<span data-ttu-id="6f289-234">Kullanarak bir dosya sistemi bölüm için yazma `mkfs` komutu.</span><span class="sxs-lookup"><span data-stu-id="6f289-234">Write a file system to the partition by using the `mkfs` command.</span></span>

```bash
sudo mkfs -t ext4 /dev/sdc1
```

<span data-ttu-id="6f289-235">Böylece işletim sisteminde erişilebilir yeni diski bağlayın.</span><span class="sxs-lookup"><span data-stu-id="6f289-235">Mount the new disk so that it is accessible in the operating system.</span></span>

```bash
sudo mkdir /datadrive && sudo mount /dev/sdc1 /datadrive
```

<span data-ttu-id="6f289-236">Disk şimdi aracılığıyla erişilebilir *datadrive* çalıştırarak doğrulanabilir mountpoint `df -h` komutu.</span><span class="sxs-lookup"><span data-stu-id="6f289-236">The disk can now be accessed through the *datadrive* mountpoint, which can be verified by running the `df -h` command.</span></span> 

```bash
df -h
```

<span data-ttu-id="6f289-237">Çıktı üzerinde oluşturulmuş yeni bir sürücüye gösterir */datadrive*.</span><span class="sxs-lookup"><span data-stu-id="6f289-237">The output shows the new drive mounted on */datadrive*.</span></span>

```bash
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda1        30G  1.4G   28G   5% /
/dev/sdb1       6.8G   16M  6.4G   1% /mnt
/dev/sdc1        50G   52M   47G   1% /datadrive
```

<span data-ttu-id="6f289-238">Yeniden başlatmanın ardından sürücüsünün yeniden emin olmak için onu eklenmeli */etc/fstab* dosya.</span><span class="sxs-lookup"><span data-stu-id="6f289-238">To ensure that the drive is remounted after a reboot, it must be added to the */etc/fstab* file.</span></span> <span data-ttu-id="6f289-239">Bunu yapmak için diski UUID'si almak `blkid` yardımcı programı.</span><span class="sxs-lookup"><span data-stu-id="6f289-239">To do so, get the UUID of the disk with the `blkid` utility.</span></span>

```bash
sudo -i blkid
```

<span data-ttu-id="6f289-240">Sürücü UUID'si çıktısını görüntüler `/dev/sdc1` bu durumda.</span><span class="sxs-lookup"><span data-stu-id="6f289-240">The output displays the UUID of the drive, `/dev/sdc1` in this case.</span></span>

```bash
/dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
```

<span data-ttu-id="6f289-241">Aşağıdakine benzer bir satır ekleyin */etc/fstab* dosya.</span><span class="sxs-lookup"><span data-stu-id="6f289-241">Add a line similar to the following to the */etc/fstab* file.</span></span> <span data-ttu-id="6f289-242">Ayrıca engelleri yazma Not kullanarak devre dışı bırakılabilir *engel = 0*, bu yapılandırma disk performansını artırabilir.</span><span class="sxs-lookup"><span data-stu-id="6f289-242">Also note that write barriers can be disabled using *barrier=0*, this configuration can improve disk performance.</span></span> 

```bash
UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive  ext4    defaults,nofail,barrier=0   1  2
```

<span data-ttu-id="6f289-243">Disk yapılandırılabilir, SSH oturumu kapatın.</span><span class="sxs-lookup"><span data-stu-id="6f289-243">Now that the disk has been configured, close the SSH session.</span></span>

```bash
exit
```

## <a name="resize-vm-disk"></a><span data-ttu-id="6f289-244">VM disk yeniden boyutlandırma</span><span class="sxs-lookup"><span data-stu-id="6f289-244">Resize VM disk</span></span>

<span data-ttu-id="6f289-245">Bir VM dağıtıldıktan sonra işletim sistemi diski veya hiçbir bağlı veri diski boyutu artırılabilir.</span><span class="sxs-lookup"><span data-stu-id="6f289-245">Once a VM has been deployed, the operating system disk or any attached data disks can be increased in size.</span></span> <span data-ttu-id="6f289-246">Bir diskin boyutunu artırmayı daha fazla depolama alanı ya da daha yüksek düzeyde performans (P10, P20, P30) ihtiyacı olduğunda faydalıdır.</span><span class="sxs-lookup"><span data-stu-id="6f289-246">Increasing the size of a disk is beneficial when needing more storage space or a higher level of performance (P10, P20, P30).</span></span> <span data-ttu-id="6f289-247">Disk boyutu azaltılamaz unutmayın.</span><span class="sxs-lookup"><span data-stu-id="6f289-247">Note, disks cannot be decreased in size.</span></span>

<span data-ttu-id="6f289-248">Disk boyutunu artırmayı önce kimliği veya disk adı gerekli.</span><span class="sxs-lookup"><span data-stu-id="6f289-248">Before increasing disk size, the Id or name of the disk is needed.</span></span> <span data-ttu-id="6f289-249">Kullanım [az disk listesi](/cli/azure/vm/disk#list) bir kaynak grubunda tüm diskleri döndürülecek komutu.</span><span class="sxs-lookup"><span data-stu-id="6f289-249">Use the [az disk list](/cli/azure/vm/disk#list) command to return all disks in a resource group.</span></span> <span data-ttu-id="6f289-250">Yeniden boyutlandırma istediğiniz disk adını not edin.</span><span class="sxs-lookup"><span data-stu-id="6f289-250">Take note of the disk name that you would like to resize.</span></span>

```azurecli-interactive 
az disk list -g myResourceGroupDisk --query '[*].{Name:name,Gb:diskSizeGb,Tier:accountType}' --output table
```

<span data-ttu-id="6f289-251">VM de serbest gerekir.</span><span class="sxs-lookup"><span data-stu-id="6f289-251">The VM must also be deallocated.</span></span> <span data-ttu-id="6f289-252">Kullanım [az vm serbest bırakma]( /cli/azure/vm#deallocate) durdurun ve VM serbest bırakma için komutu.</span><span class="sxs-lookup"><span data-stu-id="6f289-252">Use the [az vm deallocate]( /cli/azure/vm#deallocate) command to stop and deallocate the VM.</span></span>

```azurecli-interactive 
az vm deallocate --resource-group myResourceGroupDisk --name myVM
```

<span data-ttu-id="6f289-253">Kullanım [az disk güncelleştirme](/cli/azure/vm/disk#update) diski yeniden boyutlandırmak için komutu.</span><span class="sxs-lookup"><span data-stu-id="6f289-253">Use the [az disk update](/cli/azure/vm/disk#update) command to resize the disk.</span></span> <span data-ttu-id="6f289-254">Bu örnek adlı bir disk yeniden boyutlandırır *myDataDisk* 1 terabayttan küçük için.</span><span class="sxs-lookup"><span data-stu-id="6f289-254">This example resizes a disk named *myDataDisk* to 1 terabyte.</span></span>

```azurecli-interactive 
az disk update --name myDataDisk --resource-group myResourceGroupDisk --size-gb 1023
```

<span data-ttu-id="6f289-255">Yeniden boyutlandırma işlemi tamamlandıktan sonra VM'yi başlatın.</span><span class="sxs-lookup"><span data-stu-id="6f289-255">Once the resize operation has completed, start the VM.</span></span>

```azurecli-interactive 
az vm start --resource-group myResourceGroupDisk --name myVM
```

<span data-ttu-id="6f289-256">İşletim sistemi diski yeniden boyutlandırılabilir, bölüm otomatik olarak olması genişletilmiştir.</span><span class="sxs-lookup"><span data-stu-id="6f289-256">If you’ve resized the operating system disk, the partition is automatically be expanded.</span></span> <span data-ttu-id="6f289-257">Bir veri diski yeniden boyutlandırılabilir VM'ler işletim sisteminde genişletilecek geçerli bölümler gerekir.</span><span class="sxs-lookup"><span data-stu-id="6f289-257">If you have resized a data disk, any current partitions need to be expanded in the VMs operating system.</span></span>

## <a name="snapshot-azure-disks"></a><span data-ttu-id="6f289-258">Azure diskleri anlık görüntüsünü alın</span><span class="sxs-lookup"><span data-stu-id="6f289-258">Snapshot Azure disks</span></span>

<span data-ttu-id="6f289-259">Bir disk anlık disk okuma yalnızca, zaman noktası kopyasını oluşturur.</span><span class="sxs-lookup"><span data-stu-id="6f289-259">Taking a disk snapshot creates a read only, point-in-time copy of the disk.</span></span> <span data-ttu-id="6f289-260">Azure VM anlık görüntüler, yapılandırma değişiklikleri yapmadan önce bir VM durumunu hızlı bir şekilde kaydetmek için kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="6f289-260">Azure VM snapshots are useful for quickly saving the state of a VM before making configuration changes.</span></span> <span data-ttu-id="6f289-261">İstenmeyen olması için yapılandırma değişiklikleri kanıtlanmasına durumunda VM durumunu anlık görüntü kullanılarak geri yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="6f289-261">In the event the configuration changes prove to be undesired, VM state can be restored using the snapshot.</span></span> <span data-ttu-id="6f289-262">Birden fazla disk bir VM'ye sahip olduğu anlık görüntü diğer bağımsız olarak her diskin alınır.</span><span class="sxs-lookup"><span data-stu-id="6f289-262">When a VM has more than one disk, a snapshot is taken of each disk independently of the others.</span></span> <span data-ttu-id="6f289-263">Uygulama tutarlı yedek almak için disk anlık görüntüler gerçekleştirmeden önce VM durdurma göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="6f289-263">For taking application consistent backups, consider stopping the VM before taking disk snapshots.</span></span> <span data-ttu-id="6f289-264">Alternatif olarak, kullanın [Azure Backup hizmeti](/azure/backup/), VM çalışırken otomatik yedeklemeler sağlar.</span><span class="sxs-lookup"><span data-stu-id="6f289-264">Alternatively, use the [Azure Backup service](/azure/backup/), which enables you to perform automated backups while the VM is running.</span></span>

### <a name="create-snapshot"></a><span data-ttu-id="6f289-265">Anlık görüntü oluşturma</span><span class="sxs-lookup"><span data-stu-id="6f289-265">Create snapshot</span></span>

<span data-ttu-id="6f289-266">Bir sanal makine disk anlık oluşturmadan önce kimliği veya disk adı gerekli.</span><span class="sxs-lookup"><span data-stu-id="6f289-266">Before creating a virtual machine disk snapshot, the Id or name of the disk is needed.</span></span> <span data-ttu-id="6f289-267">Kullanım [az vm Göster](https://docs.microsoft.com/en-us/cli/azure/vm#show) disk kimliği döndürülecek komutu.</span><span class="sxs-lookup"><span data-stu-id="6f289-267">Use the [az vm show](https://docs.microsoft.com/en-us/cli/azure/vm#show) command to return the disk id.</span></span> <span data-ttu-id="6f289-268">Bu örnekte, böylece daha sonraki bir adımda kullanılabilir disk kimliği bir değişkende depolanır.</span><span class="sxs-lookup"><span data-stu-id="6f289-268">In this example, the disk id is stored in a variable so that it can be used in a later step.</span></span>

```azurecli-interactive 
osdiskid=$(az vm show -g myResourceGroupDisk -n myVM --query "storageProfile.osDisk.managedDisk.id" -o tsv)
```

<span data-ttu-id="6f289-269">Sanal makine diskini kimliğini sahip olduğunuza göre aşağıdaki komut diskin anlık görüntüsünü oluşturur.</span><span class="sxs-lookup"><span data-stu-id="6f289-269">Now that you have the id of the virtual machine disk, the following command creates a snapshot of the disk.</span></span>

```azurcli
az snapshot create -g myResourceGroupDisk --source "$osdiskid" --name osDisk-backup
```

### <a name="create-disk-from-snapshot"></a><span data-ttu-id="6f289-270">Disk anlık görüntüden oluşturma</span><span class="sxs-lookup"><span data-stu-id="6f289-270">Create disk from snapshot</span></span>

<span data-ttu-id="6f289-271">Bu anlık görüntü sonra sanal makineyi yeniden oluşturmak için kullanılan bir diske dönüştürülebilir.</span><span class="sxs-lookup"><span data-stu-id="6f289-271">This snapshot can then be converted into a disk, which can be used to recreate the virtual machine.</span></span>

```azurecli-interactive 
az disk create --resource-group myResourceGroupDisk --name mySnapshotDisk --source osDisk-backup
```

### <a name="restore-virtual-machine-from-snapshot"></a><span data-ttu-id="6f289-272">Sanal makine anlık görüntüden geri yükleme</span><span class="sxs-lookup"><span data-stu-id="6f289-272">Restore virtual machine from snapshot</span></span>

<span data-ttu-id="6f289-273">Sanal makine kurtarması göstermek için var olan sanal makineyi silin.</span><span class="sxs-lookup"><span data-stu-id="6f289-273">To demonstrate virtual machine recovery, delete the existing virtual machine.</span></span> 

```azurecli-interactive 
az vm delete --resource-group myResourceGroupDisk --name myVM
```

<span data-ttu-id="6f289-274">Yeni bir sanal makine anlık görüntü diski oluşturun.</span><span class="sxs-lookup"><span data-stu-id="6f289-274">Create a new virtual machine from the snapshot disk.</span></span>

```azurecli-interactive 
az vm create --resource-group myResourceGroupDisk --name myVM --attach-os-disk mySnapshotDisk --os-type linux
```

### <a name="reattach-data-disk"></a><span data-ttu-id="6f289-275">Veri diski yeniden bağlayın</span><span class="sxs-lookup"><span data-stu-id="6f289-275">Reattach data disk</span></span>

<span data-ttu-id="6f289-276">Tüm veri diskleri sanal makineyi yeniden gerekir.</span><span class="sxs-lookup"><span data-stu-id="6f289-276">All data disks need to be reattached to the virtual machine.</span></span>

<span data-ttu-id="6f289-277">İlk disk adı kullanarak verileri bulma [az disk listesi](https://docs.microsoft.com/cli/azure/disk#list) komutu.</span><span class="sxs-lookup"><span data-stu-id="6f289-277">First find the data disk name using the [az disk list](https://docs.microsoft.com/cli/azure/disk#list) command.</span></span> <span data-ttu-id="6f289-278">Bu örnek diskin adını adlı bir değişkende yerleştirir *datadisk*, sonraki adımda kullanılır.</span><span class="sxs-lookup"><span data-stu-id="6f289-278">This example places the name of the disk in a variable named *datadisk*, which is used in the next step.</span></span>

```azurecli-interactive 
datadisk=$(az disk list -g myResourceGroupDisk --query "[?contains(name,'myVM')].[name]" -o tsv)
```

<span data-ttu-id="6f289-279">Kullanım [az vm diskini](https://docs.microsoft.com/cli/azure/vm/disk#attach) diski eklemek için komutu.</span><span class="sxs-lookup"><span data-stu-id="6f289-279">Use the [az vm disk attach](https://docs.microsoft.com/cli/azure/vm/disk#attach) command to attach the disk.</span></span>

```azurecli-interactive 
az vm disk attach –g myResourceGroupDisk –-vm-name myVM –-disk $datadisk
```

## <a name="next-steps"></a><span data-ttu-id="6f289-280">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="6f289-280">Next steps</span></span>

<span data-ttu-id="6f289-281">Bu öğreticide, VM diskleri konuları hakkında gibi öğrenilen:</span><span class="sxs-lookup"><span data-stu-id="6f289-281">In this tutorial, you learned about VM disks topics such as:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6f289-282">İşletim sistemi ve geçici disklerle</span><span class="sxs-lookup"><span data-stu-id="6f289-282">OS disks and temporary disks</span></span>
> * <span data-ttu-id="6f289-283">Veri diskleri</span><span class="sxs-lookup"><span data-stu-id="6f289-283">Data disks</span></span>
> * <span data-ttu-id="6f289-284">Standart ve Premium diskleri</span><span class="sxs-lookup"><span data-stu-id="6f289-284">Standard and Premium disks</span></span>
> * <span data-ttu-id="6f289-285">Disk performansı</span><span class="sxs-lookup"><span data-stu-id="6f289-285">Disk performance</span></span>
> * <span data-ttu-id="6f289-286">Ekleme ve veri diskleri hazırlama</span><span class="sxs-lookup"><span data-stu-id="6f289-286">Attaching and preparing data disks</span></span>
> * <span data-ttu-id="6f289-287">Diskleri yeniden boyutlandırma</span><span class="sxs-lookup"><span data-stu-id="6f289-287">Resizing disks</span></span>
> * <span data-ttu-id="6f289-288">Disk anlık görüntüler</span><span class="sxs-lookup"><span data-stu-id="6f289-288">Disk snapshots</span></span>

<span data-ttu-id="6f289-289">VM yapılandırması otomatikleştirme hakkında bilgi edinmek için sonraki öğretici ilerleyin.</span><span class="sxs-lookup"><span data-stu-id="6f289-289">Advance to the next tutorial to learn about automating VM configuration.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="6f289-290">VM yapılandırmasını otomatikleştirme</span><span class="sxs-lookup"><span data-stu-id="6f289-290">Automate VM configuration</span></span>](./tutorial-automate-vm-deployment.md)
