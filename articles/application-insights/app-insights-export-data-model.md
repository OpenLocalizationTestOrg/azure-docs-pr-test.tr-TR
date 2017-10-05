---
title: "Azure uygulama Öngörüler veri modeli | Microsoft Docs"
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
ms.openlocfilehash: a485ddd555f65473d81896effc4a3562bda71410
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="application-insights-export-data-model"></a><span data-ttu-id="8d8ef-103">Uygulama Öngörüler dışarı aktarma veri modeli</span><span class="sxs-lookup"><span data-stu-id="8d8ef-103">Application Insights Export Data Model</span></span>
<span data-ttu-id="8d8ef-104">Bu tabloda telemetri gönderildiği özelliklerini [Application Insights](app-insights-overview.md) SDK'ları portalı.</span><span class="sxs-lookup"><span data-stu-id="8d8ef-104">This table lists the properties of telemetry sent from the [Application Insights](app-insights-overview.md) SDKs to the portal.</span></span>
<span data-ttu-id="8d8ef-105">Bu özellikler, veri çıkışı görürsünüz [sürekli verme](app-insights-export-telemetry.md).</span><span class="sxs-lookup"><span data-stu-id="8d8ef-105">You'll see these properties in data output from [Continuous Export](app-insights-export-telemetry.md).</span></span>
<span data-ttu-id="8d8ef-106">Ayrıca özellik filtrelerini görüntülendikleri [ölçüm Gezgini](app-insights-metrics-explorer.md) ve [tanılama arama](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="8d8ef-106">They also appear in property filters in [Metric Explorer](app-insights-metrics-explorer.md) and [Diagnostic Search](app-insights-diagnostic-search.md).</span></span>

<span data-ttu-id="8d8ef-107">Dikkat edilecek noktalar:</span><span class="sxs-lookup"><span data-stu-id="8d8ef-107">Points to note:</span></span>

* <span data-ttu-id="8d8ef-108">`[0]`Bu tablolarda dizin eklemek için sahip olduğu yolu noktasında gösterir; ancak her zaman değil 0.</span><span class="sxs-lookup"><span data-stu-id="8d8ef-108">`[0]` in these tables denotes a point in the path where you have to insert an index; but it isn't always 0.</span></span>
* <span data-ttu-id="8d8ef-109">Süreler milisaniyeye, bu nedenle 10000000 onda içinde olan 1 saniye ==.</span><span class="sxs-lookup"><span data-stu-id="8d8ef-109">Time durations are in tenths of a microsecond, so 10000000 == 1 second.</span></span>
* <span data-ttu-id="8d8ef-110">Tarihler ve saatler UTC olan ve ISO biçiminde verilir.`yyyy-MM-DDThh:mm:ss.sssZ`</span><span class="sxs-lookup"><span data-stu-id="8d8ef-110">Dates and times are UTC, and are given in the ISO format `yyyy-MM-DDThh:mm:ss.sssZ`</span></span>


## <a name="example"></a><span data-ttu-id="8d8ef-111">Örnek</span><span class="sxs-lookup"><span data-stu-id="8d8ef-111">Example</span></span>
    // A server report about an HTTP request
    {
    "request": [
      {
        "urlData": { // derived from 'url'
          "host": "contoso.org",
          "base": "/",
          "hashTag": ""
        },
        "responseCode": 200, // Sent to client
        "success": true, // Default == responseCode<400
        // Request id becomes the operation id of child events
        "id": "fCOhCdCnZ9I=",  
        "name": "GET Home/Index",
        "count": 1, // 100% / sampling rate
        "durationMetric": {
          "value": 1046804.0, // 10000000 == 1 second
          // Currently the following fields are redundant:
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
        // last octagon is anonymized to 0 at portal:
        "clientip": "168.62.177.0",
        "province": "",
        "city": ""
      },
      "data": {
        "isSynthetic": true, // we identified source as a bot
        // percentage of generated data sent to portal:
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
  <span data-ttu-id="8d8ef-112">}</span><span class="sxs-lookup"><span data-stu-id="8d8ef-112">}</span></span>

## <a name="context"></a><span data-ttu-id="8d8ef-113">Bağlam</span><span class="sxs-lookup"><span data-stu-id="8d8ef-113">Context</span></span>
<span data-ttu-id="8d8ef-114">Tüm telemetri türlerini içerik bölümü tarafından yayımlanır.</span><span class="sxs-lookup"><span data-stu-id="8d8ef-114">All types of telemetry are accompanied by a context section.</span></span> <span data-ttu-id="8d8ef-115">Bu alanların tümünü her veri noktası ile aktarılır.</span><span class="sxs-lookup"><span data-stu-id="8d8ef-115">Not all of these fields are transmitted with every data point.</span></span>

| <span data-ttu-id="8d8ef-116">Yol</span><span class="sxs-lookup"><span data-stu-id="8d8ef-116">Path</span></span> | <span data-ttu-id="8d8ef-117">Tür</span><span class="sxs-lookup"><span data-stu-id="8d8ef-117">Type</span></span> | <span data-ttu-id="8d8ef-118">Notlar</span><span class="sxs-lookup"><span data-stu-id="8d8ef-118">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8d8ef-119">Context.Custom.Dimensions [0]</span><span class="sxs-lookup"><span data-stu-id="8d8ef-119">context.custom.dimensions [0]</span></span> |<span data-ttu-id="8d8ef-120">Nesne]</span><span class="sxs-lookup"><span data-stu-id="8d8ef-120">object [ ]</span></span> |<span data-ttu-id="8d8ef-121">Anahtar-değer çiftleri özel özellikler parametresiyle ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="8d8ef-121">Key-value string pairs set by custom properties parameter.</span></span> <span data-ttu-id="8d8ef-122">Anahtar uzunluğu en fazla 100, en fazla uzunluğu 1024 değerleri.</span><span class="sxs-lookup"><span data-stu-id="8d8ef-122">Key max length 100, values max length 1024.</span></span> <span data-ttu-id="8d8ef-123">100'den fazla benzersiz değer özelliği aranabilecek ancak kesimleme kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="8d8ef-123">More than 100 unique values, the property can be searched but cannot be used for segmentation.</span></span> <span data-ttu-id="8d8ef-124">İkey başına en fazla 200 anahtarları.</span><span class="sxs-lookup"><span data-stu-id="8d8ef-124">Max 200 keys per ikey.</span></span> |
| <span data-ttu-id="8d8ef-125">Context.Custom.Metrics [0]</span><span class="sxs-lookup"><span data-stu-id="8d8ef-125">context.custom.metrics [0]</span></span> |<span data-ttu-id="8d8ef-126">Nesne]</span><span class="sxs-lookup"><span data-stu-id="8d8ef-126">object [ ]</span></span> |<span data-ttu-id="8d8ef-127">Anahtar-değer çiftleri TrackMetrics ve özel ölçümleri parametresi tarafından ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="8d8ef-127">Key-value pairs set by custom measurements parameter and by TrackMetrics.</span></span> <span data-ttu-id="8d8ef-128">Anahtar en büyük uzunluğunu 100 değerleri sayısal olabilir.</span><span class="sxs-lookup"><span data-stu-id="8d8ef-128">Key max length 100, values may be numeric.</span></span> |
| <span data-ttu-id="8d8ef-129">context.data.eventTime</span><span class="sxs-lookup"><span data-stu-id="8d8ef-129">context.data.eventTime</span></span> |<span data-ttu-id="8d8ef-130">Dize</span><span class="sxs-lookup"><span data-stu-id="8d8ef-130">string</span></span> |<span data-ttu-id="8d8ef-131">UTC</span><span class="sxs-lookup"><span data-stu-id="8d8ef-131">UTC</span></span> |
| <span data-ttu-id="8d8ef-132">context.data.isSynthetic</span><span class="sxs-lookup"><span data-stu-id="8d8ef-132">context.data.isSynthetic</span></span> |<span data-ttu-id="8d8ef-133">Boole değeri</span><span class="sxs-lookup"><span data-stu-id="8d8ef-133">boolean</span></span> |<span data-ttu-id="8d8ef-134">İstek bir bot veya web testi görünür.</span><span class="sxs-lookup"><span data-stu-id="8d8ef-134">Request appears to come from a bot or web test.</span></span> |
| <span data-ttu-id="8d8ef-135">context.data.samplingRate</span><span class="sxs-lookup"><span data-stu-id="8d8ef-135">context.data.samplingRate</span></span> |<span data-ttu-id="8d8ef-136">Sayı</span><span class="sxs-lookup"><span data-stu-id="8d8ef-136">number</span></span> |<span data-ttu-id="8d8ef-137">Portala gönderilen SDK'sı tarafından oluşturulan telemetri yüzdesi.</span><span class="sxs-lookup"><span data-stu-id="8d8ef-137">Percentage of telemetry generated by the SDK that is sent to portal.</span></span> <span data-ttu-id="8d8ef-138">0,0 100.0 aralığı.</span><span class="sxs-lookup"><span data-stu-id="8d8ef-138">Range 0.0-100.0.</span></span> |
| <span data-ttu-id="8d8ef-139">Context.Device</span><span class="sxs-lookup"><span data-stu-id="8d8ef-139">context.device</span></span> |<span data-ttu-id="8d8ef-140">Nesne</span><span class="sxs-lookup"><span data-stu-id="8d8ef-140">object</span></span> |<span data-ttu-id="8d8ef-141">İstemci aygıtı</span><span class="sxs-lookup"><span data-stu-id="8d8ef-141">Client device</span></span> |
| <span data-ttu-id="8d8ef-142">Context.Device.browser</span><span class="sxs-lookup"><span data-stu-id="8d8ef-142">context.device.browser</span></span> |<span data-ttu-id="8d8ef-143">Dize</span><span class="sxs-lookup"><span data-stu-id="8d8ef-143">string</span></span> |<span data-ttu-id="8d8ef-144">IE, Chrome...</span><span class="sxs-lookup"><span data-stu-id="8d8ef-144">IE, Chrome, ...</span></span> |
| <span data-ttu-id="8d8ef-145">context.device.browserVersion</span><span class="sxs-lookup"><span data-stu-id="8d8ef-145">context.device.browserVersion</span></span> |<span data-ttu-id="8d8ef-146">Dize</span><span class="sxs-lookup"><span data-stu-id="8d8ef-146">string</span></span> |<span data-ttu-id="8d8ef-147">Chrome 48,0...</span><span class="sxs-lookup"><span data-stu-id="8d8ef-147">Chrome 48.0, ...</span></span> |
| <span data-ttu-id="8d8ef-148">context.device.deviceModel</span><span class="sxs-lookup"><span data-stu-id="8d8ef-148">context.device.deviceModel</span></span> |<span data-ttu-id="8d8ef-149">Dize</span><span class="sxs-lookup"><span data-stu-id="8d8ef-149">string</span></span> | |
| <span data-ttu-id="8d8ef-150">context.device.deviceName</span><span class="sxs-lookup"><span data-stu-id="8d8ef-150">context.device.deviceName</span></span> |<span data-ttu-id="8d8ef-151">Dize</span><span class="sxs-lookup"><span data-stu-id="8d8ef-151">string</span></span> | |
| <span data-ttu-id="8d8ef-152">Context.Device.id</span><span class="sxs-lookup"><span data-stu-id="8d8ef-152">context.device.id</span></span> |<span data-ttu-id="8d8ef-153">Dize</span><span class="sxs-lookup"><span data-stu-id="8d8ef-153">string</span></span> | |
| <span data-ttu-id="8d8ef-154">Context.Device.Locale</span><span class="sxs-lookup"><span data-stu-id="8d8ef-154">context.device.locale</span></span> |<span data-ttu-id="8d8ef-155">Dize</span><span class="sxs-lookup"><span data-stu-id="8d8ef-155">string</span></span> |<span data-ttu-id="8d8ef-156">tr GB, de-DE...</span><span class="sxs-lookup"><span data-stu-id="8d8ef-156">en-GB, de-DE, ...</span></span> |
| <span data-ttu-id="8d8ef-157">Context.Device.Network</span><span class="sxs-lookup"><span data-stu-id="8d8ef-157">context.device.network</span></span> |<span data-ttu-id="8d8ef-158">Dize</span><span class="sxs-lookup"><span data-stu-id="8d8ef-158">string</span></span> | |
| <span data-ttu-id="8d8ef-159">context.device.oemName</span><span class="sxs-lookup"><span data-stu-id="8d8ef-159">context.device.oemName</span></span> |<span data-ttu-id="8d8ef-160">Dize</span><span class="sxs-lookup"><span data-stu-id="8d8ef-160">string</span></span> | |
| <span data-ttu-id="8d8ef-161">context.device.osVersion</span><span class="sxs-lookup"><span data-stu-id="8d8ef-161">context.device.osVersion</span></span> |<span data-ttu-id="8d8ef-162">Dize</span><span class="sxs-lookup"><span data-stu-id="8d8ef-162">string</span></span> |<span data-ttu-id="8d8ef-163">Ana bilgisayar işletim sistemi</span><span class="sxs-lookup"><span data-stu-id="8d8ef-163">Host OS</span></span> |
| <span data-ttu-id="8d8ef-164">context.device.roleInstance</span><span class="sxs-lookup"><span data-stu-id="8d8ef-164">context.device.roleInstance</span></span> |<span data-ttu-id="8d8ef-165">Dize</span><span class="sxs-lookup"><span data-stu-id="8d8ef-165">string</span></span> |<span data-ttu-id="8d8ef-166">Sunucu ana bilgisayar kimliği</span><span class="sxs-lookup"><span data-stu-id="8d8ef-166">ID of server host</span></span> |
| <span data-ttu-id="8d8ef-167">context.device.roleName</span><span class="sxs-lookup"><span data-stu-id="8d8ef-167">context.device.roleName</span></span> |<span data-ttu-id="8d8ef-168">Dize</span><span class="sxs-lookup"><span data-stu-id="8d8ef-168">string</span></span> | |
| <span data-ttu-id="8d8ef-169">Context.Device.Type</span><span class="sxs-lookup"><span data-stu-id="8d8ef-169">context.device.type</span></span> |<span data-ttu-id="8d8ef-170">Dize</span><span class="sxs-lookup"><span data-stu-id="8d8ef-170">string</span></span> |<span data-ttu-id="8d8ef-171">Bilgisayar Tarayıcı...</span><span class="sxs-lookup"><span data-stu-id="8d8ef-171">PC, Browser, ...</span></span> |
| <span data-ttu-id="8d8ef-172">Context.location</span><span class="sxs-lookup"><span data-stu-id="8d8ef-172">context.location</span></span> |<span data-ttu-id="8d8ef-173">Nesne</span><span class="sxs-lookup"><span data-stu-id="8d8ef-173">object</span></span> |<span data-ttu-id="8d8ef-174">Clientip türetilmiş.</span><span class="sxs-lookup"><span data-stu-id="8d8ef-174">Derived from clientip.</span></span> |
| <span data-ttu-id="8d8ef-175">Context.location.City</span><span class="sxs-lookup"><span data-stu-id="8d8ef-175">context.location.city</span></span> |<span data-ttu-id="8d8ef-176">Dize</span><span class="sxs-lookup"><span data-stu-id="8d8ef-176">string</span></span> |<span data-ttu-id="8d8ef-177">Biliniyorsa clientip türetilmiş</span><span class="sxs-lookup"><span data-stu-id="8d8ef-177">Derived from clientip, if known</span></span> |
| <span data-ttu-id="8d8ef-178">Context.location.clientip</span><span class="sxs-lookup"><span data-stu-id="8d8ef-178">context.location.clientip</span></span> |<span data-ttu-id="8d8ef-179">Dize</span><span class="sxs-lookup"><span data-stu-id="8d8ef-179">string</span></span> |<span data-ttu-id="8d8ef-180">Son Sekizgene 0 olarak gizlidir.</span><span class="sxs-lookup"><span data-stu-id="8d8ef-180">Last octagon is anonymized to 0.</span></span> |
| <span data-ttu-id="8d8ef-181">Context.location.continent</span><span class="sxs-lookup"><span data-stu-id="8d8ef-181">context.location.continent</span></span> |<span data-ttu-id="8d8ef-182">Dize</span><span class="sxs-lookup"><span data-stu-id="8d8ef-182">string</span></span> | |
| <span data-ttu-id="8d8ef-183">Context.location.country</span><span class="sxs-lookup"><span data-stu-id="8d8ef-183">context.location.country</span></span> |<span data-ttu-id="8d8ef-184">Dize</span><span class="sxs-lookup"><span data-stu-id="8d8ef-184">string</span></span> | |
| <span data-ttu-id="8d8ef-185">Context.location.Province</span><span class="sxs-lookup"><span data-stu-id="8d8ef-185">context.location.province</span></span> |<span data-ttu-id="8d8ef-186">Dize</span><span class="sxs-lookup"><span data-stu-id="8d8ef-186">string</span></span> |<span data-ttu-id="8d8ef-187">Eyalet veya il</span><span class="sxs-lookup"><span data-stu-id="8d8ef-187">State or province</span></span> |
| <span data-ttu-id="8d8ef-188">Context.Operation.id</span><span class="sxs-lookup"><span data-stu-id="8d8ef-188">context.operation.id</span></span> |<span data-ttu-id="8d8ef-189">Dize</span><span class="sxs-lookup"><span data-stu-id="8d8ef-189">string</span></span> |<span data-ttu-id="8d8ef-190">Aynı işlem kimliğine sahip öğeler portalda ilgili öğeler gösterilir.</span><span class="sxs-lookup"><span data-stu-id="8d8ef-190">Items that have the same operation id are shown as Related Items in the portal.</span></span> <span data-ttu-id="8d8ef-191">Genellikle istek kimliği.</span><span class="sxs-lookup"><span data-stu-id="8d8ef-191">Usually the request id.</span></span> |
| <span data-ttu-id="8d8ef-192">Context.Operation.Name</span><span class="sxs-lookup"><span data-stu-id="8d8ef-192">context.operation.name</span></span> |<span data-ttu-id="8d8ef-193">Dize</span><span class="sxs-lookup"><span data-stu-id="8d8ef-193">string</span></span> |<span data-ttu-id="8d8ef-194">URL veya isteği adı</span><span class="sxs-lookup"><span data-stu-id="8d8ef-194">url or request name</span></span> |
| <span data-ttu-id="8d8ef-195">context.operation.parentId</span><span class="sxs-lookup"><span data-stu-id="8d8ef-195">context.operation.parentId</span></span> |<span data-ttu-id="8d8ef-196">Dize</span><span class="sxs-lookup"><span data-stu-id="8d8ef-196">string</span></span> |<span data-ttu-id="8d8ef-197">İç içe geçmiş ilgili öğeler sağlar.</span><span class="sxs-lookup"><span data-stu-id="8d8ef-197">Allows nested related items.</span></span> |
| <span data-ttu-id="8d8ef-198">Context.Session.id</span><span class="sxs-lookup"><span data-stu-id="8d8ef-198">context.session.id</span></span> |<span data-ttu-id="8d8ef-199">Dize</span><span class="sxs-lookup"><span data-stu-id="8d8ef-199">string</span></span> |<span data-ttu-id="8d8ef-200">Aynı kaynak işlemlerinin grubunun kimliği.</span><span class="sxs-lookup"><span data-stu-id="8d8ef-200">Id of a group of operations from the same source.</span></span> <span data-ttu-id="8d8ef-201">Bir işlem olmadan 30 dakikalık bir süre bir oturum sonuna işaret eder.</span><span class="sxs-lookup"><span data-stu-id="8d8ef-201">A period of 30 minutes without an operation signals the end of a session.</span></span> |
| <span data-ttu-id="8d8ef-202">context.session.isFirst</span><span class="sxs-lookup"><span data-stu-id="8d8ef-202">context.session.isFirst</span></span> |<span data-ttu-id="8d8ef-203">Boole değeri</span><span class="sxs-lookup"><span data-stu-id="8d8ef-203">boolean</span></span> | |
| <span data-ttu-id="8d8ef-204">context.user.accountAcquisitionDate</span><span class="sxs-lookup"><span data-stu-id="8d8ef-204">context.user.accountAcquisitionDate</span></span> |<span data-ttu-id="8d8ef-205">Dize</span><span class="sxs-lookup"><span data-stu-id="8d8ef-205">string</span></span> | |
| <span data-ttu-id="8d8ef-206">context.user.anonAcquisitionDate</span><span class="sxs-lookup"><span data-stu-id="8d8ef-206">context.user.anonAcquisitionDate</span></span> |<span data-ttu-id="8d8ef-207">Dize</span><span class="sxs-lookup"><span data-stu-id="8d8ef-207">string</span></span> | |
| <span data-ttu-id="8d8ef-208">context.user.anonId</span><span class="sxs-lookup"><span data-stu-id="8d8ef-208">context.user.anonId</span></span> |<span data-ttu-id="8d8ef-209">Dize</span><span class="sxs-lookup"><span data-stu-id="8d8ef-209">string</span></span> | |
| <span data-ttu-id="8d8ef-210">context.user.authAcquisitionDate</span><span class="sxs-lookup"><span data-stu-id="8d8ef-210">context.user.authAcquisitionDate</span></span> |<span data-ttu-id="8d8ef-211">Dize</span><span class="sxs-lookup"><span data-stu-id="8d8ef-211">string</span></span> |[<span data-ttu-id="8d8ef-212">Kimliği doğrulanmış kullanıcı</span><span class="sxs-lookup"><span data-stu-id="8d8ef-212">Authenticated User</span></span>](app-insights-api-custom-events-metrics.md#authenticated-users) |
| <span data-ttu-id="8d8ef-213">context.user.isAuthenticated</span><span class="sxs-lookup"><span data-stu-id="8d8ef-213">context.user.isAuthenticated</span></span> |<span data-ttu-id="8d8ef-214">Boole değeri</span><span class="sxs-lookup"><span data-stu-id="8d8ef-214">boolean</span></span> | |
| <span data-ttu-id="8d8ef-215">internal.data.documentVersion</span><span class="sxs-lookup"><span data-stu-id="8d8ef-215">internal.data.documentVersion</span></span> |<span data-ttu-id="8d8ef-216">Dize</span><span class="sxs-lookup"><span data-stu-id="8d8ef-216">string</span></span> | |
| <span data-ttu-id="8d8ef-217">internal.Data.id</span><span class="sxs-lookup"><span data-stu-id="8d8ef-217">internal.data.id</span></span> |<span data-ttu-id="8d8ef-218">Dize</span><span class="sxs-lookup"><span data-stu-id="8d8ef-218">string</span></span> | |

## <a name="events"></a><span data-ttu-id="8d8ef-219">Olaylar</span><span class="sxs-lookup"><span data-stu-id="8d8ef-219">Events</span></span>
<span data-ttu-id="8d8ef-220">Tarafından oluşturulan özel olaylar [TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent).</span><span class="sxs-lookup"><span data-stu-id="8d8ef-220">Custom events generated by [TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent).</span></span>

| <span data-ttu-id="8d8ef-221">Yol</span><span class="sxs-lookup"><span data-stu-id="8d8ef-221">Path</span></span> | <span data-ttu-id="8d8ef-222">Tür</span><span class="sxs-lookup"><span data-stu-id="8d8ef-222">Type</span></span> | <span data-ttu-id="8d8ef-223">Notlar</span><span class="sxs-lookup"><span data-stu-id="8d8ef-223">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8d8ef-224">[0] olay sayısı</span><span class="sxs-lookup"><span data-stu-id="8d8ef-224">event [0] count</span></span> |<span data-ttu-id="8d8ef-225">tamsayı</span><span class="sxs-lookup"><span data-stu-id="8d8ef-225">integer</span></span> |<span data-ttu-id="8d8ef-226">100 / ([örnekleme](app-insights-sampling.md) hızı).</span><span class="sxs-lookup"><span data-stu-id="8d8ef-226">100/([sampling](app-insights-sampling.md) rate).</span></span> <span data-ttu-id="8d8ef-227">Örneğin 4 =&gt; % 25.</span><span class="sxs-lookup"><span data-stu-id="8d8ef-227">For example 4 =&gt; 25%.</span></span> |
| <span data-ttu-id="8d8ef-228">Olay [0] adı</span><span class="sxs-lookup"><span data-stu-id="8d8ef-228">event [0] name</span></span> |<span data-ttu-id="8d8ef-229">Dize</span><span class="sxs-lookup"><span data-stu-id="8d8ef-229">string</span></span> |<span data-ttu-id="8d8ef-230">Olay adı.</span><span class="sxs-lookup"><span data-stu-id="8d8ef-230">Event name.</span></span>  <span data-ttu-id="8d8ef-231">En fazla uzunluk 250.</span><span class="sxs-lookup"><span data-stu-id="8d8ef-231">Max length 250.</span></span> |
| <span data-ttu-id="8d8ef-232">Olay [0] URL'si</span><span class="sxs-lookup"><span data-stu-id="8d8ef-232">event [0] url</span></span> |<span data-ttu-id="8d8ef-233">Dize</span><span class="sxs-lookup"><span data-stu-id="8d8ef-233">string</span></span> | |
| <span data-ttu-id="8d8ef-234">Olay [0] urlData.base</span><span class="sxs-lookup"><span data-stu-id="8d8ef-234">event [0] urlData.base</span></span> |<span data-ttu-id="8d8ef-235">Dize</span><span class="sxs-lookup"><span data-stu-id="8d8ef-235">string</span></span> | |
| <span data-ttu-id="8d8ef-236">Olay [0] urlData.host</span><span class="sxs-lookup"><span data-stu-id="8d8ef-236">event [0] urlData.host</span></span> |<span data-ttu-id="8d8ef-237">Dize</span><span class="sxs-lookup"><span data-stu-id="8d8ef-237">string</span></span> | |

## <a name="exceptions"></a><span data-ttu-id="8d8ef-238">Özel durumlar</span><span class="sxs-lookup"><span data-stu-id="8d8ef-238">Exceptions</span></span>
<span data-ttu-id="8d8ef-239">Raporları [özel durumları](app-insights-asp-net-exceptions.md) sunucu ve tarayıcı.</span><span class="sxs-lookup"><span data-stu-id="8d8ef-239">Reports [exceptions](app-insights-asp-net-exceptions.md) in the server and in the browser.</span></span>

| <span data-ttu-id="8d8ef-240">Yol</span><span class="sxs-lookup"><span data-stu-id="8d8ef-240">Path</span></span> | <span data-ttu-id="8d8ef-241">Tür</span><span class="sxs-lookup"><span data-stu-id="8d8ef-241">Type</span></span> | <span data-ttu-id="8d8ef-242">Notlar</span><span class="sxs-lookup"><span data-stu-id="8d8ef-242">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8d8ef-243">basicException [0] derlemesi</span><span class="sxs-lookup"><span data-stu-id="8d8ef-243">basicException [0] assembly</span></span> |<span data-ttu-id="8d8ef-244">Dize</span><span class="sxs-lookup"><span data-stu-id="8d8ef-244">string</span></span> | |
| <span data-ttu-id="8d8ef-245">basicException [0] sayısı</span><span class="sxs-lookup"><span data-stu-id="8d8ef-245">basicException [0] count</span></span> |<span data-ttu-id="8d8ef-246">tamsayı</span><span class="sxs-lookup"><span data-stu-id="8d8ef-246">integer</span></span> |<span data-ttu-id="8d8ef-247">100 / ([örnekleme](app-insights-sampling.md) hızı).</span><span class="sxs-lookup"><span data-stu-id="8d8ef-247">100/([sampling](app-insights-sampling.md) rate).</span></span> <span data-ttu-id="8d8ef-248">Örneğin 4 =&gt; % 25.</span><span class="sxs-lookup"><span data-stu-id="8d8ef-248">For example 4 =&gt; 25%.</span></span> |
| <span data-ttu-id="8d8ef-249">basicException [0] exceptionGroup</span><span class="sxs-lookup"><span data-stu-id="8d8ef-249">basicException [0] exceptionGroup</span></span> |<span data-ttu-id="8d8ef-250">Dize</span><span class="sxs-lookup"><span data-stu-id="8d8ef-250">string</span></span> | |
| <span data-ttu-id="8d8ef-251">basicException [0] exceptionType</span><span class="sxs-lookup"><span data-stu-id="8d8ef-251">basicException [0] exceptionType</span></span> |<span data-ttu-id="8d8ef-252">Dize</span><span class="sxs-lookup"><span data-stu-id="8d8ef-252">string</span></span> | |
| <span data-ttu-id="8d8ef-253">basicException [0] failedUserCodeMethod</span><span class="sxs-lookup"><span data-stu-id="8d8ef-253">basicException [0] failedUserCodeMethod</span></span> |<span data-ttu-id="8d8ef-254">Dize</span><span class="sxs-lookup"><span data-stu-id="8d8ef-254">string</span></span> | |
| <span data-ttu-id="8d8ef-255">basicException [0] failedUserCodeAssembly</span><span class="sxs-lookup"><span data-stu-id="8d8ef-255">basicException [0] failedUserCodeAssembly</span></span> |<span data-ttu-id="8d8ef-256">Dize</span><span class="sxs-lookup"><span data-stu-id="8d8ef-256">string</span></span> | |
| <span data-ttu-id="8d8ef-257">basicException [0] handledAt</span><span class="sxs-lookup"><span data-stu-id="8d8ef-257">basicException [0] handledAt</span></span> |<span data-ttu-id="8d8ef-258">Dize</span><span class="sxs-lookup"><span data-stu-id="8d8ef-258">string</span></span> | |
| <span data-ttu-id="8d8ef-259">basicException [0] hasFullStack</span><span class="sxs-lookup"><span data-stu-id="8d8ef-259">basicException [0] hasFullStack</span></span> |<span data-ttu-id="8d8ef-260">Boole değeri</span><span class="sxs-lookup"><span data-stu-id="8d8ef-260">boolean</span></span> | |
| <span data-ttu-id="8d8ef-261">basicException [0] kimliği</span><span class="sxs-lookup"><span data-stu-id="8d8ef-261">basicException [0] id</span></span> |<span data-ttu-id="8d8ef-262">Dize</span><span class="sxs-lookup"><span data-stu-id="8d8ef-262">string</span></span> | |
| <span data-ttu-id="8d8ef-263">basicException [0] yöntemi</span><span class="sxs-lookup"><span data-stu-id="8d8ef-263">basicException [0] method</span></span> |<span data-ttu-id="8d8ef-264">Dize</span><span class="sxs-lookup"><span data-stu-id="8d8ef-264">string</span></span> | |
| <span data-ttu-id="8d8ef-265">basicException [0] iletisi</span><span class="sxs-lookup"><span data-stu-id="8d8ef-265">basicException [0] message</span></span> |<span data-ttu-id="8d8ef-266">Dize</span><span class="sxs-lookup"><span data-stu-id="8d8ef-266">string</span></span> |<span data-ttu-id="8d8ef-267">Özel durum iletisi.</span><span class="sxs-lookup"><span data-stu-id="8d8ef-267">Exception message.</span></span> <span data-ttu-id="8d8ef-268">En fazla uzunluk 10k.</span><span class="sxs-lookup"><span data-stu-id="8d8ef-268">Max length 10k.</span></span> |
| <span data-ttu-id="8d8ef-269">basicException [0] outerExceptionMessage</span><span class="sxs-lookup"><span data-stu-id="8d8ef-269">basicException [0] outerExceptionMessage</span></span> |<span data-ttu-id="8d8ef-270">Dize</span><span class="sxs-lookup"><span data-stu-id="8d8ef-270">string</span></span> | |
| <span data-ttu-id="8d8ef-271">basicException [0] outerExceptionThrownAtAssembly</span><span class="sxs-lookup"><span data-stu-id="8d8ef-271">basicException [0] outerExceptionThrownAtAssembly</span></span> |<span data-ttu-id="8d8ef-272">Dize</span><span class="sxs-lookup"><span data-stu-id="8d8ef-272">string</span></span> | |
| <span data-ttu-id="8d8ef-273">basicException [0] outerExceptionThrownAtMethod</span><span class="sxs-lookup"><span data-stu-id="8d8ef-273">basicException [0] outerExceptionThrownAtMethod</span></span> |<span data-ttu-id="8d8ef-274">Dize</span><span class="sxs-lookup"><span data-stu-id="8d8ef-274">string</span></span> | |
| <span data-ttu-id="8d8ef-275">basicException [0] outerExceptionType</span><span class="sxs-lookup"><span data-stu-id="8d8ef-275">basicException [0] outerExceptionType</span></span> |<span data-ttu-id="8d8ef-276">Dize</span><span class="sxs-lookup"><span data-stu-id="8d8ef-276">string</span></span> | |
| <span data-ttu-id="8d8ef-277">basicException [0] outerId</span><span class="sxs-lookup"><span data-stu-id="8d8ef-277">basicException [0] outerId</span></span> |<span data-ttu-id="8d8ef-278">Dize</span><span class="sxs-lookup"><span data-stu-id="8d8ef-278">string</span></span> | |
| <span data-ttu-id="8d8ef-279">basicException [0] parsedStack [0] derlemesi</span><span class="sxs-lookup"><span data-stu-id="8d8ef-279">basicException [0] parsedStack [0] assembly</span></span> |<span data-ttu-id="8d8ef-280">Dize</span><span class="sxs-lookup"><span data-stu-id="8d8ef-280">string</span></span> | |
| <span data-ttu-id="8d8ef-281">basicException [0] [0] parsedStack fileName</span><span class="sxs-lookup"><span data-stu-id="8d8ef-281">basicException [0] parsedStack [0] fileName</span></span> |<span data-ttu-id="8d8ef-282">Dize</span><span class="sxs-lookup"><span data-stu-id="8d8ef-282">string</span></span> | |
| <span data-ttu-id="8d8ef-283">basicException [0] [0] parsedStack düzeyi</span><span class="sxs-lookup"><span data-stu-id="8d8ef-283">basicException [0] parsedStack [0] level</span></span> |<span data-ttu-id="8d8ef-284">tamsayı</span><span class="sxs-lookup"><span data-stu-id="8d8ef-284">integer</span></span> | |
| <span data-ttu-id="8d8ef-285">basicException [0] [0] parsedStack satır</span><span class="sxs-lookup"><span data-stu-id="8d8ef-285">basicException [0] parsedStack [0] line</span></span> |<span data-ttu-id="8d8ef-286">tamsayı</span><span class="sxs-lookup"><span data-stu-id="8d8ef-286">integer</span></span> | |
| <span data-ttu-id="8d8ef-287">basicException [0] [0] parsedStack yöntemi</span><span class="sxs-lookup"><span data-stu-id="8d8ef-287">basicException [0] parsedStack [0] method</span></span> |<span data-ttu-id="8d8ef-288">Dize</span><span class="sxs-lookup"><span data-stu-id="8d8ef-288">string</span></span> | |
| <span data-ttu-id="8d8ef-289">basicException [0] yığını</span><span class="sxs-lookup"><span data-stu-id="8d8ef-289">basicException [0] stack</span></span> |<span data-ttu-id="8d8ef-290">Dize</span><span class="sxs-lookup"><span data-stu-id="8d8ef-290">string</span></span> |<span data-ttu-id="8d8ef-291">En fazla uzunluk 10k</span><span class="sxs-lookup"><span data-stu-id="8d8ef-291">Max length 10k</span></span> |
| <span data-ttu-id="8d8ef-292">basicException [0] typeName</span><span class="sxs-lookup"><span data-stu-id="8d8ef-292">basicException [0] typeName</span></span> |<span data-ttu-id="8d8ef-293">Dize</span><span class="sxs-lookup"><span data-stu-id="8d8ef-293">string</span></span> | |

## <a name="trace-messages"></a><span data-ttu-id="8d8ef-294">İzleme iletileri</span><span class="sxs-lookup"><span data-stu-id="8d8ef-294">Trace Messages</span></span>
<span data-ttu-id="8d8ef-295">Tarafından gönderilen [TrackTrace](app-insights-api-custom-events-metrics.md#tracktrace)ve bunun [günlüğü bağdaştırıcıları](app-insights-asp-net-trace-logs.md).</span><span class="sxs-lookup"><span data-stu-id="8d8ef-295">Sent by [TrackTrace](app-insights-api-custom-events-metrics.md#tracktrace), and by the [logging adapters](app-insights-asp-net-trace-logs.md).</span></span>

| <span data-ttu-id="8d8ef-296">Yol</span><span class="sxs-lookup"><span data-stu-id="8d8ef-296">Path</span></span> | <span data-ttu-id="8d8ef-297">Tür</span><span class="sxs-lookup"><span data-stu-id="8d8ef-297">Type</span></span> | <span data-ttu-id="8d8ef-298">Notlar</span><span class="sxs-lookup"><span data-stu-id="8d8ef-298">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8d8ef-299">ileti [0] GünlükçüAdı</span><span class="sxs-lookup"><span data-stu-id="8d8ef-299">message [0] loggerName</span></span> |<span data-ttu-id="8d8ef-300">Dize</span><span class="sxs-lookup"><span data-stu-id="8d8ef-300">string</span></span> | |
| <span data-ttu-id="8d8ef-301">ileti [0] parametreleri</span><span class="sxs-lookup"><span data-stu-id="8d8ef-301">message [0] parameters</span></span> |<span data-ttu-id="8d8ef-302">Dize</span><span class="sxs-lookup"><span data-stu-id="8d8ef-302">string</span></span> | |
| <span data-ttu-id="8d8ef-303">ileti [0] ham</span><span class="sxs-lookup"><span data-stu-id="8d8ef-303">message [0] raw</span></span> |<span data-ttu-id="8d8ef-304">Dize</span><span class="sxs-lookup"><span data-stu-id="8d8ef-304">string</span></span> |<span data-ttu-id="8d8ef-305">Günlük iletisi, uzunluk üst sınırı 10k.</span><span class="sxs-lookup"><span data-stu-id="8d8ef-305">The log message, max length 10k.</span></span> |
| <span data-ttu-id="8d8ef-306">[0] iletisi önem düzeyi</span><span class="sxs-lookup"><span data-stu-id="8d8ef-306">message [0] severityLevel</span></span> |<span data-ttu-id="8d8ef-307">Dize</span><span class="sxs-lookup"><span data-stu-id="8d8ef-307">string</span></span> | |

## <a name="remote-dependency"></a><span data-ttu-id="8d8ef-308">Uzak bağımlılık</span><span class="sxs-lookup"><span data-stu-id="8d8ef-308">Remote dependency</span></span>
<span data-ttu-id="8d8ef-309">TrackDependency tarafından gönderilir.</span><span class="sxs-lookup"><span data-stu-id="8d8ef-309">Sent by TrackDependency.</span></span> <span data-ttu-id="8d8ef-310">Rapor performansı ve kullanımı için kullanılan [bağımlılıkları çağrıları](app-insights-asp-net-dependencies.md) server ve AJAX çağrıları tarayıcıda.</span><span class="sxs-lookup"><span data-stu-id="8d8ef-310">Used to report performance and usage of [calls to dependencies](app-insights-asp-net-dependencies.md) in the server, and AJAX calls in the browser.</span></span>

| <span data-ttu-id="8d8ef-311">Yol</span><span class="sxs-lookup"><span data-stu-id="8d8ef-311">Path</span></span> | <span data-ttu-id="8d8ef-312">Tür</span><span class="sxs-lookup"><span data-stu-id="8d8ef-312">Type</span></span> | <span data-ttu-id="8d8ef-313">Notlar</span><span class="sxs-lookup"><span data-stu-id="8d8ef-313">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8d8ef-314">remoteDependency [0] zaman uyumsuz</span><span class="sxs-lookup"><span data-stu-id="8d8ef-314">remoteDependency [0] async</span></span> |<span data-ttu-id="8d8ef-315">Boole değeri</span><span class="sxs-lookup"><span data-stu-id="8d8ef-315">boolean</span></span> | |
| <span data-ttu-id="8d8ef-316">remoteDependency [0] baseName</span><span class="sxs-lookup"><span data-stu-id="8d8ef-316">remoteDependency [0] baseName</span></span> |<span data-ttu-id="8d8ef-317">Dize</span><span class="sxs-lookup"><span data-stu-id="8d8ef-317">string</span></span> | |
| <span data-ttu-id="8d8ef-318">remoteDependency [0] commandName</span><span class="sxs-lookup"><span data-stu-id="8d8ef-318">remoteDependency [0] commandName</span></span> |<span data-ttu-id="8d8ef-319">Dize</span><span class="sxs-lookup"><span data-stu-id="8d8ef-319">string</span></span> |<span data-ttu-id="8d8ef-320">Örneğin "home/Index"</span><span class="sxs-lookup"><span data-stu-id="8d8ef-320">For example "home/index"</span></span> |
| <span data-ttu-id="8d8ef-321">remoteDependency [0] sayısı</span><span class="sxs-lookup"><span data-stu-id="8d8ef-321">remoteDependency [0] count</span></span> |<span data-ttu-id="8d8ef-322">tamsayı</span><span class="sxs-lookup"><span data-stu-id="8d8ef-322">integer</span></span> |<span data-ttu-id="8d8ef-323">100 / ([örnekleme](app-insights-sampling.md) hızı).</span><span class="sxs-lookup"><span data-stu-id="8d8ef-323">100/([sampling](app-insights-sampling.md) rate).</span></span> <span data-ttu-id="8d8ef-324">Örneğin 4 =&gt; % 25.</span><span class="sxs-lookup"><span data-stu-id="8d8ef-324">For example 4 =&gt; 25%.</span></span> |
| <span data-ttu-id="8d8ef-325">remoteDependency [0] dependencyTypeName</span><span class="sxs-lookup"><span data-stu-id="8d8ef-325">remoteDependency [0] dependencyTypeName</span></span> |<span data-ttu-id="8d8ef-326">Dize</span><span class="sxs-lookup"><span data-stu-id="8d8ef-326">string</span></span> |<span data-ttu-id="8d8ef-327">HTTP SQL...</span><span class="sxs-lookup"><span data-stu-id="8d8ef-327">HTTP, SQL, ...</span></span> |
| <span data-ttu-id="8d8ef-328">remoteDependency [0] durationMetric.value</span><span class="sxs-lookup"><span data-stu-id="8d8ef-328">remoteDependency [0] durationMetric.value</span></span> |<span data-ttu-id="8d8ef-329">Sayı</span><span class="sxs-lookup"><span data-stu-id="8d8ef-329">number</span></span> |<span data-ttu-id="8d8ef-330">Bağımlılık yanıtıyla tamamlanmasından çağrı süresi</span><span class="sxs-lookup"><span data-stu-id="8d8ef-330">Time from call to completion of response by dependency</span></span> |
| <span data-ttu-id="8d8ef-331">remoteDependency [0] kimliği</span><span class="sxs-lookup"><span data-stu-id="8d8ef-331">remoteDependency [0] id</span></span> |<span data-ttu-id="8d8ef-332">Dize</span><span class="sxs-lookup"><span data-stu-id="8d8ef-332">string</span></span> | |
| <span data-ttu-id="8d8ef-333">remoteDependency [0] adı</span><span class="sxs-lookup"><span data-stu-id="8d8ef-333">remoteDependency [0] name</span></span> |<span data-ttu-id="8d8ef-334">Dize</span><span class="sxs-lookup"><span data-stu-id="8d8ef-334">string</span></span> |<span data-ttu-id="8d8ef-335">URL.</span><span class="sxs-lookup"><span data-stu-id="8d8ef-335">Url.</span></span> <span data-ttu-id="8d8ef-336">En fazla uzunluk 250.</span><span class="sxs-lookup"><span data-stu-id="8d8ef-336">Max length 250.</span></span> |
| <span data-ttu-id="8d8ef-337">remoteDependency [0] resultCode</span><span class="sxs-lookup"><span data-stu-id="8d8ef-337">remoteDependency [0] resultCode</span></span> |<span data-ttu-id="8d8ef-338">Dize</span><span class="sxs-lookup"><span data-stu-id="8d8ef-338">string</span></span> |<span data-ttu-id="8d8ef-339">HTTP bağımlılık</span><span class="sxs-lookup"><span data-stu-id="8d8ef-339">from HTTP dependency</span></span> |
| <span data-ttu-id="8d8ef-340">remoteDependency [0] başarılı</span><span class="sxs-lookup"><span data-stu-id="8d8ef-340">remoteDependency [0] success</span></span> |<span data-ttu-id="8d8ef-341">Boole değeri</span><span class="sxs-lookup"><span data-stu-id="8d8ef-341">boolean</span></span> | |
| <span data-ttu-id="8d8ef-342">remoteDependency [0] türü</span><span class="sxs-lookup"><span data-stu-id="8d8ef-342">remoteDependency [0] type</span></span> |<span data-ttu-id="8d8ef-343">Dize</span><span class="sxs-lookup"><span data-stu-id="8d8ef-343">string</span></span> |<span data-ttu-id="8d8ef-344">HTTP Sql...</span><span class="sxs-lookup"><span data-stu-id="8d8ef-344">Http, Sql,...</span></span> |
| <span data-ttu-id="8d8ef-345">remoteDependency [0] URL'si</span><span class="sxs-lookup"><span data-stu-id="8d8ef-345">remoteDependency [0] url</span></span> |<span data-ttu-id="8d8ef-346">Dize</span><span class="sxs-lookup"><span data-stu-id="8d8ef-346">string</span></span> |<span data-ttu-id="8d8ef-347">En fazla uzunluk 2000</span><span class="sxs-lookup"><span data-stu-id="8d8ef-347">Max length 2000</span></span> |
| <span data-ttu-id="8d8ef-348">remoteDependency [0] urlData.base</span><span class="sxs-lookup"><span data-stu-id="8d8ef-348">remoteDependency [0] urlData.base</span></span> |<span data-ttu-id="8d8ef-349">Dize</span><span class="sxs-lookup"><span data-stu-id="8d8ef-349">string</span></span> |<span data-ttu-id="8d8ef-350">En fazla uzunluk 2000</span><span class="sxs-lookup"><span data-stu-id="8d8ef-350">Max length 2000</span></span> |
| <span data-ttu-id="8d8ef-351">remoteDependency [0] urlData.hashTag</span><span class="sxs-lookup"><span data-stu-id="8d8ef-351">remoteDependency [0] urlData.hashTag</span></span> |<span data-ttu-id="8d8ef-352">Dize</span><span class="sxs-lookup"><span data-stu-id="8d8ef-352">string</span></span> | |
| <span data-ttu-id="8d8ef-353">remoteDependency [0] urlData.host</span><span class="sxs-lookup"><span data-stu-id="8d8ef-353">remoteDependency [0] urlData.host</span></span> |<span data-ttu-id="8d8ef-354">Dize</span><span class="sxs-lookup"><span data-stu-id="8d8ef-354">string</span></span> |<span data-ttu-id="8d8ef-355">En fazla uzunluk 200</span><span class="sxs-lookup"><span data-stu-id="8d8ef-355">Max length 200</span></span> |

## <a name="requests"></a><span data-ttu-id="8d8ef-356">İstekler</span><span class="sxs-lookup"><span data-stu-id="8d8ef-356">Requests</span></span>
<span data-ttu-id="8d8ef-357">Tarafından gönderilen [TrackRequest](app-insights-api-custom-events-metrics.md#trackrequest).</span><span class="sxs-lookup"><span data-stu-id="8d8ef-357">Sent by [TrackRequest](app-insights-api-custom-events-metrics.md#trackrequest).</span></span> <span data-ttu-id="8d8ef-358">Standart modüller, sunucuda ölçülen bu raporları sunucu yanıt süresi için kullanın.</span><span class="sxs-lookup"><span data-stu-id="8d8ef-358">The standard modules use this to reports server response time, measured at the server.</span></span>

| <span data-ttu-id="8d8ef-359">Yol</span><span class="sxs-lookup"><span data-stu-id="8d8ef-359">Path</span></span> | <span data-ttu-id="8d8ef-360">Tür</span><span class="sxs-lookup"><span data-stu-id="8d8ef-360">Type</span></span> | <span data-ttu-id="8d8ef-361">Notlar</span><span class="sxs-lookup"><span data-stu-id="8d8ef-361">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8d8ef-362">[0] isteği sayısı</span><span class="sxs-lookup"><span data-stu-id="8d8ef-362">request [0] count</span></span> |<span data-ttu-id="8d8ef-363">tamsayı</span><span class="sxs-lookup"><span data-stu-id="8d8ef-363">integer</span></span> |<span data-ttu-id="8d8ef-364">100 / ([örnekleme](app-insights-sampling.md) hızı).</span><span class="sxs-lookup"><span data-stu-id="8d8ef-364">100/([sampling](app-insights-sampling.md) rate).</span></span> <span data-ttu-id="8d8ef-365">Örneğin: 4 =&gt; % 25.</span><span class="sxs-lookup"><span data-stu-id="8d8ef-365">For example: 4 =&gt; 25%.</span></span> |
| <span data-ttu-id="8d8ef-366">İstek [0] durationMetric.value</span><span class="sxs-lookup"><span data-stu-id="8d8ef-366">request [0] durationMetric.value</span></span> |<span data-ttu-id="8d8ef-367">Sayı</span><span class="sxs-lookup"><span data-stu-id="8d8ef-367">number</span></span> |<span data-ttu-id="8d8ef-368">Karşılık gelen istek süresi.</span><span class="sxs-lookup"><span data-stu-id="8d8ef-368">Time from request arriving to response.</span></span> <span data-ttu-id="8d8ef-369">1e7 1'ler ==</span><span class="sxs-lookup"><span data-stu-id="8d8ef-369">1e7 == 1s</span></span> |
| <span data-ttu-id="8d8ef-370">[0] istek kimliği</span><span class="sxs-lookup"><span data-stu-id="8d8ef-370">request [0] id</span></span> |<span data-ttu-id="8d8ef-371">Dize</span><span class="sxs-lookup"><span data-stu-id="8d8ef-371">string</span></span> |<span data-ttu-id="8d8ef-372">İşlem kimliği</span><span class="sxs-lookup"><span data-stu-id="8d8ef-372">Operation id</span></span> |
| <span data-ttu-id="8d8ef-373">İstek [0] adı</span><span class="sxs-lookup"><span data-stu-id="8d8ef-373">request [0] name</span></span> |<span data-ttu-id="8d8ef-374">Dize</span><span class="sxs-lookup"><span data-stu-id="8d8ef-374">string</span></span> |<span data-ttu-id="8d8ef-375">GET/POST + temel url.</span><span class="sxs-lookup"><span data-stu-id="8d8ef-375">GET/POST + url base.</span></span>  <span data-ttu-id="8d8ef-376">En fazla uzunluk 250</span><span class="sxs-lookup"><span data-stu-id="8d8ef-376">Max length 250</span></span> |
| <span data-ttu-id="8d8ef-377">İstek [0] yanıt kodu</span><span class="sxs-lookup"><span data-stu-id="8d8ef-377">request [0] responseCode</span></span> |<span data-ttu-id="8d8ef-378">tamsayı</span><span class="sxs-lookup"><span data-stu-id="8d8ef-378">integer</span></span> |<span data-ttu-id="8d8ef-379">İstemciye gönderilen HTTP yanıtı</span><span class="sxs-lookup"><span data-stu-id="8d8ef-379">HTTP response sent to client</span></span> |
| <span data-ttu-id="8d8ef-380">İstek [0] başarılı</span><span class="sxs-lookup"><span data-stu-id="8d8ef-380">request [0] success</span></span> |<span data-ttu-id="8d8ef-381">Boole değeri</span><span class="sxs-lookup"><span data-stu-id="8d8ef-381">boolean</span></span> |<span data-ttu-id="8d8ef-382">Varsayılan == (yanıt kodu &lt; 400)</span><span class="sxs-lookup"><span data-stu-id="8d8ef-382">Default == (responseCode &lt; 400)</span></span> |
| <span data-ttu-id="8d8ef-383">İstek [0] URL'si</span><span class="sxs-lookup"><span data-stu-id="8d8ef-383">request [0] url</span></span> |<span data-ttu-id="8d8ef-384">Dize</span><span class="sxs-lookup"><span data-stu-id="8d8ef-384">string</span></span> |<span data-ttu-id="8d8ef-385">Konak dahil değil</span><span class="sxs-lookup"><span data-stu-id="8d8ef-385">Not including host</span></span> |
| <span data-ttu-id="8d8ef-386">İstek [0] urlData.base</span><span class="sxs-lookup"><span data-stu-id="8d8ef-386">request [0] urlData.base</span></span> |<span data-ttu-id="8d8ef-387">Dize</span><span class="sxs-lookup"><span data-stu-id="8d8ef-387">string</span></span> | |
| <span data-ttu-id="8d8ef-388">İstek [0] urlData.hashTag</span><span class="sxs-lookup"><span data-stu-id="8d8ef-388">request [0] urlData.hashTag</span></span> |<span data-ttu-id="8d8ef-389">Dize</span><span class="sxs-lookup"><span data-stu-id="8d8ef-389">string</span></span> | |
| <span data-ttu-id="8d8ef-390">İstek [0] urlData.host</span><span class="sxs-lookup"><span data-stu-id="8d8ef-390">request [0] urlData.host</span></span> |<span data-ttu-id="8d8ef-391">Dize</span><span class="sxs-lookup"><span data-stu-id="8d8ef-391">string</span></span> | |

## <a name="page-view-performance"></a><span data-ttu-id="8d8ef-392">Sayfa görünümü performansı</span><span class="sxs-lookup"><span data-stu-id="8d8ef-392">Page View Performance</span></span>
<span data-ttu-id="8d8ef-393">Tarayıcı tarafından gönderilen.</span><span class="sxs-lookup"><span data-stu-id="8d8ef-393">Sent by the browser.</span></span> <span data-ttu-id="8d8ef-394">(Zaman uyumsuz AJAX çağrıları) tam görüntülenecek isteğini başlatarak kullanıcıdan bir sayfanın işlenmesi için gereken süre ölçer.</span><span class="sxs-lookup"><span data-stu-id="8d8ef-394">Measures the time to process a page, from user initiating the request to display complete (excluding async AJAX calls).</span></span>

<span data-ttu-id="8d8ef-395">Bağlam değerleri, istemci işletim sistemi ve tarayıcı sürümü gösterir.</span><span class="sxs-lookup"><span data-stu-id="8d8ef-395">Context values show client OS and browser version.</span></span>

| <span data-ttu-id="8d8ef-396">Yol</span><span class="sxs-lookup"><span data-stu-id="8d8ef-396">Path</span></span> | <span data-ttu-id="8d8ef-397">Tür</span><span class="sxs-lookup"><span data-stu-id="8d8ef-397">Type</span></span> | <span data-ttu-id="8d8ef-398">Notlar</span><span class="sxs-lookup"><span data-stu-id="8d8ef-398">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8d8ef-399">clientPerformance [0] clientProcess.value</span><span class="sxs-lookup"><span data-stu-id="8d8ef-399">clientPerformance [0] clientProcess.value</span></span> |<span data-ttu-id="8d8ef-400">tamsayı</span><span class="sxs-lookup"><span data-stu-id="8d8ef-400">integer</span></span> |<span data-ttu-id="8d8ef-401">Sayfanın görüntüleme için HTML Alma bitiş saati.</span><span class="sxs-lookup"><span data-stu-id="8d8ef-401">Time from end of receiving the HTML to displaying the page.</span></span> |
| <span data-ttu-id="8d8ef-402">clientPerformance [0] adı</span><span class="sxs-lookup"><span data-stu-id="8d8ef-402">clientPerformance [0] name</span></span> |<span data-ttu-id="8d8ef-403">Dize</span><span class="sxs-lookup"><span data-stu-id="8d8ef-403">string</span></span> | |
| <span data-ttu-id="8d8ef-404">clientPerformance [0] networkConnection.value</span><span class="sxs-lookup"><span data-stu-id="8d8ef-404">clientPerformance [0] networkConnection.value</span></span> |<span data-ttu-id="8d8ef-405">tamsayı</span><span class="sxs-lookup"><span data-stu-id="8d8ef-405">integer</span></span> |<span data-ttu-id="8d8ef-406">Bir ağ bağlantısı kurmak için geçen süre.</span><span class="sxs-lookup"><span data-stu-id="8d8ef-406">Time taken to establish a network connection.</span></span> |
| <span data-ttu-id="8d8ef-407">clientPerformance [0] receiveRequest.value</span><span class="sxs-lookup"><span data-stu-id="8d8ef-407">clientPerformance [0] receiveRequest.value</span></span> |<span data-ttu-id="8d8ef-408">tamsayı</span><span class="sxs-lookup"><span data-stu-id="8d8ef-408">integer</span></span> |<span data-ttu-id="8d8ef-409">HTML yanıta almak için isteği gönderme bitiş saati.</span><span class="sxs-lookup"><span data-stu-id="8d8ef-409">Time from end of sending the request to receiving the HTML in reply.</span></span> |
| <span data-ttu-id="8d8ef-410">clientPerformance [0] sendRequest.value</span><span class="sxs-lookup"><span data-stu-id="8d8ef-410">clientPerformance [0] sendRequest.value</span></span> |<span data-ttu-id="8d8ef-411">tamsayı</span><span class="sxs-lookup"><span data-stu-id="8d8ef-411">integer</span></span> |<span data-ttu-id="8d8ef-412">Saati HTTP isteği göndermek için gerçekleştirilecek.</span><span class="sxs-lookup"><span data-stu-id="8d8ef-412">Time from taken to send the HTTP request.</span></span> |
| <span data-ttu-id="8d8ef-413">clientPerformance [0] total.value</span><span class="sxs-lookup"><span data-stu-id="8d8ef-413">clientPerformance [0] total.value</span></span> |<span data-ttu-id="8d8ef-414">tamsayı</span><span class="sxs-lookup"><span data-stu-id="8d8ef-414">integer</span></span> |<span data-ttu-id="8d8ef-415">Sayfayı görüntülemeye isteği göndermek başlangıç süresi.</span><span class="sxs-lookup"><span data-stu-id="8d8ef-415">Time from starting to send the request to displaying the page.</span></span> |
| <span data-ttu-id="8d8ef-416">clientPerformance [0] URL'si</span><span class="sxs-lookup"><span data-stu-id="8d8ef-416">clientPerformance [0] url</span></span> |<span data-ttu-id="8d8ef-417">Dize</span><span class="sxs-lookup"><span data-stu-id="8d8ef-417">string</span></span> |<span data-ttu-id="8d8ef-418">Bu istek URL'si</span><span class="sxs-lookup"><span data-stu-id="8d8ef-418">URL of this request</span></span> |
| <span data-ttu-id="8d8ef-419">clientPerformance [0] urlData.base</span><span class="sxs-lookup"><span data-stu-id="8d8ef-419">clientPerformance [0] urlData.base</span></span> |<span data-ttu-id="8d8ef-420">Dize</span><span class="sxs-lookup"><span data-stu-id="8d8ef-420">string</span></span> | |
| <span data-ttu-id="8d8ef-421">clientPerformance [0] urlData.hashTag</span><span class="sxs-lookup"><span data-stu-id="8d8ef-421">clientPerformance [0] urlData.hashTag</span></span> |<span data-ttu-id="8d8ef-422">Dize</span><span class="sxs-lookup"><span data-stu-id="8d8ef-422">string</span></span> | |
| <span data-ttu-id="8d8ef-423">clientPerformance [0] urlData.host</span><span class="sxs-lookup"><span data-stu-id="8d8ef-423">clientPerformance [0] urlData.host</span></span> |<span data-ttu-id="8d8ef-424">Dize</span><span class="sxs-lookup"><span data-stu-id="8d8ef-424">string</span></span> | |
| <span data-ttu-id="8d8ef-425">clientPerformance [0] urlData.protocol</span><span class="sxs-lookup"><span data-stu-id="8d8ef-425">clientPerformance [0] urlData.protocol</span></span> |<span data-ttu-id="8d8ef-426">Dize</span><span class="sxs-lookup"><span data-stu-id="8d8ef-426">string</span></span> | |

## <a name="page-views"></a><span data-ttu-id="8d8ef-427">Sayfa görünümleri</span><span class="sxs-lookup"><span data-stu-id="8d8ef-427">Page Views</span></span>
<span data-ttu-id="8d8ef-428">TrackPageView() tarafından gönderilen veya [stopTrackPage](app-insights-api-custom-events-metrics.md#page-views)</span><span class="sxs-lookup"><span data-stu-id="8d8ef-428">Sent by trackPageView() or [stopTrackPage](app-insights-api-custom-events-metrics.md#page-views)</span></span>

| <span data-ttu-id="8d8ef-429">Yol</span><span class="sxs-lookup"><span data-stu-id="8d8ef-429">Path</span></span> | <span data-ttu-id="8d8ef-430">Tür</span><span class="sxs-lookup"><span data-stu-id="8d8ef-430">Type</span></span> | <span data-ttu-id="8d8ef-431">Notlar</span><span class="sxs-lookup"><span data-stu-id="8d8ef-431">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8d8ef-432">Görünüm [0] sayısı</span><span class="sxs-lookup"><span data-stu-id="8d8ef-432">view [0] count</span></span> |<span data-ttu-id="8d8ef-433">tamsayı</span><span class="sxs-lookup"><span data-stu-id="8d8ef-433">integer</span></span> |<span data-ttu-id="8d8ef-434">100 / ([örnekleme](app-insights-sampling.md) hızı).</span><span class="sxs-lookup"><span data-stu-id="8d8ef-434">100/([sampling](app-insights-sampling.md) rate).</span></span> <span data-ttu-id="8d8ef-435">Örneğin 4 =&gt; % 25.</span><span class="sxs-lookup"><span data-stu-id="8d8ef-435">For example 4 =&gt; 25%.</span></span> |
| <span data-ttu-id="8d8ef-436">Görünüm [0] durationMetric.value</span><span class="sxs-lookup"><span data-stu-id="8d8ef-436">view [0] durationMetric.value</span></span> |<span data-ttu-id="8d8ef-437">tamsayı</span><span class="sxs-lookup"><span data-stu-id="8d8ef-437">integer</span></span> |<span data-ttu-id="8d8ef-438">Değeri trackPageView() veya startTrackPage() - isteğe bağlı olarak ayarlanmış stopTrackPage().</span><span class="sxs-lookup"><span data-stu-id="8d8ef-438">Value optionally set in trackPageView() or by startTrackPage() - stopTrackPage().</span></span> <span data-ttu-id="8d8ef-439">Aynı clientPerformance değerleri.</span><span class="sxs-lookup"><span data-stu-id="8d8ef-439">Not the same as clientPerformance values.</span></span> |
| <span data-ttu-id="8d8ef-440">Görünüm [0] adı</span><span class="sxs-lookup"><span data-stu-id="8d8ef-440">view [0] name</span></span> |<span data-ttu-id="8d8ef-441">Dize</span><span class="sxs-lookup"><span data-stu-id="8d8ef-441">string</span></span> |<span data-ttu-id="8d8ef-442">Sayfa başlığı.</span><span class="sxs-lookup"><span data-stu-id="8d8ef-442">Page title.</span></span>  <span data-ttu-id="8d8ef-443">En fazla uzunluk 250</span><span class="sxs-lookup"><span data-stu-id="8d8ef-443">Max length 250</span></span> |
| <span data-ttu-id="8d8ef-444">Görünüm [0] URL'si</span><span class="sxs-lookup"><span data-stu-id="8d8ef-444">view [0] url</span></span> |<span data-ttu-id="8d8ef-445">Dize</span><span class="sxs-lookup"><span data-stu-id="8d8ef-445">string</span></span> | |
| <span data-ttu-id="8d8ef-446">Görünüm [0] urlData.base</span><span class="sxs-lookup"><span data-stu-id="8d8ef-446">view [0] urlData.base</span></span> |<span data-ttu-id="8d8ef-447">Dize</span><span class="sxs-lookup"><span data-stu-id="8d8ef-447">string</span></span> | |
| <span data-ttu-id="8d8ef-448">Görünüm [0] urlData.hashTag</span><span class="sxs-lookup"><span data-stu-id="8d8ef-448">view [0] urlData.hashTag</span></span> |<span data-ttu-id="8d8ef-449">Dize</span><span class="sxs-lookup"><span data-stu-id="8d8ef-449">string</span></span> | |
| <span data-ttu-id="8d8ef-450">Görünüm [0] urlData.host</span><span class="sxs-lookup"><span data-stu-id="8d8ef-450">view [0] urlData.host</span></span> |<span data-ttu-id="8d8ef-451">Dize</span><span class="sxs-lookup"><span data-stu-id="8d8ef-451">string</span></span> | |

## <a name="availability"></a><span data-ttu-id="8d8ef-452">Kullanılabilirlik</span><span class="sxs-lookup"><span data-stu-id="8d8ef-452">Availability</span></span>
<span data-ttu-id="8d8ef-453">Raporları [kullanılabilirlik web testleri](app-insights-monitor-web-app-availability.md).</span><span class="sxs-lookup"><span data-stu-id="8d8ef-453">Reports [availability web tests](app-insights-monitor-web-app-availability.md).</span></span>

| <span data-ttu-id="8d8ef-454">Yol</span><span class="sxs-lookup"><span data-stu-id="8d8ef-454">Path</span></span> | <span data-ttu-id="8d8ef-455">Tür</span><span class="sxs-lookup"><span data-stu-id="8d8ef-455">Type</span></span> | <span data-ttu-id="8d8ef-456">Notlar</span><span class="sxs-lookup"><span data-stu-id="8d8ef-456">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8d8ef-457">Kullanılabilirlik [0] availabilityMetric.name</span><span class="sxs-lookup"><span data-stu-id="8d8ef-457">availability [0] availabilityMetric.name</span></span> |<span data-ttu-id="8d8ef-458">Dize</span><span class="sxs-lookup"><span data-stu-id="8d8ef-458">string</span></span> |<span data-ttu-id="8d8ef-459">availability</span><span class="sxs-lookup"><span data-stu-id="8d8ef-459">availability</span></span> |
| <span data-ttu-id="8d8ef-460">Kullanılabilirlik [0] availabilityMetric.value</span><span class="sxs-lookup"><span data-stu-id="8d8ef-460">availability [0] availabilityMetric.value</span></span> |<span data-ttu-id="8d8ef-461">Sayı</span><span class="sxs-lookup"><span data-stu-id="8d8ef-461">number</span></span> |<span data-ttu-id="8d8ef-462">1.0 veya 0,0</span><span class="sxs-lookup"><span data-stu-id="8d8ef-462">1.0 or 0.0</span></span> |
| <span data-ttu-id="8d8ef-463">Kullanılabilirlik [0] sayısı</span><span class="sxs-lookup"><span data-stu-id="8d8ef-463">availability [0] count</span></span> |<span data-ttu-id="8d8ef-464">tamsayı</span><span class="sxs-lookup"><span data-stu-id="8d8ef-464">integer</span></span> |<span data-ttu-id="8d8ef-465">100 / ([örnekleme](app-insights-sampling.md) hızı).</span><span class="sxs-lookup"><span data-stu-id="8d8ef-465">100/([sampling](app-insights-sampling.md) rate).</span></span> <span data-ttu-id="8d8ef-466">Örneğin 4 =&gt; % 25.</span><span class="sxs-lookup"><span data-stu-id="8d8ef-466">For example 4 =&gt; 25%.</span></span> |
| <span data-ttu-id="8d8ef-467">Kullanılabilirlik [0] dataSizeMetric.name</span><span class="sxs-lookup"><span data-stu-id="8d8ef-467">availability [0] dataSizeMetric.name</span></span> |<span data-ttu-id="8d8ef-468">Dize</span><span class="sxs-lookup"><span data-stu-id="8d8ef-468">string</span></span> | |
| <span data-ttu-id="8d8ef-469">Kullanılabilirlik [0] dataSizeMetric.value</span><span class="sxs-lookup"><span data-stu-id="8d8ef-469">availability [0] dataSizeMetric.value</span></span> |<span data-ttu-id="8d8ef-470">tamsayı</span><span class="sxs-lookup"><span data-stu-id="8d8ef-470">integer</span></span> | |
| <span data-ttu-id="8d8ef-471">Kullanılabilirlik [0] durationMetric.name</span><span class="sxs-lookup"><span data-stu-id="8d8ef-471">availability [0] durationMetric.name</span></span> |<span data-ttu-id="8d8ef-472">Dize</span><span class="sxs-lookup"><span data-stu-id="8d8ef-472">string</span></span> | |
| <span data-ttu-id="8d8ef-473">Kullanılabilirlik [0] durationMetric.value</span><span class="sxs-lookup"><span data-stu-id="8d8ef-473">availability [0] durationMetric.value</span></span> |<span data-ttu-id="8d8ef-474">Sayı</span><span class="sxs-lookup"><span data-stu-id="8d8ef-474">number</span></span> |<span data-ttu-id="8d8ef-475">Test süresi.</span><span class="sxs-lookup"><span data-stu-id="8d8ef-475">Duration of test.</span></span> <span data-ttu-id="8d8ef-476">1e7 1'ler ==</span><span class="sxs-lookup"><span data-stu-id="8d8ef-476">1e7==1s</span></span> |
| <span data-ttu-id="8d8ef-477">Kullanılabilirlik [0] iletisi</span><span class="sxs-lookup"><span data-stu-id="8d8ef-477">availability [0] message</span></span> |<span data-ttu-id="8d8ef-478">Dize</span><span class="sxs-lookup"><span data-stu-id="8d8ef-478">string</span></span> |<span data-ttu-id="8d8ef-479">Hata tanılama</span><span class="sxs-lookup"><span data-stu-id="8d8ef-479">Failure diagnostic</span></span> |
| <span data-ttu-id="8d8ef-480">Kullanılabilirlik [0] sonucu</span><span class="sxs-lookup"><span data-stu-id="8d8ef-480">availability [0] result</span></span> |<span data-ttu-id="8d8ef-481">Dize</span><span class="sxs-lookup"><span data-stu-id="8d8ef-481">string</span></span> |<span data-ttu-id="8d8ef-482">Geçişi/başarısız</span><span class="sxs-lookup"><span data-stu-id="8d8ef-482">Pass/Fail</span></span> |
| <span data-ttu-id="8d8ef-483">Kullanılabilirlik [0] runLocation</span><span class="sxs-lookup"><span data-stu-id="8d8ef-483">availability [0] runLocation</span></span> |<span data-ttu-id="8d8ef-484">Dize</span><span class="sxs-lookup"><span data-stu-id="8d8ef-484">string</span></span> |<span data-ttu-id="8d8ef-485">Http isteği coğrafi kaynağı</span><span class="sxs-lookup"><span data-stu-id="8d8ef-485">Geo source of http req</span></span> |
| <span data-ttu-id="8d8ef-486">Kullanılabilirlik [0] testName</span><span class="sxs-lookup"><span data-stu-id="8d8ef-486">availability [0] testName</span></span> |<span data-ttu-id="8d8ef-487">Dize</span><span class="sxs-lookup"><span data-stu-id="8d8ef-487">string</span></span> | |
| <span data-ttu-id="8d8ef-488">Kullanılabilirlik [0] testRunId</span><span class="sxs-lookup"><span data-stu-id="8d8ef-488">availability [0] testRunId</span></span> |<span data-ttu-id="8d8ef-489">Dize</span><span class="sxs-lookup"><span data-stu-id="8d8ef-489">string</span></span> | |
| <span data-ttu-id="8d8ef-490">Kullanılabilirlik [0] testTimestamp</span><span class="sxs-lookup"><span data-stu-id="8d8ef-490">availability [0] testTimestamp</span></span> |<span data-ttu-id="8d8ef-491">Dize</span><span class="sxs-lookup"><span data-stu-id="8d8ef-491">string</span></span> | |

## <a name="metrics"></a><span data-ttu-id="8d8ef-492">Ölçümler</span><span class="sxs-lookup"><span data-stu-id="8d8ef-492">Metrics</span></span>
<span data-ttu-id="8d8ef-493">TrackMetric() tarafından oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="8d8ef-493">Generated by TrackMetric().</span></span>

<span data-ttu-id="8d8ef-494">Ölçü değerini context.custom.metrics[0 içinde bulundu]</span><span class="sxs-lookup"><span data-stu-id="8d8ef-494">The metric value is found in context.custom.metrics[0]</span></span>

<span data-ttu-id="8d8ef-495">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="8d8ef-495">For example:</span></span>

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

## <a name="about-metric-values"></a><span data-ttu-id="8d8ef-496">Ölçüm değerleri hakkında</span><span class="sxs-lookup"><span data-stu-id="8d8ef-496">About metric values</span></span>
<span data-ttu-id="8d8ef-497">Ölçüm değerleri, hem ölçüm raporlar ve diğer yerlerde, standart nesne yapısıyla raporlanır.</span><span class="sxs-lookup"><span data-stu-id="8d8ef-497">Metric values, both in metric reports and elsewhere, are reported with a standard object structure.</span></span> <span data-ttu-id="8d8ef-498">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="8d8ef-498">For example:</span></span>

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

<span data-ttu-id="8d8ef-499">Şu anda - yine de bu değişebilir gelecekte - tüm değerlerin standart SDK modüllerden bildirilen `count==1` ve yalnızca `name` ve `value` alanları kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="8d8ef-499">Currently - though this might change in the future - in all values reported from the standard SDK modules, `count==1` and only the `name` and `value` fields are useful.</span></span> <span data-ttu-id="8d8ef-500">Kendi TrackMetric çağrıları yazma varsa, bunlar olacak farklı yalnızca durumda olur diğer parametreler kümesindeki.</span><span class="sxs-lookup"><span data-stu-id="8d8ef-500">The only case where they would be different would be if you write your own TrackMetric calls in which you set the other parameters.</span></span>

<span data-ttu-id="8d8ef-501">Diğer alanları amacı portalına trafiğini azaltmak için SDK toplanacak ölçümleri izin vermektir.</span><span class="sxs-lookup"><span data-stu-id="8d8ef-501">The purpose of the other fields is to allow metrics to be aggregated in the SDK, to reduce traffic to the portal.</span></span> <span data-ttu-id="8d8ef-502">Örneğin, her bir ölçüm raporu göndermeden önce birkaç art arda okumalar ortalama.</span><span class="sxs-lookup"><span data-stu-id="8d8ef-502">For example, you could average several successive readings before sending each metric report.</span></span> <span data-ttu-id="8d8ef-503">Ardından min, max, standart sapma ve toplam değeri (sum veya ortalama) hesaplamak ve rapor tarafından temsil edilen okumalar sayısına sayısını ayarlamak.</span><span class="sxs-lookup"><span data-stu-id="8d8ef-503">Then you would calculate the min, max, standard deviation and aggregate value (sum or average) and set count to the number of readings represented by the report.</span></span>

<span data-ttu-id="8d8ef-504">Yukarıdaki tablolarda, biz nadiren kullanılan alanları sayısı, min, max, stdDev ve sampledValue atlamış.</span><span class="sxs-lookup"><span data-stu-id="8d8ef-504">In the tables above, we have omitted the rarely-used fields count, min, max, stdDev and sampledValue.</span></span>

<span data-ttu-id="8d8ef-505">Önceden bir araya getirildiği ölçümleri yerine kullanabileceğiniz [örnekleme](app-insights-sampling.md) telemetri miktarının azaltılmasını gerekiyorsa.</span><span class="sxs-lookup"><span data-stu-id="8d8ef-505">Instead of pre-aggregating metrics, you can use [sampling](app-insights-sampling.md) if you need to reduce the volume of telemetry.</span></span>

### <a name="durations"></a><span data-ttu-id="8d8ef-506">Süreleri</span><span class="sxs-lookup"><span data-stu-id="8d8ef-506">Durations</span></span>
<span data-ttu-id="8d8ef-507">Aksi takdirde belirtilenler dışında süreleri 10000000.0 1 saniye anlamına bir milisaniyeye onda içinde gösterilir.</span><span class="sxs-lookup"><span data-stu-id="8d8ef-507">Except where otherwise noted, durations are represented in tenths of a microsecond, so that 10000000.0 means 1 second.</span></span>

## <a name="see-also"></a><span data-ttu-id="8d8ef-508">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="8d8ef-508">See also</span></span>
* [<span data-ttu-id="8d8ef-509">Application Insights</span><span class="sxs-lookup"><span data-stu-id="8d8ef-509">Application Insights</span></span>](app-insights-overview.md)
* [<span data-ttu-id="8d8ef-510">Sürekli dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="8d8ef-510">Continuous Export</span></span>](app-insights-export-telemetry.md)
* [<span data-ttu-id="8d8ef-511">Kod örnekleri</span><span class="sxs-lookup"><span data-stu-id="8d8ef-511">Code samples</span></span>](app-insights-export-telemetry.md#code-samples)
