---
title: "Azure tanılama performans sayaçları aaaUse | Microsoft Docs"
description: "Performansı ayarlamak ve performans sayaçları Azure bulut Hizmetleri veya sanal makine toofind performans sorunlarını kullanın."
services: cloud-services
documentationcenter: .net
author: rboucher
manager: jwhit
editor: tysonn
ms.assetid: fc4c61e9-d49d-4ed9-a32c-b91cdf851909
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/29/2016
ms.author: robb
ms.openlocfilehash: f3250816c01fc6e164a6aae48da5035845e6d2b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-use-performance-counters-in-an-azure-application"></a><span data-ttu-id="f0168-103">Oluşturma ve bir Azure uygulamasında performans sayaçlarını kullanma</span><span class="sxs-lookup"><span data-stu-id="f0168-103">Create and use performance counters in an Azure application</span></span>
<span data-ttu-id="f0168-104">Bu makalede hello avantajları ve nasıl Azure uygulamanıza tooput performans sayaçları açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="f0168-104">This article describes hello benefits of and how tooput performance counters into your Azure application.</span></span> <span data-ttu-id="f0168-105">Toocollect verileri kullanmak, engelleri bulun ve sistem ve uygulama performansı ayarlamak.</span><span class="sxs-lookup"><span data-stu-id="f0168-105">You can use them toocollect data, find bottlenecks, and tune system and application performance.</span></span>

<span data-ttu-id="f0168-106">Windows Server, IIS ve ASP.NET için kullanılabilen performans sayaçlarının de toplanabilir ve toodetermine hello durumunu Azure web rolleri, çalışan rolleri ve sanal makineleri kullanılır.</span><span class="sxs-lookup"><span data-stu-id="f0168-106">Performance counters available for Windows Server, IIS, and ASP.NET can also be collected and used toodetermine hello health of your Azure web roles, worker roles, and Virtual Machines.</span></span> <span data-ttu-id="f0168-107">Ayrıca, oluşturabilir ve özel performans sayaçları kullanın.</span><span class="sxs-lookup"><span data-stu-id="f0168-107">You can also create and use custom performance counters.</span></span>  

<span data-ttu-id="f0168-108">Performans sayacı verilerini inceleyebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="f0168-108">You can examine performance counter data</span></span>

