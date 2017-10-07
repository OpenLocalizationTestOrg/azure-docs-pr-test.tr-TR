---
title: "aaaLinux VM boyutları Azure'da | Microsoft Docs"
description: "Farklı boyutlarda Hello Azure Linux sanal makineler için kullanılabilir listeler."
services: virtual-machines-linux
documentationcenter: 
author: jonbeck7
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: da681171-f045-4c80-a5a9-d8bd47964673
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 07/28/2017
ms.author: jonbeck
ms.openlocfilehash: 56cbe0a0d7d34def07636edba74c4c699e336012
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="sizes-for-linux-virtual-machines-in-azure"></a><span data-ttu-id="b398a-103">Azure'daki Linux sanal makineler için Boyutlar</span><span class="sxs-lookup"><span data-stu-id="b398a-103">Sizes for Linux virtual machines in Azure</span></span>
<span data-ttu-id="b398a-104">Bu makalede hello kullanılabilir boyutları ve Linux uygulamaları ve iş yüklerini toorun kullanabileceğiniz Azure sanal makineler için başlangıç seçenekleri.</span><span class="sxs-lookup"><span data-stu-id="b398a-104">This article describes hello available sizes and options for hello Azure virtual machines you can use toorun your Linux apps and workloads.</span></span> <span data-ttu-id="b398a-105">Bu kaynaklar toouse planlaması yaparken de dağıtım konuları toobe farkında sağlar.</span><span class="sxs-lookup"><span data-stu-id="b398a-105">It also provides deployment considerations toobe aware of when you're planning toouse these resources.</span></span> <span data-ttu-id="b398a-106">Bu makalede ayrıca kullanılabilir [Windows sanal makineleri](../windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b398a-106">This article is also available for [Windows virtual machines](../windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


