---
title: "Hyper-V VM (VMM ile) çoğaltma tooAzure Azure Site Recovery ile çoğaltma ilkesi aaaSet | Microsoft Docs"
description: "Açıklar nasıl tooset (VMM ile) Hyper-V VM çoğaltma tooAzure Azure Site Recovery ile çoğaltma ilkesi"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: ee808b20-324b-4198-b831-edb65b95e8b7
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: e1579fde559ca34eca19a01e740fec28a0df2f9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="step-10-set-up-a-replication-policy-for-hyper-v-vm-replication-with-vmm-tooazure"></a><span data-ttu-id="e0158-103">10. adım: Hyper-V VM çoğaltma (VMM ile) tooAzure için bir çoğaltma ilkesi ayarlama</span><span class="sxs-lookup"><span data-stu-id="e0158-103">Step 10: Set up a replication policy for Hyper-V VM replication (with VMM) tooAzure</span></span>


<span data-ttu-id="e0158-104">Ayarladıktan sonra [ağ eşlemesi](vmm-to-azure-walkthrough-network-mapping.md), bir çoğaltma ilkesi T\tooreplicate şirket içi System Center Virtual Machine Manager (VMM) Bulutlar tooAzure yönetilen Hyper-V sanal makinelerin Bu makale tooconfigure kullanın, hello kullanma[ Azure Site Recovery](site-recovery-overview.md) hello Azure portal hizmeti.</span><span class="sxs-lookup"><span data-stu-id="e0158-104">After setting up [network mapping](vmm-to-azure-walkthrough-network-mapping.md), use this article tooconfigure a replication policy T\tooreplicate on-premises Hyper-V virtual machines managed in System Center Virtual Machine Manager (VMM) clouds tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="e0158-105">Bu makaleyi okuduktan sonra tüm yorumlar hello altındaki ya da hello sonrası [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="e0158-105">After reading this article, post any comments at hello bottom, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>



## <a name="create-a-policy"></a><span data-ttu-id="e0158-106">Bir ilke oluşturun</span><span class="sxs-lookup"><span data-stu-id="e0158-106">Create a policy</span></span>

1. <span data-ttu-id="e0158-107">Yeni bir çoğaltma ilkesi toocreate tıklatın **altyapıyı hazırlama** > **çoğaltma ayarları** > **+ oluştur ve ilişkilendir**.</span><span class="sxs-lookup"><span data-stu-id="e0158-107">toocreate a new replication policy, click **Prepare infrastructure** > **Replication Settings** > **+Create and associate**.</span></span>

    ![Ağ](./media/vmm-to-azure-walkthrough-replication/gs-replication.png)
2. <span data-ttu-id="e0158-109">**İlke oluştur ve ilişkilendir** bölümünde bir ilke adı belirtin.</span><span class="sxs-lookup"><span data-stu-id="e0158-109">In **Create and associate policy**, specify a policy name.</span></span>
3. <span data-ttu-id="e0158-110">İçinde **kopyalama sıklığı**, ne sıklıkta hello ilk çoğaltma (her 30 saniyede, 5 veya 15 dakika) sonra tooreplicate değişim verileri istediğinizi belirtin.</span><span class="sxs-lookup"><span data-stu-id="e0158-110">In **Copy frequency**, specify how often you want tooreplicate delta data after hello initial replication (every 30 seconds, 5 or 15 minutes).</span></span>

    > [!NOTE]
    >  <span data-ttu-id="e0158-111">30 ikinci sıklığı toopremium depolama çoğaltırken desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="e0158-111">A 30 second frequency isn't supported when replicating toopremium storage.</span></span> <span data-ttu-id="e0158-112">Merhaba sınırlaması, premium depolama birimi tarafından desteklenen hello anlık görüntü sayısı blob (100) başına tarafından belirlenir.</span><span class="sxs-lookup"><span data-stu-id="e0158-112">hello limitation is determined by hello number of snapshots per blob (100) supported by premium storage.</span></span> [<span data-ttu-id="e0158-113">Daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="e0158-113">Learn more</span></span>](../storage/common/storage-premium-storage.md#snapshots-and-copy-blob)

4. <span data-ttu-id="e0158-114">İçinde **kurtarma noktası bekletme**, saat cinsinden ne kadar süreyle hello bekletme penceresi belirtin her kurtarma noktası için olabilir.</span><span class="sxs-lookup"><span data-stu-id="e0158-114">In **Recovery point retention**, specify in hours how long hello retention window will be for each recovery point.</span></span> <span data-ttu-id="e0158-115">Korumalı makineler olabilir bir pencere içinde tooany noktası kurtarıldı.</span><span class="sxs-lookup"><span data-stu-id="e0158-115">Protected machines can be recovered tooany point within a window.</span></span>
5. <span data-ttu-id="e0158-116">**Uygulamayla tutarlı anlık görüntü sıklığı** kısmında, uygulamayla tutarlı anlık görüntüleri içeren kurtarma noktasının hangi sıklıkta oluşturulacağını (1-12 saat) belirtin.</span><span class="sxs-lookup"><span data-stu-id="e0158-116">In **App-consistent snapshot frequency**, specify how frequently (1-12 hours) recovery points containing application-consistent snapshots will be created.</span></span> <span data-ttu-id="e0158-117">Hyper-V iki çeşit anlık kullanır — bir artımlı hello tüm sanal makinenin anlık görüntüsünü sunan standart anlık görüntü ve zaman içinde nokta verilerin bir anlık görüntüsünü hello uygulama hello sanal makine içinde geçen uygulama tutarlı bir anlık görüntü.</span><span class="sxs-lookup"><span data-stu-id="e0158-117">Hyper-V uses two types of snapshots — a standard snapshot that provides an incremental snapshot of hello entire virtual machine, and an application-consistent snapshot that takes a point-in-time snapshot of hello application data inside hello virtual machine.</span></span> <span data-ttu-id="e0158-118">Uygulamayla tutarlı anlık görüntüleri hello anlık görüntü alınırken uygulamaların tutarlı bir durumda olan birim gölge kopyası hizmeti (VSS) tooensure kullanın.</span><span class="sxs-lookup"><span data-stu-id="e0158-118">Application-consistent snapshots use Volume Shadow Copy Service (VSS) tooensure that applications are in a consistent state when hello snapshot is taken.</span></span> <span data-ttu-id="e0158-119">Uygulamayla tutarlı anlık görüntüleri etkinleştirirseniz, kaynak sanal makinelerde çalışan uygulamaların hello performansını etkiler unutmayın.</span><span class="sxs-lookup"><span data-stu-id="e0158-119">Note that if you enable application-consistent snapshots, it will affect hello performance of applications running on source virtual machines.</span></span> <span data-ttu-id="e0158-120">Ayarladığınız hello değeri, yapılandırdığınız ilave kurtarma noktası hello sayısından daha az olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="e0158-120">Ensure that hello value you set is less than hello number of additional recovery points you configure.</span></span>
6. <span data-ttu-id="e0158-121">İçinde **ilk çoğaltma başlangıç zamanı**, ne zaman toostart hello ilk çoğaltma gösterir.</span><span class="sxs-lookup"><span data-stu-id="e0158-121">In **Initial replication start time**, indicate when toostart hello initial replication.</span></span> <span data-ttu-id="e0158-122">Merhaba çoğaltmanın internet bant genişliğiniz tooschedule isteyebilirsiniz şekilde meşgul saatleriniz dışında.</span><span class="sxs-lookup"><span data-stu-id="e0158-122">hello replication occurs over your internet bandwidth so you might want tooschedule it outside your busy hours.</span></span>
7. <span data-ttu-id="e0158-123">İçinde **Azure'da depolanan verileri şifrele**, belirtin olup olmadığını tooencrypt Azure depolama alanında rest veri.</span><span class="sxs-lookup"><span data-stu-id="e0158-123">In **Encrypt data stored on Azure**, specify whether tooencrypt at rest data in Azure storage.</span></span> <span data-ttu-id="e0158-124">Daha sonra, **Tamam**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e0158-124">Then click **OK**.</span></span>

    ![Çoğaltma ilkesi](./media/vmm-to-azure-walkthrough-replication/gs-replication2.png)
8. <span data-ttu-id="e0158-126">Yeni bir ilke oluşturduğunuzda, otomatik olarak hello VMM Bulutu ile ilişkili.</span><span class="sxs-lookup"><span data-stu-id="e0158-126">When you create a new policy it's automatically associated with hello VMM cloud.</span></span> <span data-ttu-id="e0158-127">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e0158-127">Click **OK**.</span></span> <span data-ttu-id="e0158-128">Bu çoğaltma ilkesini ek VMM Bulutları (ve bunlara hello VM'ler) ilişkilendirebilirsiniz **çoğaltma** > ilke adı > **VMM Bulutu ile ilişkilendir**.</span><span class="sxs-lookup"><span data-stu-id="e0158-128">You can associate additional VMM clouds (and hello VMs in them) with this replication policy in **Replication** > policy name > **Associate VMM Cloud**.</span></span>

    ![Çoğaltma ilkesi](./media/vmm-to-azure-walkthrough-replication/policy-associate.png)



## <a name="next-steps"></a><span data-ttu-id="e0158-130">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e0158-130">Next steps</span></span>

<span data-ttu-id="e0158-131">Çok Git[adım 11: çoğaltmasını etkinleştir](vmm-to-azure-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="e0158-131">Go too[Step 11: Enable replication](vmm-to-azure-walkthrough-enable-replication.md)</span></span>
