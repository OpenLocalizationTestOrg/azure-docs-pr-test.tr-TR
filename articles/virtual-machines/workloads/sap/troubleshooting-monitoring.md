---
title: "aaaTroubleshooting ve izleme, SAP HANA azure'da (büyük örnekler) | Microsoft Docs"
description: "Sorun giderme ve Azure (büyük örnekler) üzerinde SAP HANA izleyin."
services: virtual-machines-linux
documentationcenter: 
author: RicksterCDN
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 12/01/2016
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 1f1cd35820e227fd99af495431cd4b826aa53600
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tootroubleshoot-and-monitor-sap-hana-large-instances-on-azure"></a><span data-ttu-id="a8e20-103">Nasıl tootroubleshoot ve İzleyici SAP HANA (büyük örnekler) Azure ile ilgili</span><span class="sxs-lookup"><span data-stu-id="a8e20-103">How tootroubleshoot and monitor SAP HANA (large instances) on Azure</span></span>


## <a name="monitoring-in-sap-hana-on-azure-large-instances"></a><span data-ttu-id="a8e20-104">SAP HANA (büyük örnekler) azure'da izleme</span><span class="sxs-lookup"><span data-stu-id="a8e20-104">Monitoring in SAP HANA on Azure (Large Instances)</span></span>

<span data-ttu-id="a8e20-105">SAP HANA Azure (büyük örnekler) üzerinde diğer bir Iaas dağıtımından farklı — hello uygulamasıdır yapmak ve bunları nasıl bu kaynakları aşağıdaki hello ve hangi işletim sistemi hello toomonitor gerekir:</span><span class="sxs-lookup"><span data-stu-id="a8e20-105">SAP HANA on Azure (Large Instances) is no different from any other IaaS deployment — you need toomonitor what hello OS and hello application is doing and how these consume hello following resources:</span></span>

- <span data-ttu-id="a8e20-106">CPU</span><span class="sxs-lookup"><span data-stu-id="a8e20-106">CPU</span></span>
- <span data-ttu-id="a8e20-107">Bellek</span><span class="sxs-lookup"><span data-stu-id="a8e20-107">Memory</span></span>
- <span data-ttu-id="a8e20-108">Ağ bant genişliği</span><span class="sxs-lookup"><span data-stu-id="a8e20-108">Network bandwidth</span></span>
- <span data-ttu-id="a8e20-109">Disk alanı</span><span class="sxs-lookup"><span data-stu-id="a8e20-109">Disk space</span></span>

<span data-ttu-id="a8e20-110">Azure sanal makinelerle yukarıda adı hello kaynak sınıfları yeterli olup veya olup bunlar tükendiğinde toofigure gerektiği.</span><span class="sxs-lookup"><span data-stu-id="a8e20-110">As with Azure Virtual Machines you need toofigure out whether hello resource classes named above are sufficient, or whether these get depleted.</span></span> <span data-ttu-id="a8e20-111">İşte daha fazla ayrıntı her hello farklı sınıflar:</span><span class="sxs-lookup"><span data-stu-id="a8e20-111">Here is more detail on each of hello different classes:</span></span>

<span data-ttu-id="a8e20-112">**CPU kaynak tüketimi:** SAP HANA karşı belirli iş yükü için tanımlanan hello orandır zorlanan toomake emin yeterli CPU kaynakları kullanılabilir toowork bellekte depolanır hello veriler aracılığıyla olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="a8e20-112">**CPU resource consumption:** hello ratio that SAP defined for certain workload against HANA is enforced toomake sure that there should be enough CPU resources available toowork through hello data that is stored in memory.</span></span> <span data-ttu-id="a8e20-113">Bununla birlikte, burada HANA toomissing dizinler veya benzer sorunlar nedeniyle sorgular yürütme CPU çok tüketen durumlar olabilir.</span><span class="sxs-lookup"><span data-stu-id="a8e20-113">Nevertheless, there might be cases where HANA consumes a lot of CPU executing queries due toomissing indexes or similar issues.</span></span> <span data-ttu-id="a8e20-114">Başka bir deyişle, CPU kaynak tüketimini hello belirli HANA Hizmetleri tarafından tüketilen CPU kaynaklarının yanı sıra hello HANA büyük örneği birim izlemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="a8e20-114">This means you should monitor CPU resource consumption of hello HANA large instance unit as well as CPU resources consumed by hello specific HANA services.</span></span>

