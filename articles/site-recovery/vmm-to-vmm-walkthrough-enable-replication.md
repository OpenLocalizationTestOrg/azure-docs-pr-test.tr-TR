---
title: "aaaEnable Hyper-V çoğaltma tooa Azure Site Recovery ile ikincil site | Microsoft Docs"
description: "Nasıl tooenable çoğaltma Hyper-V sanal makinelerini tooa çoğaltmak için ikincil System Center VMM site Azure Site Recovery ile açıklar."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d8782d14-9fef-4396-8912-ff945efc851b
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: b4484e0118cb23f343187fe867d9795d30926baf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="step-9-enable-replication-tooa-secondary-site-for-hyper-v-vms"></a>9. adım: çoğaltma tooa ikincil site için Hyper-V sanal makineleri etkinleştirme


Bir çoğaltma ilkesi ayarladıktan sonra bu makale tooenable çoğaltma tooa ikincil System Center Virtual Machine Manager (VMM) site içi Hyper-V sanal kullanarak makineler için (VM) kullanmanız [Azure Site Recovery](site-recovery-overview.md).

Bu makaleyi okuduktan sonra tüm yorumlar hello altındaki ya da hello sonrası [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).



## <a name="select-vms-tooreplicate"></a>Sanal makineleri tooreplicate seçin

1. **2. Adım: Uygulama çoğaltma** > **Kaynak** seçeneklerine tıklayın. 

    ![Çoğaltmayı etkinleştirme](./media/vmm-to-vmm-walkthrough-enable-replication/enable-replication1.png)

2. İçinde **kaynak**hello VMM sunucusunu seçin ve hello hangi hello tooreplicate istediğiniz Hyper-V konaklarının bulunduğu bulut. Daha sonra, **Tamam**'a tıklayın.

    ![Çoğaltmayı etkinleştirme](./media/vmm-to-vmm-walkthrough-enable-replication/enable-replication2.png)
3. İçinde **hedef**, hello ikincil VMM sunucusu ve bulut doğrulayın.
4. İçinde **sanal makineleri**, tooprotect hello listeden istediğiniz hello VM'ler seçin.

    ![Sanal makine korumasını etkinleştirme](./media/vmm-to-vmm-walkthrough-enable-replication/enable-replication5.png)

Merhaba ilerlemesini izleyebilirsiniz **korumayı etkinleştir** eylemde **işleri** > **Site Recovery işleri**. Merhaba sonra **korumayı Sonlandır** işi tamamlandığında, hello ilk çoğaltma tamamlandıktan ve hello sanal makine yük devretme için hazır.

Şunlara dikkat edin:

- Merhaba VMM konsolunda sanal makineler için korumayı etkinleştirebilirsiniz. Tıklatın **korumayı etkinleştir** hello sanal makine Özellikleri'nde hello araç çubuğunda > **Azure Site Recovery** sekmesi.
- Çoğaltma etkinleştirdikten sonra hello VM özelliklerini görüntüleyebilir, **çoğaltılan öğeler**. Merhaba üzerinde **Essentials** panoyu hello çoğaltma ilkesi hello VM ve durumu hakkındaki bilgileri görebilirsiniz. Tıklatın **özellikleri** daha fazla ayrıntı için.

## <a name="onboard-existing-vms"></a>Yerleşik VM'ler

Hyper-V çoğaltma ile çoğaltma mevcut sanal makineler VMM varsa, gerçekleştirebilir şekilde Azure Site Recovery çoğaltma için:

1. VM varolan hello barındıran hello Hyper-V server hello birincil bulutta bulunduğundan ve hello çoğaltma sanal makinesi barındıran bu hello Hyper-V server hello ikincil bulutta bulunduğundan emin olun.
2. Bir çoğaltma ilkesi hello birincil VMM bulutu için yapılandırılmış olduğundan emin olun.
3. Merhaba birincil sanal makine için çoğaltmayı etkinleştirin. Azure Site Recovery ve VMM hello aynı çoğaltma konak ve sanal makine algılandığında, Azure Site Recovery yeniden kullanılacak ve hello kullanarak yeniden çoğaltma ayarları belirtilen emin olun.


## <a name="next-steps"></a>Sonraki adımlar

Çok Git[adım 10: bir yük devretme testi](vmm-to-vmm-walkthrough-test-failover.md).
