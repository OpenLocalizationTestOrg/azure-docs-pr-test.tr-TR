---
title: "vmm'de Hyper-V Vm'lerini çoğaltma için aaaConfigure ağ eşlemesi bulut Azure Site Recovery ile tooAzure | Microsoft Docs"
description: "Vmm'de Hyper-V sanal makineleri çoğaltırken tooconfigure ağ eşlemesi tooAzure Azure Site Recovery ile nasıl Bulutlar açıklar"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: tysonn
ms.assetid: 8e7d868e-00f3-4e8b-9a9e-f23365abf6ac
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: 081a9fdb0ffa4114099e9bcb9c1b1e43ad26ecbb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="step-9-configure-network-mapping-for-hyper-v-replication-with-vmm-tooazure"></a><span data-ttu-id="4e1e1-103">9. adım: Hyper-V çoğaltma (VMM ile) tooAzure için ağ eşlemesini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="4e1e1-103">Step 9: Configure network mapping for Hyper-V replication (with VMM) tooAzure</span></span>

<span data-ttu-id="4e1e1-104">Merhaba ayarladıktan sonra [kaynak ve hedef çoğaltma ayarları](vmm-to-azure-walkthrough-source-target.md), bu makale tooconfigure ağ eşlemesi toomap şirket içi VMM VM ağları ve Azure ağları arasında kullanın.</span><span class="sxs-lookup"><span data-stu-id="4e1e1-104">After you set up hello [source and target replication settings](vmm-to-azure-walkthrough-source-target.md), use this article tooconfigure network mapping toomap between on-premises VMM VM networks, and Azure networks.</span></span>

