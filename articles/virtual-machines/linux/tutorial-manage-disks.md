---
title: aaaManage Azure diskleri hello Azure CLI ile | Microsoft Docs
description: "Öğretici - hello Azure CLI ile Azure diskleri yönetme"
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
ms.openlocfilehash: ad29cfbec5f9738f47705b19d0450c9a2f555492
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-disks-with-hello-azure-cli"></a><span data-ttu-id="24a20-103">Hello Azure CLI ile Azure diskleri yönetme</span><span class="sxs-lookup"><span data-stu-id="24a20-103">Manage Azure disks with hello Azure CLI</span></span>

<span data-ttu-id="24a20-104">Azure sanal makineleri diskleri toostore hello VM'ler işletim sistemi, uygulamaları ve verileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="24a20-104">Azure virtual machines use disks toostore hello VMs operating system, applications, and data.</span></span> <span data-ttu-id="24a20-105">Bir VM oluştururken önemli toochoose disk boyutu ve yapılandırma beklenen uygun toohello iş yüküne bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="24a20-105">When creating a VM it is important toochoose a disk size and configuration appropriate toohello expected workload.</span></span> <span data-ttu-id="24a20-106">Bu öğretici, dağıtma ve VM diskleri yönetme kapsar.</span><span class="sxs-lookup"><span data-stu-id="24a20-106">This tutorial covers deploying and managing VM disks.</span></span> <span data-ttu-id="24a20-107">Hakkında bilgi edinin:</span><span class="sxs-lookup"><span data-stu-id="24a20-107">You learn about:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="24a20-108">İşletim sistemi ve geçici disklerle</span><span class="sxs-lookup"><span data-stu-id="24a20-108">OS disks and temporary disks</span></span>
> * <span data-ttu-id="24a20-109">Veri diskleri</span><span class="sxs-lookup"><span data-stu-id="24a20-109">Data disks</span></span>
> * <span data-ttu-id="24a20-110">Standart ve Premium diskleri</span><span class="sxs-lookup"><span data-stu-id="24a20-110">Standard and Premium disks</span></span>
> * <span data-ttu-id="24a20-111">Disk performansı</span><span class="sxs-lookup"><span data-stu-id="24a20-111">Disk performance</span></span>
> * <span data-ttu-id="24a20-112">Ekleme ve veri diskleri hazırlama</span><span class="sxs-lookup"><span data-stu-id="24a20-112">Attaching and preparing data disks</span></span>
> * <span data-ttu-id="24a20-113">Diskleri yeniden boyutlandırma</span><span class="sxs-lookup"><span data-stu-id="24a20-113">Resizing disks</span></span>
> * <span data-ttu-id="24a20-114">Disk anlık görüntüler</span><span class="sxs-lookup"><span data-stu-id="24a20-114">Disk snapshots</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="24a20-115">Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, Bu öğretici hello Azure CLI Sürüm 2.0.4 çalıştırmasını gerektirir veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="24a20-115">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="24a20-116">Çalıştırma `az --version` toofind hello sürümü.</span><span class="sxs-lookup"><span data-stu-id="24a20-116">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="24a20-117">Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="24a20-117">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="default-azure-disks"></a><span data-ttu-id="24a20-118">Azure diskleri varsayılan</span><span class="sxs-lookup"><span data-stu-id="24a20-118">Default Azure disks</span></span>

<span data-ttu-id="24a20-119">Bir Azure sanal makine oluşturulduğunda, iki diskleri otomatik olarak eklenen toohello sanal makine içindir.</span><span class="sxs-lookup"><span data-stu-id="24a20-119">When an Azure virtual machine is created, two disks are automatically attached toohello virtual machine.</span></span> 

<span data-ttu-id="24a20-120">**İşletim sistemi diski** - işletim sistemi disklerinde too1 terabayt boyutta ve ana hello VM'ler işletim sistemi.</span><span class="sxs-lookup"><span data-stu-id="24a20-120">**Operating system disk** - Operating system disks can be sized up too1 terabyte, and hosts hello VMs operating system.</span></span> <span data-ttu-id="24a20-121">Merhaba işletim sistemi diski olarak etiketlenmiş */dev/sda* varsayılan olarak.</span><span class="sxs-lookup"><span data-stu-id="24a20-121">hello OS disk is labeled */dev/sda* by default.</span></span> <span data-ttu-id="24a20-122">Merhaba işletim sistemi disk yapılandırması önbelleğe alma hello disk işletim sistemi performans için optimize edilmiştir.</span><span class="sxs-lookup"><span data-stu-id="24a20-122">hello disk caching configuration of hello OS disk is optimized for OS performance.</span></span> <span data-ttu-id="24a20-123">Bu yapılandırma nedeniyle, işletim sistemi diski hello **vermemelisiniz** konak uygulamalar veya veri.</span><span class="sxs-lookup"><span data-stu-id="24a20-123">Because of this configuration, hello OS disk **should not** host applications or data.</span></span> <span data-ttu-id="24a20-124">Uygulamalar ve veriler için bu makalenin sonraki bölümlerinde ayrıntılı veri diskleri kullanın.</span><span class="sxs-lookup"><span data-stu-id="24a20-124">For applications and data, use data disks, which are detailed later in this article.</span></span> 