| <span data-ttu-id="b398a-107">Tür</span><span class="sxs-lookup"><span data-stu-id="b398a-107">Type</span></span>                     | <span data-ttu-id="b398a-108">Boyutlar</span><span class="sxs-lookup"><span data-stu-id="b398a-108">Sizes</span></span>           |    <span data-ttu-id="b398a-109">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b398a-109">Description</span></span>       |
|--------------------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------|
| [<span data-ttu-id="b398a-110">Genel amaçlı</span><span class="sxs-lookup"><span data-stu-id="b398a-110">General purpose</span></span>](sizes-general.md)          | <span data-ttu-id="b398a-111">Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0-7</span><span class="sxs-lookup"><span data-stu-id="b398a-111">Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0-7,</span></span>  | <span data-ttu-id="b398a-112">Dengeli CPU/bellek oranı.</span><span class="sxs-lookup"><span data-stu-id="b398a-112">Balanced CPU-to-memory ratio.</span></span> <span data-ttu-id="b398a-113">Test ve geliştirme, küçük toomedium veritabanları ve düşük toomedium trafiği web sunucuları için idealdir.</span><span class="sxs-lookup"><span data-stu-id="b398a-113">Ideal for testing and development, small toomedium databases, and low toomedium traffic web servers.</span></span> |
| [<span data-ttu-id="b398a-114">İşlem için iyileştirilmiş</span><span class="sxs-lookup"><span data-stu-id="b398a-114">Compute optimized</span></span>](sizes-compute.md)        | <span data-ttu-id="b398a-115">FS, F</span><span class="sxs-lookup"><span data-stu-id="b398a-115">Fs, F</span></span>             | <span data-ttu-id="b398a-116">Yüksek CPU/bellek oranı.</span><span class="sxs-lookup"><span data-stu-id="b398a-116">High CPU-to-memory ratio.</span></span> <span data-ttu-id="b398a-117">Orta düzey trafik web sunucuları, ağ cihazları, banyo işlemleri ve uygulama sunucuları için iyidir.</span><span class="sxs-lookup"><span data-stu-id="b398a-117">Good for medium traffic web servers, network appliances, bath processes, and application servers.</span></span>        |
| [<span data-ttu-id="b398a-118">Bellek için iyileştirilmiş</span><span class="sxs-lookup"><span data-stu-id="b398a-118">Memory optimized</span></span>](sizes-memory.md)         | <span data-ttu-id="b398a-119">Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D</span><span class="sxs-lookup"><span data-stu-id="b398a-119">Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D</span></span>   | <span data-ttu-id="b398a-120">Yüksek bellek CPU oranı.</span><span class="sxs-lookup"><span data-stu-id="b398a-120">High memory-to-CPU ratio.</span></span> <span data-ttu-id="b398a-121">İlişkisel veritabanı sunucuları, Orta toolarge önbellekleri ve bellek içi analizi için mükemmel.</span><span class="sxs-lookup"><span data-stu-id="b398a-121">Great for relational database servers, medium toolarge caches, and in-memory analytics.</span></span>                 |
| [<span data-ttu-id="b398a-122">Depolama için iyileştirilmiş</span><span class="sxs-lookup"><span data-stu-id="b398a-122">Storage optimized</span></span>](sizes-storage.md)        | <span data-ttu-id="b398a-123">Ls</span><span class="sxs-lookup"><span data-stu-id="b398a-123">Ls</span></span>                | <span data-ttu-id="b398a-124">Yüksek disk aktarım hızı ve GÇ.</span><span class="sxs-lookup"><span data-stu-id="b398a-124">High disk throughput and IO.</span></span> <span data-ttu-id="b398a-125">Büyük Veri, SQL ve NoSQL veritabanları için ideal.</span><span class="sxs-lookup"><span data-stu-id="b398a-125">Ideal for Big Data, SQL, and NoSQL databases.</span></span>                                                         |
| [<span data-ttu-id="b398a-126">GPU</span><span class="sxs-lookup"><span data-stu-id="b398a-126">GPU</span></span>](sizes-gpu.md)            | <span data-ttu-id="b398a-127">NV, NC</span><span class="sxs-lookup"><span data-stu-id="b398a-127">NV, NC</span></span>            | <span data-ttu-id="b398a-128">Yoğun Grafik işleme ve video düzenleme için hedeflenen özelleştirilmiş sanal makineler.</span><span class="sxs-lookup"><span data-stu-id="b398a-128">Specialized virtual machines targeted for heavy graphic rendering and video editing.</span></span> <span data-ttu-id="b398a-129">Tek veya birden çok GPU ile kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="b398a-129">Available with single or multiple GPUs.</span></span>       |
| [<span data-ttu-id="b398a-130">Yüksek performanslı işlem</span><span class="sxs-lookup"><span data-stu-id="b398a-130">High performance compute</span></span>](sizes-hpc.md) | <span data-ttu-id="b398a-131">H, A8-11</span><span class="sxs-lookup"><span data-stu-id="b398a-131">H, A8-11</span></span>          | <span data-ttu-id="b398a-132">İşleme düzeyi yüksek olan isteğe bağlı ağ arabirimleri (RDMA) içeren sanal makineler, şimdiye kadarki en hızlı ve en güçlü CPU ile sunuluyor.</span><span class="sxs-lookup"><span data-stu-id="b398a-132">Our fastest and most powerful CPU virtual machines with optional high-throughput network interfaces (RDMA).</span></span> 

<br>

