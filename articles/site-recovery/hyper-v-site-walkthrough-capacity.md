---
title: "Kapasite ve Hyper-V VM (VMM olmadan) çoğaltma tooAzure Azure Site Recovery ile ölçeklendirme aaaPlan | Microsoft Docs"
description: "Bu makale tooplan kapasite ve ölçek Azure Site Recovery ile Hyper-V sanal makineleri tooAzure çoğaltırken kullanın"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 8687af60-5b50-481c-98ee-0750cbbc2c57
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/21/2017
ms.author: raynew
ms.openlocfilehash: f5b029f273e51c01c7d918d176832f6d1735b5f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="step-3-plan-capacity-and-scaling-for-hyper-v-tooazure-replication"></a><span data-ttu-id="f76a6-103">3. adım: kapasite ve Hyper-V tooAzure çoğaltma için ölçeklendirme planlama</span><span class="sxs-lookup"><span data-stu-id="f76a6-103">Step 3: Plan capacity and scaling for Hyper-V tooAzure replication</span></span>

<span data-ttu-id="f76a6-104">Bu makale toofigure için kapasite planlaması ve ölçeklendirme, şirket içi Hyper-V Vm'lerini (System Center VMM olmadan) tooAzure ile çoğaltırken kullanmak [Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f76a6-104">Use this article toofigure out planning for capacity and scaling, when replicating on-premises Hyper-V VMs (without System Center VMM) tooAzure with [Azure Site Recovery](site-recovery-overview.md).</span></span>

