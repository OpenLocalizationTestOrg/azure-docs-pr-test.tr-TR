---
title: "Hyper-V VM (System Center VMM olmadan) çoğaltma tooAzure Azure Site Recovery ile çoğaltma ilkesi aaaSet | Microsoft Docs"
description: "Hyper-V sanal makineleri tooAzure depolama çoğaltırken çoğaltma ilkesi tooset gereken hello adımları özetler"
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 1777e0eb-accb-42b5-a747-11272e131a52
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/22/2017
ms.author: raynew
ms.openlocfilehash: 4bd7161f4a0f015da0ecf595fbc6861ede5d68b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="step-9-set-up-a-replication-policy-for-hyper-v-vm-replication-tooazure"></a>9. adım: Hyper-V VM çoğaltma tooAzure için bir çoğaltma ilkesi ayarlayın

Bu makalede nasıl hello kullanarak Hyper-V sanal makineleri tooAzure (System Center VMM olmadan) çoğaltırken çoğaltma ilkesi tooset [Azure Site Recovery](site-recovery-overview.md) hello Azure portal hizmeti.


POST açıklamaları ve soruları hello altındaki bu makalenin veya hello [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="about-snapshots"></a>Anlık görüntüler hakkında

Hyper-V iki çeşit anlık kullanır — bir artımlı hello tüm sanal makinenin anlık görüntüsünü sunan standart anlık görüntü ve zaman içinde nokta verilerin bir anlık görüntüsünü hello uygulama hello sanal makine içinde geçen uygulama tutarlı bir anlık görüntü.
    - Uygulamayla tutarlı anlık görüntüleri hello anlık görüntü alınırken uygulamaların tutarlı bir durumda olan birim gölge kopyası hizmeti (VSS) tooensure kullanın.
    - Uygulamayla tutarlı anlık görüntüleri etkinleştirirseniz kaynak sanal makinelerde çalışan uygulamaların hello performansını etkiler. Ayarladığınız hello değeri, yapılandırdığınız ilave kurtarma noktası hello sayısından daha az olduğundan emin olun.

## <a name="set-up-a-replication-policy"></a>Bir çoğaltma ilkesini ayarlayın

1. Yeni bir çoğaltma ilkesi toocreate tıklatın **altyapıyı hazırlama** > **çoğaltma ayarları** > **+ oluştur ve ilişkilendir**.

    ![Ağ](./media/hyper-v-site-walkthrough-replication/gs-replication.png)
2. **İlke oluştur ve ilişkilendir** bölümünde bir ilke adı belirtin.
3. İçinde **kopyalama sıklığı**, ne sıklıkta hello ilk çoğaltma (her 30 saniyede, 5 veya 15 dakika) sonra tooreplicate değişim verileri istediğinizi belirtin.

    > [!NOTE]
    > 30 ikinci sıklığı toopremium depolama çoğaltırken desteklenmiyor. Merhaba sınırlaması, premium depolama birimi tarafından desteklenen hello anlık görüntü sayısı blob (100) başına tarafından belirlenir. [Daha fazla bilgi edinin](../storage/common/storage-premium-storage.md#snapshots-and-copy-blob).

4. İçinde **kurtarma noktası bekletme**, saat cinsinden süreyi belirtin hello bekletme penceresi olduğu için her kurtarma noktası. Sanal makineleri olabilir bir pencere içinde tooany noktası kurtarıldı.
5. İçinde **uygulamayla tutarlı anlık görüntü sıklığı**, ne sıklıkla (1-12 saat) içeren uygulamayla tutarlı anlık görüntüleri kurtarma noktalarını belirtin oluşturulur.
6. İçinde **ilk çoğaltma başlangıç zamanı**, ne zaman toostart hello ilk çoğaltma belirtin. Merhaba çoğaltmanın internet bant genişliğiniz tooschedule isteyebilirsiniz şekilde meşgul saatleriniz dışında. Daha sonra, **Tamam**'a tıklayın.

    ![Çoğaltma ilkesi](./media/hyper-v-site-walkthrough-replication/gs-replication2.png)

Yeni bir ilke oluşturduğunuzda, otomatik olarak hello Hyper-V sitesi ile ilişkili. Birden fazla çoğaltma ilkesi ile bir Hyper-V sitesi (ve hello VM'ler da) ilişkilendirebilirsiniz **çoğaltma** > ilke adı > **ilişkilendirmek Hyper-V sitesi**.



## <a name="next-steps"></a>Sonraki adımlar

Çok Git[adım 10: çoğaltmasını etkinleştir](hyper-v-site-walkthrough-enable-replication.md)
