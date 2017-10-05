---
title: "Hedef (fiziksel Azure) hazırlama | Microsoft Docs"
description: "Bu makalede, Azure için Windows veya Linux çalıştıran fiziksel sunucuları çoğaltıyor başlatmak üzere Azure ortamınızı hazırlamak açıklar."
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
ms.openlocfilehash: aa7a32ace8354f615a8b8cc137f6bdf48fbadf48
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="prepare-target-vmware-to-azure"></a><span data-ttu-id="8f9b9-103">Hedef (VMware Azure için) hazırlama</span><span class="sxs-lookup"><span data-stu-id="8f9b9-103">Prepare target (VMware to Azure)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8f9b9-104">Vmware’den Azure’a</span><span class="sxs-lookup"><span data-stu-id="8f9b9-104">VMware to Azure</span></span>](./site-recovery-prepare-target-vmware-to-azure.md)
> * [<span data-ttu-id="8f9b9-105">Azure için fiziksel</span><span class="sxs-lookup"><span data-stu-id="8f9b9-105">Physical to Azure</span></span>](./site-recovery-prepare-target-physical-to-azure.md)

<span data-ttu-id="8f9b9-106">Bu makalede, Azure'da Windows veya Linux çalıştıran fiziksel sunucuları (x 64) çoğaltılması başlatmak üzere Azure ortamınızı hazırlamak açıklar.</span><span class="sxs-lookup"><span data-stu-id="8f9b9-106">This article describes how to prepare your Azure environment to start replicating physical servers (x64) running Windows or Linux into Azure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8f9b9-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="8f9b9-107">Prerequisites</span></span>

<span data-ttu-id="8f9b9-108">Makalede aşağıdaki varsayılmaktadır:</span><span class="sxs-lookup"><span data-stu-id="8f9b9-108">The article assumes the following:</span></span>
- <span data-ttu-id="8f9b9-109">Fiziksel sunucuyu korumak için bir kurtarma Hizmetleri kasası oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="8f9b9-109">You have created a Recovery Services Vault to protect your physical servers.</span></span> <span data-ttu-id="8f9b9-110">Kurtarma Hizmetleri Kasası'nı oluşturabilirsiniz [Azure portal](http://portal.azure.com "Azure portal").</span><span class="sxs-lookup"><span data-stu-id="8f9b9-110">You can create a Recovery Services Vault from the [Azure portal](http://portal.azure.com "Azure portal").</span></span>
- <span data-ttu-id="8f9b9-111">Sahip olduğunuz [, şirket içi ortamınızın Kurulumu](./site-recovery-set-up-physical-to-azure.md) fiziksel sunucuları Azure'a çoğaltma için.</span><span class="sxs-lookup"><span data-stu-id="8f9b9-111">You have [setup your on-premises environment](./site-recovery-set-up-physical-to-azure.md) to replicate physical servers to Azure.</span></span>

## <a name="prepare-target"></a><span data-ttu-id="8f9b9-112">Hedef hazırlama</span><span class="sxs-lookup"><span data-stu-id="8f9b9-112">Prepare target</span></span>

<span data-ttu-id="8f9b9-113">Tamamladıktan sonra **adım 1:Select koruma hedefi** ve **2. adım: kaynak hazırlama**, gittiğiniz **adım 3: hedef**</span><span class="sxs-lookup"><span data-stu-id="8f9b9-113">After completing the **Step 1:Select Protection goal** and **Step 2:Prepare Source**, you are taken to **Step 3: Target**</span></span>

![Hedef hazırlama](./media/site-recovery-prepare-target-physical-to-azure/prepare-target-physical-to-azure.png)

1. <span data-ttu-id="8f9b9-115">**Abonelik:** açılan menüsünde, fiziksel sunucularınızı çoğaltmak istediğiniz aboneliği seçin.</span><span class="sxs-lookup"><span data-stu-id="8f9b9-115">**Subscription:** From the drop down menu, select the Subscription that you want to replicate your physical servers to.</span></span>
2. <span data-ttu-id="8f9b9-116">**Dağıtım modeli:** (Klasik veya Resource Manager) dağıtım modeli seçin</span><span class="sxs-lookup"><span data-stu-id="8f9b9-116">**Deployment Model:** Select the deployment model (Classic or Resource Manager)</span></span>

<span data-ttu-id="8f9b9-117">Seçilen dağıtım modelini temel alan bir doğrulama fiziksel sunucularınızın en az bir uyumlu depolama hesabı ve sanal ağ çoğaltmak için hedef abonelik ve yük devretme olmasını sağlamak için çalıştırılır.</span><span class="sxs-lookup"><span data-stu-id="8f9b9-117">Based on the chosen deployment model, a validation is run to ensure that you have at least one compatible storage account and virtual network in the target subscription to replicate and failover your physical servers to.</span></span>

<span data-ttu-id="8f9b9-118">Doğrulamaları başarıyla tamamlandığında, sonraki adıma dönmek için Tamam'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="8f9b9-118">Once the validations complete successfully, click OK to go to the next step.</span></span>

<span data-ttu-id="8f9b9-119">Uyumlu Resource Manager depolama hesabı veya sanal ağ yok ya da daha fazla eklemek istediğiniz, tıklayarak bunu yapabilirsiniz **+ depolama hesabı** veya **+ ağ** düğmelerini dikey pencerenin üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="8f9b9-119">If you don't have a compatible Resource Manager storage account or virtual network, or would like to add more, you can do so by clicking the **+ Storage Account** or **+ Network** buttons on the top of the blade.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8f9b9-120">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8f9b9-120">Next steps</span></span>
<span data-ttu-id="8f9b9-121">[Çoğaltma ayarlarını yapılandırın](./site-recovery-setup-replication-settings-vmware.md).</span><span class="sxs-lookup"><span data-stu-id="8f9b9-121">[Configure replication settings](./site-recovery-setup-replication-settings-vmware.md).</span></span>