1. <span data-ttu-id="f0168-109">Doğrudan hello uygulama ana bilgisayarda Uzak Masaüstü kullanarak erişilen hello Performans İzleyicisi aracıyla</span><span class="sxs-lookup"><span data-stu-id="f0168-109">Directly on hello application host with hello Performance Monitor tool accessed using Remote Desktop</span></span>
2. <span data-ttu-id="f0168-110">System Center Operations Manager kullanarak Azure Management Pack Merhaba</span><span class="sxs-lookup"><span data-stu-id="f0168-110">With System Center Operations Manager using hello Azure Management Pack</span></span>
3. <span data-ttu-id="f0168-111">Merhaba erişim diğer izleme araçları ile tanılama veri tooAzure depolama aktarılan.</span><span class="sxs-lookup"><span data-stu-id="f0168-111">With other monitoring tools that access hello diagnostic data transferred tooAzure storage.</span></span> <span data-ttu-id="f0168-112">Bkz: [deposu ve görünüm tanılama verilerini Azure storage'da](https://msdn.microsoft.com/library/azure/hh411534.aspx) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="f0168-112">See [Store and View Diagnostic Data in Azure Storage](https://msdn.microsoft.com/library/azure/hh411534.aspx) for more information.</span></span>  

<span data-ttu-id="f0168-113">Merhaba, uygulamanızda hello performansını izleme hakkında daha fazla bilgi için [Azure portal](http://portal.azure.com/), bkz: [tooMonitor Cloud Services nasıl](https://www.azure.com/manage/services/cloud-services/how-to-monitor-a-cloud-service/).</span><span class="sxs-lookup"><span data-stu-id="f0168-113">For more information on monitoring hello performance of your application in hello [Azure portal](http://portal.azure.com/), see [How tooMonitor Cloud Services](https://www.azure.com/manage/services/cloud-services/how-to-monitor-a-cloud-service/).</span></span>

<span data-ttu-id="f0168-114">Bir günlük oluşturma ve stratejisi izleme ve tanılama ve diğer teknikleri tootroubleshoot sorunları kullanarak ek ayrıntılı yönergeler için ve Azure uygulamalarını en iyi duruma getirme, bkz: [Azure geliştirmek için en iyi uygulamaları sorunlarını giderme Uygulamaları](https://msdn.microsoft.com/library/azure/hh771389.aspx).</span><span class="sxs-lookup"><span data-stu-id="f0168-114">For additional in-depth guidance on creating a logging and tracing strategy and using diagnostics and other techniques tootroubleshoot problems and optimize Azure applications, see [Troubleshooting Best Practices for Developing Azure Applications](https://msdn.microsoft.com/library/azure/hh771389.aspx).</span></span>

## <a name="enable-performance-counter-monitoring"></a><span data-ttu-id="f0168-115">Performans sayacı izlemeyi etkinleştir</span><span class="sxs-lookup"><span data-stu-id="f0168-115">Enable performance counter monitoring</span></span>
<span data-ttu-id="f0168-116">Performans sayaçları varsayılan olarak etkin değildir.</span><span class="sxs-lookup"><span data-stu-id="f0168-116">Performance counters are not enabled by default.</span></span> <span data-ttu-id="f0168-117">Uygulamanızın veya bir başlangıç görevi her rol örneği toomonitor istediğiniz Aracısı Yapılandırma tooinclude hello belirli performans sayaçları hello varsayılan tanılama değiştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="f0168-117">Your application or a startup task must modify hello default diagnostics agent configuration tooinclude hello specific performance counters that you wish toomonitor for each role instance.</span></span>

### <a name="performance-counters-available-for-microsoft-azure"></a><span data-ttu-id="f0168-118">Microsoft Azure için kullanılabilen performans sayaçlarının</span><span class="sxs-lookup"><span data-stu-id="f0168-118">Performance counters available for Microsoft Azure</span></span>
<span data-ttu-id="f0168-119">Azure, Windows Server, IIS ve ASP.NET yığını hello hello performans sayaçları kümesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="f0168-119">Azure provides a subset of hello performance counters available for Windows Server, IIS and hello ASP.NET stack.</span></span> <span data-ttu-id="f0168-120">Merhaba aşağıdaki tabloda bazı Azure uygulamaları için özellikle ilgisini çeken hello performans sayaçları listeler.</span><span class="sxs-lookup"><span data-stu-id="f0168-120">hello following table lists some of hello performance counters of particular interest for Azure applications.</span></span>

| <span data-ttu-id="f0168-121">Sayacı Kategori: Nesnesi (örneği)</span><span class="sxs-lookup"><span data-stu-id="f0168-121">Counter Category: Object (Instance)</span></span> | <span data-ttu-id="f0168-122">Sayaç adı</span><span class="sxs-lookup"><span data-stu-id="f0168-122">Counter Name</span></span> | <span data-ttu-id="f0168-123">Başvuru</span><span class="sxs-lookup"><span data-stu-id="f0168-123">Reference</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f0168-124">.NET CLR özel durumları (*genel*)</span><span class="sxs-lookup"><span data-stu-id="f0168-124">.NET CLR Exceptions(*Global*)</span></span> |<span data-ttu-id="f0168-125"># Durum / sn</span><span class="sxs-lookup"><span data-stu-id="f0168-125"># Exceps Thrown / sec</span></span> |<span data-ttu-id="f0168-126">Özel durum performans sayaçları</span><span class="sxs-lookup"><span data-stu-id="f0168-126">Exception Performance Counters</span></span> |
| <span data-ttu-id="f0168-127">.NET CLR bellek (*genel*)</span><span class="sxs-lookup"><span data-stu-id="f0168-127">.NET CLR Memory(*Global*)</span></span> |<span data-ttu-id="f0168-128">GC % zaman</span><span class="sxs-lookup"><span data-stu-id="f0168-128">% Time in GC</span></span> |<span data-ttu-id="f0168-129">Bellek performansı sayaçları</span><span class="sxs-lookup"><span data-stu-id="f0168-129">Memory Performance Counters</span></span> |
| <span data-ttu-id="f0168-130">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="f0168-130">ASP.NET</span></span> |<span data-ttu-id="f0168-131">Uygulama yeniden başlatma</span><span class="sxs-lookup"><span data-stu-id="f0168-131">Application Restarts</span></span> |<span data-ttu-id="f0168-132">ASP.NET için performans sayaçları</span><span class="sxs-lookup"><span data-stu-id="f0168-132">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="f0168-133">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="f0168-133">ASP.NET</span></span> |<span data-ttu-id="f0168-134">İstek Yürütme Süresi</span><span class="sxs-lookup"><span data-stu-id="f0168-134">Request Execution Time</span></span> |<span data-ttu-id="f0168-135">ASP.NET için performans sayaçları</span><span class="sxs-lookup"><span data-stu-id="f0168-135">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="f0168-136">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="f0168-136">ASP.NET</span></span> |<span data-ttu-id="f0168-137">Bağlantısı kesilen istek sayısı</span><span class="sxs-lookup"><span data-stu-id="f0168-137">Requests Disconnected</span></span> |<span data-ttu-id="f0168-138">ASP.NET için performans sayaçları</span><span class="sxs-lookup"><span data-stu-id="f0168-138">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="f0168-139">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="f0168-139">ASP.NET</span></span> |<span data-ttu-id="f0168-140">Çalışan işlemi yeniden başlatılır</span><span class="sxs-lookup"><span data-stu-id="f0168-140">Worker Process Restarts</span></span> |<span data-ttu-id="f0168-141">ASP.NET için performans sayaçları</span><span class="sxs-lookup"><span data-stu-id="f0168-141">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="f0168-142">ASP.NET uygulamaları (**toplam**)</span><span class="sxs-lookup"><span data-stu-id="f0168-142">ASP.NET Applications(**Total**)</span></span> |<span data-ttu-id="f0168-143">Toplam istek sayısı</span><span class="sxs-lookup"><span data-stu-id="f0168-143">Requests Total</span></span> |<span data-ttu-id="f0168-144">ASP.NET için performans sayaçları</span><span class="sxs-lookup"><span data-stu-id="f0168-144">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="f0168-145">ASP.NET uygulamaları (**toplam**)</span><span class="sxs-lookup"><span data-stu-id="f0168-145">ASP.NET Applications(**Total**)</span></span> |<span data-ttu-id="f0168-146">İsteği/sn</span><span class="sxs-lookup"><span data-stu-id="f0168-146">Requests/Sec</span></span> |<span data-ttu-id="f0168-147">ASP.NET için performans sayaçları</span><span class="sxs-lookup"><span data-stu-id="f0168-147">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="f0168-148">ASP.NET v4.0.30319</span><span class="sxs-lookup"><span data-stu-id="f0168-148">ASP.NET v4.0.30319</span></span> |<span data-ttu-id="f0168-149">İstek Yürütme Süresi</span><span class="sxs-lookup"><span data-stu-id="f0168-149">Request Execution Time</span></span> |<span data-ttu-id="f0168-150">ASP.NET için performans sayaçları</span><span class="sxs-lookup"><span data-stu-id="f0168-150">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="f0168-151">ASP.NET v4.0.30319</span><span class="sxs-lookup"><span data-stu-id="f0168-151">ASP.NET v4.0.30319</span></span> |<span data-ttu-id="f0168-152">İstek Bekleme süresi</span><span class="sxs-lookup"><span data-stu-id="f0168-152">Request Wait Time</span></span> |<span data-ttu-id="f0168-153">ASP.NET için performans sayaçları</span><span class="sxs-lookup"><span data-stu-id="f0168-153">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="f0168-154">ASP.NET v4.0.30319</span><span class="sxs-lookup"><span data-stu-id="f0168-154">ASP.NET v4.0.30319</span></span> |<span data-ttu-id="f0168-155">İstek geçerli</span><span class="sxs-lookup"><span data-stu-id="f0168-155">Requests Current</span></span> |<span data-ttu-id="f0168-156">ASP.NET için performans sayaçları</span><span class="sxs-lookup"><span data-stu-id="f0168-156">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="f0168-157">ASP.NET v4.0.30319</span><span class="sxs-lookup"><span data-stu-id="f0168-157">ASP.NET v4.0.30319</span></span> |<span data-ttu-id="f0168-158">Sıraya alınan istek sayısı</span><span class="sxs-lookup"><span data-stu-id="f0168-158">Requests Queued</span></span> |<span data-ttu-id="f0168-159">ASP.NET için performans sayaçları</span><span class="sxs-lookup"><span data-stu-id="f0168-159">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="f0168-160">ASP.NET v4.0.30319</span><span class="sxs-lookup"><span data-stu-id="f0168-160">ASP.NET v4.0.30319</span></span> |<span data-ttu-id="f0168-161">Reddedilen istek sayısı</span><span class="sxs-lookup"><span data-stu-id="f0168-161">Requests Rejected</span></span> |<span data-ttu-id="f0168-162">ASP.NET için performans sayaçları</span><span class="sxs-lookup"><span data-stu-id="f0168-162">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="f0168-163">Bellek</span><span class="sxs-lookup"><span data-stu-id="f0168-163">Memory</span></span> |<span data-ttu-id="f0168-164">Kullanılabilir MBayt</span><span class="sxs-lookup"><span data-stu-id="f0168-164">Available MBytes</span></span> |<span data-ttu-id="f0168-165">Bellek performansı sayaçları</span><span class="sxs-lookup"><span data-stu-id="f0168-165">Memory Performance Counters</span></span> |
| <span data-ttu-id="f0168-166">Bellek</span><span class="sxs-lookup"><span data-stu-id="f0168-166">Memory</span></span> |<span data-ttu-id="f0168-167">Kaydedilmiş Bayt</span><span class="sxs-lookup"><span data-stu-id="f0168-167">Committed Bytes</span></span> |<span data-ttu-id="f0168-168">Bellek performansı sayaçları</span><span class="sxs-lookup"><span data-stu-id="f0168-168">Memory Performance Counters</span></span> |
| <span data-ttu-id="f0168-169">İşlemci(_Toplam)</span><span class="sxs-lookup"><span data-stu-id="f0168-169">Processor(_Total)</span></span> |<span data-ttu-id="f0168-170">% İşlemci zamanı</span><span class="sxs-lookup"><span data-stu-id="f0168-170">% Processor Time</span></span> |<span data-ttu-id="f0168-171">ASP.NET için performans sayaçları</span><span class="sxs-lookup"><span data-stu-id="f0168-171">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="f0168-172">TCPv4</span><span class="sxs-lookup"><span data-stu-id="f0168-172">TCPv4</span></span> |<span data-ttu-id="f0168-173">Bağlantı hataları</span><span class="sxs-lookup"><span data-stu-id="f0168-173">Connection Failures</span></span> |<span data-ttu-id="f0168-174">TCP nesnesi</span><span class="sxs-lookup"><span data-stu-id="f0168-174">TCP Object</span></span> |
| <span data-ttu-id="f0168-175">TCPv4</span><span class="sxs-lookup"><span data-stu-id="f0168-175">TCPv4</span></span> |<span data-ttu-id="f0168-176">Kurulan bağlantılar</span><span class="sxs-lookup"><span data-stu-id="f0168-176">Connections Established</span></span> |<span data-ttu-id="f0168-177">TCP nesnesi</span><span class="sxs-lookup"><span data-stu-id="f0168-177">TCP Object</span></span> |
| <span data-ttu-id="f0168-178">TCPv4</span><span class="sxs-lookup"><span data-stu-id="f0168-178">TCPv4</span></span> |<span data-ttu-id="f0168-179">Bağlantıları Sıfırla</span><span class="sxs-lookup"><span data-stu-id="f0168-179">Connections Reset</span></span> |<span data-ttu-id="f0168-180">TCP nesnesi</span><span class="sxs-lookup"><span data-stu-id="f0168-180">TCP Object</span></span> |
| <span data-ttu-id="f0168-181">TCPv4</span><span class="sxs-lookup"><span data-stu-id="f0168-181">TCPv4</span></span> |<span data-ttu-id="f0168-182">Kesim gönderilen/sn</span><span class="sxs-lookup"><span data-stu-id="f0168-182">Segments Sent/sec</span></span> |<span data-ttu-id="f0168-183">TCP nesnesi</span><span class="sxs-lookup"><span data-stu-id="f0168-183">TCP Object</span></span> |
| <span data-ttu-id="f0168-184">Ağ Interface(*)</span><span class="sxs-lookup"><span data-stu-id="f0168-184">Network Interface(*)</span></span> |<span data-ttu-id="f0168-185">Alınan Bayt/sn</span><span class="sxs-lookup"><span data-stu-id="f0168-185">Bytes Received/sec</span></span> |<span data-ttu-id="f0168-186">Ağ arabirimi nesnesi</span><span class="sxs-lookup"><span data-stu-id="f0168-186">Network Interface Object</span></span> |
| <span data-ttu-id="f0168-187">Ağ Interface(*)</span><span class="sxs-lookup"><span data-stu-id="f0168-187">Network Interface(*)</span></span> |<span data-ttu-id="f0168-188">Gönderilen bayt/sn</span><span class="sxs-lookup"><span data-stu-id="f0168-188">Bytes Sent/sec</span></span> |<span data-ttu-id="f0168-189">Ağ arabirimi nesnesi</span><span class="sxs-lookup"><span data-stu-id="f0168-189">Network Interface Object</span></span> |
| <span data-ttu-id="f0168-190">Ağ arabirimi (Microsoft sanal makine veri yolu ağ bağdaştırıcısı _2)</span><span class="sxs-lookup"><span data-stu-id="f0168-190">Network Interface(Microsoft Virtual Machine Bus Network Adapter _2)</span></span> |<span data-ttu-id="f0168-191">Alınan Bayt/sn</span><span class="sxs-lookup"><span data-stu-id="f0168-191">Bytes Received/sec</span></span> |<span data-ttu-id="f0168-192">Ağ arabirimi nesnesi</span><span class="sxs-lookup"><span data-stu-id="f0168-192">Network Interface Object</span></span> |
| <span data-ttu-id="f0168-193">Ağ arabirimi (Microsoft sanal makine veri yolu ağ bağdaştırıcısı _2)</span><span class="sxs-lookup"><span data-stu-id="f0168-193">Network Interface(Microsoft Virtual Machine Bus Network Adapter _2)</span></span> |<span data-ttu-id="f0168-194">Gönderilen bayt/sn</span><span class="sxs-lookup"><span data-stu-id="f0168-194">Bytes Sent/sec</span></span> |<span data-ttu-id="f0168-195">Ağ arabirimi nesnesi</span><span class="sxs-lookup"><span data-stu-id="f0168-195">Network Interface Object</span></span> |
| <span data-ttu-id="f0168-196">Ağ arabirimi (Microsoft sanal makine veri yolu ağ bağdaştırıcısı _2)</span><span class="sxs-lookup"><span data-stu-id="f0168-196">Network Interface(Microsoft Virtual Machine Bus Network Adapter _2)</span></span> |<span data-ttu-id="f0168-197">Toplam Bayt/sn</span><span class="sxs-lookup"><span data-stu-id="f0168-197">Bytes Total/sec</span></span> |<span data-ttu-id="f0168-198">Ağ arabirimi nesnesi</span><span class="sxs-lookup"><span data-stu-id="f0168-198">Network Interface Object</span></span> |

## <a name="create-and-add-custom-performance-counters-tooyour-application"></a><span data-ttu-id="f0168-199">Oluşturma ve özel performans sayaçları tooyour uygulama ekleme</span><span class="sxs-lookup"><span data-stu-id="f0168-199">Create and add custom performance counters tooyour application</span></span>
<span data-ttu-id="f0168-200">Azure destek toocreate sahiptir ve web rolleri ve çalışan rolleri için özel performans sayaçları değiştirin.</span><span class="sxs-lookup"><span data-stu-id="f0168-200">Azure has support toocreate and modify custom performance counters for web roles and worker roles.</span></span> <span data-ttu-id="f0168-201">Merhaba sayaçları kullanılan tootrack ve İzleyici uygulamaya özgü davranışını olabilir.</span><span class="sxs-lookup"><span data-stu-id="f0168-201">hello counters may be used tootrack and monitor application-specific behavior.</span></span> <span data-ttu-id="f0168-202">Oluşturun ve bir başlangıç görevi, web rolü ve çalışan rolü yükseltilmiş izinleri olan özel performans sayacı kategorileri ve tanımlayıcıları silin.</span><span class="sxs-lookup"><span data-stu-id="f0168-202">You can create and delete custom performance counter categories and specifiers from a startup task, web role, or worker role with elevated permissions.</span></span>

> [!NOTE]
> <span data-ttu-id="f0168-203">Toocustom performans sayaçları değişiklikleri yapar kod izinleri toorun yükseltilmiş gerekir.</span><span class="sxs-lookup"><span data-stu-id="f0168-203">Code that makes changes toocustom performance counters must have elevated permissions toorun.</span></span> <span data-ttu-id="f0168-204">Merhaba kodu bir web rolü veya çalışan rolü ise hello rolü hello etiketi içermelidir <Runtime executionContext="elevated" /> hello ServiceDefinition.csdef hello rol tooinitialize için doğru dosya.</span><span class="sxs-lookup"><span data-stu-id="f0168-204">If hello code is in a web role or worker role, hello role must include hello tag <Runtime executionContext="elevated" /> in hello ServiceDefinition.csdef file for hello role tooinitialize properly.</span></span>
>
>

<span data-ttu-id="f0168-205">Özel performans sayacı verileri tooAzure depolama hello Tanılama aracı kullanarak gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f0168-205">You can send custom performance counter data tooAzure storage using hello diagnostics agent.</span></span>

<span data-ttu-id="f0168-206">Merhaba standart performans sayacı verilerini hello Azure işler tarafından oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="f0168-206">hello standard performance counter data is generated by hello Azure processes.</span></span> <span data-ttu-id="f0168-207">Özel performans sayacı verilerini, web rolü ya da çalışan rolü uygulamanız tarafından oluşturulmuş olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="f0168-207">Custom performance counter data must be created by your web role or worker role application.</span></span> <span data-ttu-id="f0168-208">Bkz: [performans sayacı türleri](https://msdn.microsoft.com/library/z573042h.aspx) hello özel performans sayaçları depolanan veri türleri hakkında bilgi için.</span><span class="sxs-lookup"><span data-stu-id="f0168-208">See [Performance Counter Types](https://msdn.microsoft.com/library/z573042h.aspx) for information on hello types of data that can be stored in custom performance counters.</span></span> <span data-ttu-id="f0168-209">Bkz: [performans sayaçları örnek](http://code.msdn.microsoft.com/azure/) oluşturur ve bir web rolünde özel performans sayacı verilerini ayarlayan bir örnek.</span><span class="sxs-lookup"><span data-stu-id="f0168-209">See [PerformanceCounters Sample](http://code.msdn.microsoft.com/azure/) for an example that creates and sets custom performance counter data in a web role.</span></span>

## <a name="store-and-view-performance-counter-data"></a><span data-ttu-id="f0168-210">Depolama ve görünüm performans sayacı verileri</span><span class="sxs-lookup"><span data-stu-id="f0168-210">Store and view performance counter data</span></span>
<span data-ttu-id="f0168-211">Azure tanılama diğer bilgilerle performans sayacı verileri önbelleğe alır.</span><span class="sxs-lookup"><span data-stu-id="f0168-211">Azure caches performance counter data with other diagnostic information.</span></span> <span data-ttu-id="f0168-212">Bu veriler, Performans İzleyicisi gibi uzak masaüstü erişimi tooview araçları kullanarak hello rol örneği çalışırken, Uzaktan izleme için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="f0168-212">This data is available for remote monitoring while hello role instance is running using remote desktop access tooview tools such as Performance Monitor.</span></span> <span data-ttu-id="f0168-213">toopersist hello veri hello rol örneği dışında hello Tanılama Aracı hello veri tooAzure depolama aktarmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="f0168-213">toopersist hello data outside of hello role instance, hello diagnostics agent must transfer hello data tooAzure storage.</span></span> <span data-ttu-id="f0168-214">önbelleğe alınmış hello performans sayacı verilerini Hello boyut sınırını hello Tanılama Aracı yapılandırılabilir veya olabilir tüm tanılama veri hello için paylaşılan bir sınır toobe parçası yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="f0168-214">hello size limit of hello cached performance counter data can be configured in hello diagnostics agent, or it may be configured toobe part of a shared limit for all hello diagnostic data.</span></span> <span data-ttu-id="f0168-215">Merhaba arabellek boyutunu ayarlama hakkında daha fazla bilgi için bkz: [OverallQuotaInMB](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitorconfiguration.overallquotainmb.aspx) ve [DirectoriesBufferConfiguration](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.directoriesbufferconfiguration.aspx).</span><span class="sxs-lookup"><span data-stu-id="f0168-215">For more information about setting hello buffer size, see [OverallQuotaInMB](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitorconfiguration.overallquotainmb.aspx) and [DirectoriesBufferConfiguration](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.directoriesbufferconfiguration.aspx).</span></span> <span data-ttu-id="f0168-216">Bkz: [deposu ve görünüm tanılama verilerini Azure storage'da](https://msdn.microsoft.com/library/azure/hh411534.aspx) hello Tanılama Aracı tootransfer veri tooa depolama hesabı kurma genel bir bakış için.</span><span class="sxs-lookup"><span data-stu-id="f0168-216">See [Store and View Diagnostic Data in Azure Storage](https://msdn.microsoft.com/library/azure/hh411534.aspx) for an overview of setting up hello diagnostics agent tootransfer data tooa storage account.</span></span>

<span data-ttu-id="f0168-217">Her yapılandırılmış performans sayacı örneği belirtilen örnekleme hızında kaydedilir ve örneklenen hello veriler aktarılır toohello depolama hesabı zamanlanmış aktarım isteği veya isteğe bağlı aktarım isteği.</span><span class="sxs-lookup"><span data-stu-id="f0168-217">Each configured performance counter instance is recorded at a specified sampling rate, and hello sampled data is transferred toohello storage account either by a scheduled transfer request or an on-demand transfer request.</span></span> <span data-ttu-id="f0168-218">Otomatik aktarımları olarak dakikada bir kez sıklıkta zamanlanabilir.</span><span class="sxs-lookup"><span data-stu-id="f0168-218">Automatic transfers may be scheduled as often as once per minute.</span></span> <span data-ttu-id="f0168-219">Performans sayacı verilerini Hello Tanılama aracı tarafından aktarılan bir tablo, WADPerformanceCountersTable, hello depolama hesabında depolanır.</span><span class="sxs-lookup"><span data-stu-id="f0168-219">Performance counter data transferred by hello diagnostics agent is stored in a table, WADPerformanceCountersTable, in hello storage account.</span></span> <span data-ttu-id="f0168-220">Bu tablo erişilen ve standart Azure depolama API yöntemleriyle sorgulanan.</span><span class="sxs-lookup"><span data-stu-id="f0168-220">This table may be accessed and queried with standard Azure storage API methods.</span></span> <span data-ttu-id="f0168-221">Bkz: [Microsoft Azure performans sayaçları örnek](http://code.msdn.microsoft.com/Windows-Azure-PerformanceCo-7d80ebf9) sorgulama ve performans sayacı verilerini hello WADPerformanceCountersTable tablosundan görüntüleyen bir örnek.</span><span class="sxs-lookup"><span data-stu-id="f0168-221">See [Microsoft Azure PerformanceCounters Sample](http://code.msdn.microsoft.com/Windows-Azure-PerformanceCo-7d80ebf9) for an example of querying and displaying performance counter data from hello WADPerformanceCountersTable table.</span></span>

> [!NOTE]
> <span data-ttu-id="f0168-222">Merhaba Tanılama Aracı aktarımı sıklığı ve sıra gecikme bağlı olarak, hello hello depolama hesabındaki en son performans sayacı verilerini birkaç dakika eski olabilir.</span><span class="sxs-lookup"><span data-stu-id="f0168-222">Depending on hello diagnostics agent transfer frequency and queue latency, hello most recent performance counter data in hello storage account may be several minutes out of date.</span></span>
>
>

## <a name="enable-performance-counters-using-diagnostics-configuration-file"></a><span data-ttu-id="f0168-223">Tanılama yapılandırma dosyası kullanarak performans sayaçları sağlar</span><span class="sxs-lookup"><span data-stu-id="f0168-223">Enable performance counters using diagnostics configuration file</span></span>
<span data-ttu-id="f0168-224">Azure uygulamanızda yordamı tooenable performans sayaçlarını izleyerek hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="f0168-224">Use hello following procedure tooenable performance counters in your Azure application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f0168-225">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="f0168-225">Prerequisites</span></span>
<span data-ttu-id="f0168-226">Bu bölümde, uygulamanıza hello Tanılama izleme alınan ve hello tanılama yapılandırma dosyası tooyour Visual Studio çözümü (diagnostics.wadcfg SDK 2.4 ve aşağıda veya diagnostics.wadcfgx SDK 2.5 ve üzeri) eklenen varsayar.</span><span class="sxs-lookup"><span data-stu-id="f0168-226">This section assumes that you have imported hello Diagnostics monitor into your application and added hello diagnostics configuration file tooyour Visual Studio solution (diagnostics.wadcfg in SDK 2.4 and below or diagnostics.wadcfgx in SDK 2.5 and above).</span></span> <span data-ttu-id="f0168-227">Adım 1 ve 2'de bkz [Azure Cloud Services ve sanal makineleri etkinleştirme tanılamada](cloud-services-dotnet-diagnostics.md)) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="f0168-227">See steps 1 and 2 in [Enabling Diagnostics in Azure Cloud Services and Virtual Machines](cloud-services-dotnet-diagnostics.md)) for more information.</span></span>

## <a name="step-1-collect-and-store-data-from-performance-counters"></a><span data-ttu-id="f0168-228">1. adım: Toplamak ve performans sayaçlarını veri depolama</span><span class="sxs-lookup"><span data-stu-id="f0168-228">Step 1: Collect and store data from performance counters</span></span>
<span data-ttu-id="f0168-229">Merhaba tanılama tooyour Visual Studio çözümü dosya ekledikten sonra bir Azure uygulamasında hello toplama ve performans sayacı verilerinin depolanması yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f0168-229">After you have added hello diagnostics file tooyour Visual Studio solution, you can configure hello collection and storage of performance counter data in an Azure application.</span></span> <span data-ttu-id="f0168-230">Bu, performans sayaçları toohello tanılama dosyasını ekleyerek yapılır.</span><span class="sxs-lookup"><span data-stu-id="f0168-230">This is done by adding performance counters toohello diagnostics file.</span></span> <span data-ttu-id="f0168-231">Tanılama verilerini, performans sayaçları dahil olmak üzere, ilk hello örneğinde toplanır.</span><span class="sxs-lookup"><span data-stu-id="f0168-231">Diagnostics data, including performance counters, is first collected on hello instance.</span></span> <span data-ttu-id="f0168-232">kalıcı toohello WADPerformanceCountersTable tablo sonra hello Azure tablo hizmeti hello veri, şunları yapacaksınız şekilde toospecify depolama hesabı, uygulamanızda da hello.</span><span class="sxs-lookup"><span data-stu-id="f0168-232">hello data is then persisted toohello WADPerformanceCountersTable table in hello Azure Table service, so you will also need toospecify hello storage account in your application.</span></span> <span data-ttu-id="f0168-233">Uygulamanızı yerel olarak hello işlem öykünücüsü test ettiğiniz, aynı zamanda tanılama verilerini yerel olarak hello depolama öykünücüsü saklayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f0168-233">If you're testing your application locally in hello Compute Emulator, you can also store diagnostics data locally in hello Storage Emulator.</span></span> <span data-ttu-id="f0168-234">Tanılama verileri depolamak önce toohello önce geçmesi gereken [Azure portal](http://portal.azure.com/) ve klasik depolama hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f0168-234">Before you store diagnostics data, you must first go toohello [Azure portal](http://portal.azure.com/) and create a classic storage account.</span></span> <span data-ttu-id="f0168-235">En iyi toolocate depolama hesabınızdaki uygulamadır hello Azure uygulamanız aynı coğrafi konum.</span><span class="sxs-lookup"><span data-stu-id="f0168-235">A best practice is toolocate your storage account in hello same geo-location as your Azure application.</span></span> <span data-ttu-id="f0168-236">Tutma hello tarafından Azure uygulaması ve depolama hesabı olan içinde Merhaba coğrafi konuma, harici bant genişliği maliyetlerini ödeme yapmaktan kaçınmak ve gecikme süresini azaltmak.</span><span class="sxs-lookup"><span data-stu-id="f0168-236">By keeping hello Azure application and storage account are in hello same geo-location, you avoid paying external bandwidth costs and reduce latency.</span></span>

### <a name="add-performance-counters-toohello-diagnostics-file"></a><span data-ttu-id="f0168-237">Performans sayaçları toohello tanılama dosyası ekleme</span><span class="sxs-lookup"><span data-stu-id="f0168-237">Add performance counters toohello diagnostics file</span></span>
<span data-ttu-id="f0168-238">Kullanabileceğiniz birçok sayaç vardır.</span><span class="sxs-lookup"><span data-stu-id="f0168-238">There are many counters you can use.</span></span> <span data-ttu-id="f0168-239">Merhaba aşağıdaki örnek, web ve çalışan rolü izleme için önerilen birkaç performans sayaçlarını gösterir.</span><span class="sxs-lookup"><span data-stu-id="f0168-239">hello following example shows several performance counters that are recommended for web and worker role monitoring.</span></span>

<span data-ttu-id="f0168-240">Merhaba tanılama dosyasını (diagnostics.wadcfg SDK 2.4 ve altı veya diagnostics.wadcfgx SDK 2.5 ve üzeri) açın ve toohello DiagnosticMonitorConfiguration öğesi aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="f0168-240">Open hello diagnostics file (diagnostics.wadcfg in SDK 2.4 and below or diagnostics.wadcfgx in SDK 2.5 and above) and add hello following toohello DiagnosticMonitorConfiguration element:</span></span>

```xml
<PerformanceCounters bufferQuotaInMB="0" scheduledTransferPeriod="PT30M">
    <PerformanceCounterConfiguration counterSpecifier="\Memory\Available Bytes" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT30S" />

    <!-- Use hello Process(w3wp) category counters in a web role -->

    <PerformanceCounterConfiguration counterSpecifier="\Process(w3wp)\% Processor Time" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\Process(w3wp)\Private Bytes" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\Process(w3wp)\Thread Count" sampleRate="PT30S" />

    <!-- Use hello Process(WaWorkerHost) category counters in a worker role.
        <PerformanceCounterConfiguration counterSpecifier="\Process(WaWorkerHost)\% Processor Time" sampleRate="PT30S" />
        <PerformanceCounterConfiguration counterSpecifier="\Process(WaWorkerHost)\Private Bytes" sampleRate="PT30S" />
        <PerformanceCounterConfiguration counterSpecifier="\Process(WaWorkerHost)\Thread Count" sampleRate="PT30S" />
    -->

    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Interop(_Global_)\# of marshalling" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Loading(_Global_)\% Time Loading" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR LocksAndThreads(_Global_)\Contention Rate / sec" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Memory(_Global_)\# Bytes in all Heaps" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Networking(_Global_)\Connections Established" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Remoting(_Global_)\Remote Calls/sec" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Jit(_Global_)\% Time in Jit" sampleRate="PT30S" />
</PerformanceCounters>
```

<span data-ttu-id="f0168-241">Merhaba en hello koleksiyon için veri türü (Azure günlükleri, IIS günlükleri, vb.) kullanılabilir dosya sistemi depolama miktarını belirtir hello bufferQuotaInMB özniteliği.</span><span class="sxs-lookup"><span data-stu-id="f0168-241">hello bufferQuotaInMB attribute, which specifies hello maximum amount of file system storage that is available for hello data collection type (Azure logs, IIS logs, etc.).</span></span> <span data-ttu-id="f0168-242">Merhaba varsayılan 0'dır.</span><span class="sxs-lookup"><span data-stu-id="f0168-242">hello default is 0.</span></span> <span data-ttu-id="f0168-243">Merhaba kotasına ulaşıldığında, yeni veriler eklendikçe hello eski veriler silinir.</span><span class="sxs-lookup"><span data-stu-id="f0168-243">When hello quota is reached, hello oldest data is deleted as new data is added.</span></span> <span data-ttu-id="f0168-244">Tüm hello bufferQuotaInMB özellikleri Hello toplamını hello OverallQuotaInMB özniteliği hello değerinden büyük olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="f0168-244">hello sum of all hello bufferQuotaInMB properties must be greater than hello value of hello OverallQuotaInMB attribute.</span></span> <span data-ttu-id="f0168-245">Ne kadar depolama tanılama verilerini hello koleksiyonu için gerekli olacak belirleme daha ayrıntılı bilgi için bkz: Merhaba Kurulum WAD bölümünü [Azure uygulamaları geliştirmek için en iyi uygulamaları sorunlarını giderme](https://msdn.microsoft.com/library/windowsazure/hh771389.aspx).</span><span class="sxs-lookup"><span data-stu-id="f0168-245">For a more detailed discussion of determining how much storage will be required for hello collection of diagnostics data, see hello Setup WAD section of [Troubleshooting Best Practices for Developing Azure Applications](https://msdn.microsoft.com/library/windowsazure/hh771389.aspx).</span></span>

<span data-ttu-id="f0168-246">Zamanlanmış veri aktarımlarını hello aralığını belirtir, hello scheduledTransferPeriod özniteliği toohello minute en yakın yukarı yuvarlanmasını.</span><span class="sxs-lookup"><span data-stu-id="f0168-246">hello scheduledTransferPeriod attribute, which specifies hello interval between scheduled transfers of data, rounded up toohello nearest minute.</span></span> <span data-ttu-id="f0168-247">Örnek hello tooPT30M (30 dakika) ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="f0168-247">In hello following examples, it is set tooPT30M (30 minutes).</span></span> <span data-ttu-id="f0168-248">Ayar hello aktarımı dönem tooa küçük gibi değer 1 dakika, üretim uygulamanızın performansını olumsuz yönde etkileyen ancak test hızlı çalışan tanılama görmek için kullanışlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="f0168-248">Setting hello transfer period tooa small value, such as 1 minute, will adversely impact your application's performance in production but can be useful for seeing diagnostics working quickly when you are testing.</span></span> <span data-ttu-id="f0168-249">Merhaba zamanlanmış transfer süresi tanılama veri büyüklükte hello uygulamanızın performansını etkilemez ancak hello örneğinde üzerine değildir küçük tooensure olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="f0168-249">hello scheduled transfer period should be small enough tooensure that diagnostic data is not overwritten on hello instance, but large enough that it will not impact hello performance of your application.</span></span>

<span data-ttu-id="f0168-250">Merhaba counterSpecifier özniteliği hello performans sayacı toocollect belirtir.</span><span class="sxs-lookup"><span data-stu-id="f0168-250">hello counterSpecifier attribute specifies hello performance counter toocollect.</span></span> <span data-ttu-id="f0168-251">Hello sampleRate özniteliği hello oranı aktarılma hello performans sayacı, bu durumda 30 saniye örneklenen belirtir.</span><span class="sxs-lookup"><span data-stu-id="f0168-251">hello sampleRate attribute specifies hello rate at which hello performance counter should be sampled, in this case 30 seconds.</span></span>

<span data-ttu-id="f0168-252">Toocollect istediğiniz hello performans sayaçları ekledikten sonra değişiklikler toohello tanılama dosyanızı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="f0168-252">Once you've added hello performance counters that you want toocollect, save your changes toohello diagnostics file.</span></span> <span data-ttu-id="f0168-253">Ardından, hello tanılama verilerini için kalıcı toospecify hello depolama hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="f0168-253">Next, you need toospecify hello storage account that hello diagnostics data will be persisted to.</span></span>

### <a name="specify-hello-storage-account"></a><span data-ttu-id="f0168-254">Merhaba depolama hesabı belirtin</span><span class="sxs-lookup"><span data-stu-id="f0168-254">Specify hello storage account</span></span>
<span data-ttu-id="f0168-255">tanılama bilgileri tooyour Azure depolama hesabı, belirtmeniz gerekir toopersist, hizmet yapılandırma (ServiceConfiguration.cscfg) dosyasında bir bağlantı dizesi.</span><span class="sxs-lookup"><span data-stu-id="f0168-255">toopersist your diagnostics information tooyour Azure Storage account, you must specify a connection string in your service configuration (ServiceConfiguration.cscfg) file.</span></span>

<span data-ttu-id="f0168-256">Azure SDK 2.5 için hello depolama hesabı hello diagnostics.wadcfgx dosyasında belirtilebilir.</span><span class="sxs-lookup"><span data-stu-id="f0168-256">For Azure SDK 2.5, hello Storage Account can be specified in hello diagnostics.wadcfgx file.</span></span>

> [!NOTE]
> <span data-ttu-id="f0168-257">Bu yönergeler yalnızca tooAzure SDK 2.4 geçerlidir ve aşağıdaki.</span><span class="sxs-lookup"><span data-stu-id="f0168-257">These instructions only apply tooAzure SDK 2.4 and below.</span></span> <span data-ttu-id="f0168-258">Azure SDK 2.5 için hello depolama hesabı hello diagnostics.wadcfgx dosyasında belirtilebilir.</span><span class="sxs-lookup"><span data-stu-id="f0168-258">For Azure SDK 2.5, hello Storage Account can be specified in hello diagnostics.wadcfgx file.</span></span>
>
>

<span data-ttu-id="f0168-259">tooset hello bağlantı dizelerini:</span><span class="sxs-lookup"><span data-stu-id="f0168-259">tooset hello connection strings:</span></span>

1. <span data-ttu-id="f0168-260">Depolama alanınız için sık kullandığınız metin düzenleyiciyi ve kümesi hello bağlantı dizesi kullanarak hello ServiceConfiguration.Cloud.cscfg dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="f0168-260">Open hello ServiceConfiguration.Cloud.cscfg file using your favorite text editor and set hello connection string for your storage.</span></span> <span data-ttu-id="f0168-261">Merhaba *AccountName* ve *AccountKey* değerleri hello erişim tuşları altında hello depolama hesabı Panosu Azure portalında bulundu.</span><span class="sxs-lookup"><span data-stu-id="f0168-261">hello *AccountName* and *AccountKey* values are found in hello Azure portal in hello storage account dashboard, under Access keys.</span></span>

    ```xml
    <ConfigurationSettings>
      <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="DefaultEndpointsProtocol=https;AccountName=<name>;AccountKey=<key>"/>
    </ConfigurationSettings>
    ```
2. <span data-ttu-id="f0168-262">Merhaba ServiceConfiguration.Cloud.cscfg dosyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="f0168-262">Save hello ServiceConfiguration.Cloud.cscfg file.</span></span>
3. <span data-ttu-id="f0168-263">Merhaba ServiceConfiguration.Local.cscfg dosyasını açın ve UseDevelopmentStorage tootrue ayarlandığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="f0168-263">Open hello ServiceConfiguration.Local.cscfg file and verify that UseDevelopmentStorage is set tootrue.</span></span>

    ```xml
    <ConfigurationSettings>
      <Settingname="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="UseDevelopmentStorage=true"/>
    </ConfigurationSettings>
    ```
   <span data-ttu-id="f0168-264">Merhaba bağlantı dizelerini ayarlayın, uygulamanızın dağıtıldığında, uygulamanızın tanılama veri tooyour depolama hesabı korunur.</span><span class="sxs-lookup"><span data-stu-id="f0168-264">Now that hello connection strings are set, your application will persist diagnostics data tooyour storage account when your application is deployed.</span></span>
4. <span data-ttu-id="f0168-265">Kaydet ve projenizi yapılandırın ve ardından uygulamanızı dağıtın.</span><span class="sxs-lookup"><span data-stu-id="f0168-265">Save and build your project, then deploy your application.</span></span>

## <a name="step-2-optional-create-custom-performance-counters"></a><span data-ttu-id="f0168-266">2. adım: (İsteğe bağlı) oluşturma özel performans sayaçları</span><span class="sxs-lookup"><span data-stu-id="f0168-266">Step 2: (Optional) Create custom performance counters</span></span>
<span data-ttu-id="f0168-267">Ayrıca toohello performans sayaçları önceden tanımlanmış, kendi özel performans sayaçları toomonitor web veya çalışan rolleri ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f0168-267">In addition toohello pre-defined performance counters, you can add your own custom performance counters toomonitor web or worker roles.</span></span> <span data-ttu-id="f0168-268">Özel performans sayaçları kullanılan tootrack ve İzleyici uygulamaya özgü davranış ve oluşturulabilir veya bir başlangıç görevi, web rolü ya da yükseltilmiş izinleri olan çalışan rolü silindi.</span><span class="sxs-lookup"><span data-stu-id="f0168-268">Custom performance counters may be used tootrack and monitor application-specific behavior and can be created or deleted in a startup task, web role, or worker role with elevated permissions.</span></span>

<span data-ttu-id="f0168-269">Hello Azure Tanılama Aracı hello performans sayacı yapılandırması başlattıktan bir dakika hello .wadcfg dosyasından yeniler.</span><span class="sxs-lookup"><span data-stu-id="f0168-269">hello Azure diagnostics agent refreshes hello performance counter configuration from hello .wadcfg file one minute after starting.</span></span>  <span data-ttu-id="f0168-270">Hello Azure Tanılama Aracı tooload çalıştığında hello OnStart yöntemi özel performans sayaçları oluşturursanız ve başlangıç görevleri bir dakika tooexecute uzun sürer, özel performans sayaçları oluşturulmuş değil bunları.</span><span class="sxs-lookup"><span data-stu-id="f0168-270">If you create custom performance counters in hello OnStart method and your startup tasks take longer than one minute tooexecute, your custom performance counters will not have been created when hello Azure Diagnostics agent tries tooload them.</span></span>  <span data-ttu-id="f0168-271">Bu senaryoda, Azure tanılama doğru özel performans sayaçları dışındaki tüm tanılama verilerini yakalar görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="f0168-271">In this scenario, you will see that Azure Diagnostics correctly captures all diagnostics data except your custom performance counters.</span></span>  <span data-ttu-id="f0168-272">tooresolve bu sorunu hello performans sayaçlarını bir başlangıç görevi oluşturmak veya performans sayaçları hello oluşturduktan sonra başlangıç görevi bazıları toohello OnStart yöntemi iş taşıyın.</span><span class="sxs-lookup"><span data-stu-id="f0168-272">tooresolve this issue, create hello performance counters in a startup task or move some of your startup task work toohello OnStart method after creating hello performance counters.</span></span>

<span data-ttu-id="f0168-273">Aşağıdaki adımları toocreate sayaç "\MyCustomCounterCategory\MyButton1Counter" adlı basit bir özel performans hello gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="f0168-273">Perform hello following steps toocreate a simple custom performance counter named "\MyCustomCounterCategory\MyButton1Counter":</span></span>

1. <span data-ttu-id="f0168-274">Uygulamanız için Hello Hizmet tanım dosyası (CSDEF) açın.</span><span class="sxs-lookup"><span data-stu-id="f0168-274">Open hello service definition file (CSDEF) for your application.</span></span>
2. <span data-ttu-id="f0168-275">Merhaba çalışma zamanı öğesi toohello WebRole veya örn öğesi tooallow yürütme yükseltilmiş ayrıcalıklarla ekleyin:</span><span class="sxs-lookup"><span data-stu-id="f0168-275">Add hello Runtime element toohello WebRole or WorkerRole element tooallow execution with elevated privileges:</span></span>

    ```xml
    <runtime executioncontext="elevated"/>
    ```
3. <span data-ttu-id="f0168-276">Merhaba dosyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="f0168-276">Save hello file.</span></span>
4. <span data-ttu-id="f0168-277">Merhaba tanılama dosyasını (diagnostics.wadcfg SDK 2.4 ve altı veya diagnostics.wadcfgx SDK 2.5 ve üzeri) açın ve aşağıdaki toohello DiagnosticMonitorConfiguration hello ekleyin</span><span class="sxs-lookup"><span data-stu-id="f0168-277">Open hello diagnostics file (diagnostics.wadcfg in SDK 2.4 and below or diagnostics.wadcfgx in SDK 2.5 and above) and add hello following toohello DiagnosticMonitorConfiguration</span></span>

    ```xml
    <PerformanceCounters bufferQuotaInMB="0" scheduledTransferPeriod="PT30M">
      <PerformanceCounterConfiguration counterSpecifier="\MyCustomCounterCategory\MyButton1Counter" sampleRate="PT30S"/>
    </PerformanceCounters>
    ```
5. <span data-ttu-id="f0168-278">Merhaba dosyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="f0168-278">Save hello file.</span></span>
6. <span data-ttu-id="f0168-279">Merhaba özel performans sayacı kategorisi temel çağırmadan önce hello OnStart yönteminde, rolü oluşturun. OnStart.</span><span class="sxs-lookup"><span data-stu-id="f0168-279">Create hello custom performance counter category in hello OnStart method of your role, before invoking base.OnStart.</span></span> <span data-ttu-id="f0168-280">zaten yoksa, hello aşağıdaki C# örnek özel bir kategori oluşturur:</span><span class="sxs-lookup"><span data-stu-id="f0168-280">hello following C# example creates a custom category, if it does not already exist:</span></span>

    ```csharp
    public override bool OnStart()
    {
      if (!PerformanceCounterCategory.Exists("MyCustomCounterCategory"))
      {
         CounterCreationDataCollection counterCollection = new CounterCreationDataCollection();

         // add a counter tracking user button1 clicks
         CounterCreationData operationTotal1 = new CounterCreationData();
         operationTotal1.CounterName = "MyButton1Counter";
         operationTotal1.CounterHelp = "My Custom Counter for Button1";
         operationTotal1.CounterType = PerformanceCounterType.NumberOfItems32;
         counterCollection.Add(operationTotal1);

         PerformanceCounterCategory.Create(
           "MyCustomCounterCategory",
           "My Custom Counter Category",
           PerformanceCounterCategoryType.SingleInstance, counterCollection);

         Trace.WriteLine("Custom counter category created.");
      }
      else {
        Trace.WriteLine("Custom counter category already exists.");
      }

    return base.OnStart();
    }
    ```
7. <span data-ttu-id="f0168-281">Merhaba sayaçları, uygulamanızda güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="f0168-281">Update hello counters within your application.</span></span> <span data-ttu-id="f0168-282">Aşağıdaki örneğine hello özel performans sayacı Button1_Click olayları güncelleştirir:</span><span class="sxs-lookup"><span data-stu-id="f0168-282">hello following example updates a custom performance counter on Button1_Click events:</span></span>

    ```csharp
    protected void Button1_Click(object sender, EventArgs e)
    {
      PerformanceCounter button1Counter = new PerformanceCounter(
        "MyCustomCounterCategory",
        "MyButton1Counter",
        string.Empty,
        false);
      button1Counter.Increment();
      this.Button1.Text = "Button 1 count: " +
        button1Counter.RawValue.ToString();
    }
    ```
8. <span data-ttu-id="f0168-283">Merhaba dosyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="f0168-283">Save hello file.</span></span>  

<span data-ttu-id="f0168-284">Özel performans sayacı verilerini şimdi hello Azure tanılama İzleyici tarafından toplanacaktır.</span><span class="sxs-lookup"><span data-stu-id="f0168-284">Custom performance counter data will now be collected by hello Azure diagnostics monitor.</span></span>

## <a name="step-3-query-performance-counter-data"></a><span data-ttu-id="f0168-285">3. adım: performans sayacı verileri Sorgulama</span><span class="sxs-lookup"><span data-stu-id="f0168-285">Step 3: Query performance counter data</span></span>
<span data-ttu-id="f0168-286">Uygulamanız dağıtıldıktan sonra çalışmaya, hello Tanılama izleme başlayacak performans sayaçlarını toplama ve bu verileri tooAzure depolama kalıcı yapma.</span><span class="sxs-lookup"><span data-stu-id="f0168-286">Once your application is deployed and running, hello Diagnostics monitor will begin collecting performance counters and persisting that data tooAzure storage.</span></span> <span data-ttu-id="f0168-287">Visual Studio Araçları Sunucu Gezgini gibi kullandığınız [Azure Storage Gezgini](http://azurestorageexplorer.codeplex.com/), veya [Azure tanılama Manager](http://www.cerebrata.com/Products/AzureDiagnosticsManager/Default.aspx) Cerebrata tarafından hello verilerde tooview hello performans sayaçları WADPerformanceCountersTable tablo.</span><span class="sxs-lookup"><span data-stu-id="f0168-287">You use tools such as Server Explorer in Visual Studio,  [Azure Storage Explorer](http://azurestorageexplorer.codeplex.com/), or [Azure Diagnostics Manager](http://www.cerebrata.com/Products/AzureDiagnosticsManager/Default.aspx) by Cerebrata tooview hello performance counters data in hello WADPerformanceCountersTable table.</span></span> <span data-ttu-id="f0168-288">Merhaba tablo hizmetini kullanarak program aracılığıyla da sorgulayabilirsiniz [C#](../cosmos-db/table-storage-how-to-use-dotnet.md), [Java](../cosmos-db/table-storage-how-to-use-java.md), [Node.js](../cosmos-db/table-storage-how-to-use-nodejs.md), [Python](../cosmos-db/table-storage-how-to-use-python.md), [Ruby](../cosmos-db/table-storage-how-to-use-ruby.md), veya [PHP](../cosmos-db/table-storage-how-to-use-php.md).</span><span class="sxs-lookup"><span data-stu-id="f0168-288">You can also programmatically query hello Table service using [C#](../cosmos-db/table-storage-how-to-use-dotnet.md),  [Java](../cosmos-db/table-storage-how-to-use-java.md),  [Node.js](../cosmos-db/table-storage-how-to-use-nodejs.md), [Python](../cosmos-db/table-storage-how-to-use-python.md), [Ruby](../cosmos-db/table-storage-how-to-use-ruby.md), or [PHP](../cosmos-db/table-storage-how-to-use-php.md).</span></span>

<span data-ttu-id="f0168-289">Merhaba aşağıdaki C# örnek temel bir hello WADPerformanceCountersTable Tablo sorgusu gösterir ve hello tanılama veri tooa CSV dosyası kaydeder.</span><span class="sxs-lookup"><span data-stu-id="f0168-289">hello following C# example shows a basic query against hello WADPerformanceCountersTable table and saves hello diagnostics data tooa CSV file.</span></span> <span data-ttu-id="f0168-290">Merhaba performans sayaçları tooa CSV dosyası kaydedildikten sonra Microsoft Excel veya bazı diğer aracı toovisualize hello veri özellikleri Grafikleme hello kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f0168-290">Once hello performance counters are saved tooa CSV file, you can use hello graphing capabilities in Microsoft Excel or some other tool toovisualize hello data.</span></span> <span data-ttu-id="f0168-291">Emin tooadd hello Azure SDK'sı .NET Ekim 2012 ve üzeri için dahil edilen bir başvuru tooMicrosoft.WindowsAzure.Storage.dll olabilir.</span><span class="sxs-lookup"><span data-stu-id="f0168-291">Be sure tooadd a reference tooMicrosoft.WindowsAzure.Storage.dll, which is included in hello Azure SDK for .NET October 2012 and later.</span></span> <span data-ttu-id="f0168-292">Merhaba, yüklü toohello % Program Files%\Microsoft SDKs\Microsoft Azure.NET SDK\version-num\ref\ dizini derlemesidir.</span><span class="sxs-lookup"><span data-stu-id="f0168-292">hello assembly is installed toohello %Program Files%\Microsoft SDKs\Microsoft Azure.NET SDK\version-num\ref\ directory.</span></span>

```csharp
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Auth;
using Microsoft.WindowsAzure.Storage.Table;
...

// Get hello connection string. When using Microsoft Azure Cloud Services, it is recommended
// you store your connection string using hello Microsoft Azure service configuration
// system (*.csdef and *.cscfg files). You can you use hello CloudConfigurationManager type
// tooretrieve your storage connection string.  If you're not using Cloud Services, it's
// recommended that you store hello connection string in your web.config or app.config file.
// Use hello ConfigurationManager type tooretrieve your storage connection string.

string connectionString = Microsoft.WindowsAzure.CloudConfigurationManager.GetSetting("StorageConnectionString");
//string connectionString = System.Configuration.ConfigurationManager.ConnectionStrings["StorageConnectionString"].ConnectionString;

// Get a reference toohello storage account using hello connection string.  You can also use hello development
// storage account (Storage Emulator) for local debugging.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(connectionString);
//CloudStorageAccount storageAccount = CloudStorageAccount.DevelopmentStorageAccount;

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable object that represents hello "WADPerformanceCountersTable" table.
CloudTable table = tableClient.GetTableReference("WADPerformanceCountersTable");

// Create hello table query, filter on a specific CounterName, DeploymentId and RoleInstance.
TableQuery<PerformanceCountersEntity> query = new TableQuery<PerformanceCountersEntity>()
  .Where(
    TableQuery.CombineFilters(
      TableQuery.GenerateFilterCondition("CounterName", QueryComparisons.Equal, @"\Processor(_Total)\% Processor Time"),
      TableOperators.And,
      TableQuery.CombineFilters(
      TableQuery.GenerateFilterCondition("DeploymentId", QueryComparisons.Equal, "ec26b7a1720447e1bcdeefc41c4892a3"),
      TableOperators.And,
      TableQuery.GenerateFilterCondition("RoleInstance", QueryComparisons.Equal, "WebRole1_IN_0")
    )
  )
);

// Execute hello table query.
IEnumerable<PerformanceCountersEntity> result = table.ExecuteQuery(query);

// Process hello query results and build a CSV file.
StringBuilder sb = new StringBuilder("TimeStamp,EventTickCount,DeploymentId,Role,RoleInstance,CounterName,CounterValue\n");

foreach (PerformanceCountersEntity entity in result)
{
  sb.Append(entity.Timestamp + "," + entity.EventTickCount + "," + entity.DeploymentId + ","
    + entity.Role + "," + entity.RoleInstance + "," + entity.CounterName + "," + entity.CounterValue+"\n");
}

StreamWriter sw = File.CreateText(@"C:\temp\PerfCounters.csv");
sw.Write(sb.ToString());
sw.Close();
```

<span data-ttu-id="f0168-293">Varlıkları eşleme türetilen özel bir sınıf kullanarak tooC # nesnelerini **TableEntity**.</span><span class="sxs-lookup"><span data-stu-id="f0168-293">Entities map tooC# objects using a custom class derived from **TableEntity**.</span></span> <span data-ttu-id="f0168-294">Merhaba aşağıdaki kod bir performans sayacının hello temsil eden bir varlık sınıfı tanımlar **WADPerformanceCountersTable** tablo.</span><span class="sxs-lookup"><span data-stu-id="f0168-294">hello following code defines an entity class that represents a performance counter in hello **WADPerformanceCountersTable** table.</span></span>

```csharp
public class PerformanceCountersEntity : TableEntity
{
  public long EventTickCount { get; set; }
  public string DeploymentId { get; set; }
  public string Role { get; set; }
  public string RoleInstance { get; set; }
  public string CounterName { get; set; }
  public double CounterValue { get; set; }
}
```

## <a name="next-steps"></a><span data-ttu-id="f0168-295">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="f0168-295">Next Steps</span></span>
[<span data-ttu-id="f0168-296">Azure tanılama üzerinde ek makaleleri görüntüleme</span><span class="sxs-lookup"><span data-stu-id="f0168-296">View additional articles on Azure Diagnostics</span></span>](../azure-diagnostics.md)
