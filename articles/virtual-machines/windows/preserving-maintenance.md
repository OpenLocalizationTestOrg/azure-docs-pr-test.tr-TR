---
title: "Windows Azure VM'ler için VM koruma bakım aaa | Microsoft Docs"
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
ms.openlocfilehash: b798f0afd9d8dc60ca8a78f7cc77435a0ddc76fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="vm-preserving-maintenance-with-in-place-vm-migration"></a>VM bakım yerinde VM geçiş ile koruma

Güncelleştirmeleri Hello çoğunluğu hiçbir etkisi toohosted VM'ler varken, burada güncelleştirmeleri toocomponents veya Hizmetleri (olmadan hello sanal makinenin tam yeniden başlatma) en az girişim toorunning VM'ler neden durumlar vardır.

Bu güncelleştirmeleri "güncelleştirme bellek koruma" olarak da bilinir yerinde dinamik geçiş olanağını sunar teknolojisi ile yapılır. Merhaba konak güncelleştirirken hello sanal makine barındırma ortamı (örneğin temel işletim sistemi) hello hello gerekli güncelleştirmeleri ve düzeltme eklerini uygularken RAM hello bellekte koruma "Duraklatıldı" bir duruma yerleştirilir.
Merhaba sanal makine ardından duraklatıldıktan sonra 30 saniye içinde devam ettirilir.
Durumdan çıktıktan sonra hello saati hello sanal makinenin otomatik olarak eşitlenir.

Tüm güncelleştirmeler bu mekanizma kullanılarak dağıtılabilir, ancak kısa duraklatma süresi güncelleştirmeleri bu şekilde büyük ölçüde dağıtma etkisi toovirtual makineler azaltır.

Çok örnekli (VM'ler bir kullanılabilirlik kümesinde) uygulanan bir güncelleştirme etki alanı aynı anda güncelleştirmelerdir.

Bazı uygulamalar, bu güncelleştirmeleri diğerlerinden daha fazla tarafından etkilenebilir. Örneğin, gerçek zamanlı Olay işleme, akış veya kod veya yüksek verimlilik senaryoları, ağ gerçekleştiren uygulamaları tasarlanmış tootolerate 30 saniyelik duraklamalar olmayabilir. Bir sanal makinede çalışan uygulamalar tarafından arama hello gelecek güncelleştirmeleri hakkında bulabilir [zamanlanmış olayları](../virtual-machines-scheduled-events.md) hello API [Azure meta veri hizmeti](../virtual-machines-instancemetadataservice-overview.md).
