---
title: "Hyper-V VM (VMM olmadan) Azure'a çoğaltma için Azure Site Recovery ile ölçekleme ve kapasite planlaması | Microsoft Docs"
description: "Hyper-V sanal makineleri Azure Site Recovery ile azure'a çoğaltırken planı kapasite ve ölçek bu makaleyi kullanın"
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
ms.openlocfilehash: c7891c188c2cecbbf056fa79672a13bb16fa7fcf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="step-3-plan-capacity-and-scaling-for-hyper-v-to-azure-replication"></a><span data-ttu-id="bbba7-103">3. adım: kapasite ve Hyper-V için Azure çoğaltma ölçeklendirme planlama</span><span class="sxs-lookup"><span data-stu-id="bbba7-103">Step 3: Plan capacity and scaling for Hyper-V to Azure replication</span></span>

<span data-ttu-id="bbba7-104">Bu makale için kapasite planlaması ve ölçeklendirme, şirket içi Hyper-V Vm'lerini (System Center VMM olmadan) çoğaltırken ekleneceğini Azure ile kullanmak [Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="bbba7-104">Use this article to figure out planning for capacity and scaling, when replicating on-premises Hyper-V VMs (without System Center VMM) to Azure with [Azure Site Recovery](site-recovery-overview.md).</span></span>

