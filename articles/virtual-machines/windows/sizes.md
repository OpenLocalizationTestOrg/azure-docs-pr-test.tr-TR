---
title: "aaaWindows VM boyutları Azure'da | Microsoft Docs"
description: "Farklı boyutlarda Hello azure'da Windows sanal makineler için kullanılabilir listeler."
services: virtual-machines-windows
documentationcenter: 
author: jonbeck7
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: aabf0d30-04eb-4d34-b44a-69f8bfb84f22
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/28/2017
ms.author: jonbeck
ms.openlocfilehash: 80bd8241b134031c41b56224e841c7557c4845cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="sizes-for-windows-virtual-machines-in-azure"></a><span data-ttu-id="90051-103">Azure'da Windows sanal makineler için Boyutlar</span><span class="sxs-lookup"><span data-stu-id="90051-103">Sizes for Windows virtual machines in Azure</span></span>

<span data-ttu-id="90051-104">Bu makalede hello kullanılabilir boyutları ve Windows uygulamaları ve iş yüklerini toorun kullanabileceğiniz Azure sanal makineler için başlangıç seçenekleri.</span><span class="sxs-lookup"><span data-stu-id="90051-104">This article describes hello available sizes and options for hello Azure virtual machines you can use toorun your Windows apps and workloads.</span></span> <span data-ttu-id="90051-105">Bu kaynaklar toouse planlaması yaparken de dağıtım konuları toobe farkında sağlar.</span><span class="sxs-lookup"><span data-stu-id="90051-105">It also provides deployment considerations toobe aware of when you're planning toouse these resources.</span></span>  <span data-ttu-id="90051-106">Bu makalede ayrıca kullanılabilir [Linux sanal makineleri](../linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="90051-106">This article is also available for [Linux virtual machines](../linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


