---
title: Azure uygulama hizmetinde uygulamalar aaaMonitor | Microsoft Docs
description: "Azure Portal kullanarak Azure App Service'te toomonitor uygulamalarını nasıl hello öğrenin."
services: app-service
documentationcenter: 
author: btardif
manager: erikre
editor: 
ms.assetid: d273da4e-07de-48e0-b99d-4020d84a425e
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/07/2016
ms.author: byvinyal
ms.openlocfilehash: 80d5a466102a894a49d04ae35aa54cc1d05a58df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-to-monitor-apps-in-azure-app-service"></a><span data-ttu-id="2202a-103">Nasıl yapılır: Azure uygulama hizmetinde uygulamaları izleme</span><span class="sxs-lookup"><span data-stu-id="2202a-103">How to: Monitor Apps in Azure App Service</span></span>
<span data-ttu-id="2202a-104">[Uygulama hizmeti](http://go.microsoft.com/fwlink/?LinkId=529714) hello yerleşik izleme işlevselliği sağlayan [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="2202a-104">[App Service](http://go.microsoft.com/fwlink/?LinkId=529714) provides built in monitoring functionality in hello [Azure Portal](https://portal.azure.com).</span></span>
<span data-ttu-id="2202a-105">Bu hello özelliği tooreview içerir **kotaları** ve **ölçümleri** hello ayarlama uygulama hizmeti planı yanı sıra bir uygulama için **uyarıları** ve hatta **ölçeklendirme** bu ölçümleri göre otomatik olarak.</span><span class="sxs-lookup"><span data-stu-id="2202a-105">This includes hello ability tooreview **quotas** and **metrics** for an app as well as hello App Service plan, setting up **alerts** and even **scaling** automatically based on these metrics.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="understanding-quotas-and-metrics"></a><span data-ttu-id="2202a-106">Anlama kotalar ve ölçümleri</span><span class="sxs-lookup"><span data-stu-id="2202a-106">Understanding Quotas and Metrics</span></span>
### <a name="quotas"></a><span data-ttu-id="2202a-107">Kotalar</span><span class="sxs-lookup"><span data-stu-id="2202a-107">Quotas</span></span>
<span data-ttu-id="2202a-108">App Service içinde barındırılan konu toocertain uygulamalardır *sınırları* kullanabilecekleri kaynaklar.</span><span class="sxs-lookup"><span data-stu-id="2202a-108">Applications hosted in App Service are subject toocertain *limits* on the resources they can use.</span></span> <span data-ttu-id="2202a-109">Merhaba sınırları hello tarafından tanımlanan **uygulama hizmeti planı** hello uygulamayla ilişkili.</span><span class="sxs-lookup"><span data-stu-id="2202a-109">hello limits are defined by hello **App Service plan** associated with hello app.</span></span>

<span data-ttu-id="2202a-110">Merhaba uygulaması barındırılıyorsa bir **serbest** veya **paylaşılan** planlama hello uygulama kullanabileceğiniz hello kaynaklardaki hello sınırları tarafından tanımlanan sonra **kotaları**.</span><span class="sxs-lookup"><span data-stu-id="2202a-110">If hello application is hosted in a **Free** or **Shared** plan, then hello limits on hello resources hello app can use are defined by **Quotas**.</span></span>

<span data-ttu-id="2202a-111">Merhaba uygulaması barındırılıyorsa bir **temel**, **standart** veya **Premium** planlama hello sınırları kullanabilecekleri hello kaynaklar tarafından hello ayarlayın, sonra da **boyutu** (Küçük, Orta, büyük) ve **örnek sayısını** (1, 2, 3,...) Merhaba, **uygulama hizmeti planı**.</span><span class="sxs-lookup"><span data-stu-id="2202a-111">If hello application is hosted in a **Basic**, **Standard** or **Premium** plan, then hello limits on hello resources they can use are set by hello **size** (Small, Medium, Large) and **instance count** (1, 2, 3, ...) of hello **App Service plan**.</span></span>

<span data-ttu-id="2202a-112">**Kotalar** için **serbest** veya **paylaşılan** uygulamalar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="2202a-112">**Quotas** for **Free** or **Shared** apps are:</span></span>

* <span data-ttu-id="2202a-113">**CPU(short)**</span><span class="sxs-lookup"><span data-stu-id="2202a-113">**CPU(Short)**</span></span>
  * <span data-ttu-id="2202a-114">Bu uygulamada 5 dakikalık bir zaman aralığı için izin verilen CPU miktarı.</span><span class="sxs-lookup"><span data-stu-id="2202a-114">Amount of CPU allowed for this application in a 5-minute interval.</span></span> <span data-ttu-id="2202a-115">Bu kota her 5 dakikada bir yeniden ayarlar.</span><span class="sxs-lookup"><span data-stu-id="2202a-115">This quota re-sets every 5 minutes.</span></span>
* <span data-ttu-id="2202a-116">**CPU(Day)**</span><span class="sxs-lookup"><span data-stu-id="2202a-116">**CPU(Day)**</span></span>
  * <span data-ttu-id="2202a-117">CPU bir gün içinde bu uygulama için izin verilen toplam miktarı.</span><span class="sxs-lookup"><span data-stu-id="2202a-117">Total amount of CPU allowed for this application in a day.</span></span> <span data-ttu-id="2202a-118">Bu kota UTC gece 24 saatte yeniden ayarlar.</span><span class="sxs-lookup"><span data-stu-id="2202a-118">This quota re-sets every 24 hours at midnight UTC.</span></span>
* <span data-ttu-id="2202a-119">**Bellek**</span><span class="sxs-lookup"><span data-stu-id="2202a-119">**Memory**</span></span>
  * <span data-ttu-id="2202a-120">Bu uygulama için izin verilen bellek toplam miktarı.</span><span class="sxs-lookup"><span data-stu-id="2202a-120">Total amount of memory allowed for this application.</span></span>
* <span data-ttu-id="2202a-121">**Bant genişliği**</span><span class="sxs-lookup"><span data-stu-id="2202a-121">**Bandwidth**</span></span>
  * <span data-ttu-id="2202a-122">Giden bant genişliği bir gün içinde bu uygulama için izin verilen toplam miktarı.</span><span class="sxs-lookup"><span data-stu-id="2202a-122">Total amount of outgoing bandwidth allowed for this application in a day.</span></span>
    <span data-ttu-id="2202a-123">Bu kota UTC gece 24 saatte yeniden ayarlar.</span><span class="sxs-lookup"><span data-stu-id="2202a-123">This quota re-sets every 24 hours at midnight UTC.</span></span>
* <span data-ttu-id="2202a-124">**Dosya sistemi**</span><span class="sxs-lookup"><span data-stu-id="2202a-124">**Filesystem**</span></span>
  * <span data-ttu-id="2202a-125">İzin verilen depolama alanı toplam miktarı.</span><span class="sxs-lookup"><span data-stu-id="2202a-125">Total amount of storage allowed.</span></span>

<span data-ttu-id="2202a-126">barındırılan yalnızca kota geçerli tooapps hello **temel**, **standart** ve **Premium** planları olan **dosya sistemi**.</span><span class="sxs-lookup"><span data-stu-id="2202a-126">hello only quota applicable tooapps hosted on **Basic**, **Standard** and **Premium** plans is **Filesystem**.</span></span>

<span data-ttu-id="2202a-127">Merhaba belirli kotalar, sınırları ve farklı uygulama hizmeti SKU'ları hello kullanılabilir özellikler hakkında daha fazla bilgi şurada bulunabilir: [Azure aboneliği hizmet sınırları](../azure-subscription-service-limits.md#app-service-limits)</span><span class="sxs-lookup"><span data-stu-id="2202a-127">More information about hello specific quotas, limits and features available to hello different App Service SKUs can be found here: [Azure Subscription Service Limits](../azure-subscription-service-limits.md#app-service-limits)</span></span>

#### <a name="quota-enforcement"></a><span data-ttu-id="2202a-128">Kota zorlama</span><span class="sxs-lookup"><span data-stu-id="2202a-128">Quota Enforcement</span></span>
<span data-ttu-id="2202a-129">Kullanım uygulamada hello aşarsa **CPU (kısa)**, **CPU (gün)**, veya **bant genişliği** hello kota yeniden getirilene kadar kota sonra hello uygulama durdurulacak.</span><span class="sxs-lookup"><span data-stu-id="2202a-129">If an application in its usage exceeds hello **CPU (short)**, **CPU (Day)**, or **bandwidth** quota then hello application will be stopped until hello quota re-sets.</span></span> <span data-ttu-id="2202a-130">Tüm gelen istekleri sonuçlanır bu süre boyunca bir **HTTP 403**.</span><span class="sxs-lookup"><span data-stu-id="2202a-130">During this time, all incoming requests will result in an **HTTP 403**.</span></span>
![][http403]

<span data-ttu-id="2202a-131">Varsa hello uygulama **bellek** kota aşıldı sonra hello uygulama yeniden başlatılmasından olacaktır.</span><span class="sxs-lookup"><span data-stu-id="2202a-131">If hello application **memory** quota is exceeded, then hello application will be re-started.</span></span>

<span data-ttu-id="2202a-132">Merhaba, **Filesystem** kota aşıldı sonra herhangi bir yazma işlemi başarısız olur, bu toologs yazma içerir.</span><span class="sxs-lookup"><span data-stu-id="2202a-132">If hello **Filesystem** quota is exceeded, then any write operation will fail, this includes writing toologs.</span></span>

<span data-ttu-id="2202a-133">Kotalar artırılabilir veya uygulama hizmeti planınızı yükselterek uygulamanızdan kaldırıldı.</span><span class="sxs-lookup"><span data-stu-id="2202a-133">Quotas can be increased or removed from your app by upgrading your App Service plan.</span></span>

### <a name="metrics"></a><span data-ttu-id="2202a-134">Ölçümler</span><span class="sxs-lookup"><span data-stu-id="2202a-134">Metrics</span></span>
<span data-ttu-id="2202a-135">**Ölçümleri** hello uygulama ya da uygulama hizmeti planının davranışı hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="2202a-135">**Metrics** provide information about hello app, or App Service plan's behavior.</span></span>

<span data-ttu-id="2202a-136">İçin bir **uygulama**, hello kullanılabilir ölçümler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="2202a-136">For an **Application**, hello available metrics are:</span></span>

* <span data-ttu-id="2202a-137">**Ortalama yanıt süresi**</span><span class="sxs-lookup"><span data-stu-id="2202a-137">**Average Response Time**</span></span>
  * <span data-ttu-id="2202a-138">MS hello uygulama tooserve istekleri için geçen ortalama süre hello.</span><span class="sxs-lookup"><span data-stu-id="2202a-138">hello average time taken for hello app tooserve requests in ms.</span></span>
* <span data-ttu-id="2202a-139">**Ortalama bellek çalışma kümesi**</span><span class="sxs-lookup"><span data-stu-id="2202a-139">**Average memory working set**</span></span>
  * <span data-ttu-id="2202a-140">Merhaba ortalama MIB hello uygulama tarafından kullanılan bellek miktarı.</span><span class="sxs-lookup"><span data-stu-id="2202a-140">hello average amount of memory in MiBs used by hello app.</span></span>
* <span data-ttu-id="2202a-141">**CPU süresi**</span><span class="sxs-lookup"><span data-stu-id="2202a-141">**CPU Time**</span></span>
  * <span data-ttu-id="2202a-142">CPU miktarını Hello hello uygulama tarafından kullanılan saniye cinsinden.</span><span class="sxs-lookup"><span data-stu-id="2202a-142">hello amount of CPU in seconds consumed by hello app.</span></span> <span data-ttu-id="2202a-143">Bu ölçüm bakın hakkında daha fazla bilgi için: [CPU zamanı vs CPU yüzdesi](#cpu-time-vs-cpu-percentage)</span><span class="sxs-lookup"><span data-stu-id="2202a-143">For more information about this metric see: [CPU time vs CPU percentage](#cpu-time-vs-cpu-percentage)</span></span>
* <span data-ttu-id="2202a-144">**Verileri**</span><span class="sxs-lookup"><span data-stu-id="2202a-144">**Data In**</span></span>
  * <span data-ttu-id="2202a-145">Merhaba hello uygulamada MIB tarafından tüketilen gelen bant genişliği miktarı.</span><span class="sxs-lookup"><span data-stu-id="2202a-145">hello amount of incoming bandwidth consumed by hello app in MiBs.</span></span>
* <span data-ttu-id="2202a-146">**Giden veriler**</span><span class="sxs-lookup"><span data-stu-id="2202a-146">**Data Out**</span></span>
  * <span data-ttu-id="2202a-147">Merhaba hello uygulamada MIB tarafından tüketilen giden bant genişliği miktarı.</span><span class="sxs-lookup"><span data-stu-id="2202a-147">hello amount of outgoing bandwidth consumed by hello app in MiBs.</span></span>
* <span data-ttu-id="2202a-148">**HTTP 2xx**</span><span class="sxs-lookup"><span data-stu-id="2202a-148">**Http 2xx**</span></span>
  * <span data-ttu-id="2202a-149">Bir http durum kodunu kaynaklanan isteklerin sayısı > = 200 ancak < 300.</span><span class="sxs-lookup"><span data-stu-id="2202a-149">Count of requests resulting in a http status code >= 200 but < 300.</span></span>
* <span data-ttu-id="2202a-150">**HTTP 3xx**</span><span class="sxs-lookup"><span data-stu-id="2202a-150">**Http 3xx**</span></span>
  * <span data-ttu-id="2202a-151">Bir http durum kodunu kaynaklanan isteklerin sayısı > = 300 ancak < 400.</span><span class="sxs-lookup"><span data-stu-id="2202a-151">Count of requests resulting in a http status code >= 300 but < 400.</span></span>
* <span data-ttu-id="2202a-152">**HTTP 401**</span><span class="sxs-lookup"><span data-stu-id="2202a-152">**Http 401**</span></span>
  * <span data-ttu-id="2202a-153">HTTP 401 durum kodunu kaynaklanan isteklerin sayısı.</span><span class="sxs-lookup"><span data-stu-id="2202a-153">Count of requests resulting in HTTP 401 status code.</span></span>
* <span data-ttu-id="2202a-154">**HTTP 403**</span><span class="sxs-lookup"><span data-stu-id="2202a-154">**Http 403**</span></span>
  * <span data-ttu-id="2202a-155">HTTP 403 durum kodunu kaynaklanan isteklerin sayısı.</span><span class="sxs-lookup"><span data-stu-id="2202a-155">Count of requests resulting in HTTP 403 status code.</span></span>
* <span data-ttu-id="2202a-156">**HTTP 404**</span><span class="sxs-lookup"><span data-stu-id="2202a-156">**Http 404**</span></span>
  * <span data-ttu-id="2202a-157">HTTP 404 durum kodunu kaynaklanan isteklerin sayısı.</span><span class="sxs-lookup"><span data-stu-id="2202a-157">Count of requests resulting in HTTP 404 status code.</span></span>
* <span data-ttu-id="2202a-158">**HTTP 406**</span><span class="sxs-lookup"><span data-stu-id="2202a-158">**Http 406**</span></span>
  * <span data-ttu-id="2202a-159">HTTP 406 durum kodunu kaynaklanan isteklerin sayısı.</span><span class="sxs-lookup"><span data-stu-id="2202a-159">Count of requests resulting in HTTP 406 status code.</span></span>
* <span data-ttu-id="2202a-160">**HTTP 4xx**</span><span class="sxs-lookup"><span data-stu-id="2202a-160">**Http 4xx**</span></span>
  * <span data-ttu-id="2202a-161">Bir http durum kodunu kaynaklanan isteklerin sayısı > = 400 ancak < 500.</span><span class="sxs-lookup"><span data-stu-id="2202a-161">Count of requests resulting in a http status code >= 400 but < 500.</span></span>
* <span data-ttu-id="2202a-162">**HTTP sunucu hataları**</span><span class="sxs-lookup"><span data-stu-id="2202a-162">**Http Server Errors**</span></span>
  * <span data-ttu-id="2202a-163">Bir http durum kodunu kaynaklanan isteklerin sayısı > = 500 ancak < 600.</span><span class="sxs-lookup"><span data-stu-id="2202a-163">Count of requests resulting in a http status code >= 500 but < 600.</span></span>
* <span data-ttu-id="2202a-164">**Bellek çalışma kümesi**</span><span class="sxs-lookup"><span data-stu-id="2202a-164">**Memory working set**</span></span>
  * <span data-ttu-id="2202a-165">Geçerli hello uygulamada MIB tarafından kullanılan bellek miktarı.</span><span class="sxs-lookup"><span data-stu-id="2202a-165">Current amount of memory used by hello app in MiBs.</span></span>
* <span data-ttu-id="2202a-166">**İstekleri**</span><span class="sxs-lookup"><span data-stu-id="2202a-166">**Requests**</span></span>
  * <span data-ttu-id="2202a-167">Sonuçta elde edilen HTTP durum kodunu ne olursa olsun istekleri toplam sayısı.</span><span class="sxs-lookup"><span data-stu-id="2202a-167">Total number of requests regardless of their resulting HTTP status code.</span></span>

<span data-ttu-id="2202a-168">İçin bir **uygulama hizmeti planı**, hello kullanılabilir ölçümler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="2202a-168">For an **App Service plan**, hello available metrics are:</span></span>

> [!NOTE]
> <span data-ttu-id="2202a-169">Uygulama hizmeti planı ölçümleri planları için kullanılabilir yalnızca **temel**, **standart** ve **Premium** SKU.</span><span class="sxs-lookup"><span data-stu-id="2202a-169">App Service plan metrics are only available for plans in **Basic**, **Standard** and **Premium** SKU.</span></span>
> 
> 

* <span data-ttu-id="2202a-170">**CPU yüzdesi**</span><span class="sxs-lookup"><span data-stu-id="2202a-170">**CPU Percentage**</span></span>
  * <span data-ttu-id="2202a-171">Merhaba ortalama CPU hello planının tüm örneklerinde kullanılır.</span><span class="sxs-lookup"><span data-stu-id="2202a-171">hello average CPU used across all instances of hello plan.</span></span>
* <span data-ttu-id="2202a-172">**Bellek yüzdesi**</span><span class="sxs-lookup"><span data-stu-id="2202a-172">**Memory Percentage**</span></span>
  * <span data-ttu-id="2202a-173">Merhaba ortalama bellek hello planının tüm örneklerinde kullanılır.</span><span class="sxs-lookup"><span data-stu-id="2202a-173">hello average memory used across all instances of hello plan.</span></span>
* <span data-ttu-id="2202a-174">**Verileri**</span><span class="sxs-lookup"><span data-stu-id="2202a-174">**Data In**</span></span>
  * <span data-ttu-id="2202a-175">Merhaba planının tüm örneklerinde kullanılan hello ortalama gelen bant genişliği.</span><span class="sxs-lookup"><span data-stu-id="2202a-175">hello average incoming bandwidth used across all instances of hello plan.</span></span>
* <span data-ttu-id="2202a-176">**Giden veriler**</span><span class="sxs-lookup"><span data-stu-id="2202a-176">**Data Out**</span></span>
  * <span data-ttu-id="2202a-177">Merhaba ortalama hello planının tüm örneklerinde kullanılan bant genişliği giden.</span><span class="sxs-lookup"><span data-stu-id="2202a-177">hello average outgoing bandwidth used across all instances of hello plan.</span></span>
* <span data-ttu-id="2202a-178">**Disk Sırası Uzunluğu**</span><span class="sxs-lookup"><span data-stu-id="2202a-178">**Disk Queue Length**</span></span>
  * <span data-ttu-id="2202a-179">Merhaba ortalama sayısı okuma ve yazma depolama üzerinde sıraya alınan istekleri.</span><span class="sxs-lookup"><span data-stu-id="2202a-179">hello average number of both read and write requests that were queued on storage.</span></span> <span data-ttu-id="2202a-180">Yüksek disk sırası uzunluğu tooexcessive disk g/ç yavaşlamadan bir uygulamanın göstergesidir.</span><span class="sxs-lookup"><span data-stu-id="2202a-180">A high disk queue length is an indication of an application that might be slowing down due tooexcessive disk I/O.</span></span>
* <span data-ttu-id="2202a-181">**HTTP sırası uzunluğu**</span><span class="sxs-lookup"><span data-stu-id="2202a-181">**Http Queue Length**</span></span>
  * <span data-ttu-id="2202a-182">Merhaba ortalama yerine getirilmesini önce toosit hello sırasına olan HTTP isteği sayısı.</span><span class="sxs-lookup"><span data-stu-id="2202a-182">hello average number of HTTP requests that had toosit on hello queue before being fulfilled.</span></span> <span data-ttu-id="2202a-183">Yüksek veya artan HTTP sırası uzunluğu, yoğun yük altında bir planı belirtisidir.</span><span class="sxs-lookup"><span data-stu-id="2202a-183">A high or increasing HTTP Queue length is a symptom of a plan under heavy load.</span></span>

### <a name="cpu-time-vs-cpu-percentage"></a><span data-ttu-id="2202a-184">CPU zamanı vs CPU yüzdesi</span><span class="sxs-lookup"><span data-stu-id="2202a-184">CPU time vs CPU percentage</span></span>
<!-- toodo: Fix Anchor (#CPU-time-vs.-CPU-percentage) -->

<span data-ttu-id="2202a-185">CPU kullanımı yansıtacak 2 ölçümleri vardır.</span><span class="sxs-lookup"><span data-stu-id="2202a-185">There are 2 metrics that reflect CPU usage.</span></span> <span data-ttu-id="2202a-186">**CPU süresi** ve **CPU yüzdesi**</span><span class="sxs-lookup"><span data-stu-id="2202a-186">**CPU time** and **CPU percentage**</span></span>

<span data-ttu-id="2202a-187">**CPU süresi** barındırılan uygulamalar için yararlıdır **serbest** veya **paylaşılan** kendi kotaları birini hello uygulama tarafından kullanılan CPU dakika cinsinden tanımlanır beri planları.</span><span class="sxs-lookup"><span data-stu-id="2202a-187">**CPU Time** is useful for apps hosted in **Free** or **Shared** plans since one of their quotas is defined in CPU minutes used by hello app.</span></span>

<span data-ttu-id="2202a-188">**CPU yüzdesi** hello üzerinde barındırılan uygulamalar için diğer yandan yararlıdır **temel**, **standart** ve **premium** dışa Genişletilebilir beri planları ve bu ölçüm Merhaba iyi bir göstergesidir tüm örneklerde genel kullanım.</span><span class="sxs-lookup"><span data-stu-id="2202a-188">**CPU percentage** on hello other hand is useful for apps hosted in **basic**, **standard** and **premium** plans since they can be scaled out and this metric is a good indication of hello overall usage across all instances.</span></span>

## <a name="metrics-granularity-and-retention-policy"></a><span data-ttu-id="2202a-189">Ölçümleri ayrıntı düzeyi ve bekletme ilkesi</span><span class="sxs-lookup"><span data-stu-id="2202a-189">Metrics Granularity and Retention Policy</span></span>
<span data-ttu-id="2202a-190">Bir uygulama ve uygulama hizmeti planı ölçümleri oturum ve hello ile Merhaba hizmet tarafından toplanan ayrıntı düzeyi ve bekletme ilkeleri aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="2202a-190">Metrics for an application and app service plan are logged and aggregated by hello service with hello following granularities and retention policies:</span></span>

* <span data-ttu-id="2202a-191">**Dakika** ayrıntı düzeyi ölçümleri için korunur **48 saat**</span><span class="sxs-lookup"><span data-stu-id="2202a-191">**Minute** granularity metrics are retained for **48 hours**</span></span>
* <span data-ttu-id="2202a-192">**Saat** ayrıntı düzeyi ölçümleri için korunur **30 gün**</span><span class="sxs-lookup"><span data-stu-id="2202a-192">**Hour** granularity metrics are retained for **30 days**</span></span>
* <span data-ttu-id="2202a-193">**Gün** ayrıntı düzeyi ölçümleri için korunur **90 gün**</span><span class="sxs-lookup"><span data-stu-id="2202a-193">**Day** granularity metrics are retained for **90 days**</span></span>

## <a name="monitoring-quotas-and-metrics-in-hello-azure-portal"></a><span data-ttu-id="2202a-194">Kotalar ve ölçümleri hello Azure Portal izleme.</span><span class="sxs-lookup"><span data-stu-id="2202a-194">Monitoring Quotas and Metrics in hello Azure Portal.</span></span>
<span data-ttu-id="2202a-195">Merhaba farklı hello durumunu gözden geçirebilirsiniz **kotaları** ve **ölçümleri** hello uygulamada etkileyen [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="2202a-195">You can review hello status of hello different **quotas** and **metrics** affecting an application in hello [Azure Portal](https://portal.azure.com).</span></span>

<span data-ttu-id="2202a-196">![][quotas]
**Kotalar** ayarlar altında bulunabilir >**kotaları**.</span><span class="sxs-lookup"><span data-stu-id="2202a-196">![][quotas]
**Quotas** can be found under Settings>**Quotas**.</span></span> <span data-ttu-id="2202a-197">Merhaba UX gözden geçirmenizi sağlar: (1) hello kotaları adı, (2), sıfırlama aralığı, (3), geçerli sınırı ve (4) geçerli değeri.</span><span class="sxs-lookup"><span data-stu-id="2202a-197">hello UX allows you to review: (1) hello quotas name, (2) its reset interval, (3) its current limit and (4) current value.</span></span>

<span data-ttu-id="2202a-198">![][metrics]
**Ölçümleri** hello kaynak dikey penceresinden doğrudan erişim olabilir.</span><span class="sxs-lookup"><span data-stu-id="2202a-198">![][metrics]
**Metrics** can be access directly from hello resource blade.</span></span> <span data-ttu-id="2202a-199">Merhaba grafik tarafından da özelleştirebilirsiniz: (1) **tıklatın** ve seçin (2) üzerinde **grafiği Düzenle**.</span><span class="sxs-lookup"><span data-stu-id="2202a-199">You can also customize hello chart by: (1) **click** on it, and select (2) **edit chart**.</span></span>
<span data-ttu-id="2202a-200">Buradan hello (3) değiştirebilirsiniz **zaman aralığı**, (4) **grafik türü**ve (5) **ölçümleri** toodisplay.</span><span class="sxs-lookup"><span data-stu-id="2202a-200">From here you can change hello (3) **time range**, (4) **chart type**, and (5) **metrics** toodisplay.</span></span>  

<span data-ttu-id="2202a-201">Burada ölçümler hakkında daha fazla bilgi edinebilirsiniz: [izleme hizmeti ölçümleri](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md).</span><span class="sxs-lookup"><span data-stu-id="2202a-201">You can learn more about metrics here: [Monitor service metrics](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md).</span></span>

## <a name="alerts-and-autoscale"></a><span data-ttu-id="2202a-202">Uyarılar ve otomatik ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="2202a-202">Alerts and Autoscale</span></span>
<span data-ttu-id="2202a-203">Bir uygulama veya uygulama hizmeti planı tooalerts, toolearn bunu hakkında daha fazla yukarı bağlanabilir için ölçümlerini görmek [uyarı bildirimleri alma](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)</span><span class="sxs-lookup"><span data-stu-id="2202a-203">Metrics for an App or App Service plan can be hooked up tooalerts, toolearn more about this, see [Receive alert notifications](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)</span></span>

<span data-ttu-id="2202a-204">Basic barındırılan uygulama hizmeti uygulamalar standart veya premium App Service planları Destek **otomatik ölçeklendirme**.</span><span class="sxs-lookup"><span data-stu-id="2202a-204">App Service apps hosted in basic, standard or premium App Service Plans support **autoscale**.</span></span> <span data-ttu-id="2202a-205">Merhaba uygulaması atlayarak sağlama olduğunda bu uygulama hizmeti planı ölçümleri izleyin ve artırabilir veya gerektiği gibi ek kaynaklar sağlayarak hello örnek sayısı azaltabilirsiniz tooconfigure kuralları veya kaydetme para sağlar.</span><span class="sxs-lookup"><span data-stu-id="2202a-205">This allows you tooconfigure rules that monitor the App Service plan metrics and can increase or decrease hello instance count providing additional resources as needed, or saving money when hello application is over-provision.</span></span> <span data-ttu-id="2202a-206">Otomatik ölçek burada hakkında daha fazla bilgi edinebilirsiniz: [nasıl tooScale](../monitoring-and-diagnostics/insights-how-to-scale.md) ve burada [Azure İzleyici otomatik ölçeklendirmeyi yönelik en iyi uygulamalar](../monitoring-and-diagnostics/insights-autoscale-best-practices.md)</span><span class="sxs-lookup"><span data-stu-id="2202a-206">You can learn more about auto scale here: [How tooScale](../monitoring-and-diagnostics/insights-how-to-scale.md) and here [Best practices for Azure Monitor autoscaling](../monitoring-and-diagnostics/insights-autoscale-best-practices.md)</span></span>

> [!NOTE]
> <span data-ttu-id="2202a-207">Azure hesabı için kaydolmadan önce Azure App Service ile başlatılan tooget istiyorsanız, çok Git[App Service'i deneyin](https://azure.microsoft.com/try/app-service/), burada hemen bir kısa süreli başlangıç web uygulaması App Service'te oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2202a-207">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="2202a-208">Kredi kartı ve taahhüt gerekmez.</span><span class="sxs-lookup"><span data-stu-id="2202a-208">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="2202a-209">Yapılan değişiklikler</span><span class="sxs-lookup"><span data-stu-id="2202a-209">What's changed</span></span>
* <span data-ttu-id="2202a-210">Web siteleri tooApp hizmet değişikliği Kılavuzu toohello için bkz: [Azure App Service ve mevcut Azure hizmetlerine etkileri](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="2202a-210">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

[fzilla]:http://go.microsoft.com/fwlink/?LinkId=247914
[vmsizes]:http://go.microsoft.com/fwlink/?LinkID=309169



<!-- Images. -->
[http403]: ./media/web-sites-monitor/http403.png
[quotas]: ./media/web-sites-monitor/quotas.png
[metrics]: ./media/web-sites-monitor/metrics.png
