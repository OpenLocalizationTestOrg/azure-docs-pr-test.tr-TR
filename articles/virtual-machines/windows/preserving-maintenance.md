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
# <a name="vm-preserving-maintenance-with-in-place-vm-migration"></a>VM bakım yerinde VM geçiş ile koruma

Güncelleştirmelerin çoğunun olmakla birlikte barındırılan sanal makineleri üzerinde etkisi, burada bileşenleri veya hizmetleri için güncelleştirmeleri (tam yeniden başlatmadan sanal makinenin) sanal makineleri çalıştırmak için en az girişim sonucunda durumlar vardır.

Bu güncelleştirmeleri "güncelleştirme bellek koruma" olarak da bilinir yerinde dinamik geçiş olanağını sunar teknolojisi ile yapılır. Ana bilgisayar güncelleştirirken, sanal makine barındırma ortamı (örneğin temel işletim sistemi) gerekli güncelleştirmeleri ve düzeltme eklerini uygularken RAM bellek koruma "Duraklatıldı" bir duruma yerleştirilir.
Sanal makine ardından duraklatıldıktan sonra 30 saniye içinde devam ettirilir.
Devam ettirildikten sonra, sanal makinenin saati otomatik olarak eşitlenir.

Tüm güncelleştirmeler bu mekanizma kullanılarak dağıtılamaz, ancak kısa duraklatma süresi düşünüldüğünde, güncelleştirmelerin bu şekilde dağıtılmasıyla sanal makinelere etki büyük ölçüde azaltılır.

Çok örnekli (VM'ler bir kullanılabilirlik kümesinde) uygulanan bir güncelleştirme etki alanı aynı anda güncelleştirmelerdir.

Bazı uygulamalar, bu güncelleştirmeleri diğerlerinden daha fazla tarafından etkilenebilir. Gerçek zamanlı Olay işleme, akış veya kod veya yüksek verimlilik senaryoları, ağ gerçekleştiren uygulamaları Örneğin, 30 saniyelik duraklamalar tolerans için tasarlanmamış olabilir. Bir sanal makinede çalışan uygulamalar, gelecek güncelleştirmeleri hakkında arayarak bulabilir [zamanlanmış olayları](../virtual-machines-scheduled-events.md) API'si [Azure meta veri hizmeti](../virtual-machines-instancemetadataservice-overview.md).
