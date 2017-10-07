---
title: "Azure Site RECOVERY'yi kullanarak VMware çoğaltma tooAzure için bir kasa yukarı aaaSet | Microsoft Docs"
description: "Azure Site RECOVERY'yi kullanarak VMware çoğaltma tooAzure için bir kasa yukarı tooset gereken hello adımları özetler"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 8bce940e-f19f-4418-8360-aee7b073519a
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 8a7755a6c9a3f55f241c615e425285bc4b782493
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="step-7-set-up-a-vault-for-vmware-replication-tooazure"></a>7. adım: VMware çoğaltma tooAzure için bir kasa ayarlayın


Bu makalede nasıl tooset yukarı bir kasa ve istediğinizi belirtin, şirket içi konumdan hello kullanarak tooAzure tooreplicate [Azure Site Recovery](site-recovery-overview.md) hello Azure portal hizmeti.


POST açıklamaları ve soruları hello altındaki bu makalenin veya hello [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).




## <a name="create-a-recovery-services-vault"></a>Kurtarma Hizmetleri kasası oluşturma

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

## <a name="select-a-protection-goal"></a>Koruma hedefi seçin

İstediğinizi seçin, tooreplicate ve tooreplicate için istediğiniz.

1. Tıklatın **kurtarma Hizmetleri kasaları** > kasası.
2. Hello kaynak menüsü, tıklatın **Site Recovery** > **altyapıyı hazırlama** > **koruma hedefi**.
3. İçinde **koruma hedefi**seçin **tooAzure** > **Evet, VMware vSphere hiper yönetici ile**.



## <a name="next-steps"></a>Sonraki adımlar

Çok Git[adım 8: kaynak ve hedef ayarlama](vmware-walkthrough-source-target.md)