<span data-ttu-id="f76a6-105">Bu makaleyi okuduktan sonra hello altındaki tüm yorumlar post veya üzerinde hello teknik sorular sormak [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="f76a6-105">After reading this article, post any comments at hello bottom, or ask technical questions on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="how-do-i-start-capacity-planning"></a><span data-ttu-id="f76a6-106">Kapasite planlama nasıl başlamanız gerekir?</span><span class="sxs-lookup"><span data-stu-id="f76a6-106">How do I start capacity planning?</span></span>


<span data-ttu-id="f76a6-107">Çoğaltma ortamınız hakkında bilgi toplamak ve bu makalede vurgulanmış hello konuları birlikte bu bilgileri kullanarak kapasite planlama.</span><span class="sxs-lookup"><span data-stu-id="f76a6-107">You gather information about your replication environment, and then plan capacity using this information, together with hello considerations highlighted in this article.</span></span>


## <a name="gather-information"></a><span data-ttu-id="f76a6-108">Bilgileri toplayın</span><span class="sxs-lookup"><span data-stu-id="f76a6-108">Gather information</span></span>

1. <span data-ttu-id="f76a6-109">VM'ler, VM başına disk ve disk başına depolama dahil olmak üzere çoğaltma ortamınız hakkında bilgi toplayın.</span><span class="sxs-lookup"><span data-stu-id="f76a6-109">Gather information about your replication environment, including VMs, disks per VMs, and storage per disk.</span></span>
2. <span data-ttu-id="f76a6-110">Çoğaltılan veriler için günlük değişim (dalgalanma) oranı tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="f76a6-110">Identify your daily change (churn) rate for replicated data.</span></span> <span data-ttu-id="f76a6-111">Merhaba karşıdan [Hyper-V kapasite planlama aracı](https://www.microsoft.com/download/details.aspx?id=39057) tooget hello değişim oranı.</span><span class="sxs-lookup"><span data-stu-id="f76a6-111">Download hello [Hyper-V capacity planning tool](https://www.microsoft.com/download/details.aspx?id=39057) tooget hello change rate.</span></span> <span data-ttu-id="f76a6-112">Ortalamalar hafta toocapture bu aracı çalıştırın öneririz.</span><span class="sxs-lookup"><span data-stu-id="f76a6-112">We recommend you run this tool over a week toocapture averages.</span></span>
 

## <a name="figure-out-capacity"></a><span data-ttu-id="f76a6-113">Kapasitesi Şekil</span><span class="sxs-lookup"><span data-stu-id="f76a6-113">Figure out capacity</span></span>

<span data-ttu-id="f76a6-114">Toplama seçtiğiniz hello bilgilere dayanarak hello çalıştırmak [Site kurtarma kapasite planlayıcısı aracı](http://aka.ms/asr-capacity-planner-excel) tooanalyze kaynak ortamınız ve iş yükleri, bant genişliği gereksinimlerini ve sunucu kaynaklarını hello kaynak konumu için tahmin etmek ve hello Merhaba hedef konumda gereken kaynakları (sanal makineler ve depolama vb.).</span><span class="sxs-lookup"><span data-stu-id="f76a6-114">Based on hello information you've gather, you run hello [Site Recovery Capacity Planner Tool](http://aka.ms/asr-capacity-planner-excel) tooanalyze your source environment and workloads, estimate bandwidth needs and server resources for hello source location, and hello resources (virtual machines and storage etc), that you need in hello target location.</span></span> <span data-ttu-id="f76a6-115">Merhaba aracı modları birkaç içinde çalıştırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f76a6-115">You can run hello tool in a couple of modes:</span></span>

- <span data-ttu-id="f76a6-116">Hızlı planlama: hello aracı tooget ağ ve sunucu tahminleri ortalama bir VM'ler, diskleri, depolama ve değişim oranı sayısına göre bu modda çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="f76a6-116">Quick planning: Run hello tool in this mode tooget network and server projections based on an average number of VMs, disks, storage, and change rate.</span></span>
- <span data-ttu-id="f76a6-117">Ayrıntılı planlama: Bu modda hello aracını çalıştırın ve her iş yükü VM düzeyinde ayrıntılarını sağlayın.</span><span class="sxs-lookup"><span data-stu-id="f76a6-117">Detailed planning: Run hello tool in this mode, and provide details of each workload at VM level.</span></span> <span data-ttu-id="f76a6-118">VM uyumluluk çözümlemek ve ağ ve sunucu tahminleri alın.</span><span class="sxs-lookup"><span data-stu-id="f76a6-118">Analyze VM compatibility and get network and server projections.</span></span>

<span data-ttu-id="f76a6-119">Şimdi hello aracını çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="f76a6-119">Now run hello tool:</span></span>

1. <span data-ttu-id="f76a6-120">Merhaba karşıdan [aracı](http://aka.ms/asr-capacity-planner-excel)</span><span class="sxs-lookup"><span data-stu-id="f76a6-120">Download hello [tool](http://aka.ms/asr-capacity-planner-excel)</span></span>
2. <span data-ttu-id="f76a6-121">toorun hello hızlı Planlayıcısı izleyin [bu yönergeleri](site-recovery-capacity-planner.md#run-the-quick-planner)ve select hello senaryo **Hyper-V tooAzure**.</span><span class="sxs-lookup"><span data-stu-id="f76a6-121">toorun hello quick planner, follow [these instructions](site-recovery-capacity-planner.md#run-the-quick-planner), and select hello scenario **Hyper-V tooAzure**.</span></span>
3. <span data-ttu-id="f76a6-122">toorun Merhaba ayrıntılı Planlayıcısı, izleyin [bu yönergeleri](site-recovery-capacity-planner.md#run-the-detailed-planner)ve select hello senaryo **Hyper-V tooAzure**.</span><span class="sxs-lookup"><span data-stu-id="f76a6-122">toorun hello detailed planner, follow [these instructions](site-recovery-capacity-planner.md#run-the-detailed-planner), and select hello scenario **Hyper-V tooAzure**.</span></span>

## <a name="control-network-bandwidth"></a><span data-ttu-id="f76a6-123">Ağ bant genişliğini denetlemek</span><span class="sxs-lookup"><span data-stu-id="f76a6-123">Control network bandwidth</span></span>

<span data-ttu-id="f76a6-124">Gereksinim duyduğunuz hesaplanan hello bant genişliği sonra birkaç hello çoğaltma için kullanılan bant genişliği miktarını kontrol eden için seçenekler vardır:</span><span class="sxs-lookup"><span data-stu-id="f76a6-124">After you've calculated hello bandwidth you need, you have a couple of options for controlling hello amount of bandwidth used for replication:</span></span>

* <span data-ttu-id="f76a6-125">**Bant genişliğini kısıtlama**: tooAzure çoğaltır Hyper-V trafiği belirli bir Hyper-V ana bilgisayar üzerinden gider.</span><span class="sxs-lookup"><span data-stu-id="f76a6-125">**Throttle bandwidth**: Hyper-V traffic that replicates tooAzure goes through a specific Hyper-V host.</span></span> <span data-ttu-id="f76a6-126">Merhaba ana bilgisayar sunucusunda bant genişliğini kısıtlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f76a6-126">You can throttle bandwidth on hello host server.</span></span>
* <span data-ttu-id="f76a6-127">**Bant genişliği üzerinde etki**: birkaç kayıt defteri anahtarlarını kullanarak çoğaltma için kullanılan hello bant genişliği etkileyebilir.</span><span class="sxs-lookup"><span data-stu-id="f76a6-127">**Influence bandwidth**: You can influence hello bandwidth used for replication using a couple of registry keys.</span></span>

### <a name="throttle-bandwidth"></a><span data-ttu-id="f76a6-128">Bant genişliğini kısıtlama</span><span class="sxs-lookup"><span data-stu-id="f76a6-128">Throttle bandwidth</span></span>
1. <span data-ttu-id="f76a6-129">Merhaba Hyper-V konak sunucusunda Hello Microsoft Azure Backup MMC eklentisini açın.</span><span class="sxs-lookup"><span data-stu-id="f76a6-129">Open hello Microsoft Azure Backup MMC snap-in on hello Hyper-V host server.</span></span> <span data-ttu-id="f76a6-130">Varsayılan olarak Microsoft Azure yedekleme için bir kısayol hello masaüstünde veya C:\Program Files\Microsoft Azure Recovery Services agent\bin\wabadmin yolunda kullanılabilir durumdadır.</span><span class="sxs-lookup"><span data-stu-id="f76a6-130">By default a shortcut for Microsoft Azure Backup is available on hello desktop or in C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin.</span></span>
2. <span data-ttu-id="f76a6-131">Merhaba ek bileşeninde tıklatın **özelliklerini değiştirme**.</span><span class="sxs-lookup"><span data-stu-id="f76a6-131">In hello snap-in click **Change Properties**.</span></span>
3. <span data-ttu-id="f76a6-132">Merhaba üzerinde **azaltma** sekmesini seçin **yedekleme işlemleri için Internet bant genişliği kullanımı daraltmayı etkinleştir**, iş için hello sınırını ayarlama ve saat İş dışı.</span><span class="sxs-lookup"><span data-stu-id="f76a6-132">On hello **Throttling** tab select **Enable internet bandwidth usage throttling for backup operations**, and set hello limits for work and non-work hours.</span></span> <span data-ttu-id="f76a6-133">Geçerli aralıklar saniye başına 512 Kbps too102 Mbps arasındadır.</span><span class="sxs-lookup"><span data-stu-id="f76a6-133">Valid ranges are from 512 Kbps too102 Mbps per second.</span></span>

    ![Bant genişliğini kısıtlama](./media/hyper-v-site-walkthrough-capacity/throttle2.png)

<span data-ttu-id="f76a6-135">Merhaba de kullanabilirsiniz [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409.aspx) tooset cmdlet azaltma.</span><span class="sxs-lookup"><span data-stu-id="f76a6-135">You can also use hello [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409.aspx) cmdlet tooset throttling.</span></span> <span data-ttu-id="f76a6-136">Bu ayara ilişkin örneği aşağıda bulabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f76a6-136">Here's a sample:</span></span>

    $mon = [System.DayOfWeek]::Monday
    $tue = [System.DayOfWeek]::Tuesday
    Set-OBMachineSetting -WorkDay $mon, $tue -StartWorkHour "9:00:00" -EndWorkHour "18:00:00" -WorkHourBandwidth  (512*1024) -NonWorkHourBandwidth (2048*1024)

<span data-ttu-id="f76a6-137">**Set-OBMachineSetting - NoThrottle** hiçbir azaltmanın gerekli olmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="f76a6-137">**Set-OBMachineSetting -NoThrottle** indicates that no throttling is required.</span></span>

### <a name="influence-network-bandwidth"></a><span data-ttu-id="f76a6-138">Ağ bant genişliği üzerinde etki oluşturma</span><span class="sxs-lookup"><span data-stu-id="f76a6-138">Influence network bandwidth</span></span>
1. <span data-ttu-id="f76a6-139">Merhaba kayıt defterinde çok gidin**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Replication**.</span><span class="sxs-lookup"><span data-stu-id="f76a6-139">In hello registry navigate too**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Replication**.</span></span>
   * <span data-ttu-id="f76a6-140">bir çoğaltma diskte tooinfluence hello bant genişliği trafiği değiştirebilir hello değeri hello **UploadThreadsPerVM**, veya yoksa hello anahtar oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f76a6-140">tooinfluence hello bandwidth traffic on a replicating disk, modify hello value hello **UploadThreadsPerVM**, or create hello key if it doesn't exist.</span></span>
   * <span data-ttu-id="f76a6-141">Azure, yeniden çalışma trafiği için tooinfluence hello bant genişliği değiştirme hello değeri **DownloadThreadsPerVM**.</span><span class="sxs-lookup"><span data-stu-id="f76a6-141">tooinfluence hello bandwidth for failback traffic from Azure, modify hello value **DownloadThreadsPerVM**.</span></span>
2. <span data-ttu-id="f76a6-142">Merhaba varsayılan değer 4'tür.</span><span class="sxs-lookup"><span data-stu-id="f76a6-142">hello default value is 4.</span></span> <span data-ttu-id="f76a6-143">"Fazla sağlanan" bir ağda, bu kayıt defteri anahtarları hello varsayılan değerlerinin değiştirilmesi.</span><span class="sxs-lookup"><span data-stu-id="f76a6-143">In an “overprovisioned” network, these registry keys should be changed from hello default values.</span></span> <span data-ttu-id="f76a6-144">Merhaba en fazla 32'dir.</span><span class="sxs-lookup"><span data-stu-id="f76a6-144">hello maximum is 32.</span></span> <span data-ttu-id="f76a6-145">Trafik toooptimize hello değeri izleyin.</span><span class="sxs-lookup"><span data-stu-id="f76a6-145">Monitor traffic toooptimize hello value.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f76a6-146">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f76a6-146">Next steps</span></span>

<span data-ttu-id="f76a6-147">Çok Git[4. adım: ağ planlama](hyper-v-site-walkthrough-network.md).</span><span class="sxs-lookup"><span data-stu-id="f76a6-147">Go too[Step 4: Plan networking](hyper-v-site-walkthrough-network.md).</span></span>