<span data-ttu-id="24a20-125">**Geçici disk** -geçici diskler hello üzerinde bulunan bir katı hal sürücüsü kullanan aynı Azure ana bilgisayar hello VM olarak.</span><span class="sxs-lookup"><span data-stu-id="24a20-125">**Temporary disk** - Temporary disks use a solid-state drive that is located on hello same Azure host as hello VM.</span></span> <span data-ttu-id="24a20-126">Temp disklerinin yüksek oranda kullanıcı durumda ve geçici veri işleme gibi işlemler için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="24a20-126">Temp disks are highly performant and may be used for operations such as temporary data processing.</span></span> <span data-ttu-id="24a20-127">Ancak, Hello VM taşınan tooa yeni ana bilgisayar ise, geçici bir diskte depolanan tüm verileri kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="24a20-127">However, if hello VM is moved tooa new host, any data stored on a temporary disk is removed.</span></span> <span data-ttu-id="24a20-128">Merhaba hello geçici disk boyutunu hello VM boyutu tarafından belirlenir.</span><span class="sxs-lookup"><span data-stu-id="24a20-128">hello size of hello temporary disk is determined by hello VM size.</span></span> <span data-ttu-id="24a20-129">Geçici diskleri etiketli */dev/sdb* ve mountpoint, */mnt*.</span><span class="sxs-lookup"><span data-stu-id="24a20-129">Temporary disks are labeled */dev/sdb* and have a mountpoint of */mnt*.</span></span>

### <a name="temporary-disk-sizes"></a><span data-ttu-id="24a20-130">Geçici disk boyutları</span><span class="sxs-lookup"><span data-stu-id="24a20-130">Temporary disk sizes</span></span>

| <span data-ttu-id="24a20-131">Tür</span><span class="sxs-lookup"><span data-stu-id="24a20-131">Type</span></span> | <span data-ttu-id="24a20-132">VM boyutu</span><span class="sxs-lookup"><span data-stu-id="24a20-132">VM Size</span></span> | <span data-ttu-id="24a20-133">En büyük geçici disk boyutu (GB)</span><span class="sxs-lookup"><span data-stu-id="24a20-133">Max temp disk size (GB)</span></span> |
|----|----|----|
| [<span data-ttu-id="24a20-134">Genel amaçlı</span><span class="sxs-lookup"><span data-stu-id="24a20-134">General purpose</span></span>](sizes-general.md) | <span data-ttu-id="24a20-135">A ve D serisi</span><span class="sxs-lookup"><span data-stu-id="24a20-135">A and D series</span></span> | <span data-ttu-id="24a20-136">800</span><span class="sxs-lookup"><span data-stu-id="24a20-136">800</span></span> |
| [<span data-ttu-id="24a20-137">İşlem için iyileştirilmiş</span><span class="sxs-lookup"><span data-stu-id="24a20-137">Compute optimized</span></span>](sizes-compute.md) | <span data-ttu-id="24a20-138">F serisi</span><span class="sxs-lookup"><span data-stu-id="24a20-138">F series</span></span> | <span data-ttu-id="24a20-139">800</span><span class="sxs-lookup"><span data-stu-id="24a20-139">800</span></span> |
| [<span data-ttu-id="24a20-140">Bellek için iyileştirilmiş</span><span class="sxs-lookup"><span data-stu-id="24a20-140">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md) | <span data-ttu-id="24a20-141">D ve G serisi</span><span class="sxs-lookup"><span data-stu-id="24a20-141">D and G series</span></span> | <span data-ttu-id="24a20-142">6144</span><span class="sxs-lookup"><span data-stu-id="24a20-142">6144</span></span> |
| [<span data-ttu-id="24a20-143">Depolama için iyileştirilmiş</span><span class="sxs-lookup"><span data-stu-id="24a20-143">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md) | <span data-ttu-id="24a20-144">L serisi</span><span class="sxs-lookup"><span data-stu-id="24a20-144">L series</span></span> | <span data-ttu-id="24a20-145">5630</span><span class="sxs-lookup"><span data-stu-id="24a20-145">5630</span></span> |
| [<span data-ttu-id="24a20-146">GPU</span><span class="sxs-lookup"><span data-stu-id="24a20-146">GPU</span></span>](sizes-gpu.md) | <span data-ttu-id="24a20-147">N serisi</span><span class="sxs-lookup"><span data-stu-id="24a20-147">N series</span></span> | <span data-ttu-id="24a20-148">1440</span><span class="sxs-lookup"><span data-stu-id="24a20-148">1440</span></span> |
| [<span data-ttu-id="24a20-149">Yüksek performans</span><span class="sxs-lookup"><span data-stu-id="24a20-149">High performance</span></span>](sizes-hpc.md) | <span data-ttu-id="24a20-150">A ve H serisi</span><span class="sxs-lookup"><span data-stu-id="24a20-150">A and H series</span></span> | <span data-ttu-id="24a20-151">2000</span><span class="sxs-lookup"><span data-stu-id="24a20-151">2000</span></span> |

## <a name="azure-data-disks"></a><span data-ttu-id="24a20-152">Azure veri diski</span><span class="sxs-lookup"><span data-stu-id="24a20-152">Azure data disks</span></span>

<span data-ttu-id="24a20-153">Uygulama yükleme ve verilerini depolamak için ek veri disklerinin eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="24a20-153">Additional data disks can be added for installing applications and storing data.</span></span> <span data-ttu-id="24a20-154">Veri diskleri sağlam ve esnek veri depolama burada istenen herhangi bir durumda kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="24a20-154">Data disks should be used in any situation where durable and responsive data storage is desired.</span></span> <span data-ttu-id="24a20-155">Her veri diski 1 terabayttan küçük maksimum kapasitesine sahiptir.</span><span class="sxs-lookup"><span data-stu-id="24a20-155">Each data disk has a maximum capacity of 1 terabyte.</span></span> <span data-ttu-id="24a20-156">kaç tane veri diskleri ekli tooa VM olabilir hello sanal makine Hello boyutunu belirler.</span><span class="sxs-lookup"><span data-stu-id="24a20-156">hello size of hello virtual machine determines how many data disks can be attached tooa VM.</span></span> <span data-ttu-id="24a20-157">Her VM çekirdek için iki veri diskleri eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="24a20-157">For each VM core, two data disks can be attached.</span></span> 

