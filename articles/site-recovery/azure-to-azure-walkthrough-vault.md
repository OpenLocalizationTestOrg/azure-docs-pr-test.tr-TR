---
title: "Azure Site Recovery ile bölgeler arasında Azure VM repliction için bir kasa yukarı aaaSet | Microsoft Docs"
description: "Azure Site Kurtarma'yı kullanarak Azure bölgeler arasında Azure çoğaltma için bir kasa yukarı tooset gereken hello adımları özetler"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmon
editor: 
ms.assetid: 40472189-3d80-4963-b175-8bddcbc2f61f
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: raynew
ms.openlocfilehash: 9959c59c7ea57114763f13bf060404ddd267ba80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="step-4-set-up-a-vault-for-azure-tooazure-replication"></a><span data-ttu-id="ab866-103">4. adım: Azure tooAzure çoğaltma için bir kasa ayarlayın</span><span class="sxs-lookup"><span data-stu-id="ab866-103">Step 4: Set up a vault for Azure tooAzure replication</span></span>

<span data-ttu-id="ab866-104">Sonra [ağlarını planlama](azure-to-azure-walkthrough-network.md), hello kullanarak tooanother Azure bölgesi çoğaltma Bu makale tooset Azure sanal makineleri (VM'ler) için bir kasa yukarı kullanmak [Azure Site Recovery](site-recovery-overview.md) hello Azure portal hizmeti.</span><span class="sxs-lookup"><span data-stu-id="ab866-104">After [planning networks](azure-to-azure-walkthrough-network.md), use this article tooset up a vault, for Azure virtual machines (VMs) replicating tooanother Azure region, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

- <span data-ttu-id="ab866-105">Merhaba makale bitirdikten sonra ayarlanmış bir kurtarma Hizmetleri kasası olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ab866-105">When you finish hello article, you should have a Recovery Services vault set up.</span></span>
- <span data-ttu-id="ab866-106">Bu makalenin hello altındaki tüm yorumlar gönderin ya da hello sorular sormak [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="ab866-106">Post any comments at hello bottom of this article, or ask questions in hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>



>[!NOTE]
>
> <span data-ttu-id="ab866-107">Azure VM çoğaltma şu anda önizlemede değil.</span><span class="sxs-lookup"><span data-stu-id="ab866-107">Azure VM replication is currently in preview.</span></span>




## <a name="create-a-vault"></a><span data-ttu-id="ab866-108">Bir kasa oluşturun</span><span class="sxs-lookup"><span data-stu-id="ab866-108">Create a vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

>[!NOTE]
>
> <span data-ttu-id="ab866-109">Merhaba kurtarma Hizmetleri kasası, VM'ler tooreplicate istediğiniz hello konumda oluşturmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="ab866-109">We recommend that you create hello Recovery Services vault in hello location where you want your VMs tooreplicate.</span></span> <span data-ttu-id="ab866-110">Hedef konumunuz olan hello Orta BİZE, örneğin, hello kasasına oluşturun **Orta ABD**.</span><span class="sxs-lookup"><span data-stu-id="ab866-110">For example, if your target location is hello central US, create hello vault in **Central US**.</span></span>


## <a name="next-steps"></a><span data-ttu-id="ab866-111">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ab866-111">Next steps</span></span>

<span data-ttu-id="ab866-112">Çok Git[5. adım: çoğaltmasını etkinleştir](azure-to-azure-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="ab866-112">Go too[Step 5: Enable replication](azure-to-azure-walkthrough-enable-replication.md)</span></span>
