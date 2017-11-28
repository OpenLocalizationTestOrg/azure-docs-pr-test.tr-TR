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
# <a name="step-7-set-up-a-vault-for-vmware-replication-tooazure"></a><span data-ttu-id="a4a89-103">7. adım: VMware çoğaltma tooAzure için bir kasa ayarlayın</span><span class="sxs-lookup"><span data-stu-id="a4a89-103">Step 7: Set up a vault for VMware replication tooAzure</span></span>


<span data-ttu-id="a4a89-104">Bu makalede nasıl tooset yukarı bir kasa ve istediğinizi belirtin, şirket içi konumdan hello kullanarak tooAzure tooreplicate [Azure Site Recovery](site-recovery-overview.md) hello Azure portal hizmeti.</span><span class="sxs-lookup"><span data-stu-id="a4a89-104">This article describes how tooset up a vault, and specify what you want tooreplicate from your on-premises location, tooAzure using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>


<span data-ttu-id="a4a89-105">POST açıklamaları ve soruları hello altındaki bu makalenin veya hello [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="a4a89-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>




## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="a4a89-106">Kurtarma Hizmetleri kasası oluşturma</span><span class="sxs-lookup"><span data-stu-id="a4a89-106">Create a Recovery Services vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

## <a name="select-a-protection-goal"></a><span data-ttu-id="a4a89-107">Koruma hedefi seçin</span><span class="sxs-lookup"><span data-stu-id="a4a89-107">Select a protection goal</span></span>

<span data-ttu-id="a4a89-108">İstediğinizi seçin, tooreplicate ve tooreplicate için istediğiniz.</span><span class="sxs-lookup"><span data-stu-id="a4a89-108">Select what you want tooreplicate, and where you want tooreplicate to.</span></span>

1. <span data-ttu-id="a4a89-109">Tıklatın **kurtarma Hizmetleri kasaları** > kasası.</span><span class="sxs-lookup"><span data-stu-id="a4a89-109">Click **Recovery Services vaults** > vault.</span></span>
2. <span data-ttu-id="a4a89-110">Hello kaynak menüsü, tıklatın **Site Recovery** > **altyapıyı hazırlama** > **koruma hedefi**.</span><span class="sxs-lookup"><span data-stu-id="a4a89-110">In hello Resource Menu, click **Site Recovery** > **Prepare Infrastructure** > **Protection goal**.</span></span>
3. <span data-ttu-id="a4a89-111">İçinde **koruma hedefi**seçin **tooAzure** > **Evet, VMware vSphere hiper yönetici ile**.</span><span class="sxs-lookup"><span data-stu-id="a4a89-111">In **Protection goal**, select **tooAzure** > **Yes, with VMware vSphere Hypervisor**.</span></span>



## <a name="next-steps"></a><span data-ttu-id="a4a89-112">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a4a89-112">Next steps</span></span>

<span data-ttu-id="a4a89-113">Çok Git[adım 8: kaynak ve hedef ayarlama](vmware-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="a4a89-113">Go too[Step 8: Set up source and target](vmware-walkthrough-source-target.md)</span></span>
