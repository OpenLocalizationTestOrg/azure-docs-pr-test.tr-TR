---
title: "Hyper-V VM (VMM ile) çoğaltma tooAzure Azure Site Recovery ile çoğaltma ilkesi aaaSet | Microsoft Docs"
description: "Açıklar nasıl tooset (VMM ile) Hyper-V VM çoğaltma tooAzure Azure Site Recovery ile çoğaltma ilkesi"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: ee808b20-324b-4198-b831-edb65b95e8b7
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: e1579fde559ca34eca19a01e740fec28a0df2f9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="step-10-set-up-a-replication-policy-for-hyper-v-vm-replication-with-vmm-tooazure"></a>10. adım: Hyper-V VM çoğaltma (VMM ile) tooAzure için bir çoğaltma ilkesi ayarlama


Ayarladıktan sonra [ağ eşlemesi](vmm-to-azure-walkthrough-network-mapping.md), bir çoğaltma ilkesi T\tooreplicate şirket içi System Center Virtual Machine Manager (VMM) Bulutlar tooAzure yönetilen Hyper-V sanal makinelerin Bu makale tooconfigure kullanın, hello kullanma[ Azure Site Recovery](site-recovery-overview.md) hello Azure portal hizmeti.

Bu makaleyi okuduktan sonra tüm yorumlar hello altındaki ya da hello sonrası [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).



## <a name="create-a-policy"></a>Bir ilke oluşturun

1. Yeni bir çoğaltma ilkesi toocreate tıklatın **altyapıyı hazırlama** > **çoğaltma ayarları** > **+ oluştur ve ilişkilendir**.

    ![Ağ](./media/vmm-to-azure-walkthrough-replication/gs-replication.png)
2. **İlke oluştur ve ilişkilendir** bölümünde bir ilke adı belirtin.
3. İçinde **kopyalama sıklığı**, ne sıklıkta hello ilk çoğaltma (her 30 saniyede, 5 veya 15 dakika) sonra tooreplicate değişim verileri istediğinizi belirtin.

    > [!NOTE]
    >  30 ikinci sıklığı toopremium depolama çoğaltırken desteklenmiyor. Merhaba sınırlaması, premium depolama birimi tarafından desteklenen hello anlık görüntü sayısı blob (100) başına tarafından belirlenir. [Daha fazla bilgi](../storage/common/storage-premium-storage.md#snapshots-and-copy-blob)

4. İçinde **kurtarma noktası bekletme**, saat cinsinden ne kadar süreyle hello bekletme penceresi belirtin her kurtarma noktası için olabilir. Korumalı makineler olabilir bir pencere içinde tooany noktası kurtarıldı.
5. **Uygulamayla tutarlı anlık görüntü sıklığı** kısmında, uygulamayla tutarlı anlık görüntüleri içeren kurtarma noktasının hangi sıklıkta oluşturulacağını (1-12 saat) belirtin. Hyper-V iki çeşit anlık kullanır — bir artımlı hello tüm sanal makinenin anlık görüntüsünü sunan standart anlık görüntü ve zaman içinde nokta verilerin bir anlık görüntüsünü hello uygulama hello sanal makine içinde geçen uygulama tutarlı bir anlık görüntü. Uygulamayla tutarlı anlık görüntüleri hello anlık görüntü alınırken uygulamaların tutarlı bir durumda olan birim gölge kopyası hizmeti (VSS) tooensure kullanın. Uygulamayla tutarlı anlık görüntüleri etkinleştirirseniz, kaynak sanal makinelerde çalışan uygulamaların hello performansını etkiler unutmayın. Ayarladığınız hello değeri, yapılandırdığınız ilave kurtarma noktası hello sayısından daha az olduğundan emin olun.
6. İçinde **ilk çoğaltma başlangıç zamanı**, ne zaman toostart hello ilk çoğaltma gösterir. Merhaba çoğaltmanın internet bant genişliğiniz tooschedule isteyebilirsiniz şekilde meşgul saatleriniz dışında.
7. İçinde **Azure'da depolanan verileri şifrele**, belirtin olup olmadığını tooencrypt Azure depolama alanında rest veri. Daha sonra, **Tamam**'a tıklayın.

    ![Çoğaltma ilkesi](./media/vmm-to-azure-walkthrough-replication/gs-replication2.png)
8. Yeni bir ilke oluşturduğunuzda, otomatik olarak hello VMM Bulutu ile ilişkili. **Tamam** düğmesine tıklayın. Bu çoğaltma ilkesini ek VMM Bulutları (ve bunlara hello VM'ler) ilişkilendirebilirsiniz **çoğaltma** > ilke adı > **VMM Bulutu ile ilişkilendir**.

    ![Çoğaltma ilkesi](./media/vmm-to-azure-walkthrough-replication/policy-associate.png)



## <a name="next-steps"></a>Sonraki adımlar

Çok Git[adım 11: çoğaltmasını etkinleştir](vmm-to-azure-walkthrough-enable-replication.md)
