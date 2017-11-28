---
title: aaaManage Azure diskleri hello Azure PowerShell ile | Microsoft Docs
description: "Öğretici - Azure diskleri hello Azure PowerShell ile yönetme"
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
ms.openlocfilehash: 2f61ad18bc94bab527d7ae593da603c6073adc89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-disks-with-powershell"></a><span data-ttu-id="272c3-103">PowerShell ile Azure diskleri yönetme</span><span class="sxs-lookup"><span data-stu-id="272c3-103">Manage Azure disks with PowerShell</span></span>

<span data-ttu-id="272c3-104">Azure sanal makineleri diskleri toostore hello VM'ler işletim sistemi, uygulamaları ve verileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="272c3-104">Azure virtual machines use disks toostore hello VMs operating system, applications, and data.</span></span> <span data-ttu-id="272c3-105">Bir VM oluştururken önemli toochoose disk boyutu ve yapılandırma beklenen uygun toohello iş yüküne bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="272c3-105">When creating a VM it is important toochoose a disk size and configuration appropriate toohello expected workload.</span></span> <span data-ttu-id="272c3-106">Bu öğretici, dağıtma ve VM diskleri yönetme kapsar.</span><span class="sxs-lookup"><span data-stu-id="272c3-106">This tutorial covers deploying and managing VM disks.</span></span> <span data-ttu-id="272c3-107">Hakkında bilgi edinin:</span><span class="sxs-lookup"><span data-stu-id="272c3-107">You learn about:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="272c3-108">İşletim sistemi ve geçici disklerle</span><span class="sxs-lookup"><span data-stu-id="272c3-108">OS disks and temporary disks</span></span>
> * <span data-ttu-id="272c3-109">Veri diskleri</span><span class="sxs-lookup"><span data-stu-id="272c3-109">Data disks</span></span>
> * <span data-ttu-id="272c3-110">Standart ve Premium diskleri</span><span class="sxs-lookup"><span data-stu-id="272c3-110">Standard and Premium disks</span></span>
> * <span data-ttu-id="272c3-111">Disk performansı</span><span class="sxs-lookup"><span data-stu-id="272c3-111">Disk performance</span></span>
> * <span data-ttu-id="272c3-112">Ekleme ve veri diskleri hazırlama</span><span class="sxs-lookup"><span data-stu-id="272c3-112">Attaching and preparing data disks</span></span>

