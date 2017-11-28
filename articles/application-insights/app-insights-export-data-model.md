---
title: "aaaAzure uygulama Öngörüler veri modeli | Microsoft Docs"
description: "JSON içinde sürekli dışarı aktarılmış ve filtre olarak kullanılan özellikleri tanımlar."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: cabad41c-0518-4669-887f-3087aef865ea
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/21/2016
ms.author: bwren
ms.openlocfilehash: 5ff3ce7953b91cc69b5d96c0ea9b6d58a6016e61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-export-data-model"></a><span data-ttu-id="b18d5-103">Uygulama Öngörüler dışarı aktarma veri modeli</span><span class="sxs-lookup"><span data-stu-id="b18d5-103">Application Insights Export Data Model</span></span>
<span data-ttu-id="b18d5-104">Hello gönderilen telemetri hello özelliklerini bu tabloda [Application Insights](app-insights-overview.md) SDK'ları toohello portal.</span><span class="sxs-lookup"><span data-stu-id="b18d5-104">This table lists hello properties of telemetry sent from hello [Application Insights](app-insights-overview.md) SDKs toohello portal.</span></span>
<span data-ttu-id="b18d5-105">Bu özellikler, veri çıkışı görürsünüz [sürekli verme](app-insights-export-telemetry.md).</span><span class="sxs-lookup"><span data-stu-id="b18d5-105">You'll see these properties in data output from [Continuous Export](app-insights-export-telemetry.md).</span></span>
<span data-ttu-id="b18d5-106">Ayrıca özellik filtrelerini görüntülendikleri [ölçüm Gezgini](app-insights-metrics-explorer.md) ve [tanılama arama](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="b18d5-106">They also appear in property filters in [Metric Explorer](app-insights-metrics-explorer.md) and [Diagnostic Search](app-insights-diagnostic-search.md).</span></span>

<span data-ttu-id="b18d5-107">Noktaları toonote:</span><span class="sxs-lookup"><span data-stu-id="b18d5-107">Points toonote:</span></span>

* <span data-ttu-id="b18d5-108">`[0]`Bu tablolarda hello yolda bir dizin tooinsert sahip olduğu bir noktası gösterir; ancak her zaman değil 0.</span><span class="sxs-lookup"><span data-stu-id="b18d5-108">`[0]` in these tables denotes a point in hello path where you have tooinsert an index; but it isn't always 0.</span></span>
* <span data-ttu-id="b18d5-109">Süreler milisaniyeye, bu nedenle 10000000 onda içinde olan 1 saniye ==.</span><span class="sxs-lookup"><span data-stu-id="b18d5-109">Time durations are in tenths of a microsecond, so 10000000 == 1 second.</span></span>
* <span data-ttu-id="b18d5-110">Tarihler ve saatler UTC olan ve hello ISO biçiminde verilir.`yyyy-MM-DDThh:mm:ss.sssZ`</span><span class="sxs-lookup"><span data-stu-id="b18d5-110">Dates and times are UTC, and are given in hello ISO format `yyyy-MM-DDThh:mm:ss.sssZ`</span></span>


## <a name="example"></a><span data-ttu-id="b18d5-111">Örnek</span><span class="sxs-lookup"><span data-stu-id="b18d5-111">Example</span></span>
    // A server report about an HTTP request
    {
    "request": [
      {
        "urlData": { // derived from 'url'
          "host": "contoso.org",
          "base": "/",
          "hashTag": ""
        },
        "responseCode": 200, // Sent tooclient
        "success": true, // Default == responseCode<400
        // Request id becomes hello operation id of child events
        "id": "fCOhCdCnZ9I=",  
        "name": "GET Home/Index",
        "count": 1, // 100% / sampling rate
        "durationMetric": {
          "value": 1046804.0, // 10000000 == 1 second
          // Currently hello following fields are redundant:
          "count": 1.0,
          "min": 1046804.0,
          "max": 1046804.0,
          "stdDev": 0.0,
          "sampledValue": 1046804.0
        },
        "url": "/"
      }
    ],
    "internal": {
      "data": {
        "id": "7f156650-ef4c-11e5-8453-3f984b167d05",
        "documentVersion": "1.61"
      }
    },
    "context": {
      "device": { // client browser
        "type": "PC",
        "screenResolution": { },
        "roleInstance": "WFWEB14B.fabrikam.net"
      },
      "application": { },
      "location": { // derived from client ip
        "continent": "North America",
        "country": "United States",
        // last octagon is anonymized too0 at portal:
        "clientip": "168.62.177.0",
        "province": "",
        "city": ""
      },
      "data": {
        "isSynthetic": true, // we identified source as a bot
        // percentage of generated data sent tooportal:
        "samplingRate": 100.0,
        "eventTime": "2016-03-21T10:05:45.7334717Z" // UTC
      },
      "user": {
        "isAuthenticated": false,
        "anonId": "us-tx-sn1-azr", // bot agent id
        "anonAcquisitionDate": "0001-01-01T00:00:00Z",
        "authAcquisitionDate": "0001-01-01T00:00:00Z",
        "accountAcquisitionDate": "0001-01-01T00:00:00Z"
      },
      "operation": {
        "id": "fCOhCdCnZ9I=",
        "parentId": "fCOhCdCnZ9I=",
        "name": "GET Home/Index"
      },
      "cloud": { },
      "serverDevice": { },
      "custom": { // set by custom fields of track calls
        "dimensions": [ ],
        "metrics": [ ]
      },
      "session": {
        "id": "65504c10-44a6-489e-b9dc-94184eb00d86",
        "isFirst": true
      }
    }
  <span data-ttu-id="b18d5-112">}</span><span class="sxs-lookup"><span data-stu-id="b18d5-112">}</span></span>

## <a name="context"></a><span data-ttu-id="b18d5-113">Bağlam</span><span class="sxs-lookup"><span data-stu-id="b18d5-113">Context</span></span>
<span data-ttu-id="b18d5-114">Tüm telemetri türlerini içerik bölümü tarafından yayımlanır.</span><span class="sxs-lookup"><span data-stu-id="b18d5-114">All types of telemetry are accompanied by a context section.</span></span> <span data-ttu-id="b18d5-115">Bu alanların tümünü her veri noktası ile aktarılır.</span><span class="sxs-lookup"><span data-stu-id="b18d5-115">Not all of these fields are transmitted with every data point.</span></span>

