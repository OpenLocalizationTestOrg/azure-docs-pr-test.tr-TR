---
title: "Azure Site Recovery kullanarak Hyper-V çoğaltma (System Center VMM olmadan) için bir kasa ayarlama | Microsoft Docs"
description: "Azure Site Recovery kullanarak Hyper-V çoğaltma için bir kasa ayarlamak için gereken adımları özetler"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: a936b3e2-0dbe-47ac-a98e-5285d96dc786
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/22/2017
ms.author: raynew
ms.openlocfilehash: 8212ff011633c3a89d3310e828b6d5f1cda6ce3f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="step-7-set-up-a-vault-for-hyper-v-replication"></a><span data-ttu-id="31b51-103">7. adım: Hyper-V çoğaltma için bir kasa ayarlayın</span><span class="sxs-lookup"><span data-stu-id="31b51-103">Step 7: Set up a vault for Hyper-V replication</span></span>

<span data-ttu-id="31b51-104">Bu makalede bir kasasını oluşturup ve Azure kullanarak, şirket içi konumdan çoğaltmak istediğiniz belirtmek nasıl [Azure Site Recovery](site-recovery-overview.md) Azure portalında hizmet.</span><span class="sxs-lookup"><span data-stu-id="31b51-104">This article describes how to set up a vault, and specify what you want to replicate from your on-premises location, to Azure using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>


<span data-ttu-id="31b51-105">POST açıklamaları ve soruları alt bu makalenin veya üzerinde [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="31b51-105">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="31b51-106">Kurtarma Hizmetleri kasası oluşturma</span><span class="sxs-lookup"><span data-stu-id="31b51-106">Create a Recovery Services vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]



## <a name="select-a-protection-goal"></a><span data-ttu-id="31b51-107">Koruma hedefi seçin</span><span class="sxs-lookup"><span data-stu-id="31b51-107">Select a protection goal</span></span>

<span data-ttu-id="31b51-108">Neleri çoğaltmak istediğinizi ve bunları nereye çoğaltacağınızı seçin.</span><span class="sxs-lookup"><span data-stu-id="31b51-108">Select what you want to replicate, and where you want to replicate to.</span></span>

1. <span data-ttu-id="31b51-109">Tıklatın **kurtarma Hizmetleri kasaları** > kasası.</span><span class="sxs-lookup"><span data-stu-id="31b51-109">Click **Recovery Services vaults** > vault.</span></span>
2. <span data-ttu-id="31b51-110">Kaynak menüye tıklayın **Site Recovery** > **altyapıyı hazırlama** > **koruma hedefi**.</span><span class="sxs-lookup"><span data-stu-id="31b51-110">In the Resource Menu, click **Site Recovery** > **Prepare Infrastructure** > **Protection goal**.</span></span>
3. <span data-ttu-id="31b51-111">İçinde **koruma hedefi**seçin **için Azure** > **Evet, Hyper-V ile**.</span><span class="sxs-lookup"><span data-stu-id="31b51-111">In **Protection goal**, select **To Azure** > **Yes, with Hyper-V**.</span></span> <span data-ttu-id="31b51-112">Seçin **Hayır** değil VMM kullandığınızı doğrulamak için.</span><span class="sxs-lookup"><span data-stu-id="31b51-112">Select **No** to confirm you're not using VMM.</span></span> 

    ![Hedefleri seçme](./media/hyper-v-site-walkthrough-create-vault/choose-goals2.png)



## <a name="next-steps"></a><span data-ttu-id="31b51-114">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="31b51-114">Next steps</span></span>

<span data-ttu-id="31b51-115">Git [adım 8: kaynak ve hedef ayarlama](hyper-v-site-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="31b51-115">Go to [Step 8: Set up source and target](hyper-v-site-walkthrough-source-target.md)</span></span>
