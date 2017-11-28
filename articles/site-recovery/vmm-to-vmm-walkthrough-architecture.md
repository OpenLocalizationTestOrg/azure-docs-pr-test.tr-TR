---
title: "Hyper-V çoğaltma tooa Azure Site Recovery ile ikincil site için aaaReview hello mimarisi | Microsoft Docs"
description: "Bu makalede, şirket içi Hyper-V sanal makineleri tooa ikincil System Center VMM site Azure Site Recovery ile çoğaltmak için hello mimarisine genel bakış sağlar."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 07099161-4cc7-4f32-8eb9-2a71bbf0750b
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: 0de4b4e8601116c73e6fd710597ce4e561884368
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="step-1-review-hello-architecture-for-hyper-v-replication-tooa-secondary-site"></a><span data-ttu-id="38d08-103">1. adım: Hyper-V çoğaltma tooa ikincil site gözden geçirme hello mimarisi</span><span class="sxs-lookup"><span data-stu-id="38d08-103">Step 1: Review hello architecture for Hyper-V replication tooa secondary site</span></span>

<span data-ttu-id="38d08-104">Bu makalede hello bileşenleri ve işlemler çoğaltırken söz konusu şirket içi System Center Virtual Machine Manager (VMM) bulutlarında, tooa hello kullanarak ikincil VMM sitesi Hyper-V sanal makineleri (VM'ler) [Azure Site Recovery](site-recovery-overview.md)hello Azure portal hizmeti.</span><span class="sxs-lookup"><span data-stu-id="38d08-104">This article describes hello components and processes involved when replicating on-premises Hyper-V virtual machines (VMs) in System Center Virtual Machine Manager (VMM) clouds, tooa secondary VMM site using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="38d08-105">Bu makalenin veya hello hello altındaki tüm yorumlar sonrası [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="38d08-105">Post any comments at hello bottom of this article, or in hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>



## <a name="architectural-components"></a><span data-ttu-id="38d08-106">Mimari bileşenler</span><span class="sxs-lookup"><span data-stu-id="38d08-106">Architectural components</span></span>

<span data-ttu-id="38d08-107">İşte Hyper-V sanal makineleri tooa ikincil VMM sitesi çoğaltmak için gerekir.</span><span class="sxs-lookup"><span data-stu-id="38d08-107">Here's what you need for replicating Hyper-V VMs tooa secondary VMM site.</span></span>

<span data-ttu-id="38d08-108">**Bileşen**</span><span class="sxs-lookup"><span data-stu-id="38d08-108">**Component**</span></span> | <span data-ttu-id="38d08-109">**Konum**</span><span class="sxs-lookup"><span data-stu-id="38d08-109">**Location**</span></span> | <span data-ttu-id="38d08-110">**Ayrıntılar**</span><span class="sxs-lookup"><span data-stu-id="38d08-110">**Details**</span></span>
--- | --- | ---
<span data-ttu-id="38d08-111">**Azure**</span><span class="sxs-lookup"><span data-stu-id="38d08-111">**Azure**</span></span> | <span data-ttu-id="38d08-112">Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="38d08-112">Subscription in Azure.</span></span> | <span data-ttu-id="38d08-113">Kurtarma Hizmetleri kasası hello Azure aboneliği tooorchestrate oluşturup VMM konumları arasında çoğaltma yönetin.</span><span class="sxs-lookup"><span data-stu-id="38d08-113">You create a Recovery Services vault in hello Azure subscription, tooorchestrate and manage replication between VMM locations.</span></span>
<span data-ttu-id="38d08-114">**VMM sunucusu**</span><span class="sxs-lookup"><span data-stu-id="38d08-114">**VMM server**</span></span> | <span data-ttu-id="38d08-115">Birincil ve ikincil VMM konumu gerekir.</span><span class="sxs-lookup"><span data-stu-id="38d08-115">You need a VMM primary and secondary location.</span></span> | <span data-ttu-id="38d08-116">Bir VMM sunucusunun hello birincil sitede ve hello ikincil sitedeki öneririz</span><span class="sxs-lookup"><span data-stu-id="38d08-116">We recommend a VMM server in hello primary site, and one in hello secondary site</span></span> 
<span data-ttu-id="38d08-117">**Hyper-V sunucusu**</span><span class="sxs-lookup"><span data-stu-id="38d08-117">**Hyper-V server**</span></span> |  <span data-ttu-id="38d08-118">Bir veya daha fazla Hyper-V ana bilgisayar sunucuları hello birincil ve ikincil VMM bulutlarında.</span><span class="sxs-lookup"><span data-stu-id="38d08-118">One or more Hyper-V host servers in hello primary and secondary VMM clouds.</span></span> | <span data-ttu-id="38d08-119">Veri hello LAN veya Kerberos veya sertifika kimlik doğrulaması kullanarak VPN üzerinden hello birincil ve ikincil Hyper-V ana bilgisayar sunucuları arasında çoğaltılır.</span><span class="sxs-lookup"><span data-stu-id="38d08-119">Data is replicated between hello primary and secondary Hyper-V host servers over hello LAN or VPN, using Kerberos or certificate authentication.</span></span>  
<span data-ttu-id="38d08-120">**Hyper-V VM’leri**</span><span class="sxs-lookup"><span data-stu-id="38d08-120">**Hyper-V VMs**</span></span> | <span data-ttu-id="38d08-121">Hyper-V ana bilgisayar sunucusunda.</span><span class="sxs-lookup"><span data-stu-id="38d08-121">On Hyper-V host server.</span></span> | <span data-ttu-id="38d08-122">Merhaba kaynak ana bilgisayar sunucusunun tooreplicate istediğiniz en az bir VM'ye sahip olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="38d08-122">hello source host server should have at least one VM that you want tooreplicate.</span></span>

## <a name="replication-process"></a><span data-ttu-id="38d08-123">Çoğaltma işlemi</span><span class="sxs-lookup"><span data-stu-id="38d08-123">Replication process</span></span>

1. <span data-ttu-id="38d08-124">Azure hesabı hello ayarlayın, bir kurtarma Hizmetleri kasası oluşturun ve istediğinizi belirtin tooreplicate.</span><span class="sxs-lookup"><span data-stu-id="38d08-124">You set up hello Azure account, create a Recovery Services vault, and specify what you want tooreplicate.</span></span>
2. <span data-ttu-id="38d08-125">Hello Azure Site kurtarma sağlayıcısı VMM sunucuları ve her Hyper-V ana bilgisayarda hello Microsoft Azure kurtarma Hizmetleri aracısını yükleme içeren hello kaynak ve hedef çoğaltma ayarlarını yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="38d08-125">You configure hello source and target replication settings, which includes installing hello Azure Site Recovery Provider on VMM servers, and hello Microsoft Azure Recovery Services agent on each Hyper-V host.</span></span>
3. <span data-ttu-id="38d08-126">Merhaba kaynak VMM bulutu için bir çoğaltma ilkesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="38d08-126">You create a replication policy for hello source VMM cloud.</span></span> <span data-ttu-id="38d08-127">Merhaba, uygulanan tooall hello bulut ana bilgisayarda yer alan VM'ler ilkesidir.</span><span class="sxs-lookup"><span data-stu-id="38d08-127">hello policy is applied tooall VMs located on hosts in hello cloud.</span></span>
4. <span data-ttu-id="38d08-128">Her VMM için çoğaltmayı etkinleştirmek ve seçtiğiniz hello ayarlarına uygun olarak bir VM başlangıç çoğaltması gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="38d08-128">You enable replication for each VMM, and initial replication of a VM occurs in accordance with hello settings you choose.</span></span>
5. <span data-ttu-id="38d08-129">İlk çoğaltma sonrasında, delta değişikliklerin çoğaltılması başlar.</span><span class="sxs-lookup"><span data-stu-id="38d08-129">After initial replication, replication of delta changes begins.</span></span> <span data-ttu-id="38d08-130">Bir öğe için izlenen değişiklikler bir .hrl dosyasında saklanır.</span><span class="sxs-lookup"><span data-stu-id="38d08-130">Tracked changes for an item are held in a .hrl file.</span></span>


![Şirket içi tooon içi](./media/vmm-to-vmm-walkthrough-architecture/arch-onprem-onprem.png)

## <a name="failover-and-failback-process"></a><span data-ttu-id="38d08-132">Yük devretme ve yeniden çalışma işlemi</span><span class="sxs-lookup"><span data-stu-id="38d08-132">Failover and failback process</span></span>

1. <span data-ttu-id="38d08-133">Şirket içi siteler arasında planlanmış veya planlanmamış bir [yük devretme](site-recovery-failover.md) gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="38d08-133">You can run a planned or unplanned [failover](site-recovery-failover.md) between on-premises sites.</span></span> <span data-ttu-id="38d08-134">Planlanmış bir yük devretme çalıştırın, sonra kaynak VM'ler tooensure kapatın, veri kaybı.</span><span class="sxs-lookup"><span data-stu-id="38d08-134">If you run a planned failover, then source VMs are shut down tooensure no data loss.</span></span>
2. <span data-ttu-id="38d08-135">Üzerinde tek bir makine başarısız veya oluşturma [kurtarma planlarına](site-recovery-create-recovery-plans.md) birden fazla makine tooorchestrate yük devretme.</span><span class="sxs-lookup"><span data-stu-id="38d08-135">You can fail over a single machine, or create [recovery plans](site-recovery-create-recovery-plans.md) tooorchestrate failover of multiple machines.</span></span>
4. <span data-ttu-id="38d08-136">Merhaba yük devretme makineler hello ikincil konumdaki sonra bir planlanmamış yük devretme tooa ikincil site gerçekleştirirseniz koruma veya çoğaltma için etkin değil.</span><span class="sxs-lookup"><span data-stu-id="38d08-136">If you perform an unplanned failover tooa secondary site, after hello failover machines in hello secondary location aren't enabled for protection or replication.</span></span> <span data-ttu-id="38d08-137">Planlanmış bir yük devretme hello yük devretme sonrasında çalıştırdıysanız hello ikincil konumdaki makineler korunur.</span><span class="sxs-lookup"><span data-stu-id="38d08-137">If you ran a planned failover, after hello failover, machines in hello secondary location are protected.</span></span>
5. <span data-ttu-id="38d08-138">Ardından, VM hello çoğaltmasından hello yük devretme toostart erişilirken hello iş yükü uygulayın.</span><span class="sxs-lookup"><span data-stu-id="38d08-138">Then, you commit hello failover toostart accessing hello workload from hello replica VM.</span></span>
6. <span data-ttu-id="38d08-139">Birincil sitenizi yeniden kullanılabilir duruma geldiğinde, çoğaltmayı tersine çevirme tooreplicate hello ikincil site toohello birincil gelen başlatır.</span><span class="sxs-lookup"><span data-stu-id="38d08-139">When your primary site is available again, you initiate reverse replication tooreplicate from hello secondary site toohello primary.</span></span> <span data-ttu-id="38d08-140">Çoğaltmayı tersine çevirme hello sanal makineleri korumalı bir duruma getirir, ancak hello ikincil veri merkezine hala hello etkin konumdur.</span><span class="sxs-lookup"><span data-stu-id="38d08-140">Reverse replication brings hello virtual machines into a protected state, but hello secondary datacenter is still hello active location.</span></span>
7. <span data-ttu-id="38d08-141">toomake hello birincil site hello etkin konuma yeniden planlı bir yük devretme ikincil tooprimary, başka bir tersine çoğaltma tarafından izlenen işlemini başlatır.</span><span class="sxs-lookup"><span data-stu-id="38d08-141">toomake hello primary site into hello active location again, you initiate a planned failover from secondary tooprimary, followed by another reverse replication.</span></span>



## <a name="next-steps"></a><span data-ttu-id="38d08-142">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="38d08-142">Next steps</span></span>

<span data-ttu-id="38d08-143">Çok Git[2. adım: gözden hello Önkoşullar ve sınırlamalar](vmm-to-vmm-walkthrough-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="38d08-143">Go too[Step 2: Review hello prerequisites and limitations](vmm-to-vmm-walkthrough-prerequisites.md).</span></span>