| <span data-ttu-id="90051-107">Tür</span><span class="sxs-lookup"><span data-stu-id="90051-107">Type</span></span>                     | <span data-ttu-id="90051-108">Boyutlar</span><span class="sxs-lookup"><span data-stu-id="90051-108">Sizes</span></span>           |    <span data-ttu-id="90051-109">Açıklama</span><span class="sxs-lookup"><span data-stu-id="90051-109">Description</span></span>       |
|--------------------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------|
| [<span data-ttu-id="90051-110">Genel amaçlı</span><span class="sxs-lookup"><span data-stu-id="90051-110">General purpose</span></span>](sizes-general.md)          | <span data-ttu-id="90051-111">Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0-7</span><span class="sxs-lookup"><span data-stu-id="90051-111">Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0-7</span></span> | <span data-ttu-id="90051-112">Dengeli CPU/bellek oranı.</span><span class="sxs-lookup"><span data-stu-id="90051-112">Balanced CPU-to-memory ratio.</span></span> <span data-ttu-id="90051-113">Test ve geliştirme, küçük toomedium veritabanları ve düşük toomedium trafiği web sunucuları için idealdir.</span><span class="sxs-lookup"><span data-stu-id="90051-113">Ideal for testing and development, small toomedium databases, and low toomedium traffic web servers.</span></span> |
| [<span data-ttu-id="90051-114">İşlem için iyileştirilmiş</span><span class="sxs-lookup"><span data-stu-id="90051-114">Compute optimized</span></span>](sizes-compute.md)        | <span data-ttu-id="90051-115">FS, F</span><span class="sxs-lookup"><span data-stu-id="90051-115">Fs, F</span></span>             | <span data-ttu-id="90051-116">Yüksek CPU/bellek oranı.</span><span class="sxs-lookup"><span data-stu-id="90051-116">High CPU-to-memory ratio.</span></span> <span data-ttu-id="90051-117">Orta yoğunlukta trafiğe sahip web sunucuları, ağ gereçleri, toplu işlemler ve uygulama sunucuları için uygundur.</span><span class="sxs-lookup"><span data-stu-id="90051-117">Good for medium traffic web servers, network appliances, batch processes, and application servers.</span></span>        |
| [<span data-ttu-id="90051-118">Bellek için iyileştirilmiş</span><span class="sxs-lookup"><span data-stu-id="90051-118">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md)         | <span data-ttu-id="90051-119">Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D</span><span class="sxs-lookup"><span data-stu-id="90051-119">Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D</span></span>   | <span data-ttu-id="90051-120">Yüksek bellek CPU oranı.</span><span class="sxs-lookup"><span data-stu-id="90051-120">High memory-to-CPU ratio.</span></span> <span data-ttu-id="90051-121">İlişkisel veritabanı sunucuları, Orta toolarge önbellekleri ve bellek içi analizi için mükemmel.</span><span class="sxs-lookup"><span data-stu-id="90051-121">Great for relational database servers, medium toolarge caches, and in-memory analytics.</span></span>                 |
| [<span data-ttu-id="90051-122">Depolama için iyileştirilmiş</span><span class="sxs-lookup"><span data-stu-id="90051-122">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md)        | <span data-ttu-id="90051-123">Ls</span><span class="sxs-lookup"><span data-stu-id="90051-123">Ls</span></span>                | <span data-ttu-id="90051-124">Yüksek disk aktarım hızı ve GÇ.</span><span class="sxs-lookup"><span data-stu-id="90051-124">High disk throughput and IO.</span></span> <span data-ttu-id="90051-125">Büyük Veri, SQL ve NoSQL veritabanları için ideal.</span><span class="sxs-lookup"><span data-stu-id="90051-125">Ideal for Big Data, SQL, and NoSQL databases.</span></span>                                                         |
| [<span data-ttu-id="90051-126">GPU</span><span class="sxs-lookup"><span data-stu-id="90051-126">GPU</span></span>](sizes-gpu.md)            | <span data-ttu-id="90051-127">NV, NC</span><span class="sxs-lookup"><span data-stu-id="90051-127">NV, NC</span></span>            | <span data-ttu-id="90051-128">Yoğun Grafik işleme ve video düzenleme için hedeflenen özelleştirilmiş sanal makineler.</span><span class="sxs-lookup"><span data-stu-id="90051-128">Specialized virtual machines targeted for heavy graphic rendering and video editing.</span></span> <span data-ttu-id="90051-129">Tek veya birden çok GPU ile kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="90051-129">Available with single or multiple GPUs.</span></span>       |
| [<span data-ttu-id="90051-130">Yüksek performanslı işlem</span><span class="sxs-lookup"><span data-stu-id="90051-130">High performance compute</span></span>](sizes-hpc.md) | <span data-ttu-id="90051-131">H, A8-11</span><span class="sxs-lookup"><span data-stu-id="90051-131">H, A8-11</span></span>          | <span data-ttu-id="90051-132">İşleme düzeyi yüksek olan isteğe bağlı ağ arabirimleri (RDMA) içeren sanal makineler, şimdiye kadarki en hızlı ve en güçlü CPU ile sunuluyor.</span><span class="sxs-lookup"><span data-stu-id="90051-132">Our fastest and most powerful CPU virtual machines with optional high-throughput network interfaces (RDMA).</span></span> 

<br> 