| <span data-ttu-id="b18d5-116">Yol</span><span class="sxs-lookup"><span data-stu-id="b18d5-116">Path</span></span> | <span data-ttu-id="b18d5-117">Tür</span><span class="sxs-lookup"><span data-stu-id="b18d5-117">Type</span></span> | <span data-ttu-id="b18d5-118">Notlar</span><span class="sxs-lookup"><span data-stu-id="b18d5-118">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b18d5-119">Context.Custom.Dimensions [0]</span><span class="sxs-lookup"><span data-stu-id="b18d5-119">context.custom.dimensions [0]</span></span> |<span data-ttu-id="b18d5-120">Nesne]</span><span class="sxs-lookup"><span data-stu-id="b18d5-120">object [ ]</span></span> |<span data-ttu-id="b18d5-121">Anahtar-değer çiftleri özel özellikler parametresiyle ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="b18d5-121">Key-value string pairs set by custom properties parameter.</span></span> <span data-ttu-id="b18d5-122">Anahtar uzunluğu en fazla 100, en fazla uzunluğu 1024 değerleri.</span><span class="sxs-lookup"><span data-stu-id="b18d5-122">Key max length 100, values max length 1024.</span></span> <span data-ttu-id="b18d5-123">100'den fazla benzersiz değer hello özelliği aranabilecek ancak kesimleme kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="b18d5-123">More than 100 unique values, hello property can be searched but cannot be used for segmentation.</span></span> <span data-ttu-id="b18d5-124">İkey başına en fazla 200 anahtarları.</span><span class="sxs-lookup"><span data-stu-id="b18d5-124">Max 200 keys per ikey.</span></span> |
| <span data-ttu-id="b18d5-125">Context.Custom.Metrics [0]</span><span class="sxs-lookup"><span data-stu-id="b18d5-125">context.custom.metrics [0]</span></span> |<span data-ttu-id="b18d5-126">Nesne]</span><span class="sxs-lookup"><span data-stu-id="b18d5-126">object [ ]</span></span> |<span data-ttu-id="b18d5-127">Anahtar-değer çiftleri TrackMetrics ve özel ölçümleri parametresi tarafından ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="b18d5-127">Key-value pairs set by custom measurements parameter and by TrackMetrics.</span></span> <span data-ttu-id="b18d5-128">Anahtar en büyük uzunluğunu 100 değerleri sayısal olabilir.</span><span class="sxs-lookup"><span data-stu-id="b18d5-128">Key max length 100, values may be numeric.</span></span> |
| <span data-ttu-id="b18d5-129">context.data.eventTime</span><span class="sxs-lookup"><span data-stu-id="b18d5-129">context.data.eventTime</span></span> |<span data-ttu-id="b18d5-130">Dize</span><span class="sxs-lookup"><span data-stu-id="b18d5-130">string</span></span> |<span data-ttu-id="b18d5-131">UTC</span><span class="sxs-lookup"><span data-stu-id="b18d5-131">UTC</span></span> |
| <span data-ttu-id="b18d5-132">context.data.isSynthetic</span><span class="sxs-lookup"><span data-stu-id="b18d5-132">context.data.isSynthetic</span></span> |<span data-ttu-id="b18d5-133">Boole değeri</span><span class="sxs-lookup"><span data-stu-id="b18d5-133">boolean</span></span> |<span data-ttu-id="b18d5-134">İstek bir bot veya web testi toocome görünür.</span><span class="sxs-lookup"><span data-stu-id="b18d5-134">Request appears toocome from a bot or web test.</span></span> |
| <span data-ttu-id="b18d5-135">context.data.samplingRate</span><span class="sxs-lookup"><span data-stu-id="b18d5-135">context.data.samplingRate</span></span> |<span data-ttu-id="b18d5-136">Sayı</span><span class="sxs-lookup"><span data-stu-id="b18d5-136">number</span></span> |<span data-ttu-id="b18d5-137">Merhaba tooportal gönderilen SDK'sı tarafından oluşturulan telemetri yüzdesi.</span><span class="sxs-lookup"><span data-stu-id="b18d5-137">Percentage of telemetry generated by hello SDK that is sent tooportal.</span></span> <span data-ttu-id="b18d5-138">0,0 100.0 aralığı.</span><span class="sxs-lookup"><span data-stu-id="b18d5-138">Range 0.0-100.0.</span></span> |
| <span data-ttu-id="b18d5-139">Context.Device</span><span class="sxs-lookup"><span data-stu-id="b18d5-139">context.device</span></span> |<span data-ttu-id="b18d5-140">Nesne</span><span class="sxs-lookup"><span data-stu-id="b18d5-140">object</span></span> |<span data-ttu-id="b18d5-141">İstemci aygıtı</span><span class="sxs-lookup"><span data-stu-id="b18d5-141">Client device</span></span> |
| <span data-ttu-id="b18d5-142">Context.Device.browser</span><span class="sxs-lookup"><span data-stu-id="b18d5-142">context.device.browser</span></span> |<span data-ttu-id="b18d5-143">Dize</span><span class="sxs-lookup"><span data-stu-id="b18d5-143">string</span></span> |<span data-ttu-id="b18d5-144">IE, Chrome...</span><span class="sxs-lookup"><span data-stu-id="b18d5-144">IE, Chrome, ...</span></span> |
| <span data-ttu-id="b18d5-145">context.device.browserVersion</span><span class="sxs-lookup"><span data-stu-id="b18d5-145">context.device.browserVersion</span></span> |<span data-ttu-id="b18d5-146">Dize</span><span class="sxs-lookup"><span data-stu-id="b18d5-146">string</span></span> |<span data-ttu-id="b18d5-147">Chrome 48,0...</span><span class="sxs-lookup"><span data-stu-id="b18d5-147">Chrome 48.0, ...</span></span> |
| <span data-ttu-id="b18d5-148">context.device.deviceModel</span><span class="sxs-lookup"><span data-stu-id="b18d5-148">context.device.deviceModel</span></span> |<span data-ttu-id="b18d5-149">Dize</span><span class="sxs-lookup"><span data-stu-id="b18d5-149">string</span></span> | |
| <span data-ttu-id="b18d5-150">context.device.deviceName</span><span class="sxs-lookup"><span data-stu-id="b18d5-150">context.device.deviceName</span></span> |<span data-ttu-id="b18d5-151">Dize</span><span class="sxs-lookup"><span data-stu-id="b18d5-151">string</span></span> | |
| <span data-ttu-id="b18d5-152">Context.Device.id</span><span class="sxs-lookup"><span data-stu-id="b18d5-152">context.device.id</span></span> |<span data-ttu-id="b18d5-153">Dize</span><span class="sxs-lookup"><span data-stu-id="b18d5-153">string</span></span> | |
| <span data-ttu-id="b18d5-154">Context.Device.Locale</span><span class="sxs-lookup"><span data-stu-id="b18d5-154">context.device.locale</span></span> |<span data-ttu-id="b18d5-155">Dize</span><span class="sxs-lookup"><span data-stu-id="b18d5-155">string</span></span> |<span data-ttu-id="b18d5-156">tr GB, de-DE...</span><span class="sxs-lookup"><span data-stu-id="b18d5-156">en-GB, de-DE, ...</span></span> |
| <span data-ttu-id="b18d5-157">Context.Device.Network</span><span class="sxs-lookup"><span data-stu-id="b18d5-157">context.device.network</span></span> |<span data-ttu-id="b18d5-158">Dize</span><span class="sxs-lookup"><span data-stu-id="b18d5-158">string</span></span> | |
| <span data-ttu-id="b18d5-159">context.device.oemName</span><span class="sxs-lookup"><span data-stu-id="b18d5-159">context.device.oemName</span></span> |<span data-ttu-id="b18d5-160">Dize</span><span class="sxs-lookup"><span data-stu-id="b18d5-160">string</span></span> | |
| <span data-ttu-id="b18d5-161">context.device.osVersion</span><span class="sxs-lookup"><span data-stu-id="b18d5-161">context.device.osVersion</span></span> |<span data-ttu-id="b18d5-162">Dize</span><span class="sxs-lookup"><span data-stu-id="b18d5-162">string</span></span> |<span data-ttu-id="b18d5-163">Ana bilgisayar işletim sistemi</span><span class="sxs-lookup"><span data-stu-id="b18d5-163">Host OS</span></span> |
| <span data-ttu-id="b18d5-164">context.device.roleInstance</span><span class="sxs-lookup"><span data-stu-id="b18d5-164">context.device.roleInstance</span></span> |<span data-ttu-id="b18d5-165">Dize</span><span class="sxs-lookup"><span data-stu-id="b18d5-165">string</span></span> |<span data-ttu-id="b18d5-166">Sunucu ana bilgisayar kimliği</span><span class="sxs-lookup"><span data-stu-id="b18d5-166">ID of server host</span></span> |
| <span data-ttu-id="b18d5-167">context.device.roleName</span><span class="sxs-lookup"><span data-stu-id="b18d5-167">context.device.roleName</span></span> |<span data-ttu-id="b18d5-168">Dize</span><span class="sxs-lookup"><span data-stu-id="b18d5-168">string</span></span> | |
| <span data-ttu-id="b18d5-169">Context.Device.Type</span><span class="sxs-lookup"><span data-stu-id="b18d5-169">context.device.type</span></span> |<span data-ttu-id="b18d5-170">Dize</span><span class="sxs-lookup"><span data-stu-id="b18d5-170">string</span></span> |<span data-ttu-id="b18d5-171">Bilgisayar Tarayıcı...</span><span class="sxs-lookup"><span data-stu-id="b18d5-171">PC, Browser, ...</span></span> |
| <span data-ttu-id="b18d5-172">Context.location</span><span class="sxs-lookup"><span data-stu-id="b18d5-172">context.location</span></span> |<span data-ttu-id="b18d5-173">Nesne</span><span class="sxs-lookup"><span data-stu-id="b18d5-173">object</span></span> |<span data-ttu-id="b18d5-174">Clientip türetilmiş.</span><span class="sxs-lookup"><span data-stu-id="b18d5-174">Derived from clientip.</span></span> |
| <span data-ttu-id="b18d5-175">Context.location.City</span><span class="sxs-lookup"><span data-stu-id="b18d5-175">context.location.city</span></span> |<span data-ttu-id="b18d5-176">Dize</span><span class="sxs-lookup"><span data-stu-id="b18d5-176">string</span></span> |<span data-ttu-id="b18d5-177">Biliniyorsa clientip türetilmiş</span><span class="sxs-lookup"><span data-stu-id="b18d5-177">Derived from clientip, if known</span></span> |
| <span data-ttu-id="b18d5-178">Context.location.clientip</span><span class="sxs-lookup"><span data-stu-id="b18d5-178">context.location.clientip</span></span> |<span data-ttu-id="b18d5-179">Dize</span><span class="sxs-lookup"><span data-stu-id="b18d5-179">string</span></span> |<span data-ttu-id="b18d5-180">Son Sekizgene anonim too0 ' dir.</span><span class="sxs-lookup"><span data-stu-id="b18d5-180">Last octagon is anonymized too0.</span></span> |
| <span data-ttu-id="b18d5-181">Context.location.continent</span><span class="sxs-lookup"><span data-stu-id="b18d5-181">context.location.continent</span></span> |<span data-ttu-id="b18d5-182">Dize</span><span class="sxs-lookup"><span data-stu-id="b18d5-182">string</span></span> | |
| <span data-ttu-id="b18d5-183">Context.location.country</span><span class="sxs-lookup"><span data-stu-id="b18d5-183">context.location.country</span></span> |<span data-ttu-id="b18d5-184">Dize</span><span class="sxs-lookup"><span data-stu-id="b18d5-184">string</span></span> | |
| <span data-ttu-id="b18d5-185">Context.location.Province</span><span class="sxs-lookup"><span data-stu-id="b18d5-185">context.location.province</span></span> |<span data-ttu-id="b18d5-186">Dize</span><span class="sxs-lookup"><span data-stu-id="b18d5-186">string</span></span> |<span data-ttu-id="b18d5-187">Eyalet veya il</span><span class="sxs-lookup"><span data-stu-id="b18d5-187">State or province</span></span> |
| <span data-ttu-id="b18d5-188">Context.Operation.id</span><span class="sxs-lookup"><span data-stu-id="b18d5-188">context.operation.id</span></span> |<span data-ttu-id="b18d5-189">Dize</span><span class="sxs-lookup"><span data-stu-id="b18d5-189">string</span></span> |<span data-ttu-id="b18d5-190">Aynı işlem kimliği ilgili öğeler hello Portalı'nda gösterilen hello sahip öğeler.</span><span class="sxs-lookup"><span data-stu-id="b18d5-190">Items that have hello same operation id are shown as Related Items in hello portal.</span></span> <span data-ttu-id="b18d5-191">Genellikle hello istek kimliği.</span><span class="sxs-lookup"><span data-stu-id="b18d5-191">Usually hello request id.</span></span> |
| <span data-ttu-id="b18d5-192">Context.Operation.Name</span><span class="sxs-lookup"><span data-stu-id="b18d5-192">context.operation.name</span></span> |<span data-ttu-id="b18d5-193">Dize</span><span class="sxs-lookup"><span data-stu-id="b18d5-193">string</span></span> |<span data-ttu-id="b18d5-194">URL veya isteği adı</span><span class="sxs-lookup"><span data-stu-id="b18d5-194">url or request name</span></span> |
| <span data-ttu-id="b18d5-195">context.operation.parentId</span><span class="sxs-lookup"><span data-stu-id="b18d5-195">context.operation.parentId</span></span> |<span data-ttu-id="b18d5-196">Dize</span><span class="sxs-lookup"><span data-stu-id="b18d5-196">string</span></span> |<span data-ttu-id="b18d5-197">İç içe geçmiş ilgili öğeler sağlar.</span><span class="sxs-lookup"><span data-stu-id="b18d5-197">Allows nested related items.</span></span> |
| <span data-ttu-id="b18d5-198">Context.Session.id</span><span class="sxs-lookup"><span data-stu-id="b18d5-198">context.session.id</span></span> |<span data-ttu-id="b18d5-199">Dize</span><span class="sxs-lookup"><span data-stu-id="b18d5-199">string</span></span> |<span data-ttu-id="b18d5-200">Merhaba işlemlerinden grubunun kimliği aynı kaynağı.</span><span class="sxs-lookup"><span data-stu-id="b18d5-200">Id of a group of operations from hello same source.</span></span> <span data-ttu-id="b18d5-201">Bir işlem olmadan 30 dakikalık bir süre bir oturum hello sonuna işaret eder.</span><span class="sxs-lookup"><span data-stu-id="b18d5-201">A period of 30 minutes without an operation signals hello end of a session.</span></span> |
| <span data-ttu-id="b18d5-202">context.session.isFirst</span><span class="sxs-lookup"><span data-stu-id="b18d5-202">context.session.isFirst</span></span> |<span data-ttu-id="b18d5-203">Boole değeri</span><span class="sxs-lookup"><span data-stu-id="b18d5-203">boolean</span></span> | |
| <span data-ttu-id="b18d5-204">context.user.accountAcquisitionDate</span><span class="sxs-lookup"><span data-stu-id="b18d5-204">context.user.accountAcquisitionDate</span></span> |<span data-ttu-id="b18d5-205">Dize</span><span class="sxs-lookup"><span data-stu-id="b18d5-205">string</span></span> | |
| <span data-ttu-id="b18d5-206">context.user.anonAcquisitionDate</span><span class="sxs-lookup"><span data-stu-id="b18d5-206">context.user.anonAcquisitionDate</span></span> |<span data-ttu-id="b18d5-207">Dize</span><span class="sxs-lookup"><span data-stu-id="b18d5-207">string</span></span> | |
| <span data-ttu-id="b18d5-208">context.user.anonId</span><span class="sxs-lookup"><span data-stu-id="b18d5-208">context.user.anonId</span></span> |<span data-ttu-id="b18d5-209">Dize</span><span class="sxs-lookup"><span data-stu-id="b18d5-209">string</span></span> | |
| <span data-ttu-id="b18d5-210">context.user.authAcquisitionDate</span><span class="sxs-lookup"><span data-stu-id="b18d5-210">context.user.authAcquisitionDate</span></span> |<span data-ttu-id="b18d5-211">Dize</span><span class="sxs-lookup"><span data-stu-id="b18d5-211">string</span></span> |[<span data-ttu-id="b18d5-212">Kimliği doğrulanmış kullanıcı</span><span class="sxs-lookup"><span data-stu-id="b18d5-212">Authenticated User</span></span>](app-insights-api-custom-events-metrics.md#authenticated-users) |
| <span data-ttu-id="b18d5-213">context.user.isAuthenticated</span><span class="sxs-lookup"><span data-stu-id="b18d5-213">context.user.isAuthenticated</span></span> |<span data-ttu-id="b18d5-214">Boole değeri</span><span class="sxs-lookup"><span data-stu-id="b18d5-214">boolean</span></span> | |
| <span data-ttu-id="b18d5-215">internal.data.documentVersion</span><span class="sxs-lookup"><span data-stu-id="b18d5-215">internal.data.documentVersion</span></span> |<span data-ttu-id="b18d5-216">Dize</span><span class="sxs-lookup"><span data-stu-id="b18d5-216">string</span></span> | |
| <span data-ttu-id="b18d5-217">internal.Data.id</span><span class="sxs-lookup"><span data-stu-id="b18d5-217">internal.data.id</span></span> |<span data-ttu-id="b18d5-218">Dize</span><span class="sxs-lookup"><span data-stu-id="b18d5-218">string</span></span> | |

## <a name="events"></a><span data-ttu-id="b18d5-219">Olaylar</span><span class="sxs-lookup"><span data-stu-id="b18d5-219">Events</span></span>
<span data-ttu-id="b18d5-220">Tarafından oluşturulan özel olaylar [TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent).</span><span class="sxs-lookup"><span data-stu-id="b18d5-220">Custom events generated by [TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent).</span></span>

| <span data-ttu-id="b18d5-221">Yol</span><span class="sxs-lookup"><span data-stu-id="b18d5-221">Path</span></span> | <span data-ttu-id="b18d5-222">Tür</span><span class="sxs-lookup"><span data-stu-id="b18d5-222">Type</span></span> | <span data-ttu-id="b18d5-223">Notlar</span><span class="sxs-lookup"><span data-stu-id="b18d5-223">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b18d5-224">[0] olay sayısı</span><span class="sxs-lookup"><span data-stu-id="b18d5-224">event [0] count</span></span> |<span data-ttu-id="b18d5-225">tamsayı</span><span class="sxs-lookup"><span data-stu-id="b18d5-225">integer</span></span> |<span data-ttu-id="b18d5-226">100 / ([örnekleme](app-insights-sampling.md) hızı).</span><span class="sxs-lookup"><span data-stu-id="b18d5-226">100/([sampling](app-insights-sampling.md) rate).</span></span> <span data-ttu-id="b18d5-227">Örneğin 4 =&gt; % 25.</span><span class="sxs-lookup"><span data-stu-id="b18d5-227">For example 4 =&gt; 25%.</span></span> |
| <span data-ttu-id="b18d5-228">Olay [0] adı</span><span class="sxs-lookup"><span data-stu-id="b18d5-228">event [0] name</span></span> |<span data-ttu-id="b18d5-229">Dize</span><span class="sxs-lookup"><span data-stu-id="b18d5-229">string</span></span> |<span data-ttu-id="b18d5-230">Olay adı.</span><span class="sxs-lookup"><span data-stu-id="b18d5-230">Event name.</span></span>  <span data-ttu-id="b18d5-231">En fazla uzunluk 250.</span><span class="sxs-lookup"><span data-stu-id="b18d5-231">Max length 250.</span></span> |
| <span data-ttu-id="b18d5-232">Olay [0] URL'si</span><span class="sxs-lookup"><span data-stu-id="b18d5-232">event [0] url</span></span> |<span data-ttu-id="b18d5-233">Dize</span><span class="sxs-lookup"><span data-stu-id="b18d5-233">string</span></span> | |
| <span data-ttu-id="b18d5-234">Olay [0] urlData.base</span><span class="sxs-lookup"><span data-stu-id="b18d5-234">event [0] urlData.base</span></span> |<span data-ttu-id="b18d5-235">Dize</span><span class="sxs-lookup"><span data-stu-id="b18d5-235">string</span></span> | |
| <span data-ttu-id="b18d5-236">Olay [0] urlData.host</span><span class="sxs-lookup"><span data-stu-id="b18d5-236">event [0] urlData.host</span></span> |<span data-ttu-id="b18d5-237">Dize</span><span class="sxs-lookup"><span data-stu-id="b18d5-237">string</span></span> | |

## <a name="exceptions"></a><span data-ttu-id="b18d5-238">Özel durumlar</span><span class="sxs-lookup"><span data-stu-id="b18d5-238">Exceptions</span></span>
<span data-ttu-id="b18d5-239">Raporları [özel durumları](app-insights-asp-net-exceptions.md) hello sunucu ve hello tarayıcı.</span><span class="sxs-lookup"><span data-stu-id="b18d5-239">Reports [exceptions](app-insights-asp-net-exceptions.md) in hello server and in hello browser.</span></span>

| <span data-ttu-id="b18d5-240">Yol</span><span class="sxs-lookup"><span data-stu-id="b18d5-240">Path</span></span> | <span data-ttu-id="b18d5-241">Tür</span><span class="sxs-lookup"><span data-stu-id="b18d5-241">Type</span></span> | <span data-ttu-id="b18d5-242">Notlar</span><span class="sxs-lookup"><span data-stu-id="b18d5-242">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b18d5-243">basicException [0] derlemesi</span><span class="sxs-lookup"><span data-stu-id="b18d5-243">basicException [0] assembly</span></span> |<span data-ttu-id="b18d5-244">Dize</span><span class="sxs-lookup"><span data-stu-id="b18d5-244">string</span></span> | |
| <span data-ttu-id="b18d5-245">basicException [0] sayısı</span><span class="sxs-lookup"><span data-stu-id="b18d5-245">basicException [0] count</span></span> |<span data-ttu-id="b18d5-246">tamsayı</span><span class="sxs-lookup"><span data-stu-id="b18d5-246">integer</span></span> |<span data-ttu-id="b18d5-247">100 / ([örnekleme](app-insights-sampling.md) hızı).</span><span class="sxs-lookup"><span data-stu-id="b18d5-247">100/([sampling](app-insights-sampling.md) rate).</span></span> <span data-ttu-id="b18d5-248">Örneğin 4 =&gt; % 25.</span><span class="sxs-lookup"><span data-stu-id="b18d5-248">For example 4 =&gt; 25%.</span></span> |
| <span data-ttu-id="b18d5-249">basicException [0] exceptionGroup</span><span class="sxs-lookup"><span data-stu-id="b18d5-249">basicException [0] exceptionGroup</span></span> |<span data-ttu-id="b18d5-250">Dize</span><span class="sxs-lookup"><span data-stu-id="b18d5-250">string</span></span> | |
| <span data-ttu-id="b18d5-251">basicException [0] exceptionType</span><span class="sxs-lookup"><span data-stu-id="b18d5-251">basicException [0] exceptionType</span></span> |<span data-ttu-id="b18d5-252">Dize</span><span class="sxs-lookup"><span data-stu-id="b18d5-252">string</span></span> | |
| <span data-ttu-id="b18d5-253">basicException [0] failedUserCodeMethod</span><span class="sxs-lookup"><span data-stu-id="b18d5-253">basicException [0] failedUserCodeMethod</span></span> |<span data-ttu-id="b18d5-254">Dize</span><span class="sxs-lookup"><span data-stu-id="b18d5-254">string</span></span> | |
| <span data-ttu-id="b18d5-255">basicException [0] failedUserCodeAssembly</span><span class="sxs-lookup"><span data-stu-id="b18d5-255">basicException [0] failedUserCodeAssembly</span></span> |<span data-ttu-id="b18d5-256">Dize</span><span class="sxs-lookup"><span data-stu-id="b18d5-256">string</span></span> | |
| <span data-ttu-id="b18d5-257">basicException [0] handledAt</span><span class="sxs-lookup"><span data-stu-id="b18d5-257">basicException [0] handledAt</span></span> |<span data-ttu-id="b18d5-258">Dize</span><span class="sxs-lookup"><span data-stu-id="b18d5-258">string</span></span> | |
| <span data-ttu-id="b18d5-259">basicException [0] hasFullStack</span><span class="sxs-lookup"><span data-stu-id="b18d5-259">basicException [0] hasFullStack</span></span> |<span data-ttu-id="b18d5-260">Boole değeri</span><span class="sxs-lookup"><span data-stu-id="b18d5-260">boolean</span></span> | |
| <span data-ttu-id="b18d5-261">basicException [0] kimliği</span><span class="sxs-lookup"><span data-stu-id="b18d5-261">basicException [0] id</span></span> |<span data-ttu-id="b18d5-262">Dize</span><span class="sxs-lookup"><span data-stu-id="b18d5-262">string</span></span> | |
| <span data-ttu-id="b18d5-263">basicException [0] yöntemi</span><span class="sxs-lookup"><span data-stu-id="b18d5-263">basicException [0] method</span></span> |<span data-ttu-id="b18d5-264">Dize</span><span class="sxs-lookup"><span data-stu-id="b18d5-264">string</span></span> | |
| <span data-ttu-id="b18d5-265">basicException [0] iletisi</span><span class="sxs-lookup"><span data-stu-id="b18d5-265">basicException [0] message</span></span> |<span data-ttu-id="b18d5-266">Dize</span><span class="sxs-lookup"><span data-stu-id="b18d5-266">string</span></span> |<span data-ttu-id="b18d5-267">Özel durum iletisi.</span><span class="sxs-lookup"><span data-stu-id="b18d5-267">Exception message.</span></span> <span data-ttu-id="b18d5-268">En fazla uzunluk 10k.</span><span class="sxs-lookup"><span data-stu-id="b18d5-268">Max length 10k.</span></span> |
| <span data-ttu-id="b18d5-269">basicException [0] outerExceptionMessage</span><span class="sxs-lookup"><span data-stu-id="b18d5-269">basicException [0] outerExceptionMessage</span></span> |<span data-ttu-id="b18d5-270">Dize</span><span class="sxs-lookup"><span data-stu-id="b18d5-270">string</span></span> | |
| <span data-ttu-id="b18d5-271">basicException [0] outerExceptionThrownAtAssembly</span><span class="sxs-lookup"><span data-stu-id="b18d5-271">basicException [0] outerExceptionThrownAtAssembly</span></span> |<span data-ttu-id="b18d5-272">Dize</span><span class="sxs-lookup"><span data-stu-id="b18d5-272">string</span></span> | |
| <span data-ttu-id="b18d5-273">basicException [0] outerExceptionThrownAtMethod</span><span class="sxs-lookup"><span data-stu-id="b18d5-273">basicException [0] outerExceptionThrownAtMethod</span></span> |<span data-ttu-id="b18d5-274">Dize</span><span class="sxs-lookup"><span data-stu-id="b18d5-274">string</span></span> | |
| <span data-ttu-id="b18d5-275">basicException [0] outerExceptionType</span><span class="sxs-lookup"><span data-stu-id="b18d5-275">basicException [0] outerExceptionType</span></span> |<span data-ttu-id="b18d5-276">Dize</span><span class="sxs-lookup"><span data-stu-id="b18d5-276">string</span></span> | |
| <span data-ttu-id="b18d5-277">basicException [0] outerId</span><span class="sxs-lookup"><span data-stu-id="b18d5-277">basicException [0] outerId</span></span> |<span data-ttu-id="b18d5-278">Dize</span><span class="sxs-lookup"><span data-stu-id="b18d5-278">string</span></span> | |
| <span data-ttu-id="b18d5-279">basicException [0] parsedStack [0] derlemesi</span><span class="sxs-lookup"><span data-stu-id="b18d5-279">basicException [0] parsedStack [0] assembly</span></span> |<span data-ttu-id="b18d5-280">Dize</span><span class="sxs-lookup"><span data-stu-id="b18d5-280">string</span></span> | |
| <span data-ttu-id="b18d5-281">basicException [0] [0] parsedStack fileName</span><span class="sxs-lookup"><span data-stu-id="b18d5-281">basicException [0] parsedStack [0] fileName</span></span> |<span data-ttu-id="b18d5-282">Dize</span><span class="sxs-lookup"><span data-stu-id="b18d5-282">string</span></span> | |
| <span data-ttu-id="b18d5-283">basicException [0] [0] parsedStack düzeyi</span><span class="sxs-lookup"><span data-stu-id="b18d5-283">basicException [0] parsedStack [0] level</span></span> |<span data-ttu-id="b18d5-284">tamsayı</span><span class="sxs-lookup"><span data-stu-id="b18d5-284">integer</span></span> | |
| <span data-ttu-id="b18d5-285">basicException [0] [0] parsedStack satır</span><span class="sxs-lookup"><span data-stu-id="b18d5-285">basicException [0] parsedStack [0] line</span></span> |<span data-ttu-id="b18d5-286">tamsayı</span><span class="sxs-lookup"><span data-stu-id="b18d5-286">integer</span></span> | |
| <span data-ttu-id="b18d5-287">basicException [0] [0] parsedStack yöntemi</span><span class="sxs-lookup"><span data-stu-id="b18d5-287">basicException [0] parsedStack [0] method</span></span> |<span data-ttu-id="b18d5-288">Dize</span><span class="sxs-lookup"><span data-stu-id="b18d5-288">string</span></span> | |
| <span data-ttu-id="b18d5-289">basicException [0] yığını</span><span class="sxs-lookup"><span data-stu-id="b18d5-289">basicException [0] stack</span></span> |<span data-ttu-id="b18d5-290">Dize</span><span class="sxs-lookup"><span data-stu-id="b18d5-290">string</span></span> |<span data-ttu-id="b18d5-291">En fazla uzunluk 10k</span><span class="sxs-lookup"><span data-stu-id="b18d5-291">Max length 10k</span></span> |
| <span data-ttu-id="b18d5-292">basicException [0] typeName</span><span class="sxs-lookup"><span data-stu-id="b18d5-292">basicException [0] typeName</span></span> |<span data-ttu-id="b18d5-293">Dize</span><span class="sxs-lookup"><span data-stu-id="b18d5-293">string</span></span> | |

## <a name="trace-messages"></a><span data-ttu-id="b18d5-294">İzleme iletileri</span><span class="sxs-lookup"><span data-stu-id="b18d5-294">Trace Messages</span></span>
<span data-ttu-id="b18d5-295">Tarafından gönderilen [TrackTrace](app-insights-api-custom-events-metrics.md#tracktrace)ile Merhaba [günlüğü bağdaştırıcıları](app-insights-asp-net-trace-logs.md).</span><span class="sxs-lookup"><span data-stu-id="b18d5-295">Sent by [TrackTrace](app-insights-api-custom-events-metrics.md#tracktrace), and by hello [logging adapters](app-insights-asp-net-trace-logs.md).</span></span>

| <span data-ttu-id="b18d5-296">Yol</span><span class="sxs-lookup"><span data-stu-id="b18d5-296">Path</span></span> | <span data-ttu-id="b18d5-297">Tür</span><span class="sxs-lookup"><span data-stu-id="b18d5-297">Type</span></span> | <span data-ttu-id="b18d5-298">Notlar</span><span class="sxs-lookup"><span data-stu-id="b18d5-298">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b18d5-299">ileti [0] GünlükçüAdı</span><span class="sxs-lookup"><span data-stu-id="b18d5-299">message [0] loggerName</span></span> |<span data-ttu-id="b18d5-300">Dize</span><span class="sxs-lookup"><span data-stu-id="b18d5-300">string</span></span> | |
| <span data-ttu-id="b18d5-301">ileti [0] parametreleri</span><span class="sxs-lookup"><span data-stu-id="b18d5-301">message [0] parameters</span></span> |<span data-ttu-id="b18d5-302">Dize</span><span class="sxs-lookup"><span data-stu-id="b18d5-302">string</span></span> | |
| <span data-ttu-id="b18d5-303">ileti [0] ham</span><span class="sxs-lookup"><span data-stu-id="b18d5-303">message [0] raw</span></span> |<span data-ttu-id="b18d5-304">Dize</span><span class="sxs-lookup"><span data-stu-id="b18d5-304">string</span></span> |<span data-ttu-id="b18d5-305">Merhaba günlük iletisi, uzunluk üst sınırı 10k.</span><span class="sxs-lookup"><span data-stu-id="b18d5-305">hello log message, max length 10k.</span></span> |
| <span data-ttu-id="b18d5-306">[0] iletisi önem düzeyi</span><span class="sxs-lookup"><span data-stu-id="b18d5-306">message [0] severityLevel</span></span> |<span data-ttu-id="b18d5-307">Dize</span><span class="sxs-lookup"><span data-stu-id="b18d5-307">string</span></span> | |

## <a name="remote-dependency"></a><span data-ttu-id="b18d5-308">Uzak bağımlılık</span><span class="sxs-lookup"><span data-stu-id="b18d5-308">Remote dependency</span></span>
<span data-ttu-id="b18d5-309">TrackDependency tarafından gönderilir.</span><span class="sxs-lookup"><span data-stu-id="b18d5-309">Sent by TrackDependency.</span></span> <span data-ttu-id="b18d5-310">Kullanılan tooreport performansını ve kullanımını [toodependencies çağırır](app-insights-asp-net-dependencies.md) hello server ve AJAX çağrıları hello tarayıcıda.</span><span class="sxs-lookup"><span data-stu-id="b18d5-310">Used tooreport performance and usage of [calls toodependencies](app-insights-asp-net-dependencies.md) in hello server, and AJAX calls in hello browser.</span></span>

| <span data-ttu-id="b18d5-311">Yol</span><span class="sxs-lookup"><span data-stu-id="b18d5-311">Path</span></span> | <span data-ttu-id="b18d5-312">Tür</span><span class="sxs-lookup"><span data-stu-id="b18d5-312">Type</span></span> | <span data-ttu-id="b18d5-313">Notlar</span><span class="sxs-lookup"><span data-stu-id="b18d5-313">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b18d5-314">remoteDependency [0] zaman uyumsuz</span><span class="sxs-lookup"><span data-stu-id="b18d5-314">remoteDependency [0] async</span></span> |<span data-ttu-id="b18d5-315">Boole değeri</span><span class="sxs-lookup"><span data-stu-id="b18d5-315">boolean</span></span> | |
| <span data-ttu-id="b18d5-316">remoteDependency [0] baseName</span><span class="sxs-lookup"><span data-stu-id="b18d5-316">remoteDependency [0] baseName</span></span> |<span data-ttu-id="b18d5-317">Dize</span><span class="sxs-lookup"><span data-stu-id="b18d5-317">string</span></span> | |
| <span data-ttu-id="b18d5-318">remoteDependency [0] commandName</span><span class="sxs-lookup"><span data-stu-id="b18d5-318">remoteDependency [0] commandName</span></span> |<span data-ttu-id="b18d5-319">Dize</span><span class="sxs-lookup"><span data-stu-id="b18d5-319">string</span></span> |<span data-ttu-id="b18d5-320">Örneğin "home/Index"</span><span class="sxs-lookup"><span data-stu-id="b18d5-320">For example "home/index"</span></span> |
| <span data-ttu-id="b18d5-321">remoteDependency [0] sayısı</span><span class="sxs-lookup"><span data-stu-id="b18d5-321">remoteDependency [0] count</span></span> |<span data-ttu-id="b18d5-322">tamsayı</span><span class="sxs-lookup"><span data-stu-id="b18d5-322">integer</span></span> |<span data-ttu-id="b18d5-323">100 / ([örnekleme](app-insights-sampling.md) hızı).</span><span class="sxs-lookup"><span data-stu-id="b18d5-323">100/([sampling](app-insights-sampling.md) rate).</span></span> <span data-ttu-id="b18d5-324">Örneğin 4 =&gt; % 25.</span><span class="sxs-lookup"><span data-stu-id="b18d5-324">For example 4 =&gt; 25%.</span></span> |
| <span data-ttu-id="b18d5-325">remoteDependency [0] dependencyTypeName</span><span class="sxs-lookup"><span data-stu-id="b18d5-325">remoteDependency [0] dependencyTypeName</span></span> |<span data-ttu-id="b18d5-326">Dize</span><span class="sxs-lookup"><span data-stu-id="b18d5-326">string</span></span> |<span data-ttu-id="b18d5-327">HTTP SQL...</span><span class="sxs-lookup"><span data-stu-id="b18d5-327">HTTP, SQL, ...</span></span> |
| <span data-ttu-id="b18d5-328">remoteDependency [0] durationMetric.value</span><span class="sxs-lookup"><span data-stu-id="b18d5-328">remoteDependency [0] durationMetric.value</span></span> |<span data-ttu-id="b18d5-329">Sayı</span><span class="sxs-lookup"><span data-stu-id="b18d5-329">number</span></span> |<span data-ttu-id="b18d5-330">Çağrı toocompletion bağımlılık tarafından yanıt süresi</span><span class="sxs-lookup"><span data-stu-id="b18d5-330">Time from call toocompletion of response by dependency</span></span> |
| <span data-ttu-id="b18d5-331">remoteDependency [0] kimliği</span><span class="sxs-lookup"><span data-stu-id="b18d5-331">remoteDependency [0] id</span></span> |<span data-ttu-id="b18d5-332">Dize</span><span class="sxs-lookup"><span data-stu-id="b18d5-332">string</span></span> | |
| <span data-ttu-id="b18d5-333">remoteDependency [0] adı</span><span class="sxs-lookup"><span data-stu-id="b18d5-333">remoteDependency [0] name</span></span> |<span data-ttu-id="b18d5-334">Dize</span><span class="sxs-lookup"><span data-stu-id="b18d5-334">string</span></span> |<span data-ttu-id="b18d5-335">URL.</span><span class="sxs-lookup"><span data-stu-id="b18d5-335">Url.</span></span> <span data-ttu-id="b18d5-336">En fazla uzunluk 250.</span><span class="sxs-lookup"><span data-stu-id="b18d5-336">Max length 250.</span></span> |
| <span data-ttu-id="b18d5-337">remoteDependency [0] resultCode</span><span class="sxs-lookup"><span data-stu-id="b18d5-337">remoteDependency [0] resultCode</span></span> |<span data-ttu-id="b18d5-338">Dize</span><span class="sxs-lookup"><span data-stu-id="b18d5-338">string</span></span> |<span data-ttu-id="b18d5-339">HTTP bağımlılık</span><span class="sxs-lookup"><span data-stu-id="b18d5-339">from HTTP dependency</span></span> |
| <span data-ttu-id="b18d5-340">remoteDependency [0] başarılı</span><span class="sxs-lookup"><span data-stu-id="b18d5-340">remoteDependency [0] success</span></span> |<span data-ttu-id="b18d5-341">Boole değeri</span><span class="sxs-lookup"><span data-stu-id="b18d5-341">boolean</span></span> | |
| <span data-ttu-id="b18d5-342">remoteDependency [0] türü</span><span class="sxs-lookup"><span data-stu-id="b18d5-342">remoteDependency [0] type</span></span> |<span data-ttu-id="b18d5-343">Dize</span><span class="sxs-lookup"><span data-stu-id="b18d5-343">string</span></span> |<span data-ttu-id="b18d5-344">HTTP Sql...</span><span class="sxs-lookup"><span data-stu-id="b18d5-344">Http, Sql,...</span></span> |
| <span data-ttu-id="b18d5-345">remoteDependency [0] URL'si</span><span class="sxs-lookup"><span data-stu-id="b18d5-345">remoteDependency [0] url</span></span> |<span data-ttu-id="b18d5-346">Dize</span><span class="sxs-lookup"><span data-stu-id="b18d5-346">string</span></span> |<span data-ttu-id="b18d5-347">En fazla uzunluk 2000</span><span class="sxs-lookup"><span data-stu-id="b18d5-347">Max length 2000</span></span> |
| <span data-ttu-id="b18d5-348">remoteDependency [0] urlData.base</span><span class="sxs-lookup"><span data-stu-id="b18d5-348">remoteDependency [0] urlData.base</span></span> |<span data-ttu-id="b18d5-349">Dize</span><span class="sxs-lookup"><span data-stu-id="b18d5-349">string</span></span> |<span data-ttu-id="b18d5-350">En fazla uzunluk 2000</span><span class="sxs-lookup"><span data-stu-id="b18d5-350">Max length 2000</span></span> |
| <span data-ttu-id="b18d5-351">remoteDependency [0] urlData.hashTag</span><span class="sxs-lookup"><span data-stu-id="b18d5-351">remoteDependency [0] urlData.hashTag</span></span> |<span data-ttu-id="b18d5-352">Dize</span><span class="sxs-lookup"><span data-stu-id="b18d5-352">string</span></span> | |
| <span data-ttu-id="b18d5-353">remoteDependency [0] urlData.host</span><span class="sxs-lookup"><span data-stu-id="b18d5-353">remoteDependency [0] urlData.host</span></span> |<span data-ttu-id="b18d5-354">Dize</span><span class="sxs-lookup"><span data-stu-id="b18d5-354">string</span></span> |<span data-ttu-id="b18d5-355">En fazla uzunluk 200</span><span class="sxs-lookup"><span data-stu-id="b18d5-355">Max length 200</span></span> |

## <a name="requests"></a><span data-ttu-id="b18d5-356">İstekler</span><span class="sxs-lookup"><span data-stu-id="b18d5-356">Requests</span></span>
<span data-ttu-id="b18d5-357">Tarafından gönderilen [TrackRequest](app-insights-api-custom-events-metrics.md#trackrequest).</span><span class="sxs-lookup"><span data-stu-id="b18d5-357">Sent by [TrackRequest](app-insights-api-custom-events-metrics.md#trackrequest).</span></span> <span data-ttu-id="b18d5-358">Merhaba Standart modüller hello sunucuda ölçülen bu tooreports sunucu yanıt süresi kullanın.</span><span class="sxs-lookup"><span data-stu-id="b18d5-358">hello standard modules use this tooreports server response time, measured at hello server.</span></span>

| <span data-ttu-id="b18d5-359">Yol</span><span class="sxs-lookup"><span data-stu-id="b18d5-359">Path</span></span> | <span data-ttu-id="b18d5-360">Tür</span><span class="sxs-lookup"><span data-stu-id="b18d5-360">Type</span></span> | <span data-ttu-id="b18d5-361">Notlar</span><span class="sxs-lookup"><span data-stu-id="b18d5-361">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b18d5-362">[0] isteği sayısı</span><span class="sxs-lookup"><span data-stu-id="b18d5-362">request [0] count</span></span> |<span data-ttu-id="b18d5-363">tamsayı</span><span class="sxs-lookup"><span data-stu-id="b18d5-363">integer</span></span> |<span data-ttu-id="b18d5-364">100 / ([örnekleme](app-insights-sampling.md) hızı).</span><span class="sxs-lookup"><span data-stu-id="b18d5-364">100/([sampling](app-insights-sampling.md) rate).</span></span> <span data-ttu-id="b18d5-365">Örneğin: 4 =&gt; % 25.</span><span class="sxs-lookup"><span data-stu-id="b18d5-365">For example: 4 =&gt; 25%.</span></span> |
| <span data-ttu-id="b18d5-366">İstek [0] durationMetric.value</span><span class="sxs-lookup"><span data-stu-id="b18d5-366">request [0] durationMetric.value</span></span> |<span data-ttu-id="b18d5-367">Sayı</span><span class="sxs-lookup"><span data-stu-id="b18d5-367">number</span></span> |<span data-ttu-id="b18d5-368">İstek gelen tooresponse saati.</span><span class="sxs-lookup"><span data-stu-id="b18d5-368">Time from request arriving tooresponse.</span></span> <span data-ttu-id="b18d5-369">1e7 1'ler ==</span><span class="sxs-lookup"><span data-stu-id="b18d5-369">1e7 == 1s</span></span> |
| <span data-ttu-id="b18d5-370">[0] istek kimliği</span><span class="sxs-lookup"><span data-stu-id="b18d5-370">request [0] id</span></span> |<span data-ttu-id="b18d5-371">Dize</span><span class="sxs-lookup"><span data-stu-id="b18d5-371">string</span></span> |<span data-ttu-id="b18d5-372">İşlem kimliği</span><span class="sxs-lookup"><span data-stu-id="b18d5-372">Operation id</span></span> |
| <span data-ttu-id="b18d5-373">İstek [0] adı</span><span class="sxs-lookup"><span data-stu-id="b18d5-373">request [0] name</span></span> |<span data-ttu-id="b18d5-374">Dize</span><span class="sxs-lookup"><span data-stu-id="b18d5-374">string</span></span> |<span data-ttu-id="b18d5-375">GET/POST + temel url.</span><span class="sxs-lookup"><span data-stu-id="b18d5-375">GET/POST + url base.</span></span>  <span data-ttu-id="b18d5-376">En fazla uzunluk 250</span><span class="sxs-lookup"><span data-stu-id="b18d5-376">Max length 250</span></span> |
| <span data-ttu-id="b18d5-377">İstek [0] yanıt kodu</span><span class="sxs-lookup"><span data-stu-id="b18d5-377">request [0] responseCode</span></span> |<span data-ttu-id="b18d5-378">tamsayı</span><span class="sxs-lookup"><span data-stu-id="b18d5-378">integer</span></span> |<span data-ttu-id="b18d5-379">HTTP yanıt gönderilen tooclient</span><span class="sxs-lookup"><span data-stu-id="b18d5-379">HTTP response sent tooclient</span></span> |
| <span data-ttu-id="b18d5-380">İstek [0] başarılı</span><span class="sxs-lookup"><span data-stu-id="b18d5-380">request [0] success</span></span> |<span data-ttu-id="b18d5-381">Boole değeri</span><span class="sxs-lookup"><span data-stu-id="b18d5-381">boolean</span></span> |<span data-ttu-id="b18d5-382">Varsayılan == (yanıt kodu &lt; 400)</span><span class="sxs-lookup"><span data-stu-id="b18d5-382">Default == (responseCode &lt; 400)</span></span> |
| <span data-ttu-id="b18d5-383">İstek [0] URL'si</span><span class="sxs-lookup"><span data-stu-id="b18d5-383">request [0] url</span></span> |<span data-ttu-id="b18d5-384">Dize</span><span class="sxs-lookup"><span data-stu-id="b18d5-384">string</span></span> |<span data-ttu-id="b18d5-385">Konak dahil değil</span><span class="sxs-lookup"><span data-stu-id="b18d5-385">Not including host</span></span> |
| <span data-ttu-id="b18d5-386">İstek [0] urlData.base</span><span class="sxs-lookup"><span data-stu-id="b18d5-386">request [0] urlData.base</span></span> |<span data-ttu-id="b18d5-387">Dize</span><span class="sxs-lookup"><span data-stu-id="b18d5-387">string</span></span> | |
| <span data-ttu-id="b18d5-388">İstek [0] urlData.hashTag</span><span class="sxs-lookup"><span data-stu-id="b18d5-388">request [0] urlData.hashTag</span></span> |<span data-ttu-id="b18d5-389">Dize</span><span class="sxs-lookup"><span data-stu-id="b18d5-389">string</span></span> | |
| <span data-ttu-id="b18d5-390">İstek [0] urlData.host</span><span class="sxs-lookup"><span data-stu-id="b18d5-390">request [0] urlData.host</span></span> |<span data-ttu-id="b18d5-391">Dize</span><span class="sxs-lookup"><span data-stu-id="b18d5-391">string</span></span> | |

## <a name="page-view-performance"></a><span data-ttu-id="b18d5-392">Sayfa görünümü performansı</span><span class="sxs-lookup"><span data-stu-id="b18d5-392">Page View Performance</span></span>
<span data-ttu-id="b18d5-393">Merhaba tarayıcı tarafından gönderilen.</span><span class="sxs-lookup"><span data-stu-id="b18d5-393">Sent by hello browser.</span></span> <span data-ttu-id="b18d5-394">Ölçüler zaman tooprocess bir sayfadan kullanıcı başlatma hello isteği toodisplay (zaman uyumsuz AJAX çağrıları hariç) tam hello.</span><span class="sxs-lookup"><span data-stu-id="b18d5-394">Measures hello time tooprocess a page, from user initiating hello request toodisplay complete (excluding async AJAX calls).</span></span>

<span data-ttu-id="b18d5-395">Bağlam değerleri, istemci işletim sistemi ve tarayıcı sürümü gösterir.</span><span class="sxs-lookup"><span data-stu-id="b18d5-395">Context values show client OS and browser version.</span></span>

| <span data-ttu-id="b18d5-396">Yol</span><span class="sxs-lookup"><span data-stu-id="b18d5-396">Path</span></span> | <span data-ttu-id="b18d5-397">Tür</span><span class="sxs-lookup"><span data-stu-id="b18d5-397">Type</span></span> | <span data-ttu-id="b18d5-398">Notlar</span><span class="sxs-lookup"><span data-stu-id="b18d5-398">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b18d5-399">clientPerformance [0] clientProcess.value</span><span class="sxs-lookup"><span data-stu-id="b18d5-399">clientPerformance [0] clientProcess.value</span></span> |<span data-ttu-id="b18d5-400">tamsayı</span><span class="sxs-lookup"><span data-stu-id="b18d5-400">integer</span></span> |<span data-ttu-id="b18d5-401">Merhaba HTML toodisplaying hello sayfası alma bitiş saati.</span><span class="sxs-lookup"><span data-stu-id="b18d5-401">Time from end of receiving hello HTML toodisplaying hello page.</span></span> |
| <span data-ttu-id="b18d5-402">clientPerformance [0] adı</span><span class="sxs-lookup"><span data-stu-id="b18d5-402">clientPerformance [0] name</span></span> |<span data-ttu-id="b18d5-403">Dize</span><span class="sxs-lookup"><span data-stu-id="b18d5-403">string</span></span> | |
| <span data-ttu-id="b18d5-404">clientPerformance [0] networkConnection.value</span><span class="sxs-lookup"><span data-stu-id="b18d5-404">clientPerformance [0] networkConnection.value</span></span> |<span data-ttu-id="b18d5-405">tamsayı</span><span class="sxs-lookup"><span data-stu-id="b18d5-405">integer</span></span> |<span data-ttu-id="b18d5-406">Bir ağ bağlantısı tooestablish geçen süre.</span><span class="sxs-lookup"><span data-stu-id="b18d5-406">Time taken tooestablish a network connection.</span></span> |
| <span data-ttu-id="b18d5-407">clientPerformance [0] receiveRequest.value</span><span class="sxs-lookup"><span data-stu-id="b18d5-407">clientPerformance [0] receiveRequest.value</span></span> |<span data-ttu-id="b18d5-408">tamsayı</span><span class="sxs-lookup"><span data-stu-id="b18d5-408">integer</span></span> |<span data-ttu-id="b18d5-409">Merhaba isteği tooreceiving hello HTML yanıta gönderme bitiş saati.</span><span class="sxs-lookup"><span data-stu-id="b18d5-409">Time from end of sending hello request tooreceiving hello HTML in reply.</span></span> |
| <span data-ttu-id="b18d5-410">clientPerformance [0] sendRequest.value</span><span class="sxs-lookup"><span data-stu-id="b18d5-410">clientPerformance [0] sendRequest.value</span></span> |<span data-ttu-id="b18d5-411">tamsayı</span><span class="sxs-lookup"><span data-stu-id="b18d5-411">integer</span></span> |<span data-ttu-id="b18d5-412">Saat çekildiği toosend hello HTTP istek.</span><span class="sxs-lookup"><span data-stu-id="b18d5-412">Time from taken toosend hello HTTP request.</span></span> |
| <span data-ttu-id="b18d5-413">clientPerformance [0] total.value</span><span class="sxs-lookup"><span data-stu-id="b18d5-413">clientPerformance [0] total.value</span></span> |<span data-ttu-id="b18d5-414">tamsayı</span><span class="sxs-lookup"><span data-stu-id="b18d5-414">integer</span></span> |<span data-ttu-id="b18d5-415">Toosend hello isteği toodisplaying hello sayfası başlatılmasını süre.</span><span class="sxs-lookup"><span data-stu-id="b18d5-415">Time from starting toosend hello request toodisplaying hello page.</span></span> |
| <span data-ttu-id="b18d5-416">clientPerformance [0] URL'si</span><span class="sxs-lookup"><span data-stu-id="b18d5-416">clientPerformance [0] url</span></span> |<span data-ttu-id="b18d5-417">Dize</span><span class="sxs-lookup"><span data-stu-id="b18d5-417">string</span></span> |<span data-ttu-id="b18d5-418">Bu istek URL'si</span><span class="sxs-lookup"><span data-stu-id="b18d5-418">URL of this request</span></span> |
| <span data-ttu-id="b18d5-419">clientPerformance [0] urlData.base</span><span class="sxs-lookup"><span data-stu-id="b18d5-419">clientPerformance [0] urlData.base</span></span> |<span data-ttu-id="b18d5-420">Dize</span><span class="sxs-lookup"><span data-stu-id="b18d5-420">string</span></span> | |
| <span data-ttu-id="b18d5-421">clientPerformance [0] urlData.hashTag</span><span class="sxs-lookup"><span data-stu-id="b18d5-421">clientPerformance [0] urlData.hashTag</span></span> |<span data-ttu-id="b18d5-422">Dize</span><span class="sxs-lookup"><span data-stu-id="b18d5-422">string</span></span> | |
| <span data-ttu-id="b18d5-423">clientPerformance [0] urlData.host</span><span class="sxs-lookup"><span data-stu-id="b18d5-423">clientPerformance [0] urlData.host</span></span> |<span data-ttu-id="b18d5-424">Dize</span><span class="sxs-lookup"><span data-stu-id="b18d5-424">string</span></span> | |
| <span data-ttu-id="b18d5-425">clientPerformance [0] urlData.protocol</span><span class="sxs-lookup"><span data-stu-id="b18d5-425">clientPerformance [0] urlData.protocol</span></span> |<span data-ttu-id="b18d5-426">Dize</span><span class="sxs-lookup"><span data-stu-id="b18d5-426">string</span></span> | |

## <a name="page-views"></a><span data-ttu-id="b18d5-427">Sayfa görünümleri</span><span class="sxs-lookup"><span data-stu-id="b18d5-427">Page Views</span></span>
<span data-ttu-id="b18d5-428">TrackPageView() tarafından gönderilen veya [stopTrackPage](app-insights-api-custom-events-metrics.md#page-views)</span><span class="sxs-lookup"><span data-stu-id="b18d5-428">Sent by trackPageView() or [stopTrackPage](app-insights-api-custom-events-metrics.md#page-views)</span></span>

| <span data-ttu-id="b18d5-429">Yol</span><span class="sxs-lookup"><span data-stu-id="b18d5-429">Path</span></span> | <span data-ttu-id="b18d5-430">Tür</span><span class="sxs-lookup"><span data-stu-id="b18d5-430">Type</span></span> | <span data-ttu-id="b18d5-431">Notlar</span><span class="sxs-lookup"><span data-stu-id="b18d5-431">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b18d5-432">Görünüm [0] sayısı</span><span class="sxs-lookup"><span data-stu-id="b18d5-432">view [0] count</span></span> |<span data-ttu-id="b18d5-433">tamsayı</span><span class="sxs-lookup"><span data-stu-id="b18d5-433">integer</span></span> |<span data-ttu-id="b18d5-434">100 / ([örnekleme](app-insights-sampling.md) hızı).</span><span class="sxs-lookup"><span data-stu-id="b18d5-434">100/([sampling](app-insights-sampling.md) rate).</span></span> <span data-ttu-id="b18d5-435">Örneğin 4 =&gt; % 25.</span><span class="sxs-lookup"><span data-stu-id="b18d5-435">For example 4 =&gt; 25%.</span></span> |
| <span data-ttu-id="b18d5-436">Görünüm [0] durationMetric.value</span><span class="sxs-lookup"><span data-stu-id="b18d5-436">view [0] durationMetric.value</span></span> |<span data-ttu-id="b18d5-437">tamsayı</span><span class="sxs-lookup"><span data-stu-id="b18d5-437">integer</span></span> |<span data-ttu-id="b18d5-438">Değeri trackPageView() veya startTrackPage() - isteğe bağlı olarak ayarlanmış stopTrackPage().</span><span class="sxs-lookup"><span data-stu-id="b18d5-438">Value optionally set in trackPageView() or by startTrackPage() - stopTrackPage().</span></span> <span data-ttu-id="b18d5-439">Aynı clientPerformance değerleri olarak hello değil.</span><span class="sxs-lookup"><span data-stu-id="b18d5-439">Not hello same as clientPerformance values.</span></span> |
| <span data-ttu-id="b18d5-440">Görünüm [0] adı</span><span class="sxs-lookup"><span data-stu-id="b18d5-440">view [0] name</span></span> |<span data-ttu-id="b18d5-441">Dize</span><span class="sxs-lookup"><span data-stu-id="b18d5-441">string</span></span> |<span data-ttu-id="b18d5-442">Sayfa başlığı.</span><span class="sxs-lookup"><span data-stu-id="b18d5-442">Page title.</span></span>  <span data-ttu-id="b18d5-443">En fazla uzunluk 250</span><span class="sxs-lookup"><span data-stu-id="b18d5-443">Max length 250</span></span> |
| <span data-ttu-id="b18d5-444">Görünüm [0] URL'si</span><span class="sxs-lookup"><span data-stu-id="b18d5-444">view [0] url</span></span> |<span data-ttu-id="b18d5-445">Dize</span><span class="sxs-lookup"><span data-stu-id="b18d5-445">string</span></span> | |
| <span data-ttu-id="b18d5-446">Görünüm [0] urlData.base</span><span class="sxs-lookup"><span data-stu-id="b18d5-446">view [0] urlData.base</span></span> |<span data-ttu-id="b18d5-447">Dize</span><span class="sxs-lookup"><span data-stu-id="b18d5-447">string</span></span> | |
| <span data-ttu-id="b18d5-448">Görünüm [0] urlData.hashTag</span><span class="sxs-lookup"><span data-stu-id="b18d5-448">view [0] urlData.hashTag</span></span> |<span data-ttu-id="b18d5-449">Dize</span><span class="sxs-lookup"><span data-stu-id="b18d5-449">string</span></span> | |
| <span data-ttu-id="b18d5-450">Görünüm [0] urlData.host</span><span class="sxs-lookup"><span data-stu-id="b18d5-450">view [0] urlData.host</span></span> |<span data-ttu-id="b18d5-451">Dize</span><span class="sxs-lookup"><span data-stu-id="b18d5-451">string</span></span> | |

## <a name="availability"></a><span data-ttu-id="b18d5-452">Kullanılabilirlik</span><span class="sxs-lookup"><span data-stu-id="b18d5-452">Availability</span></span>
<span data-ttu-id="b18d5-453">Raporları [kullanılabilirlik web testleri](app-insights-monitor-web-app-availability.md).</span><span class="sxs-lookup"><span data-stu-id="b18d5-453">Reports [availability web tests](app-insights-monitor-web-app-availability.md).</span></span>

| <span data-ttu-id="b18d5-454">Yol</span><span class="sxs-lookup"><span data-stu-id="b18d5-454">Path</span></span> | <span data-ttu-id="b18d5-455">Tür</span><span class="sxs-lookup"><span data-stu-id="b18d5-455">Type</span></span> | <span data-ttu-id="b18d5-456">Notlar</span><span class="sxs-lookup"><span data-stu-id="b18d5-456">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b18d5-457">Kullanılabilirlik [0] availabilityMetric.name</span><span class="sxs-lookup"><span data-stu-id="b18d5-457">availability [0] availabilityMetric.name</span></span> |<span data-ttu-id="b18d5-458">Dize</span><span class="sxs-lookup"><span data-stu-id="b18d5-458">string</span></span> |<span data-ttu-id="b18d5-459">availability</span><span class="sxs-lookup"><span data-stu-id="b18d5-459">availability</span></span> |
| <span data-ttu-id="b18d5-460">Kullanılabilirlik [0] availabilityMetric.value</span><span class="sxs-lookup"><span data-stu-id="b18d5-460">availability [0] availabilityMetric.value</span></span> |<span data-ttu-id="b18d5-461">Sayı</span><span class="sxs-lookup"><span data-stu-id="b18d5-461">number</span></span> |<span data-ttu-id="b18d5-462">1.0 veya 0,0</span><span class="sxs-lookup"><span data-stu-id="b18d5-462">1.0 or 0.0</span></span> |
| <span data-ttu-id="b18d5-463">Kullanılabilirlik [0] sayısı</span><span class="sxs-lookup"><span data-stu-id="b18d5-463">availability [0] count</span></span> |<span data-ttu-id="b18d5-464">tamsayı</span><span class="sxs-lookup"><span data-stu-id="b18d5-464">integer</span></span> |<span data-ttu-id="b18d5-465">100 / ([örnekleme](app-insights-sampling.md) hızı).</span><span class="sxs-lookup"><span data-stu-id="b18d5-465">100/([sampling](app-insights-sampling.md) rate).</span></span> <span data-ttu-id="b18d5-466">Örneğin 4 =&gt; % 25.</span><span class="sxs-lookup"><span data-stu-id="b18d5-466">For example 4 =&gt; 25%.</span></span> |
| <span data-ttu-id="b18d5-467">Kullanılabilirlik [0] dataSizeMetric.name</span><span class="sxs-lookup"><span data-stu-id="b18d5-467">availability [0] dataSizeMetric.name</span></span> |<span data-ttu-id="b18d5-468">Dize</span><span class="sxs-lookup"><span data-stu-id="b18d5-468">string</span></span> | |
| <span data-ttu-id="b18d5-469">Kullanılabilirlik [0] dataSizeMetric.value</span><span class="sxs-lookup"><span data-stu-id="b18d5-469">availability [0] dataSizeMetric.value</span></span> |<span data-ttu-id="b18d5-470">tamsayı</span><span class="sxs-lookup"><span data-stu-id="b18d5-470">integer</span></span> | |
| <span data-ttu-id="b18d5-471">Kullanılabilirlik [0] durationMetric.name</span><span class="sxs-lookup"><span data-stu-id="b18d5-471">availability [0] durationMetric.name</span></span> |<span data-ttu-id="b18d5-472">Dize</span><span class="sxs-lookup"><span data-stu-id="b18d5-472">string</span></span> | |
| <span data-ttu-id="b18d5-473">Kullanılabilirlik [0] durationMetric.value</span><span class="sxs-lookup"><span data-stu-id="b18d5-473">availability [0] durationMetric.value</span></span> |<span data-ttu-id="b18d5-474">Sayı</span><span class="sxs-lookup"><span data-stu-id="b18d5-474">number</span></span> |<span data-ttu-id="b18d5-475">Test süresi.</span><span class="sxs-lookup"><span data-stu-id="b18d5-475">Duration of test.</span></span> <span data-ttu-id="b18d5-476">1e7 1'ler ==</span><span class="sxs-lookup"><span data-stu-id="b18d5-476">1e7==1s</span></span> |
| <span data-ttu-id="b18d5-477">Kullanılabilirlik [0] iletisi</span><span class="sxs-lookup"><span data-stu-id="b18d5-477">availability [0] message</span></span> |<span data-ttu-id="b18d5-478">Dize</span><span class="sxs-lookup"><span data-stu-id="b18d5-478">string</span></span> |<span data-ttu-id="b18d5-479">Hata tanılama</span><span class="sxs-lookup"><span data-stu-id="b18d5-479">Failure diagnostic</span></span> |
| <span data-ttu-id="b18d5-480">Kullanılabilirlik [0] sonucu</span><span class="sxs-lookup"><span data-stu-id="b18d5-480">availability [0] result</span></span> |<span data-ttu-id="b18d5-481">Dize</span><span class="sxs-lookup"><span data-stu-id="b18d5-481">string</span></span> |<span data-ttu-id="b18d5-482">Geçişi/başarısız</span><span class="sxs-lookup"><span data-stu-id="b18d5-482">Pass/Fail</span></span> |
| <span data-ttu-id="b18d5-483">Kullanılabilirlik [0] runLocation</span><span class="sxs-lookup"><span data-stu-id="b18d5-483">availability [0] runLocation</span></span> |<span data-ttu-id="b18d5-484">Dize</span><span class="sxs-lookup"><span data-stu-id="b18d5-484">string</span></span> |<span data-ttu-id="b18d5-485">Http isteği coğrafi kaynağı</span><span class="sxs-lookup"><span data-stu-id="b18d5-485">Geo source of http req</span></span> |
| <span data-ttu-id="b18d5-486">Kullanılabilirlik [0] testName</span><span class="sxs-lookup"><span data-stu-id="b18d5-486">availability [0] testName</span></span> |<span data-ttu-id="b18d5-487">Dize</span><span class="sxs-lookup"><span data-stu-id="b18d5-487">string</span></span> | |
| <span data-ttu-id="b18d5-488">Kullanılabilirlik [0] testRunId</span><span class="sxs-lookup"><span data-stu-id="b18d5-488">availability [0] testRunId</span></span> |<span data-ttu-id="b18d5-489">Dize</span><span class="sxs-lookup"><span data-stu-id="b18d5-489">string</span></span> | |
| <span data-ttu-id="b18d5-490">Kullanılabilirlik [0] testTimestamp</span><span class="sxs-lookup"><span data-stu-id="b18d5-490">availability [0] testTimestamp</span></span> |<span data-ttu-id="b18d5-491">Dize</span><span class="sxs-lookup"><span data-stu-id="b18d5-491">string</span></span> | |

## <a name="metrics"></a><span data-ttu-id="b18d5-492">Ölçümler</span><span class="sxs-lookup"><span data-stu-id="b18d5-492">Metrics</span></span>
<span data-ttu-id="b18d5-493">TrackMetric() tarafından oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="b18d5-493">Generated by TrackMetric().</span></span>

<span data-ttu-id="b18d5-494">Merhaba ölçüm değeri context.custom.metrics[0 içinde bulundu]</span><span class="sxs-lookup"><span data-stu-id="b18d5-494">hello metric value is found in context.custom.metrics[0]</span></span>

<span data-ttu-id="b18d5-495">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="b18d5-495">For example:</span></span>

    {
     "metric": [ ],
     "context": {
     ...
     "custom": {
        "dimensions": [
          { "ProcessId": "4068" }
        ],
        "metrics": [
          {
            "dispatchRate": {
              "value": 0.001295,
              "count": 1.0,
              "min": 0.001295,
              "max": 0.001295,
              "stdDev": 0.0,
              "sampledValue": 0.001295,
              "sum": 0.001295
            }
          }
         } ] }
    }

## <a name="about-metric-values"></a><span data-ttu-id="b18d5-496">Ölçüm değerleri hakkında</span><span class="sxs-lookup"><span data-stu-id="b18d5-496">About metric values</span></span>
<span data-ttu-id="b18d5-497">Ölçüm değerleri, hem ölçüm raporlar ve diğer yerlerde, standart nesne yapısıyla raporlanır.</span><span class="sxs-lookup"><span data-stu-id="b18d5-497">Metric values, both in metric reports and elsewhere, are reported with a standard object structure.</span></span> <span data-ttu-id="b18d5-498">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="b18d5-498">For example:</span></span>

      "durationMetric": {
        "name": "contoso.org",
        "type": "Aggregation",
        "value": 468.71603053650279,
        "count": 1.0,
        "min": 468.71603053650279,
        "max": 468.71603053650279,
        "stdDev": 0.0,
        "sampledValue": 468.71603053650279
      }

<span data-ttu-id="b18d5-499">Şu anda - yine de bu değişebilir hello gelecekteki - hello standart SDK modüllerden bildirilen tüm değerler de `count==1` ve yalnızca hello `name` ve `value` alanları kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="b18d5-499">Currently - though this might change in hello future - in all values reported from hello standard SDK modules, `count==1` and only hello `name` and `value` fields are useful.</span></span> <span data-ttu-id="b18d5-500">Merhaba, bunlar olacak farklı yalnızca durumda kendi TrackMetric çağrıları yazma durumunda olur, diğer parametreler hello kümesindeki.</span><span class="sxs-lookup"><span data-stu-id="b18d5-500">hello only case where they would be different would be if you write your own TrackMetric calls in which you set hello other parameters.</span></span>

<span data-ttu-id="b18d5-501">Merhaba amacı hello diğer alanları olan tooallow ölçümleri toobe hello SDK, tooreduce trafiği toohello portalı bir araya getirilir.</span><span class="sxs-lookup"><span data-stu-id="b18d5-501">hello purpose of hello other fields is tooallow metrics toobe aggregated in hello SDK, tooreduce traffic toohello portal.</span></span> <span data-ttu-id="b18d5-502">Örneğin, her bir ölçüm raporu göndermeden önce birkaç art arda okumalar ortalama.</span><span class="sxs-lookup"><span data-stu-id="b18d5-502">For example, you could average several successive readings before sending each metric report.</span></span> <span data-ttu-id="b18d5-503">Ardından hello min, max, standart sapma ve toplam değeri (sum veya ortalama) hesaplamak ve sayısı toohello hello rapor tarafından temsil edilen okumalar sayısını ayarlamak.</span><span class="sxs-lookup"><span data-stu-id="b18d5-503">Then you would calculate hello min, max, standard deviation and aggregate value (sum or average) and set count toohello number of readings represented by hello report.</span></span>

<span data-ttu-id="b18d5-504">Merhaba yukarıdaki tablolarda, biz hello nadiren kullanılan alanları sayısı, min, max, stdDev ve sampledValue atlamış.</span><span class="sxs-lookup"><span data-stu-id="b18d5-504">In hello tables above, we have omitted hello rarely-used fields count, min, max, stdDev and sampledValue.</span></span>

<span data-ttu-id="b18d5-505">Önceden bir araya getirildiği ölçümleri yerine kullanabileceğiniz [örnekleme](app-insights-sampling.md) tooreduce hello birim telemetri gerekiyorsa.</span><span class="sxs-lookup"><span data-stu-id="b18d5-505">Instead of pre-aggregating metrics, you can use [sampling](app-insights-sampling.md) if you need tooreduce hello volume of telemetry.</span></span>

### <a name="durations"></a><span data-ttu-id="b18d5-506">Süreleri</span><span class="sxs-lookup"><span data-stu-id="b18d5-506">Durations</span></span>
<span data-ttu-id="b18d5-507">Aksi takdirde belirtilenler dışında süreleri 10000000.0 1 saniye anlamına bir milisaniyeye onda içinde gösterilir.</span><span class="sxs-lookup"><span data-stu-id="b18d5-507">Except where otherwise noted, durations are represented in tenths of a microsecond, so that 10000000.0 means 1 second.</span></span>

## <a name="see-also"></a><span data-ttu-id="b18d5-508">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="b18d5-508">See also</span></span>
* [<span data-ttu-id="b18d5-509">Application Insights</span><span class="sxs-lookup"><span data-stu-id="b18d5-509">Application Insights</span></span>](app-insights-overview.md)
* [<span data-ttu-id="b18d5-510">Sürekli dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="b18d5-510">Continuous Export</span></span>](app-insights-export-telemetry.md)
* [<span data-ttu-id="b18d5-511">Kod örnekleri</span><span class="sxs-lookup"><span data-stu-id="b18d5-511">Code samples</span></span>](app-insights-export-telemetry.md#code-samples)
