---
title: "VMware VM çoğaltma tooAzure Azure Site Recovery ile çoğaltma ilkesi aaaSet | Microsoft Docs"
description: "Çoğaltma İlkesi tooset VMware Vm'lerini tooAzure depolama çoğaltırken gereken hello adımları özetler"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d7874bd8-6626-4668-9ec9-dbd2d26f8f81
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 12870f3f98a4dd412221b817581403cd4bf7a76d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="step-9-set-up-a-replication-policy-for-vmware-vm-replication-tooazure"></a><span data-ttu-id="ea4b5-103">9. adım: VMware VM çoğaltma tooAzure için bir çoğaltma ilkesi ayarlama</span><span class="sxs-lookup"><span data-stu-id="ea4b5-103">Step 9: Set up a replication policy for VMware VM replication tooAzure</span></span>


<span data-ttu-id="ea4b5-104">Bu makalede nasıl hello kullanarak VMware sanal makinelerini tooAzure çoğaltırken çoğaltma ilkesi tooset [Azure Site Recovery](site-recovery-overview.md) hello Azure portal hizmeti.</span><span class="sxs-lookup"><span data-stu-id="ea4b5-104">This article describes how tooset up a replication policy when you're replicating VMware VMs tooAzure using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>


<span data-ttu-id="ea4b5-105">POST açıklamaları ve soruları hello altındaki bu makalenin veya hello [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="ea4b5-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="configure-a-policy"></a><span data-ttu-id="ea4b5-106">Bir ilke yapılandırın</span><span class="sxs-lookup"><span data-stu-id="ea4b5-106">Configure a policy</span></span>

<span data-ttu-id="ea4b5-107">Başlamadan önce hızlı bir video genel bakış alın:</span><span class="sxs-lookup"><span data-stu-id="ea4b5-107">Get a quick video overview before you start:</span></span>
> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video2-vCenter-Server-Discovery-and-Replication-Policy/player]

1. <span data-ttu-id="ea4b5-108">Yeni bir çoğaltma ilkesi toocreate tıklatın **Site Recovery altyapısı** > **çoğaltma ilkeleri** > **+ Çoğaltma İlkesi**.</span><span class="sxs-lookup"><span data-stu-id="ea4b5-108">toocreate a new replication policy, click **Site Recovery infrastructure** > **Replication Policies** > **+Replication Policy**.</span></span>
2. <span data-ttu-id="ea4b5-109">İçinde **çoğaltma ilkesi oluşturun**, bir ilke adı belirtin.</span><span class="sxs-lookup"><span data-stu-id="ea4b5-109">In **Create replication policy**, specify a policy name.</span></span>
3. <span data-ttu-id="ea4b5-110">İçinde **RPO eşik**, hello RPO sınırını belirtin.</span><span class="sxs-lookup"><span data-stu-id="ea4b5-110">In **RPO threshold**, specify hello RPO limit.</span></span> <span data-ttu-id="ea4b5-111">Bu değer, ne sıklıkta belirtir veri kurtarma noktaları oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="ea4b5-111">This value specifies how often data recovery points are created.</span></span> <span data-ttu-id="ea4b5-112">Sürekli çoğaltma bu sınırı aşarsa bir uyarı üretilir.</span><span class="sxs-lookup"><span data-stu-id="ea4b5-112">An alert is generated if continuous replication exceeds this limit.</span></span>
4. <span data-ttu-id="ea4b5-113">İçinde **kurtarma noktası bekletme**, ne kadar süre (saat olarak) belirtin hello bekletme penceresi olduğu için her kurtarma noktası.</span><span class="sxs-lookup"><span data-stu-id="ea4b5-113">In **Recovery point retention**, specify (in hours) how long hello retention window is for each recovery point.</span></span> <span data-ttu-id="ea4b5-114">Çoğaltılan VM'ler olabilir bir pencerede tooany noktası kurtarıldı.</span><span class="sxs-lookup"><span data-stu-id="ea4b5-114">Replicated VMs can be recovered tooany point in a window.</span></span> <span data-ttu-id="ea4b5-115">Saat bekletme makineler için desteklenen too24 yukarı toopremium depolama ile standart depolama için 72 saat çoğaltılan.</span><span class="sxs-lookup"><span data-stu-id="ea4b5-115">Up too24 hours retention is supported for machines replicated toopremium storage, and 72 hours for standard storage.</span></span>
5. <span data-ttu-id="ea4b5-116">İçinde **uygulamayla tutarlı anlık görüntü sıklığı**, belirtin ne sıklıkta (dakika cinsinden) uygulamayla tutarlı anlık görüntüleri içeren kurtarma noktaları oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="ea4b5-116">In **App-consistent snapshot frequency**, specify how often (in minutes) recovery points containing application-consistent snapshots will be created.</span></span> <span data-ttu-id="ea4b5-117">Tıklatın **Tamam** toocreate hello ilkesi.</span><span class="sxs-lookup"><span data-stu-id="ea4b5-117">Click **OK** toocreate hello policy.</span></span>

    ![Çoğaltma ilkesi](./media/vmware-walkthrough-replication/gs-replication2.png)
8. <span data-ttu-id="ea4b5-119">Yeni bir ilke oluşturduğunuzda, otomatik olarak hello yapılandırma sunucusu ile ilişkili.</span><span class="sxs-lookup"><span data-stu-id="ea4b5-119">When you create a new policy it's automatically associated with hello configuration server.</span></span> <span data-ttu-id="ea4b5-120">Varsayılan olarak, eşleşen bir ilkesi yeniden çalışma için otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="ea4b5-120">By default, a matching policy is automatically created for failback.</span></span> <span data-ttu-id="ea4b5-121">Örneğin, hello çoğaltma ilkesi ise **rep İlkesi** hello geri dönme ilkesini sonra **rep İlkesi yeniden**.</span><span class="sxs-lookup"><span data-stu-id="ea4b5-121">For example, if hello replication policy is **rep-policy** then hello failback policy will be **rep-policy-failback**.</span></span> <span data-ttu-id="ea4b5-122">Bir azure'dan başlatana kadar bu ilkeyi kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="ea4b5-122">This policy isn't used until you initiate a failback from Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ea4b5-123">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ea4b5-123">Next steps</span></span>

<span data-ttu-id="ea4b5-124">Çok Git[adım 10: hello Mobility hizmetini yükleme](vmware-walkthrough-install-mobility.md)</span><span class="sxs-lookup"><span data-stu-id="ea4b5-124">Go too[Step 10: Install hello Mobility service](vmware-walkthrough-install-mobility.md)</span></span>
