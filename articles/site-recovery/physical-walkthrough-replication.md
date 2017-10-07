---
title: "fiziksel sunucu çoğaltma tooAzure Azure Site Recovery ile çoğaltma ilkesi aaaSet | Microsoft Docs"
description: "Çoğaltma fiziksel sunucuları tooAzure depolama hello Azure Site Recovery hizmetini kullanarak şirket içi olduğunda çoğaltma ilkesi tooset gereken hello adımları özetler"
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
ms.openlocfilehash: d6bdeeffc24ffc8eaba24311f7c76452edb65648
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="step-8-set-up-a-replication-policy-for-physical-server-replication-tooazure"></a><span data-ttu-id="5cef9-103">8. adım: fiziksel sunucu çoğaltma tooAzure için bir çoğaltma ilkesi ayarlama</span><span class="sxs-lookup"><span data-stu-id="5cef9-103">Step 8: Set up a replication policy for physical server replication tooAzure</span></span>


<span data-ttu-id="5cef9-104">Bu makalede nasıl hello kullanarak Windows/Linux fiziksel sunucuları tooAzure çoğaltırken çoğaltma ilkesi tooset [Azure Site Recovery](site-recovery-overview.md) hello Azure portal hizmeti.</span><span class="sxs-lookup"><span data-stu-id="5cef9-104">This article describes how tooset up a replication policy when you're replicating Windows/Linux physical servers tooAzure using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>


<span data-ttu-id="5cef9-105">POST açıklamaları ve soruları hello altındaki bu makalenin veya hello [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="5cef9-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="configure-a-policy"></a><span data-ttu-id="5cef9-106">Bir ilke yapılandırın</span><span class="sxs-lookup"><span data-stu-id="5cef9-106">Configure a policy</span></span>

1. <span data-ttu-id="5cef9-107">Tıklatın **Site Recovery altyapısı** > **çoğaltma ilkeleri** > **+ Çoğaltma İlkesi**.</span><span class="sxs-lookup"><span data-stu-id="5cef9-107">Click **Site Recovery infrastructure** > **Replication Policies** > **+Replication Policy**.</span></span>
2. <span data-ttu-id="5cef9-108">İçinde **çoğaltma ilkesi oluşturun**, bir ilke adı belirtin.</span><span class="sxs-lookup"><span data-stu-id="5cef9-108">In **Create replication policy**, specify a policy name.</span></span>
3. <span data-ttu-id="5cef9-109">İçinde **RPO eşik**, hello RPO sınırını belirtin.</span><span class="sxs-lookup"><span data-stu-id="5cef9-109">In **RPO threshold**, specify hello RPO limit.</span></span> <span data-ttu-id="5cef9-110">Bu değer ne sıklıkta gösterir veri kurtarma noktaları oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="5cef9-110">This value indicates how often data recovery points are created.</span></span> <span data-ttu-id="5cef9-111">Sürekli çoğaltma bu sınırı aşarsa bir uyarı üretilir.</span><span class="sxs-lookup"><span data-stu-id="5cef9-111">An alert is generated if continuous replication exceeds this limit.</span></span>
4. <span data-ttu-id="5cef9-112">İçinde **kurtarma noktası bekletme**, ne kadar süre (saat olarak) belirtin hello bekletme penceresi olduğu için her kurtarma noktası.</span><span class="sxs-lookup"><span data-stu-id="5cef9-112">In **Recovery point retention**, specify (in hours) how long hello retention window is for each recovery point.</span></span> <span data-ttu-id="5cef9-113">Çoğaltılan VM'ler olabilir bir pencerede tooany noktası kurtarıldı.</span><span class="sxs-lookup"><span data-stu-id="5cef9-113">Replicated VMs can be recovered tooany point in a window.</span></span> <span data-ttu-id="5cef9-114">Saat bekletme makineler için desteklenen too24 yukarı toopremium depolama ile standart depolama için 72 saat çoğaltılan.</span><span class="sxs-lookup"><span data-stu-id="5cef9-114">Up too24 hours retention is supported for machines replicated toopremium storage, and 72 hours for standard storage.</span></span>
5. <span data-ttu-id="5cef9-115">İçinde **uygulamayla tutarlı anlık görüntü sıklığı**, belirtin ne sıklıkta (dakika cinsinden) uygulamayla tutarlı anlık görüntüleri içeren kurtarma noktaları oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="5cef9-115">In **App-consistent snapshot frequency**, specify how often (in minutes) recovery points containing application-consistent snapshots will be created.</span></span> <span data-ttu-id="5cef9-116">Tıklatın **Tamam** toocreate hello ilkesi.</span><span class="sxs-lookup"><span data-stu-id="5cef9-116">Click **OK** toocreate hello policy.</span></span>

    ![Çoğaltma ilkesi](./media/physical-walkthrough-replication/gs-replication2.png)
8. <span data-ttu-id="5cef9-118">Yeni bir ilke oluşturduğunuzda, otomatik olarak hello yapılandırma sunucusu ile ilişkili.</span><span class="sxs-lookup"><span data-stu-id="5cef9-118">When you create a new policy it's automatically associated with hello configuration server.</span></span> <span data-ttu-id="5cef9-119">Varsayılan olarak, eşleşen bir ilkesi yeniden çalışma için otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="5cef9-119">By default, a matching policy is automatically created for failback.</span></span> <span data-ttu-id="5cef9-120">Örneğin, hello çoğaltma ilkesi ise **rep İlkesi** hello geri dönme ilkesini sonra **rep İlkesi yeniden**.</span><span class="sxs-lookup"><span data-stu-id="5cef9-120">For example, if hello replication policy is **rep-policy** then hello failback policy will be **rep-policy-failback**.</span></span> <span data-ttu-id="5cef9-121">Bir azure'dan başlatana kadar bu ilkeyi kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="5cef9-121">This policy isn't used until you initiate a failback from Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5cef9-122">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5cef9-122">Next steps</span></span>

<span data-ttu-id="5cef9-123">Çok Git[adım 9: hello Mobility hizmetini yükleme](physical-walkthrough-install-mobility.md)</span><span class="sxs-lookup"><span data-stu-id="5cef9-123">Go too[Step 9: Install hello Mobility service](physical-walkthrough-install-mobility.md)</span></span>