<span data-ttu-id="272c3-113">Bu öğretici hello Azure PowerShell modülü 3,6 veya sonraki bir sürümü gerektiriyor.</span><span class="sxs-lookup"><span data-stu-id="272c3-113">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="272c3-114">Çalıştırma ` Get-Module -ListAvailable AzureRM` toofind hello sürümü.</span><span class="sxs-lookup"><span data-stu-id="272c3-114">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="272c3-115">Tooupgrade gerekirse bkz [yükleme Azure PowerShell Modülü](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="272c3-115">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="default-azure-disks"></a><span data-ttu-id="272c3-116">Azure diskleri varsayılan</span><span class="sxs-lookup"><span data-stu-id="272c3-116">Default Azure disks</span></span>

<span data-ttu-id="272c3-117">Bir Azure sanal makine oluşturulduğunda, iki diskleri otomatik olarak eklenen toohello sanal makine içindir.</span><span class="sxs-lookup"><span data-stu-id="272c3-117">When an Azure virtual machine is created, two disks are automatically attached toohello virtual machine.</span></span> 

<span data-ttu-id="272c3-118">**İşletim sistemi diski** - işletim sistemi disklerinde too1 terabayt boyutta ve ana hello VM'ler işletim sistemi.</span><span class="sxs-lookup"><span data-stu-id="272c3-118">**Operating system disk** - Operating system disks can be sized up too1 terabyte, and hosts hello VMs operating system.</span></span>  <span data-ttu-id="272c3-119">Merhaba işletim sistemi diski bir sürücü harfi atanmış *c:* varsayılan olarak.</span><span class="sxs-lookup"><span data-stu-id="272c3-119">hello OS disk is assigned a drive letter of *c:* by default.</span></span> <span data-ttu-id="272c3-120">Merhaba işletim sistemi disk yapılandırması önbelleğe alma hello disk işletim sistemi performans için optimize edilmiştir.</span><span class="sxs-lookup"><span data-stu-id="272c3-120">hello disk caching configuration of hello OS disk is optimized for OS performance.</span></span> <span data-ttu-id="272c3-121">Merhaba işletim sistemi disk **vermemelisiniz** konak uygulamalar veya veri.</span><span class="sxs-lookup"><span data-stu-id="272c3-121">hello OS disk **should not** host applications or data.</span></span> <span data-ttu-id="272c3-122">Uygulamalar ve veriler için bu makalenin sonraki bölümlerinde ayrıntılı bir veri diski kullanın.</span><span class="sxs-lookup"><span data-stu-id="272c3-122">For applications and data, use a data disk, which is detailed later in this article.</span></span>

<span data-ttu-id="272c3-123">**Geçici disk** -geçici diskler hello üzerinde bulunan bir katı hal sürücüsü kullanan aynı Azure ana bilgisayar hello VM olarak.</span><span class="sxs-lookup"><span data-stu-id="272c3-123">**Temporary disk** - Temporary disks use a solid-state drive that is located on hello same Azure host as hello VM.</span></span> <span data-ttu-id="272c3-124">Temp disklerinin yüksek oranda kullanıcı durumda ve geçici veri işleme gibi işlemler için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="272c3-124">Temp disks are highly performant and may be used for operations such as temporary data processing.</span></span> <span data-ttu-id="272c3-125">Ancak, Hello VM taşınan tooa yeni ana bilgisayar ise, geçici bir diskte depolanan tüm verileri kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="272c3-125">However, if hello VM is moved tooa new host, any data stored on a temporary disk is removed.</span></span> <span data-ttu-id="272c3-126">Merhaba hello geçici disk boyutunu hello VM boyutu tarafından belirlenir.</span><span class="sxs-lookup"><span data-stu-id="272c3-126">hello size of hello temporary disk is determined by hello VM size.</span></span> <span data-ttu-id="272c3-127">Geçici diskleri bir sürücü harfi atanmış *d:* varsayılan olarak.</span><span class="sxs-lookup"><span data-stu-id="272c3-127">Temporary disks are assigned a drive letter of *d:* by default.</span></span>

### <a name="temporary-disk-sizes"></a><span data-ttu-id="272c3-128">Geçici disk boyutları</span><span class="sxs-lookup"><span data-stu-id="272c3-128">Temporary disk sizes</span></span>

| <span data-ttu-id="272c3-129">Tür</span><span class="sxs-lookup"><span data-stu-id="272c3-129">Type</span></span> | <span data-ttu-id="272c3-130">VM boyutu</span><span class="sxs-lookup"><span data-stu-id="272c3-130">VM Size</span></span> | <span data-ttu-id="272c3-131">En büyük geçici disk boyutu (GB)</span><span class="sxs-lookup"><span data-stu-id="272c3-131">Max temp disk size (GB)</span></span> |
|----|----|----|
| [<span data-ttu-id="272c3-132">Genel amaçlı</span><span class="sxs-lookup"><span data-stu-id="272c3-132">General purpose</span></span>](sizes-general.md) | <span data-ttu-id="272c3-133">A ve D serisi</span><span class="sxs-lookup"><span data-stu-id="272c3-133">A and D series</span></span> | <span data-ttu-id="272c3-134">800</span><span class="sxs-lookup"><span data-stu-id="272c3-134">800</span></span> |
| [<span data-ttu-id="272c3-135">İşlem için iyileştirilmiş</span><span class="sxs-lookup"><span data-stu-id="272c3-135">Compute optimized</span></span>](sizes-compute.md) | <span data-ttu-id="272c3-136">F serisi</span><span class="sxs-lookup"><span data-stu-id="272c3-136">F series</span></span> | <span data-ttu-id="272c3-137">800</span><span class="sxs-lookup"><span data-stu-id="272c3-137">800</span></span> |
| [<span data-ttu-id="272c3-138">Bellek için iyileştirilmiş</span><span class="sxs-lookup"><span data-stu-id="272c3-138">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md) | <span data-ttu-id="272c3-139">D ve G serisi</span><span class="sxs-lookup"><span data-stu-id="272c3-139">D and G series</span></span> | <span data-ttu-id="272c3-140">6144</span><span class="sxs-lookup"><span data-stu-id="272c3-140">6144</span></span> |
| [<span data-ttu-id="272c3-141">Depolama için iyileştirilmiş</span><span class="sxs-lookup"><span data-stu-id="272c3-141">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md) | <span data-ttu-id="272c3-142">L serisi</span><span class="sxs-lookup"><span data-stu-id="272c3-142">L series</span></span> | <span data-ttu-id="272c3-143">5630</span><span class="sxs-lookup"><span data-stu-id="272c3-143">5630</span></span> |
| [<span data-ttu-id="272c3-144">GPU</span><span class="sxs-lookup"><span data-stu-id="272c3-144">GPU</span></span>](sizes-gpu.md) | <span data-ttu-id="272c3-145">N serisi</span><span class="sxs-lookup"><span data-stu-id="272c3-145">N series</span></span> | <span data-ttu-id="272c3-146">1440</span><span class="sxs-lookup"><span data-stu-id="272c3-146">1440</span></span> |
| [<span data-ttu-id="272c3-147">Yüksek performans</span><span class="sxs-lookup"><span data-stu-id="272c3-147">High performance</span></span>](sizes-hpc.md) | <span data-ttu-id="272c3-148">A ve H serisi</span><span class="sxs-lookup"><span data-stu-id="272c3-148">A and H series</span></span> | <span data-ttu-id="272c3-149">2000</span><span class="sxs-lookup"><span data-stu-id="272c3-149">2000</span></span> |

## <a name="azure-data-disks"></a><span data-ttu-id="272c3-150">Azure veri diski</span><span class="sxs-lookup"><span data-stu-id="272c3-150">Azure data disks</span></span>

<span data-ttu-id="272c3-151">Uygulama yükleme ve verilerini depolamak için ek veri disklerinin eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="272c3-151">Additional data disks can be added for installing applications and storing data.</span></span> <span data-ttu-id="272c3-152">Veri diskleri sağlam ve esnek veri depolama burada istenen herhangi bir durumda kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="272c3-152">Data disks should be used in any situation where durable and responsive data storage is desired.</span></span> <span data-ttu-id="272c3-153">Her veri diski 1 terabayttan küçük maksimum kapasitesine sahiptir.</span><span class="sxs-lookup"><span data-stu-id="272c3-153">Each data disk has a maximum capacity of 1 terabyte.</span></span> <span data-ttu-id="272c3-154">kaç tane veri diskleri ekli tooa VM olabilir hello sanal makine Hello boyutunu belirler.</span><span class="sxs-lookup"><span data-stu-id="272c3-154">hello size of hello virtual machine determines how many data disks can be attached tooa VM.</span></span> <span data-ttu-id="272c3-155">Her VM çekirdek için iki veri diskleri eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="272c3-155">For each VM core, two data disks can be attached.</span></span> 

### <a name="max-data-disks-per-vm"></a><span data-ttu-id="272c3-156">VM başına en fazla veri diski</span><span class="sxs-lookup"><span data-stu-id="272c3-156">Max data disks per VM</span></span>

| <span data-ttu-id="272c3-157">Tür</span><span class="sxs-lookup"><span data-stu-id="272c3-157">Type</span></span> | <span data-ttu-id="272c3-158">VM boyutu</span><span class="sxs-lookup"><span data-stu-id="272c3-158">VM Size</span></span> | <span data-ttu-id="272c3-159">VM başına en fazla veri diski</span><span class="sxs-lookup"><span data-stu-id="272c3-159">Max data disks per VM</span></span> |
|----|----|----|
| [<span data-ttu-id="272c3-160">Genel amaçlı</span><span class="sxs-lookup"><span data-stu-id="272c3-160">General purpose</span></span>](sizes-general.md) | <span data-ttu-id="272c3-161">A ve D serisi</span><span class="sxs-lookup"><span data-stu-id="272c3-161">A and D series</span></span> | <span data-ttu-id="272c3-162">32</span><span class="sxs-lookup"><span data-stu-id="272c3-162">32</span></span> |
| [<span data-ttu-id="272c3-163">İşlem için iyileştirilmiş</span><span class="sxs-lookup"><span data-stu-id="272c3-163">Compute optimized</span></span>](sizes-compute.md) | <span data-ttu-id="272c3-164">F serisi</span><span class="sxs-lookup"><span data-stu-id="272c3-164">F series</span></span> | <span data-ttu-id="272c3-165">32</span><span class="sxs-lookup"><span data-stu-id="272c3-165">32</span></span> |
| [<span data-ttu-id="272c3-166">Bellek için iyileştirilmiş</span><span class="sxs-lookup"><span data-stu-id="272c3-166">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md) | <span data-ttu-id="272c3-167">D ve G serisi</span><span class="sxs-lookup"><span data-stu-id="272c3-167">D and G series</span></span> | <span data-ttu-id="272c3-168">64</span><span class="sxs-lookup"><span data-stu-id="272c3-168">64</span></span> |
| [<span data-ttu-id="272c3-169">Depolama için iyileştirilmiş</span><span class="sxs-lookup"><span data-stu-id="272c3-169">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md) | <span data-ttu-id="272c3-170">L serisi</span><span class="sxs-lookup"><span data-stu-id="272c3-170">L series</span></span> | <span data-ttu-id="272c3-171">64</span><span class="sxs-lookup"><span data-stu-id="272c3-171">64</span></span> |
| [<span data-ttu-id="272c3-172">GPU</span><span class="sxs-lookup"><span data-stu-id="272c3-172">GPU</span></span>](sizes-gpu.md) | <span data-ttu-id="272c3-173">N serisi</span><span class="sxs-lookup"><span data-stu-id="272c3-173">N series</span></span> | <span data-ttu-id="272c3-174">48</span><span class="sxs-lookup"><span data-stu-id="272c3-174">48</span></span> |
| [<span data-ttu-id="272c3-175">Yüksek performans</span><span class="sxs-lookup"><span data-stu-id="272c3-175">High performance</span></span>](sizes-hpc.md) | <span data-ttu-id="272c3-176">A ve H serisi</span><span class="sxs-lookup"><span data-stu-id="272c3-176">A and H series</span></span> | <span data-ttu-id="272c3-177">32</span><span class="sxs-lookup"><span data-stu-id="272c3-177">32</span></span> |

## <a name="vm-disk-types"></a><span data-ttu-id="272c3-178">VM disk türleri</span><span class="sxs-lookup"><span data-stu-id="272c3-178">VM disk types</span></span>

<span data-ttu-id="272c3-179">Azure disk iki tür sağlar.</span><span class="sxs-lookup"><span data-stu-id="272c3-179">Azure provides two types of disk.</span></span>

### <a name="standard-disk"></a><span data-ttu-id="272c3-180">Standart disk</span><span class="sxs-lookup"><span data-stu-id="272c3-180">Standard disk</span></span>

<span data-ttu-id="272c3-181">Standart Depolama, HDD’ler ile desteklenir ve yüksek performans sunarken uygun maliyetli depolama sağlar.</span><span class="sxs-lookup"><span data-stu-id="272c3-181">Standard Storage is backed by HDDs, and delivers cost-effective storage while still being performant.</span></span> <span data-ttu-id="272c3-182">Standart diskler için uygun maliyetli geliştirme idealdir ve iş yükü test.</span><span class="sxs-lookup"><span data-stu-id="272c3-182">Standard disks are ideal for a cost effective dev and test workload.</span></span>

### <a name="premium-disk"></a><span data-ttu-id="272c3-183">Premium disk</span><span class="sxs-lookup"><span data-stu-id="272c3-183">Premium disk</span></span>

<span data-ttu-id="272c3-184">Premium diskler, SSD tabanlı yüksek performanslı, düşük gecikme süreli disk tarafından desteklenir.</span><span class="sxs-lookup"><span data-stu-id="272c3-184">Premium disks are backed by SSD-based high-performance, low-latency disk.</span></span> <span data-ttu-id="272c3-185">Üretim iş yükü çalıştıran VM'ler için mükemmel.</span><span class="sxs-lookup"><span data-stu-id="272c3-185">Perfect for VMs running production workload.</span></span> <span data-ttu-id="272c3-186">Premium depolama destekleyen DS serisi, DSv2 serisi, GS serisi ve FS-serisi VM'ler.</span><span class="sxs-lookup"><span data-stu-id="272c3-186">Premium Storage supports DS-series, DSv2-series, GS-series, and FS-series VMs.</span></span> <span data-ttu-id="272c3-187">Üç tür (P10, P20, P30) Premium diskleri gelir, hello disk türü hello hello diskin boyutunu belirler.</span><span class="sxs-lookup"><span data-stu-id="272c3-187">Premium disks come in three types (P10, P20, P30), hello size of hello disk determines hello disk type.</span></span> <span data-ttu-id="272c3-188">Seçerken, bir disk boyutu hello değeri toohello sonraki türü yuvarlanır.</span><span class="sxs-lookup"><span data-stu-id="272c3-188">When selecting, a disk size hello value is rounded up toohello next type.</span></span> <span data-ttu-id="272c3-189">Örneğin, Hello boyutu 128 GB hello disk türü ise P10, 129 ve 512 P20 ve üzerinde 512 P30 arasında olacaktır.</span><span class="sxs-lookup"><span data-stu-id="272c3-189">For example, if hello size is below 128 GB hello disk type will be P10, between 129 and 512 P20, and over 512 P30.</span></span> 

### <a name="premium-disk-performance"></a><span data-ttu-id="272c3-190">Premium disk performansı</span><span class="sxs-lookup"><span data-stu-id="272c3-190">Premium disk performance</span></span>

|<span data-ttu-id="272c3-191">Premium depolama disk türü</span><span class="sxs-lookup"><span data-stu-id="272c3-191">Premium storage disk type</span></span> | <span data-ttu-id="272c3-192">P10</span><span class="sxs-lookup"><span data-stu-id="272c3-192">P10</span></span> | <span data-ttu-id="272c3-193">P20</span><span class="sxs-lookup"><span data-stu-id="272c3-193">P20</span></span> | <span data-ttu-id="272c3-194">P30</span><span class="sxs-lookup"><span data-stu-id="272c3-194">P30</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="272c3-195">Disk boyutu (yukarı yuvarlar)</span><span class="sxs-lookup"><span data-stu-id="272c3-195">Disk size (round up)</span></span> | <span data-ttu-id="272c3-196">128 GB</span><span class="sxs-lookup"><span data-stu-id="272c3-196">128 GB</span></span> | <span data-ttu-id="272c3-197">512 GB</span><span class="sxs-lookup"><span data-stu-id="272c3-197">512 GB</span></span> | <span data-ttu-id="272c3-198">1.024 GB (1 TB)</span><span class="sxs-lookup"><span data-stu-id="272c3-198">1,024 GB (1 TB)</span></span> |
| <span data-ttu-id="272c3-199">Disk başına IOPS</span><span class="sxs-lookup"><span data-stu-id="272c3-199">IOPS per disk</span></span> | <span data-ttu-id="272c3-200">500</span><span class="sxs-lookup"><span data-stu-id="272c3-200">500</span></span> | <span data-ttu-id="272c3-201">2,300</span><span class="sxs-lookup"><span data-stu-id="272c3-201">2,300</span></span> | <span data-ttu-id="272c3-202">5,000</span><span class="sxs-lookup"><span data-stu-id="272c3-202">5,000</span></span> |
<span data-ttu-id="272c3-203">Disk başına aktarım hızı</span><span class="sxs-lookup"><span data-stu-id="272c3-203">Throughput per disk</span></span> | <span data-ttu-id="272c3-204">100 MB/s</span><span class="sxs-lookup"><span data-stu-id="272c3-204">100 MB/s</span></span> | <span data-ttu-id="272c3-205">150 MB/s</span><span class="sxs-lookup"><span data-stu-id="272c3-205">150 MB/s</span></span> | <span data-ttu-id="272c3-206">200 MB/sn</span><span class="sxs-lookup"><span data-stu-id="272c3-206">200 MB/s</span></span> |

<span data-ttu-id="272c3-207">Disk başına maksimum IOPS Merhaba tablonun yukarısındaki tanımlayan olsa da, daha yüksek düzeyde performans birden çok veri diskleri bölümlemesine tarafından elde edilebilir.</span><span class="sxs-lookup"><span data-stu-id="272c3-207">While hello above table identifies max IOPS per disk, a higher level of performance can be achieved by striping multiple data disks.</span></span> <span data-ttu-id="272c3-208">Örneğin, 64 veri diskleri olabilir tooStandard_GS5 VM bağlı.</span><span class="sxs-lookup"><span data-stu-id="272c3-208">For instance, 64 data disks can be attached tooStandard_GS5 VM.</span></span> <span data-ttu-id="272c3-209">Her bu disklerin P30 boyuta sahip değilse, en fazla 80.000 IOPS elde edilebilir.</span><span class="sxs-lookup"><span data-stu-id="272c3-209">If each of these disks are sized as a P30, a maximum of 80,000 IOPS can be achieved.</span></span> <span data-ttu-id="272c3-210">VM başına maksimum IOPS hakkında ayrıntılı bilgi için bkz: [Linux VM boyutları](./sizes.md).</span><span class="sxs-lookup"><span data-stu-id="272c3-210">For detailed information on max IOPS per VM, see [Linux VM sizes](./sizes.md).</span></span>

## <a name="create-and-attach-disks"></a><span data-ttu-id="272c3-211">Oluşturma ve diskleri ekleme</span><span class="sxs-lookup"><span data-stu-id="272c3-211">Create and attach disks</span></span>

<span data-ttu-id="272c3-212">Bu öğreticide toocomplete hello örnek, mevcut bir sanal makine olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="272c3-212">toocomplete hello example in this tutorial, you must have an existing virtual machine.</span></span> <span data-ttu-id="272c3-213">Gerekirse, bu [komut dosyası örneği](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) sizin için bir tane oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="272c3-213">If needed, this [script sample](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) can create one for you.</span></span> <span data-ttu-id="272c3-214">Çalışma hello öğretici aracılığıyla değiştirdiğinizde hello kaynak grubu VM adları ve gerektiğinde.</span><span class="sxs-lookup"><span data-stu-id="272c3-214">When working through hello tutorial, replace hello resource group and VM names where needed.</span></span>

<span data-ttu-id="272c3-215">Merhaba ilk yapılandırma ile oluşturmayı [yeni AzureRmDiskConfig](/powershell/module/azurerm.compute/new-azurermdiskconfig).</span><span class="sxs-lookup"><span data-stu-id="272c3-215">Create hello initial configuration with [New-AzureRmDiskConfig](/powershell/module/azurerm.compute/new-azurermdiskconfig).</span></span> <span data-ttu-id="272c3-216">Aşağıdaki örnek hello 128 gigabayt cinsinden boyutu olan bir disk yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="272c3-216">hello following example configures a disk that is 128 gigabytes in size.</span></span>

```powershell
$diskConfig = New-AzureRmDiskConfig -Location EastUS -CreateOption Empty -DiskSizeGB 128
```

<span data-ttu-id="272c3-217">Merhaba ile Merhaba veri diski oluşturma [yeni AzureRmDisk](/powershell/module/azurerm.compute/new-azurermdisk) komutu.</span><span class="sxs-lookup"><span data-stu-id="272c3-217">Create hello data disk with hello [New-AzureRmDisk](/powershell/module/azurerm.compute/new-azurermdisk) command.</span></span>

```powershell
$dataDisk = New-AzureRmDisk -ResourceGroupName myResourceGroup -DiskName myDataDisk -Disk $diskConfig
```

<span data-ttu-id="272c3-218">Tooadd hello veri diski toowith hello istediğiniz Get hello sanal makine [Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) komutu.</span><span class="sxs-lookup"><span data-stu-id="272c3-218">Get hello virtual machine that you want tooadd hello data disk toowith hello [Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) command.</span></span>

```powershell
$vm = Get-AzureRmVM -ResourceGroupName myResourceGroup -Name myVM
```

<span data-ttu-id="272c3-219">Ekle hello veri disk toohello sanal makine yapılandırmasıyla hello [Ekle AzureRmVMDataDisk](/powershell/module/azurerm.compute/add-azurermvmdatadisk) komutu.</span><span class="sxs-lookup"><span data-stu-id="272c3-219">Add hello data disk toohello virtual machine configuration with hello [Add-AzureRmVMDataDisk](/powershell/module/azurerm.compute/add-azurermvmdatadisk) command.</span></span>

```powershell
$vm = Add-AzureRmVMDataDisk -VM $vm -Name myDataDisk -CreateOption Attach -ManagedDiskId $dataDisk.Id -Lun 1
```

<span data-ttu-id="272c3-220">Merhaba sanal makine ile Merhaba güncelleştirme [güncelleştirme-AzureRmVM](/powershell/module/azurerm.compute/add-azurermvmdatadisk) komutu.</span><span class="sxs-lookup"><span data-stu-id="272c3-220">Update hello virtual machine with hello [Update-AzureRmVM](/powershell/module/azurerm.compute/add-azurermvmdatadisk) command.</span></span>

```powershell
Update-AzureRmVM -ResourceGroupName myResourceGroup -VM $vm
```

## <a name="prepare-data-disks"></a><span data-ttu-id="272c3-221">Veri diskleri hazırlama</span><span class="sxs-lookup"><span data-stu-id="272c3-221">Prepare data disks</span></span>

<span data-ttu-id="272c3-222">Bir disk ekli toohello sanal makine sağlandıktan sonra yapılandırılmış toobe toouse hello disk hello işletim sistemi gerekir.</span><span class="sxs-lookup"><span data-stu-id="272c3-222">Once a disk has been attached toohello virtual machine, hello operating system needs toobe configured toouse hello disk.</span></span> <span data-ttu-id="272c3-223">Merhaba aşağıdaki örnekte nasıl toomanually yapılandırmak hello ilk disk eklenen gösterir toohello VM.</span><span class="sxs-lookup"><span data-stu-id="272c3-223">hello following example shows how toomanually configure hello first disk added toohello VM.</span></span> <span data-ttu-id="272c3-224">Bu işlem ayrıca hello kullanarak otomatikleştirilebilir [özel betik uzantısı](./tutorial-automate-vm-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="272c3-224">This process can also be automated using hello [custom script extension](./tutorial-automate-vm-deployment.md).</span></span>

### <a name="manual-configuration"></a><span data-ttu-id="272c3-225">El ile yapılandırma</span><span class="sxs-lookup"><span data-stu-id="272c3-225">Manual configuration</span></span>

<span data-ttu-id="272c3-226">RDP bağlantısı ile Merhaba sanal makine oluşturun.</span><span class="sxs-lookup"><span data-stu-id="272c3-226">Create an RDP connection with hello virtual machine.</span></span> <span data-ttu-id="272c3-227">PowerShell'i açın ve bu komut dosyasını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="272c3-227">Open up PowerShell and run this script.</span></span>

```powershell
Get-Disk | Where partitionstyle -eq 'raw' | `
Initialize-Disk -PartitionStyle MBR -PassThru | `
New-Partition -AssignDriveLetter -UseMaximumSize | `
Format-Volume -FileSystem NTFS -NewFileSystemLabel "myDataDisk" -Confirm:$false
```

## <a name="next-steps"></a><span data-ttu-id="272c3-228">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="272c3-228">Next steps</span></span>

<span data-ttu-id="272c3-229">Bu öğreticide, VM diskleri konuları hakkında gibi öğrenilen:</span><span class="sxs-lookup"><span data-stu-id="272c3-229">In this tutorial, you learned about VM disks topics such as:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="272c3-230">İşletim sistemi ve geçici disklerle</span><span class="sxs-lookup"><span data-stu-id="272c3-230">OS disks and temporary disks</span></span>
> * <span data-ttu-id="272c3-231">Veri diskleri</span><span class="sxs-lookup"><span data-stu-id="272c3-231">Data disks</span></span>
> * <span data-ttu-id="272c3-232">Standart ve Premium diskleri</span><span class="sxs-lookup"><span data-stu-id="272c3-232">Standard and Premium disks</span></span>
> * <span data-ttu-id="272c3-233">Disk performansı</span><span class="sxs-lookup"><span data-stu-id="272c3-233">Disk performance</span></span>
> * <span data-ttu-id="272c3-234">Ekleme ve veri diskleri hazırlama</span><span class="sxs-lookup"><span data-stu-id="272c3-234">Attaching and preparing data disks</span></span>

<span data-ttu-id="272c3-235">VM yapılandırması otomatikleştirme hakkında toohello sonraki öğretici toolearn ilerleyin.</span><span class="sxs-lookup"><span data-stu-id="272c3-235">Advance toohello next tutorial toolearn about automating VM configuration.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="272c3-236">VM yapılandırmasını otomatikleştirme</span><span class="sxs-lookup"><span data-stu-id="272c3-236">Automate VM configuration</span></span>](./tutorial-automate-vm-deployment.md)
