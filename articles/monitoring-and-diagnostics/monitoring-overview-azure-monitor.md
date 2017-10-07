---
title: "aaaAzure İzleyiciye Genel Bakış | Microsoft Docs"
description: "Azure İzleyici uyarıları, Web kancalarını, otomatik ölçeklendirme ve Otomasyon kullanımda istatistikleri toplar. Makale ayrıca diğer Microsoft izleme seçenekleri listeleyin."
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/12/2017
ms.author: robb
ms.openlocfilehash: ffa304e7b158f0fceb7f60ab88fab291976aa0e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-azure-monitor"></a><span data-ttu-id="79a7e-104">Azure İzleyicisi'ne genel bakış</span><span class="sxs-lookup"><span data-stu-id="79a7e-104">Overview of Azure Monitor</span></span>
<span data-ttu-id="79a7e-105">Bu makalede hello Azure Monitor Hizmeti Microsoft Azure genel bir bakış sağlar.</span><span class="sxs-lookup"><span data-stu-id="79a7e-105">This article provides an overview of hello Azure Monitor service in Microsoft Azure.</span></span> <span data-ttu-id="79a7e-106">Hangi Azure İzleyici yapar ve işaretçileri tooadditional ilgili bilgiler verilmektedir anlatılmaktadır toouse Azure İzleyicisi.</span><span class="sxs-lookup"><span data-stu-id="79a7e-106">It discusses what Azure Monitor does and provides pointers tooadditional information on how toouse Azure Monitor.</span></span>  <span data-ttu-id="79a7e-107">Bir tanıtım tercih ederseniz, bu makalenin hello altındaki sonraki adımları bağlantılara bakın.</span><span class="sxs-lookup"><span data-stu-id="79a7e-107">If you prefer a video introduction, see Next steps links at hello bottom of this article.</span></span> 

## <a name="why-monitor-your-application-or-system"></a><span data-ttu-id="79a7e-108">Neden uygulama veya sistem izleme</span><span class="sxs-lookup"><span data-stu-id="79a7e-108">Why monitor your application or system</span></span>
<span data-ttu-id="79a7e-109">Bulut uygulamalarını birçok taşıma bölümleriyle karmaşıktır.</span><span class="sxs-lookup"><span data-stu-id="79a7e-109">Cloud applications are complex with many moving parts.</span></span> <span data-ttu-id="79a7e-110">İzleme, uygulamanızı kurma kalır veri tooensure ve sistem durumu iyi çalışan sağlar.</span><span class="sxs-lookup"><span data-stu-id="79a7e-110">Monitoring provides data tooensure that your application stays up and running in a healthy state.</span></span> <span data-ttu-id="79a7e-111">Olası sorunlar kapalı veya olanları sorun giderme, toostave yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="79a7e-111">It also helps you toostave off potential problems or troubleshoot past ones.</span></span> <span data-ttu-id="79a7e-112">Ayrıca, uygulamanız hakkında izleme verileri toogain ayrıntılı Öngörüler kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="79a7e-112">In addition, you can use monitoring data toogain deep insights about your application.</span></span> <span data-ttu-id="79a7e-113">Bu bilgi tooimprove uygulama performansı veya bakım yardımcı veya aksi halde el ile müdahale gerektiren Eylemler otomatik hale getirme.</span><span class="sxs-lookup"><span data-stu-id="79a7e-113">That knowledge can help you tooimprove application performance or maintainability, or automate actions that would otherwise require manual intervention.</span></span>