<span data-ttu-id="bbba7-105">Bu makaleyi okuduktan sonra altındaki bir yorum gönderin ya da teknik sorular [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="bbba7-105">After reading this article, post any comments at the bottom, or ask technical questions on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="how-do-i-start-capacity-planning"></a><span data-ttu-id="bbba7-106">Kapasite planlama nasıl başlamanız gerekir?</span><span class="sxs-lookup"><span data-stu-id="bbba7-106">How do I start capacity planning?</span></span>


<span data-ttu-id="bbba7-107">Çoğaltma ortamınız hakkında bilgi toplamak ve bu makalede vurgulanmış konuları birlikte bu bilgileri kullanarak kapasite planlama.</span><span class="sxs-lookup"><span data-stu-id="bbba7-107">You gather information about your replication environment, and then plan capacity using this information, together with the considerations highlighted in this article.</span></span>


## <a name="gather-information"></a><span data-ttu-id="bbba7-108">Bilgileri toplayın</span><span class="sxs-lookup"><span data-stu-id="bbba7-108">Gather information</span></span>

1. <span data-ttu-id="bbba7-109">VM'ler, VM başına disk ve disk başına depolama dahil olmak üzere çoğaltma ortamınız hakkında bilgi toplayın.</span><span class="sxs-lookup"><span data-stu-id="bbba7-109">Gather information about your replication environment, including VMs, disks per VMs, and storage per disk.</span></span>
2. <span data-ttu-id="bbba7-110">Çoğaltılan veriler için günlük değişim (dalgalanma) oranı tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="bbba7-110">Identify your daily change (churn) rate for replicated data.</span></span> <span data-ttu-id="bbba7-111">Karşıdan [Hyper-V kapasite planlama aracı](https://www.microsoft.com/download/details.aspx?id=39057) değişim oranı alınamıyor.</span><span class="sxs-lookup"><span data-stu-id="bbba7-111">Download the [Hyper-V capacity planning tool](https://www.microsoft.com/download/details.aspx?id=39057) to get the change rate.</span></span> <span data-ttu-id="bbba7-112">Bu aracı ortalamalar yakalamak için bir hafta içinde çalıştırmak öneririz.</span><span class="sxs-lookup"><span data-stu-id="bbba7-112">We recommend you run this tool over a week to capture averages.</span></span>
 

## <a name="figure-out-capacity"></a><span data-ttu-id="bbba7-113">Kapasitesi Şekil</span><span class="sxs-lookup"><span data-stu-id="bbba7-113">Figure out capacity</span></span>

<span data-ttu-id="bbba7-114">Toplama seçtiğiniz bilgilere dayanarak, çalıştırmanız [Site kurtarma kapasite planlayıcısı aracı](http://aka.ms/asr-capacity-planner-excel) kaynak ortamı ve iş yükleri çözümlemek için bant genişliği gereksinimlerini ve sunucu kaynaklarını kaynak konum ve kaynakları (tahmin etme sanal makineler ve depolama vb.) hedef konumda gereken.</span><span class="sxs-lookup"><span data-stu-id="bbba7-114">Based on the information you've gather, you run the [Site Recovery Capacity Planner Tool](http://aka.ms/asr-capacity-planner-excel) to analyze your source environment and workloads, estimate bandwidth needs and server resources for the source location, and the resources (virtual machines and storage etc), that you need in the target location.</span></span> <span data-ttu-id="bbba7-115">Aracı modları birkaç içinde çalıştırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="bbba7-115">You can run the tool in a couple of modes:</span></span>

- <span data-ttu-id="bbba7-116">Hızlı planlama: aracı ağ ve sunucu tahminleri almak için bu modda ortalama bir VM'ler, diskleri, depolama ve değişim oranı sayısına göre çalıştır.</span><span class="sxs-lookup"><span data-stu-id="bbba7-116">Quick planning: Run the tool in this mode to get network and server projections based on an average number of VMs, disks, storage, and change rate.</span></span>
- <span data-ttu-id="bbba7-117">Ayrıntılı planlama: Bu modda aracını çalıştırın ve her iş yükü VM düzeyinde ayrıntılarını sağlayın.</span><span class="sxs-lookup"><span data-stu-id="bbba7-117">Detailed planning: Run the tool in this mode, and provide details of each workload at VM level.</span></span> <span data-ttu-id="bbba7-118">VM uyumluluk çözümlemek ve ağ ve sunucu tahminleri alın.</span><span class="sxs-lookup"><span data-stu-id="bbba7-118">Analyze VM compatibility and get network and server projections.</span></span>

<span data-ttu-id="bbba7-119">Şimdi aracını çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="bbba7-119">Now run the tool:</span></span>

1. <span data-ttu-id="bbba7-120">Karşıdan [aracı](http://aka.ms/asr-capacity-planner-excel)</span><span class="sxs-lookup"><span data-stu-id="bbba7-120">Download the [tool](http://aka.ms/asr-capacity-planner-excel)</span></span>
2. <span data-ttu-id="bbba7-121">Hızlı Planlayıcısı çalıştırmak için izleyin [bu yönergeleri](site-recovery-capacity-planner.md#run-the-quick-planner), senaryo seçip **Hyper-V Azure**.</span><span class="sxs-lookup"><span data-stu-id="bbba7-121">To run the quick planner, follow [these instructions](site-recovery-capacity-planner.md#run-the-quick-planner), and select the scenario **Hyper-V to Azure**.</span></span>
3. <span data-ttu-id="bbba7-122">Ayrıntılı Planlayıcısı çalıştırmak için izleyin [bu yönergeleri](site-recovery-capacity-planner.md#run-the-detailed-planner), senaryo seçip **Hyper-V Azure**.</span><span class="sxs-lookup"><span data-stu-id="bbba7-122">To run the detailed planner, follow [these instructions](site-recovery-capacity-planner.md#run-the-detailed-planner), and select the scenario **Hyper-V to Azure**.</span></span>

## <a name="control-network-bandwidth"></a><span data-ttu-id="bbba7-123">Ağ bant genişliğini denetlemek</span><span class="sxs-lookup"><span data-stu-id="bbba7-123">Control network bandwidth</span></span>

<span data-ttu-id="bbba7-124">Gereksinim duyduğunuz bant genişliği hesaplanan sonra çoğaltma için kullanılan bant genişliği miktarını denetleme seçenekleri birkaç vardır:</span><span class="sxs-lookup"><span data-stu-id="bbba7-124">After you've calculated the bandwidth you need, you have a couple of options for controlling the amount of bandwidth used for replication:</span></span>

* <span data-ttu-id="bbba7-125">**Bant genişliğini kısıtlama**: Azure'a çoğaltılan Hyper-V trafiği belirli bir Hyper-V ana bilgisayar üzerinden gider.</span><span class="sxs-lookup"><span data-stu-id="bbba7-125">**Throttle bandwidth**: Hyper-V traffic that replicates to Azure goes through a specific Hyper-V host.</span></span> <span data-ttu-id="bbba7-126">Ana bilgisayar sunucusunda bant genişliğini kısıtlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bbba7-126">You can throttle bandwidth on the host server.</span></span>
* <span data-ttu-id="bbba7-127">**Bant genişliği üzerinde etki**: birkaç kayıt defteri anahtarlarını kullanarak çoğaltma için kullanılan bant genişliği etkileyebilir.</span><span class="sxs-lookup"><span data-stu-id="bbba7-127">**Influence bandwidth**: You can influence the bandwidth used for replication using a couple of registry keys.</span></span>

### <a name="throttle-bandwidth"></a><span data-ttu-id="bbba7-128">Bant genişliğini kısıtlama</span><span class="sxs-lookup"><span data-stu-id="bbba7-128">Throttle bandwidth</span></span>
1. <span data-ttu-id="bbba7-129">Hyper-V ana bilgisayar sunucusunda Microsoft Azure Backup MMC ek bileşenini açın.</span><span class="sxs-lookup"><span data-stu-id="bbba7-129">Open the Microsoft Azure Backup MMC snap-in on the Hyper-V host server.</span></span> <span data-ttu-id="bbba7-130">Varsayılan olarak Microsoft Azure Backup için masaüstünde veya C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin yolunda bir kısayol bulunur.</span><span class="sxs-lookup"><span data-stu-id="bbba7-130">By default a shortcut for Microsoft Azure Backup is available on the desktop or in C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin.</span></span>
2. <span data-ttu-id="bbba7-131">Ek bileşende **Özellikleri Değiştir**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="bbba7-131">In the snap-in click **Change Properties**.</span></span>
3. <span data-ttu-id="bbba7-132">**Azaltma** sekmesinde **Yedekleme işlemleri için internet bant genişliği kullanımını azaltmayı etkinleştir** seçeneğini belirleyin ve çalışma saatleri ve çalışma dışı saatler için sınırları ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="bbba7-132">On the **Throttling** tab select **Enable internet bandwidth usage throttling for backup operations**, and set the limits for work and non-work hours.</span></span> <span data-ttu-id="bbba7-133">Geçerli aralıklar saniye başına 512 Kbps ila 102 Mbps arasındadır.</span><span class="sxs-lookup"><span data-stu-id="bbba7-133">Valid ranges are from 512 Kbps to 102 Mbps per second.</span></span>

    ![Bant genişliğini kısıtlama](./media/hyper-v-site-walkthrough-capacity/throttle2.png)

<span data-ttu-id="bbba7-135">Ayrıca, azaltma ayarı için [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409.aspx) cmdlet'ini de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bbba7-135">You can also use the [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409.aspx) cmdlet to set throttling.</span></span> <span data-ttu-id="bbba7-136">Bu ayara ilişkin örneği aşağıda bulabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="bbba7-136">Here's a sample:</span></span>

    $mon = [System.DayOfWeek]::Monday
    $tue = [System.DayOfWeek]::Tuesday
    Set-OBMachineSetting -WorkDay $mon, $tue -StartWorkHour "9:00:00" -EndWorkHour "18:00:00" -WorkHourBandwidth  (512*1024) -NonWorkHourBandwidth (2048*1024)

<span data-ttu-id="bbba7-137">**Set-OBMachineSetting - NoThrottle** hiçbir azaltmanın gerekli olmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="bbba7-137">**Set-OBMachineSetting -NoThrottle** indicates that no throttling is required.</span></span>

### <a name="influence-network-bandwidth"></a><span data-ttu-id="bbba7-138">Ağ bant genişliği üzerinde etki oluşturma</span><span class="sxs-lookup"><span data-stu-id="bbba7-138">Influence network bandwidth</span></span>
1. <span data-ttu-id="bbba7-139">Kayıt defterinde, **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Replication** hedefine gidin.</span><span class="sxs-lookup"><span data-stu-id="bbba7-139">In the registry navigate to **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Replication**.</span></span>
   * <span data-ttu-id="bbba7-140">Bir çoğaltma diskte bant genişliği trafiği etkilemek için değerini değiştirin **UploadThreadsPerVM**, veya yoksa anahtar oluşturun.</span><span class="sxs-lookup"><span data-stu-id="bbba7-140">To influence the bandwidth traffic on a replicating disk, modify the value the **UploadThreadsPerVM**, or create the key if it doesn't exist.</span></span>
   * <span data-ttu-id="bbba7-141">Azure'dan yeniden çalışma trafiği için bant genişliği etkilemek için değerini değiştirin **DownloadThreadsPerVM**.</span><span class="sxs-lookup"><span data-stu-id="bbba7-141">To influence the bandwidth for failback traffic from Azure, modify the value **DownloadThreadsPerVM**.</span></span>
2. <span data-ttu-id="bbba7-142">Varsayılan değer 4'tür.</span><span class="sxs-lookup"><span data-stu-id="bbba7-142">The default value is 4.</span></span> <span data-ttu-id="bbba7-143">"Fazla sağlanan" bir ağda, bu kayıt defteri anahtarlarının varsayılan değerlerinin değiştirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="bbba7-143">In an “overprovisioned” network, these registry keys should be changed from the default values.</span></span> <span data-ttu-id="bbba7-144">Maksimum değer 32'dir.</span><span class="sxs-lookup"><span data-stu-id="bbba7-144">The maximum is 32.</span></span> <span data-ttu-id="bbba7-145">Değeri iyileştirmek için trafiği izleyin.</span><span class="sxs-lookup"><span data-stu-id="bbba7-145">Monitor traffic to optimize the value.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bbba7-146">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="bbba7-146">Next steps</span></span>

<span data-ttu-id="bbba7-147">Git [4. adım: ağ planlama](hyper-v-site-walkthrough-network.md).</span><span class="sxs-lookup"><span data-stu-id="bbba7-147">Go to [Step 4: Plan networking](hyper-v-site-walkthrough-network.md).</span></span>
