---
title: "Azure Site Recovery ile azure'a VMware VM çoğaltması için bir çoğaltma ilkesi ayarlama | Microsoft Docs"
description: "VMware Vm'leri Azure depolama alanına çoğaltırken bir çoğaltma ilkesi ayarlamak için gereken adımları özetler"
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
ms.openlocfilehash: 3c4b7ad16e6a03fb605447def18f7475d502fdd1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="step-9-set-up-a-replication-policy-for-vmware-vm-replication-to-azure"></a><span data-ttu-id="4449a-103">9. adım: VMware VM Azure'a çoğaltma için bir çoğaltma ilkesi ayarlama</span><span class="sxs-lookup"><span data-stu-id="4449a-103">Step 9: Set up a replication policy for VMware VM replication to Azure</span></span>


<span data-ttu-id="4449a-104">Bu makalede Azure kullanarak VMware sanal makinelerini çoğaltma yapıyorsanız, bir çoğaltma ilkesi ayarlamak nasıl [Azure Site Recovery](site-recovery-overview.md) Azure portalında hizmet.</span><span class="sxs-lookup"><span data-stu-id="4449a-104">This article describes how to set up a replication policy when you're replicating VMware VMs to Azure using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>


<span data-ttu-id="4449a-105">POST açıklamaları ve soruları alt bu makalenin veya üzerinde [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="4449a-105">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="configure-a-policy"></a><span data-ttu-id="4449a-106">Bir ilke yapılandırın</span><span class="sxs-lookup"><span data-stu-id="4449a-106">Configure a policy</span></span>

<span data-ttu-id="4449a-107">Başlamadan önce hızlı bir video genel bakış alın:</span><span class="sxs-lookup"><span data-stu-id="4449a-107">Get a quick video overview before you start:</span></span>
> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video2-vCenter-Server-Discovery-and-Replication-Policy/player]

1. <span data-ttu-id="4449a-108">Yeni bir çoğaltma ilkesi oluşturmak için tıklatın **Site Recovery altyapısı** > **çoğaltma ilkeleri** > **+ Çoğaltma İlkesi**.</span><span class="sxs-lookup"><span data-stu-id="4449a-108">To create a new replication policy, click **Site Recovery infrastructure** > **Replication Policies** > **+Replication Policy**.</span></span>
2. <span data-ttu-id="4449a-109">İçinde **çoğaltma ilkesi oluşturun**, bir ilke adı belirtin.</span><span class="sxs-lookup"><span data-stu-id="4449a-109">In **Create replication policy**, specify a policy name.</span></span>
3. <span data-ttu-id="4449a-110">**RPO eşiği** bölümünde RPO limitini belirtin.</span><span class="sxs-lookup"><span data-stu-id="4449a-110">In **RPO threshold**, specify the RPO limit.</span></span> <span data-ttu-id="4449a-111">Bu değer, ne sıklıkta belirtir veri kurtarma noktaları oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="4449a-111">This value specifies how often data recovery points are created.</span></span> <span data-ttu-id="4449a-112">Sürekli çoğaltma bu sınırı aşarsa bir uyarı üretilir.</span><span class="sxs-lookup"><span data-stu-id="4449a-112">An alert is generated if continuous replication exceeds this limit.</span></span>
4. <span data-ttu-id="4449a-113">İçinde **kurtarma noktası bekletme**, (saat olarak) ne kadar süreyle bekletme penceresi için her kurtarma noktası belirtin.</span><span class="sxs-lookup"><span data-stu-id="4449a-113">In **Recovery point retention**, specify (in hours) how long the retention window is for each recovery point.</span></span> <span data-ttu-id="4449a-114">Çoğaltılan VM'ler penceresinde herhangi bir noktaya kurtarılabilir.</span><span class="sxs-lookup"><span data-stu-id="4449a-114">Replicated VMs can be recovered to any point in a window.</span></span> <span data-ttu-id="4449a-115">24 saat bekletme için premium depolama ve standart depolama için 72 saat çoğaltılan makineler için desteklenir.</span><span class="sxs-lookup"><span data-stu-id="4449a-115">Up to 24 hours retention is supported for machines replicated to premium storage, and 72 hours for standard storage.</span></span>
5. <span data-ttu-id="4449a-116">İçinde **uygulamayla tutarlı anlık görüntü sıklığı**, belirtin ne sıklıkta (dakika cinsinden) uygulamayla tutarlı anlık görüntüleri içeren kurtarma noktaları oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="4449a-116">In **App-consistent snapshot frequency**, specify how often (in minutes) recovery points containing application-consistent snapshots will be created.</span></span> <span data-ttu-id="4449a-117">Tıklatın **Tamam** bir ilke oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="4449a-117">Click **OK** to create the policy.</span></span>

    ![Çoğaltma ilkesi](./media/vmware-walkthrough-replication/gs-replication2.png)
8. <span data-ttu-id="4449a-119">Yeni bir ilke oluşturduğunuzda, otomatik olarak yapılandırma sunucusu ile ilişkili.</span><span class="sxs-lookup"><span data-stu-id="4449a-119">When you create a new policy it's automatically associated with the configuration server.</span></span> <span data-ttu-id="4449a-120">Varsayılan olarak, eşleşen bir ilkesi yeniden çalışma için otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="4449a-120">By default, a matching policy is automatically created for failback.</span></span> <span data-ttu-id="4449a-121">Örneğin, çoğaltma ilkesi ise **rep İlkesi** geri dönme ilkesini sonra **rep İlkesi yeniden**.</span><span class="sxs-lookup"><span data-stu-id="4449a-121">For example, if the replication policy is **rep-policy** then the failback policy will be **rep-policy-failback**.</span></span> <span data-ttu-id="4449a-122">Bir azure'dan başlatana kadar bu ilkeyi kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="4449a-122">This policy isn't used until you initiate a failback from Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4449a-123">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4449a-123">Next steps</span></span>

<span data-ttu-id="4449a-124">Git [adım 10: Mobility hizmetini yükleme](vmware-walkthrough-install-mobility.md)</span><span class="sxs-lookup"><span data-stu-id="4449a-124">Go to [Step 10: Install the Mobility service](vmware-walkthrough-install-mobility.md)</span></span>
