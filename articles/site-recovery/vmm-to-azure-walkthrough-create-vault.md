---
title: "Azure Site Recovery kullanarak Hyper-V çoğaltma (System Center VMM ile) tooAzure için bir kasa yukarı aaaSet | Microsoft Docs"
description: "Azure Site Recovery kullanarak Hyper-V çoğaltma (VMM ile) tooAzure için bir kasa yukarı tooset gereken hello adımları özetler"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: b3cd6f03-c33c-406d-91d4-5cba69f79abd
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: f2c90f3c8b0a48db1e57fefd9829d29cffff8d43
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="step-7-set-up-a-vault-for-hyper-v-replication"></a>7. adım: Hyper-V çoğaltma için bir kasa ayarlayın

Bu makalede nasıl tooset yukarı bir kasa ve istediğinizi belirtin, şirket içi konumdan hello kullanarak tooAzure tooreplicate [Azure Site Recovery](site-recovery-overview.md) hello Azure portal hizmeti.


POST açıklamaları ve soruları hello altındaki bu makalenin veya hello [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="create-a-recovery-services-vault"></a>Kurtarma Hizmetleri kasası oluşturma

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]



## <a name="select-a-protection-goal"></a>Koruma hedefi seçin

İstediğinizi seçin, tooreplicate ve tooreplicate için istediğiniz.

1. Tıklatın **kurtarma Hizmetleri kasaları** > kasası.
2. Hello kaynak menüsü, tıklatın **Site Recovery** > **altyapıyı hazırlama** > **koruma hedefi**.
3. İçinde **koruma hedefi**seçin **tooAzure** > **Evet, Hyper-V ile**. Seçin **Evet** tooconfirm olduğunuz nusing VMM. 

     ![Hedefleri seçme](./media/vmm-to-azure-walkthrough-create-vault/choose-goals.png)



## <a name="next-steps"></a>Sonraki adımlar

Çok Git[adım 8: kaynak ve hedef ayarlama](vmm-to-azure-walkthrough-source-target.md)