- <span data-ttu-id="b398a-133">Merhaba çeşitli boyutlarda fiyatlandırma hakkında daha fazla bilgi için bkz: [sanal makineler fiyatlandırma](https://azure.microsoft.com/pricing/details/virtual-machines/#Linux).</span><span class="sxs-lookup"><span data-stu-id="b398a-133">For information about pricing of hello various sizes, see [Virtual Machines Pricing](https://azure.microsoft.com/pricing/details/virtual-machines/#Linux).</span></span> 
- <span data-ttu-id="b398a-134">VM boyutları Azure bölgelerindeki kullanılabilirlik için bkz: [bölgeye göre ürünleri](https://azure.microsoft.com/regions/services/).</span><span class="sxs-lookup"><span data-stu-id="b398a-134">For availability of VM sizes in Azure regions, see [Products available by region](https://azure.microsoft.com/regions/services/).</span></span>
- <span data-ttu-id="b398a-135">Azure vm'lerinde toosee genel sınırları bkz [Azure aboneliği ve hizmet sınırları, kotaları ve kısıtlamaları](../../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="b398a-135">toosee general limits on Azure VMs, see [Azure subscription and service limits, quotas, and constraints](../../azure-subscription-service-limits.md).</span></span>
- <span data-ttu-id="b398a-136">Hakkında daha fazla bilgi [Azure işlem birimleri (ACU)](../windows/acu.md) Azure SKU'ları üzerinde işlem performans karşılaştırmanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="b398a-136">Learn more about how [Azure compute units (ACU)](../windows/acu.md) can help you compare compute performance across Azure SKUs.</span></span>


## <a name="rest-api"></a><span data-ttu-id="b398a-137">REST API'si</span><span class="sxs-lookup"><span data-stu-id="b398a-137">Rest API</span></span>

<span data-ttu-id="b398a-138">VM boyutları için hello REST API tooquery kullanma hakkında daha fazla bilgi için hello aşağıdakilere bakın:</span><span class="sxs-lookup"><span data-stu-id="b398a-138">For information on using hello REST API tooquery for VM sizes, see hello following:</span></span>

- [<span data-ttu-id="b398a-139">Yeniden boyutlandırma için kullanılabilir sanal makine boyutlarını Listele</span><span class="sxs-lookup"><span data-stu-id="b398a-139">List available virtual machine sizes for resizing</span></span>](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-for-resizing)
- [<span data-ttu-id="b398a-140">Bir abonelik için kullanılabilir sanal makine boyutlarını Listele</span><span class="sxs-lookup"><span data-stu-id="b398a-140">List available virtual machine sizes for a subscription</span></span>](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-region)
- [<span data-ttu-id="b398a-141">Bir kullanılabilirlik kümesinde kullanılabilir sanal makine boyutlarını Listele</span><span class="sxs-lookup"><span data-stu-id="b398a-141">List available virtual machine sizes in an availability set</span></span>](
https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-availability-set)

## <a name="acu"></a><span data-ttu-id="b398a-142">ACU</span><span class="sxs-lookup"><span data-stu-id="b398a-142">ACU</span></span>

<span data-ttu-id="b398a-143">Hakkında daha fazla bilgi [Azure işlem birimleri (ACU)](acu.md) Azure SKU'ları üzerinde işlem performans karşılaştırmanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="b398a-143">Learn more about how [Azure compute units (ACU)](acu.md) can help you compare compute performance across Azure SKUs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b398a-144">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b398a-144">Next steps</span></span>

<span data-ttu-id="b398a-145">Kullanılabilen hello farklı VM boyutları hakkında daha fazla bilgi edinin:</span><span class="sxs-lookup"><span data-stu-id="b398a-145">Learn more about hello different VM sizes that are available:</span></span>
- [<span data-ttu-id="b398a-146">Genel amaçlı</span><span class="sxs-lookup"><span data-stu-id="b398a-146">General purpose</span></span>](sizes-general.md)
- [<span data-ttu-id="b398a-147">İşlem için iyileştirilmiş</span><span class="sxs-lookup"><span data-stu-id="b398a-147">Compute optimized</span></span>](sizes-compute.md)
- [<span data-ttu-id="b398a-148">Bellek için iyileştirilmiş</span><span class="sxs-lookup"><span data-stu-id="b398a-148">Memory optimized</span></span>](sizes-memory.md)
- [<span data-ttu-id="b398a-149">Depolama için iyileştirilmiş</span><span class="sxs-lookup"><span data-stu-id="b398a-149">Storage optimized</span></span>](sizes-storage.md)
- [<span data-ttu-id="b398a-150">GPU</span><span class="sxs-lookup"><span data-stu-id="b398a-150">GPU</span></span>](sizes-gpu.md)
- [<span data-ttu-id="b398a-151">Yüksek performanslı işlem</span><span class="sxs-lookup"><span data-stu-id="b398a-151">High performance compute</span></span>](sizes-hpc.md)



