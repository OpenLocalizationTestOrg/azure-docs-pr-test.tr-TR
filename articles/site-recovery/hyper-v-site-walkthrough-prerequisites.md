---
title: "Azure Site Recovery kullanarak Hyper-V tooAzure çoğaltmayı (System Center VMM olmadan) aaaReview hello önkoşulları | Microsoft Docs"
description: "Çoğaltma, yük devretme ve şirket içi Hyper-V sanal makineleri tooAzure kurtarma Azure Site Recovery ile ayarlamak için hello önkoşulları açıklar"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 7ef3fb46-52f5-4c8a-b1a1-658c2305762a
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/21/2017
ms.author: raynew
ms.openlocfilehash: 3eefc3b7e3982ec6c413c1db7f7784863f9c701d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="step-2-review-hello-prerequisites-for-hyper-v-without-vmm-tooazure-replication"></a><span data-ttu-id="81c45-103">2. adım: Hyper-V (VMM olmadan) tooAzure çoğaltma hello önkoşullarını gözden geçirme</span><span class="sxs-lookup"><span data-stu-id="81c45-103">Step 2: Review hello prerequisites for Hyper-V (without VMM) tooAzure replication</span></span>

<span data-ttu-id="81c45-104">Merhaba Önkoşullar hello tabloda özetlenmiştir.</span><span class="sxs-lookup"><span data-stu-id="81c45-104">hello prerequisites are summarized in hello table.</span></span>


<span data-ttu-id="81c45-105">**Önkoşul**</span><span class="sxs-lookup"><span data-stu-id="81c45-105">**Prerequisite**</span></span> | <span data-ttu-id="81c45-106">**Ayrıntılar**</span><span class="sxs-lookup"><span data-stu-id="81c45-106">**Details**</span></span> 
--- | --- 
<span data-ttu-id="81c45-107">**Azure**</span><span class="sxs-lookup"><span data-stu-id="81c45-107">**Azure**</span></span> | <span data-ttu-id="81c45-108">[Azure gereksinimleri](site-recovery-prereq.md#azure-requirements) hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="81c45-108">Learn about [Azure requirements](site-recovery-prereq.md#azure-requirements).</span></span>
<span data-ttu-id="81c45-109">**Şirket içi sunucular**</span><span class="sxs-lookup"><span data-stu-id="81c45-109">**On-premises servers**</span></span> | <span data-ttu-id="81c45-110">[Daha fazla bilgi edinin](site-recovery-prereq.md#disaster-recovery-of-hyper-v-vms-to-azure-no-vmm) hello şirket içi Hyper-V konakları için gereksinimleri hakkında.</span><span class="sxs-lookup"><span data-stu-id="81c45-110">[Learn more](site-recovery-prereq.md#disaster-recovery-of-hyper-v-vms-to-azure-no-vmm) about requirements for hello on-premises Hyper-V hosts.</span></span>
<span data-ttu-id="81c45-111">**Şirket içi Hyper-V VM'leri**</span><span class="sxs-lookup"><span data-stu-id="81c45-111">**On-premises Hyper-V VMs**</span></span> | <span data-ttu-id="81c45-112">Tooreplicate çalışıyor istediğiniz sanal makineleri bir [işletim sistemi desteklenen](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions)ve uygun olması [Azure önkoşulları](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span><span class="sxs-lookup"><span data-stu-id="81c45-112">VMs you want tooreplicate should be running a [supported operating system](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions), and conform with [Azure prerequisites](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>
<span data-ttu-id="81c45-113">**Azure URL'leri**</span><span class="sxs-lookup"><span data-stu-id="81c45-113">**Azure URLs**</span></span> | <span data-ttu-id="81c45-114">Hyper-V konakları toothese URL'leri erişim:</span><span class="sxs-lookup"><span data-stu-id="81c45-114">Hyper-V hosts need access toothese URLs:</span></span><br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]<br/><br/> <span data-ttu-id="81c45-115">IP adresi tabanlı güvenlik duvarı kuralları varsa, iletişim tooAzure izin emin olun.</span><span class="sxs-lookup"><span data-stu-id="81c45-115">If you have IP address-based firewall rules, ensure they allow communication tooAzure.</span></span><br/></br> <span data-ttu-id="81c45-116">Merhaba izin [Azure veri merkezi IP aralıkları](https://www.microsoft.com/download/confirmation.aspx?id=41653)ve hello HTTPS (443 numaralı) bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="81c45-116">Allow hello [Azure Datacenter IP Ranges](https://www.microsoft.com/download/confirmation.aspx?id=41653), and hello HTTPS (443) port.</span></span><br/></br> <span data-ttu-id="81c45-117">IP adres aralıklarını hello aboneliğinizin Azure bölgesi ve Batı ABD (erişim denetimi ve kimlik yönetimi için kullanılan) izin verir.</span><span class="sxs-lookup"><span data-stu-id="81c45-117">Allow IP address ranges for hello Azure region of your subscription, and for West US (used for Access Control and Identity Management).</span></span>



## <a name="next-steps"></a><span data-ttu-id="81c45-118">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="81c45-118">Next steps</span></span>

- <span data-ttu-id="81c45-119">Tam dağıtımını yaptığınız, çok gidin[3. adım: kapasite planlama](hyper-v-site-walkthrough-capacity.md)</span><span class="sxs-lookup"><span data-stu-id="81c45-119">If you're doing a full deployment, go too[Step 3: Plan capacity](hyper-v-site-walkthrough-capacity.md)</span></span>
- <span data-ttu-id="81c45-120">Basit test dağıtımını yaptığınız, çok gidin[4. adım: ağ planlama](hyper-v-site-walkthrough-network.md).</span><span class="sxs-lookup"><span data-stu-id="81c45-120">If you're doing a simple test deployment, go too[Step 4: Plan networking](hyper-v-site-walkthrough-network.md).</span></span>
