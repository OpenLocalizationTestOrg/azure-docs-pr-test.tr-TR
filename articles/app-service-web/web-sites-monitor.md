---
title: "Azure uygulama hizmetinde uygulamaları izleme | Microsoft Docs"
description: "Azure portalını kullanarak Azure uygulama hizmetinde uygulamaları izleme hakkında bilgi edinin."
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
ms.openlocfilehash: 25d3776920d683fffedcd8ac6ed0e84dfe875974
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-monitor-apps-in-azure-app-service"></a><span data-ttu-id="3003f-103">Nasıl yapılır: Azure uygulama hizmetinde uygulamaları izleme</span><span class="sxs-lookup"><span data-stu-id="3003f-103">How to: Monitor Apps in Azure App Service</span></span>
<span data-ttu-id="3003f-104">[Uygulama hizmeti](http://go.microsoft.com/fwlink/?LinkId=529714) yerleşik izleme işlevselliği sağlayan [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="3003f-104">[App Service](http://go.microsoft.com/fwlink/?LinkId=529714) provides built in monitoring functionality in the [Azure Portal](https://portal.azure.com).</span></span>
<span data-ttu-id="3003f-105">Bu gözden yeteneğini içerir **kotaları** ve **ölçümleri** ayarlama uygulama hizmeti planı yanı sıra, bir uygulama için **uyarıları** ve hatta **ölçeklendirme**bu ölçümleri göre otomatik olarak.</span><span class="sxs-lookup"><span data-stu-id="3003f-105">This includes the ability to review **quotas** and **metrics** for an app as well as the App Service plan, setting up **alerts** and even **scaling** automatically based on these metrics.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="understanding-quotas-and-metrics"></a><span data-ttu-id="3003f-106">Anlama kotalar ve ölçümleri</span><span class="sxs-lookup"><span data-stu-id="3003f-106">Understanding Quotas and Metrics</span></span>
### <a name="quotas"></a><span data-ttu-id="3003f-107">Kotalar</span><span class="sxs-lookup"><span data-stu-id="3003f-107">Quotas</span></span>
<span data-ttu-id="3003f-108">App Service içinde barındırılan uygulamalar belirli tabi olan *sınırları* kullanabilecekleri kaynaklar.</span><span class="sxs-lookup"><span data-stu-id="3003f-108">Applications hosted in App Service are subject to certain *limits* on the resources they can use.</span></span> <span data-ttu-id="3003f-109">Sınırları tarafından tanımlanan **uygulama hizmeti planı** uygulamayla ilişkili.</span><span class="sxs-lookup"><span data-stu-id="3003f-109">The limits are defined by the **App Service plan** associated with the app.</span></span>

<span data-ttu-id="3003f-110">Uygulama içinde barındırılıyorsa bir **serbest** veya **paylaşılan** planlama uygulama kullanabileceğiniz kaynaklar sınırları tarafından tanımlanan sonra **kotaları**.</span><span class="sxs-lookup"><span data-stu-id="3003f-110">If the application is hosted in a **Free** or **Shared** plan, then the limits on the resources the app can use are defined by **Quotas**.</span></span>

<span data-ttu-id="3003f-111">Uygulama içinde barındırılıyorsa bir **temel**, **standart** veya **Premium** planlama sınırları kullanabilecekleri kaynaklar tarafından belirlenen sonra **boyutu**(Küçük, Orta, büyük) ve **örnek sayısını** (1, 2, 3,...), **uygulama hizmeti planı**.</span><span class="sxs-lookup"><span data-stu-id="3003f-111">If the application is hosted in a **Basic**, **Standard** or **Premium** plan, then the limits on the resources they can use are set by the **size** (Small, Medium, Large) and **instance count** (1, 2, 3, ...) of the **App Service plan**.</span></span>

<span data-ttu-id="3003f-112">**Kotalar** için **serbest** veya **paylaşılan** uygulamalar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="3003f-112">**Quotas** for **Free** or **Shared** apps are:</span></span>

* <span data-ttu-id="3003f-113">**CPU(short)**</span><span class="sxs-lookup"><span data-stu-id="3003f-113">**CPU(Short)**</span></span>
  * <span data-ttu-id="3003f-114">Bu uygulamada 5 dakikalık bir zaman aralığı için izin verilen CPU miktarı.</span><span class="sxs-lookup"><span data-stu-id="3003f-114">Amount of CPU allowed for this application in a 5-minute interval.</span></span> <span data-ttu-id="3003f-115">Bu kota her 5 dakikada bir yeniden ayarlar.</span><span class="sxs-lookup"><span data-stu-id="3003f-115">This quota re-sets every 5 minutes.</span></span>
* <span data-ttu-id="3003f-116">**CPU(Day)**</span><span class="sxs-lookup"><span data-stu-id="3003f-116">**CPU(Day)**</span></span>
  * <span data-ttu-id="3003f-117">CPU bir gün içinde bu uygulama için izin verilen toplam miktarı.</span><span class="sxs-lookup"><span data-stu-id="3003f-117">Total amount of CPU allowed for this application in a day.</span></span> <span data-ttu-id="3003f-118">Bu kota UTC gece 24 saatte yeniden ayarlar.</span><span class="sxs-lookup"><span data-stu-id="3003f-118">This quota re-sets every 24 hours at midnight UTC.</span></span>
* <span data-ttu-id="3003f-119">**Bellek**</span><span class="sxs-lookup"><span data-stu-id="3003f-119">**Memory**</span></span>
  * <span data-ttu-id="3003f-120">Bu uygulama için izin verilen bellek toplam miktarı.</span><span class="sxs-lookup"><span data-stu-id="3003f-120">Total amount of memory allowed for this application.</span></span>
* <span data-ttu-id="3003f-121">**Bant genişliği**</span><span class="sxs-lookup"><span data-stu-id="3003f-121">**Bandwidth**</span></span>
  * <span data-ttu-id="3003f-122">Giden bant genişliği bir gün içinde bu uygulama için izin verilen toplam miktarı.</span><span class="sxs-lookup"><span data-stu-id="3003f-122">Total amount of outgoing bandwidth allowed for this application in a day.</span></span>
    <span data-ttu-id="3003f-123">Bu kota UTC gece 24 saatte yeniden ayarlar.</span><span class="sxs-lookup"><span data-stu-id="3003f-123">This quota re-sets every 24 hours at midnight UTC.</span></span>
* <span data-ttu-id="3003f-124">**Dosya sistemi**</span><span class="sxs-lookup"><span data-stu-id="3003f-124">**Filesystem**</span></span>
  * <span data-ttu-id="3003f-125">İzin verilen depolama alanı toplam miktarı.</span><span class="sxs-lookup"><span data-stu-id="3003f-125">Total amount of storage allowed.</span></span>

<span data-ttu-id="3003f-126">Üzerinde barındırılan uygulamalar için geçerli tek kota **temel**, **standart** ve **Premium** planları olan **dosya sistemi**.</span><span class="sxs-lookup"><span data-stu-id="3003f-126">The only quota applicable to apps hosted on **Basic**, **Standard** and **Premium** plans is **Filesystem**.</span></span>

<span data-ttu-id="3003f-127">Özel kotalar, sınırları ve farklı uygulama hizmeti SKU'ları için kullanılabilen özellikleri hakkında daha fazla bilgi şurada bulunabilir: [Azure aboneliği hizmet sınırları](../azure-subscription-service-limits.md#app-service-limits)</span><span class="sxs-lookup"><span data-stu-id="3003f-127">More information about the specific quotas, limits and features available to the different App Service SKUs can be found here: [Azure Subscription Service Limits](../azure-subscription-service-limits.md#app-service-limits)</span></span>

#### <a name="quota-enforcement"></a><span data-ttu-id="3003f-128">Kota zorlama</span><span class="sxs-lookup"><span data-stu-id="3003f-128">Quota Enforcement</span></span>
<span data-ttu-id="3003f-129">Kullanım uygulamada aşarsa **CPU (kısa)**, **CPU (gün)**, veya **bant genişliği** kota sonra uygulama durdurulacak kota yeniden getirilene kadar.</span><span class="sxs-lookup"><span data-stu-id="3003f-129">If an application in its usage exceeds the **CPU (short)**, **CPU (Day)**, or **bandwidth** quota then the application will be stopped until the quota re-sets.</span></span> <span data-ttu-id="3003f-130">Tüm gelen istekleri sonuçlanır bu süre boyunca bir **HTTP 403**.</span><span class="sxs-lookup"><span data-stu-id="3003f-130">During this time, all incoming requests will result in an **HTTP 403**.</span></span>
![][http403]

<span data-ttu-id="3003f-131">Uygulama **bellek** kota aşıldı sonra uygulamayı yeniden başlatılmasından olacaktır.</span><span class="sxs-lookup"><span data-stu-id="3003f-131">If the application **memory** quota is exceeded, then the application will be re-started.</span></span>

<span data-ttu-id="3003f-132">Varsa **Filesystem** kota aşıldı sonra herhangi bir yazma işlemi başarısız olur, bu günlükleri yazılmasını içerir.</span><span class="sxs-lookup"><span data-stu-id="3003f-132">If the **Filesystem** quota is exceeded, then any write operation will fail, this includes writing to logs.</span></span>

<span data-ttu-id="3003f-133">Kotalar artırılabilir veya uygulama hizmeti planınızı yükselterek uygulamanızdan kaldırıldı.</span><span class="sxs-lookup"><span data-stu-id="3003f-133">Quotas can be increased or removed from your app by upgrading your App Service plan.</span></span>

### <a name="metrics"></a><span data-ttu-id="3003f-134">Ölçümler</span><span class="sxs-lookup"><span data-stu-id="3003f-134">Metrics</span></span>
<span data-ttu-id="3003f-135">**Ölçümleri** uygulama veya App Service planının davranışı hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="3003f-135">**Metrics** provide information about the app, or App Service plan's behavior.</span></span>

<span data-ttu-id="3003f-136">İçin bir **uygulama**, kullanılabilir ölçümler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="3003f-136">For an **Application**, the available metrics are:</span></span>

* <span data-ttu-id="3003f-137">**Ortalama yanıt süresi**</span><span class="sxs-lookup"><span data-stu-id="3003f-137">**Average Response Time**</span></span>
  * <span data-ttu-id="3003f-138">Milisaniye olarak isteklere hizmet uygulaması için geçen ortalama süre.</span><span class="sxs-lookup"><span data-stu-id="3003f-138">The average time taken for the app to serve requests in ms.</span></span>
* <span data-ttu-id="3003f-139">**Ortalama bellek çalışma kümesi**</span><span class="sxs-lookup"><span data-stu-id="3003f-139">**Average memory working set**</span></span>
  * <span data-ttu-id="3003f-140">Uygulama tarafından kullanılan MIB bellekte ortalama miktarı.</span><span class="sxs-lookup"><span data-stu-id="3003f-140">The average amount of memory in MiBs used by the app.</span></span>
* <span data-ttu-id="3003f-141">**CPU süresi**</span><span class="sxs-lookup"><span data-stu-id="3003f-141">**CPU Time**</span></span>
  * <span data-ttu-id="3003f-142">CPU miktarını uygulama tarafından kullanılan saniye cinsinden.</span><span class="sxs-lookup"><span data-stu-id="3003f-142">The amount of CPU in seconds consumed by the app.</span></span> <span data-ttu-id="3003f-143">Bu ölçüm bakın hakkında daha fazla bilgi için: [CPU zamanı vs CPU yüzdesi](#cpu-time-vs-cpu-percentage)</span><span class="sxs-lookup"><span data-stu-id="3003f-143">For more information about this metric see: [CPU time vs CPU percentage](#cpu-time-vs-cpu-percentage)</span></span>
* <span data-ttu-id="3003f-144">**Verileri**</span><span class="sxs-lookup"><span data-stu-id="3003f-144">**Data In**</span></span>
  * <span data-ttu-id="3003f-145">MIB uygulamada tarafından tüketilen gelen bant genişliği miktarı.</span><span class="sxs-lookup"><span data-stu-id="3003f-145">The amount of incoming bandwidth consumed by the app in MiBs.</span></span>
* <span data-ttu-id="3003f-146">**Giden veriler**</span><span class="sxs-lookup"><span data-stu-id="3003f-146">**Data Out**</span></span>
  * <span data-ttu-id="3003f-147">MIB uygulamada tarafından tüketilen giden bant genişliği miktarı.</span><span class="sxs-lookup"><span data-stu-id="3003f-147">The amount of outgoing bandwidth consumed by the app in MiBs.</span></span>
* <span data-ttu-id="3003f-148">**HTTP 2xx**</span><span class="sxs-lookup"><span data-stu-id="3003f-148">**Http 2xx**</span></span>
  * <span data-ttu-id="3003f-149">Bir http durum kodunu kaynaklanan isteklerin sayısı > = 200 ancak < 300.</span><span class="sxs-lookup"><span data-stu-id="3003f-149">Count of requests resulting in a http status code >= 200 but < 300.</span></span>
* <span data-ttu-id="3003f-150">**HTTP 3xx**</span><span class="sxs-lookup"><span data-stu-id="3003f-150">**Http 3xx**</span></span>
  * <span data-ttu-id="3003f-151">Bir http durum kodunu kaynaklanan isteklerin sayısı > = 300 ancak < 400.</span><span class="sxs-lookup"><span data-stu-id="3003f-151">Count of requests resulting in a http status code >= 300 but < 400.</span></span>
* <span data-ttu-id="3003f-152">**HTTP 401**</span><span class="sxs-lookup"><span data-stu-id="3003f-152">**Http 401**</span></span>
  * <span data-ttu-id="3003f-153">HTTP 401 durum kodunu kaynaklanan isteklerin sayısı.</span><span class="sxs-lookup"><span data-stu-id="3003f-153">Count of requests resulting in HTTP 401 status code.</span></span>
* <span data-ttu-id="3003f-154">**HTTP 403**</span><span class="sxs-lookup"><span data-stu-id="3003f-154">**Http 403**</span></span>
  * <span data-ttu-id="3003f-155">HTTP 403 durum kodunu kaynaklanan isteklerin sayısı.</span><span class="sxs-lookup"><span data-stu-id="3003f-155">Count of requests resulting in HTTP 403 status code.</span></span>
* <span data-ttu-id="3003f-156">**HTTP 404**</span><span class="sxs-lookup"><span data-stu-id="3003f-156">**Http 404**</span></span>
  * <span data-ttu-id="3003f-157">HTTP 404 durum kodunu kaynaklanan isteklerin sayısı.</span><span class="sxs-lookup"><span data-stu-id="3003f-157">Count of requests resulting in HTTP 404 status code.</span></span>
* <span data-ttu-id="3003f-158">**HTTP 406**</span><span class="sxs-lookup"><span data-stu-id="3003f-158">**Http 406**</span></span>
  * <span data-ttu-id="3003f-159">HTTP 406 durum kodunu kaynaklanan isteklerin sayısı.</span><span class="sxs-lookup"><span data-stu-id="3003f-159">Count of requests resulting in HTTP 406 status code.</span></span>
* <span data-ttu-id="3003f-160">**HTTP 4xx**</span><span class="sxs-lookup"><span data-stu-id="3003f-160">**Http 4xx**</span></span>
  * <span data-ttu-id="3003f-161">Bir http durum kodunu kaynaklanan isteklerin sayısı > = 400 ancak < 500.</span><span class="sxs-lookup"><span data-stu-id="3003f-161">Count of requests resulting in a http status code >= 400 but < 500.</span></span>
* <span data-ttu-id="3003f-162">**HTTP sunucu hataları**</span><span class="sxs-lookup"><span data-stu-id="3003f-162">**Http Server Errors**</span></span>
  * <span data-ttu-id="3003f-163">Bir http durum kodunu kaynaklanan isteklerin sayısı > = 500 ancak < 600.</span><span class="sxs-lookup"><span data-stu-id="3003f-163">Count of requests resulting in a http status code >= 500 but < 600.</span></span>
* <span data-ttu-id="3003f-164">**Bellek çalışma kümesi**</span><span class="sxs-lookup"><span data-stu-id="3003f-164">**Memory working set**</span></span>
  * <span data-ttu-id="3003f-165">Geçerli MIB uygulama tarafından kullanılan bellek miktarı.</span><span class="sxs-lookup"><span data-stu-id="3003f-165">Current amount of memory used by the app in MiBs.</span></span>
* <span data-ttu-id="3003f-166">**İstekleri**</span><span class="sxs-lookup"><span data-stu-id="3003f-166">**Requests**</span></span>
  * <span data-ttu-id="3003f-167">Sonuçta elde edilen HTTP durum kodunu ne olursa olsun istekleri toplam sayısı.</span><span class="sxs-lookup"><span data-stu-id="3003f-167">Total number of requests regardless of their resulting HTTP status code.</span></span>

<span data-ttu-id="3003f-168">İçin bir **uygulama hizmeti planı**, kullanılabilir ölçümler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="3003f-168">For an **App Service plan**, the available metrics are:</span></span>

> [!NOTE]
> <span data-ttu-id="3003f-169">Uygulama hizmeti planı ölçümleri planları için kullanılabilir yalnızca **temel**, **standart** ve **Premium** SKU.</span><span class="sxs-lookup"><span data-stu-id="3003f-169">App Service plan metrics are only available for plans in **Basic**, **Standard** and **Premium** SKU.</span></span>
> 
> 

* <span data-ttu-id="3003f-170">**CPU yüzdesi**</span><span class="sxs-lookup"><span data-stu-id="3003f-170">**CPU Percentage**</span></span>
  * <span data-ttu-id="3003f-171">Planın tüm örneklerde kullanılan ortalama CPU.</span><span class="sxs-lookup"><span data-stu-id="3003f-171">The average CPU used across all instances of the plan.</span></span>
* <span data-ttu-id="3003f-172">**Bellek yüzdesi**</span><span class="sxs-lookup"><span data-stu-id="3003f-172">**Memory Percentage**</span></span>
  * <span data-ttu-id="3003f-173">Planın tüm örneklerde kullanılan ortalama bellek.</span><span class="sxs-lookup"><span data-stu-id="3003f-173">The average memory used across all instances of the plan.</span></span>
* <span data-ttu-id="3003f-174">**Verileri**</span><span class="sxs-lookup"><span data-stu-id="3003f-174">**Data In**</span></span>
  * <span data-ttu-id="3003f-175">Planın tüm örneklerde kullanılan ortalama gelen bant genişliği.</span><span class="sxs-lookup"><span data-stu-id="3003f-175">The average incoming bandwidth used across all instances of the plan.</span></span>
* <span data-ttu-id="3003f-176">**Giden veriler**</span><span class="sxs-lookup"><span data-stu-id="3003f-176">**Data Out**</span></span>
  * <span data-ttu-id="3003f-177">Planın tüm örneklerde kullanılan bant genişliği giden ortalama.</span><span class="sxs-lookup"><span data-stu-id="3003f-177">The average outgoing bandwidth used across all instances of the plan.</span></span>
* <span data-ttu-id="3003f-178">**Disk Sırası Uzunluğu**</span><span class="sxs-lookup"><span data-stu-id="3003f-178">**Disk Queue Length**</span></span>
  * <span data-ttu-id="3003f-179">Ortalama sayısı okuma ve yazma depolama üzerinde sıraya alınan istekleri.</span><span class="sxs-lookup"><span data-stu-id="3003f-179">The average number of both read and write requests that were queued on storage.</span></span> <span data-ttu-id="3003f-180">Yüksek disk sırası uzunluğu aşırı disk g/ç nedeniyle yavaşlamadan bir uygulamanın göstergesidir.</span><span class="sxs-lookup"><span data-stu-id="3003f-180">A high disk queue length is an indication of an application that might be slowing down due to excessive disk I/O.</span></span>
* <span data-ttu-id="3003f-181">**HTTP sırası uzunluğu**</span><span class="sxs-lookup"><span data-stu-id="3003f-181">**Http Queue Length**</span></span>
  * <span data-ttu-id="3003f-182">Yerine getirilmesini önce sıraya sit gerekiyordu HTTP isteklerinin ortalama sayısı.</span><span class="sxs-lookup"><span data-stu-id="3003f-182">The average number of HTTP requests that had to sit on the queue before being fulfilled.</span></span> <span data-ttu-id="3003f-183">Yüksek veya artan HTTP sırası uzunluğu, yoğun yük altında bir planı belirtisidir.</span><span class="sxs-lookup"><span data-stu-id="3003f-183">A high or increasing HTTP Queue length is a symptom of a plan under heavy load.</span></span>

### <a name="cpu-time-vs-cpu-percentage"></a><span data-ttu-id="3003f-184">CPU zamanı vs CPU yüzdesi</span><span class="sxs-lookup"><span data-stu-id="3003f-184">CPU time vs CPU percentage</span></span>
<!-- To do: Fix Anchor (#CPU-time-vs.-CPU-percentage) -->

<span data-ttu-id="3003f-185">CPU kullanımı yansıtacak 2 ölçümleri vardır.</span><span class="sxs-lookup"><span data-stu-id="3003f-185">There are 2 metrics that reflect CPU usage.</span></span> <span data-ttu-id="3003f-186">**CPU süresi** ve **CPU yüzdesi**</span><span class="sxs-lookup"><span data-stu-id="3003f-186">**CPU time** and **CPU percentage**</span></span>

<span data-ttu-id="3003f-187">**CPU süresi** barındırılan uygulamalar için yararlıdır **serbest** veya **paylaşılan** kendi kotaları birini uygulama tarafından kullanılan CPU dakika cinsinden tanımlanır beri planları.</span><span class="sxs-lookup"><span data-stu-id="3003f-187">**CPU Time** is useful for apps hosted in **Free** or **Shared** plans since one of their quotas is defined in CPU minutes used by the app.</span></span>

<span data-ttu-id="3003f-188">**CPU yüzdesi** barındırılan uygulamalar için diğer yandan yararlıdır **temel**, **standart** ve **premium** dışa genişletilebilir ve bu ölçüm olduğundan planları bir Genel kullanım tüm örneklerde göstergesidir.</span><span class="sxs-lookup"><span data-stu-id="3003f-188">**CPU percentage** on the other hand is useful for apps hosted in **basic**, **standard** and **premium** plans since they can be scaled out and this metric is a good indication of the overall usage across all instances.</span></span>

## <a name="metrics-granularity-and-retention-policy"></a><span data-ttu-id="3003f-189">Ölçümleri ayrıntı düzeyi ve bekletme ilkesi</span><span class="sxs-lookup"><span data-stu-id="3003f-189">Metrics Granularity and Retention Policy</span></span>
<span data-ttu-id="3003f-190">Bir uygulama ve uygulama hizmeti planı ölçümleri oturum ve aşağıdaki ayrıntı düzeyi ve bekletme ilkeleri hizmet tarafından toplanan:</span><span class="sxs-lookup"><span data-stu-id="3003f-190">Metrics for an application and app service plan are logged and aggregated by the service with the following granularities and retention policies:</span></span>

* <span data-ttu-id="3003f-191">**Dakika** ayrıntı düzeyi ölçümleri için korunur **48 saat**</span><span class="sxs-lookup"><span data-stu-id="3003f-191">**Minute** granularity metrics are retained for **48 hours**</span></span>
* <span data-ttu-id="3003f-192">**Saat** ayrıntı düzeyi ölçümleri için korunur **30 gün**</span><span class="sxs-lookup"><span data-stu-id="3003f-192">**Hour** granularity metrics are retained for **30 days**</span></span>
* <span data-ttu-id="3003f-193">**Gün** ayrıntı düzeyi ölçümleri için korunur **90 gün**</span><span class="sxs-lookup"><span data-stu-id="3003f-193">**Day** granularity metrics are retained for **90 days**</span></span>

## <a name="monitoring-quotas-and-metrics-in-the-azure-portal"></a><span data-ttu-id="3003f-194">Kotalar ve Azure portalında ölçümleri izleme.</span><span class="sxs-lookup"><span data-stu-id="3003f-194">Monitoring Quotas and Metrics in the Azure Portal.</span></span>
<span data-ttu-id="3003f-195">Farklı durumunu gözden geçirebilirsiniz **kotaları** ve **ölçümleri** bir uygulamada etkileyen [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="3003f-195">You can review the status of the different **quotas** and **metrics** affecting an application in the [Azure Portal](https://portal.azure.com).</span></span>

<span data-ttu-id="3003f-196">![][quotas]
**Kotalar** ayarlar altında bulunabilir >**kotaları**.</span><span class="sxs-lookup"><span data-stu-id="3003f-196">![][quotas]
**Quotas** can be found under Settings>**Quotas**.</span></span> <span data-ttu-id="3003f-197">UX gözden geçirmenizi sağlar: (1 kotaları adı, (2), sıfırlama aralığı, (3), geçerli sınırı ve (4) geçerli değeri.</span><span class="sxs-lookup"><span data-stu-id="3003f-197">The UX allows you to review: (1) the quotas name, (2) its reset interval, (3) its current limit and (4) current value.</span></span>

<span data-ttu-id="3003f-198">![][metrics]
**Ölçümleri** kaynak dikey penceresinden doğrudan erişim olabilir.</span><span class="sxs-lookup"><span data-stu-id="3003f-198">![][metrics]
**Metrics** can be access directly from the resource blade.</span></span> <span data-ttu-id="3003f-199">Grafik tarafından da özelleştirebilirsiniz: (1) **tıklatın** ve seçin (2) üzerinde **grafiği Düzenle**.</span><span class="sxs-lookup"><span data-stu-id="3003f-199">You can also customize the chart by: (1) **click** on it, and select (2) **edit chart**.</span></span>
<span data-ttu-id="3003f-200">Buradan, (3) değiştirebilirsiniz **zaman aralığı**, (4) **grafik türü**ve (5) **ölçümleri** görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="3003f-200">From here you can change the (3) **time range**, (4) **chart type**, and (5) **metrics** to display.</span></span>  

<span data-ttu-id="3003f-201">Burada ölçümler hakkında daha fazla bilgi edinebilirsiniz: [izleme hizmeti ölçümleri](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md).</span><span class="sxs-lookup"><span data-stu-id="3003f-201">You can learn more about metrics here: [Monitor service metrics](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md).</span></span>

## <a name="alerts-and-autoscale"></a><span data-ttu-id="3003f-202">Uyarılar ve otomatik ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="3003f-202">Alerts and Autoscale</span></span>
<span data-ttu-id="3003f-203">Bu hakkında daha fazla bilgi edinmek için bir uygulama veya uygulama hizmeti planı uyarılar için bağlanabilir için ölçümlerini görmek [uyarı bildirimleri alma](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)</span><span class="sxs-lookup"><span data-stu-id="3003f-203">Metrics for an App or App Service plan can be hooked up to alerts, to learn more about this, see [Receive alert notifications](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)</span></span>

<span data-ttu-id="3003f-204">Basic barındırılan uygulama hizmeti uygulamalar standart veya premium App Service planları Destek **otomatik ölçeklendirme**.</span><span class="sxs-lookup"><span data-stu-id="3003f-204">App Service apps hosted in basic, standard or premium App Service Plans support **autoscale**.</span></span> <span data-ttu-id="3003f-205">Uygulama fazla sağlama ise, uygulama hizmeti planı ölçümleri izleyin ve artırabilir veya gerektiği gibi ek kaynaklar sağlayan örnek sayısı azaltabilirsiniz kuralları yapılandırın veya kaydetme para sağlar.</span><span class="sxs-lookup"><span data-stu-id="3003f-205">This allows you to configure rules that monitor the App Service plan metrics and can increase or decrease the instance count providing additional resources as needed, or saving money when the application is over-provision.</span></span> <span data-ttu-id="3003f-206">Otomatik ölçek burada hakkında daha fazla bilgi edinebilirsiniz: [ölçek nasıl](../monitoring-and-diagnostics/insights-how-to-scale.md) ve burada [Azure İzleyici otomatik ölçeklendirmeyi yönelik en iyi uygulamalar](../monitoring-and-diagnostics/insights-autoscale-best-practices.md)</span><span class="sxs-lookup"><span data-stu-id="3003f-206">You can learn more about auto scale here: [How to Scale](../monitoring-and-diagnostics/insights-how-to-scale.md) and here [Best practices for Azure Monitor autoscaling](../monitoring-and-diagnostics/insights-autoscale-best-practices.md)</span></span>

> [!NOTE]
> <span data-ttu-id="3003f-207">Azure hesabı için kaydolmadan önce Azure App Service’i kullanmaya başlamak isterseniz, App Service’te hemen kısa süreli bir başlangıç web uygulaması oluşturabileceğiniz [App Service’i Deneyin](https://azure.microsoft.com/try/app-service/) sayfasına gidin.</span><span class="sxs-lookup"><span data-stu-id="3003f-207">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="3003f-208">Kredi kartı ve taahhüt gerekmez.</span><span class="sxs-lookup"><span data-stu-id="3003f-208">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="3003f-209">Yapılan değişiklikler</span><span class="sxs-lookup"><span data-stu-id="3003f-209">What's changed</span></span>
* <span data-ttu-id="3003f-210">Web Sitelerinden App Service’e kadar değiştirme kılavuzu için bkz. [Azure App Service ve Mevcut Azure Hizmetlerine Etkileri](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="3003f-210">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

[fzilla]:http://go.microsoft.com/fwlink/?LinkId=247914
[vmsizes]:http://go.microsoft.com/fwlink/?LinkID=309169



<!-- Images. -->
[http403]: ./media/web-sites-monitor/http403.png
[quotas]: ./media/web-sites-monitor/quotas.png
[metrics]: ./media/web-sites-monitor/metrics.png
