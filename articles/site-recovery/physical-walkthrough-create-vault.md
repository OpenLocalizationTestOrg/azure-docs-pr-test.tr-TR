---
title: "Azure Site RECOVERY'yi kullanarak fiziksel sunucu çoğaltma tooAzure için bir kasa yukarı aaaSet | Microsoft Docs"
description: "Azure Site RECOVERY'yi kullanarak bir kasa tooreplicate fiziksel sunucuları tooAzure yukarı tooset gereken hello adımları özetler"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d99f2605-f417-4995-be77-5323136b814f
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 988928e3ece31116823f132cc39223fe44443468
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="step-6-set-up-a-vault-for-physical-server-replication-tooazure"></a>Adım 6: fiziksel sunucu çoğaltma tooAzure için bir kasa ayarlayın


Bu makalede nasıl tooset bir kasa ayarlama. Merhaba kasası oluşturun ve istediğinizi belirtin hello kullanarak şirket içi konumu tooAzure gelen tooreplicate [Azure Site Recovery](site-recovery-overview.md) hello Azure portal hizmeti.


POST açıklamaları ve soruları hello altındaki bu makalenin veya hello [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).




## <a name="create-a-recovery-services-vault"></a>Kurtarma Hizmetleri kasası oluşturma

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

## <a name="select-a-protection-goal"></a>Koruma hedefi seçin

İstediğinizi seçin, tooreplicate ve tooreplicate için istediğiniz.

1. Tıklatın **kurtarma Hizmetleri kasaları** > kasası.
2. Hello kaynak menüsü, tıklatın **Site Recovery** > **altyapıyı hazırlama** > **koruma hedefi**.
3. İçinde **koruma hedefi**seçin **tooAzure** > **değil sanallaştırılmış/diğer**.


## <a name="next-steps"></a>Sonraki adımlar

Çok Git[adım 7: kaynak ve hedef ayarlama](physical-walkthrough-source-target.md)
