---
title: "Hyper-V çoğaltma tooa Azure Site Recovery ile ikincil site için bir kasa aaaCreate | Microsoft Docs"
description: "Nasıl toocreate Hyper-V sanal makineleri tooa çoğaltırken bir kasa ikincil System Center VMM site Azure Site Recovery ile açıklar."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: ff65dbfb-cb26-410e-ab48-76971625db08
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: 96ee09cbf2376a5089b9efa09dc7ab3fb7d472cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="step-5-create-a-vault-for-hyper-v-replication-tooa-secondary-site"></a>5. adım: Hyper-V çoğaltma tooa ikincil site için bir kasa oluşturma

Şirket içi hazırlandıktan sonra [System Center Virtual Machine Manager (VMM) sunucuları ve Hyper-V konakları/kümeleri](vmm-to-vmm-walkthrough-vmm-hyper-v.md) Hyper-V çoğaltma tooa ikincil site kullanma [Azure Site Recovery](site-recovery-overview.md), oluşturabileceğiniz bir Kurtarma Hizmetleri kasası ve select hello çoğaltma senaryo.

Bu makaleyi okuduktan sonra tüm yorumlar hello altındaki ya da hello sonrası [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="create-a-recovery-services-vault"></a>Kurtarma Hizmetleri kasası oluşturma

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]


## <a name="choose-a-protection-goal"></a>Koruma hedefi seçin

Ne seçin tooreplicate ve tooreplicate için istediğiniz istiyor.

1. Tıklatın **Site Recovery** > **1. adım: altyapıyı hazırlama** > **koruma hedefi**.
2. Seçin **toorecovery site**seçip **Evet, Hyper-V ile**.
3. Seçin **Evet** VMM toomanage hello Hyper-V konakları kullanmakta olduğunuz tooindicate.
4. Seçin **Evet** bir ikincil VMM sunucunuz varsa. Tek bir VMM sunucusundaki Bulutlar arasında çoğaltma dağıtıyorsanız tıklatın **Hayır**. Daha sonra, **Tamam**'a tıklayın.

    ![Hedefleri seçme](./media/vmm-to-vmm-walkthrough-create-vault/choose-goals.png)



## <a name="next-steps"></a>Sonraki adımlar

Çok Git[adım 6: hello çoğaltma kaynağı ve hedef ayarlama](vmm-to-vmm-walkthrough-source-target.md).