<span data-ttu-id="4e1e1-105">POST açıklamaları ve soruları hello altındaki bu makalenin veya hello [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="4e1e1-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="before-you-start"></a><span data-ttu-id="4e1e1-106">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="4e1e1-106">Before you start</span></span>

- <span data-ttu-id="4e1e1-107">Hakkında bilgi edinin [ağ eşlemesi](vmm-to-azure-walkthrough-network.md#network-mapping-for-replication-to-azure).</span><span class="sxs-lookup"><span data-stu-id="4e1e1-107">Learn about [network mapping](vmm-to-azure-walkthrough-network.md#network-mapping-for-replication-to-azure).</span></span>
- <span data-ttu-id="4e1e1-108">[VMM ağ eşlemesi için hazırlanma](vmm-to-azure-walkthrough-network.md#prepare-vmm-for-network-mapping).</span><span class="sxs-lookup"><span data-stu-id="4e1e1-108">[Prepare VMM for network mapping](vmm-to-azure-walkthrough-network.md#prepare-vmm-for-network-mapping).</span></span> 
- <span data-ttu-id="4e1e1-109">Sanal makineler hello VMM sunucusunda bağlı tooa VM ağı olduğunu ve en az bir Azure sanal ağı oluşturduğunuzu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="4e1e1-109">Verify that virtual machines on hello VMM server are connected tooa VM network, and that you've created at least one Azure virtual network.</span></span> <span data-ttu-id="4e1e1-110">Birden fazla VM ağı eşlenen tooa tek Azure ağ olabilir.</span><span class="sxs-lookup"><span data-stu-id="4e1e1-110">Multiple VM networks can be mapped tooa single Azure network.</span></span>

## <a name="configure-mapping"></a><span data-ttu-id="4e1e1-111">Eşlemeyi yapılandırın</span><span class="sxs-lookup"><span data-stu-id="4e1e1-111">Configure mapping</span></span>

<span data-ttu-id="4e1e1-112">Eşleme işlemini şu şekilde yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="4e1e1-112">Configure mapping as follows:</span></span>

1. <span data-ttu-id="4e1e1-113">İçinde **Site Recovery altyapısı** > **ağ eşlemeleri** > **ağ eşlemesi**, hello tıklatın **+ ağ eşlemesi**  simgesi.</span><span class="sxs-lookup"><span data-stu-id="4e1e1-113">In **Site Recovery Infrastructure** > **Network mappings** > **Network Mapping**, click hello **+Network Mapping** icon.</span></span>

    ![Ağ eşlemesi](./media/vmm-to-azure-walkthrough-network-mapping/network-mapping1.png)
2. <span data-ttu-id="4e1e1-115">İçinde **ağ eşlemesi Ekle**seçin hello kaynak VMM sunucusunu ve **Azure** hello hedefi olarak.</span><span class="sxs-lookup"><span data-stu-id="4e1e1-115">In **Add network mapping**, select hello source VMM server, and **Azure** as hello target.</span></span>
3. <span data-ttu-id="4e1e1-116">Yük devretme sonrasında Hello abonelik ve hello dağıtım modeli doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="4e1e1-116">Verify hello subscription and hello deployment model after failover.</span></span>
4. <span data-ttu-id="4e1e1-117">İçinde **kaynak ağ**seçin hello kaynak şirket içi VM ağını hello VMM sunucusuyla ilişkili hello listeden toomap istiyor.</span><span class="sxs-lookup"><span data-stu-id="4e1e1-117">In **Source network**, select hello source on-premises VM network you want toomap from hello list associated with hello VMM server.</span></span>
5. <span data-ttu-id="4e1e1-118">İçinde **hedef ağ**, hello hangi çoğaltma Azure VM'ler konumlandırılacağı oluşturuldukları zaman Azure ağı seçin.</span><span class="sxs-lookup"><span data-stu-id="4e1e1-118">In **Target network**, select hello Azure network in which replica Azure VMs will be located when they're created.</span></span> <span data-ttu-id="4e1e1-119">Daha sonra, **Tamam**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4e1e1-119">Then click **OK**.</span></span>

    ![Ağ eşlemesi](./media/vmm-to-azure-walkthrough-network-mapping/network-mapping2.png)

<span data-ttu-id="4e1e1-121">Ağ eşlemesi başladığında gerçekleşecekler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="4e1e1-121">Here's what happens when network mapping begins:</span></span>

* <span data-ttu-id="4e1e1-122">Eşleme başladığında hello kaynak VM ağındaki VM'ler bağlı toohello hedef ağ tabanlıdır.</span><span class="sxs-lookup"><span data-stu-id="4e1e1-122">Existing VMs on hello source VM network are connected toohello target network when mapping begins.</span></span> <span data-ttu-id="4e1e1-123">Yeni sanal makineleri bağlı toohello kaynak VM ağına bağlı Çoğaltma gerçekleştiğinde eşlenen Azure ağ toohello.</span><span class="sxs-lookup"><span data-stu-id="4e1e1-123">New VMs connected toohello source VM network are connected toohello mapped Azure network when replication occurs.</span></span>
* <span data-ttu-id="4e1e1-124">Varolan bir ağ eşlemesini değiştirirseniz, çoğaltma sanal makineleri hello yeni ayarları kullanarak bağlanır.</span><span class="sxs-lookup"><span data-stu-id="4e1e1-124">If you modify an existing network mapping, replica virtual machines connect using hello new settings.</span></span>
* <span data-ttu-id="4e1e1-125">Merhaba hedef ağ birden çok alt ağı varsa ve bu alt ağlardan biri olan hello adıyla aynı alt ağda hangi hello kaynak sanal makinenin bulunduğu sonra hello çoğaltma sanal makinesi yük devretme sonrasında toothat hedef alt bağlanır.</span><span class="sxs-lookup"><span data-stu-id="4e1e1-125">If hello target network has multiple subnets, and one of those subnets has hello same name as subnet on which hello source virtual machine is located, then hello replica virtual machine connects toothat target subnet after failover.</span></span>
* <span data-ttu-id="4e1e1-126">Eşleşen ada sahip bir hedef alt ağ varsa, hello sanal makine toohello hello ağdaki ilk alt ağa bağlanır.</span><span class="sxs-lookup"><span data-stu-id="4e1e1-126">If there’s no target subnet with a matching name, hello virtual machine connects toohello first subnet in hello network.</span></span>



## <a name="next-steps"></a><span data-ttu-id="4e1e1-127">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4e1e1-127">Next steps</span></span>

<span data-ttu-id="4e1e1-128">Çok Git[adım 10: bir çoğaltma ilkesi oluşturun](vmm-to-azure-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="4e1e1-128">Go too[Step 10: Create a replication policy](vmm-to-azure-walkthrough-replication.md)</span></span>
