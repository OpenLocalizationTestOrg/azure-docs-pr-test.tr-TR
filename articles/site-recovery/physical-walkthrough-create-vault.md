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
# <a name="step-6-set-up-a-vault-for-physical-server-replication-tooazure"></a><span data-ttu-id="8dd4c-103">Adım 6: fiziksel sunucu çoğaltma tooAzure için bir kasa ayarlayın</span><span class="sxs-lookup"><span data-stu-id="8dd4c-103">Step 6: Set up a vault for physical server replication tooAzure</span></span>


<span data-ttu-id="8dd4c-104">Bu makalede nasıl tooset bir kasa ayarlama.</span><span class="sxs-lookup"><span data-stu-id="8dd4c-104">This article describes how tooset up a vault.</span></span> <span data-ttu-id="8dd4c-105">Merhaba kasası oluşturun ve istediğinizi belirtin hello kullanarak şirket içi konumu tooAzure gelen tooreplicate [Azure Site Recovery](site-recovery-overview.md) hello Azure portal hizmeti.</span><span class="sxs-lookup"><span data-stu-id="8dd4c-105">You create hello vault, and specify what you want tooreplicate from your on-premises location tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>


<span data-ttu-id="8dd4c-106">POST açıklamaları ve soruları hello altındaki bu makalenin veya hello [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="8dd4c-106">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>




## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="8dd4c-107">Kurtarma Hizmetleri kasası oluşturma</span><span class="sxs-lookup"><span data-stu-id="8dd4c-107">Create a Recovery Services vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

## <a name="select-a-protection-goal"></a><span data-ttu-id="8dd4c-108">Koruma hedefi seçin</span><span class="sxs-lookup"><span data-stu-id="8dd4c-108">Select a protection goal</span></span>

<span data-ttu-id="8dd4c-109">İstediğinizi seçin, tooreplicate ve tooreplicate için istediğiniz.</span><span class="sxs-lookup"><span data-stu-id="8dd4c-109">Select what you want tooreplicate, and where you want tooreplicate to.</span></span>

1. <span data-ttu-id="8dd4c-110">Tıklatın **kurtarma Hizmetleri kasaları** > kasası.</span><span class="sxs-lookup"><span data-stu-id="8dd4c-110">Click **Recovery Services vaults** > vault.</span></span>
2. <span data-ttu-id="8dd4c-111">Hello kaynak menüsü, tıklatın **Site Recovery** > **altyapıyı hazırlama** > **koruma hedefi**.</span><span class="sxs-lookup"><span data-stu-id="8dd4c-111">In hello Resource Menu, click **Site Recovery** > **Prepare Infrastructure** > **Protection goal**.</span></span>
3. <span data-ttu-id="8dd4c-112">İçinde **koruma hedefi**seçin **tooAzure** > **değil sanallaştırılmış/diğer**.</span><span class="sxs-lookup"><span data-stu-id="8dd4c-112">In **Protection goal**, select **tooAzure** > **Not virtualized/Other**.</span></span>


## <a name="next-steps"></a><span data-ttu-id="8dd4c-113">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8dd4c-113">Next steps</span></span>

<span data-ttu-id="8dd4c-114">Çok Git[adım 7: kaynak ve hedef ayarlama](physical-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="8dd4c-114">Go too[Step 7: Set up source and target](physical-walkthrough-source-target.md)</span></span>
