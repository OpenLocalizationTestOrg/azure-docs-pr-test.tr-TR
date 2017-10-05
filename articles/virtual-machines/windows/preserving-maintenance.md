---
title: "Azure'da Windows sanal makineleri için bakım koruma VM | Microsoft Docs"
description: "VM belleği güncelleştirmeleri koruma yerinde geçiş."
services: virtual-machines-windows
documentationcenter: 
author: zivr
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
ms.author: zivr
ms.openlocfilehash: 8888bafbc3aba24168312b611a9b4fbde25f376d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="vm-preserving-maintenance-with-in-place-vm-migration"></a><span data-ttu-id="64047-103">VM bakım yerinde VM geçiş ile koruma</span><span class="sxs-lookup"><span data-stu-id="64047-103">VM preserving maintenance with In-place VM migration</span></span>

<span data-ttu-id="64047-104">Güncelleştirmelerin çoğunun olmakla birlikte barındırılan sanal makineleri üzerinde etkisi, burada bileşenleri veya hizmetleri için güncelleştirmeleri (tam yeniden başlatmadan sanal makinenin) sanal makineleri çalıştırmak için en az girişim sonucunda durumlar vardır.</span><span class="sxs-lookup"><span data-stu-id="64047-104">While the majority of updates have no impact to hosted VMs, there are cases where updates to components or services result in minimal interference to running VMs (without a full reboot of the virtual machine).</span></span>

<span data-ttu-id="64047-105">Bu güncelleştirmeleri "güncelleştirme bellek koruma" olarak da bilinir yerinde dinamik geçiş olanağını sunar teknolojisi ile yapılır.</span><span class="sxs-lookup"><span data-stu-id="64047-105">These updates are accomplished with technology that enables in-place live migration, also called "memory-preserving update".</span></span> <span data-ttu-id="64047-106">Ana bilgisayar güncelleştirirken, sanal makine barındırma ortamı (örneğin temel işletim sistemi) gerekli güncelleştirmeleri ve düzeltme eklerini uygularken RAM bellek koruma "Duraklatıldı" bir duruma yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="64047-106">When updating the host, the virtual machine is placed into a “paused” state, preserving the memory in RAM, while the hosting environment (e.g. the underlying operating system) applies the necessary updates and patches.</span></span>
<span data-ttu-id="64047-107">Sanal makine ardından duraklatıldıktan sonra 30 saniye içinde devam ettirilir.</span><span class="sxs-lookup"><span data-stu-id="64047-107">The virtual machine is then resumed within 30 seconds of being paused.</span></span>
<span data-ttu-id="64047-108">Devam ettirildikten sonra, sanal makinenin saati otomatik olarak eşitlenir.</span><span class="sxs-lookup"><span data-stu-id="64047-108">After resuming, the clock of the virtual machine is automatically synchronized.</span></span>

<span data-ttu-id="64047-109">Tüm güncelleştirmeler bu mekanizma kullanılarak dağıtılamaz, ancak kısa duraklatma süresi düşünüldüğünde, güncelleştirmelerin bu şekilde dağıtılmasıyla sanal makinelere etki büyük ölçüde azaltılır.</span><span class="sxs-lookup"><span data-stu-id="64047-109">Not all updates can be deployed by using this mechanism, but given the short pause period, deploying updates in this way greatly reduces impact to virtual machines.</span></span>

<span data-ttu-id="64047-110">Çok örnekli (VM'ler bir kullanılabilirlik kümesinde) uygulanan bir güncelleştirme etki alanı aynı anda güncelleştirmelerdir.</span><span class="sxs-lookup"><span data-stu-id="64047-110">Multi-instance updates (VMs in an availability set) are applied one update domain at a time.</span></span>

<span data-ttu-id="64047-111">Bazı uygulamalar, bu güncelleştirmeleri diğerlerinden daha fazla tarafından etkilenebilir.</span><span class="sxs-lookup"><span data-stu-id="64047-111">Some applications may be impacted by these updates more than others.</span></span> <span data-ttu-id="64047-112">Gerçek zamanlı Olay işleme, akış veya kod veya yüksek verimlilik senaryoları, ağ gerçekleştiren uygulamaları Örneğin, 30 saniyelik duraklamalar tolerans için tasarlanmamış olabilir.</span><span class="sxs-lookup"><span data-stu-id="64047-112">Applications that perform real-time event processing, media streaming or transcoding, or high throughput networking scenarios, for example, may not be designed to tolerate a 30 second pause.</span></span> <span data-ttu-id="64047-113">Bir sanal makinede çalışan uygulamalar, gelecek güncelleştirmeleri hakkında arayarak bulabilir [zamanlanmış olayları](../virtual-machines-scheduled-events.md) API'si [Azure meta veri hizmeti](../virtual-machines-instancemetadataservice-overview.md).</span><span class="sxs-lookup"><span data-stu-id="64047-113">Applications running in a virtual machine can learn about upcoming updates by calling the [Scheduled Events](../virtual-machines-scheduled-events.md) API of the [Azure Metadata Service](../virtual-machines-instancemetadataservice-overview.md).</span></span>
