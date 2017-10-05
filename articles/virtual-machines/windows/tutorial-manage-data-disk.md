---
title: "Azure PowerShell ile Azure diskleri yönetme | Microsoft Docs"
description: "Öğretici - Azure PowerShell ile Azure diskleri yönetme"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 6f1bc9361745adc211f22416a7ba8ac1b8dc614e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-azure-disks-with-powershell"></a><span data-ttu-id="52d49-103">PowerShell ile Azure diskleri yönetme</span><span class="sxs-lookup"><span data-stu-id="52d49-103">Manage Azure disks with PowerShell</span></span>

<span data-ttu-id="52d49-104">Azure sanal makineleri diskleri sanal makineleri işletim sistemi, uygulamaları ve verileri depolamak için kullanır.</span><span class="sxs-lookup"><span data-stu-id="52d49-104">Azure virtual machines use disks to store the VMs operating system, applications, and data.</span></span> <span data-ttu-id="52d49-105">Bir VM oluşturulurken bir disk boyutu ve beklenen iş yükü için uygun yapılandırma seçmek önemlidir.</span><span class="sxs-lookup"><span data-stu-id="52d49-105">When creating a VM it is important to choose a disk size and configuration appropriate to the expected workload.</span></span> <span data-ttu-id="52d49-106">Bu öğretici, dağıtma ve VM diskleri yönetme kapsar.</span><span class="sxs-lookup"><span data-stu-id="52d49-106">This tutorial covers deploying and managing VM disks.</span></span> <span data-ttu-id="52d49-107">Hakkında bilgi edinin:</span><span class="sxs-lookup"><span data-stu-id="52d49-107">You learn about:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="52d49-108">İşletim sistemi ve geçici disklerle</span><span class="sxs-lookup"><span data-stu-id="52d49-108">OS disks and temporary disks</span></span>
> * <span data-ttu-id="52d49-109">Veri diskleri</span><span class="sxs-lookup"><span data-stu-id="52d49-109">Data disks</span></span>
> * <span data-ttu-id="52d49-110">Standart ve Premium diskleri</span><span class="sxs-lookup"><span data-stu-id="52d49-110">Standard and Premium disks</span></span>
> * <span data-ttu-id="52d49-111">Disk performansı</span><span class="sxs-lookup"><span data-stu-id="52d49-111">Disk performance</span></span>
> * <span data-ttu-id="52d49-112">Ekleme ve veri diskleri hazırlama</span><span class="sxs-lookup"><span data-stu-id="52d49-112">Attaching and preparing data disks</span></span>