### <a name="max-data-disks-per-vm"></a><span data-ttu-id="24a20-158">VM başına en fazla veri diski</span><span class="sxs-lookup"><span data-stu-id="24a20-158">Max data disks per VM</span></span>

| <span data-ttu-id="24a20-159">Tür</span><span class="sxs-lookup"><span data-stu-id="24a20-159">Type</span></span> | <span data-ttu-id="24a20-160">VM boyutu</span><span class="sxs-lookup"><span data-stu-id="24a20-160">VM Size</span></span> | <span data-ttu-id="24a20-161">VM başına en fazla veri diski</span><span class="sxs-lookup"><span data-stu-id="24a20-161">Max data disks per VM</span></span> |
|----|----|----|
| [<span data-ttu-id="24a20-162">Genel amaçlı</span><span class="sxs-lookup"><span data-stu-id="24a20-162">General purpose</span></span>](sizes-general.md) | <span data-ttu-id="24a20-163">A ve D serisi</span><span class="sxs-lookup"><span data-stu-id="24a20-163">A and D series</span></span> | <span data-ttu-id="24a20-164">32</span><span class="sxs-lookup"><span data-stu-id="24a20-164">32</span></span> |
| [<span data-ttu-id="24a20-165">İşlem için iyileştirilmiş</span><span class="sxs-lookup"><span data-stu-id="24a20-165">Compute optimized</span></span>](sizes-compute.md) | <span data-ttu-id="24a20-166">F serisi</span><span class="sxs-lookup"><span data-stu-id="24a20-166">F series</span></span> | <span data-ttu-id="24a20-167">32</span><span class="sxs-lookup"><span data-stu-id="24a20-167">32</span></span> |
| [<span data-ttu-id="24a20-168">Bellek için iyileştirilmiş</span><span class="sxs-lookup"><span data-stu-id="24a20-168">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md) | <span data-ttu-id="24a20-169">D ve G serisi</span><span class="sxs-lookup"><span data-stu-id="24a20-169">D and G series</span></span> | <span data-ttu-id="24a20-170">64</span><span class="sxs-lookup"><span data-stu-id="24a20-170">64</span></span> |
| [<span data-ttu-id="24a20-171">Depolama için iyileştirilmiş</span><span class="sxs-lookup"><span data-stu-id="24a20-171">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md) | <span data-ttu-id="24a20-172">L serisi</span><span class="sxs-lookup"><span data-stu-id="24a20-172">L series</span></span> | <span data-ttu-id="24a20-173">64</span><span class="sxs-lookup"><span data-stu-id="24a20-173">64</span></span> |
| [<span data-ttu-id="24a20-174">GPU</span><span class="sxs-lookup"><span data-stu-id="24a20-174">GPU</span></span>](sizes-gpu.md) | <span data-ttu-id="24a20-175">N serisi</span><span class="sxs-lookup"><span data-stu-id="24a20-175">N series</span></span> | <span data-ttu-id="24a20-176">48</span><span class="sxs-lookup"><span data-stu-id="24a20-176">48</span></span> |
| [<span data-ttu-id="24a20-177">Yüksek performans</span><span class="sxs-lookup"><span data-stu-id="24a20-177">High performance</span></span>](sizes-hpc.md) | <span data-ttu-id="24a20-178">A ve H serisi</span><span class="sxs-lookup"><span data-stu-id="24a20-178">A and H series</span></span> | <span data-ttu-id="24a20-179">32</span><span class="sxs-lookup"><span data-stu-id="24a20-179">32</span></span> |

## <a name="vm-disk-types"></a><span data-ttu-id="24a20-180">VM disk türleri</span><span class="sxs-lookup"><span data-stu-id="24a20-180">VM disk types</span></span>

<span data-ttu-id="24a20-181">Azure disk iki tür sağlar.</span><span class="sxs-lookup"><span data-stu-id="24a20-181">Azure provides two types of disk.</span></span>

### <a name="standard-disk"></a><span data-ttu-id="24a20-182">Standart disk</span><span class="sxs-lookup"><span data-stu-id="24a20-182">Standard disk</span></span>

<span data-ttu-id="24a20-183">Standart Depolama, HDD’ler ile desteklenir ve yüksek performans sunarken uygun maliyetli depolama sağlar.</span><span class="sxs-lookup"><span data-stu-id="24a20-183">Standard Storage is backed by HDDs, and delivers cost-effective storage while still being performant.</span></span> <span data-ttu-id="24a20-184">Standart diskler için uygun maliyetli geliştirme idealdir ve iş yükü test.</span><span class="sxs-lookup"><span data-stu-id="24a20-184">Standard disks are ideal for a cost effective dev and test workload.</span></span>

### <a name="premium-disk"></a><span data-ttu-id="24a20-185">Premium disk</span><span class="sxs-lookup"><span data-stu-id="24a20-185">Premium disk</span></span>

