---
title: "VMware VM çoğaltma tooAzure Azure Site Recovery ile çoğaltma ilkesi aaaSet | Microsoft Docs"
description: "Çoğaltma İlkesi tooset VMware Vm'lerini tooAzure depolama çoğaltırken gereken hello adımları özetler"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d7874bd8-6626-4668-9ec9-dbd2d26f8f81
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 12870f3f98a4dd412221b817581403cd4bf7a76d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="step-9-set-up-a-replication-policy-for-vmware-vm-replication-tooazure"></a>9. adım: VMware VM çoğaltma tooAzure için bir çoğaltma ilkesi ayarlama


Bu makalede nasıl hello kullanarak VMware sanal makinelerini tooAzure çoğaltırken çoğaltma ilkesi tooset [Azure Site Recovery](site-recovery-overview.md) hello Azure portal hizmeti.


POST açıklamaları ve soruları hello altındaki bu makalenin veya hello [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="configure-a-policy"></a>Bir ilke yapılandırın

Başlamadan önce hızlı bir video genel bakış alın:
> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video2-vCenter-Server-Discovery-and-Replication-Policy/player]

1. Yeni bir çoğaltma ilkesi toocreate tıklatın **Site Recovery altyapısı** > **çoğaltma ilkeleri** > **+ Çoğaltma İlkesi**.
2. İçinde **çoğaltma ilkesi oluşturun**, bir ilke adı belirtin.
3. İçinde **RPO eşik**, hello RPO sınırını belirtin. Bu değer, ne sıklıkta belirtir veri kurtarma noktaları oluşturulur. Sürekli çoğaltma bu sınırı aşarsa bir uyarı üretilir.
4. İçinde **kurtarma noktası bekletme**, ne kadar süre (saat olarak) belirtin hello bekletme penceresi olduğu için her kurtarma noktası. Çoğaltılan VM'ler olabilir bir pencerede tooany noktası kurtarıldı. Saat bekletme makineler için desteklenen too24 yukarı toopremium depolama ile standart depolama için 72 saat çoğaltılan.
5. İçinde **uygulamayla tutarlı anlık görüntü sıklığı**, belirtin ne sıklıkta (dakika cinsinden) uygulamayla tutarlı anlık görüntüleri içeren kurtarma noktaları oluşturulur. Tıklatın **Tamam** toocreate hello ilkesi.

    ![Çoğaltma ilkesi](./media/vmware-walkthrough-replication/gs-replication2.png)
8. Yeni bir ilke oluşturduğunuzda, otomatik olarak hello yapılandırma sunucusu ile ilişkili. Varsayılan olarak, eşleşen bir ilkesi yeniden çalışma için otomatik olarak oluşturulur. Örneğin, hello çoğaltma ilkesi ise **rep İlkesi** hello geri dönme ilkesini sonra **rep İlkesi yeniden**. Bir azure'dan başlatana kadar bu ilkeyi kullanılmaz.

## <a name="next-steps"></a>Sonraki adımlar

Çok Git[adım 10: hello Mobility hizmetini yükleme](vmware-walkthrough-install-mobility.md)