- <span data-ttu-id="90051-133">Merhaba çeşitli boyutlarda fiyatlandırma hakkında daha fazla bilgi için bkz: [sanal makineler fiyatlandırma](https://azure.microsoft.com/pricing/details/virtual-machines/#Windows).</span><span class="sxs-lookup"><span data-stu-id="90051-133">For information about pricing of hello various sizes, see [Virtual Machines Pricing](https://azure.microsoft.com/pricing/details/virtual-machines/#Windows).</span></span> 
- <span data-ttu-id="90051-134">Azure vm'lerinde toosee genel sınırları bkz [Azure aboneliği ve hizmet sınırları, kotaları ve kısıtlamaları](../../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="90051-134">toosee general limits on Azure VMs, see [Azure subscription and service limits, quotas, and constraints](../../azure-subscription-service-limits.md).</span></span>
- <span data-ttu-id="90051-135">Depolama maliyetleri hello depolama hesabında kullanılan sayfa ayrı ayrı göre hesaplanır.</span><span class="sxs-lookup"><span data-stu-id="90051-135">Storage costs are calculated separately based on used pages in hello storage account.</span></span> <span data-ttu-id="90051-136">Ayrıntılar için [Azure Storage fiyatlandırması](https://azure.microsoft.com/pricing/details/storage/).</span><span class="sxs-lookup"><span data-stu-id="90051-136">For details, [Azure Storage Pricing](https://azure.microsoft.com/pricing/details/storage/).</span></span>
- <span data-ttu-id="90051-137">Hakkında daha fazla bilgi [Azure işlem birimleri (ACU)](acu.md) Azure SKU'ları üzerinde işlem performans karşılaştırmanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="90051-137">Learn more about how [Azure compute units (ACU)](acu.md) can help you compare compute performance across Azure SKUs.</span></span>



## <a name="rest-api"></a><span data-ttu-id="90051-138">REST API'si</span><span class="sxs-lookup"><span data-stu-id="90051-138">Rest API</span></span>

<span data-ttu-id="90051-139">VM boyutları için hello REST API tooquery kullanma hakkında daha fazla bilgi için hello aşağıdakilere bakın:</span><span class="sxs-lookup"><span data-stu-id="90051-139">For information on using hello REST API tooquery for VM sizes, see hello following:</span></span>

- [<span data-ttu-id="90051-140">Yeniden boyutlandırma için kullanılabilir sanal makine boyutlarını Listele</span><span class="sxs-lookup"><span data-stu-id="90051-140">List available virtual machine sizes for resizing</span></span>](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-for-resizing)
- [<span data-ttu-id="90051-141">Bir abonelik için kullanılabilir sanal makine boyutlarını Listele</span><span class="sxs-lookup"><span data-stu-id="90051-141">List available virtual machine sizes for a subscription</span></span>](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-region)
- [<span data-ttu-id="90051-142">Bir kullanılabilirlik kümesinde kullanılabilir sanal makine boyutlarını Listele</span><span class="sxs-lookup"><span data-stu-id="90051-142">List available virtual machine sizes in an availability set</span></span>](
https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-availability-set)

## <a name="acu"></a><span data-ttu-id="90051-143">ACU</span><span class="sxs-lookup"><span data-stu-id="90051-143">ACU</span></span>

<span data-ttu-id="90051-144">Hakkında daha fazla bilgi [Azure işlem birimleri (ACU)](acu.md) Azure SKU'ları üzerinde işlem performans karşılaştırmanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="90051-144">Learn more about how [Azure compute units (ACU)](acu.md) can help you compare compute performance across Azure SKUs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="90051-145">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="90051-145">Next steps</span></span>

<span data-ttu-id="90051-146">Kullanılabilen hello farklı VM boyutları hakkında daha fazla bilgi edinin:</span><span class="sxs-lookup"><span data-stu-id="90051-146">Learn more about hello different VM sizes that are available:</span></span>
- [<span data-ttu-id="90051-147">Genel amaçlı</span><span class="sxs-lookup"><span data-stu-id="90051-147">General purpose</span></span>](sizes-general.md)
- [<span data-ttu-id="90051-148">İşlem için iyileştirilmiş</span><span class="sxs-lookup"><span data-stu-id="90051-148">Compute optimized</span></span>](sizes-compute.md)
- [<span data-ttu-id="90051-149">Bellek için iyileştirilmiş</span><span class="sxs-lookup"><span data-stu-id="90051-149">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md)
- [<span data-ttu-id="90051-150">Depolama için iyileştirilmiş</span><span class="sxs-lookup"><span data-stu-id="90051-150">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md)
- [<span data-ttu-id="90051-151">GPU için iyileştirilmiş</span><span class="sxs-lookup"><span data-stu-id="90051-151">GPU optimized</span></span>](sizes-gpu.md)
- [<span data-ttu-id="90051-152">Yüksek performanslı işlem</span><span class="sxs-lookup"><span data-stu-id="90051-152">High performance compute</span></span>](sizes-hpc.md)



