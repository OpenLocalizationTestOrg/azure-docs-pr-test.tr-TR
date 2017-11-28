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
# <a name="step-5-create-a-vault-for-hyper-v-replication-tooa-secondary-site"></a><span data-ttu-id="90e06-103">5. adım: Hyper-V çoğaltma tooa ikincil site için bir kasa oluşturma</span><span class="sxs-lookup"><span data-stu-id="90e06-103">Step 5: Create a vault for Hyper-V replication tooa secondary site</span></span>

<span data-ttu-id="90e06-104">Şirket içi hazırlandıktan sonra [System Center Virtual Machine Manager (VMM) sunucuları ve Hyper-V konakları/kümeleri](vmm-to-vmm-walkthrough-vmm-hyper-v.md) Hyper-V çoğaltma tooa ikincil site kullanma [Azure Site Recovery](site-recovery-overview.md), oluşturabileceğiniz bir Kurtarma Hizmetleri kasası ve select hello çoğaltma senaryo.</span><span class="sxs-lookup"><span data-stu-id="90e06-104">After preparing on-premises [System Center Virtual Machine Manager (VMM) servers and Hyper-V hosts/clusters](vmm-to-vmm-walkthrough-vmm-hyper-v.md) for Hyper-V replication tooa secondary site using [Azure Site Recovery](site-recovery-overview.md), you can create a Recovery Services vault, and select hello replication scenario.</span></span>

<span data-ttu-id="90e06-105">Bu makaleyi okuduktan sonra tüm yorumlar hello altındaki ya da hello sonrası [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="90e06-105">After reading this article, post any comments at hello bottom, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="90e06-106">Kurtarma Hizmetleri kasası oluşturma</span><span class="sxs-lookup"><span data-stu-id="90e06-106">Create a Recovery Services vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]


## <a name="choose-a-protection-goal"></a><span data-ttu-id="90e06-107">Koruma hedefi seçin</span><span class="sxs-lookup"><span data-stu-id="90e06-107">Choose a protection goal</span></span>

<span data-ttu-id="90e06-108">Ne seçin tooreplicate ve tooreplicate için istediğiniz istiyor.</span><span class="sxs-lookup"><span data-stu-id="90e06-108">Select what you want tooreplicate and where you want tooreplicate to.</span></span>

1. <span data-ttu-id="90e06-109">Tıklatın **Site Recovery** > **1. adım: altyapıyı hazırlama** > **koruma hedefi**.</span><span class="sxs-lookup"><span data-stu-id="90e06-109">Click **Site Recovery** > **Step 1: Prepare Infrastructure** > **Protection goal**.</span></span>
2. <span data-ttu-id="90e06-110">Seçin **toorecovery site**seçip **Evet, Hyper-V ile**.</span><span class="sxs-lookup"><span data-stu-id="90e06-110">Select **toorecovery site**, and select **Yes, with Hyper-V**.</span></span>
3. <span data-ttu-id="90e06-111">Seçin **Evet** VMM toomanage hello Hyper-V konakları kullanmakta olduğunuz tooindicate.</span><span class="sxs-lookup"><span data-stu-id="90e06-111">Select **Yes** tooindicate you're using VMM toomanage hello Hyper-V hosts.</span></span>
4. <span data-ttu-id="90e06-112">Seçin **Evet** bir ikincil VMM sunucunuz varsa.</span><span class="sxs-lookup"><span data-stu-id="90e06-112">Select **Yes** if you have a secondary VMM server.</span></span> <span data-ttu-id="90e06-113">Tek bir VMM sunucusundaki Bulutlar arasında çoğaltma dağıtıyorsanız tıklatın **Hayır**.</span><span class="sxs-lookup"><span data-stu-id="90e06-113">If you're deploying replication between clouds on a single VMM server, click **No**.</span></span> <span data-ttu-id="90e06-114">Daha sonra, **Tamam**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="90e06-114">Then click **OK**.</span></span>

    ![Hedefleri seçme](./media/vmm-to-vmm-walkthrough-create-vault/choose-goals.png)



## <a name="next-steps"></a><span data-ttu-id="90e06-116">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="90e06-116">Next steps</span></span>

<span data-ttu-id="90e06-117">Çok Git[adım 6: hello çoğaltma kaynağı ve hedef ayarlama](vmm-to-vmm-walkthrough-source-target.md).</span><span class="sxs-lookup"><span data-stu-id="90e06-117">Go too[Step 6: Set up hello replication source and target](vmm-to-vmm-walkthrough-source-target.md).</span></span>