<span data-ttu-id="52d49-113">Bu öğretici, Azure PowerShell modülü 3.6 veya sonraki bir sürümü gerektirir.</span><span class="sxs-lookup"><span data-stu-id="52d49-113">This tutorial requires the Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="52d49-114">Sürümü bulmak için ` Get-Module -ListAvailable AzureRM` komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="52d49-114">Run ` Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="52d49-115">Yükseltme gerekiyorsa, bkz: [yükleme Azure PowerShell Modülü](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="52d49-115">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="default-azure-disks"></a><span data-ttu-id="52d49-116">Azure diskleri varsayılan</span><span class="sxs-lookup"><span data-stu-id="52d49-116">Default Azure disks</span></span>

<span data-ttu-id="52d49-117">Bir Azure sanal makine oluşturulduğunda, iki disk otomatik olarak sanal makineye bağlanmış.</span><span class="sxs-lookup"><span data-stu-id="52d49-117">When an Azure virtual machine is created, two disks are automatically attached to the virtual machine.</span></span> 

<span data-ttu-id="52d49-118">**İşletim sistemi diski** -işletim sistemi disklerinde en fazla 1 terabayttan küçük boyuta sahip ve VM'ler işletim sistemi barındırır.</span><span class="sxs-lookup"><span data-stu-id="52d49-118">**Operating system disk** - Operating system disks can be sized up to 1 terabyte, and hosts the VMs operating system.</span></span>  <span data-ttu-id="52d49-119">İşletim sistemi diski bir sürücü harfi atanmış *c:* varsayılan olarak.</span><span class="sxs-lookup"><span data-stu-id="52d49-119">The OS disk is assigned a drive letter of *c:* by default.</span></span> <span data-ttu-id="52d49-120">İşletim sistemi disk yapılandırması önbelleğe alma disk işletim sistemi performans için optimize edilmiştir.</span><span class="sxs-lookup"><span data-stu-id="52d49-120">The disk caching configuration of the OS disk is optimized for OS performance.</span></span> <span data-ttu-id="52d49-121">İşletim sistemi diski **vermemelisiniz** konak uygulamalar veya veri.</span><span class="sxs-lookup"><span data-stu-id="52d49-121">The OS disk **should not** host applications or data.</span></span> <span data-ttu-id="52d49-122">Uygulamalar ve veriler için bu makalenin sonraki bölümlerinde ayrıntılı bir veri diski kullanın.</span><span class="sxs-lookup"><span data-stu-id="52d49-122">For applications and data, use a data disk, which is detailed later in this article.</span></span>

<span data-ttu-id="52d49-123">**Geçici disk** -geçici diskleri VM ile aynı Azure konakta bulunan bir katı hal sürücüsü kullanın.</span><span class="sxs-lookup"><span data-stu-id="52d49-123">**Temporary disk** - Temporary disks use a solid-state drive that is located on the same Azure host as the VM.</span></span> <span data-ttu-id="52d49-124">Temp disklerinin yüksek oranda kullanıcı durumda ve geçici veri işleme gibi işlemler için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="52d49-124">Temp disks are highly performant and may be used for operations such as temporary data processing.</span></span> <span data-ttu-id="52d49-125">Ancak, VM yeni bir ana bilgisayara taşındığında, geçici bir diskte depolanan tüm verileri kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="52d49-125">However, if the VM is moved to a new host, any data stored on a temporary disk is removed.</span></span> <span data-ttu-id="52d49-126">Geçici disk boyutunu VM boyutu tarafından belirlenir.</span><span class="sxs-lookup"><span data-stu-id="52d49-126">The size of the temporary disk is determined by the VM size.</span></span> <span data-ttu-id="52d49-127">Geçici diskleri bir sürücü harfi atanmış *d:* varsayılan olarak.</span><span class="sxs-lookup"><span data-stu-id="52d49-127">Temporary disks are assigned a drive letter of *d:* by default.</span></span>

### <a name="temporary-disk-sizes"></a><span data-ttu-id="52d49-128">Geçici disk boyutları</span><span class="sxs-lookup"><span data-stu-id="52d49-128">Temporary disk sizes</span></span>

| <span data-ttu-id="52d49-129">Tür</span><span class="sxs-lookup"><span data-stu-id="52d49-129">Type</span></span> | <span data-ttu-id="52d49-130">VM boyutu</span><span class="sxs-lookup"><span data-stu-id="52d49-130">VM Size</span></span> | <span data-ttu-id="52d49-131">En büyük geçici disk boyutu (GB)</span><span class="sxs-lookup"><span data-stu-id="52d49-131">Max temp disk size (GB)</span></span> |
|----|----|----|
| [<span data-ttu-id="52d49-132">Genel amaçlı</span><span class="sxs-lookup"><span data-stu-id="52d49-132">General purpose</span></span>](sizes-general.md) | <span data-ttu-id="52d49-133">A ve D serisi</span><span class="sxs-lookup"><span data-stu-id="52d49-133">A and D series</span></span> | <span data-ttu-id="52d49-134">800</span><span class="sxs-lookup"><span data-stu-id="52d49-134">800</span></span> |
| [<span data-ttu-id="52d49-135">İşlem için iyileştirilmiş</span><span class="sxs-lookup"><span data-stu-id="52d49-135">Compute optimized</span></span>](sizes-compute.md) | <span data-ttu-id="52d49-136">F serisi</span><span class="sxs-lookup"><span data-stu-id="52d49-136">F series</span></span> | <span data-ttu-id="52d49-137">800</span><span class="sxs-lookup"><span data-stu-id="52d49-137">800</span></span> |
| [<span data-ttu-id="52d49-138">Bellek için iyileştirilmiş</span><span class="sxs-lookup"><span data-stu-id="52d49-138">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md) | <span data-ttu-id="52d49-139">D ve G serisi</span><span class="sxs-lookup"><span data-stu-id="52d49-139">D and G series</span></span> | <span data-ttu-id="52d49-140">6144</span><span class="sxs-lookup"><span data-stu-id="52d49-140">6144</span></span> |
| [<span data-ttu-id="52d49-141">Depolama için iyileştirilmiş</span><span class="sxs-lookup"><span data-stu-id="52d49-141">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md) | <span data-ttu-id="52d49-142">L serisi</span><span class="sxs-lookup"><span data-stu-id="52d49-142">L series</span></span> | <span data-ttu-id="52d49-143">5630</span><span class="sxs-lookup"><span data-stu-id="52d49-143">5630</span></span> |
| [<span data-ttu-id="52d49-144">GPU</span><span class="sxs-lookup"><span data-stu-id="52d49-144">GPU</span></span>](sizes-gpu.md) | <span data-ttu-id="52d49-145">N serisi</span><span class="sxs-lookup"><span data-stu-id="52d49-145">N series</span></span> | <span data-ttu-id="52d49-146">1440</span><span class="sxs-lookup"><span data-stu-id="52d49-146">1440</span></span> |
| [<span data-ttu-id="52d49-147">Yüksek performans</span><span class="sxs-lookup"><span data-stu-id="52d49-147">High performance</span></span>](sizes-hpc.md) | <span data-ttu-id="52d49-148">A ve H serisi</span><span class="sxs-lookup"><span data-stu-id="52d49-148">A and H series</span></span> | <span data-ttu-id="52d49-149">2000</span><span class="sxs-lookup"><span data-stu-id="52d49-149">2000</span></span> |

## <a name="azure-data-disks"></a><span data-ttu-id="52d49-150">Azure veri diski</span><span class="sxs-lookup"><span data-stu-id="52d49-150">Azure data disks</span></span>

<span data-ttu-id="52d49-151">Uygulama yükleme ve verilerini depolamak için ek veri disklerinin eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="52d49-151">Additional data disks can be added for installing applications and storing data.</span></span> <span data-ttu-id="52d49-152">Veri diskleri sağlam ve esnek veri depolama burada istenen herhangi bir durumda kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="52d49-152">Data disks should be used in any situation where durable and responsive data storage is desired.</span></span> <span data-ttu-id="52d49-153">Her veri diski 1 terabayttan küçük maksimum kapasitesine sahiptir.</span><span class="sxs-lookup"><span data-stu-id="52d49-153">Each data disk has a maximum capacity of 1 terabyte.</span></span> <span data-ttu-id="52d49-154">Kaç tane veri diskleri için bir VM eklenebilecek sanal makine boyutunu belirler.</span><span class="sxs-lookup"><span data-stu-id="52d49-154">The size of the virtual machine determines how many data disks can be attached to a VM.</span></span> <span data-ttu-id="52d49-155">Her VM çekirdek için iki veri diskleri eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="52d49-155">For each VM core, two data disks can be attached.</span></span> 

### <a name="max-data-disks-per-vm"></a><span data-ttu-id="52d49-156">VM başına en fazla veri diski</span><span class="sxs-lookup"><span data-stu-id="52d49-156">Max data disks per VM</span></span>

| <span data-ttu-id="52d49-157">Tür</span><span class="sxs-lookup"><span data-stu-id="52d49-157">Type</span></span> | <span data-ttu-id="52d49-158">VM boyutu</span><span class="sxs-lookup"><span data-stu-id="52d49-158">VM Size</span></span> | <span data-ttu-id="52d49-159">VM başına en fazla veri diski</span><span class="sxs-lookup"><span data-stu-id="52d49-159">Max data disks per VM</span></span> |
|----|----|----|
| [<span data-ttu-id="52d49-160">Genel amaçlı</span><span class="sxs-lookup"><span data-stu-id="52d49-160">General purpose</span></span>](sizes-general.md) | <span data-ttu-id="52d49-161">A ve D serisi</span><span class="sxs-lookup"><span data-stu-id="52d49-161">A and D series</span></span> | <span data-ttu-id="52d49-162">32</span><span class="sxs-lookup"><span data-stu-id="52d49-162">32</span></span> |
| [<span data-ttu-id="52d49-163">İşlem için iyileştirilmiş</span><span class="sxs-lookup"><span data-stu-id="52d49-163">Compute optimized</span></span>](sizes-compute.md) | <span data-ttu-id="52d49-164">F serisi</span><span class="sxs-lookup"><span data-stu-id="52d49-164">F series</span></span> | <span data-ttu-id="52d49-165">32</span><span class="sxs-lookup"><span data-stu-id="52d49-165">32</span></span> |
| [<span data-ttu-id="52d49-166">Bellek için iyileştirilmiş</span><span class="sxs-lookup"><span data-stu-id="52d49-166">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md) | <span data-ttu-id="52d49-167">D ve G serisi</span><span class="sxs-lookup"><span data-stu-id="52d49-167">D and G series</span></span> | <span data-ttu-id="52d49-168">64</span><span class="sxs-lookup"><span data-stu-id="52d49-168">64</span></span> |
| [<span data-ttu-id="52d49-169">Depolama için iyileştirilmiş</span><span class="sxs-lookup"><span data-stu-id="52d49-169">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md) | <span data-ttu-id="52d49-170">L serisi</span><span class="sxs-lookup"><span data-stu-id="52d49-170">L series</span></span> | <span data-ttu-id="52d49-171">64</span><span class="sxs-lookup"><span data-stu-id="52d49-171">64</span></span> |
| [<span data-ttu-id="52d49-172">GPU</span><span class="sxs-lookup"><span data-stu-id="52d49-172">GPU</span></span>](sizes-gpu.md) | <span data-ttu-id="52d49-173">N serisi</span><span class="sxs-lookup"><span data-stu-id="52d49-173">N series</span></span> | <span data-ttu-id="52d49-174">48</span><span class="sxs-lookup"><span data-stu-id="52d49-174">48</span></span> |
| [<span data-ttu-id="52d49-175">Yüksek performans</span><span class="sxs-lookup"><span data-stu-id="52d49-175">High performance</span></span>](sizes-hpc.md) | <span data-ttu-id="52d49-176">A ve H serisi</span><span class="sxs-lookup"><span data-stu-id="52d49-176">A and H series</span></span> | <span data-ttu-id="52d49-177">32</span><span class="sxs-lookup"><span data-stu-id="52d49-177">32</span></span> |

## <a name="vm-disk-types"></a><span data-ttu-id="52d49-178">VM disk türleri</span><span class="sxs-lookup"><span data-stu-id="52d49-178">VM disk types</span></span>

<span data-ttu-id="52d49-179">Azure disk iki tür sağlar.</span><span class="sxs-lookup"><span data-stu-id="52d49-179">Azure provides two types of disk.</span></span>

### <a name="standard-disk"></a><span data-ttu-id="52d49-180">Standart disk</span><span class="sxs-lookup"><span data-stu-id="52d49-180">Standard disk</span></span>

<span data-ttu-id="52d49-181">Standart Depolama, HDD’ler ile desteklenir ve yüksek performans sunarken uygun maliyetli depolama sağlar.</span><span class="sxs-lookup"><span data-stu-id="52d49-181">Standard Storage is backed by HDDs, and delivers cost-effective storage while still being performant.</span></span> <span data-ttu-id="52d49-182">Standart diskler için uygun maliyetli geliştirme idealdir ve iş yükü test.</span><span class="sxs-lookup"><span data-stu-id="52d49-182">Standard disks are ideal for a cost effective dev and test workload.</span></span>

### <a name="premium-disk"></a><span data-ttu-id="52d49-183">Premium disk</span><span class="sxs-lookup"><span data-stu-id="52d49-183">Premium disk</span></span>

<span data-ttu-id="52d49-184">Premium diskler, SSD tabanlı yüksek performanslı, düşük gecikme süreli disk tarafından desteklenir.</span><span class="sxs-lookup"><span data-stu-id="52d49-184">Premium disks are backed by SSD-based high-performance, low-latency disk.</span></span> <span data-ttu-id="52d49-185">Üretim iş yükü çalıştıran VM'ler için mükemmel.</span><span class="sxs-lookup"><span data-stu-id="52d49-185">Perfect for VMs running production workload.</span></span> <span data-ttu-id="52d49-186">Premium depolama destekleyen DS serisi, DSv2 serisi, GS serisi ve FS-serisi VM'ler.</span><span class="sxs-lookup"><span data-stu-id="52d49-186">Premium Storage supports DS-series, DSv2-series, GS-series, and FS-series VMs.</span></span> <span data-ttu-id="52d49-187">Üç tür (P10, P20, P30) Premium diskleri gelir, disk türü disk boyutunu belirler.</span><span class="sxs-lookup"><span data-stu-id="52d49-187">Premium disks come in three types (P10, P20, P30), the size of the disk determines the disk type.</span></span> <span data-ttu-id="52d49-188">Disk boyutu değeri seçerken, sonraki türü yuvarlanır.</span><span class="sxs-lookup"><span data-stu-id="52d49-188">When selecting, a disk size the value is rounded up to the next type.</span></span> <span data-ttu-id="52d49-189">128 GB boyutu ise, örneğin, disk türünü P10, 129 ve 512 P20 ve üzerinde 512 P30 arasında olacaktır.</span><span class="sxs-lookup"><span data-stu-id="52d49-189">For example, if the size is below 128 GB the disk type will be P10, between 129 and 512 P20, and over 512 P30.</span></span> 

### <a name="premium-disk-performance"></a><span data-ttu-id="52d49-190">Premium disk performansı</span><span class="sxs-lookup"><span data-stu-id="52d49-190">Premium disk performance</span></span>

|<span data-ttu-id="52d49-191">Premium depolama disk türü</span><span class="sxs-lookup"><span data-stu-id="52d49-191">Premium storage disk type</span></span> | <span data-ttu-id="52d49-192">P10</span><span class="sxs-lookup"><span data-stu-id="52d49-192">P10</span></span> | <span data-ttu-id="52d49-193">P20</span><span class="sxs-lookup"><span data-stu-id="52d49-193">P20</span></span> | <span data-ttu-id="52d49-194">P30</span><span class="sxs-lookup"><span data-stu-id="52d49-194">P30</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="52d49-195">Disk boyutu (yukarı yuvarlar)</span><span class="sxs-lookup"><span data-stu-id="52d49-195">Disk size (round up)</span></span> | <span data-ttu-id="52d49-196">128 GB</span><span class="sxs-lookup"><span data-stu-id="52d49-196">128 GB</span></span> | <span data-ttu-id="52d49-197">512 GB</span><span class="sxs-lookup"><span data-stu-id="52d49-197">512 GB</span></span> | <span data-ttu-id="52d49-198">1.024 GB (1 TB)</span><span class="sxs-lookup"><span data-stu-id="52d49-198">1,024 GB (1 TB)</span></span> |
| <span data-ttu-id="52d49-199">Disk başına IOPS</span><span class="sxs-lookup"><span data-stu-id="52d49-199">IOPS per disk</span></span> | <span data-ttu-id="52d49-200">500</span><span class="sxs-lookup"><span data-stu-id="52d49-200">500</span></span> | <span data-ttu-id="52d49-201">2,300</span><span class="sxs-lookup"><span data-stu-id="52d49-201">2,300</span></span> | <span data-ttu-id="52d49-202">5,000</span><span class="sxs-lookup"><span data-stu-id="52d49-202">5,000</span></span> |
<span data-ttu-id="52d49-203">Disk başına aktarım hızı</span><span class="sxs-lookup"><span data-stu-id="52d49-203">Throughput per disk</span></span> | <span data-ttu-id="52d49-204">100 MB/s</span><span class="sxs-lookup"><span data-stu-id="52d49-204">100 MB/s</span></span> | <span data-ttu-id="52d49-205">150 MB/s</span><span class="sxs-lookup"><span data-stu-id="52d49-205">150 MB/s</span></span> | <span data-ttu-id="52d49-206">200 MB/sn</span><span class="sxs-lookup"><span data-stu-id="52d49-206">200 MB/s</span></span> |

<span data-ttu-id="52d49-207">Yukarıdaki tabloda, disk başına maksimum IOPS tanımlanmaktadır olsa da, daha yüksek düzeyde performans birden çok veri diskleri bölümlemesine tarafından elde edilebilir.</span><span class="sxs-lookup"><span data-stu-id="52d49-207">While the above table identifies max IOPS per disk, a higher level of performance can be achieved by striping multiple data disks.</span></span> <span data-ttu-id="52d49-208">Örneğin, 64 veri diskleri Standard_GS5 VM eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="52d49-208">For instance, 64 data disks can be attached to Standard_GS5 VM.</span></span> <span data-ttu-id="52d49-209">Her bu disklerin P30 boyuta sahip değilse, en fazla 80.000 IOPS elde edilebilir.</span><span class="sxs-lookup"><span data-stu-id="52d49-209">If each of these disks are sized as a P30, a maximum of 80,000 IOPS can be achieved.</span></span> <span data-ttu-id="52d49-210">VM başına maksimum IOPS hakkında ayrıntılı bilgi için bkz: [Linux VM boyutları](./sizes.md).</span><span class="sxs-lookup"><span data-stu-id="52d49-210">For detailed information on max IOPS per VM, see [Linux VM sizes](./sizes.md).</span></span>

## <a name="create-and-attach-disks"></a><span data-ttu-id="52d49-211">Oluşturma ve diskleri ekleme</span><span class="sxs-lookup"><span data-stu-id="52d49-211">Create and attach disks</span></span>

<span data-ttu-id="52d49-212">Örneğin bu öğreticiyi tamamlamak için var olan bir sanal makine olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="52d49-212">To complete the example in this tutorial, you must have an existing virtual machine.</span></span> <span data-ttu-id="52d49-213">Gerekirse, bu [komut dosyası örneği](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) sizin için bir tane oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="52d49-213">If needed, this [script sample](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) can create one for you.</span></span> <span data-ttu-id="52d49-214">Çalışma öğretici aracılığıyla değiştirdiğinizde VM ve kaynak grubu adları gerektiğinde.</span><span class="sxs-lookup"><span data-stu-id="52d49-214">When working through the tutorial, replace the resource group and VM names where needed.</span></span>

<span data-ttu-id="52d49-215">İlk yapılandırma ile oluşturmayı [yeni AzureRmDiskConfig](/powershell/module/azurerm.compute/new-azurermdiskconfig).</span><span class="sxs-lookup"><span data-stu-id="52d49-215">Create the initial configuration with [New-AzureRmDiskConfig](/powershell/module/azurerm.compute/new-azurermdiskconfig).</span></span> <span data-ttu-id="52d49-216">Aşağıdaki örnek boyutu 128 gigabayt bir disk yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="52d49-216">The following example configures a disk that is 128 gigabytes in size.</span></span>

```powershell
$diskConfig = New-AzureRmDiskConfig -Location EastUS -CreateOption Empty -DiskSizeGB 128
```

<span data-ttu-id="52d49-217">Sahip veri diski oluşturma [yeni AzureRmDisk](/powershell/module/azurerm.compute/new-azurermdisk) komutu.</span><span class="sxs-lookup"><span data-stu-id="52d49-217">Create the data disk with the [New-AzureRmDisk](/powershell/module/azurerm.compute/new-azurermdisk) command.</span></span>

```powershell
$dataDisk = New-AzureRmDisk -ResourceGroupName myResourceGroup -DiskName myDataDisk -Disk $diskConfig
```

<span data-ttu-id="52d49-218">İle verileri diske eklemek istediğiniz sanal makine Al [Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) komutu.</span><span class="sxs-lookup"><span data-stu-id="52d49-218">Get the virtual machine that you want to add the data disk to with the [Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) command.</span></span>

```powershell
$vm = Get-AzureRmVM -ResourceGroupName myResourceGroup -Name myVM
```

<span data-ttu-id="52d49-219">Sanal makine yapılandırması için veri diski Ekle [Ekle AzureRmVMDataDisk](/powershell/module/azurerm.compute/add-azurermvmdatadisk) komutu.</span><span class="sxs-lookup"><span data-stu-id="52d49-219">Add the data disk to the virtual machine configuration with the [Add-AzureRmVMDataDisk](/powershell/module/azurerm.compute/add-azurermvmdatadisk) command.</span></span>

```powershell
$vm = Add-AzureRmVMDataDisk -VM $vm -Name myDataDisk -CreateOption Attach -ManagedDiskId $dataDisk.Id -Lun 1
```

<span data-ttu-id="52d49-220">Sanal makineyle güncelleştirme [güncelleştirme-AzureRmVM](/powershell/module/azurerm.compute/add-azurermvmdatadisk) komutu.</span><span class="sxs-lookup"><span data-stu-id="52d49-220">Update the virtual machine with the [Update-AzureRmVM](/powershell/module/azurerm.compute/add-azurermvmdatadisk) command.</span></span>

```powershell
Update-AzureRmVM -ResourceGroupName myResourceGroup -VM $vm
```

## <a name="prepare-data-disks"></a><span data-ttu-id="52d49-221">Veri diskleri hazırlama</span><span class="sxs-lookup"><span data-stu-id="52d49-221">Prepare data disks</span></span>

<span data-ttu-id="52d49-222">Bir disk sanal makineye bağlandıktan sonra işletim sistemi diski kullanacak şekilde yapılandırılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="52d49-222">Once a disk has been attached to the virtual machine, the operating system needs to be configured to use the disk.</span></span> <span data-ttu-id="52d49-223">Aşağıdaki örnek VM eklenen ilk diski el ile yapılandırmak nasıl gösterir.</span><span class="sxs-lookup"><span data-stu-id="52d49-223">The following example shows how to manually configure the first disk added to the VM.</span></span> <span data-ttu-id="52d49-224">Bu işlem ayrıca kullanarak otomatikleştirilebilir [özel betik uzantısı](./tutorial-automate-vm-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="52d49-224">This process can also be automated using the [custom script extension](./tutorial-automate-vm-deployment.md).</span></span>

### <a name="manual-configuration"></a><span data-ttu-id="52d49-225">El ile yapılandırma</span><span class="sxs-lookup"><span data-stu-id="52d49-225">Manual configuration</span></span>

<span data-ttu-id="52d49-226">RDP bağlantısı ile sanal makine oluşturun.</span><span class="sxs-lookup"><span data-stu-id="52d49-226">Create an RDP connection with the virtual machine.</span></span> <span data-ttu-id="52d49-227">PowerShell'i açın ve bu komut dosyasını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="52d49-227">Open up PowerShell and run this script.</span></span>

```powershell
Get-Disk | Where partitionstyle -eq 'raw' | `
Initialize-Disk -PartitionStyle MBR -PassThru | `
New-Partition -AssignDriveLetter -UseMaximumSize | `
Format-Volume -FileSystem NTFS -NewFileSystemLabel "myDataDisk" -Confirm:$false
```

