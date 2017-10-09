---
title: "azure'da Windows sanal makineleri için bakım koruma aaaVM | Microsoft Docs"
description: "VM belleği güncelleştirmeleri koruma yerinde geçiş."
services: virtual-machines-windows
documentationcenter: 
author: 
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/27/2017
ms.author: 
ms.openlocfilehash: 544a2dcca52bb3ac51d341bceaf4ba3e7c71fd82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="vm-preserving-maintenance-in-place-vm-migration"></a><span data-ttu-id="869c7-103">VM Bakım (yerinde VM geçiş) koruma</span><span class="sxs-lookup"><span data-stu-id="869c7-103">VM preserving maintenance (In-place VM migration)</span></span>

<span data-ttu-id="869c7-104">Güncelleştirmeleri Hello çoğunluğu hiçbir etkisi toohosted VM'ler varken, burada güncelleştirmeleri toocomponents veya Hizmetleri (olmadan hello sanal makinenin tam yeniden başlatma) en az girişim toorunning VM'ler neden durumlar vardır.</span><span class="sxs-lookup"><span data-stu-id="869c7-104">While hello majority of updates have no impact toohosted VMs, there are cases where updates toocomponents or services result in minimal interference toorunning VMs (without a full reboot of hello virtual machine).</span></span>

<span data-ttu-id="869c7-105">Bu güncelleştirmeleri "güncelleştirme bellek koruma" olarak da bilinir yerinde dinamik geçiş olanağını sunar teknolojisi ile yapılır.</span><span class="sxs-lookup"><span data-stu-id="869c7-105">These updates are accomplished with technology that enables in-place live migration, also called "memory-preserving update".</span></span> <span data-ttu-id="869c7-106">Merhaba konak güncelleştirirken hello sanal makine barındırma ortamı (örneğin temel işletim sistemi) hello hello gerekli güncelleştirmeleri ve düzeltme eklerini uygularken RAM hello bellekte koruma "Duraklatıldı" bir duruma yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="869c7-106">When updating hello host, hello virtual machine is placed into a “paused” state, preserving hello memory in RAM, while hello hosting environment (e.g. the underlying operating system) applies hello necessary updates and patches.</span></span>
<span data-ttu-id="869c7-107">Merhaba sanal makine ardından duraklatıldıktan sonra 30 saniye içinde devam ettirilir.</span><span class="sxs-lookup"><span data-stu-id="869c7-107">hello virtual machine is then resumed within 30 seconds of being paused.</span></span>
<span data-ttu-id="869c7-108">Durumdan çıktıktan sonra hello saati hello sanal makinenin otomatik olarak eşitlenir.</span><span class="sxs-lookup"><span data-stu-id="869c7-108">After resuming, hello clock of hello virtual machine is automatically synchronized.</span></span>

<span data-ttu-id="869c7-109">Tüm güncelleştirmeler bu mekanizma kullanılarak dağıtılabilir, ancak kısa duraklatma süresi güncelleştirmeleri bu şekilde büyük ölçüde dağıtma etkisi toovirtual makineler azaltır.</span><span class="sxs-lookup"><span data-stu-id="869c7-109">Not all updates can be deployed by using this mechanism, but given the short pause period, deploying updates in this way greatly reduces impact toovirtual machines.</span></span>

<span data-ttu-id="869c7-110">Çok örnekli (VM'ler bir kullanılabilirlik kümesinde) uygulanan bir güncelleştirme etki alanı aynı anda güncelleştirmelerdir.</span><span class="sxs-lookup"><span data-stu-id="869c7-110">Multi-instance updates (VMs in an availability set) are applied one update domain at a time.</span></span>

<span data-ttu-id="869c7-111">Bazı uygulamalar, bu güncelleştirmeleri diğerlerinden daha fazla tarafından etkilenebilir.</span><span class="sxs-lookup"><span data-stu-id="869c7-111">Some applications may be impacted by these updates more than others.</span></span> <span data-ttu-id="869c7-112">Örneğin, gerçek zamanlı Olay işleme, akış veya kod veya yüksek verimlilik senaryoları, ağ gerçekleştiren uygulamaları tasarlanmış tootolerate 30 saniyelik duraklamalar olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="869c7-112">Applications that perform real-time event processing, media streaming or transcoding, or high throughput networking scenarios, for example, may not be designed tootolerate a 30 second pause.</span></span> <span data-ttu-id="869c7-113">Bir sanal makinede çalışan uygulamalar tarafından arama hello gelecek güncelleştirmeleri hakkında bulabilir [zamanlanmış olayları](../virtual-machines-scheduled-events.md) hello API [Azure meta veri hizmeti](../virtual-machines-instancemetadataservice-overview.md).</span><span class="sxs-lookup"><span data-stu-id="869c7-113">Applications running in a virtual machine can learn about upcoming updates by calling hello [Scheduled Events](../virtual-machines-scheduled-events.md) API of hello [Azure Metadata Service](../virtual-machines-instancemetadataservice-overview.md).</span></span>