<span data-ttu-id="24a20-186">Premium diskler, SSD tabanlı yüksek performanslı, düşük gecikme süreli disk tarafından desteklenir.</span><span class="sxs-lookup"><span data-stu-id="24a20-186">Premium disks are backed by SSD-based high-performance, low-latency disk.</span></span> <span data-ttu-id="24a20-187">Üretim iş yükü çalıştıran VM'ler için mükemmel.</span><span class="sxs-lookup"><span data-stu-id="24a20-187">Perfect for VMs running production workload.</span></span> <span data-ttu-id="24a20-188">Premium depolama destekleyen DS serisi, DSv2 serisi, GS serisi ve FS-serisi VM'ler.</span><span class="sxs-lookup"><span data-stu-id="24a20-188">Premium Storage supports DS-series, DSv2-series, GS-series, and FS-series VMs.</span></span> <span data-ttu-id="24a20-189">Üç tür (P10, P20, P30) Premium diskleri gelir, hello disk türü hello hello diskin boyutunu belirler.</span><span class="sxs-lookup"><span data-stu-id="24a20-189">Premium disks come in three types (P10, P20, P30), hello size of hello disk determines hello disk type.</span></span> <span data-ttu-id="24a20-190">Seçerken, bir disk boyutu hello değeri toohello sonraki türü yuvarlanır.</span><span class="sxs-lookup"><span data-stu-id="24a20-190">When selecting, a disk size hello value is rounded up toohello next type.</span></span> <span data-ttu-id="24a20-191">Merhaba disk boyutu 128 GB daha az ise, örneğin, hello disk P10 türüdür.</span><span class="sxs-lookup"><span data-stu-id="24a20-191">For example, if hello disk size is less than 128 GB, hello disk type is P10.</span></span> <span data-ttu-id="24a20-192">Merhaba disk boyutu 129 GB ile 512 GB arasında ise, hello bir P20 boyutudur.</span><span class="sxs-lookup"><span data-stu-id="24a20-192">If hello disk size is between 129 GB and 512 GB, hello size is a P20.</span></span> <span data-ttu-id="24a20-193">Hiçbir şey üzerinde 512 GB hello boyutudur bir P30.</span><span class="sxs-lookup"><span data-stu-id="24a20-193">Anything over 512 GB, hello size is a P30.</span></span>

### <a name="premium-disk-performance"></a><span data-ttu-id="24a20-194">Premium disk performansı</span><span class="sxs-lookup"><span data-stu-id="24a20-194">Premium disk performance</span></span>

|<span data-ttu-id="24a20-195">Premium depolama disk türü</span><span class="sxs-lookup"><span data-stu-id="24a20-195">Premium storage disk type</span></span> | <span data-ttu-id="24a20-196">P10</span><span class="sxs-lookup"><span data-stu-id="24a20-196">P10</span></span> | <span data-ttu-id="24a20-197">P20</span><span class="sxs-lookup"><span data-stu-id="24a20-197">P20</span></span> | <span data-ttu-id="24a20-198">P30</span><span class="sxs-lookup"><span data-stu-id="24a20-198">P30</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="24a20-199">Disk boyutu (yukarı yuvarlar)</span><span class="sxs-lookup"><span data-stu-id="24a20-199">Disk size (round up)</span></span> | <span data-ttu-id="24a20-200">128 GB</span><span class="sxs-lookup"><span data-stu-id="24a20-200">128 GB</span></span> | <span data-ttu-id="24a20-201">512 GB</span><span class="sxs-lookup"><span data-stu-id="24a20-201">512 GB</span></span> | <span data-ttu-id="24a20-202">1.024 GB (1 TB)</span><span class="sxs-lookup"><span data-stu-id="24a20-202">1,024 GB (1 TB)</span></span> |
| <span data-ttu-id="24a20-203">Disk başına en fazla IOPS</span><span class="sxs-lookup"><span data-stu-id="24a20-203">Max IOPS per disk</span></span> | <span data-ttu-id="24a20-204">500</span><span class="sxs-lookup"><span data-stu-id="24a20-204">500</span></span> | <span data-ttu-id="24a20-205">2,300</span><span class="sxs-lookup"><span data-stu-id="24a20-205">2,300</span></span> | <span data-ttu-id="24a20-206">5,000</span><span class="sxs-lookup"><span data-stu-id="24a20-206">5,000</span></span> |
<span data-ttu-id="24a20-207">Disk başına aktarım hızı</span><span class="sxs-lookup"><span data-stu-id="24a20-207">Throughput per disk</span></span> | <span data-ttu-id="24a20-208">100 MB/s</span><span class="sxs-lookup"><span data-stu-id="24a20-208">100 MB/s</span></span> | <span data-ttu-id="24a20-209">150 MB/s</span><span class="sxs-lookup"><span data-stu-id="24a20-209">150 MB/s</span></span> | <span data-ttu-id="24a20-210">200 MB/sn</span><span class="sxs-lookup"><span data-stu-id="24a20-210">200 MB/s</span></span> |