## <a name="next-steps"></a><span data-ttu-id="52d49-228">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="52d49-228">Next steps</span></span>

<span data-ttu-id="52d49-229">Bu öğreticide, VM diskleri konuları hakkında gibi öğrenilen:</span><span class="sxs-lookup"><span data-stu-id="52d49-229">In this tutorial, you learned about VM disks topics such as:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="52d49-230">İşletim sistemi ve geçici disklerle</span><span class="sxs-lookup"><span data-stu-id="52d49-230">OS disks and temporary disks</span></span>
> * <span data-ttu-id="52d49-231">Veri diskleri</span><span class="sxs-lookup"><span data-stu-id="52d49-231">Data disks</span></span>
> * <span data-ttu-id="52d49-232">Standart ve Premium diskleri</span><span class="sxs-lookup"><span data-stu-id="52d49-232">Standard and Premium disks</span></span>
> * <span data-ttu-id="52d49-233">Disk performansı</span><span class="sxs-lookup"><span data-stu-id="52d49-233">Disk performance</span></span>
> * <span data-ttu-id="52d49-234">Ekleme ve veri diskleri hazırlama</span><span class="sxs-lookup"><span data-stu-id="52d49-234">Attaching and preparing data disks</span></span>

<span data-ttu-id="52d49-235">VM yapılandırması otomatikleştirme hakkında bilgi edinmek için sonraki öğretici ilerleyin.</span><span class="sxs-lookup"><span data-stu-id="52d49-235">Advance to the next tutorial to learn about automating VM configuration.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="52d49-236">VM yapılandırmasını otomatikleştirme</span><span class="sxs-lookup"><span data-stu-id="52d49-236">Automate VM configuration</span></span>](./tutorial-automate-vm-deployment.md)
