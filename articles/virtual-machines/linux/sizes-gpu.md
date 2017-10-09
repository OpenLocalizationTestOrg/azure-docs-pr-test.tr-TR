---
title: "aaaAzure Linux VM boyutları - GPU | Microsoft Docs"
description: "Merhaba farklı en iyi duruma getirilmiş GPU boyutlarını Azure Linux sanal makineler için kullanılabilir listeler."
services: virtual-machines-linux
documentationcenter: 
author: jonbeck7
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 07/28/2017
ms.author: jonbeck
ms.openlocfilehash: e98f720499be37df4048aeb513aa4f6b187b7335
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="gpu-linux-vm-sizes"></a><span data-ttu-id="1e665-103">GPU Linux VM boyutları</span><span class="sxs-lookup"><span data-stu-id="1e665-103">GPU Linux VM sizes</span></span>

[!INCLUDE [virtual-machines-common-sizes-gpu](../../../includes/virtual-machines-common-sizes-gpu.md)]


[!INCLUDE [virtual-machines-common-sizes-table-defs](../../../includes/virtual-machines-common-sizes-table-defs.md)]

[!INCLUDE [virtual-machines-n-series-linux-support](../../../includes/virtual-machines-n-series-linux-support.md)]

<span data-ttu-id="1e665-104">Sürücü yükleme ve doğrulama adımları için bkz [N-serisi sürücü kurulumu Linux için](n-series-driver-setup.md).</span><span class="sxs-lookup"><span data-stu-id="1e665-104">For driver installation and verification steps, see [N-series driver setup for Linux](n-series-driver-setup.md).</span></span>

[!INCLUDE [virtual-machines-n-series-considerations](../../../includes/virtual-machines-n-series-considerations.md)]

* <span data-ttu-id="1e665-105">Yüklemenizi öneririz yok X sunucu ya da hello nouveau sürücü Ubuntu NC Vm'lerinde kullanan diğer sistemler.</span><span class="sxs-lookup"><span data-stu-id="1e665-105">We don't recommend installing X server or other systems that use hello nouveau driver on Ubuntu NC VMs.</span></span> <span data-ttu-id="1e665-106">NVIDIA GPU sürücüleri yüklemeden önce toodisable hello nouveau sürücüsü gerekir.</span><span class="sxs-lookup"><span data-stu-id="1e665-106">Before installing NVIDIA GPU drivers, you need toodisable hello nouveau driver.</span></span>  

## <a name="other-sizes"></a><span data-ttu-id="1e665-107">Diğer boyutlara</span><span class="sxs-lookup"><span data-stu-id="1e665-107">Other sizes</span></span>
- [<span data-ttu-id="1e665-108">Genel amaçlı</span><span class="sxs-lookup"><span data-stu-id="1e665-108">General purpose</span></span>](sizes-general.md)
- [<span data-ttu-id="1e665-109">İşlem için iyileştirilmiş</span><span class="sxs-lookup"><span data-stu-id="1e665-109">Compute optimized</span></span>](sizes-compute.md)
- [<span data-ttu-id="1e665-110">Bellek için iyileştirilmiş</span><span class="sxs-lookup"><span data-stu-id="1e665-110">Memory optimized</span></span>](sizes-memory.md)
- [<span data-ttu-id="1e665-111">Depolama için iyileştirilmiş</span><span class="sxs-lookup"><span data-stu-id="1e665-111">Storage optimized</span></span>](sizes-storage.md)
- [<span data-ttu-id="1e665-112">Yüksek performanslı işlem</span><span class="sxs-lookup"><span data-stu-id="1e665-112">High performance compute</span></span>](sizes-hpc.md)

## <a name="next-steps"></a><span data-ttu-id="1e665-113">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1e665-113">Next steps</span></span>
<span data-ttu-id="1e665-114">Hakkında daha fazla bilgi [Azure işlem birimleri (ACU)](acu.md) Azure SKU'ları üzerinde işlem performans karşılaştırmanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="1e665-114">Learn more about how [Azure compute units (ACU)](acu.md) can help you compare compute performance across Azure SKUs.</span></span>