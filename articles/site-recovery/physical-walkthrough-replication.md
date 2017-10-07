---
title: "fiziksel sunucu çoğaltma tooAzure Azure Site Recovery ile çoğaltma ilkesi aaaSet | Microsoft Docs"
description: "Çoğaltma fiziksel sunucuları tooAzure depolama hello Azure Site Recovery hizmetini kullanarak şirket içi olduğunda çoğaltma ilkesi tooset gereken hello adımları özetler"
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
ms.openlocfilehash: d6bdeeffc24ffc8eaba24311f7c76452edb65648
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="step-8-set-up-a-replication-policy-for-physical-server-replication-tooazure"></a>8. adım: fiziksel sunucu çoğaltma tooAzure için bir çoğaltma ilkesi ayarlama


Bu makalede nasıl hello kullanarak Windows/Linux fiziksel sunucuları tooAzure çoğaltırken çoğaltma ilkesi tooset [Azure Site Recovery](site-recovery-overview.md) hello Azure portal hizmeti.


POST açıklamaları ve soruları hello altındaki bu makalenin veya hello [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="configure-a-policy"></a>Bir ilke yapılandırın

1. Tıklatın **Site Recovery altyapısı** > **çoğaltma ilkeleri** > **+ Çoğaltma İlkesi**.
2. İçinde **çoğaltma ilkesi oluşturun**, bir ilke adı belirtin.
3. İçinde **RPO eşik**, hello RPO sınırını belirtin. Bu değer ne sıklıkta gösterir veri kurtarma noktaları oluşturulur. Sürekli çoğaltma bu sınırı aşarsa bir uyarı üretilir.
4. İçinde **kurtarma noktası bekletme**, ne kadar süre (saat olarak) belirtin hello bekletme penceresi olduğu için her kurtarma noktası. Çoğaltılan VM'ler olabilir bir pencerede tooany noktası kurtarıldı. Saat bekletme makineler için desteklenen too24 yukarı toopremium depolama ile standart depolama için 72 saat çoğaltılan.
5. İçinde **uygulamayla tutarlı anlık görüntü sıklığı**, belirtin ne sıklıkta (dakika cinsinden) uygulamayla tutarlı anlık görüntüleri içeren kurtarma noktaları oluşturulur. Tıklatın **Tamam** toocreate hello ilkesi.

    ![Çoğaltma ilkesi](./media/physical-walkthrough-replication/gs-replication2.png)
8. Yeni bir ilke oluşturduğunuzda, otomatik olarak hello yapılandırma sunucusu ile ilişkili. Varsayılan olarak, eşleşen bir ilkesi yeniden çalışma için otomatik olarak oluşturulur. Örneğin, hello çoğaltma ilkesi ise **rep İlkesi** hello geri dönme ilkesini sonra **rep İlkesi yeniden**. Bir azure'dan başlatana kadar bu ilkeyi kullanılmaz.

## <a name="next-steps"></a>Sonraki adımlar

Çok Git[adım 9: hello Mobility hizmetini yükleme](physical-walkthrough-install-mobility.md)
