---
title: "aaaScheduler yüksek kullanılabilirlik ve güvenilirlik"
description: "Yüksek Scheduler kullanılabilirliği ve güvenilirliği"
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 5ec78e60-a9b9-405a-91a8-f010f3872d50
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/16/2016
ms.author: deli
ms.openlocfilehash: 5c9efb333eb42b393adc5deea657ca99206d425e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="scheduler-high-availability-and-reliability"></a><span data-ttu-id="ae124-103">Yüksek Scheduler kullanılabilirliği ve güvenilirliği</span><span class="sxs-lookup"><span data-stu-id="ae124-103">Scheduler High-Availability and Reliability</span></span>
## <a name="azure-scheduler-high-availability"></a><span data-ttu-id="ae124-104">Yüksek Azure Scheduler kullanılabilirliği</span><span class="sxs-lookup"><span data-stu-id="ae124-104">Azure Scheduler High-Availability</span></span>
<span data-ttu-id="ae124-105">Çekirdek Azure platformu hizmet olarak Azure Scheduler yüksek oranda kullanılabilir ve coğrafi olarak yedekli hizmet dağıtımı ve coğrafi bölge iş çoğaltma özellikleri.</span><span class="sxs-lookup"><span data-stu-id="ae124-105">As a core Azure platform service, Azure Scheduler is highly available and features both geo-redundant service deployment and geo-regional job replication.</span></span>

