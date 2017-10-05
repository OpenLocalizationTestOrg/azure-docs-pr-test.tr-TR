---
title: "Azure Site Recovery ile ikincil siteye Hyper-V çoğaltma için bir kasa oluşturun | Microsoft Docs"
description: "Azure Site Recovery ile ikincil System Center VMM siteye Hyper-V sanal makineleri çoğaltırken bir kasa oluşturmayı açıklar."
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
ms.openlocfilehash: 28cfcf12b2e369f96664c163c0b6f2aa8a6ddcb9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="step-5-create-a-vault-for-hyper-v-replication-to-a-secondary-site"></a><span data-ttu-id="dd09d-103">5. adım: Hyper-V çoğaltma için bir kasa ikincil bir siteye oluşturma</span><span class="sxs-lookup"><span data-stu-id="dd09d-103">Step 5: Create a vault for Hyper-V replication to a secondary site</span></span>

<span data-ttu-id="dd09d-104">Şirket içi hazırlandıktan sonra [System Center Virtual Machine Manager (VMM) sunucuları ve Hyper-V konakları/kümeleri](vmm-to-vmm-walkthrough-vmm-hyper-v.md) kullanarak bir ikincil site için Hyper-V çoğaltma için [Azure Site Recovery](site-recovery-overview.md), oluşturabileceğiniz bir Kurtarma Hizmetleri kasası ve çoğaltma senaryosuna seçin.</span><span class="sxs-lookup"><span data-stu-id="dd09d-104">After preparing on-premises [System Center Virtual Machine Manager (VMM) servers and Hyper-V hosts/clusters](vmm-to-vmm-walkthrough-vmm-hyper-v.md) for Hyper-V replication to a secondary site using [Azure Site Recovery](site-recovery-overview.md), you can create a Recovery Services vault, and select the replication scenario.</span></span>

<span data-ttu-id="dd09d-105">Bu makaleyi okuduktan sonra yapmak istediğiniz tüm yorumları makalenin alt kısmında veya [Azure Kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)'nda paylaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dd09d-105">After reading this article, post any comments at the bottom, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="dd09d-106">Kurtarma Hizmetleri kasası oluşturma</span><span class="sxs-lookup"><span data-stu-id="dd09d-106">Create a Recovery Services vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]


## <a name="choose-a-protection-goal"></a><span data-ttu-id="dd09d-107">Koruma hedefi seçin</span><span class="sxs-lookup"><span data-stu-id="dd09d-107">Choose a protection goal</span></span>

<span data-ttu-id="dd09d-108">Neleri çoğaltmak istediğinizi ve bunları nereye çoğaltacağınızı seçin.</span><span class="sxs-lookup"><span data-stu-id="dd09d-108">Select what you want to replicate and where you want to replicate to.</span></span>

1. <span data-ttu-id="dd09d-109">Tıklatın **Site Recovery** > **1. adım: altyapıyı hazırlama** > **koruma hedefi**.</span><span class="sxs-lookup"><span data-stu-id="dd09d-109">Click **Site Recovery** > **Step 1: Prepare Infrastructure** > **Protection goal**.</span></span>
2. <span data-ttu-id="dd09d-110">Seçin **kurtarma sitesine**seçip **Evet, Hyper-V ile**.</span><span class="sxs-lookup"><span data-stu-id="dd09d-110">Select **To recovery site**, and select **Yes, with Hyper-V**.</span></span>
3. <span data-ttu-id="dd09d-111">Seçin **Evet** Hyper-V ana bilgisayarları yönetmek için VMM kullandığınızı belirtmek için.</span><span class="sxs-lookup"><span data-stu-id="dd09d-111">Select **Yes** to indicate you're using VMM to manage the Hyper-V hosts.</span></span>
4. <span data-ttu-id="dd09d-112">Seçin **Evet** bir ikincil VMM sunucunuz varsa.</span><span class="sxs-lookup"><span data-stu-id="dd09d-112">Select **Yes** if you have a secondary VMM server.</span></span> <span data-ttu-id="dd09d-113">Tek bir VMM sunucusundaki Bulutlar arasında çoğaltma dağıtıyorsanız tıklatın **Hayır**.</span><span class="sxs-lookup"><span data-stu-id="dd09d-113">If you're deploying replication between clouds on a single VMM server, click **No**.</span></span> <span data-ttu-id="dd09d-114">Daha sonra, **Tamam**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="dd09d-114">Then click **OK**.</span></span>

    ![Hedefleri seçme](./media/vmm-to-vmm-walkthrough-create-vault/choose-goals.png)



## <a name="next-steps"></a><span data-ttu-id="dd09d-116">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="dd09d-116">Next steps</span></span>

<span data-ttu-id="dd09d-117">Git [6. adım: çoğaltma kaynağı ve hedef ayarlama](vmm-to-vmm-walkthrough-source-target.md).</span><span class="sxs-lookup"><span data-stu-id="dd09d-117">Go to [Step 6: Set up the replication source and target](vmm-to-vmm-walkthrough-source-target.md).</span></span>