<span data-ttu-id="24a20-211">Disk başına maksimum IOPS Merhaba tablonun yukarısındaki tanımlayan olsa da, daha yüksek düzeyde performans birden çok veri diskleri bölümlemesine tarafından elde edilebilir.</span><span class="sxs-lookup"><span data-stu-id="24a20-211">While hello above table identifies max IOPS per disk, a higher level of performance can be achieved by striping multiple data disks.</span></span> <span data-ttu-id="24a20-212">Örneğin, bir Standard_GS5 VM en 80.000 IOPS elde edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="24a20-212">For instance, a Standard_GS5 VM can achieve a maximum of 80,000 IOPS.</span></span> <span data-ttu-id="24a20-213">VM başına maksimum IOPS hakkında ayrıntılı bilgi için bkz: [Linux VM boyutları](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="24a20-213">For detailed information on max IOPS per VM, see [Linux VM sizes](sizes.md).</span></span>

## <a name="create-and-attach-disks"></a><span data-ttu-id="24a20-214">Oluşturma ve diskleri ekleme</span><span class="sxs-lookup"><span data-stu-id="24a20-214">Create and attach disks</span></span>

<span data-ttu-id="24a20-215">Veri diskleri oluşturulan ve VM oluşturma zamanı veya var olan VM tooan bağlı.</span><span class="sxs-lookup"><span data-stu-id="24a20-215">Data disks can be created and attached at VM creation time or tooan existing VM.</span></span>

### <a name="attach-disk-at-vm-creation"></a><span data-ttu-id="24a20-216">VM oluşturulurken diski kullanıma açın</span><span class="sxs-lookup"><span data-stu-id="24a20-216">Attach disk at VM creation</span></span>

<span data-ttu-id="24a20-217">Bir kaynak grubu ile Merhaba oluşturmak [az grubu oluşturma](https://docs.microsoft.com/cli/azure/group#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="24a20-217">Create a resource group with hello [az group create](https://docs.microsoft.com/cli/azure/group#create) command.</span></span> 

```azurecli-interactive 
az group create --name myResourceGroupDisk --location eastus
```

<span data-ttu-id="24a20-218">Hello kullanarak bir VM oluşturma [az vm oluşturma]( /cli/azure/vm#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="24a20-218">Create a VM using hello [az vm create]( /cli/azure/vm#create) command.</span></span> <span data-ttu-id="24a20-219">Merhaba `--datadisk-sizes-gb` olmayan bir ek disk oluşturulması gerektiğini ve toohello sanal makineye bağlı kullanılan toospecify bağımsız değişken.</span><span class="sxs-lookup"><span data-stu-id="24a20-219">hello `--datadisk-sizes-gb` argument is used toospecify that an additional disk should be created and attached toohello virtual machine.</span></span> <span data-ttu-id="24a20-220">toocreate ve birden fazla disk ekleyin, disk boyutu değerleri boşlukla ayrılmış bir listesini kullanın.</span><span class="sxs-lookup"><span data-stu-id="24a20-220">toocreate and attach more than one disk, use a space-delimited list of disk size values.</span></span> <span data-ttu-id="24a20-221">Aşağıdaki örneğine hello VM iki veri disklerinde, her iki 128 GB oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="24a20-221">In hello following example, a VM is created with two data disks, both 128 GB.</span></span> <span data-ttu-id="24a20-222">Merhaba disk boyutları 128 GB olduğundan, bu diskleri hem de disk başına en fazla 500 IOPS sağlar P10s olarak yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="24a20-222">Because hello disk sizes are 128 GB, these disks are both configured as P10s, which provide maximum 500 IOPS per disk.</span></span>

```azurecli-interactive 
az vm create \
  --resource-group myResourceGroupDisk \
  --name myVM \
  --image UbuntuLTS \
  --size Standard_DS2_v2 \
  --data-disk-sizes-gb 128 128 \
  --generate-ssh-keys
```

### <a name="attach-disk-tooexisting-vm"></a><span data-ttu-id="24a20-223">Disk tooexisting VM ekleme</span><span class="sxs-lookup"><span data-stu-id="24a20-223">Attach disk tooexisting VM</span></span>

<span data-ttu-id="24a20-224">toocreate ve yeni disk tooan var olan bir sanal makine ekleme, hello kullanma [az vm diskini](/cli/azure/vm/disk#attach) komutu.</span><span class="sxs-lookup"><span data-stu-id="24a20-224">toocreate and attach a new disk tooan existing virtual machine, use hello [az vm disk attach](/cli/azure/vm/disk#attach) command.</span></span> <span data-ttu-id="24a20-225">Merhaba aşağıdaki örnekte bir premium disk boyutu, 128 gigabayt oluşturur ve VM hello son adımda oluşturduğunuz toohello ekler.</span><span class="sxs-lookup"><span data-stu-id="24a20-225">hello following example creates a premium disk, 128 gigabytes in size, and attaches it toohello VM created in hello last step.</span></span>

```azurecli-interactive 
az vm disk attach --vm-name myVM --resource-group myResourceGroupDisk --disk myDataDisk --size-gb 128 --sku Premium_LRS --new 
```

## <a name="prepare-data-disks"></a><span data-ttu-id="24a20-226">Veri diskleri hazırlama</span><span class="sxs-lookup"><span data-stu-id="24a20-226">Prepare data disks</span></span>

<span data-ttu-id="24a20-227">Bir disk ekli toohello sanal makine sağlandıktan sonra yapılandırılmış toobe toouse hello disk hello işletim sistemi gerekir.</span><span class="sxs-lookup"><span data-stu-id="24a20-227">Once a disk has been attached toohello virtual machine, hello operating system needs toobe configured toouse hello disk.</span></span> <span data-ttu-id="24a20-228">Aşağıdaki örnek hello nasıl toomanually yapılandırmak bir disk gösterir.</span><span class="sxs-lookup"><span data-stu-id="24a20-228">hello following example shows how toomanually configure a disk.</span></span> <span data-ttu-id="24a20-229">Bu işlem ayrıca içinde ele bulut-init, kullanarak otomatik olarak yapılabilir bir [sonraki öğretici](./tutorial-automate-vm-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="24a20-229">This process can also be automated using cloud-init, which is covered in a [later tutorial](./tutorial-automate-vm-deployment.md).</span></span>

### <a name="manual-configuration"></a><span data-ttu-id="24a20-230">El ile yapılandırma</span><span class="sxs-lookup"><span data-stu-id="24a20-230">Manual configuration</span></span>

<span data-ttu-id="24a20-231">Bir SSH bağlantısı ile Merhaba sanal makine oluşturun.</span><span class="sxs-lookup"><span data-stu-id="24a20-231">Create an SSH connection with hello virtual machine.</span></span> <span data-ttu-id="24a20-232">Merhaba örnek IP adresinin hello genel IP hello sanal makinenin ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="24a20-232">Replace hello example IP address with hello public IP of hello virtual machine.</span></span>

```azurecli-interactive 
ssh 52.174.34.95
```

<span data-ttu-id="24a20-233">Bölüm hello diskle `fdisk`.</span><span class="sxs-lookup"><span data-stu-id="24a20-233">Partition hello disk with `fdisk`.</span></span>

```bash
(echo n; echo p; echo 1; echo ; echo ; echo w) | sudo fdisk /dev/sdc
```

<span data-ttu-id="24a20-234">Hello kullanarak bir dosya sistemi toohello bölümü yazma `mkfs` komutu.</span><span class="sxs-lookup"><span data-stu-id="24a20-234">Write a file system toohello partition by using hello `mkfs` command.</span></span>

```bash
sudo mkfs -t ext4 /dev/sdc1
```

<span data-ttu-id="24a20-235">Böylece hello işletim sisteminde erişilebilir hello yeni diski bağlayın.</span><span class="sxs-lookup"><span data-stu-id="24a20-235">Mount hello new disk so that it is accessible in hello operating system.</span></span>

```bash
sudo mkdir /datadrive && sudo mount /dev/sdc1 /datadrive
```

<span data-ttu-id="24a20-236">Merhaba disk şimdi hello erişilebilir *datadrive* hello çalıştırarak doğrulanabilir mountpoint `df -h` komutu.</span><span class="sxs-lookup"><span data-stu-id="24a20-236">hello disk can now be accessed through hello *datadrive* mountpoint, which can be verified by running hello `df -h` command.</span></span> 

```bash
df -h
```

<span data-ttu-id="24a20-237">Merhaba çıktısını gösterir hello yeni sürücü üzerinde takılı */datadrive*.</span><span class="sxs-lookup"><span data-stu-id="24a20-237">hello output shows hello new drive mounted on */datadrive*.</span></span>

```bash
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda1        30G  1.4G   28G   5% /
/dev/sdb1       6.8G   16M  6.4G   1% /mnt
/dev/sdc1        50G   52M   47G   1% /datadrive
```

<span data-ttu-id="24a20-238">Sürücü hello tooensure bir yeniden başlatmadan sonra yeniden, toohello eklenmelidir */etc/fstab* dosya.</span><span class="sxs-lookup"><span data-stu-id="24a20-238">tooensure that hello drive is remounted after a reboot, it must be added toohello */etc/fstab* file.</span></span> <span data-ttu-id="24a20-239">toodo, bu nedenle, hello hello disk UUID'si hello ile almak `blkid` yardımcı programı.</span><span class="sxs-lookup"><span data-stu-id="24a20-239">toodo so, get hello UUID of hello disk with hello `blkid` utility.</span></span>

```bash
sudo -i blkid
```

<span data-ttu-id="24a20-240">Merhaba çıktısını görüntüler hello hello sürücü UUID'si `/dev/sdc1` bu durumda.</span><span class="sxs-lookup"><span data-stu-id="24a20-240">hello output displays hello UUID of hello drive, `/dev/sdc1` in this case.</span></span>

```bash
/dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
```

<span data-ttu-id="24a20-241">Toohello aşağıdaki satırı benzer toohello ekleme */etc/fstab* dosya.</span><span class="sxs-lookup"><span data-stu-id="24a20-241">Add a line similar toohello following toohello */etc/fstab* file.</span></span> <span data-ttu-id="24a20-242">Ayrıca engelleri yazma Not kullanarak devre dışı bırakılabilir *engel = 0*, bu yapılandırma disk performansını artırabilir.</span><span class="sxs-lookup"><span data-stu-id="24a20-242">Also note that write barriers can be disabled using *barrier=0*, this configuration can improve disk performance.</span></span> 

```bash
UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive  ext4    defaults,nofail,barrier=0   1  2
```

<span data-ttu-id="24a20-243">Merhaba disk yapılandırıldı, hello SSH oturumu kapatın.</span><span class="sxs-lookup"><span data-stu-id="24a20-243">Now that hello disk has been configured, close hello SSH session.</span></span>

```bash
exit
```

## <a name="resize-vm-disk"></a><span data-ttu-id="24a20-244">VM disk yeniden boyutlandırma</span><span class="sxs-lookup"><span data-stu-id="24a20-244">Resize VM disk</span></span>

<span data-ttu-id="24a20-245">Bir VM dağıtıldıktan sonra hello işletim sistemi diski veya hiçbir bağlı veri diski boyutu artırılabilir.</span><span class="sxs-lookup"><span data-stu-id="24a20-245">Once a VM has been deployed, hello operating system disk or any attached data disks can be increased in size.</span></span> <span data-ttu-id="24a20-246">Bir diskin Hello boyutunu artırmayı daha fazla depolama alanı ya da daha yüksek düzeyde performans (P10, P20, P30) ihtiyacı olduğunda faydalıdır.</span><span class="sxs-lookup"><span data-stu-id="24a20-246">Increasing hello size of a disk is beneficial when needing more storage space or a higher level of performance (P10, P20, P30).</span></span> <span data-ttu-id="24a20-247">Disk boyutu azaltılamaz unutmayın.</span><span class="sxs-lookup"><span data-stu-id="24a20-247">Note, disks cannot be decreased in size.</span></span>

<span data-ttu-id="24a20-248">Disk boyutunun artırılması önce kimliği hello veya hello disk adı gereklidir.</span><span class="sxs-lookup"><span data-stu-id="24a20-248">Before increasing disk size, hello Id or name of hello disk is needed.</span></span> <span data-ttu-id="24a20-249">Kullanım hello [az disk listesi](/cli/azure/vm/disk#list) komutu tooreturn tüm diskler bir kaynak grubunda.</span><span class="sxs-lookup"><span data-stu-id="24a20-249">Use hello [az disk list](/cli/azure/vm/disk#list) command tooreturn all disks in a resource group.</span></span> <span data-ttu-id="24a20-250">Merhaba disk adı tooresize istediğiniz not edin.</span><span class="sxs-lookup"><span data-stu-id="24a20-250">Take note of hello disk name that you would like tooresize.</span></span>

```azurecli-interactive 
az disk list -g myResourceGroupDisk --query '[*].{Name:name,Gb:diskSizeGb,Tier:accountType}' --output table
```

<span data-ttu-id="24a20-251">Merhaba VM deallocated olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="24a20-251">hello VM must also be deallocated.</span></span> <span data-ttu-id="24a20-252">Kullanım hello [az vm serbest bırakma]( /cli/azure/vm#deallocate) komut toostop ve hello VM serbest bırakma.</span><span class="sxs-lookup"><span data-stu-id="24a20-252">Use hello [az vm deallocate]( /cli/azure/vm#deallocate) command toostop and deallocate hello VM.</span></span>

```azurecli-interactive 
az vm deallocate --resource-group myResourceGroupDisk --name myVM
```

<span data-ttu-id="24a20-253">Kullanım hello [az disk güncelleştirme](/cli/azure/vm/disk#update) komutu tooresize hello disk.</span><span class="sxs-lookup"><span data-stu-id="24a20-253">Use hello [az disk update](/cli/azure/vm/disk#update) command tooresize hello disk.</span></span> <span data-ttu-id="24a20-254">Bu örnek adlı bir disk yeniden boyutlandırır *myDataDisk* too1 terabayt.</span><span class="sxs-lookup"><span data-stu-id="24a20-254">This example resizes a disk named *myDataDisk* too1 terabyte.</span></span>

```azurecli-interactive 
az disk update --name myDataDisk --resource-group myResourceGroupDisk --size-gb 1023
```

<span data-ttu-id="24a20-255">Merhaba yeniden boyutlandırma işlemi tamamlandıktan sonra hello VM başlatın.</span><span class="sxs-lookup"><span data-stu-id="24a20-255">Once hello resize operation has completed, start hello VM.</span></span>

```azurecli-interactive 
az vm start --resource-group myResourceGroupDisk --name myVM
```

<span data-ttu-id="24a20-256">İşletim sistemi diski hello boyutlandırdıysanız hello bölüm otomatik olarak olması genişletilmiştir.</span><span class="sxs-lookup"><span data-stu-id="24a20-256">If you’ve resized hello operating system disk, hello partition is automatically be expanded.</span></span> <span data-ttu-id="24a20-257">Bir veri diski yeniden boyutlandırılabilir, geçerli tüm bölümler hello VM'ler işletim sisteminde genişletilmiş toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="24a20-257">If you have resized a data disk, any current partitions need toobe expanded in hello VMs operating system.</span></span>

## <a name="snapshot-azure-disks"></a><span data-ttu-id="24a20-258">Azure diskleri anlık görüntüsünü alın</span><span class="sxs-lookup"><span data-stu-id="24a20-258">Snapshot Azure disks</span></span>

<span data-ttu-id="24a20-259">Bir disk anlık hello disk okuma yalnızca, zaman noktası kopyasını oluşturur.</span><span class="sxs-lookup"><span data-stu-id="24a20-259">Taking a disk snapshot creates a read only, point-in-time copy of hello disk.</span></span> <span data-ttu-id="24a20-260">Azure VM anlık görüntüler, yapılandırma değişiklikleri yapmadan önce bir VM hello durumunu hızlı bir şekilde kaydetmek için kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="24a20-260">Azure VM snapshots are useful for quickly saving hello state of a VM before making configuration changes.</span></span> <span data-ttu-id="24a20-261">Merhaba olay hello yapılandırma değişiklikleri kanıtlanmasına istenmeden toobe, VM durumunu hello anlık görüntü kullanılarak geri yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="24a20-261">In hello event hello configuration changes prove toobe undesired, VM state can be restored using hello snapshot.</span></span> <span data-ttu-id="24a20-262">Birden fazla disk bir VM'ye sahip olduğu bir anlık görüntü hello bağımsız olarak her disk oluşturulduğunda diğerleri.</span><span class="sxs-lookup"><span data-stu-id="24a20-262">When a VM has more than one disk, a snapshot is taken of each disk independently of hello others.</span></span> <span data-ttu-id="24a20-263">Uygulama tutarlı yedek almak için disk anlık görüntüler çıkarmadan önce hello VM durdurma göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="24a20-263">For taking application consistent backups, consider stopping hello VM before taking disk snapshots.</span></span> <span data-ttu-id="24a20-264">Alternatif olarak, hello kullanın [Azure Backup hizmeti](/azure/backup/), hangi etkinleştirir, tooperform VM çalıştıran hello sırasında yedeklemeleri otomatik.</span><span class="sxs-lookup"><span data-stu-id="24a20-264">Alternatively, use hello [Azure Backup service](/azure/backup/), which enables you tooperform automated backups while hello VM is running.</span></span>

### <a name="create-snapshot"></a><span data-ttu-id="24a20-265">Anlık görüntü oluşturma</span><span class="sxs-lookup"><span data-stu-id="24a20-265">Create snapshot</span></span>

<span data-ttu-id="24a20-266">Bir sanal makine disk anlık oluşturmadan önce hello kimliği veya hello disk adı gerekli.</span><span class="sxs-lookup"><span data-stu-id="24a20-266">Before creating a virtual machine disk snapshot, hello Id or name of hello disk is needed.</span></span> <span data-ttu-id="24a20-267">Kullanım hello [az vm Göster](https://docs.microsoft.com/en-us/cli/azure/vm#show) komutu tooreturn hello disk kimliği. Bu örnekte, böylece daha sonraki bir adımda kullanılabilir hello disk kimliği bir değişkende depolanır.</span><span class="sxs-lookup"><span data-stu-id="24a20-267">Use hello [az vm show](https://docs.microsoft.com/en-us/cli/azure/vm#show) command tooreturn hello disk id. In this example, hello disk id is stored in a variable so that it can be used in a later step.</span></span>

```azurecli-interactive 
osdiskid=$(az vm show -g myResourceGroupDisk -n myVM --query "storageProfile.osDisk.managedDisk.id" -o tsv)
```

<span data-ttu-id="24a20-268">Merhaba sanal makine diski hello kimliğini sahip olduğunuza göre hello aşağıdaki komut hello diskin anlık görüntüsünü oluşturur.</span><span class="sxs-lookup"><span data-stu-id="24a20-268">Now that you have hello id of hello virtual machine disk, hello following command creates a snapshot of hello disk.</span></span>

```azurcli
az snapshot create -g myResourceGroupDisk --source "$osdiskid" --name osDisk-backup
```

### <a name="create-disk-from-snapshot"></a><span data-ttu-id="24a20-269">Disk anlık görüntüden oluşturma</span><span class="sxs-lookup"><span data-stu-id="24a20-269">Create disk from snapshot</span></span>

<span data-ttu-id="24a20-270">Bu anlık görüntü sonra kullanılan toorecreate hello sanal makineye bağlanabilir bir diske dönüştürülebilir.</span><span class="sxs-lookup"><span data-stu-id="24a20-270">This snapshot can then be converted into a disk, which can be used toorecreate hello virtual machine.</span></span>

```azurecli-interactive 
az disk create --resource-group myResourceGroupDisk --name mySnapshotDisk --source osDisk-backup
```

### <a name="restore-virtual-machine-from-snapshot"></a><span data-ttu-id="24a20-271">Sanal makine anlık görüntüden geri yükleme</span><span class="sxs-lookup"><span data-stu-id="24a20-271">Restore virtual machine from snapshot</span></span>

<span data-ttu-id="24a20-272">toodemonstrate sanal makine kurtarması, delete hello varolan sanal makine.</span><span class="sxs-lookup"><span data-stu-id="24a20-272">toodemonstrate virtual machine recovery, delete hello existing virtual machine.</span></span> 

```azurecli-interactive 
az vm delete --resource-group myResourceGroupDisk --name myVM
```

<span data-ttu-id="24a20-273">Başlangıç anlık görüntü diskten yeni bir sanal makine oluşturun.</span><span class="sxs-lookup"><span data-stu-id="24a20-273">Create a new virtual machine from hello snapshot disk.</span></span>

```azurecli-interactive 
az vm create --resource-group myResourceGroupDisk --name myVM --attach-os-disk mySnapshotDisk --os-type linux
```

### <a name="reattach-data-disk"></a><span data-ttu-id="24a20-274">Veri diski yeniden bağlayın</span><span class="sxs-lookup"><span data-stu-id="24a20-274">Reattach data disk</span></span>

<span data-ttu-id="24a20-275">Tüm veri diskleri yeniden toobe toohello sanal makine gerekir.</span><span class="sxs-lookup"><span data-stu-id="24a20-275">All data disks need toobe reattached toohello virtual machine.</span></span>

<span data-ttu-id="24a20-276">İlk hello kullanarak hello veri disk adı Bul [az disk listesi](https://docs.microsoft.com/cli/azure/disk#list) komutu.</span><span class="sxs-lookup"><span data-stu-id="24a20-276">First find hello data disk name using hello [az disk list](https://docs.microsoft.com/cli/azure/disk#list) command.</span></span> <span data-ttu-id="24a20-277">Bu örnek yerler hello adlı bir değişkende hello diskin adını *datadisk*, hello sonraki adımda kullanılır.</span><span class="sxs-lookup"><span data-stu-id="24a20-277">This example places hello name of hello disk in a variable named *datadisk*, which is used in hello next step.</span></span>

```azurecli-interactive 
datadisk=$(az disk list -g myResourceGroupDisk --query "[?contains(name,'myVM')].[name]" -o tsv)
```

<span data-ttu-id="24a20-278">Kullanım hello [az vm diskini](https://docs.microsoft.com/cli/azure/vm/disk#attach) komutu tooattach hello disk.</span><span class="sxs-lookup"><span data-stu-id="24a20-278">Use hello [az vm disk attach](https://docs.microsoft.com/cli/azure/vm/disk#attach) command tooattach hello disk.</span></span>

```azurecli-interactive 
az vm disk attach –g myResourceGroupDisk –-vm-name myVM –-disk $datadisk
```

## <a name="next-steps"></a><span data-ttu-id="24a20-279">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="24a20-279">Next steps</span></span>

<span data-ttu-id="24a20-280">Bu öğreticide, VM diskleri konuları hakkında gibi öğrenilen:</span><span class="sxs-lookup"><span data-stu-id="24a20-280">In this tutorial, you learned about VM disks topics such as:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="24a20-281">İşletim sistemi ve geçici disklerle</span><span class="sxs-lookup"><span data-stu-id="24a20-281">OS disks and temporary disks</span></span>
> * <span data-ttu-id="24a20-282">Veri diskleri</span><span class="sxs-lookup"><span data-stu-id="24a20-282">Data disks</span></span>
> * <span data-ttu-id="24a20-283">Standart ve Premium diskleri</span><span class="sxs-lookup"><span data-stu-id="24a20-283">Standard and Premium disks</span></span>
> * <span data-ttu-id="24a20-284">Disk performansı</span><span class="sxs-lookup"><span data-stu-id="24a20-284">Disk performance</span></span>
> * <span data-ttu-id="24a20-285">Ekleme ve veri diskleri hazırlama</span><span class="sxs-lookup"><span data-stu-id="24a20-285">Attaching and preparing data disks</span></span>
> * <span data-ttu-id="24a20-286">Diskleri yeniden boyutlandırma</span><span class="sxs-lookup"><span data-stu-id="24a20-286">Resizing disks</span></span>
> * <span data-ttu-id="24a20-287">Disk anlık görüntüler</span><span class="sxs-lookup"><span data-stu-id="24a20-287">Disk snapshots</span></span>

<span data-ttu-id="24a20-288">VM yapılandırması otomatikleştirme hakkında toohello sonraki öğretici toolearn ilerleyin.</span><span class="sxs-lookup"><span data-stu-id="24a20-288">Advance toohello next tutorial toolearn about automating VM configuration.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="24a20-289">VM yapılandırmasını otomatikleştirme</span><span class="sxs-lookup"><span data-stu-id="24a20-289">Automate VM configuration</span></span>](./tutorial-automate-vm-deployment.md)