### <a name="geo-redundant-service-deployment"></a><span data-ttu-id="ae124-106">Coğrafi olarak yedekli hizmet dağıtımı</span><span class="sxs-lookup"><span data-stu-id="ae124-106">Geo-redundant service deployment</span></span>
<span data-ttu-id="ae124-107">Azure Zamanlayıcı hello Azure'da bugün olduğu neredeyse her coğrafi bölgede kullanıcı Arabirimi aracılığıyla kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="ae124-107">Azure Scheduler is available via hello UI in almost every geo region that's in Azure today.</span></span> <span data-ttu-id="ae124-108">Azure Scheduler bulunan bölgelere Hello listesidir [burada listelenen](https://azure.microsoft.com/regions/#services).</span><span class="sxs-lookup"><span data-stu-id="ae124-108">hello list of regions that Azure Scheduler is available in is [listed here](https://azure.microsoft.com/regions/#services).</span></span> <span data-ttu-id="ae124-109">Bir veri merkezi barındırılan bir bölgede kullanılamıyor işlenen hello hizmet başka bir veri merkezinden kullanılabilir olacak şekilde, Azure Scheduler hello yük devretme özelliklerini demektir.</span><span class="sxs-lookup"><span data-stu-id="ae124-109">If a data center in a hosted region is rendered unavailable, hello failover capabilities of Azure Scheduler are such that hello service is available from another data center.</span></span>

### <a name="geo-regional-job-replication"></a><span data-ttu-id="ae124-110">Coğrafi bölge iş çoğaltma</span><span class="sxs-lookup"><span data-stu-id="ae124-110">Geo-regional job replication</span></span>
<span data-ttu-id="ae124-111">Yalnızca olan Azure Scheduler ancak kendi iş yönetim istekleri için de coğrafi olarak çoğaltılmış kullanılabilir ön uç hello.</span><span class="sxs-lookup"><span data-stu-id="ae124-111">Not only is hello Azure Scheduler front-end available for management requests, but your own job is also geo-replicated.</span></span> <span data-ttu-id="ae124-112">Bir bölgede bir kesinti olduğunda Azure Scheduler yöneltilir ve o hello işi hello eşleştirilmiş coğrafi bölgede başka bir veri merkezi çalıştırıldığı sağlar.</span><span class="sxs-lookup"><span data-stu-id="ae124-112">When there’s an outage in one region, Azure Scheduler fails over and ensures that hello job is run from another data center in hello paired geographic region.</span></span>

<span data-ttu-id="ae124-113">Örneğin, bir iş Orta Güney ABD içinde oluşturduysanız, Azure Scheduler Kuzey Orta ABD o işe otomatik olarak çoğaltır.</span><span class="sxs-lookup"><span data-stu-id="ae124-113">For example, if you’ve created a job in South Central US, Azure Scheduler automatically replicates that job in North Central US.</span></span> <span data-ttu-id="ae124-114">Olduğunda hata Orta Güney ABD içinde Azure Scheduler Kuzey merkezi Bizden bu hello işini çalıştır sağlar.</span><span class="sxs-lookup"><span data-stu-id="ae124-114">When there’s a failure in South Central US, Azure Scheduler ensures that hello job is run from North Central US.</span></span> 

![][1]

<span data-ttu-id="ae124-115">Sonuç olarak, Azure Scheduler, veri kalır içinde daha geniş aynı coğrafi bölgede bir Azure hatası durumunda hello sağlar.</span><span class="sxs-lookup"><span data-stu-id="ae124-115">As a result, Azure Scheduler ensures that your data stays within hello same broader geographic region in case of an Azure failure.</span></span> <span data-ttu-id="ae124-116">Sonuç olarak, iş yalnızca tooadd yüksek kullanılabilirlik yinelenen olmayan – Azure Scheduler otomatik olarak işleriniz için yüksek kullanılabilirlik yetenekleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="ae124-116">As a result, you need not duplicate your job just tooadd high availability – Azure Scheduler automatically provides high-availability capabilities for your jobs.</span></span>

## <a name="azure-scheduler-reliability"></a><span data-ttu-id="ae124-117">Azure Zamanlayıcı güvenilirlik</span><span class="sxs-lookup"><span data-stu-id="ae124-117">Azure Scheduler Reliability</span></span>
<span data-ttu-id="ae124-118">Azure Zamanlayıcı kendi yüksek oranda kullanılabilirlik garanti eder ve farklı bir yaklaşım toouser oluşturulan işler alır.</span><span class="sxs-lookup"><span data-stu-id="ae124-118">Azure Scheduler guarantees its own high-availability and takes a different approach toouser-created jobs.</span></span> <span data-ttu-id="ae124-119">Örneğin, işinizi kullanılamaz bir HTTP uç noktası çağırabilir.</span><span class="sxs-lookup"><span data-stu-id="ae124-119">For example, your job may invoke an HTTP endpoint that’s unavailable.</span></span> <span data-ttu-id="ae124-120">Azure Zamanlayıcı yine de tooexecute işinizi başarılı bir şekilde, diğer seçenekleri toodeal başarısızlıkla vererek çalışır.</span><span class="sxs-lookup"><span data-stu-id="ae124-120">Azure Scheduler nonetheless tries tooexecute your job successfully, by giving you alternative options toodeal with failure.</span></span> <span data-ttu-id="ae124-121">Azure Scheduler bunu iki şekilde yapar:</span><span class="sxs-lookup"><span data-stu-id="ae124-121">Azure Scheduler does this in two ways:</span></span>

### <a name="configurable-retry-policy-via-retrypolicy"></a><span data-ttu-id="ae124-122">"RetryPolicy" aracılığıyla yapılandırılabilir yeniden deneme ilkesi</span><span class="sxs-lookup"><span data-stu-id="ae124-122">Configurable Retry Policy via “retryPolicy”</span></span>
<span data-ttu-id="ae124-123">Azure Zamanlayıcı tooconfigure bir yeniden deneme ilkesi sağlar.</span><span class="sxs-lookup"><span data-stu-id="ae124-123">Azure Scheduler allows you tooconfigure a retry policy.</span></span> <span data-ttu-id="ae124-124">Bir işi başarısız olursa, varsayılan olarak 30 saniyelik aralıklarda yeniden dört kez daha, hello iş Zamanlayıcı dener.</span><span class="sxs-lookup"><span data-stu-id="ae124-124">By default, if a job fails, Scheduler tries hello job again four more times, at 30-second intervals.</span></span> <span data-ttu-id="ae124-125">Bu yeniden deneme ilkesi toobe daha agresif (örneğin, on kez 30 saniyelik aralıklarda) yeniden yapılandırabilir veya ok (örneğin, iki kez günlük aralıklarla.)</span><span class="sxs-lookup"><span data-stu-id="ae124-125">You may re-configure this retry policy toobe more aggressive (for example, ten times, at 30-second intervals) or looser (for example, two times, at daily intervals.)</span></span>

<span data-ttu-id="ae124-126">Ne zaman bu yardımcı olabilecek örnek olarak, haftada bir kez çalıştırır ve bir HTTP uç noktası çağıran bir iş oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ae124-126">As an example of when this may help, you may create a job that runs once a week and invokes an HTTP endpoint.</span></span> <span data-ttu-id="ae124-127">Merhaba HTTP uç noktası kapalı birkaç saat işiniz çalıştırıldığında ise, bu yana bile hello varsayılan yeniden deneme ilkesi başarısız olur, toowait daha fazla için bir hafta hello iş toorun yeniden istemeyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ae124-127">If hello HTTP endpoint is down for a few hours when your job runs, you may not want toowait one more week for hello job toorun again since even hello default retry policy will fail.</span></span> <span data-ttu-id="ae124-128">Böyle durumlarda, hello standart yeniden deneme ilkesi tooretry üç saatte (örneğin) yerine her 30 saniyede yapılandırabilir.</span><span class="sxs-lookup"><span data-stu-id="ae124-128">In such cases, you may reconfigure hello standard retry policy tooretry every three hours (for example) instead of every 30 seconds.</span></span>

<span data-ttu-id="ae124-129">tooconfigure bir yeniden deneme ilkesi başvurmak çok nasıl toolearn[retryPolicy](scheduler-concepts-terms.md#retrypolicy).</span><span class="sxs-lookup"><span data-stu-id="ae124-129">toolearn how tooconfigure a retry policy, refer too[retryPolicy](scheduler-concepts-terms.md#retrypolicy).</span></span>

### <a name="alternate-endpoint-configurability-via-erroraction"></a><span data-ttu-id="ae124-130">"ErrorAction" yoluyla diğer uç nokta yapılandırılabilirlik</span><span class="sxs-lookup"><span data-stu-id="ae124-130">Alternate Endpoint Configurability via “errorAction”</span></span>
<span data-ttu-id="ae124-131">Azure Scheduler işi için Hello hedef uç noktaya erişilemiyor kalırsa, Azure Scheduler, yeniden deneme ilkesi izledikten sonra toohello alternatif hata işleme uç noktasını geri döner.</span><span class="sxs-lookup"><span data-stu-id="ae124-131">If hello target endpoint for your Azure Scheduler job remains unreachable, Azure Scheduler falls back toohello alternate error-handling endpoint after following its retry policy.</span></span> <span data-ttu-id="ae124-132">Alternatif bir hata işleme uç noktasını yapılandırdıysanız, Azure Scheduler bunu çağırır.</span><span class="sxs-lookup"><span data-stu-id="ae124-132">If an alternate error-handling endpoint is configured, Azure Scheduler invokes it.</span></span> <span data-ttu-id="ae124-133">Başka bir uç nokta ile kendi işleri hatanın hello karşılaştıkları yüksek oranda kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="ae124-133">With an alternate endpoint, your own jobs are highly available in hello face of failure.</span></span>

<span data-ttu-id="ae124-134">Örneğin, aşağıdaki hello diyagramındaki kendi yeniden deneme ilkesi toohit New York web hizmeti Azure Scheduler izler.</span><span class="sxs-lookup"><span data-stu-id="ae124-134">As an example, in hello diagram below, Azure Scheduler follows its retry policy toohit a New York web service.</span></span> <span data-ttu-id="ae124-135">Hello başarısız denemeden sonra alternatif olup olmadığını denetler.</span><span class="sxs-lookup"><span data-stu-id="ae124-135">After hello retries fail, it checks if there's an alternate.</span></span> <span data-ttu-id="ae124-136">Sonra ilerler ve toohello alternatif hello ile aynı istekleri yapan başlatır yeniden deneme ilkesi.</span><span class="sxs-lookup"><span data-stu-id="ae124-136">It then goes ahead and starts making requests toohello alternate with hello same retry policy.</span></span>

![][2]

<span data-ttu-id="ae124-137">Aynı yeniden deneme ilkesi hello Not tooboth hello özgün eylem ve hello alternatif hata eylemi uygular.</span><span class="sxs-lookup"><span data-stu-id="ae124-137">Note that hello same retry policy applies tooboth hello original action and hello alternate error action.</span></span> <span data-ttu-id="ae124-138">Ayrıca olası toohave hello alternatif hata eylemin eylem türü hello ana eylemin eylem türünden farklı.</span><span class="sxs-lookup"><span data-stu-id="ae124-138">It’s also possible toohave hello alternate error action’s action type be different from hello main action’s action type.</span></span> <span data-ttu-id="ae124-139">Örneğin, Hello ana eylemi bir HTTP uç noktası çağırma, ancak hello hata eylemi bunun yerine bir depolama kuyruğu, hizmet veri yolu kuyruğu ya da hata günlüğünü olmadığından hizmet veri yolu konusu eylemi olabilir.</span><span class="sxs-lookup"><span data-stu-id="ae124-139">For example, while hello main action may be invoking an HTTP endpoint, hello error action may instead be a storage queue, service bus queue, or service bus topic action that does error-logging.</span></span>

<span data-ttu-id="ae124-140">tooconfigure alternatif bir uç nokta başvurmak çok nasıl toolearn[errorAction](scheduler-concepts-terms.md#action-and-erroraction).</span><span class="sxs-lookup"><span data-stu-id="ae124-140">toolearn how tooconfigure an alternate endpoint, refer too[errorAction](scheduler-concepts-terms.md#action-and-erroraction).</span></span>

## <a name="see-also"></a><span data-ttu-id="ae124-141">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ae124-141">See Also</span></span>
 [<span data-ttu-id="ae124-142">Scheduler nedir?</span><span class="sxs-lookup"><span data-stu-id="ae124-142">What is Scheduler?</span></span>](scheduler-intro.md)

 [<span data-ttu-id="ae124-143">Azure Scheduler kavramları, terminolojisi ve varlık hiyerarşisi</span><span class="sxs-lookup"><span data-stu-id="ae124-143">Azure Scheduler concepts, terminology, and entity hierarchy</span></span>](scheduler-concepts-terms.md)

 [<span data-ttu-id="ae124-144">Zamanlayıcı hello Azure portalını kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="ae124-144">Get started using Scheduler in hello Azure portal</span></span>](scheduler-get-started-portal.md)

 [<span data-ttu-id="ae124-145">Azure Scheduler’da planlar ve faturalama</span><span class="sxs-lookup"><span data-stu-id="ae124-145">Plans and billing in Azure Scheduler</span></span>](scheduler-plans-billing.md)

 [<span data-ttu-id="ae124-146">Nasıl toobuild karmaşık zamanlar ve Gelişmiş yineleme Azure Scheduler ile</span><span class="sxs-lookup"><span data-stu-id="ae124-146">How toobuild complex schedules and advanced recurrence with Azure Scheduler</span></span>](scheduler-advanced-complexity.md)

 [<span data-ttu-id="ae124-147">Azure Scheduler REST API başvurusu</span><span class="sxs-lookup"><span data-stu-id="ae124-147">Azure Scheduler REST API reference</span></span>](https://msdn.microsoft.com/library/mt629143)

 [<span data-ttu-id="ae124-148">Azure Scheduler PowerShell cmdlet’leri başvurusu</span><span class="sxs-lookup"><span data-stu-id="ae124-148">Azure Scheduler PowerShell cmdlets reference</span></span>](scheduler-powershell-reference.md)

 [<span data-ttu-id="ae124-149">Azure Scheduler sınırları, varsayılanları ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="ae124-149">Azure Scheduler limits, defaults, and error codes</span></span>](scheduler-limits-defaults-errors.md)

 [<span data-ttu-id="ae124-150">Azure Scheduler giden bağlantı kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="ae124-150">Azure Scheduler outbound authentication</span></span>](scheduler-outbound-authentication.md)

[1]: ./media/scheduler-high-availability-reliability/scheduler-high-availability-reliability-image1.png

[2]: ./media/scheduler-high-availability-reliability/scheduler-high-availability-reliability-image2.png
