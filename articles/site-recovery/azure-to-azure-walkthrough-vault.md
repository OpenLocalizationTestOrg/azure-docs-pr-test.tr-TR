---
title: "Azure Site Recovery ile bölgeler arasında Azure VM repliction için bir kasa ayarlama | Microsoft Docs"
description: "Azure Site Kurtarma'yı kullanarak Azure bölgeler arasında Azure çoğaltma için bir kasa ayarlamak için gereken adımları özetler"
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
ms.openlocfilehash: e03d17992ee0b12049636e40188950bcc4a6f31e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="step-4-set-up-a-vault-for-azure-to-azure-replication"></a><span data-ttu-id="91e44-103">4. adım: Azure için Azure'a çoğaltma için bir kasa ayarlayın</span><span class="sxs-lookup"><span data-stu-id="91e44-103">Step 4: Set up a vault for Azure to Azure replication</span></span>

<span data-ttu-id="91e44-104">Sonra [ağlarını planlama](azure-to-azure-walkthrough-network.md), Azure sanal başka bir Azure bölgesine çoğaltma, kullanarak makineleri (VM'ler) için bir kasa ayarlamak için bu makaleyi kullanın [Azure Site Recovery](site-recovery-overview.md) Azure portalında hizmet.</span><span class="sxs-lookup"><span data-stu-id="91e44-104">After [planning networks](azure-to-azure-walkthrough-network.md), use this article to set up a vault, for Azure virtual machines (VMs) replicating to another Azure region, using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>

- <span data-ttu-id="91e44-105">Makaleyi bitirdikten sonra ayarlanmış bir kurtarma Hizmetleri kasası olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="91e44-105">When you finish the article, you should have a Recovery Services vault set up.</span></span>
- <span data-ttu-id="91e44-106">Tüm yorumlarınızı bu makalenin alt kısmında paylaşabilir veya [Azure Kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)'nda soru sorabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="91e44-106">Post any comments at the bottom of this article, or ask questions in the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>



>[!NOTE]
>
> <span data-ttu-id="91e44-107">Azure VM çoğaltma şu anda önizlemede değil.</span><span class="sxs-lookup"><span data-stu-id="91e44-107">Azure VM replication is currently in preview.</span></span>




## <a name="create-a-vault"></a><span data-ttu-id="91e44-108">Bir kasa oluşturun</span><span class="sxs-lookup"><span data-stu-id="91e44-108">Create a vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

>[!NOTE]
>
> <span data-ttu-id="91e44-109">Kurtarma Hizmetleri kasası, sanal makineleri çoğaltmak istediğiniz konumda oluşturmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="91e44-109">We recommend that you create the Recovery Services vault in the location where you want your VMs to replicate.</span></span> <span data-ttu-id="91e44-110">Örneğin, hedef konumunuz Orta ise ABD, kasaya oluşturma **Orta ABD**.</span><span class="sxs-lookup"><span data-stu-id="91e44-110">For example, if your target location is the central US, create the vault in **Central US**.</span></span>


## <a name="next-steps"></a><span data-ttu-id="91e44-111">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="91e44-111">Next steps</span></span>

<span data-ttu-id="91e44-112">Git [5. adım: çoğaltmasını etkinleştir](azure-to-azure-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="91e44-112">Go to [Step 5: Enable replication](azure-to-azure-walkthrough-enable-replication.md)</span></span>
