---
title: "Hyper-V VM çoğaltma tooa Azure Site Recovery ile ikincil site için aaaMap ağları | Microsoft Docs"
description: "Hyper-V sanal makineleri tooa Azure Site Recovery ile ikincil VMM sitesi çoğaltırken toomap nasıl ağları açıklar."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 461b7c1c-ef61-4005-aeec-2324e727a3d0
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: d4f621df4ce08ae055bc6809daea0b71b76754ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="step-7-map-networks-for-hyper-v-vm-replication-tooa-secondary-site"></a><span data-ttu-id="20f69-103">7. adım: Hyper-V VM çoğaltma tooa ikincil site için ağları Eşle</span><span class="sxs-lookup"><span data-stu-id="20f69-103">Step 7: Map networks for Hyper-V VM replication tooa secondary site</span></span>


<span data-ttu-id="20f69-104">Ayarladıktan sonra [kaynak ve hedef ayarları](vmm-to-vmm-walkthrough-source-target.md) Hyper-V sanal makineleri (VM'ler) tooa ikincil System Center Virtual Machine Manager (VMM) site çoğaltmak için bu makale tooconfigure ağ eşlemesi için Hyper-V sanal kullanın Makine (VM) çoğaltma tooa ikincil site, kullanarak [Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="20f69-104">After setting up [source and target settings](vmm-to-vmm-walkthrough-source-target.md) for replicating Hyper-V virtual machines (VMs) tooa secondary System Center Virtual Machine Manager (VMM) site, use this article tooconfigure network mapping for Hyper-V virtual machine (VM) replication tooa secondary site, using  [Azure Site Recovery](site-recovery-overview.md).</span></span>

<span data-ttu-id="20f69-105">Bu makaleyi okuduktan sonra tüm yorumlar hello altındaki ya da hello sonrası [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="20f69-105">After reading this article, post any comments at hello bottom, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="before-you-start"></a><span data-ttu-id="20f69-106">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="20f69-106">Before you start</span></span>

- <span data-ttu-id="20f69-107">Hakkında bilgi edinin [ağ eşlemesi](vmm-to-vmm-walkthrough-network.md#network-mapping-overview) başlamadan önce.</span><span class="sxs-lookup"><span data-stu-id="20f69-107">Learn about [network mapping](vmm-to-vmm-walkthrough-network.md#network-mapping-overview) before you start.</span></span>
- <span data-ttu-id="20f69-108">Sanal makineler VMM sunucularında bağlı tooa VM ağı olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="20f69-108">Verify that virtual machines on VMM servers are connected tooa VM network.</span></span>

## <a name="configure-network-mapping"></a><span data-ttu-id="20f69-109">Ağ eşlemesini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="20f69-109">Configure network mapping</span></span>

1. <span data-ttu-id="20f69-110">İçinde **ağ eşlemesi** > **ağ eşlemeleri**, tıklatın **+ ağ eşlemesi**.</span><span class="sxs-lookup"><span data-stu-id="20f69-110">In **Network Mapping** > **Network mappings**, click **+Network Mapping**.</span></span>
2. <span data-ttu-id="20f69-111">İçinde **ağ eşlemesi Ekle** sekmesinde hello kaynak seçin ve VMM sunucuyu hedefleyebilir.</span><span class="sxs-lookup"><span data-stu-id="20f69-111">In **Add network mapping** tab, select hello source and target VMM servers.</span></span> <span data-ttu-id="20f69-112">Merhaba VMM sunucular ile ilişkilendirilen hello VM ağları alınır.</span><span class="sxs-lookup"><span data-stu-id="20f69-112">hello VM networks associated with hello VMM servers are retrieved.</span></span>
3. <span data-ttu-id="20f69-113">İçinde **kaynak ağ**seçin toouse hello birincil VMM sunucusu ile ilişkili bir VM ağı hello listesinden istediğiniz hello ağ.</span><span class="sxs-lookup"><span data-stu-id="20f69-113">In **Source network**, select hello network you want toouse from hello list of VM networks associated with hello primary VMM server.</span></span>
4. <span data-ttu-id="20f69-114">İçinde **hedef ağ**seçin hello ikincil VMM sunucusunda toouse istediğiniz hello ağ.</span><span class="sxs-lookup"><span data-stu-id="20f69-114">In **Target network**, select hello network you want toouse on hello secondary VMM server.</span></span> <span data-ttu-id="20f69-115">Daha sonra, **Tamam**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="20f69-115">Then click **OK**.</span></span>

    ![Ağ eşlemesi](./media/vmm-to-vmm-walkthrough-network-mapping/network-mapping2.png)

<span data-ttu-id="20f69-117">Ağ eşlemesi başladığında gerçekleşecekler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="20f69-117">Here's what happens when network mapping begins:</span></span>

* <span data-ttu-id="20f69-118">Tüm mevcut çoğaltma toohello kaynak VM ağına karşılık gelen makineleri bağlı toohello hedef VM ağı olacaktır.</span><span class="sxs-lookup"><span data-stu-id="20f69-118">Any existing replica virtual machines that correspond toohello source VM network will be connected toohello target VM network.</span></span>
* <span data-ttu-id="20f69-119">Kaynak VM ağına bağlı toohello olan yeni sanal makinelere bağlı toohello hedef eşlenen ağ çoğaltma işleminden sonra olacaktır.</span><span class="sxs-lookup"><span data-stu-id="20f69-119">New virtual machines that are connected toohello source VM network will be connected toohello target mapped network after replication.</span></span>
* <span data-ttu-id="20f69-120">Yeni bir ağ ile varolan bir eşlemesini değiştirirseniz, çoğaltma sanal makineleri hello yeni ayarlar kullanılarak bağlanır.</span><span class="sxs-lookup"><span data-stu-id="20f69-120">If you modify an existing mapping with a new network, replica virtual machines will be connected using hello new settings.</span></span>
* <span data-ttu-id="20f69-121">Hello hedef ağın birden çok alt ağı varsa ve bu alt ağlardan biri olan hello adıyla aynı alt ağda hangi hello kaynak sanal makinenin bulunduğu sonra hello çoğaltma sanal makinesi yük devretme sonrasında bağlı toothat hedef alt olacaktır.</span><span class="sxs-lookup"><span data-stu-id="20f69-121">If hello target network has multiple subnets and one of those subnets has hello same name as subnet on which hello source virtual machine is located, then hello replica virtual machine will be connected toothat target subnet after failover.</span></span> <span data-ttu-id="20f69-122">Eşleşen ada sahip bir hedef alt ağ ise hello sanal makineye bağlı toohello hello ağdaki ilk alt ağ olacaktır.</span><span class="sxs-lookup"><span data-stu-id="20f69-122">If there’s no target subnet with a matching name, hello virtual machine will be connected toohello first subnet in hello network.</span></span>



## <a name="next-steps"></a><span data-ttu-id="20f69-123">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="20f69-123">Next steps</span></span>

<span data-ttu-id="20f69-124">Çok Git[adım 8: bir çoğaltma ilkesi yapılandırma](vmm-to-vmm-walkthrough-replication.md).</span><span class="sxs-lookup"><span data-stu-id="20f69-124">Go too[Step 8: Configure a replication policy](vmm-to-vmm-walkthrough-replication.md).</span></span>
