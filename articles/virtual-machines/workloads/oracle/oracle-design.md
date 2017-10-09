---
title: "Azure üzerinde veritabanı aaaDesign ve uygulama bir Oracle | Microsoft Docs"
description: "Tasarım ve Azure ortamınızda bir Oracle veritabanına uygulayın."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: v-shiuma
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 6/22/2017
ms.author: rclaus
ms.openlocfilehash: 8fa1207458695df1c7330ec626888b1b6b8d8939
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="design-and-implement-an-oracle-database-in-azure"></a><span data-ttu-id="0fec9-103">Bir Oracle veritabanına Azure'da tasarlayıp</span><span class="sxs-lookup"><span data-stu-id="0fec9-103">Design and implement an Oracle database in Azure</span></span>

## <a name="assumptions"></a><span data-ttu-id="0fec9-104">Varsayımlar</span><span class="sxs-lookup"><span data-stu-id="0fec9-104">Assumptions</span></span>

- <span data-ttu-id="0fec9-105">Şirket içi tooAzure Oracle veritabanından toomigrate planlamanız durumunda.</span><span class="sxs-lookup"><span data-stu-id="0fec9-105">You're planning toomigrate an Oracle database from on-premises tooAzure.</span></span>
- <span data-ttu-id="0fec9-106">Oracle AWR raporlarda çeşitli ölçümleri hello bilgiye sahip.</span><span class="sxs-lookup"><span data-stu-id="0fec9-106">You have an understanding of hello various metrics in Oracle AWR reports.</span></span>
- <span data-ttu-id="0fec9-107">Uygulama performansı ve platform kullanımı bir temel bilgilere sahipsiniz.</span><span class="sxs-lookup"><span data-stu-id="0fec9-107">You have a baseline understanding of application performance and platform utilization.</span></span>

## <a name="goals"></a><span data-ttu-id="0fec9-108">Hedefleri</span><span class="sxs-lookup"><span data-stu-id="0fec9-108">Goals</span></span>

- <span data-ttu-id="0fec9-109">Anlamak nasıl toooptimize Oracle dağıtımınızda Azure.</span><span class="sxs-lookup"><span data-stu-id="0fec9-109">Understand how toooptimize your Oracle deployment in Azure.</span></span>
- <span data-ttu-id="0fec9-110">Bir Oracle veritabanına bir Azure ortamı için seçenekleri ayarlama performans keşfedin.</span><span class="sxs-lookup"><span data-stu-id="0fec9-110">Explore performance tuning options for an Oracle database in an Azure environment.</span></span>

## <a name="hello-differences-between-an-on-premises-and-azure-implementation"></a><span data-ttu-id="0fec9-111">Merhaba şirket içi arasındaki farklar ve Azure uygulaması</span><span class="sxs-lookup"><span data-stu-id="0fec9-111">hello differences between an on-premises and Azure implementation</span></span> 

<span data-ttu-id="0fec9-112">Bazı şeyleri tookeep geçirilirken aklınızda içi uygulamaları tooAzure önemli şunlardır.</span><span class="sxs-lookup"><span data-stu-id="0fec9-112">Following are some important things tookeep in mind when you're migrating on-premises applications tooAzure.</span></span> 

<span data-ttu-id="0fec9-113">Bir önemli fark, bir Azure uygulamasında VM'ler, diskler ve sanal ağlar gibi kaynakları diğer istemciler arasında paylaşılır kaynaklanır.</span><span class="sxs-lookup"><span data-stu-id="0fec9-113">One important difference is that in an Azure implementation, resources such as VMs, disks, and virtual networks are shared among other clients.</span></span> <span data-ttu-id="0fec9-114">Ayrıca, kaynakları hello gereksinimlerine göre kısıtlanan.</span><span class="sxs-lookup"><span data-stu-id="0fec9-114">In addition, resources can be throttled based on hello requirements.</span></span> <span data-ttu-id="0fec9-115">(MTBF) başarısız önleme odaklanan yerine Azure daha hello hatası (MTTR) geri kalan odaklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="0fec9-115">Instead of focusing on avoiding failing (MTBF), Azure is more focused on surviving hello failure (MTTR).</span></span>

<span data-ttu-id="0fec9-116">Merhaba aşağıdaki tabloda bazı hello bir şirket içi uygulama ve Oracle veritabanına Azure uygulaması arasındaki farklar listelenmektedir.</span><span class="sxs-lookup"><span data-stu-id="0fec9-116">hello following table lists some of hello differences between an on-premises implementation and an Azure implementation of an Oracle database.</span></span>