## <a name="azure-monitor-and-microsofts-other-monitoring-products"></a><span data-ttu-id="79a7e-114">Azure İzleyicisi'ni ve Microsoft kullanıcının diğer izleme ürünleri</span><span class="sxs-lookup"><span data-stu-id="79a7e-114">Azure Monitor and Microsoft's other monitoring products</span></span>
<span data-ttu-id="79a7e-115">Azure İzleyicisi, çoğu Microsoft Azure hizmetlerini taban düzeyi altyapı ölçümleri ve günlükleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="79a7e-115">Azure Monitor provides base level infrastructure metrics and logs for most services in Microsoft Azure.</span></span> <span data-ttu-id="79a7e-116">Henüz verilerini Azure izleyicisine koymayın azure Hizmetleri var. Bunun yerine gelecekteki hello koyacaktır.</span><span class="sxs-lookup"><span data-stu-id="79a7e-116">Azure services that do not yet put their data into Azure Monitor will put it there in hello future.</span></span>

<span data-ttu-id="79a7e-117">Microsoft, geliştiriciler, DevOps veya şirket içi yüklemeleri de BT Ops için ek izleme olanakları sağlayan ek ürün ve hizmetlerin birlikte gönderilir.</span><span class="sxs-lookup"><span data-stu-id="79a7e-117">Microsoft ships additional products and services that provide additional monitoring capabilities for developers, DevOps, or IT Ops that also have on-premises installations.</span></span> <span data-ttu-id="79a7e-118">Bir genel bakış ve bu farklı ürün ve hizmetlerin birlikte nasıl çalıştığını anlamak için bkz: [Microsoft Azure'da izleme](monitoring-overview.md).</span><span class="sxs-lookup"><span data-stu-id="79a7e-118">For an overview and understanding of how these different products and services work together, see [Monitoring in Microsoft Azure](monitoring-overview.md).</span></span>

## <a name="monitoring-sources---compute"></a><span data-ttu-id="79a7e-119">İşlem kaynakları - izleme</span><span class="sxs-lookup"><span data-stu-id="79a7e-119">Monitoring Sources - Compute</span></span>

![İzleme ve tanılama işlem dışı kaynakları modeli](./media/monitoring-overview-azure-monitor/Monitoring_Azure_Resources-compute_v6.png)

<span data-ttu-id="79a7e-121">Merhaba işlem hizmetleri içerir</span><span class="sxs-lookup"><span data-stu-id="79a7e-121">hello Compute services include</span></span> 
- <span data-ttu-id="79a7e-122">Cloud Services</span><span class="sxs-lookup"><span data-stu-id="79a7e-122">Cloud Services</span></span> 
- <span data-ttu-id="79a7e-123">Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="79a7e-123">Virtual Machines</span></span> 
- <span data-ttu-id="79a7e-124">Sanal makine ölçekleme kümeleri</span><span class="sxs-lookup"><span data-stu-id="79a7e-124">Virtual Machine scale sets</span></span> 
- <span data-ttu-id="79a7e-125">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="79a7e-125">Service Fabric</span></span>

### <a name="application---diagnostics-logs-application-logs-and-metrics"></a><span data-ttu-id="79a7e-126">Uygulama - tanılama günlükleri, uygulama günlüklerini ve ölçümleri</span><span class="sxs-lookup"><span data-stu-id="79a7e-126">Application - Diagnostics Logs, Application Logs, and Metrics</span></span>
<span data-ttu-id="79a7e-127">Uygulamaları hello işlem modeli hello konuk işletim sistemi üzerinde çalıştırılabilir.</span><span class="sxs-lookup"><span data-stu-id="79a7e-127">Applications can run on top of hello Guest OS in hello compute model.</span></span> <span data-ttu-id="79a7e-128">Bunlar, kullanıcıların kendi günlüklerini ve ölçümleri kümesini yayma.</span><span class="sxs-lookup"><span data-stu-id="79a7e-128">They emit their own set of logs and metrics.</span></span> <span data-ttu-id="79a7e-129">Azure İzleyicisi Merhaba Azure tanılama uzantısını (Windows veya Linux) toocollect üzerinde çoğu uygulama düzeyindeki ölçümlerini ve günlükleri kullanır.</span><span class="sxs-lookup"><span data-stu-id="79a7e-129">Azure Monitor relies on hello Azure diagnostics extension (Windows or Linux) toocollect most application level metrics and logs.</span></span> <span data-ttu-id="79a7e-130">Merhaba türler</span><span class="sxs-lookup"><span data-stu-id="79a7e-130">hello types include</span></span>

* <span data-ttu-id="79a7e-131">Performans sayaçları</span><span class="sxs-lookup"><span data-stu-id="79a7e-131">Performance counters</span></span>
* <span data-ttu-id="79a7e-132">Uygulama günlükleri</span><span class="sxs-lookup"><span data-stu-id="79a7e-132">Application Logs</span></span>
* <span data-ttu-id="79a7e-133">Windows olay günlükleri</span><span class="sxs-lookup"><span data-stu-id="79a7e-133">Windows Event Logs</span></span>
* <span data-ttu-id="79a7e-134">.NET olay kaynağı</span><span class="sxs-lookup"><span data-stu-id="79a7e-134">.NET Event Source</span></span>
* <span data-ttu-id="79a7e-135">IIS günlükleri</span><span class="sxs-lookup"><span data-stu-id="79a7e-135">IIS Logs</span></span>
* <span data-ttu-id="79a7e-136">Temel ETW bildirimi</span><span class="sxs-lookup"><span data-stu-id="79a7e-136">Manifest based ETW</span></span>
* <span data-ttu-id="79a7e-137">Kilitlenme bilgi dökümleri</span><span class="sxs-lookup"><span data-stu-id="79a7e-137">Crash Dumps</span></span>
* <span data-ttu-id="79a7e-138">Müşteri hata günlükleri</span><span class="sxs-lookup"><span data-stu-id="79a7e-138">Customer Error Logs</span></span>

<span data-ttu-id="79a7e-139">Merhaba tanılama uzantısını, yalnızca birkaç ölçümleri CPU kullanımı gibi kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="79a7e-139">Without hello diagnostics extension, only a few metrics like CPU usage are available.</span></span> 

### <a name="host-and-guest-vm-metrics"></a><span data-ttu-id="79a7e-140">Ana bilgisayar ve Konuk VM ölçümleri</span><span class="sxs-lookup"><span data-stu-id="79a7e-140">Host and Guest VM metrics</span></span>
<span data-ttu-id="79a7e-141">Merhaba daha önce listelenen işlem kaynakları ayrılmış bir ana bilgisayar VM ve konuk işletim sistemi ile etkileşim vardır.</span><span class="sxs-lookup"><span data-stu-id="79a7e-141">hello previously listed compute resources have a dedicated host VM and guest OS they interact with.</span></span> <span data-ttu-id="79a7e-142">Merhaba konak VM ve konuk işletim sistemi kök VM hello denk ve Konuk VM hello Hyper-V hiper yönetici modelinde kümesidir.</span><span class="sxs-lookup"><span data-stu-id="79a7e-142">hello host VM and guest OS are hello equivalent of root VM and guest VM in hello Hyper-V hypervisor model.</span></span> <span data-ttu-id="79a7e-143">Ölçümleri hem de toplayabilir.</span><span class="sxs-lookup"><span data-stu-id="79a7e-143">You can collect metrics on both.</span></span> <span data-ttu-id="79a7e-144">Ayrıca, hello konuk işletim sistemi tanılama günlüklerini toplayabilir.</span><span class="sxs-lookup"><span data-stu-id="79a7e-144">You can also collect diagnostics logs on hello guest OS.</span></span>   

### <a name="activity-log"></a><span data-ttu-id="79a7e-145">Etkinlik Günlüğü</span><span class="sxs-lookup"><span data-stu-id="79a7e-145">Activity Log</span></span>
<span data-ttu-id="79a7e-146">Hello Azure altyapısı tarafından görülen, kaynak hakkında bilgi için hello etkinlik günlüğü (daha önce işlemsel veya denetim günlüklerini denir) arayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="79a7e-146">You can search hello Activity Log (previously called Operational or Audit Logs) for information about your resource as seen by hello Azure infrastructure.</span></span> <span data-ttu-id="79a7e-147">Merhaba günlük kez kaynakları zaman oluşturulan veya yok gibi bilgileri içerir.</span><span class="sxs-lookup"><span data-stu-id="79a7e-147">hello log contains information such as times when resources are created or destroyed.</span></span>  <span data-ttu-id="79a7e-148">Daha fazla bilgi için bkz: [etkinlik günlüğü'ne genel bakış](monitoring-overview-activity-logs.md).</span><span class="sxs-lookup"><span data-stu-id="79a7e-148">For more information, see [Overview of Activity Log](monitoring-overview-activity-logs.md).</span></span> 

## <a name="monitoring-sources---everything-else"></a><span data-ttu-id="79a7e-149">İzleme kaynakları - şey</span><span class="sxs-lookup"><span data-stu-id="79a7e-149">Monitoring Sources - everything else</span></span>

![İzleme ve tanılama işlem kaynakları için modeli](./media/monitoring-overview-azure-monitor/Monitoring_Azure_Resources-non-compute_v6.png)


### <a name="resource---metrics-and-diagnostics-logs"></a><span data-ttu-id="79a7e-151">Kaynak - ölçümleri ve tanılama günlükleri</span><span class="sxs-lookup"><span data-stu-id="79a7e-151">Resource - Metrics and Diagnostics Logs</span></span>
<span data-ttu-id="79a7e-152">Toplanabilir ölçümleri ve tanılama günlüklerini hello kaynak türüne göre farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="79a7e-152">Collectable metrics and diagnostics logs vary based on hello resource type.</span></span> <span data-ttu-id="79a7e-153">Örneğin, Web uygulamaları hello Disk GÇ ve yüzde CPU istatistikler sağlar.</span><span class="sxs-lookup"><span data-stu-id="79a7e-153">For example, Web Apps provides statistics on hello Disk IO and Percent CPU.</span></span> <span data-ttu-id="79a7e-154">Bu ölçümleri yerine kuyruk boyutu ve ileti işleme gibi ölçümleri sağlar Service Bus kuyruğuna için mevcut değil.</span><span class="sxs-lookup"><span data-stu-id="79a7e-154">Those metrics don't exist for a Service Bus queue, which instead provides metrics like queue size and message throughput.</span></span> <span data-ttu-id="79a7e-155">Her kaynak için toplanabilir ölçümleri listesi kullanılabilir [ölçümleri desteklenen](monitoring-supported-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="79a7e-155">A list of collectable metrics for each resource is available at [supported metrics](monitoring-supported-metrics.md).</span></span> 

### <a name="host-and-guest-vm-metrics"></a><span data-ttu-id="79a7e-156">Ana bilgisayar ve Konuk VM ölçümleri</span><span class="sxs-lookup"><span data-stu-id="79a7e-156">Host and Guest VM metrics</span></span>
<span data-ttu-id="79a7e-157">Olmadığından değil mutlaka kaynağınız ve belirli ana bilgisayar veya konuk VM 1:1 eşlemesini ölçümleri kullanılabilir değil.</span><span class="sxs-lookup"><span data-stu-id="79a7e-157">There is not necessarily a 1:1 mapping between your resource and a particular Host or Guest VM so metrics are not available.</span></span>

### <a name="activity-log"></a><span data-ttu-id="79a7e-158">Etkinlik Günlüğü</span><span class="sxs-lookup"><span data-stu-id="79a7e-158">Activity Log</span></span>
<span data-ttu-id="79a7e-159">Merhaba etkinlik günlüğü olduğu hello aynı işlem kaynakları.</span><span class="sxs-lookup"><span data-stu-id="79a7e-159">hello activity log is hello same as for compute resources.</span></span>  

## <a name="uses-for-monitoring-data"></a><span data-ttu-id="79a7e-160">Veri izleme kullanır</span><span class="sxs-lookup"><span data-stu-id="79a7e-160">Uses for Monitoring Data</span></span>
<span data-ttu-id="79a7e-161">Veri toplama sonra yapabilirsiniz ile Azure İzleyicisi'nde aşağıdaki hello</span><span class="sxs-lookup"><span data-stu-id="79a7e-161">Once you collect your data, you can do hello following with it in Azure Monitor</span></span>

### <a name="route"></a><span data-ttu-id="79a7e-162">Yol</span><span class="sxs-lookup"><span data-stu-id="79a7e-162">Route</span></span>
<span data-ttu-id="79a7e-163">Gerçek zamanlı izleme verileri tooother konumlarda akışını sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="79a7e-163">You can stream monitoring data tooother locations in real time.</span></span>

<span data-ttu-id="79a7e-164">Örneklere şunlar dahildir:</span><span class="sxs-lookup"><span data-stu-id="79a7e-164">Examples include:</span></span>

- <span data-ttu-id="79a7e-165">Daha zengin Görselleştirme ve çözümleme araçları kullanabilmeniz için tooApplication Öngörüler gönderin.</span><span class="sxs-lookup"><span data-stu-id="79a7e-165">Send tooApplication Insights so you can use its richer visualization and analysis tools.</span></span>
- <span data-ttu-id="79a7e-166">Toothird taraf Araçlar yönlendirmek için tooEvent hub gönderin.</span><span class="sxs-lookup"><span data-stu-id="79a7e-166">Send tooEvent Hubs so you can route toothird-party tools.</span></span> 

### <a name="store-and-archive"></a><span data-ttu-id="79a7e-167">Depolama ve Arşiv</span><span class="sxs-lookup"><span data-stu-id="79a7e-167">Store and Archive</span></span>
<span data-ttu-id="79a7e-168">Bazı izleme verilerini bir kümesi süre boyunca depolanan ve Azure İzleyicisi'nde kullanılabilir zaten var.</span><span class="sxs-lookup"><span data-stu-id="79a7e-168">Some monitoring data is already stored and available in Azure Monitor for a set amount of time.</span></span> 
- <span data-ttu-id="79a7e-169">Ölçümleri 30 gün süreyle depolanır.</span><span class="sxs-lookup"><span data-stu-id="79a7e-169">Metrics are stored for 30 days.</span></span> 
- <span data-ttu-id="79a7e-170">Etkinlik günlüğü girişleri 90 gün süreyle depolanır.</span><span class="sxs-lookup"><span data-stu-id="79a7e-170">Activity log entries are stored for 90 days.</span></span> 
- <span data-ttu-id="79a7e-171">Tanılama günlüklerini hiç depolanmaz.</span><span class="sxs-lookup"><span data-stu-id="79a7e-171">Diagnostics logs are not stored at all.</span></span> 

<span data-ttu-id="79a7e-172">Yukarıda listelenen dönemleri toostore verilerin hello uzun istiyorsanız, Azure depolamayı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="79a7e-172">If you want toostore data longer than hello time periods listed above, you can use an Azure storage.</span></span> <span data-ttu-id="79a7e-173">İzleme verilerini ayarladığınız bir bekletme ilkesi temel alınarak, depolama hesabı tutulur.</span><span class="sxs-lookup"><span data-stu-id="79a7e-173">Monitoring data is kept in your storage acccount based on a retention policy you set.</span></span> <span data-ttu-id="79a7e-174">Azure depolama alanında veri işgal hello alanı hello toopay sahip.</span><span class="sxs-lookup"><span data-stu-id="79a7e-174">You do have toopay for hello space hello data takes up in Azure storage.</span></span> 

<span data-ttu-id="79a7e-175">Birkaç yolu toouse bu veriler:</span><span class="sxs-lookup"><span data-stu-id="79a7e-175">A few ways toouse this data:</span></span>

- <span data-ttu-id="79a7e-176">Yazıldıktan sonra onu okuyun ve işleme diğer araçları içinde veya Azure dışında olabilir.</span><span class="sxs-lookup"><span data-stu-id="79a7e-176">Once written, you can have other tools within or outside of Azure read it and process it.</span></span>
- <span data-ttu-id="79a7e-177">Uzun süre için bekletme ilkenizde hello bulut tookeep veri değiştirmek veya hello verilerini yerel olarak yerel bir arşiv indirilir.</span><span class="sxs-lookup"><span data-stu-id="79a7e-177">You download hello data locally for a local archive or change your retention policy in hello cloud tookeep data for extended periods of time.</span></span>  
- <span data-ttu-id="79a7e-178">Arşiv amacıyla süresiz olarak Azure depolama alanında hello veri bırakın.</span><span class="sxs-lookup"><span data-stu-id="79a7e-178">You leave hello data in Azure storage indefinitely for archive purposes.</span></span> 

### <a name="query"></a><span data-ttu-id="79a7e-179">Sorgu</span><span class="sxs-lookup"><span data-stu-id="79a7e-179">Query</span></span>
<span data-ttu-id="79a7e-180">Hello Azure İzleyici REST API'si, platformlar arası komut satırı arabirimi (CLI) komutları, PowerShell cmdlet'lerini kullanabilirsiniz ya da hello sistem veya Azure storage veri hello .NET SDK'sı tooaccess hello</span><span class="sxs-lookup"><span data-stu-id="79a7e-180">You can use hello Azure Monitor REST API, cross platform Command-Line Interface (CLI) commands, PowerShell cmdlets, or hello .NET SDK tooaccess hello data in hello system or Azure storage</span></span>

<span data-ttu-id="79a7e-181">Örneklere şunlar dahildir:</span><span class="sxs-lookup"><span data-stu-id="79a7e-181">Examples include:</span></span>

* <span data-ttu-id="79a7e-182">Yazdığınız özel bir izleme uygulama için veri alma</span><span class="sxs-lookup"><span data-stu-id="79a7e-182">Getting data for a custom monitoring application you have written</span></span>
* <span data-ttu-id="79a7e-183">Özel sorgular oluşturma ve bu verileri tooa üçüncü taraf uygulaması gönderme.</span><span class="sxs-lookup"><span data-stu-id="79a7e-183">Creating custom queries and sending that data tooa third-party application.</span></span>

### <a name="visualize"></a><span data-ttu-id="79a7e-184">Görselleştirme</span><span class="sxs-lookup"><span data-stu-id="79a7e-184">Visualize</span></span>
<span data-ttu-id="79a7e-185">Grafikleri izleme verilerinizi görselleştirme eğilimleri hello verilerine kendisini arayan hızlıdır bulmanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="79a7e-185">Visualizing your monitoring data in graphics and charts helps you find trends quicker than looking through hello data itself.</span></span>  

<span data-ttu-id="79a7e-186">Birkaç görselleştirme yöntemler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="79a7e-186">A few visualization methods include:</span></span>

* <span data-ttu-id="79a7e-187">Hello Azure portalını kullanın</span><span class="sxs-lookup"><span data-stu-id="79a7e-187">Use hello Azure portal</span></span>
* <span data-ttu-id="79a7e-188">Rota veri tooAzure Application Insights</span><span class="sxs-lookup"><span data-stu-id="79a7e-188">Route data tooAzure Application Insights</span></span>
* <span data-ttu-id="79a7e-189">Rota veri tooMicrosoft Powerbı</span><span class="sxs-lookup"><span data-stu-id="79a7e-189">Route data tooMicrosoft PowerBI</span></span>
* <span data-ttu-id="79a7e-190">Rota hello veri tooa üçüncü taraf görselleştirme aracını kullanarak ya da canlı akış veya sağlayarak hello aracı Azure depolama alanında bir arşiv okuma</span><span class="sxs-lookup"><span data-stu-id="79a7e-190">Route hello data tooa third-party visualization tool using either live streaming or by having hello tool read from an archive in Azure storage</span></span>


### <a name="automate"></a><span data-ttu-id="79a7e-191">Otomatikleştirme</span><span class="sxs-lookup"><span data-stu-id="79a7e-191">Automate</span></span>
<span data-ttu-id="79a7e-192">İzleme veri tootrigger uyarıları kullanın veya hatta tüm işlemler.</span><span class="sxs-lookup"><span data-stu-id="79a7e-192">You can use monitoring data tootrigger alerts or even whole processes.</span></span> <span data-ttu-id="79a7e-193">Örneklere şunlar dahildir:</span><span class="sxs-lookup"><span data-stu-id="79a7e-193">Examples include:</span></span>

* <span data-ttu-id="79a7e-194">Veri tooautoscale işlem örneklerini uygulama yüküne göre yukarı veya aşağı kullanın.</span><span class="sxs-lookup"><span data-stu-id="79a7e-194">Use data tooautoscale compute instances up or down based on application load.</span></span>
* <span data-ttu-id="79a7e-195">Ölçüm önceden belirlenmiş bir eşik kestiği olduğunda e-postalar gönderin.</span><span class="sxs-lookup"><span data-stu-id="79a7e-195">Send emails when a metric crosses a predetermined threshold.</span></span>
* <span data-ttu-id="79a7e-196">Web URL (Web kancası) tooexecute Azure dışında bir sistemde bir eylem çağrısı</span><span class="sxs-lookup"><span data-stu-id="79a7e-196">Call a web URL (webhook) tooexecute an action in a system outside of Azure</span></span>
* <span data-ttu-id="79a7e-197">Bir runbook'un Azure Otomasyon tooperform herhangi çeşitli görevleri Başlat</span><span class="sxs-lookup"><span data-stu-id="79a7e-197">Start a runbook in Azure automation tooperform any variety of tasks</span></span>

## <a name="methods-of-accessing-azure-monitor"></a><span data-ttu-id="79a7e-198">Azure İzleyicisi'ne erişim yöntemleri</span><span class="sxs-lookup"><span data-stu-id="79a7e-198">Methods of accessing Azure Monitor</span></span>
<span data-ttu-id="79a7e-199">Genel olarak, veri izleme, Yönlendirme ve alma yöntemleri aşağıdaki hello birini kullanarak yönetebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="79a7e-199">In general, you can manipulate data tracking, routing, and retrieval using one of hello following methods.</span></span> <span data-ttu-id="79a7e-200">Tüm yöntemler, tüm eylemler veya veri türleri için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="79a7e-200">Not all methods are available for all actions or data types.</span></span>

* [<span data-ttu-id="79a7e-201">Azure portal</span><span class="sxs-lookup"><span data-stu-id="79a7e-201">Azure portal</span></span>](https://portal.azure.com)
* [<span data-ttu-id="79a7e-202">PowerShell</span><span class="sxs-lookup"><span data-stu-id="79a7e-202">PowerShell</span></span>](insights-powershell-samples.md)  
* [<span data-ttu-id="79a7e-203">Platformlar arası komut satırı arabirimi (CLI)</span><span class="sxs-lookup"><span data-stu-id="79a7e-203">Cross-platform Command Line Interface (CLI)</span></span>](insights-cli-samples.md)
* [<span data-ttu-id="79a7e-204">REST API</span><span class="sxs-lookup"><span data-stu-id="79a7e-204">REST API</span></span>](https://docs.microsoft.com/rest/api/monitor/)
* [<span data-ttu-id="79a7e-205">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="79a7e-205">.NET SDK</span></span>](http://www.nuget.org/packages/Microsoft.Azure.Management.Monitor)

## <a name="next-steps"></a><span data-ttu-id="79a7e-206">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="79a7e-206">Next steps</span></span>
<span data-ttu-id="79a7e-207">Daha fazla bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="79a7e-207">Learn more about</span></span>
- <span data-ttu-id="79a7e-208">Videosu yalnızca Azure İzleyicisi'ni şu adresten edinilebilir</span><span class="sxs-lookup"><span data-stu-id="79a7e-208">A video walkthrough of just Azure Monitor is available at</span></span>  
<span data-ttu-id="79a7e-209">[Azure İzleyicisi ile çalışmaya başlama](https://channel9.msdn.com/Blogs/Azure-Monitoring/Get-Started-with-Azure-Monitor).</span><span class="sxs-lookup"><span data-stu-id="79a7e-209">[Get Started with Azure Monitor](https://channel9.msdn.com/Blogs/Azure-Monitoring/Get-Started-with-Azure-Monitor).</span></span> <span data-ttu-id="79a7e-210">Burada kullanabileceğiniz Azure monitör bir senaryoda açıklayan ek bir video için bkz. [Microsoft Azure keşfedin izleme ve tanılama](https://channel9.msdn.com/events/Ignite/2016/BRK2234) ve [Ignite 2016'den video Azure izleyicisinde](https://myignite.microsoft.com/videos/4977)</span><span class="sxs-lookup"><span data-stu-id="79a7e-210">An additional video explaining a scenario where you can use Azure Monitor is available at [Explore Microsoft Azure monitoring and diagnostics](https://channel9.msdn.com/events/Ignite/2016/BRK2234) and [Azure Monitor in a video from Ignite 2016](https://myignite.microsoft.com/videos/4977)</span></span>
- <span data-ttu-id="79a7e-211">Hello Azure İzleyicisi arabirimi aracılığıyla çalıştırmak [Azure İzleyicisi ile çalışmaya başlama](monitoring-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="79a7e-211">Run through hello Azure Monitor interface in [Getting Started with Azure Monitor](monitoring-get-started.md)</span></span>
- <span data-ttu-id="79a7e-212">Merhaba ayarlamak [Azure tanılama uzantıları](../azure-diagnostics.md) sanal makine, bulut hizmetinde toodiagnose sorunları çalışıyorsanız sanal makine ölçekleme kümeleri veya Service Fabric uygulaması.</span><span class="sxs-lookup"><span data-stu-id="79a7e-212">Set up hello [Azure Diagnostics Extensions](../azure-diagnostics.md) if you are attempting toodiagnose problems in your Cloud Service, Virtual Machine, Virtual machine scale sets, or Service Fabric application.</span></span>
- <span data-ttu-id="79a7e-213">[Application Insights](https://azure.microsoft.com/documentation/services/application-insights/) App Service Web uygulamanızda toodiagnostic sorunları çalışıyorsanız.</span><span class="sxs-lookup"><span data-stu-id="79a7e-213">[Application Insights](https://azure.microsoft.com/documentation/services/application-insights/) if you are trying toodiagnostic problems in your App Service Web app.</span></span>
- <span data-ttu-id="79a7e-214">[Azure Storage sorunlarını giderme](../storage/common/storage-e2e-troubleshooting.md) depolama BLOB'ları, tabloların veya kuyrukların kullanırken</span><span class="sxs-lookup"><span data-stu-id="79a7e-214">[Troubleshooting Azure Storage](../storage/common/storage-e2e-troubleshooting.md) when using Storage Blobs, Tables, or Queues</span></span>
- <span data-ttu-id="79a7e-215">[Günlük analizi](https://azure.microsoft.com/documentation/services/log-analytics/) ve hello [Operations Management Suite](https://www.microsoft.com/oms/)</span><span class="sxs-lookup"><span data-stu-id="79a7e-215">[Log Analytics](https://azure.microsoft.com/documentation/services/log-analytics/) and hello [Operations Management Suite](https://www.microsoft.com/oms/)</span></span>
