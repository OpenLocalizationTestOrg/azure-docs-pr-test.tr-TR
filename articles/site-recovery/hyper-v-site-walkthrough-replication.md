---
title: "Hyper-V VM (System Center VMM olmadan) çoğaltma tooAzure Azure Site Recovery ile çoğaltma ilkesi aaaSet | Microsoft Docs"
description: "Hyper-V sanal makineleri tooAzure depolama çoğaltırken çoğaltma ilkesi tooset gereken hello adımları özetler"
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 1777e0eb-accb-42b5-a747-11272e131a52
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/22/2017
ms.author: raynew
ms.openlocfilehash: 4bd7161f4a0f015da0ecf595fbc6861ede5d68b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="step-9-set-up-a-replication-policy-for-hyper-v-vm-replication-tooazure"></a><span data-ttu-id="a5afa-103">9. adım: Hyper-V VM çoğaltma tooAzure için bir çoğaltma ilkesi ayarlayın</span><span class="sxs-lookup"><span data-stu-id="a5afa-103">Step 9: Set up a replication policy for Hyper-V VM replication tooAzure</span></span>

<span data-ttu-id="a5afa-104">Bu makalede nasıl hello kullanarak Hyper-V sanal makineleri tooAzure (System Center VMM olmadan) çoğaltırken çoğaltma ilkesi tooset [Azure Site Recovery](site-recovery-overview.md) hello Azure portal hizmeti.</span><span class="sxs-lookup"><span data-stu-id="a5afa-104">This article describes how tooset up a replication policy when you're replicating Hyper-V VMs tooAzure (without System Center VMM) using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>


