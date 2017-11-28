---
title: "Hedef (VMware tooAzure) hazırlama | Microsoft Docs"
description: "Bu makalede nasıl tooprepare, Azure ortamı toostart VMware sanal makineleri tooAzure çoğaltılıyor."
services: site-recovery
documentationcenter: 
author: bsiva
manager: abhemraj
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: backup-recovery
ms.date: 5/31/2017
ms.author: bsiva
ms.openlocfilehash: 5975d3c122032f92f8df370ee74fa0c7012ebe2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-target-vmware-tooazure"></a><span data-ttu-id="810b5-103">Hedef (VMware tooAzure) hazırlama</span><span class="sxs-lookup"><span data-stu-id="810b5-103">Prepare target (VMware tooAzure)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="810b5-104">VMware tooAzure</span><span class="sxs-lookup"><span data-stu-id="810b5-104">VMware tooAzure</span></span>](./site-recovery-prepare-target-vmware-to-azure.md)
> * [<span data-ttu-id="810b5-105">Fiziksel tooAzure</span><span class="sxs-lookup"><span data-stu-id="810b5-105">Physical tooAzure</span></span>](./site-recovery-prepare-target-physical-to-azure.md)

<span data-ttu-id="810b5-106">Bu makalede nasıl tooprepare, Azure ortamı toostart VMware sanal makineleri tooAzure çoğaltılıyor.</span><span class="sxs-lookup"><span data-stu-id="810b5-106">This article describes how tooprepare your Azure environment toostart replicating VMware virtual machines tooAzure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="810b5-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="810b5-107">Prerequisites</span></span>

<span data-ttu-id="810b5-108">Merhaba makale hello aşağıdakileri varsayar:</span><span class="sxs-lookup"><span data-stu-id="810b5-108">hello article assumes hello following:</span></span>
- <span data-ttu-id="810b5-109">VMware sanal makineleri kurtarma Hizmetleri kasası tooprotect oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="810b5-109">You have created a Recovery Services Vault tooprotect your VMware virtual machines.</span></span> <span data-ttu-id="810b5-110">Bir kurtarma Hizmetleri kasası hello oluşturabilirsiniz [Azure portal](http://portal.azure.com "Azure portal").</span><span class="sxs-lookup"><span data-stu-id="810b5-110">You can create a Recovery Services Vault from hello [Azure portal](http://portal.azure.com "Azure portal").</span></span>
- <span data-ttu-id="810b5-111">Sahip olduğunuz [, şirket içi ortamınızın Kurulumu](./site-recovery-set-up-vmware-to-azure.md) tooreplicate VMware sanal makineleri tooAzure.</span><span class="sxs-lookup"><span data-stu-id="810b5-111">You have [setup your on-premises environment](./site-recovery-set-up-vmware-to-azure.md) tooreplicate VMware virtual machines tooAzure.</span></span>

## <a name="prepare-target"></a><span data-ttu-id="810b5-112">Hedef hazırlama</span><span class="sxs-lookup"><span data-stu-id="810b5-112">Prepare target</span></span>

<span data-ttu-id="810b5-113">Merhaba tamamladıktan sonra **adım 1:Select koruma hedefi** ve **2. adım: kaynak hazırlama**, çok alınır**adım 3: hedef**</span><span class="sxs-lookup"><span data-stu-id="810b5-113">After completing hello **Step 1:Select Protection goal** and **Step 2:Prepare Source**, you are taken too**Step 3: Target**</span></span>

![Hedef hazırlama](./media/site-recovery-prepare-target-vmware-to-azure/prepare-target-vmware-to-azure.png)

1. <span data-ttu-id="810b5-115">**Abonelik:** , sanal makinelerinizin hello açılır menü, select hello tooreplicate istediğiniz abonelik.</span><span class="sxs-lookup"><span data-stu-id="810b5-115">**Subscription:** From hello drop down menu, select hello Subscription that you want tooreplicate your virtual machines to.</span></span>
2. <span data-ttu-id="810b5-116">**Dağıtım modeli:** Select hello dağıtım modeli (Klasik veya Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="810b5-116">**Deployment Model:** Select hello deployment model (Classic or Resource Manager)</span></span>

<span data-ttu-id="810b5-117">Dağıtım modeli seçilen hello üzerinde bağlı olarak, bir doğrulama sanal makine için en az bir uyumlu depolama hesabı ve sanal ağ hello hedef abonelik tooreplicate ve yük devretme sahip tooensure çalıştırılır.</span><span class="sxs-lookup"><span data-stu-id="810b5-117">Based on hello chosen deployment model, a validation is run tooensure that you have at least one compatible storage account and virtual network in hello target subscription tooreplicate and failover your virtual machine to.</span></span>

<span data-ttu-id="810b5-118">Merhaba doğrulamaları başarıyla tamamlandığında, Tamam toogo toohello sonraki adım'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="810b5-118">Once hello validations complete successfully, click OK toogo toohello next step.</span></span>

<span data-ttu-id="810b5-119">Uyumlu Resource Manager depolama hesabı veya sanal ağ yok ya da daha fazla tooadd istersiniz, hello tıklayarak bunu yapabilirsiniz **+ depolama hesabı** veya **+ ağ** hello hello üstündeki düğmeleri Dikey.</span><span class="sxs-lookup"><span data-stu-id="810b5-119">If you don't have a compatible Resource Manager storage account or virtual network, or would like tooadd more, you can do so by clicking hello **+ Storage Account** or **+ Network** buttons on hello top of hello blade.</span></span>

## <a name="next-steps"></a><span data-ttu-id="810b5-120">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="810b5-120">Next steps</span></span>
<span data-ttu-id="810b5-121">[Çoğaltma ayarlarını yapılandırın](./site-recovery-setup-replication-settings-vmware.md).</span><span class="sxs-lookup"><span data-stu-id="810b5-121">[Configure replication settings](./site-recovery-setup-replication-settings-vmware.md).</span></span>