> 
> |  | <span data-ttu-id="0fec9-117">**Şirket içi uygulama**</span><span class="sxs-lookup"><span data-stu-id="0fec9-117">**On-premises implementation**</span></span> | <span data-ttu-id="0fec9-118">**Azure uygulama**</span><span class="sxs-lookup"><span data-stu-id="0fec9-118">**Azure implementation**</span></span> |
> | --- | --- | --- |
> | <span data-ttu-id="0fec9-119">**Ağ**</span><span class="sxs-lookup"><span data-stu-id="0fec9-119">**Networking**</span></span> |<span data-ttu-id="0fec9-120">LAN VE WAN</span><span class="sxs-lookup"><span data-stu-id="0fec9-120">LAN/WAN</span></span>  |<span data-ttu-id="0fec9-121">SDN (yazılım tanımlı ağ)</span><span class="sxs-lookup"><span data-stu-id="0fec9-121">SDN (software-defined networking)</span></span>|
> | <span data-ttu-id="0fec9-122">**Güvenlik grubu**</span><span class="sxs-lookup"><span data-stu-id="0fec9-122">**Security group**</span></span> |<span data-ttu-id="0fec9-123">IP/bağlantı noktasına kısıtlama araçları</span><span class="sxs-lookup"><span data-stu-id="0fec9-123">IP/port restriction tools</span></span> |[<span data-ttu-id="0fec9-124">Ağ güvenlik grubu (NSG)</span><span class="sxs-lookup"><span data-stu-id="0fec9-124">Network Security Group (NSG)</span></span>](https://azure.microsoft.com/blog/network-security-groups) |
> | <span data-ttu-id="0fec9-125">**Esnekliği**</span><span class="sxs-lookup"><span data-stu-id="0fec9-125">**Resilience**</span></span> |<span data-ttu-id="0fec9-126">MTBF (hataları arasındaki ortalama süre)</span><span class="sxs-lookup"><span data-stu-id="0fec9-126">MTBF (mean time between failures)</span></span> |<span data-ttu-id="0fec9-127">MTTR (saati toorecovery)</span><span class="sxs-lookup"><span data-stu-id="0fec9-127">MTTR (mean time toorecovery)</span></span>|
> | <span data-ttu-id="0fec9-128">**Planlı bakım**</span><span class="sxs-lookup"><span data-stu-id="0fec9-128">**Planned maintenance**</span></span> |<span data-ttu-id="0fec9-129">Düzeltme eki uygulama yükseltme</span><span class="sxs-lookup"><span data-stu-id="0fec9-129">Patching/upgrades</span></span>|<span data-ttu-id="0fec9-130">[Kullanılabilirlik kümeleri](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines) (düzeltme eki uygulama/Azure tarafından yönetilen yükseltme)</span><span class="sxs-lookup"><span data-stu-id="0fec9-130">[Availability sets](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines) (patching/upgrades managed by Azure)</span></span> |
> | <span data-ttu-id="0fec9-131">**Kaynak**</span><span class="sxs-lookup"><span data-stu-id="0fec9-131">**Resource**</span></span> |<span data-ttu-id="0fec9-132">Adanmış</span><span class="sxs-lookup"><span data-stu-id="0fec9-132">Dedicated</span></span>  |<span data-ttu-id="0fec9-133">Diğer istemcilerle paylaşılan</span><span class="sxs-lookup"><span data-stu-id="0fec9-133">Shared with other clients</span></span>|
> | <span data-ttu-id="0fec9-134">**Bölgeler**</span><span class="sxs-lookup"><span data-stu-id="0fec9-134">**Regions**</span></span> |<span data-ttu-id="0fec9-135">Veri merkezleri</span><span class="sxs-lookup"><span data-stu-id="0fec9-135">Datacenters</span></span> |[<span data-ttu-id="0fec9-136">Bölge çiftleri</span><span class="sxs-lookup"><span data-stu-id="0fec9-136">Region pairs</span></span>](https://docs.microsoft.com/azure/virtual-machines/windows/regions-and-availability)|
> | <span data-ttu-id="0fec9-137">**Depolama**</span><span class="sxs-lookup"><span data-stu-id="0fec9-137">**Storage**</span></span> |<span data-ttu-id="0fec9-138">SAN/fiziksel diskleri</span><span class="sxs-lookup"><span data-stu-id="0fec9-138">SAN/physical disks</span></span> |[<span data-ttu-id="0fec9-139">Azure tarafından yönetilen depolama</span><span class="sxs-lookup"><span data-stu-id="0fec9-139">Azure-managed storage</span></span>](https://azure.microsoft.com/pricing/details/managed-disks/?v=17.23h)|
> | <span data-ttu-id="0fec9-140">**Ölçeklendirme**</span><span class="sxs-lookup"><span data-stu-id="0fec9-140">**Scale**</span></span> |<span data-ttu-id="0fec9-141">Dikey Ölçek</span><span class="sxs-lookup"><span data-stu-id="0fec9-141">Vertical scale</span></span> |<span data-ttu-id="0fec9-142">Yatay ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="0fec9-142">Horizontal scale</span></span>|


### <a name="requirements"></a><span data-ttu-id="0fec9-143">Gereksinimler</span><span class="sxs-lookup"><span data-stu-id="0fec9-143">Requirements</span></span>

- <span data-ttu-id="0fec9-144">Başlangıç veritabanı boyutu ve büyüme oranını belirler.</span><span class="sxs-lookup"><span data-stu-id="0fec9-144">Determine hello database size and growth rate.</span></span>
- <span data-ttu-id="0fec9-145">Oracle AWR raporları veya diğer ağ izleme araçları göre tahmin hello IOPS gereksinimlerini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="0fec9-145">Determine hello IOPS requirements, which you can estimate based on Oracle AWR reports or other network monitoring tools.</span></span>

## <a name="configuration-options"></a><span data-ttu-id="0fec9-146">Yapılandırma seçenekleri</span><span class="sxs-lookup"><span data-stu-id="0fec9-146">Configuration options</span></span>

<span data-ttu-id="0fec9-147">Bir Azure ortamı tooimprove performans ayarlayabilirsiniz dört olası alanları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="0fec9-147">There are four potential areas that you can tune tooimprove performance in an Azure environment:</span></span>

- <span data-ttu-id="0fec9-148">Sanal makine boyutu</span><span class="sxs-lookup"><span data-stu-id="0fec9-148">Virtual machine size</span></span>
- <span data-ttu-id="0fec9-149">Ağ verimliliği</span><span class="sxs-lookup"><span data-stu-id="0fec9-149">Network throughput</span></span>
- <span data-ttu-id="0fec9-150">Disk türleri ve yapılandırmalar</span><span class="sxs-lookup"><span data-stu-id="0fec9-150">Disk types and configurations</span></span>
- <span data-ttu-id="0fec9-151">Disk önbelleği ayarları</span><span class="sxs-lookup"><span data-stu-id="0fec9-151">Disk cache settings</span></span>

### <a name="generate-an-awr-report"></a><span data-ttu-id="0fec9-152">Bir AWR raporu oluşturun</span><span class="sxs-lookup"><span data-stu-id="0fec9-152">Generate an AWR report</span></span>

<span data-ttu-id="0fec9-153">Varolan bir Oracle veritabanına varsa ve toomigrate tooAzure planlama, birkaç seçeneğiniz vardır.</span><span class="sxs-lookup"><span data-stu-id="0fec9-153">If you have an existing an Oracle database and are planning toomigrate tooAzure, you have several options.</span></span> <span data-ttu-id="0fec9-154">Merhaba Oracle AWR rapor tooget hello ölçümleri (IOPS, MB/sn, GiBs ve benzeri) çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0fec9-154">You can run hello Oracle AWR report tooget hello metrics (IOPS, Mbps, GiBs, and so on).</span></span> <span data-ttu-id="0fec9-155">Ardından hello VM topladığınız hello ölçülerine bağlı olarak seçin.</span><span class="sxs-lookup"><span data-stu-id="0fec9-155">Then choose hello VM based on hello metrics that you collected.</span></span> <span data-ttu-id="0fec9-156">Veya, altyapı takım tooget benzer bilgilerinizi başvurun.</span><span class="sxs-lookup"><span data-stu-id="0fec9-156">Or you can contact your infrastructure team tooget similar information.</span></span>

<span data-ttu-id="0fec9-157">Karşılaştırabileceğiniz normal ve yoğun saatler iş yükleri sırasında AWR raporunuzu çalıştıran düşünebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0fec9-157">You might consider running your AWR report during both regular and peak workloads, so you can compare.</span></span> <span data-ttu-id="0fec9-158">Bu raporlarda bağlı olarak, sanal makineleri hello ortalama iş yükü veya hello en fazla iş yükünü dayanarak hello boyutlandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0fec9-158">Based on these reports, you can size hello VMs based on either hello average workload or hello maximum workload.</span></span>

<span data-ttu-id="0fec9-159">Aşağıdaki nasıl örneğidir toogenerate AWR raporu:</span><span class="sxs-lookup"><span data-stu-id="0fec9-159">Following is an example of how toogenerate an AWR report:</span></span>

```bash
$ sqlplus / as sysdba
SQL> EXEC DBMS_WORKLOAD_REPOSITORY.CREATE_SNAPSHOT;
SQL> @?/rdbms/admin/awrrpt.sql
```

### <a name="key-metrics"></a><span data-ttu-id="0fec9-160">Anahtar ölçümleri</span><span class="sxs-lookup"><span data-stu-id="0fec9-160">Key metrics</span></span>

<span data-ttu-id="0fec9-161">Hello AWR raporu ' edinebilirsiniz hello ölçümler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="0fec9-161">Following are hello metrics that you can obtain from hello AWR report:</span></span>

- <span data-ttu-id="0fec9-162">Çekirdek toplam sayısı</span><span class="sxs-lookup"><span data-stu-id="0fec9-162">Total number of cores</span></span>
- <span data-ttu-id="0fec9-163">CPU saat hızı</span><span class="sxs-lookup"><span data-stu-id="0fec9-163">CPU clock speed</span></span>
- <span data-ttu-id="0fec9-164">GB cinsinden toplam bellek</span><span class="sxs-lookup"><span data-stu-id="0fec9-164">Total memory in GB</span></span>
- <span data-ttu-id="0fec9-165">CPU kullanımı</span><span class="sxs-lookup"><span data-stu-id="0fec9-165">CPU utilization</span></span>
- <span data-ttu-id="0fec9-166">En yüksek veri aktarım hızı</span><span class="sxs-lookup"><span data-stu-id="0fec9-166">Peak data transfer rate</span></span>
- <span data-ttu-id="0fec9-167">G/ç değişiklikleri (okuma/yazma) oranı</span><span class="sxs-lookup"><span data-stu-id="0fec9-167">Rate of I/O changes (read/write)</span></span>
- <span data-ttu-id="0fec9-168">Günlük oranı (MBPs) Yinele</span><span class="sxs-lookup"><span data-stu-id="0fec9-168">Redo log rate (MBPs)</span></span>
- <span data-ttu-id="0fec9-169">Ağ verimliliği</span><span class="sxs-lookup"><span data-stu-id="0fec9-169">Network throughput</span></span>
- <span data-ttu-id="0fec9-170">Ağ gecikmesi hızı (düşük/yüksek)</span><span class="sxs-lookup"><span data-stu-id="0fec9-170">Network latency rate (low/high)</span></span>
- <span data-ttu-id="0fec9-171">Veritabanı boyutu GB</span><span class="sxs-lookup"><span data-stu-id="0fec9-171">Database size in GB</span></span>
- <span data-ttu-id="0fec9-172">SQL ile alınan bayt sayısı * ağı birbirinden / tooclient</span><span class="sxs-lookup"><span data-stu-id="0fec9-172">Bytes received via SQL*Net from/tooclient</span></span>

### <a name="virtual-machine-size"></a><span data-ttu-id="0fec9-173">Sanal makine boyutu</span><span class="sxs-lookup"><span data-stu-id="0fec9-173">Virtual machine size</span></span>

#### <a name="1-estimate-vm-size-based-on-cpu-memory-and-io-usage-from-hello-awr-report"></a><span data-ttu-id="0fec9-174">1. VM boyutu hello CPU, bellek ve g/ç kullanımdan AWR rapor temel tahmin etme</span><span class="sxs-lookup"><span data-stu-id="0fec9-174">1. Estimate VM size based on CPU, memory, and I/O usage from hello AWR report</span></span>

<span data-ttu-id="0fec9-175">Bakmak bir hello sistem performans sorunlarının nerede belirten hello üst beş zamanlanmış ön plan olayları şeydir.</span><span class="sxs-lookup"><span data-stu-id="0fec9-175">One thing you might look at is hello top five timed foreground events that indicate where hello system bottlenecks are.</span></span>

<span data-ttu-id="0fec9-176">Örneğin, diyagram aşağıdaki hello hello günlük dosyası eşitleme hello tepesinde bulunur.</span><span class="sxs-lookup"><span data-stu-id="0fec9-176">For example, in hello following diagram, hello log file sync is at hello top.</span></span> <span data-ttu-id="0fec9-177">Merhaba LGWR hello günlük arabellek toohello Yinele günlük dosyasına yazar önce gerekli olan bekler hello sayısını gösterir.</span><span class="sxs-lookup"><span data-stu-id="0fec9-177">It indicates hello number of waits that are required before hello LGWR writes hello log buffer toohello redo log file.</span></span> <span data-ttu-id="0fec9-178">Bu sonuçları, daha iyi performanslı depolama veya diskleri gerekli olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="0fec9-178">These results indicate that better performing storage or disks are required.</span></span> <span data-ttu-id="0fec9-179">Ayrıca, hello diyagramı CPU (çekirdekler) hello sayısını ve hello bellek miktarını gösterir.</span><span class="sxs-lookup"><span data-stu-id="0fec9-179">In addition, hello diagram also shows hello number of CPU (cores) and hello amount of memory.</span></span>

![Merhaba AWR raporu sayfasının ekran görüntüsü](./media/oracle-design/cpu_memory_info.png)

<span data-ttu-id="0fec9-181">Merhaba Aşağıdaki diyagramda hello toplam g/ç okuma ve yazma gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="0fec9-181">hello following diagram shows hello total I/O of read and write.</span></span> <span data-ttu-id="0fec9-182">59 okuma GB ve 247.3 hello rapor hello süre boyunca yazılmış GB vardı.</span><span class="sxs-lookup"><span data-stu-id="0fec9-182">There were 59 GB read and 247.3 GB written during hello time of hello report.</span></span>

![Merhaba AWR raporu sayfasının ekran görüntüsü](./media/oracle-design/io_info.png)

#### <a name="2-choose-a-vm"></a><span data-ttu-id="0fec9-184">2. Bir VM seçin</span><span class="sxs-lookup"><span data-stu-id="0fec9-184">2. Choose a VM</span></span>

<span data-ttu-id="0fec9-185">Merhaba AWR rapor ' toplanan hello bilgilere dayanarak, hello sonraki toochoose gereksinimlerinizi karşılayan benzer bir boyutu VM'i adımdır.</span><span class="sxs-lookup"><span data-stu-id="0fec9-185">Based on hello information that you collected from hello AWR report, hello next step is toochoose a VM of a similar size that meets your requirements.</span></span> <span data-ttu-id="0fec9-186">Kullanılabilir sanal makineleri listesini hello makalesinde bulabilirsiniz [bellek için iyileştirilmiş](https://docs.microsoft.com/azure/virtual-machinFine tune es/virtual-machines-windows-sizes-memory).</span><span class="sxs-lookup"><span data-stu-id="0fec9-186">You can find a list of available VMs in hello article [Memory optimized](https://docs.microsoft.com/azure/virtual-machinFine tune es/virtual-machines-windows-sizes-memory).</span></span>

#### <a name="3-fine-tune-hello-vm-sizing-with-a-similar-vm-series-based-on-hello-acu"></a><span data-ttu-id="0fec9-187">3. Merhaba ACU üzerinde temel benzer bir VM dizisi ile Merhaba VM boyutlandırma ince ayar yapma</span><span class="sxs-lookup"><span data-stu-id="0fec9-187">3. Fine-tune hello VM sizing with a similar VM series based on hello ACU</span></span>

<span data-ttu-id="0fec9-188">Merhaba VM seçtikten sonra dikkat toohello ACU hello VM için ödeme yaparsınız.</span><span class="sxs-lookup"><span data-stu-id="0fec9-188">After you've chosen hello VM, pay attention toohello ACU for hello VM.</span></span> <span data-ttu-id="0fec9-189">Gereksinimlerinize daha iyi uyacak ACU değeri hello üzerinde göre farklı bir VM seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0fec9-189">You might choose a different VM based on hello ACU value that better suits your requirements.</span></span> <span data-ttu-id="0fec9-190">Daha fazla bilgi için bkz: [Azure işlem birimi](https://docs.microsoft.com/azure/virtual-machines/windows/acu).</span><span class="sxs-lookup"><span data-stu-id="0fec9-190">For more information, see [Azure compute unit](https://docs.microsoft.com/azure/virtual-machines/windows/acu).</span></span>

![Merhaba ACU birimleri sayfasının ekran görüntüsü](./media/oracle-design/acu_units.png)

### <a name="network-throughput"></a><span data-ttu-id="0fec9-192">Ağ verimliliği</span><span class="sxs-lookup"><span data-stu-id="0fec9-192">Network throughput</span></span>

<span data-ttu-id="0fec9-193">Diyagram aşağıdaki hello hello verimlilik ve IOPS arasındaki ilişki gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="0fec9-193">hello following diagram shows hello relation between throughput and IOPS:</span></span>

![Üretilen iş ekran görüntüsü](./media/oracle-design/throughput.png)

<span data-ttu-id="0fec9-195">Merhaba toplam ağ verimini aşağıdaki bilgilerle hello göre tahmini:</span><span class="sxs-lookup"><span data-stu-id="0fec9-195">hello total network throughput is estimated based on hello following information:</span></span>
- <span data-ttu-id="0fec9-196">SQL * Net trafiği</span><span class="sxs-lookup"><span data-stu-id="0fec9-196">SQL*Net traffic</span></span>
- <span data-ttu-id="0fec9-197">MB/sn x sunucularını (Oracle Data Guard gibi giden akış) sayısı</span><span class="sxs-lookup"><span data-stu-id="0fec9-197">MBps x number of servers (outbound stream such as Oracle Data Guard)</span></span>
- <span data-ttu-id="0fec9-198">Uygulama çoğaltma gibi diğer faktörlere</span><span class="sxs-lookup"><span data-stu-id="0fec9-198">Other factors, such as application replication</span></span>

![Ekran görüntüsü hello SQL * Net işleme](./media/oracle-design/sqlnet_info.png)

<span data-ttu-id="0fec9-200">Ağ bant genişliği gereksinimlerine bağlı olarak, çeşitli ağ geçidi türleri, toochoose için vardır.</span><span class="sxs-lookup"><span data-stu-id="0fec9-200">Based on your network bandwidth requirements, there are various gateway types for you toochoose from.</span></span> <span data-ttu-id="0fec9-201">Bunlar, temel, VpnGw ve Azure ExpressRoute içerir.</span><span class="sxs-lookup"><span data-stu-id="0fec9-201">These include basic, VpnGw, and Azure ExpressRoute.</span></span> <span data-ttu-id="0fec9-202">Daha fazla bilgi için bkz: Merhaba [VPN ağ geçidi fiyatlandırma sayfası](https://azure.microsoft.com/en-us/pricing/details/vpn-gateway/?v=17.23h).</span><span class="sxs-lookup"><span data-stu-id="0fec9-202">For more information, see hello [VPN gateway pricing page](https://azure.microsoft.com/en-us/pricing/details/vpn-gateway/?v=17.23h).</span></span>

<span data-ttu-id="0fec9-203">**Öneriler**</span><span class="sxs-lookup"><span data-stu-id="0fec9-203">**Recommendations**</span></span>

- <span data-ttu-id="0fec9-204">Ağ gecikmesi yüksek karşılaştırılan tooan şirket içi dağıtımıdır.</span><span class="sxs-lookup"><span data-stu-id="0fec9-204">Network latency is higher compared tooan on-premises deployment.</span></span> <span data-ttu-id="0fec9-205">Ağ dönüşleri can round önemli ölçüde azaltan performansı artırır.</span><span class="sxs-lookup"><span data-stu-id="0fec9-205">Reducing network round trips can greatly improve performance.</span></span>
- <span data-ttu-id="0fec9-206">tooreduce gidiş dönüş birleştirmek yüksek işlemler veya "chatty" uygulamalar üzerinde hello olan uygulamalar aynı sanal makine.</span><span class="sxs-lookup"><span data-stu-id="0fec9-206">tooreduce round-trips, consolidate applications that have high transactions or “chatty” apps on hello same virtual machine.</span></span>

### <a name="disk-types-and-configurations"></a><span data-ttu-id="0fec9-207">Disk türleri ve yapılandırmalar</span><span class="sxs-lookup"><span data-stu-id="0fec9-207">Disk types and configurations</span></span>

- <span data-ttu-id="0fec9-208">*Varsayılan işletim sistemi disk*: kalıcı veri ve önbelleğe alma bu disk türleri sunar.</span><span class="sxs-lookup"><span data-stu-id="0fec9-208">*Default OS disks*: These disk types offer persistent data and caching.</span></span> <span data-ttu-id="0fec9-209">Başlangıçta OS erişimi için optimize ve için tasarlanmamış işlemsel veya veri ambarı (analitik) iş yükleri.</span><span class="sxs-lookup"><span data-stu-id="0fec9-209">They are optimized for OS access at startup, and aren't designed for either transactional or data warehouse (analytical) workloads.</span></span>

- <span data-ttu-id="0fec9-210">*Yönetilmeyen diskleri*: Bu disk türleriyle tooyour VM diskleri karşılık hello sanal sabit disk (VHD) dosyaları depolamak hello depolama hesaplarını yönetme.</span><span class="sxs-lookup"><span data-stu-id="0fec9-210">*Unmanaged disks*: With these disk types, you manage hello storage accounts that store hello virtual hard disk (VHD) files that correspond tooyour VM disks.</span></span> <span data-ttu-id="0fec9-211">VHD dosyaları, Azure storage hesapları sayfa bloblarını olarak depolanır.</span><span class="sxs-lookup"><span data-stu-id="0fec9-211">VHD files are stored as page blobs in Azure storage accounts.</span></span>

- <span data-ttu-id="0fec9-212">*Yönetilen diskleri*: Azure VM diskleriniz için kullandığınız hello depolama hesapları yönetir.</span><span class="sxs-lookup"><span data-stu-id="0fec9-212">*Managed disks*: Azure manages hello storage accounts that you use for your VM disks.</span></span> <span data-ttu-id="0fec9-213">Merhaba disk türünü (premium veya standart) ve hello ihtiyacınız hello diskin boyutunu belirtin.</span><span class="sxs-lookup"><span data-stu-id="0fec9-213">You specify hello disk type (premium or standard) and hello size of hello disk that you need.</span></span> <span data-ttu-id="0fec9-214">Azure oluşturur ve hello disk tarafından yönetilir.</span><span class="sxs-lookup"><span data-stu-id="0fec9-214">Azure creates and manages hello disk for you.</span></span>

- <span data-ttu-id="0fec9-215">*Premium depolama diskleri*: Bu disk türleri üretim iş yükleri için uygundur.</span><span class="sxs-lookup"><span data-stu-id="0fec9-215">*Premium storage disks*: These disk types are best suited for production workloads.</span></span> <span data-ttu-id="0fec9-216">Olabilir premium depolama destekler VM diskleri ekli toospecific boyutu-serisi VM, DS, DSv2, GS ve F serisi VM'ler gibi.</span><span class="sxs-lookup"><span data-stu-id="0fec9-216">Premium storage supports VM disks that can be attached toospecific size-series VMs, such as DS, DSv2, GS, and F series VMs.</span></span> <span data-ttu-id="0fec9-217">farklı boyutlarda ile Merhaba premium disk gelir ve 096 GB 32 GB too4 arasında değişen diskleri arasından seçim yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0fec9-217">hello premium disk comes with different sizes, and you can choose between disks ranging from 32 GB too4,096 GB.</span></span> <span data-ttu-id="0fec9-218">Her disk boyutu, kendi performans özellikleri vardır.</span><span class="sxs-lookup"><span data-stu-id="0fec9-218">Each disk size has its own performance specifications.</span></span> <span data-ttu-id="0fec9-219">Uygulama gereksinimlerinize bağlı olarak, bir veya daha fazla disk tooyour VM ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0fec9-219">Depending on your application requirements, you can attach one or more disks tooyour VM.</span></span>

<span data-ttu-id="0fec9-220">Merhaba portalından yeni bir yönetilen disk oluşturduğunuzda, hello seçebilirsiniz **hesap türü** hello disk türünün toouse istiyor.</span><span class="sxs-lookup"><span data-stu-id="0fec9-220">When you create a new managed disk from hello portal, you can choose hello **Account type** for hello type of disk you want toouse.</span></span> <span data-ttu-id="0fec9-221">Tüm kullanılabilir diskleri hello açılır menüde gösterilmiştir aklınızda bulundurun.</span><span class="sxs-lookup"><span data-stu-id="0fec9-221">Keep in mind that not all available disks are shown in hello drop-down menu.</span></span> <span data-ttu-id="0fec9-222">Belirli bir VM boyutu seçtikten sonra hello menüsü yalnızca hello kullanılabilir premium storage bu VM boyutuna göre SKU'ları gösterir.</span><span class="sxs-lookup"><span data-stu-id="0fec9-222">After you choose a particular VM size, hello menu shows only hello available premium storage SKUs that are based on that VM size.</span></span>

![Merhaba yönetilen disk sayfasının ekran görüntüsü](./media/oracle-design/premium_disk01.png)

<span data-ttu-id="0fec9-224">Daha fazla bilgi için bkz: [yüksek performanslı Premium depolama ve VM'ler için yönetilen diskleri](https://docs.microsoft.com/azure/storage/storage-premium-storage).</span><span class="sxs-lookup"><span data-stu-id="0fec9-224">For more information, see [High-performance Premium Storage and managed disks for VMs](https://docs.microsoft.com/azure/storage/storage-premium-storage).</span></span>

<span data-ttu-id="0fec9-225">Depolama alanınızın bir VM üzerinde yapılandırdıktan sonra bir veritabanı oluşturmadan önce tooload test hello diskleri isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0fec9-225">After you configure your storage on a VM, you might want tooload test hello disks before creating a database.</span></span> <span data-ttu-id="0fec9-226">Gecikme süresi ve Verimlilik açısından Hello g/ç oranı hello VM'ler hello destekliyorsa belirlemenize yardımcı olacak bilerek işleme gecikmesi hedefleri ile bekleniyordu.</span><span class="sxs-lookup"><span data-stu-id="0fec9-226">Knowing hello I/O rate in terms of both latency and throughput can help you determine if hello VMs support hello expected throughput with latency targets.</span></span>

<span data-ttu-id="0fec9-227">Uygulama yükleme, Oracle Orion, Sysbench ve Fio gibi test araçları mevcuttur.</span><span class="sxs-lookup"><span data-stu-id="0fec9-227">There are a number of tools for application load testing, such as Oracle Orion, Sysbench, and Fio.</span></span>

<span data-ttu-id="0fec9-228">Bir Oracle veritabanına dağıtıldıktan sonra hello yük testi yeniden çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="0fec9-228">Run hello load test again after you've deployed an Oracle database.</span></span> <span data-ttu-id="0fec9-229">Normal ve yoğun saatler iş yükleri başlatın ve temel ortamınızın hello sonuçları göster hello.</span><span class="sxs-lookup"><span data-stu-id="0fec9-229">Start your regular and peak workloads, and hello results show you hello baseline of your environment.</span></span>

<span data-ttu-id="0fec9-230">Merhaba depolama boyutu yerine hello IOPS oranı göre daha önemli toosize hello depolama olabilir.</span><span class="sxs-lookup"><span data-stu-id="0fec9-230">It might be more important toosize hello storage based on hello IOPS rate rather than hello storage size.</span></span> <span data-ttu-id="0fec9-231">Hello IOPS 5.000 olmakla birlikte, 200 GB yeterlidir gerekirse, birden fazla ile 200 GB depolama gelse de Örneğin, hala hello P30 sınıfı premium disk alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0fec9-231">For example, if hello required IOPS is 5,000, but you only need 200 GB, you might still get hello P30 class premium disk even though it comes with more than 200 GB of storage.</span></span>

<span data-ttu-id="0fec9-232">Merhaba IOPS oranı AWR rapor hello elde edilebilir.</span><span class="sxs-lookup"><span data-stu-id="0fec9-232">hello IOPS rate can be obtained from hello AWR report.</span></span> <span data-ttu-id="0fec9-233">Merhaba Yinele günlük, fiziksel okuma ve yazma hızı tarafından belirlenir.</span><span class="sxs-lookup"><span data-stu-id="0fec9-233">It's determined by hello redo log, physical reads, and writes rate.</span></span>

![Merhaba AWR raporu sayfasının ekran görüntüsü](./media/oracle-design/awr_report.png)

<span data-ttu-id="0fec9-235">Örneğin, hello Yinele boyutuna eşit too11.63 MB / sn'dir saniye başına 12,200,000 bayt'tır.</span><span class="sxs-lookup"><span data-stu-id="0fec9-235">For example, hello redo size is 12,200,000 bytes per second, which is equal too11.63 MBPs.</span></span>
<span data-ttu-id="0fec9-236">Merhaba IOPS olan 12,200,000 / 2,358 = 5,174.</span><span class="sxs-lookup"><span data-stu-id="0fec9-236">hello IOPS is 12,200,000 / 2,358 = 5,174.</span></span>

<span data-ttu-id="0fec9-237">NET bir resim hello g/ç gereksinimlerinin aldıktan sonra bu gereksinimleri en iyi uygun toomeet sürücülerinin bir birleşimini seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0fec9-237">After you have a clear picture of hello I/O requirements, you can choose a combination of drives that are best suited toomeet those requirements.</span></span>

<span data-ttu-id="0fec9-238">**Öneriler**</span><span class="sxs-lookup"><span data-stu-id="0fec9-238">**Recommendations**</span></span>

- <span data-ttu-id="0fec9-239">Veri tablo alanı için yönetilen depolama veya Oracle ASM kullanarak hello g/ç iş yükü disk sayısı arasında yayılır.</span><span class="sxs-lookup"><span data-stu-id="0fec9-239">For data tablespace, spread hello I/O workload across a number of disks by using managed storage or Oracle ASM.</span></span>
- <span data-ttu-id="0fec9-240">Merhaba g/ç blok boyutu yoğun okuma ve yazma yoğunluklu işlemleri için arttıkça, daha fazla veri diski ekleyin.</span><span class="sxs-lookup"><span data-stu-id="0fec9-240">As hello I/O block size increases for read-intensive and write-intensive operations, add more data disks.</span></span>
- <span data-ttu-id="0fec9-241">Büyük sıralı işlemler için Hello blok boyutunu artırın.</span><span class="sxs-lookup"><span data-stu-id="0fec9-241">Increase hello block size for large sequential processes.</span></span>
- <span data-ttu-id="0fec9-242">Veri sıkıştırma tooreduce g/ç (veri ve dizinler için) kullanın.</span><span class="sxs-lookup"><span data-stu-id="0fec9-242">Use data compression tooreduce I/O (for both data and indexes).</span></span>
- <span data-ttu-id="0fec9-243">Yinele günlükleri, sistem ve temps ayrı ve farklı veri disklerinde TS geri.</span><span class="sxs-lookup"><span data-stu-id="0fec9-243">Separate redo logs, system, and temps, and undo TS on separate data disks.</span></span>
- <span data-ttu-id="0fec9-244">Varsayılan işletim sistemi diskleri (/ dev/sda) tüm uygulama dosyalarını koymayın.</span><span class="sxs-lookup"><span data-stu-id="0fec9-244">Don't put any application files on default OS disks (/dev/sda).</span></span> <span data-ttu-id="0fec9-245">Bu diskleri en iyi duruma getirilmiş olmayan için hızlı VM önyükleme zamanları ve uygulamanız için iyi bir performans sağlamayabilir.</span><span class="sxs-lookup"><span data-stu-id="0fec9-245">These disks aren't optimized for fast VM boot times, and they might not provide good performance for your application.</span></span>

### <a name="disk-cache-settings"></a><span data-ttu-id="0fec9-246">Disk önbelleği ayarları</span><span class="sxs-lookup"><span data-stu-id="0fec9-246">Disk cache settings</span></span>

<span data-ttu-id="0fec9-247">Ana bilgisayar önbelleğe almayı için üç seçenek vardır:</span><span class="sxs-lookup"><span data-stu-id="0fec9-247">There are three options for host caching:</span></span>

- <span data-ttu-id="0fec9-248">*Salt okunur*: gelecekteki okuma için tüm istekleri önbelleğe alınır.</span><span class="sxs-lookup"><span data-stu-id="0fec9-248">*Read-only*: All requests are cached for future reads.</span></span> <span data-ttu-id="0fec9-249">Tüm yazma işlemlerini kalıcı doğrudan tooAzure Blob Depolama.</span><span class="sxs-lookup"><span data-stu-id="0fec9-249">All writes are persisted directly tooAzure Blob storage.</span></span>

- <span data-ttu-id="0fec9-250">*Okuma-yazma*: "İleri okuma" algoritma budur.</span><span class="sxs-lookup"><span data-stu-id="0fec9-250">*Read-write*: This is a “read-ahead” algorithm.</span></span> <span data-ttu-id="0fec9-251">Hello okuma ve yazma işlemleri için gelecekteki okuma önbelleğe alınır.</span><span class="sxs-lookup"><span data-stu-id="0fec9-251">hello reads and writes are cached for future reads.</span></span> <span data-ttu-id="0fec9-252">Olmayan yazma aracılığıyla yazma olan toohello yerel önbelleği ilk kalıcı.</span><span class="sxs-lookup"><span data-stu-id="0fec9-252">Non-write-through writes are persisted toohello local cache first.</span></span> <span data-ttu-id="0fec9-253">Yazma aracılığıyla kullandığı için SQL Server için yazma kalıcı tooAzure depolama var.</span><span class="sxs-lookup"><span data-stu-id="0fec9-253">For SQL Server, writes are persisted tooAzure Storage because it uses write-through.</span></span> <span data-ttu-id="0fec9-254">Hafif iş yükleri için hello düşük disk gecikme süresi de sağlar.</span><span class="sxs-lookup"><span data-stu-id="0fec9-254">It also provides hello lowest disk latency for light workloads.</span></span>

- <span data-ttu-id="0fec9-255">*Hiçbiri* (devre dışı): Bu seçeneği kullanarak, hello önbellek atlayabilir.</span><span class="sxs-lookup"><span data-stu-id="0fec9-255">*None* (disabled): By using this option, you can bypass hello cache.</span></span> <span data-ttu-id="0fec9-256">Tüm hello veriler aktarılan toodisk ve tooAzure depolama kalıcı.</span><span class="sxs-lookup"><span data-stu-id="0fec9-256">All hello data is transferred toodisk and persisted tooAzure Storage.</span></span> <span data-ttu-id="0fec9-257">G/ç yoğun iş yükleri için yüksek g/ç oranı hello bu yöntemi sağlar.</span><span class="sxs-lookup"><span data-stu-id="0fec9-257">This method gives you hello highest I/O rate for I/O intensive workloads.</span></span> <span data-ttu-id="0fec9-258">Ayrıca dikkate tootake "Maliyet" gerekir.</span><span class="sxs-lookup"><span data-stu-id="0fec9-258">You also need tootake “transaction cost” into consideration.</span></span>

<span data-ttu-id="0fec9-259">**Öneriler**</span><span class="sxs-lookup"><span data-stu-id="0fec9-259">**Recommendations**</span></span>

<span data-ttu-id="0fec9-260">toomaximize hello verimlilik öneririz başlamanız **hiçbiri** ana bilgisayar önbelleğe almayı için.</span><span class="sxs-lookup"><span data-stu-id="0fec9-260">toomaximize hello throughput, we recommend that you  start with **None** for host caching.</span></span> <span data-ttu-id="0fec9-261">Premium Storage için hello hello dosya sistemiyle bağladığınızda, hello "engelleri" devre dışı bırakmalısınız olduğunu aklınızda bulundurun **ReadOnly** veya **hiçbiri** seçenekleri.</span><span class="sxs-lookup"><span data-stu-id="0fec9-261">For Premium Storage, keep in mind that you must disable hello "barriers" when you mount hello file system with hello **ReadOnly** or **None** options.</span></span> <span data-ttu-id="0fec9-262">Merhaba /etc/fstab dosyasını hello UUID toohello diskler ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="0fec9-262">Update hello /etc/fstab file with hello UUID toohello disks.</span></span>

<span data-ttu-id="0fec9-263">Daha fazla bilgi için bkz: [Linux VM'ler için Premium depolama](https://docs.microsoft.com/azure/storage/storage-premium-storage#premium-storage-for-linux-vms).</span><span class="sxs-lookup"><span data-stu-id="0fec9-263">For more information, see [Premium Storage for Linux VMs](https://docs.microsoft.com/azure/storage/storage-premium-storage#premium-storage-for-linux-vms).</span></span>

![Merhaba yönetilen disk sayfasının ekran görüntüsü](./media/oracle-design/premium_disk02.png)

- <span data-ttu-id="0fec9-265">Varsayılan işletim sistemi disklerinde kullanmak **okuma/yazma** önbelleğe alma.</span><span class="sxs-lookup"><span data-stu-id="0fec9-265">For OS disks, use default **Read/Write** caching.</span></span>
- <span data-ttu-id="0fec9-266">Sistem, TEMP ve geri alma için kullanmak **hiçbiri** önbelleğe alma için.</span><span class="sxs-lookup"><span data-stu-id="0fec9-266">For SYSTEM, TEMP, and UNDO use **None** for caching.</span></span>
- <span data-ttu-id="0fec9-267">VERİLERİN kullanmanız **hiçbiri** önbelleğe alma için.</span><span class="sxs-lookup"><span data-stu-id="0fec9-267">For DATA, use **None** for caching.</span></span> <span data-ttu-id="0fec9-268">Ancak, veritabanı salt okunur veya okuma açısından yoğun ise, **salt okunur** önbelleğe alma.</span><span class="sxs-lookup"><span data-stu-id="0fec9-268">But if your database is read-only or read-intensive, use **Read-only** caching.</span></span>

<span data-ttu-id="0fec9-269">Veri diski ayarınız kaydedildikten sonra hello işletim sistemi düzeyinde hello sürücü çıkarın ve hello değişiklik yaptıktan sonra yeniden sürece hello konağı önbellek ayarı değiştiremezsiniz.</span><span class="sxs-lookup"><span data-stu-id="0fec9-269">After your data disk setting is saved, you can't change hello host cache setting unless you unmount hello drive at hello OS level and then remount it after you've made hello change.</span></span>


## <a name="security"></a><span data-ttu-id="0fec9-270">Güvenlik</span><span class="sxs-lookup"><span data-stu-id="0fec9-270">Security</span></span>

<span data-ttu-id="0fec9-271">Ayarlama ve Azure ortamınıza yapılandırdıktan sonra hello sonraki toosecure adımdır ağınıza.</span><span class="sxs-lookup"><span data-stu-id="0fec9-271">After you have set up and configured your Azure environment, hello next step is toosecure your network.</span></span> <span data-ttu-id="0fec9-272">Bazı öneriler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="0fec9-272">Here are some recommendations:</span></span>

- <span data-ttu-id="0fec9-273">*NSG İlkesi*: NSG bir alt ağ veya NIC tarafından tanımlanabilir</span><span class="sxs-lookup"><span data-stu-id="0fec9-273">*NSG policy*: NSG can be defined by a subnet or NIC.</span></span> <span data-ttu-id="0fec9-274">Bu daha basit toocontrol erişim hello alt ağ düzeyinde hem de güvenlik ve uygulama güvenlik duvarları gibi şeyler için zorla yönlendirme olur.</span><span class="sxs-lookup"><span data-stu-id="0fec9-274">It's simpler toocontrol access at hello subnet level both for security and force routing for things like application firewalls.</span></span>

- <span data-ttu-id="0fec9-275">*Jumpbox*: daha güvenli erişim için Yöneticiler doğrudan toohello uygulama hizmeti veya veritabanı bağlanmayacak.</span><span class="sxs-lookup"><span data-stu-id="0fec9-275">*Jumpbox*: For more secure access, administrators should not directly connect toohello application service or database.</span></span> <span data-ttu-id="0fec9-276">Bir jumpbox hello yönetici makine ve Azure kaynakları arasında bir ortam olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="0fec9-276">A jumpbox is used as a media between hello administrator machine and Azure resources.</span></span>
<span data-ttu-id="0fec9-277">![Merhaba Jumpbox topoloji sayfasının ekran görüntüsü](./media/oracle-design/jumpbox.png)</span><span class="sxs-lookup"><span data-stu-id="0fec9-277">![Screenshot of hello Jumpbox topology page](./media/oracle-design/jumpbox.png)</span></span>

    <span data-ttu-id="0fec9-278">Hello Yöneticisi Makine IP kısıtlı erişim toohello yalnızca jumpbox sunmaktadır.</span><span class="sxs-lookup"><span data-stu-id="0fec9-278">hello administrator machine should offer IP-restricted access toohello jumpbox only.</span></span> <span data-ttu-id="0fec9-279">Merhaba jumpbox erişim toohello uygulama ve veritabanı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="0fec9-279">hello jumpbox should have access toohello application and database.</span></span>

- <span data-ttu-id="0fec9-280">*Özel ağ* (alt ağlar): daha iyi denetim NSG İlkesi tarafından ayarlanabilir böylece, hello uygulama hizmeti ve veritabanı farklı alt ağlarda sahip olmasını öneririz.</span><span class="sxs-lookup"><span data-stu-id="0fec9-280">*Private network* (subnets): We recommend that you have hello application service and database on separate subnets, so better control can be set by NSG policy.</span></span>


## <a name="additional-reading"></a><span data-ttu-id="0fec9-281">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="0fec9-281">Additional reading</span></span>

- [<span data-ttu-id="0fec9-282">Oracle ASM’yi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="0fec9-282">Configure Oracle ASM</span></span>](configure-oracle-asm.md)
- [<span data-ttu-id="0fec9-283">Oracle Data Guard yapılandırın</span><span class="sxs-lookup"><span data-stu-id="0fec9-283">Configure Oracle Data Guard</span></span>](configure-oracle-dataguard.md)
- [<span data-ttu-id="0fec9-284">Oracle Golden kapısı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="0fec9-284">Configure Oracle Golden Gate</span></span>](configure-oracle-golden-gate.md)
- [<span data-ttu-id="0fec9-285">Oracle yedekleme ve kurtarma</span><span class="sxs-lookup"><span data-stu-id="0fec9-285">Oracle backup and recovery</span></span>](oracle-backup-recovery.md)

## <a name="next-steps"></a><span data-ttu-id="0fec9-286">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="0fec9-286">Next steps</span></span>

- [<span data-ttu-id="0fec9-287">Öğretici: yüksek oranda kullanılabilir sanal makineleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="0fec9-287">Tutorial: Create highly available VMs</span></span>](../../linux/create-cli-complete.md)
- [<span data-ttu-id="0fec9-288">VM dağıtımı Azure CLI örnekleri keşfedin</span><span class="sxs-lookup"><span data-stu-id="0fec9-288">Explore VM deployment Azure CLI samples</span></span>](../../linux/cli-samples.md)