<span data-ttu-id="a5afa-105">POST açıklamaları ve soruları hello altındaki bu makalenin veya hello [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="a5afa-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="about-snapshots"></a><span data-ttu-id="a5afa-106">Anlık görüntüler hakkında</span><span class="sxs-lookup"><span data-stu-id="a5afa-106">About snapshots</span></span>

<span data-ttu-id="a5afa-107">Hyper-V iki çeşit anlık kullanır — bir artımlı hello tüm sanal makinenin anlık görüntüsünü sunan standart anlık görüntü ve zaman içinde nokta verilerin bir anlık görüntüsünü hello uygulama hello sanal makine içinde geçen uygulama tutarlı bir anlık görüntü.</span><span class="sxs-lookup"><span data-stu-id="a5afa-107">Hyper-V uses two types of snapshots — a standard snapshot that provides an incremental snapshot of hello entire virtual machine, and an application-consistent snapshot that takes a point-in-time snapshot of hello application data inside hello virtual machine.</span></span>
    - <span data-ttu-id="a5afa-108">Uygulamayla tutarlı anlık görüntüleri hello anlık görüntü alınırken uygulamaların tutarlı bir durumda olan birim gölge kopyası hizmeti (VSS) tooensure kullanın.</span><span class="sxs-lookup"><span data-stu-id="a5afa-108">Application-consistent snapshots use Volume Shadow Copy Service (VSS) tooensure that applications are in a consistent state when hello snapshot is taken.</span></span>
    - <span data-ttu-id="a5afa-109">Uygulamayla tutarlı anlık görüntüleri etkinleştirirseniz kaynak sanal makinelerde çalışan uygulamaların hello performansını etkiler.</span><span class="sxs-lookup"><span data-stu-id="a5afa-109">If you enable application-consistent snapshots, it will affect hello performance of applications running on source virtual machines.</span></span> <span data-ttu-id="a5afa-110">Ayarladığınız hello değeri, yapılandırdığınız ilave kurtarma noktası hello sayısından daha az olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="a5afa-110">Ensure that hello value you set is less than hello number of additional recovery points you configure.</span></span>

## <a name="set-up-a-replication-policy"></a><span data-ttu-id="a5afa-111">Bir çoğaltma ilkesini ayarlayın</span><span class="sxs-lookup"><span data-stu-id="a5afa-111">Set up a replication policy</span></span>

1. <span data-ttu-id="a5afa-112">Yeni bir çoğaltma ilkesi toocreate tıklatın **altyapıyı hazırlama** > **çoğaltma ayarları** > **+ oluştur ve ilişkilendir**.</span><span class="sxs-lookup"><span data-stu-id="a5afa-112">toocreate a new replication policy, click **Prepare infrastructure** > **Replication Settings** > **+Create and associate**.</span></span>

    ![Ağ](./media/hyper-v-site-walkthrough-replication/gs-replication.png)
2. <span data-ttu-id="a5afa-114">**İlke oluştur ve ilişkilendir** bölümünde bir ilke adı belirtin.</span><span class="sxs-lookup"><span data-stu-id="a5afa-114">In **Create and associate policy**, specify a policy name.</span></span>
3. <span data-ttu-id="a5afa-115">İçinde **kopyalama sıklığı**, ne sıklıkta hello ilk çoğaltma (her 30 saniyede, 5 veya 15 dakika) sonra tooreplicate değişim verileri istediğinizi belirtin.</span><span class="sxs-lookup"><span data-stu-id="a5afa-115">In **Copy frequency**, specify how often you want tooreplicate delta data after hello initial replication (every 30 seconds, 5 or 15 minutes).</span></span>

    > [!NOTE]
    > <span data-ttu-id="a5afa-116">30 ikinci sıklığı toopremium depolama çoğaltırken desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="a5afa-116">A 30 second frequency isn't supported when replicating toopremium storage.</span></span> <span data-ttu-id="a5afa-117">Merhaba sınırlaması, premium depolama birimi tarafından desteklenen hello anlık görüntü sayısı blob (100) başına tarafından belirlenir.</span><span class="sxs-lookup"><span data-stu-id="a5afa-117">hello limitation is determined by hello number of snapshots per blob (100) supported by premium storage.</span></span> <span data-ttu-id="a5afa-118">[Daha fazla bilgi edinin](../storage/common/storage-premium-storage.md#snapshots-and-copy-blob).</span><span class="sxs-lookup"><span data-stu-id="a5afa-118">[Learn more](../storage/common/storage-premium-storage.md#snapshots-and-copy-blob).</span></span>

4. <span data-ttu-id="a5afa-119">İçinde **kurtarma noktası bekletme**, saat cinsinden süreyi belirtin hello bekletme penceresi olduğu için her kurtarma noktası.</span><span class="sxs-lookup"><span data-stu-id="a5afa-119">In **Recovery point retention**, specify in hours how long hello retention window is for each recovery point.</span></span> <span data-ttu-id="a5afa-120">Sanal makineleri olabilir bir pencere içinde tooany noktası kurtarıldı.</span><span class="sxs-lookup"><span data-stu-id="a5afa-120">VMs can be recovered tooany point within a window.</span></span>
5. <span data-ttu-id="a5afa-121">İçinde **uygulamayla tutarlı anlık görüntü sıklığı**, ne sıklıkla (1-12 saat) içeren uygulamayla tutarlı anlık görüntüleri kurtarma noktalarını belirtin oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="a5afa-121">In **App-consistent snapshot frequency**, specify how frequently (1-12 hours) recovery points containing application-consistent snapshots are created.</span></span>
6. <span data-ttu-id="a5afa-122">İçinde **ilk çoğaltma başlangıç zamanı**, ne zaman toostart hello ilk çoğaltma belirtin.</span><span class="sxs-lookup"><span data-stu-id="a5afa-122">In **Initial replication start time**, specify when toostart hello initial replication.</span></span> <span data-ttu-id="a5afa-123">Merhaba çoğaltmanın internet bant genişliğiniz tooschedule isteyebilirsiniz şekilde meşgul saatleriniz dışında.</span><span class="sxs-lookup"><span data-stu-id="a5afa-123">hello replication occurs over your internet bandwidth so you might want tooschedule it outside your busy hours.</span></span> <span data-ttu-id="a5afa-124">Daha sonra, **Tamam**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a5afa-124">Then click **OK**.</span></span>

    ![Çoğaltma ilkesi](./media/hyper-v-site-walkthrough-replication/gs-replication2.png)

<span data-ttu-id="a5afa-126">Yeni bir ilke oluşturduğunuzda, otomatik olarak hello Hyper-V sitesi ile ilişkili.</span><span class="sxs-lookup"><span data-stu-id="a5afa-126">When you create a new policy, it's automatically associated with hello Hyper-V site.</span></span> <span data-ttu-id="a5afa-127">Birden fazla çoğaltma ilkesi ile bir Hyper-V sitesi (ve hello VM'ler da) ilişkilendirebilirsiniz **çoğaltma** > ilke adı > **ilişkilendirmek Hyper-V sitesi**.</span><span class="sxs-lookup"><span data-stu-id="a5afa-127">You can associate a Hyper-V site (and hello VMs in it) with multiple replication policies in **Replication** > policy-name > **Associate Hyper-V Site**.</span></span>



## <a name="next-steps"></a><span data-ttu-id="a5afa-128">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a5afa-128">Next steps</span></span>

<span data-ttu-id="a5afa-129">Çok Git[adım 10: çoğaltmasını etkinleştir](hyper-v-site-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="a5afa-129">Go too[Step 10: Enable replication](hyper-v-site-walkthrough-enable-replication.md)</span></span>
