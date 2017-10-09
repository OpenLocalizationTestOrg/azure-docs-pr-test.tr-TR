---
title: "Application Insights'te aaaUse Powershell tooset uyarıları | Microsoft Docs"
description: "Application Insights tooget e-postaların ölçüm değişiklikler hakkında yapılandırma otomatikleştirin."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 05d6a9e0-77a2-4a35-9052-a7768d23a196
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 10/31/2016
ms.author: bwren
ms.openlocfilehash: d68e5f9511bb4015f59175724bc1a4a04ecf43e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-tooset-alerts-in-application-insights"></a><span data-ttu-id="3908b-103">Application Insights'ta PowerShell tooset uyarıları kullanın</span><span class="sxs-lookup"><span data-stu-id="3908b-103">Use PowerShell tooset alerts in Application Insights</span></span>
<span data-ttu-id="3908b-104">Merhaba yapılandırmasını otomatik hale getirebilirsiniz [uyarıları](app-insights-alerts.md) içinde [Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3908b-104">You can automate hello configuration of [alerts](app-insights-alerts.md) in [Application Insights](app-insights-overview.md).</span></span>

<span data-ttu-id="3908b-105">Buna ek olarak, şunları yapabilirsiniz [kancalarını tooautomate yanıt tooan Uyarınız ayarlamak](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="3908b-105">In addition, you can [set webhooks tooautomate your response tooan alert](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span></span>

> [!NOTE]
> <span data-ttu-id="3908b-106">Toocreate kaynakları ve uyarılara istiyorsanız aynı hello saat, göz önünde bulundurun [bir Azure Resource Manager şablonu kullanarak](app-insights-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="3908b-106">If you want toocreate resources and alerts at hello same time, consider [using an Azure Resource Manager template](app-insights-powershell.md).</span></span>
>
>

## <a name="one-time-setup"></a><span data-ttu-id="3908b-107">Tek seferlik Kurulumu</span><span class="sxs-lookup"><span data-stu-id="3908b-107">One-time setup</span></span>
<span data-ttu-id="3908b-108">Önce Azure aboneliğinizle PowerShell kullanmadıysanız:</span><span class="sxs-lookup"><span data-stu-id="3908b-108">If you haven't used PowerShell with your Azure subscription before:</span></span>

<span data-ttu-id="3908b-109">Hello Azure Powershell modülü toorun hello betikleri istediğiniz hello makineye yükleyin.</span><span class="sxs-lookup"><span data-stu-id="3908b-109">Install hello Azure Powershell module on hello machine where you want toorun hello scripts.</span></span>

* <span data-ttu-id="3908b-110">Yükleme [Microsoft Web Platformu Yükleyicisi (v5 veya üzeri)](http://www.microsoft.com/web/downloads/platform.aspx).</span><span class="sxs-lookup"><span data-stu-id="3908b-110">Install [Microsoft Web Platform Installer (v5 or higher)](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
* <span data-ttu-id="3908b-111">Microsoft Azure Powershell tooinstall kullanın</span><span class="sxs-lookup"><span data-stu-id="3908b-111">Use it tooinstall Microsoft Azure Powershell</span></span>

## <a name="connect-tooazure"></a><span data-ttu-id="3908b-112">TooAzure Bağlan</span><span class="sxs-lookup"><span data-stu-id="3908b-112">Connect tooAzure</span></span>
<span data-ttu-id="3908b-113">Azure PowerShell'i başlatın ve [tooyour abonelik bağlanmak](/powershell/azure/overview):</span><span class="sxs-lookup"><span data-stu-id="3908b-113">Start Azure PowerShell and [connect tooyour subscription](/powershell/azure/overview):</span></span>

```PowerShell

    Add-AzureAccount
```


## <a name="get-alerts"></a><span data-ttu-id="3908b-114">Uyarıları alma</span><span class="sxs-lookup"><span data-stu-id="3908b-114">Get alerts</span></span>
    Get-AzureAlertRmRule -ResourceGroup "Fabrikam" [-Name "My rule"] [-DetailedOutput]

## <a name="add-alert"></a><span data-ttu-id="3908b-115">Uyarı ekleme</span><span class="sxs-lookup"><span data-stu-id="3908b-115">Add alert</span></span>
    Add-AlertRule  -Name "{ALERT NAME}" -Description "{TEXT}" `
     -ResourceGroup "{GROUP NAME}" `
     -ResourceId "/subscriptions/{SUBSCRIPTION ID}/resourcegroups/{GROUP NAME}/providers/microsoft.insights/components/{APP RESOURCE NAME}" `
     -MetricName "{METRIC NAME}" `
     -Operator GreaterThan  `
     -Threshold {NUMBER}   `
     -WindowSize {HH:MM:SS}  `
     [-SendEmailToServiceOwners] `
     [-CustomEmails "EMAIL1@X.COM","EMAIL2@Y.COM" ] `
     -Location "East US" // must be East US at present
     -RuleType Metric



## <a name="example-1"></a><span data-ttu-id="3908b-116">Örnek 1</span><span class="sxs-lookup"><span data-stu-id="3908b-116">Example 1</span></span>
<span data-ttu-id="3908b-117">Merhaba sunucunun yanıt tooHTTP isteği, üzerinde 5 dakika ortalaması 1 saniyeden daha yavaş ise bana e-posta.</span><span class="sxs-lookup"><span data-stu-id="3908b-117">Email me if hello server's response tooHTTP requests, averaged over 5 minutes, is slower than 1 second.</span></span> <span data-ttu-id="3908b-118">My Application Insights kaynağı IceCreamWebApp denir ve Fabrikam kaynak grubunda bulunuyor.</span><span class="sxs-lookup"><span data-stu-id="3908b-118">My Application Insights resource is called IceCreamWebApp, and it is in resource group Fabrikam.</span></span> <span data-ttu-id="3908b-119">Hello Azure aboneliği hello sahibi ben.</span><span class="sxs-lookup"><span data-stu-id="3908b-119">I am hello owner of hello Azure subscription.</span></span>

<span data-ttu-id="3908b-120">Merhaba GUID hello abonelik kimliği (değil hello izleme anahtarını hello uygulamasının) olur.</span><span class="sxs-lookup"><span data-stu-id="3908b-120">hello GUID is hello subscription ID (not hello instrumentation key of hello application).</span></span>

    Add-AlertRule -Name "slow responses" `
     -Description "email me if hello server responds slowly" `
     -ResourceGroup "Fabrikam" `
     -ResourceId "/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/Fabrikam/providers/microsoft.insights/components/IceCreamWebApp" `
     -MetricName "request.duration" `
     -Operator GreaterThan `
     -Threshold 1 `
     -WindowSize 00:05:00 `
     -SendEmailToServiceOwners `
     -Location "East US" -RuleType Metric

## <a name="example-2"></a><span data-ttu-id="3908b-121">Örnek 2</span><span class="sxs-lookup"><span data-stu-id="3908b-121">Example 2</span></span>
<span data-ttu-id="3908b-122">Bir uygulama içinde kullanmam sahip [TrackMetric()](app-insights-api-custom-events-metrics.md#trackmetric) tooreport "salesPerHour." adlı bir ölçüm</span><span class="sxs-lookup"><span data-stu-id="3908b-122">I have an application in which I use [TrackMetric()](app-insights-api-custom-events-metrics.md#trackmetric) tooreport a metric named "salesPerHour."</span></span> <span data-ttu-id="3908b-123">"SalesPerHour" üzerinde 24 saat ortalaması 100 düşerse toomy iş arkadaşlarınızı bir e-posta gönderin.</span><span class="sxs-lookup"><span data-stu-id="3908b-123">Send an email toomy colleagues if "salesPerHour" drops below 100, averaged over 24 hours.</span></span>

    Add-AlertRule -Name "poor sales" `
     -Description "slow sales alert" `
     -ResourceGroup "Fabrikam" `
     -ResourceId "/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/Fabrikam/providers/microsoft.insights/components/IceCreamWebApp" `
     -MetricName "salesPerHour" `
     -Operator LessThan `
     -Threshold 100 `
     -WindowSize 24:00:00 `
     -CustomEmails "satish@fabrikam.com","lei@fabrikam.com" `
     -Location "East US" -RuleType Metric

<span data-ttu-id="3908b-124">aynı kural hello ölçüm için kullanılabilir hello bildirilen hello kullanarak [ölçüm parametresi](app-insights-api-custom-events-metrics.md#properties) TrackEvent veya trackPageView gibi başka bir izleme çağrısı.</span><span class="sxs-lookup"><span data-stu-id="3908b-124">hello same rule can be used for hello metric reported by using hello [measurement parameter](app-insights-api-custom-events-metrics.md#properties) of another tracking call such as TrackEvent or trackPageView.</span></span>

## <a name="metric-names"></a><span data-ttu-id="3908b-125">Ölçüm adları</span><span class="sxs-lookup"><span data-stu-id="3908b-125">Metric names</span></span>
| <span data-ttu-id="3908b-126">Ölçüm adı</span><span class="sxs-lookup"><span data-stu-id="3908b-126">Metric name</span></span> | <span data-ttu-id="3908b-127">Ekran adı</span><span class="sxs-lookup"><span data-stu-id="3908b-127">Screen name</span></span> | <span data-ttu-id="3908b-128">Açıklama</span><span class="sxs-lookup"><span data-stu-id="3908b-128">Description</span></span> |
| --- | --- | --- |
| `basicExceptionBrowser.count` |<span data-ttu-id="3908b-129">Tarayıcı özel durumları</span><span class="sxs-lookup"><span data-stu-id="3908b-129">Browser exceptions</span></span> |<span data-ttu-id="3908b-130">Merhaba tarayıcıda oluşturulan Yakalanmayan Özel durumların sayısı.</span><span class="sxs-lookup"><span data-stu-id="3908b-130">Count of uncaught exceptions thrown in hello browser.</span></span> |
| `basicExceptionServer.count` |<span data-ttu-id="3908b-131">Sunucu özel durumları</span><span class="sxs-lookup"><span data-stu-id="3908b-131">Server exceptions</span></span> |<span data-ttu-id="3908b-132">Merhaba uygulama tarafından oluşturulan işlenmemiş özel durum sayısı</span><span class="sxs-lookup"><span data-stu-id="3908b-132">Count of unhandled exceptions thrown by hello app</span></span> |
| `clientPerformance.clientProcess.value` |<span data-ttu-id="3908b-133">İstemci işlem süresi</span><span class="sxs-lookup"><span data-stu-id="3908b-133">Client processing time</span></span> |<span data-ttu-id="3908b-134">Merhaba DOM yüklenene kadar belgeyi son baytını hello alma arasındaki süre.</span><span class="sxs-lookup"><span data-stu-id="3908b-134">Time between receiving hello last byte of a document until hello DOM is loaded.</span></span> <span data-ttu-id="3908b-135">Zaman uyumsuz isteği hala işliyor olabilir.</span><span class="sxs-lookup"><span data-stu-id="3908b-135">Async requests may still be processing.</span></span> |
| `clientPerformance.networkConnection.value` |<span data-ttu-id="3908b-136">Sayfa yükleme ağ bağlantı süresi</span><span class="sxs-lookup"><span data-stu-id="3908b-136">Page load network connect time</span></span> |<span data-ttu-id="3908b-137">Zaman hello tarayıcı tooconnect toohello ağ alır.</span><span class="sxs-lookup"><span data-stu-id="3908b-137">Time hello browser takes tooconnect toohello network.</span></span> <span data-ttu-id="3908b-138">Önbelleğe alınmış 0 olabilir.</span><span class="sxs-lookup"><span data-stu-id="3908b-138">Can be 0 if cached.</span></span> |
| `clientPerformance.receiveRequest.value` |<span data-ttu-id="3908b-139">Alıcı yanıt süresi</span><span class="sxs-lookup"><span data-stu-id="3908b-139">Receiving response time</span></span> |<span data-ttu-id="3908b-140">İstek toostarting tooreceive yanıtı göndermeyi tarayıcı arasındaki süre.</span><span class="sxs-lookup"><span data-stu-id="3908b-140">Time between browser sending request toostarting tooreceive response.</span></span> |
| `clientPerformance.sendRequest.value` |<span data-ttu-id="3908b-141">İstek süresi Gönder</span><span class="sxs-lookup"><span data-stu-id="3908b-141">Send request time</span></span> |<span data-ttu-id="3908b-142">Tarayıcı toosend isteği tarafından harcanan süre.</span><span class="sxs-lookup"><span data-stu-id="3908b-142">Time taken by browser toosend request.</span></span> |
| `clientPerformance.total.value` |<span data-ttu-id="3908b-143">Tarayıcı sayfa yükleme süresi</span><span class="sxs-lookup"><span data-stu-id="3908b-143">Browser page load time</span></span> |<span data-ttu-id="3908b-144">DOM, stil sayfaları, betikler ve görüntüleri yüklenene kadar kullanıcı isteği süresi.</span><span class="sxs-lookup"><span data-stu-id="3908b-144">Time from user request until DOM, stylesheets, scripts and images are loaded.</span></span> |
| `performanceCounter.available_bytes.value` |<span data-ttu-id="3908b-145">Kullanılabilir bellek</span><span class="sxs-lookup"><span data-stu-id="3908b-145">Available memory</span></span> |<span data-ttu-id="3908b-146">Bir işlem veya sistem kullanımı için hemen kullanılabilir fiziksel bellek.</span><span class="sxs-lookup"><span data-stu-id="3908b-146">Physical memory immediately available for a process or for system use.</span></span> |
| `performanceCounter.io_data_bytes_per_sec.value` |<span data-ttu-id="3908b-147">İşlemin g/ç hızı</span><span class="sxs-lookup"><span data-stu-id="3908b-147">Process IO Rate</span></span> |<span data-ttu-id="3908b-148">İkinci okuma ve yazılı toofiles, ağ ve aygıt başına toplam bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="3908b-148">Total bytes per second read and written toofiles, network and devices.</span></span> |
| `performanceCounter.number_of_exceps_thrown_per_sec.value` |<span data-ttu-id="3908b-149">özel durum oranı</span><span class="sxs-lookup"><span data-stu-id="3908b-149">exception rate</span></span> |<span data-ttu-id="3908b-150">Saniye başına oluşturulan özel durumları.</span><span class="sxs-lookup"><span data-stu-id="3908b-150">Exceptions thrown per second.</span></span> |
| `performanceCounter.percentage_processor_time.value` |<span data-ttu-id="3908b-151">İşlem CPU</span><span class="sxs-lookup"><span data-stu-id="3908b-151">Process CPU</span></span> |<span data-ttu-id="3908b-152">Merhaba işlemci tooexecution yönergeleri ile Merhaba uygulamaları işlemi için kullanılan tüm işlem iş parçacıklarının geçen sürenin yüzdesini Hello.</span><span class="sxs-lookup"><span data-stu-id="3908b-152">hello percentage of elapsed time of all process threads used by hello processor tooexecution instructions for hello applications process.</span></span> |
| `performanceCounter.percentage_processor_total.value` |<span data-ttu-id="3908b-153">İşlemci zamanı</span><span class="sxs-lookup"><span data-stu-id="3908b-153">Processor time</span></span> |<span data-ttu-id="3908b-154">Merhaba hello işlemci zamanı yüzdesi, boş olmayan iş parçacıklarında harcadığı.</span><span class="sxs-lookup"><span data-stu-id="3908b-154">hello percentage of time that hello processor spends in non-Idle threads.</span></span> |
| `performanceCounter.process_private_bytes.value` |<span data-ttu-id="3908b-155">İşlem özel bayt sayısı</span><span class="sxs-lookup"><span data-stu-id="3908b-155">Process private bytes</span></span> |<span data-ttu-id="3908b-156">Özel olarak toohello atanan bellek uygulamanın işlemleri izlenen.</span><span class="sxs-lookup"><span data-stu-id="3908b-156">Memory exclusively assigned toohello monitored application's processes.</span></span> |
| `performanceCounter.request_execution_time.value` |<span data-ttu-id="3908b-157">ASP.NET isteği yürütme süresi</span><span class="sxs-lookup"><span data-stu-id="3908b-157">ASP.NET request execution time</span></span> |<span data-ttu-id="3908b-158">Merhaba en son isteği yürütme süresi.</span><span class="sxs-lookup"><span data-stu-id="3908b-158">Execution time of hello most recent request.</span></span> |
| `performanceCounter.requests_in_application_queue.value` |<span data-ttu-id="3908b-159">ASP.NET isteklerini yürütme kuyruğundaki</span><span class="sxs-lookup"><span data-stu-id="3908b-159">ASP.NET requests in execution queue</span></span> |<span data-ttu-id="3908b-160">Merhaba uygulama istek sırası uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="3908b-160">Length of hello application request queue.</span></span> |
| `performanceCounter.requests_per_sec.value` |<span data-ttu-id="3908b-161">ASP.NET isteği hızı</span><span class="sxs-lookup"><span data-stu-id="3908b-161">ASP.NET request rate</span></span> |<span data-ttu-id="3908b-162">ASP.NET tarafından saniye başına toohello uygulama isteklerinin tüm hızı.</span><span class="sxs-lookup"><span data-stu-id="3908b-162">Rate of all requests toohello application per second from ASP.NET.</span></span> |
| `remoteDependencyFailed.durationMetric.count` |<span data-ttu-id="3908b-163">Bağımlılık hataları</span><span class="sxs-lookup"><span data-stu-id="3908b-163">Dependency failures</span></span> |<span data-ttu-id="3908b-164">Merhaba sunucu uygulama tooexternal kaynakları tarafından yapılan başarısız çağrı sayısı.</span><span class="sxs-lookup"><span data-stu-id="3908b-164">Count of failed calls made by hello server application tooexternal resources.</span></span> |
| `request.duration` |<span data-ttu-id="3908b-165">Sunucu yanıt süresi</span><span class="sxs-lookup"><span data-stu-id="3908b-165">Server response time</span></span> |<span data-ttu-id="3908b-166">Bir HTTP isteği alma ve hello yanıtı göndermeyi bitirmeden arasındaki süre.</span><span class="sxs-lookup"><span data-stu-id="3908b-166">Time between receiving an HTTP request and finishing sending hello response.</span></span> |
| `request.rate` |<span data-ttu-id="3908b-167">İstek oranı</span><span class="sxs-lookup"><span data-stu-id="3908b-167">Request rate</span></span> |<span data-ttu-id="3908b-168">Saniye başına tüm istekleri toohello uygulamasının oranı.</span><span class="sxs-lookup"><span data-stu-id="3908b-168">Rate of all requests toohello application per second.</span></span> |
| `requestFailed.count` |<span data-ttu-id="3908b-169">Başarısız istekler</span><span class="sxs-lookup"><span data-stu-id="3908b-169">Failed requests</span></span> |<span data-ttu-id="3908b-170">Bir yanıt kodu ile sonuçlandı sayısı, HTTP isteklerini > = 400</span><span class="sxs-lookup"><span data-stu-id="3908b-170">Count of HTTP requests that resulted in a response code >= 400</span></span> |
| `view.count` |<span data-ttu-id="3908b-171">Sayfa görünümleri</span><span class="sxs-lookup"><span data-stu-id="3908b-171">Page views</span></span> |<span data-ttu-id="3908b-172">Bir web sayfası için istemci kullanıcı isteklerini sayısı.</span><span class="sxs-lookup"><span data-stu-id="3908b-172">Count of client user requests for a web page.</span></span> <span data-ttu-id="3908b-173">Yapay trafiği filtrelenmelidir.</span><span class="sxs-lookup"><span data-stu-id="3908b-173">Synthetic traffic is filtered out.</span></span> |
| <span data-ttu-id="3908b-174">{, özel ölçüm adı}</span><span class="sxs-lookup"><span data-stu-id="3908b-174">{your custom metric name}</span></span> |<span data-ttu-id="3908b-175">{Ölçüm adı}</span><span class="sxs-lookup"><span data-stu-id="3908b-175">{Your metric name}</span></span> |<span data-ttu-id="3908b-176">Ölçüm değeri tarafından bildirilen [TrackMetric](app-insights-api-custom-events-metrics.md#trackmetric) veya hello [izleme çağrı ölçümleri parametresinin](app-insights-api-custom-events-metrics.md#properties).</span><span class="sxs-lookup"><span data-stu-id="3908b-176">Your metric value reported by [TrackMetric](app-insights-api-custom-events-metrics.md#trackmetric) or in hello [measurements parameter of a tracking call](app-insights-api-custom-events-metrics.md#properties).</span></span> |

<span data-ttu-id="3908b-177">Merhaba ölçümleri farklı telemetri modülleri tarafından gönderilir:</span><span class="sxs-lookup"><span data-stu-id="3908b-177">hello metrics are sent by different telemetry modules:</span></span>

| <span data-ttu-id="3908b-178">Ölçüm grubu</span><span class="sxs-lookup"><span data-stu-id="3908b-178">Metric group</span></span> | <span data-ttu-id="3908b-179">Toplayıcı Modülü</span><span class="sxs-lookup"><span data-stu-id="3908b-179">Collector module</span></span> |
| --- | --- |
| <span data-ttu-id="3908b-180">basicExceptionBrowser,</span><span class="sxs-lookup"><span data-stu-id="3908b-180">basicExceptionBrowser,</span></span><br/><span data-ttu-id="3908b-181">clientPerformance,</span><span class="sxs-lookup"><span data-stu-id="3908b-181">clientPerformance,</span></span><br/><span data-ttu-id="3908b-182">görünüm</span><span class="sxs-lookup"><span data-stu-id="3908b-182">view</span></span> |[<span data-ttu-id="3908b-183">Tarayıcı JavaScript</span><span class="sxs-lookup"><span data-stu-id="3908b-183">Browser JavaScript</span></span>](app-insights-javascript.md) |
| <span data-ttu-id="3908b-184">performanceCounter</span><span class="sxs-lookup"><span data-stu-id="3908b-184">performanceCounter</span></span> |[<span data-ttu-id="3908b-185">Performans</span><span class="sxs-lookup"><span data-stu-id="3908b-185">Performance</span></span>](app-insights-configuration-with-applicationinsights-config.md) |
| <span data-ttu-id="3908b-186">remoteDependencyFailed</span><span class="sxs-lookup"><span data-stu-id="3908b-186">remoteDependencyFailed</span></span> |[<span data-ttu-id="3908b-187">Bağımlılık</span><span class="sxs-lookup"><span data-stu-id="3908b-187">Dependency</span></span>](app-insights-configuration-with-applicationinsights-config.md) |
| <span data-ttu-id="3908b-188">isteği</span><span class="sxs-lookup"><span data-stu-id="3908b-188">request,</span></span><br/><span data-ttu-id="3908b-189">requestFailed</span><span class="sxs-lookup"><span data-stu-id="3908b-189">requestFailed</span></span> |[<span data-ttu-id="3908b-190">Sunucu isteği</span><span class="sxs-lookup"><span data-stu-id="3908b-190">Server request</span></span>](app-insights-configuration-with-applicationinsights-config.md) |

## <a name="webhooks"></a><span data-ttu-id="3908b-191">Web kancaları</span><span class="sxs-lookup"><span data-stu-id="3908b-191">Webhooks</span></span>
<span data-ttu-id="3908b-192">Yapabilecekleriniz [yanıt tooan Uyarınız otomatikleştirmek](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="3908b-192">You can [automate your response tooan alert](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span></span> <span data-ttu-id="3908b-193">Bir uyarı ortaya çıktığında azure tercih ettiğiniz bir web adresini çağırır.</span><span class="sxs-lookup"><span data-stu-id="3908b-193">Azure will call a web address of your choice when an alert is raised.</span></span>

## <a name="see-also"></a><span data-ttu-id="3908b-194">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="3908b-194">See also</span></span>
* [<span data-ttu-id="3908b-195">Komut dosyası tooconfigure Application Insights</span><span class="sxs-lookup"><span data-stu-id="3908b-195">Script tooconfigure Application Insights</span></span>](app-insights-powershell-script-create-resource.md)
* [<span data-ttu-id="3908b-196">Application Insights ve web test kaynakları Şablondan Oluştur</span><span class="sxs-lookup"><span data-stu-id="3908b-196">Create Application Insights and web test resources from templates</span></span>](app-insights-powershell.md)
* [<span data-ttu-id="3908b-197">Microsoft Azure tanılama tooApplication Öngörüler Kuplaj otomatikleştirme</span><span class="sxs-lookup"><span data-stu-id="3908b-197">Automate coupling Microsoft Azure Diagnostics tooApplication Insights</span></span>](app-insights-powershell-azure-diagnostics.md)
* [<span data-ttu-id="3908b-198">Yanıt tooan Uyarınız otomatikleştirme</span><span class="sxs-lookup"><span data-stu-id="3908b-198">Automate your response tooan alert</span></span>](../monitoring-and-diagnostics/insights-webhooks-alerts.md)