<span data-ttu-id="a8e20-115">**Bellek tüketimi:** önemli toomonitor gelen HANA içinde yanı sıra HANA dışında hello birimi üzerinde değil.</span><span class="sxs-lookup"><span data-stu-id="a8e20-115">**Memory consumption:** Is important toomonitor from within HANA, as well as outside of HANA on hello unit.</span></span> <span data-ttu-id="a8e20-116">Merhaba verileri sipariş toostay SAP yönergelerini boyutlandırma gerekli hello içinde bellek tahsis HANA nasıl tüketme HANA içinde izleyin.</span><span class="sxs-lookup"><span data-stu-id="a8e20-116">Within HANA, monitor how hello data is consuming HANA allocated memory in order toostay within hello required sizing guidelines of SAP.</span></span> <span data-ttu-id="a8e20-117">Merhaba büyük örnek düzeyi toomake ek yüklü olmayan-HANA yazılım değil çok fazla bellek kullanmasına ve bu nedenle için bellek HANA ile rekabet emin üzerinde toomonitor bellek tüketimi da isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a8e20-117">You also want toomonitor memory consumption on hello Large Instance level toomake sure that additional installed non-HANA software does not consume too much memory, and therefore compete with HANA for memory.</span></span>

<span data-ttu-id="a8e20-118">**Ağ bant genişliği:** hello Azure sanal ağ geçidi sınırlı bant genişliği hello Azure VNet taşıma verilerin, yardımcı olması için tüm tarafından alınan toomonitor hello verileri Azure VM'ler hello Azure toohello sınırları ne kadar yakın olduğunuz çıkışı bir VNet toofigure içinde hello ağ geçidi SKU'su seçtiğiniz.</span><span class="sxs-lookup"><span data-stu-id="a8e20-118">**Network bandwidth:** hello Azure VNet gateway is limited in bandwidth of data moving into hello Azure VNet, so it is helpful toomonitor hello data received by all hello Azure VMs within a VNet toofigure out how close you are toohello limits of hello Azure gateway SKU you selected.</span></span> <span data-ttu-id="a8e20-119">Merhaba HANA büyük örneği biriminde algılama toomonitor gelen ve giden ağ trafiğini de ve zaman içinde işlenir hello birimleri tookeep izini yapar.</span><span class="sxs-lookup"><span data-stu-id="a8e20-119">On hello HANA Large Instance unit, it does make sense toomonitor incoming and outgoing network traffic as well, and tookeep track of hello volumes that are handled over time.</span></span>

<span data-ttu-id="a8e20-120">**Disk alanı:** Disk alanı tüketimini genellikle zamanla artar.</span><span class="sxs-lookup"><span data-stu-id="a8e20-120">**Disk space:** Disk space consumption usually increases over time.</span></span> <span data-ttu-id="a8e20-121">Bunun pek çok nedeni vardır, ancak tüm çoğu: veri birimi artırır, işlem günlüğü yedeklemeleri, izleme dosyaları depolamak ve depolama anlık görüntüleri gerçekleştirme yürütülmesini.</span><span class="sxs-lookup"><span data-stu-id="a8e20-121">There are many reasons for this, but most of all are: data volume increases, execution of transaction log backups, storing trace files, and performing storage snapshots.</span></span> <span data-ttu-id="a8e20-122">Bu nedenle, önemli toomonitor disk alanı kullanımı ve hello HANA büyük örneği birimiyle ilişkili hello disk alanını yönetme.</span><span class="sxs-lookup"><span data-stu-id="a8e20-122">Therefore, it is important toomonitor disk space usage and manage hello disk space associated with hello HANA Large Instance unit.</span></span>

## <a name="monitoring-and-troubleshooting-from-hana-side"></a><span data-ttu-id="a8e20-123">İzleme ve HANA taraftan sorun giderme</span><span class="sxs-lookup"><span data-stu-id="a8e20-123">Monitoring and troubleshooting from HANA side</span></span>

<span data-ttu-id="a8e20-124">Sipariş tooeffectively sorunları ilgili tooSAP (büyük örnekler) azure'da HANA çözümlemek, bir sorunun hello kök nedeni aşağı yararlı toonarrow.</span><span class="sxs-lookup"><span data-stu-id="a8e20-124">In order tooeffectively analyze problems related tooSAP HANA on Azure (Large Instances), it is useful toonarrow down hello root cause of a problem.</span></span> <span data-ttu-id="a8e20-125">SAP belgelerine toohelp büyük miktarda yayımlanan.</span><span class="sxs-lookup"><span data-stu-id="a8e20-125">SAP has published a large amount of documentation toohelp you.</span></span>

<span data-ttu-id="a8e20-126">İlgili sık sorulan sorular ilgili tooSAP HANA performans SAP notları aşağıdaki hello bulunabilir:</span><span class="sxs-lookup"><span data-stu-id="a8e20-126">Applicable FAQs related tooSAP HANA performance can be found in hello following SAP Notes:</span></span>

