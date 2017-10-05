---
title: "Azure Site Kurtarma'yı kullanarak Azure çoğaltma (System Center VMM olmadan) Hyper-V için önkoşulları gözden | Microsoft Docs"
description: "Çoğaltma, yük devretme ve şirket içi Hyper-V sanal makineleri kurtarma Azure Site Recovery ile azure'a ayarlamak için Önkoşullar açıklanmaktadır"
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
ms.openlocfilehash: cbb5d3598ef91512991d7d1e9f854eb12980752b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="step-2-review-the-prerequisites-for-hyper-v-without-vmm-to-azure-replication"></a><span data-ttu-id="b7234-103">2. adım: Azure çoğaltma için Hyper-V (VMM olmadan) önkoşulları gözden geçirin</span><span class="sxs-lookup"><span data-stu-id="b7234-103">Step 2: Review the prerequisites for Hyper-V (without VMM) to Azure replication</span></span>

<span data-ttu-id="b7234-104">Önkoşullar tabloda özetlenmiştir.</span><span class="sxs-lookup"><span data-stu-id="b7234-104">The prerequisites are summarized in the table.</span></span>


<span data-ttu-id="b7234-105">**Önkoşul**</span><span class="sxs-lookup"><span data-stu-id="b7234-105">**Prerequisite**</span></span> | <span data-ttu-id="b7234-106">**Ayrıntılar**</span><span class="sxs-lookup"><span data-stu-id="b7234-106">**Details**</span></span> 
--- | --- 
<span data-ttu-id="b7234-107">**Azure**</span><span class="sxs-lookup"><span data-stu-id="b7234-107">**Azure**</span></span> | <span data-ttu-id="b7234-108">[Azure gereksinimleri](site-recovery-prereq.md#azure-requirements) hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="b7234-108">Learn about [Azure requirements](site-recovery-prereq.md#azure-requirements).</span></span>
<span data-ttu-id="b7234-109">**Şirket içi sunucular**</span><span class="sxs-lookup"><span data-stu-id="b7234-109">**On-premises servers**</span></span> | <span data-ttu-id="b7234-110">[Daha fazla bilgi edinin](site-recovery-prereq.md#disaster-recovery-of-hyper-v-vms-to-azure-no-vmm) şirket içi Hyper-V konakları için gereksinimleri hakkında.</span><span class="sxs-lookup"><span data-stu-id="b7234-110">[Learn more](site-recovery-prereq.md#disaster-recovery-of-hyper-v-vms-to-azure-no-vmm) about requirements for the on-premises Hyper-V hosts.</span></span>
<span data-ttu-id="b7234-111">**Şirket içi Hyper-V VM'leri**</span><span class="sxs-lookup"><span data-stu-id="b7234-111">**On-premises Hyper-V VMs**</span></span> | <span data-ttu-id="b7234-112">Çoğaltmak istediğiniz VM'lerin [desteklenen işletim sistemi](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions) çalıştırıyor olması ve [Azure önkoşullarına](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) uygun olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="b7234-112">VMs you want to replicate should be running a [supported operating system](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions), and conform with [Azure prerequisites](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>
<span data-ttu-id="b7234-113">**Azure URL'leri**</span><span class="sxs-lookup"><span data-stu-id="b7234-113">**Azure URLs**</span></span> | <span data-ttu-id="b7234-114">Hyper-V konakları bu URL'lere erişim gerekir:</span><span class="sxs-lookup"><span data-stu-id="b7234-114">Hyper-V hosts need access to these URLs:</span></span><br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]<br/><br/> <span data-ttu-id="b7234-115">IP adresi tabanlı güvenlik duvarı kurallarına sahipseniz bu kuralların Azure ile iletişim kurmaya izin verdiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="b7234-115">If you have IP address-based firewall rules, ensure they allow communication to Azure.</span></span><br/></br> <span data-ttu-id="b7234-116">[Azure Veri Merkezi IP Aralıkları](https://www.microsoft.com/download/confirmation.aspx?id=41653)'na ve HTTPS (443) bağlantı noktasına izin verin.</span><span class="sxs-lookup"><span data-stu-id="b7234-116">Allow the [Azure Datacenter IP Ranges](https://www.microsoft.com/download/confirmation.aspx?id=41653), and the HTTPS (443) port.</span></span><br/></br> <span data-ttu-id="b7234-117">Aboneliğinizin Azure bölgesi ve Batı ABD (Access Control ve Identity Management için kullanılır) için IP adresi aralıklarına izin verin.</span><span class="sxs-lookup"><span data-stu-id="b7234-117">Allow IP address ranges for the Azure region of your subscription, and for West US (used for Access Control and Identity Management).</span></span>



## <a name="next-steps"></a><span data-ttu-id="b7234-118">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b7234-118">Next steps</span></span>

- <span data-ttu-id="b7234-119">Tam dağıtımını yaptığınız, Git [3. adım: kapasite planlama](hyper-v-site-walkthrough-capacity.md)</span><span class="sxs-lookup"><span data-stu-id="b7234-119">If you're doing a full deployment, go to [Step 3: Plan capacity](hyper-v-site-walkthrough-capacity.md)</span></span>
- <span data-ttu-id="b7234-120">Basit test dağıtımını yaptığınız, Git [4. adım: ağ planlama](hyper-v-site-walkthrough-network.md).</span><span class="sxs-lookup"><span data-stu-id="b7234-120">If you're doing a simple test deployment, go to [Step 4: Plan networking](hyper-v-site-walkthrough-network.md).</span></span>
