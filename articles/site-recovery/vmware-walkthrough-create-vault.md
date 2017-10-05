---
title: "Azure Site RECOVERY'yi kullanarak azure'da VMware çoğaltma için bir kasa ayarlama | Microsoft Docs"
description: "Azure Site RECOVERY'yi kullanarak azure'da VMware çoğaltma için bir kasa ayarlamak için gereken adımları özetler"
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
ms.openlocfilehash: dca95ad46b8de587140c3573ba6ed5702a122032
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="step-7-set-up-a-vault-for-vmware-replication-to-azure"></a><span data-ttu-id="4c85d-103">7. adım: Azure VMware çoğaltma için bir kasa ayarlayın</span><span class="sxs-lookup"><span data-stu-id="4c85d-103">Step 7: Set up a vault for VMware replication to Azure</span></span>


<span data-ttu-id="4c85d-104">Bu makalede bir kasasını oluşturup ve Azure kullanarak, şirket içi konumdan çoğaltmak istediğiniz belirtmek nasıl [Azure Site Recovery](site-recovery-overview.md) Azure portalında hizmet.</span><span class="sxs-lookup"><span data-stu-id="4c85d-104">This article describes how to set up a vault, and specify what you want to replicate from your on-premises location, to Azure using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>


<span data-ttu-id="4c85d-105">POST açıklamaları ve soruları alt bu makalenin veya üzerinde [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="4c85d-105">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>




## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="4c85d-106">Kurtarma Hizmetleri kasası oluşturma</span><span class="sxs-lookup"><span data-stu-id="4c85d-106">Create a Recovery Services vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

## <a name="select-a-protection-goal"></a><span data-ttu-id="4c85d-107">Koruma hedefi seçin</span><span class="sxs-lookup"><span data-stu-id="4c85d-107">Select a protection goal</span></span>

<span data-ttu-id="4c85d-108">Neleri çoğaltmak istediğinizi ve bunları nereye çoğaltacağınızı seçin.</span><span class="sxs-lookup"><span data-stu-id="4c85d-108">Select what you want to replicate, and where you want to replicate to.</span></span>

1. <span data-ttu-id="4c85d-109">Tıklatın **kurtarma Hizmetleri kasaları** > kasası.</span><span class="sxs-lookup"><span data-stu-id="4c85d-109">Click **Recovery Services vaults** > vault.</span></span>
2. <span data-ttu-id="4c85d-110">Kaynak menüye tıklayın **Site Recovery** > **altyapıyı hazırlama** > **koruma hedefi**.</span><span class="sxs-lookup"><span data-stu-id="4c85d-110">In the Resource Menu, click **Site Recovery** > **Prepare Infrastructure** > **Protection goal**.</span></span>
3. <span data-ttu-id="4c85d-111">İçinde **koruma hedefi**seçin **için Azure** > **Evet, VMware vSphere hiper yönetici ile**.</span><span class="sxs-lookup"><span data-stu-id="4c85d-111">In **Protection goal**, select **To Azure** > **Yes, with VMware vSphere Hypervisor**.</span></span>



## <a name="next-steps"></a><span data-ttu-id="4c85d-112">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4c85d-112">Next steps</span></span>

<span data-ttu-id="4c85d-113">Git [adım 8: kaynak ve hedef ayarlama](vmware-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="4c85d-113">Go to [Step 8: Set up source and target](vmware-walkthrough-source-target.md)</span></span>
