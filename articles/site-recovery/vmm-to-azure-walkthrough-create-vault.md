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
# <a name="step-7-set-up-a-vault-for-hyper-v-replication"></a><span data-ttu-id="f5c23-103">7. adım: Hyper-V çoğaltma için bir kasa ayarlayın</span><span class="sxs-lookup"><span data-stu-id="f5c23-103">Step 7: Set up a vault for Hyper-V replication</span></span>

<span data-ttu-id="f5c23-104">Bu makalede nasıl tooset yukarı bir kasa ve istediğinizi belirtin, şirket içi konumdan hello kullanarak tooAzure tooreplicate [Azure Site Recovery](site-recovery-overview.md) hello Azure portal hizmeti.</span><span class="sxs-lookup"><span data-stu-id="f5c23-104">This article describes how tooset up a vault, and specify what you want tooreplicate from your on-premises location, tooAzure using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>


<span data-ttu-id="f5c23-105">POST açıklamaları ve soruları hello altındaki bu makalenin veya hello [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="f5c23-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="f5c23-106">Kurtarma Hizmetleri kasası oluşturma</span><span class="sxs-lookup"><span data-stu-id="f5c23-106">Create a Recovery Services vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]



## <a name="select-a-protection-goal"></a><span data-ttu-id="f5c23-107">Koruma hedefi seçin</span><span class="sxs-lookup"><span data-stu-id="f5c23-107">Select a protection goal</span></span>

<span data-ttu-id="f5c23-108">İstediğinizi seçin, tooreplicate ve tooreplicate için istediğiniz.</span><span class="sxs-lookup"><span data-stu-id="f5c23-108">Select what you want tooreplicate, and where you want tooreplicate to.</span></span>

1. <span data-ttu-id="f5c23-109">Tıklatın **kurtarma Hizmetleri kasaları** > kasası.</span><span class="sxs-lookup"><span data-stu-id="f5c23-109">Click **Recovery Services vaults** > vault.</span></span>
2. <span data-ttu-id="f5c23-110">Hello kaynak menüsü, tıklatın **Site Recovery** > **altyapıyı hazırlama** > **koruma hedefi**.</span><span class="sxs-lookup"><span data-stu-id="f5c23-110">In hello Resource Menu, click **Site Recovery** > **Prepare Infrastructure** > **Protection goal**.</span></span>
3. <span data-ttu-id="f5c23-111">İçinde **koruma hedefi**seçin **tooAzure** > **Evet, Hyper-V ile**.</span><span class="sxs-lookup"><span data-stu-id="f5c23-111">In **Protection goal**, select **tooAzure** > **Yes, with Hyper-V**.</span></span> <span data-ttu-id="f5c23-112">Seçin **Evet** tooconfirm olduğunuz nusing VMM.</span><span class="sxs-lookup"><span data-stu-id="f5c23-112">Select **Yes** tooconfirm you're nusing VMM.</span></span> 

     ![Hedefleri seçme](./media/vmm-to-azure-walkthrough-create-vault/choose-goals.png)



## <a name="next-steps"></a><span data-ttu-id="f5c23-114">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f5c23-114">Next steps</span></span>

<span data-ttu-id="f5c23-115">Çok Git[adım 8: kaynak ve hedef ayarlama](vmm-to-azure-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="f5c23-115">Go too[Step 8: Set up source and target](vmm-to-azure-walkthrough-source-target.md)</span></span>