- [<span data-ttu-id="a8e20-127">SAP Not #2222200 – SSS: SAP HANA ağ</span><span class="sxs-lookup"><span data-stu-id="a8e20-127">SAP Note #2222200 – FAQ: SAP HANA Network</span></span>](https://launchpad.support.sap.com/#/notes/2222200)
- [<span data-ttu-id="a8e20-128">SAP Not #2100040 – SSS: SAP HANA CPU</span><span class="sxs-lookup"><span data-stu-id="a8e20-128">SAP Note #2100040 – FAQ: SAP HANA CPU</span></span>](https://launchpad.support.sap.com/#/notes/0002100040)
- [<span data-ttu-id="a8e20-129">SAP Not #199997 – SSS: SAP HANA bellek</span><span class="sxs-lookup"><span data-stu-id="a8e20-129">SAP Note #199997 – FAQ: SAP HANA Memory</span></span>](https://launchpad.support.sap.com/#/notes/2177064)
- [<span data-ttu-id="a8e20-130">SAP Not #200000 – SSS: SAP HANA performansı iyileştirme</span><span class="sxs-lookup"><span data-stu-id="a8e20-130">SAP Note #200000 – FAQ: SAP HANA Performance Optimization</span></span>](https://launchpad.support.sap.com/#/notes/2000000)
- [<span data-ttu-id="a8e20-131">SAP Not #199930 – SSS: SAP HANA g/ç çözümleme</span><span class="sxs-lookup"><span data-stu-id="a8e20-131">SAP Note #199930 – FAQ: SAP HANA I/O Analysis</span></span>](https://launchpad.support.sap.com/#/notes/1999930)
- [<span data-ttu-id="a8e20-132">SAP Not #2177064 – SSS: SAP HANA hizmeti yeniden başlatın ve kilitleniyor</span><span class="sxs-lookup"><span data-stu-id="a8e20-132">SAP Note #2177064 – FAQ: SAP HANA Service Restart and Crashes</span></span>](https://launchpad.support.sap.com/#/notes/2177064)

<span data-ttu-id="a8e20-133">**SAP HANA uyarıları**</span><span class="sxs-lookup"><span data-stu-id="a8e20-133">**SAP HANA Alerts**</span></span>

<span data-ttu-id="a8e20-134">İlk adım olarak, hello geçerli SAP HANA uyarı günlüklerini denetleyin.</span><span class="sxs-lookup"><span data-stu-id="a8e20-134">As a first step, check hello current SAP HANA alert logs.</span></span> <span data-ttu-id="a8e20-135">SAP HANA Studio'da çok gidin**Yönetim Konsolu: Uyarı: göster: tüm uyarıları**.</span><span class="sxs-lookup"><span data-stu-id="a8e20-135">In SAP HANA Studio, go too**Administration Console: Alerts: Show: all alerts**.</span></span> <span data-ttu-id="a8e20-136">Bu sekme hello en az ve en fazla eşikleri dışında kalan belirli değerleri (boş fiziksel bellek, CPU kullanımı, vb.) için tüm SAP HANA uyarıları gösterir.</span><span class="sxs-lookup"><span data-stu-id="a8e20-136">This tab will show all SAP HANA alerts for specific values (free physical memory, CPU utilization, etc.) that fall outside of hello set minimum and maximum thresholds.</span></span> <span data-ttu-id="a8e20-137">Varsayılan olarak, denetimleri 15 dakikada bir otomatik olarak yenilenir.</span><span class="sxs-lookup"><span data-stu-id="a8e20-137">By default, checks are auto-refreshed every 15 minutes.</span></span>

![SAP HANA Studio'da tooAdministration konsol gidin: Uyarı: göster: tüm uyarılar](./media/troubleshooting-monitoring/image1-show-alerts.png)

<span data-ttu-id="a8e20-139">**CPU**</span><span class="sxs-lookup"><span data-stu-id="a8e20-139">**CPU**</span></span>

<span data-ttu-id="a8e20-140">Tooimproper eşik ayarı nedeniyle tetiklenen bir uyarı için bir çözüm tooreset toohello varsayılan veya daha uygun bir eşik değere değerdir.</span><span class="sxs-lookup"><span data-stu-id="a8e20-140">For an alert triggered due tooimproper threshold setting, a resolution is tooreset toohello default value or a more reasonable threshold value.</span></span>

![Sıfırlama toohello varsayılan değeri ya da daha uygun bir eşik değer](./media/troubleshooting-monitoring/image2-cpu-utilization.png)

<span data-ttu-id="a8e20-142">Uyarıları aşağıdaki hello CPU kaynağı sorunlarını gösterebilir:</span><span class="sxs-lookup"><span data-stu-id="a8e20-142">hello following alerts may indicate CPU resource problems:</span></span>

- <span data-ttu-id="a8e20-143">Ana bilgisayar CPU kullanımı (uyarı 5)</span><span class="sxs-lookup"><span data-stu-id="a8e20-143">Host CPU Usage (Alert 5)</span></span>
- <span data-ttu-id="a8e20-144">En son noktası işlemi (uyarı 28)</span><span class="sxs-lookup"><span data-stu-id="a8e20-144">Most recent savepoint operation (Alert 28)</span></span>
- <span data-ttu-id="a8e20-145">Kayıt noktası süresi (uyarı 54)</span><span class="sxs-lookup"><span data-stu-id="a8e20-145">Savepoint duration (Alert 54)</span></span>

<span data-ttu-id="a8e20-146">SAP HANA veritabanından hello aşağıdakilerden birini üzerinde yüksek CPU tüketimi karşılaşabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="a8e20-146">You may notice high CPU consumption on your SAP HANA database from one of hello following:</span></span>

- <span data-ttu-id="a8e20-147">Uyarı 5 (ana bilgisayar CPU kullanımı) için geçerli veya son CPU kullanımını tetiklenir</span><span class="sxs-lookup"><span data-stu-id="a8e20-147">Alert 5 (Host CPU usage) is raised for current or past CPU usage</span></span>
- <span data-ttu-id="a8e20-148">Merhaba CPU kullanımı hello genel bakış ekranda görüntülenen</span><span class="sxs-lookup"><span data-stu-id="a8e20-148">hello displayed CPU usage on hello overview screen</span></span>

![CPU kullanımı hello genel bakış ekranda görüntülenen](./media/troubleshooting-monitoring/image3-cpu-usage.png)

<span data-ttu-id="a8e20-150">Merhaba yük grafiği yüksek CPU tüketimi veya yüksek tüketim hello geçmiş gösterebilir:</span><span class="sxs-lookup"><span data-stu-id="a8e20-150">hello Load graph might show high CPU consumption, or high consumption in hello past:</span></span>

![Hello yük grafik yüksek CPU tüketimi veya yüksek tüketim hello geçmiş gösterebilir.](./media/troubleshooting-monitoring/image4-load-graph.png)

<span data-ttu-id="a8e20-152">Toohigh CPU kullanımı tetiklenen uyarı, ancak bunlarla sınırlı olmamak de dahil olmak üzere çeşitli nedenlerden kaynaklanabilir: belirli işlemleri, veri yükleme, asılı SQL deyimlerini ve hatalı sorgu performansı (örneğin, ile HANA üzerinde BW uzun süre çalışan işlerin yürütme küpleri).</span><span class="sxs-lookup"><span data-stu-id="a8e20-152">An alert triggered due toohigh CPU utilization could be caused by several reasons, including, but not limited to: execution of certain transactions, data loading, hanging of jobs, long running SQL statements, and bad query performance (for example, with BW on HANA cubes).</span></span>

<span data-ttu-id="a8e20-153">Toohello başvuran [SAP HANA sorunlarını giderme: CPU ilgili neden olur ve çözümleri](http://help.sap.com/saphelp_hanaplatform/helpdata/en/4f/bc915462db406aa2fe92b708b95189/content.htm?frameset=/en/db/6ca50424714af8b370960c04ce667b/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=46&amp;show_children=false) ayrıntılı sorun giderme adımları için site.</span><span class="sxs-lookup"><span data-stu-id="a8e20-153">Refer toohello [SAP HANA Troubleshooting: CPU Related Causes and Solutions](http://help.sap.com/saphelp_hanaplatform/helpdata/en/4f/bc915462db406aa2fe92b708b95189/content.htm?frameset=/en/db/6ca50424714af8b370960c04ce667b/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=46&amp;show_children=false) site for detailed troubleshooting steps.</span></span>

<span data-ttu-id="a8e20-154">**İşletim Sistemi**</span><span class="sxs-lookup"><span data-stu-id="a8e20-154">**Operating System**</span></span>

<span data-ttu-id="a8e20-155">SAP HANA Linux'ta toomake saydam büyük sayfalar devre dışı bırakıldığından emin için en önemli hello birini denetimlerinin bkz [SAP Not #2131662 – saydam büyük sayfalar (THP) SAP HANA sunucularda](https://launchpad.support.sap.com/#/notes/2131662).</span><span class="sxs-lookup"><span data-stu-id="a8e20-155">One of hello most important checks for SAP HANA on Linux is toomake sure that Transparent Huge Pages are disabled, see [SAP Note #2131662 – Transparent Huge Pages (THP) on SAP HANA Servers](https://launchpad.support.sap.com/#/notes/2131662).</span></span>

- <span data-ttu-id="a8e20-156">Saydam büyük sayfalar Linux komutu aşağıdaki hello etkin olup olmadığını denetleyebilirsiniz: **kat /sys/kernel/mm/transparent\_hugepage ve etkin**</span><span class="sxs-lookup"><span data-stu-id="a8e20-156">You can check if Transparent Huge Pages are enabled through hello following Linux command: **cat /sys/kernel/mm/transparent\_hugepage/enabled**</span></span>
- <span data-ttu-id="a8e20-157">Varsa _her zaman_ içine aşağıdaki şekilde köşeli parantez içine hello saydam büyük sayfalar etkinleştirildiğini gösterir: [her zaman] madvise hiçbir zaman if _hiçbir zaman_ arasına köşeli aşağıdaki şekilde, onu o hello saydam anlamına gelir Büyük sayfalar devre dışı bırakılır: her zaman madvise [hiçbir zaman]</span><span class="sxs-lookup"><span data-stu-id="a8e20-157">If _always_ is enclosed in brackets as below, it means that hello Transparent Huge Pages are enabled: [always] madvise never; if _never_ is enclosed in brackets as below, it means that hello Transparent Huge Pages are disabled: always madvise [never]</span></span>

<span data-ttu-id="a8e20-158">Linux komutu aşağıdaki hello hiçbir şey döndürmelidir: **rpm - qa | grep ulimit.**</span><span class="sxs-lookup"><span data-stu-id="a8e20-158">hello following Linux command should return nothing: **rpm -qa | grep ulimit.**</span></span> <span data-ttu-id="a8e20-159">Görünürse _ulimit_ olan yüklü, bunu hemen kaldırın.</span><span class="sxs-lookup"><span data-stu-id="a8e20-159">If it appears _ulimit_ is installed, uninstall it immediately.</span></span>

<span data-ttu-id="a8e20-160">**Bellek**</span><span class="sxs-lookup"><span data-stu-id="a8e20-160">**Memory**</span></span>

<span data-ttu-id="a8e20-161">Bu hello tutar gözlemleyebilirsiniz SAP HANA hello tarafından ayrılan belleğin veritabanı beklenenden daha yüksektir.</span><span class="sxs-lookup"><span data-stu-id="a8e20-161">You may observe that hello amount of memory allocated by hello SAP HANA database is higher than expected.</span></span> <span data-ttu-id="a8e20-162">Uyarıları aşağıdaki hello yüksek bellek kullanımı ile ilgili sorunları belirtin:</span><span class="sxs-lookup"><span data-stu-id="a8e20-162">hello following alerts indicate issues with high memory usage:</span></span>

- <span data-ttu-id="a8e20-163">Konak fiziksel bellek kullanımı (uyarı 1)</span><span class="sxs-lookup"><span data-stu-id="a8e20-163">Host physical memory usage (Alert 1)</span></span>
- <span data-ttu-id="a8e20-164">Ad sunucusu (uyarı 12) bellek kullanımı</span><span class="sxs-lookup"><span data-stu-id="a8e20-164">Memory usage of name server (Alert 12)</span></span>
- <span data-ttu-id="a8e20-165">Sütun deposu tabloları (uyarı 40) toplam bellek kullanımı</span><span class="sxs-lookup"><span data-stu-id="a8e20-165">Total memory usage of Column Store tables (Alert 40)</span></span>
- <span data-ttu-id="a8e20-166">Bellek kullanımı (uyarı 43) hizmetleri hakkında</span><span class="sxs-lookup"><span data-stu-id="a8e20-166">Memory usage of services (Alert 43)</span></span>
- <span data-ttu-id="a8e20-167">Sütun deposu tabloların (uyarı 45) ana depolama bellek kullanımı</span><span class="sxs-lookup"><span data-stu-id="a8e20-167">Memory usage of main storage of Column Store tables (Alert 45)</span></span>
- <span data-ttu-id="a8e20-168">Çalışma zamanı döküm dosyalarını (uyarı 46)</span><span class="sxs-lookup"><span data-stu-id="a8e20-168">Runtime dump files (Alert 46)</span></span>

<span data-ttu-id="a8e20-169">Toohello başvuran [SAP HANA sorunlarını giderme: bellek sorunları](http://help.sap.com/saphelp_hanaplatform/helpdata/en/db/6ca50424714af8b370960c04ce667b/content.htm?frameset=/en/59/5eaa513dde43758b51378ab3315ebb/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=26&amp;show_children=false) ayrıntılı sorun giderme adımları için site.</span><span class="sxs-lookup"><span data-stu-id="a8e20-169">Refer toohello [SAP HANA Troubleshooting: Memory Problems](http://help.sap.com/saphelp_hanaplatform/helpdata/en/db/6ca50424714af8b370960c04ce667b/content.htm?frameset=/en/59/5eaa513dde43758b51378ab3315ebb/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=26&amp;show_children=false) site for detailed troubleshooting steps.</span></span>

<span data-ttu-id="a8e20-170">**Ağ**</span><span class="sxs-lookup"><span data-stu-id="a8e20-170">**Network**</span></span>

<span data-ttu-id="a8e20-171">Çok başvuran[SAP Not #2081065 – SAP HANA ağ sorunlarını giderme](https://launchpad.support.sap.com/#/notes/2081065) ve sorun giderme adımları bu SAP notta hello ağ gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="a8e20-171">Refer too[SAP Note #2081065 – Troubleshooting SAP HANA Network](https://launchpad.support.sap.com/#/notes/2081065) and perform hello network troubleshooting steps in this SAP Note.</span></span>

1. <span data-ttu-id="a8e20-172">İstemci ve sunucu arasındaki gidiş dönüş süresi çözümleniyor.</span><span class="sxs-lookup"><span data-stu-id="a8e20-172">Analyzing round-trip time between server and client.</span></span>
  <span data-ttu-id="a8e20-173">A.</span><span class="sxs-lookup"><span data-stu-id="a8e20-173">A.</span></span> <span data-ttu-id="a8e20-174">Merhaba SQL betiği çalıştırma [ _HANA\_ağ\_istemcileri_](https://launchpad.support.sap.com/#/notes/1969700)_._</span><span class="sxs-lookup"><span data-stu-id="a8e20-174">Run hello SQL script [_HANA\_Network\_Clients_](https://launchpad.support.sap.com/#/notes/1969700)_._</span></span>
  
2. <span data-ttu-id="a8e20-175">Düğümler arası iletişim analiz edin.</span><span class="sxs-lookup"><span data-stu-id="a8e20-175">Analyze internode communication.</span></span>
  <span data-ttu-id="a8e20-176">A.</span><span class="sxs-lookup"><span data-stu-id="a8e20-176">A.</span></span> <span data-ttu-id="a8e20-177">SQL betiği çalıştırma [ _HANA\_ağ\_Hizmetleri_](https://launchpad.support.sap.com/#/notes/1969700)_._</span><span class="sxs-lookup"><span data-stu-id="a8e20-177">Run SQL script [_HANA\_Network\_Services_](https://launchpad.support.sap.com/#/notes/1969700)_._</span></span>

3. <span data-ttu-id="a8e20-178">Linux komutu çalıştırmak **ifconfig** (Merhaba çıkış paket kayıpları yaşanan gösterir).</span><span class="sxs-lookup"><span data-stu-id="a8e20-178">Run Linux command **ifconfig** (hello output shows if any packet losses are occurring).</span></span>
4. <span data-ttu-id="a8e20-179">Linux komutu çalıştırmak **tcpdump**.</span><span class="sxs-lookup"><span data-stu-id="a8e20-179">Run Linux command **tcpdump**.</span></span>

<span data-ttu-id="a8e20-180">Ayrıca, hello açık kaynak kullanın [IPERF](https://iperf.fr/) Aracı (veya benzeri) toomeasure gerçek uygulama ağ performansı.</span><span class="sxs-lookup"><span data-stu-id="a8e20-180">Also, use hello open source [IPERF](https://iperf.fr/) tool (or similar) toomeasure real application network performance.</span></span>

<span data-ttu-id="a8e20-181">Toohello başvuran [SAP HANA sorunlarını giderme: ağ performansı ve bağlantı sorunları](http://help.sap.com/saphelp_hanaplatform/helpdata/en/a3/ccdff1aedc4720acb24ed8826938b6/content.htm?frameset=/en/dc/6ff98fa36541e997e4c719a632cbd8/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=142&amp;show_children=false) ayrıntılı sorun giderme adımları için site.</span><span class="sxs-lookup"><span data-stu-id="a8e20-181">Refer toohello [SAP HANA Troubleshooting: Networking Performance and Connectivity Problems](http://help.sap.com/saphelp_hanaplatform/helpdata/en/a3/ccdff1aedc4720acb24ed8826938b6/content.htm?frameset=/en/dc/6ff98fa36541e997e4c719a632cbd8/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=142&amp;show_children=false) site for detailed troubleshooting steps.</span></span>

<span data-ttu-id="a8e20-182">**Depolama**</span><span class="sxs-lookup"><span data-stu-id="a8e20-182">**Storage**</span></span>

<span data-ttu-id="a8e20-183">Bir son kullanıcı açısından bir uygulama (veya bir bütün olarak hello sistemi) ağır şekilde çalışan, yanıt vermiyor veya g/ç performansı ile ilgili sorun varsa toohang bile görünebilir.</span><span class="sxs-lookup"><span data-stu-id="a8e20-183">From an end-user perspective, an application (or hello system as a whole) runs sluggishly, is unresponsive, or can even seem toohang if there are issues with I/O performance.</span></span> <span data-ttu-id="a8e20-184">Merhaba, **birimleri** sekmesini SAP HANA Studio'da hello bağlı birimler ve hangi birimlerin her hizmeti tarafından kullanılan görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a8e20-184">In hello **Volumes** tab in SAP HANA Studio, you can see hello attached volumes, and what volumes are used by each service.</span></span>

![SAP HANA Studio'da Hello birimler sekmesinde birimleri ve hangi birimlerin her hizmeti tarafından kullanılan hello bağlı görebilirsiniz](./media/troubleshooting-monitoring/image5-volumes-tab-a.png)

<span data-ttu-id="a8e20-186">Merhaba alt bölümünde ayrıntılarını görebilirsiniz hello ekranın bağlı birimlerin birimler, dosyalar ve g/ç istatistikleri gibi hello.</span><span class="sxs-lookup"><span data-stu-id="a8e20-186">Attached volumes in hello lower part of hello screen you can see details of hello volumes, such as files and I/O statistics.</span></span>

![Birimler, dosyalar ve g/ç istatistikleri gibi ayrıntılarını görebilirsiniz hello ekranın hello alt bölümünde bağlı birimlerin hello](./media/troubleshooting-monitoring/image6-volumes-tab-b.png)

<span data-ttu-id="a8e20-188">Toohello başvuran [SAP HANA sorunlarını giderme: g/ç ana ilgili nedenler ve çözümler](http://help.sap.com/saphelp_hanaplatform/helpdata/en/dc/6ff98fa36541e997e4c719a632cbd8/content.htm?frameset=/en/47/4cb08a715c42fe9f7cc5efdc599959/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=55&amp;show_children=false) ve [SAP HANA sorunlarını giderme: Disk ana ilgili nedenler ve çözümler](http://help.sap.com/saphelp_hanaplatform/helpdata/en/47/4cb08a715c42fe9f7cc5efdc599959/content.htm?frameset=/en/44/3e1db4f73d42da859008df4f69e37a/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=53&amp;show_children=false) ayrıntılı sorun giderme adımları için site.</span><span class="sxs-lookup"><span data-stu-id="a8e20-188">Refer toohello [SAP HANA Troubleshooting: I/O Related Root Causes and Solutions](http://help.sap.com/saphelp_hanaplatform/helpdata/en/dc/6ff98fa36541e997e4c719a632cbd8/content.htm?frameset=/en/47/4cb08a715c42fe9f7cc5efdc599959/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=55&amp;show_children=false) and [SAP HANA Troubleshooting: Disk Related Root Causes and Solutions](http://help.sap.com/saphelp_hanaplatform/helpdata/en/47/4cb08a715c42fe9f7cc5efdc599959/content.htm?frameset=/en/44/3e1db4f73d42da859008df4f69e37a/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=53&amp;show_children=false) site for detailed troubleshooting steps.</span></span>

<span data-ttu-id="a8e20-189">**Tanılama araçları**</span><span class="sxs-lookup"><span data-stu-id="a8e20-189">**Diagnostic Tools**</span></span>

<span data-ttu-id="a8e20-190">SAP HANA sistem durumu denetimi HANA aracılığıyla gerçekleştirmek\_yapılandırma\_Minichecks.</span><span class="sxs-lookup"><span data-stu-id="a8e20-190">Perform an SAP HANA Health Check through HANA\_Configuration\_Minichecks.</span></span> <span data-ttu-id="a8e20-191">Bu aracı zaten uyarıları SAP HANA Studio'da olarak oluşturuldu kritik olabilecek teknik sorunlar döndürür.</span><span class="sxs-lookup"><span data-stu-id="a8e20-191">This tool returns potentially critical technical issues that should have already been raised as alerts in SAP HANA Studio.</span></span>

<span data-ttu-id="a8e20-192">Çok başvuran[SAP Not #1969700 – SAP HANA için SQL deyimi koleksiyonu](https://launchpad.support.sap.com/#/notes/1969700) ve hello SQL Statements.zip dosya ekli toothat Not indirin.</span><span class="sxs-lookup"><span data-stu-id="a8e20-192">Refer too[SAP Note #1969700 – SQL statement collection for SAP HANA](https://launchpad.support.sap.com/#/notes/1969700) and download hello SQL Statements.zip file attached toothat note.</span></span> <span data-ttu-id="a8e20-193">Bu .zip dosyasını hello yerel sabit sürücüde depolayın.</span><span class="sxs-lookup"><span data-stu-id="a8e20-193">Store this .zip file on hello local hard drive.</span></span>

<span data-ttu-id="a8e20-194">SAP HANA Studio'da hello **sistem bilgileri** sekmesinde, hello sağ **adı** sütun ve seçin **içeri aktarma SQL deyimlerini**.</span><span class="sxs-lookup"><span data-stu-id="a8e20-194">In SAP HANA Studio, on hello **System Information** tab, right-click in hello **Name** column and select **Import SQL Statements**.</span></span>

![SAP HANA Studio'da hello sistem bilgisi sekmesindeki hello Ad sütununda sağ tıklatın ve içeri aktarma SQL deyimlerini seçin](./media/troubleshooting-monitoring/image7-import-statements-a.png)

<span data-ttu-id="a8e20-196">Select hello SQL Statements.zip dosyası yerel olarak depolanan ve hello karşılık gelen SQL deyimlerini sahip bir klasör için içeri aktarılacak.</span><span class="sxs-lookup"><span data-stu-id="a8e20-196">Select hello SQL Statements.zip file stored locally, and a folder with hello corresponding SQL statements will be imported.</span></span> <span data-ttu-id="a8e20-197">Bu noktada, bu SQL deyimleri ile birçok farklı tanılama denetimleri çalıştırılabilir hello.</span><span class="sxs-lookup"><span data-stu-id="a8e20-197">At this point, hello many different diagnostic checks can be run with these SQL statements.</span></span>

<span data-ttu-id="a8e20-198">Örneğin, tootest SAP HANA sistem çoğaltma bant genişliği gereksinimlerini sağ hello **bant genişliği** deyiminin altında **çoğaltma: bant genişliği** seçip **açık** SQL konsolunda.</span><span class="sxs-lookup"><span data-stu-id="a8e20-198">For example, tootest SAP HANA System Replication bandwidth requirements, right-click hello **Bandwidth** statement under **Replication: Bandwidth** and select **Open** in SQL Console.</span></span>

<span data-ttu-id="a8e20-199">Merhaba tam SQL deyimini değişti ve daha sonra çalıştırılabilir izin giriş parametreleri (değişikliği bölümüne) toobe açar.</span><span class="sxs-lookup"><span data-stu-id="a8e20-199">hello complete SQL statement opens allowing input parameters (modification section) toobe changed and then executed.</span></span>

![Merhaba tam SQL deyimini değişti ve daha sonra çalıştırılabilir izin giriş parametreleri (değişikliği bölümüne) toobe açar](./media/troubleshooting-monitoring/image8-import-statements-b.png)

<span data-ttu-id="a8e20-201">Başka bir örnek hello deyimleri altında üzerinde sağ **çoğaltma: genel bakış**.</span><span class="sxs-lookup"><span data-stu-id="a8e20-201">Another example is right-clicking on hello statements under **Replication: Overview**.</span></span> <span data-ttu-id="a8e20-202">Seçin **yürütme** hello bağlam menüsünden:</span><span class="sxs-lookup"><span data-stu-id="a8e20-202">Select **Execute** from hello context menu:</span></span>

![Başka bir çoğaltma altında hello deyimleri üzerinde sağ örnektir: genel bakış.](./media/troubleshooting-monitoring/image9-import-statements-c.png)

<span data-ttu-id="a8e20-205">Bu sorun giderme konusunda yardımcı olacak bilgileri sonuçlanır:</span><span class="sxs-lookup"><span data-stu-id="a8e20-205">This results in information that helps with troubleshooting:</span></span>

![Bu sorun giderme konusunda yardımcı olacak bilgiler sonuçlanır](./media/troubleshooting-monitoring/image10-import-statements-d.png)

<span data-ttu-id="a8e20-207">Aynı HANA için hello\_yapılandırma\_Minichecks ve onay herhangi _X_ hello işaretleri _C_ (kritik) sütun.</span><span class="sxs-lookup"><span data-stu-id="a8e20-207">Do hello same for HANA\_Configuration\_Minichecks and check for any _X_ marks in hello _C_ (Critical) column.</span></span>

<span data-ttu-id="a8e20-208">Örnek çıktı:</span><span class="sxs-lookup"><span data-stu-id="a8e20-208">Sample outputs:</span></span>

<span data-ttu-id="a8e20-209">**HANA\_yapılandırma\_MiniChecks\_Rev102.01 + 1** genel SAP HANA denetimleri için.</span><span class="sxs-lookup"><span data-stu-id="a8e20-209">**HANA\_Configuration\_MiniChecks\_Rev102.01+1** for general SAP HANA checks.</span></span>

![HANA\_yapılandırma\_MiniChecks\_Rev102.01 + 1 genel SAP HANA denetimleri için](./media/troubleshooting-monitoring/image11-configuration-minichecks.png)

<span data-ttu-id="a8e20-211">**HANA\_Hizmetleri\_genel bakış** ne SAP HANA Hizmetleri şu anda çalışan bir genel bakış için.</span><span class="sxs-lookup"><span data-stu-id="a8e20-211">**HANA\_Services\_Overview** for an overview of what SAP HANA services are currently running.</span></span>

![HANA\_Hizmetleri\_ne SAP HANA Hizmetleri şu anda çalışan bir genel bakış için genel bakış](./media/troubleshooting-monitoring/image12-services-overview.png)

<span data-ttu-id="a8e20-213">**HANA\_Hizmetleri\_istatistikleri** SAP HANA için hizmet bilgileri (CPU, bellek, vs.).</span><span class="sxs-lookup"><span data-stu-id="a8e20-213">**HANA\_Services\_Statistics** for SAP HANA service information (CPU, memory, etc.).</span></span>

![<span data-ttu-id="a8e20-214">HANA\_Hizmetleri\_istatistikleri SAP HANA için hizmet bilgileri</span><span class="sxs-lookup"><span data-stu-id="a8e20-214">HANA\_Services\_Statistics for SAP HANA service information</span></span> ](./media/troubleshooting-monitoring/image13-services-statistics.png)

<span data-ttu-id="a8e20-215">**HANA\_yapılandırma\_genel bakış\_Rev110 +** hello SAP HANA örneği hakkında genel bilgi için.</span><span class="sxs-lookup"><span data-stu-id="a8e20-215">**HANA\_Configuration\_Overview\_Rev110+** for general information on hello SAP HANA instance.</span></span>

![HANA\_yapılandırma\_genel bakış\_Rev110 + hello SAP HANA örneği hakkında genel bilgi için](./media/troubleshooting-monitoring/image14-configuration-overview.png)

<span data-ttu-id="a8e20-217">**HANA\_yapılandırma\_parametreleri\_Rev70 +** toocheck SAP HANA parametreleri.</span><span class="sxs-lookup"><span data-stu-id="a8e20-217">**HANA\_Configuration\_Parameters\_Rev70+** toocheck SAP HANA parameters.</span></span>

![HANA\_yapılandırma\_parametreleri\_Rev70 + toocheck SAP HANA parametreleri](./media/troubleshooting-monitoring/image15-configuration-parameters.png)

